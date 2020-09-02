---
title: Gestire le impostazioni per il rilevamento di endpoint e risposta con i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Configurare e distribuire criteri per i dispositivi gestiti con i criteri per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Microsoft Endpoint Manager.
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
ms.openlocfilehash: ff880b564562b3e6d67dc852f97ef7a9f5d6b814
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915042"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Criteri per il rilevamento di endpoint e risposta per la sicurezza degli endpoint in Intune

Quando si integra Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Intune, è possibile usare i criteri di sicurezza degli endpoint per il rilevamento di endpoint e risposta (EDR) per gestire le impostazioni EDR ed eseguire l'onboarding di dispositivi in Microsoft Defender ATP.

Le funzionalità di rilevamento di endpoint e riposta di Microsoft Defender ATP offrono rilevamenti avanzati degli attacchi quasi in tempo reale e con la possibilità di intervenire. Gli analisti della sicurezza possono impostare la priorità degli avvisi in modo efficace, ottenere la visibilità dell'ambito completo di una violazione e intraprendere azioni di risposta per correggere le minacce.

I criteri EDR includono profili specifici della piattaforma per gestire le impostazioni per EDR. I profili includono automaticamente un *pacchetto di onboarding* per Microsoft Defender ATP. I pacchetti di onboarding rappresentano il modo in cui i dispositivi sono configurati per funzionare con Microsoft Defender ATP. Dopo l'onboarding di un dispositivo, è possibile iniziare a usare i dati sulle minacce da quel dispositivo.

I criteri EDR vengono distribuiti a gruppi di dispositivi in Azure Active Directory (Azure AD) gestiti con Intune e a raccolte di dispositivi locali gestiti con Configuration Manager, inclusi i server Windows. I criteri EDR per percorsi di gestione diversi richiedono pacchetti di onboarding diversi. È quindi possibile creare criteri EDR separati per i diversi tipi di dispositivi gestiti.

I criteri di sicurezza degli endpoint per EDR sono disponibili in *Gestione* nel nodo **Endpoint security** (Sicurezza degli endpoint) dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Visualizzare le [impostazioni per i profili di rilevamento di endpoint e risposta](endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Prerequisiti per i criteri EDR

**Generale**:

- **Tenant per Microsoft Defender Advanced Threat Protection** - È necessario integrare il tenant di Microsoft Defender ATP con il tenant di Microsoft Endpoint Manager (sottoscrizione a Intune) prima di poter creare criteri EDR. Vedere [Usare Microsoft Defender ATP](advanced-threat-protection.md) nella documentazione di Intune.

**Supporto per i client di Configuration Manager**:

- **Configurare il collegamento al tenant per i dispositivi di Configuration Manager**: per supportare la distribuzione dei criteri EDR nei dispositivi gestiti da Configuration Manager, configurare il *collegamento al tenant*. A questo scopo, è necessario configurare le raccolte di dispositivi di Configuration Manager in modo da supportare i criteri di sicurezza degli endpoint di Intune.

  Per configurare il collegamento al tenant, inclusa la sincronizzazione delle raccolte di Configuration Manager con l'interfaccia di amministrazione di Microsoft Endpoint Manager, e consentirne il funzionamento con i criteri di sicurezza degli endpoint, vedere [Configurare il collegamento al tenant per supportare i criteri di Endpoint Protection](../protect/tenant-attach-intune.md).

## <a name="edr-profiles"></a>Profili EDR

[Visualizzare le impostazioni](endpoint-security-edr-profile-settings.md) che è possibile configurare per le piattaforme e i profili seguenti.

**Intune**: per i dispositivi gestiti con Intune sono supportati gli elementi seguenti:

- Piattaforma: **Windows 10 e versioni successive**: Intune distribuisce i criteri ai dispositivi nei gruppi di Azure AD.
- Profilo: **Rilevamento di endpoint e risposta (MDM)**

**Configuration Manager** - Per i dispositivi gestiti con Configuration Manager sono supportati gli elementi seguenti:

- Piattaforma: **Windows 10 e Windows Server (ConfigMgr)** - Configuration Manager distribuisce i criteri ai dispositivi nelle raccolte di Configuration Manager.
- Profilo: **Rilevamento di endpoint e risposta (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Configurare Configuration Manager per il supporto dei criteri EDR

Prima di poter distribuire i criteri EDR per i dispositivi Configuration Manager, è necessario completare le configurazioni descritte nelle sezioni seguenti.

Queste configurazioni vengono eseguite nella console di Configuration Manager e nella distribuzione di Configuration Manager. Se non si ha familiarità con Configuration Manager, è possibile collaborare con un amministratore di Configuration Manager per completare queste attività.  

Nelle sezioni seguenti vengono descritte le attività necessarie:

1. [Installare l'aggiornamento per Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Abilitare il collegamento del tenant](#task-2-configure-tenant-attach-and-synchronize-collections)  

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

Per i dispositivi gestiti con Intune sono supportati gli elementi seguenti:

- Piattaforma: **Windows 10 e versioni successive**: Intune distribuisce i criteri ai dispositivi nei gruppi di Azure AD.
  - Profilo: **Rilevamento di endpoint e risposta (MDM)**

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Dispositivi gestiti da Configuration Manager *(in anteprima)*

Per i dispositivi gestiti con Configuration Manager sono supportati gli elementi seguenti tramite lo scenario di *collegamento al tenant*:

- Piattaforma: **Windows 10 e Windows Server (ConfigMgr)** - Configuration Manager distribuisce i criteri ai dispositivi nelle raccolte di Configuration Manager.
  - Profilo: **Rilevamento di endpoint e risposta (ConfigMgr) (anteprima)**

## <a name="create-and-deploy-edr-policies"></a>Creare e distribuire i criteri EDR

Quando la sottoscrizione di Microsoft Defender ATP è integrata con Intune, è possibile creare e distribuire i criteri EDR. Esistono due tipi diversi di criteri EDR che è possibile creare. Un tipo di criterio è per i dispositivi gestiti con Intune tramite MDM. Il secondo tipo è per i dispositivi gestiti con Configuration Manager.

Scegliere il tipo di criterio da creare durante la configurazione di un nuovo criterio EDR, scegliendo una piattaforma per il criterio.

Prima di poter distribuire i criteri ai dispositivi gestiti da Configuration Manager, configurare Configuration Manager per il supporto dei criteri EDR dall'interfaccia di amministrazione di Microsoft Endpoint Manager. Vedere [Configurare il collegamento al tenant per supportare i criteri di Endpoint Protection](../protect/tenant-attach-intune.md).


### <a name="create-edr-policies"></a>Creare i criteri EDR

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint security** (Sicurezza degli endpoint)  > **Rilevamento di endpoint e risposta** > **Crea criterio**.

3. Selezionare la piattaforma e il profilo per il criterio. Le informazioni seguenti identificano le opzioni:

   - Intune: distribuisce i criteri ai dispositivi nei gruppi di Azure AD. Quando si crea il criterio, selezionare:
     - Piattaforma: **Windows 10 e versioni successive**
     - Profilo: **Rilevamento di endpoint e risposta (MDM)**

   - Configuration Manager: distribuisce i criteri ai dispositivi nelle raccolte di Configuration Manager. Quando si crea il criterio, selezionare:
     - Piattaforma: **Windows 10 e Windows Server (ConfigMgr)**
     - Profilo: **Rilevamento di endpoint e risposta (ConfigMgr)**

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

  Il grafico **Dispositivi con sensore di ATP** mostra solo i dispositivi che completano l'onboarding in Microsoft Defender ATP tramite l'uso del profilo **Windows 10 e versioni successive**. Per assicurare che sia disponibile una rappresentazione completa dei dispositivi in questo grafico, distribuire il profilo di onboarding in tutti i dispositivi. I dispositivi che completano l'onboarding in Microsoft Defender ATP tramite metodi esterni, ad esempio Criteri di gruppo o PowerShell, vengono conteggiati come **Dispositivi senza sensore di ATP**.

- Per i criteri destinati alla piattaforma **Windows 10 e Windows Server (ConfigMgr)** , verrà visualizzata una panoramica della conformità al criterio ma non sarà possibile eseguire il drill-in per accedere a dettagli aggiuntivi. La visualizzazione è limitata perché l'interfaccia di amministrazione riceve dettagli di stato limitati da Configuration Manager, che consente di gestire la distribuzione del criterio ai dispositivi di Configuration Manager.

[Visualizzare le impostazioni](endpoint-security-edr-profile-settings.md) che è possibile configurare sia per le piattaforme che per i profili.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare i criteri di sicurezza degli endpoint](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Altre informazioni su [Rilevamento di endpoint e risposta](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) sono disponibili nella documentazione di Microsoft Defender ATP.