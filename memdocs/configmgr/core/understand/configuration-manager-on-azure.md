---
title: Configuration Manager in Azure
titleSuffix: Configuration Manager
description: Informazioni sull'uso di Configuration Manager in un ambiente Azure.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9d398d7fddab61014547fc0f8f64cd180e58ab6
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438569"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager in Azure: domande frequenti

*Si applica a: Configuration Manager (Current Branch)*

Le domande e le risposte seguenti possono aiutare a capire quando usare e come configurare Configuration Manager in Microsoft Azure.

## <a name="general-questions"></a>Domande generali
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>L'azienda sta cercando di trasferire il maggior numero possibile di server fisici in Microsoft Azure; è possibile trasferire i server di Configuration Manager in Azure?
Questo scenario è ovviamente supportato.  Vedere [Supporto per gli ambienti di virtualizzazione per Configuration Manager](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Ottimo. L'ambiente richiede più siti. Tutti i siti primari figlio devono essere presenti in Azure con il sito di amministrazione centrale o locale? Qual è l'approccio da seguire per i siti secondari?
Le comunicazioni da sito a sito (replica di database e basata su file) traggono vantaggio dalla prossimità dei siti ospitati in Azure. Tuttavia, tutto il traffico correlato ai client sarebbe remoto dai server del sito e dai sistemi del sito. Se si usa una connessione di rete veloce e affidabile tra Azure e la rete Intranet con un piano dati illimitato, un'opzione possibile è l'hosting dell'intera infrastruttura in Azure.

Se invece si usa un piano dati a consumo e i costi e la larghezza di banda disponibile sono fattori da valutare con attenzione oppure se la connessione di rete tra Azure e la rete Intranet non è veloce o potrebbe non essere affidabile, è consigliabile inserire siti specifici (e i sistemi del sito) in locale e usare i controlli relativi alla larghezza di banda integrati in Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Configuration Manager in Azure implementa uno scenario SaaS (Software come servizio)?
No, si tratta di un servizio IaaS (Infrastruttura come servizio) perché i server di infrastruttura di Configuration Manager vengono ospitati nelle macchine virtuali di Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>A quali aree è necessario prestare attenzione quando si valuta la scelta di trasferire l'infrastruttura di Configuration Manager in Azure?
Ottima domanda. Di seguito sono indicate le aree più importanti nell'ottica di questa decisione; ogni area viene esaminata in una sezione separata di questo argomento:
1. Rete
2. Disponibilità
3. Prestazioni
4. Costi
5. Esperienza dell'utente

## <a name="networking"></a>Rete
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Per quanto riguarda i requisiti di rete, è opportuno usare un Gateway VPN di Azure o ExpressRoute?
Questa decisione molto importante. Le velocità e la latenza di rete possono influire sulle funzionalità tra il server del sito e i sistemi del sito remoti e sulle comunicazione client ai sistemi del sito. È consigliabile usare ExpressRoute. Configuration Manager non prevede tuttavia limitazioni all'uso del Gateway VPN di Azure. È opportuno esaminare attentamente i requisiti specifici, come prestazioni, applicazione di patch, distribuzione del software e distribuzione di sistemi operativi, di questa infrastruttura e adottare la scelta più appropriata di conseguenza. Ecco alcuni aspetti da valutare per ogni soluzione:

- **ExpressRoute** (scelta consigliata)
  - Estensione naturale per il data center, ovvero la possibilità di unire più data center
  - Connessioni private tra i data center di Azure e l'infrastruttura
  - Mancato uso della rete Internet pubblica
  - Garanzia di affidabilità, velocità elevate, latenza inferiore ed elevata sicurezza
  - Velocità fino a 10 Gb/s e opzioni del piano dati illimitato
- **Gateway VPN**
  - VPN da sito a sito/da punto a sito
  - Traffico gestito tramite la rete Internet pubblica
  - Uso di Internet Protocol Security (IPsec) e Internet Key Exchange (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute offre molte opzioni, come il piano dati a consumo e quello illimitato, diverse velocità e un componente aggiuntivo Premium. Qual è l'opzione migliore?
La scelta delle opzioni dipende dallo scenario da implementare e dalla quantità di dati da distribuire. È possibile controllare il trasferimento di dati di Configuration Manager tra i server del sito e i punti di distribuzione, ma non è possibile controllare la comunicazione tra server del sito.   Quando si usa un piano dati a consumo, l'inserimento di siti specifici (e sistemi del sito) in locale e l'uso di [controlli relativi alla larghezza di banda predefiniti di Configuration Manager](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) consentono di mantenere sotto controllo i costi associati all'uso di Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Quali sono i requisiti di installazione, ad esempio per i domini di Active Directory? È necessario aggiungere i server del sito in un dominio di Active Directory?
Sì. Quando si esegue il trasferimento in Azure, le [configurazioni supportate](../plan-design/configs/supported-configurations.md) rimangono invariate, inclusi i requisiti di Active Directory per l'installazione di Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Sono consapevole del fatto che sia necessario aggiungere i server del sito in un dominio di Active Directory. È possibile usare Azure Active Directory?
No, Azure Active Directory non è supportato attualmente. Tutti i server del sito devono essere membri di un [dominio di Active Directory di Windows](../plan-design/configs/support-for-active-directory-domains.md).



## <a name="availability"></a>Disponibilità
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Uno dei motivi del trasferimento dell'infrastruttura in Azure è la disponibilità elevata assicurata. È possibile sfruttare i vantaggi associati alle opzioni di disponibilità elevata, come i set di disponibilità di VM di Azure per le VM che verranno usate per Configuration Manager?
Sì. I set di disponibilità di VM di Azure possono essere usati per i ruoli ridondanti del sistema del sito, come i punti di distribuzione o i punti di gestione.

È possibile anche usarli per i server del sito di Configuration Manager. Ad esempio, i siti di amministrazione centrale e i siti primari possono tutti essere inclusi nello stesso set di disponibilità, in modo da garantire che non vengano riavviati nello stesso momento.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Come è possibile rendere il database a disponibilità elevata? È possibile usare il database SQL di Azure? In alternativa è necessario usare Microsoft SQL Server in una VM?
È necessario usare Microsoft SQL Server in una VM. Configuration Manager non supporta attualmente il server di Azure SQL. È tuttavia possibile usare funzionalità come i gruppi di disponibilità AlwaysOn per il server SQL. I [gruppi di disponibilità AlwaysOn](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) sono consigliati e supportati ufficialmente a partire dalla versione 1602 di Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>È possibile usare i servizi di bilanciamento del carico di Azure con i ruoli del sistema del sito come punti di gestione o punti di aggiornamento software?
Anche se Configuration Manager non è stato testato con i servizi di bilanciamento del carico di Azure, non dovrebbero esistere effetti negativi sulle normali operazioni, se la funzionalità è trasparente per l'applicazione.


## <a name="performance"></a>Prestazioni
### <a name="what-factors-affect-performance-in-this-scenario"></a>Quali fattori influiscono sulle prestazioni in questo scenario?
[Tipo e dimensioni della VM di Azure](/azure/virtual-machines/sizes), i dischi della VM di Azure (è consigliabile l'archiviazione Premium, in particolare per SQL Server), la latenza e le velocità di rete sono le aree più importanti.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Sono disponibili altre informazioni sulle macchine virtuali di Azure, in particolare quali dimensioni di VM è consigliabile usare?
In generale, la potenza di calcolo (CPU e memoria) deve soddisfare l'[hardware consigliato per Configuration Manager](../plan-design/configs/recommended-hardware.md). Esistono tuttavia alcune differenze tra l'hardware del computer standard e le VM di Azure, soprattutto in relazione ai dischi usati da queste VM.  Le dimensioni di VM usate dipendono dalle dimensioni dell'ambiente. Ecco alcuni consigli:
- Per le distribuzioni di produzione di dimensioni significative è consigliabile usare VM di Azure di classe "**S**" perché possono sfruttare i dischi di archiviazione Premium.  Le VM di classe "S" usano l'archiviazione BLOB e in genere non soddisfano i requisiti di prestazioni necessari per un'esperienza di produzione accettabile.
- È opportuno usare più dischi di archiviazione Premium per assicurare maggiore scalabilità, con striping nella console di Gestione disco di Windows per ottimizzare il numero di IOPS (operazioni di input/output al secondo).  
- È consigliabile usare più dischi Premium o di qualità migliore durante la distribuzione iniziale del sito (P30 anziché P20) e 2 x P30 anziché 1 x P30 in un volume con striping. Se in seguito è necessario ampliare le dimensioni della VM del sito per soddisfare carichi aggiuntivi, è possibile sfruttare la capacità aggiuntiva di CPU e memoria fornita da una VM di dimensioni maggiori. I dischi che possono sfruttare la velocità effettiva di IOPS (operazioni di input/output al secondo) aggiuntiva consentita da queste dimensioni della VM sono quindi già installati.



Le tabelle seguenti elencano i conteggi di dischi consigliati nella fase iniziale da usare nei siti di amministrazione centrali e primari per installazioni di dimensioni diverse:

**Database del sito con percorso condiviso**: il sito di amministrazione centrale o primario con il database del sito sul server del sito:

| Client desktop    |Dimensione VM consigliata|Dischi consigliati|
|--------------------|-------------------|-----------------|
|**Fino a 25.000**       |   DS4_V2          |2 x P30 (con striping)  |
|**Da 25.000 a 50.000**      |   DS13_V2         |2 x P30 (con striping)  |
|**50.000 a 100.000**     |   DS14_V2         |3 x P30 (con striping)  |


**Database del sito remoto**: il sito di amministrazione centrale o primario con il database del sito sul server remoto:

| Client desktop    |Dimensione VM consigliata|Dischi consigliati |
|--------------------|-------------------|------------------|
|**Fino a 25.000**       | Server del sito: F4S </br>Server di database: DS12_V2 | Server del sito: 1xP30 </br>Server di database: 2 x P30 (con striping)  |
|**Da 25.000 a 50.000**      | Server del sito: F4S </br>Server di database: DS13_V2 | Server del sito: 1xP30 </br>Server di database: 2 x P30 (con striping)   |
|**50.000 a 100.000**     | Server del sito: F8S </br>Server di database: DS14_V2 | Server del sito: 2 x P30 (con striping)   </br>Server di database: 3 x P30 (con striping)   |

Di seguito è riportato un esempio di configurazione per un numero di client compreso tra 50 e 100.000 su DS14_V2 con 3 dischi P30 in un volume con striping, con volumi logici separati per i file di installazione e di database di Configuration Manager: ![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>Esperienza dell'utente
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>L'esperienza utente è stata citata come una delle aree di maggiore importanza. Perché?
Le decisioni adottate relative a rete, disponibilità, prestazioni e punto in cui inserire i server del sito di Configuration Manager possono avere effetti direttamente sugli utenti. È opportuno che il trasferimento in Azure sia trasparente agli utenti in modo che non riscontrino modifiche alle proprie interazioni quotidiane con Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>Ora questo aspetto è chiaro. È prevista l'installazione di un singolo sito primario autonomo in una macchina virtuale di Azure con l'obiettivo di mantenere bassi i costi. È consigliabile inserire i sistemi del sito (remoti), come i punti di gestione, i punti di distribuzione e i punti di aggiornamento del software, su macchine virtuali di Azure oppure in locale?
Ad eccezione della comunicazione dal server del sito a un punto di distribuzione, queste comunicazioni tra server in un sito possono verificarsi in qualsiasi momento e non prevedono meccanismi per controllare l'uso della larghezza di banda di rete. Poiché non è possibile controllare la comunicazione tra sistemi del sito, è necessario considerare gli eventuali costi associati a queste comunicazioni.

Altri fattori da considerare sono la velocità e la latenza di rete. Reti lente o inaffidabili potrebbero influire sulla funzionalità tra il server del sito e i sistemi del sito remoti e sulle comunicazione client ai sistemi del sito. Altri fattori importanti sono il numero di client gestiti che usano uno specifico sistema del sito e le funzionalità più usate.
In generale, è possibile sfruttare le indicazioni standard in relazione ai collegamenti WAN e ai sistemi del sito come punto di partenza. Idealmente, la velocità effettiva di rete selezionata e ottenuta tra Azure e la rete Intranet sarà coerente con una rete WAN connessa in modo appropriato con una rete veloce.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>Qual è l'approccio alla distribuzione e alla gestione dei contenuti? I punti di distribuzione standard devono essere inseriti in Azure o in locale? È consigliabile usare BranchCache o i punti di distribuzione pull locali? In alternativa, è opportuno usare esclusivamente i punti di distribuzione del cloud?
L'approccio alla gestione dei contenuti è molto simile per i server del sito e i sistemi del sito.
- Se si usa una connessione di rete veloce e affidabile tra Azure e la rete Intranet con un piano dati illimitato, un'opzione possibile è l'hosting dei punti di distribuzione standard in Azure.
- Se si usa un piano dati a consumo e la larghezza di banda è un fattore da valutare con attenzione o la connessione di rete tra Azure e la rete Intranet non è veloce o potrebbe non essere affidabile, è consigliabile valutare altri approcci. Alcune alternative sono l'inserimento di punti di distribuzione pull o standard in locale e l'uso di BranchCache. Un'opzione possibile è l'uso di punti di distribuzione basati su cloud, ma vi sono alcuni limiti ai tipi di contenuto supportati, ad esempio non vengono supportati i pacchetti di aggiornamenti software.

> [!NOTE]
>  Se è necessario il supporto PXE o multicast, usare i punti di distribuzione (standard o pull) locali per soddisfare le richieste di avvio.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Sebbene le limitazioni relative ai punti di distribuzione basati su cloud non rappresentino un problema, non intendo inserire il punto di gestione in una rete perimetrale, anche se ciò è necessario per supportare i client basati su Internet. Sono disponibili altre opzioni?
Sì. Con Configuration Manager versione 1610, è stato introdotto il [gateway di gestione cloud](../clients/manage/manage-clients-internet.md#cloud-management-gateway) come funzionalità di versione non definitiva (introdotta inizialmente nella Technical Preview versione 1606 con il nome di [servizio proxy cloud](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)).

**Cloud Management Gateway** consente di gestire i client di Configuration Manager su Internet in modo semplice. Il servizio, che viene distribuito in Microsoft Azure e richiede una sottoscrizione di Azure, si connette all'infrastruttura di Configuration Manager locale usando un nuovo ruolo, denominato punto del connettore gateway di gestione cloud. Dopo aver completato la distribuzione e la configurazione, i client sono in grado di accedere ai ruoli del sistema del sito Configuration Manager locale, indipendentemente dal fatto che siano connessi alla rete privata interna o su Internet.

È possibile iniziare a usare il gateway di gestione cloud nel proprio ambiente e inviare commenti e suggerimenti per migliorare il servizio. Per informazioni sulle funzionalità di versioni non definitive, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Inoltre, nella versione 1610 è prevista una nuova funzionalità denominata peer cache, introdotta come funzionalità di versione non definitiva. È diversa da BranchCache? Qual è l'opzione migliore?
Sì, è completamente diversa. [Peer cache](../plan-design/hierarchy/client-peer-cache.md) è una tecnologia nativa al 100% di Configuration Manager, mentre BranchCache è una funzionalità di Windows. Entrambe possono essere utili. BranchCache usa un broadcast per trovare il contenuto richiesto mentre peer cache usa le impostazioni relative al gruppo di limiti e al flusso di lavoro di distribuzione standard di Configuration Manager.

È possibile configurare qualsiasi client come origine della peer cache. Quando i punti di gestione forniscono ai client informazioni sui percorsi di origine del contenuto, forniscono informazioni dettagliate su tutte le origini di peer cache che contengono il contenuto e i punti di distribuzione richiesti dal client.


## <a name="cost"></a>Costi
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>Quali sono i dettagli relativi ai costi? Questa soluzione sarà vantaggiosa?
È difficile da stabilire poiché ogni ambiente è diverso. L'approccio migliore è quello di calcolare il prezzo per il proprio ambiente mediante il calcolatore prezzi di Microsoft Azure: https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Risorse aggiuntive
**Nozioni fondamentali:** https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipi di VM di Azure:**
- Dimensioni delle macchine virtuali di Azure: https://docs.microsoft.com/azure/virtual-machines/sizes  
- Prezzi delle macchine virtuali: https://azure.microsoft.com/pricing/details/virtual-machines/  
- Prezzi per l'archiviazione: https://azure.microsoft.com/pricing/details/storage/

**Considerazioni sulle prestazioni dei dischi:**    
- Introduzione disco Premium: https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Informazioni disco Premium più approfondite: https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Raccolta utile di grafici per obiettivi di dimensioni e prestazioni per l'archiviazione: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Altra introduzione + dati tecnici sul funzionamento dietro le quinte di Archiviazione Premium: https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilità:**
- Contratti di servizio tempo di attività di Azure IaaS: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Set di disponibilità: https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability

**Connettività:**
- ExpressRoute e VPN di Azure: https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Prezzi di ExpressRoute: https://azure.microsoft.com/pricing/details/expressroute/
- Altre informazioni su ExpressRoute: https://azure.microsoft.com/documentation/articles/expressroute-introduction/
