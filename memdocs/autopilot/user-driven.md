---
title: Modalità basata sull'utente di Windows Autopilot
description: Con la modalità basata sull'utente di Windows Autopilot è possibile configurare i dispositivi per la distribuzione in uno stato pronto all'uso senza richiedere assistenza al personale IT.
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
ms.openlocfilehash: b2c9d3b8741fdae30b42aede8f5c7443e35d8bc7
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251960"
---
# <a name="windows-autopilot-user-driven-mode"></a>Modalità definita dall'utente di Windows Autopilot

**Si applica a: Windows 10, versione 1809 o successiva**

La modalità basata sull'utente di Windows Autopilot consente di configurare nuovi dispositivi Windows 10 per trasformarli automaticamente dallo stato della Factory a uno stato pronto per l'utilizzo. Questo processo non richiede che il personale IT tocchi il dispositivo.

Il processo è semplice, in modo che chiunque possa completarlo. I dispositivi possono essere spediti o distribuiti direttamente all'utente finale con semplici istruzioni:

1. Eseguire l'unboxing del dispositivo, collegarlo e accenderlo.
2. Scegliere una lingua (obbligatoria solo quando sono installate più lingue), le impostazioni locali e la tastiera.
3. Connetterlo a una rete wireless o cablata con accesso a Internet. Se si usa wireless, l'utente deve stabilire il collegamento Wi-Fi. 
4. Specificare l'indirizzo di posta elettronica e la password per l'account dell'organizzazione.

Il resto del processo è automatizzato, come il dispositivo:
1. Aggiunge l'organizzazione.
2. Registrazioni in Intune o in un altro servizio MDM
3. Viene configurato come definito dall'organizzazione.

Eventuali richieste aggiuntive durante la configurazione guidata (OOBE) possono essere evitate. vedere [configurazione dei profili di Autopilot](profiles.md) per le opzioni disponibili.

La modalità basata sull'utente di Windows Autopilot supporta i dispositivi Azure Active Directory e ibridi Azure Active Directory aggiunti. Per altre informazioni su queste due opzioni di join, vedere [che cos'è un'identità del dispositivo](https://docs.microsoft.com/azure/active-directory/devices/overview).

Il flusso del processo completato durante il processo guidato dall'utente è il seguente:

1. Dopo la connessione a una rete, il dispositivo Scarica un profilo di Windows Autopilot. Il profilo definisce le impostazioni usate per il dispositivo. Ad esempio, definire i prompt eliminati durante la configurazione guidata.
2. Windows 10 Verifica la presenza di aggiornamenti OOBE critici. Se sono disponibili aggiornamenti, vengono installati automaticamente (se necessario, il riavvio).
3. All'utente vengono richieste le credenziali Azure Active Directory. Questa esperienza utente personalizzata Mostra il nome del tenant, il logo e il testo di accesso Azure AD.
4.  Il dispositivo si unisce Azure Active Directory o Active Directory, a seconda delle impostazioni del profilo di Windows Autopilot.
5. Il dispositivo viene registrato in Intune o in altri servizi MDM configurati. A seconda delle esigenze dell'organizzazione, questa registrazione si verifica:
    - durante il processo di join Azure Active Directory usando la registrazione automatica MDM
    - o prima del processo di join Active Directory.
6. Se configurata, verrà visualizzata la [pagina relativa allo stato della registrazione](enrollment-status.md) (ESP).
7. Al termine delle attività di configurazione del dispositivo, l'utente ha effettuato l'accesso a Windows 10 usando le credenziali fornite in precedenza. Se il dispositivo viene riavviato durante il processo ESP del dispositivo, l'utente deve immettere nuovamente le credenziali perché questi dettagli non vengono salvati in modo permanente tra i riavvii.
8. Dopo l'accesso, viene visualizzata la pagina relativa allo stato della registrazione per le attività di configurazione destinate agli utenti.

Se vengono rilevati problemi durante questo processo, vedere la documentazione relativa alla [risoluzione dei problemi di Windows Autopilot](troubleshooting.md) .

Per ulteriori informazioni sulle opzioni di join disponibili, vedere le sezioni seguenti:

- [Azure Active Directory join](#user-driven-mode-for-azure-active-directory-join) è disponibile se non è necessario che i dispositivi siano aggiunti a un dominio Active Directory locale.
- [Hybrid Azure Active Directory join](#user-driven-mode-for-hybrid-azure-active-directory-join) è disponibile per i dispositivi che devono essere aggiunti sia a Azure Active Directory sia al dominio Active Directory locale.

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Modalità guidata dall'utente per l'aggiunta di Azure Active Directory

Per completare una distribuzione basata sull'utente utilizzando Windows Autopilot, attenersi alla seguente procedura di preparazione:

1. Assicurarsi che gli utenti che eseguiranno le distribuzioni in modalità basata sull'utente possano aggiungere dispositivi ai Azure Active Directory. Per ulteriori informazioni, vedere [configurare le impostazioni del dispositivo](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings) nella documentazione di Azure Active Directory.
2. Creare un profilo di Autopilot per la modalità guidata dall'utente con le impostazioni desiderate. In Microsoft Intune, questa modalità viene scelta in modo esplicito durante la creazione del profilo. Con Microsoft Store for business e partner Center, la modalità basata sull'utente è l'impostazione predefinita e non deve essere selezionata.
3. Se si usa Intune, creare un gruppo di dispositivi in Azure Active Directory e assegnare il profilo di Autopilot al gruppo.

Per ogni dispositivo che verrà distribuito usando la distribuzione guidata dall'utente, sono necessari i passaggi aggiuntivi seguenti:

- Verificare che il dispositivo sia stato aggiunto a Windows Autopilot. L'aggiunta di un dispositivo a Windows Autopilot può essere eseguita in due modi:
  - Automaticamente da un OEM o un partner al momento dell'acquisto del dispositivo
  - Raccolta manuale come descritto in [aggiunta di dispositivi a Windows Autopilot](add-devices.md).
- Verificare che sia stato assegnato un profilo di Autopilot al dispositivo:
 - Se si usa Intune e Azure Active Directory gruppi di dispositivi dinamici, questa assegnazione può essere eseguita automaticamente.
 - Se si usa Intune e Azure Active Directory gruppi di dispositivi statici, aggiungere manualmente il dispositivo al gruppo di dispositivi.
 - Se si usano altri metodi, ad esempio Microsoft Store per le aziende o il centro per i partner, assegnare manualmente un profilo di Autopilot al dispositivo.


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>Modalità guidata dall'utente per il join ibrido Azure Active Directory

Windows Autopilot richiede che i dispositivi siano Azure Active Directory Uniti in join. Se si dispone di un ambiente di Active Directory locale, è possibile aggiungere i dispositivi al dominio locale. Per aggiungere i dispositivi, è necessario configurare i dispositivi Autopilot per essere [aggiunti a un ibrido per Azure Active Directory (Azure ad)](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

### <a name="requirements"></a>Requisiti

Per eseguire una distribuzione ibrida Azure AD aggiunta dall'utente tramite Windows Autopilot:

- È necessario creare un profilo di Windows Autopilot per la modalità guidata dall'utente e 
 - **Azure ad ibrido** join deve essere specificato come opzione selezionata in **join per Azure ad come** nel profilo di Autopilot.
- Se si usa Intune, è necessario che esista un gruppo di dispositivi in Azure Active Directory con il profilo di Windows Autopilot assegnato a tale gruppo.
- Il dispositivo deve eseguire Windows 10, versione 1809 o successiva.
- Il dispositivo deve avere accesso a un controller di dominio Active Directory. Deve essere connessa alla rete dell'organizzazione. Deve essere in grado di risolvere i record DNS per il dominio di Active Directory e il controller di dominio AD. Deve essere in grado di comunicare con il controller di dominio per autenticare l'utente.
- Il dispositivo deve essere in grado di accedere a Internet, seguendo i [requisiti di rete di Windows Autopilot documentati](networking-requirements.md).
- È necessario installare Intune Connector per Active Directory.
 - Nota: Intune Connector eseguirà un join AD locale. Pertanto, gli utenti non necessitano dell'autorizzazione di AD-join locale. Si presuppone che il connettore sia [configurato per eseguire questa azione](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) per conto dell'utente. 
- Se si usa un proxy, è necessario abilitare e configurare l'opzione delle impostazioni proxy WPAD.

**Azure ad aggiunta al dispositivo**: il processo di join di Azure ad ibrido usa il contesto di sistema per eseguire il join del Azure ad del dispositivo. Non è influenzato dalle impostazioni delle autorizzazioni di Azure AD join basate sull'utente. Tutti gli utenti possono aggiungere dispositivi a Azure AD per impostazione predefinita.

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>Modalità guidata dall'utente per l'aggiunta di Azure Active Directory ibrido con supporto VPN

I dispositivi aggiunti a Active Directory richiedono la connettività a un controller di dominio Active Directory per molte attività. Queste attività includono l'accesso utente (convalida delle credenziali dell'utente) e Criteri di gruppo applicazione. Di conseguenza, il processo di Aggiunta ad Azure AD ibrido basato sull'utente di Windows Autopilot consente di verificare che il dispositivo sia in grado di contattare un controller di dominio Active Directory eseguendo il ping del controller di dominio.

Con l'aggiunta del supporto VPN per questo scenario, è possibile configurare il processo di Aggiunta ad Azure AD ibrido per ignorare il controllo della connettività. Questa operazione non elimina la necessità di comunicare con un controller di dominio Active Directory. Al contrario, per consentire la connessione alla rete dell'organizzazione, Intune recapita la configurazione VPN necessaria prima che l'utente tenti di accedere a Windows. 


### <a name="requirements"></a>Requisiti

Per Aggiunta ad Azure AD ibrido con supporto VPN, si applicano i seguenti requisiti aggiuntivi:

- Una versione supportata di Windows 10:
 - Aggiornamento cumulativo di Windows 10 1903 + 10 dicembre (KB4530684, build del sistema operativo 18362,535) o versione successiva 
 - Aggiornamento cumulativo di Windows 10 1909 + 10 dicembre (KB4530684, build del sistema operativo 18363,535) o versione successiva 
 - Windows 10 2004 o versione successiva 
- Abilitare il nuovo interruttore "Ignora controllo connettività dominio" nel profilo Aggiunta ad Azure AD ibrido Autopilot.
- Una configurazione VPN che:
  - può essere distribuito con Intune e consente all'utente di stabilire manualmente una connessione VPN dalla schermata di accesso di Windows oppure
  - uno che stabilisce automaticamente una connessione VPN in base alle esigenze. 

La configurazione VPN specifica richiesta dipende dal software VPN e dall'autenticazione in uso. Per le soluzioni VPN di terze parti (non Microsoft), ciò comporta in genere la distribuzione di un'app Win32 (contenente il software client VPN e le informazioni di connessione specifiche, ad esempio i nomi host dell'endpoint VPN) tramite le estensioni di gestione di Intune. Consultare la documentazione del provider VPN per i dettagli di configurazione specifici del provider.

> [!NOTE]
> I requisiti della VPN non sono specifici di Windows Autopilot. Ad esempio, se è già stata implementata una configurazione VPN per abilitare la reimpostazione della password remota, in cui un utente deve accedere a Windows con una nuova password quando non è presente nella rete dell'organizzazione, è possibile usare la stessa configurazione con Windows Autopilot. Dopo che l'utente ha eseguito l'accesso per memorizzare nella cache le credenziali, i tentativi di accesso successivi non necessitano di connettività poiché è possibile usare le credenziali memorizzate nella cache. 

Nei casi in cui l'autenticazione del certificato è richiesta dal software VPN, il certificato del computer necessario deve essere distribuito anche tramite Intune. Questa distribuzione può essere eseguita usando le funzionalità di registrazione dei certificati di Intune, destinando i profili certificato al dispositivo.

I certificati utente non sono supportati perché non possono essere distribuiti fino a quando l'utente non esegue l'accesso. Inoltre, poiché non sono installate fino a quando l'utente non esegue l'accesso, i plug-in VPN non Microsoft UWP recapitati da Windows Store non sono supportati.

### <a name="validation"></a>Convalida

Prima di provare un join ibrido Azure AD usando la VPN, è importante verificare che sia possibile eseguire un processo di Aggiunta ad Azure AD ibrido basato sull'utente sulla rete dell'organizzazione. Questa conferma semplifica la risoluzione dei problemi verificando che il processo principale funzioni prima di aggiungere la configurazione aggiuntiva della VPN necessaria.

Successivamente, verificare che la configurazione della VPN (app Win32, certificati e altri requisiti) possa essere distribuita con Intune a un dispositivo esistente già ibrido Azure AD Unito. Alcuni client VPN, ad esempio, creano una connessione VPN per computer come parte del processo di installazione. Quindi, è possibile convalidare la configurazione usando passaggi simili ai seguenti:

- Da PowerShell verificare che sia stata creata almeno una connessione VPN per computer usando il comando "Get-VpnConnection-AllUserConnection".
- Tentativo di avvio manuale della connessione VPN usando il comando: RASDIAL.EXE "ConnectionName"
- Disconnettersi e verificare che l'icona "connessione VPN" possa essere visualizzata nella pagina di accesso di Windows.
- Spostare il dispositivo dalla rete aziendale e provare a stabilire la connessione usando l'icona nella pagina di accesso di Windows. Accedere a un account che non dispone di credenziali memorizzate nella cache.

Per le configurazioni VPN che si connettono automaticamente, i passaggi di convalida potrebbero essere diversi.

> [!NOTE]
> Per questo scenario è possibile usare Always On VPN. Per ulteriori informazioni, vedere la documentazione relativa alla [distribuzione di always on VPN](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) . Si noti che Intune non è ancora in grado di distribuire il profilo VPN per computer necessario. 

Per convalidare il processo, verificare che sia stato installato l'aggiornamento cumulativo di Windows 10 necessario in Windows 10 1903 o Windows 10 1909. È possibile installare manualmente l'aggiornamento durante la configurazione guidata scaricando prima l'ultima versione cumulativa da https://catalog.update.microsoft.com . A tale scopo, seguire questa procedura:

1. Premere MAIUSC + F10 per aprire un prompt dei comandi.
2. Inserire una chiave USB contenente l'aggiornamento scaricato.
3. Installare l'aggiornamento usando il comando (sostituendo il nome file reale): WUSA.EXE <filename> . msu/quiet
4. Riavviare il computer utilizzando il comando: shutdown.exe/r/t 0

In alternativa, è possibile avviare Windows Update per installare gli aggiornamenti più recenti:

1. Premere MAIUSC + F10 per aprire un prompt dei comandi.
2. Eseguire il comando "Start MS-Settings:"
3. Passare al nodo "Aggiorna & sicurezza" e verificare la disponibilità di aggiornamenti.
4. Riavviare il computer dopo l'installazione degli aggiornamenti.

### <a name="step-by-step-instructions"></a>Istruzioni dettagliate

Vedere [distribuire dispositivi ibridi Azure ad aggiunti con Intune e Windows Autopilot](https://docs.microsoft.com/intune/windows-autopilot-hybrid).



