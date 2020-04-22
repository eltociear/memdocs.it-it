---
title: Creare profili di connessione remota
titleSuffix: Configuration Manager
description: Usare i profili di connessione remota di Configuration Manager per consentire agli utenti di connettersi in modalità remota ai computer aziendali.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c9a06e1b7c14cda02a8029925785c2109ea4204b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692469"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Profili di connessione remota in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare profili di connessione remota di Configuration Manager per consentire agli utenti di connettersi in modalità remota ai computer aziendali. Questi profili consentono di distribuire le impostazioni di connessione Desktop remoto agli utenti nella gerarchia. Gli utenti possono accedere a uno qualsiasi dei propri computer aziendali tramite Desktop remoto con una connessione VPN.  

> [!IMPORTANT]  
> Quando si specificano le impostazioni del profilo di connessione remota con Configuration Manager, il client archivia le impostazioni nei criteri locali di Windows. Queste impostazioni possono sostituire le impostazioni di Desktop remoto configurate con un'altra applicazione. Inoltre, se si usa Criteri di gruppo di Windows per configurare le impostazioni di Desktop remoto, le impostazioni specificate in Criteri di gruppo sostituiranno le impostazioni di Configuration Manager.

Configuration Manager crea un gruppo di sicurezza nei client per la **connessione al PC remoto**. Quando si distribuisce un profilo di connessione remota, il client aggiunge gli utenti primari del computer a questo gruppo. Un amministratore locale può aggiungere o rimuovere manualmente utenti in questo gruppo, ma Configuration Manager aggiorna l'appartenenza alla successiva valutazione della conformità del profilo.

> [!IMPORTANT]  
> Se la relazione di affinità utente-dispositivo tra un utente e un dispositivo viene modificata, Configuration Manager disabilita il profilo di connessione remota e le impostazioni di Windows Firewall per impedire le connessioni al computer.

## <a name="prerequisites"></a>Prerequisiti  

### <a name="external-dependencies"></a>Dipendenze esterne  

- Se si vuole consentire agli utenti di connettersi da Internet, installare e configurare un server Gateway Desktop remoto. Per altre informazioni su come installare e configurare un server Gateway Desktop remoto, vedere [Servizi Desktop remoto - Accedere da qualsiasi luogo](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- Se i client eseguono un firewall basato su host, questo deve consentire il programma mstsc.exe. Quando si configura un profilo di connessione remota, abilitare l'impostazione **Consenti eccezione Windows Firewall per connessioni in domini Windows e in reti private**. Questa impostazione consente a Configuration Manager di configurare automaticamente Windows Firewall.

    > [!TIP]
    > Le impostazioni di Criteri di gruppo per configurare Windows Firewall possono sostituire la configurazione impostata in Configuration Manager. Se si usa Criteri di gruppo per configurare Windows Firewall, assicurarsi che le impostazioni di Criteri di gruppo non blocchino mstsc.exe.

    Se i client eseguono un firewall basato su host diverso, configurare manualmente questa dipendenza del firewall.  

### <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

- Per consentire a un utente di connettersi a un computer aziendale, il computer deve essere un dispositivo primario dell'utente. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- Per gestire i profili di connessione remota, l'account utente deve avere autorizzazioni specifiche in Configuration Manager. Il ruolo predefinito **Gestione impostazioni di conformità** include le autorizzazioni necessarie per gestire questi profili. Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Considerazioni sulla privacy e sulla sicurezza

### <a name="security-considerations"></a>Considerazioni sulla sicurezza  

- Specificare manualmente l'affinità utente dispositivo invece di consentire agli utenti di identificare il dispositivo principale. Non abilitare la configurazione basata sull'utilizzo.

  - Prima di poter distribuire un profilo di connessione remota, è necessario abilitare l'opzione **Consenti a tutti gli utenti primari del computer aziendale di connettersi in remoto**. Con questa configurazione, è necessario specificare sempre manualmente l'affinità utente-dispositivo. Non considerare autorevoli le informazioni raccolte da Configuration Manager dagli utenti o dal dispositivo. Se si distribuisce un profilo e un utente amministratore attendibile non specifica l'affinità utente-dispositivo, gli utenti non autorizzati potrebbero ricevere privilegi elevati ed essere in grado di connettersi in remoto ai computer.

  - Configuration Manager raccoglie informazioni basate sull'utilizzo tramite messaggi di stato, un canale di comunicazione veloce ma non sicuro. Per attenuare questa minaccia, usare la firma Server Message Block (SMB) o Internet Protocol security (IPsec) tra computer client e punto di gestione.

- Limitare i diritti amministrativi locali sul computer del server del sito. Un amministratore locale nel server del sito può aggiungere manualmente membri al gruppo di sicurezza per la **connessione al PC remoto** creato e gestito automaticamente da Configuration Manager. Questa azione può causare un aumento dei privilegi perché i membri ricevono le autorizzazioni di Desktop remoto.

### <a name="privacy-considerations"></a>Considerazioni sulla privacy  

Quando un utente si connette in remoto a un computer aziendale, scarica un file con estensione wsrdp. Questo file contiene il nome del dispositivo e il nome del server Gateway Desktop remoto. Questi valori sono necessari per creare la sessione di Desktop remoto. Il file .wsrdp viene scaricato e salvato automaticamente in locale. Tale file viene sovrascritto alla successiva esecuzione di una sessione di Desktop remoto.  

## <a name="create-a-profile"></a>Creare un profilo

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare **Profili connessione remota**.  

1. Nella scheda **Home** della barra multifunzione selezionare **Crea profilo di connessione remota** nel gruppo **Crea**.  

1. Nella pagina **Generale** della **Creazione guidata profilo connessione remota** specificare un nome e una descrizione facoltativa per il profilo. Entrambi i valori hanno un limite massimo di 256 caratteri.  

1. Nella pagina **Impostazioni profilo** specificare le impostazioni seguenti:  

    - **Nome completo e porta del server Gateway Desktop remoto (facoltativo)** : specificare il nome del server Gateway Desktop remoto da usare per le connessioni. Questo valore deve soddisfare i requisiti seguenti:

        - Il nome del server non può contenere più di 256 caratteri.
        - Il nome può contenere caratteri maiuscoli, minuscoli e numerici.
        - Ad eccezione dei punti (`.`) tra i segmenti e i due punti (`:`) prima della porta, gli unici caratteri speciali consentiti sono il trattino (`–`) e il carattere di sottolineatura (`_`).
        - Configuration Manager non supporta l'utilizzo di un IDN (Internationalized Domain Name) per questo valore.

    - **Consenti connessioni solo da computer che eseguono Desktop remoto con Autenticazione a livello di rete**: abilitata per impostazione predefinita, questa impostazione aggiunge un livello aggiuntivo di sicurezza per la connessione. Per altre informazioni, vedere [Consentire l'accesso a Desktop remoto](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Abilitare le impostazioni di connessione seguenti:

        - **Consenti connessioni remote a computer aziendali**

        - **Consenti a tutti gli utenti primari del computer aziendale di connettersi in remoto**

        - **Consenti eccezione di Windows Firewall per le connessioni nei domini Windows e nelle reti private**

        > [!IMPORTANT]  
        > Tutte e tre le impostazioni devono essere identiche per poter continuare.

        Disabilitare queste impostazioni solo quando si distribuisce un profilo per disattivare le connessioni remote.

1. Completare la procedura guidata.

Il nuovo profilo viene visualizzato nel nodo **Profili connessione remota** dell'area di lavoro **Asset e conformità**.  

## <a name="deploy"></a>Distribuisci

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare **Profili connessione remota**.

1. Nell'elenco **Profili connessione remota** selezionare il profilo che si vuole distribuire. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci** nel gruppo **Distribuzione**.  

1. Nella finestra **Distribuisci profilo connessione remota** specificare le informazioni seguenti:

    - **Raccolta**: individuare e selezionare la raccolta di dispositivi in cui si vuole distribuire il profilo.

    - **Monitora e aggiorna le regole non conformi, se supportato**: abilitare questa impostazione per correggere automaticamente le impostazioni del profilo quando non sono conformi in un dispositivo. Il profilo può essere non conforme se non esiste.

    - **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione**: se si configura una finestra di manutenzione per la raccolta in cui si distribuisce il profilo, abilitare questa opzione per consentire a Configuration Manager di monitorarla e aggiornarla al di fuori della finestra di manutenzione. Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).

    - **Genera un avviso**: abilitare questa opzione per configurare un avviso di conformità.

    - **Specificare la pianificazione per la valutazione della conformità per questa linea di base di configurazione**: specificare una pianificazione semplice o personalizzata in base alla quale il client valuta il profilo.

1. Selezionare **OK** per chiudere la finestra e creare la distribuzione.

### <a name="client-evaluation"></a>Valutazione client

Il client valuta il profilo quando un utente accede.

Se un dispositivo non fa più parte di una raccolta in cui si distribuisce un profilo di connessione remota, Configuration Manager disabilita le impostazioni nel dispositivo. Tuttavia, affinché questo processo venga eseguito correttamente, è necessario aver già distribuito almeno un elemento di configurazione o una linea di base della configurazione contenente un elemento di configurazione dal sito.

### <a name="conflict-resolution"></a>Risoluzione dei conflitti

Non distribuire più di un profilo di connessione remota con impostazioni in conflitto nello stesso dispositivo. Ad esempio, si distribuiscono due profili con impostazioni diverse nella stessa raccolta. È possibile impostare solo una distribuzione del profilo su **Monitora e aggiorna le regole non conformi, se supportato**. Questa distribuzione può sostituire le impostazioni nell'altro profilo. Configuration Manager non supporta questo tipo di distribuzione del profilo di connessione remota.

## <a name="monitor"></a>Monitoraggio

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare **Distribuzioni**. Nell'elenco **Distribuzioni** selezionare la distribuzione del profilo di connessione remota.

È possibile esaminare le informazioni di riepilogo sulla conformità della distribuzione del profilo di connessione remota nella pagina principale. Per visualizzare informazioni più dettagliate, selezionare la distribuzione del profilo. Nella scheda **Home** della barra multifunzione selezionare quindi **Visualizza stato** nel gruppo **Distribuzione**. Questa azione apre la pagina **Stato distribuzione**.  

La pagina **Stato distribuzione** contiene le seguenti schede:  

- **Conforme**: Viene visualizzata la conformità del profilo di connessione remota in base al numero di asset interessati.

    > [!IMPORTANT]  
    > Se non è applicabile, il client non valuta un profilo di connessione remota. Tuttavia, segnala comunque la conformità.

- **Errore**: Viene visualizzato un elenco di tutti gli errori per la distribuzione del profilo di connessione remota selezionato in base al numero di asset interessati.

- **Non conforme**: Viene visualizzato un elenco di tutte le regole non conformi nel profilo di connessione remota in base al numero di asset interessati.

- **Sconosciuto**: viene visualizzato un elenco di tutti i dispositivi non conformi alla distribuzione del profilo di connessione remota selezionata, insieme allo stato del client corrente per i dispositivi.

In qualsiasi scheda aprire una regola per creare un sottonodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità**. Questo sottonodo contiene tutti i dispositivi con lo stato di conformità della scheda selezionata.

Il riquadro **Dettagli asset** visualizza i dispositivi con lo stato di conformità selezionato per questo profilo. Aprire un dispositivo nell'elenco per visualizzare informazioni aggiuntive.

## <a name="reports"></a>Report

Configuration Manager include report predefiniti che è possibile usare per monitorare le informazioni sui profili di connessione remota. Tali report dispongono della categoria report di **Gestione conformità e impostazioni**.  

> [!IMPORTANT]  
> Quando si usano i parametri **Filtro dispositivo** e **Filtro utente** nei report per le impostazioni di conformità, usare il carattere jolly `%`.  

Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).  
