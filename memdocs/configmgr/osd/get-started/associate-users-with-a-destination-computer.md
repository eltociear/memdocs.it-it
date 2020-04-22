---
title: Associare utenti a un computer
titleSuffix: Configuration Manager
description: Configurare Configuration Manager per associare gli utenti ai computer di destinazione quando si distribuiscono sistemi operativi.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709009"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Associare gli utenti a un computer di destinazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si usa Configuration Manager per la distribuzione dei sistemi operativi, è possibile associare gli utenti al computer di destinazione. Questa opzione è valida indipendentemente dal fatto che un singolo utente o più utenti siano gli utenti primari del computer di destinazione.  

L'affinità utente dispositivo supporta la gestione incentrata sull'utente durante la distribuzione delle applicazioni. Quando si associa un utente al computer di destinazione in cui viene installato un sistema operativo, successivamente è possibile distribuire le applicazioni all'utente associato e le applicazioni verranno installate automaticamente nel computer di destinazione. Nonostante sia possibile configurare il supporto per l'affinità utente-dispositivo durante la distribuzione del sistema operativo, non è possibile usare l'affinità utente-dispositivo per distribuire il sistema operativo.  

Per altre informazioni sull'affinità utente dispositivo, vedere l'argomento [Link users and devices with user device affinity in System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Collegare utenti e dispositivi con l'affinità utente dispositivo in System Center Configuration Manager).  

Esistono diversi metodi con i quali è possibile integrare l'affinità utente-dispositivo nelle distribuzioni del sistema operativo. È possibile integrare l'affinità utente-dispositivo nelle distribuzioni PXE, nelle distribuzioni dei supporti di avvio e nelle distribuzioni dei supporti pre-installati.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Creare una sequenza attività che includa la variabile **SMSTSAssignUsersMode**

Aggiungere la variabile **SMSTSAssignUsersMode** all'inizio della sequenza di attività usando il passaggio [Imposta variabile della sequenza di attività](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). Questa variabile specifica la modalità di gestione delle informazioni utente da parte della sequenza attività.

Per altre informazioni, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Creare un comando di preavvio che raccoglie le informazioni utente

Il comando di preavvio può essere uno script VBScript con una casella di input. Può anche essere un'applicazione HTML (HTA) che convalida i dati utente immessi. 

Questo comando di preavvio deve impostare la variabile **SMSTSUDAUsers** usata durante l'esecuzione della sequenza di attività. Questa variabile può essere impostata su un computer, una raccolta o una variabile della sequenza attività.

Per altre informazioni, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configurare la modalità di associazione dell'utente al computer di destinazione utilizzata da punti di distribuzione e supporti

Il punto di distribuzione o i supporti supportano l'associazione di utenti al computer di destinazione in cui viene distribuito il sistema operativo. Usare uno dei metodi seguenti: 

- [Configurare un punto di distribuzione in modo che accetti le richieste di avvio PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [Creare supporti di avvio](../deploy-use/create-bootable-media.md)  
- [Creare supporti preinstallati](../deploy-use/create-prestaged-media.md)  


La configurazione del supporto per l'affinità utente-dispositivo non ha un metodo predefinito per la convalida dell'identità utente. Questo comportamento è importante quando un tecnico effettua il provisioning del computer e immette le informazioni per conto dell'utente. Oltre a impostare il modo in cui la sequenza di attività gestisce le informazioni utente, la configurazione di queste opzioni nel punto di distribuzione e nei supporti consente di limitare le distribuzioni avviate da un avvio PXE o da un tipo di supporto specifico.
