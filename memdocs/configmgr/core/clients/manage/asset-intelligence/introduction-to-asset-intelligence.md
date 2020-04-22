---
title: Introduzione ad Asset Intelligence
titleSuffix: Configuration Manager
description: Usare Asset Intelligence in Configuration Manager per eseguire l'inventario delle licenze software e gestire l'utilizzo di queste in tutta l'organizzazione.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695089"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Introduzione ad Asset Intelligence in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Eseguire l'inventario delle licenze software e gestire l'utilizzo di queste in tutta l'organizzazione tramite il catalogo di Asset Intelligence. Asset Intelligence aggiunge classi di inventario hardware per ampliare la gamma di informazioni raccolte da Configuration Manager, compresi i titoli dei componenti hardware e dei programmi software usati nell'ambiente in uso. Sono disponibili più di 60 report per la presentazione di queste informazioni in un formato di facile utilizzo. Molti di questi report sono collegati a report più specifici. È possibile eseguire query per ottenere informazioni generali e usare la funzione di drill-down per informazioni più dettagliate. 

È anche possibile aggiungere informazioni personalizzate al catalogo di Asset Intelligence, ad esempio categorie, famiglie ed etichette software, nonché requisiti hardware personalizzati. Per aggiornare dinamicamente il catalogo di Asset Intelligence con le informazioni più aggiornate disponibili, è possibile connetterlo a Microsoft Cloud. 

Usare Asset Intelligence per riconciliare l'utilizzo delle licenze software dell'organizzazione. Importare le informazioni relative alle licenze software nel database del sito di Configuration Manager per visualizzarle a fronte del software in corso di utilizzo.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a> Catalogo di Asset Intelligence  

Il catalogo di Asset Intelligence è un set di tabelle di database archiviate nel database del sito. Queste tabelle, che includono informazioni di categorizzazione e identificazione per oltre 300.000 titoli e versioni software, consentono anche di gestire i requisiti hardware per titoli software specifici.  

Asset Intelligence offre le informazioni relative alle licenze software per i titoli software in uso, sia Microsoft che non Microsoft. Nel catalogo di Asset Intelligence è disponibile un set predefinito di requisiti hardware per i titoli software ed è possibile creare nuove informazioni di requisiti hardware definiti dall'utente per soddisfare requisiti personalizzati. È anche possibile personalizzare le informazioni nel catalogo di Asset Intelligence e caricare le informazioni sui titoli software personalizzati in Microsoft Cloud a scopo di categorizzazione.  

Sono disponibili aggiornamenti del catalogo di Asset Intelligence che includono informazioni sui titoli software rilasciati di recente e che possono essere scaricati periodicamente per eseguire aggiornamenti in blocco del catalogo. È anche possibile aggiornare dinamicamente il catalogo tramite il punto di sincronizzazione di Asset Intelligence.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorie software  

Le categorie software di Asset Intelligence vengono usate per categorizzare in modo generale i titoli software di inventario e come raggruppamenti generali di famiglie software più specifiche. Un esempio di categoria software potrebbe essere "aziende del settore energetico" e una famiglia software all'interno di tale categoria software potrebbe essere "petrolio e gas" o "energia idroelettrica". Nel catalogo di Asset Intelligence molte categorie software sono predefinite. È possibile creare categorie definite dall'utente per definire altro software di inventario. Lo stato di convalida di tutte le categorie software predefinite è sempre impostato su **Convalidato**. Lo stato delle informazioni delle categorie software personalizzate aggiunte al catalogo di Asset Intelligence è **Definito dall'utente**. 

Per altre informazioni su come gestire le categorie software, vedere [Configurazione di Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Le informazioni sulle categorie software predefinite archiviate nel catalogo di Asset Intelligence sono di sola lettura e non possono essere modificate o eliminate. Gli utenti amministratori possono aggiungere, modificare o eliminare categorie software definite dall'utente.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Famiglie software  

Le famiglie software di Asset Intelligence vengono usate per definire i titoli software di inventario all'interno delle categorie software. Nel catalogo di Asset Intelligence molte famiglie software sono predefinite. È possibile creare categorie definite dall'utente per definire altro software di inventario. Lo stato di convalida di tutte le famiglie software predefinite è sempre impostato su **Convalidato**. Lo stato delle informazioni delle famiglie software personalizzate aggiunte al catalogo di Asset Intelligence è **Definito dall'utente**. 

Per altre informazioni su come gestire le famiglie software, vedere [Configurazione di Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Le informazioni sulle famiglie software predefinite sono di sola lettura e non possono essere modificate. Gli utenti amministratori possono aggiungere, modificare o eliminare famiglie software definite dall'utente.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> Etichette software  

Le etichette software di Asset Intelligence personalizzate consentono di creare filtri per raggruppare i titoli software e visualizzarli nei report di Asset Intelligence. Usare le etichette software per creare gruppi definiti dall'utente di titoli software con un attributo comune. È ad esempio possibile creare l'etichetta software Shareware, associarla ai titoli shareware di inventario ed eseguire un report per visualizzare tutti i titoli software a cui l'etichetta è associata. Non ci sono etichette predefinite. Lo stato di convalida per le etichette software è sempre **Definito da utente**. 

Per altre informazioni su come gestire le etichette software, vedere [Configurazione di Asset Intelligence](configuring-asset-intelligence.md).  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisiti hardware  

Usare le informazioni sui requisiti hardware per verificare che i computer soddisfino tali requisiti per i titoli software prima di sceglierli come destinazione per le distribuzioni di software. Gestire i requisiti hardware per i titoli software nell'area di lavoro **Asset e conformità** nel nodo **Requisiti hardware** all'interno del nodo **Asset Intelligence**. 

Nel catalogo di Asset Intelligence molti requisiti hardware sono predefiniti. Creare nuove informazioni sui requisiti hardware definiti dall'utente per soddisfare requisiti personalizzati. Lo stato di convalida di tutti i requisiti hardware predefiniti è sempre impostato su **Convalidato**. Lo stato delle informazioni dei requisiti hardware personalizzati aggiunte al catalogo di Asset Intelligence è **Definito dall'utente**. 

Per altre informazioni su come gestire i requisiti hardware, vedere [Configurazione di Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> I requisiti hardware visualizzati nella console di Configuration Manager vengono recuperati dal catalogo di Asset Intelligence. Non sono basati su informazioni dei titoli software di inventario provenienti dai client. 
> 
> Le informazioni sui requisiti hardware non vengono aggiornate nell'ambito del processo di sincronizzazione con Microsoft. 
> 
> È possibile creare requisiti hardware definiti dall'utente per software di inventario senza requisiti hardware associati.  

Per impostazione predefinita, per ogni requisito hardware elencato vengono visualizzate le informazioni seguenti:  

- **Titolo software**: il titolo software associato al requisito hardware  

- **CPU minima (MHz)** : la velocità minima del processore, in megahertz (MHz), richiesta dal titolo software  

- **RAM minima (KB)** : la quantità di RAM minima, in kilobyte (KB), richiesta dal titolo software  

- **Dimensioni minime spazio su disco (KB):** : la quantità minima di spazio disponibile sul disco rigido, in KB, richiesta dal titolo software  

- **Dimensioni disco minime (KB):** : la dimensione minima del disco rigido, in KB, richiesta dal titolo software  

- **Stato convalida**: lo stato di convalida per il requisito hardware  

I requisiti hardware predefiniti archiviati nel catalogo di Asset Intelligence sono di sola lettura e non possono essere eliminati. Gli utenti amministratori possono aggiungere, modificare o eliminare i requisiti hardware definiti dall'utente per i titoli software non archiviati nel catalogo di Asset Intelligence.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> Titoli software di inventario  

Per visualizzare le informazioni sui titoli software di inventario nella console di Configuration Manager, passare all'area di lavoro **Asset e conformità**, espandere il nodo **Asset Intelligence** e selezionare il nodo **Software di inventario**. L'agente di inventario hardware raccoglie le informazioni sul software di inventario dai client di Configuration Manager in base ai titoli software archiviati nel catalogo di Asset Intelligence.  

> [!Note]  
> L'agente di inventario hardware raccoglie l'inventario in base alle classi di report di inventario hardware di Asset Intelligence abilitate dall'utente. Per altre informazioni su come abilitare le classi di report, vedere [Configurazione di Asset Intelligence](configuring-asset-intelligence.md).  

Per impostazione predefinita, per ogni titolo software di inventario vengono visualizzate le informazioni seguenti:  

- **Nome**: nome del titolo software di inventario  

- **Fornitore**: nome del fornitore che ha sviluppato il titolo software di inventario  

- **Versione**: versione del prodotto del titolo software di inventario  

- **Categoria**: categoria software attualmente assegnata al titolo software di inventario  

- **Famiglia**: famiglia software attualmente assegnata al titolo software di inventario  

- **Etichetta** [**1**, **2** e **3**]: etichette personalizzate associate al titolo software. Ai titoli software di inventario possono essere associate fino a tre etichette personalizzate.  

- **Conteggio**: numero di client di Configuration Manager che hanno il titolo software in inventario  

- **Stato**: stato di convalida per il titolo software di inventario  

> [!NOTE]  
> È possibile modificare le informazioni di categorizzazione per il software di inventario solo nel sito principale nella gerarchia. Queste informazioni includono nome del prodotto, fornitore, categoria software e famiglia software. Dopo aver modificato le informazioni di categorizzazione per software predefiniti, lo stato di convalida per le modifiche software cambia da **Convalidato** a **Definito da utente**.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a>Punto di sincronizzazione di Asset Intelligence  

Il punto di sincronizzazione di Asset Intelligence è un ruolo del sistema del sito di Configuration Manager usato per connettersi a Microsoft Cloud sulla porta TCP 443 e gestire gli aggiornamenti dinamici delle informazioni del catalogo. Installare questo ruolo del sito solo nel sito principale della gerarchia. Configurare tutte le personalizzazioni del catalogo di Asset Intelligence tramite una console di Configuration Manager connessa al sito principale. 

Mentre si configurano tutti gli aggiornamenti in corrispondenza del sito principale, le informazioni del catalogo vengono replicate negli altri siti nella gerarchia. Il ruolo del sito consente di richiedere la sincronizzazione del catalogo su richiesta con Microsoft o di pianificare la sincronizzazione automatica del catalogo. Oltre al download di nuove informazioni per il catalogo, il punto di sincronizzazione di Asset Intelligence consente di caricare le informazioni sui titoli software personalizzati in Microsoft a scopo di categorizzazione. Microsoft considera informazioni pubbliche tutti i titoli software caricati. Assicurarsi che i titoli software personalizzati non includano informazioni riservate o proprietarie.  

Se si invia un titolo software senza categoria, Microsoft lo rivede solo quando sono presenti almeno quattro richieste di categorizzazione di clienti per lo stesso titolo software. I ricercatori Microsoft procedono quindi all'identificazione e alla categorizzazione e rendono disponibili le informazioni di categorizzazione del titolo software a tutti i clienti che usano il servizio online. Viene assegnata la massima priorità ai titoli software con il maggior numero di richieste di categorizzazione. È improbabile che software personalizzato e applicazioni line-of-business ricevano una categoria. Non inviare titoli software di questo tipo a Microsoft per la categorizzazione.  

Per connettersi a Microsoft Cloud, è necessario un punto di sincronizzazione di Asset Intelligence. Per informazioni su come installare il ruolo, vedere [Configurazione di Asset Intelligence](configuring-asset-intelligence.md).  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Home page di Asset Intelligence  

Il nodo **Asset Intelligence** nell'area di lavoro **Asset e conformità** è la home page di Asset Intelligence in Configuration Manager. La home page visualizza un dashboard di riepilogo delle informazioni del catalogo di Asset Intelligence.  

> [!NOTE]  
> La home page di **Asset Intelligence** non viene in genere aggiornata automaticamente mentre è visualizzata.  

La home page di **Asset Intelligence** è divisa nelle sezioni seguenti:  

- **Sincronizzazione catalogo**: informazioni sullo stato di abilitazione di Asset Intelligence e sullo stato corrente del punto di sincronizzazione di Asset Intelligence.  

    > [!NOTE]  
    > La home page visualizza questa sezione solo se si installa un punto di sincronizzazione di Asset Intelligence.  

    La sezione visualizza anche le informazioni seguenti:  

    - Pianificazione della sincronizzazione  

    - Importazione o meno di un resoconto delle licenze cliente   

    - Aggiornamento più recente dello stato  

    - Data e ora dell'aggiornamento pianificato successivo  

    - Numero di modifiche successive all'installazione del punto di sincronizzazione di Asset Intelligence   

- **Stato software di inventario**: conteggio e percentuale dei programmi software, delle categorie software e delle famiglie software di inventario identificati da Microsoft, identificati da un amministratore, con identificazione online in sospeso o non identificati e non in sospeso. Le informazioni visualizzate in formato tabella illustra il conteggio per ogni e le informazioni visualizzate nel grafico viene visualizzata la percentuale per ogni.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Report di Asset Intelligence  

I report di Asset Intelligence si trovano nella console di Configuration Manager, nell'area di lavoro **Monitoraggio** nella cartella **Asset Intelligence** nel nodo **Creazione report**. I report forniscono informazioni su hardware, gestione delle licenze e software. Per altre informazioni sui report in Configuration Manager, vedere [Introduzione ai report](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> La precisione delle informazioni su licenze e quantità dei titoli software installati visualizzate nei report di Asset Intelligence può variare rispetto al numero effettivo di titoli software installati o di licenze in uso nell'ambiente, a causa delle complesse dipendenze e limitazioni associate all'esecuzione dell'inventario delle informazioni sulle licenze per i titoli software installati in ambienti aziendali. Non usare i report di Asset Intelligence come unica fonte di informazioni per determinare la conformità delle licenze software acquistate.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a> Report hardware  

I report hardware di Asset Intelligence offrono informazioni sulle risorse hardware nell'organizzazione. Sulla base delle informazioni di inventario hardware, come velocità, memoria e dispositivi, i report hardware di Asset Intelligence possono visualizzare informazioni relative ai dispositivi USB e all'hardware che deve essere aggiornato, nonché ai computer che non sono pronti per un aggiornamento software specifico.  

> [!NOTE]  
> Alcuni dati utente nei report hardware di Asset Intelligence vengono raccolti dal registro eventi di sicurezza di Windows. Per una maggiore precisione dei report, cancellare questo registro quando si riassegna un computer a un nuovo utente.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a> Report di gestione delle licenze  

I report di Asset Intelligence sulla gestione delle licenze visualizzano dati relativi alle licenze in uso. Il report **Registro delle licenze** elenca le applicazioni Microsoft installate in un formato analogo a quello del resoconto delle licenze Microsoft. Questo formato rappresenta un metodo pratico per associare le licenze acquistate e quelle usate. Altri report sulla gestione delle licenze offrono informazioni sui computer che fungono da server per l'esecuzione del servizio di gestione delle chiavi allo scopo di ottenere dati statistici sull'attivazione di Windows.  

> [!IMPORTANT]  
> Diversi report di Asset Intelligence sulla gestione delle licenze presentano informazioni sulla funzione del Server di gestione delle chiavi, un metodo per l'amministrazione di contratti multilicenza. Se non è stato implementato un Server di gestione delle chiavi, alcuni report potrebbe non restituire dati.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a> Report software  

I report software di Asset Intelligence offrono informazioni su famiglie e categorie software e su titoli software specifici installati nei computer dell'organizzazione. I report software visualizzano informazioni relative, ad esempio, agli oggetti browser helper o ai programmi software che vengono avviati automaticamente. È possibile usare questi report per identificare adware, spyware e altro malware. È anche possibile usarli per identificare software ridondante e semplificare l'acquisizione e il supporto del software.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a> Report sui tag di identificazione software  

I report di Asset Intelligence sui tag di identificazione software offrono informazioni sui programmi software che contengono un tag di identificazione conforme allo standard ISO/IEC 19770-2. I tag di identificazione software rendono disponibili informazioni autorevoli per l'identificazione del software installato. Quando si abilita la classe di report di inventario hardware **SMS_SoftwareTag**, Configuration Manager raccoglie informazioni sul software dotato di tag di identificazione software. 

I report seguenti forniscono informazioni sul software:  

- **Software 14A - Ricerca di software con tag di identificazione software abilitato**: conteggio dei programmi software installati con un tag di identificazione software abilitato  

- **Software 14B - Computer con software specifico installato con tag di identificazione software abilitato**: tutti i computer con software installato con un tag di identificazione software abilitato specifico  

- **Software 14C - Software installato con tag di identificazione software abilitato in un computer specifico**: tutto il software installato con un tag di identificazione abilitato specifico in un computer specifico  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a> Limiti dei report  

I report di Asset Intelligence possono rendere disponibili grandi quantità di informazioni sui titoli software installati e sulle licenze software acquistate in uso. Non usare queste informazioni come unica fonte per determinare la conformità delle licenze software acquisite.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Esempi di dipendenze  
La precisione delle quantità visualizzate nei report di Asset Intelligence per i titoli software installati e le licenze possono variare rispetto alle quantità effettive in uso, a causa delle complesse dipendenze associate all'esecuzione dell'inventario delle informazioni sulle licenze per i titoli software in uso in ambienti aziendali. Gli esempi seguenti illustrano le dipendenze implicite nell'esecuzione tramite Asset Intelligence dell'inventario del software installato nell'organizzazione che potrebbero influire sulla precisione dei report di Asset Intelligence:  

- **Dipendenze dall'inventario hardware dei client**: i report di Asset Intelligence sul software installato si basano sui dati ricavati dai client di Configuration Manager tramite l'estensione dell'inventario hardware per abilitare i report di Asset Intelligence. A causa di questa dipendenza dai report di inventario hardware, i report di Asset Intelligence includono solo i dati dei client che completano correttamente i processi di inventario hardware con le classi di report WMI di Asset Intelligence richieste abilitate. Poiché i client di Configuration Manager eseguono i processi di inventario hardware in base a una pianificazione definita dall'utente amministratore, può verificarsi un ritardo nella generazione dei report dei dati, con effetti sulla precisione dei report di Asset Intelligence. 

    Ad esempio, un titolo software in licenza di inventario potrebbe essere disinstallato dopo il completamento di un ciclo di inventario hardware corretto del client. Nei report di Asset Intelligence il titolo software viene indicato come installato fino al successivo ciclo di report di inventario hardware pianificato del client.  

- **Dipendenze dai pacchetti software**: I report di Asset Intelligence sono basati sui dati relativi ai titoli software installati. Tali dati vengono raccolti tramite i processi di inventario hardware standard dei client di Configuration Manager. È possibile che alcuni dati sui titoli software non vengano raccolti correttamente. Ecco alcuni esempi di casi in cui i report di Asset Intelligence possono essere imprecisi:  

    - Installazioni software non conformi ai processi di installazione standard  

    - Installazioni software modificate prima dell'installazione   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Limitazioni legali  
Le informazioni visualizzate nei report di Asset Intelligence sono soggette a numerose limitazioni. Le informazioni visualizzate nei report non costituiscono un parere legale, contabile o professionale di altro tipo. Le informazioni offerte dai report di Asset Intelligence hanno uno scopo esclusivamente informativo. Non usarle come unica fonte per determinare la conformità dell'utilizzo delle licenze software.  

Gli esempi seguenti illustrano alcuni casi in cui l'uso di Asset Intelligence può influire sulla precisione dei report:  

- **Limitazioni relative alle quantità di utilizzo delle licenze Microsoft**:  

    - la quantità di licenze software Microsoft acquisite si basa sulle informazioni fornite dagli amministratori. Rivedere attentamente queste informazioni per assicurarsi che venga indicato il numero corretto di licenze software.  

    - La quantità indicata di licenze software Microsoft include solo le informazioni relative alle licenze software Microsoft acquisite attraverso programmi multilicenza. Non riflette le informazioni relative alle licenze software acquisite tramite rivenditori al dettaglio, OEM o altri canali di vendita di licenze software.  

    - Le licenze software acquistate negli ultimi 45 giorni potrebbero non essere incluse nella quantità di licenze software Microsoft indicata nei report a causa dei requisiti e delle pianificazioni per i report del rivenditore del software.  

    - Le quantità di licenze software Microsoft potrebbero non rispecchiare le modifiche dovute a trasferimenti delle licenze software in seguito a fusioni o acquisizioni.  

    - I termini e le condizioni in un contratto multilicenza Microsoft possono influire sul numero di licenze software indicato nei report. Possono quindi essere necessarie ulteriori verifiche da parte di un rappresentante Microsoft.  

- **Limitazioni relative alle quantità di titoli software installati**: perché i report di Asset Intelligence contengano informazioni accurate sulle quantità di titoli software installati, i client di Configuration Manager devono completare correttamente i cicli di report di inventario hardware. Se viene acquisita la licenza di un titolo software dopo l'esecuzione di un ciclo di report di inventario hardware, l'installazione o la disinstallazione di tale titolo può comparire nei report con un periodo di ritardo e non riflettersi nei report di Asset Intelligence eseguiti prima del successivo report di inventario hardware pianificato.  

- **Limitazioni relative alla riconciliazione delle licenze**: La riconciliazione della quantità di titoli software installati e della quantità di licenze software acquisite viene eseguita confrontando la quantità di licenze specificata dall'amministratore e la quantità di titoli software installati raccolta dagli inventari hardware dei client di Configuration Manager in base alla pianificazione impostata dall'amministratore. Questo confronto non offre dati conclusivi per Microsoft in merito alla situazione delle licenze. La posizione della licenza effettivo dipende i software specifico titolo licenza e l'utilizzo diritti concessi da condizioni di licenza.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a> Stati di convalida di Asset Intelligence  

Gli stati di convalida di Asset Intelligence rappresentano lo stato di convalida di origine e corrente delle informazioni nel catalogo di Asset Intelligence. La tabella seguente illustra gli stati di convalida possibili di Asset Intelligence e le azioni dell'amministratore che possono causarli.  

| Stato | Definizione | Azione dell'amministratore | Commento |  
|---------------|--------------------|------------------------------|-----------------|  
|**Convalidato**|I ricercatori Microsoft hanno definito l'elemento del catalogo|Nessuno|Stato ottimale|  
|**Definito da utente**|I ricercatori Microsoft non hanno definito l'elemento del catalogo|Personalizzazione delle informazioni del catalogo locale|Questo stato viene visualizzato nei report di Asset Intelligence|  
|**In sospeso**|I ricercatori Microsoft non hanno definito l'elemento del catalogo, ma l'elemento è stato inviato a Microsoft per la categorizzazione|Nessuna altra azione necessaria dopo la richiesta di categorizzazione|L'elemento del catalogo rimane in questo stato finché i ricercatori Microsoft non lo categorizzano e l'utente non sincronizza il catalogo di Asset Intelligence|  
|**Aggiornabile**|Un elemento di catalogo definito dall'utente è stato categorizzato in modo diverso da Microsoft durante la sincronizzazione del catalogo.|Usare l'azione **Risolvi conflitto** per decidere se usare le nuove informazioni di categorizzazione o il valore definito dall'utente precedente. Per altre informazioni su come risolvere i conflitti, vedere [Operazioni per Asset Intelligence](operations-for-asset-intelligence.md).|Dopo la risoluzione di un conflitto di categorizzazione, l'elemento non viene convalidato perché risulta ancora in conflitto, a meno che aggiornamenti della categorizzazione successivi non introducano nuove informazioni sull'elemento.|  
|**Senza categoria**|L'elemento del catalogo non è stato definito dai ricercatori Microsoft, l'elemento non è stato inviato a Microsoft per la categorizzazione e l'amministratore non ha assegnato un valore di categorizzazione definito dall'utente.|Richiesta di categorizzazione o personalizzazione delle informazioni del catalogo locale. Per altre informazioni, vedere [Operazioni per Asset Intelligence](operations-for-asset-intelligence.md).|Nessuno|  

> [!NOTE]  
> Gli elementi del catalogo inviati dall'utente a Microsoft per la categorizzazione hanno lo stato di convalida **In attesa** in un sito di amministrazione centrale, ma vengono ancora visualizzati con lo stato di convalida **Senza categoria** nei siti primari figlio.  

Per esempi di transizione da uno stato di convalida a altro, vedere [Transizioni dello stato di convalida di esempio per Asset Intelligence](example-validation-state-transitions-for-asset-intelligence.md).  
