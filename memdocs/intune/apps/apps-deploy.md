---
title: Assegnare app ai gruppi con Microsoft Intune
titleSuffix: ''
description: Informazioni su come assegnare un'app di Intune ai gruppi di utenti o dispositivi usando Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dc349e22-9e1c-42ba-9e70-fb2ef980ef7a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 665e06e6aca0a4ba4f71147325eb587b1b8b4d40
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461539"
---
# <a name="assign-apps-to-groups-with-microsoft-intune"></a>Assegnare app ai gruppi con Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Dopo avere [aggiunto un'app](apps-add.md) a Microsoft Intune, è possibile assegnarla a utenti e dispositivi. Si noti che è possibile assegnare un'app a un dispositivo indipendentemente dal fatto che il dispositivo sia gestito da Intune o meno.

> [!NOTE]
> La finalità della distribuzione in base alla disponibilità non è supportata per i gruppi di dispositivi, ma solo per i gruppi di utenti.

La tabella seguente elenca le varie opzioni per l'assegnazione di applicazioni a utenti e dispositivi:

| Opzione  | Dispositivi registrati con Intune | Dispositivi non registrati con Intune |
|-------------------------------------------------------------------------------------------|------------------------------|----------------------------------|
| Assegnazione a utenti | Sì | Sì |
| Assegnazione a dispositivi | Sì | No |
| Assegnazione di app sottoposte a wrapping o di app che includono Intune SDK (per i criteri di protezione delle app) | Sì | Sì |
| Assegnazione di app come Disponibili | Sì | Sì |
| Assegnazione di app come Obbligatorio | Sì | No |
| Disinstallazione di app | Sì | No |
| Ricezione degli aggiornamenti delle app da Intune | Sì | No |
| Installazione di app disponibili sull'app Portale aziendale da parte degli utenti finali | Sì | No |
| Installazione di app disponibili sul portale aziendale basato sul Web da parte degli utenti finali | Sì | Sì |

> [!NOTE]
> Attualmente, è possibile assegnare app iOS/iPadOS e Android (app line-of-business e acquistate nello store) a dispositivi non registrati con Intune.
>
> Per ricevere gli aggiornamenti delle app nei dispositivi che non sono registrati con Intune, gli utenti devono accedere al portale aziendale dell'organizzazione e installare manualmente gli aggiornamenti delle app.

## <a name="assign-an-app"></a>Assegnare un'app

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Tutte le app**.
3. Nel riquadro **App** selezionare l'app che si vuole assegnare.
4. Nella sezione **Gestisci** del menu selezionare **Assegnazioni**.
5. Selezionare **Aggiungi gruppo** per aprire il riquadro **Aggiungi gruppo** relativo all'app.
6. Per l'app specifica, selezionare un **tipo di assegnazione**:
   - **Disponibile per i dispositivi registrati**: assegnare l'app ai gruppi di utenti che possono installare l'app dall'app Portale aziendale o dal sito Web.
   - **Disponibile con o senza registrazione**: assegnare l'app a gruppi di utenti i cui dispositivi non sono registrati con Intune. Agli utenti deve essere assegnata una licenza di Intune. Vedere [Licenze che includono Intune](../fundamentals/licenses.md).
   - **Richiesto**: l'app viene installata nei dispositivi nei gruppi selezionati. In alcune piattaforme potrebbero essere visualizzati messaggi di aggiuntivi per chiedere all'utente finale di confermare l'avvio dell'installazione dell'app.
   - **Uninstall** (Disinstalla): l'app viene disinstallata dai dispositivi nei gruppi selezionati se Intune ha installato in precedenza l'applicazione nel dispositivo tramite un'assegnazione "Disponibile per i dispositivi registrati" o "Obbligatoria" usando la stessa distribuzione. I collegamenti Web non possono essere rimossi dopo la distribuzione.

     > [!NOTE]
     > **Solo per le app iOS/iPadOS**:
     > - Per configurare cosa accade alle app gestite quando i dispositivi non sono più gestiti, è possibile selezionare l'impostazione desiderata in **Disinstalla alla rimozione del dispositivo**. Per altre informazioni, vedere [Impostazione di disinstallazione per le app gestite iOS/iPadOS](apps-deploy.md#app-uninstall-setting-for-ios-managed-apps).
     > - Se è stato creato un profilo VPN iOS/iPadOS contenente le impostazioni VPN per app, è possibile selezionare il profilo VPN in **VPN**. Quando l'app viene eseguita, viene aperta la connessione VPN. Per altre informazioni, vedere [Impostazioni VPN per dispositivi iOS/iPadOS](../configuration/vpn-settings-ios.md).
     >
     > **Solo per le app Android**: se si distribuisce un'app per Android come **Disponibile con o senza registrazione**, la segnalazione dello stato sarà disponibile solo nei dispositivi registrati.
     >
     > **Disponibile per i dispositivi registrati**: l'app viene visualizzata come disponibile solo se l'utente che ha eseguito l'accesso al Portale aziendale è l'utente primario che ha registrato il dispositivo e se l'app è applicabile al dispositivo.

7. Per selezionare i gruppi di utenti che sono interessati da questa assegnazione di app, selezionare **Gruppi inclusi**.
8. Dopo avere selezionato uno o più gruppi da includere, selezionare **Seleziona**.
9. Nel riquadro **Assegna** fare clic su **OK** per completare la selezione dei gruppi inclusi.
10. Per escludere gruppi di utenti da questa assegnazione di app, selezionare **Escludi gruppi**.
11. Se si è scelto di escludere alcuni gruppi in **Selezione gruppi** selezionare **Seleziona**.
12. Nel riquadro **Aggiungi gruppo** selezionare **OK**.
13. Nel riquadro **Assegnazioni** dell'app selezionare **Salva**.

L'app è ora assegnata ai gruppi selezionati. Per altre informazioni sull'inclusione ed esclusione di assegnazioni di app, vedere [Includere ed escludere assegnazioni di app](apps-inc-exl-assignments.md).

## <a name="how-conflicts-between-app-intents-are-resolved"></a>Modalità di risoluzione dei conflitti tra finalità di app

Un singolo gruppo non può essere usato come destinazione per più finalità di assegnazione di app. Se tuttavia un utente o un dispositivo è membro di più gruppi a ognuno dei quali è assegnata una finalità diversa, si verificherà un conflitto. Non è consigliabile creare conflitti di assegnazione per le applicazioni.
Le informazioni nella tabella seguente consentono di conoscere la finalità risultante quando si verifica un conflitto:

| Finalità gruppo 1 | Finalità gruppo 2 | Finalità risultante |
|-----------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Obbligatoria per l'utente|Disponibile per l'utente|Richiesto e disponibile|
|Obbligatoria per l'utente|Disinstallazione utente|Richiesto|
|Disponibile per l'utente|Disinstallazione utente|Uninstall|
|Obbligatoria per l'utente|Obbligatoria per il dispositivo|Entrambe presenti. Intune: obbligatoria
|Obbligatoria per l'utente|Disinstallazione dal dispositivo|Entrambe presenti. Intune: obbligatoria
|Disponibile per l'utente|Obbligatoria per il dispositivo|Entrambe presenti. Intune: obbligatoria (obbligatoria e disponibile)
|Disponibile per l'utente|Disinstallazione dal dispositivo|Entrambe presenti. Intune: disponibile.<br><br>L'app viene visualizzata nel portale aziendale.<br><br>Se l'app è già installata perché la sua finalità precedente era "app obbligatoria", viene disinstallata.<br><br>Se l'utente seleziona **Installa dal portale aziendale**, l'app viene installata e la finalità di disinstallazione non viene rispettata.|
|Disinstallazione utente|Obbligatoria per il dispositivo|Entrambe presenti. Intune: obbligatoria|
|Disinstallazione utente|Disinstallazione dal dispositivo|Entrambe presenti. Intune: disinstallazione|
|Obbligatoria per il dispositivo|Disinstallazione dal dispositivo|Richiesto|
|Obbligatoria e disponibile per l'utente|Disponibile per l'utente|Richiesto e disponibile|
|Obbligatoria e disponibile per l'utente|Disinstallazione utente|Richiesto e disponibile|
|Obbligatoria e disponibile per l'utente|Obbligatoria per il dispositivo|Entrambe presenti, obbligatoria e disponibile
|Obbligatoria e disponibile per l'utente|Disinstallazione dal dispositivo|Entrambe presenti. Intune: obbligatoria (obbligatoria e disponibile)
|Disponibile per l'utente senza registrazione|Obbligatoria e disponibile per l'utente|Richiesto e disponibile
|Disponibile per l'utente senza registrazione|Obbligatoria per l'utente|Richiesto
|Disponibile per l'utente senza registrazione|Disponibile per l'utente|Disponibile|
|Disponibile per l'utente senza registrazione|Obbligatoria per il dispositivo|Obbligatoria e disponibile senza registrazione|
|Disponibile per l'utente senza registrazione|Disinstallazione dal dispositivo|Disinstallazione e disponibile senza registrazione.<br><br>Se l'utente non ha installato l'app dal portale aziendale, la finalità di disinstallazione viene rispettata.<br><br>Se l'utente installa l'app dal portale aziendale, l'installazione ha priorità più alta rispetto alla disinstallazione.|

> [!NOTE]
> Solo per le app dello Store iOS gestite, quando si aggiungono queste app in Microsoft Intune assegnandole come **obbligatorie**, le app vengono create automaticamente con entrambe le finalità **Obbligatoria** e **Disponibile**.<br><br>
> Le app dello Store iOS (non le app VPP per iOS/iPadOS) di destinazione con scopo obbligatorio verranno applicate sul dispositivo al momento della connessione di quest'ultimo e verranno visualizzate anche nell'app Portale aziendale.<br><br>
> In caso di conflitti relativi all'impostazione **Disinstalla alla rimozione del dispositivo**, l'app non viene rimossa dal dispositivo quando quest'ultimo non è più gestito.

## <a name="managed-google-play-app-deployment-to-unmanaged-devices"></a>Distribuzione di app di Google Play gestito a dispositivi non gestiti
Per i dispositivi Android in uno scenario di distribuzione APP-WE (App Protection Policy Without Enrollment) non registrato, è possibile usare Google Play gestito per distribuire app dello Store e app line-of-business agli utenti. Le app di Google Play gestito impostate come **disponibili con o senza registrazione** vengono visualizzate nell'app Play Store nel dispositivo dell'utente finale e non nell'app Portale aziendale. Utente finale selezionerà e installerà le app distribuite in questo modo dall'app Play. Poiché le app vengono installate da Google Play gestito, per l'utente finale non è necessario modificare le impostazioni del dispositivo in uso per consentire l'installazione di app da origini sconosciute. In questo modo i dispositivi sono più protetti. Se uno sviluppatore di app pubblica in Play una nuova versione di un'app installata nel dispositivo di un utente, l'app viene aggiornata automaticamente da Play. 

Passaggi per assegnare un'app di Google Play gestito a dispositivi non gestiti:

1. Connettere il tenant di Intune a Google Play gestito. Se questa operazione è già stata eseguita per consentire la gestione di dispositivi del profilo di lavoro Android Enterprise, dedicati, completamente gestiti o di proprietà aziendale con profilo di lavoro, non occorre ripeterla.
2. Aggiungere app da Google Play gestito alla console di Intune.
3. Assegnare le app di Google Play gestito come **disponibili con o senza registrazione** al gruppo utenti desiderato. Le impostazioni **Obbligatoria** e **Disinstalla** per le app non sono supportate per i dispositivi non registrati.
4. Assegnare criteri di protezione delle app al gruppo utenti.
5. La volta successiva in cui l'utente finale aprirà l'app Portale aziendale, un messaggio visualizzato informerà della disponibilità di app nell'app Play Store.  L'utente potrà toccare questa notifica per passare direttamente all'app Play e visualizzare le app aziendali o accedere all'app Play Store separatamente.
6. L'utente finale può espandere il menu di scelta rapida all'interno dell'app Play Store e passare dal proprio account Google personale (in cui sono visualizzate le app personali) all'account aziendale (in cui sono visualizzate le app line-of-business assegnate) e viceversa. Per installare le app, l'utente finale può toccare Installa nell'app Play Store.

Quando viene eseguita una cancellazione selettiva di app nella console di Intune, l'account aziendale viene rimosso automaticamente dall'app Play Store. Da quel momento l'utente finale non visualizzerà più le app aziendali nel catalogo delle app di Play Store. Quando l'account aziendale viene rimosso da un dispositivo, le app installate da Play Store rimangono installate nel dispositivo e non vengono disinstallate. 

## <a name="app-uninstall-setting-for-ios-managed-apps"></a>Impostazione di disinstallazione per le app gestite iOS
Per i dispositivi iOS/iPadOS è possibile scegliere cosa deve accadere alle app gestite al momento dell'annullamento della registrazione del dispositivo da Intune o alla rimozione del profilo di gestione tramite l'impostazione **Disinstalla alla rimozione del dispositivo**. Questa impostazione si applica alle app solo dopo che il dispositivo è stato registrato e le app sono state installate come gestite. Non è possibile configurare l'impostazione per le app Web o i collegamenti Web. Dopo il ritiro di una Cancellazione selettiva di app, vengono rimossi solo i dati protetti da Mobile Application Management (MAM).

Per le nuove assegnazioni, vengono inseriti automaticamente i valori predefiniti per l'impostazione, come indicato di seguito:

|Tipo di app iOS | Impostazione predefinita per "Disinstalla alla rimozione del dispositivo" |
|--------------------|----------------|
| App line-of-business | Sì |
| App Store | No |
| App VPP | No |
| App predefinita | No |

>[!NOTE]
>**Tipi di assegnazione "Disponibile":** Se si aggiorna questa impostazione per gruppi "Disponibile per i dispositivi registrati" o "Disponibile con o senza registrazione", gli utenti che hanno già l'app gestita riceveranno l'impostazione aggiornata solo quando sincronizzeranno il dispositivo con Intune e reinstalleranno l'app. 
>
>**Assegnazioni preesistenti:** Le assegnazioni esistenti prima dell'introduzione di questa impostazione rimangono invariate e tutte le app gestite verranno rimosse quando il dispositivo verrà rimosso dalla gestione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul monitoraggio delle assegnazioni di app, vedere [Come monitorare le app](apps-monitor.md).
