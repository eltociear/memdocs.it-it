---
title: Notifiche di riavvio del dispositivo
titleSuffix: Configuration Manager
description: Riavviare il comportamento delle notifiche per diverse impostazioni client in Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 11a7330220ed1aa8f4c3f813418ea86e59e0e1fc
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608006"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Notifiche di riavvio del dispositivo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le notifiche ricevute da un utente per un riavvio del dispositivo in sospeso possono variare in base alle [impostazioni client di riavvio del computer](#client-settings) e alla versione di Configuration Manager in uso. Questo articolo consente di configurare l'esperienza utente per le notifiche di riavvio del dispositivo in sospeso.

## <a name="deployment-types-for-restart-notifications"></a>Tipi di distribuzione per le notifiche di riavvio

Le [impostazioni client per il riavvio del computer](#client-settings) modificano l'esperienza utente per tutte le distribuzioni richieste che necessitano dei seguenti tipi di riavvio:

- [Applicazione](../../../apps/deploy-use/deploy-applications.md)
- [Sequenza di attività](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Aggiornamento software](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Tipi di notifica di riavvio

Quando un dispositivo richiede un riavvio, l'utente finale riceve una notifica da parte del client.

### <a name="toast-notification"></a>Avviso popup

Una notifica di tipo avviso popup di Windows informa l'utente che è necessario riavviare il dispositivo. Le informazioni della notifica di tipo avviso popup possono essere diverse a seconda della versione di Configuration Manager in esecuzione. Questo tipo di notifica è nativo per il sistema operativo Windows. È anche possibile notare software di terze parti che usa questo tipo di notifica.

:::image type="content" source="media/3555947-restart-toast.png" alt-text="Notifica di tipo avviso popup del riavvio in sospeso":::

### <a name="software-center-notification-with-snooze"></a>Notifica di Software Center con sospensione

Software Center mostra una notifica con un'opzione di sospensione e il tempo rimanente prima di forzare il riavvio dei dispositivi. Il messaggio può essere diverso a seconda della versione di Configuration Manager.

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="Notifica di riavvio in sospeso di Software Center con pulsante di rinvio":::

### <a name="software-center-final-countdown-notification"></a>Notifica finale del conto alla rovescia di Software Center

Software Center mostra questa notifica finale di conto alla rovescia che l'utente non può chiudere né sospendere.

:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="Conto alla rovescia finale per riavvio di Software Center":::

A partire dalla versione 1906, l'utente non visualizzerà un indicatore di stato nella notifica di riavvio fino a quando non mancheranno meno di 24 ore al riavvio.

### <a name="software-center-notification-before-deadline"></a>Notifica di Software Center prima della scadenza

Se l'utente installa in modo proattivo il software necessario prima della scadenza ed è necessario un riavvio, viene visualizzata una notifica diversa. La notifica seguente si verifica quando l'impostazione dell'esperienza utente consente le notifiche e non si usano notifiche di tipo avviso popup per la distribuzione. Per altre informazioni sulla configurazione di queste impostazioni, vedere le impostazioni dell'[esperienza utente**di**distribuzione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) e [Notifiche utente per le distribuzioni richieste](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Notifica per il software installato in modo proattivo":::

#### <a name="available-apps"></a>App disponibili

Se non si usano le notifiche di tipo avviso popup, la finestra di dialogo per il software contrassegnato come **disponibile** è simile al software installato in modo proattivo. Per il software **disponibile**, la notifica non ha una scadenza per il riavvio e l'utente può scegliere il proprio intervallo per rinviarlo. Per altre informazioni, vedere [Impostazioni di approvazione](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="Il software disponibile non ha una scadenza per il riavvio nella notifica":::

### <a name="software-center-notification-of-required-restart"></a>Notifica di Software Center di richiesta di riavvio

<!--3601213-->

A partire dalla versione 2006 è possibile configurare le impostazioni del client per impedire il riavvio automatico dei dispositivi quando richiesto da una distribuzione. Quando per una distribuzione richiesta è necessario eseguire il riavvio, ma l'impostazione del client **Configuration Manager può forzare il riavvio di un dispositivo** è disabilitata, vedere la notifica seguente:

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="Notifica di Software Center per il riavvio del computer":::

Se si sceglie **Posponi** per questa notifica, la notifica verrà visualizzata nuovamente in base alla frequenza delle notifiche di promemoria di riavvio specificata. Il dispositivo non verrà riavviato fino a quando non si seleziona **Riavvia** o non si riavvia Windows manualmente.

> [!NOTE]
> Per impostazione predefinita, Configuration Manager può comunque forzare il riavvio dei dispositivi.

## <a name="client-settings"></a>Impostazioni client

Per controllare i comportamenti di riavvio del client, configurare le impostazioni client del dispositivo seguenti nel gruppo **Riavvio del computer**. Per altre informazioni, vedere [Come configurare le impostazioni client](configure-client-settings.md).

### <a name="configuration-manager-can-force-a-device-to-restart"></a>Configuration Manager può forzare il riavvio di un dispositivo

<!--3601213-->

A partire dalla versione 2006 è possibile configurare le impostazioni del client per impedire il riavvio automatico dei dispositivi quando richiesto da una distribuzione. Configuration Manager abilita questa impostazione per impostazione predefinita

> [!IMPORTANT]
> Questa impostazione client si applica a tutte le distribuzioni di applicazioni, aggiornamenti software e pacchetti nel dispositivo. Fino a quando un utente non riavvia manualmente il dispositivo:
>
> - Gli aggiornamenti software e le revisioni dell'app potrebbero non essere installate completamente
> - È possibile che non vengano eseguite le installazioni di software aggiuntivo

Quando si disabilita questa impostazione, non è possibile specificare la quantità di tempo dopo la scadenza per il riavvio del dispositivo o la visualizzazione della notifica con il conto alla rovescia visualizzata all'utente.

> [!NOTE]
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Specificare la durata dell'attesa dopo la scadenza prima del riavvio di un dispositivo (minuti)

Queste impostazioni devono avere una durata minore della finestra di manutenzione più breve applicata al computer. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../manage/collections/use-maintenance-windows.md).

Il valore predefinito è 90 minuti. A partire dalla versione 1906, il valore massimo è aumentato da 1440 minuti (24 ore) a 20160 minuti (due settimane).

> [!NOTE]
> In precedenza, questa impostazione era denominata **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)** .

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Specificare la quantità di tempo per cui a un utente viene visualizzato una notifica di conto alla rovescia finale prima del riavvio di un dispositivo (minuti)

Queste impostazioni devono avere una durata minore della finestra di manutenzione più breve applicata al computer. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../manage/collections/use-maintenance-windows.md).

Il valore predefinito è 15 minuti.

> [!NOTE]
> In precedenza, questa impostazione era denominata **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)** .

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Specificare la frequenza delle notifiche del promemoria presentate all'utente dopo la scadenza prima che un dispositivo venga riavviato (minuti)
<!--3976435-->
_A partire dalla versione 1906_

Il valore di durata della frequenza deve essere minore del valore di **Specificare la durata dell'attesa dopo la scadenza prima del riavvio del dispositivo (minuti)** meno il valore di **Specificare la quantità di tempo per cui a un utente viene visualizzato una notifica di conto alla rovescia finale prima del riavvio di un dispositivo (minuti)** . In caso contrario, le notifiche di promemoria non funzionano.

Il valore predefinito è 240 minuti.

> [!NOTE]
> In precedenza, questa impostazione era denominata **Specificare la durata di sospensione per le notifiche di conto alla rovescia per il riavvio del computer (minuti)** .

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>Quando una distribuzione richiede un riavvio, viene visualizzata una finestra di dialogo anziché un avviso popup
<!--3555947-->
A partire dalla versione 1902, la configurazione di questa impostazione su **Sì** rede più invasiva l'esperienza utente. Questa impostazione si applica a tutte le distribuzioni di applicazioni, sequenze di attività e aggiornamenti software. Per altre informazioni, vedere [Pianificare Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> In Configuration Manager 1902, in determinate circostanze, la finestra di dialogo non sostituisce le notifiche di tipo avviso popup. Per risolvere questo problema, installare l'[aggiornamento cumulativo per Configuration Manager versione 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Notifiche di riavvio del dispositivo (versione 1906)
<!--3976435-->
Alcuni clienti preferiscono notifiche di riavvio frequenti e consentono agli utenti di posticipare un breve intervallo di tempo. Altri consentono agli utenti di posticipare il riavvio per periodi di tempo più lunghi e raramente notificano agli utenti il riavvio in sospeso. A partire da Configuration Manager versione 1906, si ha un controllo aggiuntivo sulla tempistica e sulla frequenza delle notifiche di riavvio.

### <a name="install-required-software-at-or-after-the-deadline"></a>Installare il software necessario entro o dopo la scadenza

Quando il software richiesto viene installato alla scadenza o successivamente, gli utenti visualizzano le notifiche a seconda delle impostazioni client selezionate.

Se l'impostazione **Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup** è impostata su:

- **No**: Windows visualizza le notifiche di tipo avviso popup finché la distribuzione non raggiunge la notifica di conto alla rovescia finale.

- **Sì**: Software Center visualizza una notifica nelle modalità seguenti.

  - Se mancano più di 24 ore al riavvio, viene visualizzato un orario di riavvio stimato. La tempistica di questa notifica è basata sull'impostazione: **Specificare la durata dell'attesa dopo la scadenza prima del riavvio di un dispositivo (minuti)** .

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="Mancano più di 24 ore al riavvio":::

  - Se mancano meno di 24 ore al riavvio, viene visualizzato un indicatore di stato. La tempistica di questa notifica è basata sull'impostazione: **Specificare la durata dell'attesa dopo la scadenza prima del riavvio di un dispositivo (minuti)** .

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="Mancano meno di 24 ore al riavvio":::

Se l'utente seleziona **Posponi**, viene visualizzata un'altra notifica temporanea alla scadenza del periodo di sospensione. Questo comportamento presuppone che non sia ancora stato raggiunto il conto alla rovescia finale. La tempistica della notifica successiva è basata sull'impostazione: **Specificare la frequenza delle notifiche del promemoria presentate all'utente dopo la scadenza prima che un dispositivo venga riavviato (minuti)** . Se l'utente seleziona **Posponi** e l'intervallo di sospensione è pari a un'ora, Software Center invia una nuova notifica all'utente entro 60 minuti. Questo comportamento presuppone che non sia ancora stato raggiunto il conto alla rovescia finale.

Quando viene raggiunto il conto alla rovescia finale, Software Center mostra all'utente una notifica che non può chiudere. L'indicatore di stato è rosso e l'utente non può usare l'opzione **Posponi**.

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="Notifica finale del conto alla rovescia di Software Center nella versione 1906":::

### <a name="proactively-install-required-software-before-the-deadline"></a>Installare in modo proattivo il software richiesto prima della scadenza

Se l'utente installa in modo proattivo un software che richiede il riavvio prima della scadenza, viene visualizzata una notifica diversa. Per altre informazioni sulla configurazione di queste impostazioni, vedere le impostazioni dell'[esperienza utente**di**distribuzione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) e [Notifiche utente per le distribuzioni richieste](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

La notifica seguente si verifica quando l'impostazione dell'esperienza utente consente le notifiche e non si usano notifiche di tipo avviso popup per la distribuzione:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Notifica per il software installato in modo proattivo":::

Quando la distribuzione raggiunge la scadenza, Software Center si comporta come per [installare il software necessario entro o dopo la scadenza](#install-required-software-at-or-after-the-deadline).

## <a name="example-configurations"></a>Configurazioni di esempio

Gli esempi seguenti descrivono come configurare le impostazioni client per ottenere comportamenti specifici.

### <a name="reminders-are-off"></a>I promemoria sono disattivati

| Impostazione | Valore |
|---------|---------|
|Specificare la durata dell'attesa dopo la scadenza prima del riavvio di un dispositivo (minuti)|180|
|Specificare la quantità di tempo per cui a un utente viene visualizzato una notifica di conto alla rovescia finale prima del riavvio di un dispositivo (minuti)|60|
|Specificare la frequenza delle notifiche del promemoria presentate all'utente dopo la scadenza prima che un dispositivo venga riavviato (minuti)|240|
|Quando una distribuzione richiede un riavvio, viene visualizzata una finestra di dialogo anziché un avviso popup|No|

Il dispositivo verrà riavviato tre ore (**180** minuti) dopo la scadenza della distribuzione. Un'ora (**60** minuti) prima del riavvio, viene visualizzato un conto alla rovescia che non è possibile chiudere né posporre. La prima notifica di promemoria viene impostata per iniziare quattro ore (**240** minuti) dopo la scadenza, successivamente al riavvio. In tal modo l'utente non visualizza alcun promemoria.

### <a name="low-reminder-frequency"></a>Frequenza di promemoria bassa

| Impostazione | Valore |
|---------|---------|
|Specificare la durata dell'attesa dopo la scadenza prima del riavvio di un dispositivo (minuti)|7200|
|Specificare la quantità di tempo per cui a un utente viene visualizzato una notifica di conto alla rovescia finale prima del riavvio di un dispositivo (minuti)|120|
|Specificare la frequenza delle notifiche del promemoria presentate all'utente dopo la scadenza prima che un dispositivo venga riavviato (minuti)|900|
|Quando una distribuzione richiede un riavvio, viene visualizzata una finestra di dialogo anziché un avviso popup|Sì|

Il dispositivo si riavvia cinque giorni (**7200** minuti) dopo la scadenza della distribuzione. Due ore (**120** minuti) prima del riavvio, viene visualizzato un conto alla rovescia che non è possibile chiudere né posporre. Questa configurazione rende disponibili 118 ore per visualizzare i promemoria (`(7200 - 120) / 60`). 15 ore (**900** minuti) dopo la scadenza, Software Center visualizza il primo promemoria. Viene visualizzato un massimo di sei promemoria aggiuntivi ogni 15 ore (**900 minuti**). L'utente visualizza il promemoria come una finestra sullo schermo e non come una notifica che scompare in pochi secondi.

### <a name="high-reminder-frequency"></a>Frequenza promemoria elevata

| Impostazione | Valore |
|---------|---------|
|Specificare la durata dell'attesa dopo la scadenza prima del riavvio di un dispositivo (minuti)|2880|
|Specificare la quantità di tempo per cui a un utente viene visualizzato una notifica di conto alla rovescia finale prima del riavvio di un dispositivo (minuti)|60|
|Specificare la frequenza delle notifiche del promemoria presentate all'utente dopo la scadenza prima che un dispositivo venga riavviato (minuti)|30|
|Quando una distribuzione richiede un riavvio, viene visualizzata una finestra di dialogo anziché un avviso popup|Sì|

Il dispositivo si riavvia due giorni (**2880** minuti) dopo la scadenza della distribuzione. Un'ora (**60** minuti) prima del riavvio, viene visualizzato un conto alla rovescia che non è possibile chiudere né posporre. Questa configurazione rende disponibili 47 ore per visualizzare i promemoria (`(2880 - 60) / 60`). **30** minuti dopo la scadenza, Software Center visualizza il primo promemoria. Viene visualizzato un massimo di 92 promemoria aggiuntivi ogni **30 minuti**. L'utente visualizza il promemoria come una finestra sullo schermo e non come una notifica che scompare in pochi secondi.

## <a name="device-restart-notifications-version-1902"></a>Notifiche di riavvio del dispositivo (versione 1902)

<!--3555947-->
In alcuni casi gli utenti non vedono la notifica di tipo avviso popup di Windows per un riavvio o una distribuzione necessaria, quindi non vedono l'esperienza per posporre il promemoria. Questo comportamento può causare un'esperienza utente insoddisfacente quando il client raggiunge una scadenza.

A partire dalla versione 1902, quando sono richieste modifiche software o le distribuzioni richiedono un riavvio, si ha la possibilità di usare una finestra di dialogo più invasiva.

Nel gruppo [Riavvio del computer](#client-settings) abilitare l'opzione seguente: **Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup**.  

La configurazione di questa impostazione client modifica l'esperienza utente per tutte le distribuzioni richieste che richiedono un riavvio con notifiche di tipo avviso popup:

:::image type="content" source="media/3555947-restart-toast-initial.png" alt-text="Notifica di tipo avviso popup per riavvio richiesto":::

Alla finestra di dialogo di Software Center più invasiva:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Finestra di dialogo per riavviare il computer":::

Se l'utente non ha riavviato il dispositivo dopo l'installazione, riceverà una notifica come promemoria. Questo promemoria temporaneo verrà visualizzato all'utente in base all'impostazione client: **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)** . Questa impostazione rappresenta il tempo complessivo a disposizione dell'utente per riavviare il computer prima che venga forzato il riavvio.

- Notifica temporanea quando si usano le notifiche di tipo avviso popup:

    :::image type="content" source="media/3555947-restart-toast.png" alt-text="Notifica di tipo avviso popup del riavvio in sospeso":::

- Notifica temporanea quando si usa la finestra di dialogo di Software Center, non un avviso popup:

    :::image type="content" source="media/3555947-1902-hide-notification.png" alt-text="Notifica di riavvio in sospeso di Software Center con pulsante di rinvio nella versione 1902":::

Se l'utente non ha riavviato dopo la notifica temporanea, riceverà la notifica finale del conto alla rovescia e non avrà la possibilità di chiuderla. L'intervallo di tempo in cui viene visualizzata la notifica finale è basato sull'impostazione client: **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)** . Se, ad esempio, l'impostazione è 60, la notifica finale viene visualizzata un'ora prima che venga forzato il riavvio:

:::image type="content" source="media/3555947-1902-final-countdown.png" alt-text="Notifica finale del conto alla rovescia di Software Center nella versione 1902":::

Le impostazioni seguenti devono avere una durata più breve della [finestra di manutenzione](../manage/collections/use-maintenance-windows.md) più breve applicata al computer:

- **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)**
- **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)**

> [!IMPORTANT]
> In Configuration Manager 1902, in determinate circostanze, la finestra di dialogo non sostituisce le notifiche di tipo avviso popup. Per risolvere questo problema, installare l'[aggiornamento cumulativo per Configuration Manager versione 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="log-files"></a>File di registro

Per risolvere i problemi relativi ai riavvii dei dispositivi, usare i file **RebootCoordinator.log** e **SCNotify.log** nel client. In base al tipo specifico di distribuzione, può anche essere necessario [file di log](../../plan-design/hierarchy/log-files.md) del client aggiuntivi.

## <a name="next-steps"></a>Passaggi successivi

- [Come configurare le impostazioni client](configure-client-settings.md)
- [Impostazioni dell'**esperienza utente** della distribuzione dell'applicazione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Notifiche utente per distribuzioni richieste](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
