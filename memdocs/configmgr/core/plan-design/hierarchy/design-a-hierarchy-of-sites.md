---
title: Progettare la gerarchia di un sito
titleSuffix: Configuration Manager
description: Comprendere le topologie disponibili e le opzioni di gestione di Configuration Manager per pianificare la gerarchia del sito.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e14cf57e962d7bc90cc39db9ecfea68d9c5b00e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073348"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Progettare una gerarchia di siti per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di installare il primo sito di una nuova gerarchia di Configuration Manager, è consigliabile conoscere:  

- Le topologie disponibili per Configuration Manager  

- I tipi di siti disponibili e le relazioni tra di loro  

- L'ambito di gestione previsto da ogni tipo di sito  

- Le opzioni di gestione del contenuto che consentono di ridurre il numero di siti da installare  

Sarà quindi possibile pianificare una topologia che soddisfi in modo efficiente le attuali esigenze aziendali e possa espandersi in un secondo tempo per gestire la crescita futura.  

Durante la pianificazione, tenere presenti le limitazioni sull'aggiunta di siti a una gerarchia o a un sito autonomo:  

- È possibile installare un nuovo sito primario in un sito di amministrazione centrale, fino al [numero supportato di siti primari](../configs/size-and-scale-numbers.md) per la gerarchia.  

- È possibile [espandere un sito primario autonomo per installare un nuovo sito di amministrazione centrale](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand), per installare quindi altri siti primari.  

- È possibile installare nuovi siti secondari in un sito primario, fino ai [limiti supportati per il sito primario](../configs/size-and-scale-numbers.md) e la gerarchia globale.  

- Non è possibile aggiungere a una gerarchia esistente un sito installato in precedenza per unire due siti autonomi. Configuration Manager supporta solo l'installazione di nuovi siti in una gerarchia di siti esistente.  


> [!NOTE]  
> Quando si pianifica una nuova installazione di Configuration Manager, è necessario conoscere le [note sulla versione](../../servers/deploy/install/release-notes.md) in cui sono descritti nel dettaglio i problemi delle versioni attive. Le note sulla versione si applicano a tutti i rami di Configuration Manager. Quando si usa il ramo [Technical Preview](../../get-started/technical-preview.md), nella documentazione si troveranno i problemi specifici di tale ramo per ciascuna versione della Technical Preview.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a> Topologia di gerarchia  

Le topologie di gerarchia vanno da:  

- Topologia più semplice: un singolo sito primario autonomo  

- Topologia più complessa: un gruppo di siti primari e secondari connessi a un sito di amministrazione centrale nel livello superiore della gerarchia  

Gli elementi determinanti per stabilire il tipo e il numero di siti da usare in una gerarchia sono in genere il numero e il tipo di dispositivi che è necessario supportare.   

### <a name="standalone-primary-site"></a>Sito primario autonomo

Usare un sito primario autonomo quando un singolo sito primario è in grado di supportare la gestione di tutti i dispositivi e tutti gli utenti. Per altre informazioni, vedere la sezione relativa ai [numeri di ridimensionamento e scalabilità](../configs/size-and-scale-numbers.md). Questa topologia funziona anche quando le sedi geografiche aziendali possono essere gestite da un singolo sito primario. Per semplificare la gestione del traffico di rete, è possibile usare più punti di gestione nei gruppi di limiti e un'infrastruttura di contenuto accuratamente pianificata. Per altre informazioni, vedere [Configurare gruppi di limiti](../../servers/deploy/configure/boundary-groups.md) e [Concetti di base per la gestione dei contenuti](fundamental-concepts-for-content-management.md).  

Questa topologia offre i vantaggi seguenti:  

- Carico amministrativo semplificato  

- Semplifica l'assegnazione del sito client e l'individuazione di servizi e risorse disponibili  

- Eliminazione dei possibili ritardi introdotti dalla replica di database tra siti  

- Opzione per espandere un sito primario autonomo in una gerarchia più ampia con un sito di amministrazione centrale. Questa opzione consente di installare quindi nuovi siti primari per espandere la distribuzione.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Sito di amministrazione centrale con uno o più siti primari figlio 

Usare questa topologia quando sono necessari più siti primari per supportare la gestione di tutti gli utenti e i dispositivi. È obbligatoria quando è necessario usare più di un singolo sito primario. 

Questa topologia offre i vantaggi seguenti:  

- Supporta fino a 25 siti primari, consentendo di espandere la gerarchia.    

- Si usa sempre il sito di amministrazione centrale, se non si reinstallano i siti. Questa opzione è permanente. Non è possibile scollegare un sito primario figlio per trasformarlo in un sito primario autonomo.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> Determinare quando usare un sito di amministrazione centrale  

Usare un sito di amministrazione centrale per configurare le impostazioni a livello di gerarchia e per monitorare tutti i siti e gli oggetti nella gerarchia. Questo tipo di sito non gestisce i client direttamente ma coordina la replica dei dati tra i siti, che include la configurazione di siti e client in tutta la gerarchia.  

Le informazioni seguenti possono essere utili per decidere quando installare un sito di amministrazione centrale:  

- Il sito di amministrazione centrale è il sito di livello superiore nella gerarchia.  

- Quando si configura una gerarchia con più di un sito primario, installare un sito di amministrazione centrale.  

     - Se servono due o più siti primari immediatamente, installare innanzitutto il sito di amministrazione centrale.  

     - Quando si ha già un sito primario e si vuole quindi installare un sito di amministrazione centrale, [espandere il sito primario autonomo](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) per installare il sito di amministrazione centrale.  

- Il sito di amministrazione centrale supporta solo i siti primari come siti figlio.  

- Al sito di amministrazione centrale non è possibile assegnare client.  

- Il sito di amministrazione centrale non supporta i ruoli del sistema del sito che supportano direttamente i client, come punti di gestione e punti di distribuzione.  

- È possibile gestire tutti i client nella gerarchia ed eseguire tutte le attività di gestione del sito dalla console di Configuration Manager connessa al sito di amministrazione centrale. Queste attività includono l'installazione di punti di gestione o altri ruoli del sistema del sito in siti figlio primari o secondari.  

- Quando si usa un sito di amministrazione centrale, questo è l'unico punto da cui è possibile visualizzare i dati del sito da tutti i siti nella gerarchia. Questi dati includono informazioni quali dati di inventario e messaggi di stato.  

- È possibile configurare le operazioni di individuazione in tutta la gerarchia dal sito di amministrazione centrale. Da tale sito, assegnare metodi di individuazione da eseguire nei singoli siti primari.  

- È possibile gestire la protezione in tutta la gerarchia mediante l'assegnazione di raccolte, ambiti di protezione e ruoli di sicurezza differenti a diversi utenti amministratori. Queste configurazioni si applicano a ogni sito nella gerarchia.  

- È possibile configurare la replica per controllare la comunicazione tra siti all'interno della gerarchia, pianificare la replica di database per i dati del sito e gestire la larghezza di banda per il trasferimento tra siti di dati basati su file.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> Determinare quando usare un sito primario  

Utilizzare i siti primari per gestire i client. Installare un sito primario come sito figlio al di sotto di un sito di amministrazione centrale oppure come primo sito di una nuova gerarchia. Un sito primario che è il primo sito di una gerarchia crea un sito primario autonomo. Sia i siti primari figlio che i siti primari autonomi supportano siti secondari.  

È consigliabile aggiungere altri siti primari per i motivi seguenti:  

- Per aumentare il numero di dispositivi e gestirli con una singola gerarchia.  

- Per soddisfare i requisiti di gestione dell'organizzazione. Ad esempio, è possibile installare un sito primario in una posizione remota per gestire il trasferimento del contenuto di distribuzione attraverso una rete a larghezza di banda ridotta.  

     - È tuttavia possibile usare opzioni per limitare l'uso della larghezza di banda di rete in fase di trasferimento dei dati a un punto di distribuzione. Questa funzionalità di gestione dei contenuti può sostituire la necessità di installare ulteriori siti.  


Le informazioni seguenti possono essere utili per decidere quando installare un sito primario:  

- Un sito primario può essere un sito primario autonomo o un sito primario figlio in una gerarchia più grande. Quando un sito primario è membro di una gerarchia con un sito di amministrazione centrale, i siti utilizzano la replica database per replicare i dati tra i siti. Ad eccezione del caso in cui non sia necessario supportare più client e dispositivi rispetto alla capacità di un singolo sito primario, considerare l'installazione di un sito primario autonomo. Dopo l'installazione di un sito primario autonomo, è possibile espanderlo in futuro, se necessario, in modo che faccia riferimento a un nuovo sito di amministrazione centrale per potenziare la distribuzione.  

- Un sito primario supporta solo un sito di amministrazione centrale come sito padre.  

- Un sito primario supporta solo siti secondari come siti figlio e può supportarne più d'uno.  

- I siti primari sono responsabili dell'elaborazione di tutti i dati client dei client ad essi assegnati.  

- I siti primari utilizzano la replica di database per comunicare direttamente con il relativo sito di amministrazione centrale. Questo comportamento viene configurato automaticamente quando si installa un nuovo sito.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> Determinare quando usare un sito secondario  

Utilizzare i siti secondari per gestire il trasferimento dei dati client e del contenuto di distribuzione su reti a larghezza di banda ridotta.  

Un sito secondario viene gestito da un sito di amministrazione centrale o dal sito primario padre diretto del sito secondario. I siti secondari sono collegati a un sito primario. Non è possibile spostarli in un sito padre diverso senza prima disinstallarli e successivamente reinstallarli come siti figlio del nuovo sito primario.

È comunque possibile distribuire contenuto tra due siti secondari peer per gestire la replica basata su file del contenuto della distribuzione. Per trasferire i dati client a un sito primario, il sito secondario utilizza la replica basata su file. Un sito secondario usa anche la replica di database per comunicare con il relativo sito primario padre.  

Si consiglia di installare un sito secondario in presenza di una delle seguenti condizioni:  

- Non è necessario un punto di connettività locale per un utente amministratore.  

- È necessario gestire il trasferimento del contenuto della distribuzione ai siti di livello inferiore nella gerarchia.  

- È necessario gestire le informazioni sui client inviate ai siti di livello superiore nella gerarchia.  

Se non si vuole installare un sito secondario e si dispone di client in sedi remote, prendere in considerazione le opzioni seguenti:  

- Uso di tecnologie peer-to-peer come Windows BranchCache  

- Abilitazione di punti di distribuzione per il controllo e la pianificazione della larghezza di banda   

È possibile usare queste opzioni di gestione dei contenuti con o senza siti secondari, per ridurre le dimensioni dell'infrastruttura di Configuration Manager. Per altre informazioni sulle opzioni di gestione dei contenuti in Configuration Manager, vedere [Determinare quando usare le opzioni di gestione dei contenuti](#BKMK_ChooseSecondaryorDP).  


Le informazioni seguenti possono essere utili per decidere quando installare un sito secondario:  

- Se non è disponibile un'istanza locale di SQL Server, i server dei siti secondari installano automaticamente SQL Server Express durante l'installazione del sito.  

- L'installazione del sito secondario viene avviata dalla console di Configuration Manager, invece che dal programma di installazione eseguito direttamente in un computer.  

- I siti secondari usano un subset delle informazioni nel database del sito. In questo modo si riduce la quantità di dati replicati da SQL tra il sito primario padre e il sito secondario.  

- I siti secondari supportano il routing del contenuto basato su file in altri siti secondari che dispongono di un sito primario padre comune.  

- Le installazioni dei siti secondari installano automaticamente i ruoli del sistema del sito punto di gestione e punto di distribuzione sul server del sito secondario.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> Determinare quando usare le opzioni di gestione dei contenuti  

Se si dispone di client in percorsi di rete remoti, considerare l'utilizzo di una o più opzioni di gestione dei contenuti piuttosto che di un sito primario o secondario. Le opzioni seguenti spesso eliminano la necessità di installare un sito:  

- Ottimizzazione recapito per Windows 10  

- Peer cache di Configuration Manager  

- Windows BranchCache  

- Configurazione di punti di distribuzione per il controllo della larghezza di banda  

- Copia manuale del contenuto nei punti di distribuzione (pre-installazione del contenuto)  


Considerare la distribuzione di un punto di distribuzione piuttosto che l'installazione di un altro sito in presenza di una delle condizioni seguenti:  

- La larghezza di banda della rete è sufficiente per consentire ai computer client in remoto di comunicare con un punto di gestione nel sito primario. I client comunicano con un punto di gestione per scaricare i criteri client e inviare informazioni di individuazione, di inventario e relative allo stato dei report.  

- Il Servizio trasferimento intelligente in background (BITS) non garantisce un controllo della larghezza di banda adeguato ai requisiti della rete.  

Per altre informazioni sulle opzioni di gestione dei contenuti in Configuration Manager, vedere [Concetti di base per la gestione dei contenuti](fundamental-concepts-for-content-management.md).  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> Oltre la topologia di gerarchia  

Oltre alla topologia di gerarchia iniziale, considerare anche le domande seguenti:  

- Quali ruoli del sistema del sito forniscono servizi o funzionalità dai diversi siti della gerarchia?  

- Come verranno gestite nell'infrastruttura le configurazioni e le funzionalità valide per l'intera gerarchia?  


Le considerazioni comuni seguenti sono trattate in articoli separati. Queste informazioni sono importanti perché possono influenzare la progettazione della gerarchia o esserne influenzate:  

- Quando si prepara la [gestione di computer e dispositivi](../../clients/manage/manage-clients.md), valutare se i dispositivi si trovano nell'infrastruttura locale, nel cloud o includono dispositivi di proprietà degli utenti (BYOD). Valutare anche come gestire i dispositivi che supportano più opzioni di gestione, ad esempio se gestire i computer Windows 10 con Configuration Manager o tramite l'integrazione con Microsoft Intune. Per altre informazioni, vedere [Scegliere una soluzione di gestione dei dispositivi](../choose-a-device-management-solution.md).  

- Comprendere gli effetti dell'infrastruttura di rete disponibile sul flusso di dati tra sedi remote. Per altre informazioni, vedere l'articolo sulla [preparazione dell'ambiente di rete](../network/configure-firewalls-ports-domains.md). Considerare anche la posizione geografica degli utenti e dei dispositivi da gestire e se l'accesso all'infrastruttura avviene dalla rete locale o da Internet.  

- Pianificare un'infrastruttura del contenuto per distribuire in modo efficiente il contenuto ai dispositivi gestiti. Il contenuto include applicazioni, aggiornamenti software e sistemi operativi. Per altre informazioni, vedere [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto).  

- Determinare quali [caratteristiche e funzionalità di Configuration Manager](../changes/features-and-capabilities.md) si intende usare. Caratteristiche diverse richiedono diversi ruoli del sistema del sito o una diversa infrastruttura di Windows. In una gerarchia a più siti, decidere dove distribuirle per ottimizzare l'uso delle risorse di rete e dei server.  

- Considerare la sicurezza per i dati e i dispositivi, incluso l'uso di un'infrastruttura a chiave pubblica (PKI). Per altre informazioni, vedere [requisiti dei certificati PKI](../network/pki-certificate-requirements.md).  


Vedere gli articoli seguenti per le configurazioni specifiche del sito:  

- [Pianificare per il provider SMS](plan-for-the-sms-provider.md)  

- [Pianificare per il database del sito](plan-for-the-site-database.md)  

- [Pianificare i server e i ruoli del sistema del sito](plan-for-site-system-servers-and-site-system-roles.md)  

- [Pianificare la sicurezza](../security/plan-for-security.md)  

- [Managing network bandwidth](manage-network-bandwidth.md) durante la distribuzione dei contenuti all'interno di un sito  


Prendere in considerazione configurazioni che si estendono a più siti e gerarchie  

- [High availability options](../../servers/deploy/configure/high-availability-options.md) (Opzioni di disponibilità elevata) per siti e gerarchie

- [Estendere lo schema di Active Directory](../network/extend-the-active-directory-schema.md) e configurare i siti per [pubblicare i dati del sito](../../servers/deploy/configure/publish-site-data.md)  

- [Trasferimenti di dati tra siti](data-transfers-between-sites.md)  

- [Nozioni fondamentali sull'amministrazione basata su ruoli](../../understand/fundamentals-of-role-based-administration.md)  

- [Gestire i client su Internet](../../clients/manage/manage-clients-internet.md)  

