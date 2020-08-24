---
title: Usare i supporti autonomi per distribuire Windows
titleSuffix: Configuration Manager
description: Usare i supporti autonomi in Configuration Manager per distribuire Windows dove la larghezza di banda è limitata come opzione per installare e aggiornare i computer.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124653"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Usare i supporti autonomi per distribuire Windows senza usare la rete

*Si applica a: Configuration Manager (Current Branch)*

I supporti autonomi in Configuration Manager contengono tutti gli elementi necessari per distribuire un sistema operativo in un computer. Il supporto include l'immagine d'avvio, l'immagine del sistema operativo, i criteri della sequenza di attività, le applicazioni, i driver e altro ancora. Le distribuzioni di supporti autonomi consentono di distribuire i sistemi operativi nelle condizioni seguenti:

- In ambienti in cui non è semplice copiare un'immagine del sistema operativo o altri pacchetti di grandi dimensioni sulla rete.

- In ambienti senza connettività di rete o con connettività di rete a larghezza di banda ridotta.

Usare i supporti autonomi negli scenari di distribuzione del sistema operativo seguenti:

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)

Completare i passaggi in uno di questi scenari di distribuzione del sistema operativo. Usare quindi le sezioni seguenti per preparare e creare i supporti autonomi.

## <a name="unsupported-task-sequence-actions"></a>Azioni della sequenza di attività non supportate

Quando si usano i supporti autonomi, Configuration Manager non supporta le azioni seguenti nella sequenza di attività:

- Passaggio [Applica automaticamente i driver](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers). L'applicazione automatica di driver di dispositivo dal catalogo di driver non è supportata. Per rendere disponibile un set specificato di driver per Installazione di Windows, usare il passaggio [Applica pacchetto di driver](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage).

- Istallazione di aggiornamenti software.

- Installazione del software prima della distribuzione del sistema operativo.

- Associazione di utenti al computer di destinazione per l'affinità utente-dispositivo.

- Installazione dinamica dei pacchetti con il passaggio [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage).

- Installazione dinamica delle applicazioni con il passaggio [Installa applicazione](../understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!NOTE]
> Se la sequenza di attività per la distribuzione di un sistema operativo include il passaggio **Installa pacchetto** e si creano i supporti autonomi in un sito di amministrazione centrale, può verificarsi un errore. Il sito di amministrazione centrale non dispone dei criteri di configurazione client per abilitare l'agente di distribuzione del software durante l'esecuzione della sequenza di attività. Nel file **CreateTsMedia.log** può essere visualizzato l'errore seguente:
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> Per i supporti autonomi che includono un passaggio **Installa pacchetto**, creare i supporti autonomi in un sito primario nel quale è abilitato l'agente di distribuzione software.
>
> In alternativa, modificare la sequenza di attività per aggiungere un passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) dopo il passaggio [Imposta Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr). Il passaggio **Esegui riga di comando** esegue il comando WMI seguente per abilitare l'agente di distribuzione software prima dell'esecuzione del primo passaggio **Installa pacchetto**:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione

Quando si usano i supporti autonomi per avviare il processo di distribuzione del sistema operativo, configurare la distribuzione per rendere disponibile il sistema operativo per i supporti. Nella pagina **Impostazioni distribuzione** della distribuzione, per l'impostazione **Rendi disponibile per**, selezionare una delle opzioni seguenti:

- Client di Configuration Manager, supporti e PXE

- Solo supporti e PXE

- Solo supporti e PXE (nascosto)

## <a name="create-the-standalone-media"></a>Creare i supporti autonomi

È possibile specificare se i supporti autonomi sono unità flash USB o set di CD/DVD. Il computer che avvierà i supporti deve supportare l'opzione scelta come unità di avvio. Per altre informazioni, vedere [Creare supporti autonomi](create-stand-alone-media.md).

## <a name="install-the-os-from-standalone-media"></a>Installare il sistema operativo dai supporti autonomi

Per installare il sistema operativo, inserire i supporti autonomi nel computer e quindi accenderlo.

## <a name="next-steps"></a>Passaggi successivi

[Esperienze utente per la distribuzione del sistema operativo](../understand/user-experience.md#task-sequence-wizard)
