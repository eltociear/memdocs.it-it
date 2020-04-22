---
title: Creare condizioni globali
titleSuffix: Configuration Manager
description: È possibile creare condizioni globali per specificare la modalità in cui un'applicazione viene resa disponibile e distribuita nei dispositivi client.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689539"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Come creare condizioni globali in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager le condizioni globali sono regole che rappresentano le condizioni tecniche o aziendali che l'utente può usare per specificare il modo in cui un'applicazione viene distribuita e resa disponibile per i dispositivi client. Le condizioni globali sono accessibili dalla pagina **Requisiti** della Creazione guidata tipo di distribuzione.  

> [!NOTE]  
>  È possibile modificare le condizioni globali solo dal sito in cui sono state create.  

 Usare le procedure seguenti per creare le condizioni globali di Configuration Manager.  

## <a name="provide-basic-information-about-the-global-condition"></a>Fornire informazioni di base sulla condizione globale  
 Sono disponibili diversi tipi di condizioni globali. Opzioni diverse sono associate a diversi tipi di condizione globale. Quando si seleziona un tipo specifico di condizione globale, Configuration Manager visualizza le opzioni che si applicano a quella selezione.  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Condizioni globali**.  

3.  Nel gruppo **Crea** della scheda **Home** scegliere **Crea condizione globale**.  

4.  Nella finestra di dialogo **Crea condizione globale** , fornire un nome e una descrizione opzionale per la condizione globale.  

5.  Nell'elenco a discesa **Tipo di dispositivo** scegliere se la condizione globale è per un computer **Windows** o un dispositivo **Windows Mobile**.  

6.  Nell'elenco a discesa **Tipo di condizione** , scegliere una delle seguenti opzioni:  

    -   **Impostazione** : questa opzione consente di controllare l'esistenza di uno o più elementi su dispositivi client. È ad esempio possibile controllare la presenza di un file, di una cartella o di un valore della chiave del Registro di sistema in un dispositivo client.  

    -   **Espressione**: questa opzione consente di configurare regole più complesse per controllare se la condizione viene soddisfatta su dispositivi client. È ad esempio possibile controllare se la memoria fisica di un computer è tra 2 GB e 4 GB oppure se un dispositivo mobile usa un touch-screen per l'input.  

## <a name="set-up-rules-for-the-global-condition"></a>Configurare le regole per la condizione globale  
 La procedura per la definizione delle regole per le condizioni globali è diversa a seconda che si tratti della configurazione di un'impostazione o di un'espressione. Usare la procedura applicabile presentata di seguito per configurare un'impostazione o un'espressione per la condizione globale.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Per configurare un'impostazione per la condizione globale  

1. Nell'elenco a discesa **Tipo di condizione** , scegliere **Impostazione**.  

2. Nell'elenco a discesa **Tipo di impostazione** , scegliere l'elemento da utilizzare come condizione per cui verranno controllati i requisiti. Sono disponibili i seguenti tipi di impostazione e configurazione.  

   - **Query Active Directory**  

     -   **Prefisso LDAP** : specificare un prefisso LDAP valido per la query Servizi di dominio Active Directory per valutare la conformità nei computer client. È possibile usare **LDAP://** o **GC://** .  

     -   **Nome distinto (DN)** : specificare il nome distinto dell'oggetto Active Directory Domain Services di cui verrà valutata la conformità nei computer client.  

     -   **Filtro di ricerca** : specificare un filtro LDAP opzionale per rifinire i risultati derivanti dalla query Servizi di dominio Active Directory per valutare la conformità nei computer client.  

     -   **Ambito di ricerca** : specificare l'ambito di ricerca in Servizi di dominio Active Directory:  

         -   **Base**: esegue una query solo dell'oggetto specificato.  

         -   **Un livello**: questa opzione non è usata in questa versione di Configuration Manager.  

         -   **Sottoalbero**: esegue una query dell'oggetto specificato e il relativo sottoalbero completo nella directory.  

     -   **Proprietà** : specificare la proprietà dell'oggetto Servizi di dominio Active Directory che sarà utilizzato per valutare la conformità nei computer client.  

     -   **Query** : visualizza la query LDAP creata dalle voci in **Prefisso LDAP**, **Nome distinto (DN)** , **Filtro di ricerca** se specificati e **Proprietà**. Questa query verrà utilizzata per valutare la conformità nei computer client.  

   - **Assembly**  

     -   **Nome assembly** : specifica il nome dell'oggetto assembly da cercare. Il nome non può essere lo stesso di un altro oggetto assembly dello stesso tipo e deve essere registrato nella Global Assembly Cache. Il nome dell'assembly può contenere un massimo di 256 caratteri.  

     > [!NOTE]  
     >  Un assembly è una porzione di codice che può essere condivisa tra applicazioni. I nomi file degli assembly possono avere estensione dll o exe. La cache di assembly globale è una cartella denominata *%systemroot%\assembly* nei computer client in cui sono memorizzati tutti gli assembly condivisi.  

   - **File system**  

     - **Tipo**: dall'elenco a discesa selezionare se si vuole effettuare la ricerca di un **File** o di una **Cartella**.  

     - **Percorso** : specificare il percorso al file o alla cartella specificati nei computer client. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente *%USERPROFILE%* nel percorso.  

       > [!NOTE]  
       >  Se si utilizza la variabile di ambiente *%USERPROFILE%* nei campi **Percorso** o **Nome file o cartella** , verrà effettuata la ricerca di tutti i profili utente sui computer client. Ciò potrebbe causare l'individuazione di più istanze del file o della cartella.  

     - **Nome file o cartella** : specificare il nome dell'oggetto file o cartella di cui verrà effettuata la ricerca. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente *%USERPROFILE%* nel nome file o cartella. Nel nome del file è anche possibile usare i caratteri jolly * e ?.  

       > [!NOTE]  
       >  Se si specifica un nome file o cartella e si utilizzano dei caratteri jolly, ciò potrebbe produrre un numero elevato di risultati. Questo potrebbe portare a un uso elevato delle risorse nei computer client e a un intenso traffico di rete quando si segnalano i risultati a Configuration Manager.  

     - **Includi sottocartelle** : abilitare questa opzione se si desidera effettuare la ricerca anche nelle sottocartelle nel percorso specificato.  

     - **Il file o la cartella sono associati a un'applicazione a 64 bit**: scegliere se effettuare la ricerca anche nel percorso dei file del sistema a 64 bit ( *%windir%* \system32), oltre al percorso dei file del sistema a 32 bit ( *%windir%* \syswow64) nei client di Configuration Manager con una versione a 64 bit di Windows.  

       > [!NOTE]  
       >  Se nel percorso dei file del sistema a 64 e 32 bit sullo stesso computer a 64 bit esiste lo stesso file o cartella, la condizione globale individuerà più file.  

       Il tipo di impostazione **File system** non supporta la specificazione di un percorso UNC in una condivisione di rete nel campo **Percorso** .  

   - **Metabase IIS**  

     -   **Percorso metabase** : specificare un percorso valido per la metabase IIS.  

     -   **ID proprietà** : specificare la proprietà numerica dell'impostazione della metabase IIS.  

   - **Chiave del Registro di sistema**  

     -   **Hive**: dall'elenco a discesa scegliere l'hive del Registro di sistema in cui si vuole effettuare la ricerca.  

     -   **Chiave** : specificare il nome della chiave del Registro di sistema in cui si desidera effettuare la ricerca. Il formato utilizzato deve essere *key\subkey*.  

     -   **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit** : consente di specificare se effettuare la ricerca anche tra le chiavi del Registro di sistema a 64 bit, oltre alle chiavi del Registro di sistema a 32 bit su client con una versione a 64 bit di Windows.  

         > [!NOTE]  
         >  Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individuerà più chiavi del Registro di sistema.  

   - **Valore del Registro di sistema**  

     -   **Hive** : dall'elenco a discesa, selezionare l'hive del Registro di sistema in cui si desidera effettuare la ricerca.  

     -   **Chiave** : specificare il nome della chiave del Registro di sistema in cui si desidera effettuare la ricerca. Il formato utilizzato deve essere *key\subkey*.  

     -   **Valore** : specificare il valore che deve essere contenuto all'interno della chiave del Registro di sistema specificato.  

     -   **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit** : consente di specificare se effettuare la ricerca anche tra le chiavi del Registro di sistema a 64 bit, oltre alle chiavi del Registro di sistema a 32 bit su client con una versione a 64 bit di Windows.  

         > [!NOTE]  
         >  Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individuerà più chiavi del Registro di sistema.  

   - **Script**  

     -   **Script di individuazione**: scegliere **Aggiungi** per immetterne uno oppure selezionare lo script da usare. È possibile usare script di Windows PowerShell, VBScript o JScript.  

     -   **Esegui script utilizzando le credenziali dell'utente connesso**: se si abilita questa opzione, lo script verrà eseguito nei computer client usando le credenziali dell'utente connesso.  

         > [!NOTE]  
         >  Il valore restituito dallo script verrà utilizzato per valutare la conformità della condizione globale. Ad esempio, quando si usa VBScript, si può usare il comando **WScript.Echo Risultato** per restituire il valore della variabile Risultato alla condizione globale.  
         >   
         >  Se lo script restituisce più valori, questi valori devono trovarsi su una singola riga, separati dal punto e virgola. Se ogni valore si trova su una riga distinta, la valutazione avrà esito negativo.  

   - **Query SQL**  

     -   **Istanza SQL Server** : scegliere se si desidera che la query SQL venga eseguita sul nome dell'istanza predefinita, di tutte le istanze o dell'istanza di un database specifico.  

         > [!NOTE]  
         >  Il nome dell'istanza deve fare riferimento a un'istanza locale di SQL Server. Per fare riferimento a un'istanza di SQL server del cluster, è necessario utilizzare un'impostazione script.  

     -   **Database** : specificare il nome del database di Microsoft SQL Server per cui verrà eseguita la query SQL.  

     -   **Colonna** : specificare il nome della colonna restituito dall'istruzione Transact-SQL da utilizzare per valutare la conformità della condizione globale.  

     -   **Istruzione Transact-SQL** : specificare la query SQL completa da utilizzare per la condizione globale. È anche possibile scegliere **Apri** per aprire una query SQL esistente.  

   - **Query WQL**  

     -   **Spazio dei nomi** : specificare lo spazio dei nomi WMI che sarà utilizzato per costruire una query WQL che verrà valutata per la conformità nei computer client. Il valore predefinito è Root\cimv2.  

     -   **Classe** : specificare la classe WMI che sarà utilizzata per costruire una query WQL che verrà valutata per la conformità nei computer client.  

     -   **Proprietà** : specificare la proprietà WMI che sarà utilizzata per costruire una query WQL che verrà valutata per la conformità nei computer client.  

     -   **Clausola WHERE della query WQL** : è possibile utilizzare l'elemento **Clausola WHERE della query WQL** per specificare una clausola WHERE da applicare allo spazio dei nomi, alla classe e alla proprietà specifici nei computer client.  

   - **Query XPath**  

     -   **Percorso** : specificare il percorso del file XML nei computer client che verrà usato per valutare la conformità. Configuration Manager supporta l'uso di tutte le variabili di ambiente di sistema Windows e la variabile utente *%USERPROFILE%* nel nome del percorso.  

     -   **Nome file XML**: specificare il nome file che contiene la query XML da usare per valutare la conformità nei computer client.  

     -   **Includi sottocartelle** : abilitare questa opzione se si desidera effettuare la ricerca anche nelle sottocartelle nel percorso specificato.  

     -   **Il file è associato a un'applicazione a 64 bit**: scegliere se effettuare la ricerca anche nel percorso dei file del sistema a 64 bit ( *%windir%* \system32), oltre al percorso dei file del sistema a 32 bit ( *%windir%* \syswow64) nei client di Configuration Manager con una versione a 64 bit di Windows.  

     -   **Query XPath** : specificare una query XPath valida e completa da utilizzare per valutare la conformità nei computer client.  

     -   **Spazi dei nomi** : aprire la finestra di dialogo **Spazi dei nomi XML** per individuare gli spazi dei nomi e i prefissi da utilizzare durante la query XPath.  

3. Nell'elenco a discesa **Tipo di dati** , scegliere il formato in cui i dati verranno restituiti dalla condizione prima di essere utilizzato per controllare i requisiti.  

   > [!NOTE]  
   >  L'elenco a discesa **Tipo di dati** non viene visualizzato per tutti i tipi di impostazioni.  

4. Configurare altri dettagli relativi a questa impostazione nell'elenco a discesa **Tipo di impostazione**. Gli elementi che è possibile configurare variano a seconda del tipo di impostazione selezionato.  

5. Scegliere **OK** per salvare la regola e chiudere la finestra di dialogo **Crea condizione globale**.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Configurare un'espressione per la condizione globale  

1.  Nell'elenco a discesa **Tipo di condizione** , scegliere **Espressione**.  

2.  Scegliere **Aggiungi clausola** per aprire la finestra di dialogo **Aggiungi clausola**.  

3.  Dall'elenco a discesa **Seleziona categoria** , selezionare se l'espressione è per un utente o un dispositivo. In alternativa, selezionare **Personalizzata** per utilizzare una condizione globale configurata in precedenza.  

4.  Dall'elenco a discesa **Seleziona una condizione** , selezionare la condizione da utilizzare per valutare se l'utente o il dispositivo soddisfano i requisiti della regola. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

5.  Dall'elenco a discesa **Scegli operatore** , scegliere l'operatore da utilizzare per confrontare la condizione selezionata con il valore specificato per valutare se l'utente o il dispositivo soddisfano i requisiti della regola. Gli operatori disponibili variano a seconda della condizione selezionata.  

6.  Nel campo **Valore** , specificare i valori da utilizzare con la condizione e l'operatore selezionati per valutare se l'utente o il dispositivo soddisfano i requisiti della regola. I valori disponibili variano a seconda della condizione e dell'operatore selezionati.  

7.  Scegliere **OK** per salvare l'espressione e per chiudere la finestra di dialogo **Aggiungi clausola**.  

8.  Quando si è terminato di aggiungere clausole alla condizione globale, scegliere **OK** per chiudere la finestra di dialogo **Crea condizione globale** e per salvare la condizione globale.  
