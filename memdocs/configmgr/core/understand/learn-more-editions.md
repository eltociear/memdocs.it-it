---
title: Licenze e rami
titleSuffix: Configuration Manager
description: Informazioni sui requisiti di licenza per le opzioni di installazione disponibili con Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906057"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Licenze e rami per Configuration Manager

*Si applica a: Configuration Manager (Current Branch) e System Center Configuration Manager (Long-Term Servicing Branch)*

Questo articolo illustra i requisiti di licenza per le opzioni di installazione disponibili con Configuration Manager. Queste opzioni di installazione includono i rami seguenti:

- Current Branch
- Long-Term Servicing Branch (LTSB)
- Installazione di valutazione di Current Branch
- Technical Preview Branch

## <a name="licensing-overview"></a>Panoramica delle licenze

I clienti con contratti Software Assurance attivi per le licenze di Configuration Manager, o con diritti di sottoscrizione equivalenti alla data 1 ottobre 2016, hanno diritto a usare la versione 1606 di ottobre 2016 di Configuration Manager. I clienti con diritti per Configuration Manager in data 1 ottobre 2016 o successiva, al momento dell'installazione avranno a disposizione due opzioni con licenza: Current Branch e Long-Term Servicing Branch (LTSB).

Per i termini e le condizioni relativi ai prodotti acquistati tramite i programmi multilicenza Microsoft, vedere [Condizioni di licenza e documentazione](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).


## <a name="licensed-branches"></a>Rami con licenza

Questo articolo fa riferimento al contratto Software Assurance o a diritti di sottoscrizione equivalenti. Questo contratto di licenza Microsoft concede i diritti per installare e usare Configuration Manager.

### <a name="current-branch"></a>Current Branch

Current Branch richiede un contratto Software Assurance attivo o diritti equivalenti per Configuration Manager. Per altre informazioni, vedere [Software Assurance e Current Branch](#software-assurance-and-the-current-branch).

Questo ramo è supportato per l'uso in ambienti di produzione per cui si vogliono ottenere regolarmente aggiornamenti qualitativi e funzionali da Microsoft. Consente di usare tutte le funzionalità e tutti i miglioramenti.

A partire dalla versione 1710, ogni versione di aggiornamento continua a essere supportata per 18 mesi dalla data in cui viene resa disponibile a livello generale. Per altre informazioni, vedere [Supporto per le versioni di System Center Configuration Manager Current Branch](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>Long-Term Servicing Branch (LTSB)

Il ramo LTSB richiede un contratto Software Assurance corrente con Microsoft a partire dal 1° ottobre 2016. Per altre informazioni, vedere [Software Assurance e LTSB](#software-assurance-and-the-ltsb).

Questo ramo è supportato per l'uso in ambienti di produzione. È destinato all'uso da parte di clienti che hanno lasciato scadere Software Assurance o diritti di sottoscrizione equivalenti per Configuration Manager dopo il 1° ottobre 2016. Rispetto a Current Branch questo ramo presenta delle limitazioni.

Per questo ramo vengono resi disponibili gli aggiornamenti della sicurezza critici per Configuration Manager ma non vengono rese disponibili le nuove funzionalità.

### <a name="evaluation-installation-of-the-current-branch"></a>Installazione di valutazione di Current Branch

La versione di valutazione non richiede un contratto Software Assurance con Microsoft. Le [installazioni di valutazione](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) sono sempre di Current Branch ed è possibile usarle per 180 giorni.

È possibile aggiornare l'installazione di valutazione a un'installazione completa di Current Branch. Non è possibile aggiornare un'installazione di valutazione a Long-Term Servicing Branch.

### <a name="technical-preview-branch"></a>Technical Preview Branch

È anche disponibile [Technical Preview Branch](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview). Questo ramo è una build limitata di Configuration Manager che consente di provare le nuove funzionalità. È possibile installare la Technical Preview tramite supporti diversi rispetto alle versioni con licenza. Per altre informazioni, vedere [Technical Preview](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Contratti Software Assurance

Lo stato di Software Assurance per le licenze di Configuration Manager o diritti di sottoscrizione equivalenti, il 1° ottobre 2016 o in data successiva, determina il ramo che è possibile installare e usare.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance e Current Branch

I diritti per l'uso di Configuration Manager Current Branch sono forniti da:

- **System Center:** i clienti con sottoscrizione Software Assurance attiva per licenze System Center Standard o Datacenter possono installare e usare l'opzione Current Branch di Configuration Manager.

- **System Center Configuration Manager:** i clienti con sottoscrizione Software Assurance attiva per licenze di Configuration Manager o con diritti di sottoscrizione equivalenti possono installare e usare l'opzione Current Branch di Configuration Manager.

Se si ha una sottoscrizione Software Assurance attiva per le licenze di Configuration Manager o diritti di sottoscrizione equivalenti il 1° ottobre 2016 o in data successiva:

- È possibile installare e usare Current Branch.
- Se si lascia scadere la sottoscrizione Software Assurance, è necessario disinstallare Current Branch.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance e LTSB

Se si ha una sottoscrizione Software Assurance attiva per le licenze di Configuration Manager o diritti di sottoscrizione equivalenti il 1° ottobre 2016 o in data successiva:

- È possibile installare e usare LTSB. I clienti che hanno diritti perpetui su Configuration Manager o lasciano scadere la sottoscrizione Software Assurance o equivalente possono installare la versione di Configuration Manager LTSB corrente al momento della scadenza.

LTSB si basa sulla versione Current Branch 1606, con le limitazioni seguenti:

- La conversione da Current Branch a LTSB non è supportata. Se si ha un sito Current Branch, è necessario installare LTSB come nuovo sito.  

- LTSB non supporta tutte le funzionalità di Current Branch. Per altre informazioni, vedere [Introduzione a Long-Term Servicing Branch](introduction-to-the-ltsb.md). Queste limitazioni prevedono un set limitato di funzionalità, opzioni di aggiornamento limitate e un ciclo di vita separato per il supporto del prodotto.  

### <a name="software-assurance-expiration-date"></a>Data di scadenza di Software Assurance

A partire dalla versione di ottobre 2016 del supporto di base 1606 per Configuration Manager, è possibile specificare la data di scadenza del contratto Software Assurance. La **data di scadenza di Software Assurance** è un valore facoltativo con la funzione di semplice promemoria. Aggiungerla quando di esegue l'installazione di Configuration Manager o in un secondo momento nella console di Configuration Manager.

> [!NOTE]
> Microsoft non convalida la data di scadenza specificata e non usa tale data per la convalida della licenza. Usarla come promemoria della data di scadenza. Questo valore è utile quando Configuration Manager verifica periodicamente la disponibilità di nuovi aggiornamenti software online. Lo stato della licenza di Software Assurance deve essere valido per poter usufruire di tali aggiornamenti aggiuntivi.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Per specificare la data di scadenza di Software Assurance

- Quando si esegue il programma di installazione dal supporto di Configuration Manager, specificare il valore nella pagina **Codice Product Key** dell'installazione guidata.

- Specificare il valore nella scheda **Gestione licenze** di **Impostazioni gerarchia** nella console di Configuration Manager.


## <a name="licensing-resources"></a>Risorse relative alle licenze

Per altri dettagli sulle licenze dei prodotti, usare le risorse seguenti.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Centro servizi per contratti multilicenza

- [Panoramica del Centro servizi per contratti multilicenza](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Termini per i contratti multilicenza Microsoft per i prodotti](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- I clienti che hanno acquistato contratti multilicenza possono ottenere un riepilogo delle proprie licenze dal [Centro servizi per contratti multilicenza](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Dal menu **Licenze** scegliere **Riepilogo licenze**.

### <a name="vlsc-videos"></a>Video sul Centro servizi per contratti multilicenza

- Per video di formazione sul funzionamento del Centro servizi per contratti multilicenza, passare a [Microsoft Volume Licensing Service Center training and resources](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) (Formazione e risorse sul Centro servizi per contratti multilicenza MIcrosoft) e selezionare **How-to videos** (Video pratici).

- [Dove cercare il proprio contratto Software Assurance](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (a 43 secondi dall'inizio)  

- [Come ottenere le autorizzazioni per il Centro servizi per contratti multilicenza](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). È possibile delegare le autorizzazioni in lettura e scrittura per il Centro servizi per contratti multilicenza ad altri utenti nell'organizzazione.
