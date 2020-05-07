---
title: Porte usate per le connessioni
titleSuffix: Configuration Manager
description: Informazioni sulle porte di rete necessarie e personalizzabili usate da Configuration Manager per le connessioni.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b75ebe7e768080a1239e817c514b634cdcf64179
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587173"
---
# <a name="ports-used-in-configuration-manager"></a>Porte usate in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo articolo sono elencate le porte di rete usate da Configuration Manager. Alcune connessioni usano porte non configurabili e altre supportano porte personalizzate specificate dall'utente. Se si usa una tecnologia di filtro delle porte, verificare che le porte richieste siano disponibili. Queste tecnologie di filtro delle porte includono firewall, router, server proxy o IPsec.

> [!NOTE]  
> Se si supportano client basati su Internet usando il bridging SSL, oltre ai requisiti delle porte è necessario consentire anche ad alcune intestazioni e alcuni verbi HTTP di superare il firewall.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Porte che è possibile configurare

Configuration Manager consente di configurare le porte per i tipi di comunicazione seguenti:  

- Dal punto per siti Web del Catalogo applicazioni al punto per servizi Web del Catalogo applicazioni  

- Dal punto proxy di registrazione al punto di registrazione  

- Da client a sistemi del sito che eseguono IIS  

- Da client a Internet (come impostazioni server proxy)  

- Dal punto di aggiornamento software a Internet (come impostazioni server proxy)  

- Dal punto di aggiornamento software al server WSUS  

- Dal server del sito al server del database del sito  

- Dal server del sito al server di database WSUS

- Punti di Reporting Services  

  > [!NOTE]  
  > Le porte in uso per il ruolo del sistema del sito del punto di Reporting Services sono configurate in SQL Server Reporting Services. Queste porte vengono usate da Configuration Manager durante le comunicazioni al punto di Reporting Services. Assicurarsi di esaminare queste porte per definire le informazioni del filtro IP per i criteri IPsec o per la configurazione dei firewall.  

Per impostazione predefinita, la porta HTTP usata per la comunicazione dal client al sistema del sito è la porta 80 e la porta HTTPS predefinita è la porta 443. Le porte per la comunicazione dal client al sistema del sito su HTTP o HTTPS possono essere modificate durante l'installazione o nelle proprietà del sito di Configuration Manager.  

Le porte in uso per il ruolo del sistema del sito del punto di Reporting Services sono configurate in SQL Server Reporting Services. Queste porte vengono usate da Configuration Manager durante le comunicazioni al punto di Reporting Services. Assicurarsi di esaminare queste porte quando si definiscono le informazioni del filtro IP per i criteri IPsec o per la configurazione dei firewall.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Porte non configurabili  

Configuration Manager non consente di configurare le porte per i tipi di comunicazione seguenti:  

- Da sito a sito  

- Dal server del sito al sistema del sito  

- Dalla console di Configuration Manager al provider SMS  

- Dalla console di Configuration Manager a Internet  

- Connessioni a servizi cloud, ad esempio Microsoft Intune e punti di distribuzione cloud  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Porte usate dai sistemi del sito e dai client di Configuration Manager  

Nelle sezioni seguenti vengono riportati i dettagli delle porte usate per la comunicazione in Configuration Manager. Le frecce nel titolo della sezione indicano la direzione della comunicazione:  

- --> Indica che un computer avvia la comunicazione e l'altro risponde sempre  

- &lt; --> Indica che la comunicazione può essere avviata da uno dei due computer  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Punto di sincronizzazione di Asset Intelligence --> Microsoft  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Punto di sincronizzazione di Asset Intelligence --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Punto per servizi Web del Catalogo applicazioni --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Punto per siti Web del Catalogo applicazioni --> Punto per servizi Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client --> Punto per siti Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Client --> Client  

Il proxy di riattivazione usa anche i messaggi di richiesta echo ICMP da un client a un altro client. I client usano questo tipo di comunicazione per verificare se l'altro client è attivo nella rete. ICMP viene talvolta indicato come comandi ping. ICMP non ha un numero di protocollo UDP o TCP e pertanto non è elencato nella tabella seguente. Tuttavia, qualsiasi firewall basato su host presente nei computer client o negli altri dispositivi di rete all'interno del sottoinsieme deve consentire il traffico ICMP affinché la comunicazione del proxy di riattivazione venga eseguita correttamente.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Riattivazione LAN|9 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|--|  
|Proxy di riattivazione|25536 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|--|  
|Trasmissione della peer cache di Windows PE|8004|--|  
|Download della peer cache di Windows PE|--|8003|  

Per altre informazioni, vedere [Peer cache di Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> Client --> Modulo criteri del servizio Registrazione dispositivi di rete (SCEP) di Configuration Manager

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Client --> Punto di distribuzione cloud  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Per altre informazioni, vedere [Porte e flusso di dati](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> Client --> Cloud Management Gateway (CMG)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Per altre informazioni, vedere [Porte CMG e flusso di dati](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> Client--> Punto di distribuzione, sia standard sia pull  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|
|Aggiornamenti rapidi|--|8005 <sup>[Nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Usare le impostazioni client per configurare la porta alternativa per gli aggiornamenti rapidi. Per altre informazioni, vedere [Porta usata dai client per ricevere richieste per contenuto differenziale](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content).

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> Client --> Punto di distribuzione configurato per multicast, sia standard sia pull  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Protocollo multicast|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> Client --> Punto di distribuzione configurato per PXE, sia standard sia pull  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 e 68|--|  
|TFTP|69 <sup>[Nota 4](#bkmk_note4)</sup> |--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

> [!Important]  
> Se si abilita un firewall basato su host, verificare che le regole consentano al server di inviare e ricevere su queste porte. Quando si abilita un punto di distribuzione per PXE, Configuration Manager è in grado di abilitare le regole in ingresso (ricezione) per il firewall di Windows. Non consente di configurare le regole in uscita (invio).<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Client --> Punto di stato di fallback  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Client --> Controller di dominio catalogo globale

Un client di Configuration Manager non contatta un server di catalogo globale quando si tratta di un computer di un gruppo di lavoro o quando è configurato per la comunicazione solo con Internet.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Catalogo globale LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Client --> Punto di gestione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Notifica client (comunicazione predefinita prima di eseguire il fallback su HTTP o HTTPS)|--|10123 <sup>[Nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Client --> Punto di aggiornamento software  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 o 8530 <sup>[Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 o 8531 <sup>[Nota 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Client --> Punto di migrazione stato  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> Punto di connessione di CMG --> Servizio cloud CMG  

Configuration Manager usa queste connessioni per compilare il canale CMG. Per altre informazioni, vedere [Porte CMG e flusso di dati](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (scelta consigliata)|--|10140-10155|  
|HTTPS (fallback con una macchina virtuale)|--|443|  
|HTTPS (fallback con due o più macchine virtuali)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> Punto di connessione CMG --> Punto di gestione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Per altre informazioni, vedere [Porte CMG e flusso di dati](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> Punto di connessione CMG --> Punto di aggiornamento software  

La porta specifica dipende dalla configurazione del punto di aggiornamento software.

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Per altre informazioni, vedere [Porte CMG e flusso di dati](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Console di Configuration Manager --> Client  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Controllo remoto (controllo)|--|2701|  
|Assistenza remota (RDP e RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Console di Configuration Manager --> Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

La console di Configuration Manager usa l'accesso a Internet per le azioni seguenti:

- Download degli aggiornamenti software da Microsoft Update per i pacchetti di distribuzione.
- Elemento Commenti e suggerimenti nella barra multifunzione.
- Collegamenti alla documentazione all'interno della console.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Console di Configuration Manager --> Punto di Reporting Services  

|Descrizione|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Console di Configuration Manager --> Server del sito  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (connessione iniziale a WMI per individuare il sistema provider)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Console di Configuration Manager --> Provider SMS  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Modulo criteri del servizio Registrazione dispositivi di rete (NDES) di Configuration Manager --> Punto di registrazione certificati  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> Punto di servizio del data warehouse --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> Punto di distribuzione, sia standard sia pull --> Punto di gestione

Un punto di distribuzione comunica con il punto di gestione negli scenari seguenti:  

- Per segnalare lo stato del contenuto di pre-installazione  

- Per segnalare i dati di riepilogo sull'utilizzo  

- Per segnalare la convalida del contenuto  

- Per segnalare lo stato di download dei pacchetti (solo punto di distribuzione pull)

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Punto di Endpoint Protection --> Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Punto di Endpoint Protection --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Punto proxy di registrazione --> Punto di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Punto di registrazione --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Connettore Exchange Server --> Exchange Online  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Gestione remota Windows su HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Connettore Exchange Server --> Exchange Server locale  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Gestione remota Windows su HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Computer Mac --> Punto proxy di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Punto di gestione --> Controller di dominio  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|389|389|  
|LDAP sicuro (LDAPS, per firma e binding)|636|636|  
|Catalogo globale LDAP|--|3268|  
|Agente mapping endpoint RPC|--|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> Punto di gestione &lt; --> Server del sito

<sup>[Nota 5](#bkmk_note5)</sup>

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Agente mapping endpoint RPC|--|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Punto di gestione --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo mobile --> Punto proxy di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Punto di Reporting Services --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> Punto di connessione del servizio --> Azure (CMG)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS per la distribuzione del servizio CMG|--|443|

Per altre informazioni, vedere [Porte CMG e flusso di dati](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Server del sito &lt; --> Punto per servizi Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Server del sito &lt; --> Punto per siti Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Server del sito &lt; --> Punto di sincronizzazione di Asset Intelligence  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Server del sito --> Client  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Riattivazione LAN|9 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Server del sito --> Punto di distribuzione cloud  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Per altre informazioni, vedere [Porte e flusso di dati](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> Server del sito--> Punto di distribuzione, sia standard sia pull

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Server del sito --> Controller di dominio  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|389|389|
|LDAP sicuro (LDAPS, per firma e binding)|636|636|
|Catalogo globale LDAP|--|3268|  
|Agente mapping endpoint RPC|--|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Server del sito &lt; --> Punto di registrazione certificati  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> Server del sito &lt;--> Punto di connessione CMG

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Server del sito &lt; --> Punto di Endpoint Protection  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Server del sito &lt; --> Punto di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Server del sito &lt; --> Punto proxy di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Server del sito &lt; --> Punto di stato di fallback

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Server del sito --> Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Nota 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Server del sito &lt; --> Autorità di certificazione emittente (CA)

Questa comunicazione viene usata quando si distribuiscono i profili certificato usando il punto di registrazione del certificato. La comunicazione non viene usata per ogni server del sito della gerarchia. Viene usata solo per il server del sito in cima alla gerarchia.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Agente mapping endpoint RPC|135|135|  
|RPC (DCOM)|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> Server del sito--> Server che ospita la condivisione della libreria di contenuto remoto

È possibile spostare la libreria del contenuto in un'altra posizione di archiviazione per liberare spazio su disco rigido nei server del sito primario o di amministrazione centrale. Per altre informazioni, vedere [Configurare una raccolta contenuto remota per il server del sito](the-content-library.md#bkmk_remote).

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> Server del sito &lt;-> Punto di connessione del servizio

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Server del sito &lt; --> Punto di Reporting Services

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> Server del sito &lt; --> Server del sito  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Server del sito --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

Durante l'installazione di un sito che usa un'istanza di SQL Server remota per ospitare il database del sito, aprire le seguenti porte tra il server del sito e SQL Server:  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> Server del sito --> SQL Server per WSUS  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[Nota 3](#bkmk_note3) Porta alternativa disponibile</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Server del sito --> Provider SMS  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DYNAMIC <sup>[Nota 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Server del sito &lt; --> Punto di aggiornamento software

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|HTTP|--|80 o 8530 <sup>[Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 o 8531 <sup>[Nota 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Server del sito &lt; --> Punto di migrazione dello stato

<sup>[Nota 5](#bkmk_note5)</sup>  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Provider SMS --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Punto di aggiornamento software --> Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Nota 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Punto di aggiornamento software --> Server upstream di WSUS  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 o 8530 <sup>[Nota 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 o 8531 <sup>[Nota 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

La replica di database tra siti richiede SQL Server in un sito per comunicare direttamente con l'istanza di SQL Server del sito padre o del sito figlio.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Servizio SQL Server|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  
|SQL Server Service Broker|--|4022 <sup>[Nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

> [!TIP]  
> Configuration Manager non richiede SQL Server Browser, che usa la porta UDP 1434.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Punto di migrazione dello stato --> SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 <sup>[vedere la nota 2](#bkmk_note2) Porta alternativa disponibile</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Note per le porte usate dai sistemi del sito e dai client di Configuration Manager  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> Nota 1: Porta server proxy

Questa porta non può essere configurata, ma può essere instradata attraverso un server proxy configurato.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> Nota 2: Porta alternativa disponibile

È possibile definire una porta alternativa in Configuration Manager per questo valore. Se si definisce una porta personalizzata, usare la porta personalizzata nelle informazioni sul filtro IP per i criteri IPSec o per configurare i firewall.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> Nota 3: Windows Server Update Services (WSUS)

WSUS può essere installato per l'uso delle porte 80/443 o 8530/8531 per la comunicazione client. Quando si esegue WSUS in Windows Server 2012 o Windows Server 2016, WSUS viene configurato per impostazione predefinita per l'uso della porta 8530 per HTTP e della porta 8531 per HTTPS.  

Al termine dell'installazione, è possibile modificare la porta. Non è necessario usare lo stesso numero di porta per tutta la gerarchia del sito.  

- Se la porta HTTP è la porta 80, la porta HTTPS deve essere la porta 443.  

- Se la porta HTTP è diversa, la porta HTTPS deve essere uguale o maggiore di 1, ad esempio 8530 e 8531.

    > [!NOTE]  
    >  Quando si configura il punto di aggiornamento software per l'uso di HTTPS, deve essere aperta anche la porta HTTP. I dati non crittografati, ad esempio il contratto di licenza per aggiornamenti specifici, usano la porta HTTP.

- Il server del sito effettua una connessione al server SQL che ospita il database SUSDB quando si abilitano le opzioni seguenti per la pulizia di WSUS:
  - Aggiungere indici non cluster al database di WSUS per migliorare le prestazioni di pulizia di WSUS
  - Rimuovere gli aggiornamenti obsoleti dal database di WSUS
  
  Se la porta predefinita di SQL Server viene modificata in una porta alternativa con Gestione configurazione SQL Server, verificare che il server del sito sia in grado di connettersi usando la porta definita. Configuration Manager non supporta porte dinamiche. Per impostazione predefinita, le istanze denominate di SQL Server usano le porte dinamiche per le connessioni al motore di database. Se si usa un'istanza denominata, configurare manualmente la porta statica.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> Nota 4: Daemon Trivial FTP (TFTP)

Il servizio del sistema Daemon Trivial FTP (TFTP) non richiede un nome utente o una password ed è parte integrante di Servizi di distribuzione Windows. Il servizio Daemon Trivial FTP implementa il supporto per il protocollo TFTP definito nei seguenti RFC:  

- RFC 1350: TFTP  

- RFC 2347: Estensione opzione  

- RFC 2348: Opzione dimensione blocco  

- RFC 2349: Intervallo di timeout e opzioni dimensione trasferimento  

TFTP è progettato per supportare ambienti di avvio privi di dischi. I daemon TFTP sono in ascolto sulla porta UDP 69 ma rispondono da una porta elevata allocata in modo dinamico. Se si abilita questa porta, il servizio TFTP può ricevere richieste TFTP in ingresso, ma il server selezionato non può rispondere a tali richieste. Non è possibile consentire al server selezionato di rispondere alle richieste TFTP in entrata, a meno che il server TFTP non venga configurato per rispondere dalla porta 69.  

Il punto di distribuzione che supporta PXE e il client in Windows PE selezionano porte di numero alto ad assegnazione dinamica per i trasferimenti TFTP. Queste porte sono definite da Microsoft in un intervallo compreso tra 49152 e 65535. Per altre informazioni, vedere [Panoramica dei servizi e requisiti delle porte per Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

Durante l'effettivo avvio PXE, tuttavia, la scheda di rete presente nel dispositivo seleziona la porta di numero alto ad assegnazione dinamica usata durante il trasferimento TFTP. La scheda di rete presente nel dispositivo non è associata alle porte di numero alto ad assegnazione dinamica definite da Microsoft. È associata solo alle porte definite in RFC 1350. Questa porta può essere una qualsiasi nell'intervallo compreso tra 0 e 65535. Per altre informazioni sulle porte di numero alto ad assegnazione dinamica usate dalla scheda di rete, contattare il produttore dell'hardware del dispositivo.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> Nota 5: Comunicazione tra server del sito e sistemi del sito

Per impostazione predefinita, la comunicazione tra il server del sito e i sistemi del sito è bidirezionale. Il server del sito avvia la comunicazione per configurare il sistema del sito, quindi la maggior parte dei sistemi del sito si riconnette al server del sito per inviare le informazioni sullo stato. I punti di distribuzione e i punti di Reporting Services non inviano informazioni sullo stato. Se si seleziona **Richiedi al server del sito di avviare le connessioni al sistema del sito** nelle proprietà del sistema del sito dopo aver eseguito l'installazione, il sistema del sito non avvierà la comunicazione al server del sito. Al contrario, il server del sito avvia la comunicazione. Usa l'account di installazione del sistema del sito per l'autenticazione al server del sistema del sito.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> Nota 6: Porte dinamiche

Le porte dinamiche usano un intervallo di numeri di porta definito dalla versione del sistema operativo. Queste porte sono note anche come porte temporanee. Per informazioni sugli intervalli di porta predefiniti, vedere [Panoramica dei servizi e requisiti per le porte di rete per Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Altri elenchi di porte  

Nelle sezioni seguenti vengono fornite ulteriori informazioni sulle porte usate da Configuration Manager.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Da client a condivisioni server

I client usano Server Message Block (SMB) ogni volta che si connettono alle condivisioni UNC. Ad esempio:

- Installazione client manuale che specifica la proprietà della riga di comando **/source:** di CCMSetup.exe  

- Client di Endpoint Protection che scaricano i file di definizione da un percorso UNC

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Connessioni a Microsoft SQL Server

Per la comunicazione al motore di database di SQL Server e per la replica tra siti, è possibile usare la porta di SQL Server predefinita o specificare porte personalizzate:  

- Le comunicazioni intrasito usano:  

  - SQL Server Service Broker, che usa per impostazione predefinita la porta TCP 4022.  

  - Servizio SQL Server che usa per impostazione predefinita la porta TCP 1433.  

- La comunicazione all'interno del sito tra il motore di database di SQL Server e i diversi ruoli di sistema del sito di Configuration Manager usa la porta TCP 1433 per impostazione predefinita.  

- Configuration Manager usa le stesse porte e gli stessi protocolli per comunicare con ciascuna replica del gruppo di disponibilità SQL che ospita il database del sito come se la replica fosse un'istanza autonoma di SQL Server.

Quando si usa Azure e il database del sito si trova dietro un bilanciamento del carico interno o esterno, configurare i componenti seguenti:

- Eccezioni del firewall in ogni replica
- Regole di bilanciamento del carico

Configurare le porte seguenti:

- SQL su TCP: TCP 1433
- SQL Server Service Broker: TCP 4022
- Server Message Block (SMB): TCP 445
- Mapper di endpoint RPC: TCP 135

> [!WARNING]  
> Configuration Manager non supporta porte dinamiche. Per impostazione predefinita, le istanze denominate di SQL Server usano le porte dinamiche per le connessioni al motore di database. Se si usa un'istanza denominata, configurare manualmente la porta statica per la comunicazione tra siti.  

I ruoli del sistema del sito seguenti comunicano direttamente con il database di SQL Server:  

- Punto per servizi Web del Catalogo applicazioni  

- Ruolo del punto di registrazione certificati  

- Ruolo del punto di registrazione  

- Punto di gestione  

- Server del sito  

- Punto di Reporting Services  

- Provider SMS  

- SQL Server --> SQL Server  

Se SQL Server ospita un database da più di un sito, ogni database deve usare un'istanza separata di SQL Server. Configurare ogni istanza con un set univoco di porte.  

Se si abilita un firewall basato su host su SQL Server, configurarlo in modo da consentire le porte appropriate. Inoltre, configurare i firewall di rete tra i computer che comunicano con SQL Server.  

Per un esempio di come configurare SQL Server per l'uso di una porta specifica, vedere [Configurare un server per l'attesa su una porta TCP specifica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Individuazione e pubblicazione

Configuration Manager usa le porte seguenti per l'individuazione e la pubblicazione delle informazioni del sito:

- Lightweight Directory Access Protocol (LDAP): 389
- LDAP sicuro (LDAPS, per firma e binding): 636
- Catalogo globale LDAP: 3268
- Mapper di endpoint RPC: 135
- RPC: porte TCP elevate allocate dinamicamente
- TCP: 1024: 5000
- TCP:  49152: 65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Connessioni esterne stabilite da Configuration Manager

I sistemi del sito o i client locali di Configuration Manager possono eseguire le connessioni esterne seguenti:  

- [Punto di sincronizzazione di Asset Intelligence --&gt; Microsoft](#BKMK_PortsAI)  

- [Punto di Endpoint Protection --&gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Client --&gt; Controller di dominio catalogo globale](#BKMK_PortsClient-GCDC)  

- [Console di Configuration Manager --&gt; Internet](#BKMK_PortsConsole-Internet)  

- [Punto di gestione --&gt; Controller di dominio](#BKMK_PortsMP-DC)  

- [Server del sito --&gt; Controller di dominio](#BKMK_PortsSite-DC)  

- [Server del sito &lt; --&gt; Autorità di certificazione emittente (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [Punto di aggiornamento software --&gt; Internet](#BKMK_PortsSUP-Internet)  

- [Punto di aggiornamento software --&gt;Server upstream di WSUS](#BKMK_PortsSUP-WSUS)  

- [Punto di connessione del servizio --> Azure](#bkmk_scp-cmg)  

- [Punto di connessione di CMG --> Servizio cloud CMG](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Requisiti di installazione per sistemi del sito che supportano client basati su Internet

> [!Note]  
> Questa sezione si applica solo alla gestione client basata su Internet (IBCM). Non è applicabile per Cloud Management Gateway. Per altre informazioni, vedere [Gestire i client su Internet](../../clients/manage/manage-clients-internet.md).  

I punti di gestione basati su Internet, i punti di distribuzione che supportano i client basati su Internet, il punto di aggiornamento software e il punto di stato di fallback usano le porte seguenti per l'installazione e il ripristino:  

- Server del sito --> Sistema del sito: mapper di endpoint RPC tramite la porta TCP e UDP 135.  

- Server del sito --> Sistema del sito: Porte TCP dinamiche RPC  

- Server del sito &lt; --> Sistema del sito: Server Message Block (SMB) tramite la porta TCP 445

Le installazioni di applicazioni e pacchetti nei punti di distribuzione richiedono le seguenti porte RPC:  

- Server del sito -- > Punto di distribuzione: mapper di endpoint RPC tramite la porta TCP e UDP 135

- Server del sito -- > Punto di distribuzione: Porte TCP dinamiche RPC  

Usare IPsec per proteggere il traffico tra il server del sito e i sistemi del sito. Se è necessario limitare le porte dinamiche usate con RPC, è possibile usare lo strumento di configurazione RPC di Microsoft (rpccfg.exe) per configurare un intervallo limitato di porte per tali pacchetti RPC. Per altre informazioni, vedere [Come configurare RPC per l'uso di determinate porte e come proteggere tali porte tramite IPSec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Prima di installare questi sistemi del sito, verificare che il servizio Registro di sistema remoto sia in esecuzione nel server di sistema del sito e di aver specificato un account di installazione sistema del sito se il sistema del sito si trova in una foresta Active Directory diversa senza una relazione di trust. Ad esempio il servizio Registro di sistema remoto viene usato nei server che eseguono sistemi del sito, ad esempio punti di distribuzione sia pull sia standard, server SQL remoti e il Catalogo applicazioni.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Porte usate dall'installazione client di Configuration Manager

Le porte usate da Configuration Manager durante l'installazione del client dipendono dal metodo di distribuzione.

- Per un elenco di porte per ogni metodo di distribuzione client, vedere [Porte usate durante la distribuzione client di Configuration Manager](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment)  

- Per altre informazioni su come configurare Windows Firewall nel client per la comunicazione durante e dopo l'installazione del client, vedere [Impostazioni di Windows Firewall e delle porte per i client](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Porte usate dalla migrazione

Il server del sito che esegue la migrazione usa diverse porte per connettersi ai siti applicabili nella gerarchia di origine. Per altre informazioni, vedere [Configurazioni necessarie per la migrazione](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Porte usate da Windows Server

Nella tabella seguente vengono elencate alcune porte chiave usate da Windows Server.

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 e 68|--|  
|Risoluzione nomi NetBIOS|137|--|  
|Servizio datagrammi NetBIOS|138|--|  
|Servizio di sessione NetBIOS|--|139|  
|Autenticazione Kerberos|--|88|

Per altre informazioni, vedere gli articoli seguenti:

- [Panoramica dei servizi e requisiti per le porte di rete per il sistema server Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Come configurare un firewall per domini e trust](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
