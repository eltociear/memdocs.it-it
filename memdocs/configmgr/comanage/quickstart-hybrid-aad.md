---
title: Usare Azure AD per la co-gestione
titleSuffix: Configuration Manager
description: Con Azure AD si possono sfruttare i vantaggi a livello di produttività per gli utenti e di sicurezza per le risorse, sia per gli ambienti cloud che locali
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c757632e96eb9bdaca829d4a19e5e156fcf52577
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694985"
---
# <a name="use-azure-ad-for-co-management"></a>Usare Azure AD per la co-gestione

Nel cloud, l'identità è il nuovo elemento centrale per il controllo. Azure Active Directory (Azure AD) consente il collegamento di utenti, dispositivi e applicazioni negli ambienti cloud e locali. La registrazione dei dispositivi in Azure AD consente di migliorare la produttività per gli utenti e la sicurezza per le risorse. L'aggiunta dei dispositivi in Azure AD è fondamentale sia per la co-gestione che per l'accesso condizionale basato sul dispositivo.

Per altre informazioni sull'accesso condizionale basato sul dispositivo, vedere [Procedura: Richiedere dispositivi gestiti per l'accesso alle app cloud con l'accesso condizionale](/azure/active-directory/conditional-access/require-managed-devices)

Nel video seguente il Senior Program Manager Sandeep Deo e il Product Marketing Manager Adam Harbour trattano e illustrano Azure AD per la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD offre due opzioni per i dispositivi di proprietà dell'azienda in base alle esigenze dell'organizzazione:  

- **Dispositivo aggiunto ad Azure AD**: aggiungere i dispositivi Windows 10 ad Azure AD senza la necessità di aggiungerli ad Active Directory in locale  

  - Supporto di Windows 10

  - La configurazione può essere eseguita senza interventi aggiuntivi negli ambienti locali  

  - Con l'abilitazione di poche impostazioni in Azure AD, è possibile consentire agli utenti di aggiungere i dispositivi ad Azure AD tramite l'esperienza di installazione di Windows (Configurazione guidata)  

  - Per altre informazioni, vedere [Procedura: Pianificare l'implementazione dell'aggiunta ad Azure AD](/azure/active-directory/devices/azureadjoin-plan)  

- **Dispositivo aggiunto ad Azure AD ibrido**: aggiungere i dispositivi aggiunti a un dominio esistenti ad Azure AD  

  - Supporto di Windows 10, Windows 8.1 e Windows 7

  - Configurazione con le attestazioni di AD FS o Azure AD Connect  

  - Per Windows 10 l'aggiunta viene eseguita nel contesto del computer, quindi gli utenti non dovranno eseguire passaggi aggiuntivi  

  - Per altre informazioni, vedere [Procedura: Pianificare l'implementazione dell'aggiunta ad Azure Active Directory ibrido](/azure/active-directory/devices/hybrid-azuread-join-plan).  

Entrambe le opzioni offrono funzionalità simili per gli utenti. La scelta è flessibile e dipende dalle esigenze specifiche. Ad esempio, è possibile [accedere alle risorse locali](/azure/active-directory/devices/azuread-join-sso) dai computer aggiunti ad Azure AD anche se non sono aggiunti ad Active Directory.

È possibile aggiungere dispositivi ad Azure AD in diversi ambienti, indipendentemente dal [metodo di autenticazione](/azure/active-directory/hybrid/choose-ad-authn). Ad esempio, l'autenticazione federata o l'autenticazione cloud.

Se è già disponibile un'infrastruttura Active Directory in locale, la configurazione di entrambe le opzioni è immediata.

## <a name="benefits"></a>Vantaggi

L'aggiunta dei dispositivi ad Azure AD offre i vantaggi seguenti per l'organizzazione:

### <a name="single-sign-on-to-cloud-resources"></a>Accesso Single Sign-On alle risorse del cloud

Nei dispositivi aggiunti ad Azure AD si ottiene un'esperienza integrata di accesso a qualsiasi risorsa nel cloud o locale. Dopo l'accesso a un computer Windows aggiunto ad Azure AD si ottiene l'accesso Single Sign-On a tutte le applicazioni senza alcuna richiesta di accesso aggiuntiva.  

### <a name="windows-hello-for-business"></a>Windows Hello for Business

Windows Hello for Business offre autenticazione avanzata senza password per Windows 10. Aggiungendo i dispositivi ad Azure AD è possibile abilitare Windows Hello for Business per l'intera base utenti sia per le risorse nel cloud che locali. Windows Hello for Business evita il problema di ricordare le password complesse o di esporle inavvertitamente. Il processo di accesso è semplice e sicuro.

Per altre informazioni, vedere [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Accesso condizionale basato sul dispositivo

Abilitare l'accesso condizionale basato sullo stato del dispositivo per proteggere meglio i dati dell'organizzazione. Per l'accesso condizionale basato sul dispositivo è richiesto un dispositivo gestito. Questo dispositivo deve essere un dispositivo conforme o un dispositivo aggiunto ad Azure AD ibrido. Per i dispositivi aggiunti ad Azure AD, è necessario Intune per contrassegnare il dispositivo come conforme. Per la gestione di dispositivi aggiunti ad Azure AD ibrido, invece, viene usato lo stato del dispositivo stesso per valutare l'accesso condizionale. La co-gestione offre l'ulteriore vantaggio di poter valutare la conformità tramite Intune per i dispositivi aggiunti ad Azure AD ibrido. Questa funzionalità garantisce che la configurazione del dispositivo sia intatta.

Per altre informazioni sull'accesso condizionale basato sul dispositivo, vedere [Procedura: Richiedere dispositivi gestiti per l'accesso alle app cloud con l'accesso condizionale](/azure/active-directory/conditional-access/require-managed-devices).  

### <a name="automatic-device-licensing"></a>Gestione automatica delle licenze dei dispositivi

Tutti i dispositivi Windows 10 aggiunti ad Azure AD passano attraverso controlli di licenza. Questi controlli consentono di aggiornare automaticamente i dispositivi da Pro a Enterprise tramite il cloud Microsoft. Quando si rimuove la sottoscrizione dall'utente, viene effettuato automaticamente il downgrade della licenza del dispositivo. Questa funzionalità garantisce un punto unico di controllo per la gestione delle licenze di Windows, senza processi complicati o sistemi locali.

### <a name="self-service-functionality"></a>Funzionalità self-service

Le funzionalità self-service includono la reimpostazione della password self-service e la chiave di ripristino di BitLocker. Azure AD offre anche opzioni dirette per reimpostare la password o accedere alle chiavi di ripristino di BitLocker. È possibile usare Azure AD per reimpostare la password direttamente dalla schermata di blocco di Windows, anziché da un Web browser. Queste funzionalità riducono le complicazioni per gli utenti e consentono di limitare i costi del supporto tecnico per l'organizzazione.  

Per altre informazioni, vedere [Esercitazione: Consentire agli utenti di sbloccare l'account o reimpostare le password usando la reimpostazione della password self-service di Azure Active Directory](/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Enterprise State Roaming

Tutti i dispositivi aggiunti ad Azure AD possono sincronizzare le impostazioni nel cloud. Qualsiasi dispositivo a cui accede un utente sincronizza tutte le impostazioni per un'esperienza più produttiva.  

## <a name="value-proposition"></a>Proposta di valore

L'aggiunta dei dispositivi ad Azure AD tramite uno dei due metodi disponibili velocizza la trasformazione digitale. Diventano disponibili più funzionalità fornite da Microsoft 365. Le esperienze saranno migliori e si potrà contare su una maggiore sicurezza per i dati.

Azure AD offre varie opzioni per semplificare i carichi di lavoro, ad esempio:

- Gestire tutte le identità dei dispositivi dell'organizzazione da un'unica posizione  

- Ridurre i costi dell'help desk abilitando la reimpostazione della password self-service. In questo modo gli utenti possono reimpostare la password dalla schermata di blocco di Windows 10 nel dispositivo in qualsiasi momento.  

## <a name="configure"></a>Configura

Se è già disponibile un ambiente Active Directory in locale e si vogliono aggiungere i dispositivi aggiunti a un dominio ad Azure AD, configurare dispositivi aggiunti ad Azure AD ibrido. Per altre informazioni, vedere [Procedura: Pianificare l'implementazione dell'aggiunta ad Azure Active Directory ibrido](/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager include l'impostazione client [Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Per altre informazioni sulla configurazione delle impostazioni client, vedere [Come configurare le impostazioni client](../core/clients/deploy/configure-client-settings.md).

Se si vuole configurare l'aggiunta ad Azure AD per i dispositivi senza aggiungerli anche al dominio locale, prendere in esame le considerazioni per l'uso dell'aggiunta ad Azure AD nell'ambiente specifico. Dopo aver deciso di implementare l'aggiunta ad Azure AD, sono disponibili molte opzioni per la distribuzione in base alle esigenze dell'organizzazione. Per altre informazioni, vedere gli articoli seguenti:

- [Procedura: Pianificare l'implementazione dell'aggiunta ad Azure AD](/azure/active-directory/devices/azureadjoin-plan)  
- [Identificazione delle opzioni di provisioning](/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)