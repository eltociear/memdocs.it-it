---
title: Aggiornare i client Linux e UNIX
titleSuffix: Configuration Manager
description: Aggiornare un client in un server Linux o UNIX in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696819"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Come aggiornare i client per i server Linux e UNIX in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

È possibile aggiornare il client per Linux e UNIX in un computer a una versione più recente senza disinstallare il client corrente. A questo scopo, installare il pacchetto di installazione nuovo client nel computer usando la proprietà della riga di comando **-keepdb**. Quando il client per Linux e UNIX viene installato, i dati client esistenti vengono sovrascritti con i file del nuovo client. Tuttavia, la proprietà della riga di comando **-keepdb** indica al processo di installazione di conservare l'identificatore univoco (GUID), il database locale di informazioni e l'archivio certificati del client. Queste informazioni verranno quindi usate dalla nuova installazione client.  

 Poniamo l'esempio di un computer RHEL5 x64 che esegue il client dalla versione originale del client di Configuration Manager per Linux e UNIX. Per aggiornare questo client alla versione del client dell'aggiornamento cumulativo 1, eseguire manualmente lo script **install** per installare il pacchetto client applicabile dell'aggiornamento cumulativo 1 con l'aggiunta dell'opzione della riga di comando **-keepdb**. Vedere la riga di comando di esempio seguente:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Come usare una distribuzione software per aggiornare il client in server Linux e UNIX  
 È possibile usare una distribuzione software per aggiornare il client per Linux e UNIX a una nuova versione. Il client di Configuration Manager non può tuttavia eseguire direttamente lo script di installazione per installare il nuovo client, perché l'installazione di un nuovo client deve per prima cosa disinstallare il client corrente. Questa azione terminerebbe il processo del client di Configuration Manager che esegue lo script di installazione prima che l'installazione del nuovo client abbia inizio. Per usare correttamente una distribuzione software per installare il nuovo client, è necessario pianificare l'installazione in modo che venga avviata in un secondo momento ed eseguita dalle funzionalità di pianificazione predefinite del sistema operativo.  

 Usare una distribuzione software per copiare prima di tutto i file per il pacchetto di installazione del nuovo client nel computer client. Quindi distribuire ed eseguire uno script per pianificare il processo di installazione client. Lo script usa il comando predefinito **at** del sistema operativo per ritardare l'avvio. Al momento dell'esecuzione dello script, il suo funzionamento sarà gestito dal sistema operativo client e non dal client di Configuration Manager nel computer. Questo comportamento consente alla riga di comando chiamata dallo script di disinstallare prima il client di Configuration Manager e quindi di installare il nuovo client. Queste azioni completano il processo di aggiornamento del client nel computer Linux o UNIX. Al termine dell'aggiornamento, il client aggiornato continuerà a essere gestito da Configuration Manager.  

 Usare la procedura seguente per configurare una distribuzione software per l'aggiornamento del client per Linux e UNIX. Gli esempi e i passaggi seguenti consentono di aggiornare un computer RHEL5 x64 che esegue la versione iniziale del client alla versione dell'aggiornamento cumulativo 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Per usare una distribuzione software per aggiornare il client in server Linux e UNIX  

1. Copiare il pacchetto di installazione del nuovo client nel computer che esegue il client di Configuration Manager da aggiornare.  

    Inserire ad esempio il pacchetto di installazione client e lo script di installazione per l'aggiornamento cumulativo 1 nel percorso seguente del computer client: **/tmp/PATCH**  

2. Creare uno script per gestire l'aggiornamento del client di Configuration Manager. Quindi inserire una copia dello script nella stessa cartella del computer client scelta per i file di installazione client al passaggio 1.  

    Lo script non richiede un nome specifico. Deve contenere righe di comando sufficienti per usare i file di installazione client contenuti in una cartella locale nel computer client e per installare il pacchetto di installazione client usando la proprietà della riga di comando **-keepdb**. Usare la proprietà della riga di comando **-keepdb** per conservare l'identificatore univoco del client corrente in modo che venga usato dal nuovo client che si sta installando.  

    Ad esempio, si può creare uno script denominato **upgrade.sh** che contiene le righe seguenti:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Quindi copiarlo nella cartella **/tmp/PATCH** del computer client.

3. Usare la distribuzione software per fare in modo che ogni client usi il comando predefinito **at** del computer per eseguire lo script **upgrade.sh** con un breve ritardo prima dell'esecuzione dello script.  

    Ad esempio, usare la riga di comando seguente per eseguire lo script: **at -f /tmp/upgrade.sh -m now + 5 minutes**  

   Dopo aver correttamente pianificato l'esecuzione dello script **upgrade.sh** , il client invia un messaggio di stato per indicare che la distribuzione software è stata completata correttamente. L'effettiva installazione del client, tuttavia, verrà gestita dal computer dopo il ritardo. Al termine dell'aggiornamento del client, convalidare l'installazione esaminando il file **/var/opt/microsoft/scxcm.log** nel computer client. Verificare che il client sia installato e in comunicazione con il sito visualizzando i dettagli per il client nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità** della console di Configuration Manager.  
