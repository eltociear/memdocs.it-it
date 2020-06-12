---
title: Integrare Jamf Cloud Connector Pro con Microsoft Intune
titleSuffix: Microsoft Intune
description: Usare Jamf Cloud Connector con i criteri di conformità di Microsoft Intune insieme all'accesso condizionale di Azure Active Directory per favorire l'integrazione e la protezione dei dispositivi gestiti tramite Jamf.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 734a1361d8889ca1463e8d8986239e088b90cd09
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206367"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Usare Jamf Cloud Connector con Microsoft Intune

Questo articolo può essere utile per installare Jamf Cloud Connector al fine di integrare Jamf Pro con Microsoft Intune. Cloud Connector consente di automatizzare molti dei passaggi necessari per la configurazione manuale dell'integrazione, documentata in [Integrare Jamf Pro con Intune per la conformità](../protect/conditional-access-integrate-jamf.md).

Quando si configura Cloud Connector:

- La configurazione crea automaticamente le applicazioni Jamf Pro in Azure, eliminando la necessità di configurarle manualmente.
- È possibile integrare più istanze di Jamf Pro con lo stesso tenant di Azure che ospita la sottoscrizione di Intune in uso.

La connessione di più istanze di Jamf Pro con un singolo tenant di Azure è supportata solo quando si usa Cloud Connector. Quando si usa una connessione configurata manualmente è possibile integrare una sola istanza di Jamf con un tenant di Azure.

L'uso del connettore cloud è facoltativo:

- Per i nuovi tenant che non si integrano ancora con Jamf, è possibile scegliere di configurare Cloud Connector come descritto in questo articolo. In alternativa è possibile configurare manualmente l'integrazione, come descritto in [Integrare Jamf Pro con Intune per la conformità](../protect/conditional-access-integrate-jamf.md).
- Per i tenant che hanno già una configurazione manuale, è possibile scegliere di rimuovere l'integrazione e quindi configurare Cloud Connector. Questo articolo descrive sia la rimozione di un'integrazione esistente sia la configurazione del connettore cloud.

Se si prevede di sostituire l'integrazione precedente con Jamf Cloud Connector:

- Usare la [procedura di rimozione della configurazione corrente](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), che include l'eliminazione delle app Enterprise per Jamf Pro e la disattivazione dell'integrazione manuale. Quindi è possibile usare la [procedura di configurazione del connettore cloud](#configure-the-cloud-connector-for-a-new-tenant).
- Non è necessario ripetere la registrazione dei dispositivi. I dispositivi già registrati possono usare Cloud Connector senza nessuna configurazione aggiuntiva.
- Assicurarsi di configurare Cloud Connector entro 24 ore dalla rimozione dell'integrazione manuale, per garantire che i dispositivi registrati possano continuare a segnalare il proprio stato.

Per altre informazioni su Jamf Cloud Connector, vedere [Configuring the macOS Intune Integration using the Cloud Connector](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) (Configurare l'integrazione con Intune per macOS tramite Cloud Connector) in docs.Jamf.com.

## <a name="prerequisites"></a>Prerequisiti

**Prodotti e servizi**:  
- Jamf Pro 10.18 o versione successiva
- Un account utente Jamf Pro con privilegi di accesso condizionale  
- Microsoft Intune
- Microsoft Azure AD Premium
- [App Portale aziendale per macOS](https://aka.ms/macoscompanyportal)
- Dispositivi macOS con OS X 10.12 Yosemite o versioni successive

**Rete**:  
Le seguenti porte ed endpoint devono essere accessibili per garantire l'integrazione corretta di Jamf e Intune:

- **Intune**: Porta 443
- **Apple**: Porte 2195, 2196 e 5223 (notifiche push a Intune)
- **Jamf**: Porte 80 e 5223

- Endpoint:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

Per il corretto funzionamento di APNS in rete, è necessario abilitare anche le connessioni in uscita e i reindirizzamenti dalle porte seguenti:

- Blocco Apple 17.0.0.0/8 sulle porte TCP 5223 e 443 da tutte le reti client.
- Porte 2195 e 2196 dai server Jamf Pro.

Per altre informazioni su queste porte, vedere i seguenti articoli:

- [Requisiti di configurazione di rete di Intune e larghezza di banda](../fundamentals/network-bandwidth-use.md).
- [Network Ports Used by Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) (Porte di rete usate da Jamf Pro) su jamf.com.
- [Porte TCP e UDP usate dai prodotti software Apple](https://support.apple.com/HT202944) su support.apple.com

**Account**:  
Le procedure descritte in questo articolo richiedono l'uso di account con le autorizzazioni seguenti:

- **Console Jamf Pro**: un account con autorizzazioni per la gestione di Jamf Pro
- **Interfaccia di amministrazione di Microsoft Endpoint Manager**: Amministratore globale
- **Portale di Azure**: Amministratore globale

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Rimuovere l'integrazione di Jamf Pro per un tenant configurato in precedenza

Usare la procedura seguente per rimuovere un'integrazione di Jamf Pro configurata manualmente dal tenant di Azure *prima* di poter configurare il connettore Cloud.

Se non è stata configurata in precedenza una connessione tra Jamf Pro e Intune o se sono presenti una o più connessioni che usano già Cloud Connector, ignorare questa procedura e iniziare con [Configurare Cloud Connector per un nuovo tenant](#configure-the-cloud-connector-for-a-new-tenant).

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Rimuovere un'integrazione Jamf Pro configurata manualmente

1. Accedere alla console di Jamf Pro.

2. Selezionare **Settings** (Impostazioni, l'icona a forma di ingranaggio nell'angolo superiore destro) e quindi selezionare **Global Management**  (Gestione globale) > **Conditional Access** (Accesso condizionale).

   ![Passare a Conditional Access (Accesso condizionale)](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Selezionare **Edit** (Modifica).

4. Deselezionare la casella di controllo **Enable Intune Integration for macOS** (Abilita integrazione con Intune per macOS).

   Quando si deseleziona questa impostazione, si disabilita la connessione ma si salva la configurazione.

5. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere **Amministrazione del tenant** > **Gestione dei dispositivi partner**.

   Nel nodo **Gestione dei dispositivi partner** eliminare l'**ID applicazione** nel campo **Specificare l'ID app Azure Active Directory per Jamf** e quindi selezionare **Salva**.

   L'ID applicazione è l'ID dell'app Azure Enterprise che è stata creata in Azure quando è stata configurata un'integrazione manuale di Jamf Pro.

6. Accedere al [portale di Azure](https://portal.azure.com/) con un account che dispone di autorizzazioni Amministratore globale e passare ad **Azure Active Directory** > **Applicazioni aziendali**.

   Trovare le due app Jamf ed eliminarle. Le nuove applicazioni verranno create automaticamente quando si configura Jamf Cloud Connector nella procedura seguente.

   ![Selezionare le app Jamf da eliminare](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Dopo la disattivazione dell'integrazione in Jamf Pro e l'eliminazione delle applicazioni Enterprise, il nodo **Gestione dispositivi partner** visualizza come stato della connessione **Terminata**.

   ![Stato connessione Terminata](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Dopo aver rimosso correttamente la configurazione manuale per l'integrazione di Jamf Pro, è possibile configurare l'integrazione usando Cloud Connector. A tale scopo, vedere [Configurare Cloud Connector per un nuovo tenant](#configure-the-cloud-connector-for-a-new-tenant) in questo articolo.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Configurare Cloud Connector per un nuovo tenant

Usare la procedura seguente per configurare Jamf Cloud Connector al fine di integrare Jamf Pro e Microsoft Intune se:

- Non è presente nessuna integrazione tra Jamf Pro e Intune configurata per il tenant Azure.
- È già configurato un Cloud Connector tra Jamf Pro e Intune nel tenant di Azure e si vuole integrare un'istanza di Jamf aggiuntiva con la sottoscrizione.

Se attualmente è presente un'integrazione configurata manualmente tra Intune e Jamf Pro, prima di procedere vedere [Rimuovere l'integrazione di Jamf Pro per un tenant configurato in precedenza](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) in questo articolo per rimuovere l'integrazione. La rimozione di un'integrazione configurata manualmente è necessaria per poter configurare correttamente Jamf Cloud Connector.

### <a name="create-a-new-connection"></a>Creare una nuova connessione

1. Accedere alla console di Jamf Pro.

2. Selezionare **Settings** (Impostazioni, l'icona a forma di ingranaggio nell'angolo superiore destro) e quindi selezionare **Global Management**  (Gestione globale) > **Conditional Access** (Accesso condizionale).

   ![Passare a Conditional Access (Accesso condizionale)](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Selezionare **Edit** (Modifica).

4. Selezionare la casella di controllo **Enable Intune Integration for macOS** (Abilita integrazione con Intune per macOS).
   - Selezionare questa impostazione per fare in modo che Jamf Pro invii gli aggiornamenti dell'inventario a Microsoft Intune.
   - È possibile deselezionare questa impostazione per disabilitare la connessione ma salvare la configurazione.

   > [!IMPORTANT]
   > Se **Enable Intune Integration for macOS** (Abilita integrazione con Intune per macOS) è già selezionata e *Connection Type* (Tipo di connessione) è impostato su **Manual** (Manuale), è necessario rimuovere questa integrazione prima di continuare. Vedere [Rimuovere l'integrazione di Jamf Pro per un tenant configurato in precedenza](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) in questo articolo prima di continuare.

5. In *Connection Type* (Tipo di connessione) selezionare **Cloud Connector**.

   ![Selezionare Cloud Connector nella console Jamf Pro](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. Nel menu a comparsa **Sovereign Cloud** (Cloud sovrano) selezionare la posizione del cloud sovrano di Microsoft. Se si sta sostituendo l'integrazione precedente con Jamf Cloud Connector, è possibile ignorare questo passaggio se è stata specificata la posizione.

7. Selezionare una delle seguenti opzioni di pagina di destinazione per i computer non riconosciuti da Microsoft Azure:
   - **Pagina predefinita di registrazione del dispositivo Jamf Pro**: a seconda dello stato del dispositivo macOS, questa opzione reindirizza gli utenti al portale di registrazione dispositivi Jamf Pro (per la registrazione con Jamf Pro) o all'app Portale aziendale Intune (per la registrazione con Azure AD).
   - **Pagina Accesso negato**
   - **URL personalizzato**
  
   Se si sta sostituendo l'integrazione precedente con Jamf Cloud Connector, è possibile ignorare questo passaggio se è stata specificata la pagina di destinazione.
  
8. Selezionare **Connetti**. Si viene reindirizzati alla registrazione delle applicazioni Jamf Pro in Azure.

   Quando richiesto, specificare le credenziali di Microsoft Azure e seguire le istruzioni visualizzate per concedere le autorizzazioni richieste. Si concederanno autorizzazioni per **Cloud Connector** e poi di nuovo per l'**app di registrazione utenti Cloud Connector**. Entrambe le app sono registrate in Azure come applicazioni aziendali.

   Dopo la concessione delle autorizzazioni a entrambe le app viene visualizzata la pagina **Application ID** (ID applicazione).

9. Nella pagina **Application ID** (ID applicazione) selezionare **Copy and open Intune** (Copia e apri Intune).

   ![ID applicazione](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   Il valore *Application ID* viene copiato negli Appunti di sistema per l'uso nel passaggio successivo e viene aperto il nodo **Gestione dei dispositivi partner** nell'*interfaccia di amministrazione di Microsoft Endpoint Manager*. (**Amministrazione del tenant** > **Gestione dei dispositivi partner**).

10. Nel nodo **Gestione dei dispositivi partner** scegliere *Incolla* per incollare l'**ID applicazione** nel campo **Specificare l'ID app Azure Active Directory per Jamf** e selezionare **Salva**.

    ![Configurare la gestione dei dispositivi partner](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Tornare alla pagina dell'ID applicazione in Jamf Pro e selezionare **Confirm** (Conferma).

12. Jamf Pro completa la configurazione ed esegue il testing, quindi visualizza l'esito positivo o negativo della connessione nella pagina delle impostazioni Conditional Access (Accesso condizionale). L'immagine seguente è un esempio di connessione riuscita:

    ![La configurazione riuscita è confermata in Jamf Pro](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. Nell'interfaccia di amministrazione di Microsoft Endpoint Manager aggiornare il nodo **Gestione dei dispositivi partner**. La connessione ora viene visualizzata come **Attiva**:

    ![Lo stato della connessione è attivo](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Dopo che la connessione tra Jamf Pro e Microsoft Intune viene stabilita correttamente, Jamf Pro invia a Microsoft Intune informazioni di inventario per ogni computer registrato con Azure AD (la registrazione con Azure AD è un flusso di lavoro dell'utente finale). È possibile visualizzare Conditional Access Inventory State (Stato di inventario per l'accesso condizionale) per un utente e un computer nella categoria Local User Account (Account utente locale) delle informazioni di inventario di un computer in Jamf Pro.

Dopo aver integrato un'istanza di Jamf Pro usando Jamf Cloud Connector, è possibile usare la stessa procedura per configurare istanze aggiuntive di Jamf Pro con la stessa sottoscrizione di Intune nel tenant di Azure.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Impostare i criteri di conformità e registrare i dispositivi

Dopo aver configurato l'integrazione tra Intune e Jamf, è necessario [applicare i criteri di conformità per i dispositivi gestiti da Jamf](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Disconnettere Jamf Pro e Intune

Se è necessario rimuovere l'integrazione di Jamf Pro con Intune, seguire questa procedura per rimuovere la connessione dalla console di Jamf Pro. Queste informazioni sono valide sia per Cloud Connector sia per un'integrazione configurata manualmente.

1. In Jamf Pro passare a **Global Management** >  (Gestione globale) **Conditional Access** (Accesso condizionale). Nella scheda **macOS Intune Integration** (Integrazione con Intune per macOS) selezionare **Edit** (Modifica).

2. Deselezionare la casella di controllo **Enable Intune Integration for macOS** (Abilita integrazione con Intune per macOS).

3. Selezionare **Salva**. Jamf Pro invia la configurazione a Intune e l'integrazione viene terminata.

4. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

5. Selezionare **Amministrazione del tenant** > **Connettori e token** > **Gestione dei dispositivi partner** per verificare che lo stato ora sia **Terminato**.

   > [!NOTE]
   > I dispositivi Mac dell'organizzazione verranno rimossi alla data visualizzata nella console (3 mesi).

## <a name="get-support-for-the-cloud-connector"></a>Supporto tecnico per Cloud Connector

Poiché Cloud Connector crea automaticamente le app Azure Enterprise necessarie per l'integrazione, il primo punto di contatto per il supporto è **Jamf**. Le opzioni includono:

- Invio di un messaggio di posta elettronica a `support@jamf.com`
- Uso del portale di supporto Jamf Nation: https://www.jamf.com/support/ 


Prima di contattare il supporto tecnico:

- Esaminare i prerequisiti, ad esempio le porte e la versione del prodotto in uso.
- Verificare che le autorizzazioni per le due app Jamf Pro seguenti create in Azure non siano state modificate. Le modifiche alle autorizzazioni dell'app non sono supportate da Intune e possono causare un errore di integrazione.

  **App di registrazione utenti Cloud Connector**:
  - Nome API: Microsoft Graph
    - Autorizzazione: Accesso e lettura del profilo utente
    - Tipo: Delegate
    - Concessa tramite: Consenso amministratore
    - Concessa da: Un amministratore

  **App Cloud Connector**:
  - Nome API: Microsoft Graph (istanza 1)
    - Autorizzazione: Accesso e lettura del profilo utente
    - Tipo: Delegate
    - Concessa tramite: Consenso amministratore
    - Concessa da: Un amministratore

  - Nome API: Microsoft Graph (istanza 2)
    - Autorizzazione: Lettura dati directory
    - Tipo: Applicazione
    - Concessa tramite: Consenso amministratore
    - Concessa da: Un amministratore

  - Nome API: API Intune
    - Autorizzazione: Send device attribute to Microsoft Intune (Invio attributo del dispositivo a Microsoft Intune)
    - Tipo: Applicazione
    - Concessa tramite: Consenso amministratore
    - Concessa da: Un amministratore

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Domande frequenti su Jamf Cloud Connector

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Quali dati vengono condivisi tramite Cloud Connector?

Cloud Connector esegue l'autenticazione con Microsoft Azure e invia dati di inventario del dispositivo da Jamf Pro ad Azure. Cloud Connector gestisce anche l'individuazione dei servizi in Azure, lo scambio di token, gli errori di comunicazione e il ripristino di emergenza.

### <a name="where-is-device-inventory-data-stored"></a>Dove vengono archiviati i dati di inventario dei dispositivi?

I dati di inventario dei dispositivi vengono archiviati nel database Jamf Pro.

### <a name="what-credentials-are-stored"></a>Quali credenziali vengono archiviate?

Non viene archiviata nessuna credenziale. Quando si configura Cloud Connector, gli amministratori devono consentire l'aggiunta dell'app multi-tenant Jamf e dell'app del connettore macOS nativo al tenant Azure AD. Dopo l'aggiunta dell'applicazione multi-tenant, Cloud Connector richiede token di accesso per interagire con l'API di Azure. L'accesso alle applicazioni può essere revocato in qualsiasi momento in Microsoft Azure.

### <a name="how-is-data-encrypted"></a>In che modo vengono crittografati i dati?

Cloud Connector usa Transport Layer Security (TLS) per i dati scambiati tra Jamf Pro e Microsoft Azure.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>In che modo Jamf rileva quale dispositivo è associato a quale istanza di Jamf Pro?

Jamf Pro usa i microservizi in AWS per indirizzare correttamente le informazioni del dispositivo all'istanza appropriata.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>È possibile passare dall'uso di Cloud Connector al tipo di connessione manuale?

Sì. È possibile ripristinare il tipo di connessione manuale e seguire i passaggi per la configurazione manuale. In caso di domande, rivolgersi a Jamf per assistenza.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Dopo che sono state modificate le autorizzazioni in una o in entrambe le app obbligatorie (*Cloud Connector* e l'*app di registrazione utenti Cloud Connector*) la registrazione non funziona. Questa operazione è supportata?

La modifica delle autorizzazioni per le app non è supportata.

### <a name="is-there-a-log-file-in-jamf-pro-that-shows-if-the-connection-type-has-been-changed"></a>In Jamf Pro è presente un file di log che indica se il tipo di connessione è stato modificato?

Sì, le modifiche vengono registrate nel file JAMFChangeManagement.log. Per visualizzare i log di Change Management accedere a Jamf Pro, andare a **Settings** (Impostazioni) > **System Settings** (Impostazioni di sistema) > **Change Management** (Gestione modifiche) > **Logs** (Log), cercare in **Object type** (Tipo oggetto) l'opzione **Conditional Access** (Accesso condizionale) e fare clic su **Details** (Dettagli) per visualizzare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

- [Applicare criteri di conformità a dispositivi gestiti da Jamf](../protect/conditional-access-assign-jamf.md)
- [Dati inviati da Jamf a Intune](../protect/data-jamf-sends-to-intune.md)
