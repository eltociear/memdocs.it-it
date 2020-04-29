---
title: Registrare un dispositivo Android con Portale aziendale Intune e Intercede
description: Registrare un dispositivo Android e configurare l'autenticazione con credenziali derivate con Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8afc499f85e91658b411a25988ac858ca59030cc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81616047"
---
# <a name="set-up-android-device-with-company-portal-and-intercede"></a>Configurare un dispositivo Android con Portale aziendale e Intercede

Registrare il dispositivo nell'app Portale aziendale Intune per ottenere l'accesso protetto per dispositivi mobili alla posta elettronica, ai file e alle app dell'organizzazione. Dopo la registrazione, il dispositivo diventa *gestito*. L'organizzazione può assegnare criteri e app al dispositivo tramite un provider di gestione di dispositivi mobili (MDM), ad esempio Intune.

Durante la registrazione, si installeranno anche credenziali derivate nel dispositivo. L'organizzazione potrebbe richiedere di usare le credenziali derivate come metodo di autenticazione per l'accesso alle risorse o per la firma e la crittografia dei messaggi di posta elettronica.

Può essere necessario configurare credenziali derivate se si usa una smart card per:

* Accedere ad app, reti Wi-Fi e reti private virtuali (VPN) aziendali o dell'istituto di istruzione
* Firmare e crittografare i messaggi di posta elettronica aziendali o dell'istituto di istruzione usando i certificati S/MIME

Contenuto dell'articolo:

* Registrare un dispositivo mobile Android con Portale aziendale Intune.
* Configurare la propria smart card installando credenziali derivate dal provider di credenziali derivate dell'organizzazione, [Intercede](https://www.intercede.com/).  

## <a name="what-are-derived-credentials"></a>Che cosa sono le credenziali derivate?

Le credenziali derivate sono un certificato derivato dalle credenziali della smart card e installato nel dispositivo. Consente di accedere in remoto alle risorse aziendali, impedendo agli utenti non autorizzati di accedere a informazioni riservate.

Le credenziali derivate vengono usate per:

* Autenticare i dipendenti e gli studenti che accedono ad app, reti Wi-Fi e VPN aziendali o dell'istituto di istruzione
* Firmare e crittografare i messaggi di posta elettronica aziendali o dell'istituto di istruzione usando i certificati S/MIME

Le credenziali derivate sono un'implementazione delle linee guida del National Institute of Standards and Technology (NIST) per le credenziali derivate di verifica dell'identità personale (PIV) come parte della Pubblicazione speciale 800-157.

## <a name="prerequisites"></a>Prerequisiti

 Per completare la registrazione, sono necessari:

* Smart card fornita dall'azienda o dall'istituto di istruzione
* Accesso a un computer o a un chiosco multimediale che consente di accedere con la smart card
* Un dispositivo nuovo o con impostazioni predefinite ripristinate che esegue Android 7.0 o versione successiva
* L'app Microsoft Intune installata sul dispositivo

## <a name="enroll-device"></a>Registrare il dispositivo  

1. Accendere il dispositivo nuovo o con le impostazioni predefinite ripristinate.  
2. Nella schermata **Benvenuto** selezionare la lingua. Se è stato indicato di eseguire la registrazione con un codice a matrice o NFC, seguire la procedura corrispondente riportata di seguito.  
     * NFC: toccare con il dispositivo supportato da NFC il dispositivo di un programmatore per connettersi alla rete dell'organizzazione. Seguire le istruzioni visualizzate. Quando si raggiunge la schermata delle condizioni del servizio di Chrome, procedere al passaggio 5.  

     * Codice a matrice: seguire la procedura descritta in [Registrazione con codice a matrice](#qr-code-enrollment).  

     Se si è ricevuta indicazione di usare un altro metodo, procedere al passaggio 3.    

3. Connettersi alla rete Wi-Fi e toccare **AVANTI**. Seguire la procedura corrispondente al metodo di registrazione. 

    * Token: quando si arriva alla schermata di accesso di Google, seguire la procedura in [Registrazione con token](#token-enrollment).  
    * Google Zero Touch: dopo la connessione alla rete Wi-Fi, il dispositivo verrà riconosciuto dall'organizzazione. Procedere al passaggio 4 e seguire le istruzioni visualizzate fino al completamento dell'installazione.    
 
       ![Immagine di esempio della schermata delle condizioni di Google che viene visualizzata se si usa Google Zero Touch, con il pulsante Accept & Continue (Accetta e continua) evidenziato.](./media/google-zero-touch-intune-app-01.png)   
   
4. Esaminare le condizioni di Google. Toccare quindi **ACCEPT & CONTINUE** (Accetta e continua).  

      ![Immagine di esempio della schermata delle condizioni di Google, con il pulsante Accept & Continue (Accetta e continua) evidenziato.](./media/fully-managed-intune-app-04.png)   

5. Esaminare le condizioni d'uso di Chrome. Toccare quindi **ACCEPT & CONTINUE** (Accetta e continua).  

   ![Immagine di esempio della schermata Termini di servizio di Chrome, con il pulsante Accept & Continue (Accetta e continua) evidenziato.](./media/fully-managed-intune-app-06.png)  

6. Nella schermata di accesso toccare **Sign-in options** (Opzioni di accesso) e quindi **Sign in from another device** (Accesso da un altro dispositivo). 

7. Annotare il codice visualizzato.  

8. Passare al dispositivo abilitato per la smart card e andare all'indirizzo Web visualizzato sullo schermo. 

9. Immettere il codice annotato precedentemente.

   > [!div class="mx-imgBorder"]
   > ![Screenshot della richiesta di immissione del codice nel sito Web Portale aziendale.](./media/enter-code-intercede.png)

10. Inserire la smart card per accedere.  

11. Nella schermata di accesso selezionare l'account aziendale o dell'istituto di istruzione. Tornare quindi al dispositivo mobile.

12. A seconda dei requisiti dell'organizzazione, potrebbe essere richiesto di aggiornare le impostazioni, ad esempio per la schermata di blocco o la crittografia. Se vengono visualizzate queste richieste, toccare **SET** (Imposta) e seguire le istruzioni visualizzate.  

       ![Immagine di esempio della schermata Set up your work phone (Configura telefono aziendale), con il pulsante Set (Imposta) evidenziato.](./media/fully-managed-intune-app-10.png)   

13. Per installare le app aziendali nel dispositivo, toccare **INSTALL** (Installa). Al termine dell'installazione, toccare **NEXT** (Avanti).  

       ![Immagine di esempio della schermata Set up your work phone (Configura telefono aziendale), con il pulsante Install (Installa) evidenziato.](./media/fully-managed-intune-app-11.png)    

14. Toccare **START** (Avvia) per aprire l'app Microsoft Intune. 

    ![Immagine di esempio della schermata Set up your work phone (Configura telefono aziendale), con il pulsante Start (Avvia) evidenziato.](./media/fully-managed-intune-app-17.png)   
 

15. Tornare all'app Intune sul dispositivo mobile e seguire le istruzioni visualizzate per completare la registrazione del dispositivo. 

    ![Immagine di esempio della schermata di registrazione del dispositivo e configurazione dell'accesso, con il pulsante Done (Fine) evidenziato.](./media/fully-managed-intune-app-19.png)   

16. Per completare la configurazione del dispositivo, passare alla sezione relativa alla [configurazione della smart card](enroll-android-device-intercede.md#set-up-smart-card) in questo articolo.  

### <a name="qr-code-enrollment"></a>Registrazione con codice a matrice  
In questa sezione verrà eseguita la scansione del codice a matrice fornito dall'azienda.  Al termine, si verrà reindirizzati nuovamente alla procedura per la registrazione del dispositivo.     
  
1. Nella schermata **iniziale** toccare la schermata cinque volte per avviare il programma di configurazione del codice a matrice.  

   ![Immagine di esempio della schermata iniziale di configurazione del dispositivo con evidenziate le istruzioni per toccare lo schermo.](./media/qr-code-intune-app-01.png)  

2. Seguire le istruzioni visualizzate per la connessione alla rete Wi-Fi.  
3. Se il dispositivo non include uno scanner di codici a matrice, le schermate di installazione indicheranno lo stato di avanzamento mentre viene installato uno scanner. Attendere il completamento dell'installazione.  
4. Quando richiesto, eseguire la scansione del codice a matrice del profilo di registrazione fornito dall'organizzazione.  
5. Tornare alla procedura [Registrare il dispositivo](#enroll-device), passaggio 4 per continuare l'installazione.  

### <a name="token-enrollment"></a>Registrazione del token  
In questa sezione si immetterà il token fornito dall'azienda. Al termine, si verrà reindirizzati nuovamente alla procedura per la registrazione del dispositivo.  

1. Nella schermata di accesso a Google, in **Indirizzo email o numero di telefono** digitare **afw#setup**. Toccare **Avanti**. 

   ![Immagine di esempio della schermata di accesso a Google, che mostra che è stato digitato "afw#setup" nel campo.](./media/token-intune-app-01.png)   

2. Scegliere **Installa** per l'app **Android Device Policy**. Proseguire con l'installazione. A seconda del dispositivo, potrebbe essere necessario leggere e accettare condizioni aggiuntive.    

3. Nella schermata **Enroll this device** (Registra dispositivo) selezionare **Next** (Avanti).  

4. Selezionare **Enter code** (Immetti codice).  

5. Nella schermata **Scan or enter code** (Scansione o immissione codice) digitare il codice assegnato dall'organizzazione.  Fare quindi clic su **Avanti**.  

   ![Immagine di esempio della schermata Scan or enter code (Scansione o immissione codice) con evidenziato il pulsante Next (Avanti).](./media/token-intune-app-04.png)  

6. Tornare alla procedura [Registrare il dispositivo](#enroll-device), passaggio 4 per continuare l'installazione.

## <a name="set-up-smart-card"></a>Configurare una smart card  

1. Al termine della registrazione, l'app Intune invierà una notifica per la configurazione della smart card. Toccare la notifica. Se non si riceve la notifica, controllare la posta elettronica.

   > [!div class="mx-imgBorder"]
   > ![Screenshot di esempio della notifica push di Portale aziendale nella schermata iniziale del dispositivo.](./media/action-required-in-app-android.png)

2. Nella schermata di **configurazione della smart card**:

   1. Toccare il collegamento alle istruzioni di configurazione dell'organizzazione. Se l'organizzazione non fornisce istruzioni aggiuntive, verrà visualizzato questo articolo.

   2. Toccare **Inizia**.  

   > [!div class="mx-imgBorder"]
   > ![Screenshot di esempio della schermata di configurazione dell'accesso con smart card per dispositivi mobili di Portale aziendale.](./media/smart-card-open-entrust-android.png)

3. Passare al dispositivo o al chiosco multimediale self-service abilitato per la smart card e aprire l'app MyID. Accedere con le proprie credenziali aziendali.

4. Selezionare l'opzione per richiedere l'ID.

5. Quando viene richiesto quale profilo usare, selezionare l'opzione per l'attivazione con credenziali per dispositivi mobili. Verrà visualizzato un codice a matrice.  

6. Tornare al dispositivo Android. Nella schermata Portale aziendale > **Ottieni il codice a matrice** toccare **Avanti**.

    > [!div class="mx-imgBorder"]
    > ![Screenshot di esempio della schermata Ottieni il codice a matrice di Portale aziendale.](./media/get-qr-code-entrust-android.png)

7. Se viene richiesto di consentire all'app Intune di usare la fotocamera, toccare **Consenti**.

8. Eseguire la scansione dell'immagine del codice a matrice sul dispositivo abilitato per la smart card.

9. L'app Intune inizierà a scaricare e installare i certificati necessari per accedere alle risorse aziendali o dell'istituto di istruzione. A seconda della connessione Internet, questo processo potrebbe richiedere un certo tempo. Non chiudere l'app durante questo periodo di tempo.

    > [!div class="mx-imgBorder"]
    > ![Screenshot di esempio della schermata "Download e installazione dei certificati" di Portale aziendale](./media/install-certificates-entrust-android.png)

10. Elaborati tutti i certificati, attendere che l'app Intune completi la configurazione del dispositivo. Si noterà che la configurazione è stata completata quando viene visualizzato il messaggio **La configurazione è completata** .

    > [!div class="mx-imgBorder"]
    > ![Screenshot di esempio del Portale aziendale, schermata "La configurazione è completata"](./media/all-set-android.png)

## <a name="next-steps"></a>Passaggi successivi

Al termine della registrazione, sarà possibile accedere alle risorse aziendali, come la posta elettronica, le reti Wi-Fi e tutte le app rese disponibili dall'organizzazione. Per altre informazioni su come ottenere, cercare, installare e disinstallare le app nell'app Intune, vedere:

* [Usare le app gestite nel dispositivo](use-managed-apps-on-your-device-android.md)  
* [Gestire le app dal sito Web del portale aziendale](manage-apps-cpweb.md)  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
