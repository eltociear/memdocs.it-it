---
title: Collegamento del tenant di Microsoft Endpoint Manager
titleSuffix: Configuration Manager
description: Caricare i dispositivi Configuration Manager nel servizio cloud e intraprendere le azioni dall'interfaccia di amministrazione.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: be1c938cfcf332edb37e24e4094567f88f363560
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795619"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Connessione tenant di Microsoft Endpoint Manager: azioni dispositivo e sincronizzazione dispositivo
<!--3555758 live 3/4/2020-->
*Si applica a: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft ha riunito Configuration Manager e Intune in un'unica console denominata **Interfaccia di amministrazione di Microsoft Endpoint Manager**.

A partire da Configuration Manager versione 2002, è possibile caricare i dispositivi Configuration Manager nel servizio cloud ed eseguire le azioni dal pannello **dispositivi** nell'interfaccia di amministrazione.

## <a name="prerequisites"></a>Prerequisiti

- Un account *amministratore globale* per l'accesso quando si applica questa modifica. Per ulteriori informazioni, vedere la pagina relativa ai [ruoli di amministratore Azure Active Directory (Azure ad)](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Il caricamento crea un'app di terze parti e un'entità servizio di prima entità nel tenant del Azure AD.
- Un ambiente cloud pubblico di Azure.
- Gli account utente che attivano le azioni del dispositivo presentano i prerequisiti seguenti:
   - È stato individuato con [Azure Active Directory individuazione utente](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) e [Active Directory individuazione utente](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Ciò significa che l'account utente deve essere un oggetto utente sincronizzato in Azure AD.
   - Autorizzazione **avvia Configuration Manager azione** in **attività remote** nell'interfaccia di amministrazione di Microsoft Endpoint Manager.


## <a name="internet-endpoints"></a>Endpoint Internet

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>Abilita caricamento dispositivo

- Se la co-gestione è attualmente abilitata, [modificare le proprietà di co-gestione](#bkmk_edit) per abilitare il caricamento del dispositivo.
- Se la co-gestione non è abilitata, [usare la **Configurazione guidata co-gestione** ](#bkmk_config) per abilitare il caricamento del dispositivo.
   - È possibile caricare i dispositivi senza abilitare la registrazione automatica per la co-gestione o cambiare i carichi di lavoro in Intune.
- Verranno caricati tutti i dispositivi gestiti da Configuration Manager con **Sì** nella colonna **client** . Se necessario, è possibile limitare il caricamento a una singola raccolta di dispositivi.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Modificare le proprietà di co-gestione per abilitare il caricamento del dispositivo

Se la co-gestione è attualmente abilitata, modificare le proprietà di co-gestione per abilitare il caricamento dei dispositivi attenendosi alle istruzioni seguenti:

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.
1. Fare clic con il pulsante destro del mouse sulle impostazioni di co-gestione e selezionare **Proprietà**.
1. Nella scheda **Configure upload** (Configura caricamento) selezionare **Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager**. Fare clic su **Apply**.
   - L'impostazione predefinita per il caricamento del dispositivo è **Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager**. Se necessario, è possibile limitare il caricamento a una singola raccolta di dispositivi.

   [![Configurazione guidata della co-gestione](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. Quando richiesto, accedere con l'account di *amministratore globale*.
1. Fare clic su **Sì** per accettare la notifica **Crea un'applicazione di AAD**. Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione.
1. Fare clic su **OK** per uscire dalle proprietà di co-gestione dopo aver apportato le modifiche.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Usare la configurazione guidata della co-gestione per abilitare il caricamento del dispositivo
Se la co-gestione non è abilitata, usare la **Configurazione guidata co-gestione** per abilitare il caricamento del dispositivo. È possibile caricare i dispositivi senza abilitare la registrazione automatica per la co-gestione o cambiare i carichi di lavoro in Intune. Abilitare il caricamento del dispositivo attenendosi alle istruzioni seguenti:

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.
1. Nella barra multifunzione fare clic su **Configura la co-gestione** per aprire la procedura guidata.
1. Nella pagina **Onboarding del tenant** selezionare **AzurePublicCloud** per l'ambiente in uso. Il cloud di Azure per enti pubblici non è supportato.
1. Fare clic su **Accedi**. Usare l'account di *amministratore globale* per accedere.
1. Assicurarsi che l'opzione **carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager** sia selezionata nella pagina **onboarding del tenant** .
   - Verificare che l'opzione **Abilita registrazione automatica client per la co-gestione** non sia selezionata se non si vuole abilitare la co-gestione adesso. Se si vuole abilitare la co-gestione, selezionare l'opzione.
   - Se si Abilita la co-gestione insieme al caricamento del dispositivo, verranno fornite ulteriori pagine della procedura guidata per il completamento. Per altre informazioni, vedere [Abilitare la co-gestione](../comanage/how-to-enable.md).

   [![Configurazione guidata della co-gestione](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Fare clic su **Avanti** e quindi su **Sì** per accettare la notifica **Crea un'applicazione di AAD**. Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione.
1. Nella pagina **Configura caricamento** selezionare l'impostazione consigliata per il caricamento dei **dispositivi per tutti i dispositivi gestiti da Microsoft endpoint Configuration Manager**. Se necessario, è possibile limitare il caricamento a una singola raccolta di dispositivi.
1. Fare clic su **Riepilogo** per verificare la selezione e quindi su **Avanti**.
1. Al termine della procedura guidata, fare clic su **Chiudi**.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Verifica il caricamento

1. Aprire **CMGatewaySyncUploadWorker. log** dalla &lt; directory di installazione di ConfigMgr> \Logs.
1. Il tempo di sincronizzazione successivo è indicato dalle voci di log simili a `Next run time will be at approximately: 02/28/2020 16:35:31` .
1. Per i caricamenti dei dispositivi, cercare voci di log simili a `Batching N records` . **N** è il numero di dispositivi caricati nel cloud. 
1. Il caricamento viene eseguito ogni 15 minuti per le modifiche. Una volta caricate le modifiche, potrebbero essere necessari altri 5-10 minuti affinché le modifiche apportate al client siano visualizzate nell'interfaccia di **amministrazione di Microsoft Endpoint Manager**.

## <a name="perform-device-actions"></a>Eseguire azioni del dispositivo

1. In un browser passare a`endpoint.microsoft.com`
1. Selezionare **dispositivi** quindi **tutti i dispositivi** per visualizzare i dispositivi caricati. **ConfigMgr** verrà visualizzato nella colonna **gestito da** per i dispositivi caricati.
   [![Tutti i dispositivi nell'interfaccia di amministrazione di Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Fare clic su un dispositivo per caricare la relativa pagina **Panoramica** .
1. Fare clic su una delle azioni seguenti:
   - **Sincronizzazione dei criteri del computer**
   - **Sincronizzazione dei criteri utente**
   - **Ciclo di valutazione app**

   [![Panoramica del dispositivo nell'interfaccia di amministrazione di Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Problemi noti

### <a name="specific-devices-dont-synchronize"></a>Dispositivi specifici non sincronizzati

<!--7099564-->
È possibile che dispositivi specifici, che sono Configuration Manager client, non vengano caricati nel servizio.

**Dispositivi interessati:** Se un dispositivo è un punto di distribuzione che usa lo stesso certificato PKI sia per la funzionalità del punto di distribuzione che per l'agente client, il dispositivo non verrà incluso nel tenant Connetti dispositivo Sincronizza.

**Comportamento:** Quando si esegue la connessione tenant durante la fase di caricamento, viene eseguita la prima volta una sincronizzazione completa. I cicli di sincronizzazione successivi sono sincronizzazioni Delta. Qualsiasi aggiornamento ai dispositivi interessati provocherà la rimozione del dispositivo dalla sincronizzazione.

## <a name="log-files"></a>File di registro
Usare i log seguenti che si trovano nel punto di connessione del servizio:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui file di log di allocazione tenant, vedere [risolvere i problemi di connessione tenant](technical-reference.md).
