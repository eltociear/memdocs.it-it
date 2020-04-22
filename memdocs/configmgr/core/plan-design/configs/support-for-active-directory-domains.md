---
title: Supporto per i domini di Active Directory
titleSuffix: Configuration Manager
description: Informazioni sui requisiti per un sistema del sito di Configuration Manager in un dominio di Active Directory.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688579"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Supporto per i domini di Active Directory in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Tutti i sistemi del sito di Configuration Manager devono essere membri di un dominio di Active Directory supportato. I computer client Configuration Manager possono essere membri del dominio o membri del gruppo di lavoro.  

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni

- L'appartenenza al dominio si applica anche ai sistemi del sito che supportano la gestione client basata su Internet in una rete perimetrale (queste reti sono dette anche DMZ e subnet schermate).  

- Non è supportata per modificare le configurazioni seguenti per un computer che ospita un ruolo del sistema del sito:  

  - Appartenenza al dominio, inclusa la rimozione di un sistema del sito dal dominio e la successiva aggiunta allo stesso dominio.

  - Nome di dominio  

  - Nome computer  

  Prima di apportare queste modifiche, disinstallare il ruolo del sistema del sito. Per apportare queste modifiche a un server del sito, disinstallare prima il sito. È anche possibile prendere in considerazione la creazione di un [server del sito in modalità passiva](../../servers/deploy/configure/site-server-high-availability.md) per semplificare la gestione di questa modifica in un server del sito.

- Configuration Manager supporta il livello di funzionalità del dominio e delle foreste di Windows Server 2008 R2 o versione successiva.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Spazio dei nomi non contiguo

È possibile installare client e sistemi del sito di Configuration Manager in un dominio che contiene uno *spazio dei nomi non contiguo*.  

In uno spazio dei nomi non contiguo il suffisso DNS primario di un computer non corrisponde al nome di dominio DNS di Active Directory di tale computer. Un altro scenario di spazio dei nomi non contiguo si ottiene quando il nome di dominio NetBIOS di un controller di dominio non corrisponde al nome di dominio DNS di Active Directory.  

### <a name="disjoint-scenarios"></a>Scenari non contigui

Nelle sezioni successive vengono identificati gli scenari supportati per uno spazio dei nomi non contiguo.  

#### <a name="scenario-1"></a>Scenario 1

Il suffisso DNS primario del controller di dominio è diverso dal nome di dominio DNS di Active Directory. I computer membri del dominio possono essere contigui o non contigui.

Il controller di dominio è non contiguo in questo scenario. I computer membri del dominio, ad esempio computer e server del sito, possono avere un suffisso DNS primario che corrisponde a:

- Suffisso DNS primario del controller di dominio
- Nome di dominio DNS di Active Directory

#### <a name="scenario-2"></a>Scenario 2

Un computer membro in un dominio di Active Directory è non contiguo, anche se il controller di dominio è contiguo.

In questo scenario il suffisso DNS primario del sistema del sito è diverso dal nome di dominio DNS di Active Directory. Il suffisso DNS primario del controller di dominio è uguale al nome di dominio DNS di Active Directory. I computer membri che sono client di Configuration Manager possono avere un suffisso DNS primario che corrisponde a:

- Suffisso DNS primario del server di sistema del sito non contiguo
- Nome di dominio DNS di Active Directory

### <a name="configure-disjoint-namespace"></a>Configurare lo spazio dei nomi non contiguo

Per consentire a un computer di accedere ai controller di dominio non contigui, modificare l'attributo **msDS-AllowedDNSSuffixes** di Active Directory nel contenitore dell'oggetto dominio. Aggiungere all'attributo entrambi i suffissi DNS.  

Per assicurarsi che l'*elenco di ricerca dei suffissi DNS* contenga tutti gli spazi dei nomi DNS nell'organizzazione, configurare l'elenco di ricerca per ogni computer nel dominio non contiguo. Includere nell'elenco degli spazi dei nomi i suffissi seguenti:

- Suffisso DNS primario del controller di dominio
- Nome di dominio DNS
- Eventuali spazi dei nomi aggiuntivi per altri server con cui Configuration Manager potrebbe comunicare

È possibile usare i criteri di gruppo per configurare l'elenco di **ricerca dei suffissi Domain Name System (DNS)** .  

> [!IMPORTANT]  
> Quando si fa riferimento a un computer in Configuration Manager, immettere il computer usando il suffisso DNS primario. Questo suffisso deve corrispondere al nome di dominio completo registrato come attributo **dnsHostName** nel dominio di Active Directory e al nome dell'entità servizio associata al sistema.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Domini con etichetta singola

Configuration Manager supporta client e sistemi del sito in un nome di dominio con etichetta singola quando vengono soddisfatti i criteri seguenti:  

- Configurare il dominio con etichetta singola in Active Directory Domain Services con uno spazio dei nomi DNS non contiguo che dispone di un dominio di livello superiore valido.  

  **Ad esempio:** Il dominio con etichetta singola di Contoso è configurato per avere uno spazio dei nomi contoso.com indipendente in DNS. Quando si specifica il suffisso DNS in Configuration Manager per un computer nel dominio Contoso, specificare "Contoso.com" e non "Contoso".  

- Le connessioni DCOM (Distributed Component Object Model) tra i server del sito nel contesto del sistema devono essere stabilite usando l'autenticazione Kerberos.  
