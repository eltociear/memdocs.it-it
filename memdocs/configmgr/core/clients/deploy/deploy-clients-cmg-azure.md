---
title: Installare il client con Azure AD
titleSuffix: Configuration Manager
description: Installare e assegnare il client di Configuration Manager in dispositivi Windows 10 usando Azure Active Directory per l'autenticazione
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b447e5c8d34a4b8758fa0fd6109113b0675a635
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347016"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione

Per installare il client di Configuration Manager nei dispositivi Windows 10 con l'autenticazione di Azure AD, integrare Configuration Manager con Azure Active Directory (Azure AD). I client possono essere sulla Intranet in comunicazione diretta con un punto di gestione abilitato per HTTPS o con qualsiasi punto di comunicazione in un sito abilitato per HTTP avanzato. Possono anche essere basati su Internet e comunicare attraverso il gateway di gestione cloud o un punto di gestione basato su Internet. Questo processo usa Azure AD per autenticare i client per il sito di Configuration Manager. Azure AD evita di dover configurare e usare i certificati di autenticazione client.

La configurazione di Azure AD può essere più semplice per alcuni clienti rispetto alla configurazione di un'infrastruttura a chiave pubblica (PKI) per l'autenticazione basata su certificato. Alcune funzionalità richiedono l'onboarding del sito in Azure AD, ma non richiedono necessariamente l'aggiunta dei client ad Azure AD.<!-- SCCMDocs issue 1259 --> Per altre informazioni, vedere gli articoli seguenti:

- [Pianificare Azure Active Directory](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Usare Azure AD per la co-gestione](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Prima di iniziare

- Un tenant di Azure AD è un prerequisito  

- Requisiti dei dispositivi:  

  - Windows 10  

  - Aggiunto ad Azure AD, aggiunto solo al dominio cloud o ibrido aggiunto ad Azure AD  

- Requisiti dell'utente:  

  - L'utente che ha eseguito l'accesso deve essere un'identità Azure AD.

  - Se l'utente è un'identità federata o sincronizzata, configurare sia [Individuazione utente Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) che [Individuazione utente Azure AD](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc) di Configuration Manager. Per altre informazioni sulle identità ibride, vedere [Definire una strategia di adozione della soluzione ibrida di gestione delle identità](https://docs.microsoft.com/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->

- Oltre ai [prerequisiti esistenti](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) per il ruolo del sistema del sito punto di gestione, abilitare anche **ASP.NET 4.5** in questo server. Includere eventuali altre opzioni che vengono automaticamente selezionate quando si abilita ASP.NET 4.5.  

- Determinare se il punto di gestione richiede HTTPS. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- Se necessario, configurare un [gateway di gestione cloud](../manage/cmg/plan-cloud-management-gateway.md) per distribuire i client basati su Internet. Per i client locali che eseguono l'autenticazione con Azure AD, non è necessario un gateway di gestione cloud.  

> [!TIP]
> A partire dalla versione 2002,<!--5686290--> Configuration Manager estende il supporto per i dispositivi basati su Internet che non si connettono spesso alla rete interna, non possono essere aggiunti ad Azure Active Directory (Azure AD) e non hanno un metodo per installare un certificato emesso da PKI. Per altre informazioni, vedere [Autenticazione basata su token per CMG](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Configurare i servizi di Azure per la gestione cloud

Connettere il sito di Configuration Manager ad Azure AD come primo passaggio. Per informazioni dettagliate su questo processo, vedere [Configurare i servizi di Azure da usare con Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md). Creare una connessione al servizio **Gestione cloud**.

Abilitare l'[individuazione di utenti di Azure AD](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) come parte dell'onboarding in **Gestione cloud**.

Eseguite queste operazioni, il sito di Configuration Manager è connesso ad Azure AD.

## <a name="configure-client-settings"></a>Configurare le impostazioni client

Tali impostazioni consentono di configurare i dispositivi Windows 10 come aggiunti in modo ibrido. Consentono inoltre di abilitare i client basati su Internet per l'uso del gateway di gestione cloud e del punto di distribuzione cloud.

1. Configurare le impostazioni client seguenti nel gruppo **Servizi cloud**. Per altre informazioni, vedere [Come configurare le impostazioni client](configure-client-settings.md).

    - **Consentire accesso al punto di distribuzione cloud**: abilitare questa impostazione per consentire ai dispositivi basati su Internet di ottenere il contenuto necessario per l'installazione del client di Configuration Manager. Se il contenuto non è disponibile nel punto di distribuzione cloud, dispositivi possono recuperarlo dal gateway di gestione cloud. Il bootstrap di installazione del client ritenta il punto di distribuzione cloud per quattro ore prima di eseguire il fallback al gateway di gestione cloud.<!--495533-->  

    - **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory**: impostare su **Sì** o **No**. L'impostazione predefinita è **Sì**. Questo è il comportamento predefinito anche in Windows 10, versione 1709.

        > [!TIP]
        > I dispositivi aggiunti in modo ibrido vengono inseriti in un dominio di Active Directory locale e registrati con Azure AD. Per altre informazioni, vedere [Dispositivi aggiunti ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid).<!-- MEMDocs#325 -->

    - **Consenti ai client di usare un gateway di gestione cloud**: impostare su **Sì** (impostazione predefinita) o su **No**.  

2. Distribuire le impostazioni client per la raccolta necessaria di dispositivi. Non distribuire queste impostazioni alle raccolte di utenti.

Per verificare se il dispositivo è aggiunto in modo ibrido, eseguire `dsregcmd.exe /status` in un prompt dei comandi. Se il dispositivo è aggiunto ad Azure AD oppure è aggiunto in modo ibrido, nel campo **AzureAdjoined** nei risultati è presente il valore **Sì**. Per altre informazioni, vedere [comando dsregcmd - stato del dispositivo](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd).

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Installare e registrare il client usando l'identità di Azure AD

Per installare manualmente il client usando l'identità di Azure AD, per prima cosa esaminare il processo generale nella sezione [Come installare manualmente i client](deploy-clients-to-windows-computers.md#BKMK_Manual).

> [!Note]  
> Il dispositivo richiede l'accesso a Internet per contattare Azure AD, ma non deve necessariamente essere basato su Internet.

L'esempio seguente illustra la struttura generale della riga di comando: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](about-client-installation-properties.md).

Il parametro **/mp** e la proprietà **CCMHOSTNAME** specificano uno degli elementi seguenti, a seconda dello scenario:

- Punto di gestione locale. Specificare solo il parametro **/mp**. La proprietà **CCMHOSTNAME** non è obbligatoria.
- Gateway di gestione cloud
- Punto di gestione basato su Internet

La proprietà **SMSMP** specifica il punto di gestione locale o basato su Internet.

In questo esempio viene usato un gateway di gestione cloud. Sostituisce i valori di esempio: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Il sito pubblica le informazioni aggiuntive di Azure AD in Cloud Management Gateway (CMG). Un client aggiunto ad Azure AD ottiene queste informazioni da CMG durante il processo ccmsetup, usando lo stesso tenant a cui viene aggiunto. Questo comportamento semplifica ulteriormente l'installazione del client in un ambiente con più di un tenant di Azure AD. Le uniche due proprietà di ccmsetup richieste sono **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

Per automatizzare l'installazione del client usando l'identità di Azure AD con Microsoft Intune, vedere [How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) (Come preparare i dispositivi basati su Internet per la cogestione).

## <a name="next-steps"></a>Passaggi successivi

Al termine dell'operazione, è possibile continuare a [monitorare e gestire i client](../manage/monitor-clients.md).
