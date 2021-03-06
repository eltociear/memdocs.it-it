---
title: Registrazione dei dispositivi aggiunti ad Azure AD - Windows Autopilot
titleSuffix: ''
description: Usare Windows Autopilot per registrare dispositivi aggiunti ad Azure Active Directory ibrido in Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1580726640612325fd22ca1fa4ae55517036644
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568585"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Distribuire dispositivi aggiunti ad Azure AD ibrido usando Intune e Windows Autopilot
È possibile usare Intune e Windows Autopilot per configurare i dispositivi aggiunti ad Azure Active Directory ibrido. A tale scopo, eseguire i passaggi descritti in questo articolo.

## <a name="prerequisites"></a>Prerequisiti

Configurare correttamente i [dispositivi aggiunti ad Azure AD ibrido](/azure/active-directory/devices/hybrid-azuread-join-plan). Assicurarsi di [verificare la registrazione del dispositivo](/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration) usando il cmdlet Get-MsolDevice.

Il dispositivo da registrare deve rispettare i requisiti seguenti:
- Usare Windows 10 v1809 o versione successiva.
- Accesso a Internet in [seguito ai requisiti di rete di Windows Autopilot](/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements).
- Hanno accesso a un controller di dominio Active Directory. Il dispositivo deve essere connesso alla rete dell'organizzazione, in modo da poter:
  - Risolvere i record DNS per il dominio di Active Directory e il controller di dominio AD.
  - Comunicare con il controller di dominio per autenticare l'utente.
- Il ping del controller di dominio del dominio a cui si sta tentando di partecipare è riuscito.
- Se si usa un proxy, è necessario abilitare e configurare l'opzione delle impostazioni proxy WPAD.
- Eseguire la Configurazione guidata.
- Usare un tipo di autorizzazione supportato da Azure Active Directory nella Configurazione guidata.

## <a name="set-up-windows-10-automatic-enrollment"></a>Configurare la registrazione automatica di Windows 10

1. Accedere ad Azure, nel riquadro sinistro selezionare **Azure Active Directory**  >  **Mobility (MDM e MAM)**  >  **Microsoft Intune**.

2. Assicurarsi che gli utenti che distribuiscono dispositivi aggiunti a Azure AD usando Intune e Windows siano membri di un gruppo incluso nell' **ambito utente MDM**.

    ![Riquadro Configura di Servizi Mobility (MDM e MAM)](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

3. Usare i valori predefiniti nelle caselle **URL delle condizioni per l'utilizzo di MDM**, **URL individuazione MDM** e **URL conformità MDM**, quindi selezionare **Salva**.

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>Aumentare il limite di account computer nell'unità organizzativa

Intune Connector per Active Directory crea computer registrati in Autopilot nel dominio Active Directory locale. Il computer che ospita Intune Connector deve avere l'autorizzazione per la creazione di oggetti computer all'interno del dominio. 

In alcuni domini, ai computer non vengono concessi i diritti per la creazione di computer. Sui domini è anche impostato un limite predefinito (pari a 10) che si applica a tutti gli utenti e i computer a cui non sono stati delegati i diritti di creazione di oggetti computer. I diritti devono essere delegati a computer che ospitano Intune Connector nell'unità organizzativa in cui vengono creati i dispositivi ibridi Azure AD aggiunti.

L'unità organizzativa a cui vengono assegnate le autorizzazioni per la creazione di computer deve corrispondere a:
- L'unità organizzativa specificata nel profilo Aggiunta a un dominio.
- Se non è selezionato alcun profilo, il nome di dominio del computer per il dominio.

1. Aprire **Utenti e computer di Active Directory (DSA.msc)** .

2. Fare clic con il pulsante destro del mouse sull'unità organizzativa da usare per creare computer ibridi Azure AD aggiunti > **controllo delegati**.

    ![Comando Delega controllo](./media/windows-autopilot-hybrid/delegate-control.png)

3. Nella procedura **Delega guidata del controllo** scegliere **Avanti** > **Aggiungi** > **Tipi di oggetto**.

4. Nel riquadro **tipi di oggetto** selezionare i **computer**  >  **OK**.

    ![Riquadro Tipi di oggetto](./media/windows-autopilot-hybrid/object-types-computers.png)

5. Nel riquadro **Seleziona utenti, computer o gruppi** nella casella **Immettere i nomi degli oggetti da selezionare** immettere il nome del computer in cui è installato Connector.

    ![Riquadro Seleziona utenti, computer o gruppi](./media/windows-autopilot-hybrid/enter-object-names.png)

6. Selezionare **Controlla nomi** per convalidare l'immissione> **OK** > **Avanti**.

7. Selezionare **Crea un'attività personalizzata per eseguire la delega** > **Avanti**.

8. Selezionare **solo gli oggetti seguenti nella cartella**  >  **oggetti computer**.

9. Selezionare **Crea oggetti selezionati in questa cartella** ed **Elimina gli oggetti selezionati in questa cartella**.

    ![Riquadro Tipo di oggetti Active Directory](./media/windows-autopilot-hybrid/only-following-objects.png)
 
10. Selezionare **Avanti**.

11. In **Autorizzazioni** selezionare la casella di controllo **Controllo completo**. Questa azione consente di selezionare tutte le altre opzioni.

    ![Riquadro Autorizzazioni](./media/windows-autopilot-hybrid/full-control.png)

12. Selezionare **Avanti** > **Fine**.

## <a name="install-the-intune-connector"></a>Installare Intune Connector

Il connettore di Intune per Active Directory deve essere installato in un computer che esegue Windows Server 2016 o versioni successive. Il computer deve anche avere accesso a Internet e al servizio Active Directory. Per aumentare la scalabilità e la disponibilità, è possibile installare più connettori nell'ambiente in uso. È consigliabile installare il connettore in un server che non esegue altri connettori di Intune. Ogni connettore deve essere in grado di creare oggetti computer in qualsiasi dominio che si desidera supportare.

> [!NOTE]
> Se l'organizzazione ha più domini e si installano più connettori Intune, è necessario usare un account del servizio che sia in grado di creare oggetti computer in tutti i domini, anche se si prevede di implementare il join Azure AD ibrido solo per un dominio specifico. Se si tratta di domini non trusted, è necessario disinstallare i connettori da domini in cui non si vuole usare Windows Autopilot. In caso contrario, con più connettori tra più domini, tutti i connettori devono essere in grado di creare oggetti computer in tutti i domini.

Intune Connector richiede gli [stessi endpoint di Intune](../intune/fundamentals/intune-endpoints.md).

1. Disattivare la Configurazione sicurezza avanzata IE. Per impostazione predefinita, in Windows Server la Configurazione sicurezza avanzata di Internet Explorer è attivata. Se non si è in grado di accedere al connettore Intune per Active Directory, disattivare la configurazione di sicurezza avanzata di IE per l'amministratore. [Come disattivare la Configurazione sicurezza avanzata di Internet Explorer](/archive/blogs/chenley/how-to-turn-off-internet-explorer-enhanced-security-configuration). 
2. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Dispositivi** > **Windows** > **Registrazione Windows** > **Connettore di Intune per Active Directory** > **Aggiungi**. 
3. Seguire le istruzioni per scaricare il connettore.
4. Aprire il file di installazione del connettore scaricato *ODJConnectorBootstrapper.exe* per installare il connettore.
5. Al termine dell'installazione selezionare **Configura**.
6. Selezionare **Accedi**.
7. Immettere le credenziali utente del ruolo Amministratore globale o Amministratore di Intune. 
 All'account utente deve essere assegnata una licenza di Intune.
8. Passare a **Dispositivi** > **Windows** > **Registrazione Windows** > **Connettore di Intune per Active Directory** e verificare che lo stato della connessione sia **Attivo**.

> [!NOTE]
> Dopo l'accesso, la visualizzazione del connettore nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) può richiedere qualche minuto. Il connettore viene visualizzato solo se può comunicare correttamente con il servizio Intune.

### <a name="configure-web-proxy-settings"></a>Configurare le impostazioni del proxy Web

Se nell'ambiente di rete è presente un proxy Web, vedere [Usare server proxy locali esistenti](../intune/enrollment/autopilot-hybrid-connector-proxy.md) per garantire il corretto funzionamento del connettore di Intune per Active Directory.


## <a name="create-a-device-group"></a>Creare un gruppo di dispositivi
1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Gruppi** > **Nuovo gruppo**.

1. Nel riquadro **gruppo** scegliere le opzioni seguenti:

    1. In **Tipo gruppo** selezionare **Sicurezza**.
    2. Immettere un **Nome gruppo** e una **Descrizione gruppo**.
    3. Selezionare un **Tipo di appartenenza**.

4. Se è stata selezionata l'opzione **dispositivi dinamici** per il tipo di appartenenza, nel riquadro **gruppo** selezionare **membri dispositivo dinamici**.

5. Nella casella **regola avanzata** immettere una delle righe di codice seguenti:
    - Per creare un gruppo che includa tutti i dispositivi Autopilot, digitare `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`.
    - Il campo Tag di gruppo di Intune è associato all'attributo OrderID nei dispositivi Azure AD. Se si vuole creare un gruppo che includa tutti i dispositivi Autopilot con un tag di gruppo specifico (OrderID), digitare: `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Per creare un gruppo che includa tutti i dispositivi Autopilot con un ID ordine di acquisto specifico, digitare `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`.
 
6. Selezionare **Salva**  >  **creazione**. 

## <a name="register-your-autopilot-devices"></a>Registrare i dispositivi di Autopilot

Selezionare uno dei modi seguenti per registrare i dispositivi di Autopilot.

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>Registrare i dispositivi di Autopilot che sono già registrati

1. Creare un profilo di distribuzione di Autopilot con l'opzione **Converti tutti i dispositivi interessati in Autopilot** impostata su **Sì**. 
2. Assegnare il profilo a un gruppo contenente i membri da registrare automaticamente in Autopilot.

Per altre informazioni, vedere [Creare un profilo di distribuzione Autopilot](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

### <a name="register-autopilot-devices-that-arent-enrolled"></a>Registrare i dispositivi di Autopilot che non sono registrati

Se i dispositivi non sono ancora registrati, è possibile registrarli. Per altre informazioni, vedere [Aggiungere dispositivi](enrollment-autopilot.md#add-devices).

### <a name="register-devices-from-an-oem"></a>Registrare i dispositivi da un OEM

Quando vengono acquistati nuovi dispositivi, alcuni OEM possono registrare i dispositivi per l'utente. Per ulteriori informazioni, vedere la pagina relativa alla [registrazione OEM](add-devices.md#oem-registration).

Prima di essere iscritti in Intune, i dispositivi Autopilot *registrati* vengono visualizzati in tre posizioni (con i nomi impostati sui numeri di serie):
- Il riquadro **Dispositivi di Autopilot** in Intune nel portale di Azure. Selezionare **Registrazione dispositivi** > **Registrazione Windows** > **Dispositivo**.
- Il riquadro **Dispositivi di Azure AD** in Intune nel portale di Azure. Selezionare **Dispositivi** > **Dispositivi di Azure AD**.
- Per visualizzare il riquadro **Tutti dispositivi** in Azure Active Directory nel portale di Azure selezionare **Dispositivi** > **Tutti i dispositivi**.

Dopo la *registrazione* i dispositivi di Autopilot vengono visualizzati in quattro posizioni:
- Il riquadro **Dispositivi di Autopilot** in Intune nel portale di Azure. Selezionare **Registrazione dispositivi** > **Registrazione Windows** > **Dispositivo**.
- Il riquadro **Dispositivi di Azure AD** in Intune nel portale di Azure. Selezionare **Dispositivi** > **Dispositivi di Azure AD**.
- Il riquadro **Tutti i dispositivi** in Azure Active Directory nel portale di Azure. Selezionare **Dispositivi** > **Tutti i dispositivi**.
- Il riquadro **Tutti i dispositivi** in Intune nel portale di Azure. Selezionare **Dispositivi** > **Tutti i dispositivi**.

Dopo la registrazione dei dispositivi di Autopilot, i nomi dei dispositivi diventano il nome host del dispositivo. Per impostazione predefinita, il nome host inizia con *DESKTOP-* .


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>Creare e assegnare un profilo di distribuzione AutoPilot
I profili di distribuzione AutoPilot vengono usati per configurare i dispositivi AutoPilot.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Windows** > **Registrazione Windows** > **Profili di distribuzione** > **Crea profilo**.
2. Nella pagina **Informazioni di base** specificare un **Nome** e una **Descrizione** facoltativa.
3. Se si vuole che tutti i dispositivi nei gruppi assegnati vengano automaticamente converti in Autopilot, impostare **Converti tutti i dispositivi interessati in Autopilot** su **Sì**. Tutti i dispositivi di proprietà dell'azienda non Autopilot nei gruppi assegnati verranno registrati con il servizio di distribuzione Autopilot. I dispositivi di proprietà personale non verranno convertiti in Autopilot. L'elaborazione della registrazione può richiedere fino a 48 ore. Quando la registrazione viene annullata e il dispositivo viene reimpostato, Autopilot eseguirà la registrazione. Dopo che un dispositivo è stato registrato in questo modo, se si disabilita o rimuove l'assegnazione del profilo, il dispositivo non verrà rimosso dal servizio di distribuzione di Autopilot. È invece necessario [rimuovere direttamente il dispositivo](enrollment-autopilot.md#delete-autopilot-devices).
4. Selezionare **Avanti**.
5. Nella pagina **Configurazione guidata** per **Modalità di distribuzione** selezionare **Definita dall'utente**.
6. Nella casella **Aggiungi ad Azure AD come** selezionare **Aggiunto ad Azure AD ibrido**.
7. Se si distribuiscono dispositivi fuori dalla rete dell'organizzazione usando il supporto VPN, impostare l'opzione **Ignora controllo connettività dominio** su **Sì**. Per altre informazioni, vedere [modalità guidata dall'utente per l'aggiunta di Azure Active Directory ibrido con supporto VPN](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support).
8. Se necessario, configurare le opzioni rimanenti nella pagina **Configurazione guidata**.
9. Selezionare **Avanti**.
10. Nella pagina **tag ambito** selezionare i [tag di ambito](../intune/fundamentals/scope-tags.md) per questo profilo.
11. Selezionare **Avanti**.
12. Nella pagina **Assegnazioni** selezionare **Selezionare i gruppi da includere** > cercare e selezionare il gruppo di dispositivi > **Seleziona**.
13. Selezionare **Avanti** > **Crea**.

Il passaggio dello stato del profilo del dispositivo da *Non assegnato* ad *Assegnazione* e infine ad *Assegnato* richiede circa 15 minuti.

## <a name="optional-turn-on-the-enrollment-status-page"></a>(Facoltativo) Attivare la pagina dello stato della registrazione

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Dispositivi** > **Windows** > **Registrazione Windows** > **Pagina relativa allo stato della registrazione**.
2. Nel riquadro **Pagina relativa allo stato della registrazione** selezionare **Predefinito** > **Impostazioni**.
3. Nella casella **Mostra lo stato dell'installazione di profili e applicazioni** scegliere **Sì**.
4. Configurare le altre opzioni in base alle proprie esigenze.
5. Selezionare **Salva**.

## <a name="create-and-assign-a-domain-join-profile"></a>Creare e assegnare un profilo di aggiunta al dominio

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare**Dispositivi** > **Profili di configurazione** > **Crea profilo**.
2. Immettere le proprietà seguenti:
    - **Nome**: immettere un nome descrittivo per il nuovo profilo.
    - **Descrizione**: Immettere una descrizione del profilo.
    - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
    - **Tipo di profilo**: selezionare **Aggiunta a un dominio (anteprima)** .
3. Selezionare **Impostazioni** e quindi specificare **Prefisso nome computer** e **Nome dominio**.
4. (Facoltativo) Specificare **Unità organizzativa** (OU) in [formato nome distinto (DN)](/windows/desktop/ad/object-names-and-identities#distinguished-name). Alcune delle opzioni possibili sono:
    - Specificare un'unità organizzativa in cui è stato delegato il controllo al dispositivo Windows 2016 che esegue Intune Connector.
    - Specificare un'unità organizzativa in cui è stato delegato il controllo ai computer radice nell'implementazione Active Directory locale.
    - Se questo campo viene lasciato vuoto, l'oggetto computer verrà creato nel contenitore predefinito Active Directory (CN=Computers se non è mai stato [modificato](https://support.microsoft.com/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom)).
 
    Ecco alcuni esempi validi:
      - OU=Level 1,OU=Level2,DC=contoso,DC=com
      - OU=Mine,DC=contoso,DC=com
 
    Di seguito sono riportati alcuni esempi che non sono validi:
      - CN = Computers, DC = contoso, DC = com (non è possibile specificare un contenitore, ma lasciare vuoto il valore per utilizzare l'impostazione predefinita per il dominio)
      - OU = Mine (è necessario specificare il dominio tramite il controller di dominio = attributi)
 
    > [!NOTE]
    > Non racchiudere tra virgolette il valore in **Unità organizzativa**.

5. Selezionare **OK** > **Crea**. Il profilo viene creato e visualizzato nell'elenco.
6. [Assegnare un profilo di dispositivo](../intune/configuration/device-profile-assign.md#assign-a-device-profile) allo stesso gruppo usato nel passaggio [creare un gruppo di dispositivi](windows-autopilot-hybrid.md#create-a-device-group). È possibile usare gruppi diversi se è necessario aggiungere dispositivi a diversi domini o unità organizzative.

> [!NOTE]
> Le funzionalità di denominazione per Windows Autopilot per l'aggiunta ad Azure AD ibrido non supportano le variabili, ad esempio %SERIAL%, e supportano solo i prefissi per il nome del computer.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato Windows AutoPilot, scoprire come gestire i dispositivi. Per altre informazioni, vedere [Informazioni sulla gestione dei dispositivi in Microsoft Intune](../intune/remote-actions/device-management.md).