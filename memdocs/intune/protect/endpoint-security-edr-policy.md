---
title: Gestire le impostazioni per il rilevamento di endpoint e risposta con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri per i dispositivi gestiti con i criteri per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
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
ms.openlocfilehash: ac8f82396571a7ae39df43662000f9f3f17d0430
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990872"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Criteri per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Intune

Quando si integra Microsoft Defender Advanced Threat Protection
 (Defender ATP) con Intune, è possibile usare i criteri di sicurezza degli endpoint per il rilevamento di endpoint e risposta (EDR) per gestire le impostazioni EDR ed eseguire l'onboarding di dispositivi in Defender ATP.

Le funzionalità di Rilevamento di endpoint e riposta di Defender ATP offrono rilevamenti avanzati degli attacchi quasi in tempo reale e di utilità pratica. Gli analisti della sicurezza possono impostare la priorità degli avvisi in modo efficace, ottenere la visibilità dell'ambito completo di una violazione e intraprendere azioni di risposta per correggere le minacce.

I criteri EDR includono profili specifici della piattaforma per gestire le impostazioni per EDR. I profili includono automaticamente un *pacchetto di onboarding* per Defender ATP. I pacchetti di onboarding rappresentano il modo in cui i dispositivi sono configurati per funzionare con Defender ATP. Dopo l'onboarding di un dispositivo, è possibile iniziare a usare i dati sulle minacce da quel dispositivo.

I criteri EDR vengono distribuiti a gruppi di dispositivi in Azure Active Directory (Azure AD) gestiti con Intune e a raccolte di dispositivi locali gestiti con Configuration Manager, inclusi i server Windows. I criteri EDR per percorsi di gestione diversi richiedono pacchetti di onboarding diversi. È quindi possibile creare criteri EDR separati per i diversi tipi di dispositivi gestiti.

> [!TIP]
> Il supporto per i dispositivi gestiti con Configuration Manager è disponibile in *anteprima pubblica*.

I criteri di sicurezza degli endpoint per EDR sono disponibili in *Gestione* nel nodo **Endpoint security** (Sicurezza degli endpoint) dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Visualizzare le [impostazioni per i profili di rilevamento di endpoint e risposta](../protect/endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Prerequisiti per i criteri EDR

**Generale**:

- **Tenant per Microsoft Defender Advanced Threat Protection**: è necessario integrare il tenant di Defender ATP con il tenant di Microsoft Endpoint Manager (sottoscrizione a Intune) prima di poter creare criteri EDR. Vedere [Usare Microsoft Defender ATP](../protect/advanced-threat-protection.md) nella documentazione di Intune.

**Per supportare i dispositivi da Configuration Manager**:

Per supportare l'uso di criteri EDR con i dispositivi di Configuration Manager, l'ambiente di Configuration Manager richiede le configurazioni aggiuntive seguenti. Questo articolo illustra le [indicazioni sulla configurazione](#set-up-configuration-manager-to-support-edr-policy):

- **Configuration Manager versione 2002 o successiva**: il sito deve eseguire Configuration Manager 2002 o versione successiva.

- **Installare l'aggiornamento di Configuration Manager**: per abilitare il supporto in Configuration Manager 2002 per l'uso dei criteri EDR creati nell'interfaccia di amministrazione di Microsoft Endpoint Manager, installare l'aggiornamento seguente dalla console di Configuration Manager:
  - **Hotfix di Configuration Manager 2002 (KB4563473)**

- **Configurare il collegamento del tenant**: il collegamento del tenant consente di sincronizzare le raccolte di dispositivi da Configuration Manager all'interfaccia di amministrazione di Microsoft Endpoint Manager. È quindi possibile usare l'interfaccia di amministrazione per distribuire i criteri EDR a tali raccolte.

  Il collegamento del tenant è spesso configurato con la co-gestione, ma è possibile configurarlo automaticamente.

- **Sincronizzare le raccolte di Configuration Manager**: quando si configura il collegamento del tenant, è possibile selezionare le raccolte di dispositivi di Configuration Manager da sincronizzare con l'interfaccia di amministrazione di Microsoft Endpoint Manager. È anche possibile modificare le raccolte di dispositivi sincronizzate in un secondo momento. I criteri EDR per i dispositivi di Configuration Manager possono essere assegnati solo a raccolte sincronizzate.

  Dopo aver selezionato le raccolte da sincronizzare, è necessario abilitarle per l'uso con Microsoft Defender ATP.

- **Autorizzazioni per Azure AD**: per completare la configurazione del collegamento del tenant e configurare le raccolte di Configuration Manager da sincronizzare con l'interfaccia di amministrazione di Microsoft Endpoint Manager, è necessario un account con le autorizzazioni di amministratore globale per la sottoscrizione di Azure.

## <a name="edr-profiles"></a>Profili EDR

[Visualizzare le impostazioni](../protect/endpoint-security-edr-profile-settings.md) che è possibile configurare per le piattaforme e i profili seguenti.

**Intune**: per i dispositivi gestiti con Intune sono supportati gli elementi seguenti:

- Piattaforma: **Windows 10 e versioni successive**: Intune distribuisce i criteri ai dispositivi nei gruppi di Azure AD.
- Profilo: **Rilevamento di endpoint e risposta (MDM)**

**Configuration Manager** *(in anteprima)* : per i dispositivi gestiti con Configuration Manager sono supportati gli elementi seguenti:

- Piattaforma: **Windows 10 e Windows Server**: Configuration Manager distribuisce i criteri ai dispositivi nelle raccolte di Configuration Manager.
- Profilo: **Rilevamento di endpoint e risposta (ConfigMgr) (anteprima)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Configurare Configuration Manager per il supporto dei criteri EDR

Prima di poter distribuire i criteri EDR per i dispositivi Configuration Manager, è necessario completare le configurazioni descritte nelle sezioni seguenti.

Queste configurazioni vengono eseguite nella console di Configuration Manager e nella distribuzione di Configuration Manager. Se non si ha familiarità con Configuration Manager, è possibile collaborare con un amministratore di Configuration Manager per completare queste attività.  

Nelle sezioni seguenti vengono descritte le attività necessarie:

1. [Installare l'aggiornamento per Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Abilitare il collegamento del tenant](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Selezionare le raccolte da sincronizzare](#task-3-select-collections-to-synchronize)
4. [Abilitare le raccolte per Microsoft Defender ATP](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> Per altre informazioni sull'uso di Microsoft Defender ATP con Configuration Manager, vedere gli articoli seguenti nella documentazione di Configuration Manager:
>
> - [Eseguire l'onboarding di client di Configuration Manager in Microsoft Defender ATP tramite l'interfaccia di amministrazione di Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Collegamento del tenant di Microsoft Endpoint Manager: sincronizzazione e azioni dei dispositivi](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Attività 1: installare l'aggiornamento per Configuration Manager

Configuration Manager versione 2002 richiede un aggiornamento per supportare l'uso con i criteri di rilevamento di endpoint e risposta distribuiti dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

**Dettagli sull'aggiornamento**:

- **Hotfix di Configuration Manager 2002 (KB4563473)**

Questo aggiornamento è disponibile come *aggiornamento nella console* per Configuration Manager 2002.

Per installarlo, seguire le istruzioni disponibili in [Installare gli aggiornamenti nella console](../../configmgr/core/servers/manage/install-in-console-updates.md) nella documentazione di Configuration Manager.

Dopo aver installato l'aggiornamento, tornare qui per continuare a configurare l'ambiente per supportare i criteri EDR dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Attività 2: configurare il collegamento del tenant e sincronizzare le raccolte

Se la co-gestione è stata abilitata in precedenza, il collegamento del tenant è già configurato ed è possibile passare all'[attività 3](#task-3-select-collections-to-synchronize).

Con il collegamento del tenant è possibile specificare le raccolte di dispositivi dalla distribuzione di Configuration Manager per la sincronizzazione con l'interfaccia di amministrazione di Microsoft Endpoint Manager. Dopo aver sincronizzato le raccolte, usare l'interfaccia di amministrazione per visualizzare le informazioni su tali dispositivi e per distribuire i criteri EDR da Intune.  

Per altre informazioni sul collegamento del tenant, vedere [Abilitare il collegamento di tenant](../../configmgr/tenant-attach/device-sync-actions.md) nella documentazione di Configuration Manager.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Abilitare il collegamento del tenant se la co-gestione è disabilitata

> [!TIP]
> Per abilitare il collegamento del tenant è possibile usare la **Configurazione guidata della co-gestione** nella console di Configuration Manager, ma non è necessario abilitare la co-gestione.

Se si prevede di abilitare la co-gestione, prima di continuare è consigliabile acquisire familiarità con questa funzionalità, con i relativi prerequisiti e con il modo in cui gestire i carichi di lavoro. Vedere [Informazioni sulla co-gestione](../../configmgr/comanage/overview.md) nella documentazione di Configuration Manager.

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.
2. Nella barra multifunzione fare clic su **Configura la co-gestione** per aprire la procedura guidata.
3. Nella pagina **Onboarding del tenant** selezionare **AzurePublicCloud** per l'ambiente in uso. Il cloud di Azure per enti pubblici non è supportato.
   1. Fare clic su **Accedi**. Usare l'account di *amministratore globale* per accedere.

   2. Nella pagina **Onboarding del tenant** verificare che l'opzione **Upload to Microsoft Endpoint Manager admin center** (Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager) sia selezionata.

   3. Rimuovere il segno di spunta da **Abilita la registrazione automatica dei client per la co-gestione**.

      Quando questa opzione è selezionata, la procedura guidata visualizza altre pagine per completare la configurazione della co-gestione. Per altre informazioni, vedere [Abilitare la co-gestione](../../configmgr/comanage/how-to-enable.md) nella documentazione di Configuration Manager.

     ![Configurare il collegamento del tenant](./media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Fare clic su **Avanti** e quindi su **Sì** per accettare la notifica **Crea un'applicazione di AAD**. Questa azione esegue il provisioning di un'entità servizio e crea una registrazione dell'applicazione Azure AD per semplificare la sincronizzazione delle raccolte nell'interfaccia di amministrazione di Microsoft Endpoint Manager.

5. Nella pagina **Configure upload** (Configura caricamento) è possibile configurare le raccolte da sincronizzare. È possibile limitare la configurazione a una o più raccolte di dispositivi o usare l'impostazione di caricamento dei dispositivi consigliata per **All my devices managed by Microsoft Endpoint Configuration Manager** (Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager).

6. Fare clic su **Riepilogo** per verificare la selezione e quindi su **Avanti**.

7. Al termine della procedura guidata, fare clic su **Chiudi**.

   Il collegamento del tenant è ora configurato e le raccolte selezionate vengono sincronizzate con l'interfaccia di amministrazione di Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Abilitare il collegamento del tenant quando si usa la co-gestione

1. Nella console di amministrazione di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-gestione**.

2. Fare clic con il pulsante destro del mouse sulle impostazioni di co-gestione e selezionare **Proprietà**.

3. Nella scheda **Configure upload** (Configura caricamento) selezionare **Carica nell'interfaccia di amministrazione di Microsoft Endpoint Manager**. Fare clic su **Apply**.
   - L'impostazione predefinita per il caricamento del dispositivo è **Tutti i dispositivi personali gestiti da Microsoft Endpoint Configuration Manager**. È anche possibile scegliere di limitare la configurazione a una o più raccolte di dispositivi.

     ![Visualizzare la scheda proprietà di co-gestione](./media/endpoint-security-edr-policy/configure-upload.png)

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

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Attività 4: abilitare le raccolte per Microsoft Defender ATP

Dopo aver configurato le raccolte per la sincronizzazione con l'interfaccia di amministrazione di Microsoft Endpoint Manager, è comunque necessario abilitare tali raccolte in modo che siano idonee per l'onboarding e i criteri di Microsoft Defender ATP.  Per eseguire questa operazione è necessario modificare le proprietà di ogni raccolta nella console di Configuration Manager.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Abilitare le raccolte per l'uso con Advanced Threat Protection

1. Da una console di Configuration Manager connessa al sito di livello superiore, fare clic con il pulsante destro del mouse su una raccolta di dispositivi sincronizzata con l'interfaccia di amministrazione di Microsoft Endpoint Manager e scegliere **Proprietà**.

2. Nella scheda **Sincronizzazione cloud** abilitare l'opzione **Make this collection available to assign Microsoft Defender ATP policies in Intune** (Rendi disponibile questa raccolta per assegnare i criteri di Microsoft Defender ATP in Intune).

   - Non è possibile selezionare questa opzione se la gerarchia di Configuration Manager non è collegata al tenant.
  
   ![Configurare la sincronizzazione cloud](./media/endpoint-security-edr-policy/cloud-sync.png)

3. Selezionare **OK** per salvare la configurazione.

   I dispositivi in questa raccolta possono ora ricevere i criteri di Microsoft Defender ATP.

## <a name="create-and-deploy-edr-policies"></a>Creare e distribuire i criteri EDR

Quando la sottoscrizione di Microsoft Defender ATP è integrata con Intune, è possibile creare e distribuire i criteri EDR. Esistono due tipi diversi di criteri EDR che è possibile creare. Un tipo di criterio è per i dispositivi gestiti con Intune tramite MDM. Il secondo tipo è per i dispositivi gestiti con Configuration Manager.

È possibile scegliere il tipo di criterio quando si sceglie la piattaforma per la creazione di un nuovo criterio EDR.

Prima di poter distribuire i criteri ai dispositivi gestiti da Configuration Manager, [configurare Configuration Manager per il supporto dei criteri EDR](#set-up-configuration-manager-to-support-edr-policy) dall'interfaccia di amministrazione di Microsoft Endpoint Manager.

### <a name="create-edr-policies"></a>Creare i criteri EDR

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint security** (Sicurezza degli endpoint)  > **Rilevamento di endpoint e risposta** > **Crea criterio**.

3. Selezionare la piattaforma e il profilo per il criterio. Le informazioni seguenti identificano le opzioni:

   - Intune: distribuisce i criteri ai dispositivi nei gruppi di Azure AD. Quando si crea il criterio, selezionare:
     - Piattaforma: **Windows 10 e versioni successive**
     - Profilo: **Rilevamento di endpoint e risposta (MDM)**

   - Configuration Manager: distribuisce i criteri ai dispositivi nelle raccolte di Configuration Manager. Quando si crea il criterio, selezionare:
     - Piattaforma: **Windows 10 e Windows Server**
     - Profilo: **Rilevamento di endpoint e risposta (ConfigMgr) (anteprima)**

4. Selezionare **Crea**.

5. Nella pagina **Informazioni di base** immettere un nome e una descrizione per il profilo, quindi scegliere **Avanti**.

6. Nella pagina **Impostazioni di configurazione** configurare le impostazioni da gestire con questo profilo. Il pacchetto di onboarding viene incluso automaticamente e non è un elemento che è possibile configurare.

   Al termine della configurazione delle impostazioni, selezionare **Avanti**.

7. *Questo passaggio si applica solo al profilo **rilevamento di endpoint e risposta***:  

   Nella pagina **Tag di ambito** scegliere **Selezionare i tag di ambito** per aprire il riquadro *Seleziona tag* per assegnare tag di ambito al profilo.
  
   Selezionare **Avanti** per continuare.

8. Nella pagina **Assegnazioni** selezionare i gruppi o le raccolte che riceveranno questo criterio. La scelta dipende dalla piattaforma e dal profilo selezionati:

   - Per Intune, è possibile selezionare i gruppi da Azure AD.
   - Per Configuration Manager, è possibile selezionare le raccolte sincronizzate nell'interfaccia di amministrazione di Microsoft Endpoint Manager e abilitate per i criteri di Microsoft Defender ATP da Configuration Manager.

   È possibile scegliere di non assegnare gruppi o raccolte al momento e modificare il criterio per aggiungere un'assegnazione successivamente.

   Quando si è pronti per continuare, selezionare **Avanti**.

9. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**.

   Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

## <a name="edr-policy-reports"></a>Report sui criteri EDR

È possibile visualizzare i dettagli sui criteri EDR distribuiti nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Per visualizzarli, passare a **Endpoint Security** (Sicurezza degli endpoint)  > **Endpoint deployment and response** (Distribuzione di endpoint e risposta) e selezionare un criterio di cui si vuole visualizzare i dettagli di conformità:

- Per i criteri destinati alla piattaforma **Windows 10 e versioni successive** (Intune), verrà visualizzata una panoramica della conformità al criterio. È anche possibile selezionare il grafico per visualizzare un elenco di dispositivi che hanno ricevuto il criterio ed eseguire il drill-in dei singoli dispositivi per altri dettagli.

- Per i criteri destinati alla piattaforma **Windows 10 e Windows Server** (Configuration Manager), verrà visualizzata una panoramica della conformità al criterio ma non sarà possibile eseguire il drill-in per visualizzare dettagli aggiuntivi. La visualizzazione è limitata perché l'interfaccia di amministrazione riceve dettagli di stato limitati da Configuration Manager, che consente di gestire la distribuzione del criterio ai dispositivi di Configuration Manager.

[Visualizzare le impostazioni](../protect/endpoint-security-edr-profile-settings.md) che è possibile configurare sia per le piattaforme che per i profili.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
- Altre informazioni su [Rilevamento di endpoint e risposta](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) sono disponibili nella documentazione di Microsoft Defender ATP.
