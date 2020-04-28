---
title: Disponibilità elevata
titleSuffix: Configuration Manager
description: Informazioni su come distribuire Configuration Manager usando opzioni che consentono di mantenere un livello elevato di disponibilità dei servizi.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073314"
---
# <a name="high-availability-options-for-configuration-manager"></a>Opzioni di disponibilità elevata per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo descrive come distribuire Configuration Manager usando opzioni che consentono di mantenere un livello elevato di disponibilità dei servizi.

Le seguenti opzioni di Configuration Manager supportano la disponibilità elevata:

- Configurare i siti primari autonomi con un server del sito aggiuntivo in modalità passiva.  

- Configurare un gruppo di disponibilità Always On di SQL Server per il database del sito nei siti primari e nel sito di amministrazione centrale.

- I siti supportano più istanze dei ruoli del sistema del sito che forniscono importanti servizi ai client, ad esempio i punti di gestione e i punti di distribuzione.  

- I siti di amministrazione centrale e primari supportano il backup del database del sito. Il database del sito archivia tutte le configurazioni per i siti e i client. I siti di una gerarchia condividono questi dati di configurazione.  

- Le opzione di ripristino sito predefinite possono ridurre il tempo di inattività del server. Queste opzioni avanzate semplificano il ripristino quando si ha una gerarchia con un sito di amministrazione centrale.  

- I client possono correggere automaticamente problemi tipici senza intervento amministrativo.  

- I siti generano avvisi relativi ai client che non riescono a inviare dati recenti, che informano gli amministratori di potenziali problemi.  

- Configuration Manager fornisce diversi report e dashboard predefiniti. Usarli per identificare i problemi e le tendenze prima che diventino un problema per il funzionamento di server e client.  

Configuration Manager include diverse funzionalità che forniscono il servizio in tempo quasi reale. Se queste funzionalità sono fondamentali per soddisfare i requisiti aziendali, pianificare e configurare i siti e le gerarchie per la disponibilità elevata. Ad esempio:  

- [Azioni di notifica client](../../../clients/manage/manage-clients.md), ad esempio riavvio, analisi di Windows Defender iniziali o desktop remoto.  

- Messaggi basati sullo stato per le funzionalità di monitoraggio, ad esempio aggiornamenti software e protezione degli endpoint.

- [Script](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Le altre funzionalità di Configuration Manager non forniscono il servizio in tempo reale. Queste funzionalità includono, a titolo esemplificativo, impostazioni client, inventario hardware e software, distribuzioni software e impostazioni di conformità. È previsto che funzionino con una certa latenza dei dati. È insolito che la maggior parte degli scenari che comportano un'interruzione temporanea del servizio costituisca un problema critico. Per ridurre al minimo il tempo di inattività, mantenere l'autonomia di funzionamento e fornire un alto livello di servizio, configurare i siti e le gerarchie con la disponibilità elevata.  

Ad esempio, i client di Configuration Manager in genere funzionano in maniera autonoma tramite pianificazioni e configurazioni note delle operazioni, nonché tramite pianificazioni per l'invio di dati al sito per l'elaborazione.  

- Quando i client non riescono a contattare il sito, memorizzano nella cache i dati e li inviano solo quando riescono a contattare il sito.  

- I client che non riescono a contattare il sito continuano a funzionare. Usano le informazioni memorizzate nella cache e le pianificazioni note più recenti, finché non riescono a contattare il sito e ricevono nuovi criteri. Un client, ad esempio, può conservare un'applicazione scaricata precedentemente da eseguire o installare.

- Il sito monitora i sistemi del sito e i client per verificare la disponibilità di aggiornamenti dello stato periodici. Può generare avvisi quando la registrazione di questi componenti non riesce.  

- I report predefiniti forniscono informazioni su operazioni in corso, operazioni storiche e tendenze correnti. Configuration Manager supporta anche messaggi basati sullo stato che forniscono informazioni quasi in tempo reale sulle operazioni in corso.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a> Disponibilità elevata per siti e gerarchie  

### <a name="use-a-site-server-in-passive-mode"></a>Usare un server del sito in modalità passiva

Installare un server del sito aggiuntivo in modalità *passiva* per un sito primario autonomo. Il server del sito in modalità passiva è in aggiunta al server del sito esistente in modalità *attiva*. Un server del sito in modalità passiva è disponibile per l'uso immediato, quando è necessario. Per altre informazioni, vedere [Disponibilità elevata del server del sito](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Usare una raccolta contenuto remota

Spostare la raccolta contenuto del sito in una posizione remota che fornisca uno spazio di archiviazione a disponibilità elevata. Questa funzionalità è un requisito per la disponibilità elevata del server del sito. Per altre informazioni, vedere [Raccolta contenuto](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="centralize-content-sources"></a>Centralizzare le origini contenuto

Tutto il contenuto software in Configuration Manager richiede un percorso di origine del pacchetto in rete. Usare uno spazio di archiviazione centralizzato a disponibilità elevata per ospitare un percorso di origine del pacchetto comune per tutto il contenuto.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Usare un gruppo di disponibilità SQL Server Always On per ospitare il database del sito

Ospitare il database del sito nei siti primari e nel sito di amministrazione centrale nei gruppi di disponibilità Always On di SQL Server. Per altre informazioni, vedere [SQL Server Always On per database del sito a disponibilità elevata](sql-server-alwayson-for-a-highly-available-site-database.md).  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Utilizzare un cluster SQL Server per ospitare il database del sito

Quando si utilizza un cluster SQL Server per il database su un sito di amministrazione centrale o primario, si utilizza il supporto di failover integrato in SQL Server.  

I siti secondari non possono usare un cluster di SQL Server e non supportano il backup o il ripristino del database del sito. Ripristinare un sito secondario reinstallando il sito secondario dal relativo sito primario padre.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Distribuire una gerarchia di siti con un sito di amministrazione centrale e uno o più siti primari figlio

Questa configurazione può fornire una tolleranza d'errore quando i siti gestiscono segmenti di rete con sovrapposizione. Offre anche un'opzione di ripristino aggiuntiva per usare le informazioni nel database condiviso disponibile su un altro sito per ricreare il database del sito sul sito ripristinato. Usare questa opzione per sostituire un backup non riuscito o non disponibile del database di un sito non funzionante.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Creare backup regolari in siti di amministrazione centrale e primari

Creando e testando un normale backup del sito, ci si assicura di avere i dati necessari per ripristinare un sito e si impara come ripristinare un sito in una quantità minima di tempo.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Installare più istanze di ruoli del sistema del sito

Quando si installano più istanze dei ruoli del sistema del sito critici, si forniscono punti di contatto ridondanti per i client. Più punti di gestione e punti di distribuzione, ad esempio, forniscono un servizio ridondante nell'eventualità che un server specifico sia offline.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Installare più istanze del provider SMS in un sito

Il provider SMS fornisce il punto di contatto amministrativo per una o più console di Configuration Manager. Per fornire ridondanza per i punti di contatto per l'amministrazione del sito e della gerarchia, installare più provider SMS.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a> Disponibilità elevata per ruoli del sistema del sito

In ogni sito, si distribuiscono i ruoli del sistema del sito per fornire i servizi che si desidera che i client utilizzino in tale sito. Il database del sito contiene le informazioni di configurazione per il sito e per tutti i client. Utilizzare una o più delle opzioni disponibili per fornire elevata disponibilità al database del sito, nonché il ripristino del sito e del database del sito se necessario.  

### <a name="redundancy-for-important-site-system-roles"></a>Ridondanza per ruoli del sistema del sito importanti

- Punto per servizi Web del catalogo applicazioni  

- Punto per siti Web del catalogo applicazioni  

- Punto di distribuzione  

- Punto di gestione  

- Punto di aggiornamento software  

- Punto di migrazione stato  

Per garantire ridondanza per la creazione di report su siti e client, installare più istanze del punto di Reporting Services.

Per il supporto per il failover con il punto di aggiornamento software, usare Windows PowerShell per installare questo ruolo in un cluster Bilanciamento carico di rete Windows.  

### <a name="built-in-site-backup"></a>Backup del sito incorporato

Configuration Manager include un'attività di backup predefinita che permette di eseguire il backup del sito e delle informazioni critiche in base a una pianificazione regolare. Inoltre, l'Installazione guidata di Configuration Manager supporta azioni di ripristino del sito per ripristinare il normale funzionamento del sito.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Pubblicazione nei Servizi di dominio Active Directory e DNS

Configurare ogni sito per la pubblicazione dei dati sul sito in Active Directory Domain Services e DNS. Questa pubblicazione consente ai client di identificare il server più accessibile della rete. I client la usano anche per identificare quando i nuovi server di sistema del sito sono disponibili per fornire servizi importanti, ad esempio i punti di gestione.  

### <a name="sms-provider-and-configuration-manager-console"></a>Provider SMS e console di Configuration Manager

Configuration Manager supporta l'installazione di più provider SMS in server separati come più punti di accesso per la console. Se un server di un provider SMS è offline, è comunque possibile visualizzare e gestire siti e client.  

Quando una console di Configuration Manager si connette a un sito, si connette a un'istanza del provider SMS nel sito. L'istanza del provider SMS viene selezionata in modo casuale. Se il provider SMS selezionato non è disponibile, è possibile scegliere tra le opzioni seguenti:  

- Riconnettere la console al sito. A ogni nuova richiesta di connessione viene assegnata in modo casuale un'istanza del provider SMS. È possibile che alla nuova connessione venga assegnata un'istanza disponibile.  

- Connettere la console a un sito di Configuration Manager diverso e gestire la configurazione da questa connessione. Questa opzione introduce un leggero ritardo delle modifiche alla configurazione di non più di pochi minuti. Quando il provider SMS per il sito è online, riconnettere la console di Configuration Manager direttamente al sito che si vuole gestire.  

Installare la console di Configuration Manager in più computer per permetterne l'uso agli amministratori. Ogni provider SMS supporta le connessioni da più di una console.  

### <a name="management-point"></a>Punto di gestione

Installare più punti di gestione su ciascun sito primario e abilitare i siti alla pubblicazione dei dati del sito sull'infrastruttura di Active Directory e in DNS.  

Più punti di gestione consentono di bilanciare il carico dell'utilizzo di un unico punto di gestione da parte di più client. Si consiglia anche di installare una o più repliche di database per i punti di gestione. Questa configurazione riduce le operazioni a elevato utilizzo di processori del punto di gestione. Aumenta anche la disponibilità di questo ruolo del sistema del sito critico.  

I siti secondari supportano solo l'installazione di un punto di gestione, che deve trovarsi nel server del sito secondario. I punti di gestione nei siti secondari non hanno una configurazione a disponibilità elevata.  

> [!NOTE]  
> I dispositivi mobili gestiti in locale si connettono solo a un punto di gestione nel sito primario. Il punto di gestione viene assegnato da Configuration Manager al dispositivo mobile durante la registrazione e in seguito non cambia. Quando si installano più punti di gestione e se ne abilita più di uno per i dispositivi mobili, il punto di gestione assegnato a un client del dispositivo mobile non è deterministico.  
>
> Se il punto di gestione usato da un client del dispositivo mobile non è più disponibile, occorre risolvere il problema del punto di gestione oppure cancellare il dispositivo mobile e registrarlo di nuovo in modo che possa essere assegnato a un punto di gestione operativo abilitato per i dispositivi mobili.  

### <a name="distribution-point"></a>Punto di distribuzione

Installare più punti di distribuzione e distribuire il contenuto in più punti di distribuzione. Aggiungere più di un punto di distribuzione per ogni gruppo di limiti per assicurarsi che i client ottengano più opzioni nella richiesta di contenuto. Configurare le relazioni dei gruppi di limiti in modo che abbiano un comportamento di fallback prevedibile in un altro gruppo di limiti o punto di distribuzione cloud. Per altre informazioni, vedere [Configurare gruppi di limiti](boundary-groups.md).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Punto per servizi Web del catalogo applicazioni e punto per siti Web del catalogo applicazioni

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Installare più istanze di ogni ruolo del sistema del sito. Per prestazioni ottimali, distribuirne una di ogni ruolo nello stesso server di sistema del sito.  

Ogni ruolo di sistema del sito del catalogo applicazioni fornisce le stesse informazioni rispetto alle altre istanze di tale ruolo, indipendentemente dalla posizione nella gerarchia. Quando un client richiede il catalogo applicazioni e i client sono stati configurati per rilevare automaticamente il punto per siti Web del catalogo applicazioni predefinito, il client viene indirizzato a un'istanza disponibile. Il client preferiscono le istanze del catalogo applicazioni locali, in base alla posizione di rete corrente del client.  

Per altre informazioni su questa impostazione client e sul funzionamento del rilevamento automatico, vedere le impostazioni client [Agente computer](../../../clients/deploy/about-client-settings.md#computer-agent).  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a> Disponibilità elevata per i client  

### <a name="client-operations-are-autonomous"></a>Le operazioni dei client sono autonome

L'autonomia del client Configuration Manager include i comportamenti seguenti:  

- I client non richiedono un contatto continuo con nessun server del sistema del sito specifico. Utilizzano configurazioni note per eseguire azioni preconfigurate in base a una pianificazione.  

- I client possono usare qualsiasi istanza disponibile di un ruolo del sistema del sito che fornisce servizi ai client. Provano a contattare i server noti fino a quando non individuano un server disponibile.  

- I client possono eseguire inventari, distribuzioni software e analoghe azioni pianificate indipendenti dal contatto diretto con i server del sistema del sito.  

- I client configurati per l'uso di un punto di stato di fallback possono inviare dettagli al punto di stato di fallback quando non riescono a comunicare con un punto di gestione.  

### <a name="clients-can-repair-themselves"></a>I client sono in grado di ripristinarsi da soli

I client correggono automaticamente i problemi più comuni senza un intervento amministrativo diretto.  

- I client valutano periodicamente in modo autonomo il proprio stato. Intraprendono azioni per correggere problemi comuni usando una cache locale di passaggi correttivi e file di origine per i ripristini.  

- Quando un client non riesce a inviare informazioni al proprio sito, il sito può generare un avviso. Gli utenti amministratori che ricevono questi avvisi possono richiedere un intervento immediato per ripristinare il normale funzionamento del client.  

### <a name="clients-cache-information-to-use-in-the-future"></a>I client memorizzano nella cache informazioni da utilizzare in futuro

Quando un client comunica con un punto di gestione, il client può ottenere e memorizzare nella cache le informazioni seguenti:  

- Impostazioni client  

- Pianificazioni client  

- Informazioni su distribuzioni software e un download del software che il client ha pianificato di installare, quando la distribuzione è configurata per queste azioni.  

Quando un client non riesce a contattare un punto di gestione, i client memorizzano nella cache locale le informazioni su stato, stato attuale e client, che inviano al sito. Il client trasferisce questi dati dopo aver stabilito il contatto con un punto di gestione.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>Il client può inviare lo stato a un punto di stato di fallback

Quando si configura un client per l'uso di un punto di stato di fallback, si fornisce un punto aggiuntivo di contatto per consentire al client di inviare dettagli importanti sul proprio funzionamento. I client configurati per usare un punto di stato di fallback continuano a inviare lo stato delle operazioni a quel ruolo del sistema del sito anche quando il client non riesce a comunicare con un punto di gestione.  

### <a name="central-management-of-client-data-and-client-identity"></a>Gestione centrale dei dati client e identità client

Il database del sito, anziché il client singolo, mantiene informazioni importanti sull'identità di ogni client e associa tali dati a un computer o a un utente specifico.  

- I file di origine del client in un computer possono essere disinstallati e reinstallati senza influire sui record cronologici del computer in cui è installato il client.  

- Eventuali errori di un computer client non compromettono l'integrità delle informazioni archiviate nel database. Queste informazioni possono rimanere disponibili per la creazione di report.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a> Opzioni per siti e ruoli del sistema del sito non a disponibilità elevata

Alcuni sistemi del sito non supportano istanze multiple in un sito o nella gerarchia. Queste informazioni consentono di prepararsi per i casi in cui i sistemi del sito passino in modalità offline.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Punto di sincronizzazione di Asset Intelligence (gerarchia)

Questo ruolo del sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

- Risolvere la causa della mancata presenza online del sistema del sito.  

- Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

### <a name="endpoint-protection-point-hierarchy"></a>Punto di Endpoint Protection (gerarchia)

Questo ruolo del sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

- Risolvere la causa della mancata presenza online del sistema del sito.  

- Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

### <a name="enrollment-point-site"></a>Punto di registrazione (sito)

Questo ruolo del sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

- Risolvere la causa della mancata presenza online del sistema del sito.  

- Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

### <a name="enrollment-proxy-point-site"></a>Punto proxy di registrazione (sito)

Questo ruolo del sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Tuttavia, è possibile installare più istanze di questo ruolo di sistema del sito in un sito e in più siti nella gerarchia. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

- Risolvere la causa della mancata presenza online del sistema del sito.  

- Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

Quando si dispone di più server proxy di registrazione in un sito, è possibile utilizzare un alias DNS per il nome del server. Quando si utilizza questa configurazione, round robin DNS fornisce tolleranza d'errore e bilanciamento del carico parziali per la fase di registrazione dei dispositivi mobili da parte degli utenti.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Punto di stato di fallback (sito o gerarchia)

Questo ruolo del sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

- Risolvere la causa della mancata presenza online del sistema del sito.  

- Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server. Poiché il punto di stato di fallback viene assegnato ai client durante l'installazione, è necessario modificare i client esistenti in modo che usino il nuovo server di sistema del sito.  

### <a name="service-connection-point-hierarchy"></a>Punto di connessione del servizio (gerarchia)

Anche se questo ruolo del sistema del sito è fondamentale per mantenere aggiornato Configuration Manager Current Branch, non è in genere usato frequentemente. Se questo sistema non risulta più in linea, usare una delle seguenti opzioni:

- Risolvere la causa della mancata presenza online del sistema del sito.  

- Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  


## <a name="see-also"></a>Vedere anche

- [Configurazioni supportate](../../../plan-design/configs/supported-configurations.md)  

- [Recommended hardware](../../../plan-design/configs/recommended-hardware.md) (Hardware consigliato)  

- [Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Prerequisiti del sito e del sistema del sito](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Impatto degli errori del sito](../../manage/site-failure-impacts.md)  
