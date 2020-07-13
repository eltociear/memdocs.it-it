---
title: Gestire i dispositivi con la sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Informazioni su come gli amministratori della sicurezza possono usare il nodo di sicurezza degli endpoint per visualizzare e gestire i dispositivi in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 55a73806e343ac23525dbd2a28950d46285bf9a3
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088531"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Gestire i dispositivi con la sicurezza degli endpoint in Microsoft Intune

Nel ruolo di amministratore della sicurezza, è possibile usare la vista *Tutti dispositivi* nell'interfaccia di amministrazione di Microsoft Endpoint Manager per rivedere e gestire i dispositivi. La vista mostra un elenco di tutti i dispositivi in Azure Active Directory (Azure AD). Sono inclusi i dispositivi gestiti da Intune, Configuration Manager e in [co-gestione](https://docs.microsoft.com/configmgr/comanage/overview) tra Intune e Configuration Manager. I dispositivi possono trovarsi nel cloud e provenire dall'infrastruttura locale quando sono integrati in Azure AD.

 Per trovare la vista, aprire l'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selezionare **Sicurezza degli endpoint** > **Tutti dispositivi**.

La vista iniziale *Tutti dispositivi* mostra i dispositivi e include le informazioni principali relative a ognuno di essi:

- Modalità di gestione del dispositivo
- Stato di conformità
- Dettagli del sistema operativo
- Data dell'ultima sincronizzazione del dispositivo
- E altre informazioni

![Vista Tutti dispositivi nell'interfaccia di amministrazione](./media/endpoint-security-manage-devices/all-device-view.png)

Quando si visualizzano i dettagli dei dispositivi, è possibile selezionare un dispositivo per avere accesso ad altre informazioni.

## <a name="available-details-by-management-type"></a>Dettagli disponibili per modalità di gestione

Quando si visualizzano i dispositivi nell'interfaccia di amministrazione di Microsoft Endpoint Manager, prendere in considerazione la modalità di gestione del dispositivo. L'origine della modalità di gestione influisce sulle informazioni visualizzate nell'interfaccia di amministrazione e sulle azioni disponibili per gestire il dispositivo.

Prendere in considerazione i campi seguenti:

- **Gestito da**: questa colonna identifica la modalità di gestione del dispositivo. Di seguito sono descritte le opzioni della colonna Gestito da:

  - **MDM**: questi dispositivi sono gestiti da Intune. I dati di conformità vengono raccolti e comunicati da Intune nell'interfaccia di amministrazione.

  - **ConfigMgr**: questi dispositivi vengono visualizzati nell'interfaccia di amministrazione di Microsoft Endpoint Manager quando si usa il *collegamento di tenant* per aggiungere i dispositivi gestiti con Configuration Manager. Per essere gestito, un dispositivo deve eseguire il client di Configuration Manager ed essere:

    - In un gruppo di lavoro (aggiunto ad AAD e non)
    - Aggiunto a un dominio
    - Aggiunto ad AAD ibrido (aggiunto ad AD e AAD)

    Lo stato di conformità dei dispositivi gestiti da Configuration Manager non è visibile nell'interfaccia di amministrazione di Microsoft Endpoint Manager.

    Per altre informazioni, vedere [Abilitare il collegamento di tenant](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions) nella documentazione di Configuration Manager.

  - **MDM/Agente di ConfigMgr**: questi dispositivi sono in co-gestione tra Intune e Configuration Manager.

    Con la co-gestione è possibile [scegliere diversi carichi di lavoro di co-gestione](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) per determinare quali aspetti vengono gestiti da Configuration Manager o da Intune. Queste scelte influiscono sui criteri applicati dal dispositivo e sul modo in cui i dati di conformità vengono comunicati all'interfaccia di amministrazione.

    Ad esempio, è possibile usare Intune per configurare i criteri per antivirus, firewall e crittografia. Questi tipi di criteri sono considerati criteri per *Endpoint Protection*. Per fare in modo che un dispositivo co-gestito usi i criteri di Intune e non i criteri di Configuration Manager, impostare il cursore di co-gestione relativo a Endpoint Protection su *Intune* o *Intune pilota*. Se il cursore è impostato su Configuration Manager, il dispositivo userà i criteri e le impostazioni di Configuration Manager.

  - **Workspace ONE** - Questi dispositivi vengono gestiti dal partner per la conformità dei dispositivi, Workspace ONE. Per altre informazioni, vedere [Partner per la conformità dei dispositivi](../protect/device-compliance-partners.md).

- **Conformità**: la conformità viene valutata in base ai criteri di conformità assegnati al dispositivo. L'origine di questi criteri e le informazioni contenute nella console dipendono dalla modalità di gestione del dispositivo: Intune, Configuration Manager o co-gestione. Affinché i dispositivi co-gestiti possano dichiarare lo stato di conformità, impostare il cursore di co-gestione relativo alla conformità del dispositivo su Intune o Intune pilota.  

  Una volta che lo stato di conformità viene dichiarato all'interfaccia di amministrazione per un dispositivo, è possibile espandere i dettagli per visualizzare altre informazioni. Quando un dispositivo non è conforme, esaminare i dettagli per ottenere informazioni sui criteri non conformi. Tali informazioni possono essere utili per altre analisi e per rendere il dispositivo conforme.

- **Ultima sincronizzazione**: questo campo identifica l'ultima volta in cui il dispositivo ha dichiarato il proprio stato.

## <a name="review-a-devices-policy"></a>Esaminare i criteri dei dispositivi

Quando si visualizza l'elenco dei dispositivi, è possibile selezionare un dispositivo per avere accesso ad altre informazioni aprendo la pagina *Panoramica* del dispositivo.

Dalla pagina Panoramica di un dispositivo è quindi possibile selezionare **Configurazione sicurezza endpoint** per visualizzare i criteri di sicurezza degli endpoint che si applicano a tale dispositivo. I dettagli dei criteri sono disponibili per i dispositivi gestiti da MDM e Intune.

![Vista dei dettagli dei criteri di sicurezza degli endpoint](./media/endpoint-security-manage-devices/view-policy-details.png)

I dispositivi gestiti da Configuration Manager non mostrano dettagli dei criteri. Per visualizzare informazioni aggiuntive su questi dispositivi, usare la console di Configuration Manager.

## <a name="remote-actions-for-devices"></a>Azioni remote per i dispositivi

Le azioni remote sono azioni che possono essere avviate o applicate a un dispositivo dall'interfaccia di amministrazione di Microsoft Endpoint Manager. Quando si visualizzano i dettagli di un dispositivo, è possibile accedere alle azioni remote che si applicano al dispositivo.

Le azioni remote vengono visualizzate nella parte superiore della pagina *Panoramica* dei dispositivi. Le azioni che non possono essere visualizzate a causa di spazio limitato sullo schermo sono disponibili selezionando i puntini di sospensione sul lato destro:

![Vista delle azioni aggiuntive](./media/endpoint-security-manage-devices/view-additional-actions.png)

Le azioni remote disponibili variano a seconda della modalità di gestione del dispositivo:

- **Intune**: sono disponibili tutte le [azioni remote di Intune](../remote-actions/device-management.md) applicabili alla piattaforma del dispositivo.  
- **Configuration Manager**: è possibile usare le azioni seguenti di Configuration Manager:

  - Sincronizzazione dei criteri del computer
  - Sincronizzazione dei criteri utente
  - Ciclo di valutazione app

- **Co-gestione**: è possibile accedere sia alle azioni remote di Intune che alle azioni di Configuration Manager.

Alcune azioni remote di Intune possono contribuire alla protezione dei dispositivi o dei dati che possono trovarsi sul dispositivo. Con le azioni remote è possibile:

- Bloccare un dispositivo
- Ripristinare un dispositivo
- Rimuovere i dati aziendali
- Eseguire l'analisi per la ricerca di malware al di fuori di un'esecuzione pianificata
- Ruotare le chiavi di BitLocker

Le azioni remote seguenti di Intune sono di particolare interesse per l'amministratore della sicurezza e sono un sottoinsieme dell'[elenco completo](../remote-actions/device-inventory.md#view-the-device-details). Non tutte le azioni sono disponibili per tutte le piattaforme del dispositivo. I collegamenti rimandano al contenuto che fornisce dettagli approfonditi su ogni azione.

- [Sincronizzazione del dispositivo](../remote-actions/device-sync.md): consente di sincronizzare immediatamente il dispositivo con Intune. Quando un dispositivo esegue la sincronizzazione, riceve tutte le azioni in sospeso o i criteri assegnati.  

- [Riavvio](../remote-actions/device-restart.md): consente di forzare il riavvio di un dispositivo Windows 10 entro cinque minuti. Il proprietario del dispositivo non viene avvisato automaticamente del riavvio e può perdere il proprio lavoro.

- [Analisi veloce](../configuration/device-restrictions-windows-10.md): consente di eseguire un'analisi veloce del dispositivo con Defender alla ricerca di malware, inviando successivamente i risultati a Intune. Un'analisi veloce esamina i percorsi comuni in cui potrebbe essere presente malware registrato, ad esempio chiavi del Registro di sistema e cartelle di avvio Windows note.

- [Analisi completa](../configuration/device-restrictions-windows-10.md): consente di eseguire un'analisi del dispositivo con Defender alla ricerca di malware, inviando successivamente i risultati a Intune. Un'analisi completa esamina i percorsi comuni in cui potrebbe essere presente malware registrato e analizza anche ogni file e cartella presente nel dispositivo.

- Aggiornamento dell'intelligence della sicurezza di Windows Defender: consente di aggiornare le definizioni malware del dispositivo per Microsoft Defender Antivirus. Questa azione non avvia un'analisi.

- [Rotazione delle chiavi BitLocker](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key): consente di ruotare in modalità remota la chiave di ripristino di BitLocker di un dispositivo che esegue Windows 10 versione 1909 o successiva.

È anche possibile usare **Azioni in blocco del dispositivo** per gestire alcune azioni, ad esempio *Ritira* e *Cancella* per più dispositivi allo stesso tempo. Le [azioni in blocco](../remote-actions/bulk-device-actions.md) sono disponibili nella vista *Tutti dispositivi*. Si seleziona la piattaforma, quindi l'azione e successivamente si specificano fino a 100 dispositivi.

![Selezione delle azioni in blocco](./media/endpoint-security-manage-devices/select-bulk-actions.png)

Le opzioni gestite per i dispositivi non hanno effetto fino a quando il dispositivo non viene sincronizzato con Intune.

## <a name="next-steps"></a>Passaggi successivi

[Gestire la sicurezza degli endpoint in Intune](../protect/endpoint-security.md)