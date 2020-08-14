---
title: Pre-provisioning di BitLocker in Windows PE
titleSuffix: Configuration Manager
description: L'attività di pre-provisioning di BitLocker in Configuration Manager attiva BitLocker dall'ambiente preinstallazione di Windows prima della distribuzione del sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124944"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Esecuzione del pre-provisioning di BitLocker in Windows PE con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il passaggio della sequenza di attività **pre-provisioning di BitLocker** in Configuration Manager consente di attivare BitLocker dall'ambiente preinstallazione di Windows (Windows PE) prima della distribuzione del sistema operativo. Solo lo spazio su disco usato viene crittografato e pertanto i tempi di crittografia sono molto più veloci. Questa operazione viene eseguita applicando una protezione in chiaro generata in modo casuale al volume formattato e crittografando il volume prima di eseguire il processo di installazione di Windows. La possibilità di eseguire il pre-provisioning di BitLocker è stata introdotta in Windows 8 e Windows Server 2012. Tuttavia, è possibile eseguire il pre-provisioning di BitLocker su un disco rigido e installare Windows 7, purché si segua la procedura specifica. Dopo aver completato l'installazione di Windows 7, è necessario impostare una protezione con chiave di BitLocker in quanto il pannello di controllo Windows 7 BitLocker non supporta BitLocker con una protezione in chiaro. È necessario aggiungere una protezione con chiave utilizzando il passaggio **Attiva BitLocker** oppure utilizzando lo strumento della riga di comando manage-bde.exe.  

 In generale, è necessario effettuare le seguenti operazioni per eseguire correttamente il pre-provisioning di BitLocker in un computer su cui verrà installato Windows 7:  

- Riavviare il computer in Windows PE  

  > [!IMPORTANT]  
  >  Per eseguire il pre-provisioning di BitLocker, è necessario utilizzare un'immagine di avvio con Windows PE 4 o versione successiva. Per altre informazioni sulle versioni Windows PE supportate in Configuration Manager, vedere [Dipendenze esterne a Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Partizionare e formattare il disco rigido  

- Eseguire il pre-provisioning di BitLocker  

- Installare Windows 7 con sistema operativo e impostazioni di rete specifiche  

- Aggiungere una protezione con chiave a BitLocker  

  In Configuration Manager, la modalità consigliata per il pre-provisioning di BitLocker su disco rigido e l'installazione di Windows 7 è di creare una nuova sequenza di attività e selezionare **Installa un pacchetto immagine esistente** nella pagina **Crea nuova sequenza attività** della **Creazione guidata della sequenza attività**. La procedura guidata crea i passaggi della sequenza di attività elencati nella tabella riportata di seguito.  

> [!NOTE]  
>  La sequenza di attività potrebbe richiedere passaggi ulteriori a seconda della configurazione delle impostazioni nella procedura guidata. Ad esempio, si potrebbe avere il passaggio **Acquisisci impostazioni Windows** se è stato selezionato **Impostazioni di Microsoft Windows acquisite** nella pagina **Migrazione stato** della procedura guidata.  

|Passaggio della sequenza di attività|Dettagli|  
|------------------------|-------------|  
|Disattiva BitLocker|Questo passaggio consente di disattivare la crittografia BitLocker, se è attiva. Per altre informazioni, vedere [Disabilitare BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Riavviare il computer in Windows PE|Questo passaggio riavvia il computer in Windows PE eseguendo l'immagine di avvio assegnata alla sequenza di attività. Per eseguire il pre-provisioning di BitLocker, è necessario utilizzare un'immagine di avvio con Windows PE 4 o versione successiva. Per altre informazioni, vedere [Riavviare il computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Disco di partizione 0 - BIOS<br /><br /> Disco di partizione 0 - UEFI|Questi passaggi formattano e partizionano l'unità specificata nel computer di destinazione tramite BIOS o UEFI. La sequenza di attività utilizza UEFI quando rileva che il computer di destinazione è in modalità UEFI. Per altre informazioni, vedere [Formato e partizione del disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Eseguire il pre-provisioning di BitLocker|Questo passaggio attiva BitLocker in un'unità mentre si trova in Windows PE. Solo lo spazio su disco utilizzato è crittografato. Poiché nel passaggio precedente il disco rigido è stato partizionato e formattato, non sono presenti dati e la crittografia si completa molto rapidamente. Per altre informazioni, vedere [Pre-provisioning di BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Applica sistema operativo|Questo passaggio prepara il file di risposta utilizzato per installare il sistema operativo sul computer di destinazione e imposta la variabile della sequenza di attività OSDTargetSystemDrive sulla lettera di unità della partizione che contiene i file del sistema operativo. Il file di risposta e la variabile vengono utilizzati dal passaggio Imposta Windows e ConfigMgr per installare il sistema operativo. Per altre informazioni, vedere [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Applica impostazioni Windows|Questo passaggio consente di aggiungere le impostazioni di Windows al file di risposta. Il file di risposta viene utilizzato dal passaggio Imposta Windows e ConfigMgr per installare il sistema operativo. Per altre informazioni, vedere [Applicare le impostazioni Windows](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Applica impostazioni di rete|Questo passaggio consente di aggiungere le impostazioni di rete al file di risposta. Il file di risposta viene utilizzato dal passaggio Imposta Windows e ConfigMgr per installare il sistema operativo. Per altre informazioni, vedere [il passaggio Applica impostazioni di rete](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Applica driver dispositivo|Questo passaggio associa e installa i driver come parte della distribuzione del sistema operativo. Per altre informazioni, vedere [Applica automaticamente i driver](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Imposta Windows e ConfigMgr|Questo passaggio esegue la transizione da Windows PE al nuovo sistema operativo. Questo passaggio della sequenza di attività è una parte necessaria di qualsiasi distribuzione del sistema operativo. Installa il client di Configuration Manager nel nuovo sistema operativo e prepara la sequenza di attività per continuare l'esecuzione nel nuovo sistema operativo. Per altre informazioni, vedere [Impostare Windows e Configuration Manager](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Attiva BitLocker|Questo passaggio attiva la crittografia BitLocker sul disco rigido e imposta le protezioni con chiave. Poiché per il disco rigido è stato eseguito il pre-provisioning con BitLocker, questo passaggio si completa molto rapidamente. Windows 7 richiede l'aggiunta di una protezione con chiave. Se non si utilizza questo passaggio, è possibile eseguire lo strumento della riga di comando manage-bde.exe per impostare una protezione con chiave. Per altre informazioni, vedere [Abilitare BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
