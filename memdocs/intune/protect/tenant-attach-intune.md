---
title: Usare i criteri di Intune con i dispositivi di Configuration Manager collegati al tenant | Microsoft Docs
description: Configurare il collegamento al tenant dei dispositivi di Configuration Manager nell'interfaccia di amministrazione di Microsoft Endpoint Manager in modo da potervi distribuire i criteri di Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 5c3d5bd14efddc74e1898f374bbaac2aa962ebf7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193666"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Configurare il collegamento al tenant per supportare i criteri di sicurezza degli endpoint da Intune

Quando si usa lo scenario di collegamento al tenant di Configuration Manager, è possibile distribuire i criteri di sicurezza degli endpoint di Intune ai dispositivi gestiti con Configuration Manager. Per usare questo scenario, è necessario prima configurare il collegamento al tenant per Configuration Manager e abilitare le raccolte di dispositivi di Configuration Manager per l'uso con Intune. Una volta abilitate le raccolte per l'uso, usare l'interfaccia di amministrazione di Microsoft Endpoint Manager per creare e distribuire i criteri.

I tipi di criteri seguenti sono supportati dai dispositivi di Configuration Manager collegati al tenant:

- Criteri antivirus di sicurezza degli endpoint
- Criteri di rilevamento degli endpoint e risposta per la sicurezza

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Requisiti per l'uso dei criteri di Intune per il collegamento al tenant

Per supportare i criteri di sicurezza degli endpoint di Intune con i dispositivi di Configuration Manager, l'ambiente di Configuration Manager richiede le configurazioni seguenti. Questo articolo illustra le [indicazioni sulla configurazione](#set-up-configuration-manager-to-support-intune-policies):

### <a name="general-requirements-for-tenant-attach"></a>Requisiti generali per il collegamento al tenant

- **Configurare il collegamento al tenant**: con lo scenario di *collegamento al tenant* è possibile sincronizzare le raccolte di dispositivi di Configuration Manager con l'interfaccia di amministrazione di Microsoft Endpoint Manager. È quindi possibile usare l'interfaccia di amministrazione per distribuire i criteri supportati a tali raccolte.

  Il collegamento del tenant è spesso configurato con la co-gestione, ma è possibile configurarlo automaticamente.

- **Sincronizzare le raccolte di Configuration Manager**: quando si configura il collegamento del tenant, è possibile selezionare le raccolte di dispositivi di Configuration Manager da sincronizzare con l'interfaccia di amministrazione di Microsoft Endpoint Manager. È anche possibile modificare le raccolte di dispositivi sincronizzate in un secondo momento. I criteri per i dispositivi di Configuration Manager possono essere assegnati solo a raccolte sincronizzate.

  Dopo aver selezionato le raccolte da sincronizzare, è necessario abilitarle per l'uso con i criteri di sicurezza degli endpoint di Intune.

- **Autorizzazioni per Azure AD**: per completare la configurazione del collegamento al tenant, è necessario un account con autorizzazioni di amministratore globale per la sottoscrizione di Azure.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Requisiti specifici per i criteri di sicurezza degli endpoint di Intune

- **Criteri antivirus** (*anteprima*):

  - **Configuration Manager** - Sono supportati gli ambienti seguenti:

    - **Configuration Manager (Current Branch) versione 2006 o successiva** - Con questa versione Current Branch è stato aggiunto il supporto per i criteri antivirus di Intune.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Tenant per Microsoft Defender Advanced Threat Protection** - È necessario integrare il tenant di Microsoft Defender ATP con il tenant di Microsoft Endpoint Manager (sottoscrizione di Intune).  Vedere [Usare Microsoft Defender ATP](advanced-threat-protection.md) nella documentazione di Intune.

- **Criteri di rilevamento di endpoint e risposta**:

  - **Configuration Manager** - Sono supportati gli ambienti seguenti:

    - **Configuration Manager Technical Preview 2003 o versione successiva** - Con questa versione Technical Preview 2003 è stato aggiunto il supporto per i criteri di rilevamento di endpoint e risposta di Intune.

    - **Configuration Manager (Current Branch) versione 2002 o successiva** -Se si usa Configuration Manager con la versione 2002, è necessario installare l'aggiornamento in console **Configuration Manager 2002 Hotfix (KB4563473)** . Questo aggiornamento abilita il supporto in Configuration Manager 2002 per l'uso dei criteri di sicurezza degli endpoint.

  - **Tenant per Microsoft Defender Advanced Threat Protection** - È necessario integrare il tenant di Microsoft Defender ATP con il tenant di Microsoft Endpoint Manager (sottoscrizione di Intune).  Vedere [Usare Microsoft Defender ATP](advanced-threat-protection.md) nella documentazione di Intune.

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Configurare Configuration Manager per il supporto dei criteri di Intune

Prima di distribuire i criteri di Intune per i dispositivi di Configuration Manager, completare le configurazioni descritte nelle sezioni seguenti. Queste configurazioni eseguono l'onboarding dei dispositivi di Configuration Manager con Microsoft Defender ATP e ne consentono il funzionamento con i criteri di Intune.

Le attività seguenti vengono completate nella console di Configuration Manager. Se non si ha familiarità con Configuration Manager, è possibile collaborare con un amministratore di Configuration Manager per completare queste attività.

1. [Installare l'aggiornamento per Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Abilitare il collegamento del tenant](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Selezionare le raccolte da sincronizzare](#task-3-select-collections-to-synchronize)
4. [Abilitare le raccolte per il supporto dei criteri di Intune](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Per altre informazioni sull'uso di Microsoft Defender ATP con Configuration Manager, vedere gli articoli seguenti nella documentazione di Configuration Manager:
>
> - [Eseguire l'onboarding di client di Configuration Manager in Microsoft Defender ATP tramite l'interfaccia di amministrazione di Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Collegamento del tenant di Microsoft Endpoint Manager: sincronizzazione e azioni dei dispositivi](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Attività 1: installare l'aggiornamento per Configuration Manager

Se si usa Configuration Manager (Current Branch) versione 2002, installare l'aggiornamento in console seguente, che aggiunge il supporto per i criteri di sicurezza degli endpoint distribuiti dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

**Dettagli sull'aggiornamento**:

- **Hotfix di Configuration Manager 2002 (KB4563473)**

Per installarlo, seguire le istruzioni disponibili in [Installare gli aggiornamenti nella console](../../configmgr/core/servers/manage/install-in-console-updates.md) nella documentazione di Configuration Manager.

Dopo aver installato l'aggiornamento, tornare qui per continuare a configurare l'ambiente per supportare i criteri di sicurezza degli endpoint dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Attività 2: configurare il collegamento del tenant e sincronizzare le raccolte

Con il collegamento del tenant è possibile specificare le raccolte di dispositivi dalla distribuzione di Configuration Manager per la sincronizzazione con l'interfaccia di amministrazione di Microsoft Endpoint Manager. Dopo aver sincronizzato le raccolte, usare l'interfaccia di amministrazione per visualizzare le informazioni su tali dispositivi e per distribuire i criteri di sicurezza degli endpoint di Intune.

Per altre informazioni sul collegamento al tenant, vedere [Abilitare il collegamento al tenant](../../configmgr/tenant-attach/device-sync-actions.md) nella documentazione di Configuration Manager.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Abilitare il collegamento del tenant se la co-gestione è disabilitata

> [!TIP]
> Per abilitare il collegamento del tenant è possibile usare la **Configurazione guidata della co-gestione** nella console di Configuration Manager, ma non è necessario abilitare la co-gestione.
>
> Se si prevede di abilitare la co-gestione, prima di continuare è consigliabile acquisire familiarità con questa funzionalità, con i relativi prerequisiti e con il modo in cui gestire i carichi di lavoro. Vedere [Informazioni sulla co-gestione](../../configmgr/comanage/overview.md) nella documentazione di Configuration Manager.

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.
2. Nella barra multifunzione fare clic su **Configura la co-gestione** per aprire la procedura guidata.
3. Nella pagina **Onboarding del tenant** selezionare **AzurePublicCloud** per l'ambiente in uso. Il cloud di Azure per enti pubblici non è supportato.
   1. Fare clic su **Accedi**. Usare l'account di *amministratore globale* per accedere.

   2. Nella pagina **Onboarding del tenant** verificare che l'opzione **Upload to Microsoft Endpoint Manager admin center** (Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager) sia selezionata.

   3. Rimuovere il segno di spunta da **Abilita la registrazione automatica dei client per la co-gestione**.

      Quando questa opzione è selezionata, la procedura guidata visualizza altre pagine per completare la configurazione della co-gestione. Per altre informazioni, vedere [Abilitare la co-gestione](../../configmgr/comanage/how-to-enable.md) nella documentazione di Configuration Manager.

     ![Configurare il collegamento del tenant](./media/tenant-attach-intune/tenant-onboarding.png)

4. Fare clic su **Avanti** e quindi su **Sì** per accettare la notifica **Crea un'applicazione di AAD**. Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione delle raccolte nell'interfaccia di amministrazione di Microsoft Endpoint Manager.

5. Nella pagina **Configure upload** (Configura caricamento) è possibile configurare le raccolte da sincronizzare. È possibile limitare la configurazione a una o più raccolte di dispositivi o usare l'impostazione di caricamento dei dispositivi consigliata per **All my devices managed by Microsoft Endpoint Configuration Manager** (Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager).

   > [!TIP]
   > È possibile ignorare la selezione delle raccolte per il momento e in seguito usare le informazioni nell'attività 3 per configurare le raccolte da sincronizzare con l'interfaccia di amministrazione di Microsoft Endpoint Manager.

6. Fare clic su **Riepilogo** per verificare la selezione e quindi su **Avanti**.

7. Al termine della procedura guidata, fare clic su **Chiudi**.

   Il collegamento del tenant è ora configurato e le raccolte selezionate vengono sincronizzate con l'interfaccia di amministrazione di Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Abilitare il collegamento al tenant quando si usa già la co-gestione

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.

2. Fare clic con il pulsante destro del mouse sulle impostazioni di co-gestione e selezionare **Proprietà**.

3. Nella scheda **Configure upload** (Configura caricamento) selezionare **Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager**. Fare clic su **Apply**.

   L'impostazione predefinita per il caricamento del dispositivo è **Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager**. È anche possibile scegliere di limitare la configurazione a una o più raccolte di dispositivi.

   ![Visualizzare la scheda proprietà di co-gestione](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > È possibile ignorare la selezione delle raccolte per il momento e in seguito usare le informazioni nell'attività 3 per configurare le raccolte da sincronizzare con l'interfaccia di amministrazione di Microsoft Endpoint Manager.

4. Quando richiesto, accedere con l'account di *amministratore globale*.

5. Fare clic su **Sì** per accettare la notifica **Crea un'applicazione di AAD**. Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione.

6. Fare clic su **OK** per uscire dalle proprietà di co-gestione dopo aver apportato le modifiche.

   Il collegamento del tenant è ora configurato e le raccolte selezionate vengono sincronizzate con l'interfaccia di amministrazione di Microsoft Endpoint Manager.

### <a name="task-3-select-collections-to-synchronize"></a>Attività 3: selezionare le raccolte da sincronizzare

Quando il collegamento del tenant è configurato, è possibile selezionare le raccolte da sincronizzare. Se non si è ancora eseguita la sincronizzazione delle raccolte o se è necessario riconfigurare quelle da sincronizzare, è possibile modificare le proprietà della co-gestione nella console di Configuration Manager per eseguire questa operazione.

#### <a name="select-collections"></a>Selezionare le raccolte

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.

2. Fare clic con il pulsante destro del mouse sulle impostazioni di co-gestione e selezionare **Proprietà**.

3. Nella scheda **Configure upload** (Configura caricamento) selezionare **Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager**. Fare clic su **Apply**.

   L'impostazione predefinita per il caricamento del dispositivo è **Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager**. È anche possibile scegliere di limitare la configurazione a una o più raccolte di dispositivi.

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Attività 4: Abilitare le raccolte per i criteri di sicurezza degli endpoint

Dopo aver configurato le raccolte per la sincronizzazione con l'interfaccia di amministrazione di Microsoft Endpoint Manager, abilitarle per l'uso con i criteri di sicurezza degli endpoint. Quando si abilitano le raccolte di dispositivi per l'uso con i criteri di sicurezza degli endpoint di Intune, si configurano i dispositivi in tali raccolte per l'onboarding con Microsoft Defender ATP.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Abilitare le raccolte per l'uso con i criteri di sicurezza degli endpoint

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Passaggi successivi

- [Configurare i criteri di sicurezza degli endpoint](endpoint-security-policy.md#create-an-endpoint-security-policy) per *antivirus* e *rilevamento degli endpoint e risposta*.

- Altre informazioni su [Rilevamento di endpoint e risposta](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) sono disponibili nella documentazione di Microsoft Defender ATP.