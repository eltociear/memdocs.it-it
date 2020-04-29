---
title: Crittografare i dati di ripristino
titleSuffix: Configuration Manager
description: Crittografare le chiavi di ripristino di BitLocker, i pacchetti di ripristino e gli hash delle password TPM attraverso la rete e nel database di Configuration Manager.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709349"
---
# <a name="encrypt-recovery-data"></a>Crittografare i dati di ripristino

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Quando si creano criteri di gestione di BitLocker, Configuration Manager distribuisce il servizio di ripristino in un punto di gestione. Nella pagina **Gestione client** dei criteri di gestione di BitLocker, quando si sceglie **Configura i servizi di gestione di BitLocker**, il client esegue il backup delle informazioni di ripristino delle chiavi nel database del sito. Queste informazioni includono le chiavi di ripristino di BitLocker, i pacchetti di ripristino e gli hash delle password TPM. Quando gli utenti restano bloccati fuori dal dispositivo protetto, è possibile usare queste informazioni per aiutarli ripristinare l'accesso nel dispositivo.

Considerata la natura sensibile di queste informazioni, è opportuno proteggerle nelle circostanze seguenti:

- Configuration Manager richiede una connessione HTTPS tra il client e il servizio di ripristino per crittografare i dati in transito attraverso la rete. Sono disponibili due opzioni:

  - Abilitare il sito Web IIS per HTTPS nel punto di gestione che ospita il servizio di ripristino, non nell'intero ruolo del punto di gestione. Questa opzione si applica solo a Configuration Manager versione 2002.<!-- 5925660 -->

  - Configurare il punto di gestione per HTTPS. Nelle proprietà del punto di gestione l'impostazione **Connessioni client** deve essere **HTTPS**. Questa opzione si applica a Configuration Manager versioni 1910 o 2002.

    > [!NOTE]
    > Attualmente non è supportato il protocollo HTTP avanzato.

- Prendere inoltre in considerazione la possibilità di crittografare questi dati quando vengono archiviati nel database del sito. È possibile usare la crittografia a livello di cella di SQL Server con il proprio certificato.

    Se non si vuole creare un certificato di crittografia di gestione di BitLocker, acconsentire esplicitamente all'archiviazione in testo normale dei dati di ripristino. Quando si creano criteri di gestione di BitLocker, abilitare l'opzione **Consenti l'archiviazione delle informazioni di ripristino come testo normale**.

    > [!NOTE]
    > Un altro livello di sicurezza consiste nel crittografare l'intero database del sito. Se si abilita la crittografia nel database, non ci sono problemi funzionali in Configuration Manager.
    >
    > Applicare la crittografia con cautela, soprattutto in ambienti di grandi dimensioni. A seconda delle tabelle crittografate e della versione di SQL, è possibile riscontrare un calo delle prestazioni del 25%. Aggiornare i piani di backup e ripristino in modo da poter ripristinare correttamente i dati crittografati.

## <a name="certificate-requirements"></a>Requisiti per i certificati

### <a name="https-server-authentication-certificate"></a>Certificato di autenticazione server HTTPS

<!--5925660-->

In Configuration Manager Current Branch versione 1910, per integrare il servizio di ripristino di BitLocker in Configuration Manager era necessario abilitare un punto di gestione per HTTPS. La connessione HTTPS, infatti, è necessaria per crittografare le chiavi di ripristino attraverso la rete dal client Configuration Manager al punto di gestione. La procedura di configurazione del punto di gestione e di tutti i client per HTTPS, tuttavia, può risultare per molti clienti troppo complessa.

A partire dalla versione 2002, il requisito HTTPS è valido solo per il sito Web IIS che ospita il servizio di ripristino, non per l'intero ruolo del punto di gestione. Con questa modifica vengono comunque soddisfatti i requisiti del certificato e crittografate le chiavi di ripristino in transito.

A questo punto, la proprietà **Connessioni client** del punto di gestione può essere **HTTP** o **HTTPS**. Se il punto di gestione è configurato per **HTTP**, per supportare il servizio di ripristino di BitLocker:

1. Acquisire un certificato di autenticazione server. Associare il certificato al sito Web IIS nel punto di gestione che ospita il servizio di ripristino di BitLocker.

2. Configurare i client in modo che considerino attendibile il certificato di autenticazione server. Esistono due metodi per confermare l'attendibilità:

    - Usare un certificato di un provider pubblico considerato attendibile a livello globale. Ad esempio, tra gli altri, DigiCert, Thawte, o VeriSign. I client Windows includono le autorità di certificazione (CA) che rilasciano i certificati radice trusted da questi provider. Usando un certificato di autenticazione server rilasciato da uno di questi provider, i client dovrebbero confermare automaticamente l'attendibilità.

    - Usare un certificato rilasciato da un'autorità di certificazione dall'infrastruttura a chiave pubblica dell'organizzazione. Nella maggior parte delle implementazioni di infrastruttura a chiave pubblica le autorità di certificazione radice attendibili vengono aggiunte ai client di Windows. Ad esempio, usando i servizi certificati Active Directory con criteri di gruppo. Se si rilascia il certificato di autenticazione server da un'autorità di certificazione che i client non considerano automaticamente attendibile, aggiungere ai client il certificato radice trusted dell'autorità.

> [!TIP]
> Gli unici client che devono comunicare con il servizio di ripristino sono quelli che si intende impostare come destinazione dei criteri di gestione di BitLocker e che includono una regola di **Gestione client**.

Nel client usare il file **BitLockerManagementHandler.log** per risolvere i problemi relativi a questa connessione. Per la connettività al servizio di ripristino, il log mostra l'URL usato dal client. Individuare una voce che inizia con `Checking for Recovery Service at`.

> [!NOTE]
> Se il sito ha più di un punto di gestione, abilitare HTTPS in tutti i punti di gestione del sito con cui un client gestito da BitLocker potrebbe potenzialmente comunicare. Se il punto di gestione HTTPS non è disponibile, il client potrebbe eseguire il failover a un punto di gestione HTTP e quindi non depositare la chiave di ripristino.
>
> Questa raccomandazione si applica a entrambe le opzioni: abilitazione del punto di gestione per HTTPS o abilitazione del sito Web IIS che ospita il servizio di ripristino nel punto di gestione.

### <a name="sql-encryption-certificate"></a>Certificato di crittografia SQL

Usare questo certificato per abilitare la crittografia a livello di cella di SQL Server per i dati di ripristino di BitLocker. È possibile usare un processo personalizzato per creare e distribuire il certificato di crittografia di gestione di BitLocker, a condizione che siano soddisfatti i requisiti seguenti:

- Il nome del certificato di crittografia di gestione di BitLocker deve essere `BitLockerManagement_CERT`.

- Crittografare il certificato con una chiave master del database.

- Per gli utenti SQL seguenti sono necessarie autorizzazioni di **controllo** per il certificato:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Distribuire lo stesso certificato in ogni database del sito nella gerarchia.

- Creare il certificato con la versione più recente di SQL Server nell'ambiente in uso. Ad esempio:
  - I certificati creati con SQL Server 2016 o versioni successive sono compatibili con SQL Server 2014 o versioni precedenti.
  - I certificati creati con SQL Server 2014 o versioni precedenti non sono compatibili con SQL Server 2016 o versioni successive.

## <a name="example-scripts"></a>Script di esempio

Questi script SQL sono esempi per la creazione e la distribuzione di un certificato di crittografia di gestione di BitLocker nel database del sito di Configuration Manager.

### <a name="create-certificate"></a>Crea il certificato

Questo script di esempio esegue le azioni seguenti:

- Crea un certificato
- Imposta le autorizzazioni
- Crea una chiave master del database

Prima di usare questo script in un ambiente di produzione, modificare i valori seguenti:

- Nome database sito (`CM_ABC`)
- Password per la creazione della chiave master (`MyMasterKeyPassword`)
- Data di scadenza certificato (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Eseguire il backup del certificato

Questo script di esempio esegue il backup di un certificato. Quando si salva il certificato in un file, è possibile [ripristinarlo](#restore-certificate) in altri database del sito nella gerarchia.

Prima di usare questo script in un ambiente di produzione, modificare i valori seguenti:

- Nome database sito (`CM_ABC`)
- Percorso file e nome (`C:\BitLockerManagement_CERT_KEY`)
- Password della chiave di esportazione (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Archiviare il file di certificato esportato e la password associata in un luogo sicuro.

### <a name="restore-certificate"></a>Ripristinare il certificato

Questo script di esempio ripristina un certificato da un file. Usare questo processo per distribuire un certificato creato in un altro database del sito.

Prima di usare questo script in un ambiente di produzione, modificare i valori seguenti:

- Nome database sito (`CM_ABC`)
- Password chiave master (`MyMasterKeyPassword`)
- Percorso file e nome (`C:\BitLockerManagement_CERT_KEY`)
- Password della chiave di esportazione (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Verifica il certificato

Usare questo script SQL per verificare che SQL abbia creato correttamente il certificato con le autorizzazioni necessarie.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Se il certificato è valido, lo script restituisce un valore `1`.

## <a name="see-also"></a>Vedere anche

Per altre informazioni su questi comandi SQL, vedere gli articoli seguenti:

- [Chiavi di crittografia del database e di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [CREATE CERTIFICATE](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [BACKUP CERTIFICATE](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [CREATE MASTER KEY](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [BACKUP MASTER KEY](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Concedere le autorizzazioni per i certificati](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
