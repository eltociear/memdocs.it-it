---
title: Opzioni dei ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Per informazioni dettagliate sui ruoli del sistema del sito di Configuration Manager non di chiara comprensione, vedere questo articolo.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704809"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Opzioni di configurazione per i ruoli del sistema del sito in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La maggior parte delle opzioni di configurazione per i ruoli del sistema del sito di Configuration Manager è di chiara comprensione o descritta nelle finestre di dialogo o nella procedura guidata durante la configurazione. Le sezioni seguenti illustrano i ruoli del sistema del sito le cui impostazioni possono richiedere informazioni aggiuntive.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> Punto per siti Web del Catalogo applicazioni  

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Per altre informazioni su come configurare il punto per siti Web del Catalogo applicazioni, vedere [Pianificare e configurare la gestione delle applicazioni](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> Punto per servizi Web del Catalogo applicazioni  

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Per altre informazioni su come configurare il punto per servizi Web del Catalogo applicazioni, vedere [Pianificare e configurare la gestione delle applicazioni](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> Punto di registrazione certificati  

Per altre informazioni su come configurare il punto di registrazione certificati, vedere [Introduzione ai profili certificato](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a> Punto di distribuzione  

Per altre informazioni su come configurare il punto di distribuzione per la distribuzione del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](manage-content-and-content-infrastructure.md).  

Per altre informazioni su come configurare il punto di distribuzione per le distribuzioni di PXE, vedere [Usare PXE per distribuire Windows in rete](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

Per altre informazioni su come configurare il punto di distribuzione per le distribuzioni multicast, vedere [Usare il multicast per distribuire Windows in rete](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Installa e configura IIS, se richiesto da Configuration Manager

Selezionare questa opzione per consentire a Configuration Manager di installare e configurare IIS nel sistema del sito, se non è già installato. IIS deve essere installato su tutti i punti di distribuzione ed è necessario selezionare questa impostazione per proseguire la procedura guidata.  

### <a name="site-system-installation-account"></a>Account di installazione del sistema del sito

Per i punti di distribuzione installati in un server del sito, solo l'account del computer del server del sito viene supportato per l'uso come account di installazione del sistema del sito. Per altre informazioni, vedere [Account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> Punto di registrazione  

I punti di registrazione vengono usati per installare i computer macOS e registrare i dispositivi gestiti con la funzionalità di gestione dei dispositivi mobili in locale. Per altre informazioni, vedere gli articoli seguenti:  

- [Come distribuire i client in computer Mac](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Modalità di registrazione dei dispositivi nella gestione di dispositivi mobili locale](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>Connessioni consentite

L'impostazione HTTPS viene selezionata automaticamente e richiede un certificato PKI sul server per l'autenticazione tra server e punto proxy di registrazione, nonché per la crittografia dei dati tramite SSL. Per altre informazioni, vedere [requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in IIS, vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> Punto proxy di registrazione  

Per altre informazioni su come configurare un punto proxy di registrazione per i dispositivi mobili, vedere [Modalità di registrazione dei dispositivi nella gestione di dispositivi mobili locale](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

### <a name="client-connections"></a>Connessioni client

L'impostazione HTTPS viene selezionata automaticamente. Nel server sono necessari i certificati PKI seguenti:

- Per l'autenticazione del server ai dispositivi mobili e ai computer Mac registrati con Configuration Manager
- Per la crittografia dei dati tramite Secure Sockets Layer (SSL)

Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in IIS, vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> Punto di stato di fallback  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Numero di messaggi di stato e Intervallo di limitazione (in secondi)

Le impostazioni predefinite per queste opzioni sono 10.000 messaggio di stato e 3.600 secondi per l'intervallo di limitazione. Anche se queste impostazioni sono sufficienti nella maggior parte dei casi, potrebbe essere necessario modificarle quando entrambe le condizioni seguenti sono vere:  

- Il punto di stato di fallback accetta connessioni solo dalla rete intranet.  

- Il punto di stato di fallback viene utilizzato durante un'implementazione della distribuzione client per molti computer.  

In questo scenario, un flusso continuo di messaggi di stato può creare un backlog di messaggi di stato che determina un utilizzo elevato del processore sul server del sito per un periodo di tempo prolungato. Inoltre, potrebbe non essere possibile visualizzare le informazioni aggiornate sulla distribuzione dei client nella console di Configuration Manager e nei report sulla distribuzione dei client.  

Queste impostazioni del punto di stato di fallback sono progettate per essere configurate per messaggi di stato generati durante la distribuzione dei client. Non sono pensate per problemi di comunicazione dei client, come nel caso in cui i client su Internet non riescono a connettersi al punto di gestione basato su Internet. Dal momento che il punto di stato di fallback non può applicare queste impostazioni solo ai messaggi di stato generati durante la distribuzione dei client, non configurarle quando il punto di stato di fallback accetta connessioni da Internet.  

Ogni computer in cui l'installazione del client di Configuration Manager viene completata correttamente invia i quattro messaggi di stato seguenti al punto di stato di fallback:  

- Distribuzione di client avviata  

- Distribuzione client completata  

- Assegnazione client avviata  

- Assegnazione client completata  

I computer nei quali non è possibile eseguire l'installazione o che assegnano il client di Configuration Manager inviano messaggi di stato aggiuntivi.  

Se ad esempio si distribuisce il client di Configuration Manager a 20.000 computer, questa distribuzione può inviare 80.000 messaggi di stato al punto di stato di fallback. Dal momento che la configurazione predefinita della limitazione della larghezza di banda della rete consente l'invio di 10.000 messaggi di stato al punto di stato di fallback ogni 3600 secondi (1 ora), è possibile che i messaggi di stato vengano inclusi nel backlog sul punto di stato di fallback. Considerare anche la larghezza di banda della rete disponibile tra il punto di stato di fallback e il server del sito e la potenza di quest'ultimo per l'elaborazione di un numero elevato di messaggi di stato.  

Per evitare questi problemi, prendere in considerazione l'opportunità di aumentare il numero di messaggi di stato e ridurre l'intervallo di limitazione.  

Reimpostare i valori di limitazione per il punto di stato di fallback in presenza di una delle condizioni seguenti:  

- Si ritiene che i valori di limitazione correnti siano superiori a quelli richiesti per l'elaborazione dei messaggi di stato dal punto di stato di fallback.  

- Si ritiene che le impostazioni di limitazione correnti determinino un utilizzo elevato del processore sul server del sito.  

Non modificare le impostazioni di limitazione per il punto di stato di fallback senza aver compreso le conseguenze di tale azione. Se ad esempio le impostazioni di limitazione vengono aumentate, l'utilizzo del processore sul server del sito potrebbe crescere contestualmente, rallentando così tutte le operazioni del sito.  
