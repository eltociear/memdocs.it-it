---
title: Distribuzione di Windows Autopilot per il guanto bianco
description: Distribuzione di Windows Autopilot per il guanto bianco
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune, pre-provisioning
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itproF
manager: laurawi
ms.audience: itpro
author: greg-lindsay
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: e08c69412fef2149d71c684fed6b900b88c9cb60
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756517"
---
# <a name="windows-autopilot-for-white-glove-deployment"></a>Distribuzione di Windows Autopilot per il guanto bianco

**Si applica a: Windows 10, versione 1903** 

Windows Autopilot consente alle organizzazioni di effettuare facilmente il provisioning di nuovi dispositivi, sfruttando le immagini OEM preinstallate e i driver con un processo semplice che può essere eseguito dall'utente finale per aiutare a rendere il dispositivo pronto per l'azienda.

 ![OEM](images/wg01.png)

Windows Autopilot può inoltre fornire un servizio di <I>guanto bianco</I> che consente ai partner o al personale IT di eseguire il pre-provisioning di un PC Windows 10 in modo che sia completamente configurato e pronto per l'azienda. Dal punto di vista dell'utente finale, l'esperienza basata sull'utente di Windows Autopilot è invariata, ma lo stato del dispositivo con provisioning completo è più veloce.

Con **Windows Autopilot per la distribuzione del guanto bianco**, il processo di provisioning è suddiviso. Le porzioni che richiedono molto tempo vengono eseguite da IT, partner o OEM. L'utente finale completa semplicemente alcune impostazioni e criteri necessari per poter iniziare a usare il dispositivo.

 ![OEM](images/wg02.png)

Abilitata con Microsoft Intune in Windows 10, versione 1903 e versioni successive, le funzionalità di distribuzione dei guanti bianchi si basano sugli [scenari esistenti basati sugli utenti](user-driven.md)di Windows Autopilot, supportando la modalità basata sull'utente per Azure Active Directory join e la modalità basata sull'utente per gli scenari ibridi Azure Active Directory join.

## <a name="prerequisites"></a>Prerequisiti

Oltre ai [requisiti di Windows Autopilot](windows-autopilot-requirements.md), Windows Autopilot per la distribuzione del guanto bianco aggiunge quanto segue:

- È necessario Windows 10, versione 1903 o successiva.
- Una sottoscrizione di Intune.
- Dispositivi fisici che supportano il TPM 2,0 e l'attestazione del dispositivo; le macchine virtuali non sono supportate.  Il processo di provisioning del guanto bianco sfrutta le funzionalità di distribuzione automatica di Windows Autopilot, quindi i requisiti TPM 2,0.
- Dispositivi fisici con connettività Ethernet; La connettività Wi-Fi non è supportata a causa della necessità di scegliere una lingua, impostazioni locali e una tastiera per eseguire tale connessione Wi-Fi. Questa operazione in un processo di pre-provisioning può impedire all'utente di scegliere la lingua, le impostazioni locali e la tastiera quando ricevono il dispositivo.

>[!IMPORTANT]
>Poiché l'OEM o il fornitore esegue il processo di guanto bianco, questo <u>non richiede l'accesso a un'infrastruttura di dominio locale dell'utente finale</u>. Si tratta di un tipico scenario ibrido Azure AD Unito perché il riavvio del dispositivo è stato posticipato. Il dispositivo viene risigillato prima del momento in cui è prevista la connettività a un controller di dominio e la rete di dominio viene contattata quando il dispositivo viene sbloccato in locale dall'utente finale.

## <a name="preparation"></a>Preparazione

I dispositivi di cui è stato effettuato il provisioning per il guanto bianco sono registrati per Autopilot tramite il normale processo di registrazione. 

Per essere pronti a provare Windows Autopilot per la distribuzione di guanto bianco, assicurarsi di poter usare in primo luogo i possibili scenari basati sugli utenti di Windows Autopilot esistenti:

- Aggiunta Azure AD guidata dall'utente.  I dispositivi possono essere distribuiti usando Windows Autopilot e aggiunti a un tenant di Azure Active Directory.
- Basato sull'utente con Azure AD ibrido join.  I dispositivi possono essere distribuiti usando Windows Autopilot e aggiunti a un dominio di Active Directory locale, quindi registrati con Azure Active Directory per abilitare le funzionalità di Azure AD ibrido join.

Se non è possibile completare questi scenari, Windows Autopilot per la distribuzione del guanto bianco avrà esito negativo perché si basa su questi scenari.

Per abilitare la distribuzione del guanto bianco, un'impostazione del profilo di Autopilot aggiuntiva deve essere configurata dal cliente o dall'amministratore IT tramite il proprio account di Intune, prima di iniziare il processo del guanto bianco nella struttura del servizio di provisioning:

 ![Consenti guanto bianco](images/allow-white-glove-oobe.png)

Il processo di pre-provisioning per la distribuzione di Windows Autopilot per il guanto bianco applicherà tutti i criteri destinati ai dispositivi da Intune.  Che include i certificati, i modelli di sicurezza, le impostazioni, le app e altro ancora, tutto ciò che è destinato al dispositivo.  Verranno inoltre installate eventuali app (Win32 o LOB) configurate per l'installazione nel contesto di dispositivo e destinate all'utente che è stato pre-assegnato al dispositivo Autopilot. Assicurarsi di non specificare come destinazione le app Win32 e LOB nello stesso dispositivo. 

> [!NOTE]
> Selezionare la modalità del linguaggio come utente specificato nei profili di Autopilot per garantire l'accesso semplice alla modalità di provisioning del guanto bianco. La fase White Glove tecnici installerà tutte le app destinate al dispositivo, oltre a tutte le app del contesto di dispositivo destinate agli utenti, destinate all'utente assegnato. Se non è stato assegnato alcun utente, installerà solo le app destinate al dispositivo. Altri criteri di destinazione utente non verranno applicati fino a quando l'utente non accede al dispositivo. Per verificare questi comportamenti, assicurarsi di creare le app e i criteri appropriati destinati a dispositivi e utenti.

## <a name="scenarios"></a>Scenari

Windows Autopilot per la distribuzione del guanto bianco supporta due scenari distinti:
- Distribuzioni basate sugli utenti con Azure AD join.  Il dispositivo verrà aggiunto a un tenant Azure AD.
- Distribuzioni basate sugli utenti con Aggiunta ad Azure AD ibrido.  Il dispositivo verrà aggiunto a un dominio di Active Directory locale e registrato separatamente con Azure AD.
Ognuno di questi scenari è costituito da due parti, un flusso tecnico e un flusso utente.  A un livello elevato, queste parti sono le stesse per Azure AD join e Azure AD ibrido join; le differenze sono visualizzate principalmente dall'utente finale nei passaggi di autenticazione.

### <a name="technician-flow"></a>Flusso tecnico

Quando il cliente o l'amministratore IT ha assegnato tutte le app e le impostazioni desiderate ai propri dispositivi tramite Intune, il tecnico del guanto bianco può iniziare il processo di guanto bianco.  Il tecnico può essere membro del personale IT, di un partner di servizi o di un OEM. ogni organizzazione può decidere chi deve eseguire queste attività. Indipendentemente dallo scenario, il processo che deve essere eseguito dal tecnico è lo stesso:
- Avviare il dispositivo (che esegue gli SKU di Windows 10 Pro, Enterprise o Education versione 1903 o successiva).
- Dalla prima schermata OOBE (che potrebbe essere una selezione della lingua o una schermata di selezione delle impostazioni locali), non fare clic su **Avanti**.  Premere invece il tasto Windows cinque volte per visualizzare una finestra di dialogo Opzioni aggiuntive.  Da questa schermata scegliere l'opzione **provisioning di Windows Autopilot** , quindi fare clic su **continua**.

  ![choice](images/choice.png)

- Nella schermata **configurazione di Windows Autopilot** verranno visualizzate informazioni sul dispositivo:
    - Profilo di Autopilot assegnato al dispositivo.
    - Nome dell'organizzazione per il dispositivo.
    - Utente assegnato al dispositivo (se presente).
    - Codice a matrice contenente un identificatore univoco per il dispositivo, utile per cercare il dispositivo in Intune per apportare le modifiche di configurazione necessarie, ad esempio l'assegnazione di un utente, l'aggiunta del dispositivo a tutti i gruppi aggiuntivi necessari per l'app o i criteri di destinazione.
    - **Nota**: i codici a matrice possono essere analizzati usando un'app complementare, che configurerà anche il dispositivo per specificare a chi appartiene.  Un [esempio Open Source dell'app complementare](https://github.com/Microsoft/WindowsAutopilotCompanion) che si integra con Intune tramite il API Graph è stato pubblicato in GitHub dal team di Autopilot.
- Convalidare le informazioni visualizzate.  Se sono necessarie modifiche, impostarle e quindi fare clic su **Aggiorna** per scaricare di nuovo i dettagli aggiornati sul profilo di Autopilot.

  ![destinazione](images/landing.png)

- Fare clic su **provision** per avviare il processo di provisioning.

Se il processo di pre-provisioning viene completato correttamente:
- Verrà visualizzata una schermata di stato verde con informazioni sul dispositivo, inclusi gli stessi dettagli presentati in precedenza (ad esempio, il profilo di Autopilot, il nome dell'organizzazione, l'utente assegnato, il codice a matrice) e il tempo trascorso per i passaggi di pre-provisioning.
 ![White-Glove-result](images/white-glove-result.png)
- Fare clic su **Richiudi** per arrestare il dispositivo.  A questo punto, il dispositivo può essere spedito all'utente finale.

>[!NOTE]
>Il flusso tecnico eredita il comportamento dalla [modalità di distribuzione automatica](self-deploying.md). Per la documentazione relativa alla modalità di distribuzione automatica, viene usata la pagina relativa allo stato della registrazione per mantenere il dispositivo in uno stato di provisioning e impedire all'utente di procedere al desktop dopo la registrazione, ma prima di applicare il software e la configurazione. Di conseguenza, se la pagina relativa allo stato della registrazione è disabilitata, è possibile che il pulsante di richiusura venga visualizzato prima che il software e la configurazione si applichino consentendo di passare al flusso utente prima del completamento del provisioning del flusso di lavoro. La schermata verde verifica che la registrazione abbia avuto esito positivo, non che il flusso del tecnico sia necessariamente completo.

Se il processo di pre-provisioning ha esito negativo:
- Verrà visualizzata una schermata di stato rossa con le informazioni sul dispositivo, inclusi gli stessi dettagli presentati in precedenza (ad esempio, il profilo di Autopilot, il nome dell'organizzazione, l'utente assegnato, il codice a matrice) e il tempo trascorso per i passaggi di pre-provisioning.
- I log di diagnostica possono essere raccolti dal dispositivo, quindi possono essere reimpostati per avviare di nuovo il processo.

### <a name="user-flow"></a>Flusso utente

Se il processo di pre-provisioning è stato completato correttamente e il dispositivo è stato risigillato, può essere recapitato all'utente finale per completare il normale processo guidato dall'utente di Windows Autopilot.  Eseguiranno una serie di passaggi standard:

- Accendere il dispositivo.
- Selezionare la lingua, le impostazioni locali e il layout di tastiera appropriati.
- Connettersi a una rete (se si usa il Wi-Fi).  L'accesso a Internet è sempre obbligatorio.  Se si utilizza Aggiunta ad Azure AD ibrido, è necessario che sia disponibile anche la connettività a un controller di dominio.
- Nella schermata di accesso con personalizzazione immettere le credenziali Azure Active Directory dell'utente.
- Se si usa Aggiunta ad Azure AD ibrido, il dispositivo viene riavviato; dopo il riavvio, immettere le credenziali di Active Directory dell'utente.
- I criteri e le app aggiuntive verranno recapitati al dispositivo, come rilevato dalla pagina relativa allo stato della registrazione (ESP).  Al termine dell'operazione, l'utente sarà in grado di accedere al desktop.

## <a name="related-topics"></a>Argomenti correlati

[Video su guanto bianco](https://youtu.be/nE5XSOBV0rI)
