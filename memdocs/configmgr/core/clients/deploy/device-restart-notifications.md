---
title: Notifiche di riavvio del dispositivo
titleSuffix: Configuration Manager
description: Riavviare il comportamento delle notifiche per diverse impostazioni client in Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693959"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Notifiche di riavvio del dispositivo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le notifiche ricevute da un utente per un riavvio del dispositivo in sospeso possono variare in base alle [impostazioni client di riavvio del computer](about-client-settings.md#computer-restart) e alla versione di Configuration Manager in uso. Questo articolo consente agli amministratori di determinare qual è l'esperienza utente riguardo alle notifiche di riavvio del dispositivo in sospeso.

>[!NOTE]
> - Illustra in particolare le impostazioni client disponibili in Configuration Manager versione 1902 e versione 1906.


## <a name="deployment-types-for-restart-notifications"></a>Tipi di distribuzione per le notifiche di riavvio

Le [impostazioni client per il riavvio del computer](about-client-settings.md#computer-restart) modificano l'esperienza utente per tutte le distribuzioni richieste che necessitano dei seguenti tipi di riavvio:

- [Applicazione](../../../apps/deploy-use/deploy-applications.md)
- [Sequenza di attività](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Aggiornamento software](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Tipi di notifica di riavvio

Quando è necessario un riavvio l'utente finale riceve una notifica del riavvio imminente. Gli utenti possono ricevere quattro tipi di notifiche generali:

**Notifica di tipo avviso popup**, che indica che è necessario un riavvio. Le informazioni della notifica di tipo avviso popup possono essere diverse a seconda della versione di Configuration Manager in esecuzione. Questo tipo di notifica è nativo del sistema operativo Windows e può essere usato anche da prodotti software di terze parti.

![Notifica di tipo avviso popup del riavvio in sospeso](media/3555947-restart-toast.png)

Notifica di Software Center con un'opzione che consente di rinviare l'azione e indica il tempo rimanente prima dell'applicazione di un riavvio. Il messaggio può essere diverso a seconda della versione di Configuration Manager.

![Notifica di riavvio in sospeso di Software Center con pulsante di rinvio](media/3976435-snooze-restart-countdown.png)

Notifica finale del conto alla rovescia di Software Center che non può essere chiusa dall'utente. Il pulsante di rinvio è disattivato.

![Notifica finale del conto alla rovescia di Software Center](media/3976435-final-restart-countdown.png)

Se l'utente installa in modo proattivo un software che richiede il riavvio prima della scadenza, viene visualizzata una notifica diversa. La notifica seguente si verifica quando l'impostazione dell'esperienza utente consente le notifiche e non si usano notifiche di tipo avviso popup per la distribuzione. Per altre informazioni sulla configurazione di queste impostazioni, vedere le impostazioni dell'[esperienza utente**di**distribuzione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) e [Notifiche utente per le distribuzioni richieste](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Notifica per il software installato in modo proattivo](media/3976435-proactive-user-restart-notification.png)

- Se non si usano le notifiche di tipo avviso popup, la finestra di dialogo per il software contrassegnato come **disponibile** è simile al software installato in modo proattivo.

  - Per il software **disponibile**, la notifica non ha una scadenza per il riavvio e l'utente può scegliere il proprio intervallo per rinviarlo. Per altre informazioni, vedere [Impostazioni di approvazione](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

    ![Il software contrassegnato come "disponibile" non ha una scadenza per il riavvio nella notifica.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Notifiche di riavvio del dispositivo nella versione 1902

<!--3555947-->
In alcuni casi gli utenti non vedono la notifica di tipo avviso popup di Windows per un riavvio o una distribuzione necessaria, quindi non vedono l'esperienza per posporre il promemoria. Questo comportamento può causare un'esperienza utente insoddisfacente quando il client raggiunge una scadenza.

A partire dalla versione 1902, quando sono richieste modifiche software o le distribuzioni richiedono un riavvio, si ha la possibilità di usare una finestra di dialogo più invasiva.

Nel gruppo [Riavvio del computer](about-client-settings.md#computer-restart) abilitare l'opzione seguente: **Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup**.  

La configurazione di questa impostazione client modifica l'esperienza utente per tutte le distribuzioni richieste che richiedono un riavvio con notifiche di tipo avviso popup:

![Notifica di tipo avviso popup per riavvio richiesto](media/3555947-restart-toast-initial.png)  

Alla finestra di dialogo di Software Center più invasiva:

![Finestra di dialogo per riavviare il computer](media/3976435-proactive-user-restart-notification.png)

Se l'utente non ha riavviato il dispositivo dopo l'installazione, riceverà una notifica come promemoria. Questo promemoria temporaneo verrà visualizzato all'utente in base all'impostazione client: **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)** . Questa impostazione rappresenta il tempo complessivo a disposizione dell'utente per riavviare il computer prima che venga forzato il riavvio.

- Notifica temporanea quando si usano le notifiche di tipo avviso popup:

  ![Notifica di tipo avviso popup del riavvio in sospeso](media/3555947-restart-toast.png)

- Notifica temporanea quando si usa la finestra di dialogo di Software Center, non un avviso popup:

  ![Notifica di riavvio in sospeso di Software Center con pulsante di rinvio](media/3555947-1902-hide-notification.png)

Se l'utente non ha riavviato dopo la notifica temporanea, riceverà la notifica finale del conto alla rovescia e non avrà la possibilità di chiuderla. L'intervallo di tempo in cui viene visualizzata la notifica finale è basato sull'impostazione client: **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)** . Se, ad esempio, l'impostazione è 60, la notifica finale viene visualizzata un'ora prima che venga forzato il riavvio:

![Notifica finale del conto alla rovescia di Software Center](media/3555947-1902-final-countdown.png)

Le impostazioni seguenti devono avere una durata più breve della [finestra di manutenzione](../manage/collections/use-maintenance-windows.md) più breve applicata al computer:

- **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)**
- **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)**

> [!IMPORTANT]
> In Configuration Manager 1902, in determinate circostanze, la finestra di dialogo non sostituisce le notifiche di tipo avviso popup. Per risolvere questo problema, installare l'[aggiornamento cumulativo per Configuration Manager versione 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>Notifiche di riavvio del dispositivo a partire dalla versione 1906
<!--3976435-->
Alcuni amministratori preferiscono notifiche di riavvio frequenti e un breve intervallo di tempo per posporre il riavvio. Altri amministratori consentono agli utenti di posporre il riavvio per periodi di tempo più lunghi e vogliono che gli utenti vengano informati raramente del riavvio in sospeso. La versione 1906 di Configuration Manager offre agli amministratori un controllo aggiuntivo sui tempi e sulla frequenza delle notifiche di riavvio. Gli elementi seguenti sono stati introdotti nella versione 1906 per offrire all'amministratore maggiore controllo:

- L'opzione **Specificare la durata del rinvio per le notifiche con conto alla rovescia per il riavvio del computer (minuti)** è stata aggiunta alle [impostazioni client di riavvio del computer](about-client-settings.md#computer-restart).
- Il valore massimo per **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)** è stato aumentato da 1440 minuti (24 ore) a 20160 minuti (due settimane).
- L'utente non visualizzerà un indicatore di stato nella notifica di riavvio fino a quando non mancheranno meno di 24 ore al riavvio.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Notifiche quando il software richiesto viene installato alla scadenza o successivamente

Quando il software richiesto viene installato alla scadenza o successivamente, gli utenti visualizzano le notifiche a seconda delle impostazioni client selezionate.

Se l'impostazione **Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup** è impostata su:

- **No**: vengono usate notifiche di tipo avviso popup finché non viene raggiunta la notifica finale del conto alla rovescia.
- **Sì**: viene visualizzata una notifica di Software Center.
  - Se mancano più di 24 ore al riavvio, viene visualizzato un orario di riavvio stimato. La tempistica di questa notifica è basata sull'impostazione: **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)** .

     ![Mancano più di 24 ore al riavvio](media/3976435-notification-greater-than-24-hours.png)

  - Se il riavvio è posticipato per più di 24 ore, viene visualizzato un indicatore di stato. La tempistica di questa notifica è basata sull'impostazione: **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)**

     ![Mancano meno di 24 ore al riavvio](media/3976435-notification-less-than-24-hours.png)

Se l'utente seleziona il pulsante di **rinvio**, si riceverà un'altra notifica temporanea al termine del periodo di rinvio, posto che non sia stato ancora raggiunto il conto alla rovescia finale. La tempistica della notifica successiva è basata sull'impostazione: **Specificare la durata del rinvio per le notifiche con conto alla rovescia per il riavvio del computer (ore)** . Se l'utente seleziona **Posponi** e l'intervallo di rinvio è un'ora, l'utente riceverà nuovamente una notifica entro 60 minuti, posto che non abbia ancora raggiunto il conto alla rovescia finale.

Quando viene raggiunto il conto alla rovescia finale, l'utente riceve una notifica che non può chiudere. L'indicatore di stato è in rosso e l'utente non può premere **Posponi**.

![Notifica finale del conto alla rovescia di Software Center nella versione 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>L'utente esegue l'installazione in modo proattivo prima della scadenza

Se l'utente installa in modo proattivo un software che richiede il riavvio prima della scadenza, viene visualizzata una notifica diversa. Per altre informazioni sulla configurazione di queste impostazioni, vedere le impostazioni dell'[esperienza utente**di**distribuzione](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) e [Notifiche utente per le distribuzioni richieste](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

La notifica seguente si verifica quando l'impostazione dell'esperienza utente consente le notifiche e non si usano notifiche di tipo avviso popup per la distribuzione:

![Notifica per il software installato in modo proattivo](media/3976435-proactive-user-restart-notification.png)

Quando viene raggiunta la scadenza per il software, viene seguito il comportamento [Notifiche quando il software richiesto viene installato alla scadenza o successivamente](#notifications-when-required-software-is-installed-at-or-after-the-deadline).

## <a name="log-files"></a>File di registro

Usare **RebootCoordinator.log** e **SCNotify.log** per la risoluzione dei problemi relativi al riavvio del dispositivo. Può anche essere necessario usare [file di log](../../plan-design/hierarchy/log-files.md) client aggiuntivi in base al tipo di distribuzione usato.

## <a name="next-steps"></a>Passaggi successivi

- [Introduzione alla gestione delle applicazioni](../../../apps/understand/introduction-to-application-management.md)
- [Introduzione alla distribuzione del sistema operativo](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Introduzione alla gestione degli aggiornamenti software](../../../sum/understand/software-updates-introduction.md)
