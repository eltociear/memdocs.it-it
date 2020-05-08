---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1705 per Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3259bd1b20740046e70b1ef53281b0ff235a3896
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905473"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1705 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1705. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    

**Problemi noti di questa versione Technical Preview:**
-   **Il connettore della suite Operations Manager Suite non viene aggiornato**. Quando si esegue l'aggiornamento da una versione Technical Preview precedente nella quale era configurato il connettore OMS, tale connettore non viene aggiornato e non è più disponibile nella console. Dopo l'aggiornamento, è necessario [usare la Procedura guidata per i servizi di Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) e ristabilire la connessione all'area di lavoro OMS.
-   **La sincronizzazione dei driver di Microsoft Surface non riesce**. Anche se il supporto per i driver di Microsoft Surface è indicato in **Novità** nella console di Configuration Manager della Technical Preview, questa funzionalità non funziona ancora come previsto.
-   **Impossibile creare i criteri di rinvio di Windows Update for Business** Anche se la possibilità di configurare i criteri di rinvio di Windows Update for Business è indicata in **Novità** nella console di Configuration Manager per la Technical Preview, la procedura guidata non si apre e non è possibile configurare alcun criterio.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Strumento di reimpostazione dell'aggiornamento  
È possibile usare lo Strumento di reimpostazione dell'aggiornamento **CMUpdateReset.exe** per risolvere i problemi quando gli aggiornamenti nella console mostrano problemi di download o replica. Questo strumento è incluso nella versione Technical Preview 1705. È reperibile nel server del sito della Technical Preview dopo aver installato l'anteprima nella cartella ***\cd.latest\SMSSETUP\TOOLS***.

È possibile usare questo strumento con le versioni Technical Preview 1606 o successive. Poiché include il supporto per le versioni precedenti, lo strumento può essere usato con numerosi scenari di aggiornamento per Technical Preview, senza dover attendere la disponibilità della versione Technical Preview successiva.

È possibile usare questo strumento quando un aggiornamento nella console non è ancora installato e il relativo stato è Non riuscito. Uno stato Non riuscito può indicare che il download dell'aggiornamento è ancora in corso ma risulta bloccato e sta impiegando troppo tempo, ad esempio molte ore in più rispetto alle previsioni cronologiche per i pacchetti di aggiornamento di dimensioni simili. Può anche trattarsi di un errore nella replica dell'aggiornamento nei siti primari figlio.  

Lo strumento viene eseguito nell'aggiornamento specificato. Per impostazione predefinita, lo strumento non elimina gli aggiornamenti scaricati o installati correttamente.  

### <a name="prerequisites"></a>Prerequisiti
L'account usato per eseguire lo strumento richiede le autorizzazioni seguenti:
-   **Lettura** e **Scrittura** per il database del sito del sito di amministrazione centrale e per ogni sito primario della gerarchia. Per impostare queste autorizzazioni, aggiungere l'account utente come membro dei [ruoli predefiniti del database ](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** e **db_datareader** nel database di Configuration Manager di ogni sito. Lo strumento non interagisce con i siti secondari.
-   **Amministratore locale** nel sito di livello superiore della gerarchia.
-   **Amministratore locale** nel computer che ospita il punto di connessione del servizio.

È necessario il GUID del pacchetto di aggiornamento da reimpostare. Per ottenere il GUID:
-   Nella console passare a **Amministrazione** > **Aggiornamenti e manutenzione** e quindi nel riquadro informazioni fare clic con il pulsante destro del mouse sull'intestazione di una delle colonne, ad esempio **Stato**, quindi selezionare **GUID pacchetto**. La colonna viene aggiunta alla visualizzazione e mostra il GUID del pacchetto di aggiornamento.

> [!TIP]  
> Per copiare il GUID, selezionare la riga del pacchetto di aggiornamento da ripristinare e quindi copiarla premendo CTRL+C. Copiando la selezione in un editor di testo, è possibile copiare solo il GUID per usarlo come parametro della riga di comando quando si esegue lo strumento.

### <a name="run-the-tool"></a>Eseguire lo strumento    
Lo strumento deve essere eseguito nel sito di livello superiore della gerarchia.

Quando si esegue lo strumento, usare i parametri della riga di comando per specificare l'istanza di SQL Server del sito di livello superiore della gerarchia, il nome del database del sito e il GUID del pacchetto di aggiornamento da reimpostare. Lo strumento identifica quindi i server aggiuntivi a cui deve accedere, in base allo stato degli aggiornamenti.   

Se il pacchetto di aggiornamento è nella fase *successiva al download*, lo strumento non esegue la pulizia del pacchetto. In alternativa, è possibile forzare la rimozione di un aggiornamento scaricato correttamente tramite il parametro per l'eliminazione forzata. I parametri della riga di comando vengono descritti più avanti in questo argomento.

Dopo l'esecuzione dello strumento:
-   Se è stato eliminato un pacchetto, riavviare il servizio SMS_Executive dei siti di livello superiore e quindi cercare gli aggiornamenti per scaricare nuovamente il pacchetto.
-   Se il pacchetto non è stato eliminato non è necessaria alcuna azione, poiché l'aggiornamento reinizializza e riavvia la replica o l'installazione.

**Parametri della riga di comando:**  


|                        Parametro                         |                                                            Descrizione                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN dell'istanza di SQL Server del sito di livello superiore>** | *Richiesto* <br> Specificare il FQDN dell'istanza di SQL Server che ospita il database del sito per il sito di livello superiore della gerarchia. |
|                **-D &lt;Nome database>**                 |                             *Richiesto* <br> Specificare il nome del database dei siti di livello superiore.                             |
|                 **-P &lt;GUID pacchetto>**                 |                        *Richiesto* <br> Specificare il GUID del pacchetto di aggiornamento da reimpostare.                        |
|           **-I &lt;Nome istanza SQL Server>**           |                   *Facoltativo* <br> Identifica l'istanza di SQL Server che ospita il database del sito.                   |
|                       **-FDELETE**                       |                      *Facoltativo* <br> Consente di forzare l'eliminazione di un pacchetto di aggiornamento scaricato correttamente.                      |

 **Esempi:**  
 In uno scenario tipico, si vuole reimpostare un aggiornamento che presenta problemi di download. L'FQDN di SQL Server è *server1.fabrikam.com*, il database del sito è *CM_XYZ* e il GUID del pacchetto è *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Eseguire: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 In uno scenario più complesso, si vuole forzare l'eliminazione del pacchetto di aggiornamento che crea problemi. L'FQDN di SQL Server è *server1.fabrikam.com*, il database del sito è *CM_XYZ* e il GUID del pacchetto è *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Eseguire: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Provare lo strumento con la Technical Preview  
È possibile usare questo strumento con le versioni Technical Preview 1606 o successive. Poiché include il supporto per le versioni precedenti, lo strumento può essere usato con numerosi scenari di aggiornamento per Technical Preview, senza dover attendere la disponibilità della versione Technical Preview successiva.

Eseguire lo strumento in un pacchetto di aggiornamento di una versione Technical Preview prima che l'aggiornamento completi il controllo dei prerequisiti. Il completamento del controllo dei prerequisiti è indicato da uno degli stati seguenti del pacchetto in **Amministrazione** > **Aggiornamenti e manutenzione**:  
-   **Controllo prerequisiti superato**
-   **Controllo prerequisiti superato con avviso**
-   **Controllo prerequisiti non riuscito**


## <a name="high-dpi-console-support"></a>Supporto per console con DPI elevato

In questa versione sono state risolte le problematiche legate a come la console di Configuration Manager ridimensiona e visualizza diverse parti dell'interfaccia utente su dispositivi con DPI elevato, ad esempio un Surface Book.


## <a name="peer-cache-improvements"></a>Miglioramenti della peer cache
A partire da questa Technical Preview, Peer Cache [non usa l'account di accesso alla rete](../plan-design/hierarchy/client-peer-cache.md) per autenticare le richieste di download dai peer.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Miglioramenti per i gruppi di disponibilità Always On di SQL Server  
Con questa versione è ora possibile usare le repliche con commit asincrono nei gruppi di disponibilità Always On di SQL Server usati con Configuration Manager.  Ciò significa che è possibile aggiungere repliche aggiuntive ai gruppi di disponibilità da usare come backup remoti, e quindi usarli in caso di ripristino di emergenza.  

- Configuration Manager supporta l'uso della replica con commit asincrono per ripristinare la replica sincrona.  Vedere le [opzioni di ripristino del database del sito](../servers/manage/recover-sites.md#site-database-recovery-options) nell'argomento Backup e ripristino per informazioni su come eseguire questa operazione.

- Questa versione non supporta il failover per l'uso della replica con commit asincrono come database del sito.
  > [!CAUTION]  
  > Poiché Configuration Manager non convalida lo stato della replica con commit asincrono per verificare che sia corrente, e [per comportamento normale del prodotto, una replica di questo tipo può non essere sincronizzata](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2014#AvailabilityModes), l'uso di una replica con commit asincrono come database del sito può mettere a rischio l'integrità dei dati del sito.  

- In un gruppo di disponibilità è possibile usare lo stesso numero e tipo di repliche supportate dalla versione di SQL Server in uso.   In precedenza, il supporto era limitato a due repliche con commit sincrono.

### <a name="configure-an-asynchronous-commit-replica"></a>Configurare una replica con commit asincrono
Per aggiungere una replica asincrona a un [gruppo di disponibilità usato con Configuration Manager](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md), non è necessaria eseguire gli script di configurazione necessari per configurare una replica sincrona, perché non viene offerto supporto per l'uso di tale replica asincrona come database del sito. Per altre informazioni, vedere [Aggiungere una replica secondaria a un gruppo di disponibilità](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server?view=sql-server-2014).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Usare la replica asincrona per il ripristino del sito
Prima di usare una replica asincrona per ripristinare il database del sito, è necessario arrestare il sito primario attivo per evitare altre operazioni di scrittura nel database del sito. Dopo aver arrestato il sito, è possibile usare una replica asincrona al posto di un [database ripristinato manualmente](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).

Per arrestare il sito, è possibile usare lo[Strumento di manutenzione gerarchia](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) per interrompere i servizi principali nel server del sito. Usare la riga di comando: **Preinst.exe /stopsite**   

Arrestare il sito equivale ad arrestare il servizio Gestione componenti del sito (sitecomp) e poi il servizio SMS_Executive service, nel server del sito.


## <a name="improved-user-notifications-for-office-365-updates"></a>Notifiche utente migliorate per gli aggiornamenti di Office 365
Sono stati apportati miglioramenti per usare l'esperienza utente a portata di clic di Office quando un client installa un aggiornamento di Office 365. I miglioramenti includono le notifiche a comparsa e in-app e un conto alla rovescia. In precedenza, quando un aggiornamento di Office 365 veniva inviato a un client, le applicazioni di Office aperte venivano chiuse automaticamente senza preavviso. Dopo l'aggiornamento, le applicazioni di Office non verranno chiuse in modo imprevisto.

### <a name="prerequisites"></a>Prerequisiti
Questo aggiornamento si applica ai client di Office 365 ProPlus.

### <a name="known-issues"></a>Problemi noti
Quando un client valuta l'assegnazione di un aggiornamento di Office 365 per la prima volta e l'aggiornamento ha una scadenza pianificata nel passato, pianificata immediatamente o pianificata entro 30 minuti, l'esperienza utente di Office 365 può risultare incoerente. Il client potrebbe ad esempio visualizzare una finestra di dialogo con un conto alla rovescia di 30 minuti per l'aggiornamento, ma l'imposizione effettiva potrebbe avviarsi prima della fine del conto alla rovescia. Per evitare questo comportamento, considerare quanto segue:
- Distribuire l'aggiornamento di Office 365 con una scadenza pianificata dopo più di 60 minuti rispetto all'ora corrente.
- Configurare una finestra di manutenzione durante le ore non lavorative per la raccolta o un periodo di tolleranza per l'imposizione della distribuzione.

### <a name="try-it-out"></a>Verifica
Provare a completare le attività seguenti e quindi inviare **Feedback** dalla scheda **Home** della barra multifunzione per comunicarci come è andata:
- Distribuire l'aggiornamento di Office 365 a un client con una scadenza impostata dopo almeno 60 minuti rispetto all'ora corrente. Osservare il nuovo comportamento nel client.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurare e distribuire i criteri di Windows Defender Application Guard

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) è una nuova funzionalità di Windows che consente di proteggere gli utenti con l'apertura di siti Web non attendibili in un contenitore protetto isolato non è accessibile da altre parti del sistema operativo. In questa versione Technical Preview, è stato aggiunto il supporto per configurare questa funzionalità usando le impostazioni di conformità di Configuration Manager configurate dall'utente e quindi distribuite in una raccolta.
Questa funzionalità verrà rilasciata in anteprima per la versione a 64 bit di Windows 10 Creators Update. Per provare ora questa funzionalità è necessario usare una versione di anteprima dell'aggiornamento.


### <a name="before-you-start"></a>Prima di iniziare

Per creare e distribuire i criteri di Windows Defender Application Guard, configurare i dispositivi Windows 10 in cui vengono distribuiti i criteri con un criterio di isolamento rete. Per altre informazioni, vedere il blog di blog indicato più avanti.
Questa funzionalità funziona solo con le build correnti di Windows 10 Insider. Per provarla, i client devono eseguire una build recente di Windows 10 Insider.

### <a name="try-it-out"></a>Verifica

Verificare di avere letto il post di blog per comprendere le nozioni di base relative a Windows Defender Application Guard.

Per creare un criterio e per individuare le impostazioni disponibili:

1.  Nella console di Configuration Manager scegliere **Asset e conformità**.
2.  Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4.  Usando il post di blog come riferimento, è possibile selezionare e configurare le impostazioni disponibili per provare la funzionalità.
5.  Al termine, completare la procedura guidata e distribuire il criterio in uno o più dispositivi Windows 10.

### <a name="further-reading"></a>Letture di approfondimento

Per altre informazioni su Windows Defender Application Guard, vedere [questo post di blog]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Per altre informazioni sulla modalità autonoma di Windows Defender Application Guard vedere [questo post di blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Nuove funzionalità per la gestione di Azure AD e del cloud

In questa versione è possibile configurare i servizi cloud affinché usino Azure AD a supporto dello scenario seguente:

- Installare manualmente il client di Configuration Manager da Internet e assegnarlo a un sito di Configuration Manager.
- Usare Intune per distribuire il client di Configuration Manager ai dispositivi via Internet.

### <a name="advantages"></a>Vantaggi

L'utilizzo dei servizi cloud e di Azure AD evita l'impiego dei certificati di autenticazione client.

È possibile individuare gli utenti di Azure AD che possono quindi essere usati nelle raccolte e in altre operazioni di Configuration Manager.

### <a name="before-you-start"></a>Prima di iniziare

- È necessario disporre di un tenant di Azure AD.
- I dispositivi devono eseguire Windows 10 ed essere aggiunti ad Azure AD.  Oltre che ad Azure AD, i client possono essere anche aggiunti al dominio.
- Oltre ai [prerequisiti esistenti](../plan-design/configs/site-and-site-system-prerequisites.md) per il ruolo del sistema del sito del punto di gestione, è anche necessario verificare che **ASP.NET 4.5** e qualsiasi altra opzione selezionata automaticamente insieme a questa siano abilitate nel computer che ospita questo ruolo del sistema del sito.
- Per usare Microsoft Intune per distribuire il client di Configuration Manager:
    - È necessario disporre di un tenant di Intune funzionante. Non è necessario che Configuration Manager e Intune siano connessi.
    - In Intune, è stata creata e distribuita un'app che contiene il client di Configuration Manager. Per altre informazioni, vedere Come installare i client nei dispositivi Windows gestiti da MDM di Intune.
- Per usare Configuration Manager per distribuire il client:
    - Almeno un punto di gestione deve essere configurato per la modalità HTTPS.
    - Configurare un gateway di gestione cloud.


### <a name="set-up-the-cloud-management-gateway"></a>Configurare il gateway di gestione cloud

Configurare il gateway di gestione cloud per consentire ai client di accedere al sito di Configuration Manager da Internet senza certificati.

Per informazioni su come eseguire questa operazione, leggere gli argomenti seguenti:

- [Pianificare il gateway di gestione cloud in Configuration Manager](../clients/manage/cmg/plan-cloud-management-gateway.md).
- [Configurare il gateway di gestione cloud per Configuration Manager](../clients/manage/cmg/setup-cloud-management-gateway.md).
- [Monitorare il gateway di gestione cloud in Configuration Manager](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurare l'applicazione Servizi di Azure in Servizi cloud di Configuration Manager

In questo modo il sito di Configuration Manager viene connesso ad Azure AD; si tratta di un prerequisito per tutte le altre operazioni di questa sezione. Per eseguire questa operazione:

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Servizi di Azure**.
2. Nella scheda **Home**, nel gruppo **Servizi di Azure**, fare clic su **Configura i servizi di Azure**.
3. Nella pagina **Servizi di Azure** della procedura guidata per i servizi di Azure, selezionare **Gestione cloud** per consentire ai client di autenticarsi nella gerarchia usando Azure AD.
4. Nella pagina **Generale** della procedura guidata specificare un nome e una descrizione per il servizio di Azure.
5. Nella pagina **App** della procedura guidata selezionare l'ambiente di Azure dall'elenco, quindi fare clic su **Sfoglia** per selezionare le applicazioni server e client da usare per configurare il servizio di Azure:
   - Nella finestra **Server App** (App server) selezionare l'app server che si vuole usare e quindi fare clic su **OK**. Le app server sono app Web di Azure che contengono le configurazioni per l'account Azure, inclusi ID del tenant, ID client e una chiave privata per i client. Se non è disponibile un'app server, usare una delle opzioni seguenti:
       - **Crea**: per creare una nuova app server, fare clic su **Crea**. Specificare un nome descrittivo per l'app e il tenant. Quindi, dopo avere effettuato l'accesso ad Azure, Configuration Manager crea l'app Web in Azure, inclusi l'ID Client e la chiave privata da usare con l'app Web. In un secondo momento, è possibile visualizzare queste informazioni dal portale di Azure.
       - **Importa**: per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant, quindi specificare ID tenant, ID client e chiave privata per l'app Web di Azure che si vuole rendere disponibile per l'uso con Configuration Manager. Dopo aver verificato le informazioni, fare clic su **OK** per continuare. Questa opzione non è attualmente disponibile in questa versione Technical Preview.
   - Ripetere la procedura per l'applicazione client.

   È necessario concedere all'applicazione l'autorizzazione *Lettura dati directory* quando si importa l'applicazione, per impostare le autorizzazioni corrette nel portale. Se si usa la creazione dell'applicazione, le autorizzazioni vengono create automaticamente con l'applicazione, ma è necessario concedere il consenso all'applicazione nel portale di Azure.
6. Nella pagina **Individuazione** della procedura guidata, selezionare **Abilita l'individuazione utente di Azure Active Directory** e quindi fare clic su **Impostazioni**.
   Nella finestra di dialogo **Impostazioni di individuazione utenti di Azure AD** configurare una pianificazione per quando si verifica l'individuazione. È anche possibile abilitare l'individuazione differenziale che verifica solo gli account nuovi o modificati in Azure AD.
7. Completare la procedura guidata.

A questo punto il sito di Configuration Manager è connesso ad Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Installare il client di Configuration Manager da Internet

Prima di iniziare, verificare che i file di origine dell'installazione client vengano archiviati localmente nel dispositivo nel quale viene installato il client.
Usare le istruzioni in [Come distribuire i client nei computer Windows](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) con la riga di comando per l'installazione seguente, sostituendo con valori personalizzati i valori dell'esempio:

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=\<GUID> AADRESOURCEURI=<https://contososerver>**

- **/NoCrlCheck**: se il punto di gestione o il gateway di gestione cloud usa un certificato server non pubblico, il client potrebbe non raggiungere il percorso CRL.
- **/Source**: Cartella locale:   posizione dei file di installazione del client.
- **CCMHOSTNAME**: nome del punto di gestione Internet. È possibile trovarlo eseguendo **gwmi - namespace root\ccm\locationservices-classe SMS_ActiveMPCandidate** da un prompt dei comandi in un client gestito.
- **SMSMP**: nome del punto di gestione di ricerca. Può trattarsi della rete Intranet.
- **SMSSiteCode**: codice del sito del sito di Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: nome e ID del tenant di Azure AD collegato a Configuration Manager. È possibile trovarlo eseguendo dsregcmd.exe /status da un prompt dei comandi su dispositivo aggiunto ad Azure AD.
- **AADCLIENTAPPID**: ID app client di Azure AD. Per informazioni su come trovarlo, vedere [Usare il portale per creare un'applicazione Azure Active Directory e un'entità servizio che possano accedere alle risorse](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
- **AADResourceUri**: URI di identificazione dell'app server di Azure AD caricata.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Usare la Procedura guidata Servizi di Azure per configurare una connessione a OMS
A partire dalla versione Technical Preview 1705, la **Procedura guidata Servizi di Azure** viene usata per configurare la connessione da Configuration Manager al servizio cloud Operations Management Suite (OMS). La procedura guidata sostituisce i precedenti flussi di lavoro per la configurazione della connessione.

-   Viene usata per configurare i servizi cloud per Configuration Manager, ad esempio OMS, Windows Store per le aziende (WSfB) e Azure Active Directory (Azure AD).  

-   Configuration Manager si connette a OMS per funzionalità quali Log Analytics o Preparazione aggiornamenti.

### <a name="prerequisites-for-the-oms-connector"></a>Prerequisiti per il connettore OMS
I prerequisiti per configurare una connessione a OMS sono identici a quelli [indicati per la versione Current Branch 1702](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Tali informazioni viene ripetute di seguito:  

-   Fornire l'autorizzazione di Configuration Manager a OMS.

-   OMS Connector deve essere installato nel computer che ospita un [punto di connessione del servizio](../servers/deploy/configure/about-the-service-connection-point.md) che si trova in [modalità online](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

-   Nel punto di connessione del servizio, insieme a OMS Connector è necessario installare Microsoft Monitoring Agent per OMS. L'agente e OMS Connector devono essere configurati per l'uso della stessa **area di lavoro OMS**. Per installare l'agente, vedere [Scaricare e installare l'agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) nella documentazione relativa a OMS.
-   Dopo aver installato l'agente e OMS Connector, è necessario configurare OMS per l'uso dei dati di Configuration Manager. A questo scopo, [importare le raccolte di Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections) nel portale di OMS.

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Usare la Procedura guidata Servizi di Azure per configurare la connessione a OMS

1.  Nella console passare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Servizi di Azure** e quindi scegliere **Configura i servizi di Azure** dalla scheda **Home** della barra multifunzione per avviare la **Procedura guidata per i servizi di Azure**.

2.  Nella pagina **Servizi di Azure** selezionare il servizio cloud Operations Management Suite. Specificare un nome descrittivo per **Nome del servizio Azure** e una descrizione facoltativa, quindi fare clic su **Avanti**.

3.  Nella pagina **App** specificare l'ambiente Azure (la versione Technical Preview supporta solo cloud pubblici). Fare clic su **Sfoglia** per aprire la finestra dell'app server.

4.  Selezionare un'app Web:

    -   **Importa**: per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant, quindi specificare ID tenant, ID client e chiave privata per l'app Web di Azure che si vuole rendere disponibile per l'uso con Configuration Manager. Dopo aver fatto clic su **Verifica** per verificare le informazioni, fare clic su **OK** per continuare.   

    > [!NOTE]   
    > Quando si configura OMS con questa versione di anteprima, OMS supporta solo la funzione di *importazione*  di un'app Web. La creazione di una nuova app Web non è supportata. Analogamente, non è possibile usare un'app già esistente per OMS.

5.  Se tutte le altre procedure sono state eseguite correttamente, le informazioni della schermata di **configurazione della connessione OMS** vengono automaticamente visualizzate. Le informazioni relative alle impostazioni di connessione vengono visualizzate in **Sottoscrizione Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.

6.  La procedura guidata esegue la connessione al servizio OMS usando le informazioni immesse dall'utente. Selezionare le raccolte di dispositivi da sincronizzare con OMS e quindi fare clic su **Aggiungi**.

7.  Verificare le impostazioni di connessione nella schermata **Riepilogo** e selezionare **Avanti**. Nella schermata **Avanzamento** viene visualizzato lo stato della connessione e quindi **Completata**.

8.  Al termine della procedura guidata, nella console di Configuration Manager viene indicato che **Operation Management Suite** è stato configurato come **Tipo di servizio cloud**.
