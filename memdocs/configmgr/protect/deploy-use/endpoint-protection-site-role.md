---
title: Creare un ruolo del sistema del sito del punto di Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come configurare Endpoint Protection per gestire la sicurezza e i malware nei computer client di Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690319"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Creare un ruolo del sistema del sito del punto di Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*

Prima di poter usare Endpoint Protection, è necessario installare il ruolo del sistema del sito Punto di Endpoint Protection. Il ruolo deve essere installato in un solo server di sistema del sito, al livello superiore della gerarchia in un sito di amministrazione centrale o un sito primario autonomo.

Usare una delle procedure seguenti a seconda che si voglia installare un nuovo server di sistema del sito per Endpoint Protection o usare un server di sistema del sito esistente:
- [Installare in un nuovo server di sistema del sito](#new-site-system-server)
- [Installare in un server di sistema del sito esistente](#existing-site-system-server)

> [!IMPORTANT]
>  Quando si installa un punto di Endpoint Protection, un client di Endpoint Protection viene installato nel server che ospita il punto di Endpoint Protection. Analisi e servizi sono disabilitati in questo client per consentirne la coesistenza con qualsiasi soluzione antimalware esistente installata nel server. Se in seguito si abilita il server per la gestione con Endpoint Protection e si seleziona l'opzione per rimuovere qualsiasi soluzione antimalware di terze parti, il prodotto di terze parti non verrà rimosso. È necessario disinstallare il prodotto manualmente.

## <a name="new-site-system-server"></a>nuovo server del sistema del sito

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, quindi fare clic su **Server e ruoli del sistema del sito**.

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**.

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di Endpoint Protection** nell'elenco di ruoli disponibili e quindi fare clic su **Avanti**.

6.  Nella pagina **Endpoint Protection** selezionare la casella di controllo **Accetto le condizioni di licenza di Endpoint Protection** e quindi fare clic su **Avanti**.

    > [!IMPORTANT]
    >  Non è possibile usare Endpoint Protection in Configuration Manager se non si accettano le condizioni di licenza.

7.  Nella pagina **Cloud Protection Service** selezionare il livello di informazioni da inviare a Microsoft per supportare lo sviluppo di nuove definizioni e quindi fare clic su **Avanti**.

    > [!NOTE]
    >  Questa opzione consente di configurare le impostazioni di Cloud Protection Service (precedentemente denominato Microsoft Active Protection Service o MAPS) usate per impostazione predefinita. È quindi possibile configurare le impostazioni personalizzate per ogni criterio antimalware creato. Cloud Protection Service consente di mantenere i computer più sicuri offrendo a Microsoft esempi di malware in modo che possa mantenere le definizioni antimalware il più aggiornate possibile. Se si usa Cloud Protection Service, il client di Endpoint Protection può usare Dynamic Signature Service per scaricare le nuove definizioni prima che vengano pubblicate in Windows Update. Per altre informazioni, vedere [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md).

8.  Completare la procedura guidata.


## <a name="existing-site-system-server"></a>server del sistema del sito esistente

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, fare clic su **Server e ruoli del sistema del sito** e quindi selezionare il server che si vuole usare per Endpoint Protection.

3.  Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**.

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di Endpoint Protection** nell'elenco di ruoli disponibili e quindi fare clic su **Avanti**.

6.  Nella pagina **Endpoint Protection** selezionare la casella di controllo **Accetto le condizioni di licenza di Endpoint Protection** e quindi fare clic su **Avanti**.

    > [!IMPORTANT]
    >  Non è possibile usare Endpoint Protection in Configuration Manager se non si accettano le condizioni di licenza.

7.  Nella pagina **Cloud Protection Service** selezionare il livello di informazioni da inviare a Microsoft per supportare lo sviluppo di nuove definizioni e quindi fare clic su **Avanti**.

    > [!NOTE]
    >  Questa opzione consente di configurare le impostazioni di Cloud Protection Service, precedentemente denominato MAPS, usate per impostazione predefinita. È possibile definire impostazioni personalizzate per ogni criterio antimalware configurato. Per altre informazioni, vedere [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md).

8.  Completare la procedura guidata.
