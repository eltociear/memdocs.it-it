---
title: Come chiudere l'account
titleSuffix: Configuration Manager
description: Come rimuovere Desktop Analytics dall'account Azure
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e24c2ee19093dd12af6e87280a31851a1f593782
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268471"
---
# <a name="how-to-close-your-account"></a>Come chiudere l'account

Se si configura Desktop Analytics nell'ambiente in uso e si decide in seguito di rimuoverlo, usare il processo seguente per chiudere l'account.

## <a name="prerequisites"></a>Prerequisiti

Solo un **amministratore globale** può chiudere o riattivare l'account nel portale di Azure.

## <a name="process-to-offboard"></a>Processo per eseguire l'offboarding

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics) in Gestione dispositivi Microsoft 365 come utente con il ruolo **Amministratore globale**.

1. Nel menu **Impostazioni globali** selezionare **Servizi connessi**. Nella sezione relativa alla registrazione dei dispositivi selezionare l'opzione **Offboard** (Esegui offboarding).

1. Se si decide di continuare, l'account viene chiuso.

> [!Important]
> Continuare con il resto di questo articolo dopo 90 giorni, oppure se non si vuole riattivare l'account.
>
> Se si vuole chiudere completamente l'account senza attendere 90 giorni, [reimpostare](account-reset.md) prima l'account.

## <a name="reactivate"></a>Riattivare l'account

Per i 90 giorni successivi per tutti gli amministratori dell'organizzazione che accedono al portale di Desktop Analytics verrà visualizzato un avviso che comunica che si è scelto di eseguire l'offboarding.

Un amministratore globale può riattivare l'account entro 90 giorni. Per ripristinare Desktop Analytics per l'organizzazione, selezionare l'opzione **Torna nella pagina**.

## <a name="delete-the-solution"></a>Eliminare la soluzione

> [!Warning]
> Continuare con il resto di questo articolo dopo 90 giorni, oppure se non si vuole riattivare l'account. Se si eliminano e disconnettono i componenti seguenti, non provare a eseguire la riattivazione.

1. Accedere al [portale di Azure](https://portal.azure.com) come utente con il ruolo **Amministratore globale**.

1. Cercare in **Tutte le risorse** il nome dell'area di lavoro di Desktop Analytics. Si tratta del nome creato durante l'iscrizione al servizio.

1. Eliminare `Microsoft365Analytics(YourWorkspaceName)` del tipo **Soluzione**.

I dati di Desktop Analytics diventano obsoleti in base ai criteri di conservazione dei dati per l'area di lavoro. È possibile continuare a usare qualsiasi altra soluzione nella stessa area di lavoro.

> [!Important]  
> Se si usa l'area di lavoro Log Analytics con altre soluzioni, non eliminare l'area di lavoro.

## <a name="remove-user-and-app-access"></a>Rimuovere l'accesso di utenti e app

1. Accedere al [portale di Azure](https://portal.azure.com) come utente con il ruolo **Amministratore globale**. Passare a **Azure Active Directory**.

1. In **Ruoli e amministratori** cercare il ruolo **Amministratore Desktop Analytics** e rimuoverne i membri.

1. In **Gruppi** rimuovere i membri dei gruppi seguenti:

    - **M365 Analytics Client Admins (Log Analytics Owners)**
    - **M365 Analytics Client Admins (Log Analytics Contributors)**

1. In **Applicazioni aziendali** eliminare o revocare le autorizzazioni di accesso alle app seguenti:

    - `MaLogAnalyticsReader`

    - L'app ConfigMgr. Per trovare il nome dell'app, passare alla console di Configuration Manager. Nell'area di lavoro **Amministrazione** espandere **Servizi cloud** e quindi selezionare il nodo **Servizi di Azure**. Aprire le proprietà del servizio **Desktop Analytics** e passare alla scheda **Applicazioni**. L'**App Web** è questa app di Azure.

        > [!Important]  
        > Prima di apportare modifiche all'app in Azure AD, assicurarsi che non venga riutilizzata in un altro servizio in Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Disconnettere Configuration Manager

1. Aprire la console di Configuration Manager come utente con il ruolo **Amministratore completo**.

1. Accedere all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e quindi selezionare il nodo **Servizi di Azure**.

1. Eliminare il servizio Desktop Analytics.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Eliminare le raccolte per le distribuzioni pilota e di produzione

1. Nella console di Configuration Manager selezionare **Raccolte dispositivi** nell'area di lavoro **Asset e conformità**.

1. Eliminare tutte le raccolte che non vengono più usate. Per impostazione predefinita, le raccolte si trovano nella cartella **Piani di distribuzione**.  

## <a name="reconfigure-clients"></a>Riconfigurare i client

### <a name="unenroll-devices"></a>Annullare la registrazione dei dispositivi

Nei dispositivi registrati rimuovere il valore di CommercialID dalle chiavi del Registro di sistema di Windows seguenti:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configurazione dei dati di diagnostica di Windows

Se non si vuole che i dispositivi continuino a inviare dati di diagnostica:

- In Windows 10: impostare il livello di dati di diagnostica su **Sicurezza**
- In Windows 7 SP1 o 8.1: disabilitare **Commercial Data Opt-in Key** (Chiave consenso esplicito per i dati commerciali)

Impostare questi valori usando uno dei metodi seguenti:

- Criteri di gruppo in **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Raccolta dati e versioni di anteprima**
- Gestione di dispositivi mobili (MDM), come ad esempio [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione).

> [!NOTE]  
> Quando si applicano queste modifiche, i dispositivi interrompono immediatamente l'invio dei dati di diagnostica. Potrebbero essere necessarie 24-48 ore perché Microsoft interrompa l'elaborazione dei dati analitici per l'area di lavoro. Microsoft elimina i dati dai servizi cloud entro un massimo di 30 giorni.
