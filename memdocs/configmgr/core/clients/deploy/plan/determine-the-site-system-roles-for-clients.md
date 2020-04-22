---
title: Ruoli del sistema del sito per i client
titleSuffix: Configuration Manager
description: Determinare i ruoli del sistema del sito per i client in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693749"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Determinare i ruoli del sistema del sito per i client di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento può essere utile per determinare i ruoli del sistema del sito necessari per la distribuzione dei client di Configuration Manager.

Per altre informazioni sul percorso di installazione di questi ruoli nella gerarchia, vedere [Progettare una gerarchia di siti](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

Per altre informazioni su come installare e configurare questi ruoli, vedere [Installare ruoli del sistema del sito](../../../servers/deploy/configure/install-site-system-roles.md).  

## <a name="management-point"></a>Punto di gestione

Per impostazione predefinita, tutti i computer client Windows usano un punto di distribuzione per l'installazione del client di Configuration Manager. I computer client possono eseguire il fallback in un punto di gestione quando non è disponibile un punto di distribuzione. Tuttavia, è possibile installare i client Windows nei computer da un'origine alternativa usando la proprietà della riga di comando CCMSetup `/source:<Path>`. Ad esempio, questa azione potrebbe essere appropriata se si installano i client su Internet. Un altro scenario è quello in cui si vuole evitare l'invio di pacchetti di rete tra il computer e il punto di gestione durante l'installazione del client. Questo scenario è dovuto al blocco delle porte richieste da parte di un firewall o a una connessione a larghezza di banda ridotta. Tutti i client devono tuttavia comunicare con un punto di gestione per essere assegnati a un sito e gestiti da Configuration Manager.  

Per altre informazioni sulle proprietà della riga di comando del client, vedere [Informazioni sulle proprietà di installazione del client](../about-client-installation-properties.md).  

Quando si installa più di un punto di gestione nella gerarchia, i client si connettono automaticamente a un punto sulla base della loro appartenenza alla foresta e del percorso di rete. Non è possibile installare più di un punto di gestione in un sito secondario.  

I client di computer Mac e i client di dispositivi mobili registrati con Configuration Manager richiedono sempre un punto di gestione per l'installazione client. Questo punto di gestione deve trovarsi in un sito primario, essere configurato per il supporto di dispositivi mobili e accettare le connessioni client da Internet. Questi client non possono usare i punti di gestione in siti secondari o connettersi a punti di gestione in altri siti primari.  

## <a name="distribution-point"></a>Punto di distribuzione

Non è necessario un punto di distribuzione per installare i client di Configuration Manager in computer Windows. Per impostazione predefinita, Configuration Manager usa un punto di distribuzione per l'installazione dei file di origine del client nei computer Windows. È possibile che venga eseguito un fallback per scaricare i file da un punto di gestione. I punti di distribuzione non vengono usati per installare i client di dispositivi mobili registrati da Configuration Manager ma vengono usati in caso di installazione del client legacy del dispositivo mobile. Se si installa il client di Configuration Manager nell'ambito della distribuzione di un sistema operativo, l'immagine del sistema operativo viene archiviata e recuperata da un punto di distribuzione.

Sebbene per l'installazione della maggior parte dei client di Configuration Manager non siano necessari punti di distribuzione, questi sono richiesti per l'installazione di software, ad esempio applicazioni e aggiornamenti software, nei client.  

## <a name="fallback-status-point"></a>Punto di stato di fallback

È possibile usare un punto di stato di fallback per monitorare la distribuzione del client per i computer Windows. È anche possibile identificare i client Windows non gestiti perché non possono comunicare con un punto di gestione.

I tipi di client seguenti non usano un punto di stato di fallback:

- Computer Mac
- Dispositivi mobili registrati da Configuration Manager
- Dispositivi mobili gestiti tramite il connettore Exchange Server

Non è richiesto un punto di stato di fallback per monitorare l'attività e lo stato dei client.  

Il punto di stato di fallback comunica sempre con i client tramite HTTP, che usa connessioni non autenticate e invia i dati come testo non crittografato. Questo comportamento rende il punto di stato di fallback vulnerabile ad attacchi, in particolare quando viene usato con la gestione client basata su Internet. Per ridurre la superficie di attacco, dedicare sempre un server all'esecuzione del punto di stato di fallback. Non installare altri ruoli del sistema del sito nello stesso server in un ambiente di produzione.  

Installare un punto di stato di fallback in presenza di tutte le condizioni seguenti:  

- Si vuole che gli errori di comunicazione client dai computer Windows vengano inviati al sito, anche se i computer client non possono comunicare con un punto di gestione.  

- Si vogliono usare i report di distribuzione client di Configuration Manager che visualizzano i dati inviati dal punto di stato di fallback.  

- Si dispone di un server dedicato per questo ruolo del sistema del sito e di ulteriori misure di sicurezza per proteggere il server da attacchi esterni.  

- I vantaggi dell'utilizzo di un punto di stato di fallback superano i rischi di protezione associati a connessioni non autenticate e trasferimenti di testo non crittografato nel traffico su HTTP.  

Non installare un punto di stato di fallback se i rischi a livello di sicurezza dell'esecuzione di un sito Web con connessioni non autenticate e trasferimenti di testo non crittografato superano i vantaggi dell'identificazione dei problemi di comunicazione client.  

## <a name="reporting-services-point"></a>Punto di Reporting Services

Configuration Manager offre molti report che consentono di monitorare l'installazione, l'assegnazione e la gestione dei client nella console di Configuration Manager. Alcuni dei report di distribuzione richiedono che i client siano assegnati a un punto di stato di fallback.  

I report non sono necessari per la distribuzione dei client. È possibile visualizzare alcune informazioni sulla distribuzione nella console di Configuration Manager o usare i file di log del client per informazioni dettagliate. Tuttavia, i report client offrono informazioni utili per monitorare e risolvere i problemi di distribuzione dei client.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Punto di registrazione e punto proxy di registrazione

Configuration Manager richiede un punto di registrazione e un punto proxy di registrazione per registrare i dispositivi mobili e i certificati per computer Mac. Questi ruoli del sistema del sito non sono necessari nelle situazioni seguenti:

- Si pianifica di gestire i dispositivi mobili tramite il connettore Exchange Server
- Si installa il client legacy del dispositivo mobile, ad esempio per Windows CE
- Si richiede e si installa il certificato client nei computer Mac indipendentemente da Configuration Manager

## <a name="application-catalog"></a>Catalogo applicazioni

> [!Important]  
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Punto di connessione del gateway di gestione cloud

È necessario un punto di connessione del gateway di gestione cloud se si configura un [gateway di gestione cloud](../../manage/cmg/plan-cloud-management-gateway.md) per [gestire i client su Internet](../../manage/manage-clients-internet.md).
