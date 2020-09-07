---
title: Registrare un dispositivo Android in Portale aziendale Intune | Microsoft Docs
description: Descrive come registrare un dispositivo Android in Portale aziendale Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ef1b6c82cae82763dc327f16e35d0e3bc522c3c7
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057471"
---
# <a name="enroll-your-device-with-company-portal"></a>Registrare il dispositivo in Portale aziendale  
Registrare il dispositivo Android personale o aziendale per ottenere accesso sicuro alla posta elettronica, alle app e ai dati aziendali. Il portale aziendale supporta i dispositivi Android, incluso Samsung Knox, che eseguono Android 4.4 e versioni successive.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox è un tipo di sicurezza che alcuni dispositivi Samsung usano per fornire protezione aggiuntiva oltre all'offerta prevista per i dispositivi Android nativi. Per determinare se il dispositivo è di tipo Samsung Knox, passare a **Impostazioni** > **Informazioni sul dispositivo**. Se non viene visualizzata l'indicazione **Versione Knox**, significa che il dispositivo è un dispositivo Android nativo.  

## <a name="install-company-portal-app"></a>Installare l'app Portale aziendale  
Installare l'app Portale aziendale Intune da [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Per l'elenco degli store nella Repubblica popolare cinese in cui è disponibile l'app, vedere [Installare l'app Portale aziendale nella Repubblica popolare cinese](install-company-portal-android-china.md).

1. Toccare **Home** > **Play Store**.

2. Cercare **Portale aziendale Intune**, quindi toccare l'app per aprirla. 

    ![android-search-company-portal](./media/and-cpinstall-1-search-cp.png)

4. Toccare **INSTALLA**.

5. Quando vengono richieste le autorizzazioni dell'app, toccare **ACCETTA**.  

    ![android-accept-company-portal-terms](./media/and-cpinstall-3-cp-accept.png)

## <a name="enroll-device"></a>Registrare il dispositivo  
Durante la registrazione potrebbe essere richiesto di scegliere la categoria che descrive meglio come viene usato il dispositivo. Il team di supporto tecnico aziendale usa questa risposta per controllare le app a cui è possibile accedere.  

1. Aprire l'app Portale aziendale e accedere con l'account aziendale o dell'istituto di istruzione.  

2. Se viene richiesto di accettare i termini e le condizioni dell'organizzazione, toccare **ACCETTA TUTTO**.  

   ![Immagine di esempio della schermata dei termini e condizioni del Portale aziendale, con il pulsante "Accetta tutto" evidenziato.](./media/accept-terms-1911.png)  


3. Esaminare le informazioni che l'organizzazione può visualizzare e quelle che non può visualizzare. Quindi toccare **CONTINUA**.


    ![Immagine di esempio di Portale aziendale, schermata Microsoft si impegna a garantire la privacy degli utenti con il pulsante Continua evidenziato.](./media/android-privacy-screen-1911.png)  
4. Esaminare i passaggi successivi. Toccare **AVANTI**.  

    ![Immagine di esempio della schermata Passaggi successivi di Portale aziendale, con il pulsante Avanti evidenziato.](./media/android-whats-next-1911.png)  


5. A seconda della versione di Android, potrebbe essere richiesto di consentire l'accesso a determinate parti del dispositivo. Queste richieste sono effettuate da Google e non sono controllate da Microsoft.  

    Toccare **Consenti** per le autorizzazioni seguenti:  
    * **Consentire a Portale aziendale di effettuare e gestire chiamate telefoniche**: questa autorizzazione consente al dispositivo di condividere il numero IMEI (International Mobile Station Equipment Identity) con Intune, il provider di gestione dei dispositivi dell'organizzazione. È sicuro consentire questa autorizzazione. Microsoft non effettuerà né gestirà mai le chiamate telefoniche.  
    * **Consentire a Portale aziendale di accedere ai contatti**: questa autorizzazione consente all'app Portale aziendale di creare, usare e gestire l'account aziendale.  È sicuro consentire questa autorizzazione. Microsoft non accederà mai ai contatti dell'utente. 

    Se si nega l'autorizzazione, la richiesta verrà visualizzata nuovamente al successivo accesso a Portale aziendale. Per disattivare i messaggi, selezionare **Non visualizzare più questo messaggio**. Per gestire le autorizzazioni dell'app, passare all'app Impostazioni > **App** > **Portale aziendale** > **Autorizzazioni** > **Telefono**.  

6. Attivare l'app di amministratore del dispositivo. 

    Portale aziendale richiede le autorizzazioni di amministratore del dispositivo per gestire in modo sicuro il dispositivo. L'attivazione dell'app consente all'organizzazione di identificare i possibili problemi di sicurezza, ad esempio tentativi ripetuti non riusciti di sbloccare il dispositivo, e rispondere in modo appropriato.  

    ![Immagine di esempio della schermata di attivazione dell'amministratore del dispositivo, con il pulsante Attiva evidenziato.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft non controlla il messaggio visualizzato in questa schermata ed è consapevole che la sua formulazione può sembrare piuttosto drastica. Portale aziendale non può specificare le restrizioni e i diritti di accesso rilevanti per l'organizzazione. In caso di domande sul modo in cui viene usata l'app nell'organizzazione, contattare il responsabile del supporto IT. Visitare il [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) per trovare le informazioni di contatto dell'organizzazione.  


7. Verrà avviata la registrazione del dispositivo. Se si usa un dispositivo Samsung Knox, verrà innanzitutto richiesto di esaminare l'informativa sulla privacy di ELM Agent.   

    ![Immagine di esempio della schermata dell'informativa sulla privacy di Samsung Knox visualizzata durante la registrazione.](./media/and-enroll-7-knox-privacy-policy.png)  

8. Nella schermata **Configurazione dell'accesso aziendale** verificare che il dispositivo sia registrato. Quindi toccare **CONTINUA**.  

    ![Immagine di esempio della schermata Configurazione dell'accesso aziendale di Portale aziendale, in cui Consenti la gestione del dispositivo risulta completato.](./media/update-settings-1911.png)  

9. L'organizzazione potrebbe richiedere all'utente di aggiornare le impostazioni del dispositivo. Toccare **RISOLVI** per modificare un'impostazione. Al termine dell'aggiornamento delle impostazioni, toccare **CONTINUA**.  

   ![Immagine di esempio della schermata Aggiorna impostazioni del dispositivo di Portale aziendale, con i pulsanti Risolvi e Continua evidenziati.](./media/resolve-settings-1911.png)  

10. Al termine dell'installazione, toccare **FINE**.    

    ![Immagine di esempio di Portale aziendale, schermata Configurazione dell'accesso aziendale che visualizza la configurazione completata e il pulsante Fine evidenziato.](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Passaggi successivi  

Prima di installare un'app aziendale o dell'istituto di istruzione, passare a **Impostazioni** > **Sicurezza** e attivare **Origini sconosciute**. Se non si attiva questa opzione, quando si tenta di installare un'app verrà visualizzato il messaggio seguente: "Installazione bloccata. per motivi di sicurezza che impediscono di installare nel dispositivo app ottenute da origini sconosciute. È possibile toccare **Impostazioni** nel messaggio per passare direttamente a **Origini sconosciute**.  

> [!Note]
> Se la propria organizzazione usa software per la gestione delle spese per telecomunicazioni, sarà necessario eseguire alcuni passaggi aggiuntivi prima che la registrazione del dispositivo sia completata. Per altre informazioni, vedere [qui](enroll-your-device-with-telecom-expense-management-android.md).

Se si verifica un errore durante la registrazione del dispositivo in Intune, è possibile [inviare un messaggio di posta elettronica al supporto tecnico aziendale](send-logs-to-your-it-admin-by-email-android.md).  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  