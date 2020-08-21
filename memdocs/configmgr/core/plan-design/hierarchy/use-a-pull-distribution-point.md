---
title: Punto di distribuzione pull
titleSuffix: Configuration Manager
description: Informazioni sulle configurazioni e le limitazioni per l'uso di un punto di distribuzione pull con Configuration Manager.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f0993f6120735f8a614801f9ac14c29870ffefe
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692588"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Usare un punto di distribuzione pull con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si distribuisce contenuto in un punto di distribuzione standard nella console di Configuration Manager, il server del sito esegue il push del contenuto al punto di distribuzione. Un punto di distribuzione pull ottiene il contenuto scaricandolo da una posizione di origine, ad esempio un client.  

Quando si distribuisce contenuto in numerosi punti di distribuzione, i punti distribuzione pull consentono di ridurre il carico di elaborazione nel server del sito e possono anche velocizzare il trasferimento del contenuto a ogni server. Normalmente, il componente per la gestione delle distribuzioni nel server del sito invia il contenuto a ogni punto di distribuzione. Il sito esegue invece l'offload del processo di trasferimento del contenuto ai punti di distribuzione pull.  

È possibile configurare singoli punti di distribuzione come punti di distribuzione pull. Per ogni punto di distribuzione pull, specificare uno o più punti di distribuzione di origine da cui può ottenere il contenuto. Un punto di distribuzione pull può scaricare contenuto solo da un punto di distribuzione specificato come punto di distribuzione di origine.

Quando si distribuisce contenuto in un punto di distribuzione pull nella console, il server del sito invia una notifica al punto di distribuzione pull, che scarica quindi il contenuto da un punto di distribuzione di origine. Un punto di distribuzione pull gestisce il trasferimento del contenuto eseguendo il download da un altro punto di distribuzione che contiene già una copia del contenuto.  

I punti di distribuzione pull supportano le stesse configurazioni e funzionalità dei normali punti di distribuzione. Un punto di distribuzione pull supporta ad esempio:

- Configurazioni multicast e PXE
- Convalida contenuto
- Distribuzione di contenuto su richiesta
- Comunicazioni HTTP o HTTPS dai client
- Opzioni per i certificati identiche a quelle degli altri punti di distribuzione
- Gestione individuale o come membro di un gruppo di punti di distribuzione  

Configurare un punto di distribuzione pull quando si installa il punto di distribuzione. Dopo aver creato un punto di distribuzione, configurarlo come punto di distribuzione pull modificando le proprietà del ruolo. Per altre informazioni su come abilitare un punto di distribuzione come punto di distribuzione pull, vedere [Punto di distribuzione pull](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull).  

Rimuovere la configurazione come punto di distribuzione pull modificando le proprietà del punto di distribuzione. Quando si rimuove la configurazione come punto di distribuzione pull, viene ripristinato il normale funzionamento. I futuri trasferimenti di contenuto al punto di distribuzione verranno gestiti dal server del sito.  

## <a name="distribution-process"></a>Processo di distribuzione

Quando si distribuisce contenuto in un punto di distribuzione pull, si verifica la sequenza di eventi seguente:

- Quando si distribuisce contenuto in un punto di distribuzione pull nella console, il componente Package Transfer Manager nel server del sito controlla il database del sito per verificare se il contenuto è disponibile in un punto di distribuzione di origine. Se non può verificare la presenza del contenuto in un punto di distribuzione di origine per il punto di distribuzione pull, ripete il controllo ogni 20 minuti finché il contenuto non risulta disponibile.  

- Quando il Package Transfer Manager conferma la disponibilità del contenuto, viene inviata una notifica al punto di distribuzione pull con la richiesta di scaricare il contenuto. Se la notifica non riesce, riprova in base alle **impostazioni dei tentativi** per i punti di distribuzione pull nel componente Distribuzione software. Quando riceve la notifica, il punto di distribuzione pull prova a scaricare il contenuto dai punti di distribuzione di origine.  

- Mentre il punto di distribuzione pull scarica il contenuto, Package Transfer Manager esegue il polling dello stato in base alle **impostazioni del polling di stato** per i punti di distribuzione pull nel componente Distribuzione software.  Al termine del download del contenuto da parte del punto di distribuzione pull, lo stato viene inviato a un punto di gestione.  

## <a name="configure-site-component-settings"></a>Configurare le impostazioni dei componenti del sito

Quando si usa un punto di distribuzione pull, esaminare e configurare le impostazioni dei componenti del sito seguenti:  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare il sito. Sulla barra multifunzione selezionare **Configura componenti del sito** e selezionare **Distribuzione software**.  

3. Passare alla scheda**Punto di distribuzione pull**.  

4. Nel gruppo **Impostazioni dei tentativi** esaminare i valori seguenti.  

    - **Numero di tentativi**: numero di tentativi effettuati da Package Transfer Manager per notificare al punto di distribuzione pull di scaricare il contenuto. Dopo il numero di tentativi specificato, Package Transfer Manager annulla il trasferimento. Il valore predefinito è 30.  

    - **Ritardo prima di riprovare (minuti)** : numero di minuti di attesa da parte di Package Transfer Manager tra un tentativo e il successivo. Il valore predefinito è 20.  

5. Nel gruppo **Impostazioni del polling di stato** esaminare i valori seguenti.  

    - **Numero di polling**: numero di volte per il quale Package Transfer Manager contatta il punto di distribuzione pull per recuperare lo stato del processo. Se esegue questo numero di tentativi prima che il processo sia completato, Package Transfer Manager annulla il trasferimento. Il valore predefinito è 72.

    - **Ritardo prima di riprovare (minuti)** : numero di minuti di attesa da parte di Package Transfer Manager tra un tentativo e il successivo. Il valore predefinito è 60.

    > [!NOTE]  
    >  Quando Package Transfer Manager annulla un processo perché viene superato il numero di tentativi di polling, il punto di distribuzione pull continua a scaricare il contenuto. Al termine, il punto di distribuzione pull invia il messaggio di stato appropriato e il nuovo stato viene riportato nella console.  

## <a name="limitations"></a>Limitazioni

- Non è possibile configurare un punto di distribuzione cloud come punto di distribuzione pull.  

- Non è possibile configurare il ruolo di punto di distribuzione in un server del sito come punto di distribuzione pull.  

- La configurazione del contenuto pre-installazione sostituisce la configurazione del punto di distribuzione pull. Se si attiva l'opzione **Abilita questo punto di distribuzione per il contenuto pre-installato** in un punto di distribuzione pull, tale punto di distribuzione attende il contenuto e non ne esegue il pull dal punto di distribuzione di origine. Come un punto di distribuzione standard abilitato per il contenuto pre-installato, non riceve contenuto dal server del sito. Per altre informazioni, vedere [Contenuto pre-installato](manage-network-bandwidth.md#BKMK_PrestagingContent).  

- Un punto di distribuzione pull non usa le configurazioni della pianificazione o dei limiti di velocità. Quando si configura un punto di distribuzione installato in precedenza come punto di distribuzione pull, le configurazioni per la pianificazione e i limiti di velocità vengono salvate ma non usate. Se in un secondo momento si rimuove la configurazione del punto di distribuzione pull, vengono implementate le configurazioni della pianificazione e dei limiti di velocità configurate in precedenza.  

    > [!NOTE]  
    >  Le schede **Pianificazione** e **Limiti di velocità** non sono visibili nelle proprietà del punto di distribuzione.  

- I punti di distribuzione pull non usano le impostazioni della scheda **Generale** di **Proprietà componente distribuzione software** per ogni sito. Tali impostazioni includono **Impostazioni distribuzione simultanea** e **Impostazioni tentativi multicast**.  

- Per trasferire contenuto da un punto di distribuzione di origine in una foresta remota, installare il client di Configuration Manager nel punto di distribuzione pull. Configurare anche un account di accesso alla rete che possa accedere al punto di distribuzione di origine. Se si abilita l'opzione del sito **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP** non è necessario un account di accesso alla rete.<!--1358228-->  

- Se il punto di distribuzione pull è anche un client di Configuration Manager, la versione del client deve essere identica a quella del sito di Configuration Manager che installa il punto di distribuzione pull. Il punto di distribuzione pull usa CCMFramework, comune al punto di distribuzione pull e al client di Configuration Manager.  

## <a name="about-source-distribution-points"></a>Informazioni sui punti di distribuzione di origine  

Quando si configura il punto di distribuzione pull, specificare uno o più punti di distribuzione di origine:  

- La procedura guidata visualizza solo i punti di distribuzione che sono qualificati per essere usati come punti di distribuzione di origine.  

- Un punto di distribuzione pull può essere specificato come un punto di distribuzione di origine per un altro punto di distribuzione pull.  

- Quando si usa la console di Configuration Manager, come punti di distribuzione di origine possono essere specificati solo i punti di distribuzione che supportano HTTP.  

- Usare Configuration Manager SDK per specificare un punto di distribuzione di origine configurato per HTTPS. Per usare un punto di distribuzione di origine configurato per HTTPS, installare il client di Configuration Manager nel punto di distribuzione pull.  

- Se gli uffici remoti hanno una connessione Internet più efficiente oppure se si vuole ridurre il carico sui collegamenti WAN, usare come origine un [punto di distribuzione cloud](use-a-cloud-based-distribution-point.md) in Microsoft Azure. Per comunicare con Microsoft Azure, il punto di distribuzione pull richiede l'accesso a Internet. Il contenuto deve essere distribuito al punto di distribuzione cloud di origine.<!--1321554-->  

    > [!Note]  
    > Questa funzionalità comporta l'addebito alla sottoscrizione di Azure per l'archiviazione dei dati e il traffico di rete in uscita. Per altre informazioni, vedere il [costo per l'uso di punti di distribuzione cloud](use-a-cloud-based-distribution-point.md#bkmk_cost).  

> [!Tip]  
> Un punto di distribuzione pull che scarica contenuto da un punto di distribuzione di origine viene conteggiato come un client nella colonna **Client a cui è stato effettuato l'accesso (univoco)** del report **Riepilogo di utilizzo dei punti di distribuzione** .  

### <a name="source-priorities"></a>Priorità delle origini

- Assegnare una priorità separata a ogni punto di distribuzione di origine oppure assegnare la stessa priorità a più punti di distribuzione di origine.  

- La priorità determina l'ordine in cui il punto di distribuzione pull richiede contenuto dai punti di distribuzione di origine.  

- Inizialmente viene contattato il punto di distribuzione di origine con il valore di priorità più basso. Se sono presenti più punti di distribuzione di origine con la stessa priorità, il punto di distribuzione pull seleziona in modo casuale una delle origini con tale priorità.  

- Se il contenuto non è disponibile nell'origine selezionata, il punto di distribuzione pull prova a scaricarlo da un altro punto di distribuzione con la stessa priorità.  

- Se nessuno dei punti di distribuzione con una determinata priorità ha il contenuto, il punto di distribuzione pull prova a scaricarlo da un punto di distribuzione di origine con il livello di priorità successivo. Questa ricerca continua finché non viene individuato il contenuto.

- Se nessuno dei punti di distribuzione di origine assegnati ha il contenuto, il punto di distribuzione pull attende 30 minuti e quindi avvia di nuovo il processo.  

## <a name="inside-the-pull-distribution-point"></a>All'interno del punto di distribuzione pull

- Per gestire il trasferimento di contenuto, i punti di distribuzione pull usano il componente **CCMFramework**, che è incluso nel client di Configuration Manager.  

- Quando si abilita il punto di distribuzione pull, il sito installa **pulldp.msi**. Questo programma di installazione aggiunge anche il componente CCMFramework. Non richiede l'installazione del client di Configuration Manager.  

- Dopo l'installazione del punto di distribuzione pull, per il relativo funzionamento viene usato principalmente il servizio **CCMExec**.  

- Quando il punto di distribuzione pull trasferisce contenuto, usa **Servizio trasferimento intelligente in background** (BITS), integrato in Windows. Un punto di distribuzione pull non richiede l'installazione dell'estensione BITS per il server IIS.<!--sms.503672 -Clarified BITS use-->

- Per i dettagli operativi, vedere i file di log seguenti nel punto di distribuzione pull:  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> Se vengono visualizzati errori HTTP 403 nei file di log dopo l'aggiunta di un punto di distribuzione pull, apportare le modifiche seguenti:
>
> 1. Nel punto di distribuzione di origine, impostare il valore del Registro di sistema seguente: `HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. Riavviare il server del punto di distribuzione di origine.
>
> Il punto di distribuzione pull dovrebbe quindi iniziare a scaricare il contenuto dall'origine. Per altre informazioni su questa chiave del Registro di sistema, vedere [Panoramica di TLS - SSL (SSP Schannel)](/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview).<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>Vedere anche  

[Concetti di base sulla gestione dei contenuti](fundamental-concepts-for-content-management.md)