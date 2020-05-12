---
title: Creare linee di base di configurazione
titleSuffix: Configuration Manager
description: Creare linee di base di configurazione in Configuration Manager da distribuire in una raccolta.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1365aec90093ee24ad967e1d68e7c414b4efa254
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906654"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Creare linee di base di configurazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


Le linee di base di configurazione in Configuration Manager contengono elementi di configurazione predefiniti e, facoltativamente, altre linee di base di configurazione. Dopo aver creato una linea di base di configurazione, è possibile distribuirla in una raccolta in modo che i dispositivi in tale raccolta la scarichino e valutino la propria conformità in base a essa.  

> [!TIP]
> Non è possibile specificare l'ordine con cui il client Configuration Manager valuta gli elementi di configurazione in una linea di base. Questa impostazione non è deterministica.<!-- MEMDocs#175 -->

## <a name="configuration-baselines"></a>Linee di base di configurazione

 Le linee di base di configurazione in Configuration Manager possono contenere revisioni specifiche degli elementi di configurazione o possono essere configurate in modo da usare sempre la versione più recente di un elemento di configurazione. Per altre informazioni sulle revisioni dell'elemento di configurazione, vedere [Attività di gestione per i dati di configurazione](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Esistono due metodi che è possibile usare per creare le linee di base di configurazione:  

- Importare i dati di configurazione da un file. Per avviare l' **Importazione guidata dei dati di configurazione**, nel nodo **Elementi di configurazione** o **Linee di base di configurazione** nell'area di lavoro **Asset e conformità** fare clic su **Importa dati di configurazione**. Per altre informazioni, vedere [Importare i dati di configurazione](import-configuration-data.md).

- Usare la finestra di dialogo **Crea linea di base di configurazione** per creare una nuova linea di base di configurazione.  

## <a name="create-a-configuration-baseline"></a>Creare una linea di base di configurazione

Per creare una linea di base di configurazione mediante la finestra di dialogo **Crea linea di base di configurazione**, usare la procedura seguente:  

1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

2. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea linea di base di configurazione**.  

3. Nella finestra di dialogo **Crea linea di base di configurazione** immettere un nome univoco e una descrizione per la linea di base di configurazione. È possibile usare un massimo di 255 caratteri per il nome e 512 caratteri per la descrizione.  

4. L'elenco **Dati configurazione** visualizza tutti gli elementi di configurazione o le linee di base di configurazione incluse in questa linea di base di configurazione. Fare clic su **Aggiungi** per aggiungere un nuovo elemento di configurazione o una nuova linea di base di configurazione all'elenco. È possibile scegliere uno degli elementi seguenti:  

   - **Elementi di configurazione**  

   - **Aggiornamenti software**  

   - **Linee di base di configurazione**  
     > [!IMPORTANT]
     > È necessario limitare ogni linea di base di configurazione a non più di 1000 aggiornamenti software.
5. Usare l'elenco **Modifica scopo** per specificare il comportamento di un elemento di configurazione selezionato nell'elenco **Dati di configurazione**. È possibile selezionare uno degli elemento seguenti:  

   -   **Richiesto**: la linea di base di configurazione viene valutata come non conforme se l'elemento di configurazione non viene rilevato in un dispositivo client. Se viene rilevato, viene valutata come conforme  

   -   **Facoltativo**: l'elemento di configurazione viene valutato solo a livello di conformità se l'applicazione a cui fa riferimento viene trovata nei computer client. Se l'applicazione non viene trovata, la linea di base di configurazione non viene contrassegnata come non conforme (applicabile solo agli elementi di configurazione dell'applicazione).  

   -   **Non consentito**: la linea di base di configurazione viene valutata come non conforme se l'elemento di configurazione viene rilevato nei computer client (applicabile solo agli elementi di configurazione dell'applicazione).  

   > [!NOTE]
   >  L'elenco **Modifica scopo** è disponibile solo se è stata selezionata l'opzione **Questo elemento di configurazione contiene le impostazioni dell'applicazione** nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**.  

6. Usare l'elenco **Modifica revisione** per selezionare un oggetto specifico o l'ultima revisione dell'elemento di configurazione per valutare la conformità nei dispositivi client o selezionare **Utilizza sempre più recente** per usare sempre l'ultima revisione. Per altre informazioni sulle revisioni dell'elemento di configurazione, vedere [Attività di gestione per i dati di configurazione](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Per rimuovere un elemento di configurazione dalla linea di base di configurazione, selezionare un elemento di configurazione e quindi fare clic su **Rimuovi**.  

8. A partire dalla versione 1806, è possibile selezionare l'opzione **Applica sempre questa baseline per client con co-gestione**. Quando è selezionata, la linea di base verrà applicata anche ai client gestiti da Intune.  Questa eccezione può essere usata per configurare le impostazioni richieste dall'organizzazione, ma non ancora disponibili in Intune.

9. Facoltativamente, fare clic su **Categorie** per assegnare alla linea di base le categorie per la ricerca e il filtro. 

10. Fare clic su **OK** per chiudere la finestra di dialogo **Crea linea di base di configurazione** e creare una nuova linea di base di configurazione.  

>[!NOTE]
> Se si modifica una linea di base esistente, ad esempio impostando l'opzione **Applica sempre questa baseline per client con co-gestione**, incrementerà la versione del contenuto della linea di base. I client dovranno valutare la nuova versione per aggiornare il report della linea di base.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a> Includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità
<!--3608345-->
*(Funzionalità introdotta nella versione 1910)*

A partire dalla versione 1910 è possibile aggiungere la valutazione delle linee di base di configurazione personalizzate come regola di valutazione dei criteri di conformità. Quando si crea o si modifica una linea di base di configurazione, è disponibile l'opzione, **Valuta questa baseline come parte della valutazione dei criteri di conformità**. Quando si aggiunge o si modifica una regola dei criteri di conformità, è disponibile una nuova condizione denominata **Includi le baseline configurate in una valutazione dei criteri di conformità**. Per i dispositivi con co-gestione, e quando si configura Intune per acquisire i risultati della valutazione della conformità di Configuration Manager come parte dello stato di conformità generale, queste informazioni vengono inviate ad Azure AD. È quindi possibile usarlo per l'accesso condizionale alle risorse di Office 365. Per altre informazioni, vedere [Accesso condizionale con la co-gestione](../../comanage/quickstart-conditional-access.md).

Per includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità, eseguire le operazioni seguenti:

- Creare e distribuire criteri di conformità in una raccolta di utenti con la regola [**Includi le baseline configurate in una valutazione dei criteri di conformità**](#bkmk_CA).
- Selezionare [**Valuta questa baseline come parte della valutazione dei criteri di conformità**](#bkmk_eval-baseline) in una linea di base di configurazione distribuita in una raccolta di dispositivi.

> [!IMPORTANT]
> Quando la destinazione è costituita da dispositivi che sono co-gestiti, assicurarsi di soddisfare i [prerequisiti di co-gestione](../../comanage/overview.md#prerequisites).

### <a name="example-evaluation-scenario"></a>Scenario di valutazione di esempio

Quando un utente fa parte di una raccolta destinata a un criterio di conformità che include la condizione della regola **Include configured baselines in compliance policy assessment** (Includi le linee di base configurate nella valutazione dei criteri di conformità), tutte le linee di base con l'opzione **Evaluate this baseline as part of compliance policy assessment** (Valuta questa linea di base come parte della valutazione dei criteri di conformità) selezionata che vengono distribuite all'utente o al dispositivo dell'utente vengono valutate per la conformità. Ad esempio:

- `User1` è parte di `User Collection 1`.
- `User1` usa `Device1`, che si trova in `Device Collection 1` e `Device Collection 2`.
- `Compliance Policy 1` ha la condizione della regola **Include configured baselines in compliance policy assessment** (Includi le linee di base configurate nella valutazione dei criteri di conformità) ed è distribuito in `User Collection 1`.
- `Configuration Baseline 1` ha l'opzione **Evaluate this baseline as part of compliance policy assessment** (Valuta questa linea di base come parte della valutazione dei criteri di conformità) selezionata ed è distribuita in `Device Collection 1`.
- `Configuration Baseline 2` ha l'opzione **Evaluate this baseline as part of compliance policy assessment** (Valuta questa linea di base come parte della valutazione dei criteri di conformità) selezionata ed è distribuita in `Device Collection 2`.

In questo scenario, quando `Compliance Policy 1` valuta la situazione in cui `User1` usa `Device1`, vengono valutate anche `Configuration Baseline 1` e `Configuration Baseline 2`.

- `User1` a volte usa `Device2`.
- `Device2` è un membro di `Device Collection 2` e `Device Collection 3`.
- In `Device Collection 3` è distribuita `Configuration Baseline 3`, ma l'opzione **Evaluate this baseline as part of compliance policy assessment** (Valuta questa linea di base come parte della valutazione dei criteri di conformità) non è selezionata.

Quando `User1` usa `Device2`, viene valutata solo `Configuration Baseline 2` quando `Compliance Policy 1` esegue la valutazione.

> [!NOTE]
><!--5582516-->
> Se il criterio di conformità valuta una nuova linea di base che non è mai stata valutata prima nel client, potrebbe segnalare un errore di mancata conformità. Questo problema si verifica se la valutazione della linea di base è ancora in esecuzione quando viene valutata la conformità. Per aggirare questo problema, fare clic su **Controlla conformità** in **Software Center**.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a> Creare e distribuire un criterio di conformità con una regola per la valutazione dei criteri di conformità della linea di base

1. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e quindi selezionare il nodo **Criteri di conformità**.
1. Fare clic su **Crea criteri di conformità** nella barra multifunzione per visualizzare la **Creazione guidata criteri di conformità**. 
1. Nella pagina **Generale** selezionare **Regole di conformità per i dispositivi gestiti con il client di Configuration Manager**.
   - I dispositivi devono essere gestiti con il client di Configuration Manager per includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità.
1. Selezionare le piattaforme in uso nelle pagine **Piattaforme supportate**.
1. Nella pagina **Regole** selezionare **Nuova** e quindi selezionare la condizione **Include configured baselines in compliance policy assessment** (Includi le linee di base configurate nella valutazione dei criteri di conformità).

   ![Condizione Includi le baseline configurate in una valutazione dei criteri di conformità](./media/3608345-create-compliance-policy-rule.png)

1. Fare clic su **OK** e quindi su **Avanti** per andare alla pagina **Riepilogo**.
1. Verificare le opzioni selezionate, fare clic su **Avanti** e quindi su **Chiudi**.
1. Nel nodo **Criteri di conformità** fare clic con il pulsante destro del mouse sul criterio creato e selezionare **Distribuisci**.
1. Scegliere la raccolta, le impostazioni di generazione avvisi e la pianificazione per la valutazione della conformità per il criterio.
1. Fare clic su **OK** per distribuire i criteri di conformità.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Selezionare una linea di base di configurazione e selezionare l'opzione "Valuta questa baseline come parte della valutazione dei criteri di conformità"

1. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e quindi selezionare il nodo **Linee di base di configurazione**.
1. Fare clic con il pulsante destro del mouse su una linea di base esistente distribuita in una raccolta di dispositivi e quindi selezionare **Proprietà**. Se necessario, è possibile creare una nuova linea di base.
   - La linea di base deve essere distribuita in una raccolta di dispositivi, non in una raccolta utenti.
1. Abilitare l'impostazione **Evaluate this baseline as part of compliance policy assessment** (Valuta questa linea di base come parte della valutazione dei criteri di conformità).
   - Per i dispositivi con co-gestione per cui Intune è l'autorità di **configurazione del dispositivo**, assicurarsi che sia selezionata anche l'opzione **Applica sempre questa baseline anche per client con co-gestione**.
1. Fare clic su **OK** per salvare le modifiche apportate alla linea di base di configurazione.

   ![Finestra di dialogo Proprietà linea di base di configurazione](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>File di log per le linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità

- ComplianceHandler.log
- SettingsAgent.log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Passaggi successivi

[Importare i dati di configurazione](import-configuration-data.md)
