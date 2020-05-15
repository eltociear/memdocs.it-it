---
title: Impostazioni di Criteri di gruppo
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni di Criteri di gruppo e locali in Windows usate da Configuration Manager e Desktop Analytics
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8251e21c7eccb87b764af75e883018bdc894ca37
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268675"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Impostazione di Criteri di gruppo per Desktop Analytics

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra nei dettagli le impostazioni di Criteri di gruppo e locali in Windows usate da Configuration Manager e Desktop Analytics.

Quando Configuration Manager registra i dispositivi in Desktop Analytics, imposta i criteri di Windows per la configurazione del dispositivo. Nella maggior parte dei casi usare solo Configuration Manager per configurare queste impostazioni.

## <a name="windows-settings"></a>Impostazioni di Windows

Configuration Manager imposta i criteri di Windows in una o in entrambe le chiavi del Registro di sistema seguenti:

- Oggetto Criteri di gruppo (**GPO**): `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Preferenza criteri **locali**: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Criteri | Percorso | Si applica a | Valore |
|--------|------|------------|-------|
| **CommercialId** | Locale | Tutte le versioni di Windows | Per consentire la visualizzazione di un dispositivo in Desktop Analytics, configurarlo usando l'ID commerciale dell'organizzazione. |
| **AllowTelemetry**  | GPO (Oggetto Criteri di gruppo) | Windows 10 | Impostare `1` per dati di diagnostica **Base**, `2` per dati di diagnostica **Avanzato** o `3` per dati di diagnostica **Completo**. Per Desktop Analytics sono necessari almeno i dati di diagnostica di base. Microsoft consiglia di usare il livello Avanzata (con limitazioni) con Desktop Analytics. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO (Oggetto Criteri di gruppo) | Windows 10 versione 1803 e successive | Questa impostazione si applica solo quando AllowTelemetry è impostata su `2`. Limita gli eventi dei dati di diagnostica avanzati inviati a Microsoft solo agli eventi richiesti da Desktop Analytics. Per altre informazioni, vedere [Eventi e campi dei dati di diagnostica avanzati di Windows 10 usati da Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO (Oggetto Criteri di gruppo) | Windows 10 versione 1803 e successive | Consentire ai dispositivi di inviare il nome del dispositivo. Il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se non si invia il nome del dispositivo, il dispositivo viene visualizzato in Desktop Analytics come "Sconosciuto". Per altre informazioni, vedere [Nome del dispositivo](enroll-devices.md#device-name). |
| **CommercialDataOptIn** | Locale | Windows 8.1 e versioni precedenti | Desktop Analytics richiede il valore `1`. Per altre informazioni, vedere [Consenso esplicito per dati commerciali in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Entrambi | Windows 8.1 e versioni precedenti | Desktop Analytics richiede il valore `1` per il corretto funzionamento della raccolta dati. |
| **DisableEnterpriseAuthProxy** | GPO (Oggetto Criteri di gruppo) | Tutte le versioni di Windows | Se l'ambiente richiede un proxy autenticato dall'utente con Autenticazione integrata di Windows per l'accesso a Internet, Desktop Analytics richiede il valore `0` per il corretto funzionamento della raccolta dati. Per altre informazioni, vedere [Autenticazione dei server proxy](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> Nella maggior parte dei casi usare solo Configuration Manager per configurare queste impostazioni. Non applicare anche queste impostazioni negli oggetti criteri di gruppo del dominio. Per altre informazioni, vedere [Risoluzione dei conflitti](enroll-devices.md#conflict-resolution).

### <a name="settings-from-upgrade-readiness"></a>Impostazioni di Preparazione aggiornamenti

Windows Analytics imposta anche i criteri seguenti tramite lo script di Preparazione aggiornamenti:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

Se nel dispositivo è stato eseguito lo script di onboarding di Preparazione aggiornamenti, è possibile che queste impostazioni dei criteri siano ancora esistenti. Non usare lo script legacy. Prima di registrare il dispositivo in Desktop Analytics, rimuovere queste impostazioni dei criteri precedenti.

## <a name="group-policy-settings"></a>Impostazioni di Criteri di gruppo

In generale, usare le raccolte di Configuration Manager per le impostazioni e la registrazione di Desktop Analytics. Usare l'appartenenza diretta o le query per includere o escludere i dispositivi dalla raccolta. Per altre informazioni, vedere [Come creare le raccolte](../core/clients/manage/collections/create-collections.md).

Configuration Manager configura l'ID commerciale e le impostazioni dei dati di diagnostica nella raccolta di destinazione. Se è necessario configurare impostazioni dei dati di diagnostica diverse per un gruppo diverso di dispositivi, usare le impostazioni di Criteri di gruppo per eseguire l'override delle impostazioni di Configuration Manager. Ad esempio, è necessario impostare il livello **Avanzata (con limitazioni)** per alcuni dispositivi e **Base** per altri. Alcuni dispositivi potrebbero avere impostazioni diverse per l'[autenticazione per il server proxy](enable-data-sharing.md#proxy-server-authentication).

Le impostazioni di Criteri di gruppo pertinenti si trovano nel percorso seguente: **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Raccolta dati e versioni di anteprima**.

Le impostazioni di Criteri di gruppo modificano solo le impostazioni del Registro di sistema nella chiave seguente: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Quando si usano le impostazioni di Criteri di gruppo per abilitare scenari complessi, prestare particolare attenzione alle impostazioni dei criteri che possono causare conflitti di configurazione. Configuration Manager configura le [impostazioni di Windows](#windows-settings) solo *se il valore non esiste già*. Le impostazioni di Criteri di gruppo hanno la precedenza sulle impostazioni di Configuration Manager, quindi alcune configurazioni di Criteri di gruppo potrebbero causare problemi con Desktop Analytics.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Impostazioni di Criteri di gruppo che potrebbero essere in conflitto con le impostazioni di Configuration Manager per Desktop Analytics

Le impostazioni di Criteri di gruppo elencate nella tabella seguente hanno un rischio più alto di causare conflitti con le impostazioni di Windows che Configuration Manager imposta nei dispositivi registrati in Desktop Analytics:

| Nome visualizzato | Valore del Registro di sistema | Effetti sui dispositivi registrati in Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Configura l'ID commerciale** | CommercialId | Se si imposta questo criterio su un valore diverso, viene eseguito l'override dell'ID commerciale impostato da Configuration Manager. Se l'ID è diverso, i dispositivi configurati potrebbero non essere visualizzati in Desktop Analytics. |
| **Consenti dati di telemetria** | AllowTelemetry | Se si imposta questo criterio su un valore diverso, viene eseguito l'override del livello dei dati di diagnostica globale impostato in Configuration Manager per la raccolta di destinazione. |
| **Limita i dati di diagnostica avanzati al minimo richiesto da Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | Questo criterio dipende dall'impostazione precedente di AllowTelemetry. A seconda del livello impostato in Configuration Manager o con Criteri di gruppo, questo criterio può modificare il livello dei dati di diagnostica nel dispositivo in **Avanzato** o **Avanzata (con limitazioni)** . Questo criterio si applica solo se AllowTelemetry è impostato su `2` (**Avanzato**). |
| **Consenti l'invio del nome dispositivo nei dati di diagnostica di Windows** | AllowDeviceNameInTelemetry | Se si sceglie di inviare i nomi dei dispositivi in Configuration Manager, è possibile eseguire l'override di questa impostazione configurando il criterio su Disabilitato. Quando si disabilita questa impostazione, i nomi dei dispositivi vengono visualizzati come "sconosciuti" in Desktop Analytics. Per altre informazioni, vedere [Nome del dispositivo](enroll-devices.md#device-name). |
| **Configura l'utilizzo del proxy autenticato per il servizio Esperienze utente connesse e telemetria** | DisableEnterpriseAuthProxy | Se si configurano i dispositivi di Configuration Manager affinché usino il proxy autenticato dall'utente (`0`) e si imposta poi questo criterio su **Disabilita utilizzo proxy autenticato** (`1`), il dispositivo invierà i dati di diagnostica nel contesto di sistema anziché nel contesto dell'utente. Se non si configura il dispositivo con un proxy in un contesto di sistema o se il dispositivo non esegue l'autenticazione al proxy, Windows non può inviare i dati di diagnostica a Desktop Analytics. |

> [!NOTE]
> Il criterio legacy **Configura esperienze utente connesse e telemetria** (TelemetryProxy) consente a Windows di inoltrare i dati di diagnostica a un proxy dedicato, invece di usare il proxy utente (WinINET) o il proxy dispositivo (WinHTTP). Alcuni componenti di Windows non supportano questo criterio. Se si usa questo criterio, è possibile che si verifichino problemi di qualità dei dati in Desktop Analytics.

#### <a name="behavior-of-disabled-settings"></a>Comportamento delle impostazioni disabilitate

Se si configurano queste impostazioni di Criteri di gruppo su **Disabilitato**, gli effetti sul comportamento del sistema sono diversi.

- Quando si disabilita il criterio **CommercialId**, Windows rimuove il valore del Registro di sistema. L'impostazione di Configuration Manager per l'ID commerciale, che viene impostata nel percorso del Registro di sistema dei criteri locali, viene quindi applicata al dispositivo.

- Per i criteri che Configuration Manager imposta nello stesso percorso del Registro di sistema di Criteri di gruppo, quando si disabilita l'impostazione in Criteri di gruppo, Windows rimuove il valore del Registro di sistema. Configuration Manager lo imposterà di nuovo al successivo ciclo di elaborazione dei criteri e a quel punto Windows lo rimuoverà al successivo aggiornamento di Criteri di gruppo. Questa modifica costante nella configurazione può causare comportamenti indesiderati con Desktop Analytics.

  - Se si impostano queste impostazioni di Criteri di gruppo su **Non configurato**, Windows rimuove il valore una volta ma non continua a rimuoverlo. Questa configurazione consente a Configuration Manager di applicare i valori come previsto.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Impostazioni di Criteri di gruppo per personalizzare l'esperienza utente

Queste impostazioni di Criteri di gruppo non sono necessarie per Configuration Manager o Desktop Analytics. È possibile definirle in Criteri di gruppo per configurare l'esperienza degli utenti con i dati di diagnostica di Windows.

| Nome visualizzato | Valore del Registro di sistema | Effetti sui dispositivi registrati in Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Configura la notifica per la modifica del consenso esplicito per telemetria** | DisableTelemetryOptInChangeNotification | A partire da Windows 10 versione 1803, Windows invia una notifica agli utenti quando viene modificato il livello dei dati di diagnostica. Usare questo criterio per disabilitare le notifiche. |
| **Configura l'esperienza utente per le impostazioni del consenso esplicito per telemetria** | DisableTelemetryOptInSettingsUx | Quando si configura il livello dei dati di diagnostica, è necessario impostare il limite superiore per il dispositivo. A partire da Windows 10 versione 1803, gli utenti possono impostare un livello inferiore. Usare questo criterio per impedire agli utenti di modificare il livello di diagnostica. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione). |
| **Disabilitare l'eliminazione dei dati di diagnostica** | DisableDeviceDelete | A partire da Windows 10 versione 1809, gli utenti possono eliminare i dati di diagnostica dalla pagina delle impostazioni **Feedback e diagnostica**. Usare questo criterio per evitare l'eliminazione dei dati di diagnostica che Microsoft ha raccolto dal dispositivo. |
| **Disabilita il Visualizzatore dati di diagnostica** | DisableDiagnosticDataViewer | A partire da Windows 10 versione 1809, gli utenti possono abilitare e aprire il Visualizzatore dati di diagnostica dalla pagina delle impostazioni **Feedback e diagnostica**. Usare questo criterio per disabilitare il Visualizzatore dati di diagnostica nelle impostazioni di Windows e impedire che visualizzi i dati di diagnostica che Microsoft ha raccolto dal dispositivo.|
