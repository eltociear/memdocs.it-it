---
title: Ottimizzare il recapito degli aggiornamenti di Windows 10
titleSuffix: Configuration Manager
description: Informazioni su come usare Configuration Manager per gestire il contenuto di aggiornamento per rimanere aggiornati con Windows 10.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c42015880cae09be48feff9c42b6b2a0d2c8544
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129315"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Ottimizzare il recapito degli aggiornamenti di Windows 10 con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per molti clienti, un percorso appropriato per ottenere gli aggiornamenti mensili di Windows 10 e rimanere aggiornati inizia dalla definizione di una strategia di distribuzione del contenuto valida con Configuration Manager. Le dimensioni degli aggiornamenti qualitativi mensili possono essere fonte di preoccupazione per le organizzazioni di grandi dimensioni. Esistono alcune tecnologie che consentono di ridurre il carico sulla rete e la larghezza di banda per ottimizzare il recapito degli aggiornamenti. Questo articolo illustra queste tecnologie, le confronta e fornisce indicazioni per prendere più facilmente decisioni su quella da usare.  
 
Windows 10 offre diversi tipi di aggiornamenti. Per altre informazioni, vedere [Tipi di aggiornamenti in Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Questo articolo è incentrato sugli aggiornamenti *qualitativi* di Windows 10 con Configuration Manager. 


## <a name="express-update-delivery"></a>Recapito rapido degli aggiornamenti

I download degli aggiornamenti qualitativi di Windows 10 possono essere di grandi dimensioni. Ogni pacchetto contiene tutte le correzioni rilasciate in precedenza per garantire coerenza e semplicità. Microsoft è riuscita a ridurre le dimensioni del contenuto di aggiornamento di Windows 10 scaricato da ogni client con una funzionalità denominata aggiornamento rapido. L'aggiornamento rapido viene usato attualmente da milioni di dispositivi per eseguire il pull degli aggiornamenti direttamente dal servizio Windows Update e consente di ridurre significativamente le dimensioni dei download. Questo vantaggio è disponibile anche per i clienti con client che non eseguono il download direttamente dal servizio Windows Update. 

Configuration Manager ha aggiunto il supporto per i [file di installazione rapida](manage-express-installation-files-for-windows-10-updates.md) degli aggiornamenti qualitativi di Windows 10 nella versione 1702. Tuttavia, per risultati ottimali è consigliabile usare Configuration Manager versione 1802 o successiva. Per ottenere prestazioni ottimali a livello di velocità di download, è anche consigliabile usare Windows 10 versione 1703 o successiva. 

> [!NOTE]  
> Il contenuto della versione rapida è notevolmente più grande rispetto alla versione con file completi. Un file di installazione rapida contiene tutte le possibili varianti per ogni file che dovrà aggiornare. Di conseguenza, la quantità di spazio su disco aumenta per gli aggiornamenti nell'origine del pacchetto di aggiornamento e nei punti di distribuzione quando si abilita il supporto dell'installazione rapida in Configuration Manager. Anche se aumenta il requisito di spazio su disco nei punti di distribuzione, si riducono le dimensioni del contenuto che i client scaricano da questi punti di distribuzione. I client scaricano solo le parti necessarie (delta) ma non l'intero aggiornamento.


## <a name="peer-to-peer-content-distribution"></a>Distribuzione del contenuto peer-to-peer

Anche se i client scaricano solo le parti del contenuto necessarie, è possibile velocizzare gli aggiornamenti di Windows nel proprio ambiente grazie all'utilizzo della distribuzione del contenuto peer-to-peer. Sfruttare i peer come origine di download per gli aggiornamenti qualitativi può essere utile per gli ambienti in cui i punti di distribuzione locale non sono presenti negli uffici remoti. Con questo comportamento non è necessario che tutti i client scarichino contenuto da un punto di distribuzione remoto su un collegamento WAN lento. L'uso dei peer può anche essere utile quando i client ricorrono al servizio Windows Update. È necessario un solo peer per scaricare il contenuto degli aggiornamenti dal cloud prima di renderlo disponibile agli altri dispositivi.

Configuration Manager supporta numerose tecnologie peer-to-peer, incluse le seguenti:
- Ottimizzazione recapito di Windows
- Peer cache di Configuration Manager
- Windows BranchCache  

Nelle sezioni successive sono disponibili ulteriori informazioni su queste tecnologie.

### <a name="windows-delivery-optimization"></a>Ottimizzazione recapito di Windows

[Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) rappresenta la tecnologia di download e il metodo di distribuzione peer-to-peer principali inclusi in Windows 10. I client Windows 10 possono ottenere il contenuto da altri dispositivi nella propria rete locale che scarica gli stessi aggiornamenti. Usando le [opzioni di Windows disponibili per Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options) è possibile configurare i client in gruppi. Questo raggruppamento consente alle organizzazioni di identificare i dispositivi che sono probabilmente i migliori candidati per soddisfare le richieste peer-to-peer. Ottimizzazione recapito riduce significativamente la larghezza di banda complessiva usata per mantenere aggiornati i dispositivi, velocizzando contemporaneamente i tempi di download.

> [!NOTE]  
> Ottimizzazione recapito è una soluzione gestita dal cloud. L'accesso a Internet al servizio cloud Ottimizzazione recapito è un requisito per utilizzare le funzionalità peer-to-peer. Per informazioni sugli endpoint Internet necessari, vedere [Domande frequenti per Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

Per ottenere risultati ottimali, potrebbe essere necessario impostare la [modalità di download](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode) di Ottimizzazione recapito su **Gruppo (2)** e definire *ID di gruppo*. In modalità gruppo, il peering può attraversare subnet interne tra i dispositivi che appartengono allo stesso gruppo, inclusi i dispositivi in uffici remoti. Usare l'opzione [ID gruppo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) per creare un gruppo personalizzato indipendentemente da domini e siti di Active Directory Domain Services. La modalità di download di gruppo è l'opzione consigliata per la maggior parte delle organizzazioni che vuole ottenere la massima ottimizzazione della larghezza di banda con Ottimizzazione recapito.

La configurazione manuale di questi ID di gruppo è difficile in caso di roaming dei client tra reti diverse. In Configuration Manager versione 1802 è stata aggiunta una nuova funzionalità per semplificare la gestione di questo processo tramite l'[integrazione di gruppi di limiti con Ottimizzazione recapito](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Quando un client viene riattivato, comunica con il punto di gestione per ottenere i criteri e fornisce informazioni sulla rete e il gruppo di limiti di appartenenza. Configuration Manager crea un ID univoco per ogni gruppo di limiti. Il sito usa le informazioni sulla posizione del client per configurare automaticamente l'ID del gruppo di Ottimizzazione recapito del client con l'ID del limite di Configuration Manager. Quando il client si sposta in un altro gruppo di limiti, comunica con il punto di gestione e viene automaticamente riconfigurato con un nuovo ID di gruppo di limiti. Grazie a questa integrazione, Ottimizzazione recapito può usare le informazioni sul gruppo di limiti di Configuration Manager per trovare un peer da cui scaricare gli aggiornamenti.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> Ottimizzazione recapito a partire dalla versione 1910
<!--4699118-->
A partire da Configuration Manager versione 1910, è possibile usare Ottimizzazione recapito per la distribuzione di tutti i contenuti di Windows Update, non solo dei file di installazione rapida, per i client che eseguono Windows 10 versione 1709 o successiva.

Per usare Ottimizzazione recapito per tutti i file di installazione di Windows Update, abilitare le [impostazioni client per gli aggiornamenti software](../../core/clients/deploy/about-client-settings.md#software-updates) seguenti:

- Impostare **Consenti ai client di scaricare contenuto differenziale quando disponibile** su **Sì**.
- Impostare **Porta usata dai client per ricevere richieste per contenuto differenziale** su 8005 (impostazione predefinita) o un numero di porta personalizzato.

> [!IMPORTANT]
> - La funzionalità Ottimizzazione del recapito deve essere abilitata (impostazione predefinita) e non ignorata. Per altre informazioni, vedere [Ottimizzazione recapito di Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference).
> - Verificare le [impostazioni client di Ottimizzazione recapito](../../core/clients/deploy/about-client-settings.md#delivery-optimization) quando si modificano le [impostazioni client degli aggiornamenti software](../../core/clients/deploy/about-client-settings.md#software-updates) per il contenuto delta.
> - Non è possibile usare Ottimizzazione recapito per gli aggiornamenti del client di Microsoft 365 Apps se è abilitato Office COM. Office COM viene usato da Configuration Manager per gestire gli aggiornamenti per i client di Microsoft 365 Apps. È possibile annullare la registrazione di Office COM per consentire l'uso di Ottimizzazione recapito per gli aggiornamenti di Microsoft 365 Apps. Quando Office COM è disabilitato, gli aggiornamenti software per Microsoft 365 Apps vengono gestiti dall'attività pianificata predefinita di Aggiornamenti automatici di Office 2.0. Ciò significa che Configuration Manager non impone né monitora il processo di installazione per gli aggiornamenti di Microsoft 365 Apps. Configuration Manager continuerà a raccogliere informazioni dall'inventario hardware per popolare il dashboard di gestione client di Office 365 nella console. Per informazioni su come annullare la registrazione di Office COM, vedere l'argomento sull'[abilitazione dei client di Office 365 al ricevimento di aggiornamenti dalla rete CDN di Office anziché da Configuration Manager](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - Quando si usa un CMG per l'archiviazione del contenuto, il contenuto per gli aggiornamenti di terze parti non viene scaricato nei client se è abilitata l'[impostazione client](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Consenti ai client di scaricare contenuto differenziale quando disponibile**. <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Peer cache di Configuration Manager

La [peer cache](../../core/plan-design/hierarchy/client-peer-cache.md) è una funzionalità di Configuration Manager che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale di Configuration Manager. La peer cache non sostituisce l'uso di altre soluzioni di peer caching come Windows BranchCache. Collabora infatti con queste soluzioni per offrire ulteriori opzioni per estendere le soluzioni tradizionali di distribuzione del contenuto, ad esempio i punti di distribuzione. La peer cache non si basa su BranchCache. Se si non abilita o non si usa BranchCache, la peer cache funziona comunque.

> [!NOTE]  
> I client possono scaricare il contenuto solo dai client della peer cache inclusi nel relativo gruppo di limiti corrente.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) è una tecnologia di ottimizzazione della larghezza di banda in Windows. Ogni client ha una cache e funge da origine alternativa per il contenuto. I dispositivi nella stessa rete possono richiedere questo contenuto. [Configuration Manager può usare BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) per consentire ai peer di operare reciprocamente come origine del contenuto, invece di dover sempre contattare un punto di distribuzione. Con BranchCache, i file vengono memorizzati nella cache in ogni singolo client e gli altri client possono recuperarli all'occorrenza. Questo approccio consente di distribuire la cache invece di usare un singolo punto di recupero. Con questo comportamento è possibile risparmiare una notevole quantità di larghezza di banda, riducendo contemporaneamente i tempi richiesti per la ricezione del contenuto richiesto nei client.



## <a name="selecting-the-right-peer-caching-technology"></a>Selezione della tecnologia di peer caching appropriata

La selezione della tecnologia di peer caching appropriata per i file di installazione rapida dipende dall'ambiente e dai requisiti. Anche se Configuration Manager supporta tutte le tecnologie peer-to-peer sopra indicate, è consigliabile usare quelle più appropriate per l'ambiente specifico. Per la maggior parte dei clienti, presupponendo che i client possano soddisfare i requisiti di Internet per Ottimizzazione recapito, la tecnologia di peer caching inclusa in Windows 10 con Ottimizzazione recapito dovrebbe essere sufficiente. Se i client non soddisfano questi requisiti per Internet, è consigliabile usare la funzionalità di peer cache di Configuration Manager. Se si usa BranchCache con Configuration Manager e questa combinazione soddisfa tutte le esigenze, i file di installazione rapida con BranchCache potrebbero essere l'opzione più appropriata. 

### <a name="peer-cache-comparison-chart"></a>Grafico di confronto di peer cache


| Funzionalità  | Ottimizzazione recapito  | Peer cache  | BranchCache  |
|---------|---------|---------|---------|
| Supportata tra subnet diverse | Sì | Sì | No |
| Limitazione larghezza di banda | Sì (nativa) | Sì (tramite BITS) | Sì (tramite BITS) |
| Supporto del contenuto parziale | Sì, per tutti i tipi di contenuto supportati elencati nella riga successiva di questa colonna. | Solo per Microsoft 365 Apps e gli aggiornamenti rapidi | Sì, per tutti i tipi di contenuto supportati elencati nella riga successiva di questa colonna. |
| Tipi di contenuto supportati | **Tramite ConfigMgr:** </br> - Aggiornamenti rapidi </br> - Tutti gli aggiornamenti di Windows (a partire dalla versione 1910) Non sono inclusi gli aggiornamenti di Microsoft 365 Apps.</br> </br> **Tramite Microsoft Cloud:**</br> - Windows e aggiornamenti della sicurezza</br> - Driver</br> - App di Windows Store</br> - App di Windows Store per le aziende | Tutti i tipi di contenuto ConfigMgr, incluse le immagini scaricate in [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | Tutti i tipi di contenuto di ConfigMgr, ad eccezione delle immagini |
| Controllo delle dimensioni della cache su disco | Sì | Sì | Sì |
| Individuazione di un'origine peer | Automatico | Manuale (impostazione agente client) | Automatico |
| Individuazione peer | Tramite il servizio cloud Ottimizzazione recapito (richiede l'accesso a Internet) | Tramite il punto di gestione (basato su gruppi di limiti client) | Multicast |
| Reporting | Sì (tramite Desktop Analytics) | Dashboard Origini dati del client di ConfigMgr | Dashboard Origini dati del client di ConfigMgr |
| Controllo dell'utilizzo WAN | Sì (nativa e controllabile tramite impostazioni di Criteri di gruppo) | Gruppi di limiti | Solo supporto subnet |
| Gestione tramite ConfigMgr | Parziale (impostazione agente client) | Sì (impostazione agente client) | Sì (impostazione agente client) |



## <a name="conclusion"></a>Conclusione

Microsoft consiglia di ottimizzare il recapito degli aggiornamenti qualitativi di Windows 10 usando Configuration Manager con file di installazione rapida e una tecnologia di peer caching, a seconda delle esigenze. Questo approccio dovrebbe risolvere le problematiche associate al download nei dispositivi Windows 10 di contenuto di grandi dimensioni per l'installazione degli aggiornamenti qualitativi. È anche consigliabile mantenere i dispositivi Windows 10 aggiornati tramite la distribuzione degli aggiornamenti qualitativi ogni mese. Questa pratica riduce il delta del contenuto degli aggiornamenti qualitativi necessari per i dispositivi ogni mese. Con la riduzione del delta del contenuto si ottengono download di dimensioni più piccole dai punti di distribuzioni o dalle origini peer. 

A causa della natura dei file di installazione rapida, le dimensioni del contenuto sono decisamente superiori rispetto al contenuto tradizionale dei file completi. Queste dimensioni comportano tempi più lunghi per il download degli aggiornamenti dal servizio Windows Update al server del sito di Configuration Manager. Aumenta anche la quantità di spazio su disco necessaria sia per il server del sito che per i punti di distribuzione. Il tempo totale necessario per scaricare e distribuire gli aggiornamenti qualitativi potrebbe essere più lungo. Tuttavia, i vantaggi a livello dei dispositivi dovrebbero essere notevoli durante il download e l'installazione degli aggiornamenti qualitativi per i dispositivi Windows 10. Per altre informazioni, vedere [Uso di file di installazione rapida](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files).

Se il maggiore carico a livello di server per gli aggiornamenti di dimensioni maggiori non è sostenibile per l'adozione del supporto dell'installazione rapida, ma i vantaggi a livello di dispositivi sono cruciali per le attività aziendali e l'ambiente, Microsoft consiglia di usare [Windows Update for Business](integrate-windows-update-for-business-windows-10.md) con Configuration Manager. Windows Update for Business offre tutti i vantaggi dell'installazione rapida senza la necessità di scaricare, archiviare e distribuire i file di installazione rapida in tutto l'ambiente. I client scaricano il contenuto direttamente dal servizio Windows Update e in questo modo possono comunque usare Ottimizzazione recapito.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Domande frequenti

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>In quale modo i download rapidi di Windows interagiscono con Configuration Manager?

L'agente di Windows Update (WUA) richiede prima di tutto il contenuto dell'aggiornamento rapido. Se non riesce a installare l'aggiornamento rapido, può tornare all'aggiornamento dei file completo.  

1. Il client di Configuration Manager indica all'agente di Windows Update di scaricare il contenuto dell'aggiornamento. Quando l'agente di Windows Update avvia un download rapido, scarica prima di tutto uno stub (ad esempio, `Windows10.0-KB1234567-<platform>-express.cab`), che fa parte del pacchetto dell'aggiornamento rapido.  

2. L'agente di Windows Update passa lo stub al programma di installazione dell'aggiornamento di Windows, per la manutenzione pacchetti basata su componenti (CBS, Component-Based Servicing). CBS usa lo stub per eseguire un inventario locale, confrontando i delta del file nel dispositivo con quello che occorre per ottenere la versione più recente del file che viene offerto.  

3. CBS richiede quindi all'agente di Windows Update di scaricare gli intervalli necessari da uno o più file di installazione rapida con estensione psf.  

4. Se Ottimizzazione recapito è abilitata e vengono individuati peer con gli intervalli necessari, il client eseguirà il download da peer indipendentemente dal client ConfigMgr. Se Ottimizzazione recapito è disabilitata o nessun peer ha gli intervalli necessari, il client ConfigMgr scaricherà questi intervalli da un punto di distribuzione locale (o da un peer o da Microsoft Update). Gli intervalli vengono passati all'agente di Windows Update che li rende disponibili a CBS per l'applicazione.


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Perché i file di installazione rapida (psf) sono grandi quando sono archiviati nelle origini peer di Configuration Manager nella cartella ccmcache?

I file di installazione rapida (psf) sono file sparse. Per determinare lo spazio effettivo usato su disco dal file, vedere la proprietà **Dimensioni su disco** del file. La proprietà Dimensioni su disco dovrebbe essere notevolmente inferiore rispetto al valore Dimensioni.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Configuration Manager supporta i file di installazione rapida con gli aggiornamenti delle funzionalità di Windows 10?

No, Configuration Manager supporta attualmente solo i file di installazione rapida con gli aggiornamenti qualitativi di Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Quanto spazio su disco è necessario per ogni aggiornamento qualitativo nel server del sito e nei punti di distribuzione?

Dipende. Per ogni aggiornamento qualitativo, nel server vengono archiviate sia la versione con file completi che la versione rapida dell'aggiornamento. Gli aggiornamenti qualitativi di Windows 10 sono cumulativi, quindi le dimensioni di questi file aumentano ogni mese. Prevedere un minimo di 5 GB per ogni aggiornamento per ogni lingua. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>I client di Configuration Manager possono comunque trarre vantaggio dai file di installazione rapida in caso di fallback al servizio Windows Update?

Sì. Se si usa l'opzione per la distribuzione degli aggiornamenti software seguente, i client possono comunque usare gli aggiornamenti rapidi e Ottimizzazione recapito in caso di fallback al servizio cloud:  

**Se gli aggiornamenti software non sono disponibili nel punto di distribuzione nei gruppi di limiti correnti, vicini o del sito, scaricare il contenuto da Microsoft Updates**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Perché il contenuto dei file di installazione rapida non viene scaricato per gli aggiornamenti esistenti dopo aver abilitato il supporto dei file di installazione rapida? 

Le modifiche diventano effettive solo per gli eventuali nuovi aggiornamenti sincronizzati e distribuiti dopo l'abilitazione del supporto.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>È disponibile un modo per visualizzare la quantità di contenuto scaricato dai peer con Ottimizzazione recapito?
Windows 10, versione 1703 (e versioni successive) include due nuovi cmdlet di PowerShell, **Get-DeliveryOptimizationPerfSnap** e **Get-DeliveryOptimizationStatus**. Questi cmdlet forniscono informazioni dettagliate su Ottimizzazione recapito e l'utilizzo della cache. Per altre informazioni, vedere [Ottimizzazione recapito per aggiornamenti Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>In quale modo i client comunicano con Ottimizzazione recapito in rete?
Per altre informazioni su porte di rete, requisiti proxy e nomi host per i firewall, vedere [Domande frequenti per Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>File di registro

Per monitorare i download delta, usare i file di registro seguenti:

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>Passaggi successivi

- [Distribuire gli aggiornamenti software](deploy-software-updates.md)
- [Distribuire automaticamente gli aggiornamenti software](automatically-deploy-software-updates.md)
