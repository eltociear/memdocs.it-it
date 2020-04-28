---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1801 per Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074215"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1801 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1801. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. 

Vedere [Technical Preview per Configuration Manager](technical-preview.md) prima di installare questa versione della Technical Preview. L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problemi noti di questa versione Technical Preview:**
- **L'aggiornamento a una nuova versione di anteprima ha esito negativo se il server del sito è in modalità passiva**. Se si usa un [server del sito primario in modalità passiva](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima dell'aggiornamento a questa nuova versione di anteprima. Sarà possibile reinstallare il server del sito in modalità passiva al termine dell'aggiornamento del sito.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Creare distribuzioni in fasi
<!-- 1357405 -->
Le distribuzioni in fasi automatizzano un'implementazione del software coordinata e in sequenza senza creare più distribuzioni. In questa versione Technical Preview è possibile completare la distribuzione guidata in fasi per le sequenze di attività nella console di amministrazione. Le distribuzioni non vengono tuttavia create. 

### <a name="try-it-out"></a>Verifica  
  Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.
 
**Creare una distribuzione in fasi per una sequenza di attività** </br>
1. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**.
2. Fare clic con il pulsante destro del mouse su una sequenza di attività esistente e selezionare **Create Phased Deployment** (Crea distribuzione in fasi). 
3. Nella scheda **Generale** assegnare alla distribuzione in fasi un nome e una descrizione (facoltativa), quindi selezionare **Automatically create default pilot and production phases** (Crea automaticamente fasi pilota e di produzione predefinite). 
4. Popolare i campi **Raccolta pilota** e **Raccolta produzione**. Selezionare **Avanti**.
5. Nella scheda **Impostazioni** scegliere un'opzione per ogni impostazione di pianificazione. Al termine, selezionare **Avanti**. 
6. Nella scheda **Phases** (Fasi) modificare le fasi se necessario e fare clic su **Avanti**.
7. Confermare le selezioni nella scheda **Riepilogo** e fare clic su **Avanti** per continuare.

## <a name="co-management-reporting"></a>Creazione di report di co-gestione
<!-- 1356648 -->
Se si usano le funzionalità di [co-gestione](../../comanage/overview.md) è ora possibile visualizzare un dashboard con informazioni sulla co-gestione nell'ambiente. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Preparazione aggiornamenti** e selezionare il dashboard **Co-gestione**. Il dashboard include i riquadri seguenti:
- **Co-managed devices** (Dispositivi co-gestiti): la percentuale di dispositivi nell'ambiente abilitati per la co-gestione
- **Distribuzione del sistema operativo**: la suddivisione dei sistemi operativi per versione. In questo grafico vengono usati i raggruppamenti seguenti:
  - Windows 7 e 8.x
  - Windows 10, versioni precedenti alla 1709
  - Windows 10, versione 1709 e successive
    > [!NOTE] 
    > Windows 10, versione 1709 e successive, è un prerequisito per la co-gestione
- **Co-management status** (Stato co-gestione): la suddivisione dei dispositivi con esito positivo e negativo nelle categorie seguenti:
   - Esito positivo, aggiunto ad Azure AD ibrido
   - Esito positivo, aggiunto ad Azure AD
   - Errore: registrazione automatica non riuscita
- **Workload transition** (Transizione carico di lavoro): grafico a barre in cui viene visualizzato il numero di dispositivi passati a Microsoft Intune per i tre carichi di lavoro disponibili: 
   - Criteri di conformità
   - Accesso alle risorse
   - Windows Update for Business

### <a name="prerequisites"></a>Prerequisiti
- Il computer che esegue la console di Configuration Manager richiede Internet Explorer 9 o versione successiva.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Miglioramenti alla pianificazione di valutazione delle regole di distribuzione automatica
<!-- 1357133 -->
In risposta a quanto richiesto nei [commenti e suggerimenti in User Voice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), è ora possibile pianificare la valutazione delle regole di distribuzione automatica (ADR, Automatic Deployment Rule) con un offset da un giorno di base. Con un offset di due giorni dopo il secondo martedì del mese, ad esempio, la regola viene valutata di giovedì. 

### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione. <br/>

**Creare una pianificazione personalizzata per la valutazione di una regola di distribuzione automatica con un offset da un giorno di base** </br>
1.  Nell'area di lavoro **Raccolta software** espandere **Aggiornamenti software** e selezionare **Regole di distribuzione automatica**.
2. Fare clic con il pulsante destro del mouse su **Regole di distribuzione automatica** e scegliere **Crea regola di distribuzione automatica**. 
3. Seguire le istruzioni visualizzate per compilare le schede **Generale**, **Impostazioni di distribuzione** e **Aggiornamenti software**. 
4. Nella scheda **Pianificazione valutazione** selezionare **Esegui la regola in base a una pianificazione** e **Personalizza**.
5. Per la pianificazione personalizzata selezionare **Mensile** e immettere un giorno di base, ad esempio il secondo martedì. 
6. Selezionare **Offset (days)** (Offset (giorni) e il numero di giorni per l'offset. Al termine, scegliere **OK**.  
7. Completare il resto della **Creazione guidata delle regole di distribuzione automatica**. 



## <a name="reassign-distribution-point"></a>Riassegnare un punto di distribuzione
<!-- 1306937 -->
Molti clienti hanno infrastrutture di Configuration Manager di grandi dimensioni e stanno diminuendo i siti primari o secondari per semplificare il proprio ambiente. Per distribuire il contenuto ai client gestiti, questi clienti devono comunque mantenere i punti di distribuzione nelle succursali. Questi punti di distribuzione spesso includono più terabyte di contenuto. La distribuzione di questo contenuto ai server remoti è dispendiosa in termini di tempo e larghezza di banda di rete. 

Questa funzionalità consente di riassegnare un punto di distribuzione a un altro sito primario senza ridistribuire il contenuto. Questa azione aggiorna l'assegnazione del sistema del sito mantenendo tutto il contenuto nel server. Se è necessario riassegnare più punti di distribuzione, eseguire prima questa azione su un singolo punto di distribuzione, quindi procedere con gli altri server uno alla volta.

> [!IMPORTANT]
> Il server del sistema del sito può ospitare solo il ruolo del punto di distribuzione. Se il server del sistema del sito ospita un altro ruolo del server di Configuration Manager, ad esempio il punto di migrazione stato, non sarà possibile riassegnare il punto di distribuzione. Non è possibile riassegnare un punto di distribuzione cloud. 

Questa opzione non funziona in questa versione a causa del limite della Technical Preview a un solo sito primario. Valutare lo scenario e inviare **Commenti e suggerimenti** sulle funzionalità di questa azione dalla scheda **Home** della barra multifunzione.
1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**.
2. Fare clic con il pulsante destro del mouse sul punto di distribuzione di destinazione e selezionare **Riassegna punto di distribuzione**. 
  ![Riassegna punto di distribuzione](media/1306937-reassign-dp.png)
3. Selezionare il server del sito e il codice del sito a cui si intende riassegnare il punto di distribuzione. 
  ![Seleziona un server del sito](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Miglioramenti all'inventario hardware
<!-- 1357389 -->
Per le classi appena aggiunte è possibile specificare lunghezze di stringa superiori a 255 caratteri per le proprietà dell'inventario hardware diverse dalle chiavi.

### <a name="try-it-out"></a>Verifica  
Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.<br/>

1. Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**, evidenziare l'impostazione di un dispositivo client da modificare, fare clic con il pulsante destro del mouse e selezionare **Proprietà**. 
2. Selezionare **Inventario hardware**, quindi **Imposta classi** e **Aggiungi**.
3. Fare clic sul pulsante **Connetti**.
4. Compilare i campi **Nome computer**, **Spazio dei nomi WMI** e selezionare **ricorsivo** se necessario. Immettere le credenziali, se necessarie per la connessione. Fare clic su **Connetti** per visualizzare le classi dello spazio dei nomi.
5. Selezionare una nuova classe e fare clic su **Modifica**.
6. Modificare la **Lunghezza** di almeno una proprietà stringa, diversa dalla chiave, in modo che sia maggiore di 255. Fare clic su **OK**. 
7. Assicurarsi che la proprietà modificata sia selezionata per **Aggiungi classe di inventario hardware** e fare clic su **OK**. 
8. Raccogliere l'inventario hardware con la classe appena aggiunta che contiene una proprietà di lunghezza superiore ai 255 caratteri. 



## <a name="improvements-to-client-settings-for-software-center"></a>Miglioramenti alle impostazioni client per Software Center
<!-- 1351224 & 1355146 -->
In questa versione della Technical Preview sono stati apportati miglioramenti per la personalizzazione di Software Center nelle impostazioni client. 

1. Le impostazioni client per Software Center ora includono un pulsante **Personalizza**.
2. È stata aggiunta un'anteprima che consente di visualizzare l'aspetto del banner di Software Center.<!--1351224-->
    - Se non viene selezionato un logo, nell'anteprima viene visualizzato il testo del nome della società e il colore.
    - Se viene selezionato un logo, nell'anteprima viene visualizzato il logo e il testo del nome della società.  
3.  **Nascondi le applicazioni non approvate nel Software Center** è una nuova impostazione per Software Center. Quando questa opzione è abilitata, le applicazioni disponibili per l'utente che richiedono l'approvazione sono nascoste in Software Center.<!--1355146-->

### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività. Quindi inviare **Commenti e suggerimenti** dalla scheda **Home** della barra multifunzione.

1. Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**. Selezionare l'impostazione di un dispositivo client da modificare. Fare clic su di essa con il pulsante destro del mouse, selezionare **Proprietà** e quindi **Software Center**.
2.  Fare clic sul pulsante **Personalizza**. Provare le diverse impostazioni di personalizzazione inclusa l'anteprima.
3. Abilitare l'impostazione **Nascondi le applicazioni non approvate nel Software Center**. Osservare le modifiche in Software Center. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Nuove impostazioni per Windows Defender Application Guard
<!-- 1356256 -->
Per i dispositivi Windows 10 versione 1709 e successive sono disponibili due nuove impostazioni per l'interazione con l'host per [Windows Defender Application Guard](../../protect/deploy-use/create-deploy-application-guard-policy.md). 
1. È possibile concedere ai siti Web l'accesso all'unità di elaborazione grafica virtuale dell'host. 
2. È possibile salvare in modo permanente nell'host i file scaricati all'interno del contenitore. </br>



## <a name="improvements-to-run-scripts"></a>Miglioramenti alla funzionalità Esegui script
<!-- 1236459 -->
La [funzionalità **Esegui script**](../../apps/deploy-use/create-deploy-scripts.md) consente ora di importare ed eseguire script PowerShell firmati. 
- Per mantenere l'integrità dello script, è necessario importare gli script firmati anziché usare l'operazione di copia e incolla. 
- Dopo l'importazione non è possibile modificare gli script firmati importati.
    
>[!IMPORTANT]
>In questa Technical Preview sono presenti due limitazioni temporanee.
>- Gli script possono essere importati solo nella funzionalità Esegui script e non possono essere modificati direttamente dalla console.
>- È possibile che gli script importati con una codifica non Unicode non vengano visualizzati correttamente nella console. Lo script verrà comunque eseguito come è stato scritto in origine.





## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
