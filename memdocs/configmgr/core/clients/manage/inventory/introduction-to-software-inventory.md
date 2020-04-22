---
title: Inventario software
titleSuffix: Configuration Manager
description: Informazioni introduttive sull'inventario software in Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695389"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Introduzione all'inventario software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare l'inventario software per raccogliere informazioni sui file nei dispositivi client. L'inventario software consente anche di raccogliere i file dai dispositivi client e archiviarli nel server del sito. L'inventario software viene raccolto quando si seleziona l'impostazione **Abilitare inventario software nei client** nelle impostazioni client. È anche possibile pianificare l'operazione nelle impostazioni client.  

Dopo aver abilitato l'inventario software e completato l'esecuzione di un ciclo di inventario software, il client invia le informazioni a un punto di gestione nel sito del client. Il punto di gestione inoltra quindi le informazioni di inventario al server del sito di Configuration Manager, che archivia tali informazioni nel database del sito.

 Esistono alcuni modi per visualizzare i dati dell'inventario software:  

- [Creare query](../../../../core/servers/manage/create-queries.md) che restituiscono i dispositivi con i file specificati.   

- Creare [raccolte basate su query](../../../../core/clients/manage/collections/introduction-to-collections.md) che includono dispositivi con i file specificati.   

- [Eseguire report](../../../servers/manage/introduction-to-reporting.md) che forniscono dettagli sui file nei dispositivi.

- Usare [Esplora inventario risorse](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) per visualizzare informazioni dettagliate relative ai file di inventario raccolti dai dispositivi client.   

 Quando si esegue l'inventario software in un dispositivo client, il primo report è un inventario completo. I report successivi contengono solo informazioni di inventario differenziale. Il server del sito elabora le informazioni differenziali in ordine di ricezione. Se mancano le informazioni differenziali per un client, il server del sito rifiuta informazioni differenziali aggiuntive e indica al client di eseguire un ciclo di inventario completo.  

 Configuration Manager può individuare i computer ad avvio doppio ma restituisce solo le informazioni di inventario relative al sistema operativo attivo nel momento in cui è stato eseguito l'inventario.  
