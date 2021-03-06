---
title: Aggiungere un'app line-of-business per Windows a Microsoft Intune
titleSuffix: ''
description: Informazioni su come aggiungere un'app line-of-business (LOB) per Windows usando Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f81c5f82-5cfa-4b97-9f73-d6cf77c06896
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b70f36873200d0adbbc356d9a482cf13cc2ea49
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913325"
---
# <a name="add-a-windows-line-of-business-app-to-microsoft-intune"></a>Aggiungere un'app line-of-business per Windows a Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Un'app line-of-business è un'app che viene aggiunta da un apposito file di installazione. Questo tipo di app viene in genere scritto internamente. I passaggi seguenti forniscono istruzioni per l'aggiunta di un'app LOB per Windows a Microsoft Intune.

> [!IMPORTANT]
> Quando si distribuiscono app Win32 usando un file di installazione con estensione msi (incluso in un file con estensione intunewin tramite lo strumento di preparazione del contenuto), provare a usare l'[estensione di gestione di Intune](../apps/intune-management-extension.md). Se vengono installate sia app Win32 sia app line-of-business durante la registrazione di Autopilot, l'installazione dell'app potrebbe non riuscire.  

## <a name="select-the-app-type"></a>Selezionare il tipo di app

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Tutte le app** > **Aggiungi**.
3. Tra i tipi di app in **Altro** nel riquadro **Seleziona il tipo di app** selezionare **App line-of-business**.
4. Fare clic su **Seleziona**. Verrà visualizzata la procedura **Aggiungi app**.

## <a name="step-1---app-information"></a>Passaggio 1 - Informazioni sull'app

### <a name="select-the-app-package-file"></a>Selezionare il file del pacchetto dell'app

1. Nel riquadro **Aggiungi app** fare clic su **Selezionare il file del pacchetto di app**. 
2. Nel riquadro **File del pacchetto dell'app** selezionare il pulsante Sfoglia. Selezionare quindi un file di installazione Windows con estensione **msi**, **appx** o **appxbundle**.
   Verranno visualizzati i dettagli dell'app.

    > [!NOTE]
    > Le estensioni file per le app di Windows ora includono **msi**, **appx**, **appxbundle**, **msix** e **msixbundle**. Per altre informazioni su **msix** vedere gli articoli [Documentazione di MSIX](/windows/msix/) e [Distribuzione di app MSIX](/windows/msix/desktop/managing-your-msix-deployment-enterprise).

3. Al termine, selezionare **OK** nel riquadro **File del pacchetto dell'app** per aggiungere l'app.

### <a name="set-app-information"></a>Impostare le informazioni sull'app

1. Nella pagina **Informazioni sull'app** aggiungere i dettagli relativi all'app. A seconda dell'app scelta, è possibile che alcuni valori nel riquadro vengano compilati automaticamente.
    - **Nome**: immettere il nome dell'app che viene visualizzato nel portale aziendale. Verificare che tutti i nomi di app usati siano univoci. Se il nome di un'app è usato due volte, solo una delle due app viene visualizzata nel portale aziendale.
    - **Descrizione**: immettere la descrizione dell'app. La descrizione viene visualizzata nel portale aziendale.
    - **Autore**: Immettere il nome dell'autore dell'app.
    - **Contesto di installazione dell'app**: selezionare il contesto di installazione da associare all'app. Per le app dual mode, selezionare il contesto desiderato per l'app. Per tutte le altre app, questa opzione è preselezionata in base al pacchetto e non può essere modificata.
    - **Ignora la versione dell'app**: impostare su **Sì** se lo sviluppatore dell'app aggiorna automaticamente l'app. Questa opzione si applica solo alle app MSI per dispositivi mobili.
    - **Argomenti della riga di comando**: immettere gli argomenti della riga di comando da applicare per l'esecuzione del file con estensione msi (facoltativo).  Un esempio è **/q**. Non includere il comando msiexec o gli argomenti, ad esempio **/i** oppure **/x**, perché vengono usati automaticamente. Per altre informazioni, vedere [Opzioni della riga di comando](/windows/desktop/Msi/command-line-options). Se il file MSI richiede opzioni aggiuntive della riga di comando, considerare la possibilità di usare la [gestione delle app Win32](app-management.md).
    - **Categoria**: selezionare una o più categorie di app predefinite o una categoria creata dall'utente. Le categorie consentono agli utenti di trovare più facilmente l'app nel portale aziendale.
    - **Visualizza come app in primo piano nel portale aziendale**: Visualizzare chiaramente l'app nella pagina principale del portale aziendale quando gli utenti cercano le app.
    - **URL di informazioni**: Immettere l'URL di un sito Web che include informazioni sull'app (facoltativo). L'URL viene visualizzato nel portale aziendale.
    - **URL privacy**: Immettere l'URL di un sito Web che include informazioni sulla privacy per l'app (facoltativo). L'URL viene visualizzato nel portale aziendale.
    - **Sviluppatore**: immettere il nome dello sviluppatore dell'app (facoltativo).
    - **Proprietario**: immettere un nome per il proprietario dell'app (facoltativo). Un esempio è **Reparto risorse umane**.
    - **Note**: immettere eventuali note da associare a questa app.
    - **Logo**: caricare un'icona che viene associata all'app. Questa icona viene visualizzata con l'app quando gli utenti visitano il portale aziendale.
2. Fare clic su **Avanti** per visualizzare la pagina **Tag di ambito**.

## <a name="step-2---select-scope-tags-optional"></a>Passaggio 2: selezionare i tag di ambito (facoltativo)

È possibile usare i tag di ambito per determinare chi può visualizzare le informazioni sull'app client in Intune. Per informazioni dettagliate complete sui tag di ambito, vedere [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito).

1. Fare clic su **Selezionare i tag di ambito** per aggiungere facoltativamente tag di ambito per l'app. 
2. Fare clic su **Avanti** per visualizzare la pagina **Assegnazioni**.

## <a name="step-3---assignments"></a>Passaggio 3: assegnazioni

1. Per l'assegnazione dell'app a gruppi, selezionare **Obbligatoria**, **Disponibile per i dispositivi registrati** o **Disinstalla**. Per altre informazioni, vedere [Aggiungere gruppi per organizzare utenti e dispositivi](../fundamentals/groups-add.md) e [Assegnare app ai gruppi con Microsoft Intune](apps-deploy.md).
2. Fare clic su **Avanti** per visualizzare la pagina **Rivedi e crea**.

## <a name="step-4---review--create"></a>Passaggio 4 - Verifica e creazione

1. Verificare i valori e le impostazioni immessi per l'app.
2. Al termine, fare clic su **Crea** per aggiungere l'app a Intune.

    Verrà visualizzato il pannello **Panoramica** per l'app line-of-business.

L'app creata viene ora visualizzata nell'elenco di app. Dall'elenco è possibile assegnare le app ai gruppi scelti. Per altre informazioni, vedere [Come assegnare app ai gruppi](apps-deploy.md).

## <a name="update-a-line-of-business-app"></a>Aggiornare un'app line-of-business

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

   > [!NOTE]
   > Per consentire al servizio Intune di distribuire correttamente un nuovo file APPX nel dispositivo, è necessario incrementare la stringa `Version` nel file AppxManifest.xml del pacchetto APPX.

## <a name="configure-a-self-updating-mobile-msi-app-to-ignore-the-version-check-process"></a>Configurare un'app MSI per dispositivi mobili con aggiornamento automatico per ignorare il processo di controllo delle versioni

È possibile configurare un'app MSI per dispositivi mobili con aggiornamento automatico nota in modo che ignori il processo di controllo delle versioni.

Alcune app basate sul programma di installazione MSI vengono aggiornate automaticamente dallo sviluppatore o con un altro metodo. Per queste app MSI con aggiornamento automatico, è possibile configurare l'impostazione **Ignora la versione dell'app** nel riquadro **Informazioni sull'app**. Se si cambia questa impostazione in **Sì**, Microsoft Intune non imporrà la versione dell'app installata nel client Windows.

Questa funzionalità consente di evitare una race condition. Ad esempio, può verificarsi una race condition quando l'app viene aggiornata automaticamente dallo sviluppatore dell'app e viene aggiornata da Intune. In entrambi i casi è possibile che si provi a imporre una versione dell'app in un client di Windows creando un conflitto.

## <a name="next-steps"></a>Passaggi successivi

- L'app creata viene visualizzata nell'elenco di app. È ora possibile assegnarla ai gruppi scelti. Per altre informazioni, vedere [Come assegnare app ai gruppi](apps-deploy.md).

- Altre informazioni sulle modalità in cui è possibile monitorare le proprietà e l'assegnazione dell'app. Vedere [Come monitorare le informazioni sulle app e le assegnazioni](apps-monitor.md).

- Altre informazioni sul contesto dell'app in Intune. Vedere [Panoramica del ciclo di vita dell'app in Microsoft Intune](app-lifecycle.md).

- Altre informazioni sulle app Win32. Vedere [Gestione delle app Win32](apps-win32-app-management.md).