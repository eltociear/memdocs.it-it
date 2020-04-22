---
title: Pianificare Software Center
titleSuffix: Configuration Manager
description: Decidere come configurare e personalizzare Software Center per consentire agli utenti di interagire con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15da90b12504fdaf7a4dd0a36704391eead877cd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689029"
---
# <a name="plan-for-software-center"></a>Pianificare Software Center

*Si applica a: Configuration Manager (Current Branch)*

Gli utenti modificano le impostazioni e cercano e installano applicazioni in Software Center. Quando si installa il client di Configuration Manager in un dispositivo Windows, viene automaticamente installato Software Center.

Per informazioni sulle altre funzionalità di Software Center, vedere il [Manuale dell'utente di Software Center](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Configurare Software Center  

Aggiornare i siti e i client di Configuration Manager alla versione 1906 o successiva per trarre vantaggio dai miglioramenti più recenti.

Di seguito sono elencati i miglioramenti apportati a Software Center:

> [!Important]  
> Questi miglioramenti iterativi di Software Center e il punto di gestione sono concepiti per il ritiro dei ruoli del catalogo applicazioni.
>
> - L'esperienza utente di Silverlight non è supportata a partire dalla versione Current Branch 1806.
> - A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni.
> - Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  

### <a name="starting-in-version-1802"></a>A partire dalla versione 1802

- L'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer** è abilitata per impostazione predefinita. La versione precedente di Software Center non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

- Gli utenti possono cercare e installare le applicazioni disponibili per gli utenti nei dispositivi aggiunti ad Azure Active Directory (Azure AD). Per altre informazioni, vedere [Deploy user-available applications on Azure AD-joined devices](../deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices) (Distribuire applicazioni disponibili per l'utente in dispositivi aggiunti ad Azure AD).  

### <a name="starting-in-version-1806"></a>A partire dalla versione 1806

- Specificare la visibilità del collegamento al sito Web del Catalogo applicazioni nella scheda **Stato dell'installazione** di Software Center. Per altre informazioni, vedere Impostazioni client di [Software Center](../../core/clients/deploy/about-client-settings.md#software-center).  

- I ruoli del catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Questa modifica consente di ridurre l'infrastruttura server necessaria per distribuire le applicazioni agli utenti. Software Center ora si affida al punto di gestione per ottenere queste informazioni e questo consente una migliore scalabilità degli ambienti di grandi dimensioni, che vengono assegnati a [gruppi di limiti](../../core/servers/deploy/configure/boundary-groups.md#management-points).<!--1358309-->  

    > [!Note]  
    > Se il Catalogo applicazioni è attualmente in uso, continua a funzionare anche se si aggiorna Configuration Manager alla versione 1806. I ruoli Punto per siti Web e Punto per servizi Web del Catalogo applicazioni non sono più *necessari*, ma sono ancora *supportati*. L'**esperienza utente di Silverlight** per il *punto per siti Web* del Catalogo applicazioni non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).
    >
    > Iniziare a pianificare la rimozione dei ruoli del Catalogo applicazioni dall'infrastruttura in futuro. Sfruttare i miglioramenti di Software Center per usare il punto di gestione e semplificare l'ambiente di Configuration Manager.  

### <a name="starting-in-version-1902"></a>A partire dalla versione 1902

- Configurare l'affinità utente-dispositivo. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="starting-in-version-1906"></a>A partire dalla versione 1906

- Software Center comunica ora con un punto di gestione per le app destinate agli utenti, se disponibili. Non usa più il catalogo applicazioni. Grazie a questa modifica, è più facile rimuovere il catalogo applicazioni dal sito.

- In precedenza, Software Center selezionava il primo punto di gestione nell'elenco di server disponibili. A partire da questa versione, usa lo stesso punto di gestione del client. Questa modifica consente a Software Center di usare lo stesso punto di gestione del client dal sito primario assegnato.

- Il punto di gestione include endpoint di Software Center per supportare le nuove funzionalità. L'integrità di questi endpoint viene ora controllata ogni cinque minuti. Segnala eventuali problemi usando messaggi di stato per il componente SMS_MP_CONTROL_MANAGER del sito.

- Non è possibile aggiungere nuovi ruoli del Catalogo applicazioni al sito. I ruoli esistenti continuano a funzionare. Solo i client esistenti usano il Catalogo applicazioni per le distribuzioni disponibili per gli utenti. I client aggiornati usano automaticamente il punto di gestione per tutte le distribuzioni.

- È possibile aggiungere fino a 5 schede personalizzate a Software Center. Per altre informazioni, vedere [Impostazioni client di Software Center](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>Riepilogo dei requisiti dell'infrastruttura per ogni versione

Usare la tabella seguente per conoscere i requisiti di Software Center in base alla versione specifica di Configuration Manager:

| Tipo di dispositivo | Versione sito | Infrastruttura |
|-----------------|--------------|----------------|
| Dispositivo aggiunto ad Azure AD<br>(o "aggiunto a un dominio cloud") | 1802 o 1806 | Punto di gestione per tutte le distribuzioni di app |
| Dispositivo [aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) in Internet | 1802 o 1806 | Gateway di gestione cloud e punto di gestione per tutte le distribuzioni di app |
| Dispositivo aggiunto a un dominio di Active Directory locale | 1802 | Catalogo applicazioni necessario per le app disponibili per gli utenti in Software Center |
| Dispositivo aggiunto a un dominio di Active Directory locale | 1806 | Punto di gestione per tutte le distribuzioni di app |

> [!Important]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.


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

## <a name="branding-software-center"></a>Personalizzazione di Software Center

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

> [!Important]
> L'esperienza utente di Silverlight per il catalogo applicazioni non è supportata a partire dalla versione Current Branch 1806. A partire dalla versione 1906, i client aggiornati usano automaticamente il punto di gestione per le distribuzioni di applicazioni disponibili per gli utenti. Non è inoltre possibile installare nuovi ruoli del Catalogo applicazioni. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910.  

Se si usa il Catalogo applicazioni, la personalizzazione segue queste priorità:  

1. Impostazioni client di **Software Center**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#software-center) (Informazioni sulle impostazioni client).  

2. *Nome dell'organizzazione* e *colore* specificati nelle proprietà del punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Opzioni di configurazione per il punto per siti Web del Catalogo applicazioni](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).  

3. Impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#computer-agent) (Informazioni sulle impostazioni client).  


## <a name="see-also"></a>Vedere anche

- [Manuale dell'utente di Software Center](../../core/understand/software-center.md)
- [Pianificare e configurare la gestione delle applicazioni](plan-for-and-configure-application-management.md)
