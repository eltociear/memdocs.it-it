---
title: Collegamento del tenant di Microsoft Endpoint Manager
titleSuffix: Configuration Manager
description: Caricare i dispositivi Configuration Manager nel servizio cloud e intraprendere le azioni dall'interfaccia di amministrazione.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: bac86ca5a74d35b64e211936806ef1735f4e0eea
ms.sourcegitcommit: 231e2c3913a1d585310dfab7ffcd5c78c6bc5703
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88970465"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Connessione tenant di Microsoft Endpoint Manager: azioni dispositivo e sincronizzazione dispositivo
<!--3555758 live 3/4/2020-->
*Si applica a: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft ha riunito Configuration Manager e Intune in un'unica console denominata **Interfaccia di amministrazione di Microsoft Endpoint Manager**.

A partire da Configuration Manager versione 2002, è possibile caricare i dispositivi Configuration Manager nel servizio cloud ed eseguire le azioni dal pannello **dispositivi** nell'interfaccia di amministrazione.

## <a name="prerequisites"></a>Prerequisiti

- Un account *amministratore globale* per l'accesso quando si applica questa modifica. Per ulteriori informazioni, vedere la pagina relativa ai [ruoli di amministratore Azure Active Directory (Azure ad)](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Il caricamento crea un'app di terze parti e un'entità servizio di prima entità nel tenant del Azure AD.
- Un ambiente cloud pubblico di Azure.
- Gli account utente che attivano le azioni del dispositivo presentano i prerequisiti seguenti:
   - È stato individuato con [Azure Active Directory individuazione utente](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) e [Active Directory individuazione utente](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Ciò significa che l'account utente deve essere un oggetto utente sincronizzato in Azure AD.
   - Autorizzazione **avvia Configuration Manager azione** in **attività remote** nell'interfaccia di amministrazione di Microsoft Endpoint Manager.
- Se il sito di amministrazione centrale ha un [provider remoto](../core/plan-design/hierarchy/plan-for-the-sms-provider.md), seguire le istruzioni per le [autorità di certificazione hanno uno scenario di provider remoto](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) nell'articolo CMPivot. <!--7796824-->

## <a name="internet-endpoints"></a>Endpoint Internet

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

Il punto di connessione del servizio esegue una connessione in uscita prolungata a questi endpoint. Verificare che il proxy usato per il punto di connessione del servizio non verifichi il timeout delle connessioni in uscita troppo rapidamente. Si consiglia di 3 minuti per le connessioni in uscita a questi endpoint Internet. <!--7820969-->

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> Abilita caricamento dispositivo quando la co-gestione è già abilitata

Se è attualmente abilitata la co-gestione, verranno usate le proprietà di co-gestione per abilitare il caricamento del dispositivo. Quando la co-gestione non è già abilitata, [usare la configurazione guidata della **co-gestione** ](#bkmk_config) per abilitare il caricamento dei dispositivi.

Quando la co-gestione è già abilitata, modificare le proprietà di co-gestione per abilitare il caricamento del dispositivo attenendosi alle istruzioni seguenti:

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.
1. Sulla barra multifunzione selezionare **Proprietà** per i criteri di produzione di co-gestione.
1. Nella scheda **Configure upload** (Configura caricamento) selezionare **Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager**. Selezionare **Applica**.
   - L'impostazione predefinita per il caricamento del dispositivo è **Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager**. Se necessario, è possibile limitare il caricamento a una singola raccolta di dispositivi.
1. Selezionare l'opzione per **abilitare l'analisi degli endpoint per i dispositivi caricati in Microsoft Endpoint Manager** se si vuole ottenere informazioni dettagliate per ottimizzare l'esperienza dell'utente finale in [endpoint Analytics](../../analytics/overview.md).

   [![Caricare i dispositivi nell'interfaccia di amministrazione di Microsoft Endpoint Manager](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Quando richiesto, accedere con l'account di *amministratore globale*.
1. Selezionare **Sì** per accettare la notifica di **creazione dell'applicazione AAD** . Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione.
1. Scegliere **OK** per uscire dalle proprietà di co-gestione dopo avere apportato le modifiche.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> Abilita caricamento dispositivo quando la co-gestione non è abilitata

Se la co-gestione non è abilitata, verrà usata la **Configurazione guidata co-gestione** per abilitare il caricamento del dispositivo. È possibile caricare i dispositivi senza abilitare la registrazione automatica per la co-gestione o cambiare i carichi di lavoro in Intune. Verranno caricati tutti i dispositivi gestiti da Configuration Manager con **Sì** nella colonna **client** . Se necessario, è possibile limitare il caricamento a una singola raccolta di dispositivi. Se nell'ambiente è già abilitata la co-gestione, [modificare le proprietà di co-gestione](#bkmk_edit) per abilitare il caricamento del dispositivo.

Quando la co-gestione non è abilitata, usare le istruzioni seguenti per abilitare il caricamento del dispositivo:

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.
1. Sulla barra multifunzione selezionare **Configura co-gestione** per aprire la procedura guidata.
1. Nella pagina **Onboarding del tenant** selezionare **AzurePublicCloud** per l'ambiente in uso. Il cloud di Azure per enti pubblici e Azure Cina 21Vianet non sono supportati.
1. Selezionare **Accedi**. Usare l'account di *amministratore globale* per accedere.
1. Assicurarsi che l'opzione **carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager** sia selezionata nella pagina **onboarding del tenant** .
   - Verificare che l'opzione **Abilita registrazione automatica client per la co-gestione** non sia selezionata se non si vuole abilitare la co-gestione adesso. Se si vuole abilitare la co-gestione, selezionare l'opzione.
   - Se si Abilita la co-gestione insieme al caricamento del dispositivo, verranno fornite ulteriori pagine della procedura guidata per il completamento. Per altre informazioni, vedere [Abilitare la co-gestione](../comanage/how-to-enable.md).

   [![Configurazione guidata della co-gestione](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Scegliere **Avanti** e quindi **Sì** per accettare la notifica di **creazione dell'applicazione AAD** . Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione.
     - Facoltativamente, è possibile importare un'applicazione Azure AD creata in precedenza durante il caricamento del tenant di connessione (a partire dalla versione 2006). Per ulteriori informazioni, vedere la sezione [importare un'applicazione Azure ad creata in precedenza](#bkmk_aad_app) .
1. Nella pagina **Configura caricamento** selezionare l'impostazione consigliata per il caricamento dei **dispositivi per tutti i dispositivi gestiti da Microsoft endpoint Configuration Manager**. Se necessario, è possibile limitare il caricamento a una singola raccolta di dispositivi.
1. Selezionare l'opzione per **abilitare l'analisi degli endpoint per i dispositivi caricati in Microsoft Endpoint Manager** se si vuole ottenere informazioni dettagliate per ottimizzare l'esperienza dell'utente finale in [endpoint Analytics](../../analytics/overview.md)
1. Selezionare **Riepilogo** per verificare la selezione, quindi scegliere **Avanti**.
1. Al termine della procedura guidata, selezionare **Chiudi**.  

## <a name="perform-device-actions"></a>Eseguire azioni del dispositivo

1. In un browser passare a `endpoint.microsoft.com`
1. Selezionare **dispositivi** quindi **tutti i dispositivi** per visualizzare i dispositivi caricati. **ConfigMgr** verrà visualizzato nella colonna **gestito da** per i dispositivi caricati.
   [![Tutti i dispositivi nell'interfaccia di amministrazione di Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Selezionare un dispositivo per caricare la pagina di **Panoramica** .
1. Scegliere una delle azioni seguenti:
   - **Sincronizzazione dei criteri del computer**
   - **Sincronizzazione dei criteri utente**
   - **Ciclo di valutazione app**

   [![Panoramica del dispositivo nell'interfaccia di amministrazione di Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> Importare un'applicazione Azure AD creata in precedenza (facoltativo)
<!--6479246-->
*(Introdotta nella versione 2006)*

Durante un [nuovo onboarding](#bkmk_config), un amministratore può specificare un'applicazione creata in precedenza durante il caricamento in un tenant. Non condividere o riutilizzare Azure AD applicazioni in più gerarchie. Se si dispone di più gerarchie, creare applicazioni Azure AD separate per ciascuna di esse.

Nella pagina **Onboarding del tenant** nella **Configurazione guidata della co-gestione** selezionare **Importa facoltativamente un'app Web separata per sincronizzare i dati del client Configuration Manager nell'interfaccia di amministrazione di Microsoft Endpoint Manager**. Questa opzione richiederà di specificare le informazioni seguenti per l'app Azure AD:

- Nome del tenant di Azure AD
- ID tenant di Azure AD
- Nome dell'applicazione
- ID client
- Chiave privata
- Scadenza della chiave privata
- URI ID app

### <a name="azure-ad-application-permissions-and-configuration"></a>Azure AD le autorizzazioni e la configurazione dell'applicazione

L'uso di un'applicazione creata in precedenza durante il caricamento in un attacco tenant richiede le autorizzazioni seguenti:

- Autorizzazioni Configuration Manager microservizi:
   - CmCollectionData. Read
   - CmCollectionData. Write

- Autorizzazioni Microsoft Graph:
   - Autorizzazione directory. Read. All [Applications](/graph/permissions-reference#application-permissions)
   - Directory. Read. tutte le autorizzazioni per la [directory delegata](/graph/permissions-reference#directory-permissions)

- Assicurarsi che sia selezionata l'opzione **Concedi l'autorizzazione dell'amministratore per il tenant** per l'applicazione Azure ad. Per altre informazioni, vedere [concedere il consenso dell'amministratore in registrazioni app](/azure/active-directory/manage-apps/grant-admin-consent).

- L'applicazione importata deve essere configurata come segue:
   - Registrato solo per gli **account in questa directory aziendale**. Per altre informazioni, vedere [modificare gli utenti che possono accedere all'applicazione](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Ha un URI ID applicazione e un segreto validi



## <a name="next-steps"></a>Passaggi successivi

- [Registrare Configuration Manager dispositivi in endpoint Analytics](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Per informazioni sui file di log di connessione del tenant, vedere [risolvere i problemi di connessione tenant](troubleshoot.md).