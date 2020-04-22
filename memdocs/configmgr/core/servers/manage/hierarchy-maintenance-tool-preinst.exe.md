---
title: Strumento di manutenzione gerarchia
titleSuffix: Configuration Manager
description: Informazioni sulle finalità dello strumento di manutenzione gerarchia e motivi per usarlo. Include informazioni di riferimento alle opzioni della riga di comando.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692599"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Strumento di manutenzione gerarchia (Preinst.exe) per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Lo strumento di manutenzione gerarchia (Preinst.exe) passa i comandi alla gestione gerarchie di Configuration Manager mentre il servizio di gestione gerarchie è in esecuzione. Lo strumento di manutenzione gerarchia viene installato automaticamente durante l'installazione di un sito di Configuration Manager. È possibile trovare Preinst.exe nella cartella condivisa \\&lt;*NomeServerSito*>\SMS_&lt;*CodiceSito*\bin\X64\00000409 del server del sito.  

 È possibile utilizzare lo strumento di manutenzione gerarchia nei seguenti scenari:  

-   Quando è richiesto uno scambio di chiavi di sicurezza, ci sono casi in cui è necessario eseguire manualmente lo scambio di chiavi pubbliche iniziale tra siti. Per altre informazioni, vedere la sezione [Scambiare manualmente chiavi pubbliche tra siti](#BKMK_ManuallyExchangeKeys) in questo argomento.  

-   Per rimuovere i processi attivi per un sito di destinazione non più disponibile.  

-   Per eliminare un server del sito dalla console di Configuration Manager quando non si è grado di disinstallare il sito tramite il programma di installazione. Se ad esempio si rimuove fisicamente un sito di Configuration Manager senza prima eseguire il programma di installazione per disinstallare tale sito, le informazioni sul sito rimarranno nel database del sito padre e quest'ultimo continuerà a tentare la comunicazione con il sito figlio. Per risolvere questo problema, è necessario eseguire lo strumento di manutenzione gerarchia ed eliminare manualmente il sito figlio dal database del sito padre.  

-   Per interrompere tutti i servizi di Configuration Manager in un sito senza dover interrompere i servizi uno per uno.  

-   Quando si ripristina un sito, è possibile utilizzare l'opzione CHILDKEYS per distribuire le chiavi pubbliche da più siti figli al sito in corso di ripristino.  

Per eseguire lo strumento di manutenzione gerarchia, l'utente corrente deve disporre dei privilegi amministrativi nel computer locale. L'utente deve inoltre disporre esplicitamente del diritto di sicurezza Amministrazione per il sito. Non è sufficiente che l'utente erediti questo diritto come membro di un gruppo che dispone di questa autorizzazione.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Opzioni della riga di comando dello strumento di manutenzione gerarchia  
Quando si utilizza lo strumento di manutenzione gerarchia, è necessario eseguirlo localmente nel server del sito di amministrazione centrale, del sito primario o del sito secondario.  

Quando si esegue lo strumento di manutenzione gerarchia, è necessario usare la sintassi seguente: preinst.exe /&lt;opzione\>. Di seguito sono elencate le opzioni della riga di comando.  

 **/DELJOB &lt;*CodiceSito*>** : usare questa opzione in un sito per eliminare tutti i processi o i comandi dal sito corrente nel sito di destinazione specificato.  

 **/DELSITE&lt; *CodiceSitoFiglioDaRimuovere*>** : usare questa opzione in un sito padre per eliminare i dati relativi ai siti figlio dal database del sito padre. In genere, è possibile utilizzare questa opzione se si rimuovono le autorizzazioni da un computer del server del sito prima che il sito sia stato disinstallato da tale computer.  

> [!NOTE]  
>  L'opzione /DELSITE non disinstalla il sito nel computer specificato dal parametro ChildSiteCodeToRemove. Questa opzione rimuove solamente le informazioni sul sito dal database del sito di Configuration Manager.  

**/DUMP &lt;*CodiceSito*>** : usare questa opzione nel server del sito locale per scrivere le immagini di controllo del sito nella cartella radice dell'unità in cui è installato il sito. È possibile scrivere un'immagine di controllo del sito specifica nella cartella o scrivere tutti i file di controllo del sito nella gerarchia.  

-   /DUMP &lt;*CodiceSito*> consente di scrivere l'immagine di controllo del sito solo per il sito specificato.  

-   /DUMP consente di scrivere i file di controllo del sito per tutti i siti.  

Un'immagine è una rappresentazione binaria del file di controllo del sito, che è archiviato nel database del sito di Configuration Manager. Il dump dell'immagine del file di controllo del sito è una somma dell'immagine di base e delle immagini differenziali in sospeso.  

Dopo aver eseguito il dump di un'immagine del file di controllo del sito con lo strumento di manutenzione gerarchia, il nome del file avrà il formato seguente: sitectrl_&lt;*CodiceSito*>.ct0.  

**/STOPSITE**: usare questa opzione nel server del sito locale per avviare un ciclo di arresto per il servizio Gestione componenti del sito di Configuration Manager, che reimposta parzialmente il sito. Quando questo ciclo di arresto viene eseguito, alcuni servizi di Configuration Manager nel server del sito e i relativi sistemi del sito remoti vengono arrestati. Questi servizi vengono contrassegnati per la reinstallazione. In seguito a questo ciclo di arresto, alcune password vengono modificate automaticamente quando i servizi vengono reinstallati.  

> [!NOTE]  
>  Se si desidera visualizzare un record per l'arresto, la reinstallazione e le modifiche alle password per Gestione componenti del sito, attivare la registrazione per questo componente prima di utilizzare questa opzione della riga di comando.  

Dopo essere stato avviato, il ciclo di arresto procede automaticamente, ignorando qualsiasi componente o computer che non risponde. Se tuttavia il servizio Gestione componenti del sito non è in grado di accedere a un sistema del sito remoto durante il ciclo di arresto, i componenti installati nel sistema del sito remoto vengono reinstallati quando il servizio Gestione componenti del sito viene riavviato. Quando viene riavviato, il servizio Gestione componenti del sito tenta ripetutamente di reinstallare tutti i servizi contrassegnati per la reinstallazione finché non completa l'operazione.  

È possibile riavviare il servizio Gestione componenti del sito utilizzando Service Manager. Dopo il riavvio, tutti i servizi interessati vengono disinstallati, reinstallati e riavviati. Dopo aver utilizzato l'opzione /STOPSITE per avviare il ciclo di arresto, è impossibile evitare i cicli di reinstallazione dopo che il servizio Gestione componenti del sito viene riavviato.  

**/KEYFORPARENT**: usare questa opzione in un sito per distribuire la chiave pubblica del sito in un sito padre.  

L'opzione /KEYFORPARENT posiziona la chiave pubblica del sito nel file &lt;*CodiceSito*>.CT4 alla radice dell'unità della cartella Programmi. Dopo aver eseguito preinst.exe con questa opzione, copiare manualmente il file &lt;*CodiceSito*>.CT4 nella cartella …\Inboxes\hman.box del sito padre (non hman.box\pubkey).  

**/KEYFORCHILD**: usare questa opzione in un sito per distribuire la chiave pubblica del sito in un sito figlio.  

L'opzione /KEYFORCHILD posiziona la chiave pubblica del sito nel file &lt;*CodiceSito*>.CT5 alla radice dell'unità della cartella Programmi. Dopo aver eseguito preinst.exe con questa opzione, copiare manualmente il file &lt;*CodiceSito*>.CT5 nella cartella …\Inboxes\hman.box del sito figlio (non hman.box\pubkey).  

**/CHILDKEYS**: è possibile usare questa opzione nei siti figlio di un sito in corso di ripristino. Utilizzare questa opzione per distribuire le chiavi pubbliche da più siti figlio nel sito in corso di ripristino.  

L'opzione /CHILDKEYS posiziona la chiave del sito in cui viene eseguita l'opzione e tutte le chiavi pubbliche dei siti figlio di tale sito nel file &lt;*CodiceSito*>.CT6.  

Dopo aver eseguito preinst.exe con questa opzione, copiare manualmente il file &lt;*CodiceSito*>.CT6 nella cartella …\Inboxes\hman.box del sito in corso di ripristino (non hman.box\pubkey).  

**/PARENTKEYS**: è possibile usare questa opzione nel sito padre di cui si sta eseguendo il ripristino. Utilizzare questa opzione per distribuire le chiavi pubbliche da tutti i siti padre nel sito in corso di ripristino.  

L'opzione /PARENTKEYS posiziona la chiave del sito in cui viene eseguita l'opzione e tutte le chiavi di ogni sito padre situato a un livello superiore rispetto a tale sito nel file&lt;CodiceSito\>.CT7.  

Dopo aver eseguito preinst.exe con questa opzione, copiare manualmente il file &lt;*CodiceSito*>.CT7 nella cartella …\Inboxes\hman.box del sito in corso di ripristino (non hman.box\pubkey).  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a> Scambiare manualmente chiavi pubbliche tra siti  
Per impostazione predefinita, l'opzione **Richiedi scambio di chiavi di sicurezza** è attivata per i siti di Configuration Manager. Quando è richiesto uno scambio di chiavi di sicurezza, ci sono due casi in cui è necessario eseguire manualmente lo scambio di chiavi iniziale tra siti:  

-   Lo schema di Active Directory non è stato esteso per Configuration Manager  

-   I siti di Configuration Manager non pubblicano i dati del sito in Active Directory  

È possibile utilizzare lo strumento di manutenzione gerarchia per esportare le chiavi pubbliche per ogni sito. Dopo che sono state esportate, è necessario scambiare manualmente le chiavi tra i siti.  

> [!NOTE]  
>  Dopo che le chiavi pubbliche sono state scambiate manualmente, è possibile esaminare il file di log **hman.log** , che registra le modifiche di configurazione del sito e la pubblicazione delle informazioni sul sito in Servizi di dominio Active Directory nel server del sito padre, per assicurarsi che il sito primario abbia elaborato la nuova chiave pubblica.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Per trasferire manualmente la chiave pubblica del sito figlio nel sito padre  

1.  Durante la connessione al sito figlio, aprire un prompt dei comandi e passare alla posizione di **Preinst.exe**.  

2.  Digitare quanto segue per esportare la chiave pubblica del sito figlio: **Preinst /keyforparent**  

3.  L'opzione /keyforparent posiziona la chiave pubblica del sito figlio nel file **&lt;codice sito\>.CT4** situato alla radice dell'unità di sistema.  

4.  Spostare il file **&lt;codice sito\>.CT4** nella **&lt;directory installazione\>\inboxes\hman.box** del sito padre.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Per trasferire manualmente la chiave pubblica del sito padre nel sito figlio  

1.  Durante la connessione al sito padre, aprire un prompt dei comandi e passare alla posizione di **Preinst.exe**.  

2.  Digitare quanto segue per esportare la chiave pubblica del sito padre: **Preinst /keyforchild**.  

3.  L'opzione /keyforchild posiziona la chiave pubblica del sito padre nel file **&lt;codice sito\>.CT5** alla radice dell'unità di sistema.  

4.  Spostare il file **&lt;codice sito\>.CT5** nella **&lt;directory installazione\>\inboxes\hman.box** del sito figlio.  
