---
title: Installare Mobile Threat Defense nel dispositivo mobile
description: Informazioni sulle app Mobile Threat Defense e su come configurarle.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 37b7006ef912d87276c11e09cb6db0c0f14059c4
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193913"
---
# <a name="install-mobile-threat-defense-app"></a>Installare un'app Mobile Threat Defense  

> [!TIP]
> Sono disponibili diverse app MTD sul mercato. L'organizzazione dovrà indicare quale usare. Se viene chiesto di installare un'app MTD e non si viene reindirizzati immediatamente alla pagina in cui configurarla o installarla, contattare il supporto il personale di supporto IT per assistenza.  

In base ai requisiti di sicurezza dell'organizzazione, potrebbe essere necessario installare l'app di un fornitore di soluzioni Mobile Threat Defense (MTD). Le app di questo tipo rilevano e avvisano l'utente delle minacce presenti nel dispositivo, ad esempio app sospette, reti o vulnerabilità del sistema operativo.  

Se l'app MTD necessaria non è disponibile, l'accesso alle app gestite protette con l'account aziendale o dell'istituto di istruzione (ad esempio Microsoft Excel o OneDrive) sarà bloccato. Questo articolo illustra [come configurare un'app MTD](set-up-mobile-threat-defense.md#set-up-mtd-app) e riacquisire l'accesso.    

## <a name="mtd-apps-for-ios"></a>App MTD per iOS
Le app MTD seguenti vengono comunemente usate nei dispositivi iOS. Selezionare un'app per aprire la relativa presentazione nell'App Store.   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>App MTD per Android 
Le app MTD seguenti vengono comunemente usate nei dispositivi Android. Selezionare un'app per aprire la relativa presentazione in Google Play.  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>Informazioni che l'organizzazione può visualizzare   

L'organizzazione non può visualizzare i dati nelle app personali, ad esempio SMS, messaggi di posta elettronica e immagini. L'app MTD fornisce all'organizzazione informazioni sulle app personali, ad esempio il nome e la versione. Le informazioni effettivamente fornite variano a seconda del fornitore di soluzioni MTD usato dall'azienda. L'organizzazione potrebbe vedere:   

* Nome dell'app  
* ID dell'app: nome univoco che identifica l'app in Google Play.  
* Versione dell'app e numero di versione breve: Numeri di versione specifici per un'app.  
* Bundle dell'app e dimensioni dinamiche: Quantità di spazio usata da un'app nel dispositivo. 


## <a name="set-up-mtd-app"></a>Configurare un'app MTD 
Quando si accede a un'app protetta, viene richiesto di installare un'app MTD. Seguire i passaggi visualizzati per completare l'installazione e ottenere accesso all'app protetta. 

Per un contesto aggiuntivo, vedere le istruzioni per [iOS](set-up-mobile-threat-defense.md#ios-setup) o [Android](set-up-mobile-threat-defense.md#android-setup) in questa sezione. Questi passaggi sono supplementari e non sostituiscono le istruzioni visualizzate sullo schermo. 

Se viene richiesto di installare un'app MTD, ma non si è certi di quale installare, contattare il personale di supporto IT per assistenza.  

### <a name="device-registration"></a>Registrazione del dispositivo  
La registrazione del dispositivo è necessaria per confermare la propria identità e connettere l'account aziendale o dell'istituto di istruzione al dispositivo. Se il dispositivo non è registrato, si verrà automaticamente indirizzati ai passaggi visualizzati sullo schermo prima di installare l'app MTD.   

Per altre informazioni sulla registrazione dei dispositivi, vedere [Registrare il dispositivo personale nella rete dell'organizzazione](/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>Installazione in iOS  
Questi passaggi iniziano nella schermata **Ottieni l'accesso**, che viene visualizzato dopo l'accesso a un'app protetta.  

1. Nella schermata **Ottieni l'accesso** seguire le istruzioni per installare l'app MTD richiesta dall'organizzazione.   
2. Tornare alla schermata **Ottieni l'accesso** e selezionare **Apri**.  
3. L'app MTD chiede l'autorizzazione per aprire Microsoft Authenticator. Selezionare **Open** (Apri). 
4. Accedere con l'account aziendale. 
5. Attendere mentre l'app MTD analizza il dispositivo per individuare le minacce alla sicurezza. 
6. Tornare all'app aziendale o dell'istituto di istruzione a cui si stava provando ad accedere in origine. A questo punto, l'organizzazione potrebbe richiedere di configurare altri requisiti di sicurezza delle app, ad esempio di creare un PIN.   
7. A questo punto dovrebbe essere possibile accedere all'app. Se si è ancora bloccati:  
    * Nella schermata **Ottieni l'accesso** selezionare **Controlla di nuovo**.  
    * Passare all'app MTD e verificare la presenza di eventuali minacce. Completare i passaggi consigliati per risolvere la minaccia e ottenere di nuovo l'accesso.    

### <a name="android-setup"></a>Installazione per Android 
Questi passaggi iniziano nella schermata **Ottieni l'accesso**, che viene visualizzato dopo l'accesso a un'app protetta.  

1. Nella schermata **Ottieni l'accesso** seguire le istruzioni per installare l'app MTD richiesta dall'organizzazione.  
2. Tornare alla schermata **Ottieni l'accesso** e selezionare **Apri**.  
3. L'app MTD chiede l'autorizzazione di accedere ad alcune aree del dispositivo, se necessario. Per il corretto funzionamento di questa app, è necessario **consentire** l'accesso ai contatti. Le autorizzazioni richieste variano in base al fornitore della soluzione MTD.  
4. Accedere con l'account aziendale.  
5. Attendere mentre l'app MTD analizza il dispositivo per individuare le minacce alla sicurezza.  
6. Tornare all'app aziendale o dell'istituto di istruzione a cui si stava provando ad accedere in origine. A questo punto, l'organizzazione potrebbe richiedere di configurare altri requisiti di sicurezza delle app, ad esempio di creare un PIN.  
7. A questo punto dovrebbe essere possibile accedere all'app. Se si è ancora bloccati:  
    * Nella schermata **Ottieni l'accesso** selezionare **Controlla di nuovo**.  
    * Passare all'app MTD e verificare la presenza di eventuali minacce. Completare i passaggi consigliati per risolvere la minaccia e ottenere di nuovo l'accesso.  


## <a name="resolving-a-threat"></a>Risoluzione di una minaccia
Se viene rilevata una minaccia che supera il livello configurato, l'organizzazione può procedere in due modi:  
   
* Blocca l'accesso: impedisce all'utente di usare le app protette dell'organizzazione quando è connesso con l'account aziendale o dell'istituto di istruzione.  
* Cancella i dati: elimina i dati aziendali o dell'istituto di istruzione da una o più app protette dell'organizzazione.  

Per risolvere una minaccia e ottenere nuovamente l'accesso alle app protette:  

1. Aprire l'app MTD nel proprio dispositivo.     
2. Leggere i dettagli della minaccia nell'app, che spiegano come potrebbe influire sul dispositivo in caso di mancata risoluzione e come risolverla. 
3. Dopo avere apportato le modifiche necessarie al dispositivo, tornare nell'app MTD e avviare una nuova analisi. Ripetere questi passaggi fino a risolvere tutte le minacce. Potrebbero essere necessari alcuni minuti prima che le modifiche vengano sincronizzate con l'organizzazione. Una volta sincronizzate le modifiche, sarà possibile ottenere nuovamente l'accesso all'app protetta. 

## <a name="get-support"></a>Ottenere supporto
Visitare il [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) per trovare le informazioni di contatto dell'organizzazione. Contattare il supporto per assistenza su:

* Identificazione dell'app MTD da usare  
* Installazione  
* Installazione non riuscita  
* Rilevamento e risoluzione di una minaccia  
* Disinstallazione di un'app MTD   
 

### <a name="share-app-logs-with-it-support"></a>Condividere i log delle app con il supporto IT  
È anche possibile inviare i log dell'app al personale del supporto IT per fornire un maggior contesto sull'installazione non riuscita.  
* Utenti Android: [caricare e inviare i log tramite posta elettronica](./send-logs-to-your-it-admin-by-email-android.md) dall'app Portale aziendale.   

* Utenti di dispositivi iOS: [recuperare e inviare i log](/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) da Microsoft Edge per iOS.  


## <a name="next-steps"></a>Passaggi successivi  

Per altre informazioni sul funzionamento delle app gestite, su come ottenerle e su come riconoscere che se ne sta usando una, vedere gli articoli seguenti.  

* [Usare le app gestite nel dispositivo Android](use-managed-apps-on-your-device-android.md)
* [Usare le app gestite nel dispositivo iOS](use-managed-apps-on-your-device-ios.md)  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).