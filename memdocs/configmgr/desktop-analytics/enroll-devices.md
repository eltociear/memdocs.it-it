---
title: Registrare i dispositivi in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su come registrare i dispositivi in Desktop Analytics.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c10e3c1cb2a0044003415d8f55a0a4ac85058656
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633314"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Come registrare i dispositivi in Desktop Analytics

Quando si connette [Configuration Manager](connect-configmgr.md) a Desktop Analytics, si configurano le impostazioni per registrare i dispositivi in Desktop Analytics. È possibile modificare queste impostazioni in qualsiasi momento. Assicurarsi anche che i dispositivi siano aggiornati.

## <a name="update-devices"></a>Aggiornare i dispositivi

Desktop Analytics usa due componenti principali di Windows:

- **Componente per la compatibilità**: Il componente per la compatibilità (**strumento di valutazione**) esegue la diagnostica sul dispositivo Windows per valutarne lo stato di compatibilità con le versioni più recenti di Windows 10.

- **Esperienze utente connesse e telemetria**: Con i dati di diagnostica di Windows abilitati, Esperienze utente connesse e telemetria (**DiagTrack**) raccoglie i dati del sistema, dell'applicazione e del driver. Microsoft analizza i dati e li condivide nuovamente con l'utente tramite Desktop Analytics.

Installare la versione più recente di questi componenti per ottimizzare l'esperienza con Desktop Analytics.

La tabella seguente elenca gli aggiornamenti per ogni componente nelle versioni del sistema operativo supportate:

| Versione sistema operativo | Strumento di valutazione | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | Incluso <sup>[Nota 1](#bkmk_note1)</sup> | [Aggiornamento cumulativo più recente](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | Incluso | [Aggiornamento cumulativo più recente](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | Incluso | [Aggiornamento cumulativo più recente](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | Incluso | [Aggiornamento cumulativo più recente](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | Incluso | [Aggiornamento cumulativo più recente](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup>[Nota 2](#bkmk_note2)</sup> | [Rollup mensile più recente](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup>[Nota 3](#bkmk_note3)</sup> | [Rollup mensile più recente](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Usare Configuration Manager per installare automaticamente gli aggiornamenti. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](../sum/deploy-use/deploy-software-updates.md).
>
> Riavviare i dispositivi dopo aver installato gli aggiornamenti per la compatibilità per la prima volta.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a> Nota 1: Windows 10

Sebbene Windows 10 includa questi componenti per impostazione predefinita, i dispositivi Windows 10 richiedono l'aggiornamento cumulativo più recente per avere tutte le funzionalità di Desktop Analytics. Ad esempio, per valutare la compatibilità del dispositivo con la versione più recente del sistema operativo e per ottenere informazioni quasi in tempo reale per le distribuzioni e lo stato della registrazione.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a> Nota 2: Windows 8.1

Microsoft incrementa regolarmente gli aggiornamenti per questo componente, ma il numero di KB associato non cambia. Assicurarsi di avere sempre la versione più recente dell'aggiornamento.

Questo componente esegue la diagnostica nei sistemi Windows 8.1 che partecipano al programma Analisi utilizzo software Windows. La diagnostica consente di determinare se è possibile che si verifichino problemi di compatibilità durante l'aggiornamento a Windows 10.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a> Nota 3: Windows 7

Se l'organizzazione non applica aggiornamenti "Rollup di qualità mensile" ai dispositivi Windows 7 e applica solo aggiornamenti "Solo sicurezza", nell'[elenco degli aggiornamenti che sostituiscono KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c) sono disponibili alcuni aggiornamenti "Solo sicurezza". È possibile installare questi aggiornamenti più recenti anziché KB 2952664.

> [!NOTE]
> Per Windows 8.1, Microsoft modifica KB 2976978 solo come parte degli aggiornamenti "Rollup di qualità mensile".

## <a name="device-enrollment"></a>Registrazione del dispositivo

Il servizio Desktop Analytics non ha agenti da installare. Per la registrazione del dispositivo è necessario configurare le impostazioni nei dispositivi che si vuole monitorare. Queste impostazioni controllano l'istanza di Desktop Analytics a cui il dispositivo deve inviare i dati e altre opzioni di configurazione.

> [!Note]  
> Se in precedenza si usava Windows Analytics, usare la stessa area di lavoro per Desktop Analytics. È necessario registrare nuovamente in Desktop Analytics i dispositivi che sono stati precedentemente registrati in Windows Analytics.
>
> È possibile avere solo un'area di lavoro di Desktop Analytics per ogni tenant di Azure AD. I dispositivi possono inviare i dati di diagnostica solo a un'area di lavoro.  

Configuration Manager offre un'esperienza integrata per la gestione e la distribuzione di queste impostazioni ai client. Per un'esperienza ottimale, usare Configuration Manager.

Quando si connette Configuration Manager a Desktop Analytics, si configurano le impostazioni per registrare i dispositivi. Per altre informazioni, vedere [Come connettere Configuration Manager a Desktop Analytics](connect-configmgr.md#bkmk_connect).

Per modificare le impostazioni, seguire questa procedura:

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare la connessione a Desktop Analytics e scegliere **Proprietà** nella barra multifunzione.

2. Nella pagina **Dati di diagnostica** apportare le modifiche necessarie alle impostazioni seguenti:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione. In caso contrario, assicurarsi che il server proxy sia configurato in modo da consentire tutti gli [endpoint](enable-data-sharing.md#endpoints) necessari prima di continuare. L'ID commerciale si può anche recuperare manualmente dal [portale di Desktop Analytics](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Livello dei dati di diagnostica di Windows 10**: Per altre informazioni, vedere [Livelli dei dati di diagnostica](enable-data-sharing.md#diagnostic-data-levels).  

    - **Consenti il nome del dispositivo nei dati di diagnostica**: Per altre informazioni, vedere [Nome del dispositivo](#device-name).  

    Quando si apportano modifiche a questa pagina, la pagina **Funzionalità disponibili** visualizza un'anteprima delle funzionalità di Desktop Analytics con le impostazioni dei dati di diagnostica selezionate.  

3. Nella pagina **Connessione di Desktop Analytics** apportare le modifiche necessarie alle impostazioni seguenti:

    - **Nome visualizzato**: Il portale di Desktop Analytics visualizza questa connessione a Configuration Manager usando questo nome.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager connette al servizio Desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**. Per altre informazioni, vedere [Autenticazione dei server proxy](enable-data-sharing.md#proxy-server-authentication).

    - **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**: Selezionare **Aggiungi** per inserire ulteriori raccolte della gerarchia **Raccolta di destinazione**. Queste raccolte sono disponibili nel portale di Desktop Analytics per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte pilota e di esclusioni pilota.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Queste raccolte continuano a essere sincronizzate quando viene modificata l'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, i dispositivi escono dalla raccolta e dal piano di distribuzione.

### <a name="windows-settings"></a>Impostazioni di Windows

Quando Configuration Manager registra i dispositivi in Desktop Analytics, imposta i criteri di Windows per la configurazione del dispositivo per Desktop Analytics. Nella maggior parte dei casi usare solo Configuration Manager per configurare queste impostazioni. Non applicare anche queste impostazioni negli oggetti criteri di gruppo del dominio.

Per altre informazioni, vedere [Impostazione di criteri di gruppo per Desktop Analytics](group-policy-settings.md).

### <a name="device-name"></a>Nome del dispositivo

A partire da Windows 10, versione 1803, il nome del dispositivo non viene più raccolto per impostazione predefinita. Per raccogliere il nome del dispositivo con i dati di diagnostica, è necessario un consenso esplicito. Senza il nome del dispositivo, è più difficile identificare i dispositivi che richiedono attenzione durante la valutazione di un aggiornamento a una nuova versione di Windows.

Se non si invia il nome del dispositivo, il dispositivo viene visualizzato in Desktop Analytics come "Sconosciuto":

![Elenco dei dispositivi di Desktop Analytics con nomi "Sconosciuto"](media/unknown-device-name.png)

Per configurare questa opzione, è disponibile un'opzione nelle impostazioni di Configuration Manager per Desktop Analytics: **Consenti il nome del dispositivo nei dati di diagnostica**. Questa impostazione di Configuration Manager controlla l'[impostazione dei criteri di Windows](group-policy-settings.md), **AllowDeviceNameInTelemetry**.

### <a name="conflict-resolution"></a>Risoluzione dei conflitti

In generale, usare le raccolte di Configuration Manager per le impostazioni e la registrazione di Desktop Analytics. Usare l'appartenenza diretta o le query per includere o escludere i dispositivi dalla raccolta. Per altre informazioni, vedere [Come creare le raccolte](../core/clients/manage/collections/create-collections.md).

Configuration Manager configura le impostazioni di Windows solo se un valore non esiste già. Se è necessario configurare impostazioni diverse per un unico gruppo di dispositivi, è possibile usare i [criteri di gruppo](group-policy-settings.md). Le impostazioni di destinazione dei criteri di gruppo hanno la precedenza sulle impostazioni di Configuration Manager. I dispositivi interessati da Criteri di gruppo potrebbero non riflettere con precisione lo stato nel dashboard [Integrità connessione](monitor-connection-health.md).

Quando si configura il livello dei dati di diagnostica, è necessario impostare il limite superiore per il dispositivo. Per impostazione predefinita, in Windows 10 versione 1803 e successive gli utenti possono scegliere di impostare un livello inferiore. È possibile controllare questo comportamento usando l'impostazione dei criteri di gruppo, **Configurare l'interfaccia utente dell'impostazione del consenso esplicito per la telemetria**. Per altre informazioni, vedere [Impostazione di criteri di gruppo per Desktop Analytics](group-policy-settings.md).

### <a name="proxy-settings"></a>Impostazioni proxy

Se l'organizzazione usa l'autenticazione del server proxy per l'accesso a Internet, assicurarsi di configurare correttamente il server proxy o i dispositivi. Per altre informazioni, vedere [Autenticazione dei server proxy](enable-data-sharing.md#proxy-server-authentication).

## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per creare piani di distribuzione in Desktop Analytics.
> [!div class="nextstepaction"]
> [Creare piani di distribuzione](create-deployment-plans.md)
