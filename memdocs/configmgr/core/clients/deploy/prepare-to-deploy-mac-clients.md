---
title: Preparare la distribuzione del client in computer Mac
titleSuffix: Configuration Manager
description: Attività di configurazione che precedono la distribuzione del client di Configuration Manager in computer Mac.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b5bcbce659601e10f44f06af94eb939767a389a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906631"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparare la distribuzione del software client in computer Mac

*Si applica a: Configuration Manager (Current Branch)*

Seguire questa procedura per assicurarsi di essere pronti a [distribuire il client di Configuration Manager in computer Mac](deploy-clients-to-macs.md).



## <a name="mac-prerequisites"></a>Prerequisiti Mac

Il pacchetto di installazione del client per Mac non viene fornito con i supporti di Configuration Manager. Scaricare i **client per altri sistemi operativi** dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=47719).  

Per l'elenco delle versioni supportate, vedere [Sistemi operativi supportati per client e dispositivi](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).



## <a name="certificate-requirements"></a>Requisiti per i certificati

Per installare e gestire i client per computer Mac sono necessari i certificati di infrastruttura a chiave pubblica (PKI). I certificati PKI proteggono la comunicazione tra i computer Mac e il sito di Configuration Manager usando l'autenticazione manuale e i trasferimenti di dati crittografati. Configuration Manager può richiedere e installare un certificato client utente. La soluzione usa Servizi certificati con un'autorità di certificazione globale (enterprise), nonché il punto di registrazione e il punto proxy di registrazione di Configuration Manager. È anche possibile richiedere e installare un certificato del computer in modo indipendente da Configuration Manager. Il certificato deve soddisfare i requisiti di Configuration Manager relativi ai certificati.  

I client Mac di Configuration Manager controllano sempre la revoca del certificato. Questa funzione non può essere disabilitata.  

Se i client Mac non riescono a individuare l'elenco di revoche di certificati (CRL), non possono connettersi ai sistemi del sito di Configuration Manager. In particolare per i client Mac che si trovano in una foresta diversa rispetto all'autorità di certificazione emittente, controllare la struttura dell'elenco di revoche di certificati. Assicurarsi che i client Mac possano individuare e scaricare un elenco di revoche di certificati.  

Prima di installare il client di Configuration Manager in un computer Mac, stabilire come installare il certificato client:  

-   Usare la registrazione di Configuration Manager tramite lo [strumento CMEnroll](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). Il processo di registrazione non supporta il rinnovo automatico dei certificati. Registrare nuovamente i computer Mac prima della scadenza del certificato.  

-   [Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager](deploy-clients-to-macs.md#bkmk_external).  

Per altre informazioni sui requisiti dei certificati per client Mac, vedere [Requisiti dei certificati PKI per Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

I client Mac vengono assegnati automaticamente al sito di Configuration Manager che li gestisce. I client Mac vengono installati come client solo Internet, anche se la comunicazione è limitata alla rete Intranet. In base a questa configurazione, i client comunicano con i punti di gestione e i punti di distribuzione abilitati per Internet nel sito assegnato. I computer Mac non comunicano con i sistemi del sito esterni al sito assegnato.  

> [!IMPORTANT]  
>  Il client di Configuration Manager per macOS non può essere usato per connettersi a un punto di gestione configurato per usare una [replica di database](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Distribuire un certificato server Web nei server di sistema del sito  

Se i sistemi del sito non hanno un certificato server Web, distribuirlo nei computer con questi ruoli del sistema del sito:  

-   Punto di gestione  

-   Punto di distribuzione  

-   Punto di registrazione  

-   Punto proxy di registrazione  

Il certificato del server Web deve includere il nome di dominio completo Internet specificato nelle proprietà del sistema del sito. Il server non deve essere accessibile da Internet per supportare i computer Mac. Se non è necessaria la gestione client basata su Internet, è possibile specificare il valore del nome di dominio completo Intranet per il nome di dominio completo Internet.  

Specificare il valore del nome di dominio completo Internet del sistema del sito nel certificato del server Web per il punto di gestione, il punto di distribuzione e il punto proxy di registrazione.

Per altre informazioni relative a una distribuzione di esempio, vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Distribuire un certificato di autenticazione client nei server di sistema del sito  

Se i sistemi del sito non hanno un certificato di autenticazione client, distribuirlo nei computer con questi ruoli del sistema del sito:  

-   Punto di gestione  

-   Punto di distribuzione  

Per una distribuzione di esempio che crea e installa il certificato client per i punti di gestione, vedere [Distribuzione del certificato client per computer Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

Per una distribuzione di esempio che crea e installa il certificato client per i punti di distribuzione, vedere [Distribuzione del certificato client per i punti di distribuzione](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Per distribuire il client in dispositivi che eseguono macOS Sierra, il nome soggetto del certificato del punto di gestione deve essere configurato correttamente. Ad esempio, usare il nome di dominio completo del server del punto di gestione.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparare il modello di certificato client per i computer Mac  

Il modello di certificato deve avere le autorizzazioni di **lettura** e **registrazione** per l'account utente che registra il certificato nel computer Mac.  

Per altre informazioni, vedere [Distribuzione del certificato client per computer Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Configurare il punto di gestione e il punto di distribuzione  

Configurare i punti di gestione per le seguenti opzioni:  

-   HTTPS  

-   Consenti connessioni client da Internet. Questo valore di configurazione è necessario per gestire computer Mac. Tuttavia, ciò non significa che i server del sistema del sito debbano essere accessibili da Internet.  

-   Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione  

Per installare il client per Mac non sono necessari punti di distribuzione. Se si vuole distribuire software in questi computer dopo l'installazione del client, configurare i punti di distribuzione per consentire le connessioni client da Internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Per configurare i punti di gestione e i punti di distribuzione per supportare i computer Mac  

Prima di iniziare questa procedura, assicurarsi di configurare il punto di gestione e il punto di distribuzione con un nome di dominio completo Internet. Se questi server non supportano la gestione client basata su Internet, specificare il nome di dominio completo Intranet come valore del nome di dominio completo Internet.

Questi ruoli del sistema del sito devono trovarsi in un sito primario.  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**. Selezionare quindi il server con i ruoli del sistema del sito corretti.  

2.  Nel riquadro dei dettagli selezionare il ruolo **Punto di gestione** e scegliere **Proprietà** nella barra multifunzione. Nella finestra **Proprietà punto di gestione** configurare queste opzioni:  

    1.  Scegliere **HTTPS**.  

    2.  Selezionare **Consenti solo connessione client Internet** o **Consenti connessioni intranet e Internet**. Per queste opzioni è necessario un nome di dominio completo Internet o Intranet.  

    3.  Selezionare **Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione**.  

    4. Selezionare **OK** per salvare la configurazione.  

3.  Nel riquadro dei dettagli del nodo Server e ruoli del sistema del sito selezionare il ruolo **Punto di distribuzione** e scegliere **Proprietà** nella barra multifunzione. Nella finestra **Proprietà punto di distribuzione** configurare queste opzioni:  

    -   Scegliere **HTTPS**.  

    -   Selezionare **Consenti solo connessione client Internet** o **Consenti connessioni intranet e Internet**. Per queste opzioni è necessario un nome di dominio completo Internet o Intranet.  

    -   Fare clic su **Importa certificato**, selezionare il file del certificato del punto di distribuzione client esportato e specificare la password.  

4.  Ripetere questa procedura per tutti i punti di gestione e i punti di distribuzione dei siti primari che gestiscono computer Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurare il punto proxy di registrazione e il punto di registrazione  

Installare entrambi i ruoli nello stesso sito. Non è necessario installarli nello stesso server del sistema del sito o nella stessa foresta Active Directory.  

Per altre informazioni sulla selezione del ruolo del sistema del sito e relative considerazioni, vedere [Ruoli del sistema del sito](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

Per aggiungere i ruoli del sistema del sito per supportare i computer Mac, vedere [Installare i ruoli del sistema del sito](../../servers/deploy/configure/install-site-system-roles.md).

Nella pagina **Selezione ruolo del sistema** selezionare **Punto proxy di registrazione** e **Punto di registrazione** dall'elenco dei ruoli disponibili.  



## <a name="install-the-reporting-services-point"></a>Installare il punto di Reporting Services  

Per altre informazioni, vedere [Installare un punto di Reporting Services](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Passaggi successivi

[Distribuire il client di Configuration Manager in computer Mac](deploy-clients-to-macs.md)  
