---
title: Crittografare il dispositivo Android per Intune | Microsoft Docs
description: Procedura per attivare la crittografia dei dispositivi Android quando richiesto da Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696273"
---
# <a name="encrypting-your-android-device"></a>Crittografia del dispositivo Android

La crittografia del dispositivo protegge i file e le cartelle dagli accessi non autorizzati in caso di furto o smarrimento del dispositivo. Rende i dati presenti nel dispositivo inaccessibili e illeggibili per gli utenti che non hanno un passcode. 

Per consentire l'accesso alle risorse aziendali o dell'istituto di istruzione, l'organizzazione potrebbe richiedere di:

* [Crittografare il dispositivo](#encrypt-device)
* [Abilitare l'avvio protetto](#enable-secure-startup)
* [Impostare il passcode di avvio, il PIN o un altro metodo di autenticazione](#set-startup-passcode)  

> [!Note]
> Alcuni dispositivi Android di Huawei, Vivo e OPPO non possono essere crittografati. Per altre informazioni, vedere [Il dispositivo è crittografato, ma le app indicano il contrario](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Crittografare il dispositivo

Per crittografare il dispositivo, seguire questa procedura. Il dispositivo può essere riavviato più volte. 

Il nome e il percorso dell'opzione di crittografia variano a seconda del produttore del dispositivo e della versione di Android. 

1. Aprire l'app **Impostazioni**.
2. Digitare **sicurezza** o **crittografia** nella barra di ricerca dell'app per trovare le impostazioni correlate.
3. Toccare l'opzione per crittografare il dispositivo. Seguire le istruzioni visualizzate.  
4. Quando richiesto, impostare una password della schermata di blocco, un PIN o un altro metodo di autenticazione, se consentito dall'organizzazione. 
5. Per ricontrollare le impostazioni, aprire l'app Portale aziendale o Microsoft Intune.
    * Utenti dell'app Portale aziendale: selezionare il dispositivo e toccare **Controlla le impostazioni del dispositivo**. 
    * Utenti di Microsoft Intune: È necessario attendere che la pagina venga aggiornata. Una volta aggiornata la pagina, lo stato della crittografia dovrebbe essere modificato in Conforme. 

## <a name="enable-secure-startup"></a>Abilitare l'avvio protetto

L'organizzazione può richiedere l'abilitazione dell'avvio protetto nell'ambito dei criteri di crittografia. Questa funzionalità protegge ulteriormente il dispositivo richiedendo l'immissione di una password o un PIN prima dell'avvio del telefono. Sono disponibili altre opzioni di autenticazione, che tuttavia variano a seconda di ciò che l'organizzazione consente. 

Il nome e il percorso dell'opzione di avvio protetto variano a seconda del produttore del dispositivo e della versione di Android. In alcuni dispositivi questa impostazione può essere indicata come **protezione avanzata**. 

1. Aprire l'app **Impostazioni**.
2. Digitare **avvio protetto** nella barra di ricerca dell'app.
3. Toccare **Avvio protetto** > **Richiedi PIN all'accensione del dispositivo**.
4. Quando richiesto, immettere il PIN del dispositivo.   
5. Per ricontrollare le impostazioni, aprire l'app Portale aziendale o Microsoft Intune.
    * Utenti dell'app Portale aziendale: selezionare il dispositivo e toccare **Controlla le impostazioni del dispositivo**. 
    * Utenti di Microsoft Intune: È necessario attendere che la pagina venga aggiornata. Una volta aggiornata la pagina, lo stato della crittografia dovrebbe essere modificato in Conforme.  


## <a name="set-startup-passcode"></a>Impostare il passcode di avvio   
Quando si [crittografa il dispositivo](#encrypt-device) e si [abilita l'avvio protetto](#enable-secure-startup), verrà richiesto di impostare il PIN del dispositivo, la password o un altro metodo di autenticazione, se consentito dall'organizzazione. Non sono necessari altri passaggi. 

Per scegliere o modificare il tipo di schermata di blocco:

1. Aprire l'app **Impostazioni**.
2. Digitare **blocco schermo** nella barra di ricerca dell'app.
3. Toccare **Tipo di blocco schermo**.
4. Toccare il tipo di blocco dello schermo che si vuole usare e seguire le istruzioni visualizzate per confermare.  

## <a name="troubleshoot"></a>Risoluzione dei problemi    
**Problema**: Il pulsante di crittografia è disabilitato.   

**Possibile soluzione**: 
* Verificare che il dispositivo sia completamente carico e collegato. La crittografia può richiedere un po' di tempo e la batteria deve essere completamente carica.   

**Problema**: Un messaggio informa che è comunque necessario crittografare il dispositivo.  

**Possibili soluzioni**:
   *  [Impostare una schermata di blocco](#set-startup-passcode) nel dispositivo. 
   * [Abilitare l'avvio protetto](#enable-secure-startup).

Serve ancora assistenza? Contattare il supporto tecnico aziendale (accedere al [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) per informazioni sul contatto) oppure scrivere al <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">team Microsoft Android</a>.  
