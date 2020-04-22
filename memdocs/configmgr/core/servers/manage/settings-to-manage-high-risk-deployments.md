---
title: Gestire le distribuzioni ad alto rischio
titleSuffix: Configuration Manager
description: Configurare le impostazioni del sito di verifica della distribuzione in Configuration Manager per avvisare gli amministratori nel caso in cui creino una distribuzione ad alto rischio.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703299"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Impostazioni per gestire le distribuzioni ad alto rischio per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager è possibile configurare le impostazioni del sito di *verifica della distribuzione*. Queste impostazioni avvisano gli amministratori se creano una distribuzione di sequenza di attività ad alto rischio. Una distribuzione ad alto rischio è:  

- Una distribuzione che viene installata automaticamente  

- Una distribuzione che può causare potenzialmente risultati indesiderati  

Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** che distribuisce un sistema operativo viene considerata come distribuzione ad alto rischio.  

> [!WARNING]
> Se si usano distribuzioni PXE e si configura l'hardware dei dispositivi con la scheda di rete come primo dispositivo di avvio, questi dispositivi possono avviare automaticamente una sequenza di attività di distribuzione del sistema operativo senza l'intervento dell'utente. Questa configurazione non viene gestita dalla procedura di verifica della distribuzione. Se da un lato questa configurazione può semplificare il processo e ridurre l'interazione dell'utente, dall'altro aumenta il rischio di ricreazione accidentale dell'immagine del dispositivo.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a> Impostazioni di verifica della distribuzione

Per ridurre l'incidenza di distribuzioni ad alto rischio indesiderate, è possibile configurare limiti di dimensioni nelle impostazioni di verifica della distribuzione seguenti:  

- **Limiti delle dimensioni della raccolta**: quando si crea una distribuzione, nascondere le raccolte che includono più client del limite consentito.  

  - **Dimensioni predefinite**: quando si crea una distribuzione, per impostazione predefinita, questa impostazione nasconde le raccolte che includono più client rispetto a questo limite. È comunque possibile visualizzare queste raccolte durante la creazione della distribuzione, ma sono nascoste per impostazione predefinita. Il valore predefinito è **100**. Per ignorare questa impostazione, immettere un valore pari a **0**.  

  - **Dimensioni massime**: quando si crea una distribuzione, questa impostazione nasconde sempre le raccolte con più client rispetto a questo limite. Il valore predefinito è **0**, che consente di ignorare l'impostazione. Il valore per **Dimensioni massime** deve essere superiore al valore per **Dimensione predefinita** .  

    Ad esempio, si imposta **Dimensioni predefinite** su 100 e **Dimensioni massime** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** vengono visualizzate solo le raccolte che includono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  

- **Raccolte con i server del sistema del sito**: quando la raccolta di destinazione contiene un computer con un ruolo del sistema del sito, bloccare le distribuzioni o richiedere la verifica prima della creazione della distribuzione. Quando viene bloccata una distribuzione, selezionare una raccolta diversa che soddisfi i criteri di verifica della distribuzione per continuare a creare la distribuzione.  

> [!NOTE]
> Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**.  

## <a name="configure-deployment-verification"></a>Configurare la verifica della distribuzione

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito**, selezionare **Siti** e quindi selezionare il sito primario da configurare.

2. Nella barra multifunzione selezionare **Proprietà** e quindi passare alla scheda **Verifica della distribuzione**.

3. Configurare le [impostazioni](#bkmk_settings) che si vuole usare e quindi scegliere **OK** per salvare la configurazione e chiudere le proprietà.

## <a name="next-steps"></a>Passaggi successivi

[Gestire le sequenze di attività: impostazioni ad alto impatto](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Configurare siti e gerarchie](../deploy/configure/configure-sites-and-hierarchies.md)
