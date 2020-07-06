---
title: Informazioni su Microsoft Intune - Azure | Microsoft Docs
description: Informazioni su Microsoft Intune, il componente per la gestione di dispositivi mobili (MDM) e per la gestione di app per dispositivi mobili (MAM) della soluzione Enterprise Mobility + Security che assicura la protezione dei dati aziendali.
keywords: informazioni su Intune
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b4e778d-ac13-4c23-974f-5122f74626bc
ms.reviewer: pmay
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28a5bc7a1ee00e9595c50d274605af1b33c1ea90
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332807"
---
# <a name="microsoft-intune-is-an-mdm-and-mam-provider-for-your-devices"></a>Microsoft Intune è un provider MDM e MAM per i dispositivi

Microsoft Intune è un servizio basato sul cloud incentrato sulla gestione di dispositivi mobili (MDM, Mobile Device Management) e sulla gestione di applicazioni mobili (MAM, Mobile Application Management). È possibile controllare il modo in cui vengono usati i dispositivi dell'organizzazione, inclusi telefoni cellulari, tablet e portatili. È anche possibile configurare criteri specifici per il controllo delle applicazioni. Ad esempio, è possibile impedire l'invio di messaggi di posta elettronica a utenti esterni all'organizzazione. Intune consente anche agli utenti dell'organizzazione di usare i propri dispositivi personali per la scuola o il lavoro. Nei dispositivi personali Intune consente di assicurarsi che i dati dell'organizzazione rimangano protetti e può isolare i dati dell'organizzazione da quelli personali.

Intune è incluso nella [suite Enterprise Mobility + Security (EMS)](https://www.microsoft.com/microsoft-365/enterprise-mobility-security) di Microsoft. Intune si integra con Azure Active Directory (Azure AD) per controllare gli utenti che hanno accesso e i contenuti cui possono accedere. Si integra anche con Azure Information Protection per la protezione dei dati. Può essere usato con la suite di prodotti Microsoft 365. Ad esempio, è possibile distribuire Microsoft Teams, OneNote e altre app di Microsoft 365 nei dispositivi. Questa funzionalità consente agli utenti dell'organizzazione di essere produttivi in tutti i dispositivi, mantenendo al tempo stesso la protezione delle informazioni dell'organizzazione con i criteri creati.

[![Immagine dell'architettura di Intune](./media/what-is-intune/intunearch_sm.png )](./media/what-is-intune/intunearchitecture.svg#lightbox)

Con Intune, è possibile:

- Scegliere di usare il cloud al 100% con Intune oppure optare per la [cogestione ](https://docs.microsoft.com/configmgr/comanage/overview) con Configuration Manager e Intune.
- Impostare le regole e configurare le impostazioni nei dispositivi personali e di proprietà dell'organizzazione per accedere ai dati e alle reti.
- Distribuire e autenticare le app nei dispositivi, in locale e nei dispositivi mobili.
- Proteggere le informazioni aziendali controllando il modo in cui gli utenti accedono alle informazioni e le condividono.
- Assicurarsi che i dispositivi e le app siano conformi ai requisiti di sicurezza.

## <a name="manage-devices"></a>Gestire dispositivi

In Intune è possibile scegliere l'approccio più adatto per gestire i dispositivi. Per i dispositivi di proprietà dell'organizzazione, è possibile avere il controllo completo sui dispositivi, incluse impostazioni, funzionalità e sicurezza. Con questo approccio, sia i dispositivi che i relativi utenti vengono "registrati" in Intune. Una volta registrati, ricevono le regole e le impostazioni tramite i criteri configurati in Intune. Ad esempio, è possibile impostare i requisiti di password e PIN, creare una connessione VPN, configurare la protezione dalle minacce e altro ancora.

Per i dispositivi personali o i dispositivi BYOD (Bring Your Own Device), gli utenti potrebbero non volere che gli amministratori dell'organizzazione abbiano il controllo completo. Con questo approccio, gli utenti hanno a disposizione diverse opzioni. Ad esempio, gli utenti possono [registrare](../enrollment/device-enrollment.md) i dispositivi se vogliono l'accesso completo alle risorse dell'organizzazione. In alternativa, se vogliono accedere solo alla posta elettronica o a Microsoft Teams, è possibile usare i criteri di protezione delle app che richiedono l'autenticazione a più fattori per usare queste app.

Quando i dispositivi vengono registrati e gestiti in Intune, gli amministratori possono:

- Vedere i dispositivi registrati e ottenere un elenco dei dispositivi che accedono alle risorse dell'organizzazione.
- Configurare i dispositivi in modo che soddisfino gli standard di sicurezza e integrità. Ad esempio, possono bloccare i dispositivi jailbroken.
- Eseguire il push dei certificati nei dispositivi in modo che gli utenti possano accedere facilmente alla rete Wi-Fi o usare una VPN per connettersi alla rete.
- Visualizzare report su utenti e dispositivi conformi e non conformi.
- Rimuovere i dati dell'organizzazione se un dispositivo viene perso, rubato o non è più usato.

**Risorse online** :

- [Che cos'è la registrazione dei dispositivi?](../enrollment/device-enrollment.md)

- [Applicare funzionalità e impostazioni nei dispositivi usando i profili dei dispositivi in Microsoft Intune](../configuration/device-profiles.md)

- [Proteggere i dispositivi con Microsoft Intune](../protect/device-protect.md)

### <a name="try-the-interactive-guide"></a>Provare la guida interattiva
La guida interattiva [Gestire i dispositivi con Microsoft Endpoint Manager](https://mslearn.cloudguides.com/en-us/guides/Manage%20devices%20with%20Microsoft%20Endpoint%20Manager) presenta in modo dettagliato l'interfaccia di amministrazione di Microsoft Endpoint Manager per illustrare come gestire e proteggere le applicazioni desktop e per dispositivi mobili.</br></br>

> [!VIDEO https://mslearn.cloudguides.com/en-us/guides/Manage%20devices%20with%20Microsoft%20Endpoint%20Manager]

## <a name="manage-apps"></a>Gestire le app

La gestione di applicazioni mobili (MAM) in Intune è progettata per proteggere i dati dell'organizzazione a livello di applicazione, incluse le app personalizzate e le app dello Store. La gestione delle app può essere usata nei dispositivi di proprietà dell'organizzazione e nei dispositivi personali.

Quando le app vengono gestite in Intune, gli amministratori possono:

- Aggiungere e assegnare app per dispositivi mobili a gruppi di utenti e dispositivi, inclusi utenti in gruppi specifici, dispositivi in gruppi specifici e altro ancora.
- Configurare le app per l'avvio o l'esecuzione con impostazioni specifiche abilitate e aggiornare le app esistenti già presenti nel dispositivo.
- Visualizzare i report in cui vengono usate le app e tenere traccia del loro uso.
- Eseguire una cancellazione selettiva rimuovendo solo i dati dell'organizzazione dalle app.

Un modo in cui Intune garantisce la protezione delle app per dispositivi mobili è attraverso i **[criteri di protezione delle app](../apps/app-protection-policy.md)** . I criteri di protezione delle app:

- Usano l'identità di Azure AD per isolare i dati dell'organizzazione dai dati personali. In questo modo i dati personali vengono separati dalle informazioni IT aziendali. Ai dati a cui si accede usando le credenziali dell'organizzazione viene assegnata protezione aggiuntiva.
- Proteggono l'accesso ai dispositivi personali limitando le azioni che gli utenti possono eseguire, come ad esempio copia e incolla, salvataggio e visualizzazione.
- Possono essere creati e distribuiti nei dispositivi registrati in Intune, registrati in un altro servizio MDM o non registrati in alcun servizio MDM. Nei dispositivi registrati i criteri di protezione delle app possono aggiungere un livello di protezione ulteriore.

Ad esempio, un utente accede a un dispositivo con le credenziali aziendali. L'identità aziendale consente l'accesso ai dati negato all'identità personale. Mano a mano che i dati aziendali vengono usati, i criteri di protezione delle app controllano le modalità di salvataggio e condivisione. Quando l'utente accede con l'identità personale, queste stesse protezioni non vengono applicate. In questo modo il reparto IT ha il controllo dei dati aziendali, mentre l'utente finale mantiene il controllo e la riservatezza dei propri dati personali.

È possibile usare Intune anche con gli altri servizi di EMS. Questa funzionalità garantisce la sicurezza delle app per dispositivi mobili aziendali oltre a quella offerta dal sistema operativo e dalle app. Le app gestite con EMS hanno accesso a un set più ampio di funzionalità di protezione dei dati e delle app per dispositivi mobili.

![Immagine dei livelli di protezione dei dati per la gestione delle app](./media/what-is-intune/managing-mobile-apps.png)

## <a name="compliance-and-conditional-access"></a>Conformità e accesso condizionale

Intune si integra con Azure AD abilitando una vasta gamma di scenari di controllo dell'accesso. Ad esempio, richiedere che i dispositivi mobili siano conformi agli standard dell'organizzazione definiti in Intune prima di accedere alle risorse di rete come posta elettronica o SharePoint. Analogamente, è possibile bloccare i servizi aziendali in modo che siano disponibili solo per un set specifico di app per dispositivi mobili. Ad esempio, Exchange Online può essere bloccato in modo da essere accessibile solo da Outlook o Outlook Mobile.

**Risorse online** :

- [Impostare regole sui dispositivi per consentire l'accesso alle risorse dell'organizzazione tramite Intune](../protect/device-compliance-get-started.md)

- [Modi comuni per usare l'accesso condizionale con Intune](../protect/conditional-access-intune-common-ways-use.md)

## <a name="how-to-get-intune"></a>Come ottenere Intune

Intune è disponibile:

- Come [servizio Azure](https://go.microsoft.com/fwlink/?linkid=2090973) autonomo
- Incluso con [Microsoft 365 ](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/microsoft-intune) e [Microsoft 365 Government](https://www.microsoft.com/microsoft-365/government)
- Come [Gestione di dispositivi mobili per Office 365 ](https://support.office.com/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd), che è costituita da alcune funzionalità di Intune limitate

Intune viene usato in molti settori, tra cui [settore pubblico](https://docs.microsoft.com/enterprise-mobility-security/solutions/ems-govt-service-description), [istruzione](https://www.microsoft.com/en-us/education/intune), in [chioschi multimediali o dispositivi dedicati](../configuration/kiosk-settings.md) per il settore produttivo e della vendita al dettaglio e altro ancora.

## <a name="next-steps"></a>Passaggi successivi

- [Problemi aziendali comuni che Intune contribuisce a risolvere](common-scenarios.md).
- Iniziare con una [versione di valutazione gratuita di Intune di 30 giorni](free-trial-sign-up.md).
- Progettare la [migrazione a Intune](migration-guide.md).
- Usando la versione di valutazione gratuita o la sottoscrizione, passare ad [Avvio rapido: Creare un profilo di posta elettronica del dispositivo per iOS](../configuration/quickstart-email-profile.md).
