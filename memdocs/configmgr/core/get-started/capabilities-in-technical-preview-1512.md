---
title: Funzionalità nella Technical Preview 1512
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1512 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f52d6956cf860de8e45ac4e532500d32bcf077ba
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074504"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1512 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1512. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.  

 Di seguito sono riportate le nuove funzionalità disponibili con questa versione.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a> Attestazione dell'integrità dei dispositivi  
 A partire dalla versione Technical Preview 1512, gli amministratori possono visualizzare lo stato di attestazione dell'integrità dei dispositivi Windows 10 nella console di Configuration Manager.  Questa funzionalità è disponibile per Configuration Manager e Configuration Manager con Microsoft Intune. L'attestazione dell'integrità dei dispositivi consente all'amministratore di assicurare che i computer client dispongano di configurazioni attendibili di BIOS, TPM e software di avvio. Per supportare l'attestazione dell'integrità dei dispositivi, i dispositivi client devono eseguire Windows 10 con TPM 2 abilitato. L'attestazione dell'integrità dei dispositivi visualizza il numero di dispositivi abilitati per ognuno degli elementi seguenti:  

-   Antimalware ad esecuzione anticipata  

-   BitLocker  

-   Avvio protetto  

-   Integrità del codice  

Nella console vengono inoltre visualizzate le principali impostazioni di attestazione dell'integrità mancanti con il numero di dispositivi.  

Per poter visualizzare l'attestazione dell'integrità del dispositivo, nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** , fare clic sul nodo **Sicurezza** e quindi su **Attestazione dell'integrità**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a> Monitoraggio di termini e condizioni nella console  
A partire dalla versione Technical Preview 1512, quando si integra Configuration Manager con Microsoft Intune, è possibile usare la console di Configuration Manager per visualizzare gli utenti che hanno accettato i termini e le condizioni configurati dal reparto IT e quelli che non lo hanno fatto.  

**Per visualizzare le informazioni di riepilogo:**  

-   Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Distribuzioni** e selezionare la distribuzione dei termini e delle condizioni che si vuole visualizzare.  

**Per visualizzare informazioni dettagliate:**  

1.  Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Termini e condizioni** e selezionare i termini e condizioni che si vuole visualizzare.  

2.  Nella parte inferiore della console selezionare la scheda **Distribuzioni**, selezionare la distribuzione e quindi fare clic su **Visualizza stato.**  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a> Miglioramenti delle impostazioni dei criteri di Endpoint Protection  
Nella Technical Preview 1512 sono state aggiunte le nuove impostazioni seguenti nei criteri antimalware di Endpoint Protection:  

-   Protezione in tempo reale: **Abilita la protezione per le applicazioni potenzialmente indesiderate al download o prima dell'installazione**  

    -   Le applicazioni potenzialmente indesiderate costituiscono una classificazione delle minacce basata sulla reputazione e sull'identificazione attraverso la ricerca. In genere, si tratta di bundler di applicazioni indesiderate o delle relative applicazioni in bundle.  

    -   Per impostazione predefinita, l'impostazione dei criteri di protezione è abilitata (impostata su "Sì"). Quando è abilitata, questa impostazione blocca le applicazioni potenzialmente indesiderate al momento del download e dell'installazione. Tuttavia, è possibile escludere determinati file o cartelle per soddisfare le esigenze specifiche dell'ambiente.  

-   Impostazioni di analisi: **Analizza le unità di rete mappate quando si esegue un'analisi completa**  

    -   Questa impostazione garantisce maggiore granularità per l'amministratore, per consentire le analisi su richiesta dei file in rete senza il rischio di analizzare sempre le unità di rete mappate durante un'analisi completa pianificata.  

    -   L'opzione **Analizza file di rete** deve essere abilitata ("Sì") perché sia possibile configurare questa impostazione.  

    -   L'impostazione predefinita è "No", che indica che durante un'analisi completa non verrà eseguito l'accesso alle unità di rete mappate.  

-   Impostazioni per l'invio automatico dei file di esempio:  

     Il motore antimalware può richiedere l'invio a Microsoft di file di esempio per un'ulteriore analisi. Per impostazione predefinita, viene sempre visualizzata una richiesta prima dell'invio di tali campioni. Gli amministratori ora possono gestire le impostazioni seguenti per configurare questo comportamento:  

    -   Avanzata: **Abilitare l'invio automatico di file di esempio per consentire a Microsoft di determinare se alcuni elementi rilevati siano dannosi**:  Impostare questa opzione su "Sì" per abilitare l'invio automatico di file di esempio. L'impostazione predefinita è "No", che indica che l'invio automatico dei file di esempio è disabilitato e verrà visualizzata una richiesta agli utenti prima dell'invio degli esempi.   (Questa impostazione è stata introdotta in System Center 2012 R2 Configuration Manager SP1)  

    -   Avanzate: **Consenti agli utenti di modificare le impostazioni di invio automatico dei file di esempio**: questa impostazione determina se un utente con diritti amministrativi locali in un dispositivo può modificare l'impostazione per l'invio automatico dei file di esempio nell'interfaccia del client. L'impostazione predefinita è "No" e indica che le impostazioni possono essere modificate solo in Configuration Manager e gli amministratori locali di un dispositivo non possono modificare questa configurazione.  

         Ad esempio, di seguito viene illustrata l'impostazione di Windows Defender in Windows 10 configurata dall'amministratore come abilitata e l'utente non è in grado di modificarla:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    In più, l'impostazione esistente **Exclude files and folders** (Escludi file e cartelle) nella sezione "Impostazioni di esclusione" dei criteri antimalware di Endpoint Protection è stata migliorata per consentire le esclusioni dei dispositivi. Ad esempio, ora è possibile specificare quanto segue come un'esclusione: **\device\mvfs** (per un file system multiversione). I criteri non convalidano il percorso del dispositivo: i criteri di protezione endpoint sono forniti al motore antimalware nel client che deve essere in grado di interpretare la stringa del dispositivo.  

**Prerequisiti per l'uso dei criteri di Endpoint Protection:**  

Per poter usare i criteri di Endpoint Protection, è prima necessario installare e gestire il client Endpoint Protection usando le impostazioni del client di Endpoint Protection. Questa operazione viene eseguita tramite il client di System Center Endpoint Protection per Windows 7, Windows 8, Windows 8.1 o Windows Defender gestito per Windows 10. Vedere [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
