---
title: Creare raccolte
titleSuffix: Configuration Manager
description: Creare raccolte in Configuration Manager per gestire più facilmente gruppi di utenti e dispositivi.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: def7a40091f6c9a45e67f5e4de7d7dca94b3cba2
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422819"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Come creare raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le raccolte costituiscono raggruppamenti di utenti o dispositivi. Usare le raccolte per attività come la gestione delle applicazioni, la distribuzione delle impostazioni di conformità o installazione degli aggiornamenti software. È anche possibile usare le raccolte per gestire gruppi di impostazioni client o con l'amministrazione basata sui ruoli per specificare le risorse accessibili per un utente amministratore. Configuration Manager contiene varie raccolte predefinite. Per altre informazioni, vedere [Introduction to Collections](introduction-to-collections.md) (Introduzione alle raccolte).  

> [!NOTE]  
> Una raccolta può contenere utenti o dispositivi, ma non entrambi.  


Le informazioni in questo articolo possono essere utili per creare le raccolte in Configuration Manager. È anche possibile importare le raccolte create nel sito di Configuration Manager corrente o in un altro. Per altre informazioni su come esportare e importare le raccolte, vedere [Come gestire le raccolte](manage-collections.md).  


## <a name="collection-rules"></a>Regole delle raccolte

Esistono diversi tipi di regole che è possibile usare per configurare i membri di una raccolta in Configuration Manager.  


### <a name="direct-rule"></a>Regola diretta

Usare le regole dirette per scegliere gli utenti o i computer da aggiungere a una raccolta. L'appartenenza non cambia a meno che non si rimuova una risorsa da Configuration Manager. Prima di poter aggiungere le risorse a una raccolta con regola diretta, è necessario che vengano individuate da Configuration Manager oppure che siano state importate. Le raccolte con regole dirette presentano un maggiore carico amministrativo rispetto alle raccolte con regole di query, dal momento che richiedono modifiche manuali.


### <a name="query-rule"></a>Regola di query

Consente di aggiornare in modo dinamico l'appartenenza di una raccolta con una query eseguita da Configuration Manager in base a una pianificazione. Ad esempio, è possibile creare una raccolta degli utenti membri dell'unità organizzativa Risorse umane in Servizi di dominio Active Directory. Questa raccolta viene aggiornata automaticamente in seguito all'aggiunta o alla rimozione di utenti nell'unità organizzativa Risorse umane.

Per esempi di query che è possibile usare per creare raccolte, vedere [Come creare query](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Regola categoria di dispositivi

È possibile semplificare la gestione dei dispositivi associando le categorie di dispositivi alle raccolte di dispositivi. 

Per altre informazioni, vedere [Classificare automaticamente i dispositivi in raccolte](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regola di inclusione raccolte

È possibile includere i membri di un'altra raccolta in una raccolta di Configuration Manager. Se la raccolta inclusa cambia, Configuration Manager aggiorna l'appartenenza della raccolta corrente in base a una pianificazione.

È possibile aggiungere più regole di inclusione raccolte in una raccolta.


### <a name="exclude-collection-rule"></a>Regola di esclusione raccolte

Le regole di esclusione raccolte consentono di escludere i membri di una raccolta da un'altra raccolta di Configuration Manager. Se la raccolta esclusa cambia, Configuration Manager aggiorna l'appartenenza della raccolta corrente in base a una pianificazione.

È possibile aggiungere più regole di esclusione raccolte in una raccolta. Se una raccolta include sia regole di inclusione raccolte che di esclusione raccolte e si verifica un conflitto, la regola di esclusione raccolte ha la priorità.

#### <a name="example"></a>Esempio
si crea una raccolta con una regola di inclusione raccolte e una di esclusione raccolte. La regola di inclusione è relativa a una raccolta di desktop Dell. La regola di esclusione è relativa a una raccolta di computer con meno di 4 GB di RAM. La nuova raccolta contiene i desktop Dell con almeno 4 GB di RAM.



## <a name="create-a-collection"></a><a name="bkmk_create"></a> Creare una raccolta  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**.  

    - Per creare una *raccolta di dispositivi*, selezionare il nodo **Raccolte dispositivi**. Nel gruppo **Crea** della scheda **Home** della barra multifunzione selezionare quindi **Crea raccolta dispositivi**.  

    - Per creare una *raccolta di utenti*, selezionare il nodo **Raccolte utenti**. Nel gruppo **Crea** della scheda **Home** della barra multifunzione selezionare quindi **Crea raccolta utenti**.  

2. Nella pagina **Generale** della procedura guidata inserire **Nome** e **Commento**. Nella sezione **Raccolta di limitazione** selezionare **Sfoglia** e quindi selezionare una raccolta di limitazione. La raccolta che si sta creando conterrà solo i membri della raccolta di limitazione.  

4. Nella pagina **Regole di appartenenza**, nell'elenco **Aggiungi regola** selezionare il tipo di regola di appartenenza da usare per la raccolta. È possibile configurare più regole per ogni raccolta. La configurazione varia in base alla regola. Per altre informazioni sulla configurazione di ogni regola, vedere le sezioni seguenti di questo articolo:  
    - [Regola diretta](#bkmk-direct)
    - [Regola di query](#bkmk-query)
    - [Regola categoria di dispositivi](#bkmk-category)
    - [Regola di inclusione raccolte](#bkmk-include)
    - [Regola di esclusione raccolte](#bkmk-exclude)

5. Nella pagina **Regole di appartenenza** esaminare inoltre le impostazioni seguenti.

    - **Utilizza aggiornamenti incrementali per questa raccolta**: selezionare questa opzione per eseguire periodicamente una scansione e aggiornare solo le risorse nuove o modificate rispetto alla valutazione raccolta precedente. Questo processo è indipendente da una valutazione raccolta completa. Per impostazione predefinita, gli aggiornamenti incrementali vengono eseguiti a intervalli di 5 minuti.  

        > [!IMPORTANT]  
        >  Le raccolte con regole di query che usano le classi seguenti non supportano gli aggiornamenti incrementali:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (per raccolte di soli utenti)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (per raccolte di soli utenti)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Pianifica un aggiornamento completo in questa raccolta**: pianificare una valutazione completa regolare dell'appartenenza alla raccolta.  

        A partire dalla versione 1810, queste modifiche del comportamento di valutazione delle raccolte possono migliorare le prestazioni del sito:<!--3607726-->  

        - In precedenza, quando si configurava una pianificazione per una raccolta basata su query, il sito continuava a valutare la query indipendentemente dall'impostazione **Pianifica un aggiornamento completo in questa raccolta**. Per disabilitare completamente la pianificazione, era necessario modificare la pianificazione impostando **Nessuno**.

            Ora il sito cancella la pianificazione quando si disabilita questa impostazione. Per specificare una pianificazione per la valutazione delle raccolte, abilitare l'opzione **Pianifica un aggiornamento completo in questa raccolta**.  

            Quando si aggiorna il sito, per qualsiasi raccolta esistente in cui è stata specificata una pianificazione, il sito abilita l'opzione **Pianifica un aggiornamento completo in questa raccolta**. Anche se questa configurazione potrebbe non essere lo scopo, era il comportamento effettivo della pianificazione prima dell'aggiornamento del sito. Per interrompere la valutazione di una raccolta in base a una pianificazione nel sito, disabilitare questa opzione.  

        - Non è possibile disabilitare la valutazione delle raccolte predefinite, come **Tutti i sistemi**, ma ora è possibile configurare la pianificazione. Questo comportamento consente di personalizzare questa azione in base ai requisiti specifici. 

            > [!TIP]  
            > Per le raccolte predefinite modificare solo l'impostazione **Ora** della pianificazione personalizzata. Non modificare **Criterio ricorrenza**. Le iterazioni future potrebbero imporre un criterio di ricorrenza specifico.  

6. Completare la procedura guidata per creare la nuova raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** .  

> [!NOTE]  
> È necessario aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta. I membri non vengono visualizzati nella raccolta fino a quando non viene eseguito il primo aggiornamento pianificato. È anche possibile selezionare manualmente il comando **Aggiorna appartenenza** per la raccolta. L'aggiornamento della raccolta potrebbe richiedere alcuni minuti.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a> Configurare una regola diretta  

1. Nella pagina **Cerca risorse** della **Creazione guidata regola di appartenenza diretta** specificare le informazioni seguenti.  

    - **Classe di risorse**: selezionare il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Ad esempio:
        - **Risorsa di sistema**: cercare i dati di inventario restituiti dai computer client.
        - **Computer sconosciuto**: selezionare tra i valori restituiti dai computer sconosciuti.
        - **Risorsa utente**: cercare informazioni sugli utenti raccolte da Configuration Manager.
        - **Risorsa gruppo utenti**: cercare informazioni sui gruppi di utenti raccolte da Configuration Manager.

    - **Nome attributo**: selezionare l'attributo associato alla classe di risorse selezionata che si vuole cercare. Ad esempio:  

        - Per selezionare i computer in base al relativo nome NetBIOS, selezionare **Risorsa di sistema** nell'elenco **Classe di risorse** e **Nome NetBIOS** nell'elenco **Nome attributo**.  

        - Per selezionare gli utenti in base al nome dell'unità organizzativa (OU), selezionare **Risorsa utente** nell'elenco **Classe di risorse** e **Nome unità organizzativa utente** nell'elenco **Nome attributo**.  

    - **Escludere le risorse contrassegnate come obsolete**: se un computer client è contrassegnato come obsoleto, non includere questo valore nei risultati della ricerca.  

    - **Escludere le risorse in cui non è installato il client di Configuration Manager**: queste risorse non verranno visualizzate nei risultati della ricerca.  

    - **Valore**: immettere un valore per la ricerca del nome di attributo selezionato. Usare il simbolo di percentuale (%) come carattere jolly. Ad esempio:  
        - Per cercare i computer con un nome NetBIOS che inizia con "M", immettere **M%** in questo campo.  
        - Per cercare gli utenti nell'unità organizzativa Contoso, immettere **Contoso** in questo campo.

2. Nella pagina **Seleziona risorse** selezionare le risorse da aggiungere alla raccolta nell'elenco **Risorse** e quindi selezionare **Avanti**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a> Configurare una regola di query  

Nella finestra di dialogo **Proprietà regola di query** specificare le informazioni seguenti.  

- **Nome**: specificare un nome univoco per la query.  

- **Importa istruzione query**: apre la finestra di dialogo **Sfoglia query**. Selezionare una [query di Configuration Manager](../../../servers/manage/create-queries.md) da usare come regola di query per la raccolta.   

- **Classe di risorse**: selezionare il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Selezionare un valore in **Risorsa di sistema** per cercare i dati di inventario restituiti dai computer client o **Computer sconosciuto** per effettuare una selezione tra i valori restituiti dai computer sconosciuti.  

- **Modifica istruzione query**: apre la finestra di dialogo **Proprietà istruzione query**, dove è possibile scrivere una query da usare come regola per la raccolta. Per altre informazioni sulle query, vedere [Introduzione alle query](../../../servers/manage/introduction-to-queries.md).  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a> Regola categoria di dispositivi

Nella finestra **Selezionare le categorie di dispositivi** sono disponibili le azioni seguenti.

- **Crea**: specificare un nome per creare una nuova categoria.
- **Rinomina**: consente di rinominare la categoria selezionata.
- **Elimina**: selezionare una o più categorie e usare questa azione per rimuoverle dall'elenco.

Per altre informazioni, vedere [Classificare automaticamente i dispositivi in raccolte](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a> Configurare una regola di inclusione raccolte  

Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da includere nella nuova raccolta e quindi selezionare **OK**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a> Configurare una regola di esclusione raccolte  

Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da escludere dalla nuova raccolta e quindi selezionare **OK**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a> Importare una raccolta  

Quando si esporta una raccolta da un sito, Configuration Manager la salva come file MOF (Managed Object Format). Usare questa procedura per importare il file nel database del sito. Per completare questa procedura, sono necessarie le autorizzazioni di **creazione** per la classe delle raccolte.

> [!IMPORTANT]  
> - Assicurarsi che il file contenga solo i dati della raccolta, provenga da una fonte attendibile e non sia stato manomesso.  
> 
> - Assicurarsi che il file sia stato esportato da un sito che esegue la stessa versione di Configuration Manager in uso.  

Per altre informazioni sull'esportazione di raccolte, vedere [Come gestire le raccolte](manage-collections.md).


1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Selezionare il nodo **Raccolte utenti** o **Raccolte dispositivi**.  

2. Nel gruppo **Crea** della scheda **Home** della barra multifunzione selezionare **Importa raccolte**.  

3. Nella pagina **Generale** dell'**Importazione guidata raccolte** selezionare **Avanti**.  

4. Nella pagina **Nome file MOF** selezionare **Sfoglia**. Passare al file MOF contenente le informazioni sulla raccolta da importare.  

5. Completare la procedura guidata per importare la raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte utenti** o **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** . Aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta appena importata.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a> Sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory

<!--3607475-->
> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1906 come [funzionalità di versione non definitiva](../../../servers/manage/pre-release-features.md). A partire dalla versione 2002, non è più una funzionalità di versione non definitiva.  

È possibile abilitare la sincronizzazione delle appartenenze alle raccolte con un gruppo di Azure Active Directory (Azure AD). Questa sincronizzazione consente di usare le regole di raggruppamento locali esistenti nel cloud creando appartenenze ai gruppi di Azure AD in base ai risultati delle appartenenze alle raccolte. È possibile sincronizzare raccolte di dispositivi. Solo i dispositivi con un record Azure Active Directory vengono riportati nel gruppo di Azure AD. Sono supportati sia i dispositivi aggiunti ad Azure AD ibrido che quelli aggiunti ad Azure Active Directory.

La sincronizzazione con Azure AD viene eseguita ogni cinque minuti. Si tratta di un processo unidirezionale, vale a dire da Configuration Manager ad Azure AD. Le modifiche apportate in Azure AD non si riflettono nelle raccolte di Configuration Manager, ma non vengano sovrascritte da Configuration Manager. Se ad esempio la raccolta di Configuration Manager ha due dispositivi e il gruppo di Azure AD ha tre dispositivi diversi, dopo la sincronizzazione il gruppo di Azure AD avrà cinque dispositivi.

### <a name="prerequisites"></a>Prerequisiti

- Integrazione con Azure AD per la [Gestione cloud](../../../servers/deploy/configure/azure-services-wizard.md)
- [Individuazione utente Azure Active Directory](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- Un punto di gestione abilitato per HTTPS o [HTTP avanzato](../../../plan-design/hierarchy/enhanced-http.md)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Creare un gruppo e impostare il proprietario in Azure AD

1. Passare a [https://portal.azure.com](https://portal.azure.com).
1. Passare ad **Azure Active Directory** > **Gruppi** > **Tutti i gruppi**.
1. Fare clic su **Nuovo gruppo** e digitare un **Nome gruppo** e, facoltativamente, una **Descrizione gruppo**.
1. Verificare che **Tipo di appartenenza** sia impostato su **Assegnato**.
1. Selezionare **Proprietari**, quindi aggiungere l'identità che creerà la relazione di sincronizzazione in Configuration Manager.
1. Fare clic su **Crea** per completare la creazione del gruppo di Azure AD.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Abilitare la sincronizzazione della raccolta per il servizio di Azure

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Servizi di Azure**.
1. Fare clic con il pulsante destro del mouse sul tenant Azure AD in cui è stato creato il gruppo e selezionare **Proprietà**.
1. Nella scheda **Sincronizzazione delle raccolte** selezionare la casella **Abilita la sincronizzazione dei gruppi di Azure Active Directory**.
1. Fare clic su **OK** per salvare l'impostazione.

### <a name="enable-the-collection-to-synchronize"></a>Abilitare la raccolta da sincronizzare

1. Nella console di Configuration Manager passare a **Asset e conformità** > **Panoramica** > **Raccolte dispositivi**.
1. Fare clic con il pulsante destro del mouse sulla raccolta da sincronizzare, quindi fare clic su **Proprietà**. 
1. Nella scheda **Sincronizzazione dei gruppi di AAD** fare clic su **Aggiungi**.
1. Dal menu a discesa selezionare il **Tenant** in cui è stato creato il gruppo di Azure AD.
1. Digitare i criteri di ricerca nel campo **Il nome inizia con**, quindi fare clic su **Cerca**.
  - Se viene richiesto di eseguire l'accesso, usare l'identità specificata come proprietario per il gruppo di Azure AD.
1. Selezionare il gruppo di destinazione, quindi fare clic su **OK** per aggiungere il gruppo e di nuovo su **OK** per uscire dalle proprietà della raccolta.
1. Prima di poter verificare l'appartenenza ai gruppi nel portale di Azure, è necessario attendere da 5 a 7 minuti.
   - Per avviare una sincronizzazione completa, fare clic con il pulsante destro del mouse sulla raccolta, quindi selezionare **Sincronizza appartenenza**.


### <a name="verify-the-azure-ad-group-membership"></a>Verificare l'appartenenza al gruppo di Azure AD

1. Passare a [https://portal.azure.com](https://portal.azure.com).
1. Passare ad **Azure Active Directory** > **Gruppi** > **Tutti i gruppi**.
1. Trovare il gruppo creato e selezionare **Membri**. 
1. Verificare che i membri riflettano quelli nella raccolta di Configuration Manager.
   - Solo i dispositivi con identità di Azure AD vengono visualizzati nel gruppo.


![Sincronizzare le raccolte in Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Uso di PowerShell

È possibile usare PowerShell per creare e importare raccolte. Per altre informazioni, vedere:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Passaggi successivi

[Gestire le raccolte](manage-collections.md)
