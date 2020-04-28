---
title: Valutazione della compatibilità
titleSuffix: Configuration Manager
description: Informazioni sulla valutazione della compatibilità per le app e i driver di Windows in Desktop Analytics.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eedd33999ce17417122b2403c777a0b560e5f197
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82109999"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Valutazione della compatibilità in Desktop Analytics

Le valutazioni dell'aggiornamento nelle soluzioni precedenti erano generiche, ad esempio: Intervento necessario o Correzione disponibile. Non viene offerto alcun indicatore visivo su come classificare in ordine di priorità app o driver con problemi, né vengono offerte informazioni sull'aggiornamento. Desktop Analytics sostituisce questa funzionalità con **Rischio di compatibilità**. Desktop Analytics visualizza la valutazione per le app solo nella visualizzazione distribuzione per uno scenario di pre-aggiornamento. Classifica le app in base ai dati analitici che Microsoft ottiene dai computer inclusi in un piano di distribuzione corrente.

Desktop Analytics usa le categorie di valutazione della compatibilità seguenti:

- **Bassa**: il servizio non ha rilevato segnali che inducano a ritenere che l'app sia a rischio in un aggiornamento di Windows. È probabile che funzioni nel sistema operativo di destinazione così com'è.

- **Media**: Analytics indica la possibilità che la funzionalità dell'applicazione risulti compromessa, anche se la correzione è probabilmente possibile.

- **Alta**: è quasi certo che l'applicazione non funzionerà durante o dopo l'aggiornamento. Potrebbe essere necessaria una correzione.

- **Sconosciuto**: l'app non è stata valutata. Non sono disponibili altre informazioni dettagliate, ad esempio *Problemi noti di MS*.

Nell'elenco di risorse app o driver in un piano di distribuzione questo valore viene visualizzato per ogni risorsa nella colonna **Rischio di compatibilità**.

## <a name="app-risk-assessment"></a>Valutazione del rischio per le app

![Diagramma delle origini di valutazione del rischio per le app](media/app-risk-assessment-sources.png)

Desktop Analytics usa diverse origini per generare la classificazione della valutazione per le applicazioni:

- [Problemi noti di Microsoft](#microsoft-known-issues)
- [Dati analitici avanzati](#advanced-insights)

È possibile trovare la valutazione per ogni origine nell'app in Desktop Analytics. Nell'elenco di risorse app in un piano di distribuzione selezionare una singola app per aprirne il riquadro a comparsa delle proprietà. Si vedrà un consiglio complessivo e un livello di valutazione. La sezione **Fattori di rischio di compatibilità** visualizza i dettagli di queste valutazioni.

## <a name="microsoft-known-issues"></a>Problemi noti di Microsoft

Desktop Analytics esamina il database di compatibilità delle app Microsoft per individuare eventuali problemi noti. Usa questo database per determinare eventuali blocchi di compatibilità esistenti per le applicazioni disponibili pubblicamente di Microsoft o altri editori. Questo controllo si applica solo al sistema operativo di destinazione per il piano di distribuzione selezionato.

Il riquadro delle proprietà dell'app indica come **Problemi noti di MS** i problemi seguenti:

### <a name="asset-is-removed-during-upgrade"></a>La risorsa viene rimossa durante l'aggiornamento

Windows ha rilevato problemi di compatibilità relativi a un'applicazione o un driver. La migrazione della risorsa alla nuova versione del sistema operativo non verrà eseguita. Per continuare l'aggiornamento, non è necessaria alcuna azione. Installare una versione compatibile dell'applicazione o del driver nella nuova versione del sistema operativo.

<!-- 3594545 -->
Windows può rimuovere queste risorse parzialmente o completamente:

- Rimozione completa: il programma di installazione di Windows rimuove completamente l'app o il driver dal dispositivo durante l'aggiornamento.
- Rimozione parziale: il programma di installazione di Windows rimuove parzialmente l'app o il driver dal dispositivo. È necessaria la disinstallazione manuale dopo l'aggiornamento di Windows.

In entrambi i casi, dopo l'aggiornamento di Windows l'utente non potrà usare l'app o l'hardware associato al driver.

Per vedere questo consiglio nel portale di Desktop Analytics:

1. In un piano di distribuzione selezionare **Preparare il gruppo pilota**.
1. Selezionare la scheda **App**.
1. Selezionare un'app e quindi visualizzare i fattori di rischio di compatibilità e i consigli nel riquadro laterale.

[![Screenshot del consiglio sulla risorsa nel portale di Desktop Analytics](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Blocco dell'aggiornamento

Windows ha rilevato problemi che causano un blocco e non può rimuovere l'applicazione durante l'aggiornamento. Potrebbe non funzionare nella nuova versione del sistema operativo. Prima di eseguire l'aggiornamento, rimuovere l'applicazione. Reinstallarla e testarla nella nuova versione del sistema operativo.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>È in corso il blocco dell'aggiornamento, ma può essere reinstallata dopo l'aggiornamento

L'applicazione è compatibile con la nuova versione del sistema operativo, ma la migrazione non verrà eseguita. Rimuovere l'applicazione prima di aggiornare Windows. Reinstallarla nella nuova versione del sistema operativo.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Blocco dell'aggiornamento, aggiornamento dell'applicazione alla versione più recente

La versione esistente dell'applicazione non è compatibile con la nuova versione del sistema operativo e la migrazione non verrà eseguita. Una versione compatibile dell'applicazione è disponibile. Aggiornare l'applicazione prima dell'aggiornamento.

### <a name="disk-encryption-blocking-upgrade"></a>La crittografia del disco ha causato un blocco dell'aggiornamento

Le funzionalità di crittografia dell'applicazione bloccano l'aggiornamento. Disabilitare la funzionalità di crittografia prima di aggiornare Windows e abilitarla dopo l'aggiornamento.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Non funziona con il nuovo sistema operativo, ma non blocca l'aggiornamento

L'applicazione non è compatibile con la nuova versione del sistema operativo, ma non blocca l'aggiornamento. Per continuare l'aggiornamento, non è necessaria alcuna azione. Installare una versione compatibile dell'applicazione nella nuova versione del sistema operativo.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Non funziona con il nuovo sistema operativo e l'aggiornamento verrà bloccato

L'applicazione non è compatibile con la nuova versione del sistema operativo e l'aggiornamento verrà bloccato. Rimuovere l'applicazione prima dell'aggiornamento. Potrebbe essere disponibile una versione compatibile dell'applicazione.

### <a name="evaluate-application-on-new-os"></a>Valutare l'applicazione con il nuovo sistema operativo

Windows eseguirà la migrazione dell'applicazione, ma ha rilevato problemi che potrebbero influire sulle prestazioni dell'app nella nuova versione del sistema operativo. Per continuare l'aggiornamento, non è necessaria alcuna azione. Testare l'applicazione nella nuova versione del sistema operativo.

### <a name="may-block-upgrade-test-application"></a>Potrebbe bloccare l'aggiornamento, applicazione di prova

Windows ha rilevato problemi che potrebbero interferire con l'aggiornamento, ma sono necessarie ulteriori indagini. Testare il comportamento dell'applicazione durante l'aggiornamento. Se blocca l'aggiornamento, rimuoverla prima dell'aggiornamento. Quindi reinstallarla e testarla nella nuova versione del sistema operativo.

### <a name="multiple"></a>Più elementi

L'applicazione è interessata da molteplici problemi. Selezionare **Query** per vedere i dettagli relativi ai problemi rilevati da Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstallare l'applicazione dopo l'aggiornamento

L'applicazione è compatibile con la nuova versione del sistema operativo, ma è necessario reinstallarla dopo l'aggiornamento di Windows. Il processo di aggiornamento rimuove l'applicazione. Per continuare l'aggiornamento, non è necessaria alcuna azione. Reinstallare l'applicazione nella nuova versione del sistema operativo.

### <a name="safeguards"></a>Misure di sicurezza

<!-- 5746559 -->

I dati di compatibilità di Windows classificano alcune app e driver con una *misura di sicurezza*, che può causare l'esito negativo o il rollback dell'aggiornamento a Windows 10. Windows può anche eseguire l'aggiornamento, ma rimuove l'app o il driver. Desktop Analytics consente ora di identificare queste misure di sicurezza in anticipo, in modo da poter correggere la risorsa prima di distribuire l'aggiornamento.

1. Nel portale di Desktop Analytics selezionare un piano di distribuzione.

1. Selezionare **Risorse del piano** nel menu e passare alla scheda **App**.

1. Filtrare la colonna del nome per visualizzare gli elementi con valori che contengono la parola `Safeguard`. Selezionare il risultato per visualizzare altre informazioni.

    > [!NOTE]
    > Questa voce non è una vera app realmente installata nei dispositivi ma un segnaposto che consente di identificare le app o i driver nell'ambiente in uso con il tag di compatibilità della misura di sicurezza.

1. Nella sezione dei consigli selezionare il collegamento *Altre informazioni*. Questo collegamento apre il sito Web Windows con l'elenco corrente di app o driver con il tag della misura di sicurezza.

1. Confrontare l'elenco pubblicato corrente con l'elenco di risorse nell'ambiente in uso. Correggere eventuali app o driver con potenziali problemi aggiornandoli a una versione compatibile.

[![Screenshot dell'app Safeguard in Desktop Analytics](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="advanced-insights"></a>Dati analitici avanzati

Desktop Analytics può anche rilevare problemi usando i dati analitici supplementari seguenti:

### <a name="adopted-version-available"></a>Versione adottata disponibile

È disponibile un'altra versione dell'app ampiamente adottata da altri clienti. Questo segnale usa i dati di adozione dell'ecosistema Windows. Nel caso la versione corrente determinasse il blocco dell'aggiornamento, valutare la possibilità di distribuire la versione alternativa. Per trovare le versioni alternative dell'applicazione adottate, vedere l'integrità dell'applicazione nella pagina "Prepara produzione".

### <a name="driver-dependency"></a>Dipendenza da driver

L'app dipende da un driver. Desktop Analytics consiglia di sottoporre l'app a test pilota per individuare eventuali regressioni. In caso di problemi, contattare l'editore per richiedere una versione conforme a Windows 10.

### <a name="additional-insights"></a>Dati analitici supplementari

<!-- 4021225 -->
Quando si aggiorna il sito e i client di Configuration Manager alla versione 1906, i client segnalano anche questi dati analitici supplementari, se il livello dei dati di diagnostica è impostato su Avanzata (con limitazioni):

> [!Important]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Questo scenario non funzionerà fin quando anche la versione del client sarà la più recente.

#### <a name="16-bit-apps"></a>App a 16 bit

Rimuovere dalle applicazioni tutti i componenti a 16 bit e sostituirli con equivalenti a 32 o 64 bit. Per altre informazioni, vedere [Storia di Windows Vista e Windows Server 2008 per sviluppatori: guida di riferimento dettagliata sulla compatibilità delle applicazioni](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\)).

L'altra opzione consiste nell'abilitare NT Virtual DOS Machine (NTVDM) per il supporto in Windows 10.

#### <a name="requires-admin-privileges"></a>Richiede privilegi di amministratore

L'app richiede che l'utente abbia l'accesso amministrativo al dispositivo. Usare un manifesto dell'app per le app che richiedono autorizzazioni di amministratore. Per altre informazioni, vedere [Creare e incorporare un manifesto dell'applicazione](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics consiglia di sottoporre l'app a test pilota per individuare eventuali regressioni.

#### <a name="java-dependency"></a>Dipendenza da Java

Molte applicazioni Java si basano su una distribuzione Java Runtime Environment (JRE) installata separatamente. Anche se le versioni meno recenti di JRE possono continuare a funzionare in Windows 10, Oracle supporta solo le versioni più recenti di JRE. L'uso di una versione di JRE meno recente e non supportata può costituire un rischio per la sicurezza. Verificare che l'applicazione usi le versioni di JRE più recenti.

#### <a name="not-dpi-aware"></a>Non sensibile ai valori DPI

L'app potrebbe riscontrare problemi di visualizzazione con risoluzioni dello schermo avanzate in Windows 10. Usare un manifesto dell'app per evitare problemi con alte risoluzioni DPI. Per altre informazioni, vedere [Manifesti dell'applicazione](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Desktop Analytics consiglia di sottoporre l'app a test pilota per individuare eventuali regressioni.

#### <a name="silverlight-framework"></a>Framework Silverlight

Microsoft consiglia di non usare Silverlight per le app non basate su browser. La data di fine supporto per Silverlight 5 è ottobre 2021.

La maggior parte dei Web browser attuali non supporta Silverlight.

| Browser | Supporto |
|---------|---------|
| Google Chrome | Fine supporto: settembre 2015 |
| Firefox | Fine supporto: Marzo 2017 |
| Microsoft Edge | Nessun plug-in disponibile |

Desktop Analytics consiglia di sottoporre l'app a test pilota per individuare eventuali regressioni.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

.NET Framework versione 1.0 non è supportato in Windows 10. La versione 1.1 non è compatibile in Windows 10. Se l'app è di un editore di terze parti, contattare il fornitore per richiedere una versione conforme a Windows 10. Altrimenti sviluppare di nuovo l'applicazione in modo che usi una versione supportata di .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

I framework .NET 2.0 e 3.5 sono supportati in Windows 10. Potrebbe essere necessario abilitare la funzionalità Windows. Per altre informazioni, vedere [Installare .NET Framework 3.5 in Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Accesso all'interfaccia utente

Le applicazioni con accesso all'interfaccia utente possono ignorare i livelli di controllo dell'interfaccia utente per indirizzare l'input verso finestre con privilegi più elevati sul desktop. Usare questa impostazione solo per applicazioni di assistive technology con interfaccia utente.

Se nell'app non vengono usate funzionalità di accessibilità, impostare il flag di accesso all'interfaccia utente nel manifesto dell'app su False. Per altre informazioni, vedere [Creare e incorporare un manifesto dell'applicazione](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics consiglia di sottoporre l'app a test pilota per individuare eventuali regressioni.

## <a name="driver-risk-assessment"></a>Valutazione del rischio per i driver

Desktop Analytics elenca e raggruppa in base alla disponibilità anche tutti i driver di cui non verrà eseguita la migrazione alla versione del sistema operativo.

È possibile trovare la valutazione per il driver in Desktop Analytics. Nell'elenco di risorse driver in un piano di distribuzione selezionare un singolo driver per aprirne il riquadro a comparsa delle proprietà. Si vedrà un consiglio complessivo e un livello di valutazione. La sezione **Fattori di rischio di compatibilità** visualizza i dettagli di queste valutazioni.

| Disponibilità driver | Azione richiesta? | Significato | Indicazioni |
|---------------------|------------------|---------------|----------|
| Disponibile nel prodotto | No, solo per conoscenza | La migrazione della versione attualmente installata di un'applicazione o un driver alla nuova versione del sistema operativo non verrà eseguita. Una versione compatibile viene installata con la nuova versione del sistema operativo. | Per continuare l'aggiornamento, non è necessaria alcuna azione. |
| Importazione da Windows Update | Sì | La migrazione della versione attualmente installata di un driver alla nuova versione del sistema operativo non verrà eseguita. Una versione compatibile è disponibile in Windows Update. | Se il computer riceve automaticamente gli aggiornamenti da Windows Update, non è necessaria alcuna azione. In caso contrario, importare un nuovo driver da Windows Update dopo l'aggiornamento di Windows. |
| Disponibile nel prodotto e in Windows Update | Sì | La migrazione della versione attualmente installata di un driver alla nuova versione del sistema operativo non verrà eseguita. Anche se durante l'aggiornamento viene installato un nuovo driver, una versione più recente è disponibile in Windows Update. | Se il computer riceve automaticamente gli aggiornamenti da Windows Update, non è necessaria alcuna azione. In caso contrario, importare un nuovo driver da Windows Update dopo l'aggiornamento di Windows. |
| Contattare il fornitore | Sì | La migrazione del driver alla nuova versione del sistema operativo non verrà eseguita e Desktop Analytics non riesce a individuare una versione compatibile. | Per una soluzione, contattare il fornitore di hardware indipendente che produce il driver oppure l'OEM (Original Equipment Manufacturer) che ha fornito il dispositivo. |

## <a name="see-also"></a>Vedere anche

Il FastTrack Center Benefit per Windows 10 offre l'accesso a **Desktop App Assure**. Questo vantaggio è un nuovo servizio progettato per risolvere i problemi relativi alla compatibilità di Windows 10 e App di Microsoft 365 per grandi imprese. Per altre informazioni, vedere [Desktop App Assure](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
