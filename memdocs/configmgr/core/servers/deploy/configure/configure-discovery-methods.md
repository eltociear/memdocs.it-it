---
title: Configurare l'individuazione
titleSuffix: Configuration Manager
description: Configurare i metodi di individuazione per trovare le risorse da gestire dalla rete, Active Directory e Azure Active Directory.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cfda27df7df537ededb1f103afdd6107354af786
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347288"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configurare i metodi di individuazione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configurare i metodi di individuazione per trovare le risorse da gestire dalla rete, Active Directory e Azure Active Directory (Azure AD). Abilitare e configurare i metodi che si vogliono usare per eseguire ricerche nell'ambiente. È anche possibile disabilitare un metodo seguendo la stessa procedura usata per abilitarlo. Le uniche eccezioni a tale procedura sono il metodo di individuazione heartbeat e di individuazione server:  

- Per impostazione predefinita, l'**individuazione heartbeat** è già abilitata quando si installa un sito primario di Configuration Manager. È configurata per l'esecuzione secondo una pianificazione di base. Lasciare l'individuazione heartbeat abilitata. In questo modo si garantisce che i record dei dati di individuazione per i dispositivi siano aggiornati. Per altre informazioni sull'individuazione heartbeat, vedere [Informazioni sull'individuazione heartbeat](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- L'**individuazione server** è un metodo di individuazione automatica. Individua i computer in uso come sistemi del sito. Non è possibile configurare o disabilitare questo metodo.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Individuazione foresta Active Directory  

Per completare la configurazione dell'individuazione foresta Active Directory, configurare le impostazioni nelle posizioni seguenti della console di Configuration Manager:  

- Nel nodo **Metodi di individuazione**:

  - Abilitare il metodo di individuazione.  

  - Impostare una pianificazione del polling.  

  - Determinare se l'individuazione crea automaticamente limiti per le subnet e i siti di Active Directory individuati.  

- Nel nodo **Foreste Active Directory**:

  - Aggiungere foreste da individuare.  

  - Abilitare l'individuazione di siti e subnet di Active Directory in quella foresta.  

  - Configurare impostazioni che consentono ai siti di Configuration Manager di pubblicare le informazioni sul sito nella foresta.  

  - Assegnare un account da usare come Account foresta Active Directory per ogni foresta.  

Usare le procedure seguenti per attivare l'individuazione foresta Active Directory e per configurare singole foreste per l'uso con l'individuazione foresta Active Directory.  

### <a name="configure-active-directory-forest-discovery"></a>Configurare l'individuazione foresta Active Directory  

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Metodi di individuazione**.  

2. Selezionare il metodo Individuazione foresta Active Directory per il sito in cui si desidera configurare l'individuazione.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà**.  

4. Nella scheda **Generale** delle proprietà configurare le impostazioni seguenti:  

    - Abilitare il metodo di individuazione.

    - Specificare le opzioni per creare i limiti del sito per i percorsi individuati.  

    - Specificare una pianificazione per l'esecuzione dell'individuazione.  

5. Selezionare **OK** per salvare la configurazione.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Configurare una foresta per l'individuazione foresta Active Directory  

1. Nell'area di lavoro **Amministrazione** espandere **Configurazione della gerarchia** e selezionare il nodo **Foreste Active Directory**. Se in precedenza è stato eseguito il metodo di individuazione foresta Active Directory, è possibile visualizzare ogni foresta rilevata nel riquadro dei risultati. L'esecuzione di questo metodo consente di individuare la foresta locale e le foreste trusted. Aggiungere manualmente foreste non trusted.  

    - Per configurare una foresta individuata in precedenza, selezionarla nel riquadro dei risultati. Nella barra multifunzione selezionare **Proprietà** per aprire le proprietà della foresta.

    - Per configurare una nuova foresta non presente nell'elenco, nella scheda **Home** della barra multifunzione selezionare **Aggiungi foresta** nel gruppo **Crea**. Verrà aperta la finestra di dialogo **Add Forests** (Aggiungi foreste).

2. Nella scheda **Generale** completare le configurazioni per la foresta che si vuole individuare e specificare un valore per **Account foresta Active Directory**. Per ulteriori informazioni su questo account, vedere [Account](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > Il metodo di individuazione della foresta Active Directory richiede un account globale per l'individuazione e la pubblicazione in foreste non trusted. Se non si usa l'account computer del server del sito, è possibile selezionare solo un account globale.  

3. Se si prevede di consentire ai siti di pubblicare i relativi dati in questa foresta, completare le configurazioni per la pubblicazione in questa foresta nella scheda **Pubblicazione**.  

    > [!NOTE]  
    > Se si consente ai siti di pubblicare in una foresta, estendere lo schema di Active Directory di tale foresta per Configuration Manager. L'account foresta Active Directory deve disporre delle autorizzazioni di tipo Controllo completo sul contenitore di sistema di tale foresta.  

4. Selezionare **OK** per salvare la configurazione.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Individuazione di Active Directory per computer, utenti o gruppi  

Per configurare l'individuazione di computer, utenti o gruppi, iniziare con questi passaggi comuni:

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Metodi di individuazione**.  

2. Selezionare il metodo per il sito in cui si desidera configurare l'individuazione.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà**.  

4. Nella scheda **Generale** delle proprietà selezionare la casella di controllo per abilitare l'individuazione. In alternativa è possibile configurare subito l'individuazione e abilitarla in un secondo momento.  

Usare quindi le informazioni nelle sezioni seguenti per configurare metodi di individuazione specifici:  

- [Individuazione gruppo Active Directory](#bkmk_config-adgd)  

- [Individuazione sistema Active Directory](#bkmk_config-adgd)  

- [Individuazione utente Active Directory](#bkmk_config-adud)  

> [!NOTE]  
> Le informazioni contenute in questa sezione non si applicano all'individuazione foresta Active Directory.  

Anche se ogni metodo di individuazione è indipendente dagli altri, tutti condividono opzioni simili. Per altre informazioni su queste opzioni di configurazione, vedere [Opzioni condivise per l'individuazione di gruppi, sistemi e utenti](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> Il polling di Active Directory da ciascuno di questi metodi di individuazione può generare notevole traffico di rete. È consigliabile pianificare ogni metodo di individuazione in modo che venga eseguito in un momento in cui il traffico di rete non condizioni negativamente gli usi aziendali della rete.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a> Configurare l'individuazione gruppo Active Directory  

1. Nella scheda **Generale** della finestra delle proprietà di individuazione gruppo Active Directory selezionare **Aggiungi** per configurare un ambito di individuazione. Selezionare **Gruppi** o **Percorso**. Completare quindi le configurazioni seguenti nella finestra di dialogo **Aggiungi gruppi** o **Aggiungi percorso di Active Directory**:  

    1. Specificare un **Nome** per questo ambito di individuazione.  

    2. Specificare un **Dominio Active Directory** o **Percorso** per la ricerca:  

        - Se si sceglie **Gruppi**, specificare uno o più gruppi di Active Directory da individuare.  

        - Se si sceglie **Percorso**, specificare un contenitore Active Directory come percorso da individuare. È anche possibile attivare una ricerca ricorsiva dei contenitori figlio di Active Directory per questo percorso.  

    3. In **Account di individuazione gruppo Active Directory** indicare l'account usato dal sito per la ricerca nell'ambito di individuazione. Per altre informazioni, vedere [Account](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Scegliere **OK** per salvare la configurazione dell'ambito di individuazione.  

2. Ripetere i passaggi precedenti per ogni ambito di individuazione aggiuntivo da definire.  

3. Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.

4. Nella scheda **Opzioni** configurare le impostazioni di filtro per escludere dall'individuazione i record dei computer non aggiornati. È anche possibile configurare l'individuazione dell'appartenenza dei gruppi di distribuzione.  

    > [!NOTE]  
    > Per impostazione predefinita, l'individuazione gruppo Active Directory rileva solo l'appartenenza dei gruppi di sicurezza.  

5. Selezionare **OK** per salvare la configurazione.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a> Configurare l'individuazione sistema Active Directory  

1. Nella scheda **Generale** della finestra delle proprietà di individuazione sistema Active Directory selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif) per specificare un nuovo contenitore Active Directory. Nella finestra di dialogo **Contenitore Active Directory** completare le configurazioni seguenti:  

    1. Digitare o cercare un percorso in **Percorso**. Questo valore è un percorso LDAP valido di un contenitore o un'unità organizzativa (OU). Il sito esegue query su questo percorso per le risorse. Ad esempio: `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Specificare le opzioni che modificano il comportamento di ricerca:  

        - **Individua oggetti all'interno dei gruppi di Active Directory**: il sito analizza anche l'appartenenza dei gruppi in questo percorso.  

        - **Esegui ricerca ricorsiva nei contenitori figlio di Active Directory**: se si abilita questa opzione, il sito esegue la ricerca in altre unità organizzative o contenitori nel percorso specificato. Se si disabilita questa opzione, il sito esegue la ricerca delle risorse solo nel percorso specifico.  

          A partire dalla versione 1806, selezionare i sottocontenitori da escludere da questa ricerca ricorsiva. Questa opzione consente di ridurre il numero di oggetti individuati. Selezionare **Aggiungi** per scegliere i contenitori nel percorso specificato. Nella finestra di dialogo Seleziona nuovo contenitore selezionare un contenitore figlio da escludere. Selezionare **OK** per chiudere la finestra di dialogo Seleziona nuovo contenitore.<!--1358143-->

          > [!Tip]  
          > L'elenco di contenitori Active Directory nella finestra delle proprietà di individuazione sistema Active Directory include una colonna **Con esclusioni**. Quando si selezionano i contenitori da escludere, questo valore è **Sì**.  

    3. Specificare per ogni percorso l'account da utilizzare come **Account di individuazione Active Directory**. Per altre informazioni, vedere [Account](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Per ogni percorso specificato, è possibile configurare una serie di opzioni di individuazione e un account di individuazione Active Directory univoco.  

    4. Scegliere **OK** per salvare la configurazione dei contenitori Active Directory.  

2. Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

3. Nella scheda **Attributi di Active Directory** configurare gli attributi aggiuntivi di Active Directory per i computer da individuare. In questa scheda sono elencati gli attributi degli oggetti predefiniti.  

    > [!Tip]  
    > Ad esempio, l'organizzazione usa l'attributo **Description** nell'account computer in Active Directory. Selezionare **Personalizzato** e aggiungere `Description` come attributo personalizzato. Quando viene eseguito il metodo di individuazione, questo attributo viene visualizzato nella scheda delle proprietà del dispositivo nella console di Configuration Manager.<!--513948-->  

4. Nella scheda **Opzioni** configurare le impostazioni di filtro per escludere dall'individuazione i record dei computer non aggiornati.  

5. Selezionare **OK** per salvare la configurazione.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a> Configurare l'individuazione utente Active Directory  

1. Nella scheda **Generale** della finestra delle proprietà di individuazione utente Active Directory selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif) per specificare un nuovo contenitore Active Directory. Nella finestra di dialogo **Contenitore Active Directory** completare le configurazioni seguenti:  

    1. Specificare uno o più percorsi in cui eseguire la ricerca.  

    2. Per ogni percorso, specificare le opzioni che modificano il comportamento di ricerca.  

    3. Specificare per ogni percorso l'account da utilizzare come **Account di individuazione Active Directory**. Per altre informazioni, vedere [Account](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Per ogni percorso specificato, è possibile configurare un'unica serie di opzioni di individuazione e un account di individuazione Active Directory univoco.  

    4. Scegliere **OK** per salvare la configurazione dei contenitori Active Directory.  

2. Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

3. Nella scheda **Attributi di Active Directory** configurare gli attributi aggiuntivi di Active Directory per i computer da individuare. In questa scheda sono elencati gli attributi degli oggetti predefiniti.  

4. Selezionare **OK** per salvare la configurazione.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a> Individuazione utenti di Azure AD

L'individuazione utenti di AD Azure non viene abilitata o configurata come altri metodi di individuazione. È necessario configurarla durante il caricamento del sito di Configuration Manager in Azure AD.

Per altre informazioni, vedere [Individuazione utenti di Azure AD](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Prerequisiti

Per abilitare e configurare questo metodo di individuazione, [Configurare i servizi di Azure](azure-services-wizard.md) per la **gestione cloud**.

Se si usa Configuration Manager per *creare* l'app Azure, questa viene configurata con le autorizzazioni necessarie.

Se si crea prima l'app in Azure e quindi la si *importa* in Configuration Manager, sarà necessario configurare l'app manualmente. Questa configurazione include la concessione all'app server dell'autorizzazione per leggere i dati della directory.

1. Aprire il [portale di Azure](https://portal.azure.com) come utente con autorizzazioni di *amministratore globale*. Passare ad **Azure Active Directory** e selezionare **Registrazioni app**. Passare a **Tutte le applicazioni**, se necessario.

1. Selezionare l'applicazione di destinazione.

1. Nel menu **Gestisci** selezionare **Autorizzazioni API**.  

    1. Nel pannello **Autorizzazioni API** selezionare **Aggiungi un'autorizzazione**.  

    2. Nel pannello **Richiedi le autorizzazioni dell'API** passare a **API usate dall'organizzazione**.  

    3. Cercare e selezionare l'API **Microsoft Graph**.  

        > [!Tip]
        > Nella versione 1810 e precedenti usare l'API **Azure Active Directory Graph**.

    4. Selezionare il gruppo **Autorizzazioni applicazione**. Espandere **Directory** e selezionare **Directory.Read.All**.  

    5. Selezionare **Aggiungi autorizzazioni**.  

1. Nella sezione **Fornisci il consenso** del pannello **Autorizzazioni API** selezionare **Concedi consenso amministratore...** . Selezionare **Sì**.  

### <a name="configure-azure-ad-user-discovery"></a>Configurare l'individuazione utenti di Azure AD

Durante la configurazione del servizio di Azure **Gestione cloud**:

- Nella pagina **Individuazione** della procedura guidata selezionare l'opzione **Abilita l'individuazione utente di Azure Active Directory**.
- Selezionare **Impostazioni**.
- Nella finestra di dialogo Impostazioni dell'individuazione utenti di Azure AD configurare una pianificazione per l'esecuzione dell'individuazione. È anche possibile abilitare l'individuazione differenziale che verifica solo gli account nuovi o modificati in Azure AD.

> [!Note]  
> Se l'utente è un'identità federata o sincronizzata, è necessario usare l'[individuazione utente Active Directory](about-discovery-methods.md#bkmk_aboutUser) di Configuration Manager nonché l'individuazione utenti di Azure AD. Per altre informazioni sulle identità ibride, vedere [Definire una strategia di adozione della soluzione ibrida di gestione delle identità](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Individuazione dei gruppi utenti di Azure AD

<!--3611956-->
> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1906 come [funzionalità di versione non definitiva](../../manage/pre-release-features.md). A partire dalla versione 2002, non è più una funzionalità di versione non definitiva.  

È possibile individuare gruppi di utenti e i relativi membri in Azure AD. Quando il sito trova utenti in precedenza non individuati nei gruppi di Azure AD, li aggiunge come nuove risorse utente in Configuration Manager. Quando il gruppo è un gruppo di sicurezza viene creato un record di risorsa gruppo utenti.

### <a name="prerequisites"></a>Prerequisiti

- [Servizio di Azure](azure-services-wizard.md) Gestione cloud
- Autorizzazione alla lettura e ricerca di gruppi di Azure AD

### <a name="limitations"></a>Limitazioni

L'individuazione delta per l'individuazione dei gruppi di utenti di Azure AD è disabilitata nella versione 1906. È possibile abilitarla a partire da Configuration Manager versione 1910.

### <a name="log-files"></a>File di registro

Usare SMS_AZUREAD_DISCOVERY_AGENT.log per la risoluzione dei problemi. Questo log viene anche condiviso con l'individuazione utenti di Azure AD. Per altre informazioni, vedere [File di log](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Abilitare l'individuazione dei gruppi utenti di Azure AD

Per abilitare l'individuazione in un servizio di Azure per la **gestione cloud** esistente:

1. Passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e quindi selezionare il nodo **Servizi di Azure**.
1. Selezionare uno dei servizi di Azure e quindi selezionare **Proprietà** nella barra multifunzione.
1. Nella scheda **Individuazione** selezionare la casella **Abilita l'individuazione gruppo di Azure Active Directory**, quindi selezionare **Impostazioni**.
1. Selezionare **Aggiungi** nella scheda **Ambiti di individuazione**.
    - È possibile modificare la **Pianificazione del polling** nell'altra scheda.
1. Selezionare uno o più gruppi utenti. È possibile **cercare** in base al nome e scegliere se si vuole visualizzare **Solo gruppi di sicurezza**.
    - Quando si seleziona **Cerca** per la prima volta, viene richiesto di accedere ad Azure.
1. Dopo aver selezionato i gruppi, scegliere **OK**.
1. Al termine dell'individuazione sarà possibile visualizzare i gruppi utenti di Azure AD nel nodo **Utenti**.

Per abilitare l'individuazione durante la configurazione di un nuovo servizio di Azure per la **gestione cloud**:

- Nella pagina **Individuazione** della procedura guidata selezionare l'opzione **Abilita l'individuazione gruppo di Azure Active Directory**.
- Selezionare **Impostazioni**.
- Nella finestra di dialogo Impostazioni di individuazione gruppi di Azure AD configurare l'ambito di individuazione e una pianificazione per l'esecuzione dell'individuazione.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Individuazione heartbeat

Configuration Manager abilita il metodo di individuazione heartbeat quando si installa un sito primario. Se si vuole usare la pianificazione predefinita eseguita ogni sette giorni, non sono necessarie altre configurazioni. In caso contrario, è necessario configurare solo la pianificazione della frequenza di invio dei record dei dati di individuazione heartbeat a un punto di gestione da parte dei client.  

> [!NOTE]  
> Se si abilitano sia l'installazione push client che l'attività di manutenzione del sito per **Cancella flag di installazione** nello stesso sito, impostare la pianificazione dell'individuazione heartbeat in modo che sia inferiore al valore di **Periodo nuova individuazione client** dell'attività di manutenzione del sito **Cancella flag di installazione**. Per altre informazioni sulle attività di manutenzione del sito, vedere [Attività di manutenzione](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Configurare la pianificazione dell'individuazione heartbeat  

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Metodi di individuazione**.  

2. Selezionare il metodo **Individuazione heartbeat** per il sito in cui si vuole configurare l'individuazione heartbeat.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà**.  

4. Configurare la frequenza con cui i client inviano i record dei dati di individuazione heartbeat. Selezionare quindi **OK** per salvare la configurazione.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Individuazione di rete  

Prima di configurare l'individuazione di rete, acquisire familiarità con gli argomenti seguenti:  

- Livelli disponibili per l'individuazione della rete  

- Opzioni disponibili per l'individuazione della rete  

- Applicazione di limiti all'individuazione della rete in rete  

Per altre informazioni, vedere [Informazioni sull'individuazione di rete](about-discovery-methods.md#bkmk_aboutNetwork).  

Nelle sezioni seguenti vengono fornite informazioni sulle configurazioni comuni per l'individuazione della rete. È possibile definire una o più di queste configurazioni per l'utilizzo durante la stessa esecuzione dell'individuazione. Se si usano più configurazioni, considerare le interazioni che possono influenzare i risultati dell'individuazione.  

Ad esempio, si individuano tutti i dispositivi SNMP (Simple Network Management Protocol) che usano uno specifico nome community SNMP. Per la stessa operazione di individuazione si disabilita l'individuazione in una subnet specifica. Durante l'esecuzione dell'individuazione, l'individuazione della rete non rileva i dispositivi SNMP con il nome community specificato nella subnet disabilitata.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Determinare la topologia di rete  

Per eseguire il mapping della rete, è possibile utilizzare un'individuazione solo per topologia. Questo tipo di individuazione non rileva i potenziali client. L'individuazione di rete solo per topologia si basa su SNMP.  

Quando si esegue il mapping della topologia di rete, configurare il valore di **Hop massimi** nella scheda **SNMP** della finestra di dialogo **Individuazione di rete - Proprietà**. Con solo pochi hop è possibile controllare la larghezza di banda di rete usata per l'individuazione. Man mano che l'individuazione di rete avanza, aumentare il numero di hop per ottenere una migliore comprensione della topologia di rete.  

Dopo aver compreso la topologia di rete, configurare proprietà aggiuntive per l'individuazione di rete. Queste proprietà consentono di individuare i potenziali client e i relativi sistemi operativi. Configurare anche l'individuazione di rete per limitare i segmenti di rete in cui eseguire la ricerca.  

Per altre informazioni, vedere [Come determinare la topologia di rete](#bkmk_proc-top)

### <a name="network-discovery-search-options"></a>Opzioni di ricerca per l'individuazione di rete

Configuration Manager supporta i metodi seguenti per la ricerca nella rete:

- [Limitare le ricerche tramite subnet](#BKMK_LimitBySubnet)
- [Eseguire ricerche in un dominio specifico](#BKMK_SearchByDomain)
- [Limitare le ricerche tramite nomi community SNMP](#BKMK_LimitBySNMPname)
- [Eseguire ricerche in un server DHCP specifico](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Limitare le ricerche mediante subnet  

È possibile configurare l'individuazione di rete per effettuare la ricerca in subnet specifiche durante un ciclo di individuazione. Per impostazione predefinita, l'individuazione di rete effettua la ricerca nella subnet del server che esegue l'individuazione. Eventuali subnet aggiuntive configurate e abilitate si applicano esclusivamente alle opzioni di ricerca SNMP e DHCP. Per la ricerca nei domini, l'individuazione della rete non è limitata dalle configurazioni per subnet.  

Se si specificano una o più subnet nella scheda **Subnet** della finestra di dialogo **Individuazione di rete - Proprietà**, la ricerca viene eseguita solo nelle subnet contrassegnate con **Attivato**.  

Quando si disabilita una subnet, il sito la esclude dall'individuazione e vengono applicate le condizioni seguenti:  

- Le query basate su SNMP non vengono eseguite sulla subnet.  

- I server DHCP non rispondono con un elenco di risorse che si trovano nella subnet.  

- Le query basate su dominio possono individuare risorse che si trovano nella subnet.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Eseguire ricerche in un dominio specifico  

È possibile configurare l'individuazione di rete per effettuare la ricerca in un dominio specifico o in un insieme di domini durante l'esecuzione dell'individuazione. Per impostazione predefinita, l'individuazione di rete effettua la ricerca nel dominio locale del server che esegue l'individuazione.  

Se si specificano uno o più domini nella scheda **Domini** della finestra di dialogo **Individuazione di rete - Proprietà**, la ricerca viene eseguita solo nei domini contrassegnati con **Attivato**.  

Quando si disabilita un dominio, il sito lo esclude dall'individuazione e vengono applicate le condizioni seguenti:  

- L'individuazione di rete non esegue query sui controller di dominio in tale dominio.  

- Le query basate su SNMP possono comunque essere eseguite sulle subnet in quel dominio.  

- I server DHCP possono comunque rispondere con un elenco di risorse presenti nel dominio.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Limitare le ricerche usando i nomi comunità SNMP  

L'individuazione di rete viene configurata per effettuare la ricerca in una comunità SNMP specifica o in un insieme di comunità durante l'esecuzione dell'individuazione. Per impostazione predefinita, il metodo configura il nome community **pubblico**.  

L'individuazione di rete utilizza i nomi comunità per accedere ai router che sono dispositivi SNMP. Un router può fornire l'individuazione di rete con informazioni su altri router e subnet che sono collegati al primo router.  

> [!NOTE]  
> I nomi comunità SNMP sono simili alle password. L'individuazione della rete può ottenere informazioni solo da un dispositivo SNMP per il quale è stato specificato un nome community. Ciascun dispositivo SNMP può avere il proprio nome comunità, ma spesso lo stesso nome comunità viene condiviso tra diversi dispositivi. Inoltre, la maggior parte dei dispositivi SNMP hanno un nome comunità predefinito, cioè **Pubblico**. Alcune organizzazioni, però, eliminano il nome comunità **pubblico** dai propri dispositivi come misura di sicurezza.  

Se si include più di una community SNMP nella scheda **SNMP** della finestra di dialogo **Individuazione di rete - Proprietà**, la ricerca viene eseguita in base all'ordine di visualizzazione. Assicurarsi che i nomi usati più di frequente si trovino all'inizio dell'elenco. Questa configurazione aiuta a ridurre al minimo il traffico di rete generato dal sito quando cerca di contattare un dispositivo usando nomi diversi.

> [!NOTE]  
> Oltre a usare il nome community SNMP, è possibile specificare l'indirizzo IP o il nome risolvibile di un dispositivo SNMP specifico. Questa operazione può essere eseguita nella scheda **Dispositivi SNMP** della finestra di dialogo **Individuazione di rete - Proprietà**.  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Eseguire ricerche in un server DHCP specifico  

È possibile configurare l'individuazione di rete per l'utilizzo di un server DHCP specifico o di più server per individuare i client DHCP durante l'esecuzione dell'individuazione.  

L'individuazione di rete effettua la ricerca in ogni server DHCP specificato nella scheda **DHCP** della finestra di dialogo **Proprietà dell'individuazione della rete** . Se il server che sta eseguendo l'individuazione esegue il lease dell'indirizzo IP da un server DHCP, è possibile configurare l'individuazione per eseguire la ricerca in tale server DHCP. Abilitare questo comportamento con l'opzione **Includi il server DHCP per il cui utilizzo è configurato il server di sito**.  

> [!NOTE]  
> Per configurare correttamente un server DHCP nell'individuazione di rete, l'ambiente deve supportare IPv4. Non è possibile configurare l'individuazione della rete per usare un server DHCP in un ambiente IPv6 nativo.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Come configurare l'individuazione di rete  

Utilizzare le seguenti procedure per individuare in primo luogo la topologia di rete, quindi per configurare l'individuazione di rete e individuare potenziali client utilizzando una o più delle opzioni di individuazione di rete disponibili.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a> Come determinare la topologia di rete  

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Metodi di individuazione**.  

2. Selezionare il metodo **Individuazione di rete** per il sito in cui si vuole individuare le risorse di rete.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà**.  

    - Nella scheda **Generale** selezionare l'opzione **Abilita individuazione della rete**. Selezionare quindi **Topologia** in **Tipo di individuazione**.  

    - Nella scheda **Subnet** selezionare l'opzione **Cerca subnet locali**.  

      > [!TIP]  
      > Se si conoscono le subnet specifiche che costituiscono la rete, deselezionare la casella di controllo **Cerca subnet locali**. Selezionare quindi l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif) e aggiungere le subnet specifiche in cui eseguire la ricerca. Per reti di grandi dimensioni, eseguire la ricerca solo in una o due subnet alla volta per ridurre al minimo l'uso della larghezza di banda di rete.  

    - Nella scheda **Domini** selezionare l'opzione **Cerca dominio locale**.  

    - Nella scheda **SNMP** selezionare un'opzione nell'elenco a discesa **Hop massimi**. Questa opzione specifica quanti hop router può usare l'individuazione di rete nel mapping della topologia.  

      > [!TIP]  
      > Quando si esegue per la prima volta la topologia di rete, configurare un numero limitato di hop router per ridurre al minimo l'utilizzo della larghezza di banda di rete.  

4. Nella scheda **Pianifica** selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif) e impostare una pianificazione per l'esecuzione dell'individuazione.  

    > [!NOTE]  
    > Non è possibile assegnare una configurazione di individuazione diversa per separare le varie pianificazioni di individuazione della rete. Ogni volta che viene eseguita l'individuazione di rete, essa utilizza la configurazione di individuazione corrente.  

5. Selezionare **OK** per accettare le configurazioni. L'individuazione di rete viene eseguita all'orario specificato.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a> Come configurare l'individuazione di rete  

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Metodi di individuazione**.  

2. Selezionare il metodo **Individuazione di rete** per il sito in cui si vuole individuare le risorse di rete.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà**.  

4. Nella scheda **Generale** selezionare l'opzione **Abilita individuazione della rete**.  

    - Selezionare un'opzione in **Tipo di individuazione** per il tipo di individuazione da eseguire.  

    - Abilitare l'opzione **Rete lenta** per fare in modo che Configuration Manager si adatti automaticamente alle reti con larghezza di banda ridotta.  

5. Per configurare l'individuazione per la ricerca nelle subnet, passare alla scheda **Subnet**. Configurare quindi una o più delle opzioni seguenti:  

    - Per eseguire l'individuazione nelle subnet locali del computer che esegue l'individuazione, abilitare l'opzione **Cerca subnet locali**.  

    - Per effettuare la ricerca in una subnet specifica, verificare che la subnet sia inclusa nell'elenco in **Subnet da cercare** e che il valore **Cerca** sia impostato su **Attivato**:  

      1. Se la subnet non è presente nell'elenco, selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuova assegnazione subnet** immettere le informazioni in **Subnet** e **Mask** e quindi selezionare **OK**. Per impostazione predefinita, una nuova subnet è abilitata per la ricerca.  

      2. Per modificare il valore di **Cerca** per una subnet nell'elenco, selezionare la subnet. Selezionare quindi l'icona **Mostra/Nascondi** per alternare il valore tra **Disattivato** e **Attivato**.  

6. Per configurare l'individuazione per la ricerca nei domini, passare alla scheda **Domini**. Configurare quindi una o più delle opzioni seguenti:  

    - Per eseguire l'individuazione nel dominio del computer che esegue l'individuazione, abilitare l'opzione **Cerca dominio locale**.  

    - Per effettuare la ricerca in un dominio specifico, verificare che il dominio sia incluso nell'elenco in **Domini** e che il valore **Cerca** sia impostato su **Attivato**:  

      1. Se il dominio non è presente nell'elenco, selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Proprietà dominio** immettere le informazioni in **Dominio** e quindi selezionare **OK**. Per impostazione predefinita, un nuovo dominio è abilitato per la ricerca.  

      2. Per modificare il valore di **Cerca** per un dominio nell'elenco, selezionare il dominio. Selezionare quindi l'icona **Mostra/Nascondi** per alternare il valore tra **Disattivato** e **Attivato**.  

7. Per configurare l'individuazione per la ricerca di nomi community SNMP specifici per i dispositivi SNMP, passare alla scheda **SNMP**. Configurare quindi una o più delle opzioni seguenti:  

    - Per aggiungere un nome community SNMP all'elenco **Nomi comunità SNMP**, selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuovo nome comunità SNMP** specificare un valore per **Nome** per la community SNMP e quindi selezionare **OK**.  

    - Per rimuovere un nome community SNMP, selezionare il nome e quindi l'icona **Elimina**![Icona Elimina](media/Disc_delete_Icon.gif).  

    - Per modificare l'ordine di ricerca dei nomi community SNMP, selezionare un nome nell'elenco. Selezionare quindi l'icona **Sposta elemento in alto**![Icona Sposta elemento in alto](media/Disc_moveUp_Icon.gif) o **Sposta elemento in basso**![Icona Sposta elemento in basso](media/Disc_moveDown_Icon.gif). Quando viene eseguita l'individuazione, viene effettuata la ricerca nei nomi comunità seguendo un ordine dall'alto in basso. 

    - Per configurare il numero massimo di hop router utilizzabili per le ricerche SNMP, selezionare il numero di hop nell'elenco a discesa **Hop massimi**.  

8. Per configurare un dispositivo SNMP, passare alla scheda **Dispositivi SNMP**. Se il dispositivo non è presente nell'elenco, selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuovo dispositivo SNMP** specificare l'indirizzo IP o il nome del dispositivo SNMP e quindi selezionare **OK**.  

    > [!NOTE]  
    > Se si specifica un nome dispositivo, Configuration Manager deve essere in grado di risolvere il nome NetBIOS in un indirizzo IP.  

9. Per configurare l'individuazione per eseguire query su server DHCP specifici, passare alla scheda **DHCP**. Configurare quindi una o più delle opzioni seguenti:  

    - Per eseguire query sul server DHCP nel computer che esegue l'individuazione, abilitare l'opzione **Always use the site server's DHCP server** (Usa sempre server DHCP del server del sito).  

      > [!NOTE]  
      > Per usare questa opzione, il server deve eseguire il lease dell'indirizzo IP da un server DHCP e non può usare un indirizzo IP statico.  

    - Per eseguire query su un server DHCP specifico, selezionare l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuovo server DHCP** specificare l'indirizzo IP o il nome del server DHCP e quindi selezionare **OK**.  

      > [!NOTE]  
      > Se si specifica un nome server, Configuration Manager deve essere in grado di risolvere il nome NetBIOS in un indirizzo IP.  

10. Per specificare quando viene eseguita l'individuazione, passare alla scheda **Pianifica**. Selezionare quindi l'icona **Nuovo**![Icona Nuovo](media/Disc_new_Icon.gif) per impostare una pianificazione per l'esecuzione dell'individuazione di rete. È possibile configurare più pianificazioni ricorrenti e più pianificazioni senza ricorrenza.  

    > [!NOTE]  
    > Se nella scheda **Pianifica** sono visualizzate più pianificazioni contemporaneamente, l'individuazione di rete viene eseguita per tutte le pianificazioni come configurata nell'orario indicato nella pianificazione. Questo vale anche per le pianificazioni ricorrenti.  

11. Selezionare **OK** per salvare le configurazioni.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Come verificare il completamento dell'individuazione di rete  

Il tempo necessario per il completamento dell'individuazione della rete può variare in base a uno o più dei fattori seguenti:  

- La dimensione della rete  

- La topologia della rete  

- Il numero massimo di hop configurati per trovare router nella rete  

- Il tipo di individuazione che viene eseguita  

L'individuazione di rete non crea messaggi per avvisare quando l'operazione è terminata. Usare la procedura seguente per verificare quando è terminata l'individuazione:  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Espandere **Stato del sistema** e quindi selezionare il nodo **Query messaggi di stato**.  

2. Selezionare la query **Tutti i messaggi di stato**.  

3. Nella scheda **Home** della barra multifunzione selezionare **Mostra messaggi** nel gruppo **Query messaggi di stato**.  

4. Nella finestra Tutti i messaggi di stato selezionare un valore nell'elenco a discesa **Seleziona data e ora** che includa il tempo trascorso dall'inizio dell'individuazione. Selezionare quindi **OK** per aprire il **Visualizzatore messaggi di stato di Configuration Manager**.  

    > [!TIP]  
    > È possibile utilizzare anche l'opzione **Specifica data e ora** per selezionare una data e un'ora specifici per l'esecuzione dell'individuazione. Questa opzione è utile quando si esegue l'individuazione della rete in una determinata data e si desidera recuperare i messaggi solo da tale data.  

5. Per convalidare il termine dell'individuazione della rete, cercare un messaggio di stato con i seguenti dettagli:  

    - ID messaggio: **502**  

    - Componente: **SMS_NETWORK_DISCOVERY**  

    - Descrizione: **Il componente è stato arrestato**  

    Se questo messaggio di stato non è presente, l'individuazione della rete non è stata completata.  

6. Per convalidare l'avvio dell'individuazione della rete, cercare un messaggio di stato con i seguenti dettagli:  

    - ID messaggio: **500**  

    - Componente: **SMS_NETWORK_DISCOVERY**  

    - Descrizione: **Il componente è stato avviato**  

    Queste informazioni verificano l'avvio dell'individuazione della rete. Se queste informazioni non sono presenti, ripianificare l'individuazione della rete.  
