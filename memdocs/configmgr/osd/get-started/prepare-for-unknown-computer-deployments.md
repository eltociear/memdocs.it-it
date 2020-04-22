---
title: Operazioni preliminari alle distribuzioni in computer sconosciuti
titleSuffix: Configuration Manager
description: Informazioni su come distribuire i sistemi operativi ai computer che non sono gestiti da Configuration Manager nell'ambiente di Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708819"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Preparare le distribuzioni in computer sconosciuti in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni di questo argomento per distribuire sistemi operativi a computer sconosciuti nell'ambiente di Configuration Manager. Un computer sconosciuto è un computer che non è gestito da Configuration Manager. Ciò vuol dire che non ci sono record di questi computer nel database di Configuration Manager. I computer sconosciuti includono i seguenti:  

- Computer in cui non è installato il client di Configuration Manager  

- Computer non importati in Configuration Manager  

- Computer non rilevati da Configuration Manager  

  È possibile distribuire sistemi operativi in computer sconosciuti con i metodi di distribuzione seguenti:  

- [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Usare i supporti di avvio per distribuire un sistema operativo](../deploy-use/create-bootable-media.md)  

- [Usare i supporti preinstallati per distribuire un sistema operativo](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Flusso di lavoro per la distribuzione in computer sconosciuti  
 Di seguito è riportato il flusso di lavoro di base per distribuire un sistema operativo in un computer sconosciuto:  

-   Selezionare un oggetto computer sconosciuto da utilizzare nella distribuzione. È possibile distribuire il sistema operativo in uno degli oggetti computer sconosciuti nella raccolta **Tutti i computer sconosciuti** oppure è possibile aggiungere gli oggetti nella raccolta **Tutti i computer sconosciuti** a un'altra raccolta. Configuration Manager offre due oggetti computer sconosciuti nella raccolta **Tutti i computer sconosciuti**. Un oggetto è per i computer x86 e l'altro per i computer x64.  

    > [!NOTE]  
    >  L'oggetto **Computer x86 sconosciuto** è solo per i computer che supportano x86. L'oggetto **Computer x64 sconosciuto** è per i computer che supportano x86 e x64. In pratica, questi oggetti descrivono l'architettura del computer di destinazione. Non descrivono il sistema operativo che si vuole distribuire nel computer di destinazione.  

-   Configurare un punto di distribuzione che supporta PXE o creare un supporto che consenta le distribuzioni in computer sconosciuti.  

-   Distribuire la sequenza di attività per installare il sistema operativo.  

## <a name="unknown-computer-installation-process"></a>Processo di installazione di computer sconosciuti  
 Quando un computer viene avviato da PXE o da un supporto per la prima volta, Configuration Manager verifica la presenza di record per tale computer nel database di Configuration Manager. Se viene rilevato un record, Configuration Manager verifica la presenza di sequenze di attività distribuite nel record. Se non viene rilevato alcun record, Configuration Manager verifica la presenza di sequenze di attività distribuite in un oggetto computer sconosciuto. In entrambi i casi, Configuration Manager esegue una delle operazioni seguenti:  

- Se c'è una sequenza di attività disponibile, Configuration Manager richiede all'utente di eseguire tale sequenza.  

- Se c'è una sequenza di attività necessaria, Configuration Manager esegue tale sequenza automaticamente.  

- Se non è distribuita una sequenza di attività per il record, Configuration Manager genera un errore che indica che non è presente nessuna sequenza di attività distribuita per il computer di destinazione.  

  Quando viene avviato un computer sconosciuto, Configuration Manager identifica il computer come computer di cui non è stato eseguito il provisioning e non come computer sconosciuto. Ciò significa che il computer è ora in grado di ricevere le sequenze attività distribuite per l'oggetto computer sconosciuto. La sequenza di attività distribuita installa quindi un'immagine del sistema operativo che deve includere il client di Configuration Manager.  

  Dopo aver installato il client di Configuration Manager, viene creato un record per il computer e tale computer viene elencato nella raccolta di Configuration Manager appropriata. Se il computer non riesce a installare l'immagine del sistema operativo o il client di Configuration Manager, viene creato un record "sconosciuto" per il computer e tale computer viene visualizzato nella raccolta **Tutti i sistemi**.  

> [!NOTE]  
>  Durante l'installazione dell'immagine del sistema operativo, la sequenza attività può recuperare le variabili raccolta ma non le variabili computer da questo computer.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Attivazione del supporto per computer sconosciuti  
 Usare le informazioni seguenti per consentire il supporto di computer sconosciuti quando si distribuisce un sistema operativo con PXE, supporti di avvio e supporti pre-installati.  

-   **PXE**  

     Selezionare la casella di controllo **Abilita supporto per computer sconosciuti** nella scheda **PXE** per un punto di distribuzione che supporta PXE. Per altre informazioni, vedere [Configurazione dei punti di distribuzione per accettare le richieste PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Supporto di avvio**  

     Selezionare la casella di controllo **Abilita supporto per computer sconosciuti** nella pagina **Protezione** della Creazione guidata del supporto per la sequenza attività. Per altre informazioni, vedere [Configurazione dei punti di distribuzione per accettare le richieste PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) e [Usare PXE per distribuire Windows in rete con Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Supporto pre-installato**  

     Selezionare la casella di controllo **Abilita supporto per computer sconosciuti** nella pagina **Protezione** della Creazione guidata del supporto per la sequenza attività. Per altre informazioni, vedere [Creare supporti pre-installati con Configuration Manager](../deploy-use/create-prestaged-media.md).  
