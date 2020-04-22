---
title: Gestire la larghezza di banda della rete per il contenuto
titleSuffix: Configuration Manager
description: Configurare la pianificazione, la limitazione della larghezza di banda della rete e il contenuto pre-installato per Configuration Manager.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ee7d00f3b5c98528d9999b83b07aa393b72e36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704159"
---
# <a name="manage-network-bandwidth-for-content"></a>Gestire la larghezza di banda della rete per il contenuto
Per gestire più facilmente la larghezza di banda della rete usata per il processo di gestione del contenuto di Configuration Manager, è possibile usare i controlli predefiniti per la pianificazione e la limitazione della larghezza di banda della rete. È inoltre possibile usare contenuto pre-installato. Le sezioni seguenti includono informazioni più dettagliate su queste opzioni.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Pianificazione e limitazione della larghezza di banda della rete  

 Quando si crea un pacchetto, cambiare il percorso di origine del contenuto oppure aggiornare il contenuto nel punto di distribuzione; i file vengono copiati dal percorso di origine sulla raccolta contenuto nel server del sito. Quindi, il contenuto viene copiato dalla raccolta contenuto nel server del sito alla raccolta contenuto nei punti di distribuzione. Quando i file origine di contenuto vengono aggiornati e i file di origine sono già stati distribuiti, Configuration Manager recupera solo i file nuovi o aggiornati e li invia al punto di distribuzione.

 È possibile usare i controlli per la pianificazione e la limitazione della larghezza di banda della rete per le comunicazioni da sito a sito e per le comunicazioni tra un server del sito e un punto di distribuzione remoto. Se la larghezza di banda della rete è limitata anche dopo la configurazione di tali controlli, può essere opportuno pre-installare il contenuto nel punto di distribuzione.  

 In Configuration Manager è possibile configurare una pianificazione e specificare le impostazioni di limitazione della larghezza di banda della rete nei punti di distribuzione remoti che determinano quando e come viene eseguita la distribuzione del contenuto. Ogni punto di distribuzione remoto può avere diverse configurazioni che consentono di limitare la larghezza di banda di rete dell'indirizzo dal server del sito al punto di distribuzione remoto. I controlli per la pianificazione e la limitazione della larghezza di banda della rete verso il punto di distribuzione remoto sono simili alle impostazioni relative a un indirizzo di mittente standard. In questo caso, le impostazioni vengono usate da un nuovo componente chiamato Package Transfer Manager.

 Package Transfer Manager distribuisce il contenuto da un server del sito, come sito primario o secondario, in un punto di distribuzione installato su un sistema del sito. Per un punto di distribuzione che non si trova su un server del sito, le impostazioni di limitazione della larghezza di banda della rete sono configurate nella scheda **Limiti di velocità**, mentre quelle di pianificazione sono specificate nella scheda **Pianifica**. Le impostazioni di ora sono basate sul fuso orario del sito di invio, non del punto di distribuzione.  

> [!IMPORTANT]  
>  Le schede **Limiti di velocità** e **Pianifica** vengono visualizzate solo nelle proprietà dei punti di distribuzione che non sono installati in un server del sito.  

Per altre informazioni, vedere [Installare e configurare punti di distribuzione per Configuration Manager](../../servers/deploy/configure/install-and-configure-distribution-points.md).  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Contenuto pre-installato  
 Prima di distribuire il contenuto, è possibile pre-installarlo in modo da aggiungere i file alla raccolta contenuto in un server del sito o in un punto di distribuzione. Poiché si trovano già nella raccolta, i file di contenuto non vengono trasferiti attraverso la rete quando si distribuisce il contenuto. È possibile pre-installare i file di contenuto per applicazioni e pacchetti.  

Nella console di Configuration Manager selezionare il contenuto che si vuole pre-installare e quindi usare la **Creazione guidata file di contenuto pre-installazione**. In questo modo, viene creato un file di contenuto pre-installato e compresso, che contiene i file e i metadati associati per il contenuto. Quindi, è possibile importare manualmente il contenuto in un server del sito o in punto di distribuzione. Tenere presente quanto segue:  

-   Quando si importa il file di contenuto pre-installato in un server del sito, i file di contenuto vengono aggiunti alla raccolta contenuto nel server del sito e quindi registrati nel database del server del sito.  

-   Quando si importa il file di contenuto pre-installato in un punto di distribuzione, i file di contenuto vengono aggiunti alla raccolta contenuto nel punto di distribuzione. Un messaggio di stato viene inviato al server del sito per segnalare al sito che il contenuto è disponibile nel punto di distribuzione.  

Facoltativamente, è possibile configurare il punto di distribuzione come **pre-installato** per la gestione della distribuzione del contenuto. Pertanto, quando si distribuisce il contenuto è possibile scegliere se:  

-   Pre-installare sempre il contenuto nel punto di distribuzione.  

-   Pre-installare il contenuto iniziale per il pacchetto e quindi usare il processo standard di distribuzione del contenuto quando sono disponibili aggiornamenti.  

-   Usare sempre il processo standard di distribuzione per il contenuto nel pacchetto.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Determinare se pre-installare il contenuto  
 Prendere in considerazione la pre-installazione di contenuto per applicazioni e pacchetti nei seguenti scenari:  

-   **Per risolvere il problema relativo alla limitazione della larghezza di banda della rete dal server del sito a un punto di distribuzione.** Se la pianificazione e la limitazione della larghezza di banda della rete non sono sufficienti per soddisfare le esigenze di larghezza di banda, valutare l'opportunità di pre-installare il contenuto nel punto di distribuzione. Per ogni punto di distribuzione è disponibile l'impostazione **Abilita questo punto di distribuzione per il contenuto pre-installato** che è possibile configurare nelle proprietà del punto di distribuzione. Quando si abilita questa opzione, il punto di distribuzione viene individuato come punto di distribuzione pre-installato ed è possibile scegliere come gestire il contenuto in base al pacchetto.  

    Le impostazioni seguenti sono disponibili nelle proprietà relative a un'applicazione, un pacchetto, un pacchetto driver, un'immagine d'avvio, un programma di installazione del sistema operativo e un'immagine. Queste impostazioni consentono di scegliere la modalità di gestione della distribuzione del contenuto nei punti di distribuzione remoti identificati come pre-installati:  

    -   **Scarica automaticamente il contenuto quando i pacchetti sono assegnati ai punti di distribuzione**: usare questa opzione quando si hanno pacchetti più piccoli e le impostazioni di pianificazione e limitazione della larghezza di banda della rete forniscono sufficiente controllo per la distribuzione del contenuto.  

    -   **Scarica solo le modifiche di contenuto nel punto di distribuzione**: usare questa opzione quando si prevede che i futuri aggiornamenti al contenuto del pacchetto abbiano in genere dimensioni più piccole rispetto al pacchetto iniziale. Ad esempio, può essere opportuno pre-installare un'applicazione come Microsoft Office perché la dimensione del pacchetto iniziale è superiore a 700 MB e quindi troppo grande da inviare attraverso la rete. Tuttavia, gli aggiornamenti del contenuto di questo pacchetto possono essere inferiori a 10 MB e sono quindi accettabili per la distribuzione in rete. Un altro esempio può essere rappresentato dai pacchetti driver per i quali la dimensione iniziale è grande, ma le aggiunte incrementali possono avere dimensioni ridotte.  

    -   **Copia manualmente il contenuto del pacchetto nel punto di distribuzione**: usare questa opzione quando si hanno pacchetti di grandi dimensioni, ad esempio un sistema operativo, e non si vuole mai usare la rete per distribuire il contenuto nel punto di distribuzione. Quando si seleziona questa opzione, è necessario pre-installare il contenuto nel punto di distribuzione.  

    > [!IMPORTANT]  
    >  Le opzioni precedenti sono applicabili in base al pacchetto e vengono usate solo quando un punto di distribuzione è identificato come pre-installato. I punti di distribuzione che non sono stati identificati come pre-installati ignorano queste impostazioni. In questo caso, il contenuto sempre viene distribuito in rete dal server del sito ai punti di distribuzione.  

-   **Ripristinare la raccolta contenuto in un server del sito.** Quando un server del sito restituisce un errore, le informazioni sui pacchetti e le applicazioni contenute nella raccolta contenuto vengono ripristinate nel database del sito come parte del processo di ripristino, ma i file della raccolta contenuto non vengono ripristinati come parte del processo. Se non si ha un backup del file system per ripristinare la raccolta contenuto, è possibile creare un file di contenuto pre-installato da un altro sito che contiene i pacchetti e le applicazioni necessari. È quindi possibile estrarre il file di contenuto pre-installato sul server del sito ripristinato. Per altre informazioni sul backup e il ripristino del server del sito, vedere [Backup e ripristino per Configuration Manager](../../servers/manage/backup-and-recovery.md).  
