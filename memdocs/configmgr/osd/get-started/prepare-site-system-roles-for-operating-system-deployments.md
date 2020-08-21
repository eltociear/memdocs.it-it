---
title: Preparare i ruoli di sistema del sito per la distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Prima di distribuire i sistemi operativi in Configuration Manager, configurare i ruoli del sistema del sito
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d9331ce452e40944e4a9b363773d254a32f2c58
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697484"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Preparare i ruoli di sistema del sito per le distribuzioni dei sistemi operativi

*Si applica a: Configuration Manager (Current Branch)*

Per distribuire i sistemi operativi in Configuration Manager, è necessario preparare i ruoli del sistema del sito seguenti che richiedono considerazioni e configurazioni specifiche.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Punti di distribuzione  

Il ruolo di sistema del sito punto di distribuzione contiene i file di origine da scaricare per i client. Questo contenuto è relativo ad applicazioni, aggiornamenti software, immagini del sistema operativo, immagini di avvio e pacchetti di driver. È possibile controllare la distribuzione del contenuto usando le opzioni della larghezza di banda, della limitazione e della pianificazione.  

È importante avere sufficienti punti di distribuzione per supportare la distribuzione dei sistemi operativi nei computer. È anche importante pianificare la posizione di questi punti di distribuzione nella gerarchia. Per altre informazioni, vedere [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto). Questo articolo include altre considerazioni sulla pianificazione dei punti di distribuzione, specifiche per la distribuzione del sistema operativo.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> Considerazioni aggiuntive sulla pianificazione per i punti di distribuzione  

Di seguito sono descritti altri aspetti della pianificazione da considerare per i punti di distribuzione:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Come evitare distribuzioni indesiderate dei sistemi operativi?  
Configuration Manager non distingue i server del sito dagli altri computer di destinazione in una raccolta. Se si distribuisce una sequenza di attività richiesta in una raccolta che include un server del sito, questo esegue la sequenza di attività esattamente come qualsiasi altro computer presente nella raccolta. Assicurarsi che la distribuzione del sistema operativo usi una raccolta che include i client previsti.  

Gestire il comportamento per le distribuzioni di sequenze di attività ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente in un client e può causare risultati imprevisti. Un esempio è il caso di una sequenza di attività con scopo impostato su Obbligatorio che distribuisce un sistema operativo. Per ridurre il rischio di una distribuzione ad alto rischio indesiderata, configurare le impostazioni di verifica della distribuzione. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Quanti computer possono ricevere simultaneamente un'immagine del sistema operativo da un singolo punto di distribuzione?  
Per stimare quanti punti di distribuzione sono necessari, considerare le variabili seguenti:  
- Velocità di elaborazione del punto di distribuzione
- Velocità del disco del punto di distribuzione
- Larghezza di banda disponibile sulla rete
- Dimensione del pacchetto immagine   
  
Ad esempio, se non si prendono in considerazione altri fattori delle risorse server, il numero massimo di computer che possono elaborare un pacchetto di immagini da 4 GB in un'ora in una rete Ethernet da 100 megabit al secondo è 11.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Per eseguire la distribuzione di un sistema operativo a un numero determinato di computer in un intervallo di tempo specifico, è necessario distribuire l'immagine a un numero appropriato di punti di distribuzione.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>È possibile distribuire un sistema operativo in un punto di distribuzione?  
È possibile distribuire un sistema operativo in un punto di distribuzione, ma l'immagine del sistema operativo deve essere ricevuta da un punto di distribuzione diverso.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Configurazione dei punti di distribuzione per accettare le richieste PXE  

Per distribuire i sistemi operativi ai client di Configuration Manager che eseguono richieste di avvio PXE, è necessario configurare uno o più punti di distribuzioni per accettare le richieste PXE. Dopo la configurazione, il punto di distribuzione risponde alle richieste di avvio PXE e stabilisce l'azione appropriata da eseguire per la distribuzione. Per altre informazioni, vedere [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe) (Installare o modificare un punto di distribuzione).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE  

È possibile personalizzare le dimensioni della finestra e del blocco TFTP RamDisk per i punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout, perché le dimensioni del blocco o della finestra sono eccessive. La personalizzazione delle dimensioni della finestra e del blocco TFTP RamDisk consentono di ottimizzare il traffico TFTP quando si usa PXE per soddisfare i requisiti di rete specifici. Per individuare la scelta più efficiente, è necessario testare le impostazioni personalizzate nel proprio ambiente.  

-   **Dimensioni del blocco TFTP**: le dimensioni del blocco corrispondono alle dimensioni dei pacchetti di dati inviati dal server al client che sta scaricando il file. Dimensioni maggiori del blocco consentono al server di inviare meno pacchetti e di conseguenza si verificano meno ritardi per il round trip tra il server e client. Dimensioni del blocco molto grandi comportano tuttavia la creazione di pacchetti frammentati, che non sono supportati dalla maggior parte delle implementazioni di client PXE.  

-   **Dimensioni della finestra TFTP**: TFTP richiede un pacchetto di acknowledgment (ACK) per ogni blocco di dati inviato. Il server non invia il blocco successivo nella sequenza finché non riceve il pacchetto ACK per il blocco precedente. L'uso di finestre TFTP consente di definire quanti blocchi di dati sono necessari per riempire una finestra. Il server invia i blocchi di dati back-to-back fino a riempire la finestra e quindi il client invia un pacchetto ACK. Se si aumentano le dimensioni di questa finestra si riduce il numero di ritardi per round trip tra il client e il server, nonché il tempo complessivo necessario per scaricare un'immagine di avvio.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modificare le dimensioni della finestra TFTP RamDisk  
Per personalizzare le dimensioni della finestra TFTP RamDisk, aggiungere la chiave del Registro di sistema seguente nei punti di distribuzione abilitati per PXE:  

- **Percorso**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamDiskTFTPWindowSize  
- **Tipo**: REG_DWORD  
- **Valore**: (dimensioni finestra personalizzate)  
    - Il valore predefinito è **1** (un blocco di dati riempie la finestra).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modificare le dimensioni del blocco TFTP RamDisk  
Per personalizzare le dimensioni della finestra TFTP RamDisk, aggiungere la chiave del Registro di sistema seguente nei punti di distribuzione abilitati per PXE:  

- **Percorso**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamDiskTFTPBlockSize  
- **Tipo**: REG_DWORD  
- **Valore**: (dimensioni blocco personalizzate)  
    - Il valore predefinito è **4096**.  

> [!Note]  
> Sia i Servizi di distribuzione Windows sia il servizio risponditore PXE di Configuration Manager supportano queste configurazioni TFTP.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> Configurare i punti di distribuzione per il supporto del multicast  

Il multicast è un metodo di ottimizzazione della rete. È possibile usarlo nei punti di distribuzione quando più client potrebbero scaricare la stessa immagine del sistema operativo nello stesso momento. Quando si usa il multicast, più computer possono scaricare contemporaneamente l'immagine del sistema operativo, perché il punto di distribuzione usa la distribuzione multicast. Senza multicast, il punto di distribuzione invia una copia dei dati a ogni client in una connessione separata. Per altre informazioni, vedere [Usare il multicast per distribuire Windows in rete](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

Prima di distribuire il sistema operativo, configurare un punto di distribuzione per il supporto del multicast. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Punto di migrazione stato  

Il punto di migrazione stato archivia i dati sullo stato dell'utente acquisiti da USMT in un computer e quindi li ripristina in un altro computer. Tuttavia, quando si acquisiscono le impostazioni utente per una distribuzione del sistema operativo nello stesso computer, ad esempio una distribuzione in cui Windows viene aggiornato nel computer di destinazione, è possibile scegliere se archiviare i dati nello stesso computer con collegamenti reali o se usare un punto di migrazione stato. Per alcune distribuzioni ai computer, quando viene creata l'archiviazione stati, Configuration Manager crea automaticamente un'associazione tra l'archiviazione stati e il computer di destinazione. Durante la pianificazione del punto di migrazione stato tenere presenti i seguenti fattori:    


### <a name="user-state-size"></a>Dimensioni stato utente  

Le dimensioni dello stato utente influiscono direttamente sull'archiviazione su disco nel punto di migrazione stato e sulle prestazioni di rete durante la migrazione. Tenere presenti le dimensioni dello stato utente e il numero di computer di cui verrà eseguita la migrazione. Tenere presenti anche le impostazioni di cui eseguire la migrazione dal computer. Se ad esempio nel server è già presente il backup della cartella **Documenti**, potrebbe non essere necessario eseguirne la migrazione nell'ambito della distribuzione dell'immagine. Evitando migrazioni superflue è possibile ridurre le dimensioni generali dello stato utente e diminuire gli effetti sulle prestazioni di rete e sull'archiviazione su disco nel punto di migrazione stato.  


### <a name="user-state-migration-tool"></a>Utilità di migrazione stato utente  

Per acquisire e ripristinare lo stato utente durante la distribuzione dei sistemi operativi, è necessario usare un pacchetto per Utilità di migrazione stato utente (USMT) che punti ai file di origine USMT. Configuration Manager crea automaticamente questo pacchetto nella console di Configuration Manager in **Raccolta software** > **Gestione applicazioni** > **Pacchetti**. Configuration Manager usa USMT 10 per acquisire lo stato utente da un sistema operativo e quindi ripristinarlo in un altro sistema operativo. Windows Assessment and Deployment Kit (Windows ADK) per Windows 10 include USMT 10.

Per una descrizione dei diversi scenari di migrazione per USMT 10, vedere [Scenari di migrazione comuni](/windows/deployment/usmt/usmt-common-migration-scenarios) nella documentazione di Windows.  


### <a name="retention-policy"></a>Criteri di conservazione  

Quando si configura il punto di migrazione stato è possibile specificare l'intervallo di tempo per cui mantenere i dati sullo stato utente archiviati al suo interno. L'intervallo di tempo per cui conservare i dati nel punto di migrazione stato dipende da due considerazioni:  

-   L'effetto dei dati archiviati sull'archiviazione su disco.  

-   La possibilità di conservare i dati per un determinato periodo nel caso in cui sia necessario eseguire un'ulteriore migrazione dei dati.  
  
  
La migrazione dello stato avviene in due fasi: acquisizione e ripristino dei dati. Quando si acquisiscono dati, i dati sullo stato utente vengono raccolti e salvati nel punto di migrazione stato. Quando si ripristinano i dati, i dati sullo stato utente vengono recuperati dal punto di migrazione stato e scritti nel computer di destinazione. Quindi, il passaggio della sequenza attività **Rilascia archiviazione stati** rilascia i dati archiviati. Quando i dati vengono rilasciati, viene avviato il timer di conservazione. Se si seleziona l'opzione per eliminare immediatamente i dati migrati, i dati sullo stato utente vengono eliminati non appena vengono rilasciati. Se si seleziona l'opzione per conservare i dati per un determinato periodo di tempo, i dati vengono eliminati dopo il rilascio dei dati sullo stato, al termine dell'intervallo di tempo stabilito. Più è lungo il periodo di conservazione impostato, maggiore sarà lo spazio su disco potenzialmente necessario.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Selezionare l'unità in cui archiviare i dati di migrazione sullo stato utente  

Quando si configura il punto di migrazione stato, è necessario specificare l'unità sul server in cui archiviare i dati sulla migrazione dello stato utente. È possibile selezionare un'unità da un elenco non modificabile di unità. Tuttavia, alcune unità potrebbero rappresentare unità non accessibili in scrittura, ad esempio l'unità CD o un'unità di condivisione non di rete. Alcune lettere di unità potrebbero non essere mappate su un'unità del computer. Quando si configura il punto di migrazione stato, specificare un'unità condivisa e scrivibile.  


### <a name="configure-a-state-migration-point"></a>Configurare un punto di migrazione stato  

Per configurare un punto di migrazione stato per archiviare i dati dello stato utente, è possibile usare i metodi seguenti:  

-   Utilizzare la **Creazione guidata server del sistema sito** per creare un nuovo server di sistema del sito per il punto di migrazione stato.  

-   Utilizzare l' **Aggiunta guidata ruoli del sistema del sito** per aggiungere un punto di migrazione stato a un server esistente.  

Quando si usano queste procedure guidate, viene richiesto di specificare le informazioni seguenti per il punto di migrazione stato:  

-   Cartelle in cui archiviare i dati dello stato utente.  

-   Numero massimo di client che possono archiviare i dati nel punto di migrazione stato.  

-   Spazio minimo disponibile per il punto di migrazione stato in cui archiviare i dati sullo stato utente.  

-   Criteri di eliminazione per il ruolo. Specificare che i dati dello stato utente verranno eliminati immediatamente dopo il ripristino in un computer oppure dopo un numero specifico di giorni dal ripristino dei dati utente in un computer.  

-   Se il punto di migrazione stato deve rispondere solo alle richieste di ripristino dei dati dello stato utente. Quando si abilita questa opzione, non è possibile usare il punto di migrazione stato per archiviare i dati dello stato utente.  

Per i passaggi relativi all'installazione di un ruolo di sistema del sito, vedere [Aggiungere ruoli di sistema del sito](../../core/servers/deploy/configure/add-site-system-roles.md).