---
title: Impostare restrizioni di registrazione in Microsoft Intune
titleSuffix: ''
description: Limitare la registrazione dalla piattaforma e impostare un limite di registrazione dei dispositivi in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/17/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f13be3c277605f11a1b16e9bcd3484cf4cdc7027
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907059"
---
# <a name="set-enrollment-restrictions"></a>Impostare le restrizioni di registrazione

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Gli amministratori di Intune sono in grado di creare e gestire restrizioni di registrazione che definiscono quali dispositivi possono essere registrati per la gestione con Intune, tra cui:
- Numero di dispositivi.
- Sistemi operativi e versioni.

È possibile creare più restrizioni e applicarle a gruppi utenti diversi. È anche possibile impostare l'[ordine di priorità](#change-enrollment-restriction-priority) delle diverse restrizioni.

>[!NOTE]
>Le restrizioni di registrazione non sono una funzionalità di sicurezza. I dispositivi compromessi possano dare risultati non previsti. Queste restrizioni sono una barriera di massimo sforzo per gli utenti legittimi.

Le restrizioni di registrazione specifiche che è possibile creare includono:

- Numero massimo di dispositivi registrati.
- Piattaforme per dispositivi che possono registrare:
  - Amministratore dispositivo Android
  - Profilo di lavoro di Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows
- Versione del sistema operativo della piattaforma per iOS/iPadOS, amministratore di dispositivi Android, profilo di lavoro Android Enterprise e Windows.
  - Versione minima.
  - Versione massima.
- Limitare i [dispositivi di proprietà personale](device-enrollment.md#bring-your-own-device) (iOS, amministratore di dispositivi Android, profilo di lavoro Android Enterprise, macOS e Windows).

## <a name="default-restrictions"></a>Restrizioni predefinite

Per il tipo e il numero massimo di dispositivi vengono applicate automaticamente restrizioni predefinite che possono essere modificate. Le restrizioni predefinite si applicano a tutte le registrazioni, con e senza utente. È possibile sostituire queste impostazioni predefinite tramite la creazione di nuove restrizioni con priorità più alta.

## <a name="create-a-device-type-restriction"></a>Creare una restrizione dei tipi di dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione** > **Crea restrizione** > **Restrizione dei tipi di dispositivo**.
2. Nella pagina **Informazioni di base** specificare un **Nome** e una **Descrizione** facoltativa.
3. Scegliere **Avanti** per andare alla pagina **Impostazioni piattaforma**.
4. In **Piattaforma** scegliere **Consenti** per le piattaforme per cui consentire questa restrizione.
    ![Acquisizione schermo per la scelta delle impostazioni della piattaforma](./media/enrollment-restrictions-set/choose-platform-settings.png)
5. In **Versioni** scegliere le versioni minima e massima che si vuole vengano supportate dalle piattaforme consentite. Per iOS e Android, le restrizioni di versione si applicano solo ai dispositivi registrati con il Portale aziendale.
     I formati delle versioni supportate includono:
    - L'amministratore dei dispositivi Android e il profilo di lavoro Android Enterprise supportano major.minor.rev.build.
    - iOS/iPadOS supporta la versione major.minor.rev. Le versioni del sistema operativo non si applicano ai dispositivi Apple registrati in Device Enrollment Program, Apple School Manager o nell'app Apple Configurator.
    - Windows supporta il formato major.minor.build.rev solo per Windows 10.
    
    > [!IMPORTANT]
    > Il comportamento delle piattaforme Android Enterprise (profilo di lavoro) e per gli amministratori di dispositivi Android è il seguente:
    > - Se entrambe le piattaforme sono consentite per lo stesso gruppo, gli utenti verranno registrati con un profilo di lavoro se il dispositivo lo supporta. In caso contrario, verranno registrati come amministratore del dispositivo. 
    > - Se entrambe le piattaforme sono consentite per il gruppo e perfezionate per versioni specifiche e non sovrapposte, gli utenti riceveranno il flusso di registrazione definito per la versione del sistema operativo in uso. 
    > - Se entrambe le piattaforme sono consentite ma bloccate per le stesse versioni, gli utenti nei dispositivi con le versioni bloccate verranno esclusi dal flusso di registrazione dell'amministratore del dispositivo Android e quindi verrà loro impedita la registrazione e verrà richiesto di disconnettersi. 
    >
    > Vale la pena sottolineare che sia la registrazione di un profilo di lavoro che quella di amministratore del dispositivo funzioneranno solo se sono stati completati i prerequisiti appropriati nella registrazione di Android. 
    
   > [!Note]
   > Windows 10 non specifica il numero di revisione durante la registrazione, quindi se si immette ad esempio 10.0.17134.100 e il dispositivo è 10.0.17134.174, il dispositivo verrà bloccato durante la registrazione.

6. In **Di proprietà personale** scegliere **Consenti** per le piattaforme da consentire come dispositivi personali.
7. In **Produttore dispositivo** immettere un elenco di produttori delimitato da virgole che si vuole bloccare.
8. Scegliere **Avanti** per passare alla pagina **Tag di ambito**.
9. Se si desidera, è possibile aggiungere i tag di ambito che si vogliono applicare a queste restrizioni sulla pagina **Tag di ambito**. Per altre informazioni sui tag di ambito, vedere [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito). Quando si usano i tag di ambito con restrizioni di registrazione, gli utenti possono riordinare solo i criteri per i quali hanno un ambito. Inoltre, possono riordinare solo le posizioni dei criteri per i quali hanno un ambito. Gli utenti visualizzano il vero numero di priorità dei criteri in ogni criterio. Un utente con ambito può indicare la priorità relativa dei criteri anche se non è in grado di visualizzare tutti gli altri criteri.
10. Scegliere **Avanti** per passare alla pagina **Assegnazioni**.
11. Scegliere **Selezionare i gruppi da includere** e usare la casella di ricerca per trovare i gruppi da includere in questa restrizione. La restrizione si applica solo ai gruppi a cui è assegnata. La restrizione ha effetto solo se viene assegnata ad almeno un gruppo. Quindi scegliere **Seleziona**. 
    ![Acquisizione schermo per la scelta delle impostazioni della piattaforma](./media/enrollment-restrictions-set/select-groups.png)
12. Selezionare **Avanti** per passare alla pagina **Rivedi e crea**.
13. Selezionare **Crea** per creare la restrizione.
14. La nuova restrizione viene creata con una priorità di livello immediatamente superiore a quello dell'impostazione predefinita. È possibile [modificare la priorità](#change-enrollment-restriction-priority).


## <a name="create-a-device-limit-restriction"></a>Creare una restrizione sul limite di dispositivi

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione** > **Crea restrizione** > **Restrizione sul limite di dispositivi**.
2. Nella pagina **Informazioni di base** specificare un **Nome** e una **Descrizione** facoltativa.
3. Scegliere **Avanti** per passare alla pagina **Limite di dispositivi**.
4. Per **Limite di dispositivi** selezionare il numero massimo di dispositivi che un utente può registrare.
    ![Acquisizione schermo per la scelta del limite di dispositivi](./media/enrollment-restrictions-set/choose-device-limit.png)
5. Scegliere **Avanti** per passare alla pagina **Tag di ambito**.
6. Se si desidera, è possibile aggiungere i tag di ambito che si vogliono applicare a queste restrizioni sulla pagina **Tag di ambito**. Per altre informazioni sui tag di ambito, vedere [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito). Quando si usano i tag di ambito con restrizioni di registrazione, gli utenti possono riordinare solo i criteri per i quali hanno un ambito. Inoltre, possono riordinare solo le posizioni dei criteri per i quali hanno un ambito. Gli utenti visualizzano il vero numero di priorità dei criteri in ogni criterio. Un utente con ambito può indicare la priorità relativa dei criteri anche se non è in grado di visualizzare tutti gli altri criteri.
7. Scegliere **Avanti** per passare alla pagina **Assegnazioni**.
8. Scegliere **Selezionare i gruppi da includere** e usare la casella di ricerca per trovare i gruppi da includere in questa restrizione. La restrizione si applica solo ai gruppi a cui è assegnata. La restrizione ha effetto solo se viene assegnata ad almeno un gruppo. Quindi scegliere **Seleziona**. 
    ![Acquisizione schermo per la selezione dei gruppi](./media/enrollment-restrictions-set/select-groups-device-limit.png)
9. Selezionare **Avanti** per passare alla pagina **Rivedi e crea**.
10. Selezionare **Crea** per creare la restrizione.
11. La nuova restrizione viene creata con una priorità di livello immediatamente superiore a quello dell'impostazione predefinita. È possibile [modificare la priorità](#change-enrollment-restriction-priority).

Durante le registrazioni BYOD viene visualizzata una notifica che informa gli utenti quando raggiungono il limite di dispositivi registrati. Ad esempio, in iOS:

![notifica iOS per il limite di dispositivi](./media/enrollment-restrictions-set/enrollment-restrictions-ios-set-limit-notification.png)

> [!IMPORTANT]
> Le restrizioni sul limite di dispositivi non vengono applicate ai tipi di registrazione di Windows seguenti:
> - Registrazioni con co-gestione
> - Registrazioni di oggetti Criteri di gruppo
> - Registrazioni aggiunte ad Azure Active Directory
> - Registrazioni in blocco aggiunte ad Azure Active Directory
> - Registrazioni di AutoPilot
> - Registrazioni di manager di registrazione dispositivi
>
> Le restrizioni sul limite di dispositivi non vengono applicate a questi tipi di registrazione perché sono considerati scenari di dispositivi condivisi.
> È possibile impostare limiti rigidi per questi tipi di registrazione [in Azure Active Directory](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).


## <a name="change-enrollment-restrictions"></a>Modificare le restrizioni di registrazione

È possibile modificare le impostazioni relative alle restrizioni di registrazione tramite la procedura seguente. Queste restrizioni non influiscono sui dispositivi già registrati. I dispositivi registrati con l'[agente del computer di Intune](../fundamentals/manage-windows-pcs-with-microsoft-intune.md) non possono essere bloccati con questa funzionalità.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **Restrizioni registrazione** > scegliere la restrizione da modificare > **Proprietà**.
2. Scegliere **Modifica** accanto alle impostazioni da modificare.
3. Nella pagina **Modifica** apportare le modifiche necessarie, passare alla pagina **Verifica e salva** e quindi scegliere **Salva**.


## <a name="blocking-personal-android-devices"></a>Blocco dei dispositivi Android personali
- Anche se si blocca la registrazione dei dispositivi dell'amministratore di dispositivi Android di proprietà personale, i dispositivi del profilo di lavoro Android Enterprise di proprietà personale possono ancora essere registrati.
- Per impostazione predefinita, le impostazioni dei dispositivi del profilo di lavoro Android Enterprise corrispondono alle impostazioni dei dispositivi dell'amministratore di dispositivi Android. Dopo la modifica delle impostazioni del profilo di lavoro Android Enterprise o dell'amministratore del dispositivo Android, questa corrispondenza andrà persa.
- Se si blocca la registrazione dei dispositivi del profilo di lavoro Android Enterprise personali, solo i dispositivi Android aziendali possono essere registrati con i profili di lavoro Android Enterprise.

## <a name="blocking-personal-windows-devices"></a>Blocco dei dispositivi Windows personali
Se si blocca la registrazione dei dispositivi Windows personali, Intune verifica che ogni nuova richiesta di registrazione Windows sia stata autorizzata come registrazione aziendale. Le registrazioni non autorizzate verranno bloccate.

I metodi seguenti si qualificano per essere autorizzati come registrazione aziendale Windows:
- L'utente che esegue la registrazione usa un [account del manager di registrazione dispositivi]( device-enrollment-manager-enroll.md).
- Il dispositivo viene registrato tramite [Windows Autopilot](../../autopilot/enrollment-autopilot.md).
- Il dispositivo viene registrato con Windows Autopilot ma non è un'opzione di sola registrazione MDM dalle impostazioni di Windows.
- Il numero IMEI del dispositivo è indicato in **Registrazione del dispositivo** >  **[Identificatori dei dispositivi aziendali](corporate-identifiers-add.md)** .
- Il dispositivo viene registrato tramite un [pacchetto di provisioning in blocco](windows-bulk-enroll.md).
- Il dispositivo viene registrato tramite un oggetto Criteri di gruppo o la [registrazione automatica da Configuration Manager per la co-gestione](/configmgr/comanage/quickstart-paths#bkmk_path1).
 
Le registrazioni seguenti sono contrassegnate come aziendali da Intune, ma dal momento che non offrono all'amministratore di Intune il controllo per ogni dispositivo, vengono bloccate:
- La [registrazione automatica al software MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) con l'[aggiunta ad Azure Active Directory durante la configurazione di Windows](/azure/active-directory/device-management-azuread-joined-devices-frx)\*.
- La [registrazione automatica al software MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) con [aggiunta ad Azure Active Directory dalle impostazioni di Windows](/azure/active-directory/user-help/user-help-register-device-on-network)*.
 
Verranno bloccati anche i seguenti metodi di registrazione personale:
- La [registrazione automatica al software MDM](windows-enroll.md#enable-windows-10-automatic-enrollment) con [aggiunta dell'account aziendale dalle impostazioni di Windows](/azure/active-directory/user-help/user-help-join-device-on-network)\*.
- Solo l'[opzione di registrazione MDM]( /windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) dalle impostazioni di Windows.

\* Questi elementi non verranno bloccati se la registrazione avviene con Autopilot.


## <a name="blocking-personal-iosipados-devices"></a>Blocco dei dispositivi iOS/iPadOS personali
Per impostazione predefinita, Intune classifica i dispositivi iOS/iPadOS come dispositivi di proprietà personale. Per essere classificato come di proprietà dell'azienda, un dispositivo iOS/iPadOS deve soddisfare una delle condizioni seguenti:
- [Deve essere registrato con un numero di serie](corporate-identifiers-add.md).
- Deve essere registrato con la registrazione automatica dei dispositivi (in precedenza DEP, Device Enrollment Program)


## <a name="change-enrollment-restriction-priority"></a>Modificare la priorità delle restrizioni di registrazione

La priorità viene usata se un utente appartiene a più gruppi a cui sono assegnate restrizioni. Gli utenti sono soggetti solo alla restrizione con priorità più alta assegnata a un gruppo di cui fanno parte. Si supponga ad esempio che Joe appartenga al gruppo A, a cui sono assegnate restrizioni con priorità 5, e anche al gruppo B, a cui sono assegnate restrizioni con priorità 2. Joe è soggetto solo alle restrizioni con priorità 2.

Quando si crea una restrizione, questa viene aggiunta all'elenco al livello immediatamente superiore a quello dell'impostazione predefinita.

La registrazione di dispositivi prevede restrizioni predefinite sia per il tipo che per il numero di dispositivi. Queste due restrizioni si applicano a tutti gli utenti, a meno che non vengano sostituite da restrizioni con priorità più alta.

>[!NOTE]
>Le restrizioni di registrazione vengono applicate agli utenti. Negli scenari di registrazione non gestiti dall'utente, ad esempio la modalità di distribuzione automatica di Windows Autopilot o il provisioning in modalità "White Glove", verranno applicate solo le restrizioni di priorità predefinite (destinate a "Tutti gli utenti").


È possibile modificare la priorità di tutte le restrizioni non predefinite.

1. Accedere al portale di Azure.
2. Selezionare **Altri servizi**, cercare **Intune** e quindi scegliere **Intune**.
3. Selezionare **Registrazione del dispositivo** > **Restrizioni registrazione**.
4. Passare il puntatore del mouse sulla restrizione nell'elenco delle priorità.
5. Usando i tre punti verticali, trascinare la priorità nella posizione voluta nell'elenco.