---
title: Configurare le opzioni
titleSuffix: Configuration Manager
description: Configurare le opzioni per l'uso di System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700069"
---
# <a name="configure-options-for-updates-publisher"></a>Configurare opzioni per Updates Publisher

*Si applica a: System Center Updates Publisher*

Rivedere e configurare le opzioni e le impostazioni correlate che influiscono sul funzionamento di Updates Publisher.

Per accedere alle opzioni di Updates Publisher, nell'angolo superiore sinistro della console fare clic sulla scheda **Updates Publisher** **Proprietà** e quindi scegliere **Opzioni**.

![Opzioni](media/properties1.png)   


Le opzioni sono divise nelle categorie seguenti:

-   Server di aggiornamento
-   Server di ConfigMgr
-   Impostazioni proxy
-   Autori attendibili
-   Avanzate
-   Aggiornamenti
-   Registrazione

## <a name="update-server"></a>Server di aggiornamento
Per poter [pubblicare aggiornamenti](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace), è prima necessario configurare Updates Publisher per il funzionamento con server di aggiornamento come WSUS (Windows Server Update Services). Questa operazione include la specifica del server, dei metodi per la connessione a quest'ultimo quando è remoto rispetto alla console e di un certificato da usare per la firma digitale degli aggiornamenti pubblicati.

- **Configurare un server di aggiornamento**. Quando si configura un server di aggiornamento, selezionare il server WSUS di primo livello (server di aggiornamento) nella gerarchia di Configuration Manager, in modo che tutti i siti figlio abbiano accesso agli aggiornamenti pubblicati.

  Se il server di aggiornamento è remoto rispetto al server di Updates Publisher, specificare il nome di dominio completo di tale server e indicare se ci si connette mediante SSL. Quando ci si connette mediante SSL, la porta predefinita passa da 8530 a 8531. Verificare che la porta impostata corrisponda a quella usata dal server di aggiornamento.

  > [!TIP]  
  > Se non si configura un server di aggiornamento, è comunque possibile usare Updates Publisher per creare aggiornamenti software.

- **Configurare il certificato di firma**. Per poter configurare il certificato di firma, è prima necessario configurare e connettersi a un server di aggiornamento.

  Updates Publisher usa il certificato di firma per firmare gli aggiornamenti software che vengono pubblicati nel server di aggiornamento. La pubblicazione ha esito negativo se il certificato digitale non è disponibile nell'archivio certificati del server di aggiornamento o del computer che esegue Updates Publisher.

  Per altre informazioni sull'aggiunta del certificato all'archivio certificati, vedere [Certificates and security for Updates Publisher](updates-publisher-security.md) (Certificati e sicurezza per Updates Publisher).

  Se un certificato digitale non viene rilevato automaticamente per il server di aggiornamento, scegliere una delle operazioni seguenti:

  -   **Sfoglia**: questa opzione è disponibile solo quando il server di aggiornamento è installato nel server in cui si esegue la console. Dopo aver selezionato un certificato, è necessario scegliere **Crea** per aggiungerlo all'archivio certificati WSUS nel server di aggiornamento. Per i certificati selezionati con questo metodo, è necessario immettere la password del file con estensione **pfx**.

  -   **Crea:** usare questa opzione per creare un nuovo certificato. Questa opzione aggiunge anche il certificato all'archivio certificati WSUS nel server di aggiornamento.

  **Se si crea un certificato di firma personalizzato**, eseguire le operazioni di configurazione seguenti:

  -   Abilitare l'opzione **Allow private key to be exported** (Rendi la chiave privata esportabile).

  -   Impostare **Utilizzo chiavi** per la firma digitale.

  -   Impostare **Minimum key size** (Dimensioni minime chiave) su un valore uguale o maggiore di 2048 bit.

  Usare l'opzione **Rimuovi** per rimuovere il certificato dall'archivio certificati WSUS. Questa opzione è disponibile quando il server di aggiornamento è locale per la console di Updates Publisher utilizzata o quando si è usato **SSL** per la connessione a un server di aggiornamento remoto.

## <a name="configmgr-server"></a>Server di ConfigMgr
Quando si usa Configuration Manager con Updates Publisher, usare le opzioni seguenti.

-   **Specify the Configuration Manager server** (Specificare il server di Configuration Manager): dopo aver abilitato il supporto per Configuration Manager, specificare la posizione del server del sito di primo livello dalla gerarchia di Configuration Manager. Se tale server è remoto rispetto a Updates Publisher, specificare il nome di dominio completo del server del sito. Scegliere **Verifica connessione** per verificare che sia possibile connettersi al server del sito.

-   **Configure thresholds** (Configura soglie): le soglie vengono usate quando si pubblicano gli aggiornamenti con un tipo di pubblicazione automatico. I valori delle soglie consentono di determinare quando viene pubblicato l'intero contenuto di un aggiornamento anziché solo i metadati. Per altre informazioni sui tipi di pubblicazione, vedere [Assign updates to a publication](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) (Assegnare aggiornamenti a una pubblicazione)

    È possibile usare una o entrambe le soglie seguenti:

    -   **Requested client count threshold** (Soglia numero di client con richiesta): definisce il numero di client che devono richiedere un aggiornamento prima che Updates Publisher sia in grado di pubblicare automaticamente il set completo di contenuto per l'aggiornamento. Fino a quando il numero di client specificato non richiede l'aggiornamento, vengono pubblicati solo i metadati degli aggiornamenti.

    -   **Package source size threshold (MB)** (Soglia dimensioni di origine del pacchetto (MB)): questa soglia impedisce la pubblicazione automatica di aggiornamenti che superano le dimensioni specificate. Se la dimensione degli aggiornamenti supera questo valore, vengono pubblicati solo i metadati. Il contenuto degli aggiornamenti di dimensioni minori di quelle specificate può essere pubblicato per intero.

## <a name="proxy-settings"></a>Impostazioni proxy
Updates Publisher usa impostazioni proxy quando si importano cataloghi del software da Internet o si pubblicano aggiornamenti in Internet.

-   Immettere il nome di dominio completo o l'indirizzo IP di un server proxy. IPv4 e IPv6 sono entrambi supportati.

-   Se il server proxy autentica gli utenti per l'accesso a Internet, è necessario specificare il nome Windows. I nomi UPN (Universal Principle Name) non sono supportati.

## <a name="trusted-publishers"></a>Autori attendibili
Quando si importa un catalogo di aggiornamenti, l'origine di tale catalogo (in base al relativo certificato) viene aggiunta come autore attendibile. Analogamente, quando si pubblica un aggiornamento, l'origine del certificato degli aggiornamenti viene aggiunto come autore attendibile.

È possibile visualizzare i dettagli per ogni autore e rimuovere un auore dall'elenco degli autori attendibili.

Il contenuto offerto da autori considerati non attendibili può potenzialmente danneggiare i computer client durante la ricerca di aggiornamenti. È consigliabile accettare contenuto solo da autori attendibili.

## <a name="advanced"></a>Avanzate
Le opzioni avanzate includono le seguenti:

-   **Repository location** (Percorso repository): visualizzare e modificare il percorso del file di database, **scupdb.sdf**. Questo file funge da repository per Updates Publisher.

-   **Timestamp:** quando questa opzione è abilitata, agli aggiornamenti firmati viene aggiunto un timestamp che indica il momento della firma. Un aggiornamento firmato durante il periodo di validità di un certificato di firma può essere usato anche dopo la scadenza di tale certificato. Per impostazione predefinita, non è possibile distribuire aggiornamenti software dopo la scadenza del relativo certificato di firma.

-   **Check for updates to subscribed catalogs** (Verifica disponibilità di aggiornamenti dei cataloghi sottoscritti): ogni volta che viene avviato, Updates Publisher può verificare automaticamente la disponibilità di aggiornamenti per i cataloghi a cui è stata eseguita la sottoscrizione. Quando viene rilevato un aggiornamento di un catalogo, vengono offerti dettagli sotto forma di **Avvisi recenti** nella finestra **Panoramica** dell'**area di lavoro Aggiornamenti**.

-   **Certificate revocation** (Revoca certificati): scegliere questa opzione per abilitare i controlli di revoca dei certificati.

-   **Local source publishing** (Pubblicazione origine locale: Updates Publisher può usare una copia locale di un aggiornamento in fase di pubblicazione prima del download di tale aggiornamento da Internet. La posizione deve essere una cartella sul computer che esegue Updates Publisher. Per impostazione predefinita, il percorso è **Documenti\LocalSourcePublishing.** Usare questo percorso quando in precedenza sono stati scaricati uno o più aggiornamenti o sono state apportate modifiche a un aggiornamento che si vuole distribuire.

-   **Pulizia guidata aggiornamenti software**: avviare la Pulizia guidata aggiornamenti software. La procedura guidata imposta come scaduti gli aggiornamenti che si trovano sul server di aggiornamento ma non nel repository di Updates Publisher. Per altri dettagli vedere [Impostare come scaduti gli aggiornamenti senza riferimenti](#expire-unreferenced-software-updates).

## <a name="updates"></a>Aggiornamenti
 A ogni avvio, Updates Publisher può verificare automaticamente la presenza di nuovi aggiornamenti. È inoltre possibile scegliere di ricevere versioni di anteprima di Updates Publisher.

Per verificare manualmente la presenza di aggiornamenti, nella console di Updates Publisher fare clic su ![Proprietà](media/properties2.png)  
per aprire **Updates Publisher Properties** (Proprietà Updates Publisher), quindi scegliere **Check for update** (Controlla aggiornamenti).

Quando individua un nuovo aggiornamento, Updates Publisher visualizza la finestra **Aggiornamento disponibile**. A questo punto è possibile scegliere di installare l'aggiornamento. Se si sceglie di non procedere all'installazione, l'aggiornamento viene offerto alla successiva apertura della console.

## <a name="logging"></a>Registrazione
Updates Publisher registra le informazioni di base su Updates Publisher in **%WINDIR%\Temp\UpdatesPublisher.log**.

Usare il blocco note o **CMTrace** per visualizzare il log. CMTrace è lo strumento dei file di log di Configuration Manager ed è disponibile nella cartella **\SMSSetup\Tools** del supporto di origine di Configuration Manager.

È possibile modificare le dimensioni e il livello di dettaglio del log.

Quando si abilita la registrazione del database, vengono incluse informazioni sulle query eseguite nel database di Updates Publisher. L'uso della registrazione del database può causare una riduzione delle prestazioni del computer su cui viene eseguito Updates Publisher.

Per visualizzare il file di log, nella console fare clic su ![Proprietà](media/properties2.png) per aprire **Updates Publisher Properties** (Proprietà Updates Publisher), quindi scegliere **View log file** (Visualizza file di log).

## <a name="expire-unreferenced-software-updates"></a>Impostare come scaduti gli aggiornamenti senza riferimenti
È possibile eseguire la **Pulizia guidata aggiornamenti software** per impostare come scaduti gli aggiornamenti che si trovano sul server di aggiornamento ma non nel repository di Updates Publisher. Viene inviata una notifica a Configuration Manager, che rimuove tali aggiornamenti per impedirne future distribuzioni.

L'impostazione di un aggiornamento come scaduto non può essere annullata. Eseguire questa operazione solo quando si ha la certezza che gli aggiornamenti software selezionati non sono più necessari per l'organizzazione.

### <a name="to-remove-expired-software-updates"></a>Per rimuovere gli aggiornamenti software scaduti
1.  Nella console di Updates Publisher fare clic su ![Proprietà](media/properties2.png) per aprire **Updates Publisher Properties** (Updates Publisher Properties), quindi scegliere **Opzioni**.

2.  Scegliere **Avanzate**, quindi, nella **Pulizia guidata aggiornamenti software**, scegliere **Avvia**.

3.  Selezionare gli aggiornamenti software che si vogliono impostare come scaduti e quindi scegliere **Avanti**.

4.  Dopo aver esaminato le selezioni, scegliere **Avanti** per accettarle e impostare come scaduti gli aggiornamenti.

5.  Al termine, scegliere **Chiudi** per completare la procedura guidata.
