---
title: Installare i ruoli per MDM locale
titleSuffix: Configuration Manager
description: Installare i ruoli del sistema del sito richiesti per la gestione dei dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724705"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Installare i ruoli del sistema del sito per MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager gestione di dispositivi mobili (MDM) locale richiede i seguenti ruoli del sistema del sito nel sito Configuration Manager:

- Punto di registrazione

- Punto proxy di registrazione

- Punto di distribuzione

- Punto di gestione dei dispositivi, un punto di gestione che è possibile consentire per i dispositivi mobili

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni

- MDM locale richiede l'abilitazione dei ruoli del sistema del sito per le comunicazioni HTTPS. Per altre informazioni, vedere [configurare i certificati per le comunicazioni attendibili in MDM locale](set-up-certificates-on-premises-mdm.md).

- Current Branch of Configuration Manager supporta solo le connessioni *Intranet* dai dispositivi ai punti di distribuzione e ai punti di gestione dei dispositivi per MDM locale. Tuttavia, se si gestiscono anche computer macOS, questi client richiedono connessioni *Internet* a tali ruoli. Quando si configura il punto di distribuzione e il punto di gestione dei dispositivi, utilizzare l'opzione per **consentire le connessioni Intranet e Internet**.

- I punti di distribuzione configurati per le connessioni Intranet richiedono la configurazione dei limiti del sito. Configuration Manager supporta solo i limiti dell'intervallo IPv4 per MDM locale. Per altre informazioni, vedere [Definire i limiti del sito e i gruppi di limiti](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Se si usano le [repliche di database](../../core/servers/deploy/configure/database-replicas-for-management-points.md) con il punto di gestione dei dispositivi, i dispositivi appena registrati non riusciranno inizialmente a connettersi. Questo errore di connessione si verifica perché la replica di database non contiene le informazioni sul dispositivo appena registrato necessario per una connessione corretta. Le repliche vengono sincronizzate ogni cinque minuti. I dispositivi non riusciranno a connettersi per i primi cinque minuti dopo la registrazione, che in genere è costituito da due tentativi di connessione. I dispositivi si connetteranno correttamente.

## <a name="add-roles"></a>Aggiungere ruoli

Se si aggiunge MDM locale a un sito con la maggior parte dei dispositivi gestiti con il client di Configuration Manager, è possibile che alcuni di questi ruoli siano già installati nel sito. Ad esempio, il punto di distribuzione è un ruolo comune e il punto di gestione dei dispositivi è necessario per gestire i dispositivi macOS.

Per ulteriori informazioni su come aggiungere ruoli al sito, vedere [aggiungere ruoli del sistema del sito](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Configurare i ruoli

Configurare ruoli nuovi o esistenti per la gestione dei dispositivi mobili. Attenersi alla procedura seguente per configurare il punto di distribuzione e il punto di gestione dei dispositivi in modo che funzionino correttamente per MDM locale:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**.

1. Selezionare il server del sistema del sito con il punto di distribuzione o il punto di gestione dei dispositivi che si desidera configurare. Selezionare il server nell'elenco, quindi selezionare il ruolo del **sistema del sito** nel riquadro dei dettagli ruoli del sistema del sito. Nella scheda **ruolo del sito** della barra multifunzione selezionare **Proprietà**.

    > [!TIP]
    > In un sito di grandi dimensioni è possibile definire l'ambito della visualizzazione in modo da visualizzare solo i server con ruoli specifici. Quando si seleziona il nodo **Server e ruoli del sistema del sito** , nella barra multifunzione del tag Home selezionare **server con ruolo**. Selezionare quindi il ruolo desiderato dall'elenco dei ruoli attualmente disponibili nel sito.

    Nella scheda **generale** delle proprietà del **sistema del sito**, assicurarsi che il **nome** sia un nome di dominio completo (FQDN). Chiudere le proprietà.

1. Nell'elenco console selezionare un server con un ruolo di punto di distribuzione locale. Selezionare il ruolo del **punto di distribuzione** nel riquadro dei dettagli ruoli del sistema del sito. Nella scheda **ruolo del sito** della barra multifunzione selezionare **Proprietà**. Nella scheda **comunicazione** delle proprietà del **punto di distribuzione**:

    1. Selezionare **https**e selezionare **Consenti solo connessioni Intranet**.

        > [!IMPORTANT]
        > Se si gestiscono anche computer macOS con il client di Configuration Manager, usare invece **Consenti connessioni Intranet e Internet** .

    1. Abilitare l'opzione per **consentire ai dispositivi mobili di connettersi a questo punto di distribuzione**, quindi chiudere le proprietà.

1. Aprire le proprietà per il ruolo del sistema del sito del **punto di gestione** .

    1. Nella scheda **generale** selezionare **https**e selezionare **Consenti solo connessioni Intranet**.

        > [!IMPORTANT]
        > Se si gestiscono anche computer macOS con il client di Configuration Manager, usare invece **Consenti connessioni Intranet e Internet** .

    1. Abilitare l'opzione per **consentire ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione**, quindi chiudere le proprietà.

        > [!NOTE]
        > Questa opzione consente di trasformare il punto di gestione in un punto di gestione *periferiche* .  

## <a name="next-step"></a>Passaggio successivo

Una volta aggiunti e configurati i ruoli per la gestione dei dispositivi mobili, configurare i server come endpoint attendibili. Questa attendibilità consente ai ruoli di comunicare con e registrare i dispositivi gestiti.

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
