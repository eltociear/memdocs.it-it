---
title: Modalità basata sull'utente di Windows Autopilot
description: La modalità basata sull'utente di Windows Autopilot consente di distribuire i dispositivi in uno stato pronto per l'uso senza richiedere assistenza al personale IT.
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
ms.openlocfilehash: b5e7c88272f8da386d25e7e7bca1973026f4407a
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756535"
---
# <a name="windows-autopilot-user-driven-mode"></a>Modalità definita dall'utente di Windows Autopilot

**Si applica a: Windows 10, versione 1809 o successiva**

La modalità basata sull'utente di Windows Autopilot è progettata per consentire la trasformazione dei nuovi dispositivi Windows 10 dallo stato iniziale della fabbrica in uno stato pronto all'uso senza che il personale IT possa toccare il dispositivo.  Il processo è progettato per essere semplice, in modo che chiunque possa completarlo, abilitando la distribuzione o la distribuzione dei dispositivi direttamente all'utente finale con semplici istruzioni:

- Eseguire l'unboxing del dispositivo, collegarlo e accenderlo.
- Scegliere una lingua (obbligatoria solo quando sono installate più lingue), le impostazioni locali e la tastiera.
- Connetterlo a una rete wireless o cablata con accesso a Internet.  Se si usa wireless, l'utente deve stabilire il collegamento Wi-Fi.  
- Specificare l'indirizzo di posta elettronica e la password per l'account dell'organizzazione.

Al termine di questi semplici passaggi, il resto del processo viene automatizzato, con il dispositivo aggiunto all'organizzazione, registrato in Intune (o un altro servizio MDM) e completamente configurato come definito dall'organizzazione.  Eventuali richieste aggiuntive durante la configurazione guidata (OOBE) possono essere evitate. vedere [configurazione dei profili di Autopilot](profiles.md) per le opzioni disponibili.

La modalità basata sull'utente di Windows Autopilot supporta i dispositivi Azure Active Directory e ibridi Azure Active Directory aggiunti.  Per altre informazioni su queste due opzioni di join, vedere [che cos'è un'identità del dispositivo](https://docs.microsoft.com/azure/active-directory/devices/overview).

Dal punto di vista del flusso del processo, le attività eseguite durante il processo guidato dall'utente sono le seguenti:

- Una volta stabilita la connessione a una rete, il dispositivo Scarica un profilo di Windows Autopilot specificando le impostazioni da usare, ad esempio le richieste durante la configurazione guidata che devono essere evitate.
- Windows 10 verificherà la presenza di aggiornamenti OOBE critici. Se gli aggiornamenti sono disponibili, verranno installati automaticamente (se necessario, il riavvio).
- All'utente verrà richiesto di Azure Active Directory credenziali, con un'esperienza utente personalizzata che mostra il nome del tenant Azure AD, il logo e il testo di accesso.
- Il dispositivo si unirà Azure Active Directory o Active Directory, in base alle impostazioni del profilo di Windows Autopilot.
- Il dispositivo eseguirà la registrazione in Intune (o in altri servizi MDM configurati).  Questa registrazione viene eseguita come parte del processo di join Azure Active Directory tramite la registrazione automatica MDM o prima del processo di join Active Directory, in base alle esigenze.
- Se configurata, verrà visualizzata la [pagina relativa allo stato della registrazione](enrollment-status.md) (ESP).
- Una volta completate le attività di configurazione del dispositivo, l'utente verrà connesso a Windows 10 con le credenziali fornite in precedenza.  Nota: se il dispositivo viene riavviato durante il processo ESP del dispositivo, l'utente dovrà immettere nuovamente le credenziali perché questi dettagli non vengono salvati in modo permanente tra i riavvii.
- Una volta effettuato l'accesso, la pagina relativa allo stato della registrazione verrà visualizzata di nuovo per le attività di configurazione di destinazione dell'utente.

Se vengono rilevati problemi durante questo processo, vedere la documentazione relativa alla [risoluzione dei problemi di Windows Autopilot](troubleshooting.md) .

Per ulteriori informazioni sulle opzioni di join disponibili, vedere le sezioni seguenti:

- [Azure Active Directory join](#user-driven-mode-for-azure-active-directory-join) è disponibile se non è necessario che i dispositivi siano aggiunti a un dominio Active Directory locale.
- [Hybrid Azure Active Directory join](#user-driven-mode-for-hybrid-azure-active-directory-join) è disponibile per i dispositivi che devono essere aggiunti sia a Azure Active Directory sia al dominio Active Directory locale.

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Modalità guidata dall'utente per l'aggiunta di Azure Active Directory

Per eseguire una distribuzione basata sull'utente mediante Windows Autopilot, è necessario completare i passaggi di preparazione seguenti:

- Assicurarsi che gli utenti che eseguiranno le distribuzioni in modalità basata sull'utente siano in grado di aggiungere dispositivi a Azure Active Directory.  Per ulteriori informazioni, vedere [configurare le impostazioni del dispositivo](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings) nella documentazione di Azure Active Directory.
- Creare un profilo di Autopilot per la modalità guidata dall'utente con le impostazioni desiderate.  In Microsoft Intune, questa modalità viene scelta in modo esplicito durante la creazione del profilo. Con Microsoft Store for Business and Partner Center, la modalità guidata dall'utente è quella predefinita e non è necessario selezionarla.
- Se si usa Intune, creare un gruppo di dispositivi in Azure Active Directory e assegnare il profilo di Autopilot al gruppo.

Per ogni dispositivo che verrà distribuito usando la distribuzione guidata dall'utente, sono necessari i passaggi aggiuntivi seguenti:

- Verificare che il dispositivo sia stato aggiunto a Windows Autopilot.  Questa aggiunta può essere eseguita automaticamente da un OEM o da un partner al momento dell'acquisto del dispositivo oppure può essere eseguita tramite un processo di raccolta manuale in un secondo momento.  Per ulteriori informazioni, vedere [aggiunta di dispositivi a Windows Autopilot](add-devices.md).
- Verificare che sia stato assegnato un profilo di Autopilot al dispositivo:
  - Se si usa Intune e Azure Active Directory gruppi di dispositivi dinamici, questa assegnazione può essere eseguita automaticamente.
  - Se si usa Intune e Azure Active Directory gruppi di dispositivi statici, aggiungere manualmente il dispositivo al gruppo di dispositivi.
  - Se si usano altri metodi, ad esempio Microsoft Store per le aziende o il centro per i partner, assegnare manualmente un profilo di Autopilot al dispositivo.


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>Modalità guidata dall'utente per il join ibrido Azure Active Directory

Windows Autopilot richiede che i dispositivi siano Azure Active Directory Uniti in join. Se si dispone di un ambiente di Active Directory locale e si desidera aggiungere i dispositivi al dominio locale, è possibile configurare i dispositivi Autopilot in modo che siano [aggiunti al Azure Active Directory (Azure ad)](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).  

### <a name="requirements"></a>Requisiti

Per eseguire una distribuzione ibrida Azure AD aggiunta dall'utente tramite Windows Autopilot:

- È necessario creare un profilo di Windows Autopilot per la modalità guidata dall'utente e 
  - **Azure ad ibrido** join deve essere specificato come opzione selezionata in **join per Azure ad come** nel profilo di Autopilot.
- Se si usa Intune, è necessario che esista un gruppo di dispositivi in Azure Active Directory con il profilo di Windows Autopilot assegnato a tale gruppo.
- Il dispositivo deve eseguire Windows 10, versione 1809 o successiva.
- Il dispositivo deve essere in grado di accedere a un controller di dominio Active Directory, quindi deve essere connesso alla rete dell'organizzazione (dove può risolvere i record DNS per il dominio di Active Directory e il controller di dominio di Active Directory e comunica con il controller di dominio per autenticare l'utente).
- Il dispositivo deve essere in grado di accedere a Internet, seguendo i [requisiti di rete di Windows Autopilot documentati](windows-autopilot-requirements.md).
- È necessario installare Intune Connector per Active Directory.
  - Nota: Intune Connector eseguirà un aggiunta AD Active Directory locale, pertanto gli utenti non necessitano dell'autorizzazione AD-join locale, presupponendo che il connettore sia [configurato per eseguire questa azione](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) per conto dell'utente. 
- Se si usa un proxy, è necessario abilitare e configurare l'opzione delle impostazioni proxy WPAD.

**Azure ad aggiunta al dispositivo**: il processo di join di Azure ad ibrido usa il contesto di sistema per eseguire il join del Azure ad del dispositivo, pertanto non è influenzato dalle impostazioni di autorizzazione del join Azure ad basate sull'utente. Inoltre, tutti gli utenti sono abilitati per aggiungere dispositivi a Azure AD per impostazione predefinita.

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>Modalità guidata dall'utente per l'aggiunta di Azure Active Directory ibrido con supporto VPN

I dispositivi aggiunti a Active Directory richiedono la connettività a un controller di dominio Active Directory per un'ampia gamma di attività, ad esempio l'accesso utente (convalida delle credenziali dell'utente) e la Criteri di gruppo applicazione.  Di conseguenza, il processo di Aggiunta ad Azure AD ibrido basato sull'utente di Windows Autopilot consente di verificare che il dispositivo sia in grado di contattare un controller di dominio Active Directory eseguendo il ping del controller di dominio.

Con l'aggiunta del supporto VPN per questo scenario, è ora possibile specificare di ignorare il controllo della connettività durante l'Aggiunta ad Azure AD ibrido.  Questa operazione non elimina la necessità di comunicare con un controller di dominio Active Directory, ma consente al dispositivo di essere prima preparato con una configurazione VPN necessaria fornita tramite Intune prima che l'utente tenti di accedere a Windows, consentendo la connettività alla rete dell'organizzazione.

### <a name="requirements"></a>Requisiti

Per Aggiunta ad Azure AD ibrido con supporto VPN, si applicano i seguenti requisiti aggiuntivi:

- Una versione supportata di Windows 10:
  - Aggiornamento cumulativo di Windows 10 1903 + 10 dicembre (KB4530684, build del sistema operativo 18362,535) o versione successiva 
  - Aggiornamento cumulativo di Windows 10 1909 + 10 dicembre (KB4530684, build del sistema operativo 18363,535) o versione successiva  
  - Windows 10 2004 o versione successiva 
- Abilitare il nuovo interruttore "Ignora controllo connettività dominio" nel profilo Aggiunta ad Azure AD ibrido Autopilot.
- Una configurazione VPN che può essere distribuita tramite Intune che consente all'utente di stabilire manualmente una connessione VPN dalla schermata di accesso di Windows o una che stabilisce automaticamente una connessione VPN in base alle esigenze.  

La configurazione VPN specifica richiesta dipende dal software VPN e dall'autenticazione in uso.  Per le soluzioni VPN di terze parti (non Microsoft), ciò comporta in genere la distribuzione di un'app Win32 (contenente il software client VPN, nonché le informazioni di connessione specifiche, ad esempio i nomi host dell'endpoint VPN) tramite le estensioni di gestione di Intune.  Consultare la documentazione del provider VPN per i dettagli di configurazione specifici del provider.

> [!NOTE]
> I requisiti VPN non sono specifici di Windows Autopilot. Ad esempio, se è già stata implementata una configurazione VPN per abilitare la reimpostazione della password remota, in cui un utente deve accedere a Windows con una nuova password quando non è presente nella rete dell'organizzazione, è possibile usare la stessa configurazione con Windows Autopilot.  Dopo che l'utente ha eseguito l'accesso per memorizzare nella cache le credenziali, i tentativi di accesso successivi non necessitano di connettività poiché è possibile usare le credenziali memorizzate nella cache. 

Nei casi in cui l'autenticazione del certificato è richiesta dal software VPN, il certificato del computer necessario deve essere distribuito anche tramite Intune.  Questa distribuzione può essere eseguita usando le funzionalità di registrazione dei certificati di Intune, destinando i profili certificato al dispositivo.

Si noti che i certificati utente non sono supportati perché questi certificati non possono essere distribuiti fino a quando l'utente non esegue l'accesso.  Inoltre, anche i plug-in VPN non Microsoft UWP recapitati da Windows Store non sono supportati perché questi plug-in non vengono installati finché l'utente non esegue l'accesso.

### <a name="validation"></a>Convalida

Prima di provare un join ibrido Azure AD usando la VPN, è importante prima di tutto verificare che sia possibile eseguire un processo di Aggiunta ad Azure AD ibrido basato sull'utente sulla rete dell'organizzazione, prima di aggiungere i requisiti aggiuntivi descritti di seguito.  Questo semplifica la risoluzione dei problemi verificando che il processo principale funzioni correttamente prima di aggiungere la configurazione aggiuntiva della VPN necessaria.

Successivamente, verificare che la configurazione della VPN (app Win32, certificati e altri requisiti) possa essere distribuita tramite Intune a un dispositivo esistente già ibrido Azure AD Unito.  Alcuni client VPN, ad esempio, creano una connessione VPN per computer come parte del processo di installazione, quindi è possibile convalidare la configurazione usando i passaggi seguenti:

- Da PowerShell verificare che sia stata creata almeno una connessione VPN per computer usando il comando "Get-VpnConnection-AllUserConnection".
- Tentativo di avvio manuale della connessione VPN usando il comando: RASDIAL.EXE "ConnectionName"
- Disconnettersi e verificare che l'icona "connessione VPN" possa essere visualizzata nella pagina di accesso di Windows.
- Spostare il dispositivo dalla rete aziendale e tentare di stabilire la connessione utilizzando l'icona nella pagina di accesso di Windows, effettuando l'accesso a un account che non dispone di credenziali memorizzate nella cache.

Per le configurazioni VPN che si connettono automaticamente, i passaggi di convalida potrebbero essere diversi.

> [!NOTE]
> Per questo scenario è possibile usare Always On VPN.  Per ulteriori informazioni, vedere la documentazione sulla [distribuzione di always on VPN](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) .  Si noti che Intune non è ancora in grado di distribuire il profilo VPN per computer necessario. 

Per convalidare il processo end-to-end, verificare che sia stato installato l'aggiornamento cumulativo di Windows 10 necessario in Windows 10 1903 o Windows 10 1909. Questo aggiornamento può essere eseguito manualmente durante la configurazione guidata scaricando prima l'ultima versione cumulativa da https://catalog.update.microsoft.com e quindi installarla manualmente:

- Premere MAIUSC + F10 per aprire un prompt dei comandi.
- Inserire una chiave USB contenente l'aggiornamento scaricato.
- Installare l'aggiornamento usando il comando (sostituendo il nome file reale): WUSA.EXE <filename> . msu/quiet
- Riavviare il computer utilizzando il comando: shutdown.exe/r/t 0

In alternativa, è possibile richiamare Windows Update per installare gli aggiornamenti più recenti tramite questo processo:

- Premere MAIUSC + F10 per aprire un prompt dei comandi.
- Eseguire il comando "Start MS-Settings:"
- Passare al nodo "Aggiorna & sicurezza" e verificare la disponibilità di aggiornamenti.
- Riavviare il computer dopo l'installazione degli aggiornamenti.

### <a name="step-by-step-instructions"></a>Istruzioni dettagliate

Vedere [distribuire dispositivi ibridi Azure ad aggiunti con Intune e Windows Autopilot](https://docs.microsoft.com/intune/windows-autopilot-hybrid).



