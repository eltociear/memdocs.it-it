---
title: Agente di raccolta log
titleSuffix: Configuration Manager
description: Usare l'agente di raccolta log per risolvere i problemi di Desktop Analytics
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8782913e40bffdcbe5a151fac8821f05b7e7fece
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268573"
---
# <a name="desktop-analytics-log-collector"></a>Agente di raccolta log di Desktop Analytics

A partire da Configuration Manager versione 1906, usare lo strumento **DesktopAnalyticsLogsCollector.ps1** dalla directory di installazione di Configuration Manager per la risoluzione dei problemi di registrazione dei dispositivi di Desktop Analytics. Lo strumento esegue alcuni passaggi di base per la risoluzione dei problemi e raccoglie i log di rilievo in un'unica directory di lavoro. È possibile condividere questo contenuto con il supporto tecnico Microsoft.


## <a name="prerequisites"></a>Prerequisiti

- Un client Desktop Analytics che esegue Windows 10, Windows 8.1 o Windows 7 con Service Pack 1

- Eseguire lo script nel dispositivo come amministratore e scegliere **Esegui come amministratore**.

    > [!Tip]
    > Con questo strumento è possibile usare la funzionalità **Script** di Configuration Manager. Per altre informazioni, vedere [Esempio 5: Distribuire lo script tramite **Script** di Configuration Manager](#bkmk_ex5).

- Per Windows 7 con Service Pack 1, PowerShell versione 4.0 o successiva
    - [.NET Framework versione 4.6 o successiva](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [versione 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) o [versione 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>Utilizzo

Ottenere lo script dal contenuto di installazione di Configuration Manager: `SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parametri

### `-LogPath`

Specifica un percorso locale o UNC per inserire il log e altri file di output.

**Valori**:

- Percorso locale (lunghezza massima = 130), ad esempio: `c:\myfolder`

- Percorso UNC (lunghezza massima = 130), ad esempio: `\\myserver\myfolder`

**Tipo**: Stringa

**Posizione**: 1

**Valore predefinito**: `$Env:SystemDrive\M365AnalyticsLogs` (Quando questo parametro è Null, vuoto o uno spazio vuoto, lo script crea la cartella M365AnalyticsLogs nell'unità di sistema).

### `-LogMode`

Specifica il livello dettagliato dei log.

**Valori**:

- `0`: Registrare i messaggi di script solo nella finestra di comando di PowerShell.

- `1`: Registrare i messaggi di script nel file di log nella cartella di output e nella finestra di comando di PowerShell.

- `2`: Registrare i messaggi di script nel file di log solo nella cartella di output.

**Tipo**: Int16

**Posizione**: 2

**Valore predefinito**: `1` (Registrare i messaggi di script nel file di log e nella finestra di comando di PowerShell).

### `-CollectNetTrace`

Specifica se lo script raccoglie la traccia di rete.

**Valori**:

- `0`: Non abilitare la traccia di rete.

- `1` (qualsiasi valore Integer diverso da zero): Abilitare la traccia di rete e raccogliere i risultati.

**Tipo**: Int16

**Posizione**: 3

**Valore predefinito**: `0` (Non abilitare la traccia di rete)

### `-CollectUTCTrace`

Specifica se lo script raccoglie la traccia UTC di Windows ed esegue la diagnosi di connettività.

**Valori**:

- `0`: Non abilitare la traccia UTC o eseguire la diagnosi di connettività.

- `1` (qualsiasi valore Integer diverso da zero): Abilitare la traccia UTC, eseguire la diagnosi di connettività e raccogliere i risultati.

**Tipo**: Int16

**Posizione**: 4

**Valore predefinito**: `0` (Non abilitare la traccia UTC o eseguire la diagnosi di connettività)


## <a name="output"></a>Output

Lo script crea una *cartella di lavoro* nel percorso specificato. Ad esempio, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Inserisce tutti i file di output in questa cartella di lavoro.

Se si abilita lo script per la scrittura in un *file di log*, lo script genera un file di log nella cartella di lavoro. Ad esempio, **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt**.

Lo script genera anche altri *file di diagnostica* nella cartella di lavoro. Ad esempio:

- `installedKBs.txt`: un elenco di aggiornamenti di Windows installati nel dispositivo
- `appcompat`: dati di compatibilità delle applicazioni
- `Reg*.txt`: una serie di file con i dati esportati dal Registro di sistema di Windows


## <a name="examples"></a>Esempi

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> Esempio 1: Eseguire lo script tramite la finestra di comando di PowerShell con i valori predefiniti

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> Esempio 2: Eseguire lo script tramite la finestra di comando di PowerShell con i parametri specificati

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> Esempio 3: Eseguire lo script tramite la finestra di comando di PowerShell con i parametri specificati nella posizione

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> Esempio 4: Eseguire lo script tramite la finestra di comando di PowerShell con il parametro specificato e i messaggi dettagliati

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> Esempio 5: Distribuire lo script tramite **Script** di Configuration Manager

Per altre informazioni, vedere [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector.ps1 è firmato digitalmente da Microsoft. Può essere necessario aggiungere il certificato di firma del codice Microsoft come autore attendibile nel dispositivo di destinazione.

1. Aprire le proprietà dello script in Esplora risorse. Passare alla scheda **Firme digitali** e selezionare **Dettagli**.

2. Nella scheda **Generale** selezionare **Visualizza certificato**.

    > [!Note]
    > Per distribuire il certificato tramite altri meccanismi, esportare prima il certificato in un file. Passare alla scheda **Dettagli** e selezionare **Copia su file**.

3. Selezionare **Installa certificato**. Importare il certificato inserendolo nell'archivio **Autori attendibili**.


## <a name="see-also"></a>Vedere anche

- [Risolvere i problemi di Desktop Analytics](troubleshooting.md)

- [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](../apps/deploy-use/create-deploy-scripts.md)
