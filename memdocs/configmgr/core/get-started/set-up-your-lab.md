---
title: Configurare un ambiente lab
titleSuffix: Configuration Manager
description: Configurare un ambiente lab per la valutazione di Configuration Manager tramite la simulazione di attività reali.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 216c61a671d7d06e434fa399bb3bae12e12f7275
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905172"
---
# <a name="set-up-a-configuration-manager-lab"></a>Configurare un lab di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le linee guida disponibili in questo argomento consentono di configurare un ambiente lab per la valutazione di Configuration Manager tramite la simulazione di attività reali.  

> [!NOTE]
> Microsoft offre una versione preconfigurata di questo lab con una versione di valutazione di Configuration Manager. Per altre informazioni, vedere [Lab Kit di distribuzione di Windows e Office](https://docs.microsoft.com/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab). 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Componenti di base  
 L'impostazione dell'ambiente per Configuration Manager richiede alcuni componenti di base per supportare l'installazione di Configuration Manager.    

-   **L'ambiente lab usa Windows Server 2012 R2**, in cui verrà installato Configuration Manager.  

     È possibile scaricare una versione di valutazione di Windows Server 2012 R2 da [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     È consigliabile modificare o disabilitare Sicurezza avanzata in Internet Explorer per semplificare l'accesso ad alcuni download a cui viene fatto riferimento durante questi esercizi. Per altre informazioni, vedere [Internet Explorer: Protezione avanzata di Internet Explorer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).  

-   **Nell'ambiente lab viene usato SQL Server 2012 SP2** per il database del sito.  

     È possibile scaricare una versione di valutazione di SQL Server 2012 dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=43340).  

     SQL Server ha requisiti in merito alle [versioni supportate di SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) che devono essere soddisfatti per l'uso con Configuration Manager.  

    -   Configuration Manager richiede una versione a 64 bit di SQL Server per ospitare il database del sito.  

    -   **SQL_Latin1_General_CP1_CI_AS** come classe **SQL Collation** .  

    -   **autenticazione di Windows**, [invece dell'autenticazione SQL](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode?view=sql-server-ver15).  

    -   È richiesta un'**istanza di SQL Server** dedicata.  

    -   Non limitare la **memoria indirizzabile di sistema** per SQL Server.  

    -   Configurare l'**account del servizio SQL Server** affinché venga eseguito usando un account utente di dominio con diritti limitati.  

    -   È necessario installare **SQL Server Reporting Services**.  

    -   **comunicazioni tra siti** usano SQL Server Service Broker sulla porta TCP predefinita 4022.  

    -   Le **comunicazioni all'interno del sito** tra il motore di database di SQL Server e i ruoli di sistema del sito di Configuration Manager specifici usano la porta TCP predefinita 1433.  

-   **Il controller di dominio usa Windows Server 2008 R2** con Active Directory Domain Services. Il controller di dominio funge anche da host per i server DHCP e DNS per l'uso con un nome di dominio completo.  

     Per altre informazioni, vedere [Panoramica di Active Directory Domain Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11)).  

-   **Hyper-V viene usato con alcune macchine virtuali** per verificare che le fasi di gestione in questi esercizi funzionino come previsto. È consigliabile avere a disposizione un minimo di tre macchine virtuali con installato Windows 10.  

     Per altre informazioni, vedere [Panoramica di Hyper-V](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).  

-   **Le autorizzazioni di amministratore** saranno necessarie per tutti questi componenti.  

    -   Configuration Manager richiede un amministratore con autorizzazioni locali nell'ambiente Windows Server  

    -   Active Directory richiede un amministratore con autorizzazioni per modificare lo schema  

    -   Le macchine virtuali richiedono autorizzazioni locali nelle macchine stesse  

Sebbene non sia necessario per questa esercitazione, è possibile vedere [Configurazioni supportate per Configuration Manager](../../core/plan-design/configs/supported-configurations.md) per altre informazioni sui requisiti per l'implementazione di Configuration Manager. Vedere la documentazione per le versioni di software diverse da quelle riportate di seguito.  

Dopo aver installato tutti questi componenti, sono necessari passaggi aggiuntivi da eseguire per configurare l'ambiente di Windows per Configuration Manager:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Preparare il contenuto di Active Directory per l'ambiente lab  
 Per questo ambiente lab verrà creato un gruppo di sicurezza e quindi vi verrà aggiunto un utente di dominio.  

-   Gruppo di sicurezza: **Evaluation**  

    -   Ambito gruppo: **Universal**  

    -   Tipo gruppo: **Security**  

-   Utente di dominio: **ConfigUser**  

     In circostanze normali, non viene concesso l'accesso universale a tutti gli utenti all'interno dell'ambiente. Questa operazione viene eseguita con questo utente per semplificare l'attivazione dell'ambiente lab.  

Nelle procedure successive sono elencati gli altri passaggi necessari per consentire ai client di Configuration Manager di eseguire query su Active Directory Domain Services per individuare le risorse del sito.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Creare il contenitore System Management  
 Configuration Manager non crea automaticamente il contenitore System Management necessario in Active Directory Domain Services quando viene esteso lo schema. Pertanto, sarà necessario crearlo per l'ambiente lab. Questo passaggio è richiesto per [installare ADSI Edit](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10)).

 Assicurarsi di avere eseguito l'accesso con un account che disponga dell'autorizzazione **Crea tutti gli oggetti figlio** nel contenitore **System** in Servizi di dominio Active Directory.  

#### <a name="to-create-the-system-management-container"></a>Per creare il contenitore System Management:  

1.  Eseguire **ADSI Edit**e connettersi al dominio in cui risiede il server del sito.  

2.  Espandere **Dominio&lt;nome di dominio completo del computer\>** , espandere **<nome distinto\>** , fare clic con il tasto destro del mouse su **CN=System**, fare clic su **Nuovo** e quindi su **Oggetto**.  

3.  Nella finestra di dialogo **Crea oggetto** , selezionare **Contenitore**, quindi fare clic su **Avanti**.  

4.  Nella casella **Valore** digitare **System Management**e quindi fare clic su **Avanti**.  

5.  Fare clic su **Fine** per completare la procedura.  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Impostare le autorizzazioni di sicurezza per il contenitore System Management  
 Concedere all'account computer del server del sito le autorizzazioni necessarie per pubblicare le informazioni del sito nel contenitore. Anche per questa attività verrà usato ADSI Edit.  

> [!IMPORTANT]  
>  Verificare di essere connessi al dominio del server del sito prima di iniziare la procedura seguente.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Per impostare le autorizzazioni di sicurezza per il contenitore System Management:  

1.  Nel riquadro della console espandere il **dominio del server del sito**, espandere **DC=&lt;<nome distinto del server\>** e quindi espandere **CN=System**. Fare clic con il pulsante destro del mouse su **CN = System Management**, quindi su **Proprietà**.  

2.  Nella finestra di dialogo **CN=System Management Proprietà** fare clic sulla scheda **Sicurezza** e quindi su **Aggiungi** per aggiungere l'account computer del server del sito. Concedere all'account le autorizzazioni **Controllo completo** .  

3.  Fare clic su **Avanzate**, selezionare l'account computer del server del sito e fare clic su **Modifica**.  

4.  Nell'elenco **Applica a** , selezionare **Questo oggetto e tutti i discendenti**.  

5.  Fare clic su **OK** per chiudere la console di **ADSI Edit** e completare la procedura.  

     Per altre informazioni, vedere [Estendere lo schema di Active Directory per Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Estendere lo schema di Active Directory usando extadsch.exe  
 Per questo ambiente lab verrà esteso lo schema di Active Directory in quanto ciò consente di usare tutte le caratteristiche e le funzionalità di Configuration Manager con il minimo carico amministrativo. L'estensione dello schema di Active Directory è una configurazione a livello di foresta eseguita solo una volta per foresta. L'estensione dello schema in modo permanente modifica il set di classi e attributi nella configurazione di Active Directory di base. Questa azione è irreversibile. L'estensione dello schema consente a Configuration Manager di accedere ai componenti che ne consentono un funzionamento efficiente all'interno dell'ambiente lab.  

> [!IMPORTANT]  
>  Assicurarsi di avere eseguito l'accesso al controllo di dominio master dello schema con un account membro del gruppo di sicurezza **Schema Admins** . Il tentativo di usare credenziali alternative avrà esito negativo.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Per estendere lo schema di Active Directory usando extadsch.exe:  

1.  Creare un backup dello stato del sistema del controller di dominio master dello schema. Per altre informazioni sul backup dei controller di dominio master, vedere [Windows Server Backup](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11))  

2.  Passare a **\SMSSETUP\BIN\X64** nel supporto di installazione.  

3.  Eseguire **extadsch.exe**.  

4.  Verificare l'esito positivo dell'estensione dello schema esaminando il file **extadsch.log** disponibile nella radice dell'unità di sistema.  

     Per altre informazioni, vedere [Estendere lo schema di Active Directory per Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Altre attività necessarie  
 È inoltre necessario completare le attività seguenti prima dell'installazione.  

 **Creare una cartella per archiviare tutti i download**  

 Per i componenti del supporto di installazione saranno necessari vari download in questa esercitazione. Prima di iniziare qualsiasi procedura di installazione, determinare una posizione che non richieda lo spostamento di questi file fino a quando non si vuole rimuovere l'ambiente lab. Per archiviare questi download è consigliabile una singola cartella con sottocartelle distinte.  

 **Installare .NET e attivare Windows Communication Foundation**  

 È necessario installare due versioni di .NET Framework, ovvero .NET 3.5.1 e quindi .NET 4.5.2+. È anche necessario attivare Windows Communication Foundation (WCF). WCF è progettato per offrire un approccio gestibile all'elaborazione distribuita, elevati livelli d interoperabilità e supporto diretto per l'orientamento dei servizi. Semplifica inoltre lo sviluppo di applicazioni connesse tramite un modello di programmazione orientato ai servizi. Per altre informazioni, vedere [Informazioni su Windows Communication Foundation](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90)).

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Per installare .NET e attivare Windows Communication Foundation:  

1.  Aprire **Server Manager**e quindi passare a **Gestisci**. Fare clic su **Aggiungi ruoli e funzionalità** per aprire l' **Aggiungi ruoli e funzionalità Wizard**.  

2.  Verificare le informazioni nel pannello **Prima di iniziare** e quindi fare clic su **Avanti**.  

3.  Selezionare **Installazione basata su ruoli o basata su funzionalità**e quindi fare clic su **Avanti**.  

4.  Selezionare il server dal **pool di server**e quindi fare clic su **Avanti**.  

5.  Esaminare il pannello **Ruoli server** e quindi fare clic su **Avanti**.  

6.  Aggiungere le **Funzionalità** seguenti selezionandole nell'elenco:  

    -   **Funzionalità di .NET Framework 3.5**  

        -   **.NET Framework 3.5 (include .NET 2.0 e 3.0)**  

    -   **Funzionalità di .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **Servizi WCF**  

            -   **Attivazione HTTP**  

            -   **Condivisione delle porte TCP**  

7.  Esaminare il **ruolo Server Web (IIS)** e la schermata **Servizi ruolo** e quindi fare clic su **Avanti**.  

8.  Esaminare la schermata **Conferma** e quindi fare clic su **Avanti**.  

9. Fare clic su **Installa** e verificare che l'installazione sia stata completata correttamente nel riquadro **Notifiche** di **Server Manager**.  

10. Al termine dell'installazione di base di .NET, passare all' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=42643) per ottenere il programma di installazione Web per .NET Framework 4.5.2. Fare clic sul pulsante **Scarica** e quindi **eseguire** il programma di installazione. Verranno automaticamente rilevati e installati i componenti necessari nella lingua selezionata.  

**Abilitare BITS, IIS e RDC**  

Il [Servizio trasferimento intelligente in background (BITS)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) viene usato per le applicazioni che devono trasferire file in modo asincrono tra un client e un server. Tramite il controllo del flusso dei trasferimenti in primo piano e in background, BITS consente di mantenere la velocità di risposta delle altre applicazioni di rete. Riprenderà anche automaticamente i trasferimenti di file se una sessione di trasferimento viene interrotta.  

Sarà necessario installare BITS per questo ambiente lab perché il server del sito verrà usato anche come punto di gestione.  

Internet Information Services (IIS) è un server Web flessibile e scalabile che può essere usato per ospitare qualsiasi elemento sul Web. Viene usato da Configuration Manager per alcuni ruoli del sistema del sito. Per altre informazioni su IIS, vedere [Siti Web per i server del sistema del sito](../../core/plan-design/network/websites-for-site-system-servers.md).  

[Compressione differenziale remota (RDC)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) è un set di API utilizzabili dalle applicazioni per determinare se sono state apportate modifiche a un set di file. RDC consente all'applicazione di replicare solo le parti modificate di un file, riducendo al minimo il traffico di rete.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Per abilitare i ruoli del server del sito BITS, IIS e RDC:  

1.  Nel server del sito aprire **Server Manager**. Passare a **Gestisci**. Fare clic su **Aggiungi ruoli e funzionalità** per aprire l' **Aggiunta guidata ruoli e funzionalità**.  

2.  Verificare le informazioni nel pannello **Prima di iniziare** e quindi fare clic su **Avanti**.  

3.  Selezionare **Installazione basata su ruoli o basata su funzionalità**e quindi fare clic su **Avanti**.  

4.  Selezionare il server dal **pool di server**e quindi fare clic su **Avanti**.  

5.  Aggiungere i **ruoli server** seguenti selezionandoli nell'elenco:  

    -   **Server Web (IIS)**  

        -   **Funzionalità HTTP comuni**  

            -   **Documento predefinito**  

            -   **Esplorazione directory**  

            -   **Errori HTTP**  

            -   **Contenuto statico**  

            -   **Reindirizzamento HTTP**  

        -   **Integrità e diagnostica**  

            -   **Registrazione HTTP**  

            -   **Strumenti di registrazione**  

            -   **Monitoraggio richieste**  

            -   **Traccia**  

    -   **Prestazioni**  

        -   **Compressione contenuto statico**  

        -   **Compressione contenuto dinamico**  

    -   **Security**  

        -   **Filtro richieste**  

        -   **Autenticazione base**  

        -   **Autenticazione mapping certificati client**  

        -   **Restrizioni per IP e domini**  

        -   **Autorizzazione URL**  

        -   **Autenticazione di Windows**  

    -   **Sviluppo applicazioni**  

        -   **Estendibilità .NET 3.5**  

        -   **Estendibilità .NET 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **Estensioni ISAPI**  

        -   **Filtri ISAPI**  

        -   **Server Side Includes**  

    -   **Server FTP**  

        -   **Servizio FTP**  

    -   **Strumenti di gestione**  

        -   **Console di gestione IIS**  

        -   **Compatibilità Gestione IIS 6**  

            -   **Compatibilità Metabase IIS 6**  

            -   **Console di gestione IIS 6**  

            -   **Strumenti di scripting di IIS 6**  

            -   **Compatibilità WMI IIS 6**  

        -   **Strumenti e script di gestione IIS 6**  

        -   **Servizio di gestione**  

6.  Aggiungere le **Funzionalità** seguenti selezionandole nell'elenco:  

    -   **Servizio trasferimento intelligente in background (BITS)**  

          -   **Estensione del server IIS**  

    -   **Strumenti di amministrazione remota del server**  

          -   **Strumenti di amministrazione funzionalità**  

          -   **Strumenti per Estensioni server BITS**  

7.  Fare clic su **Installa** e verificare che l'installazione sia stata completata correttamente nel riquadro **Notifiche** di **Server Manager**.  

Per impostazione predefinita IIS impedisce l'accesso a diversi tipi di estensioni e percorsi di file tramite comunicazione HTTP o HTTPS. Per abilitare la distribuzione di questi file a sistemi client, sarà necessario configurare il filtro richieste per IIS nel punto di distribuzione. Per altre informazioni, vedere [Filtro richieste IIS per punti di distribuzione](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Per configurare il filtro per IIS nei punti di distribuzione:  

1.  Aprire **IIS Manager** e selezionare il nome del server nella barra laterale. Verrà visualizzata la schermata **Home** .  

2.  Verificare che l'opzione **Visualizzazione funzionalità** sia selezionata nella parte inferiore della schermata **Home** . Passare a **IIS** e aprire **Filtro richieste**.  

3.  Nel riquadro **Azioni** fare clic su **Consenti estensione di file**.  

4.  Digitare **.msi** nella finestra di dialogo e quindi fare clic su **OK**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Installazione di Configuration Manager  
Verrà seguita la procedura illustrata in [Determine when to use a primary site](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) (Stabilire quando usare un sito primario) per gestire direttamente i client. In questo modo l'ambiente lab potrà supportare la gestione della [scalabilità del sistema del sito](../plan-design/configs/size-and-scale-numbers.md) dei dispositivi potenziali.  
Durante questo processo verrà installata anche la console di Configuration Manager, che da questo momento in poi verrà usata per gestire i dispositivi in valutazione.  

Prima di iniziare l'installazione, avviare il [controllo dei prerequisiti](../servers/deploy/install/prerequisite-checker.md) nel server usando Windows Server 2012 per confermare che tutte le impostazioni siano state abilitate correttamente.  

#### <a name="to-download-and-install-configuration-manager"></a>Per scaricare e installare Configuration Manager:  

1.  Passare alla pagina [System Center Valutazioni](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) per scaricare l'ultima versione di valutazione di Configuration Manager.  

2.  Decomprimere il supporto di download nel percorso predefinito.  

3.  Seguire la procedura di installazione descritta in [Installare un sito usando la configurazione guidata di Configuration Manager](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md). In questa procedura è necessario immettere quanto segue:  

    |Passaggio nella procedura di installazione del sito|Selezione|  
    |-----------------------------------------|---------------|  
    |Passaggio 4: Pagina **Codice Product Key**|Selezionare **Valutazione**.|  
    |Passaggio 7:  **Download prerequisiti**|Selezionare **Scarica file richiesti** e specificare il percorso predefinito.|  
    |Passaggio 10: **Impostazioni di installazione e del sito**|-   **Codice sito:LAB**<br />-   **Nome sito:Evaluation**<br />-   **Cartella di installazione:** specificare il percorso predefinito.|  
    |Passaggio 11: **Installazione del sito primario**|Selezionare **Installa il sito primario come sito autonomo**e quindi fare clic su **Avanti**.|  
    |Passaggio 12: **Installazione del database**|-   **Nome server SQL (FQDN):** immettere qui il nome FQDN.<br />-   **Nome istanza:** lasciare vuoto questo campo perché verrà usata l'istanza predefinita di SQL installata in precedenza.<br />-   **Porta Service Broker:** lasciare la porta predefinita impostata su 4022.|  
    |Passaggio 13: **Installazione del database**|Lasciare le impostazioni predefinite.|  
    |Passaggio 14: **Provider SMS**|Lasciare le impostazioni predefinite.|  
    |Passaggio 15: **Impostazioni di comunicazione client**|Verificare che l'opzione **Tutti i ruoli del sistema del sito accettano solo le comunicazioni HTTPS dai client** non sia selezionata|  
    |Passaggio 16: **Ruoli del sistema del sito**|Immettere il nome FQDN e verificare che l'opzione **Tutti i ruoli del sistema del sito accettano solo le comunicazioni HTTPS dai client** sia deselezionata.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a> Attivare la pubblicazione per il sito di Configuration Manager  
Ogni sito di Configuration Manager pubblica informazioni specifiche nel contenitore System Management all'interno della relativa partizione di dominio nello schema di Active Directory. I canali bidirezionali per la comunicazione tra Active Directory e Configuration Manager devono essere aperti per gestire il traffico. Si abiliterà inoltre l'individuazione della foresta per determinare alcuni componenti di Active Directory e dell'infrastruttura di rete.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Per configurare le foreste Active Directory per la pubblicazione:  

1.  Nell'angolo in basso a sinistra della console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione della gerarchia**e quindi fare clic su **Metodi di individuazione**.  

3.  Selezionare **Individuazione foresta Active Directory** e fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** selezionare **Abilita individuazione foresta Active Directory**. Dopo aver attivato l'individuazione, selezionare **Crea automaticamente i limiti dei siti di Active Directory quando vengono individuati**. Verrà visualizzata una finestra di dialogo contenente il messaggio seguente: **Eseguire l'individuazione completa appena possibile?** Fare clic su **Sì**.  

5.  Nello gruppo **Metodo di individuazione** nella parte superiore della schermata fare clic su **Esegui individuazione foresta**e quindi passare a **Foreste Active Directory** nella barra laterale. La foresta Active Directory deve essere visualizzata nell'elenco delle foreste individuate.  

6.  Passare alla scheda **Generale** nella parte superiore della schermata.  

7.  Nell'area di lavoro **Amministrazione** espandere **Configurazione della gerarchia**e quindi fare clic su **Foreste Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Per abilitare la pubblicazione delle informazioni di un sito di Configuration Manager nella foresta Active Directory:  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Verrà configurata una nuova foresta non ancora rilevata.  

3.  Nell'area di lavoro **Amministrazione** , fare clic su **Foreste Active Directory**.  

4.  Nella scheda **Pubblicazione** all'interno delle proprietà del sito selezionare la foresta connessa e quindi fare clic su **OK** per salvare la configurazione.
