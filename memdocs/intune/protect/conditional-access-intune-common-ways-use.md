---
title: Scenari di accesso condizionale
titleSuffix: Microsoft Intune
description: Informazioni sull'uso dell'accesso condizionale di Intune basato su dispositivo e basato su app.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1d4dacf29aa0c87a8356306d10bf05acbf3afb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462168"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Quali sono le modalità d'uso comuni dell'accesso condizionale con Intune?

Esistono due tipi di accesso condizionale con Intune: l'accesso condizionale basato su dispositivo e l'accesso condizionale basato su app. È necessario configurare i criteri di conformità correlati per promuovere la conformità dell'accesso condizionale nell'organizzazione. L'accesso condizionale viene in genere usato per operazioni come consentire o bloccare l'accesso a Exchange e controllare l'accesso alla rete o come integrazione per una soluzione Mobile Threat Defense.
 
Le informazioni di questo articolo illustrano come usare le funzionalità per la conformità dei *dispositivi* mobili di Intune e le funzionalità di gestione delle *applicazioni* per dispositivi mobili (MAM) di Intune. 

> [!NOTE]
> L'accesso condizionale è una funzionalità di Azure Active Directory inclusa con una licenza di Azure Active Directory Premium. Intune contribuisce a migliorare questa funzionalità aggiungendo la conformità dei dispositivi mobili e la gestione delle app per dispositivi mobili alla soluzione. Il nodo di accesso condizionale accessibile da *Intune* è lo stesso nodo accessibile da *Azure AD*.  

## <a name="device-based-conditional-access"></a>Accesso condizionale basato sul dispositivo

Intune e Azure Active Directory interagiscono per assicurarsi che solo i dispositivi gestiti e conformi abbiano accesso alla posta elettronica, ai servizi di Office 365, alle app SaaS (Software as a Service) e alle [app locali](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started). È anche possibile impostare un criterio in Azure Active Directory per consentire l'accesso ai servizi di Office 365 solo ai computer che appartengono a un dominio o ai dispositivi mobili registrati in Intune.

Intune offre funzionalità per i criteri di conformità dei dispositivi che consentono di valutare lo stato di conformità dei dispositivi. Lo stato di conformità viene segnalato ad Azure Active Directory, che lo usa per l'applicazione dei criteri di accesso condizionale creati in Azure Active Directory quando l'utente prova ad accedere alle risorse aziendali.

I criteri di accesso condizionale basato su dispositivo per Exchange Online e gli altri prodotti di Office 365 sono configurati nel [portale di Azure](../fundamentals/what-is-intune.md).

- Altre informazioni sulla [richiesta di dispositivi gestiti con accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).

- Altre informazioni sulla [conformità dei dispositivi di Intune](device-compliance-get-started.md).

- Altre informazioni sui [browser supportati con accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/technical-reference#supported-browsers).

> [!NOTE]
> Quando si abilita l'accesso in base al dispositivo per SharePoint Online o l’accesso in base al browser a Exchange Online sui dispositivi Android, gli utenti devono attivare l'opzione **Abilita l'accesso al browser** nel dispositivo registrato seguendo questa procedura:
> 1. Avviare l' **app Portale aziendale**.
> 2. Passare alla pagina **Impostazioni** facendo clic sui punti di sospensione (...) o sul tasto di menu.
> 3. Scegliere il pulsante **Abilita l'accesso al browser** . 
> 4. Nel browser Chrome disconnettersi da Office 365 e riavviare Chrome.

### <a name="conditional-access-based-on-network-access-control"></a>Accesso condizionale basato sul controllo di accesso alla rete

Intune è integrato con partner come Cisco ISE, Aruba Clear Pass e Citrix NetScaler per offrire controlli di accesso basati sulla registrazione di Intune e sullo stato di conformità del dispositivo.

L'accesso degli utenti alle risorse Wi-Fi o VPN aziendali può essere consentito o negato a condizione che il dispositivo sia gestito e conforme ai criteri di conformità dei dispositivi di Intune.

- Altre informazioni sull'[integrazione del controllo di accesso alla rete con Intune](network-access-control-integrate.md).

### <a name="conditional-access-based-on-device-risk"></a>Accesso condizionale basato sul rischio di dispositivo

Intune collabora con i fornitori di Mobile Threat Defense, che forniscono una soluzione di sicurezza per il rilevamento di malware, trojan horse e altre minacce nei dispositivi mobili.

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Funzionamento dell'integrazione tra Intune e Mobile Threat Defense

Quando nei dispositivi mobili è installato l'agente Mobile Threat Defense, questo invia messaggi sullo stato di conformità al reporting di Intune se viene rilevata una minaccia nel dispositivo mobile.

L'integrazione tra Intune e Mobile Threat Defense rappresenta un fattore per le decisioni di accesso condizionale in base al rischio del dispositivo.

- Altre informazioni su [Mobile Threat Defense di Intune](mobile-threat-defense.md).

### <a name="conditional-access-for-windows-pcs"></a>Accesso condizionale per i PC Windows

L'accesso condizionale per i PC offre funzionalità simili a quelle disponibili per i dispositivi mobili. Di seguito sono descritti i modi in cui è possibile usare l'accesso condizionale durante la gestione dei computer con Intune.

#### <a name="corporate-owned"></a>Dispositivi di proprietà dell'azienda

- **Aggiunto ad Azure AD ibrido:** questa opzione viene usata generalmente dalle organizzazioni che hanno già familiarità con la gestione dei PC tramite i criteri di gruppo di Active Directory o con Configuration Manager.

- **Aggiunta a un dominio AD e gestione tramite Intune:** questo scenario è destinato alle organizzazioni che adottano un approccio cloud-first (ovvero usano principalmente i servizi cloud con l'obiettivo di ridurre l'uso di infrastrutture locali) o esclusivamente cloud (nessuna infrastruttura locale). Azure AD Join funziona in modo ottimale in un ambiente ibrido, consentendo l'accesso alle risorse e alle app sia cloud che locali. Il dispositivo viene aggiunto ad Azure AD e viene registrato in Intune. I criteri corrispondenti possono essere usati come criteri di accesso condizionale per l'accesso alle risorse aziendali.

#### <a name="bring-your-own-device-byod"></a>Bring Your Own Device (BYOD)

- **Aggiunta alla rete aziendale e gestione di Intune:** qui l'utente può aggiungere i propri dispositivi personali per accedere ai servizi e alle risorse aziendali. È possibile usare l'aggiunta alla rete aziendale e registrare i dispositivi con la funzionalità MDM di Intune per ricevere criteri a livello di dispositivo, un'altra opzione per la valutazione dei criteri di accesso condizionale.

Altre informazioni sulla [gestione dei dispositivi in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/overview).

## <a name="app-based-conditional-access"></a>Accesso condizionale basato su app

Intune e Azure Active Directory interagiscono per verificare che solo le app gestite possano accedere alla posta elettronica aziendale o ad altri servizi di Office 365.

- Altre informazioni sull'[accesso condizionale basato su app con Intune](app-based-conditional-access-intune.md).

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Accesso condizionale di Intune per Exchange locale

L'accesso condizionale può essere usato per consentire o bloccare l'accesso a **Exchange locale** in base ai criteri di conformità e allo stato di registrazione dei dispositivi. Quando l'accesso condizionale viene usato in combinazione con i criteri di conformità dei dispositivi, possono accedere a Exchange locale solo i dispositivi conformi.

È possibile configurare le impostazioni avanzate dell'accesso condizionale per un controllo più granulare, ad esempio:

- Consentire o bloccare determinate piattaforme.

- Bloccare immediatamente i dispositivi non gestiti da Intune.

Quando si applicano i criteri di accesso condizionale e di conformità dei dispositivi, viene verificata la conformità di qualsiasi dispositivo usato per accedere a Exchange locale.

Se i dispositivi non soddisfano le condizioni previste, l'utente viene guidato nel processo di registrazione del dispositivo per la risoluzione del problema che rende il dispositivo non conforme.

> [!NOTE]
> A partire da luglio 2020, il supporto per Exchange Connector è deprecato e sostituito dall'[autenticazione moderna ibrida](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (HMA) di Exchange. L'uso di HMA non richiede la configurazione e l'uso di Exchange Connector in Intune. Con questa modifica, l'interfaccia utente per la configurazione e la gestione di Exchange Connector per Intune è stata rimossa dall'interfaccia di amministrazione di Microsoft Endpoint Manager, a meno che non si usi già Exchange Connector con la sottoscrizione.
>
> Se nel proprio ambiente è installato Exchange Connector, il tenant di Intune rimane supportato per l'uso e si continuerà ad avere accesso all'interfaccia utente che ne supporta la configurazione. Per altre informazioni, vedere [Installare il connettore locale per Exchange](../protect/exchange-connector-install.md). È possibile continuare a usare il connettore o configurare HMA e quindi disinstallare il connettore.
>
> L'autenticazione ibrida moderna fornisce funzionalità precedentemente fornite da Exchange Connector per Intune: Mapping dell'identità di un dispositivo al record di Exchange.  Questo mapping avviene ora al di fuori di una configurazione effettuata in Intune o del requisito del connettore Intune per il bridge di Intune ed Exchange. Con HMA è stato rimosso il requisito di usare la configurazione specifica di 'Intune' (connettore).


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Qual è il ruolo di Intune?

Intune valuta e gestisce lo stato del dispositivo.

#### <a name="whats-the-exchange-server-role"></a>Qual è il ruolo del server Exchange?

Il server Exchange fornisce l'API e l'infrastruttura per mettere i dispositivi in quarantena.

> [!IMPORTANT]
> Tenere presente che l'utente che usa il dispositivo deve avere un profilo di conformità e una licenza di Intune, per consentire la valutazione della conformità del dispositivo. Se all'utente non viene distribuito alcun criterio di conformità, il dispositivo viene considerato conforme e non vengono applicate restrizioni di accesso.

## <a name="next-steps"></a>Passaggi successivi

[Come configurare l'accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

[Configurare criteri di accesso condizionale basato su app](app-based-conditional-access-intune-create.md)

[Come creare criteri di accesso condizionale per Exchange locale](conditional-access-exchange-create.md)
