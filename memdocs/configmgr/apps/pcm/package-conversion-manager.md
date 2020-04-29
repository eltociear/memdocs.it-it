---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Informazioni sull'uso di Package Conversion Manager per convertire i pacchetti in applicazioni in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689009"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357861-->

A partire dalla versione 1806, Package Conversion Manager consente di convertire i pacchetti legacy di Configuration Manager in applicazioni. Le applicazioni offrono vantaggi aggiuntivi, come dipendenze, regole dei requisiti, metodi di rilevamento e affinità utente-dispositivo.

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1806 come [funzionalità di una versione non definitiva](../../core/servers/manage/pre-release-features.md). A partire dalla versione 1810, questa funzionalità non è più in versione non definitiva.  


Un'applicazione di Configuration Manager contiene file e programmi che possono essere distribuiti ai dispositivi client. Tuttavia, a differenza dei pacchetti e dei programmi legacy, un'applicazione fornisce funzionalità aggiuntive specifiche per l'utente. Ad esempio, un'applicazione potrebbe contenere tipi di distribuzione per un'installazione locale di un pacchetto software, un pacchetto di applicazioni virtuali o una versione dell'applicazione per dispositivi mobili.

Per altre informazioni, vedere gli articoli seguenti: 
- [Introduzione alla gestione delle applicazioni](../understand/introduction-to-application-management.md)  
- [Pacchetti e programmi](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Se è già installata una versione precedente di Package Conversion Manager, disinstallarla prima di aggiornare il sito. Questa versione integrata non richiede l'installazione, ma possono verificarsi conflitti con le versioni esistenti.  

La versione integrata di Package Conversion Manager funziona con i pacchetti nel sito di Configuration Manager Current Branch. Non si tratta di uno strumento autonomo. Se si hanno pacchetti e programmi in una versione precedente di Configuration Manager, eseguire prima di tutto la migrazione dei pacchetti nel sito Current Branch. Per altre informazioni, vedere [Eseguire la migrazione dei dati da una gerarchia all'altra](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager versione 1902 include i miglioramenti seguenti:
- L'analisi pianificata dei pacchetti viene eseguita ogni 7 giorni per impostazione predefinita
- Cmdlet di PowerShell per l'analisi e la conversione dei pacchetti
- Miglioramenti e correzioni di bug generali



## <a name="planning"></a>Pianificazione

Prima di iniziare a convertire i pacchetti in applicazioni, sviluppare un piano. Il processo seguente è un piano di esempio:

- [Definire un piano di conversione dei pacchetti dettagliato](#bkmk_define)  

- [Selezionare e preparare i pacchetti per la conversione](#bkmk_prepare)  

- [Selezionare i pacchetti di test](#bkmk_test)  

- [Analizzare, esaminare e convertire i pacchetti](#bkmk_analyze)  

- [Testare e distribuire le applicazioni](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a>Definire un piano di conversione dei pacchetti dettagliato

Questa sezione descrive due piani di conversione dei pacchetti di esempio:  

- [Ambiente di test con ampia disponibilità di risorse](#bkmk_define-high): è presente un ambiente di test con risorse, autorizzazioni e architettura sufficienti per replicare l'intero ambiente di produzione.  

- [Ambiente di test con quantità limitata di risorse](#bkmk_define-limited): non è presente un ambiente di test che consente di replicare l'intero ambiente di produzione.  

Modificare questi piani in base alle esigenze per altri problemi specifici dell'ambiente in uso.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a> Piano di esempio relativo a un ambiente di test con quantità elevata di risorse

L'ambiente di test ha risorse, autorizzazioni e architettura simili a quelle dell'ambiente di produzione. Usare l'ambiente di test per analizzare e convertire tutti i pacchetti in modo efficiente e quindi testare tutte le applicazioni di Configuration Manager. Dopo aver completato il processo, eseguire il trasferimento nell'ambiente di produzione. 

I passaggi del piano di conversione dei pacchetti saranno analoghi ai seguenti:  

1.  Selezionare i pacchetti da convertire.  

2.  Eseguire la migrazione dei pacchetti da convertire nell'ambiente di test.  

3.  Preparare i pacchetti alla conversione.  

4.  Selezionare i pacchetti test.  

5.  Analizzare, esaminare e convertire i pacchetti di test.  

6.  Sottoporre a test le applicazioni convertite.  

7.  Analizzare e convertire i pacchetti rimanenti (non di test).  

8.  Esportare le applicazioni dall'ambiente di test. Importarle nell'ambiente di produzione.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a> Piano di esempio relativo a un ambiente di test con quantità limitata di risorse

L'ambiente di test non ha risorse, autorizzazioni e architettura simili a quelle dell'ambiente di produzione. Non è possibile analizzare, testare e convertire tutti i pacchetti. In questo scenario analizzare, esaminare, convertire e testare solo i pacchetti di test. Eseguire quindi la migrazione dei pacchetti rimanenti nell'ambiente di produzione al fine di eseguire l'analisi e la conversione. 

I passaggi del piano di conversione dei pacchetti saranno analoghi ai seguenti:

1.  Selezionare i pacchetti da convertire.  

2.  Selezionare i pacchetti test.  

3.  Eseguire la migrazione dei pacchetti test nell'ambiente di testing.  

4.  Preparare i pacchetti test alla conversione.  

5.  Analizzare, esaminare e convertire i pacchetti di test.  

6.  Sottoporre a test le applicazioni convertite.  

7.  Esportare le applicazioni di test dall'ambiente di test. Importarle quindi nell'ambiente di produzione.  

8.  Eseguire la migrazione dei pacchetti rimanenti nell'ambiente di produzione e prepararli alla conversione.  

9.  Analizzare, esaminare e convertire i pacchetti rimanenti nell'ambiente di produzione.  

10. Rilasciare le altre applicazioni nell'ambiente di produzione.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a>Selezionare e preparare i pacchetti per la conversione

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a> Selezionare i pacchetti da convertire

Non tutti i pacchetti possono essere convertiti in applicazioni. Prima di iniziare a convertire i pacchetti, identificare quelli che non verranno convertiti. 

I tipi di pacchetti più adatti ad essere convertiti in applicazioni sono quelli che includono software rivolti all'utente, ad esempio:  

- File di Windows Installer (con estensione MSI e MSU)  

- Programmi Microsoft Application Virtualization (App-V)  

- File eseguibili di Windows (con estensione EXE)  

I tipi di pacchetti che non vengono convertiti in applicazioni e vengono conservati come pacchetti includono:

- Strumenti di manutenzione del sistema. Ad esempio, script o utilità di backup.  

- Pacchetti software per i quali non è più disponibile il supporto.

> [!Tip]  
> Dopo avere identificato i pacchetti non appropriati per la conversione in applicazioni, spostarli in una cartella separata nella console di Configuration Manager. Per creare una cartella dei pacchetti nella console di Configuration Manager:  
> - Fare clic con il pulsante destro del mouse sul nodo **Pacchetti**.  
> - Selezionare **Cartelle** e quindi **Crea cartella**.  
> - Immettere il nome della cartella, ad esempio `Not Converted`.  
> - Fare clic su **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Preparazione dei pacchetti alla conversione

Verificare che ogni pacchetto da convertire rispetti le seguenti condizioni:  

- Il percorso dei file di origine è un percorso UNC completo, ad esempio `\\Server\Share\File`.  

- I file di Windows Installer usano solo codici prodotto univoci.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a> Selezionare i pacchetti di test

Se possibile, il gruppo di pacchetti di test deve includere pacchetti che soddisfano i criteri seguenti:  

- Almeno un pacchetto test deve disporre dello stato di disponibilità **Automatico**.  

- Almeno un pacchetto test deve disporre dello stato di disponibilità **Manuale**.  

Idealmente, i pacchetti di test devono essere pacchetti principali, ad esempio:  

- Pacchetti noti all'utente.  

- Pacchetti fondamentali per l'organizzazione.  

- Pacchetti che è possibile sottoporre a test con facilità.  

Identificare i pacchetti che sono appropriati per i test. Spostarli quindi in una cartella separata nella console di Configuration Manager.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a>Analizzare, esaminare e convertire i pacchetti

#### <a name="analyze-packages"></a>Analizzare i pacchetti

Per analizzare un singolo pacchetto o un piccolo gruppo, usare Package Conversion Manager, uno strumento integrato nella console di Configuration Manager. Per altre informazioni, vedere [Come analizzare e convertire i pacchetti](how-to-analyze-and-convert.md).  

> [!NOTE]  
> Vedere il nodo **Stato della conversione pacchetti** nell'area di lavoro **Monitoraggio**. Vengono visualizzate informazioni di riepilogo sui processi di analisi e conversione.  

#### <a name="investigate-analysis-results"></a>Esaminare i risultati dell'analisi

Dopo avere analizzato i pacchetti test, esaminare i pacchetti con stato di disponibilità **Manuale** o **Errore**. Determinare i motivi per cui dispongono di tale stato. Lo stato di disponibilità potrebbe essere impostato su **Manuale** o **Errore** per alcuni dei motivi seguenti:

- Il pacchetto non contiene le informazioni necessarie per creare un metodo di rilevamento in un tipo di distribuzione dell'applicazione.  

- Il pacchetto non contiene le informazioni necessarie per convertire le raccolte in requisiti e condizioni globali.  

- Il pacchetto contiene più di un programma.  

- Il pacchetto dipende da un altro pacchetto che non è stato convertito in applicazione.  

Per altre informazioni, vedere le risorse seguenti:  

- Esaminare i messaggi di errore e le relative correzioni in [Informazioni tecniche sui messaggi di errore di Package Conversion Manager](error-messages.md)  

- Esaminare il file di log **PCMTrace.log**  

- [Risolvere i problemi di Package Conversion Manager](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>Convertire i pacchetti

Per altre informazioni su come convertire i pacchetti, vedere [Come analizzare e convertire i pacchetti](how-to-analyze-and-convert.md).

> [!NOTE]  
> Vedere il nodo **Stato della conversione pacchetti** nell'area di lavoro **Monitoraggio**. Vengono visualizzate informazioni di riepilogo sui processi di analisi e conversione.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a> Testare e distribuire le applicazioni

Sottoporre a test le applicazioni nell'ambiente di testing o in quello di produzione, in base a quanto previsto dalla pianificazione dettagliata di conversione dei pacchetti.



## <a name="recommendations"></a>Indicazioni

- Usare il nodo **Stato della conversione pacchetti** nell'area di lavoro **Monitoraggio**. Vengono visualizzate informazioni di riepilogo sui processi di analisi e conversione.  

- Esaminare i programmi nei pacchetti noti come wrapper. Usare il plug-in Package Conversion Manager per convertire le funzioni nelle funzionalità di Configuration Manager equivalenti.  

- Verificare completamente tutte le applicazioni convertite prime di distribuirle in un ambiente di produzione.  



## <a name="next-steps"></a>Passaggi successivi

[Come analizzare e convertire i pacchetti](how-to-analyze-and-convert.md)
