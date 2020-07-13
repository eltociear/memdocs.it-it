---
title: Configurare l'integrazione di Wandera Mobile Threat Protection con Intune
titleSuffix: Intune on Azure
description: Come configurare la soluzione Wandera Mobile Threat Protection con Microsoft Intune per controllare l'accesso dei dispositivi mobili alle risorse aziendali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc44bb114d6ff9089a01da2d0b7db7aa7527f4b5
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972148"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Integrare Wandera Mobile Threat Protection con Intune  

Seguire questa procedura per integrare la soluzione Wandera Mobile Threat Defense con Intune.  

## <a name="before-you-begin"></a>Prima di iniziare  

Prima di iniziare il processo di integrazione di Wandera con Intune, verificare che si siano soddisfatti i prerequisiti seguenti:

- Sottoscrizione a Intune
- Credenziali di amministratore di Azure Active Directory e ruolo assegnato in grado di concedere le autorizzazioni seguenti:

    - Accesso e lettura del profilo utente
    - Accesso alla directory come utente connesso
    - Lettura dati directory
    - Invio di informazioni sul rischio dei dispositivi a Intune
 
- Una sottoscrizione di Wandera valida
    - Un account amministratore con privilegi di super amministratore

## <a name="integration-overview"></a>Panoramica sull'integrazione

L'abilitazione dell'integrazione di Mobile Threat Defense tra Wandera e Intune comporta:

- Consentire al servizio UEM Connect di Wandera di sincronizzare le informazioni con Azure e Intune, inclusi i metadati di gestione del ciclo di vita di utenti e dispositivi, insieme al livello di minaccia del dispositivo di Mobile Threat Defense (MTD).
- Creare profili di attivazione in Wandera per definire il comportamento della registrazione del dispositivo.
- Distribuire Wandera in modalità wireless nei dispositivi iOS e Android gestiti.
- Configurare Wandera per la funzionalità self-service degli utenti finali usando MAM-WE su dispositivi iOS e Android non gestiti.

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Configurare l'integrazione di Wandera Mobile Threat Defense

La configurazione dell'integrazione tra Wandera e Intune non richiede supporto da parte del personale Wandera e può essere facilmente eseguita in pochi minuti.

### <a name="enable-support-for-wandera-in-intune"></a>Abilitare il supporto per Wandera in Intune

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Amministrazione del tenant** > **Connettori e token** > **Mobile Threat Defense** > **Aggiungi**.
3. Nella pagina **Aggiungi un connettore** selezionare **Wandera** nel menu a discesa. Selezionare quindi **Crea**.  
4. Nel riquadro Mobile Threat Defense, selezionare il connettore MTD **Wandera** nell'elenco dei connettori per aprire il riquadro **Modifica il connettore**. Selezionare **Apri la console dell'amministratore di Wandera MTD** per aprire [RADAR](https://radar.wandera.com/login), la console di amministrazione di Wandera e accedere. 
5. Nella console RADAR di Wandera passare a **Integrations > UEM Integration** (Integrazioni > Integrazione UEM) e selezionare la scheda **UEM Connect**. Usare l'elenco a discesa EMM Vendor (Fornitore EMM) e selezionare **Microsoft Intune**.
6. Verrà visualizzata una schermata simile alla seguente, che indica quali autorizzazioni devono essere concesse per completare l'integrazione:

   ![Integrazioni e autorizzazioni](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Accanto a Intune User and Device Sync (Sincronizzazione di utenti e dispositivi Intune) fare clic sul pulsante Grant (Concedi) per avviare il processo con cui si concede a Wandera il consenso di eseguire le funzioni di gestione del ciclo di vita con Azure e Intune.
8. Quando richiesto, selezionare o immettere le credenziali di amministratore di Azure. Esaminare le autorizzazioni richieste, quindi selezionare la casella di controllo per acconsentire per conto dell'organizzazione. Infine fare clic su Accetta per autorizzare l'integrazione con la gestione del ciclo di vita.

   ![Accettare le autorizzazioni](./media/wandera-mtd-connector-integration/permissions.png)

10. Si tornerà automaticamente alla console di amministrazione RADAR.  Se l'autorizzazione ha avuto esito positivo, verrà visualizzato un segno di spunta verde accanto al pulsante Grant (Concedi).
11. Ripetere il processo di consenso per le rimanenti integrazioni elencate facendo clic sui pulsanti Grant (Concedi) corrispondenti finché non compare un segno di spunta verde accanto a ognuna.

    ![Gruppo di sincronizzazione](./media/wandera-mtd-connector-integration/sync-group-name.png)

12. Tornare alla console di Intune e riprendere a modificare il connettore MTD Wandera. Attivare tutti gli interruttori disponibili e quindi salvare la configurazione.

    ![Abilitare Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune e Wandera sono ora connessi.

## <a name="create-activation-profiles-in-wandera"></a>Creare profili di attivazione in Wandera

Le distribuzioni basate su Intune risultano più semplici se si usano i profili di attivazione di Wandera definiti in RADAR.  Ogni profilo di attivazione definisce opzioni di configurazione specifiche, ad esempio i requisiti di autenticazione, le funzionalità del servizio e l'appartenenza iniziale al gruppo.

Dopo aver creato un profilo di attivazione in Wandera, lo si "assegna" a utenti e dispositivi in Intune.  Anche se un profilo di attivazione è universale per tutte le piattaforme dei dispositivi e le strategie di gestione, i passaggi seguenti definiscono come configurare Intune in base a queste differenze.

I passaggi seguenti presuppongono che sia stato creato un profilo di attivazione in Wandera da distribuire tramite Intune nei dispositivi di destinazione. Per informazioni dettagliate sulla creazione e sull'uso dei profili di attivazione di Wandera, vedere la [guida ai profili di attivazione](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links).

> [!NOTE]
> Quando si creano i profili di attivazione per la distribuzione tramite Intune o MAM-WE, assicurarsi di impostare l'utente associato sull'opzione Authenticated by Identity Provider (Autenticato dal provider di identità) > Azure Active Directory per ottenere la massima sicurezza, la compatibilità multipiattaforma e un'esperienza utente finale semplificata.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Distribuzione di Wandera in modalità wireless nei dispositivi gestiti da MDM

Per i dispositivi iOS e Android gestiti da Intune, Wandera può essere distribuito in modalità wireless per attivazioni rapide basate su push. Assicurarsi di aver già creato i profili di attivazione necessari prima di continuare con questa sezione. La distribuzione di Wandera nei dispositivi gestiti comporta:
- Aggiunta dei profili di configurazione di Wandera a Intune e assegnazione ai dispositivi di destinazione.
- Aggiunta dell'app Wandera e delle rispettive configurazioni dell'app a Intune e assegnazione ai dispositivi di destinazione.

### <a name="configure-and-deploy-ios-configuration-profiles"></a>Configurare e distribuire profili di configurazione iOS 

In questa sezione si scaricheranno i file di configurazione **necessari** per i dispositivi iOS e quindi li si distribuirà in modalità wireless tramite MDM nei dispositivi gestiti da Intune.

1. In **RADAR** passare al profilo di attivazione che si vuole distribuire facendo clic su Devices > Activations (Dispositivi > Attivazioni), quindi sulla scheda **Deployment Strategies > Managed Devices > Microsoft Endpoint Manager** (Strategie di distribuzione > Dispositivi gestiti > Microsoft Endpoint Manager).
2. Espandere le sezioni **Apple iOS Supervised** (Con supervisione Apple iOS) o **Apple iOS Unsupervised** (Senza supervisione Apple iOS) in base alla configurazione della flotta di dispositivi.
3. Scaricare i profili di configurazione forniti e prepararsi a caricarli in uno dei passaggi seguenti.
4. Aprire **Console di amministrazione di Intune** e passare a **Dispositivi > iOS/iPadOS > Profili di configurazione**.  Fare clic su **Crea profilo**.
5. Nel pannello visualizzato scegliere **iOS/iPadOS** in **Piattaforma**, quindi **Personalizzato** in Profilo. Fare quindi clic su **Crea**.
6. Nel campo **Nome** immettere un titolo descrittivo per la configurazione, possibilmente corrispondente al nome del profilo di attivazione creato in RADAR, per semplificare il riferimento incrociato in futuro. In alternativa, specificare il codice del profilo di attivazione, se si preferisce. È consigliabile indicare se la configurazione è per i dispositivi con supervisione o senza supervisione aggiungendo al nome il suffisso appropriato.
7. Facoltativamente immettere una **descrizione** specificando per gli altri amministratori dettagli aggiuntivi sullo scopo/uso della configurazione. Fare clic su **Avanti**.
8. Fare clic su **Seleziona un file** e individuare il profilo di configurazione scaricato che corrisponde al profilo di attivazione appropriato scaricato nel passaggio 3. Fare attenzione a selezionare il profilo con supervisione o senza supervisione appropriato, se sono stati scaricati entrambi. Fare clic su **Avanti**.
   <!-- image placeholder - ending future availability -->
9.  Definire **Tag di ambito** come richiesto dalle procedure di controllo degli accessi in base al ruolo di Intune.  Fare clic su **Avanti**.
10. **Assegnare** il profilo di configurazione ai gruppi di utenti o dispositivi in cui deve essere installato Wandera.  È consigliabile iniziare con un gruppo di test, quindi passare ad altri gruppi dopo aver convalidato il corretto funzionamento delle attivazioni. Fare clic su **Avanti**.
11. Esaminare la configurazione e apportare le modifiche necessarie, quindi fare clic su **Crea** per creare e distribuire il profilo di configurazione.

> [!NOTE]
> Wandera offre un profilo di distribuzione migliorato per i dispositivi iOS con supervisione. Se si ha una flotta mista di dispositivi con supervisione e senza supervisione, ripetere i passaggi precedenti per l'altro tipo di profilo, in base alle esigenze. Questa procedura deve essere eseguita per tutti i profili di attivazione futuri da distribuire tramite Intune. Contattare il supporto di Wandera se si ha una flotta mista di dispositivi iOS con supervisione e senza supervisione ed è necessaria assistenza per le assegnazioni di criteri basati sulla modalità con supervisione. 

## <a name="deploying-wandera-to-mam-we-devices"></a>Distribuzione di Wandera in dispositivi MAM-WE
Per i dispositivi non gestiti da Intune, ovvero i dispositivi MAM-WE, Wandera utilizza un'esperienza di onboarding basata sull'autenticazione integrata per attivare e proteggere i dati aziendali nelle app abilitate per MAM. 

Le sezioni seguenti descrivono come configurare Wandera e Intune per consentire agli utenti finali di attivare facilmente Wandera prima di poter accedere ai dati aziendali. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Configurare il provisioning di dispositivi di Azure in un profilo di attivazione di Wandera
I profili di attivazione da usare con MAM-WE devono avere l'utente associato impostato sull'opzione Authenticated by Identity Provider (Autenticato dal provider di identità) > Azure Active Directory.
1. Nel portale di **Wandera RADAR** selezionare un profilo di attivazione esistente o crearne uno nuovo, che i dispositivi MAM-WE useranno durante la registrazione in Devices > Activations (Dispositivi > Attivazioni). 
2. Fare clic sulla scheda **Deployment Strategies > Unmanaged Devices** (Strategie di distribuzione > Dispositivi non gestiti), quindi scorrere fino alla sezione **Azure Device Provisioning** (Provisioning di dispositivi di Azure).
3. Immettere l'**ID tenant di Azure AD** nel campo di testo appropriato. Se l'ID tenant non è disponibile, fare clic sul collegamento **Get my Tenant ID** (Ottieni l'ID tenant) per aprire Azure AD in una nuova scheda dove è possibile copiare facilmente questo valore negli Appunti.
4. (Facoltativo) Specificare **Group ID(s)** (ID gruppo) per limitare le attivazioni di utenti a gruppi specifici.
   - Se viene definito uno o più **ID gruppo**, un utente che attiva MAM-WE deve essere membro di almeno uno dei gruppi specificati per attivare l'uso di questo profilo di attivazione.
   - È possibile impostare più profili di attivazione configurati con lo stesso ID tenant di Azure, ma con ID gruppo diversi. In questo modo è possibile registrare i dispositivi in Wandera in base all'appartenenza al gruppo di Azure, abilitando funzionalità differenziate in base al gruppo al momento dell'attivazione.
   - È possibile configurare un singolo profilo di attivazione "predefinito" che non specifica alcun ID gruppo.  Questo gruppo fungerà da gruppo generico per tutte le attivazioni in cui l'utente autenticato non è membro di un gruppo con un'associazione a un altro profilo di attivazione.
5. Fare clic su **Save** (Salva) nell'angolo in alto a destra della pagina.

## <a name="next-steps"></a>Passaggi successivi
- Con i profili di attivazione di Wandera caricati in RADAR, creare app client in Intune per distribuire l'app Wandera nei dispositivi Android e iOS/iPadOS. La configurazione dell'app Wandera fornisce funzionalità essenziali per completare i profili di configurazione dei dispositivi di cui è stato effettuato il push ed è consigliata per tutte le distribuzioni. Vedere [Aggiungere app MTD](mtd-apps-ios-app-configuration-policy-add-assign.md) per le procedure e i dettagli personalizzati specifici per le app Wandera. 
- A questo punto, dopo aver integrato Wandera con Endpoint Manager, è possibile ottimizzare la configurazione, visualizzare i report ed eseguire la distribuzione in tutta la flotta di dispositivi mobili. Per guide dettagliate alla configurazione, vedere la [guida introduttiva del centro di supporto](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) nella documentazione di Wandera.
