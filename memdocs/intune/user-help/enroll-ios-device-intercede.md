---
title: Registrare un dispositivo iOS o iPadOS con Portale aziendale Intune e Intercede
description: Informazioni su come registrare un dispositivo iOS o iPadOS e configurare l'autenticazione tramite credenziali derivate con Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1bd216049c5dbda7c044949f9fa39c3b7bd56f9d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337239"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Configurare un dispositivo iOS o iPadOS con Portale aziendale e Intercede

Registrare il dispositivo nell'app Portale aziendale Intune per ottenere l'accesso protetto per dispositivi mobili alla posta elettronica, ai file e alle app dell'organizzazione.  Dopo la registrazione, il dispositivo diventa *gestito*. L'organizzazione può assegnare criteri e app al dispositivo tramite un provider di gestione di dispositivi mobili (MDM), ad esempio Intune.  

Durante la registrazione, si installeranno anche credenziali derivate nel dispositivo. L'organizzazione potrebbe richiedere di usare le credenziali derivate come metodo di autenticazione per l'accesso alle risorse o per la firma e la crittografia dei messaggi di posta elettronica. 

Può essere necessario configurare credenziali derivate se si usa una smart card per:

* Accedere ad app, reti Wi-Fi e reti private virtuali (VPN) aziendali o dell'istituto di istruzione
* Firmare e crittografare i messaggi di posta elettronica aziendali o dell'istituto di istruzione usando i certificati S/MIME  

Contenuto dell'articolo:  

* Registrare un dispositivo mobile iOS o iPadOS con Portale aziendale Intune.  
* Ottenere le credenziali derivate dal provider di credenziali derivate dell'organizzazione, [Intercede](https://www.intercede.com/).   


## <a name="what-are-derived-credentials"></a>Che cosa sono le credenziali derivate?  
Le credenziali derivate sono un certificato derivato dalle credenziali della smart card e installato nel dispositivo. Consente di accedere in remoto alle risorse aziendali, impedendo agli utenti non autorizzati di accedere a informazioni riservate.  

Le credenziali derivate vengono usate per: 
* Autenticare i dipendenti e gli studenti che accedono ad app, reti Wi-Fi e VPN aziendali o dell'istituto di istruzione
* Firmare e crittografare i messaggi di posta elettronica aziendali o dell'istituto di istruzione usando i certificati S/MIME  

Le credenziali derivate sono un'implementazione delle linee guida del National Institute of Standards and Technology (NIST) per le credenziali derivate di verifica dell'identità personale (PIV) come parte della Pubblicazione speciale 800-157.  

## <a name="prerequisites"></a>Prerequisiti

 Per completare la registrazione, sono necessari:

* Smart card fornita dall'azienda o dall'istituto di istruzione
* Accesso a un computer o a un chiosco multimediale self-service che consente di accedere con la smart card
* Dispositivo mobile
* App Portale aziendale Intune per iOS e iPadOS installata nel dispositivo


## <a name="enroll-device"></a>Registrare il dispositivo  
1. Aprire l'app Portale aziendale per iOS/iPadOS sul dispositivo mobile e accedere con l'account aziendale.  
2. Annotare il codice visualizzato.  

    ![Immagine di esempio dell'app Portale aziendale con un messaggio e il codice visualizzati.](./media/copy-code-intercede.png)  
1. Passare al dispositivo abilitato per la smart card e visitare l'indirizzo https://microsoft.com/devicelogin. 

1. Immettere il codice annotato precedentemente.
 
2. Inserire la smart card per accedere.   

3. Tornare all'app Portale aziendale sul dispositivo mobile e seguire le istruzioni visualizzate per registrare il dispositivo.  
4. Al termine della registrazione, Portale aziendale invierà una notifica per la configurazione della smart card. Toccare la notifica. Se non si riceve la notifica, controllare la posta elettronica.   

    ![Screenshot di esempio della notifica push di Portale aziendale nella schermata iniziale del dispositivo.](./media/action-required-in-app-intercede.png)  

5. Nella schermata **Configura l'accesso tramite smart card per dispositivi mobili**:  
    a. Toccare il collegamento alle istruzioni di configurazione dell'organizzazione. Se l'organizzazione non fornisce istruzioni aggiuntive, verrà visualizzato questo articolo.  
    b. Toccare **Inizia**.  

    ![Screenshot di esempio della schermata Configura l'accesso tramite smart card per dispositivi mobili di Portale aziendale.](./media/smart-card-info-intercede.png)  

6. Passare al dispositivo o al chiosco multimediale self-service abilitato per la smart card e aprire l'app MyID. Accedere con le proprie credenziali aziendali.  
7. Selezionare l'opzione per richiedere l'ID. 
8. Quando viene richiesto quale profilo usare, selezionare l'opzione per l'attivazione con credenziali per dispositivi mobili. Verrà visualizzato un codice a matrice.  
9. Tornare al dispositivo mobile. Nella schermata Portale aziendale > **Ottieni il codice a matrice** toccare **Continua**.  

    ![Screenshot di esempio della schermata Ottieni il codice a matrice di Portale aziendale.](./media/get-qr-code-intercede.png) 
 
10. Toccare **Usa la fotocamera** > **OK**.  

    ![Schermata di esempio di una richiesta di Portale aziendale, che richiede l'autorizzazione per consentire l'accesso alla fotocamera.](./media/allow-cp-camera-access-intercede.png)  

11. Eseguire la scansione dell'immagine del codice a matrice sul dispositivo abilitato per la smart card. 
12. Attendere il completamento della configurazione del dispositivo in Portale aziendale.  

## <a name="next-steps"></a>Passaggi successivi  
Al termine della registrazione, sarà possibile accedere alle risorse aziendali, come la posta elettronica, le reti Wi-Fi e tutte le app rese disponibili dall'organizzazione. Per altre informazioni su come ottenere, cercare, installare e disinstallare le app in Portale aziendale, vedere:

* [Gestire le app dal sito Web del portale aziendale](manage-apps-cpweb.md)  
* [Usare le app gestite nel dispositivo](use-managed-apps-on-your-device-ios.md)  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
