---
title: replica basata su file
titleSuffix: Configuration Manager
description: Informazioni su come Configuration Manager usa la replica basata su file per trasferire i dati tra i siti all'interno della gerarchia
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703559"
---
# <a name="file-based-replication"></a>replica basata su file

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager usa la replica basata su file per trasferire i dati basati su file tra i siti all'interno della gerarchia. Questi dati includono le applicazioni e i pacchetti che si vuole distribuire ai punti di distribuzione nei siti figlio. Gestiscono anche record dei dati di individuazione non elaborati che il sito trasferisce al sito padre e quindi elabora.  

La comunicazione tra siti basata su file usa il protocollo *Server Message Block* (SMB) sulla porta TCP/IP 445. Per controllare la quantità di dati che il sito trasferisce attraverso la rete, specificare la limitazione della larghezza di banda e la modalità a impulsi. Usare le pianificazioni per controllare quando inviare i dati attraverso la rete.  

## <a name="routes"></a><a name="bkmk_routes"></a> Route

Le informazioni seguenti possono essere utili per configurare e usare le route di replica file.  

### <a name="file-replication-route"></a>Route di replica file

Ogni route di replica file identifica un sito di destinazione a cui un sito trasferisce dati basati su file. Ogni sito supporta una route di replica file a un sito di destinazione specifico.  

Per gestire una route di replica file, passare all'area di lavoro **Amministrazione**. Espandere il nodo **Configurazione della gerarchia** e quindi selezionare **Replica file**.  

È possibile modificare le impostazioni seguenti per le route di replica file:  

#### <a name="file-replication-account"></a>Account replica file

Questo account si connette al sito di destinazione e scrive i dati nella condivisione **SMS_Site** di tale sito. Il sito ricevente elabora i dati scritti in questa condivisione. Per impostazione predefinita, quando si aggiunge un sito alla gerarchia Configuration Manager assegna l'account computer del server del sito per il nuovo sito come account di replica file per tale sito. Aggiunge quindi questo account al gruppo `SMS_SiteToSiteConnection_<sitecode>` del sito di destinazione. Questo gruppo è locale nel computer che concede l'accesso alla condivisione SMS_Site. È possibile modificare questo account in un account utente di Windows. Se si modifica l'account, verificare che il nuovo account venga aggiunto al gruppo `SMS_SiteToSiteConnection_<sitecode>` del sito di destinazione.  

> [!NOTE]  
> I siti secondari usano sempre l'account computer del server del sito secondario come **Account replica file**.  

#### <a name="schedule"></a>Pianificazione

Impostare la pianificazione per ogni route di replica file. Questa azione limita il tipo di dati e l'ora in cui i dati possono essere trasferiti al sito di destinazione.  

#### <a name="rate-limits"></a>Limiti di velocità

Specificare i limiti di velocità per ogni route di replica file. Questa azione controlla la larghezza di banda di rete usata dal sito quando trasferisce i dati al sito di destinazione:  

- **Modalità a impulsi**: Consente di specificare la dimensione dei blocchi di dati che il sito invia al sito di destinazione. È inoltre possibile specificare un ritardo tra l'invio di ogni blocco di dati. Usare questa opzione quando è necessario inviare i dati al sito di destinazione tramite una connessione di rete a larghezza di banda ridotta.

    È ad esempio possibile che si sia vincolati a inviare 1 KB di dati ogni cinque secondi, ma non 1 KB ogni tre secondi. Questo vincolo è indipendente dalla velocità del collegamento o dall'utilizzo in un determinato momento.

- **Limitato alle velocità di trasferimento massime specificate per ora**: Il sito invia i dati a un sito di destinazione usando solo la percentuale di tempo specificata. Configuration Manager non identifica la larghezza di banda disponibile della rete. Divide in intervalli il periodo di tempo in cui può inviare i dati. I dati vengono quindi inviati in un intervallo di tempo breve, seguito da intervalli di tempo in cui non vengono inviati dati.

    Ad esempio è possibile impostare la velocità massima su **50%** . Configuration Manager trasmette i dati per un periodo di tempo, seguito da un periodo di tempo uguale in cui non viene inviato alcun dato. Non vengono gestite le dimensioni effettive del blocco di dati inviato. Il sito gestisce solo la quantità di tempo durante il quale avviene l'invio dei dati.  

    > [!CAUTION]  
    > Per impostazione predefinita, un sito può usare fino a tre **invii simultanei** per trasferire i dati a un sito di destinazione. Quando si abilitano i limiti di velocità per una route di replica file, gli **invii simultanei** per l'invio dei dati a tale sito sono limitati a uno. Questo comportamento si applica anche quando l'opzione **Limita larghezza di banda disponibile (%)** è impostata su **100%** . Se ad esempio si usano le impostazioni predefinite per il mittente, la velocità di trasferimento al sito di destinazione viene ridotta a un terzo della capacità predefinita.  

#### <a name="routes-between-secondary-sites"></a>Route tra siti secondari

Configurare una route di replica file tra due siti secondari per distribuire contenuto basato su file fra tali siti.  


### <a name="sender"></a>Mittente

Ogni sito dispone di un mittente. Il mittente gestisce la connessione di rete da un sito a un sito di destinazione. Può stabilire connessioni a più siti contemporaneamente. Per connettersi a un sito, il mittente usa la route di replica file al sito e identifica l'account usato per stabilire la connessione di rete. Il mittente usa questo account anche per scrivere i dati nella condivisione SMS_Site del sito di destinazione.  

Per impostazione predefinita, il mittente scrive i dati in un sito di destinazione usando più **invii simultanei**, ovvero un *thread*. Ogni thread riesce a trasferire un oggetto basato su file differente al sito di destinazione. Quando un mittente inizia a inviare un oggetto, continua a scrivere blocchi di dati relativi a tale oggetto fino al suo completo invio. Dopo l'invio di tutti i dati relativi all'oggetto, sarà possibile iniziare l'invio di un nuovo oggetto su tale thread.  

Per gestire il mittente per un sito, passare all'area di lavoro **Amministrazione** ed espandere il nodo **Configurazione del sito**. Selezionare il nodo **Siti**, quindi selezionare **Proprietà** per il sito che si vuole gestire. Passare alla scheda **Mittente** per modificare le impostazioni del mittente.  

È possibile modificare le impostazioni seguenti per un mittente:  

#### <a name="maximum-concurrent-sendings"></a>Numero massimo di invii simultanei

Per impostazione predefinita ogni sito usa cinque invii simultanei (thread). Quando invia dati a un sito di destinazione, il sito dispone di tre thread. Aumentando tale numero, è possibile incrementare la velocità effettiva dei dati tra siti. Un maggior numero di thread significa che Configuration Manager può trasferire più file nello stesso momento. L'incremento di questo numero determina anche un aumento della richiesta di larghezza di banda della rete tra siti.  

#### <a name="retry-settings"></a>Impostazioni tentativi

Per impostazione predefinita, ogni sito ritenta la connessione due volte, con un intervallo di un minuto tra un tentativo e l'altro, in caso di connessione non riuscita. È possibile modificare il numero di tentativi di connessione e il relativo intervallo di attesa.  


## <a name="next-steps"></a>Passaggi successivi

[Database replication](database-replication.md)
