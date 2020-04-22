---
title: Introduzione alla distribuzione di sistemi operativi
titleSuffix: Configuration Manager
description: Consente di comprendere i concetti prima di distribuire sistemi operativi nell'ambiente di Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703869"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Introduzione alla distribuzione del sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare Configuration Manager per distribuire i sistemi operativi in molti modi diversi. Usare le informazioni in questa sezione per comprendere come distribuire sistemi operativi e automatizzare le attività. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a> Processo di distribuzione del sistema operativo  
 Configuration Manager offre diversi metodi con cui è possibile distribuire un sistema operativo. Sono diverse le operazioni che occorre eseguire, indipendentemente dal metodo di distribuzione usato:  

-   Identificare i driver di dispositivo di Windows necessari per eseguire l'immagine d'avvio o installare l'immagine del sistema operativo da distribuire.  

-   Identificare l'immagine d'avvio che si vuole usare per avviare il computer di destinazione.  

-   Usare una sequenza di attività per acquisire un'immagine del sistema operativo che si vuole distribuire. In alternativa, si può usare un'immagine del sistema operativo predefinita.  

-   Distribuire l'immagine di avvio, l'immagine del sistema operativo e qualsiasi contenuto relativo a un punto di distribuzione.  

-   Creare una sequenza di attività con i passaggi per distribuire l'immagine d'avvio e l'immagine del sistema operativo.  

-   Distribuire la sequenza di attività in una raccolta di computer.  

-   Monitorare la distribuzione.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a> Scenari di distribuzione del sistema operativo  
 In Configuration Manager sono disponibili molti scenari di distribuzione del sistema operativo che è possibile scegliere a seconda dell'ambiente e dello scopo dell'installazione del sistema operativo.  Ad esempio, è possibile partizionare e formattare un computer esistente con una nuova versione di Windows o aggiornare Windows alla versione più recente. Per determinare il metodo di distribuzione in grado di soddisfare le proprie esigenze, vedere [Scenari di distribuzione di sistemi operativi aziendali](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  È possibile scegliere tra gli scenari di distribuzione del sistema operativo seguenti:  

-   [Aggiornare Windows alla versione più recente](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Aggiornare un computer esistente con una nuova versione di Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Sostituire un computer esistente e trasferire le impostazioni](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a> Metodi per distribuire i sistemi operativi  
 Esistono diversi metodi con cui è possibile distribuire sistemi operativi nei computer client di Configuration Manager.  

- **Distribuzioni avviate da PXE**: le distribuzioni avviate da PXE consentono ai computer client di richiedere una distribuzione in rete. In questo metodo di distribuzione l'immagine del sistema operativo e l'immagine di avvio di Windows PE vengono inviate a un punto di distribuzione configurato per accettare le richieste di avvio da PXE. Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete con Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **Rendere disponibili i sistemi operativi in Software Center**: è possibile distribuire un sistema operativo e renderlo disponibile in Software Center. I client di Configuration Manager possono avviare l'installazione del sistema operativo da Software Center. Per altre informazioni, vedere [Sostituire un computer esistente e trasferire le impostazioni](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

- **Distribuzioni di multicast**: Le distribuzioni di multicast risparmiano larghezza di banda inviando contemporaneamente i dati a più client anziché inviare una copia dei dati a ogni client in una connessione separata. In questo metodo di distribuzione l'immagine del sistema operativo viene inviata a un punto di distribuzione. L'immagine verrà a sua volta distribuita quando i computer client richiedono la distribuzione. Per altre informazioni, vedere [Usare il multicast per distribuire Windows in rete](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Distribuzioni dei supporti di avvio**: Le distribuzioni dei supporti di avvio consentono di distribuire il sistema operativo all'avvio del computer di destinazione. All'avvio del computer di destinazione, viene recuperata la sequenza di attività, l'immagine del sistema operativo e qualsiasi altro contenuto richiesto dalla rete. Poiché tale contenuto non è incluso nel supporto, è possibile aggiornare il contenuto senza dover ricreare il supporto. Per altre informazioni, vedere [Creare supporti di avvio](../deploy-use/create-bootable-media.md).  

- **Distribuzioni autonome avviate da supporti**: Le distribuzioni autonome avviate da supporti consentono di distribuire i sistemi operativi nelle condizioni seguenti:  

  - In ambienti dove non è semplice copiare un'immagine del sistema operativo o altri pacchetti di grandi dimensioni sulla rete.  

  - In ambienti senza connettività di rete o con connettività di rete a larghezza di banda ridotta.  

    Per altre informazioni, vedere [Creare supporti autonomi](../deploy-use/create-stand-alone-media.md).  

- **Distribuzioni di supporti pre-installati**: Le distribuzioni di supporti pre-installati consentono di distribuire un sistema operativo in un computer in cui non è stato effettuato il provisioning. Il supporto preinstallato è un file WIM (Windows Imaging Format) che può essere installato in un computer bare metal dal produttore o in un centro di gestione temporanea aziendale non connesso all'ambiente di Configuration Manager.  

   Successivamente nell'ambiente di Configuration Manager il computer viene avviato usando l'immagine d'avvio fornita dal supporto, quindi il computer si collega al punto di gestione del sito per le sequenze di attività che completano il processo di download. Questo metodo di distribuzione può ridurre il traffico di rete perché l'immagine di avvio e l'immagine del sistema operativo sono già nel computer di destinazione. È possibile specificare applicazioni, pacchetti e pacchetti driver da includere nel supporto pre-installato. Per altre informazioni, vedere [Creare supporti preinstallati](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a> Immagini d'avvio  
 Un'immagine d'avvio in Configuration Manager è un'immagine Windows PE (WinPE) usata durante la distribuzione di un sistema operativo. Le immagini d'avvio vengono usate per avviare un computer in Windows PE, un sistema operativo minimo con componenti e servizi limitati che prepara il computer di destinazione per l'installazione di Windows. In Configuration Manager sono disponibili due immagini d'avvio: una per il supporto delle piattaforme x86 e una per il supporto delle piattaforme x64. Queste sono considerate immagini d'avvio predefinite. Le immagini d'avvio create e aggiunte a Configuration Manager dall'utente sono considerate immagini personalizzate. Le immagini d'avvio predefinite possono essere sostituite automaticamente quando si aggiorna Configuration Manager. Per altre informazioni sulle immagini d'avvio, vedere [Gestire le immagini d'avvio con System Center Configuration Manager](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a> Immagini del sistema operativo  
 Le immagini del sistema operativo in Configuration Manager vengono archiviate in file in formato Windows Imaging (WIM) e rappresentano una raccolta compressa dei file e delle cartelle di riferimento necessari per installare e configurare correttamente un sistema operativo in un computer. Per tutti gli scenari di distribuzione del sistema operativo, è necessario selezionare un'immagine del sistema operativo. È possibile usare l'immagine del sistema operativo predefinita o crearla da un computer di riferimento configurato dall'utente. Per altre informazioni, vedere [Manage operating system images](../get-started/manage-operating-system-images.md) (Gestire le immagini del sistema operativo).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a> Pacchetti di aggiornamento del sistema operativo  
 I pacchetti di aggiornamento del sistema operativo vengono usati per aggiornare un sistema operativo e sono distribuzioni del sistema operativo avviate dal programma di installazione. I pacchetti di aggiornamento del sistema operativo vengono importati in Configuration Manager da un DVD o da un file ISO montato. Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a> Supporti per distribuire i sistemi operativi  
 È possibile creare diversi tipi di supporti da usare per distribuire i sistemi operativi. Sono inclusi i supporti di acquisizione usati per acquisire le immagini del sistema operativo e supporti pre-installati, avviabili e autonomi usati per distribuire un sistema operativo. Usando i supporti, è possibile distribuire sistemi operativi nei computer che non dispongono di una connessione di rete o la cui connessione di rete al sito di Configuration Manager ha una larghezza di banda bassa. Per altre informazioni su come usare i supporti, vedere [Create task sequence media](../deploy-use/create-task-sequence-media.md) (Creare supporti per le sequenze di attività).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Driver di dispositivo  
 È possibile installare i driver del dispositivo nei computer di destinazione senza includerli nell'immagine del sistema operativo in fase di distribuzione. Configuration Manager offre un catalogo dei driver che contiene i riferimenti a tutti i driver di dispositivo importati in Configuration Manager. Il catalogo dei driver si trova nell'area di lavoro **Raccolta software** ed è costituito da due nodi: **Driver** e **Pacchetti driver**. Nel nodo **Driver** vengono elencati tutti i driver sono stati importati nel catalogo dei driver. È possibile usare il nodo per individuare i dettagli di tutti i driver importati, modificare a quale pacchetto driver o immagine di avvio appartiene un driver, abilitare o disabilitare un driver e altro ancora. Per altre informazioni, vedere [Gestire i driver](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a> Salvare e ripristinare lo stato utente  
 Quando vengono distribuiti i sistemi operativi, è possibile salvare lo stato utente dal computer di destinazione, distribuire il sistema operativo e quindi ripristinare lo stato utente dopo aver distribuito i sistemi operativi. In genere questo processo viene usato quando si aggiorna il sistema operativo in un computer client di Configuration Manager.  

 Le informazioni sullo stato utente vengono acquisite e ripristinate usando le sequenze attività. Quando vengono acquisite le informazioni sullo stato utente, le informazioni possono essere memorizzate in uno dei modi seguenti:  

- È possibile memorizzare i dati di stato utente in remoto configurando un punto di migrazione stato. La sequenza di attività di acquisizione invia i dati al punto di migrazione stato. Quindi, dopo aver distribuito il sistema operativo, la sequenza di attività di ripristino recupera i dati e ripristina lo stato utente nel computer di destinazione.  

- È possibile memorizzare i dati dello stato utente in una posizione specifica in locale. In questo scenario la sequenza di attività di acquisizione copia i dati utente in una posizione specifica nel computer di destinazione. Quindi, dopo aver distribuito il sistema operativo, la sequenza di attività di ripristino recupera i dati utente da tale posizione.  

- È possibile specificare i collegamenti reali che possono essere usati per ripristinare i dati utente e la relativa posizione originale. In questo scenario i dati dello stato utente rimangono sull'unità quando viene rimosso il sistema operativo precedente. Quindi, dopo aver distribuito il sistema operativo, la sequenza di attività di ripristino usa i collegamenti reali per ripristinare i dati dello stato utente nella posizione originale.  

  Per altre informazioni, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a> Distribuire a computer sconosciuti  
 È possibile distribuire sistemi operativi in computer non gestiti da Configuration Manager. Non sono presenti record di questi computer nel database di Configuration Manager. Questi computer vengono definiti computer sconosciuti. I computer sconosciuti includono i seguenti:  

- Computer in cui non è installato il client di Configuration Manager  

- Computer che non sono stati importati in Configuration Manager  

- Computer che non sono stati individuati da Configuration Manager  

  Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a> Associare utenti a un computer  
 Quando viene distribuito un sistema operativo, è possibile associare gli utenti con il computer di destinazione per supportare le azioni di affinità utente dispositivo. Quando si associa un utente al computer di destinazione, un utente amministratore può successivamente eseguire le azioni in qualsiasi computer associato all'utente, ad esempio distribuire un'applicazione al computer di un utente specifico. Tuttavia, quando si distribuisce un sistema operativo, non è possibile distribuire il sistema operativo nel computer di un utente specifico. Per altre informazioni, vedere [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Associare gli utenti a un computer di destinazione).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a> Usare sequenze di attività per automatizzare i passaggi  
 È possibile creare sequenze di attività per eseguire molteplici attività nell'ambiente di Configuration Manager. Le azioni della sequenza di attività sono definite nei singoli passaggi della sequenza. Quando si esegue la sequenza di attività, le azioni di ogni passaggio vengono eseguite a livello di riga di comando senza l'intervento dell'utente. È possibile usare le sequenze di attività per le operazioni seguenti:  

-   [Creare una sequenza di attività per installare un sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Creare una sequenza di attività per distribuzioni non di sistema operativo](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Creare una sequenza di attività per acquisire un sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Creare una sequenza di attività per acquisire e ripristinare lo stato utente](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Creare una sequenza di attività personalizzata](../deploy-use/create-a-custom-task-sequence.md)  
