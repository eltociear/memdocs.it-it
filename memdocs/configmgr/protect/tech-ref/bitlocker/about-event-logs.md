---
title: Registri eventi di BitLocker
titleSuffix: Configuration Manager
description: Uso delle informazioni di BitLocker nel registro eventi di Windows per la risoluzione dei problemi
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706029"
---
# <a name="bitlocker-event-logs"></a>Registri eventi di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

L'agente di gestione di BitLocker e i servizi Web usano i registri eventi di Windows per registrare i messaggi. Nel Visualizzatore eventi passare a **Registri applicazioni e servizi**, **Microsoft**, **Windows**. Il canale di log (nodo) varia a seconda del computer e del componente:

- **MBAM**: Agente di gestione di BitLocker in un computer client
- **MBAM-Web**:
  - Servizio di ripristino nel punto di gestione
  - Portale self-service
  - Sito Web di amministrazione e monitoraggio

Per altre informazioni sui messaggi specifici in questi registri, vedere gli articoli seguenti:

- [Registri eventi del client](client-event-logs.md)
- [Registri eventi del server](server-event-logs.md)

Per impostazione predefinita, in ogni nodo verranno visualizzati due canali di log: **Amministratore** e **Operativo**. Per informazioni più dettagliate sulla risoluzione dei problemi, è anche possibile consultare visualizzare i registri [analitici e di debug](#bkmk_debug).

## <a name="log-properties"></a>Proprietà del log

Nel Visualizzatore eventi di Windows selezionare un registro specifico. Ad esempio, **Amministratore**. Accedere al menu **Azione** e selezionare **Proprietà**. Configurare le seguenti impostazioni:

- **Dimensione massima registro (KB)** : per impostazione predefinita, questa impostazione è `1028` (1 MB) per tutti i registri.
- **Quando viene raggiunta la dimensione massima del registro eventi**: per impostazione predefinita, i registri **Amministratore** e **Operativo** sono impostati su **Sovrascrivi eventi se necessario (dal più vecchio)** .

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a> Registri analitici e di debug

È possibile abilitare registri più dettagliati ai fini della risoluzione dei problemi. Nel Visualizzatore eventi passare al menu **Visualizza** e selezionare **Visualizzazione dei registri analitici e di debug**. A questo punto, quando si passa al canale di log, verranno visualizzati due registri aggiuntivi: **Analitico** e **Debug**.

> [!TIP]
> Per impostazione predefinita, questi registri hanno le proprietà seguenti:
>
> - **Dimensione massima registro (KB)** : `1028` (1 MB)
> - **Non sovrascrivere eventi (pulizia manuale del registro)**

## <a name="export-logs-to-text"></a>Esportare i registri in file di testo

In particolare con i [log analitici e di debug](#bkmk_debug), può essere più semplice esaminare le voci di log in un singolo file di testo. Usare i seguenti comandi di PowerShell per esportare le voci del registro eventi in file di testo:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
