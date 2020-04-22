---
title: Funzionalità nella Technical Preview 1611
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1611 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e1348e9d230a5525a91e7e7dceea4da6d1311b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705469"
---
# <a name="capabilities-in-technical-preview-1611-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1611 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*



Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1611. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    

**Problemi noti di questa versione Technical Preview:**   
- ***Stato dei prerequisiti***: quando si installa la versione 1611, lo stato generale dei prerequisiti corrisponde a Controllo prerequisiti superato con avvisi, ma i prerequisiti che hanno causato gli avvisi non vengono visualizzati. Ciò può essere causato dai due prerequisiti seguenti:
  - Opzioni della memoria di creazione indici di SQL
  - Controlli per la versione di SQL Server supportata  

  Poiché si tratta solo di avvisi, possono essere ignorati.

- ***PowerShell***: Quando ci si connette a Windows PowerShell dalla console di Configuration Manager, potrebbe essere visualizzato l'errore seguente: **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml is not digitally signed** (Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml senza firma digitale).  

   È possibile risolvere questo problema sostituendo determinati file con le versioni firmate corrispondenti della versione 1610. Dalla cartella **&lt;directory di installazione>\AdminConsole\bin\\** della versione 1610 copiare tutti i file con le estensioni seguenti: **psd1**, **ps1xml** e **psm1**. Incollare questi file nella cartella **&lt;directory di installazione>\AdminConsole\bin\\** della versione Technical Preview 1611, sovrascrivendo la versione 1611 dei file.


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Pre-cache del contenuto per le distribuzioni e le sequenze di attività disponibili
In questa Technical Preview, per le distribuzioni e le sequenze di attività disponibili è possibile scegliere di usare la funzionalità di pre-cache. In questo modo, prima che gli utenti installino il contenuto, i client scaricheranno solo il contenuto pertinente.

Si supponga ad esempio di voler distribuire una sequenza di attività di aggiornamento sul posto di Windows 10, di volere una sola sequenza di attività per tutti gli utenti e di avere più architetture e/o lingue. Se si crea una distribuzione disponibile in Current Branch, il contenuto viene scaricato quando l'utente fa clic su **Installa** in Software Center. Ciò prolunga il tempo che precede l'avvio dell'installazione. In alternativa, se si crea una sequenza di attività disponibile in Current Branch, viene scaricato tutto il contenuto a cui la sequenza di attività fa riferimento, compreso il pacchetto di aggiornamento del sistema operativo per tutte le lingue e per tutte le architetture. Se le dimensioni di ciascun pacchetto sono circa 3 GB, il pacchetto di download può avere dimensioni notevoli.

Con la funzionalità di pre-cache del contenuto è possibile consentire al client di scaricare solo il contenuto applicabile non appena riceve la distribuzione. Pertanto quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto e l'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale.

### <a name="to-configure-the-pre-cache-feature"></a>Per configurare la funzionalità di pre-cache

1. Creare pacchetti di aggiornamento del sistema operativo per lingue e architetture specifiche. Specificare l'architettura e della lingua nella scheda **Origine dati** del pacchetto. Per la lingua usare la conversione decimale. Ad esempio, 1033 è il valore decimale per l'inglese e 0x0409 è il corrispondente valore esadecimale. Per i dettagli, vedere [Creare una sequenza di attività per aggiornare un sistema operativo](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

    I valori relativi all'architettura e alla lingua usati devono rispettare le condizioni dei passaggi della sequenza di attività che verranno creati nel passaggio successivo, per determinare se sia necessario usare la funzionalità di pre-cache per i pacchetti di aggiornamento del sistema operativo.
2. Creare una sequenza di attività con passaggi condizionali per le diverse lingue e le diverse architetture. Per la versione inglese, ad esempio, è possibile creare un passaggio simile al seguente:

    ![proprietà pre-cache](media/precacheproperties2.png)

    ![opzioni pre-cache](media/precacheoptions2.png)  

3. Distribuire la sequenza di attività. Per la funzionalità di pre-cache configurare le impostazioni seguenti:
    - Nella scheda **Generale** selezionare **Pre-download del contenuto per questa sequenza di attività**.
    - Nella scheda **Impostazioni di distribuzione** configurare la sequenza di attività selezionando **Disponibile** per **Scopo**. Se si crea una distribuzione **obbligatoria** la funzionalità di pre-cache non funziona.
    - Per l'impostazione **Pianifica quando questa distribuzione diventerà disponibile** della scheda **Pianificazione**, scegliere un'ora nel futuro che garantisca ai client tempo sufficiente per la funzionalità di pre-cache del contenuto, prima che la distribuzione venga resa disponibile agli utenti. È ad esempio possibile concedere alla funzionalità di pre-cache del contenuto un periodo di 3 ore nel futuro.  
    - Nella scheda **Punti di distribuzione** configurare le impostazioni **Opzioni di distribuzione**. Se in un client non è stata eseguita la funzione di pre-cache per il contenuto prima che l'utente avvii l'installazione, vengono usate queste impostazioni.


### <a name="user-experience"></a>Esperienza utente
- Quando il client riceve i criteri di distribuzione, avvia la funzione di pre-cache del contenuto, ovvero di tutto il contenuto a cui si fa riferimento (eventuali altri tipi di pacchetti) e del pacchetto di aggiornamento del solo sistema operativo corrispondente a quello del client, in base alle condizioni impostate nella sequenza di attività.
- Quando la distribuzione viene resa disponibile agli utenti (impostazione nella scheda **Pianificazione** della distribuzione), una notifica informa gli utenti della nuova distribuzione e la distribuzione stessa diventa visibile in Software Center. Per avviare l'installazione l'utente può passare a Software Center e fare clic su **Installa**.
- Se la funzione di pre-cache del contenuto non è stata eseguita completamente, vengono usate le impostazioni specificate nella scheda **Opzioni di distribuzione** della distribuzione. È consigliabile lasciare un periodo sufficiente tra il momento in cui si crea la distribuzione e l'ora in cui la distribuzione stessa diventa disponibile per gli utenti, per consentire ai client di eseguire in tempo la funzione di pre-cache del contenuto.


## <a name="see-also"></a>Vedere anche
[Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md)
