---
title: Procedure consigliate per la distribuzione di client
titleSuffix: Configuration Manager
description: Informazioni sulle procedure ottimali per la distribuzione dei client in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693879"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Procedure consigliate per la distribuzione dei client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilizzare l'installazione client basata su aggiornamento software per i computer Active Directory  
 Questo metodo di distribuzione client usa tecnologie Windows esistenti, si integra con l'infrastruttura di Active Directory, richiede la configurazione minima in Configuration Manager, è il più semplice da configurare per i firewall ed è il più sicuro. L'uso di gruppi di protezione e di filtri WMI per la configurazione dei criteri di gruppo consente di controllare in modo flessibile su quali computer installare il client di Configuration Manager.  

 Per altre informazioni, vedere [Come installare i client di Configuration Manager usando l'Installazione basata sull'aggiornamento software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Estendere lo schema di Active Directory e pubblicare il sito in modo che sia possibile eseguire CCMSetup senza opzioni di riga di comando  
 Quando si estende lo schema di Active Directory per Configuration Manager e il sito viene pubblicato su Servizi di dominio Active Directory, molte proprietà di installazione client vengono pubblicate in Servizi di dominio Active Directory. Se un computer è in grado di rilevare le proprietà di installazione del client, può usarle durante la distribuzione del client di Configuration Manager. Poiché queste informazioni vengono generate automaticamente, viene eliminato il rischio di errori umani associato all'immissione manuale delle proprietà di installazione.  

 Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Usare un'implementazione graduale per gestire l'utilizzo della CPU  
 Per ridurre al minimo l'impatto dei requisiti di elaborazione della CPU sul server del sito, usare un'implementazione graduale dei client. Distribuire i client fuori dall'orario di ufficio in modo da garantire una maggiore larghezza di banda per altri servizi durante il giorno ed evitare che i computer siano rallentati o che sia necessario un riavvio.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Attivare l'aggiornamento automatico al termine della distribuzione del client principale  
 Gli [aggiornamenti client automatici](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) sono utili quando si vuole aggiornare un numero ridotto di computer client che potrebbero essere stati esclusi dal metodo di installazione client principale, probabilmente perché offline. 

> [!NOTE]  
>  Grazie alle prestazioni migliorate di Configuration Manager, è possibile usare gli aggiornamenti automatici come metodo principale di aggiornamento dei client. Tuttavia, le prestazioni variano in base all'infrastruttura della gerarchia, come ad esempio il numero di client.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Se si installa il client con proprietà client.msi utilizzare SMSMP e FSP  
 La proprietà SMSMP specifica il punto di gestione iniziale per la comunicazione del client ed elimina la dipendenza da soluzioni di posizionamento dei servizi come Servizi di dominio Active Directory, DNS e WINS.  

 Utilizzare la proprietà FSP e installare un punto di stato di fallback in modo da poter controllare l'installazione e l'assegnazione di client e identificare eventuali problemi di comunicazione.  

 Per altre informazioni su queste opzioni, vedere [Informazioni sulle proprietà di installazione del client](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Installare i Language Pack client prima di installare i client  
È consigliabile installare i Language Pack client prima di distribuire il client. Se si installano [Language Pack client](../../../../core/servers/deploy/install/language-packs.md) (per abilitare altre lingue) in un sito dopo aver installato i client, è necessario reinstallare i client per consentire l'uso di tali lingue. Per i client di dispositivi mobili, è necessario cancellare il dispositivo e registrarlo nuovamente.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Preparare in anticipo i certificati PKI richiesti  
 Per gestire dei dispositivi su Internet, dispositivi mobili registrati e computer Mac è necessario disporre di certificati PKI sui sistemi del sito (punti di gestione e punti di distribuzione) e sui dispositivi client. Sulle reti di produzione potrebbe essere richiesta l'approvazione della gestione delle modifiche per utilizzare i nuovi certificati, il riavvio dei server di sistema del sito oppure la disconnessione e l'accesso per una nuova appartenenza al gruppo. Inoltre, potrebbe essere necessario attendere un tempo sufficiente per la replica delle autorizzazioni di protezione e per i nuovi modelli di certificato.  

 Per altre informazioni sui certificati PKI richiesti, vedere [Requisiti dei certificati PKI per Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Prima di installare i client, configurare le impostazioni client richieste e le finestre di manutenzione  
 Sebbene sia possibile [configurare le impostazioni client](../../../../core/clients/deploy/configure-client-settings.md) e le finestre di manutenzione prima o dopo aver installato i client, è meglio configurare le impostazioni richieste prima di installare i client in modo che le impostazioni vengano usate al momento dell'installazione. 

 Configurare le finestre di manutenzione per i server e per i dispositivi con Windows Embedded per garantire la continuità aziendale per i dispositivi critici. Le finestre di manutenzione garantiscono che gli aggiornamenti software richiesti e il software antimalware non determinino il riavvio del computer durante l'orario di lavoro.  

> [!IMPORTANT]  
>  Per i computer Windows 10 che si prevede di proteggere con il Filtro di scrittura unificato (UWF), è necessario configurare il dispositivo per UWF prima di installare il client. In questo modo Configuration Manager installa il client con un provider di credenziali personalizzato che blocca l'accesso degli utenti con diritti limitati al dispositivo in modalità di manutenzione.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Pianificare l'esperienza di registrazione utente per i computer Mac e i dispositivi mobili   
 Se gli utenti registrano i loro computer Mac e i dispositivi mobili in Configuration Manager, pianificare l'esperienza utente. Ad esempio, è possibile creare uno script per l'installazione e il processo di registrazione usando una pagina Web in modo che gli utenti possano inserire una quantità minima di informazioni necessarie e ricevano le istruzioni con un collegamento tramite posta elettronica.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Usare filtri di scrittura basati su file per i dispositivi Windows Embedded 
 I dispositivi incorporati che utilizzano i filtri di scrittura avanzati (EWF) sono soggetti alle risincronizzazioni dei messaggi di stato. Se si dispone solo di pochi dispositivi incorporati che utilizzano filtri di scrittura avanzati, tale evento potrebbe passare inosservato. Tuttavia, in caso di risincronizzazione delle informazioni di numerosi dispositivi integrati, come l'invio dell'inventario completo piuttosto che l'inventario differenziale, potrebbe verificarsi un significativo aumento dei pacchetti di rete e un maggiore carico di elaborazione della CPU sul server del sito.  

 Se è possibile scegliere il tipo di filtro di scrittura da abilitare, scegliere i filtri di scrittura basati su file. Configurare quindi le eccezioni per il mantenimento dello stato del client e dei dati di inventario tra riavvii dei dispositivi per la massima efficienza della rete e della CPU nel client di Configuration Manager. Per altre informazioni sui filtri di scrittura, vedere [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Per altre informazioni sul numero massimo di client con Windows Embedded supportati da un sito primario, vedere [Supported operating sysetms for clients and devices](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (Sistemi operativi supportati per client e dispositivi).  
