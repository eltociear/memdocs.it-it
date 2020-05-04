---
title: includere il file
description: Includere file
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183050"
---
Questi avvisi forniscono importanti informazioni utili per prepararsi per le modifiche e le funzionalità di Intune future.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Fine del supporto per Windows 10 Mobile in Microsoft Intune<!--3544938-->
Il supporto Mainstream Microsoft per Windows 10 Mobile è terminato nel dicembre 2019. Come indicato nella presente informativa sul supporto, gli utenti di Windows 10 Mobile non saranno più idonei a ricevere nuovi aggiornamenti della sicurezza, hotfix non di sicurezza, opzioni di supporto tecnico gratuite o aggiornamenti del contenuto tecnico online da Microsoft. A seconda del supporto del sistema operativo per dispositivi mobili, Microsoft Intune terminerà il supporto del Portale aziendale per l'app Windows 10 Mobile e del sistema operativo Windows 10 Mobile il 10 agosto 2020.

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?
Se nell'organizzazione sono distribuiti dispositivi Windows 10 Mobile, da ora al 10 agosto 2020 è possibile registrare nuovi dispositivi, aggiungere o rimuovere criteri e app o aggiornare le impostazioni di gestione. Dopo il 10 agosto, le nuove registrazioni verranno interrotte e infine verrà rimossa la gestione di Windows 10 Mobile dall'interfaccia utente di Intune. I dispositivi non verificheranno più il servizio Intune e i dati dei dispositivi e dei criteri verranno eliminati.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica
È possibile controllare i report di Intune per vedere quali dispositivi o utenti potrebbero essere interessati. Passare a **Dispositivi** > **Tutti i dispositivi** e filtrare in base al sistema operativo. È possibile aggiungere altre colonne per facilitare l'identificazione degli utenti dell'organizzazione che hanno dispositivi che eseguono Windows 10 Mobile. Richiedere agli utenti finali di aggiornare i dispositivi o di interrompere l'uso dei dispositivi per l'accesso aziendale.


### <a name="end-of-support-for-legacy-pc-management"></a>Termine del supporto per la gestione dei PC legacy

La gestione dei PC legacy non sarà più supportata a partire dal 15 ottobre 2020. Aggiornare i dispositivi a Windows 10 e registrarli nuovamente come dispositivi MDM perché continuino a essere gestiti da Intune.

[Altre informazioni](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Riduzione del supporto per l'amministratore di dispositivi Android<!--5857738-->
L'amministratore di dispositivi Android, a volte denominato gestione Android "legacy" e rilasciato con Android 2.2, è una modalità di gestione dei dispositivi Android. Funzionalità di gestione migliorate, tuttavia, sono ora disponibili in [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (con la versione Android 5.0). Con l'obiettivo di passare a una gestione dei dispositivi moderna, più ricca e sicura, Google sta riducendo il supporto per l'amministratore di dispositivi nelle nuove versioni di Android.

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?
Queste modifiche di Google influiranno sugli utenti di Intune nei modi seguenti:  
- Intune potrà offrire supporto completo per i dispositivi Android gestiti dall'amministratore di dispositivi che eseguono Android 10 e versioni successive solo fino al secondo trimestre del 2020. I dispositivi gestiti dall'amministratore di dispositivi che eseguono Android 10 o versione successiva in seguito non potranno più essere gestiti interamente. In particolare, i dispositivi interessati non riceveranno nuovi requisiti per le password.
    - I dispositivi Samsung Knox non saranno interessati in questo intervallo di tempo perché è disponibile un supporto esteso grazie all'integrazione di Intune con la piattaforma Knox. In questo modo si ottiene più tempo per pianificare la transizione dalla gestione dei dispositivi da parte dell'amministratore.    
- I dispositivi Android gestiti dall'amministratore di dispositivi che continueranno a usare versioni di Android precedenti ad Android 10 non saranno interessati e potranno continuare a essere interamente gestiti con l'amministratore di dispositivi.    
- Per tutti i dispositivi con Android 10 e versioni successive, Google ha limitato la capacità degli agenti di gestione dell'amministratore di dispositivi come il Portale aziendale di accedere alle informazioni relative all'identificatore del dispositivo. Dopo l'aggiornamento di un dispositivo ad Android 10 o versione successiva, questa limitazione influisce sulle funzionalità di Intune seguenti:  
    - Il controllo di accesso alla rete per la rete VPN non funzionerà più.   
    - L'identificazione dei dispositivi come di proprietà dell'azienda con l'IMEI o il numero di serie non contrassegnerà automaticamente i dispositivi come di proprietà dell'azienda.  
    - L'IMEI e il numero di serie non saranno più visibili agli amministratori IT in Intune. 
        > [!NOTE]
        > Ciò interessa solo i dispositivi gestiti dall'amministratore di dispositivi in Android 10 e versioni successive e non i dispositivi gestiti come Android Enterprise. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica
Per evitare la riduzione di funzionalità prevista per il terzo trimestre del 2020, è consigliabile attenersi alle indicazioni seguenti:
- Non eseguire l'onboarding di nuovi dispositivi nella gestione di tipo amministratore di dispositivi.
- Se si prevede che un dispositivo riceverà un aggiornamento ad Android 10, eseguirne la migrazione dalla gestione di tipo amministratore di dispositivi alla gestione Android Enterprise e/o ai criteri di protezione delle app.

#### <a name="additional-information"></a>Informazioni aggiuntive
- [Indicazioni di Google per la migrazione da amministratore di dispositivi ad Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Documentazione di Google sul piano per deprecare l'API amministratore di dispositivi](https://developers.google.com/android/work/device-admin-deprecation)