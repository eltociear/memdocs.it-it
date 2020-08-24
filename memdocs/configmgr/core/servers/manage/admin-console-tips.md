---
title: Modifiche e suggerimenti per la console di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sulle modifiche alla console di Configuration Manager e suggerimenti per usarla.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0a434f013da48d660efa78f5e2cdca6ced0826d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700719"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Modifiche e suggerimenti per la console di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni seguenti per conoscere le modifiche alla console di Configuration Manager e i suggerimenti per usarla:

## <a name="general-tips"></a>Suggerimenti generali

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Miglioramenti alla ricerca nella console
<!--4640570-->
*(Funzionalità introdotta nella versione 1910)*

- È possibile usare l'opzione di ricerca **Tutte le sottocartelle** dai nodi **Pacchetti driver** e **Query**.<!--2841181,5424892--> A partire dalla versione 2002, si può usare questa opzione anche dai nodi **Elementi di configurazione** e **Linee di base di configurazione**.<!--5891241-->

- Quando una ricerca restituisce più di 1000 risultati, è possibile selezionare il pulsante **OK** sulla barra di notifica per visualizzare altri risultati.<!--4640570-->

    ![Screenshot della barra di notifica per un numero eccessivo di risultati della ricerca](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Il limite predefinito per i risultati della ricerca è 1000. È possibile modificare questo valore predefinito. Nella console di Configuration Manager passare alla scheda **Ricerca** della barra multifunzione. Nel gruppo **Opzioni** selezionare **Impostazioni di ricerca**. Modificare il valore di **Risultati della ricerca**. Un numero maggiore di risultati della ricerca potrebbe richiedere più tempo per la visualizzazione.
    >
    > Per impostazione predefinita, il limite massimo superiore è 100.000. Per modificare questo limite, impostare il valore DWORD **QueryResultCountMaximum** nella chiave del Registro di sistema seguente:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > L'impostazione nella console corrisponde al valore **QueryResultCountLimit** nella stessa chiave. Un amministratore può configurare questi valori nell'hive HKLM per tutti gli utenti del dispositivo. Il valore HKCU sostituisce l'impostazione HKLM.

### <a name="role-based-administration-for-folders"></a>Amministrazione basata sui ruoli per le cartelle
<!--3600867-->
*(Funzionalità introdotta nella versione 1906)*

È possibile impostare gli ambiti di protezione nelle cartelle. Se si ha accesso a un oggetto nella cartella ma non si ha accesso alla cartella, non sarà possibile visualizzare l'oggetto. Analogamente, se si ha accesso a una cartella ma non a un oggetto all'interno della cartella, non sarà possibile visualizzare l'oggetto. Fare clic con il pulsante destro del mouse su una cartella, scegliere **Imposta ambiti di protezione** e quindi scegliere gli ambiti di protezione da applicare.

### <a name="views-sort-by-integer-values"></a>L'ordinamento nelle viste si basa sui valori interi

*(Funzionalità introdotta nella versione 1902)*

Sono state migliorate le modalità di ordinamento dei dati nelle varie visualizzazioni. Nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**, ad esempio, l'ordinamento nelle colonne seguenti si basa ora sui numeri invece che sui valori delle stringhe:  

- Numero errori
- Numero in corso
- Numero altri
- Numero riusciti
- Numero sconosciuti  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Spostare l'avviso per un numero elevato di risultati

*(Funzionalità introdotta nella versione 1902)*

Quando si seleziona un nodo della console che restituisce più di 1.000 risultati, Configuration Manager visualizza l'avviso seguente:

> Configuration Manager ha restituito un numero elevato di risultati. È possibile limitare i risultati con la ricerca oppure fare clic qui per visualizzare un massimo di 100000 risultati.

È ora presente uno spazio vuoto aggiuntivo tra questo avviso e il campo di ricerca. Questo spostamento impedisce di selezionare inavvertitamente l'avviso per visualizzare altri risultati.

### <a name="send-feedback"></a>Inviare un feedback

*(Funzionalità introdotta nella versione 1806)*
<!--1357542-->

Inviare commenti e suggerimenti dalla console.  

- **Invia smile**: inviare commenti e suggerimenti su ciò che si è apprezzato  

- **Invia faccia imbronciata**: inviare commenti e suggerimenti su ciò che non si è apprezzato  

- **Invia un suggerimento**: consente di accedere a UserVoice per condividere la propria opinione  

Per altre informazioni, vedere [Commenti e suggerimenti sul prodotto](../../understand/find-help.md#BKMK_1806Feedback).


## <a name="assets-and-compliance-workspace"></a>Area di lavoro Asset e conformità

### <a name="real-time-actions-from-device-lists"></a>Azioni in tempo reale dagli elenchi di dispositivi
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Esistono diversi modi per visualizzare un elenco di dispositivi nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità**.

- Nell'area di lavoro **Asset e conformità** selezionare il nodo **Raccolte dispositivi**. Selezionare una raccolta di dispositivi e scegliere l'azione che consente di **visualizzare i membri**. Questa azione apre un sottonodo del nodo **Dispositivi** con un elenco di dispositivi per la raccolta.  

  - Quando si seleziona il sottonodo della raccolta, è ora possibile avviare **CMPivot** dal gruppo Raccolta della barra multifunzione.  

- Nell'area di lavoro **Monitoraggio** selezionare il nodo **Distribuzioni**. Selezionare una distribuzione e scegliere l'azione di **visualizzazione dello stato** nella barra multifunzione. Nel riquadro dello stato della distribuzione fare doppio clic sugli asset totali per eseguire il drill-through in un elenco di dispositivi.  

  - Quando si seleziona un dispositivo in questo elenco, è ora possibile avviare **CMPivot** ed **eseguire script** dal gruppo Dispositivi della barra multifunzione.  


### <a name="collections-tab-in-devices-node"></a>Scheda Raccolte nel nodo Dispositivi
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Asset e conformità** passare al nodo **Dispositivi** e selezionare un dispositivo. Nel riquadro dei dettagli passare alla nuova scheda **Raccolte**. Questa scheda contiene le raccolte che includono questo dispositivo. 

> [!Note]  
> - La scheda non è attualmente disponibile da un sottonodo dispositivi del nodo **Raccolte di dispositivi**. Ad esempio, quando si seleziona l'opzione che consente di **visualizzare i membri** per una raccolta.
> - Questa scheda potrebbe non essere popolata come previsto per alcuni utenti. Per visualizzare l'elenco completo delle raccolte a cui appartiene un dispositivo, è necessario avere il ruolo di sicurezza **Amministratore completo**. Si tratta di un problema noto. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Aggiungi la colonna GUID SMBIOS ai nodi Dispositivo e Raccolta di dispositivi

*(Funzionalità introdotta nella versione 1906)*

<!--4526580-->
Nei nodi **Dispositivo** e **Raccolte di dispositivi** è ora possibile aggiungere una nuova colonna per **GUID SMBIOS**. Questo valore corrisponde alla proprietà **GUID BIOS** della classe Risorsa di sistema. Si tratta di un identificatore univoco dell'hardware del dispositivo.

### <a name="search-device-views-using-mac-address"></a>Eseguire la ricerca nelle visualizzazioni dispositivi tramite indirizzi MAC

<!--3600878-->
*(Funzionalità introdotta nella versione 1902)*

È possibile cercare un indirizzo MAC in una visualizzazione dispositivi della console di Configuration Manager. Questa proprietà è utile per gli amministratori della distribuzione di sistemi operativi durante la risoluzione dei problemi delle distribuzioni basate su Pre-Boot eXecution Environment. Quando si visualizza un elenco di dispositivi, aggiungere la colonna **Indirizzo MAC** alla visualizzazione. Usare il campo di ricerca per aggiungere i criteri di ricerca **Indirizzo MAC**.

### <a name="view-users-for-a-device"></a>Visualizzare gli utenti per un dispositivo

A partire dalla versione 1806, le colonne seguenti sono disponibili nel nodo **Dispositivi**:  

- **Utente/i primario** <!--1357280-->  

- **Utente attualmente connesso** <!--1358202-->  

    > [!NOTE]  
    > La visualizzazione dell'utente attualmente connesso richiede l'[individuazione dell'utente](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) e l'[affinità utente-dispositivo](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Per altre informazioni su come visualizzare una colonna non predefinita, vedere [Come usare la console di amministrazione](admin-console.md#columns).

### <a name="improvement-to-device-search-performance"></a>Miglioramento delle prestazioni di ricerca dei dispositivi

<!-- 3614690 -->
A partire dalla versione 1806, quando si esegue la ricerca in una raccolta di dispositivi, non viene eseguita la ricerca della parola chiave in tutte le proprietà degli oggetti. Quando non si specifica cosa cercare, la ricerca viene eseguita nelle quattro proprietà seguenti:

- Name
- Utente/i primario/i
- Utente attualmente connesso
- Nome utente ultimo accesso

Questo comportamento migliora significativamente il tempo necessario per le ricerche in base al nome, in particolare in un ambiente di grandi dimensioni. Le ricerche personalizzate in base a criteri specifici non sono interessate da questa modifica.


## <a name="software-library-workspace"></a>Area di lavoro Raccolta software

### <a name="order-by-program-name-in-task-sequence"></a>Ordinare in base al nome del programma nella sequenza di attività
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**. Modificare una sequenza di attività e selezionare o aggiungere il passaggio [Installa pacchetto](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Se un pacchetto include più di un programma, l'elenco a discesa ora visualizza i programmi in ordine alfabetico.

### <a name="task-sequences-tab-in-applications-node"></a>Scheda Sequenze di attività nel nodo Applicazioni
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, passare al nodo **Applicazioni** e selezionare un'applicazione. Nel riquadro dei dettagli passare alla nuova scheda **Sequenze di attività**. Questa scheda contiene le sequenze di attività che fanno riferimento a questa applicazione.

### <a name="drill-through-required-updates"></a>Drill-through degli aggiornamenti obbligatori
<!--4224414-->
*(Funzionalità introdotta nella versione 1906)*

1. Nella console di Configuration Manager selezionare una delle seguenti posizioni:

   - **Raccolta software** > **Aggiornamenti software** > **Tutti gli aggiornamenti software**
   - **Raccolta software** > **Manutenzione pacchetti di Windows 10** > **Tutti gli aggiornamenti di Windows 10**
   - **Raccolta software** > **Gestione client di Office 365** > **Aggiornamenti di Office 365**

1. Selezionare tutti gli aggiornamenti richiesti da almeno un dispositivo.
1. Esaminare la scheda **Riepilogo** e individuare il grafico a torta in **Statistiche**.
1. Selezionare il collegamento ipertestuale **View Required** (Visualizza richiesto) accanto al grafico a torta per eseguire il drill-down nell'elenco dei dispositivi.
1. Questa azione consente di visualizzare un nodo temporaneo in **Dispositivi** dove è possibile visualizzare i dispositivi che richiedono l'aggiornamento. È anche possibile eseguire azioni per il nodo, come creare una nuova raccolta dall'elenco.

> [!NOTE]
> A partire dal 21 aprile 2020, Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che vengano ancora visualizzati riferimenti al nome precedente nella console di Configuration Manager e nella documentazione di supporto mentre la console viene aggiornata.

### <a name="maximize-the-browse-registry-window"></a>Ingrandire la finestra Sfoglia Registro di sistema

<!--3594151 includes all MMS 1902 console changes-->
*(Funzionalità introdotta nella versione 1902)*

1. Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e quindi selezionare il nodo **Applicazioni**.
1. Selezionare un'applicazione con tipo di distribuzione basato su un metodo di rilevamento, ad esempio un metodo di rilevamento di Windows Installer.
1. Nel riquadro dei dettagli passare alla scheda **Tipi di distribuzione**.
1. Aprire le proprietà di un tipo di distribuzione e passare alla scheda **Metodo di rilevamento**. Selezionare **Aggiungi clausola**.
1. Impostare **Tipo di impostazione** su **Registro** e selezionare **Sfoglia** per aprire la finestra **Sfoglia Registro di sistema**. È ora possibile ingrandire questa finestra.  

### <a name="edit-a-task-sequence-by-default"></a>Modificare una sequenza di attività per impostazione predefinita

*(Funzionalità introdotta nella versione 1902)*

Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**. **Modifica** è ora l'azione predefinita quando si apre una sequenza di attività. In precedenza l'azione predefinita era **Proprietà**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Passare alla raccolta dalla distribuzione di un'applicazione

*(Funzionalità introdotta nella versione 1902)*

1. Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e quindi selezionare il nodo **Applicazioni**.
1. Selezionare un'applicazione. Nel riquadro dei dettagli passare alla scheda **Distribuzioni**.
1. Selezionare una distribuzione e quindi scegliere la nuova opzione **Raccolta** nella barra multifunzione della scheda Distribuzione. Questa azione cambia la visualizzazione sostituendola con la raccolta di destinazione della distribuzione.
   - Questa azione è disponibile anche dal menu di scelta rapida che viene aperto facendo clic con il pulsante destro del mouse sulla distribuzione in questa visualizzazione.


## <a name="monitoring-workspace"></a>Area di lavoro di monitoraggio

### <a name="correct-names-for-client-operations"></a>Nomi corretti per le operazioni client
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Monitoraggio** espandere **Operazioni client**. L'operazione di **passaggio al punto di aggiornamento software successivo** è ora denominata in modo corretto.

### <a name="show-collection-name-for-scripts"></a>Visualizzare il nome della raccolta per gli script
<!--4616810-->
*(Funzionalità introdotta nella versione 1906)*

Nell'area di lavoro **Monitoraggio** selezionare il nodo **Stato script**, che ora indica il **nome della raccolta** oltre all'ID.

### <a name="remove-content-from-monitoring-status"></a>Rimuovere il contenuto dal monitoraggio dello stato

*(Funzionalità introdotta nella versione 1902)*

1. Nell'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e selezionare **Stato contenuto**.
1. Selezionare un elemento nell'elenco e scegliere l'opzione **Visualizza stato** nella barra multifunzione.
1. Nel riquadro Dettagli asset fare clic con il pulsante destro del mouse su un punto di distribuzione e scegliere la nuova opzione **Rimuovi**. Questa azione rimuove il contenuto dal punto di distribuzione selezionato.

### <a name="copy-details-in-monitoring-views"></a>Copiare i dettagli nelle viste monitoraggio

*(Funzionalità introdotta nella versione 1806)*
<!--1357856-->
Copiare le informazioni dal riquadro **Dettagli asset** per i nodi di monitoraggio seguenti:  

- **Stato distribuzione contenuto**  

- **Stato distribuzione**  

![Vista Stato distribuzione, copiare i dettagli degli asset](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Area di lavoro Amministrazione

<!--4223683-->
A partire dalla versione 1906, è possibile abilitare alcuni nodi nel nodo **Protezione** per usare il servizio di amministrazione. Questa modifica consente alla console di comunicare con il provider SMS tramite HTTPS anziché tramite WMI. Per altre informazioni, vedere l'articolo sulla [configurazione del servizio di amministrazione](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Passaggi successivi

- [Usare la console](admin-console.md)
- [Notifiche della console](admin-console-notifications.md)
- [Funzionalità di accesso facilitato](../../understand/accessibility-features.md)