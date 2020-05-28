---
title: Eseguire la conversione da BIOS a UEFI
titleSuffix: Configuration Manager
description: Informazioni su come personalizzare una sequenza di attività di distribuzione del sistema operativo per preparare una partizione FAT32 per la transizione a UEFI.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0118dd448520a6f0c21bfeea5f8509bd8e49fd46
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429438"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI

Molte delle nuove funzionalità di sicurezza offerte da Windows 10 richiedono dispositivi abilitati per UEFI. Potrebbe essere che alcuni PC Windows moderni supportino UEFI ma usino un BIOS legacy. Prima, per convertire un dispositivo da BIOS a UEFI, era necessario accedere a ogni dispositivo, ripartire il disco rigido e riconfigurare il firmware.

Con Configuration Manager è possibile automatizzare le azioni seguenti:

- Preparare un disco rigido per eseguire la conversione da BIOS a UEFI
- Eseguire la conversione da BIOS a UEFI come parte del processo di aggiornamento sul posto
- Raccogliere informazioni UEFI come parte dell'inventario hardware

## <a name="hardware-inventory-collects-uefi-information"></a>L'inventario hardware raccoglie le informazioni UEFI

Per determinare se un computer viene avviato in modalità UEFI sono disponibili una classe di inventario hardware (**SMS_Firmware**) e una nuova proprietà (**UEFI**). Quando un computer viene avviato in modalità UEFI, la proprietà **UEFI** è impostata su **TRUE**. Per impostazione predefinita, l'inventario hardware abilita questa classe. Per altre informazioni sull'inventario hardware, vedere [How to configure hardware inventory](../../core/clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Creare una sequenza di attività personalizzata per preparare il disco rigido

È possibile personalizzare una sequenza di attività di distribuzione del sistema operativo usando la variabile **TSUEFIDrive**. Il passaggio **Riavvia computer** prepara una partizione FAT32 nel disco rigido per eseguire la transizione a UEFI. La procedura seguente illustra un esempio su come creare i passaggi della sequenza di attività per eseguire questa azione.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Preparare la partizione FAT32 per la conversione a UEFI

In una sequenza di attività esistente per installare un sistema operativo aggiungere un nuovo gruppo usando la procedura di conversione da BIOS a UEFI.

1. Creare un nuovo gruppo di sequenze di attività dopo i passaggi per acquisire file e impostazioni e prima dei passaggi per installare il sistema operativo. Ad esempio, creare un gruppo dopo il gruppo **Acquisisci file e impostazioni** denominato **BIOS-to-UEFI** (Da BIOS a UEFI).

1. Nella scheda **Opzioni** del nuovo gruppo aggiungere una nuova variabile della sequenza di attività come condizione. Impostare **_SMSTSBootUEFI diverso da True**. Con questa condizione, la sequenza di attività esegue questa procedura solo nei dispositivi BIOS.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Condizione per il gruppo BIOS-to-UEFI (Da BIOS a UEFI)":::

1. Nel nuovo gruppo aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.

1. Nella scheda **Opzioni** aggiungere una variabile della sequenza di attività come condizione. Impostare **_SMSTSInWinPE uguale a False**. Con questa condizione, la sequenza di attività non esegue questo passaggio se il computer è già presente in Windows PE.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Condizione nel passaggio Riavvia computer":::

1. Aggiungere un passaggio per avviare uno strumento OEM per convertire il firmware da BIOS a UEFI. Si tratta generalmente del passaggio **Esegui riga di comando** con il comando per eseguire lo strumento OEM.

1. Aggiungere il passaggio della sequenza di attività **Formato e disco partizione**. In questo passaggio configurare le opzioni seguenti:

    1. Creare la partizione FAT32 per eseguire la conversione a UEFI prima di installare il sistema operativo. Scegliere **GPT** per **Tipo di disco**.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Configurazione del passaggio Formato e disco partizione":::

    1. Accedere alle proprietà della partizione FAT32. Nel campo **Variabile** immettere `TSUEFIDrive`. Quando la sequenza di attività rileva questa variabile, avvia la preparazione per la transizione a UEFI prima di riavviare il computer.

        :::image type="content" source="media/partition-properties.png" alt-text="Configurazione delle proprietà della partizione FAT32":::

    1. Creare una partizione NTFS che la sequenza di attività usa per salvare lo stato e archiviare i file di log.

1. Aggiungere un altro passaggio della sequenza di attività **Riavvia computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.

    > [!TIP]
    > Per impostazione predefinita, le dimensioni della partizione EFI sono pari a 500 MB. In alcuni ambienti l'immagine di avvio è troppo grande per essere archiviata in questa partizione. Per risolvere questo problema, aumentare le dimensioni della partizione EFI. Impostarla ad esempio su 1 GB.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> Eseguire la conversione da BIOS a UEFI durante l'aggiornamento sul posto

Windows 10 include **MBR2GPT**, un semplice strumento di conversione. Questo strumento consente di automatizzare il processo di ripartizione del disco rigido per hardware abilitato per UEFI. È possibile integrare lo strumento di conversione nel processo di aggiornamento sul posto in Windows 10. Combinare questo strumento con la sequenza di attività di aggiornamento e con lo strumento OEM che converte il firmware da BIOS a UEFI.

### <a name="requirements"></a>Requisiti

- Versione supportata di Windows 10
- Computer con supporto per UEFI
- Strumento OEM che converte il firmware del computer da BIOS a UEFI

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Eseguire la conversione da BIOS a UEFI durante una sequenza di attività di aggiornamento sul posto

1. [Creare una sequenza di attività per aggiornare un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Modificare la sequenza di attività. Nel gruppo **Post-elaborazione** apportare le modifiche seguenti:

    1. Aggiungere il passaggio **Esegui riga di comando**. Specificare la riga di comando per lo strumento MBR2GPT. Quando viene eseguito nel sistema operativo completo, configurarlo affinché esegua la conversione del disco da MBR a GPT senza modificare o eliminare dati. In **Riga di comando** immettere il comando seguente: `MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > È anche possibile scegliere di eseguire lo strumento MBR2GPT.EXE in Windows PE anziché nel sistema operativo completo. Aggiungere un passaggio per riavviare il computer in Windows PE prima del passaggio per eseguire lo strumento MBR2GPT.EXE. A questo punto rimuovere l'opzione **/AllowFullOS** dalla riga di comando.

    Per altre informazioni sullo strumento e sulle opzioni disponibili, vedere [MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt).

    1. Aggiungere un passaggio per eseguire lo strumento OEM che converte il firmware da BIOS a UEFI. Si tratta generalmente del passaggio **Esegui riga di comando** con una riga di comando per eseguire lo strumento OEM.

    1. Aggiungere il passaggio **Riavvia computer** e selezionare **Il sistema operativo predefinito attualmente installato**.

1. Distribuire la sequenza di attività.
