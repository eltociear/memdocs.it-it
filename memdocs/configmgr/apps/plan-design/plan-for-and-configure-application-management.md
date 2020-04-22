---
title: Pianificare la gestione di applicazioni
titleSuffix: Configuration Manager
description: Implementare e configurare le dipendenze necessarie per la distribuzione di applicazioni in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689049"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Pianificare e configurare la gestione delle applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni incluse in questo articolo per implementare le dipendenze necessarie per la distribuzione di applicazioni in Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

È necessario avere IIS nei server che eseguono i ruoli del sistema del sito seguenti:

- Punto di gestione  
- Punto di distribuzione  

Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

> [!Note]  
> IIS è richiesto anche per il Catalogo applicazioni. Tuttavia, l'esperienza utente di Silverlight non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
>
> Per altre informazioni, vedere gli articoli seguenti:
>
> - [Configurare Software Center](plan-for-software-center.md#bkmk_userex)
> - [Funzionalità rimosse e deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificati in applicazioni firmate dal codice per dispositivi mobili

Per firmare un'applicazione con codice per distribuirla nei dispositivi mobili, non usare un certificato generato tramite un modello della versione 3 (**Windows Server 2008, Enterprise Edition**). Questo modello di certificato crea un certificato non compatibile con le applicazioni di Configuration Manager per dispositivi mobili.

Se si usano i Servizi certificati Active Directory per firmare con codice applicazioni per dispositivi mobili, non usare un modello di certificato della versione 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Controllare gli eventi di accesso per l'affinità utente-dispositivo  

Se si vuole creare automaticamente le affinità utente-dispositivo, configurare i client per il controllo degli eventi di accesso.

Per determinare le affinità utente-dispositivo automatiche, il client di Configuration Manager legge gli eventi di accesso di tipo **Riuscito** dal registro eventi di sicurezza di Windows. Abilitare questi eventi con i due criteri di controllo seguenti:

- **Controlla eventi di accesso account**
- **Controlla eventi di accesso**

Per creare automaticamente relazioni tra utenti e dispositivi, verificare che queste due impostazioni siano attivate nei computer client. Per configurare queste impostazioni, è possibile usare i criteri di gruppo di Windows.

Per altre informazioni sull'affinità utente-dispositivo, vedere l'argomento [Collegare utenti e dispositivi mediante l'affinità utente-dispositivo](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager


### <a name="management-point"></a>Punto di gestione

I client contattano un punto di gestione per scaricare i criteri client e per individuare il contenuto.

A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti.

Nella versione 1902 e versioni precedenti, i client usano il punto di gestione per la connessione al Catalogo applicazioni. Se i client non possono accedere a un punto di gestione, non potranno usare il catalogo applicazioni.

> [!Note]  
> A partire dalla versione 1806, i ruoli del Catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Per altre informazioni, vedere [Configurare Software Center](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> A partire dalla versione 1906, non è possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  
  

### <a name="distribution-point"></a>Punto di distribuzione

Prima di poter distribuire le applicazioni nei client, è necessario almeno un punto di distribuzione nella gerarchia. Per impostazione predefinita, durante un'installazione standard nel server del sito è attivato un ruolo del sito del punto di distribuzione. Il numero e la posizione dei punti di distribuzione variano in base ai requisiti specifici dell'ambiente.

Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="reporting-services-point"></a>Punto di Reporting Services

Per usare i report in Configuration Manager per la gestione delle applicazioni, prima installare e configurare un punto di Reporting Services.

Per altre informazioni, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>Impostazioni client

Esistono numerose impostazioni client che controllano come il client installa le applicazioni e l'esperienza utente nel dispositivo. Queste impostazioni client includono i gruppi seguenti:

- Agente computer  
- Riavvio del computer  
- Software Center  
- Distribuzione software  
- Affinità utente-dispositivo  

Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md)  
- [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Autorizzazioni di sicurezza per la gestione delle applicazioni

- Il ruolo di sicurezza **Autore applicazioni** include le autorizzazioni necessarie per creare, modificare e ritirare le applicazioni.  

- Il ruolo di sicurezza **Gestione distribuzione applicazioni** include le autorizzazioni necessarie per distribuire le applicazioni.  

- Il ruolo sicurezza **Amministratore applicazione** dispone di tutte le autorizzazioni da entrambi i ruoli sicurezza: **Autore applicazioni** e **Gestione distribuzione applicazioni**.  

Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1 o client successivo per l'esecuzione di applicazioni virtuali

Per creare applicazioni virtuali in Configuration Manager, installare App-V 4.6 SP1 o versione successiva nei dispositivi.

Prima di distribuire applicazioni virtuali, aggiornare anche il client App-V con l'aggiornamento rapido descritto nell'[articolo del supporto tecnico Microsoft 2645225](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Catalogo applicazioni

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Punto per servizi Web del catalogo applicazioni

Il punto per servizi Web del catalogo applicazioni è un ruolo del sistema del sito che fornisce informazioni sul software disponibile nella raccolta software al sito Web del catalogo applicazioni a cui accedono gli utenti.

Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Installare e configurare il Catalogo applicazioni](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Punto per siti Web del catalogo applicazioni

Il punto del sito Web del catalogo applicazioni è un ruolo del sistema del sito che offre agli utenti un elenco del software disponibile.

Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Installare e configurare il Catalogo applicazioni](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Account utente individuati per il catalogo applicazioni

Prima che gli utenti possano visualizzare e richiedere applicazioni dal catalogo applicazioni, Configuration Manager deve individuare gli account utente. Per altre informazioni, vedere [Eseguire l'individuazione](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Configurare Software Center  

Per altre informazioni sulla configurazione e personalizzazione di Software Center, vedere [Pianificare Software Center](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a> Rimuovere il catalogo applicazioni

<!-- SCCMDocs-pr issue 3051 -->

Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). L'elenco seguente riepiloga le modifiche:

- A partire dalla versione 1806, l'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato.<!--1358309--> Il ruolo Punto per servizi Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*.

- A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni.

- Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  

Questi miglioramenti iterativi di Software Center e il punto di gestione sono pensati per semplificare l'infrastruttura e rimuovere la necessità del catalogo applicazioni per le distribuzioni disponibili per gli utenti. Software Center consente di distribuire tutte le distribuzioni di app senza il catalogo applicazioni. Se si abilita TLS 1.2 e si usa HTTP con il catalogo applicazioni, inoltre, gli utenti non possono vedere le distribuzioni disponibili destinate agli utenti. Aggiornare Configuration Manager alla versione 1906 o successiva per trarre vantaggio da questi miglioramenti.

1. Aggiornare tutti i client alla versione 1806 o successiva. È consigliata la versione 1906.  

1. Impostare la personalizzazione per Software Center, anziché nelle proprietà del ruolo del sito Web del catalogo applicazioni. Per altre informazioni, vedere [Impostazioni client di Software Center](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Verificare le impostazioni client predefinite e personalizzate. Nel gruppo **Agente computer** assicurarsi che l'opzione **Punto per siti Web del Catalogo applicazioni predefinito** sia `(none)`.  

    Nella versione 1902 e nelle versioni precedenti il client passa all'uso del punto di gestione solo quando non sono presenti ruoli del catalogo applicazioni nella gerarchia. In caso contrario, i client continuano a usare una delle istanze del catalogo applicazioni nella gerarchia. Questo comportamento viene applicato a tutti i siti primari.  

1. Rimuovere i ruoli del sistema del sito **sito Web del catalogo applicazioni** e **servizio Web del catalogo applicazioni** da tutti i siti primari.

Dopo aver rimosso i ruoli del catalogo applicazioni, Software Center viene avviato usando il punto di gestione per le distribuzioni disponibili destinate agli utenti. Nella versione 1902 e versioni precedenti, per l'applicazione di questa modifica possono essere necessari fino a 65 minuti. Per verificare questo comportamento in un client specifico, esaminare `SCClient_<username>.log` e cercare una voce simile alla riga seguente:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a> Installare e configurare il catalogo applicazioni  

> [!Important]  
> Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Passaggio 1: Certificato del server Web per HTTPS

Se si usano connessioni HTTPS, distribuire un certificato del server Web nei server di sistema del sito per il punto per siti Web del catalogo applicazioni e il punto per servizi Web del catalogo applicazioni.

Se si vuole che i client usino il catalogo applicazioni da Internet, distribuire un certificato del server Web in almeno un punto di gestione. Configurarlo per le connessioni client da Internet.

Per altre informazioni sui requisiti del certificato, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Passaggio 2: Certificato di autenticazione client per HTTPS

Se si usa un certificato PKI client per le connessioni ai punti di gestione, distribuire un certificato di autenticazione client nei computer client. Anche se i client non usano un certificato PKI client per connettersi al catalogo applicazioni, è necessario che si connettano a un punto di gestione prima di poter usare il catalogo applicazioni.

Distribuire un certificato di autenticazione client nei computer client negli scenari seguenti:

- Tutti i punti di gestione in Intranet accettano solo connessioni client HTTPS.
- I client eseguono la connessione al catalogo applicazioni da Internet.

Per altre informazioni sui requisiti del certificato, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Passaggio 3: Installare e configurare i ruoli del catalogo applicazioni

Installare entrambi i ruoli Punto per servizi Web del catalogo applicazioni e Punto per siti Web del catalogo applicazioni nello stesso sito. Non è necessario installarli nello stesso server o nella stessa foresta Active Directory. Il punto per servizi Web del catalogo applicazioni deve trovarsi tuttavia nella stessa foresta del database del sito.

Per altre informazioni sulla selezione host per i server, vedere [Pianificare i server e i ruoli del sistema del sito](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Installare il catalogo applicazioni in un sito primario. Non è possibile installarlo in un sito secondario o nel sito di amministrazione centrale.  

Installare il Catalogo applicazioni in nuovo server di sistema del sito o in un server esistente nel sito. Per altre informazioni sulla procedura generale, vedere [Installare i ruoli del sistema del sito](../../core/servers/deploy/configure/install-site-system-roles.md). Nella procedura guidata per aggiungere un ruolo del sistema del sito o creare un server di sistema del sito, selezionare i ruoli seguenti nell'elenco:  

- **Punto per servizi Web del catalogo applicazioni**  
- **Punto per siti Web del catalogo applicazioni**  

> [!TIP]  
> Se si vuole che i computer client usino il catalogo applicazioni tramite Internet, specificare il nome di dominio completo (FQDN) per Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verificare l'installazione di questi ruoli del sistema del sito  

- Messaggi di stato: usare i componenti **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Ad esempio, l'ID stato **1015** per **SMS_PORTALWEB_CONTROL_MANAGER** conferma che Gestione componenti del sito ha completato l'installazione del punto per siti Web del catalogo applicazioni.  

- File di log: cercare **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Per altre informazioni, cercare i file di log **awebsvcMSI.log** e **portlwebMSI.log**.  


### <a name="step-4-configure-client-settings"></a>Passaggio 4: Configurare le impostazioni client

Se si vuole che tutti gli utenti abbiano le stesse impostazioni, configurare le impostazioni client predefinite. In caso contrario, configurare le impostazioni client personalizzate per raccolte specifiche.

Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md)  
    - Agente computer  
    - Riavvio del computer  
    - Software Center  
    - Distribuzione software  
    - Affinità utente-dispositivo  
- [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md)  

Il client di Configuration Manager configura i dispositivi con queste impostazioni durante il successivo download dei criteri client. Per attivare il recupero dei criteri per un singolo client, vedere [Come gestire i client](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passaggio 5: Verificare che il catalogo applicazioni sia operativo

Usare le procedure seguenti per verificare che il catalogo applicazioni sia operativo.

> [!NOTE]  
> L'esperienza utente con il catalogo applicazioni richiede Microsoft Silverlight. Se si usa il catalogo applicazioni direttamente da un browser, verificare prima di tutto che Microsoft Silverlight sia installato nel computer.  

> [!TIP]  
> La non aderenza ai prerequisiti è una delle più comuni cause di malfunzionamento del catalogo applicazioni dopo l'installazione. Verificare i prerequisiti per i ruoli del sistema del sito del catalogo applicazioni. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

In un browser immettere l'indirizzo del sito Web del catalogo applicazioni. Verificare che nella pagina Web siano visualizzate tre schede: **Catalogo applicazioni**, **Richieste di applicazioni** e **Dispositivi personali**.  

Usare gli indirizzi appropriati per il catalogo applicazioni tra quelli dell'elenco seguente, tenendo presente che `<server>` è il nome del computer, il nome di dominio completo Intranet o il nome di dominio completo Internet:  

- Connessioni client HTTPS e impostazioni predefinite del ruolo del sistema del sito: `https://<server>/CMApplicationCatalog`  

- Connessioni client HTTP e impostazioni predefinite del ruolo del sistema del sito: `http://<server>/CMApplicationCatalog`  

- Connessioni client HTTPS e impostazioni personalizzate del ruolo del sistema del sito: `https://<server>:<port>/<web application name>`  

- Connessioni client HTTP e impostazioni personalizzate del ruolo del sistema del sito: `http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Se è stato eseguito l'accesso al dispositivo con un account amministratore di dominio, il client di Configuration Manager non visualizza messaggi di notifica, ad esempio messaggi indicanti che è disponibile nuovo software.  
