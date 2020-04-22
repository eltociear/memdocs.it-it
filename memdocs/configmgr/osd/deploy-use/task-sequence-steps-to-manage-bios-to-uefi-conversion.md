---
title: Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI
titleSuffix: Configuration Manager
description: Informazioni su come personalizzare una sequenza di attività di distribuzione del sistema operativo per preparare una partizione FAT32 per la transizione a UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 09f844fc99d1cd5ea3c612f4747ce6a216f235ca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703389"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI
Molte delle nuove funzionalità di sicurezza offerte da Windows 10 richiedono dispositivi abilitati per UEFI. Alcuni PC Windows moderni supportano UEFI, ma usano un BIOS legacy. Per convertire un dispositivo da BIOS a UEFI, è necessario in genere accedere a ogni PC, ripartire il disco rigido e riconfigurare il firmware. Usando le sequenze di attività disponibili in Configuration Manager, è possibile preparare un disco rigido per la conversione da BIOS a UEFI, eseguire la conversione nell'ambito del processo di aggiornamento sul posto e raccogliere informazioni su UEFI nell'ambito dell'inventario hardware.

## <a name="hardware-inventory-collects-uefi-information"></a>L'inventario hardware raccoglie le informazioni UEFI
A partire dalla versione 1702, sono disponibili una nuova classe di inventario hardware (**SMS_Firmware**) e una nuova proprietà (**UEFI**) per determinare se un computer viene avviato in modalità UEFI. Quando un computer viene avviato in modalità UEFI, la proprietà **UEFI** è impostata su **TRUE**. L'impostazione è abilitata nell'inventario hardware per impostazione predefinita. Per altre informazioni sull'inventario hardware, vedere [How to configure hardware inventory](../../core/clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Creare una sequenza di attività personalizzata per preparare il disco rigido per la conversione da BIOS a UEFI
A partire da Configuration Manager versione 1610 è possibile personalizzare una sequenza di attività di distribuzione del sistema operativo con una nuova variabile, TSUEFIDrive, in modo che il passaggio **Riavvia computer** prepari una partizione FAT32 sul disco rigido per la transizione a UEFI. La procedura seguente fornisce un esempio sulle modalità di creazione dei passaggi della sequenza di attività per preparare il disco rigido alla conversione da BIOS a UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Per preparare la partizione FAT32 alla conversione a UEFI:
In una sequenza di attività esistente per installare un sistema operativo si aggiungerà un nuovo gruppo usando la procedura di conversione da BIOS a UEFI.

1. Creare un nuovo gruppo di sequenze di attività dopo aver eseguito la proceduta per acquisire file e impostazioni e prima della procedura di installazione del sistema operativo. Ad esempio, creare un gruppo dopo il gruppo **Acquisisci file e impostazioni** denominato **BIOS-to-UEFI** (Da BIOS a UEFI).
2. Nella scheda **Opzioni** del nuovo gruppo aggiungere una nuova variabile della sequenza di attività come condizione in cui **_SMSTSBootUEFI** sia **diverso** da **true**. Questa operazione blocca l'esecuzione dei passaggi nel gruppo quando il computer è già in modalità UEFI.

   ![Gruppo BIOS-to-UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Nel nuovo gruppo aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.  
4. Nella scheda **Opzioni** aggiungere una variabile della sequenza attività come condizione in cui **_SMSTSInWinPE sia uguale a false** Questa operazione blocca l'esecuzione di questo passaggio se il computer è già in Windows PE.

   ![Passaggio Riavvia il computer](../../core/get-started/media/restart-in-windows-pe.png)
5. Aggiungere un passaggio per avviare lo strumento OEM che convertirà il firmware da BIOS a UEFI. Si tratta in genere di un passaggio della sequenza di attività **Esegui riga di comando** con una riga di comando per avviare lo strumento OEM.
6. Aggiungere il passaggio della sequenza attività Formato e disco partizione che partiziona e formatta il disco rigido. Nel passaggio, eseguire le operazioni seguenti:
   1. Creare la partizione FAT32 che verrà convertita in UEFI prima di installare il sistema operativo. Scegliere **GPT** per **Tipo disco**.
    ![Passaggio Formato e disco partizione](../media/format-and-partition-disk.png)
   2. Accedere alle proprietà della partizione FAT32. Immettere **TSUEFIDrive** nel campo **Variabile**. Quando la sequenza di attività rileva questa variabile, si avvia la preparazione per la transizione di UEFI prima di riavviare il computer.
    ![Proprietà della partizione](../../core/get-started/media/partition-properties.png)
   3. Creare una partizione NTFS che il motore della sequenza di attività usa per il salvataggio dello stato e per archiviare i file di log.
7. Aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversione da BIOS a UEFI durante un aggiornamento sul posto
Windows 10 Creators Update introduce un semplice strumento di conversione che automatizza il processo di ripartizione del disco rigido per l'hardware abilitato per UEFI e integra lo strumento di conversione nel processo di aggiornamento sul posto da Windows 7 a Windows 10. Quando si usa questo strumento in combinazione con la sequenza di attività di aggiornamento del sistema operativo e con lo strumento OEM che converte il firmware da BIOS a UEFI, è possibile convertire i computer da BIOS a UEFI durante un aggiornamento sul posto a Windows 10 Creators Update.

**Requisiti**:
- Windows 10 Creators Update
- Computer con supporto per UEFI
- Strumento OEM che converte il firmware del computer da BIOS a UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Per eseguire la conversione da BIOS a UEFI durante un aggiornamento sul posto
1. Creare una sequenza di attività di aggiornamento del sistema operativo per eseguire un aggiornamento sul posto a Windows 10 Creators Update.
2. Modificare la sequenza di attività. Nel **gruppo Post-elaborazione** aggiungere i passaggi della sequenza di attività elencati di seguito.
   1. Da Generale aggiungere un passaggio **Esegui riga di comando**. Verrà aggiunta la riga di comando per lo strumento MBR2GPT che consente di convertire un disco da MBR a GPT senza modificare o eliminare dati dal disco. Nella riga di comando digitare quanto segue: **MBR2GPT /convert /disk:0 /AllowFullOS**. È possibile anche scegliere di eseguire lo strumento MBR2GPT.EXE in Windows PE e non nel sistema operativo completo. A questo scopo, è necessario aggiungere un passaggio per riavviare il computer in WinPE prima del passaggio relativo all'esecuzione dello strumento MBR2GPT.EXE e rimuovere l'opzione /AllowFullOS dalla riga di comando. Per informazioni dettagliate sullo strumento e sulle opzioni disponibili, vedere [MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Aggiungere un passaggio per avviare lo strumento OEM che convertirà il firmware da BIOS a UEFI. Si tratta in genere di un passaggio della sequenza di attività Esegui riga di comando con una riga di comando per avviare lo strumento OEM.
   3. Da Generale aggiungere il passaggio **Riavvia computer**. Per specificare cosa eseguire dopo il riavvio, selezionare **Il sistema operativo predefinito attualmente installato**.
3. Distribuire la sequenza di attività.
