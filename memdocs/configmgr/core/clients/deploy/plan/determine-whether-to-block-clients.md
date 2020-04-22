---
title: Blocco dei client
titleSuffix: Configuration Manager
description: Bloccare l'accesso client per la sicurezza del sistema tramite Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693739"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Determinare se bloccare o meno i client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Se un computer client o un dispositivo mobile client non è più considerato attendibile, è possibile bloccare il client nella console di System Center 2012 Configuration Manager. I client bloccati vengono rifiutati dall'infrastruttura di Configuration Manager e non potranno pertanto comunicare con i sistemi del sito per scaricare criteri, caricare dati di inventario o inviare messaggi di stato.  

 È necessario bloccare e sbloccare un client dal sito assegnato e non da un sito di amministrazione centrale o da un sito secondario.  

> [!IMPORTANT]  
>  Anche se il blocco in Configuration Manager consente di proteggere il sito di Configuration Manager, non fare affidamento su questa funzionalità per proteggere il sito da computer o dispositivi mobili non attendibili se si consente ai client di comunicare con sistemi del sito tramite HTTP, poiché un client bloccato potrebbe accedere nuovamente al sito con un ID hardware e un certificato autofirmato nuovi. In alternativa, utilizzare la funzionalità di blocco per bloccare i supporti di avvio persi o compromessi usati per distribuire i sistemi operativi e quando i sistemi del sito accettano connessioni client HTTPS.  

 Non è possibile bloccare i client che accedono al sito usando il certificato proxy ISV. Per altre informazioni sul certificato proxy ISV, vedere Configuration Manager Software Development Kit (SDK).  

 Se i sistemi del sito accettano connessioni client HTTPS e l'infrastruttura a chiave pubblica (PKI) supporta un elenco di revoche di certificati (CRL), considerare sempre la revoca del certificato come prima linea di difesa contro certificati potenzialmente compromessi. Il blocco dei client in Configuration Manager offre una seconda linea di difesa per la protezione della gerarchia.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Considerazioni sul blocco dei client  

-   Questa opzione è disponibile per le connessioni client HTTP e HTTPS, ma ha protezione limitata quando i client si connettono ai sistemi del sito usando il protocollo HTTP.  

-   Gli utenti amministratori di Configuration Manager hanno l'autorità per bloccare un client e la relativa azione viene eseguita nella console di Configuration Manager.  

-   La comunicazione client è stata rifiutata solo dalla gerarchia di Configuration Manager.  

    > [!NOTE]  
    >  Lo stesso client può registrarsi con una gerarchia di Configuration Manager diversa.  

-   Il client viene bloccato immediatamente dal sito di Configuration Manager.  

-   Consente di proteggere i sistemi del sito da computer e dispositivi mobili potenzialmente compromessi.  

## <a name="considerations-for-using-certificate-revocation"></a>Considerazioni sull'uso della revoca dei certificati  

-   Questa opzione è disponibile per le connessioni client di Windows HTTPS se l'infrastruttura PKI supporta un elenco di revoche di certificati (CRL).  

     I client Mac eseguono sempre il controllo CRL e non è possibile disabilitare questa funzionalità.  

     Anche se i client di dispositivi mobili non usano elenchi di revoche di certificati per verificare i certificati per i sistemi del sito, i relativi certificati possono essere revocati e verificati da Configuration Manager.  

-   Gli amministratori dell'infrastruttura a chiave pubblica hanno l'autorità per bloccare un client e la relativa azione viene eseguita fuori dalla console di Configuration Manager.  

-   La comunicazione client può essere rifiutata da qualsiasi computer o dispositivo mobile che richiede il certificato client.  

-   È probabile che si verifichi un ritardo tra la revoca di certificato e il download da parte dei sistemi del sito dell'elenco di revoche di certificati (CRL) modificato.  

-   Per molte distribuzioni di PKI, questo ritardo può essere un giorno o più. Ad esempio, in Servizi certificati Active Directory la scadenza predefinita è di una settimana per un CRL completo e un giorno per delta CRL.  

-   Consente di proteggere client e sistemi del sito da computer e dispositivi mobili potenzialmente compromessi.  

    > [!NOTE]  
    >  È possibile proteggere ulteriormente i sistemi che eseguono IIS da client sconosciuti tramite la configurazione di un elenco di certificati attendibili (CTL) in IIS.  
