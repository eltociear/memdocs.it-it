---
title: Portale del supporto tecnico per la risoluzione dei problemi
titleSuffix: Microsoft Intune
description: Il personale del supporto tecnico usa questo portale per risolvere i problemi tecnici degli utenti.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/11/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: sumitp
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ec804aa200e35391c5b283d6e26ba87002e271f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79359027"
---
# <a name="use-the-troubleshooting-portal-to-help-users-at-your-company"></a>Usare il portale per la risoluzione dei problemi per offrire assistenza agli utenti aziendali

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Il portale di risoluzione dei problemi consente agli operatori del supporto tecnico e agli amministratori di Intune di visualizzare le informazioni degli utenti per rispondere alle richieste di assistenza degli utenti. Le organizzazioni che dispongono di help desk possono assegnare il ruolo di **operatore di help desk** a un gruppo di utenti. I membri del ruolo operatore di help desk possono usare il riquadro **Risoluzione dei problemi**.

Il riquadro **Risoluzione dei problemi** visualizza anche i problemi di registrazione dell'utente. Informazioni dettagliate sul problema e i passaggi suggeriti per la correzione possono essere utili ad amministratori e operatori di help desk per la risoluzione dei problemi. Alcuni problemi di registrazione non vengono rilevati ed è possibile che per alcuni errori non siano disponibili suggerimenti per la correzione.

Per istruzioni sull'aggiunta di un ruolo operatore di help desk, vedere [Controllo degli accessi in base al ruolo (RBAC) con Intune](role-based-access-control.md).

Quando un utente contatta l'help desk per un problema tecnico di Intune, l'operatore di help desk immette il nome dell'utente. Intune visualizza dati utili che consentono di risolvere molti problemi di livello 1, tra cui:

- Stato utente
- Assignments
- Problemi di conformità
- Un dispositivo che non risponde
- Un dispositivo che non riceve le impostazioni VPN o Wi-Fi
- Un errore di installazione dell'app

## <a name="to-review-troubleshooting-details"></a>Per esaminare le informazioni sulla risoluzione dei problemi

Nel riquadro Risoluzione dei problemi scegliere **Selezionare l'utente** per visualizzare le informazioni relative all'utente. Le informazioni utente sono utili per definire lo stato corrente degli utenti e dei loro dispositivi.  

1. Accedere a [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. Nel riquadro **Intune** scegliere **Risoluzione dei problemi**.
4. Fare clic su **Seleziona** per selezionare un utente per risolvere i problemi.
5. Selezionare un utente digitando il nome o l'indirizzo di posta elettronica. Fare clic su **Seleziona**. Le informazioni di risoluzione dei problemi per l'utente vengono visualizzate nel riquadro Risoluzione dei problemi. La tabella seguente descrive tali informazioni.

> [!Note]  
> È anche possibile accedere al riquadro **Risoluzione dei problemi** digitando nel browser l'indirizzo seguente: [https://aka.ms/intunetroubleshooting](https://aka.ms/intunetroubleshooting).

## <a name="areas-of-troubleshooting-dashboard"></a>Aree del dashboard Risoluzione dei problemi

È possibile usare il riquadro **Risoluzione dei problemi** per esaminare le informazioni dell'utente.

![Dashboard per la risoluzione dei problemi, con aree numerate descritte dalla tabella seguente](./media/help-desk-operators/troubleshooting-dash.png)

| Area | Name | Descrizione |
| ---  | ---  | ---         |
| 1.   | Stato dell'account  | Mostra lo stato del tenant di Intune corrente come **Attivo** o **Inattivo**.       |
| 2.   | Selezione utente  | Nome dell'utente attualmente selezionato. Fare clic su **Cambia utente** per scegliere un nuovo utente.       |
| 3.   | Stato utente  | Visualizza lo stato della licenza Intune dell'utente, il numero di dispositivi, la conformità di ciascun dispositivo, il numero di app e la conformità delle app.       |
| 4.   | Informazioni sull'utente  | Usare l'elenco per selezionare i dettagli da esaminare nel riquadro. <br>È possibile selezionare: <ul><li>App client<li>Criteri di conformità<li> Criteri di configurazione<li>Criteri di protezione delle app <li>Restrizioni di registrazione</ul>      |
| 5.   | Appartenenza a gruppi  | Mostra i gruppi correnti di cui l'utente selezionato è membro.       |

<!-- this section needs to be updated

## Client apps reference

The apps that are running devices
- managed by Intune and Azure Active Directory (AD) 
- owned by users managed by Intune and Azure Active Directory (AD).

### Properties

The properties of client apps.

| Property      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name          | The name of the application.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| OS            | The operating system installed on the device.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Type          | You can choose an assignment type for each app.  <br> **Available** - Users install the app from the Company Portal app or website.  <br> **Not Applicable** - The app is not installed or shown in the Company Portal. <br> **Uninstall** - The app is uninstalled from devices in the selected groups.  <br> **Available with or without enrollment** - Assign this app to groups of users whose devices are not enrolled with Intune. |
| Last Modified | The name of the type of device.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Description                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device name        | The name of the type of device.                                                                                                     |
| Managed by         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| App install | Denotes whether an app install failure or success has occurred on the individual device. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last check-in      | The name of the type of device.                                                                                                     |

### App protection status

An app protection policy is available to mobile apps that integrate with Enterprise Mobility Solution (EMS) technologies. These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

| Property    | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| Status      | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| App name    | The name of the application                                                           |
| Device name | The name of the type of device.                                                       |
| Device type | The name of the type of device.                                                       |
| Policies    | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| Last sync   | The timestamp of the last time the device synchronized with Intune.                   |

## App protection policies reference

An app protection policy is available to mobile apps that integrate with EMS technologies.These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

### Properties

The table summarizes app protection policies status for devices managed by Intune.

| Property    | Description                                                                                                                                |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Name        | The name of the application.                                                                                                        |
| Deployed    | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Platform    | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Enrollment  | The name of the type of device.                                                                                                     |
| Last Update | The timestamp the policy was modified.                                                                                              |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Text                                                                                                                                |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device Name        | The name of the type of device.                                                                                                     |
| Managed By         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last Check in      | The name of the type of device.                                                                                                     |

## Compliance policies reference

Makes sure that the devices used to access company apps and data, comply with certain rules like using a PIN to access the device, and encryption of data stored on the device.

### Properties

The properties of the compliance policies.

| Property      | Description                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Assignment    | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Name          | The name of the application.                                                                                                        |
| OS            | The operating system installed on the device.                                                                                       |
| Policy Type   | The type of device ownership (**Company**, **Personal**, and **Unknown**).                                               |
| Last Modified | The name of the type of device.                                                                                                     |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Description                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device name        | The name of the type of device.                                                                                                     |
| Managed by         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, and **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last check-in      | The name of the type of device.                                                                                                     |

### App protection policies

An app protection policy is available to mobile apps that integrate with EMS technologies. These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

| Property    | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| Status      | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| App name    | The name of the application                                                           |
| Device name | The name of the type of device.                                                       |
| Device type | The name of the type of device.                                                       |
| Policies    | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| Last sync   | The timestamp of the last time the device synchronized with Intune.                   |

## Configuration policies reference

An app configuration policy is available to mobile apps with vendor-specific configuration. 

### Properties

The properties of the configuration policies.

| Property      | Description                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Assignment    | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Name          | The name of the application.                                                                                                        |
| OS            | The operating system installed on the device.                                                                                       |
| Policy Type   | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Last Modified | The name of the type of device.                                                                                                     |

### Devices

Devices managed by Intune or by users managed by Intune or Azure AD.

| Property           | Description                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Device name        | The name of the type of device.                                                                                                     |
| Managed by         | The timestamp the policy was modified.                                                                                              |
| Azure AD join type | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| Ownership          | The type of device ownership (**Company**, **Personal**, or **Unknown**).                                               |
| Intune compliant   | The name of the type of device.                                                                                                     |
| Azure AD compliant | The status of each of the users' app protection apps. The possible statuses for the apps are **Checked in** and **Not checked in**. |
| OS                 | The operating system installed on the device.                                                                                       |
| OS version         | The Operating System version number of the device.                                                                                  |
| Last check-in      | The name of the type of device.                                                                                                     |


### App protection policies

An app protection policy is available to mobile apps that integrate with EMS technologies. These policies give a baseline of protection for your corporate data when it is downloaded to mobile apps, including the Office mobile apps. 

| Property    | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| Status      | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| App name    | The name of the application                                                           |
| Device name | The name of the type of device.                                                       |
| Device type | The name of the type of device.                                                       |
| Policies    | The type of device ownership (**Company**, **Personal**, or **Unknown**). |
| Last sync   | The timestamp of the last time the device synchronized with Intune.                   |

-->

## <a name="enrollment-failure-reference"></a>Riferimento per gli errori di registrazione

Nella tabella Errori di registrazione sono elencati i tentativi di registrazione non riusciti. Un dispositivo riportato nella tabella seguente potrebbe essere stato registrato successivamente durante un altro tentativo. Alcuni tentativi non riusciti potrebbero non essere presenti. Le informazioni di mitigazione non sono disponibili per tutti gli errori.

| Colonna della tabella | Descrizione |
|-------------|----------|
| Avvio della registrazione | L'ora in cui l'utente ha iniziato la registrazione. |
| Sistema operativo | Sistema operativo del dispositivo. |
| Versione sistema operativo | Versione del sistema operativo del dispositivo. |
| Errore | Motivo dell'errore. |

### <a name="failure-details"></a>Dettagli errore

Quando si sceglie la riga di un errore, vengono forniti ulteriori dettagli.

| Sezione | Descrizione |
|-------------|----------|
| Dettagli errore | Una spiegazione più dettagliata dell'errore. |
| Possibili soluzioni | Passaggi consigliati per risolvere l'errore. Alcuni errori potrebbero non avere soluzione. |
| Risorse (facoltative) | Collegamenti per altre informazioni o aree del portale in cui intervenire. |

### <a name="enrollment-errors"></a>Errori di registrazione

| Errore | Dettagli |
|-------------|----------|
| Timeout o errore di iOS/iPadOS | Si è verificato un timeout tra il dispositivo e Intune perché l'utente ha impiegato troppo tempo a completare la registrazione. |
| L'utente non è stato trovato o non ha la licenza | L'utente non ha una licenza o è stato rimosso dal servizio. |
| Il dispositivo è già registrato | Qualcuno ha tentato di registrare un dispositivo usando il Portale aziendale su un dispositivo che risulta ancora registrato da un altro utente. |
| Nessun onboarding in Intune | È stata tentata una registrazione ma l'autorità di gestione dei dispositivi mobili (MDM) di Intune non era configurata. |
| Enrollment authorization failed (Autorizzazione di registrazione non riuscita) | È stata tentata una registrazione utilizzando una versione precedente del portale aziendale. |
| Dispositivo non supportato | Il dispositivo non soddisfa i requisiti minimi per la registrazione in Intune. |
| Le restrizioni della registrazione non sono state rispettate | Questa registrazione è stata bloccata a causa di una restrizione di registrazione configurata dall'amministratore. |
| Versione del dispositivo troppo bassa | L'amministratore ha configurato una restrizione a livello di registrazione che richiede una versione successiva del dispositivo. |
| Versione del dispositivo troppo alta | L'amministratore ha configurato una restrizione a livello di registrazione che richiede una versione precedente del dispositivo. |
| Il dispositivo non può essere registrato come dispositivo personale | L'amministratore ha configurato una restrizione a livello di registrazione che blocca le iscrizioni personali e il dispositivo in errore non è configurato come dispositivo aziendale. |
| Piattaforma del dispositivo bloccata | L'amministratore ha configurato una restrizione a livello di registrazione che blocca la piattaforma del dispositivo. |
| Token di massa scaduto | Il token di massa nel pacchetto di provisioning è scaduto. |
| Non sono stati trovati dettagli o dispositivo di AutoPilot | Quando si tenta di eseguire la registrazione, il dispositivo di Autopilot non viene rilevato. |
| Profilo di Autopilot non trovato o non assegnato | Il dispositivo non ha un profilo di Autopilot attivo. |
| Metodo di registrazione di Autopilot imprevisto | Il dispositivo ha cercato di registrarsi con un metodo non consentito. |
| Dispositivo di AutoPilot rimosso | Il dispositivo che ha eseguito un tentativo di registrazione è stato rimosso da Autopilot per questo account. |
| Numero massimo dispositivi raggiunto | Questa registrazione è stata bloccata a causa di una restrizione del limite di dispositivi configurata dall'amministratore. |
| Onboarding di Apple | La registrazione di tutti i dispositivi iOS/iPadOS è stata bloccata a causa di un certificato per le notifiche push MDM Apple mancante o scaduto in Intune. |
| Il dispositivo non è preregistrato | Il dispositivo non è stato preregistrato come aziendale e tutte le registrazioni personali sono state bloccate da un amministratore. |
| La funzionalità non è supportata | L'utente ha probabilmente tentato di eseguire la registrazione con un metodo non compatibile con la configurazione di Intune. |

## <a name="collect-available-data-from-mobile-device"></a>Raccogliere i dati disponibili dal dispositivo mobile

Usare le risorse seguenti per raccogliere i dati del dispositivo durante la risoluzione dei problemi dei dispositivi dell'utente:
- [Inviare gli errori di registrazione iOS/iPadOS all'amministratore IT](../user-help/send-errors-to-your-it-admin-ios.md)
- [Aiutare il supporto tecnico dell'azienda a risolvere i problemi dei dispositivi con la registrazione dettagliata](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md)
- [Inviare i log di Android al supporto tecnico dell'azienda usando un cavo USB](../user-help/send-logs-to-your-it-admin-using-cable-android.md)
- [Send Android diagnostic data logs to your IT administrator using email (Inviare i log dei dati Android di diagnostica all'amministratore IT tramite posta elettronica)](../user-help/send-logs-to-your-it-admin-by-email-android.md)
- [Send Android enrollment errors to your IT administrator (Inviare gli errori di registrazione Android all'amministratore IT)](../user-help/send-logs-to-your-it-admin-by-email-android.md)

## <a name="next-steps"></a>Passaggi successivi

È possibile ottenere altre informazioni sull'uso del controllo degli accessi in base al ruolo (RBAC) per definire i ruoli nel dispositivo aziendale, gestire app per dispositivi mobili e implementare attività di protezione dati. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo (RBAC) con Intune](role-based-access-control.md).

È possibile ottenere informazioni sui problemi noti in Microsoft Intune. Per altre informazioni, vedere [Problemi noti in Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).

È possibile apprendere come creare un ticket di supporto e ottenere supporto quando è necessario. [Ottenere supporto](get-support.md).
