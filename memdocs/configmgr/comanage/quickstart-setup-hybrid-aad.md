---
title: Configurare Azure AD ibrido
titleSuffix: Configuration Manager
description: Se l'ambiente include attualmente dispositivi Windows 10 aggiunti a un dominio, configurare Azure AD ibrido prima di abilitare la co-gestione
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 405303b3988e8c853ba30e8fb6d620d782b0474e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694900"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurare Azure AD ibrido per la co-gestione

In presenza di dispositivi Windows 10 aggiunti ad Active Directory in locale, prima di abilitare la co-gestione in Configuration Manager, aggiungere tali dispositivi ad Azure Active Directory (Azure AD). Questo processo è noto come aggiunta ad Azure AD ibrido. 

Nel video seguente il Senior Program Manager Sandeep Deo e il Product Marketing Manager Adam Harbour trattano e illustrano la configurazione dei dispositivi in Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Il processo di aggiunta ad Azure AD ibrido registra automaticamente i dispositivi aggiunti a un dominio locale in Azure AD. Per altre informazioni su questo processo, vedere gli articoli seguenti:
- [Informazioni sulla gestione dei dispositivi in Azure Active Directory](/azure/active-directory/device-management-introduction) 
- [Come pianificare l'aggiunta ad Azure AD ibrido](/azure/active-directory/devices/hybrid-azuread-join-plan)

L'aggiunta ad Azure AD ibrido è uno dei pilastri per la co-gestione. Questo processo può essere complesso per alcuni clienti, ad esempio:
- L'organizzazione usa una soluzione di gestione delle identità di terze parti 
- Le complicazioni correlate alla configurazione di Active Directory Federation Services (AD FS)

Per risolvere questi problemi possono essere utili alcune indicazioni. Questo articolo aiuta a evitare eventuali ritardi.


## <a name="how-to-do-it"></a>Come procedere

I dispositivi sono simili agli utenti quando si tratta di creare un'identità che si vuole proteggere. Per proteggere l'identità di un dispositivo in qualsiasi momento e in qualsiasi posizione, è necessario aggiungere l'identità del dispositivo in Azure AD.

In base al tipo di dominio in uso, esistono due modi principali per eseguire questa operazione. Configurare l'aggiunta ad Azure AD ibrido per uno dei seguenti tipi di dominio:  
- [Domini federati](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domini gestiti](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

I due metodi precedenti offrono un'esperienza ottimale. Per informazioni più dettagliate, inclusa una descrizione completa della procedura manuale, vedere gli articoli seguenti:
- [Configurare manualmente i dispositivi aggiunti ad Azure AD ibrido](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticazione pass-through di AD FS per Azure AD ibrido](/windows-server/identity/ad-fs/ad-fs-overview), che include l'individuazione di Azure AD  

Per indicazioni sulla risoluzione dei problemi, vedere la [guida alla risoluzione dei problemi per l'aggiunta ad Azure AD ibrido in Windows 10](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Case study

Una grande azienda europea produttrice di software con più di 100.000 utenti nella propria rete ha adottato un approccio granulare e in più fasi per l'abilitazione dell'aggiunta ad Azure AD ibrido.

Durante la fase di pianificazione, poiché l'aggiunta ad Azure AD ibrido è un elemento fondamentale a supporto della co-gestione, gli amministratori di Configuration Manager hanno collaborato con il team responsabile delle identità. L'azienda usava molte regole di AD FS, alcune piuttosto complesse. Per risolvere questo problema, il team responsabile delle identità ha esaminato le regole di AD FS esistenti prima di abilitare l'aggiunta ad Azure AD ibrido. Il team IT ha anche scelto di aggiornare Azure AD Connect alla versione più recente. Azure AD Connect offre ora un flusso di processo automatizzato per l'abilitazione dell'aggiunta ad Azure AD ibrido.

Dopo il completamento della distribuzione e dei test nell'ambiente di pre-produzione, questo cliente ha abilitato l'aggiunta ad Azure AD ibrido per l'intero ambiente di produzione. Nel giro di una settimana tutti i dispositivi Windows 10 erano co-gestiti.



## <a name="contact-fasttrack"></a>Contattare FastTrack

Se è necessaria assistenza per la configurazione di Azure AD in qualsiasi punto del processo, passare a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), eseguire l'accesso e richiedere assistenza. 

Per altre informazioni, vedere [Ottenere assistenza da FastTrack](quickstart-fasttrack.md).