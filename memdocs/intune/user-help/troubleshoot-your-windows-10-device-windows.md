---
title: Risolvere i problemi di accesso ai dispositivi Windows 10 dell'istituto di istruzione o aziendali | Microsoft Intune
description: Risolvere i problemi di accesso o di connessione all'account per un dispositivo Windows 10 registrato.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 7c96bef7c1be004714f0b06dd47c9c28850118da
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643421"
---
# <a name="troubleshoot-windows-10-device-access"></a>Risolvere i problemi di accesso ai dispositivi Windows 10
Questo articolo descrive come risolvere i problemi di accesso per un dispositivo Windows 10 registrato. 

## <a name="check-wi-fi-connection"></a>Controllare la connessione Wi-Fi  

Per accedere alle risorse aziendali o dell'Istituto di istruzione, è necessaria una connessione Wi-Fi. Verificare di essere connessi al Wi-Fi e provare di nuovo ad accedere alle risorse.  

## <a name="add-work-or-school-account-in-settings-app"></a>Aggiungere un account aziendale o dell'istituto di istruzione nell'app Impostazioni  
Questa procedura è identica a quella usata per registrare il dispositivo. Tuttavia, se l'account non viene visualizzato nell'app **Impostazioni**, è necessario eseguirla di nuovo.  

1. Aprire l'app **Impostazioni**. 
2. Selezionare **Account**.
3. Il passaggio successivo varia a seconda della versione di Windows 10 in uso. 
    * Versione 1607 e successive: Selezionare **Accesso aziendale o dell'istituto di istruzione**.
    * Versione 1511 e precedenti: Selezionare **Accesso società**.  
4. Verificare l'account. Se non è elencato, selezionare il pulsante **Connetti** con il segno più per aggiungerlo. 
5. Accedere con le credenziali aziendali o dell'istituto di istruzione. 
6. Seguire le istruzioni visualizzate per completare la procedura di connessione.  
7. Al termine, l'account verrà aggiunto come connessione. Sarà possibile accedere a tutte le risorse che l'organizzazione rende disponibili.   

## <a name="contact-it-support-for-access-requirements"></a>Contattare il supporto IT per i requisiti di accesso  
Se l'account aziendale o dell'Istituto di istruzione è elencato nell'app Impostazioni, il dispositivo e l'account sono già connessi. Per altre informazioni sui problemi di accesso, contattare il personale di supporto IT. È possibile che vengano applicati requisiti o restrizioni che impediscono l'accesso a determinate risorse.  

## <a name="error-messages"></a>messaggi di errore  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>Non è possibile individuare automaticamente un endpoint di gestione che corrisponde al nome utente immesso. Controlla il nome utente e riprova. Se conosci l'URL dell'endpoint di gestione, immetterlo qui.

**Causa**: Non è stato possibile verificare l'account con l'URL specificato, denominato anche endpoint di gestione.  

#### <a name="resolution"></a>Soluzione
1. Immettere nuovamente il nome utente e la password. 
2. Se il problema persiste, contattare il supporto IT per ottenere l'URL corretto, ad esempio: www.nomeazienda.onmicrosoft.com. 
3. Quando richiesto, immettere l'URL specificato. 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>Connessione assente. Assicurarsi di essere connessi alla rete.

**Causa**: Il dispositivo non è connesso al Wi-Fi ed è necessaria una connessione per aggiungere un account aziendale o dell'istituto di istruzione.     

#### <a name="resolution"></a>Soluzione
1. Dalla barra degli strumenti o dalle impostazioni del dispositivo selezionare l'icona del globo **Stato della rete**.
2. Selezionare una rete Wi-Fi > **Connetti**.  
3. Provare a connettere di nuovo l'account.  


## <a name="next-steps"></a>Passaggi successivi  

Serve ancora assistenza? Contattare il responsabile del supporto IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
