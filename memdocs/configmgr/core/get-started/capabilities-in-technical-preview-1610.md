---
title: Funzionalità nella Technical Preview 1610
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1610 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6402205ae694d719845492b1af37000a0b9335c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705359"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1610 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*



Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1610. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrare per dimensioni del contenuto nelle regole di distribuzione automatica
È ora possibile filtrare le dimensioni del contenuto per gli aggiornamenti software nelle regole di distribuzione automatica. Ad esempio, è possibile impostare il filtro **Dimensioni contenuto (KB)** su **< 2048** per scaricare solo gli aggiornamenti software inferiori a 2 MB. Questo filtro impedisce che vengano scaricati in automatico gli aggiornamenti software di grandi dimensioni al fine di migliorare il supporto della manutenzione Windows semplificata di livello inferiore quando la larghezza di banda è limitata. Per informazioni dettagliate, vedere [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e manutenzione Windows semplificata su sistemi operativi di livello inferiore).

#### <a name="to-configure-the-content-size-field"></a>Per configurare il campo Dimensioni contenuto
Per configurare il campo **Dimensioni contenuto (KB)** , accedere alla pagina **Aggiornamenti software** nella Creazione guidata delle regole di distribuzione automatica quando si crea un'ADR o accedere alla scheda **Aggiornamenti software** nelle proprietà di un'ADR esistente.

![Campo Dimensione contenuto](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funzionalità migliorate per le finestre di dialogo del software richieste
Quando si riceve il software necessario, dall'impostazione **Posponi e ricorda tra:** è possibile selezionare un'opzione dall'elenco di valori a discesa seguente:
- In seguito: specifica che le notifiche vengono programmate in base alle impostazioni di notifica configurate nelle impostazioni dell'agente client.
- Orario fisso: specifica che la notifica verrà pianificata per una nuova visualizzazione dopo l'ora selezionata. Ad esempio, se un utente seleziona 30 minuti, la notifica verrà visualizzata nuovamente dopo 30 minuti.

![Pagina dell'agente computer nelle impostazioni dell'agente client](media/computeragentsettings.png)

Il tempo di posticipo massimo è sempre basato sui valori di notifica configurati nelle impostazioni dell'agente client su ogni orario presente lungo la cronologia di distribuzione. Ad esempio, se l'impostazione nella pagina dell'agente computer **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)** è configurata per 10 ore e alla scadenza mancano più di 24 ore, all'avvio della finestra di dialogo l'utente visualizzerà un set di opzioni di posticipo mai superiori a 10 ore. Man mano che si avvicina la scadenza, la finestra di dialogo mostra un numero minore di opzioni coerente con le impostazioni dell'agente client pertinente per ogni componente della cronologia di distribuzione.

Per una distribuzione ad alto rischio, ad esempio una sequenza di attività che distribuisce un sistema operativo, l'esperienza di notifica dell'utente finale è ora più invasiva. Ogni volta che l'utente viene informato della necessità di manutenzione critica del software, invece di una notifica temporanea sulla barra delle applicazioni, nel computer dell'utente viene visualizzata una finestra di dialogo simile alla seguente:

![Finestra di dialogo del software richiesto](media/requiredsoftwaredialog.png)


Per altre informazioni:
- [Impostazioni per gestire le distribuzioni ad alto rischio](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Come configurare le impostazioni client](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negare richieste di applicazioni approvate in precedenza

In qualità di amministratore l'utente è ora in grado di negare una richiesta di applicazioni approvate in precedenza. Per installare un'applicazione negata, gli utenti successivi dovranno inviare una nuova richiesta. La negazione non disinstalla l'applicazione, ma impone che qualsiasi nuova richiesta dell'utente per l'applicazione specifica venga riapprovata. In precedenza era possibile negare soltanto richieste di applicazioni non approvate.

#### <a name="try-it-out"></a>Procedura
Per negare la richiesta di un'applicazione approvata:

1. Nella console di Configuration Manager [creare e distribuire un'applicazione](../../apps/deploy-use/create-applications.md) che richiede l'approvazione.
2. In un computer client aprire Software Center e inviare una richiesta per l'applicazione.
3. Nella console di Configuration Manager approvare la richiesta per l'applicazione.
4. Nega la richiesta dell'applicazione approvata: nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Richieste di approvazione** e selezionare la richiesta di applicazione che si vuole negare.  Nella barra multifunzione fare clic su **Nega**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Impedire l'aggiornamento automatico dei client
Tecnichal Preview 1610 presenta una nuova impostazione che consente di impedire che una raccolta di client installi automaticamente le versioni client aggiornate.  Questa funzione si applica sia all'aggiornamento automatico sia ad altri metodi, ad esempio all'aggiornamento basato sull'aggiornamento software, agli script di accesso e ai criteri di gruppo. Questa opzione può essere utile per una raccolta di computer che richiede particolare attenzione durante l'aggiornamento del client. I client che appartengono a una raccolta esclusa ignorano le richieste di aggiornamento del software client.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurare l'esclusione dall'aggiornamento automatico
Per configurare le esclusioni dall'aggiornamento automatico:
1. Nella console di Configuration Manager aprire **Impostazioni gerarchia** in **Amministrazione > Configurazione del sito > Siti** e quindi selezionare la scheda **Aggiornamento client**.
2. Selezionare la casella di controllo **Exclude specified clients from upgrade** (Escludi dall'aggiornamento i client specificati) e **Exclusion collection** (Raccolta di esclusione), quindi selezionare la raccolta da escludere. È possibile selezionare per l'esclusione solo una singola raccolta.
3. Fare clic su **OK** per chiudere e salvare la configurazione. Dopo che i client avranno aggiornato i criteri, i client appartenenti alla raccolta esclusa non installeranno più automaticamente gli aggiornamenti per il software client.

   ![Impostazioni per l'esclusione dall'aggiornamento automatico](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Anche se l'interfaccia utente indica che i client non verranno aggiornati, esistono due metodi che è possibile usare per sostituire queste impostazioni. L'installazione push del client e l'installazione manuale del client consentono di sostituire questa configurazione. Per altre informazioni, vedere la sezione seguente.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Come aggiornare un client in una raccolta esclusa
Se una raccolta è configurata per l'esclusione, i membri di tale raccolta possono aggiornare il software client solo tramite uno dei due metodi che sostituiscono l'esclusione:
- **Installazione push client**: è possibile usare l'installazione push del client per eseguire l'aggiornamento di un client che appartiene a una raccolta esclusa. Questa operazione è consentita in quanto richiesta dall'amministratore e permette di aggiornare i client lasciando invariata l'esclusione dell'intera raccolta.       
- **Installazione client manuale**: è possibile aggiornare manualmente i client che appartengono a una raccolta esclusa usando la seguente opzione della riga di comando con ccmsetup: ***/ignoreskipupgrade***.

  Se si tenta di aggiornare manualmente un client che fa parte della raccolta esclusa senza usare questa opzione, il client non installa il nuovo software client. Per altre informazioni, vedere [Come installare manualmente i client di Configuration Manager](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

Per altre informazioni su questi metodi di installazione del client, vedere [Come distribuire i client nei computer Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Impostazioni di configurazione di Windows Defender

È ora possibile configurare le impostazioni del client di Windows Defender nei computer Windows 10 registrati in Intune usando gli elementi di configurazione nella console di Configuration Manager.

In particolare, è possibile configurare le seguenti impostazioni di Windows Defender:
- Consenti il monitoraggio in tempo reale
- Consenti il monitoraggio del comportamento
- Abilita Network Inspection System
- Analizza tutti i download
- Consenti analisi script
- Monitora l'attività di file e programmi
  - File monitorati
- Giorni di rilevamento del malware risolto
- Consenti l'accesso all'interfaccia utente client
- Pianifica un'analisi del sistema
  - Giorno pianificato
  - Ora pianificata
- Pianifica analisi veloce giornaliera
  - Ora pianificata
- Limita utilizzo CPU durante un'analisi Analizza file di archivio
- Analisi dei messaggi di posta elettronica
- Analizza unità rimovibili
- Scan mapped drives (Analizza unità mappate)
- Scan files opened from net shares (Analizza file aperti da condivisioni di rete)
- Intervallo di aggiornamento della firma
- Consenti protezione cloud
- Richiedi agli utenti l'invio dei campioni
- Rilevamento di applicazioni potenzialmente indesiderate
- Cartelle e file esclusi
- Estensioni di file escluse
- Processi esclusi

> [!NOTE]
> Queste impostazioni possono essere configurate solo nei computer client che eseguono Windows 10 November Update (1511) e versioni successive.

### <a name="try-it-out"></a>Verifica

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Elementi di configurazione** e creare un nuovo **elemento di configurazione**.
2. Immettere un nome, quindi selezionare **Windows 8.1 e Windows 10** in **Impostazioni per dispositivi gestiti senza il client di Configuration Manager** e fare clic su **Avanti**.
3. Verificare che **tutti i dispositivi Windows 10 a 64 bit** e **tutti i dispositivi Windows 10 a 32 bit** siano selezionati nella pagina **Piattaforme supportate**, quindi fare clic su **Avanti**.
4. Selezionare il gruppo di impostazioni **Windows Defender**, quindi fare clic su **Avanti**.
5. Configurare le impostazioni desiderate in questa pagina, quindi fare clic su **Avanti**.
6. Completare la procedura guidata.
7. Aggiungere questo elemento di configurazione a una linea di base di configurazione e distribuire questa linea di base nei computer che eseguono Windows 10 November Update (1511) o versione successiva.

> [!NOTE]
> Ricordarsi di selezionare la casella di controllo **Monitora e aggiorna impostazioni non conformi** quando si distribuisce la linea di base di configurazione.

## <a name="request-policy-sync-from-administrator-console"></a>Richiedere la sincronizzazione dei criteri dalla console di amministrazione

Ora è possibile richiedere una sincronizzazione dei criteri per un dispositivo mobile dalla console di Configuration Manager, senza dover richiedere la sincronizzazione dal dispositivo stesso. Le informazioni sullo stato della richiesta di sincronizzazione sono disponibili nelle visualizzazioni del dispositivo come nuova colonna, denominata **Remote Sync State** (Stato sincronizzazione remota). Lo stato è visualizzato anche nella sezione **Dati di individuazione** della finestra di dialogo **Proprietà** di ogni dispositivo mobile.

### <a name="try-it-out"></a>Verifica

1. Nella console di Configuration Manager console passare ad **Asset e conformità** > **Panoramica** > Dispositivi.
2. Nel menu **Azioni remote dispositivo** selezionare **Send Sync Request** (Invia richiesta di sincronizzazione).

La sincronizzazione può richiedere da 5 a 10 minuti. Tutte le modifiche ai criteri verranno sincronizzate nel dispositivo. È possibile rilevare lo stato della richiesta di sincronizzazione nella colonna **Remote Sync State** (Stato sincronizzazione remota) nella visualizzazione **Dispositivi** o nella finestra di dialogo **Proprietà** del dispositivo.

## <a name="additional-security-role-support"></a>Supporto di ruoli di sicurezza aggiuntivi

Oltre al ruolo Amministratore completo, anche i ruoli di sicurezza predefiniti seguenti hanno ora accesso completo agli elementi nel nodo **Tutti i dispositivi di proprietà dell'azienda**, inclusi i **dispositivi predichiarati**, i **profili di registrazione iOS** e i **profili di registrazione Windows**:
- **Gestione asset**
- **Gestione accesso risorse aziendali**

A queste aree della console di Configuration Manager continua a essere concesso l'accesso in sola lettura al ruolo **Analista di sola lettura**.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Accesso condizionale per profili VPN di Windows 10

È ora possibile richiedere la conformità dei dispositivi Windows 10 registrati in Azure Active Directory per poter ottenere l'accesso alla rete VPN tramite i profili VPM di Windows 10 creati nella console di Configuration Manager. Per disporre di questa funzionalità, selezionare la casella di controllo **Abilita l'accesso condizionale per questa connessione VPN** nella pagina **Metodo di autenticazione** della procedura di creazione guidata del profilo VPN e nelle proprietà dei profili VPN di Windows 10. Se si abilita l'accesso condizionale per il profilo, è anche possibile specificare un certificato separato per l'autenticazione Single Sign-On.

## <a name="see-also"></a>Vedere anche
[Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md)
