---
title: Registrare i dispositivi macOS - Apple Business Manager o Apple School Manager
titleSuffix: ''
description: Informazioni su come registrare i dispositivi macOS di proprietà dell'azienda.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 196fc4f551596a6146513d25166b1b167aa44186
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986681"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>Registrare automaticamente i dispositivi macOS con Apple Business Manager o Apple School Manager

> [!IMPORTANT]
> Apple è recentemente passata dall'uso del programma Apple Device Enrollment Program (DEP) alla funzionalità Registrazione automatica del dispositivo. Intune sta aggiornando l'interfaccia utente di Intune in modo da rispecchiare questo cambiamento. Fino al completamento di queste modifiche, si continuerà a vedere *Device Enrollment Program* nel portale di Intune. Ogni volta che compare, viene però ora usata la funzionalità Registrazione automatica del dispositivo.

È possibile configurare la registrazione di Intune per i dispositivi macOS acquistati tramite [Apple Business Manager](https://business.apple.com/) o [Apple School Manager](https://school.apple.com/) di Apple. È possibile usare una di queste registrazioni per un numero elevato di dispositivi senza interventi diretti. È possibile fornire i dispositivi macOS direttamente agli utenti. Quando l'utente attiva il dispositivo, l'Assistente configurazione viene eseguito con impostazioni preconfigurate e il dispositivo viene registrato nella gestione di Intune.

Per configurare la registrazione, si usano i portali di Intune e di Apple. Si creano profili di registrazione contenenti le impostazioni da applicare ai dispositivi durante la registrazione.

Le registrazioni Apple Business Manager o Apple School Manager non funzionano con [manager di registrazione dispositivi](device-enrollment-manager-enroll.md).

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Prerequisiti

- Dispositivi acquistati in [Apple School Manager](https://school.apple.com/) o [Device Enrollment Program di Apple](http://deploy.apple.com)
- Un elenco di numeri di serie o un numero di ordine di acquisto.
- [Autorità di gestione dei dispositivi mobili](../fundamentals/mdm-authority-set.md)
- [Certificato push MDM Apple](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>Ottenere un token di Registrazione automatica del dispositivo Apple

Per registrare i dispositivi macOS con Registrazione automatica del dispositivo o Apple School Manager, è necessario un file di token (con estensione p7m) da Apple. Questo token consente a Intune di sincronizzare le informazioni sui dispositivi di proprietà dell'azienda. Consente anche a Intune di caricare profili di registrazione in Apple e di assegnare questi profili ai dispositivi.

Per creare un token si usa il portale di Apple. Il portale di Apple viene usato anche per assegnare i dispositivi a Intune per la gestione.

> [!NOTE]
> Se si elimina il token dal portale classico di Intune prima della migrazione ad Azure, è possibile che Intune ripristini un token Apple eliminato. È possibile eliminare nuovamente il token dal portale di Azure.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Passaggio 1. Scaricare il certificato di chiave pubblica di Intune necessario per creare il token

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **macOS** > **Registrazione di macOS** > **Token del programma di registrazione** > **Aggiungi**.

    ![Ottenere un token del programma di registrazione.](./media/device-enrollment-program-enroll-macos/image01.png)

2. Concedere a Microsoft l'autorizzazione per l'invio di informazioni su utenti e dispositivi ad Apple selezionando **Accetto**.

   ![Schermata del pannello Token DEP nell'area di lavoro dei certificati Apple per scaricare la chiave pubblica.](./media/device-enrollment-program-enroll-macos/add-enrollment-program-token-pane.png)

3. Scegliere **Download your public key** (Scarica la chiave pubblica) per scaricare e salvare il file della chiave di crittografia (con estensione pem) in locale. Il file PEM viene usato per richiedere un certificato di relazione di trust dal portale Apple.

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Passaggio 2: Usare la chiave per scaricare un token da Apple

1. Scegliere **Creare un token per Apple Device Enrollment Program** oppure **Crea un token tramite Apple School Manager** per aprire il portale di Apple appropriato e accedere con l'ID Apple aziendale. Lo stesso ID Apple può essere usato per rinnovare il token.
2. Per DEP, nel portale Apple scegliere **Get Started** (Iniziare) per **Device Enrollment Program** > **Manage Servers** > **Add MDM Server** (Device Enrollment Program, Gestisci server, Aggiungi server MDM).
3. Per Apple School Manager nel portale Apple scegliere **MDM Servers** > **Add MDM Server** (Server MDM, Aggiungi server MDM).
4. Immettere il **nome del server MDM** e scegliere **Avanti**. Il nome del server viene immesso come riferimento per identificare il server MDM (Mobile Device Management, Gestione dei dispositivi mobili). Non è il nome o l'URL del server di Microsoft Intune.

5. Viene visualizzata la finestra di dialogo **Aggiungi &lt;NomeServer&gt;** che richiede di **caricare la chiave pubblica**. Fare clic su **Scegli file** per caricare il file PEM e scegliere **Avanti**.

6. Passare a **Programmi di distribuzione** &gt; **Device Enrollment Program** &gt; **Gestione dei dispositivi**.
7. Nella sezione **Scegliere dispositivi per** specificare come vengono identificati i dispositivi:
    - **Numero di serie**
    - **Numero di ordine**
    - **Carica file CSV**.

   ![Schermata in cui viene specificata la scelta dei dispositivi in base al numero di serie, viene impostata l'azione di selezione su Assegna a server e viene selezionato il nome del server.](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. In **Scegliere un'azione** scegliere **Assegna al server,** scegliere il &lt;nome del serve&gt;r specificato per Microsoft Intune e quindi scegliere **OK**. Il portale Apple assegna i dispositivi specificati al server di Intune per la gestione e quindi visualizza il messaggio **Assegnazione completata**.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Passaggio 3. Salvare l'ID Apple usato per creare questo token

Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) specificare l'ID Apple per riferimento futuro.

![Screenshot della specifica dell'ID Apple usato per creare il token DEP e passare al token DEP.](./media/device-enrollment-program-enroll-macos/image03.png)

### <a name="step-4-upload-your-token"></a>Passaggio 4. Caricare il token
Nella casella **Token Apple** passare al file (con estensione pem) del certificato, scegliere **Apri** e quindi scegliere **Crea**. Con il certificato push, Intune può registrare e gestire i dispositivi macOS eseguendo il push dei criteri nei dispositivi registrati. Intune si sincronizza automaticamente con Apple per verificare l'account DEP.

## <a name="create-an-apple-enrollment-profile"></a>Creare un profilo di registrazione di Apple

Ora che è stato installato il token, è possibile creare un profilo di registrazione per i dispositivi. Un profilo di registrazione dispositivi consente di definire le impostazioni applicate a un gruppo di dispositivi durante la registrazione.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **macOS** > **Registrazione di macOS** > **Token del programma di registrazione**.
2. Selezionare un token, scegliere **Profili** e quindi scegliere **Crea profilo**.

    ![Screenshot di Crea profilo.](./media/device-enrollment-program-enroll-macos/image04.png)

3. In **Crea profilo** immettere un **nome** e una **descrizione** per il profilo per scopi amministrativi. Questi dettagli non vengono visualizzati agli utenti. È possibile usare questo campo **Nome** per creare un gruppo dinamico in Azure Active Directory. Usare il nome del profilo per definire il parametro enrollmentProfileName per assegnare i dispositivi con questo profilo di registrazione. Altre informazioni sui [gruppi dinamici di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).

    ![Nome e descrizione del profilo.](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. Per **Piattaforma** scegliere **macOS**.

5. In **Affinità utente** scegliere se i dispositivi con questo profilo devono essere o meno registrati con o senza un utente assegnato.
    - **Registra con affinità utente**: scegliere questa opzione per i dispositivi che appartengono a utenti e che vogliono usare l'app Portale aziendale per servizi come l'installazione di app. Se si usa ADFS, per l'affinità utente è richiesto un [endpoint misto/nome utente WS-Trust 1.3](https://technet.microsoft.com/library/adfs2-help-endpoints). [Altre informazioni](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint). L'autenticazione a più fattori non è supportata per i dispositivi macOS con affinità utente aggiunti con Registrazione automatica del dispositivo.

    - **Registra senza affinità utente**: scegliere questa opzione per un dispositivo non associato a un singolo utente. Usare questa opzione per i dispositivi che eseguono attività senza accedere ai dati utente locali. Le app come l'app Portale aziendale non funzionano.

6. Scegliere **Impostazioni di gestione dei dispositivi** e specificare se si vuole o meno usare la registrazione bloccata per i dispositivi con questo profilo. La **registrazione bloccata** disabilita le impostazioni di macOS che consentono la rimozione del profilo di gestione dal menu **Preferenze del Sistema** o tramite il **Terminale**. Dopo la registrazione del dispositivo, non sarà possibile modificare questa impostazione senza cancellare il dispositivo.

    ![Screenshot di Impostazioni di gestione dei dispositivi.](./media/device-enrollment-program-enroll-macos/devicemanagementsettingsblade-macos.png)

7. Scegliere **OK**.

8. Scegliere **Impostazioni dell'Assistente configurazione** per configurare le impostazioni di profilo seguenti:  ![Personalizzazione dell'Assistente configurazione.](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | Impostazioni di reparto | Descrizione |
    |---|---|
    | <strong>Nome reparto</strong> | Viene visualizzata quando gli utenti toccano <strong>Informazioni configurazione</strong> durante l'attivazione. |
    | <strong>Telefono del reparto</strong> | Viene visualizzata quando l'utente fa clic sul pulsante <strong>Richiesta di assistenza</strong> durante l'attivazione. |

    È possibile scegliere di visualizzare o nascondere varie schermate dell'Assistente configurazione nel dispositivo quando l'utente lo configura.
    - Se si sceglie **Nascondi**, la schermata non verrà visualizzata durante la configurazione. Dopo aver configurato il dispositivo, l'utente può comunque ancora usare il menu **Impostazioni** menu per configurare la funzionalità.
    - Se si sceglie **Mostra**, la schermata verrà visualizzata durante la configurazione. L'utente può a volte ignorare la schermata senza eseguire azioni. Ma, in un secondo momento, può usare il menu **Impostazioni** del dispositivo per configurare la funzionalità. 

    | Impostazioni delle schermate dell'Assistente configurazione | Se si sceglie **Mostra**, durante la configurazione il dispositivo... |
    |------------------------------------------|------------------------------------------|
    | <strong>Passcode</strong> | Richiederà un passcode all'utente. Richiedere sempre un passcode, a meno che il dispositivo non sia protetto o l'accesso al dispositivo non venga controllato in un altro modo, ad esempio con la modalità tutto schermo, che limita l'uso del dispositivo a una sola app. |
    | <strong>Servizi di posizione</strong> | Richiederà la posizione all'utente. |
    | <strong>Recupera</strong> | Visualizzerà la schermata App e dati. Questa schermata offre all'utente la possibilità di ripristinare o trasferire i dati da iCloud Backup durante la configurazione del dispositivo. |
    | <strong>ID iCloud e Apple</strong> | Offrirà all'utente la possibilità di accedere con l'**ID Apple** e di usare **iCloud**.                         |
    | <strong>Termini e condizioni</strong> | Richiederà all'utente di accettare i termini e le condizioni Apple. |
    | <strong>Touch ID</strong> | Offrirà all'utente la possibilità di impostare l'identificazione con impronta digitale per il dispositivo. |
    | <strong>Apple Pay</strong> | Offrirà all'utente la possibilità di configurare Apple Pay nel dispositivo. |
    | <strong>Zoom</strong> | Offrirà all'utente la possibilità di ingrandire la visualizzazione durante la configurazione del dispositivo. |
    | <strong>Siri</strong> | Offrirà all'utente la possibilità di configurare Siri. |
    | <strong>Dati di diagnostica</strong> | Visualizzerà la schermata Diagnostica all'utente. Questa schermata offre all'utente la possibilità di inviare dati di diagnostica ad Apple. |
    | <strong>FileVault</strong> | Offrirà all'utente la possibilità di configurare la crittografia FileVault. |
    | <strong>Diagnostica iCloud</strong> | Offrirà all'utente la possibilità di inviare dati di diagnostica iCloud ad Apple. |
    | <strong>Risorse di archiviazione iCloud</strong> | Offrirà all'utente la possibilità di usare le risorse di archiviazione iCloud. |    
    | <strong>Segnale schermo</strong> | Offrirà all'utente la possibilità di attivare il segnale schermo. |
    | <strong>Aspetto</strong> | Visualizzerà la schermata Aspetto all'utente. |
    | <strong>Registrazione</strong>| Richiederà all'utente di registrare il dispositivo. |
    | <strong>Privacy</strong>| Visualizzerà la schermata Privacy all'utente. |
    | <strong>Orario schermo</strong>| Visualizzerà la schermata Orario schermo per l'utente. |

9. Scegliere **OK**.

10. Per salvare il profilo, scegliere **Crea**.

## <a name="sync-managed-devices"></a>Sincronizzare i dispositivi gestiti

Adesso che Intune ha le autorizzazioni per gestire i dispositivi, è possibile sincronizzare Intune con Apple per visualizzare i dispositivi gestiti nel portale di Azure in Intune.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **macOS** > **Registrazione macOS** > **Token DEP** > scegliere un token dall'elenco > **Dispositivi** > **Sincronizza**. ![Schermata del nodo Enrollment Program Devices selezionato e con il collegamento Sincronizza selezionato.](./media/device-enrollment-program-enroll-macos/image06.png)

   Per soddisfare le condizioni Apple per un traffico DEP accettabile, Intune impone le seguenti restrizioni:
   - Una sincronizzazione completa può essere eseguita solo una volta ogni sette giorni. Durante una sincronizzazione completa, Intune recupera l'elenco aggiornato completo dei numeri di serie assegnati al server MDM di Apple connesso a Intune. Se un dispositivo del Device Enrollment Program viene eliminato dal portale di Intune senza che ne sia stata annullata l'assegnazione dal server Apple MDM nel portale Apple, il dispositivo non potrà essere reimportato in Intune fino a quando non viene eseguita la sincronizzazione completa.   
   - La sincronizzazione viene eseguita automaticamente ogni 24 ore. È anche possibile eseguire la sincronizzazione facendo clic sul pulsante **Sincronizza** (non più di una volta ogni 15 minuti). Il tempo concesso per il completamento di una richiesta di sincronizzazione è pari a 15 minuti. Il pulsante **Sincronizza** rimane disabilitato finché non viene completata la sincronizzazione. La sincronizzazione aggiorna lo stato dei dispositivi esistenti e importa i nuovi dispositivi assegnati al server MDM di Apple.

## <a name="assign-an-enrollment-profile-to-devices"></a>Assegnare un profilo DEP ai dispositivi

Prima della registrazione è necessario assegnare ai dispositivi un profilo DEP.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **macOS** > **Registrazione di macOS** > **Token del programma di registrazione** > scegliere un token nell'elenco.
2. Scegliere **Dispositivi** > scegliere i dispositivi nell'elenco > **Assegna profilo**.
3. In **Assegna profilo** scegliere un profilo per i dispositivi > **Assegna**.

### <a name="assign-a-default-profile"></a>Assegnare un profilo predefinito

È possibile selezionare un profilo predefinito macOS e iOS/iPadOS da applicare a tutti i dispositivi da registrare con un token specifico. 

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **macOS** > **Registrazione di macOS** > **Token del programma di registrazione** > scegliere un token nell'elenco.
2. Scegliere **Imposta profilo predefinito**, scegliere un profilo nell'elenco a discesa e quindi scegliere **Salva**. Questo profilo verrà applicato a tutti i dispositivi registrati con il token.

## <a name="distribute-devices"></a>Distribuire i dispositivi

Fino a questo punto sono state abilitate la gestione e la sincronizzazione tra Apple e Intune ed è stato assegnato un profilo per consentire la registrazione dei dispositivi. È ora possibile distribuire i dispositivi agli utenti. I dispositivi con affinità utente richiedono che a ogni utente sia assegnata una licenza di Intune. Per i dispositivi senza affinità utente è necessaria una licenza dispositivo. Un dispositivo attivato non può applicare un profilo di registrazione fino a quando non viene cancellato.

## <a name="renew-an-ade-token"></a>Rinnovare un token di Registrazione automatica del dispositivo

1. Passare a deploy.apple.com.  
2. In **Gestisci i server** scegliere il server MDM associato al file di token da rinnovare.
3. Scegliere **Genera nuovo token**.

    ![Screenshot della generazione di un nuovo token.](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. Scegliere **Token del server**.  
5. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Registrazione del dispositivo** > **Registrazione Apple** > **Token del programma di registrazione** > scegliere il token.
    ![Screenshot dei token del programma di registrazione.](./media/device-enrollment-program-enroll-macos/enrollmentprogramtokens.png)

6. Scegliere **Rinnova il token** e immettere l'ID Apple usato per creare il token originale.  
    ![Screenshot della generazione di un nuovo token.](./media/device-enrollment-program-enroll-macos/renewtoken.png)

7. Caricare il token appena scaricato.  
8. Scegliere **Rinnova il token**. Viene visualizzata la conferma che il token è stato rinnovato.
    ![Screenshot della conferma.](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>Passaggi successivi

Dopo la registrazione dei dispositivi macOS è possibile iniziare a [gestirli](../remote-actions/device-management.md).
