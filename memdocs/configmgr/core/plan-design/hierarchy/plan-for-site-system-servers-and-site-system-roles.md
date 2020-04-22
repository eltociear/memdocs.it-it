---
title: Pianificare ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Prendere in considerazione i server di sistema del sito e i ruoli di sistema del sito quando si pianifica la gerarchia di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706499"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Pianificare i server e i ruoli del sistema del sito in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Ogni sito di Configuration Manager installato include un server del sito, ovvero un **server del sistema del sito**. Il sito può includere anche altri server del sistema del sito nei computer remoti rispetto al server del sito. I server del sistema del sito, ovvero il server del sito o un server del sistema del sito remoto, supportano i **ruoli del sistema del sito**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a> Server del sistema del sito  

Quando si installa un ruolo del sistema del sito in un computer, il computer diventa un server del sistema del sito. In ogni sito è possibile installare uno o più server del sistema del sito aggiuntivi. Non è necessario installare altri server del sistema del sito e si può scegliere di eseguire tutti i ruoli del sistema del sito direttamente nel computer del server del sito. Ogni server di sistema del sito supporta uno o più ruoli del sistema del sito. I server supplementari possono essere utili per espandere le funzionalità e la capacità di un sito, condividendo il carico di elaborazione derivante dai ruoli del sistema del sito in un server.  

Quando si valuta se aggiungere un server del sistema del sito, verificare che il server soddisfi i prerequisiti per l'uso previsto. Aggiungerlo in un percorso di rete con larghezza di banda sufficiente per comunicare con gli endpoint previsti. Questi endpoint includono il server del sito, le risorse di dominio, un percorso basato su cloud, i server del sistema del sito e i client.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  

Installare i ruoli del sistema del sito in un computer per offrire funzionalità aggiuntive al sito. Alcuni esempi:  

- Punti di gestione aggiuntivi in modo tale che il sito possa supportare più dispositivi, fino alla capacità supportata del sito.  

- Punti di distribuzione aggiuntivi per espandere l'infrastruttura del contenuto, migliorando le prestazioni delle distribuzioni di contenuto ai dispositivi.  

- Uno o più ruoli del sistema del sito specifici per le funzionalità. Ad esempio, un punto di aggiornamento software consente di gestire gli aggiornamenti software per i dispositivi gestiti. Un punto di Reporting Services consente di eseguire report per monitorare, riconoscere e condividere informazioni sull'ambiente.  

Vari siti di Configuration Manager possono supportare diversi set di ruoli di sistema del sito. Il set di ruoli del sistema del sito supportato dipende dal tipo di sito. I tipi di sito includono un sito di amministrazione centrale, siti primari o siti secondari. La topologia della gerarchia può limitare l'uso di alcuni ruoli a determinati tipi di sito. Ad esempio, il punto di connessione del servizio è supportato solo nel sito di livello superiore della gerarchia. Il sito di livello superiore può essere un sito di amministrazione centrale o un sito primario autonomo. Questo ruolo non è supportato in un sito primario figlio o nei siti secondari.  

Dopo l'installazione di un sito, è possibile spostare la posizione di alcuni ruoli del sistema del sito dalla posizione predefinita nel server del sito a un altro server. Ad esempio i ruoli punto di gestione o punto di distribuzione vengono installati per impostazione predefinita in un server del sito primario o secondario. Installare anche altre istanze di alcuni ruoli del sistema del sito per espandere le funzionalità del sito e per soddisfare i requisiti aziendali. Alcuni ruoli sono obbligatori, mentre altri sono facoltativi.  

### <a name="configuration-manager-site-server"></a>Server del sito di Configuration Manager

Questo ruolo identifica il server in cui viene eseguito il programma di installazione di Configuration Manager per installare un sito oppure il server in cui viene installato un sito secondario. Non è possibile spostare o disinstallare questo ruolo fino a quando non viene disinstallato il sito.  

### <a name="configuration-manager-site-system"></a>Sistema del sito di Configuration Manager

Questo ruolo viene assegnato a qualsiasi computer in cui si installa un sito o un ruolo del sistema del sito. Non è possibile spostare o disinstallare questo ruolo finché non si rimuove l'ultimo ruolo del sistema del sito dal computer.  

### <a name="configuration-manager-component-site-system-role"></a>Ruolo del sistema del sito del componente di Configuration Manager

Questo ruolo identifica un sistema del sito che esegue un'istanza del servizio **SMS Executive**. È necessario per il supporto di altri ruoli, ad esempio i punti di gestione. Non è possibile spostare o disinstallare questo ruolo finché non si rimuove dal computer l'ultimo ruolo del sistema del sito applicabile.  

### <a name="configuration-manager-site-database-server"></a>Server di database del sito di Configuration Manager

Il sito assegna questo ruolo ai server di sistema del sito che contengono un'istanza del database del sito. Spostare questo ruolo solo in un nuovo server, eseguendo l'installazione per modificare il sito in modo che usi un'altra istanza di SQL Server per ospitare il database del sito.  

### <a name="sms-provider"></a>Provider SMS

Il sito assegna questo ruolo a ogni computer che ospita un'istanza del provider SMS. Il provider è l'interfaccia tra una console di Configuration Manager e il database del sito. Per impostazione predefinita, questo ruolo viene installato automaticamente nel server del sito di un sito di amministrazione centrale e nei siti primari. Installare istanze aggiuntive in ogni sito per consentire l'accesso ad altri utenti amministratori o per garantire la ridondanza.  

Per installare provider aggiuntivi eseguire il programma di installazione di Configuration Manager per [gestire il provider SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Quindi installare altri provider in computer aggiuntivi. Installare una sola istanza del provider SMS in un computer. Il computer deve trovarsi nello stesso dominio del server del sito.  

### <a name="application-catalog-web-service-point"></a>Punto per servizi Web del catalogo applicazioni

> [!Important]
> L'esperienza utente di Silverlight per il Catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Ruolo del sistema del sito che visualizza informazioni sul software per il sito Web del catalogo applicazioni dalla raccolta software. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

### <a name="application-catalog-website-point"></a>Punto per siti Web del catalogo applicazioni

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Ruolo del sistema del sito che offre agli utenti un elenco dei software disponibili dal catalogo applicazioni. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

### <a name="asset-intelligence-synchronization-point"></a>Punto di sincronizzazione di Asset Intelligence

Ruolo del sistema del sito che si connette a Microsoft per scaricare informazioni sul catalogo di Asset Intelligence. Questo ruolo carica anche i titoli senza categoria, in modo che possano essere presi in considerazione da Microsoft per una futura inclusione nel catalogo. Una gerarchia supporta un'unica istanza di questo ruolo nel sito di livello superiore della gerarchia. Se si espande un sito primario autonomo in una gerarchia più ampia, disinstallare questo ruolo dal sito primario. Quindi installarlo nel sito di amministrazione centrale.

Per altre informazioni, vedere [Asset Intelligence in System Center Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Punto di registrazione certificati

Ruolo del sistema del sito che comunica con un server in cui è in esecuzione il servizio Registrazione dispositivi di rete (NDES). Questo ruolo gestisce le richieste di certificato del dispositivo che usano il protocollo Simple Certificate Enrollment Protocol (SCEP). Questo ruolo è supportato solo nei siti primari e nel sito di amministrazione centrale.

Anche se un unico punto di registrazione certificati può fornire funzionalità a un'intera gerarchia, può essere opportuno installare più istanze di questo ruolo in uno o più siti della stessa gerarchia. Questa struttura favorisce il bilanciamento del carico. Quando esistono più istanze in una gerarchia, i client vengono assegnati in modo casuale a uno dei punti di registrazione certificati.  

Ogni punto di registrazione certificati richiede l'accesso a un'istanza separata di NDES. Non è possibile configurare due o più punti di registrazione certificati per l'uso della stessa istanza di NDES. Evitare anche di installare il punto di registrazione certificati nello stesso server che esegue NDES.  

### <a name="cloud-management-gateway-connection-point"></a>Punto di connessione del gateway di gestione cloud

Ruolo del sistema del sito per la comunicazione con il [gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Punto di servizio del data warehouse

Usare il punto di servizio del data warehouse per archiviare e creare report di dati cronologici a lungo termine nell'ambiente di Configuration Manager. Per altre informazioni, vedere [Data warehouse](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Punto di distribuzione

Ruolo di sistema del sito che contiene file di origine da scaricare per i client, ad esempio:

- Contenuti di applicazioni
- Pacchetti software
- Aggiornamenti software
- Immagini dei sistemi operativi
- Immagini d'avvio  

Per impostazione predefinita, questo ruolo viene installato nel server del sito quando si installa un nuovo sito primario o secondario. Questo ruolo non è supportato in un sito di amministrazione centrale. Installare più istanze di questo ruolo in un sito supportato e in più siti della stessa gerarchia. Per altre informazioni, vedere [Fundamental concepts for content management](fundamental-concepts-for-content-management.md) (Concetti fondamentali per la gestione dei contenuti) e [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto).  

### <a name="endpoint-protection-point"></a>Punto di Endpoint Protection

Ruolo del sistema del sito che Configuration Manager usa per accettare le condizioni di licenza di Endpoint Protection e per configurare l'appartenenza predefinita per Cloud Protection Service. Una gerarchia supporta solo un'istanza di questo ruolo, che deve trovarsi nel sito di livello superiore. Se si espande un sito primario autonomo in una gerarchia più ampia, disinstallare questo ruolo dal sito primario e quindi installarlo nel sito di amministrazione centrale. Per altre informazioni, vedere [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Punto di registrazione

Ruolo del sistema del sito che usa i certificati PKI per far sì che Configuration Manager registri i dispositivi mobili e i computer macOS. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

Se un utente registra dispositivi mobili tramite Configuration Manager e il relativo account di Active Directory si trova in una foresta considerata non attendibile dalla foresta del server del sito, installare un punto di registrazione nella foresta dell'utente. In questo modo Configuration Manager può autenticare l'utente.  

### <a name="enrollment-proxy-point"></a>Punto proxy di registrazione

Ruolo del sistema del sito che gestisce le richieste di registrazione di Configuration Manager provenienti da dispositivi mobili e computer macOS. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

Quando si supportano dispositivi mobili su Internet, installare un punto proxy di registrazione in una rete perimetrale e installarne un altro sull'intranet.

### <a name="exchange-server-connector"></a>Connettore Exchange Server

Per altre informazioni su questo ruolo, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Punto di stato di fallback

Ruolo del sistema del sito che consente di monitorare l'installazione client. Identifica i client che non sono gestiti perché non riescono a comunicare con il relativo punto di gestione. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito e in più siti della stessa gerarchia.

### <a name="management-point"></a>Punto di gestione

Ruolo del sistema del sito che invia informazioni sui criteri e sulla posizione del servizio ai client. Riceve anche i dati di configurazione dai client.  

Per impostazione predefinita, questo ruolo viene installato nel server del sito quando si installa un nuovo sito primario o secondario. I siti primari supportano più istanze di questo ruolo. I siti secondari supportano un unico punto di gestione. Detto anche punto di gestione proxy, questo ruolo in un sito secondario rappresenta un punto di contatto locale che consente ai client di ottenere criteri per computer e utenti.  

Configurare i punti di gestione per il supporto di HTTP o HTTPs. I punti di gestione possono anche supportare i dispositivi gestiti con la gestione dei dispositivi mobili locali (MDM) di Configuration Manager. Per ridurre il carico di elaborazione della CPU sul server di database del sito generato dai punti di gestione quando gestiscono le richieste provenienti dai client, usare [repliche di database per i punti di gestione](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="reporting-services-point"></a>Punto di Reporting Services

Ruolo del sistema del sito che si integra con SQL Server Reporting Services per creare e gestire rapporti per Configuration Manager. Questo ruolo è supportato nei siti primari e nel sito di amministrazione centrale ed è possibile installarne più istanze in un sito supportato. Per altre informazioni, vedere [Planning for reporting](../../servers/manage/planning-for-reporting.md) (Pianificazione per la creazione di report).  

### <a name="service-connection-point"></a>punto di connessione del servizio

Ruolo del sistema del sito che carica i dati d'uso dal sito ed è necessario per rendere disponibili gli aggiornamenti per Configuration Manager nella console. Una gerarchia supporta solo un'istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia stessa. Se si espande un sito primario autonomo in una gerarchia più ampia, disinstallare questo ruolo dal sito primario e quindi installarlo nel sito di amministrazione centrale. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Punto di aggiornamento software

Ruolo del sistema del sito che si integra con Windows Server Update Services (WSUS) per fornire aggiornamenti software ai client di Configuration Manager. Questo ruolo è supportato in tutti i siti:  

- Installare questo sistema del sito nel sito di amministrazione centrale per la sincronizzazione con WSUS.  

- Configurare ogni istanza di questo ruolo nei siti primari figlio per la sincronizzazione con il sito di amministrazione centrale.  

- Se il trasferimento dei dati nella rete risulta lento, valutare la possibilità di installare un punto di aggiornamento software nei siti secondari.  

Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Punto di migrazione stato

Quando viene eseguita la migrazione di un computer a un nuovo sistema operativo, questo ruolo del sistema del sito memorizza i dati sullo stato utente. Questo ruolo è supportato nei siti primari e nei siti secondari. Installare più istanze di questo ruolo in un sito e in più siti della stessa gerarchia. Per altre informazioni sulla memorizzazione dello stato utente durante la distribuzione di un sistema operativo, vedere [Manage user state](../../../osd/get-started/manage-user-state.md) (Gestire lo stato utente).  


## <a name="next-steps"></a>Passaggi successivi

Alcuni ruoli del sistema del sito di Configuration Manager richiedono connessioni a Internet. Se l'ambiente richiede traffico Internet per usare un server proxy, configurare questi ruoli del sistema del sito per l'uso del proxy. Per altre informazioni, vedere [Proxy server support](../network/proxy-server-support.md) (Supporto del server proxy).  
