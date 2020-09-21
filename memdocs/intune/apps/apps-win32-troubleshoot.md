---
title: Risolvere i problemi relativi alle app Win32 in Microsoft Intune
titleSuffix: ''
description: Informazioni sui metodi più comuni per risolvere i problemi relativi alle app Win32 con Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083914"
---
# <a name="troubleshoot-win32-app-issues"></a>Risolvere i problemi delle app Win32

Quando si risolvono i problemi relativi alle app Win32 usate in Microsoft Intune, è possibile usare diversi metodi. Questo articolo offre informazioni e dettagli sui problemi relativi alle app Win32 per facilitarne la soluzione. Per altre informazioni vedere [Risoluzione dei problemi di installazione delle app Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

> [!NOTE]
> Questa funzionalità di gestione delle app supporta l'architettura del sistema operativo sia a 32 bit che a 64 bit per le applicazioni Windows.

> [!IMPORTANT]
> Quando si distribuiscono app Win32, è consigliabile usare esclusivamente l'approccio con l'[estensione di gestione di Intune](../apps/intune-management-extension.md), in particolare quando si usa un programma di installazione di app Win32 a più file. Se vengono installate sia app Win32 sia app line-of-business durante la registrazione di Autopilot, l'installazione dell'app potrebbe non riuscire. L'estensione di gestione di Intune viene installata automaticamente quando uno script di PowerShell o un'app Win32 viene assegnata all'utente o al dispositivo.

## <a name="app-troubleshooting-details"></a>Informazioni dettagliate per la risoluzione dei problemi delle app

È possibile visualizzare i problemi di installazione, ad esempio quando l'app è stato creata, modificata, assegnata e recapitata a un dispositivo. L'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) offre questi e altri dettagli nel riquadro **Risoluzione dei problemi e supporto tecnico**. Per altre informazioni, vedere [Informazioni dettagliate per la risoluzione dei problemi delle app](troubleshoot-app-install.md#app-troubleshooting-details).

## <a name="troubleshooting-app-issues-by-using-logs"></a>Usare i log per risolvere i problemi relativi alle app

La visualizzazione dei dettagli dei log consente di determinare le cause dei problemi che vengono visualizzati e di risolverli. È possibile scegliere di visualizzare i [log visualizzati in Intune](apps-win32-troubleshoot.md#logs-displayed-in-intune)o i [log visualizzati tramite CMTrace](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace). 

### <a name="logs-displayed-in-intune"></a>Log visualizzati in Intune

Quando si verifica un problema di installazione con un'app Win32, è possibile scegliere l'opzione **Raccogli log** nel riquadro **Dettagli di installazione** per l'app in Intune. Per altri dettagli, vedere [Risoluzione dei problemi di installazione delle app Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-through-cmtrace"></a>Log visualizzati tramite CMTrace

I log dell'agente nel computer client sono in genere in *C:\ProgramData\Microsoft\IntuneManagementExtension\Logs*. È possibile usare *CMTrace.exe* per visualizzare questi file di log. Per altre informazioni, vedere [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Screenshot dei log dell'agente nel computer client.](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> Per consentire la corretta installazione e l'esecuzione delle app line-of-business Win32, le impostazioni antimalware devono escludere l'analisi delle directory seguenti:<p>
> **Nei computer client x64**:<br>
> *C:\Programmi (x86)\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **Nei computer client x86**:<br>
> *C:\Programmi\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> Per altre informazioni, vedere [Suggerimenti per la ricerca di virus per i computer aziendali che eseguono versioni attualmente supportate di Windows](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>Rilevare la versione del file dell'app Win32 con PowerShell

Se si hanno difficoltà nel rilevare la versione del file dell'app Win32, provare a usare o modificare il comando di PowerShell seguente:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

Nel comando di PowerShell precedente sostituire la stringa `<path to binary file>` con il percorso del file dell'app Win32. Di seguito è illustrato un percorso di esempio:

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Sostituire anche la stringa `<file version of successfully detected file>` con la versione del file da rilevare. Di seguito è illustrata una stringa di versione del file di esempio:

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Se è necessario ottenere le informazioni sulla versione dell'app Win32, è possibile usare il comando di PowerShell seguente:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

Nel comando di PowerShell precedente sostituire `<path to binary file>` con il percorso del file.

## <a name="additional-troubleshooting-areas-to-consider"></a>Altre aree della risoluzione dei problemi da tenere in considerazione
- Controllare la destinazione per verificare che l'agente sia installato nel dispositivo. L'app Win32 destinata a un gruppo o a uno script di PowerShell destinato a un gruppo creerà un criterio di installazione dell'agente per un gruppo di sicurezza.
- Controllare la versione del sistema operativo: Windows 10 1607 e versioni successive.  
- Controllare lo SKU di Windows 10. Windows 10 S o le versioni di Windows in esecuzione con la modalità S abilitata non supportano l'installazione MSI.

Per altre informazioni sulla risoluzione dei problemi relativi alle app Win32, vedere [Risolvere i problemi di installazione delle app Win32](troubleshoot-app-install.md#win32-app-installation-troubleshooting). Per informazioni sui tipi di app nei dispositivi ARM64, vedere [Tipi di app supportati nei dispositivi ARM64](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## <a name="next-steps"></a>Passaggi successivi

- [Risolvere i problemi di installazione delle app](troubleshoot-app-install.md)
