---
title: Creare una sequenza di attività per distribuzioni non di sistema operativo
titleSuffix: Configuration Manager
description: Creare sequenze di attività non destinate alla distribuzione di un sistema operativo, ad esempio per la distribuzione di software o l'automazione delle attività
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 583a90452fe077057b93150e9cb635fe9269de5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709069"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Creare una sequenza di attività per distribuzioni non di sistema operativo

*Si applica a: Configuration Manager (Current Branch)*

Le sequenze di attività in Configuration Manager consentono di automatizzare diversi tipi di attività all'interno dell'ambiente. Queste attività sono progettate e testate principalmente per la distribuzione di sistemi operativi. Configuration Manager ha molte altre funzionalità che deve essere la tecnologia principale in uso per gli scenari seguenti:

- [Installazione di applicazioni](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > A partire dalla versione 2002, è possibile installare applicazioni complesse usando le sequenze di attività con il modello di applicazione. Aggiungere un tipo di distribuzione a un'app che è una sequenza di attività per installare o disinstallare l'app. Per altre informazioni, vedere [Creare applicazioni Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Installazione di aggiornamenti software](../../sum/understand/software-updates-introduction.md)

- [Impostazione della configurazione](../../compliance/understand/ensure-device-compliance.md)

Considerare anche altre tecnologie di automazione di Microsoft System Center, ad esempio [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) e [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

L'efficacia delle sequenze di attività risiede nella loro flessibilità e nel modo in cui si usano. Sono in grado di configurare le impostazioni client, distribuire il software, aggiornare i driver, modificare gli stati utente ed effettuare altre attività in modo indipendente dalla distribuzione del sistema operativo. È possibile creare una sequenza di attività personalizzata per aggiungere qualsiasi numero di attività. L'uso di sequenze di attività personalizzate per la distribuzione non del sistema operativo è supportato in Configuration Manager. Tuttavia, se una sequenza di attività genera risultati indesiderati o incoerenti, considerare i possibili modi per semplificare l'operazione:

- Usare passaggi più semplici
- Dividere le azioni tra più sequenze di attività
- Adottare un approccio graduale alla creazione e ai test della sequenza di attività

I passaggi seguenti sono supportati in una sequenza di attività personalizzata di distribuzione non del sistema operativo:  

- [Verifica conformità](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Connessione a una cartella di rete](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Installa applicazione](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Installa aggiornamenti software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Riavvia computer](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Esegui script PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Eseguire la sequenza di attività](../understand/task-sequence-steps.md#child-task-sequence)  

- [Imposta variabili dinamiche](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Imposta variabile della sequenza di attività](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  
