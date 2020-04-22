---
title: Package Transfer Manager
titleSuffix: Configuration Manager
description: Informazioni sul modo in cui Package Transfer Manager in Configuration Manager trasferisce il contenuto da un server del sito ai punti di distribuzione remoti.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706509"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Package Transfer Manager in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In un sito di Configuration Manager, Package Transfer Manager è un componente del servizio SMS_Executive che gestisce il trasferimento di contenuto da un computer server di un sito ai punti di distribuzione remoti del sito. (Un punto di distribuzione remoto è un punto che non si trova nel computer del server di sito). Package Transfer Manager non supporta le configurazioni impostate dall'amministratore, ma la conoscenza del suo funzionamento è utile per pianificare l'infrastruttura di gestione del contenuto e anche per risolvere i problemi relativi alla distribuzione del contenuto.


Quando si distribuisce il contenuto a uno o più punti di distribuzione remoti in un sito, **Distribution Manager** crea un processo di trasferimento del contenuto e quindi comunica a Package Transfer Manager nei server del sito primario e secondario di trasferire il contenuto ai punti di distribuzione remoti.

 Package Transfer Manager registra le sue azioni nel file **pkgxfermgr.log** sul server del sito. Il file di log rappresenta l'unica posizione in cui è possibile visualizzare le attività di Package Transfer Manager.  

> [!NOTE]  
>  Nelle versioni precedenti di Configuration Manager, Distribution Manager gestisce il trasferimento del contenuto a un punto di distribuzione remoto. Distribution Manager gestisce inoltre il trasferimento del contenuto tra i siti. Con Configuration Manager, Distribution Manager continua a gestire il trasferimento del contenuto tra due siti, ma Package Transfer Manager è ora in grado di gestire il trasferimento del contenuto a un numero elevato di punti di distribuzione. Ciò consente di migliorare le prestazioni generali della distribuzione del contenuto tra diversi siti e verso i punti di distribuzione all'interno di un sito.  

Per trasferire il contenuto a un punto di distribuzione standard, Package Transfer Manager usa le stesse funzionalità di Distribution Manager delle versioni precedenti di Configuration Manager. Vale a dire gestisce attivamente il trasferimento di file a ogni punto di distribuzione remoto. Tuttavia, per distribuire il contenuto a un punto di distribuzione pull, Package Transfer Manager comunica a tale punto che il contenuto è disponibile. Il punto di distribuzione pull assume quindi il controllo del processo di trasferimento.  

Le informazioni seguenti descrivono come Package Transfer Manager gestisce il trasferimento del contenuto a punti di distribuzione standard e a punti di distribuzione configurati come pull:
1.  **L'amministratore distribuisce il contenuto a uno o più punti di distribuzione in un sito.**  

    -   **Punto di distribuzione standard:** Distribution Manager crea un processo di trasferimento del contenuto per quel contenuto.  

    -   **Punto di distribuzione pull**: Distribution Manager crea un processo di trasferimento del contenuto per quel contenuto.  

2.  **Distribution Manager esegue i controlli preliminari.**  

    -   **Punto di distribuzione standard:** Distribution Manager esegue un controllo di base per confermare che ogni punto di distribuzione è pronto per ricevere il contenuto. Dopo questa verifica, Distribution Manager comunica a Package Transfer Manager di iniziare il trasferimento del contenuto al punto di distribuzione.  

    -   **Punto di distribuzione pull**: Distribution Manager avvia Package Transfer Manager, il quale comunica al punto di distribuzione pull che è presente un nuovo processo di trasferimento del contenuto. Distribution Manager non verifica lo stato dei punti di distribuzione remoti che sono di tipo pull poiché ogni punto di distribuzione pull gestisce i propri trasferimenti di contenuto.  

3.  **Package Transfer Manager si predispone al trasferimento del contenuto.**  

    -   **Punto di distribuzione standard:** Package Transfer Manager esamina l'archivio di contenuto a istanza singola di ogni punto di distribuzione remoto specificato allo scopo di identificare eventuali file che sono già presenti in tale punto di distribuzione. Quindi Package Transfer Manager esegue la coda per il trasferimento solo di quei file che non sono già presenti.  

        > [!NOTE]  
        >  Per copiare ogni file della distribuzione nel punto di distribuzione, anche se i file sono già presenti nell'archivio a istanza singola del punto di distribuzione, usare l'azione **Ridistribuisci** per il contenuto.  

    -   **Punto di distribuzione pull**: Per ogni punto di distribuzione pull nella distribuzione, Package Transfer Manager verifica i punti di distribuzione di origine dei punti di distribuzione pull per confermare la disponibilità del contenuto.  

        -   Quando il contenuto è disponibile in almeno uno dei punti di distribuzione di origine, Package Transfer Manager invia al punto di distribuzione pull una notifica che indica al punto di distribuzione di avviare il processo di trasferimento del contenuto. La notifica include i nomi e le dimensioni dei file, gli attributi e i valori hash.  

        -   Quando il contenuto non è ancora disponibile, Package Transfer Manager non invia una notifica al punto di distribuzione. Al contrario, ripete la verifica ogni 20 minuti fino a quando il contenuto non è disponibile. Quindi, quando il contenuto è disponibile, Package Transfer Manager invia la notifica a quel punto di distribuzione pull.  

        > [!NOTE]  
        >  Per consentire al punto di distribuzione pull di copiare ogni file della distribuzione nel punto di distribuzione, anche se i file sono già presenti nell'archivio a istanza singola del punto di distribuzione, usare l'azione **Ridistribuisci** per il contenuto.  

4.  **Il trasferimento del contenuto viene avviato.**  

    -   **Punto di distribuzione standard:** Package Transfer Manager copia i file a ogni punto di distribuzione remoto. Durante il trasferimento a un punto di distribuzione standard:  

        -   Per impostazione predefinita, Package Transfer Manager può elaborare contemporaneamente tre pacchetti univoci e distribuirli ai cinque punti di distribuzione in parallelo. Complessivamente, questi sono definiti **Impostazioni distribuzione simultanea**. Per configurare la distribuzione simultanea, in **Proprietà componente distribuzione software** per ogni sito passare alla scheda **Generale**.  

        -   Package Transfer Manager usa le configurazioni di larghezza di banda di rete e di pianificazione di ogni punto di distribuzione durante il trasferimento del contenuto al punto di distribuzione. Per configurare queste impostazioni, nell'area **Proprietà** di ogni punto di distribuzione remoto passare alle schede **Pianifica** e **Limiti di velocità**. Per altre informazioni, vedere [Gestire il contenuto e l'infrastruttura del contenuto per Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Punto di distribuzione pull**: Quando un punto di distribuzione pull riceve un file di notifica, il punto di distribuzione inizia il processo di trasferimento del contenuto. Il processo di trasferimento viene eseguito in modo indipendente in ogni punto di distribuzione pull:  

        1.   La distribuzione pull identifica i file nella distribuzione del contenuto che non presenta già nel suo singolo archivio dell'istanza e si prepara per scaricare il contenuto da uno dei suoi punti di distribuzione di origine.  

        2.   Successivamente, il punto di distribuzione pull verifica ognuno dei suoi punti di distribuzione di origine, in ordine, fino a che trova un punto di distribuzione di origine con contenuto disponibile. Quando il punto di distribuzione pull identifica un punto di distribuzione di origine con il contenuto, inizia il download di tale contenuto.  

        > [!NOTE]  
        >  Il processo di download del contenuto eseguito dal punto di distribuzione pull è identico a quello usato dai client di Configuration Manager. Per il trasferimento del contenuto eseguito dal punto di distribuzione pull, non vengono usate né le impostazioni di trasferimento simultaneo, né le opzioni di pianificazione e limitazione della larghezza di banda della rete configurate per i punti di distribuzione standard.  

5.  **Il trasferimento del contenuto viene completato.**  

    -   **Punto di distribuzione standard:** al termine del trasferimento dei file a ogni punto di distribuzione remoto designato, Package Transfer Manager verifica l'hash del contenuto nel punto di distribuzione e quindi comunica a Distribution Manager che la distribuzione è completata.  

    -   **Punto di distribuzione pull**: dopo il completamento del download del contenuto, il punto di distribuzione pull verifica l'hash del contenuto e quindi invia un messaggio di stato al punto di gestione dei siti per segnalare la corretta esecuzione dell'operazione. Se dopo 60 minuti il messaggio di stato non viene ricevuto, Package Transfer Manager viene riattivato ed esegue una verifica del punto di distribuzione pull per determinare se tale punto ha scaricato il contenuto. Se il download del contenuto è in corso, Package Transfer Manager rimane in modalità di sospensione per altri 60 minuti prima di eseguire nuovamente una verifica del punto di distribuzione pull. Questo ciclo continua fino a quando il punto di distribuzione pull non ha completato il trasferimento del contenuto.  
