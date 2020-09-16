---
title: Modalità di distribuzione automatica di Windows Autopilot
description: La modalità di distribuzione automatica consente la distribuzione di un dispositivo con un'interazione minima con l'utente. Questa modalità è progettata per distribuire Windows 10 come chiosco multimediale, dispositivo di firma digitale o dispositivo condiviso.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: 13b45b972ed17d24efedaa048c0e48ea2f2d90d2
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568608"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Modalità di distribuzione automatica di Windows Autopilot

**Si applica a: Windows 10, versione 1903 o successiva**

La modalità di distribuzione automatica di Windows Autopilot consente di distribuire un dispositivo senza alcuna interazione dell'utente. Per i dispositivi con una connessione Ethernet, non è necessaria alcuna interazione con l'utente. Per i dispositivi connessi tramite Wi-Fi, l'utente deve solo:
- Scegliere la lingua, le impostazioni locali e la tastiera.
- Creare una connessione di rete. 

La modalità di distribuzione automatica fornisce tutti gli elementi seguenti:
- Aggiunge il dispositivo alla Azure Active Directory.
- Registra il dispositivo in Intune (o un altro servizio MDM) usando Azure AD per la registrazione MDM automatica.
- Verifica che tutti i criteri, le applicazioni, i certificati e i profili di rete vengano sottoposti a provisioning nel dispositivo.
- Usa la pagina relativa allo stato della registrazione per impedire l'accesso fino a quando non viene effettuato il provisioning completo del dispositivo.

>[!NOTE]
>La modalità di distribuzione automatica non supporta l'aggiunta o la Aggiunta ad Azure AD ibrido di Active Directory. Tutti i dispositivi verranno aggiunti a Azure Active Directory.

La modalità di distribuzione automatica consente di distribuire un dispositivo Windows 10 come chiosco multimediale, dispositivo di firma digitale o dispositivo condiviso.

Quando si configura un dispositivo in modalità tutto schermo, è possibile usare il browser per il [chiosco multimediale](https://www.microsoft.com/p/kiosk-browser/9ngb5s5xg2kp?rtc=1&activetab=pivot:overviewtab) . Questa app è basata su Microsoft Edge e può essere usata per creare un'esperienza di esplorazione personalizzata e gestita da MDM.

È possibile automatizzare completamente la configurazione dei dispositivi combinando la modalità self-deploing con i criteri MDM. Usare i criteri MDM per creare un account locale configurato per l'accesso automatico. Per altre informazioni, vedere:
- [Semplificazione della gestione del chiosco multimediale con Windows 10](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/simplifying-kiosk-management-for-it-with-windows-10/ba-p/187691).
- [Configurare un chiosco multimediale o un accesso digitale in Intune o in un altro servizio MDM](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service).

>[!NOTE]
>La modalità di distribuzione automatica non associa attualmente un utente al dispositivo (poiché non è stato specificato alcun ID utente o password come parte del processo). Di conseguenza, alcune funzionalità Azure AD e Intune (ad esempio il ripristino di BitLocker, l'installazione di app dalla Portale aziendale o l'accesso condizionale) potrebbero non essere disponibili per un utente che accede al dispositivo. Per ulteriori informazioni, vedere gli [scenari e le funzionalità di Windows Autopilot](windows-autopilot-scenarios.md) e [impostazione dell'algoritmo di crittografia BitLocker per i dispositivi Autopilot](bitlocker.md).

![Esperienza utente con la modalità di distribuzione automatica di Windows Autopilot](images/self-deploy-welcome.png)

## <a name="requirements"></a>Requisiti

La modalità di distribuzione automatica usa l'hardware TPM 2,0 del dispositivo per autenticare il dispositivo nel tenant Azure AD di un'organizzazione. Pertanto, i dispositivi senza TPM 2,0 non possono essere utilizzati con questa modalità. I dispositivi devono supportare anche l'attestazione del dispositivo TPM. Tutti i nuovi dispositivi Windows devono soddisfare tali requisiti.

>[!IMPORTANT]
>Se si tenta di eseguire una distribuzione in modalità self-Deploying in un dispositivo che non dispone del supporto TPM 2,0 o in una macchina virtuale, il processo avrà esito negativo durante la verifica del dispositivo con un errore di timeout 0x800705B4 (i TPMs virtuali Hyper-V non sono supportati). Si noti anche che la finestra 10, versione 1903 o successiva, è necessaria per usare la modalità di distribuzione automatica a causa di problemi con l'attestazione del dispositivo TPM in Windows 10, versione 1809. Poiché Windows 10 Enterprise 2019 LTSC si basa su Windows 10 versione 1809, la modalità di distribuzione automatica non è supportata anche in Windows 10 Enterprise 2019 LTSC. Vedere [problemi noti di Windows Autopilot](known-issues.md) per esaminare altri errori noti e soluzioni.

È possibile visualizzare un logo specifico dell'organizzazione e il nome dell'organizzazione durante il processo Autopilot. A tale scopo, Azure AD la personalizzazione dell'azienda deve essere configurata con le immagini e il testo che si desidera visualizzare. Per informazioni dettagliate, vedere [Guida introduttiva: aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso in Azure ad](/azure/active-directory/fundamentals/customize-branding) . 

## <a name="step-by-step"></a>Procedura dettagliata

Per eseguire la distribuzione in modalità self-Deploying, è necessario completare i passaggi di preparazione seguenti:

1. Creare un profilo di Autopilot per la modalità di distribuzione automatica con le impostazioni desiderate. In Microsoft Intune, questa modalità viene scelta in modo esplicito durante la creazione del profilo. Non è possibile creare un profilo nel Microsoft Store per le aziende o il centro per i partner per la modalità di distribuzione automatica.
2. Se si usa Intune, creare un gruppo di dispositivi in Azure Active Directory e assegnare il profilo di Autopilot al gruppo. Verificare che il profilo sia stato assegnato al dispositivo prima di provare a distribuire il dispositivo.
3. Avviare il dispositivo, connetterlo a Wi-Fi, se necessario, quindi attendere il completamento del processo di provisioning.

## <a name="validation"></a>Convalida

Quando si usa Windows Autopilot per eseguire la distribuzione in modalità di distribuzione automatica, è necessario osservare l'esperienza dell'utente finale seguente:

-  Una volta stabilita la connessione a una rete, il profilo di Autopilot verrà scaricato.
- Se connesso a Ethernet e il profilo di Autopilot è configurato per ignorarli, non verranno visualizzate le pagine seguenti: lingua, impostazioni locali e layout della tastiera. In caso contrario, sono necessari passaggi manuali:
  -  Se in Windows 10 sono preinstallate più lingue, l'utente deve scegliere una lingua.
  -  L'utente deve selezionare le impostazioni locali e un layout di tastiera e, facoltativamente, un secondo layout di tastiera.
-  Se connesso tramite Ethernet, non è previsto alcun messaggio di rete. Se non è disponibile alcuna connessione Ethernet e la connessione Wi-Fi è incorporata, l'utente deve connettersi a una rete wireless.
-  Windows 10 verificherà la presenza di aggiornamenti OOBE critici e, se disponibili, verranno installati automaticamente (se necessario, riavviando).
-  Il dispositivo si unirà Azure Active Directory.
-  Dopo l'aggiunta Azure Active Directory, il dispositivo si registrerà in Intune o in altri servizi MDM configurati.
-  Verrà visualizzata la [pagina relativa allo stato della registrazione](enrollment-status.md) .
-  A seconda delle impostazioni del dispositivo distribuite, il dispositivo può:
  -  Rimanere nella schermata di accesso, in cui i membri dell'organizzazione possono accedere specificando le credenziali Azure AD.
  -  Accedere automaticamente come account locale per i dispositivi configurati come un chiosco multimediale o una firma digitale.

>[!NOTE]
>La distribuzione dei criteri EAS con la modalità di distribuzione automatica per le distribuzioni in modalità tutto schermo causerà un errore di accesso automatico alla funzionalità. 

Se i risultati osservati non corrispondono a queste aspettative, consultare la documentazione relativa alla [risoluzione dei problemi di Windows Autopilot](troubleshooting.md) .
