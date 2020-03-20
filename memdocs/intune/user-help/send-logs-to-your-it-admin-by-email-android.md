---
title: Caricare e inviare i log tramite posta elettronica delle app | Microsoft Docs
description: Caricare e inviare i log tramite posta elettronica dalle app di Intune
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
ms.assetid: 85c868e7-8d63-480c-9770-4e99614a5c94
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: c288ea474fde9466b4b66056445ec93b572b29d2
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79347431"
---
# <a name="upload-and-email-logs"></a>Caricare e inviare i log tramite posta elettronica  

Se si verifica un problema nell'app Portale aziendale o Microsoft Intune, è possibile inviare tramite posta elettronica i dettagli del problema al responsabile del supporto aziendale. Questi dettagli forniranno un contesto aggiuntivo in relazione al problema.  

I dettagli relativi all'errore effettivo vengono memorizzati nel dispositivo in uno documento specifico definito _log di diagnostica_. Quando i log vengono caricati nell'app Portale aziendale o Microsoft Intune, vengono prima inviati agli sviluppatori Microsoft che lavorano sull'app. Questi log vengono usati per migliorare le funzionalità dell'app ed evitare errori in futuro. L'utente riceverà poi un ID evento imprevisto per l'errore specifico, che dovrà condividere con il referente per il supporto dell'azienda per l'uso nei casi correlati al supporto tecnico Microsoft.  

> [!Note]
> Perché il supporto tecnico dell'azienda possa individuare più facilmente la causa del problema, attivare la _registrazione dettagliata_ nel portale aziendale. Se si usa l'app Microsoft Intune, impostare **Livello di dettaglio del log** su **Dettagliato**. Nella registrazione dettagliata vengono registrati tutti i dettagli sull'errore. Tali dettagli vengono inclusi nel report. Per informazioni su come attivare la registrazione dettagliata, vedere [qui](use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md).  

## <a name="upload-and-email-logs-from-company-portal"></a>Caricare e inviare i log tramite posta elettronica da Portale aziendale  

1. Nell'app Portale aziendale è possibile avviare il supporto della posta elettronica in due modi.
    * Dalla schermata iniziale: Toccare **Menu** > **?** > **Invia messaggio di posta elettronica al supporto**.  
    * Da un messaggio di errore: Toccare **GUIDA** o **INVIA INFORMAZIONI**, se disponibile.  

    > [!NOTE]
    > **Menu** può essere un pulsante software o hardware, a seconda del dispositivo Android in uso.  

3. Toccare **Invia messaggio di posta elettronica e Carica i log**.  
4. Quando il caricamento è completo, toccare l'app di posta elettronica. 
5. Si aprirà un messaggio di posta elettronica con l'ID evento imprevisto pre-popolato nel campo Oggetto. Nel corpo del messaggio di posta elettronica descrivere il problema che si è verificato.    


## <a name="upload-and-email-logs-from-microsoft-intune-app"></a>Caricare e inviare i log tramite posta elettronica dall'app Microsoft Intune   

1. Nell'app Microsoft Intune è possibile avviare il supporto della posta elettronica in due modi.  
    * Dalla schermata iniziale: Toccare **Menu** > **?** > **Supporto tecnico**.  
    * Da un messaggio di errore: Toccare **GUIDA** o **INVIA INFORMAZIONI**, se disponibile.  

    > [!NOTE]
    > **Menu** può essere un pulsante software o hardware, a seconda del dispositivo Android in uso.

3. Toccare **Carica i log**.  
4. Al termine del caricamento, toccare **POSTA ELETTRONICA** e selezionare l'app di posta elettronica.  
5. Si aprirà un messaggio di posta elettronica con l'ID evento imprevisto pre-popolato nel campo Oggetto. Nel corpo del messaggio di posta elettronica descrivere il problema che si è verificato.  

## <a name="next-steps"></a>Passaggi successivi  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
