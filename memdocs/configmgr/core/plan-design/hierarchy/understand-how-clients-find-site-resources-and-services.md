---
title: Trovare risorse del sito
titleSuffix: Configuration Manager
description: Informazioni su come e quando i client di Configuration Manager usano la posizione del servizio per trovare le risorse del sito.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a72ff9947f6ca31ce2158c5c763602b34948a15c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075660"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>Informazioni su come i client trovano i servizi e le risorse del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I client di Configuration Manager usano un processo denominato *posizione del servizio* per individuare i server del sistema del sito con cui possono comunicare e che offrono i servizi che i client devono usare. Se si comprende come e quando i client usano la posizione del servizio per trovare le risorse del sito, è possibile configurare i siti in modo da supportare correttamente le attività client. Queste configurazioni possono richiedere l'interazione del sito con configurazioni di rete e di dominio come Active Directory Domain Services e DNS. In alternativa possono richiedere la configurazione di soluzioni alternative più complesse.  

Ecco alcuni esempi di ruoli del sistema del sito che forniscono servizi:

- Il server del sistema del sito principale per i client.
- Il punto di gestione.
- Altri server del sistema del sito con cui il client può comunicare, come i punti di distribuzione e i punti di aggiornamento software.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Nozioni fondamentali sulla posizione del servizio  
 Un client valuta il suo percorso di rete corrente, la preferenza del protocollo di comunicazione e il sito assegnato quando usa la posizione del servizio per trovare un punto di gestione con cui può comunicare.  

**Un client comunica con un punto di gestione per:**  
- Scaricare informazioni sugli altri punti di gestione per il sito, in modo da creare un *elenco dei punti di gestione* noti per i cicli futuri di individuazione della posizione del servizio.  
- Caricare i dettagli di configurazione, ad esempio inventario e stato.  
- Scaricare i criteri che impostano le configurazioni nel client e possono informare il client in merito al software che può o deve installare e altre attività correlate.  
- Richiedere informazioni su altri ruoli del sistema del sito che forniscono servizi il cui uso è stato configurato nel client. Gli esempi includono i punti di distribuzione per il software che il client può installare o un punto di aggiornamento software da cui ottenere gli aggiornamenti.  

**Un client di Configuration Manager esegue una richiesta di posizione del servizio:**  
- Ogni 25 ore di funzionamento continuativo.  
- Quando il client rileva una modifica della propria posizione o configurazione di rete.  
- Quando il servizio **ccmexec.exe** nel computer, vale a dire il servizio client di base, viene avviato.  
- Quando il client deve trovare un ruolo del sistema del sito che fornisce un servizio necessario.  

**Quando un client tenta di individuare i server che ospitano i ruoli del sistema del sito**, usa la posizione del servizio per individuare un ruolo del sistema del sito che supporta il protocollo del client (HTTP o HTTPS). Per impostazione predefinita, i client utilizzano il metodo più sicuro a loro disposizione. Considerare quanto segue:  

- Per usare HTTPS, è necessario disporre di un'infrastruttura a chiave pubblica (PKI) e installare i certificati PKI sui client e sui server. Per informazioni sulle modalità di utilizzo dei certificati, vedere [Requisiti dei certificati PKI per Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

- Quando si distribuisce un ruolo del sistema del sito che usa Internet Information Services (IIS) e supporta le comunicazioni dai client, è necessario specificare se i client si connettono al sistema del sito tramite HTTP o HTTPS. Se si usa HTTP, è necessario considerare anche le opzioni di firma e crittografia. Per altre informazioni, vedere [Pianificazione di firma e crittografia](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in [Pianificare la sicurezza](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato  
Quando un client viene assegnato per la prima volta a un sito primario, seleziona un punto di gestione predefinito per tale sito. I siti primari supportano più punti di gestione e ogni client identifica in modo indipendente un punto di gestione come proprio punto di gestione predefinito. Questo punto di gestione predefinito diventa quindi il punto di gestione assegnato di tale client. È anche possibile usare i comandi di installazione client per impostare il punto di gestione assegnato per un client al momento dell'installazione.  

Un client seleziona un punto di gestione con cui comunicare in base al relativo percorso di rete corrente e alle configurazioni del gruppo di limiti. Anche se ha un punto di gestione assegnato, questo potrebbe non essere il punto di gestione usato dal client.  

> [!NOTE]  
> Un client usa sempre il punto di gestione assegnato per i messaggi di registrazione e per alcuni messaggi di criteri, anche quando vengono inviate altre comunicazioni a un punto di gestione proxy o locale.

È possibile usare i punti di gestione preferiti. I punti di gestione preferiti sono punti di gestione del sito assegnato di un client associati a un gruppo di limiti che il client usa per individuare i server del sistema del sito. L'associazione di un punto di gestione preferito a un gruppo di limiti come server del sistema del sito è simile al modo in cui i punti di distribuzione o i punti di migrazione stato sono associati a un gruppo di limiti. Se si abilitano i punti di gestione preferiti per la gerarchia, quando un client usa un punto di gestione dal sito assegnato, verrà effettuato un tentativo di usare un punto di gestione preferito prima di altri punti di gestione dal sito assegnato.  

Per configurare l'affinità del punto di gestione, è possibile usare anche le informazioni nel blog dedicato all'[affinità del punto di gestione](https://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx) su TechNet.com. L'affinità del punto di gestione esegue l'override del comportamento predefinito per i punti di gestione assegnati e consente al client di usare uno o più punti di gestione specifici.  

Ogni volta che un client deve contattare un punto di gestione, controlla l'elenco dei punti di gestione archiviato in locale in Windows Management Instrumentation (WMI). Il client crea un elenco di punti di gestione iniziale quando viene installato. Successivamente aggiorna periodicamente l'elenco con informazioni dettagliate su ogni punto di gestione nella gerarchia.  

Quando non riesce a trovare un punto di gestione valido nel proprio elenco di punti di gestione, il client esegue una ricerca nelle seguenti origini di posizioni del servizio, in ordine, finché non trova un punto di gestione da usare:  

1.  Punto di gestione  
2.  Servizi di dominio Active Directory  
3.  DNS  
4.  WINS  

Dopo avere individuato e contattato un punto di gestione, il client scarica l'elenco corrente dei punti di gestione disponibili nella gerarchia e aggiorna l'elenco locale. Questo vale per i client appartenenti o non appartenenti a un dominio.  

Ad esempio, quando un client di Configuration Manager che si trova su Internet si connette a un punto di gestione basato su Internet, il punto di gestione invia a tale client un elenco di punti di gestione basati su Internet disponibili nel sito. Analogamente, anche i client appartenenti a un dominio o in gruppi di lavoro ricevono l'elenco dei punti di gestione che possono usare.  

A un client non configurato per Internet non vengono forniti punti di gestione solo per Internet. I client di gruppi di lavoro configurati per Internet comunicano solo con punti di gestione per Internet.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a> Elenco dei punti di gestione  
L'elenco dei punti di gestione è l'origine preferita per la posizione del servizio per un client perché si tratta di un elenco dei punti di gestione identificati in precedenza dal client, in ordine di priorità. Questo elenco viene ordinato per client, in base alla relativa posizione di rete al momento dell'aggiornamento dell'elenco, quindi viene archiviato in locale sul client in WMI.  

### <a name="building-the-initial-mp-list"></a>Creazione dell'elenco dei punti di gestione iniziale  
Durante l'installazione del client vengono usate le regole seguenti per creare l'elenco dei punti di gestione iniziale del client:  

- L'elenco iniziale include i punti di gestione specificati durante l'installazione del client (quando si usa l'opzione **SMSMP**= o **/MP**).  
- Il client esegue una query in Active Directory Domain Services alla ricerca dei punti di gestione pubblicati. Affinché possa essere identificato da Active Directory Domain Services, è necessario che il punto di gestione provenga dal sito assegnato del client e che abbia la stessa versione di prodotto del client.  
- Se durante l'installazione del client non è stato specificato alcun punto di gestione, e lo schema di Active Directory non è esteso, il client ricerca in DNS e WINS i punti di gestione pubblicati.  
- Quando il client crea l'elenco iniziale, alcuni punti di gestione nella gerarchia potrebbero non essere noti.  

### <a name="organizing-the-mp-list"></a>Organizzazione dell'elenco dei punti di gestione  
I client organizzano il proprio elenco dei punti di gestione usando le classificazioni seguenti:  

- **Proxy**: punto di gestione in un sito secondario.  
- **Locale**: qualsiasi punto di gestione associato al percorso di rete corrente del client definito dai limiti del sito. Per i limiti, tenere presente quanto segue:
  - Quando un client appartiene a più gruppi di limiti, l'elenco dei punti di gestione locali è determinato dall'unione di tutti i limiti che includono il percorso di rete corrente del client.  
  - In genere, i punti di gestione locali sono un sottoinsieme dei punti di gestione assegnati di un client, a meno che il client non si trovi in un percorso di rete associato a un altro sito con punti di gestione che servono i relativi gruppi di limiti.   


- **Assegnato**: punto di gestione che è un sistema del sito per il sito assegnato del client.  

È possibile usare i punti di gestione preferiti. I punti di gestione di un sito che non sono associati a un gruppo di limiti o che non sono in un gruppo di limiti associato al percorso di rete corrente del client, non sono considerati preferiti. Vengono usati quando il client non riesce a identificare un punto di gestione preferito disponibile.  

### <a name="selecting-a-management-point-to-use"></a>Selezione di un punto di gestione da usare  
Per le comunicazioni tipiche, un client tenta di usare un punto di gestione dalle classificazioni nell'ordine seguente, in base al percorso di rete del client:  

1.  Proxy  
2.  Locale  
3.  Assegnato  

Tuttavia, il client usa sempre il punto di gestione assegnato per i messaggi di registrazione e per alcuni messaggi di criteri, anche quando vengono inviate altre comunicazioni a un punto di gestione proxy o locale.  

All'interno di ogni classificazione (Proxy, Locale o Assegnato), il client tenta di usare un punto di gestione in base alle preferenze, nell'ordine seguente:  

1.  Idoneo per HTTPS in una foresta trusted o locale (quando il client è configurato per le comunicazioni HTTPS)  
2.  Idoneo per HTTPS non in una foresta trusted o locale (quando il client è configurato per le comunicazioni HTTPS)  
3.  Idoneo per HTTP in una foresta trusted o locale  
4.  Idoneo per HTTP non in una foresta trusted o locale  

Dal set di punti di gestione ordinato in base alle preferenze, il client tenta di usare il primo punto di gestione nell'elenco. Questo elenco ordinato di punti di gestione è casuale e non può essere ordinato. L'ordine può cambiare ogni volta che il client aggiorna il proprio elenco dei punti di gestione.  

Quando un client non riesce a mettersi in contatto con il primo punto di gestione, tenta ogni punto di gestione successivo nell'elenco. Inizia dai punti di gestione preferiti nella classificazione per poi passare a quelli non preferiti. Se un client non riesce a comunicare con nessun punto di gestione della classificazione, tenta di contattare un punto di gestione preferito della classificazione successiva e così via fino a quando non individua un punto di gestione da usare.  

Dopo aver stabilito la comunicazione con un punto di gestione, un client continua a usare lo stesso punto di gestione fino a quando:  

- Non sono trascorse 25 ore.  
- Il client non riesce a comunicare con il punto di gestione per cinque tentativi in un periodo di 10 minuti.

A quel punto il client seleziona casualmente un nuovo punto di gestione da usare.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a> Active Directory  
I client appartenenti a un dominio possono usare Servizi di dominio Active Directory per la posizione del servizio. Questa operazione richiede che i siti [pubblichino dati in Active Directory](https://technet.microsoft.com/library/hh696543.aspx).  

Un client può usare Active Directory Domain Services per la posizione del servizio quando si verificano tutte le condizioni seguenti:  

- Lo [schema di Active Directory è stato esteso](https://technet.microsoft.com/library/mt345589.aspx) o è stato esteso per System Center 2012 Configuration Manager.  
- La [foresta Active Directory è configurata per la pubblicazione](https://technet.microsoft.com/library/hh696542.aspx) e i siti di Configuration Manager sono configurati per la pubblicazione.  
- Il computer client è membro di un dominio Active Directory ed è in grado di accedere a un server di catalogo globale.  

Se un client non trova un punto di gestione da usare per la posizione del servizio in Active Directory Domain Services, tenta di usare DNS.  

##  <a name="dns"></a><a name="bkmk_dns"></a> DNS  
I client sulla Intranet possono usare DNS per il percorso del servizio. In questo caso è necessario almeno un sito in una gerarchia per pubblicare informazioni sui punti di gestione in DNS.  

È consigliabile usare DNS per la posizione del servizio in presenza di una delle condizioni seguenti:
- Lo schema di Active Directory Domain Services non viene esteso per supportare Configuration Manager.
- I client della Intranet si trovano in una foresta che non è abilitata per la pubblicazione in Configuration Manager.  
- Sono presenti client nei computer del gruppo di lavoro che non sono configurati per la gestione client basata solo su Internet (un client del gruppo di lavoro configurato per Internet comunicherà solo con i punti di gestione per Internet e non userà DNS per la posizione del servizio).  
- È possibile [configurare i client per individuare i punti di gestione da DNS](https://technet.microsoft.com/library/gg682055).  

Quando un sito pubblica i record di individuazione del servizio per i punti di gestione in DNS:  

- La pubblicazione è applicabile solo ai punti di gestione che accettano le connessioni client dalla rete Intranet.  
- La pubblicazione aggiunge un record di risorse di posizione del servizio nella zona DNS del computer del punto di gestione. Deve essere presente una voce host corrispondente in DNS per il computer.  

Per impostazione predefinita, i client aggiunti a un dominio cercano in DNS i record dei punti di gestione provenienti dal dominio locale del client. È possibile configurare una proprietà client che specifica un suffisso di dominio per un dominio in cui le informazioni relative ai punti di gestione vengono pubblicate in DNS.  

Per altre informazioni su come configurare la proprietà client del suffisso DNS, vedere [Come configurare i computer client per trovare i punti di gestione usando la pubblicazione DNS](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Se un client non trova un punto di gestione da usare per la posizione del servizio in DNS, tenta di usare WINS.  

### <a name="publish-management-points-to-dns"></a>Pubblicare punti di gestione in DNS  
Per pubblicare punti di gestione in DNS, devono verificarsi le due condizioni seguenti:  

- I server DNS supportano i record di risorse di individuazione del servizio usando una versione di BIND corrispondente a 8.1.2.  
- Gli FQDN Intranet specificati per i punti di gestione in Configuration Manager includono voci host, ad esempio record A, in DNS.  

> [!IMPORTANT]  
> La pubblicazione DNS in Configuration Manager non supporta uno spazio dei nomi indipendente. Se si ha uno spazio dei nomi indipendente, è possibile pubblicare manualmente i punti di gestione in DNS o usare uno degli altri metodi alternativi di individuazione del servizio documentati in questa sezione.  

**Quando i server DNS supportano gli aggiornamenti automatici**, è possibile configurare Configuration Manager per la pubblicazione automatica dei punti di gestione della Intranet in DNS oppure per la pubblicazione manuale di tali record in DNS. Quando i punti di gestione vengono pubblicati in DNS, il nome FQDN Intranet e il numero di porta corrispondenti sono pubblicati nel record di individuazione del servizio (SRV). La pubblicazione DNS in un sito viene configurata nelle proprietà del componente del punto di gestione dei siti. Per altre informazioni, vedere [Componenti del sito per Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**Quando la zona DNS è impostata su "Secure only" (Solo protetti) per gli aggiornamenti dinamici**, solo il primo punto di gestione da pubblicare in DNS riesce a eseguire correttamente l'operazione con le autorizzazioni predefinite.

Se solo un punto di gestione riesce a pubblicare e modificare il proprio record DNS e il server del punto di gestione è integro, i client possono ottenere l'elenco completo dei punti di gestione e quindi trovare quello preferito.


**Quando i server DNS non supportano gli aggiornamenti automatici ma supportano i record di individuazione del servizio**, è possibile pubblicare manualmente i punti di gestione in DNS. A tale scopo, è necessario specificare manualmente il record di risorse di individuazione del servizio (SRV RR) in DNS.  

Configuration Manager supporta RFC 2782 per i record relativi alla posizione del servizio. I record hanno il formato seguente: *_Servizio._Proto.Nome TTL Classe SRV Priorità Peso Porta Destinazione*  

Per pubblicare un punto di gestione in Configuration Manager, specificare i valori seguenti:  

- **_Service**: immettere **_mssms_mp**_&lt;sitecode\>, dove &lt;sitecode\> è il codice del sito del punto di gestione.  
- **._Proto**: specificare **._tcp**.  
- **.Name**: immettere il suffisso DNS del punto di gestione, ad esempio **contoso.com**.  
- **TTL**: immettere **14400**, che corrisponde a quattro ore.  
- **Classe**: specificare **IN** (in conformità con RFC 1035).  
- **Priorità**: questo campo non è usato da Configuration Manager.
- **Peso**: questo campo non è usato da Configuration Manager.  
- **Porta**: immettere il numero di porta usato dal punto di gestione, ad esempio **80** per HTTP e **443** per HTTPS.  

  > [!NOTE]  
  >  La porta dei record SRV deve corrispondere alla porta di comunicazione usata dal punto di gestione. Per impostazione predefinita si tratta della porta **80** per le comunicazioni HTTP e **443** per le comunicazioni HTTPS.  

- **Destinazione**: Immettere il nome FQDN Intranet specificato per il sistema del sito configurato con il ruolo del sito del punto di gestione.  

Se si usa il DNS di Windows Server, è possibile usare la procedura seguente per immettere questo record DNS per i punti di gestione Intranet. Se si usa un'implementazione differente per DNS, usare le informazioni riportate in questa sezione sui valori dei campi e consultare la documentazione relativa al DNS per adattare questa procedura.  

##### <a name="to-configure-automatic-publishing"></a>Per configurare la pubblicazione automatica:  

1.  Nella console di Configuration Manager espandere **Amministrazione** > **Configurazione del sito** > **Siti**.  

2.  Selezionare il sito e quindi fare clic su **Configura componenti del sito**.  

3.  Scegliere **Punto di gestione**.  

4.  Selezionare i punti di gestione da pubblicare. Questa selezione vale per la pubblicazione in Active Directory Domain Services e DNS.  

5.  Selezionare la casella per la pubblicazione in DNS. Questa casella:  

    - Consente di selezionare i punti di gestione per la pubblicazione in DNS.  

    - Non consente di configurare la pubblicazione in Active Directory Domain Services.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Per pubblicare manualmente i punti di gestione in DNS in Windows Server  

1.  Nella console di Configuration Manager specificare i nomi FQDN Intranet dei sistemi del sito.  

2.  Nella console di gestione DNS selezionare la zona DNS per il computer del punto di gestione.  

3.  Verificare che sia presente un record host (A o AAAA) per il nome FQDN Intranet del sistema del sito. Se il record non esiste, crearlo.  

4.  Usando l'opzione **Altri nuovi record**, scegliere **Posizione servizio (SRV)** nella finestra di dialogo **Tipo record di risorse**, scegliere **Crea record**, immettere le informazioni seguenti e infine scegliere **Chiudi**:  

    - **Dominio**: Se necessario, immettere il suffisso DNS del punto di gestione, ad esempio **contoso.com**.  
    - **Servizio**: digitare **_mssms_mp**_&lt;sitecode\>, dove &lt;sitecode\> è il codice del sito del punto di gestione.  
    - **Protocollo**: digitare **_tcp**.  
    - **Priorità**: questo campo non è usato da Configuration Manager.  
    - **Peso**: questo campo non è usato da Configuration Manager.  
    - **Porta**: immettere il numero di porta usato dal punto di gestione, ad esempio **80** per HTTP e **443** per HTTPS.  

      > [!NOTE]  
      > La porta dei record SRV deve corrispondere alla porta di comunicazione usata dal punto di gestione. Per impostazione predefinita si tratta della porta **80** per le comunicazioni HTTP e **443** per le comunicazioni HTTPS.  

    - **Host offering this service** (Host che offre questo servizio): Immettere il nome FQDN Intranet specificato per il sistema del sito configurato con il ruolo del sito del punto di gestione.  

Ripetere questi passaggi per ogni punto di gestione della rete Intranet che si desidera pubblicare in DNS.  

##  <a name="wins"></a><a name="bkmk_wins"></a> WINS  
Quando gli altri meccanismi di individuazione del servizio hanno esito negativo, i client possono trovare un punto di gestione iniziale tramite WINS.  

Per impostazione predefinita, un sito primario pubblica in WINS il primo punto di gestione nel sito configurato per HTTP e il primo punto di gestione configurato per HTTPS.  

Se non si desidera che i client trovino un punto di gestione HTTP in WINS, configurare i client con la proprietà CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  
