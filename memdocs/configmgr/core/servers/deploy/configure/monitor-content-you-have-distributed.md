---
title: Monitoraggio del contenuto
titleSuffix: Configuration Manager
description: Informazioni su come monitorare il contenuto distribuito usando la console di Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31edf096c57b726c3723d261db7a3103fcc311f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701129"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Monitorare il contenuto distribuito con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare la console di Configuration Manager per monitorare il contenuto distribuito, ad esempio:  

- Lo stato di tutti i tipi di pacchetto per i punti di distribuzione associati.  
- Lo stato di convalida per il contenuto di un pacchetto.  
- Lo stato del contenuto assegnato a un gruppo specifico di punti di distribuzione.  
- Lo stato del contenuto assegnato a un punto di distribuzione.  
- Lo stato delle funzionalità facoltative per ogni punto di distribuzione (convalida del contenuto, PXE e multicast).  

> [!NOTE]  
> Configuration Manager monitora solo il contenuto in un punto di distribuzione nella raccolta contenuto. Non monitora il contenuto archiviato nel punto di distribuzione in condivisioni pacchetto o personalizzate.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitoraggio dello stato del contenuto

Il nodo **Stato componente** dell'area di lavoro **Monitoraggio** fornisce informazioni sui pacchetti contenuto. Nella console di Configuration Manager esaminare informazioni quali:  

- Nome, tipo e ID del pacchetto
- Numero di punti di distribuzione a cui è stato inviato un pacchetto
- Tasso di conformità
- Data di creazione del pacchetto
- Versione di origine

Sono disponibili anche informazioni dettagliate sullo stato di qualsiasi pacchetto, tra cui:  

- Stato di distribuzione
- Numero di errori
- Distribuzioni in sospeso  
- Numero di installazioni

È anche possibile gestire le distribuzioni di contenuto ancora in corso o non completate correttamente in un punto di distribuzione:  

- L'opzione per annullare o ridistribuire il contenuto è disponibile quando si visualizza il messaggio di stato di un processo di distribuzione a un punto di distribuzione nel riquadro **Dettagli asset**. Questo riquadro è disponibile nella scheda **In corso** o nella scheda **Errore** del nodo **Stato contenuto**.  
- Inoltre, nei dettagli di un processo nella scheda **In corso** viene visualizzata la percentuale di completamento del processo, I dettagli del processo indicano anche il numero di tentativi rimanenti per un processo. Quando si visualizzano i dettagli di un processo nella scheda **Errore**, viene indicato tra quanto tempo verrà eseguito il prossimo tentativo.  

Quando si annulla una distribuzione non ancora completata, il processo di distribuzione per il trasferimento del contenuto viene interrotto:  

- Lo stato della distribuzione viene aggiornato per indicare che la distribuzione non è riuscita ed è stata annullata da un'azione dell'utente.  
- Questo nuovo stato viene visualizzato nella scheda **Errore** .  

> [!NOTE]  
> A distribuzione quasi completata, è possibile che l'annullamento della distribuzione non venga effettuato prima del completamento dell'operazione al punto di distribuzione. In tal caso, l'annullamento della distribuzione viene ignorato e lo stato indica che la distribuzione è stata eseguita correttamente.  
>
> Sebbene si possa selezionare l'opzione per annullare una distribuzione a un punto di distribuzione che si trova su un server del sito, tale operazione non ha alcun effetto. Il motivo di questo comportamento è che il server del sito e il punto di distribuzione in un server del sito condividono lo stesso archivio di contenuti a istanza singola. Non sono presenti processi di distribuzione da annullare.  

Quando si ridistribuisce il contenuto dopo un trasferimento non riuscito in un punto di distribuzione, Configuration Manager inizia subito a ridistribuire il contenuto nel punto di distribuzione, aggiornandone lo stato in base allo stato attuale di tale ridistribuzione.  

### <a name="tasks-to-monitor-content"></a>Attività per monitorare il contenuto

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e quindi selezionare il nodo **Stato contenuto**. Questo nodo visualizza i pacchetti.  

2. Selezionare il pacchetto che si vuole gestire.  

3. Nella scheda **Home** della barra multifunzione selezionare **Visualizza stato** nel gruppo **Contenuto**. La console visualizzerà informazioni dettagliate sullo stato del pacchetto.

Per altre azioni, passare a una delle sezioni seguenti:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Annullare una distribuzione ancora in corso  

1. Passare alla scheda **In corso**.

2. Nel riquadro **Dettagli asset** fare clic con il pulsante destro del mouse sulla voce relativa alla distribuzione da annullare e scegliere **Annulla**.  

3. Scegliere **Sì** per confermare l'azione e annullare il processo di distribuzione al punto di distribuzione.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Ridistribuire il contenuto dopo una distribuzione non riuscita  

1. Passare alla scheda **Errore**.

2. Nel riquadro **Dettagli asset** fare clic con il pulsante destro del mouse sulla voce relativa alla distribuzione da ridistribuire e scegliere **Ridistribuisci**.  

3. Scegliere **Sì** per confermare l'azione e avviare il processo di ridistribuzione al punto di distribuzione.  


## <a name="distribution-point-group-status"></a>Stato del gruppo di punti di distribuzione

Il nodo **Stato gruppo di punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sui gruppi di punti di distribuzione. È possibile esaminare informazioni quali:  

- Nome, descrizione e stato del gruppo di punti di distribuzione
- Numero di punti di distribuzione membri del gruppo di punti di distribuzione
- Numero di pacchetti assegnati al gruppo
- Tasso di conformità

È anche possibile visualizzare le informazioni dettagliate sullo stato seguenti:  

- Errori del gruppo di punti di distribuzione  
- Numero di distribuzioni in corso
- Numero di distribuzioni completate  

### <a name="monitor-distribution-point-group-status"></a>Monitorare lo stato del gruppo di punti di distribuzione  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e quindi selezionare il nodo **Stato gruppo di punti di distribuzione**. Verranno visualizzati i gruppi di punti di distribuzione.  

2. Selezionare il gruppo di punti di distribuzione di cui visualizzare le informazioni dettagliate sullo stato.  

3. Nella scheda **Home** della barra multifunzione selezionare **Visualizza stato**. Vengono visualizzate informazioni dettagliate sullo stato del gruppo di punti di distribuzione.  


## <a name="distribution-point-configuration-status"></a>Stato di configurazione dei punti di distribuzione

Il nodo **Stato di configurazione dei punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sul punto di distribuzione. È possibile esaminare gli attributi abilitati per il punto di distribuzione, ad esempio PXE, multicast, convalida del contenuto. Esaminare anche lo stato di distribuzione per il punto di distribuzione.

> [!WARNING]  
> Lo stato di configurazione del punto di distribuzione è relativo alle ultime 24 ore. Se il punto di distribuzione ha un errore e viene ripristinato, lo stato dell'errore potrebbe essere visualizzato fino a 24 ore dopo il ripristino del punto di distribuzione.  

### <a name="monitor-distribution-point-configuration-status"></a>Monitorare lo stato di configurazione del punto di distribuzione  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e quindi selezionare il nodo **Stato di configurazione dei punti di distribuzione**.  

2. Selezionare un punto di distribuzione.  

3. Nel riquadro dei risultati passare alla scheda **Dettagli**. Verranno visualizzate le informazioni di stato per il punto di distribuzione.  


## <a name="client-data-sources-dashboard"></a>Dashboard origini dati del client

Usare la dashboard **Origini dati del client** per acquisire altre informazioni sulle origini dalle quali i client ottengono il contenuto nell'ambiente. La dashboard inizia a visualizzare i dati dopo che i client avranno scaricato il contenuto e segnalato le informazioni al sito. Questo processo può richiedere fino a 24 ore.

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Prima di usarla è necessario abilitare la funzionalità **Peer cache client**. Per altre informazioni, vedere [Enable optional features from updates](../../manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).  

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato distribuzione** e selezionare il nodo **Origini dati del client**. Selezionare un periodo di tempo da applicare alla dashboard. Quindi selezionare il gruppo di limiti per il quale si vuole visualizzare informazioni. È possibile passare il puntatore del mouse sui riquadri per vedere altri dettagli sulle diverse origini del contenuto o dei criteri.

Usare anche il report **Origini dati del client - Riepilogo del contenuto** per visualizzare un riepilogo delle origini dati del client per ogni gruppo di limiti.

### <a name="dashboard-tiles"></a>Riquadri del dashboard

Il dashboard include i riquadri seguenti:  

#### <a name="client-content-sources"></a>Origini del contenuto client

Visualizza le origini da cui i client hanno ottenuto il contenuto:

- Punto di distribuzione
- [Punto di distribuzione cloud](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Peer cache](../../../plan-design/hierarchy/client-peer-cache.md)
- [Ottimizzazione recapito](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (a partire dalla versione 1906)<sup>[Nota 1](#bkmk_note1)</sup>
- Microsoft Update: I dispositivi segnalano questa origine quando il client di Configuration Manager scarica gli aggiornamenti software dai servizi cloud Microsoft. Questi servizi includono Microsoft Update e Office 365.

![Riquadro Origini del contenuto client nel dashboard](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> A partire dalla versione 1906<!--3555759-->, per includere Ottimizzazione recapito in questa dashboard, seguire questa procedura:
>
> - Configurare l'impostazione del client **Abilita l'installazione di aggiornamenti rapidi nei client** nel gruppo Aggiornamenti software
>
> - Distribuire gli aggiornamenti rapidi di Windows 10
>
> Per altre informazioni, vedere [Gestire i file di installazione rapida per gli aggiornamenti di Windows 10](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Punti di distribuzione

Visualizza il numero di punti di distribuzione che fanno parte del gruppo di limiti selezionato.

#### <a name="clients-that-used-a-distribution-point"></a>Client che hanno usato un punto di distribuzione

Questo riquadro indica quanti client, tra quelli presenti nel gruppo di limiti selezionato, hanno usato un punto di distribuzione per ottenere contenuto.

#### <a name="peer-cache-sources"></a>Origini di peer cache

Per il gruppo di limiti selezionato, questo riquadro indica quante origini di peer cache hanno segnalato la cronologia di download.

#### <a name="clients-that-used-a-peer"></a>Client che hanno usato un peer

Questo riquadro indica quanti client, tra quelli presenti nel gruppo di limiti selezionato, hanno usato un'origine peer cache per ottenere contenuto.

#### <a name="top-distributed-content"></a>Contenuto distribuito principale

I pacchetti più distribuiti per tipo di origine
