---
title: Configurare Asset Intelligence
titleSuffix: Configuration Manager
description: Configurare Asset Intelligence in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1a5c89d3fdd82bfa654f806c6931bde2621e714b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906604"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Configurare Asset Intelligence in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Asset Intelligence consente di eseguire l'inventario e gestire l'uso delle licenze software.   

## <a name="steps-to-configure-asset-intelligence"></a>Passaggi per la configurazione di Asset Intelligence  
   

- **Passaggio 1**: per raccogliere i dati di inventario necessari per i report di Asset Intelligence, è necessario abilitare Hardware Inventory Client Agent come descritto in [Come estendere l'inventario hardware](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Passaggio 2**: [Abilitare le classi di report per l'inventario hardware di Asset Intelligence](#BKMK_EnableAssetIntelligence).  
- **Passaggio 3**: [Installare un punto di sincronizzazione di Asset Intelligence](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Passaggio 4**: [Abilitare il controllo degli eventi di accesso con esito positivo](#BKMK_EnableSuccessLogonEvents)  
- **Passaggio 5**: [Importare le informazioni sulle licenze software](#BKMK_ImportSoftwareLicenseInformation)  
- **Passaggio 6**: [Configurare le attività di manutenzione di Asset Intelligence](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Per abilitare Asset Intelligence nei siti di Configuration Manager, è necessario abilitare una o più classi di report per l'inventario hardware di Asset Intelligence. È possibile abilitare le classi nella home page di **Asset Intelligence** o nell'area di lavoro **Amministrazione** , nel nodo **Impostazioni client** , nelle proprietà delle impostazioni client. Utilizzare una delle seguenti procedure.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Per abilitare le classi di report per l'inventario hardware di Asset Intelligence dalla home page di Asset Intelligence  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Asset Intelligence**.  

3.  Nel gruppo **Asset Intelligence** della scheda **Home** scegliere **Modifica classi di inventario**.   

4.  Per abilitare i report di Asset Intelligence, selezionare **Abilita tutte le classi di report di Asset Intelligence** oppure **Abilita solo le classi di report di Asset Intelligence selezionate** e selezionare almeno una classe di report tra quelle visualizzate.  

    > [!NOTE]  
    >  I report di Asset Intelligence che dipendono dalle classi di inventario hardware abilitate con questa procedura non visualizzano dati fino a quando i client non eseguono un'analisi dell'hardware e restituiscono l'inventario hardware.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Per abilitare le classi di report per l'inventario hardware di Asset Intelligence dalle proprietà delle impostazioni client  

1.  Nella console di Configuration Manager scegliere **Amministrazione** >  **Impostazioni client** > **Impostazioni agente client predefinite**. Se sono state create impostazioni client personalizzate, è possibile selezionarle in alternativa.  

3.  Nel gruppo **Proprietà** della scheda **Home** scegliere **Proprietà**.   

4.  Scegliere **Inventario hardware** > **Imposta classi**. .  

5.  Scegliere **Filtra per categoria** > **Classi di report di Asset Intelligence**. L'elenco delle classi viene aggiornato in modo da includere solo le classi di report per l'inventario hardware di Asset Intelligence.  

6.  Selezionare almeno una classe di report dall'elenco.  

    > [!NOTE]  
    >  I report di Asset Intelligence che dipendono dalle classi di inventario hardware abilitate con questa procedura non visualizzano dati fino a quando i client non eseguono un'analisi dell'hardware e restituiscono l'inventario hardware.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

Il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence viene usato per connettere i siti di Configuration Manager a System Center Online per la sincronizzazione delle informazioni del catalogo di Asset Intelligence. Il punto di sincronizzazione di Asset Intelligence può essere installato solo in un sistema del sito nel sito principale della gerarchia di Configuration Manager e richiede l'accesso a Internet per la sincronizzazione con System Center Online tramite la porta TCP 443.

Oltre al download di nuove informazioni per il catalogo di Asset Intelligence, il punto di sincronizzazione di Asset Intelligence consente di caricare le informazioni sui titoli software personalizzati in System Center Online per la categorizzazione. Microsoft considera informazioni pubbliche tutti i titoli software caricati. Accertarsi che i titoli software personalizzati non contengano informazioni riservate o proprietarie. Per altre informazioni su come richiedere la categorizzazione dei titoli software, vedere [Richiedere un aggiornamento del catalogo per i titoli software senza categoria](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Per installare un ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence  

1.  Nella console di Configuration Manager selezionare **Amministrazione**> **Configurazione del sito** > **Server e ruoli di sistema del sito**.  

3.  Aggiungere il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence a un server del sistema del sito nuovo o esistente:  

    -  Per un **nuovo server di sistema del sito**: Nel gruppo **Crea** della scheda **Home** selezionare **Crea server di sistema sito** per avviare la procedura guidata.   

        > [!NOTE]  
        >  Per impostazione predefinita, quando Configuration Manager installa un ruolo del sistema del sito, i file di installazione vengono installati nella prima unità disco rigido NTFS con la maggiore quantità di spazio su disco disponibile. Per evitare l'installazione di Configuration Manager in unità specifiche, creare un file vuoto denominato No_sms_on_drive.sms e copiarlo nella cartella radice dell'unità prima dell'installazione del server del sistema del sito.  

    -  Per un **server di sistema del sito esistente**: scegliere il server in cui si vuole installare il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence. Quando si sceglie un server, nel riquadro dei dettagli viene visualizzato un elenco dei ruoli del sistema del sito già installati nel server.  

         Nel gruppo **Server** della scheda **Home** scegliere **Aggiungi ruoli del sistema del sito** per avviare la procedura guidata.  

4.  Completare la pagina **Generale**. Quando si aggiunge il punto di sincronizzazione di Asset Intelligence a un server del sistema del sito esistente, verificare i valori configurati in precedenza.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di sincronizzazione di Asset Intelligence** nell'elenco dei ruoli disponibili.  

6.  Nella pagina **Impostazioni di connessione del punto di sincronizzazione di Asset Intelligence** scegliere **Avanti**.  

     Per impostazione predefinita, l'impostazione **Utilizza questo punto di sincronizzazione di Asset Intelligence** è selezionata e non può essere configurata in questa pagina. System Center Online accetta il traffico di rete solo sulla porta TCP 443, pertanto l'impostazione **Numero porta SSL** non può essere configurata in questa pagina della procedura guidata.  

7.  Facoltativamente, è possibile specificare un percorso per il file del certificato di autenticazione (con estensione pfx) di System Center Online. In genere, non si specifica un percorso per il certificato perché il provisioning del certificato di connessione viene eseguito automaticamente durante l'installazione del ruolo del sito.  

8.  Nella pagina **Impostazioni server proxy** specificare se il punto di sincronizzazione di Asset Intelligence userà un server proxy per la connessione a System Center Online per sincronizzare il catalogo e se usare credenziali per connettersi al server proxy.  

    > [!WARNING]  
    >  Se è necessario un server proxy per connettersi a System Center Online, il certificato di connessione potrebbe anche essere eliminato se scade la password dell'account utente configurato per l'autenticazione del server proxy.  

9. Nella pagina **Pianificazione della sincronizzazione** specificare se si vuole usare una pianificazione per sincronizzare il catalogo di Asset Intelligence. Quando si abilita la pianificazione della sincronizzazione, è necessario specificare una pianificazione della sincronizzazione semplice o personalizzata. Durante la sincronizzazione pianificata, il punto di sincronizzazione di Asset Intelligence si connette a System Center Online per recuperare il catalogo di Asset Intelligence più recente. È possibile sincronizzare manualmente il catalogo di Asset Intelligence dal nodo di Asset Intelligence nella console di Configuration Manager. Per istruzioni per la sincronizzazione manuale del catalogo di Asset Intelligence, vedere la sezione [Per sincronizzare manualmente il catalogo di Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) in [Operazioni per Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Completare la procedura guidata 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Quattro report di Asset Intelligence visualizzano informazioni raccolte dai registri eventi di sicurezza di Windows nei computer client. Ecco come configurare le impostazioni di accesso dei criteri di sicurezza del computer per abilitare il controllo degli eventi di accesso con esito positivo.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Per abilitare la registrazione degli eventi di accesso con esito positivo tramite criteri di sicurezza locali  

1.  In un computer client di Configuration Manager scegliere **Start** > **Strumenti di amministrazione** > **Criteri di sicurezza locali**.  

2.  Nella finestra di dialogo **Criteri di sicurezza locali**, in **Impostazioni sicurezza**, espandere **Criteri locali** e quindi scegliere **Criteri controllo**.  

3.  Nel riquadro dei risultati fare doppio clic su **Controlla eventi di accesso**, verificare che la casella di controllo **Operazione riuscita** sia selezionata e quindi scegliere **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Per abilitare la registrazione degli eventi di accesso con esito positivo tramite i criteri di sicurezza del dominio di Active Directory  

1.  In un computer controller di dominio scegliere **Start**, scegliere **Strumenti di amministrazione** e quindi **Criterio di protezione del dominio**.  

2.  Nella finestra di dialogo **Criteri di sicurezza locali**, in **Impostazioni sicurezza**, espandere **Criteri locali** e quindi scegliere **Criteri controllo**.  

3.  Nel riquadro dei risultati fare doppio clic su **Controlla eventi di accesso**, verificare che la casella di controllo **Operazione riuscita** sia selezionata e quindi scegliere **OK**.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 Le sezioni seguenti descrivono le procedure necessarie per importare le informazioni sulle licenze software in generale e quelle Microsoft nel database del sito di Configuration Manager usando Importazione guidata licenze software. Quando si importano informazioni sulle licenze software nel database del sito dai file di resoconto delle licenze, per l'account computer del server del sito sono necessarie le autorizzazioni **Controllo completo** per il file system NTFS per la condivisione file usata per importare le informazioni sulle licenze software.  

> [!IMPORTANT]  
>  Quando le informazioni sulle licenze software vengono importate nel database del sito, le informazioni esistenti vengono sovrascritte. Assicurarsi che il file di informazioni sulle licenze software usato con l'Importazione guidata licenze software contenga un elenco completo di tutte le informazioni sulle licenze software necessarie.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Per importare le informazioni sulle licenze software nel catalogo di Asset Intelligence  

1.  Nell'area di lavoro **Asset e conformità** scegliere **Asset Intelligence**.  

2.  Nel gruppo **Asset Intelligence** della scheda **Home** scegliere **Importa licenze software**.   

4.  Nella pagina **Importa** specificare se si intende importare un file di Microsoft Volume Licensing (MVLS) (con estensione xml o csv) o un file di resoconto delle licenze generale (con estensione csv). Per altre informazioni sulla creazione di un file di resoconto delle licenze generale, vedere [Creare un file di resoconto delle licenze generale per l'importazione](#BKMK_CreateGeneralLicenseStatement) più avanti in questo argomento.  

    > [!WARNING]  
    >  Per scaricare un file MVLS in formato CSV che è possibile importare nel catalogo di Asset Intelligence, vedere [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Per accedere a queste informazioni, è necessario disporre di un account registrato nel sito Web. È necessario contattare il rappresentante Microsoft per informazioni su come ottenere il file MVLS in formato XML.  

5.  Immettere il percorso UNC del file di resoconto delle licenze oppure scegliere **Sfoglia** per selezionare una cartella di rete condivisa e un file.  

    > [!NOTE]  
    >  La cartella condivisa deve essere protetta adeguatamente per evitare accessi non autorizzati al file di informazioni sulle licenze e l'account computer del computer in cui è in esecuzione la procedura guidata deve disporre delle autorizzazioni di controllo completo per la condivisione contenente il file di importazione delle licenze.  

6. Completare la procedura guidata.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Creare un file di resoconto delle licenze generale per l'importazione  
 È anche possibile importare un resoconto delle licenze generale nel catalogo di Asset Intelligence tramite un file di importazione delle licenze creato manualmente in formato delimitato da virgole (con estensione csv).  

> [!NOTE]  
>  Anche se solo i campi **Name**, **Publisher**, **Version**ed **EffectiveQuantity** devono contenere dati, nella prima riga del file di importazione delle licenze è necessario immettere tutti i campi. Tutti i campi di data devono essere visualizzati nel formato seguente: Giorno/Mese/Anno, ad esempio 04/08/2008.  

Asset Intelligence abbina i prodotti specificati nel resoconto delle licenze generale in base al nome e alla versione del prodotto, ma non in base al nome dell'editore. Nel resoconto delle licenze generale è necessario usare un nome di prodotto esattamente uguale al nome del prodotto archiviato nel database del sito. Asset Intelligence usa il numero **EffectiveQuantity** specificato nel resoconto delle licenze generale e confronta questo valore con il numero di prodotti installati nell'inventario di Configuration Manager.  

> [!TIP]  
>  Per ottenere un elenco completo dei nomi di prodotto archiviati nel database del sito di Configuration Manager, è possibile eseguire la query seguente nel database del sito: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 È possibile specificare le versioni esatte per un prodotto o una parte della versione, ad esempio solo la versione principale. Gli esempi seguenti indicano le corrispondenze di versione risultanti per una voce di versione nel resoconto delle licenze generale per un prodotto specifico.  

|Voce resoconto licenze generale|Voci corrispondenti database del sito|  
|-------------------------------------|------------------------------------|  
|Nome: "MySoftware", ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Nome: "MySoftware", Version "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Nome: "Mysoftware", Version "2"<br /><br /> Nome: "Mysoftware", Version "2.05"|Errore durante l'importazione. L'importazione non riesce quando più voci corrispondono alla stessa versione del prodotto.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Per creare un file di importazione del resoconto delle licenze generale tramite Microsoft Excel  

1.  Aprire Microsoft Excel e creare un nuovo foglio di calcolo.  

2.  Nella prima riga del nuovo foglio di calcolo immettere tutti nomi dei campi di dati delle licenze software.  

3.  Nella seconda riga e in quelle successive del nuovo foglio di calcolo immettere le informazioni sulle licenze software richieste. Assicurarsi di immettere almeno tutti i campi dei dati delle licenze software obbligatori nelle righe successive per ogni licenza software da importare. Il nome del titolo software immesso nel foglio di calcolo deve essere uguale a quello visualizzato in Esplora inventario risorse per un computer client dopo l'esecuzione dell'inventario hardware.  

4.  Salvare il file in formato csv.  

5.  Copiare il file con estensione csv nella condivisione file usata per importare le informazioni sulle licenze software nel catalogo di Asset Intelligence.  

6.  Nella console di Configuration Manager usare l'Importazione guidata licenze software per importare il file csv appena creato.  

7.  Eseguire il report **Licenza 15A - Report di riconciliazione licenza generale** per verificare che le informazioni sulle licenze siano state importate correttamente nel catalogo di Asset Intelligence.  

> [!NOTE]  
>  Per un esempio di un file di licenza software generale che è possibile usare a scopo di test, vedere [File generale di importazione delle licenze di Asset Intelligence di esempio](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabella di esempio per descrivere le licenze software  
 Quando si crea un file di importazione del resoconto delle licenze generale, è possibile usare le informazioni nella tabella seguente per descrivere le licenze software da importare nel catalogo di Asset Intelligence.  

|Nome della colonna|Tipo di dati|Richiesto|Esempio|  
|-----------------|---------------|--------------|-------------|  
|Name|Fino a 255 caratteri|Sì|Titolo software|  
|Publisher|Fino a 255 caratteri|Sì|Autore del software|  
|Version|Fino a 255 caratteri|Sì|Versione del titolo software|  
|Language|Fino a 255 caratteri|Sì|Lingua del titolo software|  
|EffectiveQuantity|Valore intero|Sì|Numero di licenze acquistate|  
|NumeroOA|Fino a 255 caratteri|No|Informazioni sull'ordine di acquisto|  
|ResellerName|Fino a 255 caratteri|No|Informazioni sul rivenditore|  
|DateOfPurchase|Valore di data nel formato seguente: GG/MM/AAAA|No|Data di acquisto della licenza|  
|SupportPurchased|Valore bit|No|0 o 1: immettere 0 per Sì o 1 per No|  
|SupportExpirationDate|Valore di data nel formato seguente: GG/MM/AAAA|No|Data di fine del supporto acquistato|  
|Comments|Fino a 255 caratteri|No|Commenti facoltativi|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Per Asset Intelligence sono disponibili le attività di manutenzione seguenti:  

-   **Verifica titolo applicazione con le informazioni di inventario**: controlla che il titolo software riportato nell'inventario software coincida con il titolo software nel catalogo di Asset Intelligence. Per impostazione predefinita, questa attività è abilitata e pianificata per l'esecuzione sabato tra le 00.00 e le 5.00. Questa attività di manutenzione è disponibile solo nel sito principale nella gerarchia di Configuration Manager.  

-   **Riepiloga dati software installato**: offre le informazioni visualizzate nell'area di lavoro **Asset e conformità** nel nodo **Software di inventario** sotto il nodo **Asset Intelligence**. All'esecuzione dell'attività, Configuration Manager raccoglie un conteggio di tutti i titoli software di inventario nel sito primario. Per impostazione predefinita, questa attività è abilitata e pianificata per l'esecuzione giornaliera tra le 00.00 e le 5.00. Questa attività di manutenzione è disponibile solo nei siti primari.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Per configurare le attività di manutenzione di Asset Intelligence  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** > **Siti**.  

3.  Selezionare il sito in cui si vuole configurare l'attività di manutenzione di Asset Intelligence.  

4.  Nel gruppo **Impostazioni** della scheda **Home** scegliere **Manutenzione sito**. Selezionare un'attività e scegliere **Modifica** per modificare le impostazioni. 

    È consigliabile impostare il periodo di tempo su orari non di punta per il sito. Il periodo di tempo è l'intervallo di tempo in cui è possibile eseguire l'attività. È definito dagli orari specificati in **Avvia dopo** e **Ultima ora di avvio** nella finestra di dialogo **Attività Proprietà** .  

    È possibile avviare immediatamente l'attività selezionando il giorno corrente e impostando **Avvia dopo** su un orario di un paio di minuti successivo all'ora corrente.  

7.  Scegliere **OK** per salvare le impostazioni. L'attività viene ora eseguita in base alla pianificazione.  

    > [!NOTE]  
    >  Se l'esecuzione dell'attività non riesce al primo tentativo, Configuration Manager esegue altri tentativi fino a quando l'attività non viene eseguita correttamente o fino alla scadenza del periodo di tempo impostato per l'esecuzione dell'attività.  
