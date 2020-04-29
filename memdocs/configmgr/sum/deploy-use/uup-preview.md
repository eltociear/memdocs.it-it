---
title: Anteprima di UUP
titleSuffix: Configuration Manager
description: Istruzioni per l'anteprima dell'integrazione UUP
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702939"
---
# <a name="uup-private-preview-instructions"></a>Istruzioni per l'anteprima privata di UUP

> [!Note]  
> Queste informazioni fanno riferimento a una funzionalità di anteprima che può essere modificata sostanzialmente prima del rilascio della versione commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

## <a name="introduction"></a>Introduzione

La piattaforma UUP (Unified Update Platform) è la piattaforma per la creazione di pacchetti e la pubblicazione che i dispositivi consumer e aziendali usano per ricevere gli aggiornamenti da Windows Update per le aziende. Il programma di anteprima privata di UUP è riservato ai clienti che hanno accettato di collaborare con Microsoft per la convalida dell'uso degli aggiornamenti di UUP in Configuration Manager per la risoluzione dei problemi relativi alla manutenzione di Windows attualmente segnalati dai clienti. Questi aggiornamenti non sono al momento disponibili pubblicamente.

Per altre informazioni su UUP, vedere il post di blog di Windows seguente: [Aggiornamento su Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Vantaggi

La funzionalità UUP e gli aggiornamenti cumulativi di Windows 10 consentono di risolvere numerosi problemi relativi alla manutenzione di Windows attualmente segnalati dai clienti.

### <a name="feature-updates"></a>Aggiornamenti delle funzionalità

- Con gli aggiornamenti delle funzionalità UUP, il processo di aggiornamento di Windows non influisce sulle funzionalità su richiesta né sui language pack.

- Eseguire l'aggiornamento direttamente al livello di conformità di sicurezza più recente. Non è necessario installare le patch di sicurezza subito dopo un aggiornamento delle funzionalità. Microsoft pubblica ogni mese un nuovo aggiornamento delle funzionalità con la patch cumulativa di sicurezza più recente. Non è necessario scaricare o distribuire la maggior parte del contenuto degli aggiornamenti delle funzionalità ogni mese. Si scarica solo la patch di sicurezza, condivisa da UUP con l'aggiornamento cumulativo.

### <a name="cumulative-updates"></a>Aggiornamenti cumulativi

- Gli aggiornamenti cumulativi con UUP includono gli aggiornamenti dello stack di manutenzione (Servicing Stack Updates, SSU) oltre agli aggiornamenti della sicurezza cumulativi mensili. Questo comportamento consente di risolvere problemi con l'orchestrazione di questi due aggiornamenti. Esso verifica che gli aggiornamenti dello stack di manutenzione siano disponibili per l'installazione degli aggiornamenti cumulativi. Non è necessario gestire e orchestrare queste relazioni.

- Gli aggiornamenti cumulativi con UUP consentono di distribuire il contenuto di funzionalità su richiesta e language pack offline. Questo comportamento consente agli utenti di aggiungere tale contenuto su richiesta. Gli utenti non hanno bisogno di scaricare questo contenuto da Internet e l'amministratore non ha necessità di capire come pre-installarlo.

## <a name="set-up"></a>Configurazione

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. Inviare l'ID WSUS a Microsoft

Per partecipare all'anteprima privata di UUP, condividere l'ID WSUS con il contatto dell'anteprima di UUP. Microsoft approva l'ambiente WSUS in uso e lo aggiunge al programma di anteprima di UUP. Senza questo ID non è possibile visualizzare eventuali aggiornamenti di UUP fino a quando l'anteprima non diventa pubblica.

Per ottenere l'ID WSUS, eseguire lo script PowerShell seguente:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

La proprietà **MUUrl** deve essere `https://sws.update.microsoft.com`. Per modificarla, vedere la risoluzione nell'articolo del supporto tecnico seguente: [La sincronizzazione di Windows Server Update Services non riesce con SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. Aggiornare Configuration Manager

Apportare le modifiche seguenti al sito di Configuration Manager per supportare questa anteprima di UUP:

#### <a name="diagnostics-and-usage-data-level"></a>Livello dati di diagnostica e di utilizzo

Valutare la possibilità di aumentare il livello dati di diagnostica e di utilizzo di Configuration Manager durante questa anteprima. Il livello **Completo** consente a Microsoft di analizzare meglio i problemi relativi a questa nuova funzionalità e di risolverli. Per altre informazioni, vedere [Livelli di raccolta dati di utilizzo e di diagnostica per la versione 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>Installare l'aggiornamento più recente

1. Aggiornare il sito con uno degli aggiornamenti seguenti:

    - Versione 1902 con l'[aggiornamento cumulativo](https://support.microsoft.com/help/4500571)
    - [Versione 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Per altre informazioni, vedere [Installare gli aggiornamenti nella console](../../core/servers/manage/install-in-console-updates.md).

2. Aggiornare i client.  

    - Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - Aggiornare tutti i client destinati agli aggiornamenti di UUP per evitare di *scaricare inutilmente circa 6 GB* di contenuto inutilizzato nei client.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Aggiornare i client Windows a una versione supportata

Per la corretta installazione degli aggiornamenti di UUP, installare entrambi gli aggiornamenti seguenti:

1. Un livello di conformità mensile cumulativo minimo specifico.

2. Un aggiornamento specifico non cumulativo e non di sicurezza da Microsoft Update Catalog. Per importare l'aggiornamento in Configuration Manager per la distribuzione, vedere [Importare gli aggiornamenti da Microsoft Update Catalog](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Versioni supportate di Windows 10 e aggiornamenti necessari

| Versione di Windows 10 | Livello di conformità minimo | Aggiornamento aggiuntivo del catalogo |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, versione 1903** | RTM | 7 novembre 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, versione 1809** | Agosto 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 novembre 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, versione 1803** | Aprile 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 novembre 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, versione 1709** | Aprile 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 novembre 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Se si applicano gli aggiornamenti del 12 novembre 2019 al client prima di applicare l'aggiornamento aggiuntivo del catalogo del 7 novembre 2019, le modifiche all'agente di Windows Update necessarie per il supporto di UUP verranno sovrascritte. Per correggere i client in tale scenario, applicare l'aggiornamento aggiuntivo del catalogo dopo l'installazione degli aggiornamenti del 12 novembre 2019.
> - Se si applica un aggiornamento delle funzionalità al client, è necessario reinstallare l'aggiornamento aggiuntivo del catalogo al termine dell'aggiornamento.
> - Per semplificare il test degli aggiornamenti delle funzionalità, importare gli aggiornamenti in Configuration Manager. Per altre informazioni, vedere [Importare gli aggiornamenti da Microsoft Update Catalog](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). Al termine dell'aggiornamento delle funzionalità, l'aggiornamento aggiuntivo del catalogo viene visualizzato come **obbligatorio**. Ciò ne consente la distribuzione automatica alla versione del sistema operativo di livello superiore.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. Consenti ai client di scaricare contenuto differenziale quando disponibile

Per eseguire correttamente il download degli aggiornamenti di UUP, abilitare l'impostazione del client **Consenti ai client di scaricare contenuto differenziale quando disponibile**. Con questa impostazione, Configuration Manager consente all'agente di Windows Update (WUA) di determinare il contenuto necessario da scaricare nei client. Questo comportamento sostituisce il comportamento predefinito, in base al quale il client di Configuration Manager scarica tutto il contenuto associato all'aggiornamento di UUP. Quando si abilita questa impostazione, WUA determina il contenuto aggiuntivo necessario di ogni aggiornamento di UUP, ad esempio, solo le funzionalità su richiesta e i language pack necessari.

Quando è abilitata, questa impostazione non influisce sui download di contenuto per i server da Internet, ma si applica solo ai download per i client. Prima di distribuire gli aggiornamenti di UUP ai client, applicare questa impostazione ai client che soddisfano le versioni supportate di UUP. Gli aggiornamenti client prerequisiti correggono i problemi di compatibilità degli aggiornamenti di UUP in WSUS e Configuration Manager.

Per altre informazioni su questa impostazione client, vedere [Informazioni sulle impostazioni client - Aggiornamenti software](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available).

### <a name="5-review-your-software-update-infrastructure"></a>5. Rivedere l'infrastruttura di aggiornamento software

Prima di sincronizzare gli aggiornamenti di UUP, rivedere le regole di distribuzione automatica e i piani di manutenzione. Se non si vogliono distribuire automaticamente questi aggiornamenti, modificare le regole di distribuzione automatica in modo da escluderli. Per altre informazioni, vedere [Come individuare gli aggiornamenti di UUP sincronizzati](#how-to-find-synced-uup-updates). Per impostazione predefinita, i piani di manutenzione esistenti distribuiscono solo aggiornamenti non di UUP. È possibile cambiare questo comportamento modificando i piani di manutenzione.

Rivedere i report di conformità e modificarli se necessario. Se, ad esempio, si misura la conformità per tutti i prodotti, verranno ora visualizzati sia gli aggiornamenti cumulativi di UUP che quelli non di UUP. I dispositivi dichiareranno la conformità a entrambi i tipi di aggiornamenti. Assicurarsi che i report di conformità in uso siano predisposti per questa modifica.

## <a name="enable-uup-and-start-testing"></a>Abilitare UUP e avviare il test

### <a name="select-products-and-classifications-to-sync"></a>Selezionare i prodotti e le classificazioni da sincronizzare

Quando si è in grado di avviare la sincronizzazione degli aggiornamenti di UUP e dopo che Microsoft ha approvato l'ID WSUS, abilitare i nuovi prodotti:

1. [Sincronizzare gli aggiornamenti software](../get-started/synchronize-software-updates.md) per popolare i nuovi prodotti.  

2. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.

3. Selezionare il sito di livello superiore, che è un sito di amministrazione centrale o un sito primario autonomo.

4. Selezionare **Configura componenti del sito** nella barra multifunzione e scegliere **Punto di aggiornamento software**.

5. Passare alla scheda **Prodotti** e selezionare uno o più dei prodotti seguenti: 

    - **Windows 10 UUP Preview**
    - **Windows Server UUP Preview**

6. Passare alla scheda **Classificazioni** e selezionare le opzioni seguenti:  

    - **Aggiornamenti della sicurezza**: per visualizzare gli aggiornamenti cumulativi di UUP  
    - **Aggiornamenti**: per visualizzare gli aggiornamenti delle funzionalità di UUP  

7. Sincronizzare di nuovo gli aggiornamenti software per visualizzare i nuovi aggiornamenti di UUP.

### <a name="how-to-find-synced-uup-updates"></a>Come individuare gli aggiornamenti di UUP sincronizzati

Dopo avere sincronizzato gli aggiornamenti di UUP nell'ambiente in uso, individuarli all'interno della Console di Configuration Manager per sottoporli a test. È possibile trovare gli aggiornamenti di anteprima in due modi:

- Poiché questi aggiornamenti di anteprima si trovano in un prodotto separato, usare il nome del prodotto per filtrare e trovare gli aggiornamenti corrispondenti. Usare il filtro di prodotto del piano di manutenzione per distribuire gli aggiornamenti delle funzionalità di UUP o non di UUP.  

- Nei nodi **Tutti gli aggiornamenti software** e **Aggiornamenti di tutte le piattaforme Windows 10** di **Raccolta software** è presente la nuova colonna facoltativa **Tag**. Questa proprietà è disponibile anche come filtro nelle regole di distribuzione automatica. Per gli aggiornamenti di UUP, cercare `UUP` in questo campo. Per gli aggiornamenti non di UUP è vuoto.  

### <a name="updates-available-during-preview"></a>Aggiornamenti disponibili durante l'anteprima

Per altre informazioni su tutti gli aggiornamenti di Windows 10 rilasciati da Microsoft, vedere [Informazioni sulla versione di Windows 10](https://docs.microsoft.com/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Aggiornamenti cumulativi da testare

Anche se possono essere visualizzati più aggiornamenti con tag UUP, iniziare con l'aggiornamento di **settembre 2019** (2019-09) o versione successiva. Ad esempio:

- 2019-09 Aggiornamento cumulativo per Windows 10 versione 1809 per sistemi basati su x64 (KB4512578)
- 2019-09 Aggiornamento cumulativo per Windows 10 versione 1803 per sistemi basati su x64 (KB4516058)
- 2019-09 Aggiornamento cumulativo per Windows 10 versione 1709 per sistemi basati su x64 (KB4516066)

#### <a name="feature-updates-to-test"></a>Aggiornamenti delle funzionalità da testare

Anche se sono visualizzati più aggiornamenti con tag UUP, iniziare con l'aggiornamento di **settembre 2019** (2019-09B) o versione successiva. Ad esempio:

- Aggiornamento delle funzionalità a Windows 10, versione 1809 x64 2019-09B
- Aggiornamento delle funzionalità a Windows 10, versione 1803 x64 2019-09B

## <a name="scenarios-to-test"></a>Scenari da sottoporre a test

### <a name="test-feature-updates"></a>Aggiornamenti delle funzionalità di test

- Eseguire l'aggiornamento direttamente al livello di conformità di sicurezza scelto  

- Installare le funzionalità su richiesta e i language pack prima dell'aggiornamento. Assicurarsi che l'aggiornamento mantenga questi componenti.  

### <a name="test-cumulative-updates"></a>Testare gli aggiornamenti cumulativi

Durante l'anteprima, mantenere i client conformi usando l'aggiornamento di tipo UUP per più aggiornamenti consecutivi. Questo test consente di comprendere il comportamento in corso.

### <a name="test-content"></a>Contenuto del test

Il primo aggiornamento per ogni versione principale (1809, 1803, 1709), con la combinazione di lingue e architetture, risulterà di grandi dimensioni, sia per il numero di file che per lo spazio su disco, rispetto a quanto si è visto in precedenza con gli aggiornamenti non di UUP. Questo contenuto aggiuntivo è destinato principalmente a tutte le funzionalità su richiesta e i Language Pack per gli aggiornamenti cumulativi. Per il primo degli aggiornamenti delle funzionalità, è disponibile contenuto di grandi dimensioni aggiuntivo.

Per gli aggiornamenti cumulativi e delle funzionalità futuri, la quantità di nuovo contenuto che il sito scarica e distribuisce è molto inferiore. Tra un aggiornamento e l'altro, UUP condivide in modo intelligente tutto il contenuto relativo alle funzionalità su richiesta e ai language pack. Non è necessario scaricare o distribuire di nuovo questo contenuto condiviso. Durante l'anteprima, nelle versioni di Windows 10 1709 e 1803, le dimensioni del download mensile sono circa uguali a quelle degli aggiornamenti cumulativi per gli scenari non di UUP. In Windows 10 versione 1809 e successive, le dimensioni del download incrementale dell'aggiornamento cumulativo sono molto inferiori ogni mese.

Se si esamina il contenuto totale scaricato e distribuito in un periodo di 12 mesi per le edizioni *non Express*, per Windows 10 versione 1803 senza UUP è circa uguale a quello della versione 1809 con UUP. Il contenuto totale scaricato e distribuito nell'intero ciclo di vita della versione è minore nella versione 1809 con UUP.

### <a name="supported-content-channels"></a>Canali di contenuto supportati

Per la versione di anteprima, testare gli scenari reali tipici in uso. UUP supporta tutti i canali di contenuto, tra cui:

- Ottimizzazione recapito di Windows
  - Quando si usa Ottimizzazione recapito, assicurarsi che la sua configurazione sia corretta. Per altre informazioni, vedere [FAQs to optimize Windows 10 update delivery](optimize-windows-10-update-delivery.md) (FAQ per ottimizzare il recapito degli aggiornamenti di Windows 10).
- Peer cache di Configuration Manager
- Windows BranchCache
- Usare l'opzione **Nessun pacchetto di distribuzione** per fare in modo che i client eseguano il download direttamente da Microsoft Update. Usare questa opzione con Ottimizzazione recapito.
- Provider di contenuti alternativi di terze parti

Per altre informazioni sui canali di contenuto, vedere [Ottimizzare il recapito degli aggiornamenti di Windows 10](optimize-windows-10-update-delivery.md).

<!-- TODO: Addlink to WSUS Perf documentation-->
