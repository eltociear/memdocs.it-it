---
title: Preparazione aggiornamenti
titleSuffix: Configuration Manager
description: Integrare Preparazione aggiornamenti con Configuration Manager per accedere ai dati relativi alla compatibilità con l'aggiornamento a Windows 10 e specificare come destinazione i dispositivi da aggiornare o correggere.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 6d9bd7aabb36895160ba8aa740c28155105e196a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693404"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integrare Preparazione aggiornamenti con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> Il servizio Windows Analytics è stato ritirato il 31 gennaio 2020. Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics è l'evoluzione di Windows Analytics. Per altre informazioni, vedere [Che cos'è Desktop Analytics](../../../desktop-analytics/overview.md).

Se il sito di Configuration Manager aveva una connessione a Preparazione aggiornamenti, è necessario rimuoverla e riconfigurare i client.

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a> Rimuovere la connessione a Preparazione aggiornamenti

1. Aprire la console di Configuration Manager come utente con il ruolo **Amministratore completo**.

1. Accedere all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e quindi selezionare il nodo **Servizi di Azure**.

1. Eliminare il servizio Windows Analytics.

## <a name="reconfigure-clients"></a>Riconfigurare i client

### <a name="unenroll-devices"></a>Annullare la registrazione dei dispositivi

Esaminare prima di tutto le impostazioni predefinite del sito o di qualsiasi dispositivo client personalizzato nel gruppo di **Windows Analytics**. Ad esempio, disabilitare l'impostazione seguente: **Gestire le impostazioni di telemetria di Windows con Configuration Manager**.

> [!IMPORTANT]
> Se si prevede di usare Desktop Analytics, questo strumento configura le impostazioni dei dati di diagnostica di Windows nei client. Usare la connessione guidata dei servizi di Azure per configurare queste impostazioni per l'uso con Desktop Analytics. Per altre informazioni, vedere [Come connettere Configuration Manager a Desktop Analytics](../../../desktop-analytics/connect-configmgr.md).

Nei dispositivi registrati rimuovere il valore di CommercialID dalle chiavi del Registro di sistema di Windows seguenti:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configurazione dei dati di diagnostica di Windows

Se non si vuole che i dispositivi continuino a inviare dati di diagnostica:

- In Windows 10: impostare il livello di dati di diagnostica su **Sicurezza**
- In Windows 7 SP1 o 8.1: disabilitare **Commercial Data Opt-in Key** (Chiave consenso esplicito per i dati commerciali)

Impostare questi valori usando uno dei metodi seguenti:

- Criteri di gruppo in **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Raccolta dati e versioni di anteprima**
- Gestione di dispositivi mobili (MDM), come ad esempio [Microsoft Intune](/intune/device-restrictions-windows-10#reporting-and-telemetry)

Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione).

> [!NOTE]  
> Quando si applicano queste modifiche, i dispositivi interrompono immediatamente l'invio dei dati di diagnostica. Potrebbero essere necessarie 24-48 ore perché Microsoft interrompa l'elaborazione dei dati analitici per l'area di lavoro. Microsoft elimina i dati dai servizi cloud entro un massimo di 30 giorni.

<!--
Upgrade Readiness is a part of [Windows Analytics](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)