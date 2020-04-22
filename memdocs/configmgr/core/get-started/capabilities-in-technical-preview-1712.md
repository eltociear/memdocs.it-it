---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1712 per Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705079"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1712 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1712. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. 

Vedere [Technical Preview per Configuration Manager](technical-preview.md) prima di installare questa versione della Technical Preview. L'articolo consente di acquisire familiarità con i requisiti e le limitazioni generali per l'uso di una Technical Preview, con l'aggiornamento tra le versioni e con l'invio di commenti e suggerimenti sulle funzionalità di una Technical Preview.     


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
  <!--sms489412-->


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Non vengono aggiornate automaticamente le applicazioni sostituite
<!-- 1351266 -->
In base ai [commenti e suggerimenti di UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), in questa versione è possibile configurare una distribuzione dell'applicazione in modo da non aggiornare automaticamente eventuali versioni sostituite. Ora quando si crea la distribuzione, nella pagina **Impostazioni di distribuzione** della **Distribuzione guidata del software**, ai fini di un'installazione **disponibile** o **necessaria**, è possibile abilitare o disabilitare l'opzione che consente di **aggiornare automaticamente eventuali versioni sostituite dell'applicazione**.


## <a name="install-multiple-applications-in-software-center"></a>Installare più applicazioni nel Software Center
<!-- 1357126 -->
Se un utente finale o un tecnico desktop deve installare più applicazioni in un dispositivo, il Software Center ora supporta l'installazione di più applicazioni selezionate. Ciò consente all'utente di essere più efficiente senza dover aspettare che termini un'installazione prima di avviare quella successiva.

Quando si usa la modalità di selezione multipla nella scheda **Applicazioni** i seguenti criteri determinano quali app vengono abilitate nel Software Center per la selezione multipla:
- L'app è visibile all'utente
- L'app non è già installata
- L'approvazione dell'amministratore non è necessaria o è già stata concessa
- Lo stato dell'app è disponibile (ad esempio, non sta ancora scaricando contenuto)

### <a name="try-it-out"></a>Verifica
**Nella console di Configuration Manager:** distribuire a un utente o un dispositivo più applicazioni per l'installazione, disponibile o richiesta (con scadenza nel futuro). Non è richiesta l'approvazione dell'amministratore. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../apps/deploy-use/deploy-applications.md).

**Nel Software Center:**
 1. La scheda **Applicazioni** si deve aprire per impostazione predefinita. 
 2. Per immettere la modalità selezione multipla nella visualizzazione elenco, fare clic sull'icona Nuovo ![Icona di selezione multipla del Software Center](media/software-center-multi-select-apps.png) nell'angolo superiore destro.
 3. Selezionare due o più app da installare facendo clic sulla casella di controllo a sinistra delle app nell'elenco.
 4. Fare clic sul pulsante di **installazione degli elementi selezionati**.

Le app vengono installate come di consueto, ma in successione.


## <a name="client-based-pxe-responder-service"></a>Servizio risponditore PXE basato su client
<!-- 1357148 -->
Un problema comune per i clienti è erogare servizi PXE in postazioni remote o succursali con infrastruttura server minima o assente. Il ruolo punto di distribuzione supporta i sistemi operativi client, ma non può essere abilitato per PXE a causa della dipendenza dai servizi di distribuzione Windows.

Sono ora disponibili nuove impostazioni client per l'abilitazione di un servizio risponditore PXE nei client di Configuration Manager. Un'immagine di avvio che supporta PXE deve trovarsi nella cache del client del risponditore PXE.

### <a name="try-it-out"></a>Verifica
Verificare che non vi siano già punti di distribuzione abilitati per PXE o altri server PXE nell'ambiente di test che possano essere in conflitto con il risponditore PXE nel client.

Nella console di Configuration Manager:
1. Nell'area di lavoro **Raccolta software**, in **Sistemi operativi**, **Sequenze attività**: creare una sequenza di attività usando il modello personalizzato.
   1. Fare clic su **Aggiungi**, selezionare **Generale** e quindi il passaggio **Imposta variabile della sequenza di attività**. Immettere **SMSTSPersistContent** come variabile della sequenza di attività, quindi immettere il valore **TRUE**.
   1. Fare clic su **Aggiungi**, selezionare **Software** e quindi il passaggio **Scarica contenuto pacchetto**. Fare clic sull'asterisco dorato e quindi selezionare un'immagine di avvio che supporta PXE. Includere le immagini di avvio x86 e x64. Configurare il passaggio da inserire nella **cache del client di Configuration Manager**.
   1. Fare clic su **Aggiungi**, selezionare **Generale** e quindi il passaggio **Imposta variabile della sequenza di attività**. Immettere **SMSTSPreserveContent** come variabile della sequenza di attività, quindi immettere il valore **TRUE**.
2. Nell'area di lavoro **Amministrazione**, **Impostazioni client**: creare un criterio di impostazioni dispositivo client personalizzate.
   1. Selezionare il gruppo **Impostazioni della cache del client**.
   1. Impostare l'opzione **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti** su **Sì**.
   1. Impostare l'opzione **Abilita il servizio risponditore PXE** su **Sì**.
   1. Per l'impostazione **Creare un certificato autofirmato o importare un certificato client PKI**, fare clic su **Specificare un certificato**. Selezionare **Importa certificato** se l'ambiente di test ha PKI, altrimenti fare clic su **OK** per creare un certificato autofirmato. 
   1. Configurare le altre impostazioni secondo le esigenze dell'ambiente di test. Le impostazioni predefinite devono funzionare a meno che non esistano requisiti specifici di sicurezza o di rete.
3. Distribuire la sequenza di attività e le impostazioni client personalizzate a una raccolta di client di destinazione identificati come risponditori PXE. Attendere che i criteri vengano applicati e che la sequenza di attività venga eseguita.
4. Avviare un altro client nella stessa subnet per avviare la rete PXE come di consueto.

### <a name="known-issues"></a>Problemi noti
- L'editor della sequenza di attività visualizza un'icona rossa di errore per il passaggio **Scarica contenuto pacchetto** quando si aggiunge un'immagine di avvio, ma la sequenza di attività viene salvata correttamente. Quando si apre di nuovo questa sequenza di attività nell'editor appare un avviso informativo che indica che non è possibile trovare gli oggetti a cui viene fatto riferimento. <!-- sms427542 -->
- L'immagine di avvio del passaggio Scarica contenuto pacchetto non appare nell'elenco di riferimenti della sequenza di attività personalizzata. Anche l'azione **Distribuisci contenuto** non è disponibile. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Modifica dell'installazione del client di Configuration Manager  
In seguito ai commenti e suggerimenti di UserVoice, [Silverlight non viene più installato automaticamente nei client.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Modifica del dashboard del dispositivo Surface
Il dashboard di Surface ora visualizza la versione del firmware per i dispositivi Surface anziché la versione del sistema operativo. Nella console passare a **Monitoraggio** > **Surface Devices** (Dispositivi Surface). È possibile visualizzare i seguenti elementi:
- Percentuale di dispositivi Surface
- Percentuale di modelli Surface
- Prime cinque versioni di firmware
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Miglioramenti del dashboard di Gestione client di Office 365 
Il dashboard di Gestione client di Office 365 ora visualizza un elenco di dispositivi rilevanti quando vengono selezionate le sezioni del grafico. Nella console passare a **Raccolta software** >**Panoramica** >**Gestione client di Office 365**. Il dashboard viene visualizzato a destra. Se si selezionano i criteri dal grafico, viene visualizzato un elenco di dispositivi.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Miglioramenti della console di Configuration Manager 
Sono stati apportati i miglioramenti seguenti alla console di Configuration Manager, molti dei quali sono il risultato dei commenti e suggerimenti di UserVoice.

- [Nell'elenco di dispositivi è visualizzato l'utente primario](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): Gli elenchi di dispositivi in Asset e conformità, Dispositivi, ora visualizzano l'utente primario per impostazione predefinita. L'ultimo utente connesso può inoltre essere aggiunto come colonna facoltativa. <!-- 1357280 -->
- [Le raccolte rinominate vengono visualizzate nelle regole di appartenenza della raccolta esistenti](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Se una raccolta è membro di un'altra raccolta e viene rinominata, il nuovo nome viene aggiornato nelle regole di appartenenza.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Miglioramenti alla distribuzione del sistema operativo
Sono stati apportati i miglioramenti seguenti alla distribuzione del sistema operativo a seguito dei commenti e suggerimenti di UserVoice.
- [Visualizzatore log predefinito nell'immagine d'avvio](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): In Windows PE quando si avvia cmtrace.exe non viene più richiesto di scegliere se rendere questo programma lo strumento di visualizzazione predefinito per i file di log. <!-- SMS 500897 -->
- Passaggio Scarica contenuto pacchetto: ora è possibile aggiungere immagini d'avvio a questo passaggio della sequenza di attività.


## <a name="windows-10-feedback-hub-app-integration"></a>Integrazione di app dell'hub di commenti e suggerimenti di Windows 10

Il feedback degli utenti è così importante che ora è abilitato attraverso l'[app dell'hub di commenti e suggerimenti](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporata in Windows 10. Quando si sceglie **Aggiungi nuovo feedback**, assicurarsi di selezionare la categoria **Enterprise Management** e di scegliere una delle sottocategorie seguenti:
- Client di Configuration Manager
- Console di Configuration Manager
- Distribuzione del sistema operativo di Configuration Manager
- Server di Configuration Manager

Continuare a usare la [pagina UserVoice](https://configurationmanager.uservoice.com/) per votare nuove idee sulle funzionalità di Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
