---
title: Assegnare client a un sito
titleSuffix: Configuration Manager
description: Assegnare i client a un sito in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32944157759e537c5b01061ab8648f242cfdac57
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693569"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Come assegnare i client a un sito in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo l'installazione di un client di Configuration Manager, è necessario aggiungerlo a un sito primario di Configuration Manager perché possa essere gestito. Il sito a cui si aggiunge il client viene definito come *sito assegnato*. I client non possono essere assegnati a un sito di amministrazione centrale o a un sito secondario.  

Il processo di assegnazione si verifica dopo che il client è stato installato correttamente e determina il sito che gestisce il computer client. È possibile assegnare il client direttamente a un sito oppure usare l'assegnazione sito automatica in cui il client individua automaticamente un sito appropriato sulla base del suo attuale percorso di rete o un sito di fallback configurato per la gerarchia.

Quando si installa il client del dispositivo mobile durante la registrazione di Configuration Manager, il dispositivo viene sempre assegnato automaticamente a un sito. Quando si installa il client in un computer, è possibile scegliere se assegnare il client a un sito oppure no. Tuttavia, quando il client viene installato ma non assegnato, non è gestito fino al corretto completamento dell'assegnazione.  
 

> [!NOTE]  
>  Assegnare sempre i client a siti che eseguono la stessa versione di Configuration Manager. Evitare di assegnare un client di Configuration Manager di una versione più recente a un sito di una versione precedente.   Se necessario, aggiornare il sito primario alla stessa versione di Configuration Manager in uso per i client.  

Una volta assegnato a un sito, il client vi rimane assegnato, anche se cambia indirizzo IP e si sposta in un altro sito. Solo un amministratore potrà assegnare manualmente il client a un altro sito o rimuovere l'assegnazione del client.  

> [!WARNING]  
>  Un'eccezione alla condizione in cui il client rimane assegnato a un sito riguarda il caso di assegnazione del client su un dispositivo con Windows Embedded quando i filtri di scrittura sono abilitati. Se i filtri di scrittura non vengono disabilitati prima dell'assegnazione del client, lo stato di assegnazione sito del client tornerà alla sua versione originale al successivo riavvio del dispositivo.  
>   
>  Ad esempio, se il client è configurato per l'assegnazione sito automatica, sarà riassegnato all'avvio, eventualmente a un sito differente. Se il client non è configurato per l'assegnazione automatica ai siti ma richiede un'assegnazione manuale, è necessario riassegnarlo manualmente dopo l'avvio per poterlo gestire nuovamente tramite Configuration Manager.  
>   
>  Per evitare tale comportamento, disabilitare i filtri di scrittura prima di assegnare il client su dispositivi incorporati, quindi abilitare i filtri di scrittura dopo aver verificato che il sito sia stato assegnato correttamente.  

Se non è possibile completare l'assegnazione del client al sito, il software client rimarrà installato ma non sarà gestito. Un client è considerato non gestito quando viene installato ma non assegnato a un sito, oppure quando viene assegnato a un sito ma non è in grado di comunicare con un punto di gestione.  

##  <a name="using-manual-site-assignment-for-computers"></a>Utilizzo dell'assegnazione manuale del sito per i computer  
 È possibile assegnare manualmente i computer client a un sito utilizzando i due metodi seguenti:  

-   Utilizzare una proprietà di installazione client che specifichi il codice del sito.  

-   Nel Pannello di controllo, in **Configuration Manager**, specificare il codice del sito.  

> [!NOTE]  
>  Se si assegna manualmente un computer client a un codice sito di Configuration Manager inesistente, l'assegnazione al sito avrà esito negativo.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> Utilizzo dell'assegnazione automatica del sito per i computer  
 L'assegnazione automatica del sito può verificarsi durante la distribuzione client o quando si seleziona **Trova sito** nella scheda **Avanzate** delle **Proprietà di Configuration Manager** nel Pannello di controllo. Il client di Configuration Manager confronta il proprio percorso di rete con i limiti configurati nella gerarchia di Configuration Manager. Se il percorso di rete del client rientra in un gruppo di limiti abilitato per l'assegnazione del sito, oppure la gerarchia è configurata per un sito di fallback, il client viene automaticamente assegnato a tale sito senza dover specificare un codice del sito.  

 È possibile configurare i limiti utilizzando uno o più degli elementi seguenti:  

-   Subnet IP  

-   Sito di Active Directory  

-   Prefisso IP v6  

-   Intervallo indirizzi IP  

> [!NOTE]  
>  Se un client di Configuration Manager ha più schede di rete e di conseguenza più indirizzi IP, l'indirizzo IP usato per l'assegnazione al sito di un client a scopo di valutazione viene assegnato in modo casuale.  

 Per informazioni su come configurare gruppi di limiti per l'assegnazione sito e un sito di fallback per l'assegnazione sito automatica, vedere [Definire i limiti del sito e i gruppi di limiti per Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 I client di Configuration Manager che usano l'assegnazione al sito automatica tentano di individuare i gruppi limite del sito pubblicati in Servizi di dominio Active Directory. Se tale metodo ha esito negativo, se ad esempio lo schema Active Directory non è esteso per Configuration Manager oppure i client sono computer di un gruppo di lavoro, i client possono reperire le informazioni sui gruppi di limiti da un punto di gestione.  

 È possibile specificare un punto di gestione che i computer client possono utilizzare al momento dell'installazione, oppure i client possono individuare un punto di gestione tramite pubblicazione DNS o WINS.  

 Se il client non è in grado di rilevare un sito associato a un gruppo di limiti contenente il relativo percorso di rete, e non è presente un sito di fallback nella gerarchia, il client eseguirà dei tentativi a intervalli di 10 minuti fino a quando non sarà assegnato a un sito.  

 I computer client di Configuration Manager non possono essere assegnati automaticamente a un sito nei seguenti casi, per i quasi sarà invece necessaria un'assegnazione manuale:  

-   Sono attualmente assegnati a un sito.  

-   Si trovano su Internet o sono configurati come client Internet esclusivi.  

-   Il relativo percorso di rete non rientra in uno dei gruppi di limiti configurati nella gerarchia di Configuration Manager e non è presente alcun sito di fallback per la gerarchia.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Completamento dell'assegnazione del sito tramite controllo della compatibilità del sito  
 Dopo che un client ha individuato il sito assegnato, vengono controllati sistema operativo e versione del client per verificare che quest'ultimo possa essere gestito da un sito di Configuration Manager. Ad esempio, Configuration Manager non può gestire i client di Configuration Manager 2007, i client di System Center 2012 Configuration Manager o i client che eseguono Windows 2000.  

 L'assegnazione al sito ha esito negativo se un client che esegue Windows 2000 viene assegnato a un sito di Configuration Manager. Quando si assegna un client di Configuration Manager 2007 o di System Center 2012 Configuration Manager a un sito di Configuration Manager (Current Branch), l'assegnazione ha esito positivo per il supporto dell'aggiornamento automatico del client. Tuttavia, finché i client di generazione precedente non vengono aggiornati a un client di Configuration Manager (ramo corrente), Configuration Manager non riuscirà a gestire questo client usando le impostazioni, le applicazioni o gli aggiornamenti software del client.  

> [!NOTE]  
>  Per supportare l'assegnazione di un client di Configuration Manager 2007 o di System Center 2012 Configuration Manager a un sito di Configuration Manager (ramo corrente), è necessario configurare l'aggiornamento automatico del client per la gerarchia. Per altre informazioni, vedere [Come aggiornare i client per i computer Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager controlla anche che il client di Configuration Manager (ramo corrente) sia stato assegnato a un sito che lo supporta. Durante la migrazione da versioni precedenti di Configuration Manager potrebbero verificarsi gli scenari seguenti.  

- Scenario: è stata usata l'assegnazione al sito automatica e i limiti si sovrappongono ai limiti definiti in una versione precedente di Configuration Manager.  

   In questo caso il client prova a rilevare automaticamente un sito di Configuration Manager (Current Branch).  

   Il client esegue prima un controllo in Servizi di dominio Active Directory e, se rileva un sito di Configuration Manager (ramo corrente) pubblicato, l'assegnazione al sito riesce. In caso contrario, ad esempio se il sito di Configuration Manager non è pubblicato o il computer è un client di un gruppo di lavoro, il client verificherà la presenza di informazioni del sito dal punto di gestione assegnato.  

  > [!NOTE]  
  >  È possibile assegnare un punto di gestione al client durante l'installazione del client usando la proprietà Client.msi **SMSMP=&lt;nome_server>** .  

   Se entrambi i metodi hanno esito negativo, si verifica un errore di assegnazione del sito ed è necessario assegnare il client manualmente.  

- Scenario: il client di Configuration Manager (Current Branch) è stato assegnato usando un codice sito specifico anziché l'assegnazione automatica, ma è stato erroneamente specificato un codice sito per una versione di Configuration Manager precedente System Center 2012 R2 Configuration Manager.  

   In questo caso l'assegnazione al sito non riesce ed è necessario riassegnare il client manualmente a un sito di Configuration Manager (ramo corrente).  

  Il controllo di compatibilità del sito richiede una delle seguenti condizioni:  

- Il client può accedere alle informazioni del sito pubblicate in Servizi di dominio Active Directory.  

- Il client può comunicare con un punto di gestione nel sito.  

  Se la verifica compatibilità del sito non viene completata correttamente, l'assegnazione al sito avrà esito negativo e il client resterà non gestito fino a quando tale verifica non verrà completata correttamente durante la successiva esecuzione.  

  L'eccezione all'esecuzione del controllo di compatibilità del sito riguarda il caso in cui un client venga configurato per un punto di gestione basato su Internet. In questo scenario non viene effettuata alcuna verifica compatibilità del sito. Se si stanno assegnando dei client a un sito contenente sistemi basati su Internet e si specifica un punto di gestione basato su Internet, assicurarsi che il client sia assegnato al sito corretto. Se si assegna erroneamente il client a un sito di Configuration Manager 2007, un sito di System Center 2012 Configuration Manager o un sito di Configuration Manager che non dispone di ruoli del sistema del sito basati su Internet, il client sarà non gestito.  

##  <a name="locating-management-points"></a>Individuazione dei punti di gestione  
 Dopo che un client viene assegnato a un sito, individua un punto di gestione all'interno del sito.  

 I computer client scaricano un elenco dei punti di gestione del sito ai quali possono connettersi. Questo processo si verifica a ogni riavvio del client, oppure ogni 25 ore o se il client rileva una modifica della rete, come la disconnessione e la riconnessione del computer alla rete o la ricezione di un nuovo indirizzo IP da parte del computer. L'elenco include i punti di gestione della intranet e indica la relativa eventuale accettazione di connessioni client tramite HTTP o HTTPS. Quando il computer client si trova su Internet e non dispone ancora di un elenco di punti di gestione, si connette al punto di gestione basato su Internet specificato per ottenere tale elenco. Quando il client dispone di un elenco dei punti di gestione per il sito assegnato, ne seleziona uno a cui connettersi:  

-   Quando il client si trova sulla intranet e dispone di un certificato PKI valido da utilizzare, sceglie i punti di gestione HTTPS prima di quelli HTTP. Individua quindi il punto di gestione più vicino in base all'appartenenza alla relativa foresta.  

-   Quando il client si trova su Internet, sceglie in modo casuale uno dei punti di gestione basati su Internet.  

I client dei dispositivi mobili registrati da Configuration Manager si connettono solo a un punto di gestione nel relativo sito assegnato e non si connettono mai ai punti di gestione nei siti secondari. Questi client si connettono sempre tramite HTTPS e il punto di gestione deve essere configurato per l'accettazione delle connessioni client su Internet. In presenza di più di un punto di gestione per i client dei dispositivi mobili nel sito primario, Configuration Manager ne sceglie uno in modo casuale durante l'assegnazione e il client del dispositivo mobile continua a usare lo stesso punto di gestione.  

Una volta scaricati i criteri client da un punto di gestione nel sito, il client diventa gestito.  

##  <a name="downloading-site-settings"></a>Download delle impostazioni del sito  
 Al termine dell'assegnazione del sito e dopo che il client ha rilevato un punto di gestione, un computer client che utilizza Servizi di dominio Active Directory per il relativo controllo di compatibilità del sito scarica le impostazioni del sito relative al client per il sito assegnato. Tali impostazioni includono i criteri di selezione del certificato client, l'opzione per l'utilizzo di un elenco di revoche di certificati e i numeri porta di richiesta client. Il client continuerà a controllare queste impostazioni su base periodica.  

 Quando i computer client non sono in grado di ottenere le impostazioni del sito da Servizi di dominio Active Directory, le scaricano dal proprio punto di gestione. I computer client possono ottenere tali impostazioni anche quando vengono installati tramite installazione push client oppure quando vengono specificate manualmente usando le proprietà di installazione client e CCMSetup.exe. Per altre informazioni su queste proprietà di installazione del client, vedere [Informazioni sui parametri e le proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Download delle impostazioni client  
 Tutti i client scaricano i criteri delle impostazioni client predefinite nonché qualsiasi criterio delle impostazioni client personalizzate applicabile. Software Center si basa su questi criteri di configurazione client per i computer Windows e comunica agli utenti che non potrà essere eseguito correttamente finché tali informazioni di configurazione non saranno scaricate. A seconda delle impostazioni client configurate, il download iniziale potrebbe richiedere qualche istante e alcune attività di gestione client potrebbero non essere eseguite fino al completamente del processo.  

##  <a name="verifying-site-assignment"></a>Verifica dell'assegnazione del sito  
 È possibile verificare l'esito dell'assegnazione del sito usando uno dei metodi seguenti:  

-   Per i client su computer Windows, usare Configuration Manager nel Pannello di controllo e verificare che il codice del sito sia visualizzato correttamente nella scheda **Sito**.  

-   Per i computer client, nell'area di lavoro **Asset e conformità** > nodo **Dispositivi** verificare che il computer visualizzi **Sì** per la colonna **Client** e il codice sito primario corretto per la colonna **Codice sito**.  

-   Per i client dispositivo mobile, nell'area di lavoro **Asset e conformità** utilizzare la raccolta **Tutti i dispositivi mobili** per verificare che il dispositivo mobile visualizzi **Sì** per la colonna **Client** e il codice sito primario corretto per la colonna **Codice sito** .  

-   Utilizzare i report per l'assegnazione del client e la registrazione del dispositivo mobile.  

-   Per i computer client, utilizzare il file LocationServices.log nel client.  

##  <a name="roaming-to-other-sites"></a>Roaming in altri siti  
 Quando i computer client nella Intranet sono assegnati a un sito primario ma cambiano percorso di rete così da ricadere in un gruppo di limiti configurato per un altro sito, vanno in roaming in un altro sito. Quando tale sito è un sito secondario del sito loro assegnato, i client possono utilizzare un punto di gestione nel secondario per scaricare criteri client e caricare dati client, evitando così di trasmettere tali dati in una rete potenzialmente lenta. I client che eseguono il roaming nei limiti di un altro sito primario o di un secondario che non è un sito figlio del sito loro assegnato utilizzano comunque sempre un punto di gestione nel sito loro assegnato per scaricare criteri client e caricare dati nel proprio sito.  

 I computer client che eseguono il roaming in altri siti (tutti i siti primari e tutti i siti secondari) possono sempre utilizzare i punti di gestione in altri siti per le richieste di percorso dei contenuti. I punti di gestione del sito corrente possono fornire ai client un elenco dei punti di distribuzione che dispongono dei contenuti richiesti dai client.  

 Per i computer client configurati per la gestione client basata solo su Internet e per i dispositivi mobili e i computer Mac registrati da Configuration Manager, questi client comunicano solo con i punti di gestione presenti nel sito loro assegnato. Questi client non comunicano mai con i punti di gestione presenti in siti secondari o in altri siti primari.  
