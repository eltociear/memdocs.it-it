---
title: Registrare i dispositivi iOS/iPadOS - Registrazione automatica dei dispositivi
titleSuffix: Microsoft Intune
description: Informazioni su come registrare i dispositivi iOS/iPadOS di proprietà dell'azienda usando Registrazione automatica dei dispositivi.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fe0b1748a40858bca55cc66b250c96725bfd9f1
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332863"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>Registrare automaticamente i dispositivi iOS/iPadOS con Registrazione automatica del dispositivo di Apple

> [!IMPORTANT]
> Apple è recentemente passata dall'uso del programma Apple Device Enrollment Program (DEP) alla funzionalità Registrazione automatica del dispositivo. Intune sta aggiornando l'interfaccia utente di Intune in modo da rispecchiare questo cambiamento. Fino al completamento di queste modifiche, si continuerà a vedere *Device Enrollment Program* nel portale di Intune. Ogni volta che compare, viene però ora usata la funzionalità Registrazione automatica del dispositivo.

È possibile configurare Intune per la registrazione dei dispositivi iOS/iPadOS acquistati con il programma [Registrazione automatica dei dispositivi](https://deploy.apple.com) di Apple. La funzionalità Registrazione automatica del dispositivo consente di registrare un numero elevato di dispositivi senza interventi diretti. Dispositivi come iPhone, iPad e MacBook possono essere spediti direttamente agli utenti. Quando l'utente accende il dispositivo, Assistente configurazione, che include la tipica esperienza di configurazione guidata per i prodotti Apple, viene eseguito con impostazioni preconfigurate e il dispositivo viene registrato nella gestione.

Per abilitare Registrazione automatica del dispositivo, si usano sia il portale di Intune che i portali [Apple Business Manager (ABM)](https://business.apple.com/) o [Apple School Manager (ASM)](https://school.apple.com/). È necessario un elenco di numeri di serie o un numero di ordine di acquisto per poter assegnare i dispositivi a Intune per la gestione in uno dei portali Apple. Si creano profili di registrazione per Registrazione automatica del dispositivo in Intune contenenti le impostazioni da applicare ai dispositivi durante la registrazione. Non è possibile usare Registrazione automatica del dispositivo con un account [Manager di registrazione dispositivi](device-enrollment-manager-enroll.md).

> [!NOTE]
> Registrazione automatica del dispositivo imposta configurazioni del dispositivo che non possono essere necessariamente rimosse dall'utente finale. Per questa ragione, prima di eseguire la [migrazione a Registrazione automatica del dispositivo](../fundamentals/migration-guide-considerations.md), è necessario cancellare i dati del dispositivo per ripristinare lo stato predefinito.

## <a name="automated-device-enrollment-and-the-company-portal"></a>Registrazione automatica del dispositivo e Portale aziendale

Le registrazioni con Registrazione automatica del dispositivo non sono compatibili con la versione di App Store dell'app Portale aziendale. È possibile concedere agli utenti l'accesso all'app Portale aziendale in un dispositivo registrato con Registrazione automatica del dispositivo. È possibile fornire questo accesso per consentire agli utenti di scegliere le app aziendali che vogliono usare nel dispositivo o di usare l'autenticazione moderna per completare il processo di registrazione. 

Per abilitare l'autenticazione moderna durante la registrazione, eseguire il push dell'app al dispositivo usando **Installa il Portale aziendale con VPP** (Volume Purchase Program) nel profilo di Registrazione automatica del dispositivo. Per altre informazioni, vedere [Registrare automaticamente i dispositivi iOS/iPadOS con Registrazione automatica del dispositivo di Apple](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

Per consentire l'aggiornamento automatico del Portale aziendale e fornire l'app Portale aziendale nei dispositivi già registrati con Registrazione automatica del dispositivo, distribuire l'app Portale aziendale tramite Intune come app Volume Purchase Program (VPP) obbligatoria con un [criterio di configurazione dell'applicazione](../apps/app-configuration-policies-use-ios.md) applicato.

## <a name="what-is-supervised-mode"></a>Che cos'è la modalità con supervisione?

Apple ha introdotto la modalità con supervisione in iOS/iPadOS 5. Un dispositivo iOS/iPadOS nella modalità con supervisione può essere gestito con più controlli, ad esempio Blocca acquisizione schermo e Blocca l'installazione di app con App Store. Questa modalità è quindi particolarmente utile per dispositivi di proprietà dell'azienda. Intune supporta la configurazione di dispositivi per la modalità con supervisione come parte di Registrazione automatica del dispositivo.

Il supporto per i dispositivi registrati con Registrazione automatica del dispositivo senza supervisione è stato deprecato in iOS/iPadOS 11. In iOS/iPadOS 11 e versioni successive, i dispositivi configurati con Registrazione automatica del dispositivo devono essere sempre con supervisione. Il flag *is_supervised* di Registrazione automatica del dispositivo viene ignorato in iOS/iPadOS 13.0 e versioni successive. Tutti i dispositivi iOS/iPadOS versione 13.0 e successive vengono supervisionati automaticamente se vengono registrati con la registrazione automatica dei dispositivi. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Prerequisiti
- Dispositivi acquistati con [Registrazione automatica del dispositivo di Apple](https://deploy.apple.com)
- [Autorità di gestione dei dispositivi mobili (MDM)](../fundamentals/mdm-authority-set.md)
- [Certificato push MDM Apple](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>Volume supportato

- Numero massimo di profili di registrazione per token: 1,000  
- Numero massimo di dispositivi con Registrazione automatica dispositivi per profilo: nessun limite (entro il numero massimo di dispositivi per token)
- Numero massimo di token di Registrazione automatica dispositivi per account Intune: 2,000
- Numero massimo di dispositivi con Registrazione automatica dispositivi per token: Il limite della prima sincronizzazione è 75.000-80.000 dispositivi. Intune continuerà a eseguire la sincronizzazione con ABM o ASM con una sincronizzazione ogni 12 ore per aggiungere ogni volta altri 80.000 dispositivi. Anche una sincronizzazione manuale consente di aggiungere 80.000 dispositivi. Le sincronizzazioni continueranno a verificarsi e i dispositivi continueranno a essere sincronizzati con Intune da ABM/ASM in batch di 75.000-80.000 dispositivi. 

## <a name="get-an-apple-ade-token"></a>Ottenere un token di Registrazione automatica del dispositivo Apple

Per registrare i dispositivi iOS/iPadOS con Registrazione automatica del dispositivo, è necessario un file di token di Registrazione automatica del dispositivo (P7M) da Apple. Questo token consente a Intune di sincronizzare le informazioni sui dispositivi configurati con Registrazione automatica del dispositivo di proprietà dell'azienda. Consente inoltre di caricare i profili di registrazione in Apple e assegnare i dispositivi a tali profili.

Per creare un token, è possibile usare il portale [Apple Business Manager (ABM)](https://business.apple.com/) o [Apple School Manager (ASM)](https://school.apple.com/). Il portale ABM/ASM viene usato anche per assegnare i dispositivi a Intune per la gestione.

> [!NOTE]
> Se si elimina il token dal portale classico di Intune prima della migrazione ad Azure, è possibile che Intune ripristini un token di Registrazione automatica del dispositivo Apple eliminato. È possibile eliminare nuovamente il token di Registrazione automatica del dispositivo dal portale di Azure.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Passaggio 1. Scaricare il certificato di chiave pubblica di Intune necessario per creare il token.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS/iPadOS** > **Registrazione di iOS/iPadOS**.

    ![Ottenere un token del programma di registrazione.](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. Scegliere **Token del programma di registrazione** > **Aggiungi**.

3. Concedere a Microsoft l'autorizzazione per l'invio di informazioni su utenti e dispositivi ad Apple selezionando **Accetto**.

   > [!NOTE]
   > Una volta superato il passaggio 2 per il download del certificato di chiave pubblica di Intune, non chiudere la procedura guidata né uscire da questa pagina. Così facendo si invaliderebbe il certificato scaricato e sarebbe necessario ripetere il processo. Se si verifica questa situazione, si noterà che il pulsante **Crea** nella scheda **Rivedi e crea** è disattivato e non è possibile completare il processo.

   ![Schermata del pannello Token DEP nell'area di lavoro dei certificati Apple per scaricare la chiave pubblica.](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. Scegliere **Download your public key** (Scarica la chiave pubblica) per scaricare e salvare il file della chiave di crittografia (con estensione pem) in locale. Il file PEM viene usato per richiedere un certificato di relazione di trust dal portale Apple.


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Passaggio 2: Usare la chiave per scaricare un token da Apple.

1. Scegliere **Crea un token tramite Apple Business Manager** per aprire il portale aziendale di Apple e accedere con l'ID Apple aziendale. Lo stesso ID Apple può essere usato per rinnovare il token di Registrazione automatica del dispositivo.
2. Nel [portale Business](https://business.apple.com) di Apple scegliere **Inizia** per **Device Enrollment Program**.

3. Nella pagina **Gestisci server** scegliere **Aggiungi server MDM**.
4. Immettere il **nome del server MDM** e scegliere **Avanti**. Il nome del server viene immesso come riferimento per identificare il server MDM (Mobile Device Management, Gestione dei dispositivi mobili). Non corrisponde al nome o all'URL del server di Microsoft Intune.

5. Viene visualizzata la finestra di dialogo **Aggiungi &lt;NomeServer&gt;** che richiede di **caricare la chiave pubblica**. Selezionare **Scegli file**. per caricare il file PEM e scegliere **Avanti**.

6. Passare a **Programmi di distribuzione** &gt; **Device Enrollment Program** &gt; **Gestione dei dispositivi**.
7. Nella sezione **Scegliere dispositivi per** specificare come vengono identificati i dispositivi:
    - **Numero di serie**
    - **Numero di ordine**
    - **Carica file CSV**.

   ![Schermata in cui viene specificata la scelta dei dispositivi in base al numero di serie, viene impostata l'azione di selezione su Assegna a server e viene selezionato il nome del server.](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. In **Scegliere un'azione** scegliere **Assegna al server,** scegliere il &lt;nome del serve&gt;r specificato per Microsoft Intune e quindi scegliere **OK**. Il portale Apple assegna i dispositivi specificati al server di Intune per la gestione e quindi visualizza il messaggio **Assegnazione completata**.

   Nel portale Apple passare a **Deployment Programs** (Programmi di distribuzione) &gt; **Device Enrollment Program** &gt; **View Assignment History** (Visualizza cronologia di assegnazione) per visualizzare un elenco di dispositivi con la rispettiva assegnazione di server MDM.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Passaggio 3. Salvare l'ID Apple usato per creare il token.

Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) specificare l'ID Apple per riferimento futuro.

![Screenshot della specifica dell'ID Apple usato per creare il token DEP e passare al token DEP.](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>Passaggio 4. Caricare il token e scegliere i tag di ambito.

1. Nella casella **Token Apple** passare al file del certificato (P7M) e scegliere **Apri**.
2. Per applicare [tag di ambito](../fundamentals/scope-tags.md) a questo token DEP, scegliere **Ambito (tag)** e selezionare i tag di ambito desiderati. I tag di ambito applicati a un token verranno ereditati dai profili e dai dispositivi aggiunti a questo token.
3. Scegliere **Crea**.

Con il certificato push, Intune può registrare e gestire i dispositivi iOS/iPadOS eseguendo il push dei criteri nei dispositivi mobili registrati. Intune si sincronizza automaticamente con Apple per verificare l'account DEP.

## <a name="create-an-apple-enrollment-profile"></a>Creare un profilo di registrazione di Apple

Ora che è stato installato il token, è possibile creare un profilo di registrazione per i dispositivi configurati con Registrazione automatica del dispositivo. Un profilo di registrazione dispositivi consente di definire le impostazioni applicate a un gruppo di dispositivi durante la registrazione. È previsto un limite di 100 profili di registrazione per ogni token di Registrazione automatica del dispositivo.

> [!NOTE]
> I dispositivi verranno bloccati se non sono disponibili licenze del portale aziendale sufficienti per un token VPP o se il token è scaduto. Intune visualizza un avviso quando un token sta per scadere o le licenze sono quasi esaurite.
 

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS/iPadOS** > **Registrazione di iOS/iPadOS** > **Token del programma di registrazione**.
2. Selezionare un token, scegliere **Profili** > **Crea profilo** > **iOS/iPadOS**.

    ![Screenshot di Crea profilo.](./media/device-enrollment-program-enroll-ios/image04.png)

3. Nella pagina **Informazioni di base** immettere un **nome** e una **descrizione** per il profilo per scopi amministrativi. Questi dettagli non vengono visualizzati agli utenti. 

    ![Nome e descrizione del profilo.](./media/device-enrollment-program-enroll-ios/image05.png)

4. Selezionare **Passaggio successivo: Impostazioni di gestione dei dispositivi**.

5. In **Affinità utente** scegliere se i dispositivi con questo profilo devono essere registrati con o senza un utente assegnato.
    - **Registra con affinità utente**: scegliere questa opzione per i dispositivi che appartengono a utenti che vogliono usare il portale aziendale per servizi come l'installazione di app. Se si usa ADFS e per l'autenticazione si usa Assistente configurazione, è richiesto un [endpoint misto/nome utente WS-Trust 1.3 ](https://technet.microsoft.com/library/adfs2-help-endpoints) [Altre informazioni](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

    - **Registra senza affinità utente**: scegliere questa opzione per i dispositivi non associati a un singolo utente. Usare questa opzione per i dispositivi che non accedono ai dati utente locali e ai dispositivi iPad condiviso Apple per le aziende. Le app come l'app Portale aziendale non funzionano.

6. Se si sceglie **Registra con affinità utente**, è possibile consentire agli utenti di eseguire l'autenticazione con il portale aziendale invece di Assistente configurazione Apple.

    ![Autenticazione con il portale aziendale.](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Se si vuole eseguire una delle operazioni seguenti, impostare **Selezione della posizione per l'autenticazione degli utenti** su **Portale aziendale**.
    >    - Usare l'autenticazione a più fattori
    >    - Richiedere agli utenti di modificare la password al primo accesso
    >    - Richiedere agli utenti di reimpostare le password scadute durante la registrazione
    >
    > Non sono supportate durante l'autenticazione con l'Assistente configurazione di Apple.

7. Se si sceglie **Portale aziendale** per **Selezione della posizione per l'autenticazione degli utenti**, è possibile usare un token VPP per installare automaticamente il portale aziendale nel dispositivo. In questo caso, l'utente non deve specificare un ID Apple. Per installare il portale aziendale con un token VPP, scegliere un token in **Install Company Portal with VPP** (Installa il portale aziendale con VPP). Richiede che il portale aziendale sia già stato aggiunto al token VPP. Per assicurarsi che l'app Portale aziendale continui a essere aggiornata dopo la registrazione, assicurarsi di aver configurato una distribuzione delle app in Intune (Intune>App client). Per fare in modo che l'interazione dell'utente non sia obbligatoria, è opportuno che l'app Portale aziendale sia un'app VPP iOS/iPadOS, impostata come app obbligatoria, e che vengano usate le licenze del dispositivo per l'assegnazione. Assicurarsi che il token non abbia una scadenza e di avere un numero sufficiente di licenze dei dispositivi per l'app Portale aziendale. Se il token ha una scadenza o se il numero di licenze è insufficiente, Intune installa invece l'app Portale aziendale dall'App Store e richiede un ID Apple. 

    > [!NOTE]
    > Quando l'opzione **Selezione della posizione per l'autenticazione degli utenti** è impostata su **Portale aziendale**, assicurarsi che il processo di registrazione del dispositivo venga eseguito nelle prime 24 ore dal download dell'app Portale aziendale nel dispositivo configurato con Registrazione automatica del dispositivo. In caso contrario, la registrazione potrebbe non riuscire e sarà necessario il ripristino delle impostazioni predefinite per registrare il dispositivo.
    
    ![Screenshot dell'installazione del portale aziendale con VPP.](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. Se si sceglie **Assistente configurazione** per **Selezione della posizione per l'autenticazione degli utenti**, ma si vuole anche usare l'accesso condizionale o distribuire le app aziendali nei dispositivi, è necessario installare il portale aziendale nel dispositivi. A tale scopo, scegliere **Sì** per **Installa il Portale aziendale**.  Se si vuole che gli utenti ricevano l'app Portale aziendale senza dover eseguire l'autenticazione in App Store, scegliere **Installa il Portale aziendale con VPP** e selezionare un token VPP. Per la corretta distribuzione, assicurarsi che il token non abbia una scadenza e di avere un numero sufficiente di licenze dei dispositivi per l'app Portale aziendale.

9. Se si era scelto un token per **Installa il Portale aziendale con VPP**, è possibile bloccare il dispositivo in modalità applicazione singola (in particolare, l'app Portale aziendale), subito dopo il completamento dell'Assistente configurazione. Scegliere **Sì** per **Run Company Portal in Single App Mode until authentication** (Esegui il portale aziendale in modalità app singola fino all'autenticazione) per impostare l'opzione. Per poter usare il dispositivo, l'utente deve prima autenticarsi effettuando l'accesso tramite il portale aziendale.

    L'autenticazione a più fattori non è supportata per un singolo dispositivo bloccato in modalità app singola. Questa limitazione esiste perché il dispositivo non può passare a un'altra app per completare il secondo fattore di autenticazione. Pertanto, se si vuole usare l'autenticazione a più fattori in un singolo dispositivo in modalità app singola, il secondo fattore deve trovarsi in un dispositivo diverso.

    Questa funzionalità è supportata solo per iOS/iPadOS 11.3.1 e versioni successive.

   ![Screenshot della modalità applicazione singola.](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. Se si vuole che i dispositivi che usano questo profilo siano inclusi nella supervisione, scegliere **Sì** per **Supervisione eseguita**.

    ![Screenshot di Impostazioni di gestione dei dispositivi.](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    I dispositivi **con supervisione** offrono più opzioni di gestione e il blocco attivazione viene disabilitato per impostazione predefinita. È consigliabile usare Registrazione automatica del dispositivo come meccanismo per l'abilitazione della modalità con supervisione, soprattutto per la distribuzione di un numero elevato di dispositivi iOS/iPadOS. È necessario supervisionare i dispositivi iPad condiviso Apple per le aziende.

    Gli utenti vengono informati che i dispositivi sono inclusi nella supervisione in due modi:

   - Nella schermata di blocco viene visualizzata l'indicazione: "This iPhone is managed by Contoso" (Questo iPhone è gestito da Contoso).
   - Nella schermata **Settings** (Impostazioni)  > **General** (Generale)  > **About** (Informazioni) viene visualizzato l'avviso: "This iPhone is supervised. Contoso can monitor your Internet traffic and locate this device." (Questo iPhone è soggetto a supervisione. Contoso può monitorare il traffico Internet e individuare il dispositivo)

     > [!NOTE]
     > Per reimpostare un dispositivo registrato senza supervisione in modo da includerlo nella supervisione, è possibile usare solo Apple Configurator. Per reimpostare il dispositivo in questo modo, è necessario connettere un dispositivo iOS/iPadOS a un computer Mac con un cavo USB. Per altre informazioni vedere la [documentazione di Apple Configurator](http://help.apple.com/configurator/mac/2.3).

11. Scegliere se usare la registrazione bloccata per i dispositivi con questo profilo. La **registrazione bloccata** disabilita le impostazioni di iOS/iPadOS che consentono la rimozione del profilo di gestione dal menu **Impostazioni**. Dopo la registrazione del dispositivo, non è possibile modificare questa impostazione senza cancellare il dispositivo. Per tali dispositivi, la modalità di gestione **Supervisione eseguita** deve essere impostata su *Sì*. 

    > [!NOTE]
    > Dopo la registrazione del dispositivo con **Registrazione bloccata** gli utenti non saranno in grado di usare **Rimuovi dispositivo** o **Ripristino impostazioni predefinite** nell'app Portale aziendale. Le opzioni non saranno disponibili per l'utente. L'utente inoltre non sarà in grado di rimuovere il dispositivo nel sito Web Portale aziendale (https://portal.manage.microsoft.com).
    > Inoltre, se un dispositivo BYOD viene convertito in un dispositivo Apple con registrazione automatica dei dispositivi e registrato con un profilo abilitato per la **Registrazione bloccata**, l'utente sarà autorizzato a usare **Rimuovi dispositivo** e **Ripristino impostazioni predefinite** per 30 giorni, quindi le opzioni saranno disabilitate o rese non disponibili. Riferimento: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859.

12. Se sono state scelte le opzioni **Registra senza affinità utente** e **Supervisione** in precedenza, è necessario decidere se configurare i dispositivi come [dispositivi iPad condiviso Apple per le aziende](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web). Scegliendo **Sì** per **iPad condiviso**, più utenti saranno in grado di accedere allo stesso dispositivo. Gli utenti eseguiranno l'autenticazione con l'ID Apple gestito e gli account di autenticazione federati oppure tramite una sessione temporanea, ad esempio un account Guest. Questa opzione richiede iOS/iPadOS 13.4 o versione successiva.

    Se si sceglie di configurare i dispositivi in modo che siano dispositivi iPad condiviso Apple per le aziende, è necessario impostare **Numero massimo di utenti memorizzati nella cache**. Impostare questo valore sul numero di utenti che si prevede useranno l'iPad condiviso. È possibile memorizzare nella cache fino a 24 utenti in un dispositivo da 32 GB o 64 GB. Se si sceglie un numero molto basso, potrebbe essere necessario un po' di tempo prima che i dati dell'utente arrivino al dispositivo dopo l'accesso. Se si sceglie un numero molto elevato, è possibile che gli utenti non dispongano di spazio su disco sufficiente.  

    > [!NOTE]
    > Per configurare iPad condiviso Apple per le aziende, usare le impostazioni seguenti: 
    > - **Affinità utente** = **Registra senza affinità utente**. 
    > - **Supervisione eseguita** = **Sì**. 
    > - **iPad condiviso** = **Sì **.
    > Le sessioni temporanee sono abilitate per impostazione predefinita e consentono agli utenti di accedere a un iPad condiviso senza un account ID Apple gestito. È possibile disabilitare le sessioni temporanee nell'iPad condiviso configurando le [impostazioni relative alle restrizioni del dispositivo](../configuration/device-restrictions-ios.md) iPad condiviso iOS/iPadOS.  

13. Scegliere se si vuole che i dispositivi con questo profilo possano **eseguire la sincronizzazione con i computer**. Se si sceglie **Consenti Apple Configurator per certificato**, è necessario selezionare un certificato in **Certificati di Apple Configurator**.

     > [!NOTE]
     > Se **Sincronizza con computer** è impostata su **Rifiuta tutto**, la funzionalità della porta sarà limitata sui dispositivi iOS e iPadOS. La porta può essere usata solo per il caricamento. L'uso di iTunes o Apple Configurator 2 sulla porta non è consentito.
     Se **Sincronizza con computer** è impostato su **Consenti Apple Configurator per certificato**, assicurarsi di salvare una copia locale del certificato a cui poter accedere in un secondo momento. Non sarà possibile apportare modifiche alla copia caricata ed è importante conservare il certificato affinché sia accessibile in futuro. Per connettersi al dispositivo iOS/iPados da un dispositivo macOS o da un PC, è necessario che nel dispositivo sia installato lo stesso certificato che effettua la connessione al dispositivo iOS/iPados registrato con il profilo Registrazione automatica del dispositivo con la configurazione e il certificato.

14. Se si sceglie **Consenti Apple Configurator per certificato** nel passaggio precedente, scegliere un certificato di Apple Configurator da importare.

15. È possibile specificare un formato di denominazione per i dispositivi che viene applicato automaticamente alla registrazione e per ogni archiviazione successiva. Per creare un modello di denominazione, selezionare **Sì** in **Applica il modello di nome di dispositivo**. Nella casella **Modello del nome del dispositivo** immettere quindi il modello da usare per i nomi che usano questo profilo. È possibile specificare un formato modello che include il tipo di dispositivo e il numero di serie. 

16. Scegliere **Avanti: Personalizzazione dell'Assistente configurazione**.

17. Nella pagina **Personalizzazione dell'Assistente configurazione** configurare le impostazioni di profilo seguenti: ![Personalizzazione dell'Assistente configurazione.](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | Impostazioni di reparto | Descrizione |
    |---|---|
    | <strong>Nome reparto</strong> | Viene visualizzata quando gli utenti toccano <strong>Informazioni configurazione</strong> durante l'attivazione. |
    |    <strong>Telefono del reparto</strong>     | Viene visualizzata quando l'utente fa clic sul pulsante <strong>Richiesta di assistenza</strong> durante l'attivazione. |

    È possibile scegliere di nascondere le schermate di Assistente configurazione nel dispositivo durante la configurazione.
    - Se si sceglie **Nascondi**, la schermata non verrà visualizzata durante la configurazione. Dopo aver configurato il dispositivo, l'utente può comunque ancora usare il menu **Impostazioni** menu per configurare la funzionalità.
    - Se si sceglie **Mostra**, la schermata verrà visualizzata durante la configurazione. L'utente può a volte ignorare la schermata senza eseguire azioni. Ma, in un secondo momento, può usare il menu **Impostazioni** del dispositivo per configurare la funzionalità. 


    | Impostazioni delle schermate dell'Assistente configurazione | Se si sceglie **Mostra**, durante la configurazione il dispositivo... |
    |------------------------------------------|------------------------------------------|
    | <strong>Passcode</strong> | Richiederà un passcode all'utente. Richiedere sempre un passcode per i dispositivi non protetti, a meno che l'accesso non venga controllato in un altro modo (ad esempio, la modalità tutto schermo che limita il dispositivo a una sola app). Per iOS/iPadOS 7.0 e versioni successive. |
    | <strong>Servizi di posizione</strong> | Richiederà la posizione all'utente. Per macOS 10.11 e versioni successive e iOS/iPados 7.0 e versioni successive. |
    | <strong>Recupera</strong> | Visualizzerà la schermata App e dati. Questa schermata offre all'utente la possibilità di ripristinare o trasferire i dati da iCloud Backup durante la configurazione del dispositivo. Per macOS 10.9 e versioni successive e iOS/iPados 7.0 e versioni successive. |
    | <strong>ID iCloud e Apple</strong> | Offrirà all'utente la possibilità di accedere con l'ID Apple e di usare iCloud. Per macOS 10.9 e versioni successive e iOS/iPados 7.0 e versioni successive.   |
    | <strong>Termini e condizioni</strong> | Richiederà all'utente di accettare i termini e le condizioni Apple. Per macOS 10.9 e versioni successive e iOS/iPados 7.0 e versioni successive. |
    | <strong>Touch ID</strong> | Offrirà all'utente la possibilità di impostare l'identificazione con impronta digitale per il dispositivo. Per macOS 10.12.4 e versioni successive e iOS/iPados 8.1 e versioni successive. |
    | <strong>Apple Pay</strong> | Offrirà all'utente la possibilità di configurare Apple Pay nel dispositivo. Per macOS 10.12.4 e versioni successive e iOS/iPados 7.0 e versioni successive. |
    | <strong>Zoom</strong> | Offrirà all'utente la possibilità di ingrandire la visualizzazione durante la configurazione del dispositivo. Per iOS/iPadOS 8.3 e versioni successive. |
    | <strong>Siri</strong> | Offrirà all'utente la possibilità di configurare Siri. Per macOS 10.12 e versioni successive e iOS/iPados 7.0 e versioni successive. |
    | <strong>Dati di diagnostica</strong> | Visualizzerà la schermata Diagnostica all'utente. Questa schermata offre all'utente la possibilità di inviare dati di diagnostica ad Apple. Per macOS 10.9 e versioni successive e iOS/iPados 7.0 e versioni successive. |
    | <strong>Segnale schermo</strong> | Offrirà all'utente la possibilità di attivare il segnale schermo. Per macOS 10.13.6 e versioni successive e iOS/iPados 9.3.2 e versioni successive. |
    | <strong>Privacy</strong> | Visualizzerà la schermata Privacy all'utente. Per macOS 10.13.4 e versioni successive e iOS/iPados 11.3 e versioni successive. |
    | <strong>Migrazione Android</strong> | Offrirà all'utente la possibilità di eseguire la migrazione dei dati da un dispositivo Android. Per iOS/iPadOS 9.0 e versioni successive.|
    | <strong>iMessage e FaceTime</strong> | Offrirà all'utente la possibilità di configurare iMessage e FaceTime. Per iOS/iPadOS 9.0 e versioni successive. |
    | <strong>Onboarding</strong> | Visualizzerà le schermate con le informazioni di onboarding per la formazione dell'utente, ad esempio Copertina e Multitasking e centro di controllo. Per iOS/iPadOS 11.0 e versioni successive. |
    | <strong>Migrazione di Watch</strong> | Offrirà all'utente la possibilità di eseguire la migrazione dei dati da un dispositivo Watch. Per iOS/iPadOS 11.0 e versioni successive.|
    | <strong>Orario schermo</strong> | Visualizzerà la schermata Orario schermo. Per macOS 10.15 e versioni successive e iOS/iPados 12.0 e versioni successive. |
    | <strong>Aggiornamento software</strong> | Visualizzerà la schermata degli aggiornamenti software obbligatori. Per iOS/iPadOS 12.0 e versioni successive. |
    | <strong>Configurazione SIM</strong> | Offrirà all'utente la possibilità di aggiungere un piano dati cellulare. Per iOS/iPadOS 12.0 e versioni successive. |
    | <strong>Aspetto</strong> | Visualizzerà la schermata Aspetto all'utente. Per macOS 10.14 e versioni successive e iOS/iPados 13.0 e versioni successive. |
    | <strong>Express Language</strong> (Lingua rapida)| Visualizzerà la schermata Express Language (Lingua rapida) all'utente. |
    | <strong>Lingua preferita</strong> | Offrirà all'utente la possibilità di scegliere la **Lingua preferita**. |
    | <strong>Device to Device Migration</strong> (Migrazione da dispositivo a dispositivo) | Offrirà all'utente la possibilità di eseguire la migrazione dei dati dal dispositivo precedente a questo dispositivo. Per iOS/iPadOS 13.0 e versioni successive. |
    | <strong>Registrazione</strong> | Consente all'utente di visualizzare la schermata di registrazione. Per macOS 10.9 e versioni successive. |
    | <strong>FileVault</strong> | Consente all’utente di visualizzare la schermata di crittografia FileVault 2. Per macOS 10.10 e versioni successive. |
    | <strong>Diagnostica di iCloud</strong> | Consente all'utente di visualizzare la schermata di iCloud Analytics. Per macOS 10.12.4 e versioni successive. |
    | <strong>Risorse di archiviazione iCloud</strong> | Consente all’utente di visualizzare la schermata Documenti e Scrivania di iCloud. Per macOS 10.13.4 e versioni successive. |
    

18. Scegliere **Avanti** per passare alla pagina **Rivedi e crea**.

19. Per salvare il profilo, scegliere **Crea**.

### <a name="dynamic-groups-in-azure-active-directory"></a>Gruppi dinamici in Azure Active Directory

È possibile usare il campo **Nome** della registrazione per creare un gruppo dinamico in Azure Active Directory. Per altre informazioni, vedere i [gruppi dinamici di Azure Active Directory](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

È possibile usare il nome del profilo per definire il [parametro enrollmentProfileName](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) e assegnare al gruppo i dispositivi con questo profilo di registrazione.

Per la distribuzione più rapida dei criteri nei dispositivi ADE con affinità utente, assicurarsi che l'utente che esegue la registrazione sia membro (prima dell'installazione del dispositivo) di un gruppo di utenti AAD. 

L'assegnazione di gruppi dinamici ai profili di registrazione può causare ritardi nella distribuzione di applicazioni e criteri ai dispositivi dopo la registrazione.


## <a name="sync-managed-devices"></a>Sincronizzare i dispositivi gestiti
Adesso che Intune ha le autorizzazioni per gestire i dispositivi, è possibile sincronizzare Intune con Apple per visualizzare i dispositivi gestiti nel portale di Azure in Intune.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS/iPadOS** > **Registrazione di iOS/iPadOS** > **Token del programma di registrazione**.

2. Scegliere un token nell'elenco > **Dispositivi** > **Sincronizza**. ![Screenshot del nodo Dispositivi DEP e del collegamento Sincronizza.](./media/device-enrollment-program-enroll-ios/image06.png)

   Per rispettare le condizioni Apple per un traffico DEP accettabile, Intune impone le restrizioni seguenti:
   - Una sincronizzazione completa può essere eseguita solo una volta ogni sette giorni. Durante una sincronizzazione completa, Intune recupera l'elenco aggiornato completo dei numeri di serie assegnati al server MDM di Apple connesso a Intune. Se un dispositivo configurato con Registrazione automatica del dispositivo viene eliminato dal portale di Intune, è necessario rimuoverne l'assegnazione dal server MDM Apple nel portale di Registrazione automatica del dispositivo. Se non è assegnato, non verrà reimportato in Intune fino all'esecuzione della sincronizzazione completa.   
   - La sincronizzazione viene eseguita automaticamente ogni 12 ore. È anche possibile eseguire la sincronizzazione facendo clic sul pulsante **Sincronizza** (non più di una volta ogni 15 minuti). Il tempo concesso per il completamento di una richiesta di sincronizzazione è pari a 15 minuti. Il pulsante **Sincronizza** rimane disabilitato finché non viene completata la sincronizzazione. La sincronizzazione aggiorna lo stato dei dispositivi esistenti e importa i nuovi dispositivi assegnati al server MDM di Apple.   


## <a name="assign-an-enrollment-profile-to-devices"></a>Assegnare un profilo DEP ai dispositivi
Prima della registrazione è necessario assegnare ai dispositivi un profilo DEP.

>[!NOTE]
>È anche possibile assegnare i numeri di serie ai profili nel pannello **Numeri di serie Apple**.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS/iPadOS** > **Registrazione di iOS/iPadOS** > **Token del programma di registrazione** > scegliere un token nell'elenco.
2. Scegliere **Dispositivi** > scegliere i dispositivi nell'elenco > **Assegna profilo**.
3. In **Assegna profilo** scegliere un profilo per i dispositivi > **Assegna**.

### <a name="assign-a-default-profile"></a>Assegnare un profilo predefinito

È possibile selezionare un profilo predefinito da applicare a tutti i dispositivi da registrare con un token specifico.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS/iPadOS** > **Registrazione di iOS/iPadOS** > **Token del programma di registrazione** > scegliere un token nell'elenco.
2. Scegliere **Imposta profilo predefinito**, scegliere un profilo nell'elenco a discesa e quindi scegliere **Salva**. Questo profilo verrà applicato a tutti i dispositivi registrati con il token.

## <a name="distribute-devices"></a>Distribuire i dispositivi
Fino a questo punto sono state abilitate la gestione e la sincronizzazione tra Apple e Intune ed è stato assegnato un profilo per consentire la registrazione dei dispositivi con Registrazione automatica del dispositivo. È ora possibile distribuire i dispositivi agli utenti. I dispositivi con affinità utente richiedono che a ogni utente sia assegnata una licenza di Intune. Per i dispositivi senza affinità utente è necessaria una licenza dispositivo. Un dispositivo attivato non può applicare un profilo di registrazione fino a quando non viene cancellato.

Vedere [Registrare il dispositivo iOS/iPadOS in Intune con Device Enrollment Program](../user-help/enroll-your-device-dep-ios.md).

## <a name="renew-an-ade-token"></a>Rinnovare un token di Registrazione automatica del dispositivo  

> [!NOTE]
> Oltre a rinnovare il token di Registrazione automatica del dispositivo annualmente, sarà necessario rinnovare il token del programma di registrazione in Intune e Apple Business Manager quando la password dell'ID Apple gestito viene modificata per l'utente che ha configurato il token in Apple Business Manager oppure quando l'utente abbandona l'organizzazione di Apple Business Manager.

1. Passare a business.apple.com.  
2. In **Gestisci i server** scegliere il server MDM associato al file di token da rinnovare.
3. Scegliere **Genera nuovo token**.

    ![Screenshot della generazione di un nuovo token.](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

4. Scegliere **Token del server**.  
5. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **iOS/iPadOS** > **Registrazione di iOS/iPadOS** > **Token del programma di registrazione** > scegliere il token.
    ![Screenshot dei token del programma di registrazione.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. Scegliere **Rinnova il token** e immettere l'ID Apple usato per creare il token originale.  
    ![Screenshot della generazione di un nuovo token.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

7. Selezionare **Avanti** per passare alla pagina **Tag di ambito** e assegnare i tag di ambito, se necessario.

8. Selezionare **Avanti** e caricare il token appena scaricato.  
9. Scegliere **Rinnova il token**. Viene visualizzata la conferma che il token è stato rinnovato.   
    ![Screenshot della conferma.](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-ade-token-from-intune"></a>Eliminare un token ADE da Intune

È possibile eliminare i token del profilo di registrazione da Intune purché
- al token non sia assegnato alcun dispositivo
- al profilo predefinito non sia assegnato alcun dispositivo

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivo** > **iOS/macOS** > **Registrazione di iOS/macOS** > **Token del programma di registrazione** > scegliere il token > **Dispositivi**.
2. Eliminare tutti i dispositivi assegnati al token.
3. Passare a **Dispositivi** > **iOS/macOS** > **Registrazione di iOS/macOS** > **Token del programma di registrazione** > scegliere il token > **Profili**.
4. Se è presente un profilo predefinito, eliminarlo.
5. Passare a **Dispositivi** > **iOS/macOS** > **Registrazione di iOS/macOS** > **Token del programma di registrazione** > scegliere il token > **Elimina**.
