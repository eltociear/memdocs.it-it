---
title: Repliche di database dei punti di gestione
titleSuffix: Configuration Manager
description: Usare una replica di database per ridurre il carico della CPU dovuto ai punti di gestione nel server di database del sito.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e647672b02c0122709b3c80fc012ed1fb82b1519
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696430"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Repliche di database per i punti di gestione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I siti primari di Configuration Manager possono usare una replica di database per ridurre sul server di database del sito il carico della CPU dovuto ai punti di gestione che gestiscono le richieste provenienti dai client.  

-   Quando un punto di gestione usa una replica di database, tale punto di gestione richiede dati dal computer di SQL Server che ospita la replica di database anziché dal server di database del sito.  

-   Questo può ridurre i requisiti di elaborazione della CPU nel server di database del sito grazie all'offload delle attività di elaborazione frequenti correlate ai client.  Un esempio di attività di elaborazione frequenti per i client include i siti in cui sono presenti moltissimi client che richiedono spesso criteri client  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> Predisporre l'uso delle repliche di database  
**Informazioni sulle repliche di database per i punti di gestione:**  

-   Le repliche sono una copia parziale del database del sito che viene replicato in un'istanza separata di SQL Server:  

    -   I siti primari supportano una replica di database dedicata per ogni punto di gestione nel sito (i siti secondari non supportano le repliche di database)  

    -   Una replica di database può essere usata da più punti di gestione dello stesso sito  

    -   SQL Server può ospitare più repliche di database che possono essere usate da più punti di gestione, purché ognuna venga eseguita in un'istanza separata di SQL Server  

-   Le repliche sincronizzano una copia del database del sito in base a una pianificazione fissa dai dati pubblicati appositamente dal server di database del sito.  

-   I punti di gestione possono essere configurati per usare una replica quando si installa il punto di gestione oppure in un secondo momento riconfigurando il punto di gestione installato in precedenza in modo da usare la replica di database  

-   È necessario monitorare regolarmente il server di database del sito e tutti i server di replica di database per garantire la corretta esecuzione della replica, le prestazioni ottimali del server di replica di database per il sito e le prestazioni client necessarie  

**Prerequisiti per le repliche di database:**  

-   **Requisiti di SQL Server:**  

    -   L'istanza di SQL Server che ospita la replica di database deve soddisfare gli stessi requisiti del server di database del sito. Non è invece necessario che la versione o edizione di SQL Server eseguita dal server di replica sia la stessa eseguita del server di database del sito, ma è sufficiente che si tratti di una versione o edizione di SQL Server supportata. Per informazioni, vedere [Supporto per le versioni di SQL Server per Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   Il servizio SQL Server nel computer che ospita il database di replica deve essere eseguito come account di **sistema** .  

    -   Nell'istanza di SQL Server che ospita il database del sito e in quella che ospita la replica di database deve essere installata la **replica di SQL Server** .  

    -   Il database del sito deve **pubblicare** la replica di database e ogni server di replica del database remoto deve **sottoscrivere** i dati pubblicati.  

    -   L'istanza di SQL Server che ospita il database del sito e quella che ospita la replica di database devono essere entrambe configurate per supportare un valore **Max Text Repl Size** di 2 GB. Per un esempio di configurazione di SQL Server 2012, vedere [Configurare l'opzione di configurazione del server max text repl size](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option?view=sql-server-ver15).  

-   **Certificato autofirmato**: per configurare una replica di database, è necessario creare un certificato autofirmato nel server di replica di database e renderlo disponibile per ogni punto di gestione che userà il server di replica di database.  

    -   Il certificato è automaticamente disponibile per un punto di gestione installato nel server di replica di database.  

    -   Per fare in modo che il certificato sia disponibile ai punti di gestione remoti, è necessario esportare il certificato e quindi aggiungerlo all'archivio certificati **Persone attendibili** del punto di gestione remoto.  

-   **Notifica client**: per supportare la notifica client con una replica di database per un punto di gestione, è necessario configurare la comunicazione tra il server di database del sito e il server di replica di database per **SQL Server Service Broker**. A questo scopo è necessario:  

    -   Configurare ogni database con informazioni sull'altro database  

    -   Scambiare certificati tra due database per proteggere le comunicazioni  

**Limitazioni quando si usano le repliche di database:**  

-   Quando il sito è configurato per pubblicare repliche di database, al posto delle normali indicazioni trovano applicazione le procedure seguenti:  

    -   [Disinstallare un server del sito che pubblica una replica di database](#BKMK_DBReplicaOps_Uninstall)  

    -   [Spostare un database del server del sito che pubblica una replica di database](#BKMK_DBReplicaOps_Move)  

-   **Aggiornamenti a Configuration Manager Current Branch**: prima di aggiornare un sito da System Center 2012 Configuration Manager a Configuration Manager Current Branch oppure prima di aggiornare Configuration Manager Current Branch all'ultima versione, è necessario disabilitare le repliche di database per i punti di gestione.  Dopo l'aggiornamento del sito, è possibile riconfigurare le repliche di database per i punti di gestione.  

-   **Più repliche in un'unica istanza di SQL Server**:  se si configura un server di replica di database per ospitare più repliche di database per i punti di gestione (ogni replica deve trovarsi in un'istanza separata), è necessario usare uno script di configurazione modificato (dal passaggio 4 della sezione successiva) per evitare di sovrascrivere il certificato autofirmato usato dalle repliche di database configurate in precedenza in tale server.  

- Le distribuzioni utente in Software Center non funzioneranno con un punto di gestione che usa una replica SQL. <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> Configurare le repliche di database  
La configurazione di una replica di database prevede i passaggi seguenti:  

-   [Passaggio 1: Configurare il server di database del sito per la pubblicazione della replica di database](#BKMK_DBReplica_ConfigSiteDB)  

-   [Passaggio 2: Configurare il server di replica di database](#BKMK_DBReplica_ConfigSrv)  

-   [Passaggio 3: Configurare i punti di gestione per l'uso della replica di database](#BKMK_DBReplica_ConfigMP)  

-   [Passaggio 4: Configurare un certificato autofirmato per il server di replica di database](#BKMK_DBReplica_Cert)  

-   [Passaggio 5: Configurare SQL Server Service Broker per il server di replica di database](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a> Passaggio 1: Configurare il server di database del sito per la pubblicazione della replica di database  
 Usare la seguente procedura come esempio di configurazione del server di database del sito in un computer Windows Server 2008 R2 per la pubblicazione della replica di database. Se si dispone di una versione diversa del sistema operativo, fare riferimento alla documentazione del sistema operativo e modificare di conseguenza i passaggi di questa procedura.  

##### <a name="to-configure-the-site-database-server"></a>Per configurare il server di database del sito  

1.  Nel server di database del sito impostare SQL Server Agent per l'avvio automatico.  

2.  Nel server di database del sito, creare un gruppo di utenti locale con il nome **ConfigMgr_MPReplicaAccess**. È necessario aggiungere l'account computer per ogni server di replica di database usato nel sito a tale gruppo per consentire ai server di replica di database di eseguire la sincronizzazione con la replica di database pubblicata.  

3.  Nel server di database del sito, configurare una condivisione file con il nome **ConfigMgr_MPReplica**.  

4.  Aggiungere le seguenti autorizzazioni per la condivisione **ConfigMgr_MPReplica** :  

    > [!NOTE]  
    >  Se SQL Server Agent usa un account diverso dall'account di sistema locale, sostituire SYSTEM con il nome account presente nel seguente elenco.  

    -   **Autorizzazioni condivisione**:  

        -   SYSTEM: **Scrittura**  

        -   ConfigMgr_MPReplicaAccess: **Lettura**  

    -   **Autorizzazioni NTFS**:  

        -   SYSTEM: **Controllo completo**  

        -   ConfigMgr_MPReplicaAccess: **Lettura**, **Lettura ed esecuzione**, **Elenca contenuti cartella**  

5.  Usare **SQL Server Management Studio** per connettersi al database del sito ed eseguire la seguente stored procedure come una query: **spCreateMPReplicaPublication**  

Al termine della stored procedure, il server di database del sito è configurato per la pubblicazione della replica di database.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Passaggio 2: Configurare il server di replica di database  
Il server di replica di database è un computer che esegue SQL Server e ospita una replica del database del sito che verrà usata dai punti gestione. In base a una pianificazione fissa, il server di replica di database sincronizza la propria copia del database con la replica di database pubblicata dal server di database del sito.  

Il server di replica di database deve soddisfare gli stessi requisiti del server di database del sito. Tuttavia, il server di replica di database può eseguire una versione o un'edizione diversa di SQL Server rispetto a quella usata dal server di database del sito. Per informazioni sulle versioni di SQL Server supportate, vedere l'argomento [Supporto per le versioni di SQL Server per Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!IMPORTANT]  
>  Il servizio SQL Server nel computer che ospita il database di replica deve essere eseguito come account di sistema.  

Usare la seguente procedura come esempio di configurazione di un server di replica di database in un computer Windows Server 2008 R2. Se si dispone di una versione diversa del sistema operativo, fare riferimento alla documentazione del sistema operativo e modificare di conseguenza i passaggi di questa procedura.  

##### <a name="to-configure-the-database-replica-server"></a>Per configurare il server di replica di database  

1. Nel server di replica di database impostare SQL Server Agent per l'avvio automatico.  

2. Nel server di replica di database usare **SQL Server Management Studio** per la connessione al server locale, quindi selezionare la cartella **Replica** , fare clic su Sottoscrizioni locali e selezionare **Nuove sottoscrizioni** per avviare **Creazione guidata nuova sottoscrizione**:  

   1. Nella pagina **Pubblicazione** della casella di riepilogo **Autore** selezionare **Trova server di pubblicazione SQL Server**, immettere il nome del server di database del sito e fare clic su **Connetti**.  

   2. Selezionare **ConfigMgr_MPReplica**, quindi fare clic su **Avanti**.  

   3. Nella pagina **Posizione in cui eseguire l'agente di distribuzione** selezionare **Esegui ogni agente nel relativo Sottoscrittore (sottoscrizioni pull)** , quindi fare clic su **Avanti**.  

   4. Nella pagina **Sottoscrittori** eseguire una delle seguenti operazioni:  

      -   Selezionare un database esistente dal server di replica di database da usare per la replica di database, quindi fare clic su **OK**.  

      -   Selezionare **Nuovo database** per creare un nuovo database per la replica di database. Nella pagina **Nuovo database** specificare un nome di database, quindi fare clic su **OK**.  

   5. Fare clic su **Avanti** per continuare.  

   6. Nella pagina **Protezione agente di distribuzione** fare clic sul pulsante delle proprietà **(.…)** nella riga Connessione al Sottoscrittore della finestra di dialogo, quindi configurare le impostazioni di protezione per la connessione.  

      > [!TIP]  
      >  Il pulsante delle proprietà **(….)** si trova nella quarta colonna della finestra di visualizzazione.  

      **Impostazioni di protezione:**  

      - Configurare l'account che esegue il processo dell'agente di distribuzione (l'account del processo):  

        -   Se SQL Server Agent viene eseguito come sistema locale, selezionare **Esegui con l'account del servizio SQL Server Agent (procedura non consigliata per la protezione)**  

        -   Se SQL Server Agent viene eseguito usando un account diverso, selezionare **Esegui con l'account di Windows seguente**, quindi configurare l'account. È possibile specificare un account Windows o un account SQL Server.  

        > [!IMPORTANT]  
        >  È necessario concedere all'account che esegue l'agente di distribuzione le autorizzazioni per l'autore come una sottoscrizione pull. Per informazioni sulla configurazione di queste autorizzazioni, vedere [Sicurezza agente di distribuzione](/sql/relational-databases/replication/distribution-agent-security?view=sql-server-ver15).  

      - Per **Connetti al server di distribuzione**, selezionare **Tramite rappresentazione dell'account del processo**.  

      - Per **Connetti al Sottoscrittore**, selezionare **Tramite rappresentazione dell'account del processo**.  

        Al termine della configurazione delle impostazioni di protezione per la connessione, fare clic su **OK** per salvarle, quindi fare clic su **Avanti**.  

   7. Nella casella di riepilogo **Pianificazione agente** della pagina **Pianificazione della sincronizzazione** selezionare **Definizione pianificazione**, quindi configurare **Nuova pianificazione processo**. Selezionare la frequenza **Quotidiana**, fare in modo che ricorra ogni **5 minuti**e impostare la durata **Nessuna data di fine**. Fare clic su **Avanti** per salvare la pianificazione, quindi fare clic nuovamente su **Avanti** .  

   8. Nella pagina **Azioni procedura guidata** selezionare la casella di controllo **Crea le sottoscrizioni**, quindi fare clic su **Avanti**.  

   9. Nella pagina **Completamento procedura guidata** fare clic su **Fine**, quindi su **Chiudi** per completare la procedura guidata.  

3. Subito dopo aver completato la Creazione guidata nuova sottoscrizione, usare **SQL Server Management Studio** per connettersi al database del server di replica di database e quindi eseguire la query seguente per attivare la proprietà del database TRUSTWORTHY:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Controllare lo stato di sincronizzazione per verificare che la sottoscrizione sia stata eseguita correttamente:  

   -   Nel computer del sottoscrittore:  

       -   In **SQL Server Management Studio**eseguire la connessione al server di replica di database, quindi espandere **Replica**.  

       -   Espandere **Sottoscrizioni locali**, fare clic con il pulsante destro del mouse sulla sottoscrizione alla pubblicazione del database del sito e quindi selezionare **Visualizza stato sincronizzazione**.  

   -   Nel computer dell'autore:  

       -   In **SQL Server Management Studio**eseguire la connessione al computer del database del sito, fare clic con il pulsante destro del mouse sulla cartella **Replica** , quindi selezionare **Avvia Monitoraggio replica**.  

5. Per abilitare l'integrazione Common Language Runtime (CLR) per la replica di database, usare **SQL Server Management Studio** per connettersi alla replica di database nel server di replica di database ed eseguire la seguente stored procedure come una query: **exec sp_configure 'clr enabled', 1; RICONFIGURARE CON SOSTITUZIONE**  

6. Per ciascun punto di gestione che usa un server di replica di database, aggiungere l'account computer relativo al punto di gestione al gruppo **Administrators** locale nel server di replica di database.  

   > [!TIP]  
   >  Questo passaggio non è necessario per i punti di gestione eseguiti nel server di replica di database.  

   La replica di database ora può essere usata da un punto di gestione.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a> Passaggio 3: Configurare i punti di gestione per l'uso della replica di database  
 È possibile configurare un punto di gestione in un sito primario per l'utilizzo di una replica di database durante l'installazione del ruolo del punto di gestione, oppure è possibile riconfigurare un punto di gestione esistente per l'utilizzo di una replica di database.  

 Per configurare un punto di gestione per l'utilizzo di una replica di database, usare le seguenti informazioni:  

-   **Per configurare un nuovo punto di gestione**: nella pagina **Database del punto di gestione** della procedura guidata utilizzata per l'installazione del punto di gestione selezionare **Utilizza replica di database** e specificare l'FQDN del computer che ospita la replica di database. Successivamente, per **Nome database del sito di Configuration Manager**, specificare il nome del database della replica di database nel computer.  

-   **Per configurare un punto di gestione installato in precedenza**: aprire la pagina delle proprietà del punto di gestione, selezionare la scheda **Database del punto di gestione**, selezionare **Usa replica di database**, quindi specificare l'FQDN del computer che ospita la replica di database. Successivamente, per **Nome database del sito di Configuration Manager**, specificare il nome del database della replica di database nel computer.  

-   **Per ogni punto di gestione che usa una replica di database**è necessario aggiungere manualmente l'account computer del server del punto di gestione al ruolo **db_datareader** per la replica di database.  

Oltre a configurare il punto di gestione per l'utilizzo del server di replica di database, è necessario abilitare **Autenticazione Windows** in **IIS** nel punto di gestione:  

1.  Aprire **Gestione Internet Information Services (IIS)** .  

2.  Selezionare il sito Web usato dal punto di gestione e aprire **Autenticazione**.  

3.  Impostare **Autenticazione Windows** su **Attivato**, quindi chiudere **Gestione Internet Information Services (IIS)** .  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> Passaggio 4: Configurare un certificato autofirmato per il server di replica di database  
 È necessario creare un certificato autofirmato nel server di replica di database e renderlo disponibile per ogni punto di gestione che utilizzerà il server di replica di database.  

 Il certificato è automaticamente disponibile per un punto di gestione installato nel server di replica di database. Tuttavia, per rendere il certificato disponibile ai punti di gestione remoti, è necessario esportare il certificato e quindi aggiungerlo all'archivio certificati Persone attendibili del punto di gestione remoto.  

 Usare le seguenti procedure come esempio di configurazione di un certificato autofirmato nel server di replica di database per un computer Windows Server 2008 R2. Se si dispone di una versione diversa del sistema operativo, fare riferimento alla documentazione del sistema operativo e modificare di conseguenza i passaggi di queste procedure.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Per configurare un certificato autofirmato per il server di replica di database  

1.  Nel server di replica di database aprire un prompt dei comandi di PowerShell con privilegi amministrativi e quindi eseguire il seguente comando: **set-executionpolicy UnRestricted**  

2.  Copiare il seguente script PowerShell e salvarlo come file con il nome **CreateMPReplicaCert.ps1**. Inserire una copia di questo file nella cartella radice della partizione di sistema del server di replica di database.  

    > [!IMPORTANT]  
    >  Se si configurano più repliche di database in un'unica istanza di SQL Server, per ogni replica successiva configurata è necessario usare una versione modificata dello script per questa procedura. Vedere  [Script supplementari per ulteriori repliche di database in un'unica istanza di SQL Server](#bkmk_supscript)  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  Nel server di replica di database eseguire il seguente comando applicabile alla configurazione di SQL Server:  

    -   Per un'istanza predefinita di SQL Server: fare clic con il pulsante destro del mouse sul file **CreateMPReplicaCert.ps1** e selezionare **Esegui con PowerShell**. Durante l'esecuzione dello script viene creato il certificato autofirmato e SQL Server viene configurato per l'utilizzo del certificato.  

    -   Per un'istanza denominata di SQL Server: usare PowerShell per eseguire il comando **%path%\CreateMPReplicaCert.ps1 xxxxxx** dove **xxxxxx** è il nome dell'istanza di SQL Server.  

    -   Dopo aver completato lo script, verificare che SQL Server Agent sia in esecuzione. In caso contrario, riavviare SQL Server Agent.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Per configurare i punti di gestione remoti per usare il certificato autofirmato del server di replica di database  

1.  Eseguire i passaggi seguenti nel server di replica di database per esportare il certificato autofirmato del server:  

    1.  Fare clic su **Start**, quindi su **Esegui**e digitare **mmc.exe**. Nella console vuota fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

    2.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

    3.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

    4.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi fare clic su **Fine**.  

    5.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

    6.  Nella console espandere **Certificati (computer locale)** , espandere **Personale**e selezionare **Certificati**.  

    7.  Fare clic con il pulsante destro del mouse sul certificato con il nome descrittivo **Certificato di identificazione di SQL Server di Configuration Manager**, fare clic su **Tutte le attività**e quindi selezionare **Esporta**.  

    8.  Completare l' **Esportazione guidata certificati** usando le opzioni predefinite e salvare il certificato con l'estensione del nome file **.cer** .  

2.  Eseguire i seguenti passaggi nel computer del punto di gestione per aggiungere il certificato autofirmato per il server di replica di database all'archivio certificati Persone attendibili nel punto di gestione:  

    1.  Ripetere i passaggi precedenti da 1.a a 1.e per configurare la console MMC dello snap-in dei **certificati** nel computer del punto di gestione.  

    2.  Nella console espandere **Certificati (computer locale)** , quindi **Persone attendibili**, fare clic con il pulsante destro del mouse su **Certificati**, selezionare **Tutte le attività**e infine **Importa** per avviare l' **Importazione guidata certificati**.  

    3.  Nella pagina **File da importare** selezionare il certificato salvato nel passaggio 1.h, quindi fare clic su **Avanti**.  

    4.  Nella pagina **Archivio certificati** selezionare **Mettere tutti i certificati nel seguente archivio**con l'opzione **Archivio certificati** impostata su **Persone attendibili**, quindi fare clic su **Avanti**.  

    5.  Fare clic su **Fine** per chiudere la procedura guidata e completare la configurazione dei certificati nel punto di gestione.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> Passaggio 5: Configurare SQL Server Service Broker per il server di replica di database  
Per supportare la notifica client con una replica di database per un punto di gestione, è necessario configurare la comunicazione tra il server di database del sito e il server di replica di database per SQL Server Service Broker. A tale scopo, è necessario configurare ogni database con le informazioni sull'altro database e scambiare i certificati tra i due database per una comunicazione protetta.  

> [!NOTE]  
>  Prima di usare la seguente procedura, è necessario che il server di replica di database completi la sincronizzazione iniziale con il server di database del sito.  

 La seguente procedura non modifica la porta Service Broker configurata in SQL Server per il server di database del sito o il server di replica di database. Al contrario, consente di configurare ogni database in modo che comunichi con l'altro database usando la porta Service Broker corretta.  

 Usare la seguente procedura per configurare Service Broker per il server di database del sito e il server di replica di database.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Per configurare Service Broker per una replica di database  

1. Usare **SQL Server Management Studio** per connettersi al database del server di replica di database, quindi eseguire la query seguente per abilitare Service Broker nel server di replica di database: **ALTER DATABASE &lt;Nome database di replica\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2. Successivamente, nel server di replica di database, configurare Service Broker per la notifica client ed esportare il certificato di Service Broker. A tale scopo, eseguire una stored procedure di SQL Server che consente di configurare Service Broker ed esportare il certificato come una singola azione. Quando si esegue la stored procedure, è necessario specificare l'FQDN del server di replica di database, il nome del database delle repliche di database e specificare un percorso per l'esportazione del file di certificato.  

    Eseguire la query seguente per configurare i dettagli necessari nel server di replica di database e per esportare il certificato per il server di replica di database: **EXEC sp_BgbConfigSSBForReplicaDB '&lt;FQDN SQL Server di replica\>', '&lt;Nome database di replica\>', '&lt;Percorso file di backup certificato\>'**  

   > [!NOTE]  
   >  Quando il server di replica di database non si trova nell'istanza predefinita di SQL Server, per questo passaggio è necessario specificare il nome dell'istanza oltre al nome del database di replica. A tale scopo, sostituire **&lt;Replica Database Name\>** con **&lt;Instance name\\Replica Database Name\>** .  

    Dopo aver esportato il certificato dal server di replica di database, inserire una copia del certificato nel server di database dei siti primari.  

3. Usare **SQL Server Management Studio** per connettersi al database del sito primario. Dopo aver eseguito la connessione al database dei siti primari, eseguire una query per importare il certificato e specificare la porta Service Broker in uso nel server di replica di database, l'FQDN del server di replica di database e il nome del database delle repliche di database. In questo modo, il database dei siti primari viene configurato per usare Service Broker per comunicare con il database del server di replica di database.  

    Eseguire la query seguente per importare il certificato dal server di replica di database e specificare i dettagli necessari: **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;Porta SQL Service Broker\>', '&lt;Percorso file certificato\>', '&lt;FQDN SQL Server di replica\>', '&lt;Nome database replica\>'**  

   > [!NOTE]  
   >  Quando il server di replica di database non si trova nell'istanza predefinita di SQL Server, per questo passaggio è necessario specificare il nome dell'istanza oltre al nome del database di replica. A tale scopo, sostituire **&lt;Replica Database Name\>** con **\Instance name\\Replica Database Name\>** .  

4. Successivamente, nel server di database del sito eseguire il comando seguente per esportare il certificato per il server di database del sito: **EXEC sp_BgbCreateAndBackupSQLCert '&lt;Percorso file di backup certificato\>'**  

    Dopo aver esportato il certificato dal server di database del sito, inserire una copia del certificato nel server di replica di database.  

5. Usare **SQL Server Management Studio** per connettersi al database del server di replica di database. Dopo aver eseguito la connessione al database del server di replica di database, eseguire una query per importare il certificato e specificare il codice del sito del sito primario e la porta Service Broker in uso nel server di database del sito. In questo modo, il server di replica di database viene configurato per usare Service Broker per comunicare con il database del sito primario.  

    Eseguire la query seguente per importare il certificato dal server di database del sito: **EXEC sp_BgbConfigSSBForRemoteService '&lt;Codice sito\>', '&lt;Porta SQL Service Broker\>', '&lt;Percorso file certificato\>'**  

   Alcuni minuti dopo aver completato la configurazione del database del sito e del database della replica di database, Notification Manager imposta la conversazione di Service Broker nel sito primario per la notifica client dal database del sito primario alla replica di database.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> Script supplementari per ulteriori repliche di database in un'unica istanza di SQL Server  
 Quando si usa lo script del passaggio 4 per configurare un certificato autofirmato per il server di replica di database in un'istanza di Server SQL in cui è già presente una replica di database che si intende continuare a usare, è necessario usare una versione modificata dello script originale. Le modifiche seguenti impediscono allo script di eliminare un certificato esistente nel server e creano i certificati successivi con nomi descrittivi univoci.  Modificare lo script originale nel modo seguente:  

-   Impostare come commento (impedire l'esecuzione) ogni riga tra le voci di script **# Delete existing cert if one exists** e **# Create the new cert**. A questo scopo, aggiungere il carattere  **#**  all'inizio di tutte le righe interessate.  

-   Per ogni replica di database successiva in cui si usa questo script di configurazione, aggiornare il nome descrittivo per il certificato.  A questo scopo, modificare la riga **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** e sostituire **ConfigMgr SQL Server Identification Certificate** con un nuovo nome, ad esempio  **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a> Gestire le configurazioni di replica di database  
 Quando si usa una replica di database in un sito, usare le informazioni nelle seguenti sezioni per integrare i processi di disinstallazione di un replica di database, disinstallazione di un sito che usa una replica di database oppure spostamento del database del sito in una nuova installazione di SQL Server. Quando si usano le informazioni delle seguenti sezioni per eliminare delle pubblicazioni, usare le informazioni disponibili per l'eliminazione di repliche transazionali per la versione di SQL Server usata per la replica di database. Per altre informazioni, vedere [Eliminare una pubblicazione](/sql/relational-databases/replication/publish/delete-a-publication?view=sql-server-ver15).  

> [!NOTE]  
>  Dopo aver ripristinato il database di un sito che era stato configurato per le repliche di database, prima di poter usare le repliche è necessario riconfigurare ciascuna replica del database, ricreando sia le pubblicazioni sia le sottoscrizioni.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Disinstallare una replica di database  
 Quando si usa una replica di database per un punto di gestione, potrebbe essere necessario disinstallare la replica di database per un periodo di tempo e quindi riconfigurarla per l'utilizzo. Ad esempio, è necessario rimuovere le repliche di database prima di aggiornare un sito di Configuration Manager a un nuovo Service Pack. Dopo aver completato l'aggiornamento del sito, è possibile ripristinare la replica di database per l'utilizzo.  

 Usare i seguenti passaggi per disinstallare una replica di database.  

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito**, selezionare **Server e ruoli del sistema del sito** e quindi nel riquadro dei dettagli selezionare il server del sistema del sito in cui è situato il punto di gestione che usa la replica di database da disinstallare.  

2.  Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse su **Punto di gestione** e selezionare **Proprietà**.  

3.  Nella scheda **Database del punto di gestione** selezionare **Usa database del sito** per configurare il punto di gestione per l'utilizzo del database del sito invece della replica di database. Quindi fare clic su **OK** per salvare la configurazione.  

4.  Successivamente, usare **SQL Server Management Studio** per eseguire le seguenti attività:  

    -   Eliminare la pubblicazione per la replica di database dal database del server del sito.  

    -   Eliminare la sottoscrizione per la replica di database dal server di replica di database.  

    -   Eliminare il database di replica dal server di replica di database.  

    -   Disattivare la pubblicazione e la distribuzione nel server di database del sito. Per disattivare la pubblicazione e la distribuzione, fare clic con il pulsante destro del mouse sulla cartella Replica e quindi su **Disattiva pubblicazione e distribuzione**.  

5.  Dopo aver eliminato la pubblicazione, la sottoscrizione e la replica di database e aver disattivato la pubblicazione nel server di database del sito, la replica di database verrà disinstallata.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Disinstallare un server del sito che pubblica una replica di database  
 Prima di disinstallare un sito che pubblica una replica di database, usare i seguenti passaggi per eseguire la pulizia della pubblicazione e delle sottoscrizioni.  

1.  Usare **SQL Server Management Studio** per eliminare la pubblicazione della replica di database dal database del server del sito.  

2.  Usare **SQL Server Management Studio** per eliminare la sottoscrizione della replica di database da ogni SQL Server remoto che ospita una replica di database per questo sito.  

3.  Disinstallare il sito.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> Spostare un database del server del sito che pubblica una replica di database  
 Quando si sposta il database del sito in un nuovo computer, usare i seguenti passaggi:  

1.  Usare **SQL Server Management Studio** per eliminare la pubblicazione della replica di database dal database del server del sito.  

2.  Usare **SQL Server Management Studio** per eliminare la sottoscrizione della replica di database da ogni server di replica di database per questo sito.  

3.  Spostare il database nel nuovo computer SQL Server. Per altre informazioni, vedere la sezione [Modificare la configurazione del database del sito](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) nell'argomento [Modificare l'infrastruttura di Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

4.  Ricreare la pubblicazione per la replica di database nel server di database del sito. Per altre informazioni, vedere la sezione [Passaggio 1: Configurare il server di database del sito per la pubblicazione della replica di database](#BKMK_DBReplica_ConfigSiteDB) in questo argomento.  

5.  Ricreare le sottoscrizioni per la replica di database in ogni server di replica di database. Per altre informazioni, vedere la sezione [Passaggio 2: Configurare il server di replica di database](#BKMK_DBReplica_ConfigSrv) in questo argomento.