---
title: Come accedere all'app del portale aziendale | Microsoft Docs
description: Informazioni su come accedere all'app Portale aziendale su più piattaforme.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4088185da2c01cfa7fd343203f7452d2796c4466
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79335822"
---
# <a name="sign-in-to-company-portal"></a>Accedere a Portale aziendale  

Si può accedere all'app Portale aziendale in tre modi:

* Accesso con l'indirizzo di posta elettronica aziendale e la relativa password.  
* Accesso con l'autenticazione basata su certificati.  
* Accesso da un altro dispositivo.    


## <a name="sign-in-with-your-email-address-and-password"></a>Accesso con l'indirizzo di posta elettronica e la password
La procedura seguente è accompagnata da screenshot dell'app Portale aziendale per iOS.  

1. Aprire l'app nel dispositivo e toccare **Accedi**.  

   ![Screenshot di esempio della pagina di accesso dell'app Portale aziendale.](./media/intune-ios-cp-signin-1908.png)


2. Immettere l'**account aziendale o dell'istituto di istruzione** e toccare **Avanti**.

   ![Viene chiesto all'utente di indicare solo l'indirizzo di posta elettronica anziché l'indirizzo di posta elettronica e la password nella stessa schermata.](./media/cp_ios_aad_signin_after_1804_002.png)

3. Immettere la password e toccare **Accedi**.

   ![La password verrà richiesta all'utente dopo che l'indirizzo di posta elettronica è stato accettato.](./media/cp_ios_aad_signin_after_1804_003.png)

4. L'app verificherà le credenziali. Al termine, è possibile accedere alle risorse dell'organizzazione e installare le app disponibili.  

   ![Terminato il processo di autenticazione, l'app Portale aziendale esegue l'accesso e visualizza una barra di caricamento.](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>Accesso con l'autenticazione basata su certificati
Questa opzione di accesso verrà visualizzata solo se l'organizzazione consente l'autenticazione basata su certificati ed è disponibile un certificato da usare.  

1. Aprire l'app Portale aziendale nel dispositivo.  

2. Immettere l'**Account aziendale o dell'istituto di istruzione**.  

3. Toccare il collegamento **Sign in with a certificate** (Accedi con un certificato).  

4. Toccare **Continua** per usare il certificato.  

## <a name="sign-in-from-another-device"></a>Accesso da un altro dispositivo

Se la società usa smart card per accedere ai computer, è probabile che sia necessario eseguire l'autenticazione accedendo da un altro dispositivo.  

1. Aprire l'app Portale aziendale nel dispositivo. Assicurarsi che sia il dispositivo che si userà per accedere alle risorse di lavoro.       

1. Selezionare **Accesso da un altro dispositivo**.  

   ![La pagina di accesso del portale aziendale chiede all'utente di immettere l'indirizzo di posta elettronica.  Vengono visualizzati il pulsante "Avanti" e il collegamento "Accesso da un altro dispositivo". È incluso anche il collegamento "Problemi di accesso all'account?" Un collegamento nella parte inferiore porta alle informazioni sulla privacy e sui cookie di Microsoft.](./media/cp_ios_aad_signin_after_1804_005.png)

2. Si riceve un codice univoco e monouso per accedere al portale aziendale. Copiare il codice.

   ![Viene indicato come passare alla pagina https://microsoft.com/devicelogin con un passcode univoco dal computer di lavoro, quindi come usare il codice per l'accesso.](./media/cp_ios_aad_signin_after_1804_006.png)

3. Nell'altro dispositivo (quello che si sta usando per eseguire l'autenticazione) aprire il browser e passare a [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin). Immettere o incollare il codice.  

   ![Un'immagine del browser dell'utente nel computer di lavoro anziché nell'app portale aziendale. Nella pagina "Accesso dispositivo" visualizzata viene chiesto all'utente di immettere il codice ricevuto nell'app portale aziendale.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. Selezionare __Continua__ per consentire a Portale aziendale di eseguire l'accesso nel dispositivo di lavoro.   

   ![L'utente ha immesso il codice univoco nel campo e il sito "Accesso dispositivo" ha chiesto di confermare che il portale aziendale di Intune è l'app corretta per la ricezione dell'autorizzazione ad accedere.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. Dopo la verifica del codice, è possibile chiudere la finestra.  

   ![Una pagina di conferma indica che l'utente ha eseguito l'accesso all'app portale aziendale sul proprio dispositivo e che questa pagina può essere chiusa.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. L'app Portale aziendale esegue l'accesso nel dispositivo di lavoro.  

   ![Dopo aver completato il processo di autenticazione, l'app del portale aziendale esegue l'accesso visualizzando una barra di caricamento.](./media/cp_ios_aad_signin_after_1804_007.png)

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  
