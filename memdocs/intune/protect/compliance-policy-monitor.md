---
title: Monitorare i criteri di conformità dei dispositivi in Microsoft Intune - Azure | Microsoft Docs
description: Usare il dashboard di conformità dei dispositivi per monitorare la conformità generale dei dispositivi, visualizzare i report e visualizzare la conformità dei dispositivi in base ai singoli criteri e alle singole impostazioni.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a2dbd43ff5a8048286693dbfb417d6bb720a877
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353034"
---
# <a name="monitor-intune-device-compliance-policies"></a>Monitorare i criteri di conformità dei dispositivi di Intune

I report sulla conformità consentono di verificare la conformità dei dispositivi e risolvere i problemi correlati alla conformità nell'organizzazione. L'uso di questi report consente di visualizzare informazioni su:

- Stato di conformità generale dei dispositivi
- Stato di conformità per una singola impostazione
- Stato di conformità per un singolo criterio
- Drill-down nei singoli dispositivi per visualizzare impostazioni e i criteri specifici che influiscono sul dispositivo

## <a name="open-the-compliance-dashboard"></a>Apertura del dashboard della conformità

Aprire il **dashboard della conformità dei dispositivi di Intune**:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Panoramica** >  scheda **Stato conformità**.

> [!IMPORTANT]
> Per ricevere i criteri di conformità, i dispositivi devono essere registrati in Intune.

## <a name="dashboard-overview"></a>Informazioni generali sul dashboard

Quando si apre il dashboard, si ottiene una panoramica con tutti i report di conformità. In questi report è possibile visualizzare e verificare:

- Conformità complessiva del dispositivo
- Conformità dei dispositivi in base ai criteri
- Conformità dei dispositivi in base alle impostazioni
- Stato dell'agente delle minacce
- Stato di protezione del dispositivo

![Immagine del dashboard che illustra il dashboard della conformità del dispositivo e i vari report](./media/compliance-policy-monitor/idc-1.png)

Se si esaminano in dettaglio questi report, si possono vedere anche tutte le impostazioni e i criteri di conformità specifici validi per un dispositivo specifico, incluso lo stato di conformità per ogni impostazione.

### <a name="device-compliance-status"></a>Stato di conformità del dispositivo

Il grafico **Stato conformità dispositivo** illustra gli stati di conformità per tutti i dispositivi registrati in Intune. Gli stati di conformità dei dispositivi vengono mantenuti in due diversi database: Intune e Azure Active Directory.

> [!IMPORTANT]
> Intune segue la pianificazione in base alla quale il dispositivo contatta il servizio per tutte le valutazioni di conformità sul dispositivo. [Altre informazioni su questa pianificazione](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

Descrizioni dei diversi stati dei criteri di conformità dei dispositivi:

- **Conforme**: il dispositivo rispetta una o più impostazioni dei criteri di conformità dei dispositivi.

- **Periodo di tolleranza**: per il dispositivo sono state definite una o più impostazioni dei criteri di conformità dei dispositivi. Tuttavia, l'utente non ha ancora applicato i criteri. Questo significa che il dispositivo non è conforme, ma si trova nel periodo di tolleranza definito dall'amministratore.

  - Altre informazioni sulle [azioni per i dispositivi non conformi](actions-for-noncompliance.md).

- **Non valutato**: stato iniziale dei dispositivi appena registrati. Di seguito sono elencate altre possibili cause per questo stato:

  - Dispositivi a cui non sono assegnati criteri di conformità e che non hanno un trigger per verificare la conformità
  - Dispositivi che non si sono connessi dall'ultimo aggiornamento dei criteri di conformità
  - Dispositivi non associati a un utente specifico, come:
    - Dispositivi iOS/iPadOS acquistati tramite il programma Device Enrollment Program (DEP) di Apple che non hanno affinità utente
    - Dispositivi dedicati Android Enterprise o Android in modalità tutto schermo
  - Dispositivi registrati con un account del manager di registrazione dispositivi

- **Non conforme**: il dispositivo non rispetta una o più impostazioni dei criteri di conformità dei dispositivi. Oppure l'utente non è conforme ai criteri.

- **Dispositivo non sincronizzato**: il dispositivo non è riuscito a segnalare lo stato dei criteri di conformità per uno dei motivi seguenti:

  - **Sconosciuto**: il dispositivo è offline o non è riuscito a comunicare con Intune o Azure AD per altri motivi.

  - **Errore**: il dispositivo non è riuscito a comunicare con Intune e Azure AD e ha ricevuto un messaggio di errore con la spiegazione del motivo.

> [!IMPORTANT]
> I dispositivi che sono registrati in Intune, ma non sono interessati da alcun criterio di conformità, vengono inclusi in questo report all'interno del bucket **Conforme**.

#### <a name="drill-down-for-more-details"></a>Eseguire il drill-down per maggiori dettagli

Selezionare uno stato nel grafico dello **stato di conformità del dispositivo**. Ad esempio, selezionare lo stato **Non conforme**:

![Scegliere lo stato non conforme](./media/compliance-policy-monitor/select-not-compliant-status.png)

Questa azione apre la finestra **Conformità del dispositivo** e visualizza i dispositivi in un grafico **Stato del dispositivo**. Nel grafico vengono visualizzati altri dettagli sui dispositivi con tale stato, tra cui la piattaforma del sistema operativo, la data dell'ultima archiviazione e altro ancora.
![Immagine del dashboard che visualizza altri dettagli sul dispositivo nello stato specifico](./media/compliance-policy-monitor/drill-down-details.png)

Per visualizzare tutti i dispositivi di proprietà di un utente specifico, è anche possibile filtrare il report grafico digitando l'indirizzo di posta elettronica dell'utente.

#### <a name="filter-and-columns"></a>Filtro e colonne

![Selezionare Filtro e Colonne per modificare i risultati nel grafico](./media/compliance-policy-monitor/filter-columns.png)

Quando si seleziona il pulsante **Filtro**, l'area a comparsa del filtro si apre con altre opzioni, tra cui lo stato di **conformità**, i dispositivi **jailbroken** e altro ancora. **Applicare** il filtro per aggiornare i risultati.

Usare la proprietà **Colonne** per aggiungere o rimuovere colonne dall'output grafico. Ad esempio, **Nome entità utente** può indicare l'indirizzo di posta elettronica registrato nel dispositivo. **Applicare** le colonne per aggiornare i risultati.

#### <a name="device-details"></a>Dettagli dispositivo

Nel grafico **Dettagli dispositivi** selezionare un dispositivo specifico, quindi selezionare **Conformità del dispositivo**:

![Scegliere un dispositivo specifico, quindi Conformità del dispositivo per vedere i criteri di conformità applicati](./media/compliance-policy-monitor/see-policies-applied-specific-device.png)

Intune visualizza altri dettagli sulle impostazioni dei criteri di conformità applicati al dispositivo. Quando si seleziona il criterio specifico, vengono visualizzate tutte le impostazioni del criterio.

### <a name="devices-without-compliance"></a>Dispositivi senza conformità

Nella pagina *Stato di conformità* accanto al grafico *Conformità dei criteri* è possibile selezionare il riquadro **Dispositivi senza criteri di conformità** per visualizzare le informazioni sui dispositivi a cui non sono assegnati criteri di conformità:

![Vedere i dispositivi senza criteri di conformità](./media/compliance-policy-monitor/devices-without-policies.png)

Quando si seleziona il riquadro vengono visualizzati tutti i dispositivi senza criteri di conformità. Vengono visualizzati anche l'utente del dispositivo, lo stato della distribuzione dei criteri e il modello del dispositivo.

#### <a name="what-you-need-to-know"></a>Informazioni importanti

- Con l'impostazione di sicurezza **Contrassegna i dispositivi senza criteri di conformità assegnati come** è importante identificare i dispositivi senza criteri di conformità. Sarà quindi possibile assegnare loro almeno un criterio di conformità.

  L'impostazione di sicurezza è configurabile nel portale di Intune. Passare a **Dispositivi** > **Criteri di conformità**  > **Impostazioni dei criteri di conformità**. Quindi impostare **Contrassegna i dispositivi senza criteri di conformità assegnati come** su **Conforme** o **Non conforme**.

  Leggere altre informazioni su questo [miglioramento alla sicurezza nel servizio Intune](https://blogs.technet.microsoft.com/intunesupport/2018/02/09/updated-upcoming-security-enhancements-in-the-intune-service/).

- Gli utenti a cui è stato assegnato un criterio di conformità di qualsiasi tipo non vengono visualizzati nel report, indipendentemente dalla piattaforma del dispositivo. Ad esempio, se è stato assegnato un criterio di conformità di Windows a un utente con un dispositivo Android, il dispositivo non appare nel report. Tuttavia, Intune considera tale dispositivo Android come non conforme. Per evitare problemi, è consigliabile creare criteri per ogni piattaforma del dispositivo e distribuirli a tutti gli utenti.

### <a name="per-policy-device-compliance"></a>Conformità dei dispositivi in base ai criteri

Il grafico **Conformità dei criteri** illustra i criteri e il numero di dispositivi conformi e non conformi.

![Visualizzare un elenco di criteri e il numero di dispositivi conformi e non conformi per tale criterio](./media/compliance-policy-monitor/idc-8.png)

### <a name="setting-compliance"></a>Conformità delle impostazioni

Il grafico **Conformità dell'impostazione** visualizza tutte le impostazioni dei criteri di conformità dei dispositivi, le piattaforme a cui vengono applicate le impostazioni dei criteri e il numero di dispositivi non conformi.

![Visualizzare un elenco di tutte le impostazioni nei vari criteri](./media/compliance-policy-monitor/idc-10.png)

## <a name="view-compliance-reports"></a>Visualizzare i report di conformità

Oltre a usare i grafici in *Stato conformità* è possibile accedere a **Report** > **Conformità del dispositivo**.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Monitoraggio**, quindi da **Conformità** selezionare il report che si vuole visualizzare. Alcuni dei report di conformità disponibili includono:

   - Conformità del dispositivo
   - Dispositivi non conformi
   - Dispositivi senza criteri di conformità
   - Conformità delle impostazioni
   - Conformità ai criteri
   - Report di attestazione dell'integrità di Windows
   - Stato dell'agente delle minacce

Per altre informazioni sui report, vedere [Report di Intune](../fundamentals/reports.md)

## <a name="view-status-of-device-policies"></a>Visualizzare lo stato dei criteri dei dispositivi

È possibile controllare i diversi stati dei criteri in base alla piattaforma. Si supponga, ad esempio, di avere un criterio di conformità macOS e di voler visualizzare i dispositivi interessati da questo criterio e verificare la presenza di eventuali conflitti o errori.

Questa funzionalità è inclusa nei report di stato del dispositivo:

1. Selezionare **Dispositivi** > **Criteri di conformità** > **Criteri**. Viene visualizzato un elenco di criteri con informazioni sulla piattaforma, sull'assegnazione o meno del criterio e altri dettagli.
2. Selezionare un criterio > **Panoramica**. In questa visualizzazione l'assegnazione del criterio include gli stati seguenti:

    - **Operazione completata**: i criteri sono stati applicati.
    - **Errore**: non è stato possibile applicare i criteri. Il messaggio in genere viene visualizzato con un codice di errore collegato a una spiegazione.
    - **Conflitto**: due impostazioni sono applicate allo stesso dispositivo e Intune non è in grado di risolvere il conflitto. Un amministratore deve esaminare la situazione.
    - **Pending**: il dispositivo non ha ancora contattato Intune per ricevere i criteri.
    - **Non applicabile**: il dispositivo non può ricevere i criteri. Ad esempio, i criteri aggiornano un'impostazione specifica di iOS 11.1, ma il dispositivo usa iOS 10.

3. Per visualizzare i dettagli sui dispositivi usando questo criterio, selezionare uno stato. Selezionare, ad esempio, **Operazione completata**. La finestra successiva conterrà i dettagli di un dispositivo specifico, tra cui il nome e lo stato di distribuzione.

## <a name="how-intune-resolves-policy-conflicts"></a>Come vengono risolti i conflitti di criteri in Intune

Possono verificarsi conflitti se vengono applicati più criteri di Intune a un dispositivo. Se le impostazioni dei criteri si sovrappongono, Intune risolve eventuali conflitti in base alle regole seguenti:

- Se le impostazioni in conflitto hanno origine da criteri di configurazione di Intune e da criteri di conformità, le impostazioni nei criteri di conformità hanno la precedenza rispetto a quelle dei criteri di configurazione, anche se queste ultime sono più sicure.

- Se sono stati distribuiti più criteri di conformità, Intune usa quelli più sicuri.

## <a name="next-steps"></a>Passaggi successivi

[Panoramica dei criteri di conformità](device-compliance-get-started.md)
