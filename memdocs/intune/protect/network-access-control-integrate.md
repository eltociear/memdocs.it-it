---
title: Integrazione del controllo di accesso alla rete con Microsoft Intune - Azure | Microsoft Docs
description: Le soluzioni di controllo di accesso alla rete (NAC, Network Access Control) consentono di verificare che i dispositivi siano registrati in Intune e che siano conformi. NAC include alcuni comportamenti e funziona con l'accesso condizionale. Vedere i passaggi per l'onboarding e ottenere un elenco di soluzioni partner.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: aa7ecff7-8579-4009-8fd6-e17074df67de
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9302e2229b84519b46c9b2ade80488e7ca10aebf
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985004"
---
# <a name="network-access-control-nac-integration-with-intune"></a>Integrazione del controllo di accesso alla rete (NAC) con Intune

Intune si integra con i partner di controllo di accesso alla rete per consentire alle organizzazioni di proteggere i dati aziendali quando i dispositivi provano ad accedere alle risorse locali.

>[!IMPORTANT]
> NAC non è attualmente supportato per i dispositivi Android Enterprise completamente gestiti o Android Enterprise dedicati.

## <a name="how-do-intune-and-nac-solutions-help-protect-your-organization-resources"></a>Protezione delle risorse aziendali con le soluzioni di Intune e NAC

Le soluzioni NAC controllano lo stato di registrazione e conformità del dispositivo con Intune e consentono di prendere decisioni relative al controllo dell'accesso. Se il dispositivo non è registrato oppure è registrato ma non è conforme ai criteri di conformità dei dispositivi Intune, deve essere reindirizzato a Intune per la registrazione o per un controllo di conformità.

### <a name="example"></a>Esempio

Se il dispositivo è registrato e conforme con Intune, la soluzione NAC dovrebbe consentire al dispositivo di accedere alle risorse aziendali. Ad esempio, agli utenti può essere consentito o negato l'accesso quando provano a usare una connessione WiFi aziendale o risorse VPN.

## <a name="feature-behaviors"></a>Comportamenti delle funzionalità

I dispositivi che stanno eseguendo la sincronizzazione con Intune non possono passare dallo stato **Conforme** / **Non conforme** allo stato **Not Synched** (Non sincronizzato) o **Sconosciuto**. Lo stato **Sconosciuto** è riservato ai dispositivi appena registrati dei quali non è ancora stata valutata la conformità.

Per i dispositivi a cui viene impedito l'accesso alle risorse, il servizio che blocca l'accesso deve reindirizzare tutti gli utenti al [portale di gestione](https://portal.manage.microsoft.com) per determinare i motivi per cui il dispositivo è bloccato.  Se gli utenti visitano questa pagina, viene rivalutata la conformità dei loro dispositivi in modo sincrono.

## <a name="nac-and-conditional-access"></a>NAC e accesso condizionale

NAC interagisce con l'accesso condizionale per le decisioni relative al controllo di accesso. Per altre informazioni, vedere [Modi comuni per usare l'accesso condizionale con Intune](conditional-access-intune-common-ways-use.md).

## <a name="how-the-nac-integration-works"></a>Funzionamento dell'integrazione NAC

L'elenco seguente è una panoramica del funzionamento dell'integrazione di NAC con Intune. I primi tre passaggi, da 1 a 3, illustrano il processo di onboarding. Dopo aver integrato la soluzione NAC con Intune, seguire i passaggi da 4 a 9 che descrivono l'intera operazione.

![Immagine concettuale del funzionamento di NAC con Intune](./media/network-access-control-integrate/ca-intune-common-ways-2.png)

1. Registrare la soluzione partner NAC con Azure Active Directory (AAD) e concedere le autorizzazioni delegate all'API NAC di Intune.
2. Configurare la soluzione partner NAC con le impostazioni appropriate, incluso l'URL di individuazione di Intune.
3. Configurare la soluzione partner NAC per l'autenticazione del certificato.
4. L'utente si connette al punto di accesso WiFi aziendale o esegue una richiesta di connessione VPN.
5. La soluzione partner NAC inoltra le informazioni sul dispositivo a Intune e chiede a Intune lo stato di conformità e la registrazione del dispositivo.
6. Se il dispositivo non è conforme o non è registrato, la soluzione partner NAC indica all'utente di registrare o risolvere la conformità del dispositivo.
7. Il dispositivo prova di nuovo a verificare la conformità e lo stato di registrazione.
8. Dopo che il dispositivo è registrato e conforme, la soluzione partner NAC Ottiene lo stato da Intune.
9. La connessione viene stabilita correttamente e consente al dispositivo di accedere alle risorse aziendali.

## <a name="use-nac-for-vpn-on-your-iosipados-devices"></a>Usare il controllo accesso alla rete per VPN nei dispositivi iOS/iPadOS

Il controllo di accesso alla rete è disponibile nelle reti VPN seguenti senza abilitarlo nel profilo VPN:

- Controllo di accesso alla rete per Cisco Legacy AnyConnect
- F5 Access Legacy
- Citrix VPN

NAC è inoltre supportato per Cisco AnyConnect, Citrix SSO e F5 Access.

### <a name="to-enable-nac-for-cisco-anyconnect-for-ios"></a>Per abilitare il controllo accesso alla rete per Cisco AnyConnect per iOS

- Integrare ISE con Intune per NAC come descritto nel collegamento seguente.
- Impostare l'opzione **Abilita il controllo accesso alla rete** nel profilo VPN su **Sì**.

### <a name="to-enable-nac-for-citrix-sso"></a>Per abilitare il controllo accesso alla rete per Citrix SSO

- Usare Citrix Gateway 12.0.59 o versione successiva.  
- Gli utenti devono avere installato Citrix SSO 1.1.6 o versione successiva.
- [Integrare NetScaler con Intune per il controllo accesso alla rete](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html) come descritto nella documentazione del prodotto Citrix.
- Nel profilo VPN selezionare **Base settings** > **Enable Network Access Control (NAC)** > **I agree** (Impostazioni di base > Abilita controllo di accesso alla rete > Accetto).

### <a name="to-enable-nac-for-f5-access"></a>Per abilitare il controllo accesso alla rete per F5 Access

- Usare F5 BIG-IP 13.1.1.5 o versione successiva.
- Integrare BIG-IP con Intune per il controllo di accesso alla rete. Per la procedura, vedere [Overview: Configuring APM for device posture checks with endpoint management systems](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) della Guida di F5.
- Nel profilo VPN selezionare **Base settings** > **Enable Network Access Control (NAC)** > **I agree** (Impostazioni di base > Abilita controllo di accesso alla rete > Accetto).

La connessione VPN viene interrotta ogni 24 ore per motivi di sicurezza. La VPN può essere riconnessa immediatamente.

Stiamo collaborando con i partner per rilasciare una soluzione di controllo accesso alla rete per i client più recenti. Quando le soluzioni saranno pronte, questo articolo verrà aggiornato con altre informazioni.

## <a name="next-steps"></a>Passaggi successivi

- [Integrate Cisco ISE with Intune](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) (Integrare ISE Cisco con Intune)
- [Integrate Citrix NetScaler with Intune](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html) (Integrare Citrix NetScaler con Intune)
- [Integrare F5 BIG-IP Access Policy Manager con Intune](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-13-0-0/6.html)
- [Integrate HP Aruba Clear Pass with Intune](https://support.arubanetworks.com/Documentation/tabid/77/DMXModule/512/Command/Core_Download/Default.aspx?EntryId=31271) (Integrare HP Aruba Clear Pass con Intune)
- [Integrare Squadra security Removable Media Manager (secRMM) con Intune](http://www.squadratechnologies.com/StaticContent/ProductDownload/secRMM/9.9.0.0/secRMMIntuneAccessControlSetupGuide.pdf)
