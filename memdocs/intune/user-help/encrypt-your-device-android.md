---
title: Crittografare il dispositivo Android per Intune | Microsoft Docs
description: Procedura per attivare la crittografia dei dispositivi Android quando richiesto da Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348783"
---
# <a name="encrypting-your-android-device"></a>Crittografia del dispositivo Android

La crittografia del dispositivo protegge i file e le cartelle dagli accessi non autorizzati in caso di furto o smarrimento del dispositivo. Dopo aver attivato la crittografia del dispositivo, solo gli utenti con la password o il PIN corretto saranno in grado di accedere al dispositivo. 

Per consentire l'accesso alle risorse aziendali o dell'istituto di istruzione, l'organizzazione potrebbe richiedere la crittografia del dispositivo Android. Alcuni dispositivi Android più recenti sono crittografati per impostazione predefinita.  

## <a name="turn-on-encryption"></a>Attivare la crittografia

Se l'app Portale aziendale o Microsoft Intune richiede di crittografare il dispositivo, completare i passaggi seguenti. 

> [!Note]
> Alcuni dispositivi Android di Huawei, Vivo e OPPO non possono essere crittografati. Per altre informazioni, vedere [qui](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

1. Impostare un blocco dello schermo del dispositivo.  
    a. Passare a **Impostazioni** > **Schermata di blocco e sicurezza** > **Tipo di blocco**.  
    b. Selezionare **PIN**, **Password** o **Sequenza**.  
    c. Seguire le istruzioni visualizzate per configurare il blocco dello schermo.  

2. Tornare a **Schermata di blocco e sicurezza** e selezionare **Avvio protetto**.
3. Scegliere **Richiedi PIN all'accensione del dispositivo** > **OK**.
4. Immettere il PIN per confermare e crittografare il dispositivo.
5. Aprire l'app Portale aziendale o Microsoft Intune.
    * Utenti dell'app Portale aziendale: selezionare il dispositivo e toccare **Controlla le impostazioni del dispositivo**. 
    * Utenti di Microsoft Intune: È necessario attendere che la pagina venga aggiornata. Una volta aggiornata la pagina, lo stato della crittografia dovrebbe essere modificato in Conforme.  

Nei dispositivi che eseguono Android 4.4 e versioni precedenti potrebbe non essere presente l'opzione **Avvio protetto**. In tal caso, completare la procedura seguente per crittografare il dispositivo.

1. Passare a **Impostazioni** > **Sicurezza** > **Crittografa dispositivo**. Le etichette visualizzate variano a seconda dei dispositivi Android. Se non viene visualizzata l'opzione **Crittografa dispositivo**, controllare in:
    * **Archiviazione** > **Crittografia archiviazione**
    * **Archiviazione** > **Schermata di blocco e sicurezza** > **Altre impostazioni di sicurezza** 

2. Seguire le istruzioni visualizzate. Durante la crittografia il dispositivo potrebbe essere riavviato più volte.
3. Aprire l'app Portale aziendale o Microsoft Intune.
    * Utenti dell'app Portale aziendale: selezionare il dispositivo e toccare **Controlla le impostazioni del dispositivo**.  
    * Utenti di Microsoft Intune: È necessario attendere che la pagina venga aggiornata. Una volta aggiornata la pagina, lo stato della crittografia dovrebbe essere modificato in Conforme.

## <a name="troubleshoot"></a>Risoluzione dei problemi  
**Problema**: Il dispositivo è già stato crittografato e

- Il pulsante di crittografia è disabilitato.
- Un messaggio informa che è necessario crittografare il dispositivo.
- Si verificano errori quando si prova a usare l'app Portale aziendale o Microsoft Intune.

**Possibili soluzioni**

- Verificare che il dispositivo sia carico e collegato.  
- Assicurarsi di aver impostato un PIN o una password nel dispositivo.  

Serve ancora assistenza? Contattare il supporto tecnico aziendale (accedere al [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) per informazioni sul contatto) oppure scrivere al <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">team Microsoft Android</a>.  
