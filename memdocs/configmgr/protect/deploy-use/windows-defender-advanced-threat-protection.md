---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Informazioni su come gestire e monitorare Microsoft Defender Advanced Threat Protection, un nuovo servizio che consente alle organizzazioni di rispondere agli attacchi avanzati.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 186751bb8b1768b34573e2b614ce992b58fa9232
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706239"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Si applica a: Configuration Manager (Current Branch)*

Endpoint Protection consente di gestire e monitorare [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (in precedenza noto come Windows Defender ATP). Microsoft Defender ATP consente alle aziende di rilevare e analizzare attacchi avanzati alle loro reti e di reagire in modo efficace. I criteri di Configuration Manager possono essere utili per l'onboarding e il monitoraggio dei client Windows 10.

Microsoft Defender ATP è un servizio disponibile in [Windows Defender Security Center](https://securitycenter.windows.com). Tramite l'aggiunta e la distribuzione di un file di configurazione per il caricamento di client, Configuration Manager è in grado di monitorare lo stato di distribuzione e l'integrità dell'agente di Microsoft Defender ATP. Microsoft Defender ATP è supportato nei PC che eseguono il client Configuration Manager o [gestiti da Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

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
- Windows 7 SP1
- Windows 8.1
- Windows 10, versione 1607 o successiva
- Windows Server 2008 R2 SP1
- R2 per Windows Server 2012
- Windows Server 2016
- Windows Server 2016, versione 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Creare un file di configurazione per l'onboarding

1. Passare al [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/) ed eseguire l'accesso.
1. Selezionare **Gestione computer** in **Impostazioni** e quindi selezionare **Onboarding**.
1. Selezionare i sistemi operativi per l'onboarding dall'elenco.
   - Se si sta eseguendo l'onboarding di Windows 10, Windows Server 1803 e Windows Server 2019:
      1. Selezionare **Configuration Manager (Current Branch) versione 1606** e selezionare **Scarica pacchetto**.
      1. Scaricare il file di archivio compresso (zip) ed estrarre il contenuto.
   - Se si sta eseguendo l'onboarding di un altro sistema operativo Windows: 
      1. Selezionare i sistemi operativi per l'onboarding dall'elenco. Ad esempio, scegliere **Windows 7 e 8.1** oppure **Windows Server 2008 R2 SP1, 2012 R2 e 2016**.
      1. Al termine del processo, copiare i valori per **Chiave dell'area di lavoro** e **ID area di lavoro** dalla sezione **Configura connessione**.

> [!IMPORTANT]
> Il file di configurazione di Microsoft Defender ATP contiene informazioni riservate che devono essere protette.

## <a name="onboard-devices"></a>Eseguire l'onboarding dei dispositivi

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** > **Criteri di Windows Defender ATP** e selezionare **Crea criterio di Windows Defender ATP**. Viene visualizzata la Creazione guidata criteri di Microsoft Defender ATP.  
1. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Onboarding** (Caricamento).
1. Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Microsoft Defender ATP dell'organizzazione.
   - Per **Windows 7 e 8.1** o **Windows Server 2008 R2 SP1, 2012 R2 e 2016**, fornire la **Chiave dell'area di lavoro** e l'**ID dell'area di lavoro**.
1. Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  

   - **Nessuno**

   - **Tutti i tipi di file**  
1. Esaminare le informazioni di riepilogo e completare la procedura guidata.  

Selezionare **Distribuisci** per distribuire i criteri di Microsoft Defender ATP ai client.

## <a name="monitor"></a>Monitoraggio

1. Nella console di Configuration Manager passare a **Monitoraggio** > **Sicurezza** e quindi selezionare **Windows Defender ATP**.  

1. Esaminare il dashboard di Microsoft Defender Advanced Threat Protection.  

    - **Windows Defender Agent Deployment Status** (Stato distribuzione agente Windows Defender): numero e percentuale di computer client gestiti idonei con criteri di Microsoft Defender ATP attivi di cui è stato eseguito l'onboarding  

    - **Integrità dell'agente di Windows Defender ATP**: percentuale di computer client che inviano informazioni sullo stato per il relativo agente di Microsoft Defender ATP  

        - **Integro**: funziona correttamente  

        - **Inattivo**: nessun dato inviato al servizio durante il periodo di tempo  

        - **Stato agente**: il servizio di sistema per l'agente in Windows non è in esecuzione  

        - **Non caricati**: i criteri sono stati applicati ma l'agente non ha segnalato l'onboarding dei criteri  

## <a name="create-an-offboarding-configuration-file"></a>Creare un file di configurazione di offboarding  

1. Accedere al [servizio online Microsoft Defender ATP](https://securitycenter.windows.com/).

1. Selezionare **Gestione computer** in **Impostazioni** e quindi selezionare **Onboarding**.  

1. Selezionare **Configuration Manager (Current Branch) versione 1606** e fare clic su **Endpoint offboarding** (Offboarding endpoint).  

1. Scaricare il file di archivio compresso (zip) ed estrarre il contenuto. I file per l'offboarding sono validi per 30 giorni.

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** > **Criteri di Windows Defender ATP** e selezionare **Crea criterio di Windows Defender ATP**. Viene visualizzata la Creazione guidata criteri di Microsoft Defender ATP.  

1. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Offboarding**.

1. Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Microsoft Defender ATP dell'organizzazione.

1. Esaminare le informazioni di riepilogo e completare la procedura guidata.  

Selezionare **Distribuisci** per distribuire i criteri di Microsoft Defender ATP ai client.  

> [!IMPORTANT]
> I file di configurazione di Microsoft Defender ATP contengono informazioni sensibili che devono essere protette.

## <a name="next-steps"></a>Passaggi successivi

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Risolvere i problemi di onboarding di Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)