---
title: Risolvere i problemi dei profili di posta elettronica in Microsoft Intune - Azure | Microsoft Docs
description: Descrizioni dei problemi comuni relativi ai profili di posta elettronica di Microsoft Intune, tra cui i profili duplicati e gli errori nei dispositivi Android Samsung KNOX Standard, e delle relative soluzioni.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d011d6111ede4bb5879e53e771d20b792bf00d3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995127"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Problemi comuni e soluzioni per i profili di posta elettronica in Microsoft Intune

Esaminare alcuni problemi comuni relativi ai profili di posta elettronica e le relative procedure di risoluzione.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Agli utenti viene richiesto ripetutamente di immettere la password

Agli utenti viene richiesto ripetutamente di immettere la password per il profilo di posta elettronica. Se i certificati vengono usati per autenticare e autorizzare l'utente, controllare le assegnazioni di tutti i profili certificato. In genere, questi profili certificato vengono assegnati a gruppi di utenti e non a gruppi di dispositivi. Se uno dei profili certificato non è destinato a un utente, Intune continua a ritentare la distribuzione del profilo di posta elettronica.

Se la catena di profili di posta elettronica viene assegnata a gruppi di utenti, assicurarsi che anche i profili certificato vengano assegnati a gruppi di utenti.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Per i profili distribuiti nei gruppi di dispositivi si riscontrano errori e latenza

I profili di posta elettronica vengono in genere assegnati a gruppi di utenti. In alcuni casi è possibile che vengano assegnati a gruppi di dispositivi.

- Ad esempio, quando si vuole distribuire un profilo di posta elettronica basato su certificati solo ai dispositivi Surface e non ai desktop. In questo scenario, l'assegnazione a gruppi di dispositivi potrebbe avere senso. Tenere presente che questi dispositivi potrebbero risultare non conformi, possono restituire errori e potrebbero non ottenere immediatamente i profili di posta elettronica.

  In questo esempio si crea il profilo di posta elettronica e si assegna il profilo a gruppi di dispositivi. Il dispositivo viene riavviato e si verifica un ritardo prima che un utente esegua l'accesso. Durante questo ritardo viene distribuito il profilo certificato PKCS, assegnato a gruppi di utenti. Non essendo ancora presente alcun utente, il profilo certificato PKCS causa la mancata conformità del dispositivo. Nel Visualizzatore eventi potrebbero essere anche visualizzati errori per il dispositivo.

  Per ottenere la conformità, l'utente accede al dispositivo e viene sincronizzato con Intune per ricevere i criteri. Gli utenti possono eseguire la risincronizzazione manualmente o attendere la sincronizzazione successiva.

- Si supponga, ad esempio, di usare gruppi dinamici. Se Azure AD non aggiorna immediatamente i gruppi dinamici, questi dispositivi potrebbero risultare non conformi.

In questi scenari occorre decidere se è più importante usare i gruppi di dispositivi o è preferibile mostrare tutti i criteri come conformi.

## <a name="device-already-has-an-email-profile-installed"></a>Nel dispositivo è già installato un profilo di posta elettronica

Se gli utenti creano un profilo di posta elettronica prima di registrarsi in Intune o in Microsoft 365 MDM, il profilo di posta elettronica distribuito da Intune potrebbe non funzionare nel modo previsto:

- **iOS/iPadOS**: Intune rileva un profilo di posta elettronica esistente duplicato in base all'indirizzo di posta elettronica e al nome host. Il profilo di posta elettronica creato dall'utente blocca la distribuzione del profilo creato da Intune. Questo scenario rappresenta un problema comune, dato che gli utenti di iOS/iPadOS in genere creano un profilo di posta elettronica e poi eseguono la registrazione. L'app Portale aziendale indica che l'utente non è conforme e potrebbe richiedergli di rimuovere il profilo di posta elettronica.

  L'utente deve rimuovere il proprio profilo di posta elettronica in modo che il profilo di Intune possa essere distribuito. Per evitare questo problema, richiedere agli utenti di registrarsi e consentire a Intune di distribuire il profilo di posta elettronica. Gli utenti possono quindi creare il proprio profilo di posta elettronica.

- **Windows**: Intune rileva un profilo di posta elettronica esistente duplicato in base all'indirizzo di posta elettronica e al nome host. Intune sovrascrive il profilo di posta elettronica esistente creato dall'utente.

- **Samsung KNOX Standard**: Intune identifica un account di posta elettronica duplicato in base all'indirizzo di posta elettronica e lo sovrascrive con il profilo di Intune. Se questo account viene configurato dall'utente, viene sovrascritto nuovamente dal profilo di Intune. Questo comportamento potrebbe confondere l'utente di cui viene sovrascritta la configurazione dell'account.

Samsung KNOX non usa il nome host per identificare il profilo. È consigliabile evitare di creare più profili di posta elettronica da distribuire allo stesso indirizzo di posta elettronica in host diversi, perché si sovrascrivono tra loro.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Errore 0x87D1FDE8 per il dispositivo KNOX Standard

**Problema**: dopo la creazione e la distribuzione di un profilo di posta elettronica di Exchange Active Sync per Samsung KNOX Standard per diversi dispositivi Android, l'errore **0x87D1FDE8** o **Correzione non riuscita** viene visualizzato nella scheda Criteri delle proprietà del dispositivo.

Verificare la configurazione del profilo EAS per Samsung KNOX e i criteri di origine. L'opzione di sincronizzazione Samsung Notes non è più supportata e non deve essere selezionata nel profilo. Assicurarsi che i dispositivi abbiano tempo sufficiente per elaborare i criteri, fino a 24 ore.

## <a name="unable-to-send-images-from--email-account"></a>Impossibile inviare immagini dall'account di posta elettronica

Gli utenti con account di posta elettronica configurati automaticamente non possono inviare immagini o foto dai propri dispositivi. Questo scenario può verificarsi se l'opzione **Consenti di inviare i messaggi di posta elettronica dalle applicazioni di terze parti** non è abilitata.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione**.
3. Selezionare il profilo di posta elettronica > **Proprietà** > **Impostazioni**.
4. Impostare l'opzione **Consenti l'invio di messaggi di posta elettronica da applicazioni di terze parti** su **Abilita**.

## <a name="next-steps"></a>Passaggi successivi

Ottenere [supporto da Microsoft](../fundamentals/get-support.md) o usare i [forum della community](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
