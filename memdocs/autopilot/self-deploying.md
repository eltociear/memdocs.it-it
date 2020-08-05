---
title: Modalità di distribuzione automatica di Windows Autopilot
description: La modalità di distribuzione automatica consente la distribuzione di un dispositivo con un'interazione minima con l'utente. Questa modalità è progettata per distribuire Windows 10 come chiosco multimediale, dispositivo di firma digitale o dispositivo condiviso.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 5fccc36ff1ecacaee3d2aa3ed7c317faaaefc113
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756540"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Modalità di distribuzione automatica di Windows Autopilot

**Si applica a: Windows 10, versione 1903 o successiva**

La modalità di distribuzione automatica di Windows Autopilot consente la distribuzione di un dispositivo senza alcuna interazione dell'utente. Per i dispositivi con una connessione Ethernet, non è necessaria alcuna interazione con l'utente. per i dispositivi connessi tramite Wi-Fi, non è necessaria alcuna interazione dopo aver effettuato la connessione Wi-Fi (scegliendo la lingua, le impostazioni locali e la tastiera, quindi effettuando una connessione di rete).  

La modalità di distribuzione automatica unisce il dispositivo in Azure Active Directory, registra il dispositivo in Intune (o un altro servizio MDM) sfruttando Azure AD per la registrazione MDM automatica e garantisce che tutti i criteri, le applicazioni, i certificati e i profili di rete vengano sottoposti a provisioning nel dispositivo, sfruttando la pagina relativa allo stato della registrazione per impedire l'accesso al desktop fino a quando non viene eseguito il 

>[!NOTE]
>La modalità di distribuzione automatica non supporta l'aggiunta o la Aggiunta ad Azure AD ibrido di Active Directory.  Tutti i dispositivi verranno aggiunti a Azure Active Directory.

La modalità di distribuzione automatica è progettata per distribuire Windows 10 come chiosco multimediale, dispositivo di firma digitale o dispositivo condiviso. Quando si configura un chiosco multimediale, è possibile sfruttare il nuovo browser Kiosk, un'app basata su Microsoft Edge, che può essere usata per creare un'esperienza di esplorazione personalizzata e gestita da MDM. In combinazione con i criteri MDM per creare un account locale e configurarlo per l'accesso automatico, è possibile automatizzare la configurazione completa del dispositivo. Per altre informazioni su queste opzioni, vedere semplificazione della gestione di chioschi multimediali con Windows 10.  Per altri dettagli, vedere [configurare un chiosco multimediale o un accesso digitale in Intune o altro servizio MDM](https://docs.microsoft.com/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service) .

>[!NOTE]
>La modalità di distribuzione automatica non associa attualmente un utente al dispositivo (poiché non è stato specificato alcun ID utente o password come parte del processo).  Di conseguenza, alcune funzionalità Azure AD e Intune (ad esempio il ripristino di BitLocker, l'installazione di app dalla Portale aziendale o l'accesso condizionale) potrebbero non essere disponibili per un utente che accede al dispositivo. Per ulteriori informazioni, vedere gli [scenari e le funzionalità di Windows Autopilot](windows-autopilot-scenarios.md) e [impostare l'algoritmo di crittografia BitLocker per i dispositivi Autopilot](bitlocker.md).

![Esperienza utente con la modalità di distribuzione automatica di Windows Autopilot](images/self-deploy-welcome.png)

## <a name="requirements"></a>Requisiti

Poiché la modalità di distribuzione automatica usa l'hardware TPM 2,0 di un dispositivo per autenticare il dispositivo nel tenant Azure AD di un'organizzazione, non è possibile usare i dispositivi senza TPM 2,0 con questa modalità.  I dispositivi devono supportare anche l'attestazione del dispositivo TPM.  Tutti i dispositivi Windows appena prodotti devono soddisfare tali requisiti.

>[!IMPORTANT]
>Se si tenta di eseguire una distribuzione in modalità self-Deploying in un dispositivo che non dispone del supporto TPM 2,0 o in una macchina virtuale, il processo avrà esito negativo durante la verifica del dispositivo con un errore di timeout 0x800705B4 (i TPMs virtuali Hyper-V non sono supportati). Si noti anche che la finestra 10, versione 1903 o successiva, è necessaria per usare la modalità di distribuzione automatica a causa di problemi con l'attestazione del dispositivo TPM in Windows 10, versione 1809. Poiché Windows 10 Enterprise 2019 LTSC si basa su Windows 10 versione 1809, la modalità di distribuzione automatica non è supportata anche in Windows 10 Enterprise 2019 LTSC. Vedere [problemi noti di Windows Autopilot](known-issues.md) per esaminare altri errori noti e soluzioni.

Per visualizzare un logo specifico dell'organizzazione e il nome dell'organizzazione durante il processo di Autopilot, Azure Active Directory la personalizzazione dell'azienda deve essere configurata con le immagini e il testo da visualizzare.  Per informazioni dettagliate, vedere [Guida introduttiva: aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso in Azure ad](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) . 

## <a name="step-by-step"></a>Procedura dettagliata

Per eseguire una distribuzione in modalità self-Deploying utilizzando Windows Autopilot, è necessario completare i passaggi di preparazione seguenti:

-   Creare un profilo di Autopilot per la modalità di distribuzione automatica con le impostazioni desiderate.  In Microsoft Intune, questa modalità viene scelta in modo esplicito durante la creazione del profilo. Si noti che non è possibile creare un profilo in Microsoft Store for business o centro per i partner per la modalità di distribuzione automatica.
-   Se si usa Intune, creare un gruppo di dispositivi in Azure Active Directory e assegnare il profilo di Autopilot al gruppo.  Verificare che il profilo sia stato assegnato al dispositivo prima di provare a distribuire il dispositivo.
-   Avviare il dispositivo, connetterlo al Wi-Fi, se necessario, quindi attendere il completamento del processo di provisioning.

## <a name="validation"></a>Convalida

Quando si esegue una distribuzione in modalità self-Deploying utilizzando Windows Autopilot, è necessario osservare l'esperienza dell'utente finale seguente:

-   Una volta stabilita la connessione a una rete, il profilo di Autopilot verrà scaricato.
-   Se il profilo di Autopilot è stato configurato per configurare automaticamente la lingua, le impostazioni locali e il layout della tastiera, queste schermate OOBE dovrebbero essere ignorate purché sia disponibile la connettività Ethernet.  In caso contrario, sono necessari passaggi manuali:
    -   Se in Windows 10 sono preinstallate più lingue, l'utente deve scegliere una lingua.
    -   L'utente deve selezionare le impostazioni locali e un layout di tastiera e, facoltativamente, un secondo layout di tastiera.
-   Se connesso tramite Ethernet, non è previsto alcun messaggio di rete.  Se non è disponibile alcuna connessione Ethernet e la connessione Wi-Fi è incorporata, l'utente deve connettersi a una rete wireless.
-   Windows 10 verificherà la presenza di aggiornamenti OOBE critici e, se disponibili, verranno installati automaticamente (se necessario, il riavvio).
-   Il dispositivo si unirà Azure Active Directory.
-   Dopo l'aggiunta Azure Active Directory, il dispositivo si registrerà in Intune o in altri servizi MDM configurati.
-   Verrà visualizzata la [pagina relativa allo stato della registrazione](enrollment-status.md) .
-   A seconda delle impostazioni del dispositivo distribuite, il dispositivo può:
    -   Rimanere nella schermata di accesso, in cui i membri dell'organizzazione possono accedere specificando le credenziali Azure AD.
    -   Accedere automaticamente come account locale per i dispositivi configurati come un chiosco multimediale o una firma digitale.

>[!NOTE]
>La distribuzione dei criteri EAS con la modalità di distribuzione automatica per le distribuzioni in modalità tutto schermo causerà un errore di accesso automatico alla funzionalità. 

Se i risultati osservati non corrispondono a queste aspettative, consultare la documentazione relativa alla [risoluzione dei problemi di Windows Autopilot](troubleshooting.md) .
