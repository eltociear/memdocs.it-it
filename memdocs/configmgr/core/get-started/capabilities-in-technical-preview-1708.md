---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1708 per Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705159"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1708 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1708. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemi noti di questa versione Technical Preview:**
- **L'aggiornamento alla versione Technical Preview 1708 ha esito negativo se il server del sito è in modalità passiva**. Quando si esegue la versione Technical Preview 1706 o 1707 ed è presente un [server del sito primario in modalità passiva](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima di poter aggiornare il sito Technical Preview alla versione 1708. Sarà possibile reinstallare il server del sito in modalità passiva quando nel sito è in esecuzione la versione 1708.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.




**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Miglioramenti per specificare i parametri degli script quando si distribuiscono gli script di PowerShell da Configuration Manager
<!-- 1236459 -->

Da Configuration Manager 1706 in poi, è possibile [creare ed eseguire script di PowerShell dalla console di Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).

In [Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) la funzionalità è stata ampliata in modo da consentire a Configuration Manager di leggere i parametri dello script.

In questa versione di Technical Preview è stata ampliata la capacità dei parametri degli script di rilevare i parametri obbligatori e facoltativi e chiedere di immetterli.

### <a name="try-it-out"></a>Verifica

1. Seguire le istruzioni per [creare ed eseguire script di PowerShell dalla console di Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).
2. Nella nuova pagina **Parametri script** della **creazione guidata di script** scegliere un parametro e quindi modificare i valori.
La procedura guidata mostra quali parametri sono obbligatori e quali sono facoltativi.
4. Al termine della modifica dei parametri, completare la procedura guidata.

Quando viene eseguito lo script, verranno usati i valori dei parametri configurati. Se non è stato configurato un parametro obbligatorio, all'utente finale viene chiesto di fornire il parametro quando viene eseguito lo script.

## <a name="management-insights"></a>Informazioni dettagliate sulla gestione
<!-- 1353967 -->
Ora è possibile ottenere informazioni dettagliate sullo stato corrente dell'ambiente in base all'analisi dei dati nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. Rivedere le informazioni dettagliate sulla gestione nella console di Configuration Manager in **Amministrazione** > **Management Insights** (Informazioni dettagliate gestione) > **All Insights** (Tutte le informazioni dettagliate). In questa versione sono disponibili le informazioni dettagliate seguenti:

- **Applicazioni senza distribuzioni**: elenca le applicazioni dell'ambiente senza distribuzioni attive. Aiuta a individuare ed eliminare le applicazioni non usate per semplificare l'elenco di applicazioni visualizzato nella console.
- **Raccolte vuote**: un elenco delle raccolte dell'ambiente che non hanno membri. È possibile eliminare queste raccolte ad esempio per semplificare l'elenco delle raccolte visualizzate durante la distribuzione di oggetti.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Riavviare i computer dalla console di Configuration Manager   
<!-- 1356283 -->
A partire da questa versione, è possibile usare la console di Configuration Manager per identificare i dispositivi client che richiedono il riavvio e quindi usare un'azione di notifica client per riavviarli.

Per identificare i dispositivi in attesa di riavvio, passare ad **Asset e conformità** > **Dispositivi** e selezionare una raccolta con i dispositivi che potrebbero richiedere un riavvio. Dopo aver selezionato una raccolta, è possibile visualizzare lo stato per ogni dispositivo nel riquadro dei dettagli, in una nuova colonna denominata **Riavvio in sospeso**. Ogni dispositivo ha un valore **Sì** o **No**.

Per creare la notifica client per riavviare un dispositivo:
1. Individuare il dispositivo da riavviare nel nodo Dispositivi della console.
2. Fare clic con il pulsante destro del mouse sul dispositivo, selezionare **Notifica client**, quindi selezionare **Riavvia**. Verrà visualizzata una finestra di informazioni sul riavvio. Fare clic su **OK** per riavviare la richiesta.

Quando la notifica viene ricevuta da un client, viene visualizzata una finestra di notifica di **Software Center** per informare l'utente del riavvio. Per impostazione predefinita, il riavvio viene eseguito dopo 90 minuti. È possibile modificare il tempo di riavvio configurando le [impostazioni del client](../clients/deploy/configure-client-settings.md). Le impostazioni per il comportamento del riavvio sono disponibili nella scheda [Riavvio del computer](../clients/deploy/about-client-settings.md#computer-restart) delle impostazioni predefinite.


### <a name="try-it-out"></a>Verifica
Provare a completare le attività seguenti e quindi inviare **Feedback** dalla scheda **Home** della barra multifunzione per comunicarci come è andata:
1. Distribuire un'app o un aggiornamento a un dispositivo richiederà che il dispositivo venga riavviato per completare l'installazione.
2. Individuare il dispositivo nel nodo **Asset e conformità** > **Dispositivi** della console e verificare sia visualizzato **Sì** nella colonna **Riavvio in sospeso**. Prima che lo stato Riavvio in sospeso venga visualizzato nella console potrebbero passare fino a 20 minuti.
3. Monitorare il dispositivo per confermare che la notifica di Software Center si apra e che il dispositivo venga riavviato correttamente.


## <a name="software-center-customization"></a>Personalizzazione di Software Center
<!-- 1351224 -->
È possibile aggiungere elementi di branding aziendale e specificare la visibilità delle schede in Software Center. È possibile aggiungere il nome specifico della società per Software Center, impostare un tema di colori per la configurazione di Software Center, impostare il logo della società e impostare le schede visibili per i dispositivi client.

### <a name="customize-software-center"></a>Personalizzare Software Center

Per modificare Software Center:

1. Nella console di **Configuration Manager** scegliere **Amministrazione** > **Impostazioni client**. Fare clic sull'istanza di impostazione client desiderata.
2. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.
3. Nella finestra di dialogo **Impostazioni predefinite** scegliere **Software Center**.
4. Selezionare **Sì** per **scegliere le nuove impostazioni per specificare informazioni sulla società**, in modo da abilitare le impostazioni di personalizzazione di Software Center.
5. Digitare il **nome della società**.
6. Selezionare la **combinazione colori per Software Center**.
7. Fare clic su **Sfoglia** per accedere al logo per Software Center. Il logo deve essere di 400 x 100 pixel, nel formato JPEG o PNG e con dimensioni massime di 750 KB.
8. Selezionare **SÌ** per rendere visibili le schede in Software Center per i dispositivi client. È necessario che sia visibile almeno una scheda:

    -  Scheda Enable Applications (Abilita applicazioni)
    -  Scheda Abilita aggiornamenti
    -  Scheda Enable Operating Systems (Abilita sistemi operativi)
    -  Scheda Enable Installation Status (Abilita stato installazione)
    -  Scheda Enable Device compliance (Abilita conformità dispositivo)
    -  Scheda Enable Options (Abilita opzioni)

### <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla gestione delle applicazioni in Configuration Manager, vedere [Introduzione alla gestione delle applicazioni](../../apps/understand/introduction-to-application-management.md).
