---
title: Risolvere i problemi relativi a Connected Cache
titleSuffix: Configuration Manager
description: Dettagli tecnici relativi a Microsoft Connected Cache per facilitare la risoluzione dei problemi.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5be6158a2ed7d79af2bee72c81a462e4d83b68e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700869"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Risolvere i problemi relativi a Microsoft Connected Cache in Configuration Manager

Questo articolo presenta i dettagli tecnici relativi a Microsoft Connected Cache in Configuration Manager. È utile per risolvere i problemi che possono verificarsi nel proprio ambiente. Per altre informazioni sul funzionamento e sull'uso di questa funzionalità, vedere [Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> A partire dalla versione 1910, questa funzionalità è denominata **Microsoft Connected Cache**. In precedenza era nota come Cache in rete di Ottimizzazione recapito (DOINC).

## <a name="verify"></a>Verifica

Quando si installa correttamente il server di cache in rete di Ottimizzazione recapito e si configurano correttamente i client, questi vengono scaricati dal server di cache installato nel punto di distribuzione anziché da Internet.

Verificare questo comportamento [in un client](#bkmk_verify-client) o [nel server](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a> Verifica in un client

1. In un client che esegue Windows 10, versione 1809 o successiva, scaricare il contenuto gestito dal cloud. Per altre informazioni sui tipi di contenuto supportati da Connected Cache, vedere [Verificare Connected Cache](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Aprire PowerShell ed eseguire il comando seguente: `Get-DeliveryOptimizationStatus`

Ad esempio:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Si noti che l'attributo `BytesFromCacheServer` non è zero.

Se il client non è configurato correttamente o il server di cache non è installato correttamente, il client di Ottimizzazione recapito esegue il fallback all'origine cloud originale. L'attributo BytesFromCacheServer sarà quindi zero.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a> Verifica nel server

Verificare prima di tutto che le proprietà del Registro di sistema siano configurate correttamente: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`. Ad esempio, il percorso della cache nell'unità è `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`, dove `PrimaryDrivesInput` può essere costituito da più unità, ad esempio `C,D,E`.

Usare quindi il metodo seguente per simulare una richiesta di download del client nel server con le intestazioni obbligatorie.

1. Aprire una finestra di PowerShell a 64 bit come amministratore.
2. Eseguire il comando seguente e sostituire `<DoincServer>` con il nome o l'indirizzo IP del server:

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

L'output sarà simile all'esempio seguente:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Gli attributi seguenti indicano l'esito positivo:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>File di registro

- Log di configurazione ARR: `%temp%\arr_setup.log`

- Log del server di cache in rete di Ottimizzazione recapito: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` nel punto di distribuzione e `DistMgr.log` nel server del sito

- Log operativi IIS: Per impostazione predefinita, `%SystemDrive%\inetpub\logs\LogFiles`

- Log operativo del server di cache in rete di Ottimizzazione recapito: `C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Tra gli altri usi, questo log consente di identificare i problemi di connettività con Microsoft Cloud.

## <a name="setup-error-codes"></a>Codici di errore di installazione

Nella tabella seguente sono elencati i possibili codici di errore che possono verificarsi quando Configuration Manager installa Connected Cache nel punto di distribuzione:

| Codice errore | Descrizione errore |
|------------|-------------------|
| 0x00000000 | Operazione completata |
| 0x00000BC2 | Operazione completata, riavvio richiesto |
| 0x00000643 | Errore di installazione generico |
| 0x00D00001 | L'installazione di Connected Cache può essere eseguita solo se Internet Information Services (IIS) è stato installato |
| 0x00D00002 | L'installazione di Connected Cache può essere eseguita solo se nel server è presente un sito Web predefinito |
| 0x00D00003 | Non è possibile installare Connected Cache se ARR (Application Request Routing) è già installato |
| 0x00D00004 | L'installazione di Connected Cache può essere eseguita solo se ARR (Application Request Routing) è stato installato dallo script Install.ps1 |
| 0x00D00005 | L'installazione di Connected Cache richiede che la sessione di PowerShell venga eseguita come amministratore |
| 0x00D00006 | L'installazione di Connected Cache può essere eseguita solo da un ambiente PowerShell a 64 bit |
| 0x00D00007 | L'installazione di Connected Cache può essere eseguita solo in Windows Server |
| 0x00D00008 | Errore: il numero di unità cache specificato deve corrispondere al numero di percentuali di dimensioni delle unità cache specificato |
| 0x00D00009 | Errore: è necessario specificare un ID di nodo di cache valido |
| 0x00D0000A | Errore: è necessario specificare un set di unità cache valido |
| 0x00D0000B | Errore: è necessario specificare un set di percentuali di dimensioni unità cache valido |
| 0x00D0000C | Errore: è necessario specificare un set di percentuali di dimensioni unità cache o le dimensioni dell'unità cache in GB |
| 0x00D0000D | Errore: non è possibile specificare sia un set di percentuali di dimensioni unità cache che le dimensioni dell'unità cache in GB |
| 0x00D0000E | Errore: il numero di unità cache specificato deve corrispondere al numero di dimensioni dell'unità cache in GB specificato |
| 0x00D0000F | Errore: non è stato possibile eseguire il backup del file applicationhost.config da $AppHostConfig a $AppHostConfigDestinationName |
| 0x00D00010 | Errore: non è stato possibile eseguire il backup del file web.config del sito Web predefinito da $WebsiteConfigFilePath a $WebConfigDestinationName |
| 0x00D00011 | Errore: Si è verificata un'eccezione in SetupARRWebFarm.ps1 |
| 0x00D00012 | Errore: Si è verificata un'eccezione in SetupARRWebFarmRewriteRules.ps1 |
| 0x00D00013 | Errore: Si è verificata un'eccezione in SetupARRWebFarmProperties.ps1 |
| 0x00D00014 | Errore: Si è verificata un'eccezione in SetupAllowableServerVariables.ps1 |
| 0x00D00015 | Errore: Si è verificata un'eccezione in SetupFirewallRules.ps1 |
| 0x00D00016 | Errore: Si è verificata un'eccezione in SetupAppPoolProperties.ps1 |
| 0x00D00017 | Errore: Si è verificata un'eccezione in SetupARROutboundRules.ps1 |
| 0x00D00018 | Errore: Si è verificata un'eccezione in SetupARRDiskCache.ps1 |
| 0x00D00019 | Errore: Si è verificata un'eccezione in SetupARRProperties.ps1 |
| 0x00D0001A | Errore: Si è verificata un'eccezione in SetupARRHealthProbes.ps1 |
| 0x00D0001B | Errore: Si è verificata un'eccezione in VerifyIISSItesStarted.ps1 |
| 0x00D0001C | Errore: Si è verificata un'eccezione in SetDrivesToHealthy.ps1 |
| 0x00D0001D | Errore: Si è verificata un'eccezione in VerifyCacheNodeSetup.ps1 |
| 0x00D0001E | Non è possibile installare Connected Cache se il sito Web predefinito non si trova sulla porta 80 |
| 0x00D0001F | Errore: l'allocazione di unità cache in percentuale non può superare 100 |
| 0x00D00020 | Errore: l'allocazione di unità cache in GB non può superare lo spazio disponibile dell'unità |
| 0x00D00021 | Errore: l'allocazione di unità cache in percentuale deve essere maggiore di 0 |
| 0x00D00022 | Errore: l'allocazione di unità cache in GB deve essere maggiore di 0 |
| 0x00D00023 | Errore: si è verificata un'eccezione in RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Errore: si è verificata un'eccezione in RegisterScheduledTask_Maintenance |
| 0x00D00025 | Errore: si è verificata un'eccezione durante la configurazione delle regole di riscrittura per la farm HTTPS: $FarmName |
| 0x00D00026 | Errore: si è verificata un'eccezione durante la configurazione delle regole di riscrittura per la farm HTTP: $FarmName |
| 0x00D00027 | Non è possibile installare Connected Cache perché l'installazione del software dipendente "ARR (Application Request Routing)" non è riuscita. Vedere il file di log che si trova in %temp%\arr_setup.log |

## <a name="iis-configurations"></a>Configurazioni di IIS

L'installazione del server di cache di Ottimizzazione recapito apporta diverse modifiche alla configurazione di IIS nel punto di distribuzione.

### <a name="application-request-routing"></a>Application Request Routing

Il server di cache di Ottimizzazione recapito installa e configura [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) di IIS. Per evitare potenziali conflitti, questo componente non può essere già installato nel punto di distribuzione.

### <a name="allowed-server-variables"></a>Variabili del server consentite

Dopo aver installato il server di cache di Ottimizzazione recapito, il sito Web predefinito ha le variabili del server *locale* seguenti:

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>Regole di riscrittura

Il server di cache di Ottimizzazione recapito aggiunge le regole di riscrittura seguenti:

#### <a name="inbound-rewrite-rules"></a>Regole di riscrittura in ingresso

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Regole di riscrittura in uscita

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Gestire le risorse del server

Lo spazio su disco necessario per ogni server di cache di Ottimizzazione recapito può variare in base ai requisiti di aggiornamento dell'organizzazione. 100 GB dovrebbero essere uno spazio sufficiente per memorizzare nella cache il contenuto seguente:

- Un aggiornamento delle funzionalità
- Da due a tre mesi di aggiornamenti qualitativi e di Office
- App Microsoft Intune e app incluse in Windows

Il server di cache di Ottimizzazione recapito non deve utilizzare molta memoria di sistema o tempo del processore. Se si nota un notevole consumo di risorse di memoria o del processore dopo aver installato il server di cache di Ottimizzazione recapito, analizzare i file di log di IIS e ARR.

Se i file di log di IIS e ARR occupano troppo spazio sul server, sono disponibili vari metodi per gestire i file di log. Per altre informazioni, vedere [Gestione dell'archiviazione dei file di log IIS](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Vedere anche

[Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
