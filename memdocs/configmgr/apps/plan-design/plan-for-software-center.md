---
title: Pianificare Software Center
titleSuffix: Configuration Manager
description: Decidere come configurare e personalizzare Software Center per consentire agli utenti di interagire con Configuration Manager.
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 802dbaa4188199e555a5cc0143ed599ad454e27e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695172"
---
# <a name="plan-for-software-center"></a>Pianificare Software Center

*Si applica a: Configuration Manager (Current Branch)*

Gli utenti modificano le impostazioni e cercano e installano applicazioni in Software Center. Quando si installa il client di Configuration Manager in un dispositivo Windows, viene automaticamente installato Software Center.

Per informazioni sulle altre funzionalità di Software Center, vedere il [Manuale dell'utente di Software Center](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Configurare Software Center  

Aggiornare i siti e i client di Configuration Manager alla versione 1906 o successiva per sfruttare i vantaggi offerti dalle funzionalità più recenti di Software Center.

> [!IMPORTANT]
> Questi miglioramenti iterativi di Software Center e il punto di gestione sono concepiti per il ritiro dei ruoli del catalogo applicazioni.
>
> - L'esperienza utente di Silverlight non è supportata a partire dalla versione Current Branch 1806.
> - A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni.
> - Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.

- L'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer** è abilitata per impostazione predefinita. La versione precedente di Software Center non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

- Specificare la visibilità del collegamento al sito Web del Catalogo applicazioni nella scheda **Stato dell'installazione** di Software Center. Per altre informazioni, vedere Impostazioni client di [Software Center](../../core/clients/deploy/about-client-settings.md#software-center).

- A partire dalla versione 1906, è possibile aggiungere a Software Center fino a cinque schede personalizzate. Per altre informazioni, vedere [Impostazioni client di Software Center](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

- In Software Center gli utenti possono configurare l'affinità utente-dispositivo. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

- A partire dalla versione 2006, è possibile configurare i dispositivi co-gestiti per l'uso del Portale aziendale per le app di Intune e di Configuration Manager. Per altre informazioni, vedere [Usare l'app Portale aziendale in dispositivi con co-gestione](../../comanage/company-portal.md).<!--CMADO-3601237,INADO-4297660-->

> [!IMPORTANT]
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

### <a name="software-center-and-user-available-applications"></a>Software Center e applicazioni disponibili per gli utenti

- I ruoli del Catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Questo comportamento consente di ridurre l'infrastruttura server necessaria per distribuire le applicazioni agli utenti. Per ottenere queste informazioni, Software Center si basa sul punto di gestione, che consente una maggiore scalabilità degli ambienti di grandi dimensioni tramite l'assegnazione di questi ultimi a [gruppi di limiti](../../core/servers/deploy/configure/boundary-groups.md#management-points).<!--1358309-->

- Gli utenti possono cercare e installare le applicazioni disponibili per gli utenti nei dispositivi aggiunti ad Azure Active Directory (Azure AD). A partire dalla versione 2006, è possibile ottenere le app disponibili per gli utenti in dispositivi basati su Internet e aggiunti a un dominio. Per altre informazioni, vedere [Distribuire applicazioni disponibili per l'utente](../deploy-use/deploy-applications.md#deploy-user-available-applications).

- A partire dalla versione 1906, Software Center comunica con un punto di gestione per le app destinate agli utenti disponibili. Non usa più il catalogo applicazioni. Grazie a questa modifica, è più facile rimuovere il catalogo applicazioni dal sito.

- In precedenza, Software Center selezionava il primo punto di gestione nell'elenco di server disponibili. A partire dalla versione 1906, usa lo stesso punto di gestione del client. Questa modifica consente a Software Center di usare lo stesso punto di gestione del client dal sito primario assegnato.

## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a> Sostituzione delle notifiche di tipo avviso popup con una finestra di dialogo

<!--3555947-->
In alcuni casi gli utenti non vedono la notifica di tipo avviso popup di Windows per un riavvio o una distribuzione necessaria, quindi non vedono l'esperienza per posporre il promemoria. Questo comportamento può causare un'esperienza utente insoddisfacente quando il client raggiunge una scadenza.

A partire dalla versione 1902, quando [sono richieste modifiche software](#software-changes-are-required) o le distribuzioni [richiedono un riavvio](#restart-required), si ha la possibilità di usare una finestra di dialogo più invasiva.

### <a name="software-changes-are-required"></a>Sono richieste modifiche software

Quando si [distribuisce un'applicazione](../deploy-use/deploy-applications.md) come richiesta con scadenza nel futuro, nella pagina **Esperienza utente** della Distribuzione guidata del software selezionare le opzioni di notifica utente seguenti:

- **Visualizza in Software Center e mostra tutte le notifiche**
- **Quando sono necessarie modifiche al software, mostra una finestra di dialogo all'utente invece di un avviso popup**

La configurazione di questa impostazione di distribuzione modifica l'esperienza utente per questo scenario.

Dalla notifica di tipo avviso popup seguente:

![Notifica popup che segnala che sono richieste modifiche software](media/3555947-required-toast.png)  

Alla finestra di dialogo seguente:

![Finestra di dialogo per modifiche software necessarie](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Riavvio richiesto

Nel gruppo [Riavvio del computer](../../core/clients/deploy/about-client-settings.md#computer-restart) abilitare l'opzione seguente: **Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup**.  

La configurazione di questa impostazione client modifica l'esperienza utente per tutte le distribuzioni richieste che necessitano di un riavvio dei tipi seguenti:

- [Applicazione](../deploy-use/deploy-applications.md)
- [Sequenza di attività](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Aggiornamento software](../../sum/deploy-use/deploy-software-updates.md)

Dalla notifica di tipo avviso popup seguente:

![Notifica di tipo avviso popup per riavvio richiesto](media/3555947-restart-toast.png)  

Alla finestra di dialogo seguente:

![Finestra di dialogo per riavviare il computer](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> In Configuration Manager 1902, in determinate circostanze, la finestra di dialogo non sostituisce le notifiche di tipo avviso popup. Per risolvere questo problema, installare l'[aggiornamento cumulativo per Configuration Manager versione 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="brand-software-center"></a>Personalizzare Software Center

Modificare l'aspetto di Software Center in modo che risponda ai requisiti di personalizzazione dell'organizzazione. Questa configurazione consente agli utenti di considerare attendibile Software Center.

### <a name="configure-software-center-branding"></a>Configurare la personalizzazione di Software Center

<!-- 1351224 -->
Personalizzare l'aspetto di Software Center aggiungendo gli elementi di personalizzazione dell'organizzazione e specificando la visibilità delle schede.

Per altre informazioni, vedere gli articoli seguenti:

- Gruppo di impostazioni client di [Software Center](../../core/clients/deploy/about-client-settings.md#software-center)  
- [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Priorità di personalizzazione

Configuration Manager applica la personalizzazione per Software Center in base alle priorità seguenti:  

1. Impostazioni client di **Software Center**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#software-center) (Informazioni sulle impostazioni client).  

2. Impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#computer-agent) (Informazioni sulle impostazioni client).  

#### <a name="application-catalog-branding-priorities"></a>Priorità di personalizzazione del Catalogo applicazioni

> [!IMPORTANT]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  

Se si usa il Catalogo applicazioni, la personalizzazione segue queste priorità:  

1. Impostazioni client di **Software Center**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#software-center) (Informazioni sulle impostazioni client).  

2. *Nome dell'organizzazione* e *colore* specificati nelle proprietà del punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Opzioni di configurazione per il punto per siti Web del Catalogo applicazioni](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).  

3. Impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#computer-agent) (Informazioni sulle impostazioni client).  

## <a name="see-also"></a>Vedere anche

- [Manuale dell'utente di Software Center](../../core/understand/software-center.md)

- [Pianificare e configurare la gestione delle applicazioni](plan-for-and-configure-application-management.md)

- [Usare l'app Portale aziendale in dispositivi con co-gestione](../../comanage/company-portal.md)
