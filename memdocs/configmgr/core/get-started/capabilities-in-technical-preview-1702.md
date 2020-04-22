---
title: Funzionalità nella Technical Preview 1702
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1702 per Configuration Manager.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 73b8111cbada129997cec965ca685f1ef22b1f3a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705309"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1702 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1702. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Inviare commenti e suggerimenti dalla console di Configuration Manager

Questa anteprima introduce nuove opzioni per l'invio di commenti e suggerimenti nella console di Configuration Manager. Le opzioni di Commenti e suggerimenti consentono di inviare commenti e suggerimenti direttamente al team di sviluppo, tramite il sito Web UserVoice di Configuration Manager.  

> È possibile trovare l'opzione **Commenti e suggerimenti**:
> -  Nella barra multifunzione, all'estrema sinistra della scheda Home di ogni nodo.  
>    ![Barra multifunzione](./media/feedback-home.png)

-  Facendo clic con il pulsante destro del mouse su qualsiasi oggetto nella console.   
    ![Opzione con clic con il pulsante destro del mouse](./media/feedback-option.png)   

Quando si seleziona **Commenti e suggerimenti**, il browser visualizza il sito Web UserVoice di Configuration Manager all'indirizzo https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Modifiche per Aggiornamenti e manutenzione
Le modifiche seguenti sono state introdotte con questa versione di anteprima.

**Opzioni di aggiornamento più semplici**  
Quando l'infrastruttura necessita di due o più aggiornamenti, viene scaricato solo l'aggiornamento più recente. Ad esempio, se la versione corrente del sito è più vecchia di due o più versioni rispetto alla versione più recente disponibile, viene scaricata automaticamente solo la versione più recente dell'aggiornamento.  

È possibile scaricare e installare gli altri aggiornamenti disponibili, anche quando non sono la versione più recente. Tuttavia, si riceverà un avviso che notificherà che l'aggiornamento è stato sostituito da una versione più recente. Per scaricare un aggiornamento *Disponibile per il download*, selezionare l'aggiornamento nella console e quindi fare clic su **Scarica**.

**Miglioramento della pulizia degli aggiornamenti precedenti**   
È stata aggiunta una funzione di pulizia automatica che elimina i download non necessari dalla cartella 'EasySetupPayload' nel server del sito.  


## <a name="peer-cache-improvements"></a>Miglioramenti della peer cache
A partire da questa versione, il computer di origine della peer cache rifiuta le richieste di contenuti quando soddisfa una delle condizioni seguenti:  
-  È in modalità di batteria in esaurimento.
-  Il carico della CPU supera l'80% nel momento in cui il contenuto viene richiesto.
-  L'I/O disco ha un valore di *AvgDiskQueueLength* superiore a 10.
-  Non vi sono più connessioni disponibili al computer.   

È possibile configurare queste impostazioni tramite la classe di configurazione dell'agente client per la funzionalità di origine peer (*SMS_WinPEPeerCacheConfig*) quando si usa l'SDK di Configuration Manager.

Quando il computer rifiuta una richiesta di contenuto, il computer richiedente continuerà a cercare il contenuto da origini alternative nel pool dei percorsi di origine del contenuto disponibili.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a>Usare Azure Active Directory Domain Services per gestire dispositivi, utenti e gruppi

Con questa versione di Technical Preview è possibile gestire i dispositivi aggiunti a un dominio gestito di servizi di Azure Active Directory (AD) Domain Services. È anche possibile individuare dispositivi, utenti e gruppi nel dominio con vari metodi di individuazione di Configuration Manager.

L'infrastruttura del sito e i client di Technical Preview e il dominio di Azure AD Domain Services devono essere eseguiti in Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configurare Configuration Manager per l'uso di Azure AD
Per usare Azure AD con Configuration Manager, è necessario quanto segue:
- Sottoscrizione di Azure.
- Azure AD con Domain Services (DS).
- Sito di Configuration Manager eseguito in una macchina virtuale di Azure aggiunta ad Azure AD.
- Client di Configuration Manager in esecuzione nello stesso ambiente di Azure AD.

Per configurare Azure AD Domain Services, vedere [Introduzione a Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Individuare risorse
Dopo avere configurato Configuration Manager per l'esecuzione in Azure AD, è possibile usare i metodi di individuazione di Active Directory seguenti per la ricerca di risorse in Azure AD:  
- Individuazione sistema Active Directory
- individuazione utenti di Active Directory
- Individuazione gruppo Active Directory  

Per ogni metodo da usare, modificare la query LDAP per cercare le strutture di unità organizzativa di Azure Active Directory anziché i contenitori tipici di Active Directory locale. Questo richiede che la query venga indirizzata per la ricerca in Active Directory nella sottoscrizione di Azure.  

Negli esempi seguenti viene usata una Azure AD di *contoso.onmicrosoft.com*:
- **Individuazione del sistema**   
  Azure AD archivia i dispositivi nell'unità organizzativa **AADDC Computers**.  Configurare quanto segue:  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **Individuazione degli utenti** AAD archivia gli utenti nell'unità organizzativa **AADDC Users**.  Configurare quanto segue:
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Individuazione dei gruppi**  
Azure AD non ha un'unità organizzativa dove archiviare i gruppi. Al contrario, usare la stessa struttura generale delle query relative al sistema o agli utenti e configurare la query LDAP in modo che punti all'unità organizzativa contenente i gruppi da individuare.

Per altre informazioni su Azure AD, vedere gli argomenti seguenti:  
- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) su azure.microsoft.com.
- [Documentazione di Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services) su docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Miglioramento dei criteri di conformità dei dispositivi per l'accesso condizionale

È ora disponibile una nuova regola di criteri di conformità dei dispositivi per impedire l'accesso alle risorse aziendali che supportano l'accesso condizionale, quando gli utenti usano applicazioni incluse in un elenco di app non conformi. L'elenco di app non conformi può essere definito dall'amministratore quando si aggiunge la nuova regola conforme **App che non possono essere installate**. Questa regola richiede che l'amministratore immetta **Nome app**, **ID app** e **Autore app** (facoltativo) quando si aggiunge un'app all'elenco di app non conformi. Questa impostazione si applica solo a dispositivi iOS e Android.

Ciò consente alle organizzazioni di ridurre la perdita di dati da app non protette e di impedire l'uso eccessivo di dati in alcune applicazioni.

### <a name="try-it-out"></a>Procedura

**Scenario:** identificare le app che potrebbero causare perdita di dati inviando dati aziendali all'esterno dell'azienda o che causano un uso eccessivo dei dati e quindi [creare un criterio di conformità dei dispositivi per l'accesso condizionale](../../mdm/understand/what-happened-to-hybrid.md) che aggiunge queste app all'elenco di app non conformi. In questo modo verrà bloccato l'accesso alle risorse aziendali che supportano l'accesso condizionale fino a quando l'utente non potrà rimuovere l'app bloccata.

## <a name="antimalware-client-version-alert"></a>Avviso della versione del client antimalware
A partire da questa versione della Technical Preview, Configuration Manager Endpoint Protection genera un avviso se oltre il 20% (valore predefinito) dei client gestiti usa una versione obsoleta del client antimalware, ad esempio il client di Windows Defender o Endpoint Protection.

### <a name="try-it-out"></a>Procedura
Assicurarsi che Endpoint Protection sia abilitato su tutti i client desktop e server mediante i criteri delle impostazioni client. È ora possibile visualizzare **Versione client antimalware** e **Endpoint Protection Deployment Status** (Stato distribuzione Endpoint Protection) passando ad **Asset e conformità** > **Panoramica** > **Dispositivi** > **Tutti i client desktop e di server**. Per controllare un avviso, visualizzare **Avvisi** nell'area di lavoro **Monitoraggio**. Se più del 20% dei client gestiti esegue una versione scaduta del software antimalware, viene visualizzato l'avviso La versione del client antimalware è obsoleta. Questo avviso non viene visualizzato nella scheda **Monitoraggio** > **Panoramica**. Per aggiornare i client antimalware scaduti, abilitare gli aggiornamenti software per i client antimalware.

Per configurare la percentuale oltre la quale viene generato l'avviso, espandere **Monitoraggio** > **Avvisi** > **Tutti gli avvisi**, fare doppio clic su **I client antimalware sono obsoleti** e modificare l'opzione **Genera un avviso se la percentuale di client gestiti con una versione obsoleta del client antimalware è superiore a**.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Valutazione della conformità degli aggiornamenti di Windows Update for Business
È ora possibile configurare una regola di aggiornamento dei criteri di conformità per includere i risultati della valutazione di Windows Update for Business nella valutazione dell'accesso condizionale.
> [!IMPORTANT]
> È necessario Windows 10 Insider Preview Build 15019 o versione successiva per usare la valutazione della conformità per gli aggiornamenti di Windows Update for Business.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Consentire a Windows Update for Business di gestire gli aggiornamenti di Windows 10
Per raccogliere informazioni di valutazione della conformità per Windows Update for Business, usare la procedura seguente per configurare le impostazioni dell'agente client perché consenta esplicitamente a Windows Update for Business di gestire gli aggiornamenti di Windows 10.
1. Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**.
2. Nelle proprietà per le impostazioni client passare a **Aggiornamenti software** e selezionare **Sì** per l'impostazione **Gestione degli aggiornamenti di Windows 10 con Windows Update for Business**.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Creare criteri di conformità per la valutazione di Windows Update for Business
1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Criteri di conformità**.
2. Fare clic su **Crea criteri di conformità** o selezionare un criterio di conformità esistente da modificare.
3. Nella pagina Generale specificare un nome e una descrizione, selezionare **Regole di conformità per i dispositivi gestiti con il client di Configuration Manager**, impostare la gravità di non conformità per la creazione di report e fare clic su **Avanti**.
4. Nella pagina Piattaforme supportate selezionare **Windows 10** e fare clic su **Avanti**.
5. Nella pagina Regole fare clic su **Nuovo**, quindi per **Condizione** scegliere **Require Windows Update for Business compliance** (Richiedi conformità Windows Update for Business). L'impostazione **Valore** viene impostata automaticamente su **True**.

Il nuovo criterio viene visualizzato nel nodo **Criteri di conformità** dell'area di lavoro **Asset e conformità** .

### <a name="deploy-a-compliance-policy"></a>Distribuire i criteri di conformità
1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** e quindi su **Criteri di conformità**.
2. Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.
3. Nella finestra di dialogo **Distribuisci criteri di conformità** , fare clic su **Sfoglia** per selezionare la raccolta utente a cui distribuire il criterio.
   È anche possibile selezionare le opzioni per creare avvisi da inviare quando il criterio non è conforme. È anche possibile configurare la pianificazione in base alla quale verrà valutata la conformità del criterio.
4. Al termine, fare clic su **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorare i criteri di conformità
Dopo aver creato i criteri di conformità, è possibile monitorare i risultati di conformità nella console di Configuration Manager. Per informazioni dettagliate, vedere [Monitorare i criteri di conformità](../../mdm/understand/what-happened-to-hybrid.md).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Miglioramenti alle impostazioni e ai messaggi di notifica di Software Center per le sequenze di attività a impatto elevato
Questa versione include i miglioramenti seguenti alle impostazioni di Software Center e ai messaggi di notifica per le sequenze di attività di distribuzione a impatto elevato:

- Nelle proprietà per la sequenza di attività è ora possibile configurare qualsiasi sequenza di attività, comprese le sequenze di attività non del sistema operativo, come distribuzioni ad alto rischio. Qualsiasi sequenza di attività che soddisfi determinate condizioni viene definita automaticamente come a impatto elevato. Per altri dettagli, vedere [Gestire le distribuzioni ad alto rischio](../servers/manage/settings-to-manage-high-risk-deployments.md).
- Nelle proprietà per la sequenza di attività è possibile scegliere di usare il messaggio di notifica predefinito o crearne uno personalizzato per le distribuzioni a impatto elevato.
- Nelle proprietà per la sequenza di attività è possibile configurare le proprietà di Software Center, tra cui l'obbligatorietà del riavvio, le dimensioni del download della sequenza di attività e il tempo di esecuzione stimato.
- Il messaggio predefinito di distribuzione a impatto elevato per gli aggiornamenti sul posto indica ora che la migrazione di applicazioni, dati e impostazioni è stata eseguita automaticamente. In precedenza il messaggio predefinito per qualsiasi installazione del sistema operativo indicava che tutte le applicazioni, i dati e le impostazioni sarebbero andati persi, il che non era vero per gli aggiornamenti sul posto.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Impostare una sequenza di attività come una sequenza di attività a impatto elevato
Attenersi alla procedura seguente per impostare una sequenza di attività a impatto elevato.
> [!NOTE]
> Qualsiasi sequenza di attività che soddisfi determinate condizioni viene definita automaticamente come a impatto elevato. Per altri dettagli, vedere [Gestire le distribuzioni ad alto rischio](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Sequenze di attività**.
2. Selezionare l'attività da modificare e fare clic su **Proprietà**.
3. Nella scheda **Notifica utente** selezionare **Questa è una sequenza di attività a impatto elevato**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Creare una notifica personalizzata per le distribuzioni ad alto rischio
1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Sequenze di attività**.
2. Selezionare l'attività da modificare e fare clic su **Proprietà**.
3. Nella scheda **Notifica utente** selezionare **Usa il testo personalizzato**.
   > [!NOTE]
   >  È possibile impostare il testo della notifica utente solo quando l'opzione **Questa è una sequenza di attività a impatto elevato** è selezionata.

4. Configurare le impostazioni seguenti (massimo 255 caratteri per casella di testo):

   **Testo dell'intestazione della notifica all'utente**: specifica il testo blu che viene visualizzato nella notifica utente di Software Center. Ad esempio, nella notifica utente predefinita questa sezione contiene un testo simile a "Confermare l'aggiornamento del sistema operativo in questo computer".

   **Testo del messaggio di notifica all'utente**: sono presenti tre caselle di testo che specificano il corpo della notifica personalizzata.
   - Prima casella di testo: specifica il corpo principale del testo, in genere contenente le istruzioni per l'utente. Ad esempio, nella notifica utente predefinita questa sezione contiene un testo simile a "L'aggiornamento del sistema operativo potrebbe durare a lungo e richiedere più riavvii del computer".
   - Seconda casella di testo: specifica il testo in grassetto nel corpo principale del testo. Ad esempio, nella notifica utente predefinita questa sezione contiene un testo simile a "Questo aggiornamento sul posto installa il nuovo sistema operativo ed esegue automaticamente la migrazione di app, dati e impostazioni".
   - Terza casella di testo: specifica l'ultima riga di testo in grassetto. Ad esempio, nella notifica all'utente predefinita questa sezione contiene un testo simile a "Fare clic su Installa per iniziare, altrimenti fare clic su Annulla".   

   Si supponga di configurare la notifica personalizzata seguente nelle proprietà.

   ![Notifica personalizzata per una sequenza di attività](./media/user-notification.png)

   Verrà visualizzato il messaggio di notifica seguente quando l'utente finale apre il programma di installazione da Software Center.

   ![Notifica personalizzata per una sequenza di attività](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurare le proprietà di Software Center
Attenersi alla procedura seguente per configurare i dettagli per la sequenza di attività visualizzata in Software Center. Tali dettagli sono solo a scopo informativo.  
1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Sequenze di attività**.
2. Selezionare l'attività da modificare e fare clic su **Proprietà**.
3. Nella scheda **Generale** sono disponibili le impostazioni seguenti per Software Center:
   - **Riavvio necessario**: consente all'utente di sapere se è necessario un riavvio durante l'installazione.
   - **Dimensioni del download (MB)** : specifica quanti megabyte vengono visualizzati in Software Center per la sequenza di attività.  
   - **Tempo di esecuzione stimato (minuti)** : specifica il tempo di esecuzione stimato in minuti che viene visualizzato in Software Center per la sequenza di attività.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Controllare l'esecuzione di file eseguibili prima di installare un'applicazione

Nella finestra di dialogo **Proprietà** *\<nome tipo di distribuzione>* di un tipo di distribuzione, nella scheda Comportamento installazione, è ora possibile specificare uno o più file eseguibili che, se in esecuzione, bloccano l'installazione del tipo di distribuzione. L'utente deve chiudere il file eseguibile in esecuzione, che in alternativa può essere chiuso automaticamente per le distribuzioni con scopo richiesto, prima dell'installazione del tipo di distribuzione.

### <a name="try-it-out"></a>Procedura.

1. Nelle proprietà di un tipo di distribuzione di Configuration Manager scegliere la scheda **Comportamento di installazione**.
2. Scegliere **Aggiungi** per aggiungere uno o più nomi di file eseguibile che si vuole cercare. È anche possibile aggiungere un nome visualizzato per facilitare agli utenti l'identificazione delle applicazioni nell'elenco.
3. Se la distribuzione avrà scopo richiesto, nella distribuzione guidata del software è possibile scegliere **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**.

Se l'applicazione è stata distribuita come **Disponibile** e un utente finale tenta di installare un'applicazione, verrà richiesto di chiudere tutti i file eseguibili in esecuzione specificati, prima di poter procedere con l'installazione.

Se l'applicazione è stata distribuita come **Richiesta** e l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione** è selezionata, verrà visualizzata una finestra di dialogo che informa che i file eseguibili specificati verranno chiusi automaticamente quando viene raggiunta la scadenza dell'installazione dell'applicazione. È possibile pianificare queste finestre di dialogo in **Impostazioni client** > **Agente computer**. Se non si vuole che l'utente finale visualizzi questi messaggi, selezionare **Nascondi in Software Center e nascondi tutte le notifiche** nella scheda **Esperienza utente** delle proprietà di distribuzione.

Se l'applicazione è stata distribuita come **Richiesta** e l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione** non è selezionata, l'installazione dell'applicazione avrà esito negativo se sono in esecuzione una o più applicazioni tra quelle specificate.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Creare certificati PFX con il supporto di S/MIME

È ora possibile creare un profilo di certificato PFX che supporta S/MIME e distribuirlo agli utenti.  Questo certificato può essere quindi usato per la crittografia S/MIME e la decrittografia nei dispositivi che l'utente ha registrato.

È ora possibile anche specificare più autorità di certificazione (CA) in più ruoli del sistema del sito del punto di registrazione certificati e quindi assegnare le richieste di processo dell'autorità di certificazione come parte del profilo di certificato.

Per i dispositivi iOS, è possibile associare un profilo di certificato PFX a un profilo di posta elettronica e abilitare la crittografia S/MIME.  Questo abilita S/MIME nel client di posta elettronica nativo in iOS e vi associa il certificato di crittografia S/MIME corretto.

Per altre informazioni sui certificati in Configuration Manager, vedere [Introduzione ai profili certificato]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Nuove impostazioni di conformità per i dispositivi iOS

Sono state aggiunte nuove impostazioni che è possibile usare negli elementi di configurazione per i dispositivi iOS. Si tratta di impostazioni che in precedenza esistevano nella configurazione autonoma di Microsoft Intune, rese ora disponibili per Intune con Configuration Manager. Per assistenza su queste impostazioni, vedere [Impostazioni dei criteri di iOS in Microsoft Intune](/mem/intune/configuration/device-restrictions-ios).

- **Sincronizza i dati dalle app gestite a iCloud**
- **Esegui handoff per continuare le attività nell'altro dispositivo**
- **Condivisione foto iCloud**
- **Libreria foto di iCloud**
- **Ritieni attendibili gli autori di una nuova app aziendale**
- **Consenti all'utente di scaricare contenuti da iBook Store contrassegnati come "Erotici"** (solo modalità di supervisione)
- **Forza gli Apple Watch associati a usare il rilevamento del polso**
- **Password per le richieste in uscita di AirPlay**
- **Modifica le impostazioni dell'account** (solo modalità di supervisione)
- **Modifiche alle impostazioni dell'utilizzo della rete dati dell'app** (solo modalità di supervisione)
- **Elimina tutti i contenuti e tutte le impostazioni** (solo modalità di supervisione)
- **Configura le restrizioni nel dispositivo** (solo modalità di supervisione)
- **Usa l'associazione di host per controllare i dispositivi a cui può essere associato un dispositivo iOS** (solo modalità di supervisione)
- **Installa i profili di configurazione e i certificati** (solo modalità di supervisione)
- **Modifica del nome dispositivo** (solo modalità di supervisione)
- **Modifica del passcode** (solo modalità di supervisione)
- **Associazione di Apple Watch** (solo modalità di supervisione)
- **Modifica delle impostazioni di notifica** (solo modalità di supervisione)
- **Modifica dello sfondo** (solo modalità di supervisione)
- **Modifica delle impostazioni di invio dei dati di diagnostica** (solo modalità di supervisione)
- **Modifica Bluetooth** (solo modalità di supervisione)
- **AirDrop** (solo modalità di supervisione)
- **Usa Siri per eseguire query nel contenuto generato dall'utente da Internet** (solo modalità di supervisione)
- **Filtro di Siri per le espressioni volgari** (solo modalità di supervisione)
- **Restituisci risultati da Internet nella ricerca Spotlight** (solo modalità di supervisione)
- **Ricerca della definizione della parola** (solo modalità di supervisione)
- **Tastiere predittive** (solo modalità di supervisione)
- **Correzione automatica** (solo modalità di supervisione)
- **Controllo ortografico tastiera** (solo modalità di supervisione)
- **Scelte rapide da tastiera** (solo modalità di supervisione)
  <!--- - **Enterprise app trust settings modification** --->
- **Installazione di app solo con Apple Configurator e iTunes** (solo modalità di supervisione)
- **Download automatici delle app** (solo modalità di supervisione)
- **Modifica le impostazioni dell'app Find My Friends** (solo modalità di supervisione)
- **Accesso a iBooks Store** (solo modalità di supervisione)
- **App Messages** (solo modalità di supervisione)
- **Podcast** (solo modalità di supervisione)
- **Apple Music** (solo modalità di supervisione)
- **iTunes Radio** (solo modalità di supervisione)
- **Apple News** (solo modalità di supervisione)
- **Game Center** (solo modalità di supervisione)
- **Considera AirDrop come destinazione non gestita**

## <a name="android-for-work-support"></a>Supporto per Android for Work

A partire dalla versione 1702 di Technical Preview, è possibile associare un account Google al tenant di MDM ibrida. Ciò consente di eseguire le operazioni seguenti:

- Registrare i [dispositivi Android supportati](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) come Android for Work, creando profili di lavoro in tali dispositivi registrati
- Approvare le applicazioni nello store di Play for Work, sincronizzarle con la console di Configuration Manager e quindi distribuirle ai profili di lavoro dei dispositivi
- Creare e distribuire gli elementi di configurazione per configurare le impostazioni del profilo di lavoro e della password per i dispositivi
- Creare e distribuire elementi dei criteri di conformità e profili di accesso alle risorse per i dispositivi Android for Work come già accade per i dispositivi Android
- Eseguire la cancellazione selettiva nei dispositivi Android for Work

Quando si registra un dispositivo come Android for work, viene creato un profilo di lavoro nel dispositivo gestibile da Intune. Questo profilo di lavoro coesiste con il profilo personale nel dispositivo Android. Gli utenti possono passare facilmente dalle app profilo di lavoro alle app profilo personale. Non è possibile gestire gli elementi nel profilo personale. Le app e i dati personali rimangono non gestiti. Configuration Manager ha il controllo completo sul profilo di lavoro e i relativi contenuti e può rimuoverlo dal dispositivo.

Android for Work è una piattaforma separata da Android, e sarà necessario decidere quale tipo di gestione usare per i dispositivi Android che supportano i profili di lavoro.

### <a name="try-it-out"></a>Verifica
Le sezioni seguenti descrivono la gestione di Android for Work.

#### <a name="enable-android-for-work-management"></a>Abilitare la gestione di Android for Work
1. Creare un account Google all'indirizzo https://accounts.google.com/SignUp da usare come account amministratore di Android for Work, che verrà associato a tutte le attività di gestione di Android for Work per il tenant di Intune. Potrebbe trattarsi di un account di Google condiviso tra gli amministratori che gestiscono i dispositivi Android. Si tratta dell'account Google usato dall'organizzazione per gestire e pubblicare applicazioni nella console di Play for Work. Questo account verrà usato per approvare le applicazioni nello store di Play for Work, quindi è consigliabile appuntarsi nome dell'account e password.
2. Abilitare la registrazione di Android associando l'account Google al tenant di Intune gestito in Configuration Manager:
   1. Accedere ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune** e selezionare la propria sottoscrizione Intune.
   2. Nella barra multifunzione fare clic su **Configura piattaforme** > **Android** e assicurarsi che l'opzione **Abilita registrazione Android** sia selezionata.
   3. Nella barra multifunzione fare clic su **Configura piattaforme** > **Android for Work**.
   4. Nella finestra di dialogo fare clic su **Configura Android for Work nella console di Intune**. La console di Intune viene aperta nel Web browser.
   5. Usare le credenziali di amministratore di Intune per accedere al portale di Intune.
   6. Fare clic su **Configura** per aprire il sito Web Android for Work di Google Play.
   7. Nella pagina di accesso di Google immettere le credenziali Google dal passaggio 1 e quindi specificare le informazioni aziendali.
3. Quando si torna al portale di Intune, Android for Work è attivato e sono disponibili tre opzioni di registrazione per i dispositivi Android for Work:
   - **Gestisci tutti i dispositivi come Android**: (disabilitata) tutti i dispositivi Android, inclusi i dispositivi Android for Work, verranno registrati come dispositivi Android convenzionali
   - **Gestisci i dispositivi supportati come Android for Work**: (abilitata) tutti i dispositivi che supportano Android for Work vengano registrati come dispositivi Android for Work. Tutti i dispositivi che non supportano Android for Work vengono registrati come dispositivi Android convenzionali.
   - **Gestisci i dispositivi supportati per gli utenti solo in questi gruppi come Android for Work**: (test) consente di usare la gestione Android for Work per un insieme di utenti limitato. Solo i membri dei gruppi selezionati che registrano un dispositivo che supporta Android for Work vengono registrati come dispositivi Android for Work. Tutti gli altri vengono registrati come dispositivi Android.
  
> [!NOTE]
> Un problema noto impedisce all'opzione **Gestisci i dispositivi supportati per gli utenti solo in questi gruppi come Android for Work** di funzionare come previsto. I dispositivi degli utenti nei gruppi Azure AD specificati saranno registrati come Android anziché Android for Work. Per testare Android for Work, è necessario usare **Gestisci i dispositivi supportati come Android for Work**.


  Per consentire la registrazione Android for Work è necessario selezionare una delle ultime due opzioni. L'opzione **Gestisci i dispositivi supportati per gli utenti solo in questi gruppi come Android for Work** richiede che siano prima impostati i gruppi di sicurezza di Azure Active Directory.

Quando l'associazione sarà stata completata, il nome dell'account e il nome dell'organizzazione saranno visualizzati nel portale di Intune. A quel punto sarà possibile chiudere entrambi i browser.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Approvare e distribuire le applicazioni Android for Work
Attenersi alla procedura seguente per approvare le applicazioni nello store di Play for Work, sincronizzarle con la console di Configuration Manager e quindi distribuirle ai dispositivi Android for Work gestiti. Per distribuire applicazioni a profili di lavoro degli utenti, è necessario approvarle in Play for Work e quindi sincronizzarle con la console di Configuration Manager.

1. Aprire un browser e andare a: https://play.google.com/work.
2. Accedere usando l'account di amministratore di Google associato al tenant di Intune.
3. Cercare le applicazioni che si vuole distribuire nell'ambiente e fare clic su **Approva** per ognuna di esse.
4. Nella console di Configuration Manager passare a **Amministratore** > **Panoramica** > **Servizi cloud** > **Android for Work** e fare clic su **Sincronizza**.
5. Attendere fino a 10 minuti che le applicazioni si sincronizzino e passare a **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Informazioni di licenza per le app dello Store**.
6. Fare clic su un'app sincronizzata da Play for Work e quindi su **Crea applicazione**.
7. Completare la procedura guidata e fare clic su **Chiudi**.
8. Passare a **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Applicazioni**, selezionare un'applicazione Android for Work e distribuire come di consueto.

Per eseguire la sincronizzazione delle applicazioni Play for Work con Configuration Manager, è necessario approvare almeno un'applicazione sul sito Web Play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Registrare un dispositivo Android for Work
La procedura di registrazione dei dispositivi Android for Work è simile alla registrazione per Android. Scaricare ed eseguire l'app portale aziendale per Android nel dispositivo mobile. Verrà richiesto di creare un profilo di lavoro come parte del processo di registrazione.  Dopo aver creato il profilo di lavoro, è necessario passare alla versione gestita del portale aziendale. Il portale aziendale gestito viene contrassegnato con una valigetta arancione nell'angolo in basso a destra.

#### <a name="create-and-deploy-a-configuration-item"></a>Creare e distribuire un elemento di configurazione
Android for Work ha due gruppi di impostazioni per gli elementi di configurazione:
- Password
- Profilo di lavoro

È possibile configurare la condivisione dei contenuti tra i profili di lavoro, nonché gli elementi di configurazione seguenti nei dispositivi che eseguono Android 6 o versione successiva:
- Il comportamento delle applicazioni che richiedono autorizzazioni specifiche
- La possibilità di visualizzare le notifiche delle applicazioni all'interno del profilo di lavoro nella schermata di blocco

Per eseguire una prova, creare un elemento di configurazione mediante il flusso di lavoro standard, scegliere **Android for Work** nella pagina **Generale** e configurare le impostazioni per ognuno dei gruppi di impostazioni, aggiungendo l'elemento di configurazione a una linea di base ed eseguendo la distribuzione come di consueto. Queste impostazioni verranno applicate solo ai dispositivi registrati come Android for Work e non a quelli registrati come Android.

#### <a name="perform-selective-wipe"></a>Eseguire la cancellazione selettiva
I dispositivi registrati come Android for Work possono essere cancellati solo in modo selettivo in quanto l'utente gestisce solo il profilo di lavoro. Ciò impedisce che venga cancellato il profilo personale. Quando si eseguire la cancellazione selettiva in un dispositivo Android for Work, viene rimosso il profilo di lavoro, compresi tutte le app e i dati, e la registrazione del dispositivo viene annullata.

Per eseguire la cancellazione selettiva in un dispositivo Android for Work, usare il [processo di cancellazione selettiva](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) consueto nella console di Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problemi noti di Android for Work
**Se si configura la sincronizzazione pianificata nei profili di posta elettronica di Android for Work, la distribuzione non riesce** Una delle opzioni dell'interfaccia utente di ConfigMgr per i profili di posta elettronica di Android for Work è quella relativa alla pianificazione. In altre piattaforme questa consente all'amministratore di configurare una pianificazione per la sincronizzazione della posta elettronica e degli altri dati dell'account di posta elettronica fino ai dispositivi mobili in cui viene distribuito. Per i profili di posta elettronica di Android for Work non funziona, e se si sceglie un'opzione diversa da "Non configurato" il profilo non verrà distribuito in nessun dispositivo.
