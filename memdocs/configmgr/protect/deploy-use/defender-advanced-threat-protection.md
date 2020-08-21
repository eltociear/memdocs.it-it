---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Informazioni su come gestire e monitorare Microsoft Defender Advanced Threat Protection, un nuovo servizio che consente alle organizzazioni di rispondere agli attacchi avanzati.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5feaf05a6829d902b1d8dcbe57722dfce410de6f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693540"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Si applica a: Configuration Manager (Current Branch)*

Endpoint Protection consente di gestire e monitorare [Microsoft Defender Advanced Threat Protection (ATP)](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (in precedenza noto come Windows Defender ATP). Microsoft Defender ATP consente alle aziende di rilevare e analizzare attacchi avanzati alle loro reti e di reagire in modo efficace. I criteri di Configuration Manager possono essere utili per l'onboarding e il monitoraggio dei client Windows 10.

Microsoft Defender ATP è un servizio disponibile in [Microsoft Defender Security Center](https://securitycenter.windows.com). Tramite l'aggiunta e la distribuzione di un file di configurazione per il caricamento di client, Configuration Manager è in grado di monitorare lo stato di distribuzione e l'integrità dell'agente di Microsoft Defender ATP. Microsoft Defender ATP è supportato nei PC che eseguono il client Configuration Manager o [gestiti da Microsoft Intune](/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Prerequisiti

- Sottoscrizione al servizio online Microsoft Defender Advanced Threat Protection  
- Computer client che eseguono il client Configuration Manager
- Client che usano un sistema operativo elencato nella sezione [Sistemi operativi client supportati](#bkmk_os) riportata di seguito.

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> Sistemi operativi client supportati

In base alla versione di Configuration Manager in esecuzione, è possibile eseguire l'onboarding dei sistemi operativi client seguenti:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager 1910 e versioni precedenti

- Computer cient che eseguono Windows 10, 1607 e versioni successive

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager versione 2002 e successive
<!--5229962-->
A partire da Configuration Manager versione 2002, è possibile eseguire l'onboarding dei sistemi operativi seguenti:

- Windows 8.1
- Windows 10, versione 1607 o successiva
- R2 per Windows Server 2012
- Windows Server 2016
- Windows Server 2016, versione 1803 o successive
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Informazioni sull'onboarding in ATP con Configuration Manager

Sistemi operativi diversi hanno esigenze diverse per l'onboarding in ATP. Windows 8.1 e altri dispositivi del sistema operativo di livello inferiore richiedono i valori **Chiave area di lavoro** e **ID area di lavoro** per l'onboarding. Per i dispositivi di livello superiore, ad esempio Windows Server versione 1803, è necessario il file di configurazione dell'onboarding. Configuration Manager installa anche Microsoft Monitoring Agent (MMA) quando richiesto dai dispositivi di cui viene eseguito l'onboarding, ma non aggiorna automaticamente l'agente.

I sistemi operativi di livello superiore includono:
- Windows 10 versione 1607 e successive
- Windows Server 2016, versione 1803 o successive
- Windows Server 2019

I sistemi operativi di livello inferiore includono:
- Windows 8.1
- R2 per Windows Server 2012
- Windows Server 2016, versione 1709 e precedenti

Quando si esegue l'onboarding dei dispositivi in ATP con Configuration Manager, i criteri ATP vengono distribuiti in una raccolta o in più raccolte di destinazione. In alcuni casi la raccolta di destinazione contiene dispositivi che eseguono un numero qualsiasi di sistemi operativi supportati. Le istruzioni per l'onboarding di questi dispositivi variano a seconda che la destinazione sia una raccolta contenente dispositivi con sistemi operativi di livello superiore, di livello inferiore o entrambi.

- Se la raccolta di destinazione contiene sia dispositivi di livello superiore che di livello inferiore, usare le istruzioni per [eseguire l'onboarding dei dispositivi che eseguono qualsiasi sistema operativo supportato](#bkmk_any_os) (scelta consigliata).
- Se la raccolta contiene solo dispositivi di livello superiore, è possibile usare le [istruzioni per l'onboarding di livello superiore](#bkmk_uplevel).
- Se la raccolta contiene solo dispositivi di livello inferiore, è possibile usare le [istruzioni per l'onboarding di livello inferiore](#bkmk_downlevel).

> [!Warning]
> - Se la raccolta di destinazione contiene dispositivi di livello superiore e si usano le istruzioni per i dispositivi di livello inferiore, non verrà eseguito l'onboarding dei dispositivi di livello superiore.
> - Se la raccolta di destinazione contiene dispositivi di livello inferiore e si usano le istruzioni per i dispositivi di livello superiore, non verrà eseguito l'onboarding dei dispositivi di livello inferiore.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a> Eseguire l'onboarding dei dispositivi con qualsiasi sistema operativo supportato in ATP (scelta consigliata)
 È possibile eseguire l'onboarding in ATP dei dispositivi che eseguono uno qualsiasi dei [sistemi operativi supportati](#bkmk_os), specificando il file di configurazione, il valore **Chiave area di lavoro** e il valore **ID area di lavoro** in Configuration Manager.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Ottenere il file di configurazione, l'ID dell'area di lavoro e la chiave dell'area di lavoro

1. Passare al [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/) ed eseguire l'accesso.
1. Selezionare **Impostazioni** e quindi selezionare **Onboarding** nell'intestazione **Gestione dispositivi**.
1. Per il sistema operativo selezionare **Windows 10**.
1. Scegliere **Microsoft Endpoint Configuration Manager Current Branch e versioni successive** come metodo di distribuzione.
1. Fare clic su **Scarica pacchetto**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Download del file di configurazione per l'onboarding" lightbox="media/5229962-onboarding-configuration.png":::
1. Scaricare il file di archivio compresso (zip) ed estrarre il contenuto.
1. Selezionare **Impostazioni** e quindi selezionare **Onboarding** nell'intestazione **Gestione dispositivi**.
1. Per il sistema operativo selezionare **Windows 7 SP1 e 8.1** oppure **Windows Server 2008 R2 SP1, 2012 R2 e 2016** nell'elenco.
   - I valori **Chiave area di lavoro** e **ID area di lavoro** saranno uguali indipendentemente dalle opzioni scelte.
1. Copiare i valori per **Chiave area di lavoro** e **ID area di lavoro** dalla sezione **Configura connessione**.

   > [!IMPORTANT]
   > Il file di configurazione di Microsoft Defender ATP contiene informazioni riservate che devono essere protette.


### <a name="onboard-the-devices"></a>Eseguire l'onboarding dei dispositivi

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** > **Criteri di Microsoft Defender ATP**.
1. Selezionare **Crea criterio di Microsoft Defender ATP** per aprire la procedura guidata Criteri di Microsoft Defender ATP. 
1. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Onboarding** (Caricamento).
1. **Passare** al file di configurazione estratto dal file ZIP scaricato.
1. Specificare i valori **Chiave area di lavoro** e **ID area di lavoro**, quindi fare clic su **Avanti**.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Creazione guidata criteri di Microsoft Defender ATP" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  
   - **Nessuno**
   - **Tutti i tipi di file**  
1. Esaminare le informazioni di riepilogo e completare la procedura guidata.  
1. Fare clic con il pulsante destro del mouse sul criterio creato e quindi scegliere **Distribuisci** per distribuire i criteri di Microsoft Defender ATP ai client.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a> Eseguire l'onboarding dei dispositivi che eseguono sistemi operativi di livello superiore in ATP

I client di livello superiore richiedono un file di configurazione dell'onboarding per l'onboarding in ATP. I sistemi operativi di livello superiore includono:
- Windows 10 versione 1607 e successive 
- Windows Server 2016, versione 1803 e successive
- Windows Server 2019

Se la raccolta di destinazione contiene sia dispositivi di livello superiore che di livello inferiore, o in caso di dubbi sulla composizione della raccolta, usare le istruzioni per [eseguire l'onboarding dei dispositivi che eseguono qualsiasi sistema operativo supportato](#bkmk_any_os) (scelta consigliata).

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Ottenere un file di configurazione dell'onboarding per i dispositivi di livello superiore

1. Passare al [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/) ed eseguire l'accesso.
1. Selezionare **Impostazioni** e quindi selezionare **Onboarding** nell'intestazione **Gestione dispositivi**.
1. Per il sistema operativo selezionare **Windows 10**.
1. Scegliere **Microsoft Endpoint Configuration Manager Current Branch e versioni successive** come metodo di distribuzione.
1. Fare clic su **Scarica pacchetto**.
1. Scaricare il file di archivio compresso (zip) ed estrarre il contenuto.

> [!IMPORTANT]
> Il file di configurazione di Microsoft Defender ATP contiene informazioni riservate che devono essere protette.


### <a name="onboard-the-up-level-devices"></a>Eseguire l'onboarding dei dispositivi di livello superiore

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** > **Criteri di Microsoft Defender ATP** e selezionare **Crea criterio di Microsoft Defender ATP**. Viene visualizzata la Creazione guidata criteri di Microsoft Defender ATP.  
1. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Onboarding** (Caricamento).
1. **Passare** al file di configurazione estratto dal file ZIP scaricato.
   > [!Note]
   > Per Configuration Manager versione 2002 saranno necessari i valori **Chiave area di lavoro** e **ID area di lavoro** anche se si esegue l'onboarding solo di dispositivi di livello superiore. Per ottenere questi valori, selezionare **Impostazioni** > **Onboarding** > **Windows 7 e 8.1** dal [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188-->
1. Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  
   - **Nessuno**
   - **Tutti i tipi di file**  
1. Esaminare le informazioni di riepilogo e completare la procedura guidata.  
1. Fare clic con il pulsante destro del mouse sul criterio creato e quindi scegliere **Distribuisci** per distribuire i criteri di Microsoft Defender ATP ai client.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a> Caricare i dispositivi che eseguono sistemi operativi di livello inferiore in ATP

I client di livello inferiore richiedono i valori **Chiave area di lavoro** e **ID area di lavoro** per l'onboarding di ATP. I sistemi operativi di livello inferiore includono:
- Windows 8.1
- R2 per Windows Server 2012
- Windows Server 2016, versione 1709 e precedenti

Se la raccolta di destinazione contiene sia dispositivi di livello superiore che di livello inferiore, o in caso di dubbi sulla composizione della raccolta, usare le istruzioni per [eseguire l'onboarding dei dispositivi che eseguono qualsiasi sistema operativo supportato](#bkmk_any_os) (scelta consigliata).

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>Ottenere i valori Chiave area di lavoro e ID area di lavoro per i dispositivi di livello inferiore

1. Passare al [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/) ed eseguire l'accesso.
1. Selezionare **Impostazioni** e quindi selezionare **Onboarding** nell'intestazione **Gestione dispositivi**.
1. Per il sistema operativo selezionare **Windows 7 SP1 e 8.1** oppure **Windows Server 2008 R2 SP1, 2012 R2 e 2016** nell'elenco.
   - I valori **Chiave area di lavoro** e **ID area di lavoro** saranno uguali indipendentemente dalle opzioni scelte.
1. Copiare i valori per **Chiave area di lavoro** e **ID area di lavoro** dalla sezione **Configura connessione**.

### <a name="onboard-the-down-level-devices"></a>Caricare i dispositivi di livello inferiore

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** > **Criteri di Microsoft Defender ATP** e selezionare **Crea criterio di Microsoft Defender ATP**. Viene visualizzata la Creazione guidata criteri di Microsoft Defender ATP.  
1. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Onboarding** (Caricamento).
1. Specificare i valori **Chiave area di lavoro** e **ID area di lavoro**.
   > [!Note]
   > - Per Configuration Manager versione 2002, il file di configurazione sarà necessario anche se si esegue l'onboarding solo di dispositivi di livello inferiore. Per ottenere questi valori, selezionare **Impostazioni** > **Onboarding** > **Windows 10** dal [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188--> 
   > - Il file di configurazione di Microsoft Defender ATP contiene informazioni riservate che devono essere protette.
1. Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  
   - **Nessuno**
   - **Tutti i tipi di file**  
1. Esaminare le informazioni di riepilogo e completare la procedura guidata.  
1. Fare clic con il pulsante destro del mouse sul criterio creato e quindi scegliere **Distribuisci** per distribuire i criteri di Microsoft Defender ATP ai client.


## <a name="monitor"></a>Monitoraggio

1. Nella console di Configuration Manager passare a **Monitoraggio** > **Sicurezza** e quindi selezionare **Microsoft Defender ATP**.  

1. Esaminare il dashboard di Microsoft Defender Advanced Threat Protection.  

    - **Stato di onboarding dell'agente di Microsoft Defender ATP**: numero e percentuale di computer client gestiti idonei con criteri di Microsoft Defender ATP attivi di cui è stato eseguito l'onboarding  

    - **Integrità dell'agente di Microsoft Defender ATP**: percentuale di computer client che inviano informazioni sullo stato per il relativo agente di Microsoft Defender ATP  

        - **Integro**: funziona correttamente  

        - **Inattivo**: nessun dato inviato al servizio durante il periodo di tempo  

        - **Stato agente**: il servizio di sistema per l'agente in Windows non è in esecuzione  

        - **Non caricati**: i criteri sono stati applicati ma l'agente non ha segnalato l'onboarding dei criteri  

## <a name="create-an-offboarding-configuration-file"></a>Creare un file di configurazione di offboarding  

1. Accedere al [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/).
1. Selezionare **Impostazioni** e quindi selezionare **Offboarding** nell'intestazione **Gestione dispositivi**.
1. Selezionare **Windows 10** per il sistema operativo e **Microsoft Endpoint Configuration Manager Current Branch e versioni successive** come metodo di distribuzione.
   - L'uso dell'opzione **Windows 10** garantisce che venga eseguito l'offboading di tutti i dispositivi nella raccolta e che MMA venga disinstallato quando necessario.
1. Scaricare il file di archivio compresso (zip) ed estrarre il contenuto. I file per l'offboarding sono validi per 30 giorni.

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** > **Criteri di Microsoft Defender ATP** e selezionare **Crea criterio di Microsoft Defender ATP**. Viene visualizzata la Creazione guidata criteri di Microsoft Defender ATP.  

1. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Offboarding**.

1. **Passare** al file di configurazione estratto dal file ZIP scaricato.

1. Esaminare le informazioni di riepilogo e completare la procedura guidata.  

Selezionare **Distribuisci** per distribuire i criteri di Microsoft Defender ATP ai client.  

> [!IMPORTANT]
> I file di configurazione di Microsoft Defender ATP contengono informazioni sensibili che devono essere protette.

## <a name="next-steps"></a>Passaggi successivi

- [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Risolvere i problemi di onboarding di Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)