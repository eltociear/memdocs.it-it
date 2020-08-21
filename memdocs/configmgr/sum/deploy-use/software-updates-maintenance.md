---
title: Manutenzione degli aggiornamenti software
titleSuffix: Configuration Manager
description: Per gestire gli aggiornamenti in Configuration Manager, è possibile pianificare l'attività di pulizia di WSUS oppure eseguirla manualmente.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: a327d50a2743f81407530355b6fd5101ce6a8b02
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696906"
---
# <a name="software-updates-maintenance"></a>Manutenzione degli aggiornamenti software

*Si applica a: Configuration Manager (Current Branch)*

È possibile pianificare ed eseguire attività di pulizia WSUS nella console di Configuration Manager, dalle proprietà del componente del punto di aggiornamento software. Quando si sceglie di eseguire l'attività di pulizia WSUS, questa verrà eseguita dopo la successiva sincronizzazione degli aggiornamenti software.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Per pianificare ed eseguire il processo di pulizia WSUS

Pianificare il processo di pulizia WSUS seguendo questa procedura:

1. Nella console di Configuration Manager passare a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito al livello superiore della gerarchia di Configuration Manager.

3. Fare clic su **Configura componenti del sito** nel gruppo **Impostazioni** , quindi fare clic su **Punto di aggiornamento software** per aprire Proprietà del componente del punto di aggiornamento software.  

4. Esaminare **Comportamento di sostituzione**. Se necessario, modificare il comportamento.

   ![Screenshot di Comportamento di sostituzione](media/supersedence-behavior.png)

5. Fare clic sulla scheda **Regole di sostituzione** e selezionare **Eseguire pulizia guidata WSUS**. Nella versione 1806, l'opzione è stata rinominata **Esegui la pulizia WSUS dopo la sincronizzazione**.

6. Fare clic su **OK**. Se si esegue la versione 1806, fare clic su **Chiudi**.

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportamento del processo di pulizia WSUS nella versione 1802 e precedenti

Nelle versioni precedenti a Configuration Manager versione 1806, l'opzione della pulizia WSUS esegue questo elemento:

- Opzione **Aggiornamenti scaduti** della pulizia guidata WSUS solo nel server WSUS del sito principale.

  ![Screenshot della pulizia WSUS degli aggiornamenti scaduti](media/wsus-cleanup-expired.PNG)

- Ogni sette giorni viene eseguita una pulizia degli elementi di configurazione degli aggiornamenti software nel database di Configuration Manager e vengono così rimossi gli aggiornamenti non necessari dalla console.
  - Questa pulizia non rimuoverà dalla console di Configuration Manager gli aggiornamenti scaduti attualmente distribuiti.

È comunque necessario eseguire operazioni di manutenzione aggiuntive sul database WSUS principale e su tutti gli altri database WSUS nell'ambiente. Per altre informazioni e istruzioni, vedere il post di blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Guida completa alla manutenzione con Microsoft WSUS e i punti di aggiornamento software di Configuration Manager).

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportamento del processo di pulizia WSUS a partire dalla versione 1806

A partire dalla versione 1806, l'opzione di pulizia WSUS viene eseguita dopo ogni sincronizzazione per questi elementi:
<!--1357898 -->

- Opzione **Aggiornamenti scaduti** per i server WSUS nei siti CAS e primari.
  - I server WSUS per i server secondari non eseguono la pulizia WSUS per gli aggiornamenti scaduti.
- Configuration Manager crea un elenco degli aggiornamenti sostituiti dal proprio database. L'elenco è basato sul comportamento di sostituzione nelle proprietà del componente del punto di aggiornamento software.
  - Gli elementi di configurazione degli aggiornamenti che soddisfano i criteri del comportamento di sostituzione vengono impostati come scaduti nella console di Configuration Manager.
  - Gli aggiornamenti vengono rifiutati in WSUS per i siti CAS e primari, ma non per i siti secondari.
- Ogni sette giorni viene eseguita una pulizia degli elementi di configurazione degli aggiornamenti software nel database di Configuration Manager e vengono così rimossi gli aggiornamenti non necessari dalla console.
  - Questa pulizia non rimuoverà dalla console di Configuration Manager gli aggiornamenti scaduti attualmente distribuiti.

> [!NOTE]
> I mesi di attesa prima della scadenza di un aggiornamento sostituito sono basati sulla data di creazione dell'aggiornamento sostitutivo. Se per questa impostazione si usano 2 mesi, ad esempio, gli aggiornamenti che sono stati sostituiti verranno rifiutati in WSUS e impostati come scaduti in Configuration Manager quando l'aggiornamento sostitutivo risale a 2 mesi prima.

Nei database WSUS dei siti secondari tutte le operazioni di manutenzione di WSUS devono essere eseguite manualmente. Nei siti CAS e primari non vengono eseguite le opzioni di **Pulizia server Windows Server Update Services** seguenti:

- Aggiornamenti e revisioni dell'aggiornamento non utilizzati
- Computer non in contatto con il server
- File di aggiornamento non necessari

  Per altre informazioni e istruzioni, vedere il post di blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Guida completa alla manutenzione con Microsoft WSUS e i punti di aggiornamento software di Configuration Manager).

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>Comportamento del processo di pulizia WSUS a partire dalla versione 1810

A partire dalla versione 1810, è possibile specificare regole di sostituzione per gli aggiornamenti delle funzionalità separatamente dagli aggiornamenti diversi dalle funzionalità nelle proprietà del componente del punto di aggiornamento software. L'opzione di pulizia WSUS viene eseguita dopo ogni sincronizzazione per questi elementi:
<!--2839349,3098809, 2977644-->

- Opzione **Aggiornamenti scaduti** per i server WSUS nei siti CAS, primari e secondari.
- Configuration Manager crea un elenco degli aggiornamenti sostituiti dal proprio database. L'elenco è basato sul comportamento di sostituzione nelle proprietà del componente del punto di aggiornamento software.
  - Gli elementi di configurazione degli aggiornamenti che soddisfano i criteri del comportamento di sostituzione vengono impostati come scaduti nella console di Configuration Manager.
  - Gli aggiornamenti vengono rifiutati in WSUS per i siti CAS, primari e secondari.
- Ogni sette giorni viene eseguita una pulizia degli elementi di configurazione degli aggiornamenti software nel database di Configuration Manager e vengono così rimossi gli aggiornamenti non necessari dalla console.
  - Questa pulizia non rimuoverà dalla console di Configuration Manager gli aggiornamenti scaduti attualmente distribuiti.

> [!NOTE]
> I mesi di attesa prima della scadenza di un aggiornamento sostituito sono basati sulla data di creazione dell'aggiornamento sostitutivo. Se per questa impostazione si usano 2 mesi, ad esempio, gli aggiornamenti che sono stati sostituiti verranno rifiutati in WSUS e impostati come scaduti in Configuration Manager quando l'aggiornamento sostitutivo risale a 2 mesi prima.

Nei siti CAS, primari e secondari non vengono eseguite le opzioni di **Pulizia server Windows Server Update Services** seguenti:

- Aggiornamenti e revisioni dell'aggiornamento non utilizzati
- Computer non in contatto con il server
- File di aggiornamento non necessari

  Per altre informazioni e istruzioni, vedere il post di blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Guida completa alla manutenzione con Microsoft WSUS e i punti di aggiornamento software di Configuration Manager).

## <a name="wsus-cleanup-starting-in-version-1906"></a>Pulizia di WSUS a partire dalla versione 1906
<!--41101009-->

 Sono disponibili attività di manutenzione di WSUS aggiuntive che possono essere eseguite da Configuration Manager per mantenere l'integrità dei punti di aggiornamento software. Oltre a rifiutare gli aggiornamenti scaduti in WSUS, Configuration Manager può aggiungere indici non cluster ai database WSUS e rimuovere gli aggiornamenti obsoleti dai database WSUS. La manutenzione di WSUS avviene dopo ogni sincronizzazione.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Rifiutare gli aggiornamenti scaduti in WSUS secondo le regole di sostituzione

Il rifiuto degli aggiornamenti in WSUS migliora le prestazioni rimuovendo gli aggiornamenti dai cataloghi inviati ai client. Il rifiuto degli aggiornamenti che Configuration Manager contrassegna come sostituiti riduce ulteriormente i cataloghi e migliora le prestazioni.

1. Nella console di Configuration Manager passare a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito al livello superiore della gerarchia di Configuration Manager.
3. Fare clic su **Configura componenti del sito** nel gruppo Impostazioni, quindi fare clic su **Punto di aggiornamento software** per aprire Proprietà del componente del punto di aggiornamento software.
4. Nella scheda **Manutenzione WSUS** selezionare **Decline expired updates in WSUS according to supersedence rules** (Rifiuta gli aggiornamenti scaduti in WSUS secondo le regole di sostituzione).

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Aggiungere indici non cluster al database di WSUS per migliorare le prestazioni di pulizia di WSUS

L'aggiunta di indici non cluster consente di migliorare le prestazioni della pulizia di WSUS eseguita da Configuration Manager.

1. Nella console di Configuration Manager passare a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito al livello superiore della gerarchia di Configuration Manager.
3. Fare clic su **Configura componenti del sito** nel gruppo Impostazioni, quindi fare clic su **Punto di aggiornamento software** per aprire Proprietà del componente del punto di aggiornamento software.
4. Nella scheda **Manutenzione WSUS** selezionare **Add non-clustered indexes to the WSUS database** (Aggiungi indici non cluster al database WSUS).
5. In ogni database SUSDB usato da Configuration Manager gli indici vengono aggiunti alle tabelle seguenti:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>Autorizzazioni SQL per la creazione di indici

Quando il database WSUS si trova in un server SQL remoto, può essere necessario aggiungere autorizzazioni in SQL per creare gli indici. L'account usato per la connessione al database WSUS e la creazione di indici può variare. Se si specifica un [account di connessione al server WSUS nelle proprietà del punto di aggiornamento software](../get-started/install-a-software-update-point.md#wsus-server-connection-account), verificare che l'account disponga delle autorizzazioni SQL. Se non si specifica un account di connessione al server WSUS, l'account computer del server del sito deve disporre delle autorizzazioni SQL.

- Per la creazione di un indice è richiesta l'autorizzazione `ALTER` per la tabella o vista. L'account deve essere un membro del ruolo predefinito del server`sysadmin` o dei ruoli predefiniti del database `db_ddladmin` e `db_owner`. Per altre informazioni sulla creazione dell'indice e le autorizzazioni, vedere [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions).
- È necessario concedere all'account l'autorizzazione del server `CONNECT SQL`. Per altre informazioni, vedere [Autorizzazione del server GRANT (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

> [!NOTE]  
>  Se il database WSUS si trova in un server SQL remoto tramite una porta non predefinita, non è possibile aggiungere gli indici. Per questo scenario, è possibile creare un [alias del server usando Gestione configurazione SQL Server](/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017). Dopo l'aggiunta dell'alias e quando Configuration Manager può stabilire una connessione con il database, gli indici verranno aggiunti.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Rimuovere gli aggiornamenti obsoleti dal database di WSUS

Gli aggiornamenti obsoleti sono aggiornamenti inutilizzati e revisioni di aggiornamento nel database WSUS. In generale, un aggiornamento viene considerato obsoleto quando non è più incluso in [Microsoft Update Catalog](https://www.catalog.update.microsoft.com/) e non è necessario per altri aggiornamenti come prerequisito o dipendenza.

1. Nella console di Configuration Manager passare a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito al livello superiore della gerarchia di Configuration Manager.
3. Fare clic su **Configura componenti del sito** nel gruppo Impostazioni, quindi fare clic su **Punto di aggiornamento software** per aprire Proprietà del componente del punto di aggiornamento software.
4. Nella scheda **Manutenzione WSUS** selezionare **Remove obsolete updates from the WSUS database** (Rimuovi aggiornamenti obsoleti dal database WSUS).
   - La rimozione degli aggiornamenti obsoleti potrà essere eseguita per un massimo di 30 minuti prima di essere arrestata. Verrà nuovamente avviata dopo la successiva sincronizzazione.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>Autorizzazioni SQL per la rimozione degli aggiornamenti obsoleti

Quando il database WSUS è in un server SQL remoto, l'account computer del server del sito richiede le autorizzazioni di SQL seguenti:

- Ruoli predefiniti del database `db_datareader` e `db_datawriter`. Per altre informazioni, vedere [Ruoli a livello di database](/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles).
- L'autorizzazione del server `CONNECT SQL` deve essere concessa all'account computer del server del sito. Per altre informazioni, vedere [Autorizzazione del server GRANT (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

#### <a name="wsus-cleanup-wizard"></a>Pulizia guidata WSUS

A partire dalla versione 1906 nei siti CAS, primari e secondari non vengono eseguite le opzioni di **Pulizia server Windows Server Update Services** seguenti:

- Computer non in contatto con il server
- File di aggiornamento non necessari

  Per altre informazioni e istruzioni, vedere il post di blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Guida completa alla manutenzione con Microsoft WSUS e i punti di aggiornamento software di Configuration Manager).


### <a name="known-issues-for-version-1906"></a>Problemi noti per la versione 1906

Considerare lo scenario seguente:
<!--5418148-->
- Si sta usando Configuration Manager versione 1906
- Sono presenti punti di aggiornamento software remoti che usano un database interno di Windows
- Nelle **proprietà del componente punto di aggiornamento software** una delle opzioni seguenti è selezionata nella scheda **Manutenzione WSUS**:
   - Aggiungi indici non cluster al database di WSUS
   - Rimuovere gli aggiornamenti obsoleti dal database di WSUS

In questo scenario, Configuration Manager non è in grado di eseguire le attività di manutenzione WSUS precedenti per i punti di aggiornamento software remoti usando un database interno di Windows. Questo problema si verifica perché il database interno di Windows non consente le connessioni remote. In `WSyncMgr.log` nel server del sito verranno visualizzati gli errori seguenti:

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

Per risolvere il problema, è possibile automatizzare la manutenzione WSUS per i punti di aggiornamento software remoti usando un database interno di Windows. Per altre informazioni e procedure dettagliate, vedere la [Guida completa alla manutenzione di Microsoft WSUS e dei punti di aggiornamento software di Configuration Manager](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

## <a name="updates-cleanup-log-entries"></a>Voci di log per la pulizia degli aggiornamenti

È possibile verificare la pulizia esaminando le voci seguenti in wsyncmgr.log:

- Il rifiuto degli aggiornamenti sostituiti in WSUS è completato quando è presente la voce di log `Cleanup processed <number> total updates and declined <number>`
- È in corso l'avvio della pulizia WSUS quando è presente la voce `Calling WSUS Cleanup.`
- La pulizia WSUS per gli aggiornamenti scaduti è completata quando è presente la voce `Successfully completed WSUS Cleanup.`
- La pulizia degli elementi di configurazione degli aggiornamenti scaduti di Configuration Manager è stata avviata quando è presente la voce `Deleting old expired updates...`
- La pulizia degli elementi di configurazione degli aggiornamenti scaduti di Configuration Manager è completata quando è presente la voce `Deleted <number> expired updates total`