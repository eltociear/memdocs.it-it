---
title: Registrare un dispositivo Android con l'app Microsoft Intune e DISA Purebred
description: Informazioni su come registrare un dispositivo Android e configurare l'autenticazione tramite credenziali derivate con DISA Purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 584392891320f96eed16863225ffb323dc240594
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880610"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Configurare un dispositivo Android con l'app Microsoft Intune e DISA Purebred

Registrare il dispositivo con l'app Microsoft Intune per ottenere l'accesso protetto per dispositivi mobili alla posta elettronica, ai file e alle app dell'organizzazione. Dopo la registrazione, il dispositivo diventa *gestito*. L'organizzazione può assegnare criteri e app al dispositivo tramite un provider di gestione di dispositivi mobili (MDM), ad esempio Intune.  

Durante la registrazione, si installeranno anche credenziali derivate nel dispositivo. L'organizzazione potrebbe richiedere di usare le credenziali derivate come metodo di autenticazione per l'accesso alle risorse o per la firma e la crittografia dei messaggi di posta elettronica.

Può essere necessario configurare credenziali derivate se si usa una smart card per:

* Accedere ad app, reti Wi-Fi e reti private virtuali (VPN) aziendali o dell'istituto di istruzione
* Firmare e crittografare i messaggi di posta elettronica aziendali o dell'istituto di istruzione usando i certificati S/MIME

Contenuto dell'articolo:

* Registrare un dispositivo mobile Android con l'app Intune
* Configurare la propria smart card installando credenziali derivate dal provider di credenziali derivate dell'organizzazione, [DISA Purebred](https://public.cyber.mil/pki-pke/purebred/)

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
* L'app Purebred installata sul dispositivo (l'app deve essere installata automaticamente subito dopo la configurazione del dispositivo. In caso contrario, contattare il responsabile del supporto IT.)

Durante l'installazione sarà inoltre necessario contattare un agente o un rappresentante di Purebred.

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

16. Per completare la configurazione del dispositivo, passare alla sezione relativa alla [configurazione della smart card](enroll-android-device-disa-purebred.md#set-up-smart-card) in questo articolo.  

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

> [!NOTE]
> Per completare questa procedura, l'app Purebred è necessaria e verrà installata automaticamente nel dispositivo dopo la registrazione. Se l'app non è ancora disponibile dopo un breve periodo di tempo, contattare il personale del supporto IT.  

1. Al termine della registrazione, l'app Intune invierà una notifica per la configurazione della smart card. Toccare la notifica. Se non si riceve la notifica, controllare la posta elettronica.

   > [!div class="mx-imgBorder"]
   > ![Screenshot della notifica push dell'app Intune nella schermata iniziale del dispositivo.](./media/action-required-in-app-android.png)

2. Nella schermata di **configurazione della smart card**:

   1. Toccare il collegamento alle istruzioni di configurazione dell'organizzazione ed esaminarle. Se l'organizzazione non fornisce istruzioni aggiuntive, verrà visualizzato questo articolo.

   2. Toccare **Inizia**.   

   > [!div class="mx-imgBorder"]
   > ![Screenshot dell'app di Intune, schermata configurazione della smart card.](./media/smart-card-open-disa-purebred-android.png)

3. Nella schermata **Ottieni certificati** toccare **AVVIA PUREBRED** per aprire l'app Purebred. (L'app deve essere stata installata automaticamente sul dispositivo. In caso contrario, contattare il supporto tecnico.)  

   > [!div class="mx-imgBorder"]
   > ![Screenshot della richiesta dell'app Intune di aprire l'app DISA Purebred.](./media/open-app-prompt-disa-purbred-android.png)  

4. Per una corretta esecuzione, l'app Purebred potrebbe richiedere autorizzazioni aggiuntive. Toccare **Consenti** o **Consenti sempre** quando richiesto. Per ulteriori informazioni sui motivi per cui queste autorizzazioni sono necessarie, rivolgersi al personale di supporto o all'agente Purebred.  

5. Una volta nell'app Purebred, collaborare con l'agente Purebred dell'organizzazione per scaricare e installare i certificati necessari per accedere alle risorse aziendali o dell'istituto di istruzione.

    > [!IMPORTANT]
    > Durante questo processo, toccare **OK** o **Installa** quando richiesto. Non modificare i nomi delle autorità di certificazione (CA) o dei certificati richiesti per l'installazione.    

6. Al termine dell'installazione, si riceverà una notifica che indica che i certificati sono pronti. Toccare la notifica per tornare all'app Intune.

    > [!div class="mx-imgBorder"]
    > ![Screenshot della schermata "Consenti accesso ai certificati"](./media/certificates-ready-prompt-disa-purbred-android.png)

7. Dalla schermata **Consenti accesso ai certificati** si concede all'app di Intune l'autorizzazione per accedere alle credenziali derivate ottenute da DISA Purebred. Questo passaggio garantisce che l'organizzazione possa verificare l'identità dell'utente quando accede alle risorse aziendali o dell'istituto di istruzione protette.  

    1. Toccare **AVANTI**.

       > [!div class="mx-imgBorder"]
       > ![Screenshot della conferma "I certificati sono pronti"](./media/certificates-access-disa-purbred-android.png)

    2. Quando compare la richiesta **Scegli certificato**, non modificare la selezione. Il certificato corretto è già selezionato, quindi è sufficiente toccare **Seleziona** o **OK**.  

       > [!div class="mx-imgBorder"]
       > ![Screenshot della richiesta "Scegli certificato"](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. Poiché le credenziali derivate sono costituite da più certificati, è possibile che venga visualizzata la richiesta **Scegli certificato** più volte. Ripetere il passaggio precedente fino a quando non vengono visualizzate altre richieste.  

8. Elaborati tutti i certificati, attendere che l'app Intune completi la configurazione del dispositivo. Si noterà che la configurazione è stata completata quando viene visualizzato il messaggio **La configurazione è completata** .  

    > [!div class="mx-imgBorder"]
    > ![Screenshot della schermata "La configurazione è completata"](./media/all-set-android.png)

## <a name="next-steps"></a>Passaggi successivi

Al termine della registrazione, sarà possibile accedere alle risorse aziendali, come la posta elettronica, le reti Wi-Fi e tutte le app rese disponibili dall'organizzazione. Per altre informazioni su come ottenere, cercare, installare e disinstallare le app nell'app Intune, vedere:

* [Usare le app gestite nel dispositivo](use-managed-apps-on-your-device-android.md)  
* [Gestire le app dal sito Web del portale aziendale](manage-apps-cpweb.md)  


Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
