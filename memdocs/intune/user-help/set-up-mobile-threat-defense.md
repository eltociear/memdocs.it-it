---
title: Installare Mobile Threat Defense nel dispositivo mobile
description: Informazioni su come installare Mobile Threat Defense nel dispositivo mobile.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/27/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 676af3373acd399056a0ebdc77c9152442a72101
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182277"
---
# <a name="install-mobile-threat-defense"></a>Installare Mobile Threat Defense   

Come parte dei requisiti di sicurezza dell'organizzazione, potrebbe essere necessario installare l'app di un fornitore di soluzioni Mobile Threat Defense (MTD). Le app di questo tipo rilevano e avvisano l'utente delle minacce presenti nel dispositivo, ad esempio app sospette, reti o vulnerabilità del sistema operativo.  

Se non è disponibile l'app MTD necessaria, l'accesso alle app protette con l'account aziendale o dell'istituto di istruzione sarà bloccato. Questo articolo illustra [come installare un'app MTD](set-up-mobile-threat-defense.md#install-app) per sbloccarlo.  

Sono disponibili diverse app del fornitore MTD che è possibile installare, tutte con nomi diversi. L'organizzazione comunicherà quale app usare. Se viene richiesto di installare l'app, ma non vengono fornite altre istruzioni o un collegamento per ottenere l'app, contattare il supporto IT. 


## <a name="information-your-organization-can-see"></a>Informazioni che l'organizzazione può visualizzare   

L'organizzazione non può visualizzare i dati nelle app personali, ad esempio SMS, messaggi di posta elettronica e immagini. L'app MTD fornisce all'organizzazione informazioni sulle app personali, ad esempio il nome e la versione. Le informazioni effettivamente fornite variano a seconda del fornitore di soluzioni MTD usato dall'azienda. L'organizzazione potrebbe vedere:   

* Nome dell'app  
* ID dell'app: nome univoco che identifica l'app in Google Play.  
* Versione dell'app e numero di versione breve: Numeri di versione specifici per un'app.  
* Bundle dell'app e dimensioni dinamiche: Quantità di spazio usata da un'app nel dispositivo. 


## <a name="install-app"></a>Installare l'app    
Quando si accede a un'app protetta, viene automaticamente richiesto di installare un'app MTD. Per completare l'installazione, seguire i passaggi sullo schermo. Per ulteriori informazioni, seguire la procedura descritta in questa sezione.  
 
Potrebbe anche essere richiesto di registrare il dispositivo. La registrazione è necessaria per confermare la propria identità e connettere l'account aziendale o dell'istituto di istruzione al dispositivo. Se non si è registrati, si verrà automaticamente guidati nella procedura corrispondente prima di installare l'app MTD. Quando si arriva alla schermata **Ottieni l'accesso**, è possibile avviare la procedura di installazione.  

Per altre informazioni sulla registrazione dei dispositivi, vedere [Registrare il dispositivo personale nella rete dell'organizzazione](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>Installazione in iOS  

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

1. Nella schermata **Ottieni l'accesso** seguire le istruzioni per installare l'app MTD richiesta dall'organizzazione.  
2. Tornare alla schermata **Ottieni l'accesso** e selezionare **Apri**.  
3. L'app MTD chiede l'autorizzazione di accedere ad alcune aree del dispositivo, se necessario. Per il corretto funzionamento di questa app, è necessario **consentire** l'accesso ai contatti. Le autorizzazioni richieste variano in base al fornitore della soluzione MTD.  
4. Accedere con l'account aziendale.  
5. Attendere mentre l'app MTD analizza il dispositivo per individuare le minacce alla sicurezza.  
6. Tornare all'app aziendale o dell'istituto di istruzione a cui si stava provando ad accedere in origine. A questo punto, l'organizzazione potrebbe richiedere di configurare altri requisiti di sicurezza delle app, ad esempio di creare un PIN.  
7. A questo punto dovrebbe essere possibile accedere all'app. Se si è ancora bloccati:  
    * Nella schermata **Ottieni l'accesso** selezionare **Controlla di nuovo**.  
    * Passare all'app MTD e verificare la presenza di eventuali minacce. Completare i passaggi consigliati per risolvere la minaccia e ottenere di nuovo l'accesso.  

### <a name="installation-failed"></a>L'installazione non è riuscita  

Se l'installazione non riesce, contattare il responsabile del supporto IT. Visitare il [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) per trovare le informazioni di contatto dell'organizzazione.  

È anche possibile inviare i log dell'app al responsabile del supporto IT per fornire più contesto sull'installazione.  
* Utenti Android: [caricare e inviare i log tramite posta elettronica](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) dall'app Portale aziendale.   

* Utenti di dispositivi iOS: [recuperare e inviare i log](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) da Microsoft Edge per iOS.  

## <a name="resolve-a-threat"></a>Risolvere una minaccia  
Se una minaccia supera il livello di minaccia configurato, l'organizzazione può procedere in due modi:  
   
* Blocca l'accesso: impedisce all'utente di usare le app protette dell'organizzazione quando è connesso con l'account aziendale o dell'istituto di istruzione.  
* Cancella i dati: elimina i dati aziendali o dell'istituto di istruzione da una o più app protette dell'organizzazione.  

Per risolvere una minaccia e ottenere nuovamente l'accesso, aprire l'app MTD nel dispositivo. Leggere le informazioni fornite per apprendere in che modo la minaccia potrebbe influire sul dispositivo e come risolverla. Dopo aver seguito i passaggi per risolvere la minaccia, tornare all'app MTD e avviare una nuova analisi. Potrebbero essere necessari alcuni minuti per ottenere di nuovo l'accesso all'organizzazione.  

## <a name="next-steps"></a>Passaggi successivi  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).

