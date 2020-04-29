---
title: Usare i supporti autonomi per distribuire Windows
titleSuffix: Configuration Manager
description: I supporti autonomi in Configuration Manager consentono di distribuire Windows dove la larghezza di banda è limitata nonché di installare e aggiornare i computer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709039"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Usare i supporti autonomi per distribuire Windows senza usare la rete

*Si applica a: Configuration Manager (Current Branch)*

I supporti autonomi in Configuration Manager contengono tutti gli elementi necessari per distribuire un sistema operativo in un computer, tra cui l'immagine d'avvio, l'immagine del sistema operativo e la sequenza di attività per installare il sistema operativo, incluse le applicazioni, i driver e così via. Le distribuzioni autonome avviate da supporti consentono di distribuire i sistemi operativi nelle condizioni seguenti:  

-   In ambienti dove non è semplice copiare un'immagine del sistema operativo o altri pacchetti di grandi dimensioni sulla rete.  

-   In ambienti senza connettività di rete o con connettività di rete a larghezza di banda ridotta.  

È possibile usare il supporto autonomo negli scenari di distribuzione del sistema operativo seguenti:  

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)  

  Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi usare le sezioni seguenti per preparare e creare il supporto autonomo.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Azioni della sequenza di attività non supportate quando si usa il supporto autonomo  
 Se la procedura descritta in uno degli scenari di distribuzione del sistema operativo supportati è stata completata, la sequenza di attività per distribuire o aggiornare il sistema operativo è stata creata e tutti i contenuti associati sono stati distribuiti in un punto di distribuzione. Quando si usa il supporto autonomo, nella sequenza di attività le azioni seguenti non sono supportate:  

-   Passaggio Applica automaticamente i driver nella sequenza di attività. L'applicazione automatica di driver di dispositivo dal catalogo di driver non è supportata, ma è possibile scegliere il passaggio Applica pacchetto di driver per rendere disponibile un set di driver specificato per l'installazione di Windows.  

-   Istallazione di aggiornamenti software.  

-   Installazione del software prima della distribuzione del sistema operativo.  

-   Associazione di utenti al computer di destinazione per il supporto dell'affinità utente dispositivo.  

-   Installazione dinamica dei pacchetti tramite l'attività Installa pacchetti.  

-   Installazioni dinamiche delle applicazioni tramite l'attività Installa applicazione.  

> [!NOTE]  
>  Se la sequenza di attività per la distribuzione di un sistema operativo include il passaggio [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage) e si crea il supporto autonomo in un sito di amministrazione centrale, può verificarsi un errore. Il sito di amministrazione centrale non dispone dei criteri di configurazione del client necessari per abilitare l'agente di distribuzione software durante l'esecuzione della sequenza di attività. Nel file CreateTsMedia.log potrebbe essere visualizzato l'errore seguente:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  Per un supporto autonomo che include il passaggio **Installa pacchetto** , è necessario creare il supporto autonomo in un sito primario in cui l'agente di distribuzione software sia abilitato oppure aggiungere un passaggio [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) dopo il passaggio [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e prima del primo passaggio **Installa pacchetto** nella sequenza di attività. Il passaggio **Esegui riga di comando** esegue un comando WMIC per abilitare l'agente di distribuzione software prima dell'esecuzione del primo passaggio Installa pacchetto. È possibile usare quanto segue nel passaggio della sequenza di attività **Esegui riga di comando** :  
>   
>  **Riga di comando**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione  
 Quando si usa un supporto autonomo per avviare il processo di distribuzione del sistema operativo, è necessario configurare la distribuzione per rendere disponibile il sistema operativo per il supporto. È possibile eseguire questa configurazione nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione.  Per l'impostazione **Rendi disponibile per** , configurare uno degli elementi seguenti:  

-   **Client di Configuration Manager, supporti e PXE**  

-   **Solo supporti e PXE**  

-   **Solo supporti e PXE (nascosto)**  

## <a name="create-the-stand-alone-media"></a>Creare il supporto autonomo  
 È possibile specificare se il supporto autonomo è un'unità flash USB o un set di CD/DVD. Il computer in cui verrà avviato il supporto deve supportare l'opzione scelta come unità di avvio. Per altre informazioni, vedere [Creare supporti autonomi](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Installare il sistema operativo dal supporto autonomo  
 Inserire il supporto autonomo in un'unità di avvio del computer e quindi accendere il sistema per installare il sistema operativo.  
