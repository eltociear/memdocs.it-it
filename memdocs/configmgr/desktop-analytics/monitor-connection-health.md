---
title: Monitorare l'integrità della connessione
titleSuffix: Configuration Manager
description: Informazioni dettagliate su come monitorare l'integrità della connessione e lo stato dei dispositivi per Desktop Analytics in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ecd8b83224cbcbfe367a3b1db160d680952a4407
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700838"
---
# <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare il dashboard **Integrità connessione** in Configuration Manager per eseguire il drill-down delle categorie in base all'integrità del dispositivo. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere il nodo **Manutenzione di Desktop Analytics** e selezionare il dashboard **Integrità connessione**.  

[![Screenshot del dashboard Integrità connessione di Configuration Manager](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

Quando si configura Desktop Analytics per la prima volta, è possibile che i grafici non visualizzino i dati completi. L'invio dei dati di diagnostica al servizio Desktop Analytics da parte dei dispositivi attivi, l'elaborazione dei dati da parte del servizio e la sincronizzazione con il sito di Configuration Manager possono richiedere 2-3 giorni.<!-- 4098037 -->

## <a name="connection-details"></a>Dettagli connessione

Questo riquadro visualizza le informazioni di base seguenti sulla connessione tra Configuration Manager e Desktop Analytics:

- **Nome del tenant**: nome della connessione di Desktop Analytics nel nodo **Servizi di Azure**

- **Raccolta di destinazione**: la stessa *raccolta di destinazione* specificata al momento della connessione di Configuration Manager a Desktop Analytics. Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager connette al servizio Desktop Analytics.

- **Dispositivi interessati**: tutti i dispositivi nella raccolta di destinazione, esclusi i dispositivi:

  - A cui sono state rimosse le autorizzazioni
  - Obsoleti
  - Inattivo
  - Non gestiti
  - Che eseguono versioni LTSC (Long-Term Servicing Channel) di Windows 10
  - Che eseguono Windows Server

    Per altre informazioni su questi stati dei dispositivi, vedere [Informazioni sullo stato del client](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager carica in Desktop Analytics tutti i dispositivi nella raccolta di destinazione ad eccezione dei client a cui sono state rimosse le autorizzazioni e dei client obsoleti.

- **Dispositivi idonei per DA**: differenza tra il numero dei dispositivi di destinazione e il numero dei dispositivi non idonei per Desktop Analytics, ad esempio i dispositivi nella raccolta di destinazione che eseguono Windows Server o Windows 10 LTSC (Long-Term Servicing Channel).

## <a name="last-sync-details"></a>Dettagli dell'ultima sincronizzazione

Questo riquadro mostra quando Configuration Manager esegue la sincronizzazione con il servizio cloud di Desktop Analytics e indica il numero di dispositivi sincronizzati.

- **Dispositivi sincronizzati**: numero di dispositivi idonei che Configuration Manager ha inviato a Desktop Analytics. Il servizio include questi dispositivi nello snapshot visibile.

- **Ultima sincronizzazione del servizio**: stessa indicazione temporale del campo **Ultimo aggiornamento** nel portale Desktop Analytics.

- **Prossima sincronizzazione del servizio**: indica quando è previsto lo snapshot giornaliero successivo in Desktop Analytics.

> [!Note]  
> La prima volta che si registrano dispositivi in Desktop Analytics, il caricamento e l'elaborazione dei dati possono richiedere diversi giorni. Durante questo periodo, il riquadro **Dettagli dell'ultima sincronizzazione** può risultare vuoto.
> Quando si richiede uno snapshot su richiesta, poi, nessuno dei valori in questo riquadro viene aggiornato automaticamente. Per altre informazioni, vedere [Latenza dei dati](troubleshooting.md#data-latency).

Se si ritiene che alcuni dispositivi non vengano visualizzati in Desktop Analytics, verificare che Desktop Analytics li supporti. Per altre informazioni, vedere [Prerequisiti](overview.md#prerequisites).

## <a name="connection-health"></a>Integrità connessione

Il grafico **Integrità connessione** visualizza il numero di dispositivi negli stati di integrità seguenti:  

- [Registrazione completata correttamente](#properly-enrolled): il dispositivo viene visualizzato in Desktop Analytics con un inventario completo
- [Non è possibile eseguire la registrazione](#unable-to-enroll): è presente un problema che causa un blocco e impedisce la registrazione del dispositivo
- [Avviso di configurazione](#configuration-alert): il dispositivo non viene visualizzato in Desktop Analytics o viene visualizzato con un inventario incompleto. Configuration Manager ha anche identificato un problema relativo alla registrazione del dispositivo.
- [In attesa di registrazione](#awaiting-enrollment): Configuration Manager ha configurato il dispositivo, ma questo non è ancora visualizzato in Desktop Analytics
- [Stato in sospeso](#status-pending): Configuration Manager sta ancora configurando il dispositivo o non ha ricevuto dati sufficienti da quest'ultimo per determinarne lo stato
- [Dati mancanti](#missing-data): Configuration Manager ha configurato il dispositivo, ma Desktop Analytics ha solo dati parziali

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Il numero totale di dispositivi in questo grafico deve corrispondere al valore **Dispositivi idonei per DA** nel riquadro Dettagli connessione.

Selezionare la sezione nel grafico in cui eseguire il drill-down in un elenco di dispositivi con lo stato selezionato. Per altre informazioni, vedere [Elenco dei dispositivi](#device-list).

Selezionare nella legenda il nome della categoria per rimuoverla o aggiungerla dal grafico. Questa azione consente di ingrandire il grafico in modo da poter visualizzare le dimensioni relative dei segmenti più piccoli.

### <a name="properly-enrolled"></a>Registrazione completata correttamente

Il dispositivo ha gli attributi seguenti:

- Client di Configuration Manager versione 1902 o successiva  
- Nessun errore di configurazione  
- Desktop Analytics ha ricevuto dati di diagnostica completi da questo dispositivo negli ultimi 28 giorni  
- Desktop Analytics ha un inventario completo della configurazione del dispositivo e delle app installate  

### <a name="unable-to-enroll"></a>Non è possibile eseguire la registrazione

Configuration Manager rileva uno o più problemi che causano un blocco e impediscono la registrazione del dispositivo. Per altre informazioni, vedere l'elenco delle proprietà del dispositivo [Proprietà dei dispositivi Desktop Analytics in Configuration Manager](#bkmk_config-issues).  

La versione del client di Configuration Manager, ad esempio, non corrisponde almeno alla versione 1902 (5.0.8790). Aggiornare il client alla versione più recente. Prendere in considerazione la possibilità di abilitare l'aggiornamento automatico del client per il sito di Configuration Manager. Per altre informazioni, vedere [Aggiornare i client](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

> [!TIP]
> Esiste un problema noto con la patch di sicurezza estesa di aprile 2020 per Windows 7 che impedisce ai dispositivi di segnalare correttamente questo errore. Per altre informazioni, vedere le [note sulla versione](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

A partire dalla versione 2002, è possibile identificare più facilmente i problemi di configurazione del proxy client in due aree:

- **Controlli della connettività degli endpoint**: se i client non riescono a raggiungere un endpoint richiesto, viene visualizzato un avviso di configurazione nel dashboard. Eseguire il drill-down nei client che non sono in grado di eseguire la registrazione per individuare gli endpoint ai quali i client non possono connettersi a causa di problemi di configurazione del proxy. Per altre informazioni, vedere [Controlli della connettività degli endpoint](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Stato della connettività**: se i client usano un server proxy per accedere a Desktop Analytics, Configuration Manager visualizza i problemi di autenticazione del proxy dai client. Eseguire il drill-down per visualizzare i client che non possono eseguire la registrazione a causa di problemi di autenticazione del proxy. Per altre informazioni, vedere [Stato della connettività](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Avviso di configurazione

Il dispositivo non viene visualizzato in Desktop Analytics o viene visualizzato con un inventario incompleto. Configuration Manager ha anche identificato un problema relativo alla registrazione del dispositivo. Per altre informazioni, vedere l'elenco delle proprietà del dispositivo [Proprietà dei dispositivi Desktop Analytics in Configuration Manager](#bkmk_config-issues).

Il dispositivo, ad esempio, non ha connettività al servizio. Per altre informazioni, vedere [Connettività all'endpoint di diagnostica di Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>In attesa di registrazione

Desktop Analytics non ha dati di diagnostica per questo dispositivo. Questo problema può essere dovuto al fatto che il dispositivo è stato aggiunto di recente alla raccolta di destinazione e non ha ancora inviato dati. Questo stato può anche indicare che il dispositivo non comunica correttamente con il servizio e che i dati di diagnostica più recenti risalgono a più di 28 giorni prima.

Assicurarsi che il dispositivo sia in grado di comunicare con il servizio. Per altre informazioni, vedere [Endpoint](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Stato in sospeso

Configuration Manager sta ancora configurando il dispositivo o non ha ricevuto dati sufficienti da quest'ultimo per determinarne lo stato.

### <a name="missing-data"></a>Dati mancanti

Configuration Manager ha configurato correttamente il dispositivo, ma Desktop Analytics non è in grado di creare una valutazione della compatibilità. Non ha un set di dati completo per la configurazione del dispositivo (Census) o per le app installate (inventario).

Questo problema spesso si risolve automaticamente quando il dispositivo esegue un nuovo tentativo. Se persiste, assicurarsi che il dispositivo sia in grado di comunicare con il servizio. Per altre informazioni, vedere [Endpoint](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Elenco dei dispositivi

Per visualizzare un elenco specifico di dispositivi in base allo stato, iniziare con il dashboard **Integrità connessione**. Selezionare uno dei segmenti del riquadro **Integrità connessione** ed eseguire il drill-down a un elenco di dispositivi con lo stesso stato. Per impostazione predefinita, questa visualizzazione di dispositivi personalizzata mostra le colonne di Desktop Analytics seguenti:

- Configurazione dell'ID commerciale
- Aggiornamento minimo per la compatibilità
- Consenso esplicito per i dati di diagnostica di Windows
- Consenso esplicito per i dati commerciali di Windows
- Connettività all'endpoint di diagnostica di Windows
- Stato della connettività (a partire dalla versione 2002)
- Controlli della connettività degli endpoint (a partire dalla versione 2002)

Queste colonne corrispondono ai [prerequisiti](overview.md#prerequisites) chiave dei dispositivi per la comunicazione con Desktop Analytics.

[![Screenshot dell'elenco dei dispositivi che non è possibile registrare](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Selezionare un dispositivo per visualizzare l'elenco completo delle proprietà disponibili nel riquadro dei dettagli. È anche possibile aggiungere queste proprietà come colonne all'elenco dei dispositivi.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> Proprietà dispositivo

Le proprietà dispositivo di Desktop Analytics seguenti sono disponibili come colonne nell'elenco dei dispositivi di Configuration Manager:

- [Controlli della connettività degli endpoint](#endpoint-connectivity-checks) (a partire dalla versione 2002)
- [Stato della connettività](#connectivity-status) (a partire dalla versione 2002)
- [Configurazione dello strumento di valutazione](#appraiser-configuration)  
- [Aggiornamento minimo per la compatibilità](#minimum-compatibility-update)  
- [Versione dello strumento di valutazione](#appraiser-version)  
- [Ultima esecuzione completa corretta dello strumento di valutazione](#last-successful-full-run-of-appraiser)  
- [Raccolta di dati dello strumento di valutazione](#appraiser-data-collection)  
- [Ultima esecuzione completa corretta di Census](#last-successful-full-run-of-census)  
- [Raccolta di dati di Census](#census-data-collection)  
- [Connettività all'endpoint di diagnostica di Windows](#windows-diagnostic-endpoint-connectivity)  
- [Controlla i dati di diagnostica dell'utente finale](#check-end-user-diagnostic-data)  
- [Controlla il proxy utente](#check-user-proxy)  
- [Configurazione dell'ID commerciale](#commercial-id-configuration)  
- [Consenso esplicito per i dati commerciali di Windows](#windows-commercial-data-opt-in)  
- [Controlla il nome del dispositivo nei dati di diagnostica](#check-device-name-in-diagnostic-data)  
- [Configurazione del servizio DiagTrack](#diagtrack-service-configuration)  
- [Versione di DiagTrack](#diagtrack-version)  
- [Recupero dell'ID SQM](#sqm-id-retrieval)  
- [Recupero dell'identificatore univoco del dispositivo](#unique-device-identifier-retrieval)  
- [Consenso esplicito per i dati di diagnostica di Windows](#windows-diagnostic-data-opt-in)  

Il riquadro **Blocchi della registrazione e avvisi di configurazione più frequenti** del dashboard Integrità connessione visualizza le proprietà per le quali i dispositivi segnalano più spesso problemi.

### <a name="endpoint-connectivity-checks"></a>Controlli della connettività degli endpoint

A partire dalla versione 2002,<!-- 4963230 --> per rilevare i problemi di autenticazione del proxy, i client eseguono controlli di connettività sugli endpoint necessari. Se un client non riesce a raggiungere un endpoint necessario, questa proprietà mostra un elenco numerato degli endpoint a cui non è possibile connettersi a causa di problemi di configurazione del proxy. Confrontare questo elenco con l'elenco pubblicato di [endpoint necessari](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Stato della connettività

A partire dalla versione 2002,<!-- 4963383 --> se i client usano un server proxy per accedere a Desktop Analytics, questa proprietà mostra i problemi di autenticazione del proxy. Include i dettagli seguenti correlati all'autenticazione proxy:

- Codice di stato
- Codice restituito

Nel file di log verranno visualizzati errori simili ai seguenti:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Dove `%s` è l'URL di un endpoint necessario.

Possono anche comparire messaggi di errore non deterministici, che non richiedono attenzione finché i dispositivi non hanno problemi di registrazione. Ad esempio:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Per altre informazioni sulla configurazione dei server proxy per l'uso con Desktop Analytics, vedere [Autenticazione del server proxy](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Configurazione dello strumento di valutazione

<!--20,21-->
Lo strumento di valutazione è il componente di Windows che corrisponde agli [aggiornamenti per la compatibilità](enroll-devices.md#update-devices). Questo strumento valuta il livello di compatibilità delle app e dei driver nel dispositivo con la versione più recente di Windows.

Se il controllo ha esito positivo, il componente strumento di valutazione è configurato correttamente nel dispositivo.

In caso contrario, può essere visualizzato uno degli errori seguenti:

- Non è possibile configurare la raccolta di dati di compatibilità dell'app per il dispositivo (SetRequestAllAppraiserVersions). Controllare i log per ottenere i dettagli dell'eccezione  

- Non è possibile configurare la raccolta di dati di compatibilità dell'app per il dispositivo (SetRequestAllAppraiserVersions). Controllare i log per ottenere i dettagli dell'eccezione  

- Non è possibile scrivere RequestAllAppraiserVersions nella chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Appraiser`. Verificare le autorizzazioni  

Verificare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account di sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare.  

Per altre informazioni, vedere M365AHandler.log nel client.  

### <a name="minimum-compatibility-update"></a>Aggiornamento minimo per la compatibilità

<!--18,19,32-->
L'aggiornamento per la compatibilità (appraiser.dll) non è installato o non è aggiornato nel dispositivo. La sua versione è precedente al requisito minimo per Desktop Analytics, 10.0.17763.

Installare l'aggiornamento per la compatibilità più recente. Per altre informazioni, vedere [Aggiornamenti per la compatibilità](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Versione dello strumento di valutazione

Questa proprietà visualizza la versione corrente del componente strumento di valutazione nel dispositivo. La versione del file è visualizzata in `%windir%\System32\appraiser.dll`, senza punti decimali. La versione 10.0.17763 del file viene visualizzata come 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Ultima esecuzione completa corretta dello strumento di valutazione

Questa proprietà visualizza la data e l'ora dell'ultima esecuzione corretta dello strumento di valutazione nel dispositivo.

### <a name="appraiser-data-collection"></a>Raccolta di dati dello strumento di valutazione

<!--Appraiser run status-->
<!--22,33-->
Questa proprietà visualizza il risultato più recente dell'esecuzione del componente strumento di valutazione in Windows.

In caso di esito negativo, può visualizzare uno degli errori seguenti:

- Non è possibile raccogliere i dati di compatibilità dell'app (RunAppraiser). Controllare i log per altri dettagli  

- La raccolta di dati relativi alla compatibilità dell'app (CompatTelRunner.exe) è stata completata con un codice errore  

Per altre informazioni, vedere M365AHandler.log nel client.

Verificare la presenza del file seguente: `%windir%\System32\CompatTelRunner.exe`. Se non esiste, reinstallare gli [aggiornamenti per la compatibilità ](enroll-devices.md#update-devices) necessari. Assicurarsi che nessun altro componente di sistema, ad esempio Criteri di gruppo o un servizio antimalware, stia rimuovendo questo file.

Se il file M365AHandler.log nel client include uno degli errori seguenti:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Per facilitare la correzione di questi errori, eseguire i comandi seguenti da una console di Windows PowerShell con privilegi elevati nel client interessato:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Ultima esecuzione completa corretta di Census

Questa proprietà visualizza la data e l'ora dell'ultima esecuzione corretta di Census nel dispositivo.

### <a name="census-data-collection"></a>Raccolta di dati di Census

<!-- Census run status -->
<!--51,52-->
Census è il componente di Windows che esegue l'inventario del dispositivo. I dati di inventario vengono usati per comprendere il dispositivo e la relativa configurazione.

Questa proprietà visualizza il risultato più recente dell'esecuzione del componente Census in Windows.

In caso di esito negativo, può visualizzare uno degli errori seguenti:

- Non è possibile raccogliere dati sul dispositivo e sulla rispettiva configurazione (RunCensus). Controllare i log per ottenere i dettagli dell'eccezione  

- Lo strumento per la raccolta dei dati del dispositivo e della configurazione (devicecensus.exe) non è stato trovato  

Per altre informazioni, vedere M365AHandler.log nel client.

Verificare la presenza del file seguente: `%windir%\System32\DeviceCensus.exe`. Se non esiste, reinstallare gli [aggiornamenti per la compatibilità ](enroll-devices.md#update-devices) necessari. Assicurarsi che nessun altro componente di sistema, ad esempio Criteri di gruppo o un servizio antimalware, stia rimuovendo questo file.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Connettività all'endpoint di diagnostica di Windows

<!--12,15-->
Se il controllo ha esito positivo, il dispositivo può connettersi all'endpoint di Esperienze utente connesse e telemetria (Vortex).

In caso contrario, può essere visualizzato uno degli errori seguenti:  

- Non è possibile connettersi all'endpoint di Esperienze utente connesse e telemetria (Vortex). Controllare le impostazioni della rete o del proxy  

- Non è possibile verificare la connettività all'endpoint di Esperienze utente connesse e telemetria (CheckVortexConnectivity). Controllare i log per ottenere i dettagli dell'eccezione  

I dispositivi verificano la connettività con una richiesta GET all'endpoint seguente in base alla versione del sistema operativo:

| Versione sistema operativo | Endpoint |
|------------|----------|
| - Windows 10, versione 1809 o successiva<br/>- Windows 10, versione 1803 con aggiornamento cumulativo 2018-09 o successiva | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versione 1803 *senza* aggiornamento cumulativo 2018-09 o successiva | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versione 1709 o precedente | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Assicurarsi che il dispositivo sia in grado di comunicare con il servizio. Questo controllo convalida alcuni ma non tutti gli endpoint richiesti. Per altre informazioni, vedere [Endpoint](enable-data-sharing.md#endpoints).  

Per altre informazioni, vedere M365AHandler.log nel client.  

### <a name="check-end-user-diagnostic-data"></a>Controlla i dati di diagnostica dell'utente finale

<!--1004-->
Se il controllo ha esito negativo, un utente ha selezionato un livello inferiore di dati di diagnostica di Windows nel dispositivo. L'esito negativo può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [Impostazioni di Windows](enroll-devices.md#windows-settings).

A seconda dei requisiti aziendali, è possibile disabilitare la scelta da parte dell'utente tramite Criteri di gruppo. Usare l'impostazione per **configurare l'interfaccia utente dell'impostazione del consenso esplicito per la telemetria**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).

### <a name="check-user-proxy"></a>Controlla il proxy utente

<!--30,35-->
L'impostazione DisableEnterpriseAuthProxy è abilitata per impostazione predefinita per Windows 7. Per i computer Windows 8.1 Configuration Manager imposta DisableEnterpriseAuthProxy su 0 (non disabilitata).

Questa proprietà può visualizzare gli errori seguenti:

- Il proxy di autenticazione è abilitato. Impostare DisableEnterpriseAuthProxy su 0 in `HKLM:\Software\Policies\Microsoft\Windows\DataCollection`

- Non è possibile verificare lo stato del proxy di autenticazione. Controllare i log per ottenere i dettagli dell'eccezione

Per altre informazioni, vedere M365AHandler.log nel client.  

Verificare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account di sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. L'esito negativo può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [Impostazioni di Windows](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Configurazione dell'ID commerciale

<!--9, 11, 53-->
Per eseguire il mapping delle informazioni dai dispositivi all'area di lavoro di Desktop Analytics, Microsoft usa un ID commerciale univoco. Quando si integra Configuration Manager con Desktop Analytics, viene automaticamente eseguita una query sul servizio per individuare questo ID. Configuration Manager deve applicare automaticamente questo ID ai client a cui sono destinate le impostazioni di Desktop Analytics.

Se il controllo ha esito positivo, il dispositivo è configurato correttamente con un ID commerciale.

In caso contrario, può essere visualizzato uno degli errori seguenti:

- Non è possibile scrivere CommercialId nella chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Verificare le autorizzazioni  

- Non è possibile aggiornare il valore CommercialId nella chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Controllare i log per ottenere i dettagli dell'eccezione  

- Specificare il valore corretto per CommercialId in `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Per altre informazioni, vedere M365AHandler.log nel client.  

Verificare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account di sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. L'esito negativo può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [Impostazioni di Windows](enroll-devices.md#windows-settings).  

Per il dispositivo è presente un ID diverso. Questa chiave del Registro di sistema viene usata da Criteri di gruppo e ha la precedenza sull'ID specificato da Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a> Per visualizzare l'ID commerciale nel portale Desktop Analytics, usare la procedura seguente:

1. Passare al portale Desktop Analytics e selezionare **Servizi connessi** nel gruppo Impostazioni globali.  

2. Nel riquadro **Servizi connessi** il riquadro**Registra i dispositivi** è selezionato per impostazione predefinita. Nel riquadro Registra i dispositivi la sezione Informazioni visualizza la chiave ID commerciale.  

[![Screenshot dell'ID commerciale nel portale Desktop Analytics](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Usare **Ottieni una nuova chiave ID** solo se non è possibile usare quella corrente. Se si rigenera l'ID commerciale, [registrare di nuovo i dispositivi con il nuovo ID](enroll-devices.md#device-enrollment). Questo processo può causare la perdita di dati di diagnostica durante la transizione.  

### <a name="windows-commercial-data-opt-in"></a>Consenso esplicito per i dati commerciali di Windows

<!--64-->
Questa proprietà è specifica dei dispositivi che eseguono Windows 7 o Windows 8.1. Esegue test simili a quelli di [Consenso esplicito per i dati di diagnostica di Windows](#windows-diagnostic-data-opt-in), ad eccezione del valore CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Controlla il nome del dispositivo nei dati di diagnostica

<!--56,58-->
Se questo controllo ha esito positivo, il dispositivo è configurato correttamente per la condivisione del nome dispositivo.

In caso contrario, può essere visualizzato uno degli errori seguenti:

- Non è possibile controllare il nome dispositivo da inviare a Microsoft come parte dei dati di diagnostica di Windows. Controllare i log per ottenere i dettagli dell'eccezione  

- Non è possibile scrivere AllowDeviceNameInTelemetry nella chiave del Registro di sistema `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Verificare le autorizzazioni  

Per altre informazioni, vedere M365AHandler.log nel client.  

Verificare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account di sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. L'esito negativo può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [Impostazioni di Windows](enroll-devices.md#windows-settings).  

Assicurarsi che un altro meccanismo dei criteri, ad esempio Criteri di gruppo, non disabiliti questa impostazione.

### <a name="diagtrack-service-configuration"></a>Configurazione del servizio DiagTrack

<!--44,45,50-->
Se il controllo ha esito positivo, il componente DiagTrack è configurato correttamente nel dispositivo. La versione minima richiesta da Desktop Analytics è la versione 10010586 (10.0.10586).

In caso contrario, può essere visualizzato uno degli errori seguenti:

- Il componente Esperienze utente connesse e telemetria (diagtrack.dll) è obsoleto. Controllare i requisiti  

    > [!TIP]
    > Esiste un problema noto con la patch di sicurezza estesa di aprile 2020 per Windows 7 che impedisce ai dispositivi di segnalare correttamente questo errore. Per altre informazioni, vedere le [note sulla versione](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

- Non è possibile trovare il componente Esperienze utente connesse e telemetria (diagtrack.dll). Controllare i requisiti  

- Abilitare e avviare il servizio Esperienze utente connesse e telemetria per l'invio di dati a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installare gli aggiornamenti più recenti. Per altre informazioni, vedere [Aggiornare i dispositivi](enroll-devices.md#update-devices).

Assicurarsi che il servizio **Esperienze utente connesse e telemetria** nel dispositivo sia in esecuzione.

### <a name="diagtrack-version"></a>Versione di DiagTrack

Questa proprietà visualizza la versione corrente del componente Esperienze utente connesse e telemetria nel dispositivo. La versione del file è visualizzata in `%windir%\System32\diagtrack.dll`, senza punti decimali. La versione 10.0.10586 del file, ad esempio, viene visualizzata come 10010586.

### <a name="sqm-id-retrieval"></a>Recupero dell'ID SQM

<!--38-->
Questa proprietà è destinata principalmente ai dispositivi Windows 7. Può essere usata da versioni successive del sistema operativo come identificatore di fallback per il dispositivo.

Se l'operazione non riesce, può essere visualizzato l'errore seguente:

- Non è possibile recuperare l'identificatore di telemetria del dispositivo legacy (SQM ID)

Per altre informazioni, vedere M365AHandler.log nel client.  

Assicurarsi che non siano presenti ID duplicati nell'ambiente in uso se, ad esempio, i dispositivi sono stati distribuiti con un'immagine del sistema operativo non generalizzata.

### <a name="unique-device-identifier-retrieval"></a>Recupero dell'identificatore univoco del dispositivo

<!--54-->
Desktop Analytics usa il servizio account Microsoft per un'identità del dispositivo più affidabile.

Assicurarsi che il servizio **Assistente per l'accesso all'account Microsoft** non sia disabilitato. Il tipo di avvio deve essere **Manuale (avvio trigger)** .

Per disabilitare l'accesso dell'account Microsoft dell'utente finale, usare le impostazioni dei criteri anziché bloccare l'endpoint. Per altre informazioni, vedere [Account Microsoft nell'organizzazione](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Consenso esplicito per i dati di diagnostica di Windows

<!--8,40,55,62-->
Questa proprietà controlla che Windows sia configurato correttamente per consentire i dati di diagnostica. La proprietà controlla il valore AllowTelemetry nelle chiavi del Registro di sistema seguenti:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Verificare le autorizzazioni per queste chiavi del Registro di sistema. Assicurarsi che l'account di sistema locale possa accedere a queste chiavi per il client di Configuration Manager da impostare. L'esito negativo può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [Impostazioni di Windows](enroll-devices.md#windows-settings).  

Per altre informazioni, vedere M365AHandler.log nel client.  

## <a name="see-also"></a>Vedere anche

[Risolvere i problemi di Desktop Analytics](troubleshooting.md)