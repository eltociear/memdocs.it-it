---
title: Personalizzare il portale self-service
titleSuffix: Configuration Manager
description: Aggiungere informazioni personalizzate specifiche dell'organizzazione al portale self-service di gestione di BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa7f95e18775862427254839a2aab2c229e31057
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697331"
---
# <a name="customize-the-self-service-portal"></a>Personalizzare il portale self-service

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Dopo aver [installato il portale self-service di BitLocker](setup-websites.md), è possibile personalizzarlo per la propria organizzazione. Aggiungere un avviso personalizzato, il nome della propria organizzazione e altre informazioni specifiche dell'organizzazione.

## <a name="branding"></a>Personalizzazione

Personalizzare il portale self-service con il nome della propria organizzazione, l'URL dell'help desk e un testo di avviso.

1. Accedere come amministratore al server Web che ospita il portale self-service.

1. Avviare **Gestione Internet Information Services (IIS)** (eseguire **inetmgr.exe**).

1. Espandere **Siti**, espandere **Sito Web predefinito** e selezionare il nodo **SelfService**. Nel gruppo **ASP.NET** del riquadro dei dettagli aprire **Impostazioni applicazione**.

    [![schermata di esempio delle impostazioni dell'applicazione SelfService in Gestione IIS](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Selezionare l'elemento da modificare e selezionare **Modifica** nel riquadro **Azioni**. Modificare il **Valore** con il nuovo nome che si vuole usare.

    > [!CAUTION]
    > Non modificare i valori **Nome**. Ad esempio, non modificare `CompanyName`, modificare `Contoso IT`. Se si modificano i valori **Nome**, il portale self-service non funzionerà più.

Le modifiche hanno effetto immediato.

### <a name="supported-branding-values"></a>Valori di personalizzazione supportati

I valori che è possibile impostare sono riportati nella tabella seguente:

|Name|Descrizione|Valore&nbsp;predefinito|
|--- |--- |--- |
|CompanyName|Nome dell'organizzazione visualizzato nel portale self-service come intestazione nella parte superiore di ogni pagina.|`Contoso IT`|
|DisplayNotice|Visualizza un avviso iniziale che l'utente deve confermare.|`true`|
|HelpdeskText|Stringa nel riquadro destro sotto a "For all other related issues" (Per tutti gli altri problemi correlati)|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|Collegamento per la stringa HelpdeskText.|(vuoto)|
|NoticeTextPath|Testo di avviso iniziale che l'utente deve confermare. Per impostazione predefinita, il percorso completo sul server Web è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`. Modificare e salvare il file in un editor di testo normale. Il valore di questo percorso è relativo all'applicazione SelfService.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Per uno screenshot del portale self-service predefinito, vedere [Portale self-service di BitLocker](self-service-portal.md).

> [!TIP]
> Se necessario, è possibile localizzare alcune di queste stringhe per visualizzarle in lingue diverse. Per altre informazioni, vedere [Localizzazione](#bkmk_localize).

## <a name="session-time-out"></a>Timeout sessione

Per fare in modo che la sessione di un utente scada dopo un periodo di inattività specificato, è possibile modificare l'impostazione relativa al timeout sessione per il portale self-service.

1. Accedere come amministratore al server Web che ospita il portale self-service.

1. Avviare **Gestione Internet Information Services (IIS)** (eseguire **inetmgr.exe**).

1. Espandere **Siti**, espandere **Sito Web predefinito** e selezionare il nodo **SelfService**. Nel gruppo **ASP.NET** del riquadro dei dettagli aprire **Stato sessione**.

1. Nel gruppo **Impostazioni cookie** modificare il valore di **Timeout (in minuti)** . Si tratta del numero di minuti dopo i quali la sessione utente scade. Il valore predefinito è `5`. Per disabilitare questa impostazione in modo da disattivare il timeout, impostare il valore su `0`.

1. Nel riquadro **Azioni** selezionare **Applica**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a> Localizzare il testo e l'URL dell'help desk

È possibile configurare le versioni localizzate dell'istruzione `HelpdeskText` e del link `HelpdeskUrl` del portale self-service. Questa stringa informa gli utenti su come ottenere supporto aggiuntivo durante l'uso del portale. Se si configura il testo localizzato, nel portale viene visualizzata la versione localizzata per i Web browser nella lingua scelta. Se non è possibile trovare una versione localizzata, nelle impostazioni `HelpdeskText` e `HelpdeskUrl` viene visualizzato il valore predefinito.

1. Accedere come amministratore al server Web che ospita il portale self-service.

1. Avviare **Gestione Internet Information Services (IIS)** (eseguire **inetmgr.exe**).

1. Espandere **Siti**, espandere **Sito Web predefinito** e selezionare il nodo **SelfService**. Nel gruppo **ASP.NET** del riquadro dei dettagli aprire **Impostazioni applicazione**.

1. Nel riquadro **Azioni** selezionare **Aggiungi**.

1. Nella finestra **Aggiungi impostazione applicazione** configurare i valori seguenti:

    - **Nome**: immettere `HelpdeskText_<language>`, dove `<language>` è il codice della lingua per il testo.

      Ad esempio, per creare un'istruzione `HelpdeskText` localizzata in spagnolo (Spagna), il nome è `HelpdeskText_es-es`.

    - **Valore**: la stringa localizzata da visualizzare nel riquadro destro del portale self-service sotto a "For all other related issues" (Per tutti gli altri problemi correlati)

1. Selezionare **OK** per salvare la nuova impostazione.

1. Ripetere questa procedura per aggiungere una nuova impostazione applicazione per `HelpdeskUrl_<language>` corrispondente all'impostazione `HelpdeskText_<language>` associata.

Ripetere questa procedura per aggiungere una coppia di impostazioni per tutte le lingue supportate nell'organizzazione.

## <a name="localize-the-notice-file"></a>Localizzare il file di avviso

È possibile configurare le versioni localizzate dell'avviso iniziale che l'utente deve confermare nel portale self-service. Per impostazione predefinita, il percorso completo sul server Web è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`.

Per visualizzare il testo di avviso localizzato, creare un file notice.txt localizzato. Salvarlo quindi in una cartella della lingua specifica. Ad esempio: `Self Service Website\es-es\Notice.txt` per lo spagnolo (Spagna).

Il portale self-service visualizza il testo di avviso in base alle regole seguenti:

- Se il file di avviso predefinito non è disponibile, il portale visualizza un messaggio che indica che il file predefinito è mancante.

- Se si crea un file di avviso localizzato nella cartella della lingua appropriata, viene visualizzato il testo dell'avviso localizzato.

- Se il server Web non trova una versione localizzata del file di avviso, visualizza il testo di avviso predefinito.

- Se l'utente imposta il browser su una lingua che non ha un avviso localizzato, il portale visualizza l'avviso predefinito.

### <a name="create-a-localized-notice-file"></a>Creare un file di avviso localizzato

1. Accedere come amministratore al server Web che ospita il portale self-service.

1. Creare una cartella `<language>` per ogni lingua supportata nel percorso dell'applicazione `Self Service Website`. Ad esempio, `es-es` per spagnolo (Spagna). Per impostazione predefinita, il percorso completo è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`.

    Per un elenco dei codici lingua validi che è possibile usare, vedere [National Language Support (NLS) API Reference](/windows/win32/intl/locale-identifiers#predefined-locale-identifiers) (Riferimento API NLS).

    > [!TIP]
    > Il nome della cartella della lingua può essere anche il nome della lingua di sistema. Ad esempio, **es** per spagnolo, anziché **es-es** per spagnolo (Spagna) e **es-ar** per spagnolo (Argentina). Se l'utente imposta il browser su **es-es**e la cartella della lingua non esiste, il server Web controlla in modo ricorsivo la cartella delle impostazioni locali **padre**. (Le impostazioni locali padre sono definite in .NET.) Ad esempio, `Self Service Website\es\Notice.txt`. Questo fallback ricorsivo simula le regole di caricamento delle risorse .NET.

1. Creare una copia del file di avviso predefinito con il testo localizzato. Salvarlo nella cartella per il codice della lingua. Ad esempio, per spagnolo (Spagna), il percorso completo è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt` per impostazione predefinita.

Ripetere questa procedura per un file di avviso localizzato per tutte le lingue supportate nell'organizzazione.

## <a name="next-steps"></a>Passaggi successivi

Ora che il portale self-service è stato installato e personalizzato, è possibile provare a usarlo. Per altre informazioni, vedere [Portale self-service di BitLocker](self-service-portal.md).