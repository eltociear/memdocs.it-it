---
title: Ripristino di Windows Autopilot
description: Il ripristino di Windows Autopilot riporta il dispositivo a uno stato pronto per l'azienda, consentendo all'utente successivo di eseguire l'accesso e ottenere la produttività in modo rapido e semplice.
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
ms.openlocfilehash: e084663527d48c83d42d426792da0bedddd35942
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907929"
---
# <a name="windows-autopilot-reset"></a>Ripristino di Windows Autopilot

- Si applica a: Windows 10, versione 1709 e successive (reimpostazione locale)
- Si applica a: Windows 10, versione 1809 e successive (reimpostazione remota)

La reimpostazione di Windows Autopilot rimuove i file personali, le app e le impostazioni e riapplica le impostazioni originali di un dispositivo, mantenendo la connessione di identità a Azure AD e la relativa connessione di gestione a Intune, in modo che il dispositivo sia ancora una volta pronto per l'uso. Il ripristino di Windows Autopilot riporta il dispositivo a uno stato pronto per l'azienda, consentendo all'utente successivo di eseguire l'accesso e ottenere la produttività in modo rapido e semplice. 

Il processo di reimpostazione di Windows Autopilot mantiene automaticamente le informazioni dal dispositivo esistente:
 
-   Impostare area, lingua e tastiera sui valori configurati in origine.
-   Dettagli della connessione Wi-Fi.
-   Pacchetti di provisioning applicati in precedenza al dispositivo, nonché un pacchetto di provisioning presente in un'unità USB quando viene avviato il processo di reimpostazione. 
-   Azure Active Directory l'appartenenza al dispositivo e le informazioni di registrazione MDM.

Il ripristino di Windows Autopilot impedisce all'utente di accedere al desktop fino a quando queste informazioni non vengono ripristinate, inclusa la nuova applicazione di eventuali pacchetti di provisioning.  Per i dispositivi registrati in un servizio MDM, il ripristino di Windows Autopilot viene bloccato anche fino a quando non viene completata una sincronizzazione MDM.  
Quando si usa la reimpostazione di Autopilot in un dispositivo, l'utente primario del dispositivo viene rimosso. L'utente successivo che accede dopo la reimpostazione verrà impostato come utente primario.
 
 
>[!NOTE]
>La reimpostazione di Autopilot non supporta i dispositivi Azure AD ibrido aggiunti.

## <a name="scenarios"></a>Scenari

Il ripristino di Windows Autopilot supporta due scenari:

-   Il [ripristino locale](#reset-devices-with-local-windows-autopilot-reset) è stato avviato dal personale IT o da altri amministratori dell'organizzazione.
-   Il [ripristino remoto](#reset-devices-with-remote-windows-autopilot-reset) è stato avviato in remoto dal personale IT tramite un servizio MDM, ad esempio Microsoft Intune.

I requisiti aggiuntivi e i dettagli di configurazione si applicano a ogni scenario. Per ulteriori informazioni, vedere i collegamenti dettagliati sopra.

## <a name="reset-devices-with-local-windows-autopilot-reset"></a>Ripristinare i dispositivi con la reimpostazione di Windows Autopilot locale 

**Si applica a: Windows 10, versione 1709 e successive**

Per eseguire questa attività, è necessario il ruolo di amministratore del servizio Intune.  Per altre informazioni, vedere [Aggiungere utenti e concedere autorizzazioni amministrative a Intune](/intune/users-add).

Gli amministratori IT possono eseguire un ripristino di Windows Autopilot locale per rimuovere rapidamente i file personali, le app e le impostazioni e ripristinare i dispositivi Windows 10 dalla schermata di blocco in qualsiasi momento e applicare le impostazioni originali e la registrazione di gestione (Azure Active Directory e la gestione dei dispositivi), in modo che i dispositivi siano pronti per l'uso. Con la reimpostazione di un autopilot locale, i dispositivi vengono restituiti a uno stato completamente configurato o approvato dall'IT.

Per abilitare la reimpostazione di Autopilot locale in Windows 10:

1. [Abilitare i criteri per la funzionalità](#enable-local-windows-autopilot-reset)
2. [Attivare un reset per ogni dispositivo](#trigger-local-windows-autopilot-reset)

### <a name="enable-local-windows-autopilot-reset"></a>Abilitare la reimpostazione di Windows Autopilot locale

Per abilitare una reimpostazione di Windows Autopilot locale, è necessario configurare il criterio **DisableAutomaticReDeploymentCredentials** . Questo criterio è documentato nei [criteri CSP](/windows/client-management/mdm/policy-csp-credentialproviders), **CredentialProviders/DisableAutomaticReDeploymentCredentials**. Per impostazione predefinita, Windows Autopilot locale è disabilitato. In questo modo si garantisce che la reimpostazione di un autopilot locale non venga attivata per errore.

È possibile impostare i criteri utilizzando uno di questi metodi:

- Provider MDM

    - Quando si usa Intune, è possibile creare un nuovo profilo di configurazione del dispositivo, specificando "Windows 10 o versione successiva" per la piattaforma, "restrizioni del dispositivo" per il tipo di profilo e "generale" per la categoria impostazioni.  L'impostazione di **ridistribuzione automatica** deve essere impostata su **Consenti**.  Distribuire questa impostazione in tutti i dispositivi in cui deve essere consentita una reimpostazione locale.
    - Se si usa un provider MDM diverso da Intune, vedere la documentazione del provider MDM per informazioni su come impostare questo criterio. 

- Progettazione configurazione Windows

    È possibile [utilizzare Progettazione configurazione Windows](/windows/configuration/provisioning-packages/provisioning-create-package) per impostare le **impostazioni di Runtime > criteri > CredentialProviders > DisableAutomaticReDeploymentCredentials** impostazione su 0, quindi creare un pacchetto di provisioning.

- Configurare l'app per i PC scolastici

    La versione più recente dell'app set up School PC supporta l'abilitazione della reimpostazione di Windows Autopilot locale.

### <a name="trigger-local-windows-autopilot-reset"></a>Attivare la reimpostazione di Windows Autopilot locale

L'esecuzione di un ripristino di Windows Autopilot locale è un processo in due passaggi: attivarlo e quindi eseguire l'autenticazione. Dopo aver eseguito questi due passaggi, è possibile consentire l'esecuzione del processo e, al termine, il dispositivo sarà pronto per l'uso. 

**Per attivare una reimpostazione di Autopilot locale**

1. Dalla schermata di blocco del dispositivo Windows, immettere la sequenza di tasti: **CTRL + ![ tasto Windows ](images/windows_glyph.png) + R**. 

    ![Premere CTRL + tasto Windows + R nella schermata di blocco di Windows](images/autopilot-reset-lockscreen.png)

    Verrà visualizzata una schermata di accesso personalizzata per la reimpostazione di Autopilot locale. La schermata serve due scopi:
    1. Confermare/verificare che l'utente finale abbia il diritto di attivare la reimpostazione di Autopilot locale
    2. Inviare una notifica all'utente nel caso in cui venga usato un pacchetto di provisioning, creato con progettazione configurazione di Windows, come parte del processo.

    ![Schermata di accesso personalizzata per la reimpostazione di Autopilot locale](images/autopilot-reset-customlogin.png)

2. Accedere con le credenziali dell'account amministratore. Se è stato creato un pacchetto di provisioning, collegare l'unità USB e attivare la reimpostazione di Autopilot locale.

    Dopo l'attivazione della reimpostazione di Autopilot locale, viene avviato il processo di reimpostazione. Al termine del provisioning, il dispositivo è nuovamente pronto per l'uso.

## <a name="reset-devices-with-remote-windows-autopilot-reset"></a>Ripristinare i dispositivi con la reimpostazione di Windows Autopilot remota

**Si applica a: Windows 10, versione 1809 o successiva**

Quando si esegue una reimpostazione di Windows Autopilot remota, è possibile usare un servizio MDM di questo tipo Microsoft Intune per avviare il processo di reimpostazione, evitando che il personale IT o altri amministratori possano visitare ogni computer per avviare il processo.

Per abilitare un dispositivo per un ripristino remoto di Windows Autopilot, il dispositivo deve essere gestito da MDM e Unito a Azure AD. Questa funzionalità non è supportata nei dispositivi registrati con la [modalità di distribuzione automatica Autopilot](self-deploying.md).

### <a name="triggering-a-remote-windows-autopilot-reset"></a>Attivazione di una reimpostazione di Windows Autopilot remota

Per attivare un ripristino remoto di Windows Autopilot tramite Intune, attenersi alla procedura seguente:
 
-   Passare alla scheda **dispositivi** nella console di Intune. 
-   Nella visualizzazione **tutti i dispositivi** selezionare i dispositivi di ripristino di destinazione e quindi fare clic su **altro** per visualizzare le azioni del dispositivo. 
-   Selezionare **Autopilot Reset** per avviare l'attività di reimpostazione. 

>[!NOTE]
>L'opzione di reimpostazione di Autopilot non verrà abilitata in Microsoft Intune per i dispositivi che non eseguono Windows 10 Build 17672 o versione successiva.

>[!IMPORTANT]
>La funzionalità per la reimpostazione di Autopilot resterà disattivata, **a meno che non** si reimposti il dispositivo con Autopilot (usando la funzionalità di reimpostazione aggiornata o Sysprep manuale del dispositivo).

Al termine della reimpostazione, il dispositivo è nuovamente pronto per l'uso.
 


## <a name="troubleshooting"></a>Risoluzione dei problemi

Per la reimpostazione di Windows Autopilot è necessario che [ambiente ripristino Windows (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) sia configurato e abilitato correttamente nel dispositivo. Se non è configurata e abilitata, verrà segnalato un errore, ad esempio `Error code: ERROR_NOT_SUPPORTED (0x80070032)` .

Per assicurarsi che WinRE sia abilitato, usare lo [ strumentoREAgentC.exe](/windows-hardware/manufacture/desktop/reagentc-command-line-options) per eseguire il comando seguente:

```
reagentc /enable
```

Se la reimpostazione di Windows Autopilot non riesce dopo l'abilitazione di WinRE o se non è possibile abilitare WinRE, contattare [supporto tecnico Microsoft](https://support.microsoft.com) per assistenza.