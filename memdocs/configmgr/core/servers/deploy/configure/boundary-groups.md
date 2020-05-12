---
title: Configurare gruppi di limiti
titleSuffix: Configuration Manager
description: Aiutare i client a trovare i sistemi del sito usando i gruppi di limiti per organizzare logicamente i percorsi di rete correlati chiamati limiti
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce77c43f49556b3a60e36f05127f82d4d135762a
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643269"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configurare gruppi di limiti per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare i gruppi di limiti in Configuration Manager per organizzare logicamente i percorsi di rete correlati ([limiti](boundaries.md)) e semplificare la gestione dell'infrastruttura. Prima di usare il gruppo di limiti, assegnare i limiti ai gruppi di limiti.

Per impostazione predefinita, Configuration Manager crea un gruppo di limiti predefinito in ogni sito.

Per configurare i gruppi di limiti, associare i limiti (percorsi di rete) e i ruoli del sistema del sito, come i punti di distribuzione, al gruppo di limiti. Questa configurazione consente di associare i client ai server del sistema del sito, come i punti di distribuzione, che si trovano vicino ai client nella rete.

Per aumentare la disponibilità dei server per una gamma più ampia di percorsi di rete, assegnare lo stesso limite e lo stesso server a più gruppi di limiti.

I client usano un gruppo di limiti per gli scopi seguenti:  

- Assegnazione automatica al sito  
- Ricerca di un server del sistema del sito che può fornire un servizio, tra cui:

  - Punti di distribuzione per il percorso del contenuto  
  - Punti di aggiornamento software  
  - Punti di migrazione dello stato  

    > [!NOTE]
    > Il punto di migrazione stato non usa relazioni di fallback. Per altre informazioni, vedere [Fallback](#fallback).

  - Punti di gestione preferiti  

    > [!NOTE]  
    > Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dall'interno della configurazione del gruppo di limiti. Per altre informazioni, vedere [Abilitare l'uso dei punti di gestione preferiti](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Cloud Management Gateway (a partire dalla versione 1902)

## <a name="boundary-groups-and-relationships"></a>Gruppi di limiti e relazioni

Per ogni gruppo di limiti nella gerarchia, è possibile assegnare:

- Uno o più limiti. Il gruppo di limiti **corrente** di un client è un percorso di rete definito come limite assegnato a un gruppo di limiti specifico. Un client può avere più di un gruppo di limiti corrente.  

- Uno o più ruoli del sistema del sito. I client possono usare sempre i ruoli associati al gruppo di limiti corrente. A seconda delle configurazioni aggiuntive, possono usare i ruoli in gruppi di limiti aggiuntivi.  

Per ogni gruppo di limiti creato, è possibile configurare un collegamento unidirezionale a un altro gruppo di limiti. Il collegamento è definito **relazione**. I gruppi di limiti con cui si stabilisce il collegamento sono chiamati gruppi di limiti **adiacenti**. Un gruppo di limiti può avere più relazioni, ciascuna con uno specifico gruppo di limiti adiacente.

Se un client non riesce a trovare un sistema del sito disponibile nel gruppo di limiti corrente, la configurazione di ogni relazione determina quando iniziare a cercare in un gruppo di limiti adiacente. Questa ricerca in altri gruppi è definita **fallback**.

Per altre informazioni, vedere le procedure seguenti:  

- [Creare un gruppo di limiti](boundary-group-procedures.md#bkmk_create)  
- [Configurare un gruppo di limiti](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a> Visualizzare i gruppi di limiti per i dispositivi

<!--6521835-->

A partire dalla versione 2002, per facilitare l'identificazione e la risoluzione dei problemi relativi ai comportamenti dei dispositivi con gruppi di limiti, è possibile visualizzare i gruppi di limiti per dispositivi specifici. Nel nodo **Dispositivi** o quando si visualizzano i membri di una **Raccolta di dispositivi**, aggiungere la nuova colonna **Gruppi di limiti** alla visualizzazione elenco.

- Se un dispositivo è incluso in più di un gruppo di limiti, il valore è un elenco delimitato da virgole di nomi di gruppi di limiti.

- I dati vengono aggiornati quando il client effettua una richiesta di posizione al sito o al massimo ogni 24 ore.

- Se un client è in roaming e non è un membro di un gruppo di limiti, il valore è vuoto.

> [!NOTE]
> Queste informazioni sono dati del sito e sono disponibili solo nei siti primari. Non verrà visualizzato alcun valore per questa colonna quando si connette Configuration Manager a un sito di amministrazione centrale.

## <a name="fallback"></a>Fallback

Per evitare problemi quando i client non riescono a trovare un sistema del sito disponibile nel gruppo di limiti corrente, definire la relazione tra i gruppi di limiti per il comportamento di fallback. Il fallback consente a un client di espandere la ricerca di un sistema del sito disponibile a gruppi di limiti aggiuntivi.

Le relazioni vengono configurate in una scheda **Relazioni** delle proprietà del gruppo di limiti. Quando si configura una relazione, si definisce un collegamento a un gruppo di limiti adiacente. Per ogni tipo di ruolo del sistema del sito supportato, configurare impostazioni indipendenti per il fallback a tale gruppo di limiti adiacente. Per altre informazioni, vedere [Configurare il comportamento di fallback](boundary-group-procedures.md#bkmk_bg-fallback).

Ad esempio, quando si configura una relazione con un gruppo di limiti specifico, impostare il fallback per i punti di distribuzione dopo 20 minuti. Il valore predefinito è 120 minuti. Per un esempio più esteso, vedere [Esempio d'uso dei gruppi di limiti](#example-of-using-boundary-groups).

Se un client non riesce a trovare un ruolo del sistema del sito disponibile nel gruppo di limiti corrente, il client usa il tempo di fallback in minuti. Tale tempo di fallback determina quando il client inizia a eseguire la ricerca di un sistema del sito disponibile associato al gruppo di limiti adiacente.  

Se un client non riesce a trovare un sistema del sito disponibile, inizia la ricerca nei percorsi dei gruppi di limiti adiacenti. Questo comportamento aumenta il pool di sistemi del sito disponibili. La configurazione dei gruppi di limiti e delle relative relazioni definisce l'uso del client di questo pool di sistemi del sito disponibili.

- Un gruppo di limiti può avere più di una relazione. Con questa configurazione è possibile configurare il fallback per ogni tipo di sistema del sito a diversi gruppi adiacenti dopo diversi intervalli di tempo.  

- I client eseguono il fallback solo in un gruppo di limiti direttamente adiacente al loro gruppo di limiti corrente.  

- Se un client fa parte di più gruppi di limiti, il relativo gruppo di limiti corrente è definito come l'unione di tutti i gruppi di limiti. Il client esegue il fallback ai gruppi adiacenti di uno dei gruppi di limiti originali.  

> [!NOTE]
> Il ruolo del punto di migrazione stato non usa relazioni di fallback. Se si aggiungono sia i ruoli del punto di migrazione stato che i ruoli del punto di distribuzione allo stesso server del sistema del sito, non configurare il fallback per il gruppo di limiti. Se è necessario usare il fallback del gruppo di limiti per il punto di distribuzione, aggiungere il ruolo del punto di migrazione stato in un altro server del sistema del sito.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>Gruppo di limiti predefinito del sito

È possibile creare gruppi di limiti personalizzati e ogni sito dispone di un gruppo di limiti predefinito creato da Configuration Manager. Questo gruppo è denominato **Default-Site-Boundary-Group&lt;codicesito>** . Ad esempio, il gruppo per il sito ABC sarebbe denominato **Default-Site-Boundary-Group&lt;ABC>** .

Per ogni gruppo di limiti creato, Configuration Manager crea automaticamente un collegamento implicito a ogni gruppo di limiti predefinito del sito nella gerarchia.  

- Il collegamento implicito è un'opzione di fallback predefinita da un gruppo di limiti corrente al gruppo di limiti predefinito del sito. Il tempo di fallback predefinito è 120 minuti.  

- Per i client che non si trovano in un limite associato a un gruppo di limiti: per identificare i ruoli del sistema del sito validi, usare il gruppo di limiti predefinito dal sito assegnato.  

Per gestire il fallback al gruppo di limiti predefinito del sito:  

- Aprire le proprietà del gruppo di limiti predefinito del sito e modificare i valori nella scheda **Comportamento predefinito**. Le modifiche apportate in questa scheda si applicano a *tutti* i collegamenti impliciti a questo gruppo di limiti. Quando si configura un collegamento esplicito a questo gruppo di limiti del sito predefinito da un altro gruppo di limiti, le impostazioni predefinite vengono sostituite.  

- Aprire le proprietà di un gruppo di limiti personalizzato. Modificare i valori per il collegamento esplicito a un gruppo di limiti predefinito del sito. Quando si imposta un nuovo intervallo in minuti per il fallback o il blocco del fallback, la modifica influisce solo sul collegamento che si sta configurando. La configurazione del collegamento esplicito sostituisce quella della scheda **Comportamento predefinito** di un gruppo di limiti predefinito del sito.  

## <a name="site-assignment"></a>Assegnazione sito  

È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

- Un client appena installato che usa l'assegnazione automatica sito viene aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  

- Dopo l'assegnazione a un sito, un client non cambia la propria assegnazione sito quando cambia il percorso di rete. Ad esempio, un client effettua il roaming in un nuovo percorso di rete. Questo percorso è un limite in un gruppo di limiti con un'assegnazione sito diversa. Il sito assegnato del client non cambia.  

- Quando l'individuazione sistema Active Directory rileva una nuova risorsa, il sito valuta le informazioni di rete per la risorsa in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  

- Quando un limite è membro di più gruppi di limiti con diversi siti assegnati, i client selezionano uno dei siti in modo casuale.  

- Le modifiche a un sito assegnato a gruppi di limiti si applicano solo alle nuove azioni di assegnazione sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione sito per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Per altre informazioni su come configurare l'assegnazione sito, vedere le procedure seguenti:

- [Configurare l'assegnazione sito e selezionare i server del sistema del sito](boundary-group-procedures.md#bkmk_references)
- [Configurare un sito di fallback per l'assegnazione sito automatica](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Punti di distribuzione

Quando un client richiede il percorso di un punto di distribuzione, Configuration Manager invia al client un elenco dei sistemi del sito. Questi sistemi del sito sono del tipo appropriato associato a ogni gruppo di limiti che include il percorso di rete corrente del client:

- **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione in un'origine contenuto valida. Questo percorso può essere un punto di distribuzione o un'origine peer cache.  

- **Durante la distribuzione del sistema operativo**, i client richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato.  

  - I client acquisiscono il contenuto in base ai comportamenti dei gruppi di limiti. Per altre informazioni, vedere [Supporto della sequenza di attività per i gruppi di limiti](#bkmk_bgr-osd).  

Quando viene distribuito il contenuto, se un client richiede contenuto non disponibile da un'origine nel gruppo di limiti corrente, il client continua a richiedere tale contenuto. Il client prova diverse origini del contenuto nel gruppo di limiti corrente finché non raggiunge il periodo di fallback per un gruppo di limiti adiacente o per il gruppo di limiti del sito predefinito. Se il client non ha ancora trovato il contenuto, estende la ricerca alle origini contenuto in modo da includere i gruppi di limiti adiacenti.

Se si configura la distribuzione del contenuto su richiesta e il contenuto non è disponibile in un punto di distribuzione quando viene richiesto da un client, il sito inizia a trasferire il contenuto al punto di distribuzione. È possibile che il client rilevi il server come origine contenuto prima di eseguire il fallback per l'uso di un gruppo di limiti adiacente.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a> Installazione client

<!--1358840-->
Durante l'installazione del client Configuration Manager, il processo ccmsetup contatta il punto di gestione per individuare i contenuti necessari. Il punto di gestione restituisce i punti di distribuzione in base alla configurazione del gruppo di limiti. Se si definiscono le relazioni nel gruppo di limiti, il punto di gestione restituisce i punti di distribuzione nell'ordine seguente:

1. Gruppo di limiti corrente  
2. Gruppi di limiti adiacenti  
3. Gruppo di limiti predefinito del sito  

> [!Note]  
> Il processo di installazione client non usa il tempo di fallback. Per individuare il più rapidamente possibile il contenuto, esegue immediatamente il fallback nel gruppo di limiti successivo.
>
> Nelle versioni precedenti di Configuration Manager, durante questo processo il punto di gestione restituiva solo i punti di distribuzione nel gruppo di limiti corrente del client. Se non era disponibile alcun contenuto, il processo di installazione eseguiva il fallback scaricando il contenuto dal punto di gestione. Non era disponibile alcuna opzione per eseguire il fallback ai punti di distribuzione in altri gruppi di limiti nei quali poteva essere disponibile il contenuto necessario.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a> Supporto della sequenza di attività per i gruppi di limiti

<!--1359025-->
Quando un dispositivo esegue una sequenza di attività e deve acquisire il contenuto, il dispositivo usa comportamenti dei gruppi di limiti simili al client di Configuration Manager.

Questo comportamento può essere configurato usando le impostazioni seguenti nella pagina **Punti di distribuzione** della distribuzione della sequenza di attività:

- **Usare un punto di distribuzione remoto quando non sono disponibili punti di distribuzione locali**: per questa distribuzione la sequenza di attività può eseguire il fallback ai punti di distribuzione in un gruppo di limiti adiacente.  

- **Consenti ai client di usare i punti di distribuzione dal gruppo di limiti del sito predefinito**: per questa distribuzione la sequenza di attività può eseguire il fallback ai punti di distribuzione nel gruppo di limiti del sito predefinito.  

Per usare questo nuovo comportamento, assicurarsi di aggiornare i client alla versione più recente.

#### <a name="location-priority"></a>Priorità della posizione  

La sequenza di attività tenta di acquisire i contenuti nell'ordine seguente:  

1. Origini di peer cache  

2. Punti di distribuzione nel gruppo di limiti *corrente*  

3. Punti di distribuzione in un gruppo di limiti *adiacente*  

    > [!Important]  
    > A causa della natura in tempo reale dell'elaborazione della sequenza di attività, non viene atteso il tempo di failover in un gruppo di limiti adiacente. I tempi di failover vengono usati per classificare in ordine di priorità i gruppi di limiti adiacenti. Ad esempio, se la sequenza di attività non riesce ad acquisire il contenuto da un punto di distribuzione nel gruppo di limiti corrente, tenta immediatamente da un punto di distribuzione in un gruppo di limiti adiacente con il tempo di failover più breve. Se il processo ha esito negativo, effettua il failover in un punto di distribuzione in un gruppo di limiti adiacente con il tempo di failover più lungo.  

4. Punti di distribuzione nel gruppo di limiti *predefinito del sito*  

Il file di log della sequenza di attività **smsts.log** mostra la priorità delle origini delle posizioni usate in base alle proprietà della distribuzione.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> Opzioni del gruppo di limiti per download peer

<!--1356193, 1358749-->
Sono disponibili le impostazioni aggiuntive seguenti per i gruppi di limiti per offrire maggiore controllo sulla distribuzione del contenuto nell'ambiente:  

- [Consenti i download peer in questo gruppo di limiti](#bkmk_bgoptions1)  

- [Durante i download peer, usa solo i peer entro la stessa subnet](#bkmk_bgoptions2)  

- [Preferisci i punti di distribuzione rispetto ai peer entro la stessa subnet](#bkmk_bgoptions3)  

- [Preferisci i punti di distribuzione cloud rispetto ai punti di distribuzione](#bkmk_bgoptions4)  

Per altre informazioni su come configurare queste impostazioni, vedere [Configurare gruppi di limiti](boundary-group-procedures.md#bkmk_config).

Se un dispositivo si trova in più gruppi di limiti, per queste impostazioni si applicano i comportamenti seguenti:

- **Consenti i download peer in questo gruppo di limiti**: se questa opzione è disabilitata in un gruppo di limiti, il client non userà l'ottimizzazione per il recapito.
- **Durante i download peer, usa solo i peer entro la stessa subnet**: se è abilitata in uno dei gruppi di limiti, questa impostazione è attiva.
- **Preferisci i punti di distribuzione rispetto ai peer entro la stessa subnet**: se è abilitata in uno dei gruppi di limiti, questa impostazione è attiva.
- **Preferisci le origini basate sul cloud rispetto alle origini locali**: se è abilitata in uno dei gruppi di limiti, questa impostazione è attiva.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a> Consenti i download peer in questo gruppo di limiti

Questa opzione è attivata per impostazione predefinita. Il punto di gestione fornisce ai client un elenco di posizioni del contenuto che include le origini peer. Questa impostazione influisce anche sull'applicazione di ID di gruppo per l'[ottimizzazione recapito](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).  

Esistono due scenari comuni in cui potrebbe essere utile disabilitare questa opzione:  

- In presenza di un gruppo di limiti che include limiti da posizioni geograficamente dislocate, come una VPN. Due client possono essere inclusi nello stesso gruppo di limiti perché sono connessi tramite VPN, ma trovarsi in luoghi molto lontani non appropriati per la condivisione peer del contenuto.  

- Se si usa un singolo gruppo di limiti di grandi dimensioni per l'assegnazione del sito che non fa riferimento ad alcun punto di distribuzione.  

> [!IMPORTANT]
> Se un dispositivo è incluso in più di un gruppo di limiti, assicurarsi di abilitare questa impostazione in tutti i gruppi di limiti per il dispositivo. In caso contrario, il client non userà l'ottimizzazione recapito. Ad esempio, non imposta la chiave del Registro di sistema DOGroupID.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a> Durante i download peer, usa solo i peer entro la stessa subnet

Questa impostazione dipende dall'opzione precedente. Se si abilita questa opzione, il punto di gestione include nell'elenco delle posizioni del contenuto solo le origini peer incluse nella stessa subnet del client.

Scenari comuni per l'abilitazione di questa opzione:

- La progettazione del gruppo di limiti per la distribuzione del contenuto include un solo gruppo di limiti di grandi dimensioni che si sovrappone ad altri gruppi di limiti più piccoli. Con questa nuova impostazione, l'elenco di origini di contenuto che il punto di gestione fornisce ai client include solo le origini peer dalla stessa subnet.

- È disponibile un singolo gruppo di limiti di grandi dimensioni per tutti gli uffici remoti. Abilitare questa opzione e i client potranno condividere solo il contenuto all'interno della subnet nell'ufficio remoto, invece di correre i rischi correlati alla condivisione del contenuto tra posizioni diverse.

A partire dalla versione 2002, a seconda della configurazione della rete è ora possibile escludere determinate subnet per l'individuazione delle corrispondenze. Ad esempio, si vuole includere un limite ma escludere una subnet VPN specifica. Per impostazione predefinita, Configuration Manager esclude la subnet Teredo predefinita (`2001:0000:%`).<!--3555777-->

> [!NOTE]
> Nella versione 2002, quando si [espande un sito primario autonomo](../install/prerequisites-for-installing-sites.md#bkmk_expand) per aggiungere un sito di amministrazione centrale, viene ripristinato l'elenco di esclusione delle subnet predefinito. Per risolvere questo problema, dopo l'espansione del sito eseguire lo script di PowerShell per personalizzare l'elenco di esclusioni delle subnet nel sito di amministrazione centrale.<!-- 6309068 -->

Importare l'elenco di esclusioni delle subnet come stringa di subnet separate da virgole. Usare il segno di percentuale (`%`) come carattere jolly. Nel server del sito di livello superiore impostare o leggere la proprietà incorporata **SubnetExclusionList** per il componente **SMS_HIERARCHY_MANAGER** nella classe **SMS_SCI_Component**. Per altre informazioni, vedere [Classe WMI server SMS_SCI_Component](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md).

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Esempio di script di PowerShell per aggiornare l'elenco di esclusione delle subnet

Lo script seguente è un esempio di come modificare questo valore. Aggiungere le subnet alla variabile **PropertyValue** dopo `2001:0000:%,172.16.16.0`. Si tratta di una stringa separata da virgole. Eseguire questo script nel server del sito di livello superiore nella gerarchia.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Per impostazione predefinita, Configuration Manager include la subnet Teredo in questo elenco. Quando si modifica l'elenco, leggere sempre prima il valore esistente. Aggiungere altre subnet all'elenco, quindi impostare il nuovo valore.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a> Preferisci i punti di distribuzione rispetto ai peer entro la stessa subnet

Per impostazione predefinita, il punto di gestione classifica le origini di peer cache in cima all'elenco delle posizioni dei contenuti. Questa impostazione inverte tale priorità per i client che si trovano nella stessa subnet dell'origine di peer cache.

> [!TIP]
> Questo comportamento si applica al client di Configuration Manager. Non si applica quando la sequenza di attività scarica contenuto. Quando viene eseguita, la sequenza di attività predilige le origini peer cache rispetto ai punti di distribuzione.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a> Preferisci i punti di distribuzione cloud rispetto ai punti di distribuzione

Se è presente una succursale con un collegamento Internet più veloce, è possibile classificare in ordine di priorità i contenuti cloud.  

Nella versione 1902 questa impostazione è **Preferisci le origini basate sul cloud rispetto alle origini locali**. Le origini basate su cloud includono quanto segue:<!-- SCCMDocs#1529 -->

- Punti di distribuzione cloud
- Microsoft Update (aggiunto nella versione 1902)

## <a name="software-update-points"></a>Punti di aggiornamento software

I client usano i gruppi di limiti per trovare un nuovo punto di aggiornamento software. Per controllare quali server possono essere trovati da un client, aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti.

Se si aggiungono tutti i punti di aggiornamento software esistenti al gruppo di limiti del sito predefinito, il client seleziona un punto di aggiornamento software dal pool di server disponibili. Questo comportamento è simile a quello delle versioni precedenti di Configuration Manager Current Branch. Per ottenere un comportamento di selezione e fallback controllato, aggiungere singoli punti di aggiornamento software a gruppi di limiti diversi.

Se si installa un nuovo sito, i punti di aggiornamento software non vengono aggiunti al gruppo di limiti del sito predefinito. Assegnare i punti di aggiornamento software a un gruppo di limiti in modo che i client possano trovarli e usarli.

### <a name="fallback-for-software-update-points"></a>Fallback per i punti di aggiornamento software

Il fallback per i punti di aggiornamento software è configurato come altri ruoli del sistema del sito, ma con le avvertenze seguenti:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>I nuovi client usano i gruppi di limiti per selezionare i punti di aggiornamento software

I nuovi client installati selezionano un punto di aggiornamento software dai server associati ai gruppi di limiti configurati. Ciò sostituisce il comportamento precedente in cui i client selezionano un punto di aggiornamento software in maniera casuale da un elenco di server che condividono la foresta dei client.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>I client continuano a usare l'ultimo punto di aggiornamento software valido noto fino a quando non eseguono il fallback per trovare un nuovo punto

I client che hanno già un punto di aggiornamento software continuano a usarlo fino a quando non può essere raggiunto. Questo comportamento include l'uso continuativo di un punto di aggiornamento software non associato al gruppo di limiti corrente del client.

Si tratta di un comportamento intenzionale. Il client continua a usare un punto di aggiornamento software esistente anche se non è incluso nel gruppo di limiti corrente del client. Quando il punto di aggiornamento software viene modificato, il client sincronizza i dati con il nuovo server, il che determina un uso significativo della rete. Se tuti client i client passano contemporaneamente a un nuovo server, il ritardo nella transizione può evitare la saturazione della rete.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Un client prova sempre a raggiungere l'ultimo punto di aggiornamento software valido noto per 120 minuti prima di avviare il fallback

Dopo 120 minuti, se il client non ha stabilito il contatto, inizia il fallback. All'avvio del fallback, il client riceve un elenco di tutti i punti di aggiornamento software nel gruppo di limiti corrente. I punti di aggiornamento software aggiuntivi del gruppo di limiti predefinito del sito e di quelli adiacenti sono disponibili in base alle configurazioni di fallback.

### <a name="fallback-configurations-for-software-update-points"></a>Configurazioni di fallback per i punti di aggiornamento software

È possibile impostare **Orari di fallback (in minuti)** per i punti di aggiornamento software su meno di 120 minuti. Il client prova comunque a raggiungere il punto di aggiornamento software originale per 120 minuti. La ricerca viene quindi espansa su server aggiuntivi. I tempi di fallback del gruppo di limiti iniziano la prima volta in cui il client non riesce a raggiungere il server originale. Quando il client espande la ricerca, il sito specifica tutti i gruppi di limiti configurati per meno di 120 minuti.

Per bloccare il fallback per un punto di aggiornamento software a un gruppo di limiti adiacente, configurare l'impostazione su **Non eseguire mai il fallback**.

Dopo l'esito negativo nel raggiungere il server originale per due ore, il client usa quindi un ciclo più breve per stabilire una connessione a un nuovo punto di aggiornamento software. In questo modo il client può eseguire rapidamente una ricerca nell'elenco in espansione di potenziali punti di aggiornamento software.

#### <a name="example"></a>Esempio

Si configurano punti di aggiornamento software nel gruppo di limiti *A* per il fallback dopo **10** minuti. Si configura la stessa impostazione per il gruppo di limiti *B* per **130** minuti. Un client nel gruppo di limiti *Z* non riesce a raggiungere l'ultimo punto di aggiornamento software valido noto.

- Per i successivi 120 minuti, il client prova a raggiungere solo il server originale nel gruppo di limiti Z. Dopo 10 minuti, Configuration Manager aggiunge i punti di aggiornamento software del gruppo di limiti A al pool di server disponibili. Il client tuttavia non prova a contattare questi o altri server fino a che non è trascorso il periodo iniziale di 120 minuti.  

- Dopo avere provato a contattare il punto di aggiornamento software originale per 120 minuti, il client espande la ricerca. Aggiunge i server al pool disponibile di punti di aggiornamento software che si trovano nel gruppo di limiti corrente e in quelli adiacenti con una configurazione di 120 minuti o meno. Questo pool include i server nel gruppo di limiti A, aggiunti in precedenza al pool di server disponibili.  

- Dopo altri 10 minuti, il client espande la ricerca per includere i punti di aggiornamento software del gruppo di limiti B. Il tempo totale è di 130 minuti dopo il primo tentativo non riuscito del client di raggiungere l'ultimo punto di aggiornamento software valido noto.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Passare manualmente a un nuovo punto di aggiornamento software

Oltre a usare il fallback, usare la notifica client per forzare manualmente il passaggio di un dispositivo a un nuovo punto di aggiornamento software.

Quando si passa a un nuovo server, i dispositivi usano il fallback per trovare il nuovo server. I client passano al nuovo punto di aggiornamento software durante il successivo ciclo di analisi per aggiornamenti software.<!-- SCCMDocs#1537 -->

Esaminare le configurazioni del gruppo di limiti. Prima di apportare questa modifica, verificare che i punti di aggiornamento software si trovino nei gruppi di limiti corretti.

Per altre informazioni, vedere [Passaggio manuale dei client a un nuovo punto di aggiornamento software](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

## <a name="management-points"></a>Punti di gestione

<!-- 1324594 -->
Configurare relazioni di fallback per i punti di gestione tra gruppi di limiti. Questo comportamento consente un maggiore controllo per i punti di gestione usati dai client. Nella scheda **Relazioni** delle proprietà del gruppo di limiti è presente una colonna per il punto di gestione. Quando si aggiunge un nuovo gruppo di limiti di fallback, attualmente il tempo di fallback per il punto di gestione è sempre zero (0). Questo comportamento corrisponde all'opzione **Comportamento predefinito** del gruppo di limiti predefinito del sito.

Nelle versioni precedenti si verificava comunemente un problema in presenza di un punto di gestione protetto in una rete protetta. I client nella rete principale ricevevano criteri che includevano questo punto di gestione protetto, anche se non potevano comunicare con esso attraverso un firewall. Per risolvere il problema, usare ora l'opzione **Non eseguire mai il fallback** per assicurarsi che i client eseguano il fallback solo nei punti di gestione con cui possono comunicare.

> [!Note]  
> Se si abilitano i punti di distribuzione nel gruppo di limiti predefinito del sito per il fallback e un punto di gestione si trova nella stessa posizione di un punto di distribuzione, il sito aggiunge anche tale punto di gestione al gruppo di limiti predefinito del sito.<!--VSO 2841292-->  

Se un client si trova in un gruppo di limiti senza alcun punto di gestione assegnato, il sito fornisce al client l'intero elenco di punti di gestione. Questo comportamento garantisce che un client riceva sempre un elenco di punti di gestione.

Il comportamento del fallback dei gruppi di limiti dei punti di gestione non cambia durante l'installazione dei client (ccmsetup.exe). Se la riga di comando non specifica il punto di gestione iniziale tramite il parametro /MP, il nuovo client riceve l'elenco completo dei punti di gestione disponibili. Per il processo di avvio iniziale, il client usa il primo punto di gestione a cui può accedere. Una volta registratosi con il sito, il client riceve l'elenco dei punti di gestione correttamente ordinato con questo nuovo comportamento.

Per altre informazioni sul comportamento del client per acquisire il contenuto durante l'installazione, vedere [Installazione client](#bkmk_ccmsetup).

Durante l'aggiornamento del client, se non si specifica il parametro della riga di comando /MP, il client esegue query sulle origini, come Active Directory e WMI, per qualsiasi punto di gestione disponibile. L'aggiornamento dei client non rispetta la configurazione dei gruppi di limiti. <!--VSO 2841292-->  

Per consentire ai client di usare questa funzionalità, abilitare l'impostazione seguente: **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** in **Impostazioni gerarchia**.

> [!Note]  
> I processi di distribuzione dei sistemi operativi non sono a conoscenza dei gruppi di limiti per i punti di gestione.  

### <a name="troubleshooting"></a>Risoluzione dei problemi

Nel log **LocationServices.log** sono presenti nuove voci. L'attributo **Locality** identifica uno degli stati seguenti:

- **0**: Sconosciuto  

- **1**: il punto di gestione specificato si trova solo nel gruppo di limiti predefinito del sito per il fallback  

- **2**: il punto di gestione specificato si trova in un gruppo di limiti remoto o adiacente. Quando il punto di gestione si trova sia in un gruppo di limiti vicino sia in quello predefinito del sito, l'attributo locality è uguale a 2.  

- **3**: il punto di gestione specificato si trova nel gruppo di limiti locale o corrente. Quando il punto di gestione si trova sia nel gruppo di limiti corrente e in uno vicino o in quello predefinito del sito, l'attributo locality è uguale a 3. Se non si abilita l'impostazione dei punti di gestione preferiti in Impostazioni gerarchia, l'attributo locality è sempre uguale a 3, indipendentemente dal gruppo di limiti in cui si trova il punto di gestione.  

I client usano prima i punti di gestione locali (locality 3), quindi quelli remoti (locality 2) e infine eseguono il fallback (locality 1).

Quando un client riceve cinque errori in 10 minuti e non riesce a comunicare con un punto di gestione nel relativo gruppo di limiti corrente, cerca di contattare un punto di gestione in un gruppo di limiti adiacente o in quello predefinito del sito. Se in seguito il punto di gestione nel gruppo di limiti corrente torna online, il client torna al punto di gestione locale al successivo ciclo di aggiornamento. Il ciclo di aggiornamento avviene ogni 24 ore o al riavvio del servizio agente di Configuration Manager.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a> Punti di gestione preferiti

> [!Note]
> Il comportamento dell'impostazione per la gerarchia **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** è cambiato a partire dalla versione 1802. Quando si abilita questa impostazione, Configuration Manager usa la funzionalità del gruppo di limiti per il punto di gestione assegnato. Per altre informazioni, vedere [Punti di gestione](#management-points).

I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

- Il client prova a usare un punto di gestione preferito del sito assegnato prima di usarne uno non configurato come preferito per il sito assegnato.  

- Per usare questa opzione, abilitare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** in **Impostazioni gerarchia**. Configurare quindi i gruppi di limiti nei singoli siti primari. Includere i punti di gestione che devono essere associati ai limiti associati del gruppo di limiti. Per altre informazioni, vedere [Abilitare l'uso dei punti di gestione preferiti](boundary-group-procedures.md#bkmk_proc-prefer).  

- Quando si configurano i punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio del relativo elenco. Questo elenco include tutti i punti di gestione dal sito assegnato del client.  

> [!NOTE]  
> Il roaming del client si ha quando vengono modificati i percorsi di rete, ad esempio quando un computer portatile viene spostato in un ufficio remoto. Quando un client effettua il roaming, è possibile che usi un punto di gestione del sito locale prima di provare a usare un server del sito assegnato. Questo elenco di server dal sito assegnato include i punti di gestione preferiti. Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Limiti sovrapposti  

Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto. Quando il percorso di rete del client appartiene a più gruppi di limiti:

- Quando un client richiede il contenuto, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno contenuto.  

- Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  

## <a name="example-of-using-boundary-groups"></a>Esempio d'uso dei gruppi di limiti

L'esempio seguente usa un client che esegue la ricerca di contenuto da un punto di distribuzione. Questo esempio può essere applicato ad altri ruoli del sistema del sito che usano i gruppi di limiti.

Creare tre gruppi di limiti che non condividono i limiti o i server del sistema del sito:  

- Gruppo BG_A con punti di distribuzione DP_A1 e DP_A2  

- Gruppo BG_B con punti di distribuzione DP_B1 e DP_B2  

- Gruppo BG_C con punti di distribuzione DP_C1 e DP_C2  

Aggiungere i percorsi di rete dei client come limiti solo al gruppo di limiti BG_A. Configurare quindi le relazioni da tale gruppo di limiti per gli altri due gruppi di limiti:  

- Configurare i punti di distribuzione per il primo gruppo *adiacente* (BG_B) da usare dopo 10 minuti. Questo gruppo contiene i punti di distribuzione DP_B1 e DP_B2. Entrambi sono ben connessi ai percorsi dei limiti del primo gruppo.  

- Configurare il secondo gruppo *adiacente* (BG_C) da usare dopo 20 minuti. Questo gruppo contiene i punti di distribuzione DP_C1 e DP_C2. Entrambi si trovano a un WAN rispetto agli altri due gruppi limite.  

- Aggiungere anche al gruppo di limiti del sito predefinito un punto di distribuzione aggiuntivo che si trova nel server del sito. Questo server è il percorso di origine del contenuto meno preferito, ma si trova in posizione centrale per tutti i gruppi di limiti.

    Esempio di gruppi limite e tempi di fallback:

    ![Esempio di gruppi di limiti e tempi di fallback](media/BG_Fallback.png)  

Con questa configurazione:  

- Il client inizia la ricerca di contenuto dai punti di distribuzione nel gruppo di limiti *corrente* (BG_A). Cerca ogni punto di distribuzione per due minuti e quindi passa al punto di distribuzione successivo nel gruppo di limiti. Il pool di percorsi di origine del contenuto validi del client include DP_A1 e DP_A2.  

- Se il client non riesce a trovare il contenuto nel proprio gruppo limite *corrente* dopo 10 minuti di ricerca, aggiunge i punti di distribuzione dal gruppo limite BG_B alla ricerca. Prosegue quindi la ricerca di contenuto da un punto di distribuzione nel relativo pool combinato di server. Questo pool include ora i server dei gruppi di limiti BG_A e BG_B. Il client continua a contattare ogni punto di distribuzione per due minuti prima di passare al server successivo del pool. Il pool di percorsi di origine del contenuto validi del client include DP_A1, DP_A2, DP_B1 e DP_B2.  

- Dopo altri 10 minuti (20 minuti in totale), se il client non ha ancora trovato un punto di distribuzione con contenuto, espande il proprio pool per includere i server disponibili del secondo gruppo *adiacente*, il gruppo di limiti BG_C. Ora il client esegue la ricerca in sei punti di distribuzione: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2. Continua la modifica in un nuovo punto di distribuzione ogni due minuti finché non trova il contenuto.  

- Se il client non ha trovato contenuto dopo un totale di 120 minuti, esegue il fallback per includere il *gruppo di limiti del sito predefinito* nella ricerca. Il pool include ora tutti i punti di distribuzione dei tre gruppi di limiti configurati e il punto di distribuzione finale presente nel server del sito. Il client continua quindi la ricerca del contenuto, modificando i punti di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.  

Configurando i diversi gruppi adiacenti in modo da renderli disponibili in momenti diversi, è possibile controllare quando i punti di distribuzione specifici vengono aggiunti come percorso di origine del contenuto. Il client usa il fallback al gruppo di limiti del sito predefinito come garanzia per il contenuto che non è disponibile negli altri percorsi.

## <a name="changes-from-prior-versions"></a>Modifiche rispetto alle versioni precedenti

Di seguito sono riportate le modifiche principali ai gruppi di limiti e alle modalità di ricerca del contenuto da parte dei client in Configuration Manager Current Branch. Molti di queste modifiche e concetti funzionano in combinazione.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Rimozione delle configurazioni per i punti lenti o veloci

I singoli punti di distribuzione non vengono più configurati come punti di distribuzione lenti o veloci. Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente. Grazie a questa modifica, la scheda **Riferimenti** delle proprietà del gruppo limite non supporta la configurazione Veloce o Lento.  

### <a name="new-default-boundary-group-at-each-site"></a>Nuovo gruppo di limiti predefinito in ogni sito

Ogni sito primario ha un nuovo gruppo di limiti predefinito denominato **Default-Site-Boundary-Group&lt;codicesito>** . Quando un client non si trova in un percorso di rete assegnato a un gruppo di limiti, usa i sistemi del sito associati al gruppo predefinito del sito assegnato. Considerare l'uso di questo gruppo limite come sostituzione del concetto di percorso del contenuto di fallback.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>Rimozione dell'opzione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto)

La configurazione di un punto di distribuzione da usare per il fallback non avviene più in modo esplicito. Le opzioni per configurare questa impostazione vengono rimosse dalla console.

Il risultato dell'impostazione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) in un tipo di distribuzione per le applicazioni cambia. Questa impostazione su un tipo di distribuzione consente ora al client di usare il gruppo limite del sito predefinito come percorso di origine del contenuto.

#### <a name="boundary-groups-relationships"></a>Relazioni tra gruppi di limiti

È possibile collegare ogni gruppo di limiti a uno o più gruppi di limiti aggiuntivi. Questi collegamenti formano relazioni che è possibile configurare nella nuova scheda delle proprietà del gruppo di limiti denominata **Relazioni**:  

- Ogni gruppo limite associato direttamente a un client viene chiamato gruppo limite **corrente**.  

- Qualsiasi gruppo di limiti che un client può usare grazie all'associazione tra il gruppo di limiti *corrente* del client e un altro gruppo viene chiamato gruppo di limiti **adiacente**.  

- Nella scheda **Relazioni** aggiungere gruppi di limiti da usare come gruppo di limiti *adiacente*. Configurare anche un tempo in minuti per il fallback. Nel momento in cui un client non riesce a trovare il contenuto da un punto di distribuzione nel gruppo *corrente* avvia la ricerca dei percorsi del contenuto nei gruppi di limiti *adiacenti*.  

    Quando si aggiunge o si modifica una configurazione del gruppo di limiti, è possibile bloccare il fallback in tale gruppo di limiti dal gruppo corrente che si sta configurando.  

Per usare la nuova configurazione, definire le associazioni esplicite (collegamenti) da un gruppo di limiti a un altro. Configurare tutti i punti di distribuzione in tale gruppo associato con la stessa durata in minuti. Quando un client non riesce a trovare l'origine di un contenuto del relativo gruppo di limiti *corrente*, il tempo configurato determina quando può iniziare a cercare le origini del contenuto nel gruppo di limiti adiacente.

Oltre ai gruppi limite configurati in modo esplicito, ogni gruppo limite dispone di un collegamento implicito al gruppo limite del sito predefinito. Il collegamento diventa attivo dopo 120 minuti. Il gruppo di limiti del sito predefinito diventa quindi un gruppo di limiti adiacente. Questo comportamento consente ai client di usare come percorsi di origine del contenuto i punti di distribuzione associati a quel gruppo di limiti.

Questo comportamento sostituisce ciò che in precedenza veniva definito "fallback per il contenuto". Eseguire l'override di questo comportamento predefinito di 120 minuti associando in modo esplicito il gruppo di limiti del sito predefinito a un gruppo *corrente*. Impostare un periodo di tempo specifico in minuti o bloccare completamente il fallback per impedirne l'uso.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>I client provano a ottenere il contenuto da ogni punto di distribuzione per un massimo di due minuti

Quando un client cerca un percorso di origine del contenuto, prova ad accedere a ogni punto di distribuzione per due minuti prima di passare a un altro punto di distribuzione. Questo comportamento è diverso rispetto alle versioni precedenti in cui i client provavano a connettersi a un punto di distribuzione per un massimo di due ore.

- I client selezionano casualmente il primo punto di distribuzione dal pool dei server disponibili nel gruppo (o nei gruppi) di limiti *corrente* del client.  

- Dopo due minuti, se il client non ha trovato il contenuto, passa a un nuovo punto di distribuzione e prova a ottenere il contenuto da tale server. Questo processo viene ripetuto ogni due minuti fino a quando il client trova il contenuto o raggiunge l'ultimo server del pool.  

- Se un client non trova un percorso di origine del contenuto valido nel pool *corrente* prima di raggiungere l'intervallo di fallback in un gruppo di limiti *adiacente*, il client aggiunge i punti di distribuzione del gruppo *adiacente* alla fine dell'elenco corrente. e quindi cerca nel gruppo espanso di percorsi di origine che include i punti di distribuzione di entrambi i gruppi di limiti.  

    > [!TIP]  
    > Quando si crea un collegamento esplicito tra il gruppo di limiti corrente e il gruppo di limiti del sito predefinito e si definisce un intervallo di fallback inferiore al tempo di fallback per il collegamento a un gruppo di limiti adiacente, i client iniziano la ricerca dei percorsi di origine dal gruppo di limiti del sito predefinito prima di includere il gruppo adiacente.  

- Quando il client non riesce a ottenere il contenuto dall'ultimo server nel pool, avvia nuovamente il processo.  

## <a name="see-also"></a>Vedere anche

- [Procedure per i gruppi di limiti](boundary-group-procedures.md)  

- [Informazioni sui limiti](boundaries.md)  

- [Concetti di base sulla gestione dei contenuti](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
