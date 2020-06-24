---
title: Aggiornare le funzionalità del BIOS di Windows usando i criteri MDM in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere un profilo dell'interfaccia di configurazione del firmware del dispositivo (DFCI, Device Firmware Configuration Interface) per gestire le impostazioni UEFI, ad esempio CPU, hardware integrato e opzioni di avvio nei dispositivi Windows 10 in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb45550f8c38237bebcc54db5531ab244ab10d84
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531520"
---
# <a name="use-device-firmware-configuration-interface-profiles-on-windows-devices-in-microsoft-intune-public-preview"></a>Usare i profili dell'interfaccia di configurazione del firmware del dispositivo nei dispositivi Windows in Microsoft Intune (anteprima pubblica)

Quando si usa Intune per gestire i dispositivi Autopilot, è possibile gestire le impostazioni UEFI (BIOS) dopo la registrazione dei dispositivi tramite l'interfaccia DFCI (Device Firmware Configuration Interface). Per una panoramica di vantaggi, scenari e prerequisiti, vedere [Overview of DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/) (Panoramica di PFCI).

DFCI [abilita Windows](https://docs.microsoft.com/windows/client-management/mdm/uefi-csp) per il passaggio dei comandi di gestione da Intune a UEFI (Unified Extensible Firmware Interface).

In Intune è possibile usare questa funzionalità per controllare le impostazioni del BIOS. In genere, il firmware è più resiliente agli attacchi dannosi. Limita il controllo degli utenti finali sul BIOS: una condizione utile in una situazione compromessa.

Ad esempio, si supponga di usare dispositivi Windows 10 in un ambiente protetto e di voler disabilitare la fotocamera. È possibile disabilitare la fotocamera a livello di firmware e in questo caso non è rilevante quello che fa l'utente finale. Se si reinstalla il sistema operativo o si cancella il computer, la fotocamera non verrà riattivata. Sempre a titolo di esempio, si supponga di bloccare le opzioni di avvio per impedire agli utenti di avviare un altro sistema operativo o una versione precedente di Windows che non ha le stesse funzionalità di sicurezza.

Quando si reinstalla una versione precedente di Windows, si installa un sistema operativo separato o si formatta il disco rigido, non è possibile ignorare la gestione DFCI. Questa funzionalità può impedire al malware di comunicare con i processi del sistema operativo, inclusi i processi del sistema operativo con privilegi elevati. La catena di certificati di DFCI usa la crittografia a chiave pubblica e non dipende dalla sicurezza delle password UEFI (BIOS) locali. Questo livello di sicurezza impedisce agli utenti locali di accedere alle impostazioni gestite dai menu UEFI (BIOS) del dispositivo.

Questa funzionalità si applica a:

- Windows 10 RS5 (1809) e versioni successive su firmware UEFI supportato

## <a name="before-you-begin"></a>Prima di iniziare

- Il produttore del dispositivo deve avere aggiunto DFCI al firmware UEFI durante il processo di produzione o come aggiornamento del firmware da installare. Collaborare con i fornitori dei dispositivi per individuare [i produttori che supportano DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/#oems-that-support-dfci) o la versione del firmware necessaria per l'uso di DFCI.

- Il dispositivo deve essere registrato per Windows Autopilot da un [partner Microsoft Cloud Solution Provider (CSP)](https://partner.microsoft.com/cloud-solution-provider) o registrato direttamente dall'OEM. 

  I dispositivi registrati manualmente per Autopilot, ad esempio [importati da un file CSV](../enrollment/enrollment-autopilot.md#add-devices), non sono autorizzati a usare DFCI. Per impostazione predefinita, la gestione DFCI richiede l'attestazione esterna dell'acquisizione commerciale del dispositivo tramite un OEM o una registrazione di partner Microsoft CSP per Windows Autopilot.

  Dopo la registrazione del dispositivo, il numero di serie viene visualizzato nell'elenco dei dispositivi Windows Autopilot.

  Per altre informazioni su Autopilot, inclusi tutti i requisiti, vedere [Registrare dispositivi Windows in Intune con Windows Autopilot](../enrollment/enrollment-autopilot.md).

## <a name="create-your-azure-ad-security-groups"></a>Creare i gruppi di sicurezza di Azure AD

I profili di distribuzione Autopilot vengono assegnati ai gruppi di sicurezza Azure AD. Assicurarsi di creare gruppi che includano i dispositivi supportati da DFCI. Per i dispositivi DFCI, la maggior parte delle organizzazioni può creare gruppi di dispositivi anziché gruppi di utenti. Prendere in considerazione gli scenari seguenti:

- Il personale del reparto Risorse umane dispone di diversi dispositivi Windows. Per motivi di sicurezza, si vuole che nessuno in questo gruppo usi la fotocamera nei dispositivi. In questo scenario è possibile creare un gruppo di sicurezza per gli utenti del reparto RU, in modo che i criteri vengano applicati agli utenti del gruppo RU, indipendentemente dal tipo di dispositivo.
- Nell'impianto di produzione sono disponibili 10 dispositivi. In tutti i dispositivi si vuole impedire l'avvio da un dispositivo USB. In questo scenario è possibile creare un gruppo di sicurezza per i dispositivi e aggiungere questi 10 dispositivi al gruppo.

Per altre informazioni sulla creazione dei gruppi in Intune, vedere [Aggiungere gruppi per organizzare utenti e dispositivi](../fundamentals/groups-add.md).

## <a name="create-the-profiles"></a>Creare i profili

Per usare DFCI, creare i profili seguenti e assegnarli al gruppo.

### <a name="create-an-autopilot-deployment-profile"></a>Creare un profilo di distribuzione Autopilot

Questo profilo configura e preconfigura i nuovi dispositivi. Il [profilo di distribuzione Autopilot](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile) elenca i passaggi per la creazione del profilo.

### <a name="create-an-enrollment-state-page-profile"></a>Creare un profilo della pagina dello stato di registrazione

Questo profilo assicura che i dispositivi vengano verificati e abilitati per DFCI durante l'installazione di Windows. È consigliabile usare questo profilo per bloccare l'uso del dispositivo fino a quando non vengono installati tutti i profili e tutte le app. Il [profilo della pagina dello stato di registrazione](../enrollment/windows-enrollment-status.md) elenca i passaggi per la creazione del profilo.

### <a name="create-the-dfci-profile"></a>Creare il profilo DFCI

Questo profilo include le impostazioni DFCI configurate.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: scegliere **Windows 10 e versioni successive**.
    - **Profilo**: selezionare **Interfaccia di configurazione del firmware del dispositivo**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo valido, ad esempio, è **Windows: Configurare le impostazioni DFCI nei dispositivi Windows**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** completare le impostazioni seguenti:

    - **Consenti all'utente locale di modificare le impostazioni UEFI**: Le opzioni disponibili sono:
      - **Solo le impostazioni non configurate**: l'utente locale può modificare qualsiasi impostazione *ad eccezione* delle impostazioni esplicitamente impostate su **Abilita** o **Disabilita** da Intune.
      - **Nessuno**: l'utente locale non può modificare le impostazioni UEFI (BIOS), incluse le impostazioni non visualizzate nel profilo DFCI.

    - **CPU e virtualizzazione di I/O**: Le opzioni disponibili sono:
        - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
        - **Attivata**: il BIOS abilita le funzionalità di virtualizzazione di CPU e I/O della piattaforma per l'uso da parte del sistema operativo. Attiva le tecnologie di sicurezza basata sulla virtualizzazione Windows e Device Guard.
    - **Fotocamere**: Le opzioni disponibili sono:
        - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
        - **Attivata**: tutte le fotocamere incorporate gestite direttamente da UEFI (BIOS) vengono abilitate. Le periferiche, come le fotocamere USB, non sono interessate.
        - **Disabilitato**: tutte le fotocamere incorporate gestite direttamente da UEFI (BIOS) vengono disabilitate. Le periferiche, come le fotocamere USB, non sono interessate.
    - **Microfoni e altoparlanti**:  Le opzioni disponibili sono:
        - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
        - **Attivata**: tutti i microfoni e gli altoparlanti gestiti direttamente da UEFI (BIOS) vengono abilitati. Le periferiche, come i dispositivi USB, non sono interessate.
        - **Disabilitato**: tutti i microfoni e gli altoparlanti gestiti direttamente da UEFI (BIOS) vengono disabilitati. Le periferiche, come i dispositivi USB, non sono interessate.
    - **Radio (Bluetooth, Wi-Fi, NFC e così via)** : Le opzioni disponibili sono:
        - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
        - **Attivata**: tutte le radio incorporate gestite direttamente da UEFI (BIOS) vengono abilitate. Le periferiche, come i dispositivi USB, non sono interessate.
        - **Disabilitato**: tutte le radio incorporate gestite direttamente da UEFI (BIOS) vengono disabilitate. Le periferiche, come i dispositivi USB, non sono interessate.

        > [!WARNING]
        > Se si disabilita l'impostazione **Radio**, il dispositivo richiede una connessione di rete cablata. In caso contrario, il dispositivo potrebbe non essere gestibile.

    - **Avvia da supporti di memorizzazione esterni (USB, SD)** : Le opzioni disponibili sono:
        - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
        - **Attivata**: UEFI (BIOS) consente l'avvio da supporti di archiviazione non su disco rigido.
        - **Disabilitato**: UEFI (BIOS) non consente l'avvio da supporti di archiviazione non su disco rigido.
    - **Avvia dalle schede di rete** : Le opzioni disponibili sono:
        - **Non configurata**: Intune non modifica o aggiorna questa impostazione.
        - **Attivata**: UEFI (BIOS) consente l'avvio dalle interfacce di rete predefinite.
        - **Disabilitato**: UEFI (BIOS) non consente l'avvio dalle interfacce di rete predefinite.

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o il gruppo utente che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

Alla successiva sincronizzazione di ogni dispositivo, viene applicato il criterio.

## <a name="assign-the-profiles-and-reboot"></a>Assegnare i profili e riavviare

Assicurarsi di [assegnare](../configuration/device-profile-assign.md) i profili ai gruppi di sicurezza di Azure AD che includono i dispositivi DFCI. Il profilo può essere assegnato quando al momento della creazione o dopo.

Quando il dispositivo esegue Windows Autopilot, mentre è attiva la pagina Stato registrazione DFCI può forzare un riavvio. Il primo riavvio esegue la registrazione di UEFI in Intune. 

Per verificare che il dispositivo sia registrato è possibile riavviarlo nuovamente, ma questa operazione non è obbligatoria. Usare le istruzioni del produttore del dispositivo per aprire il menu UEFI e verificare che UEFI ora è gestito.

Alla successiva sincronizzazione del dispositivo con Intune, Windows riceve le impostazioni DFCI. Riavviare il dispositivo. Il terzo riavvio è necessario perché UEFI riceva le impostazioni DFCI da Windows.

## <a name="update-existing-dfci-settings"></a>Aggiornare le impostazioni di DFCI esistenti

Se lo si desidera, è possibile modificare le impostazioni di DFCI esistenti nei dispositivi in uso. Nel profilo DFCI esistente modificare le impostazioni e salvare le modifiche. Dato che il profilo è già assegnato, le nuove impostazioni DFCI diventano effettive quando:

1. Il dispositivo si sincronizza con il servizio Intune per verificare gli aggiornamenti del profilo. Le sincronizzazioni avvengono in diversi momenti. Per altre informazioni, vedere [quando i dispositivi ottengono aggiornamenti dei criteri, del profilo o delle app](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

2. Per applicare le nuove impostazioni, riavviare il dispositivo [da remoto](../remote-actions/device-restart.md) o localmente.

È anche possibile [segnalare ai dispositivi di eseguire la sincronizzazione](../remote-actions/device-sync.md). Una volta completata la sincronizzazione, [inviare il segnale di riavvio](../remote-actions/device-restart.md).

>[!NOTE]
> L'eliminazione del profilo DFCI o la rimozione di un dispositivo dal gruppo assegnato al profilo non comporta la rimozione delle impostazioni di DFCI o la riabilitazione dei menu UEFI (BIOS). Se si vuole interrompere l'uso di DFCI, aggiornare il profilo DFCI esistente. Per altre informazioni sulle procedure, vedere [Ritiro](#retire) in questo articolo.

## <a name="reuse-retire-or-recover-the-device"></a>Riutilizzare, ritirare o ripristinare il dispositivo

### <a name="reuse"></a>Riutilizzo

Se si prevede di ripristinare Windows per reimpiegare il dispositivo, [cancellare il dispositivo](../remote-actions/devices-wipe.md). **Non** rimuovere il record del dispositivo Autopilot.

Dopo la cancellazione del dispositivo, spostare il dispositivo nel gruppo a cui sono stati assegnati i nuovi profili DFCI e Autopilot. Assicurarsi di riavviare il dispositivo per rieseguire la configurazione di Windows.

### <a name="retire"></a>Ritiro

Quando si è pronti per ritirare il dispositivo e rilasciarlo dalla gestione, aggiornare il profilo DFCI con le impostazioni UEFI (BIOS) desiderate per lo stato di uscita. In genere, è utile abilitare tutte le impostazioni. Ad esempio:

1. Aprire il profilo DFCI (**Dispositivi** > **Profili di configurazione**).
2. Modificare l'impostazione **Consenti all'utente locale di modificare le impostazioni UEFI** impostandola su **Solo le impostazioni non configurate**.
3. Impostare tutte le altre impostazioni su **Non configurata**.
4. Salvare le impostazioni.

Questa procedura sblocca i menu UEFI (BIOS) del dispositivo. I valori rimangono identici a quelli del profilo (**Abilitato** o **Disabilitato**) e non vengono reimpostati su alcun valore del sistema operativo predefinito.

A questo punto si è pronti per la cancellazione del dispositivo. Una volta cancellato il dispositivo, eliminare il record Autopilot. L'eliminazione del record impedisce la ripetizione automatica della registrazione del dispositivo in fase di riavvio.

### <a name="recover"></a>Ripristino

Se si cancella un dispositivo e si elimina il record Autopilot prima di sbloccare i menu UEFI (BIOS), i menu rimangono bloccati. Intune non può inviare aggiornamenti del profilo per sbloccarlo.

Per sbloccare il dispositivo, aprire il menu UEFI (BIOS) e aggiornare la gestione dalla rete. Il ripristino sblocca i menu ma lascia tutte le impostazioni UEFI (BIOS) impostate sui valori del profilo dell'interfaccia di configurazione del firmware del dispositivo di Intune precedente.

## <a name="end-user-impact"></a>Impatto sugli utenti finali

Quando vengono applicati i criteri DFCI, gli utenti locali non possono modificare le impostazioni configurate da DFCI, anche se il menu UEFI (BIOS) è protetto da password. A seconda delle impostazioni configurate, gli utenti finali possono ricevere errori per componenti hardware non trovati o che non possono essere diagnosticati. Assicurarsi di fornire agli utenti finali la documentazione che illustra le opzioni che sono state disabilitate.  

## <a name="next-steps"></a>Passaggi successivi

Dopo l'[assegnazione del profilo](device-profile-assign.md), [monitorarne lo stato](device-profile-monitor.md).
