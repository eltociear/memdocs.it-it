---
title: Modificare l'infrastruttura
titleSuffix: Configuration Manager
description: Apportare modifiche o eseguire azioni che interessano l'infrastruttura di Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694359"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Modificare l'infrastruttura di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver installato uno o più siti, può essere necessario modificare le configurazioni o eseguire azioni che incidono sull'infrastruttura.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> Gestire il provider SMS

Il provider SMS fornisce il punto di contatto amministrativo per una o più console di Configuration Manager. Quando si installano più provider SMS, è possibile fornire ridondanza per i punti di contatto per l'amministrazione del sito e della gerarchia.

In ogni sito di Configuration Manager è possibile eseguire nuovamente il programma di installazione per:

- Aggiungere un'altra istanza del provider SMS. Ogni istanza aggiuntiva del provider SMS deve trovarsi in un computer separato.

- Rimuovere un'istanza del provider SMS. Per rimuovere l'ultimo provider SMS per un sito, è necessario disinstallare il sito.

È possibile monitorare l'installazione o la rimozione del provider SMS visualizzando **ConfigMgrSetup.log** nella cartella radice del server del sito su cui si esegue il programma di installazione.

Prima di modificare il provider SMS in un sito, vedere [Pianificare per il provider SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Gestire la configurazione del provider SMS per un sito  

1. Eseguire il **programma di installazione di Configuration Manager** da `\BIN\X64\setup.exe` nella cartella di installazione del sito di Configuration Manager.

1. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**.

1. Nella pagina **Manutenzione sito** selezionare **Modifica configurazione provider SMS**.

1. Nella pagina **Gestisci provider SMS** selezionare una delle opzioni seguenti:

    - **Aggiungi nuovo provider SMS**: specificare il nome di dominio completo di un computer che ospiterà il provider SMS e che attualmente non ne ospita uno.

    - **Disinstalla il provider SMS specificato**: selezionare il nome del computer da cui si vuole rimuovere il provider SMS.

    > [!TIP]  
    > Per spostare il provider SMS tra due computer, occorre prima installarlo nel nuovo computer e poi rimuoverlo dal percorso originale. Non esiste un'opzione dedicata per spostare il provider SMS tra computer.

Al termine dell'Installazione guidata, viene completata la configurazione del provider SMS. Nella scheda **Generale** delle **Proprietà** del sito verificare i computer in cui è installato un provider SMS per un sito.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> Gestire la console di Configuration Manager

Di seguito sono riportate le attività che è possibile eseguire per gestire la console di Configuration Manager:

- Per modificare la lingua visualizzata nella console di Configuration Manager, vedere la sezione [Gestire la lingua della console di Configuration Manager](#BKMK_ManageConsoleLanguages).

- Per installare console aggiuntive, vedere [Installare la console di Configuration Manager](../deploy/install/install-consoles.md).

- Per configurare le autorizzazioni DCOM per abilitare console remote rispetto al server del sito, vedere [Configurare le autorizzazioni DCOM per le console remote di Configuration Manager](#BKMK_ConfigDCOMforRemoteConsole).

- Per modificare le autorizzazioni amministrative che limitano ciò che gli utenti possono fare e vedere nella console, vedere [Modificare l'ambito amministrativo di un utente amministratore](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> Gestire la lingua della console di Configuration Manager

Durante l'installazione del server del sito, i file di installazione della console di Configuration Manager e i Language Pack supportati per il sito vengono copiati nella sottocartella `\Tools\ConsoleSetup`del percorso di installazione di Configuration Manager nel server del sito.

- Quando si avvia l'installazione della console di Configuration Manager da questa cartella nel server del sito, la console di Configuration Manager e i file dei Language Pack supportati vengono copiati nel computer.

- Quando un Language Pack è disponibile per l'impostazione della lingua corrente nel computer, la console di Configuration Manager viene aperta in questa lingua.

- Se il Language Pack associato non è disponibile per la console di Configuration Manager, la console viene aperta in inglese (Stati Uniti).

Ad esempio, si installa la console di Configuration Manager da un server del sito che supporta l'inglese, il tedesco e il francese. Se si apre la console di Configuration Manager su un computer con un'impostazione lingua configurata sul francese, la console si aprirà in francese. Se si apre la console di Configuration Manager in un computer con la lingua configurata sul giapponese, la console si aprirà in inglese perché il Language Pack giapponese non è disponibile.  

A ogni apertura della console di Configuration Manager:

- Vengono determinate le impostazioni di lingua configurate per il computer
- Viene verificata la disponibilità di un Language Pack associato per la console di Configuration Manager
- Viene aperta la console usando il Language Pack appropriato

Per aprire la console di Configuration Manager in inglese indipendentemente dalle impostazioni di lingua configurate nel computer, rimuovere o rinominare manualmente i file dei Language Pack nel computer.

Usare le procedure seguenti per avviare la console di Configuration Manager in inglese indipendentemente dalle impostazioni locali configurate nel computer.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Per installare una versione solo in lingua inglese della console di Configuration Manager nei computer  

1. In Esplora risorse passare a `\Tools\ConsoleSetup\LanguagePack` nel percorso di installazione di Configuration Manager.

1. Rinominare i file **.msp** e **.mst** Ad esempio, è possibile modificare **&lt;nome file\>.MSP** in **&lt;nome file\>.MSP.disabled**.

1. Installare la console di Configuration Manager nel computer.

    > [!IMPORTANT]
    > Quando vengono configurate nuove lingue per il server del sito, i file .msp e .mst vengono ricopiati nella cartella **LanguagePack** ed è necessario ripetere questa procedura per installare le nuove console di Configuration Manager solo in lingua inglese.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Disabilitare temporaneamente una lingua della console in un'installazione della console di Configuration Manager esistente

1. Nel computer che esegue la console di Configuration Manager chiudere la console.

1. In Esplora risorse passare a &lt;*PercorsoInstallazioneConsole*>\Bin\ nel computer della console di Configuration Manager.  

1. Rinominare la cartella della lingua appropriata per la lingua configurata nel computer. Ad esempio, se le impostazioni della lingua per il computer erano configurate per il tedesco, è possibile rinominare la cartella **de** in **de.disabled**.  

1. Per aprire la console di Configuration Manager nella lingua configurata per il computer, rinominare la cartella con il nome originale. Ad esempio, rinominare **de.disabled** in **de**.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configurare le autorizzazioni DCOM per le console remote

L'account utente che esegue la console di Configuration Manager richiede l'autorizzazione ad accedere al database del sito usando il provider SMS. Tuttavia, un utente amministratore che usa una console di Configuration Manager remota deve avere anche le autorizzazioni DCOM di **attivazione remota** per:

- Il computer del server del sito

- Ogni computer che ospita un'istanza del provider SMS

Il gruppo di sicurezza **SMS Admins** concede l'accesso a un provider SMS in un computer e può essere usato anche per concedere le autorizzazioni DCOM necessarie. Questo gruppo è locale nel computer quando il provider SMS è in esecuzione in un server membro. È un gruppo locale di dominio quando il provider SMS è in esecuzione in un controller di dominio.

> [!IMPORTANT]
> La console di Configuration Manager usa WMI per connettersi al provider SMS, mentre WMI internamente usa DCOM. Se la console di Configuration Manager è in esecuzione in un computer diverso dal computer del provider SMS, richiede le autorizzazioni per attivare un server DCOM nel computer del provider SMS. Per impostazione predefinita, l'attivazione remota viene concessa solo ai membri del gruppo Administrators incorporato.
>
> Se si concede l'autorizzazione di attivazione remota al gruppo SMS Admins, un membro di tale gruppo potrebbe tentare degli attacchi DCOM contro il computer del provider SMS. Questa configurazione aumenta anche la superficie di attacco del computer. Per limitare questo rischio, è necessario monitorare attentamente l'appartenenza al gruppo SMS Admins.

Usare la procedura riportata di seguito per configurare ciascun sito di amministrazione centrale (CAS), server del sito primario e ciascun computer in cui è installato il provider SMS per concedere l'accesso alla console remota di Configuration Manager per gli utenti amministratori.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Configurare le autorizzazioni DCOM per le connessioni remote della console di Configuration Manager

1. Come amministratore del computer di destinazione, eseguire `Dcomcnfg.exe` per aprire **Servizi componenti**.

1. Espandere **Servizi componenti**, **Computer** e selezionare **Risorse del computer**. Scegliere **Proprietà** dal menu **Azione**.

1. Nella finestra di dialogo **Proprietà computer** passare alla scheda **Sicurezza COM**. Nella sezione **Autorizzazioni di esecuzione e attivazione** selezionare **Modifica limiti**.

1. Nella finestra **Autorizzazioni di esecuzione e attivazione** selezionare **Aggiungi**.

1. Nel campo **Immettere i nomi degli oggetti da selezionare** della finestra **Seleziona utenti, computer, account di servizio o gruppi** digitare `SMS Admins`, quindi fare clic su **OK**.

   > [!TIP]
   > Per individuare il gruppo SMS Admins può essere necessario modificare l'impostazione: **Da questo percorso**. Questo gruppo è locale nel computer quando il provider SMS è in esecuzione in un server membro ed è un gruppo locale di dominio quando il provider SMS è in esecuzione in un controller di dominio.

1. Nella sezione **Autorizzazioni per SMS Admins** selezionare la colonna **Consenti** per la riga **Attivazione remota** per consentire l'attivazione remota.

1. Selezionare **OK** per salvare le modifiche e chiudere tutte le finestre.

Il computer è ora configurato per consentire l'accesso alla console remota di Configuration Manager ai membri del gruppo Amministratori SMS.

Ripetere questa procedura in ciascun computer del provider SMS che supporti console remote di Configuration Manager.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> Modificare la configurazione del database del sito

Dopo aver installato un sito, è possibile modificarne la configurazione del database e del server di database. Per apportare modifiche, eseguire il programma di installazione di Configuration Manager in un server CAS o un server del sito primario. È possibile spostare il database del sito in una nuova istanza di SQL Server sullo stesso computer o su un computer diverso sul quale è in esecuzione una versione supportata di SQL Server. Queste modifiche e quelle correlate non sono supportate per la configurazione del database nei siti secondari.

Per altre informazioni sui limiti del supporto, vedere [Criteri di supporto per la modifica manuale del database in un ambiente di Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> Quando si modifica la configurazione del database di un sito, Configuration Manager riavvia o reinstalla i servizi di Configuration Manager nel server del sito e nei server del sistema del sito remoto che comunicano con il database.

### <a name="modify-the-database-configuration"></a>Modificare la configurazione del database

Eseguire il programma di installazione di Configuration Manager nel server del sito e selezionare l'opzione **Esegui una manutenzione del sito o reimposta il sito**. Selezionare quindi l'opzione **Modifica la configurazione di SQL Server**. È possibile modificare le seguenti configurazioni del database del sito:

- Il server basato su Windows che ospita il database.

- L'istanza di SQL Server in uso su un server che ospita il database SQL Server.

- Nome del database.

- Porta di SQL Server usata da Configuration Manager.

- Porta di SQL Server Service Broker usata da Configuration Manager.

### <a name="move-the-site-database"></a>Spostare il database del sito

Se si sposta il database del sito, rivedere anche le configurazioni seguenti:

- Quando si sposta il database del sito in un nuovo computer, aggiungere l'account computer del server del sito al gruppo **Administrators** locale nel computer che esegue SQL Server. Se si usa un cluster di SQL Server per il database del sito, aggiungere l'account computer al gruppo **Administrators** locale di ogni computer nodo del cluster di Windows Server.

- Quando si sposta il database in una nuova istanza di SQL Server o in un nuovo computer SQL Server, abilitare l'integrazione di Common Language Runtime (CLR). Usare **SQL Server Management Studio** per connettersi all'istanza di SQL Server che ospita il database del sito. Eseguire quindi la stored procedure seguente come query: `sp_configure 'clr enabled',1; reconfigure`

- Verificare che la nuova istanza di SQL Server abbia accesso al percorso di backup. Quando si usa un percorso UNC per archiviare il backup del database del sito, dopo lo spostamento del database in un nuovo server, verificare che l'account computer del nuovo SQL Server abbia autorizzazioni di **scrittura** per il percorso UNC. Questa configurazione include i casi in cui di spostamento in un gruppo di disponibilità AlwaysOn di SQL Server o in un cluster di SQL Server.

> [!IMPORTANT]
> Prima di spostare un database contenente una o più repliche di database per i punti di gestione, rimuovere le repliche di database. Dopo aver completato lo spostamento del database, è possibile riconfigurare le repliche di database. Per altre informazioni, vedere [Repliche di database per i punti di gestione](../deploy/configure/database-replicas-for-management-points.md).

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> Gestire il nome dell'entità servizio (SPN) per il server di database del sito

È possibile scegliere l'account che esegue i servizi di SQL per il database del sito:

- Quando i servizi vengono eseguiti con l'account di sistema del computer, il nome dell'entità servizio viene registrato automaticamente.

- Quando i servizi vengono eseguiti con un account utente locale di dominio, registrare manualmente il SPN. Il SPN consente ai client SQL e ad altri sistemi del sito di eseguire l'autenticazione con Kerberos. Senza l'autenticazione Kerberos, la comunicazione con il database potrebbe non riuscire.

Per altre informazioni su SPN e connessioni Kerberos, vedere [Registrazione di un nome dell'entità servizio per le connessioni Kerberos](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

È possibile registrare un SPN per l'account del servizio SQL Server del server di database del sito usando lo strumento **Setspn**. Eseguire Setspn come amministratore di dominio in un computer nello stesso dominio di SQL Server.

Le procedure seguenti sono esempi di come configurare il nome dell'entità servizio per l'account del servizio SQL Server. Per altre informazioni su Setspn, vedere la [panoramica su Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Creare manualmente il nome dell'entità di servizio (SPN) di un utente di dominio per l'account del servizio SQL Server

1. Aprire un prompt dei comandi come amministratore.

1. Immettere un comando valido per creare il valore SPN per il nome NetBIOS e il nome di dominio completo:

    > [!IMPORTANT]
    > Quando si crea un SPN per un server SQL del cluster, specificare il nome virtuale del cluster di SQL Server come nome del computer SQL Server.

    - Nome NetBIOS: `setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        ad esempio `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN: `setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        ad esempio `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > Il comando per registrare un SPN per un'istanza denominata di SQL Server è lo stesso usato per la registrazione di un SPN per un'istanza predefinita. L'unica eccezione è che il numero di porta deve corrispondere alla porta usata dall'istanza denominata.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Verificare che il nome SPN dell'utente di dominio sia registrato correttamente

1. Aprire un prompt dei comandi come amministratore.

1. Immettere il comando seguente: `setspn -L <domain\SQL service account>`

    ad esempio `setspn -L contoso\sqlservice`

1. Esaminare il **ServicePrincipalName** registrato. Assicurarsi di aver creato un SPN valido per SQL Server.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Modificare l'account del servizio SQL Server dal sistema locale a un account utente di dominio

1. Creare o selezionare un dominio o un account utente del sistema locale che si desidera utilizzare come account servizio SQL Server.

1. Aprire **Gestione configurazione SQL Server**.

1. Selezionare **Servizi di SQL Server** e quindi aprire **SQL Server&lt;NOME ISTANZA\>** .

1. Passare alla scheda **Accedi**. Selezionare **Questo account**, quindi immettere il nome utente e la password per l'account utente di dominio creati al passaggio 1.

1. Confermare la modifica dell'account del servizio e riavviare il servizio SQL Server.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a> Eseguire una reimpostazione del sito

Quando viene eseguita la reimpostazione di un CAS o di un sito primario, il sito:

- Riapplica le autorizzazioni di file e registro di sistema predefinite di Configuration Manager

- Reinstalla tutti i componenti e tutti i ruoli del sistema del sito

I siti secondari non supportano la reimpostazione.

Le reimpostazioni di siti possono essere eseguite manualmente. Possono anche essere eseguite automaticamente dopo aver modificato la configurazione del sito. Ad esempio:

- Se è stata apportata una modifica agli account usati dai componenti di Configuration Manager, è consigliabile eseguire una reimpostazione manuale del sito. Questo consente di assicurarsi che componenti del sito vengano aggiornati in modo da usare i nuovi dati degli account.

- Se si modificano le lingue del client o del server in un sito, Configuration Manager esegue automaticamente una reimpostazione del sito. La reimpostazione è necessaria perché il sito possa usare le nuove lingue.

> [!NOTE]
> Una reimpostazione del sito non comporta la reimpostazione delle autorizzazioni di accesso a oggetti non Configuration Manager.

### <a name="what-happens-during-a-site-reset"></a>Cosa accade durante una reimpostazione del sito

Quando viene eseguita la reimpostazione di un sito:

1. Il programma di installazione interrompe e riavvia il servizio **SMS_SITE_COMPONENT_MANAGER** e i componenti thread del servizio **SMS_EXECUTIVE** .

1. Il programma di installazione rimuove e quindi ricrea la cartella condivisa del sistema del sito e il componente **SMS Executive** nel computer locale e nei computer del sistema del sito remoto.

1. Il programma di installazione riavvia il servizio **SMS_SITE_COMPONENT_MANAGER**, che installa i servizi **SMS_EXECUTIVE** e **SMS_SQL_MONITOR**.

La reimpostazione del sito ripristina gli oggetti seguenti:

- Le chiavi del Registro di sistema **SMS** o **NAL** e qualsiasi altra sottochiave di queste chiavi.

- L'albero della directory di file di Configuration Manager e qualsiasi sottodirectory o file predefinito presenti nell'albero.

### <a name="prerequisites-for-site-reset"></a>Prerequisiti per la reimpostazione del sito

L'account usato per eseguire una reimpostazione del sito deve avere le autorizzazioni seguenti:

- Per reimpostare il CAS:

  - **Amministratore** locale nel server CAS

  - Privilegi equivalenti al ruolo di sicurezza dell'amministrazione basata su ruoli **Amministratore completo**

- Per reimpostare un sito primario:

  - **Amministratore** locale nel server del sito primario

  - Privilegi equivalenti al ruolo di sicurezza dell'amministrazione basata su ruoli **Amministratore completo**
  
  - Se il sito primario si trova in una gerarchia con un CAS, anche questo account deve essere un **Amministratore** locale nel server CAS.

### <a name="limitations-for-a-site-reset"></a>Limitazioni per la reimpostazione del sito

Se la gerarchia è configurata per supportare i [test degli aggiornamenti client in una raccolta di pre-produzione](../../clients/manage/upgrade/test-client-upgrades.md), non è possibile usare una reimpostazione del sito per modificare i Language Pack server o client installati nei siti.

### <a name="run-a-site-reset"></a>Eseguire una reimpostazione del sito

1. Avviare il programma di installazione di Configuration Manager nel server del sito usando uno dei metodi seguenti:

    - Nel menu**Start** selezionare **Installazione di Configuration Manager**.

    - Nella directory dei *supporti di installazione* di Configuration Manager aprire `\SMSSETUP\BIN\X64\setup.exe`. Verificare che la versione corrisponda a quella del sito.

    - Nella directory in cui è *installato* Configuration Manager aprire `\BIN\X64\setup.exe`.

1. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**.

1. Nella pagina **Manutenzione sito** selezionare **Reimposta sito senza modifiche alla configurazione**.

1. Fare clic su **Sì** per iniziare la reimpostazione del sito.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> Gestire i Language Pack in un sito

Dopo l'installazione di un sito, è possibile gestire i Language Pack di server e client in uso.

### <a name="server-language-packs"></a>Language Pack server

*Si applica a: Installazioni delle console di Configuration Manager, nuove installazioni dei ruoli del sistema del sito applicabili*

Dopo aver aggiornato i Language Pack server in un sito è possibile aggiungere il supporto per i Language Pack nelle console di Configuration Manager.

Per aggiungere il supporto per un Language Pack server in una console di Configuration Manager, installare la console di Configuration Manager dalla cartella **ConsoleSetup** in un server del sito che include il Language Pack da usare. Se la console di Configuration Manager è già installata, è necessario innanzitutto disinstallarla per consentire alla nuova installazione di identificare l'elenco corrente di Language Pack supportati.

### <a name="client-language-packs"></a>Language Pack client

Le modifiche ai Language Pack dei client aggiornano i file di origine dell'installazione client. Le nuove installazioni di client o gli aggiornamenti aggiungono il supporto per l'elenco aggiornato di lingue del client.

Dopo aver aggiornato i Language Pack client in un sito, installare ogni client che userà i Language Pack tramite i file di origine che includono i Language Pack client.

Per altre informazioni sulle lingue di client e server supportate da Configuration Manager, vedere [Language Pack](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Modificare i Language Pack supportati in un sito

1. Avviare il programma di installazione di Configuration Manager nel server del sito usando uno dei metodi seguenti:

    - Nel menu**Start** selezionare **Installazione di Configuration Manager**.

    - Nella directory dei *supporti di installazione* di Configuration Manager aprire `\SMSSETUP\BIN\X64\setup.exe`. Verificare che la versione corrisponda a quella del sito.

    - Nella directory in cui è *installato* Configuration Manager aprire `\BIN\X64\setup.exe`.

1. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**.

1. Nella pagina **Manutenzione sito** selezionare **Modifica la configurazione della lingua**.

1. Nella pagina **Download prerequisiti** selezionare una delle opzioni seguenti:

    - **Scarica file richiesti**: per acquisire gli aggiornamenti nei Language Pack.

    - **Utilizza file scaricati precedentemente**: per usare i file scaricati in precedenza che includono i Language Pack da aggiungere al sito.

1. Nella pagina **Selezione della lingua server** selezionare le lingue del server supportate dal sito.

1. Nella pagina **Selezione della lingua client**, selezionare le lingue del client supportate dal sito.

1. Completare la procedura guidata per modificare il supporto delle lingue nel sito.

    > [!NOTE]
    > Configuration Manager avvia una reimpostazione del sito che reinstalla anche tutti i ruoli di sistema del sito presenti nel sito.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> Modificare la soglia di avviso del server di database

Per impostazione predefinita, Configuration Manager genera avvisi quando lo spazio libero su disco in un server di database del sito è insufficiente:

- Genera un avviso quando lo spazio disponibile su disco è pari o inferiore a 10 GB
- Genera un avviso critico quando lo spazio disponibile su disco è pari o inferiore a 5 GB

È possibile modificare questi valori o disattivare gli avvisi per ogni sito:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.

1. Selezionare il sito da configurare. Nella barra multifunzione selezionare **Proprietà**.

1. Passare alla scheda **Avvisi** e modificare le impostazioni.

## <a name="uninstall-sites-and-hierarchies"></a>Disinstallare siti e gerarchie

Può essere necessario disinstallare un ruolo del sistema del sito, un sito o una gerarchia di Configuration Manager. Per altre informazioni, vedere [Disinstallare ruoli, siti e gerarchie](../deploy/install/uninstall-sites-and-hierarchies.md).

A partire dalla versione 2002, è anche possibile rimuovere il CAS da una gerarchia, mantenendo però il sito primario. Per altre informazioni, vedere [Rimuovere il sito di amministrazione centrale](../deploy/install/remove-central-administration-site.md).
