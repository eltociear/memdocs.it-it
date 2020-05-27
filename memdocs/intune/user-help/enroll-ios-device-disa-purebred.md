---
title: Registrare un dispositivo iOS o iPadOS con Portale aziendale Intune e DISA Purebred
description: Informazioni su come registrare un dispositivo iOS o iPadOS e configurare l'autenticazione tramite credenziali derivate con DISA Purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 50330bbdc61eeeada022c44f4d1f2f68b31f19a4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881551"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Configurare un dispositivo iOS o iPadOS con Portale aziendale e DISA Purebred  

Registrare il dispositivo nell'app Portale aziendale Intune per ottenere l'accesso protetto per dispositivi mobili alla posta elettronica, ai file e alle app dell'organizzazione. Dopo la registrazione, il dispositivo diventa *gestito*. L'organizzazione può assegnare criteri e app al dispositivo tramite un provider di gestione di dispositivi mobili (MDM), ad esempio Intune.  

Durante la registrazione, si installeranno anche credenziali derivate nel dispositivo. L'organizzazione potrebbe richiedere di usare le credenziali derivate come metodo di autenticazione per l'accesso alle risorse o per la firma e la crittografia dei messaggi di posta elettronica. 

Può essere necessario configurare credenziali derivate se si usa una smart card per:

* Accedere ad app, reti Wi-Fi e reti private virtuali (VPN) aziendali o dell'istituto di istruzione
* Firmare e crittografare i messaggi di posta elettronica aziendali o dell'istituto di istruzione usando i certificati S/MIME  

Contenuto dell'articolo:  

   * Registrare un dispositivo mobile iOS o iPadOS con Portale aziendale Intune.  
   * Ottenere le credenziali derivate dal provider di credenziali derivate dell'organizzazione, DISA Purebred: https:\//cyber.mil/pki-pke/purebred/.  

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
* Dispositivo mobile
* App Portale aziendale Intune per iOS e iPadOS installata nel dispositivo   

Durante l'installazione sarà inoltre necessario contattare un agente o un rappresentante di Purebred.      

## <a name="enroll-device"></a>Registrare il dispositivo  
1. Aprire l'app Portale aziendale per iOS/iPadOS sul dispositivo mobile e accedere con l'account aziendale.  

2. Annotare il codice visualizzato.  

    ![Immagine di esempio dell'app Portale aziendale con un messaggio e il codice visualizzati.](./media/copy-code-intercede.png)  
3. Passare al dispositivo abilitato per la smart card e visitare l'indirizzo https://microsoft.com/devicelogin. 
4. Immettere il codice annotato precedentemente.  

    ![Screenshot di esempio della richiesta di immissione del codice nel sito Web Portale aziendale.](./media/enter-code-intercede.png)   

5. Inserire la smart card per accedere.  
6. Tornare all'app Portale aziendale sul dispositivo mobile e seguire le istruzioni visualizzate per registrare il dispositivo.  
7. Al termine della registrazione, Portale aziendale invierà una notifica per la configurazione della smart card. Toccare la notifica. Se non si riceve la notifica, controllare la posta elettronica.   

    ![Screenshot di esempio della notifica push di Portale aziendale nella schermata iniziale del dispositivo.](./media/action-required-in-app-intercede.png)  
8. Nella schermata **Configura l'accesso tramite smart card per dispositivi mobili**:  
    a. Toccare il collegamento alle istruzioni di configurazione dell'organizzazione. Se l'organizzazione non fornisce istruzioni aggiuntive, verrà visualizzato questo articolo.  
    b. Fare clic su **Apri** per aprire l'app Purebred.  

    ![Screenshot di esempio della schermata Configura l'accesso tramite smart card per dispositivi mobili di Portale aziendale.](./media/smart-card-open-disa-purebred.png)  
9. Quando viene richiesto di consentire a Portale aziendale di aprire l'app di registrazione Purebred, selezionare **Apri**.   

    ![Screenshot di esempio della richiesta di aprire l'app DISA Purebred in Portale aziendale.](./media/open-app-prompt-disa-purbred.png)  
10. Se l'app funziona correttamente, collaborare con l'agente di Purebred dell'organizzazione per configurare e scaricare il profilo di configurazione per la pre-registrazione in Purebred.   
11. Passare all'app Impostazioni > **Generale** > **Gestione di profili e dispositivi** > **Installa profilo** e toccare **Installa**.  
12. Immettere il passcode del dispositivo.  
13. Installare il profilo. Potrebbe essere necessario toccare **Installa** più di una volta per avviare l'installazione. 
14. Tornare all'app di registrazione Purebred. Seguire le istruzioni dell'agente di Purebred per continuare.  
 
15. Dopo aver scaricato il profilo di configurazione, passare all'app Impostazioni > **Generale** > **Gestione di profili e dispositivi** > **Installa profilo** e toccare **Installa**.   
16.  Immettere il passcode del dispositivo.
17. Installare il profilo. Potrebbe essere necessario toccare **Installa** più di una volta per avviare l'installazione. 
18. Al termine dell'installazione, tornare all'app Portale aziendale.  
19.  Nella schermata **Configura l'accesso tramite smart card per dispositivi mobili** toccare **Continua**.  

20. Dalla schermata **Importa certificati** sarà possibile recuperare e importare le credenziali derivate ottenute da DISA Purebred.  

    a. Toccare **Continua**.   

    ![Screenshot di esempio della schermata Importa certificati di Portale aziendale.](./media/import-certificate-disa-purebred.png)  
    b. Passare a iCloud Drive **Sfoglia** > **Posizioni** e toccare **Altre posizioni**.  

    ![Screenshot di esempio di iCloud Drive, con l'opzione Altre posizioni nel menu Sfoglia evidenziata.](./media/icloud-drive-more-locations.png)  
    c. Toccare l'interruttore per abilitare **Portachiavi Purebred**.  

    ![Screenshot di esempio della visualizzazione Sfoglia di iCloud Drive, con l'interruttore Portachiavi Purebred abilitato.](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Toccare **Pacchetto credenziali Purebred**.  

    ![Screenshot di esempio di una schermata di iOS con l'opzione selezionabile Pacchetto credenziali Purebred.](./media/purebred-credential-package.png)  
    f. Verrà visualizzato un elenco di certificati. Selezionarne uno e quindi toccare **Importa la chiave**.  

    ![Screenshot di esempio di un elenco di certificati selezionabili, con uno già selezionato.](./media/import-purebred-keychain.png) 
21. Tornare all'app Portale aziendale e attendere il completamento della configurazione del dispositivo in Portale aziendale.   

## <a name="next-steps"></a>Passaggi successivi  
Al termine della registrazione, sarà possibile accedere alle risorse aziendali, come la posta elettronica, le reti Wi-Fi e tutte le app rese disponibili dall'organizzazione. Per altre informazioni su come ottenere, cercare, installare e disinstallare le app in Portale aziendale, vedere:

* [Gestire le app dal sito Web del portale aziendale](manage-apps-cpweb.md)  
* [Usare le app gestite nel dispositivo](use-managed-apps-on-your-device-ios.md)  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
