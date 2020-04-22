---
title: Configurare il controllo remoto
titleSuffix: Configuration Manager
description: Configurare il controllo remoto in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1362f44c510fd34aebc6af77efc63e881c27688c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696469"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Configurazione del controllo remoto in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 Questa procedura descrive la configurazione delle impostazioni client predefinite per il controllo remoto. Queste impostazioni si applicano a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, assegnare un'impostazione client di dispositivo personalizzata a una raccolta contenente i computer. Per altre informazioni, vedere [Come configurare le impostazioni client](../../../../core/clients/deploy/configure-client-settings.md). 

Per usare Assistenza remota o Desktop remoto è necessario installare e configurare questi programmi nel computer che esegue la console di Configuration Manager. Per altre informazioni su come installare e configurare Assistenza remota o Desktop remoto, vedere la documentazione di Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Per abilitare il controllo remoto e configurare le impostazioni client  

1. Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

2. Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

3. Nella finestra di dialogo **Predefinito** scegliere **Strumenti remoti**.  

4. Configurare le impostazioni client per il controllo remoto, Assistenza remota e Desktop remoto. Per un elenco di impostazioni client di strumenti remoti che è possibile configurare, vedere [Strumenti remoti](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   È possibile modificare il nome della società visualizzato nella finestra di dialogo **Controllo remoto di Configuration Manager** configurando un valore per **Nome organizzazione visualizzato in Software Center** nelle impostazioni client **Agente computer** .  

   I computer client vengono configurati con queste impostazioni al successivo download dei criteri client. Per iniziare il recupero dei criteri per un singolo client, vedere [Come gestire i client](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Abilitare la traduzione della tastiera

Per impostazione predefinita Configuration Manager trasmette la posizione del tasto dal percorso del visualizzatore al percorso del condivisore. Ciò può causare problemi per le configurazioni della tastiera diverse tra il visualizzatore e il condivisore. Ad esempio, se un visualizzatore con tastiera inglese digitava "A", la tastiera francese del condivisore generava una "Q". Ora è possibile configurare il controllo remoto in modo che il carattere stesso venga trasmesso dalla tastiera del visualizzatore al condivisore e che il condivisore riceva ciò che il visualizzatore intende digitare.

Per attivare la traduzione della tastiera, in **Controllo remoto di Configuration Manager** scegliere **Azione** e poi scegliere **Enable keyboard translation** (Abilita traduzione tastiera) per trasmettere la posizione del tasto.

> [!NOTE]
>
> I tasti speciali, ad esempio ~!#@$%, non verranno tradotti correttamente.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Tasti di scelta rapida per il visualizzatore controllo remoto

|Tasti di scelta rapida|Descrizione|  
|-----------------------|-----------------|  
|ALT+PGSU|Passa tra i programmi in esecuzione, da sinistra a destra.|  
|ALT+PGGIÙ|Passa tra i programmi in esecuzione, da destra a sinistra.|  
|ALT+INS|Scorre i programmi in esecuzione nell'ordine in cui sono stati aperti.|  
|ALT+HOME|Visualizza il menu **Start** .|  
|CTRL+ALT+FINE|Visualizza la finestra di dialogo relativa alla sicurezza di Windows (CTRL+ALT+CANC).|  
|ALT+CANC|Visualizza il menu di Windows.|  
|CTRL+ALT+Segno di sottrazione (sul tastierino numerico)|Copia la finestra attiva del computer locale negli Appunti del computer remoto.|  
|CTRL+ALT+Segno di addizione (sul tastierino numerico)|Copia l'intera area della finestra del computer locale negli Appunti del computer remoto.|  
