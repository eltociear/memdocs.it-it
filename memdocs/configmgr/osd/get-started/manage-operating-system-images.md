---
title: Gestire le immagini del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni sui metodi per gestire le immagini del sistema operativo archiviate nei file di immagine di Windows (WIM).
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa574cd3db2e7a3d3277912ed4a383f71d33e59c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124288"
---
# <a name="manage-os-images-with-configuration-manager"></a>Gestire le immagini del sistema operativo con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le immagini del sistema operativo in Configuration Manager sono archiviate nel formato file di immagine di Windows (WIM). Queste immagini sono una raccolta compressa dei file e delle cartelle di riferimento usati per installare e configurare un nuovo sistema operativo in un computer. Molti scenari di distribuzione del sistema operativo richiedono un'immagine del sistema operativo.


## <a name="os-image-types"></a>Tipi di immagine del sistema operativo

È possibile usare un'[immagine del sistema operativo predefinita](#default-image) o crearne una da un [computer di riferimento](#bkmk_capture) configurato dall'utente. Quando si configura il computer di riferimento, si aggiungono al sistema operativo i file del sistema operativo e driver, file di supporto, aggiornamenti software, strumenti ed applicazioni. Quindi si acquisisce il sistema operativo per creare il file immagine.

### <a name="default-image"></a>Immagine predefinita

I file di installazione di Windows includono l'immagine del sistema operativo predefinita. Questa immagine è un'immagine del sistema operativo di base, che contiene un set di driver standard. Quando si usa l'immagine del sistema operativo predefinita, usare i passaggi della sequenza di attività per installare le app e aggiungere altre configurazioni dopo l'installazione del sistema operativo in un dispositivo. Individuare l'immagine del sistema operativo predefinita nei file di origine di Windows: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Vantaggi dell'immagine predefinita

- Le dimensioni dell'immagine sono minori di quelle di un'immagine acquisita.  

- L'installazione di app e l'esecuzione di configurazioni con i passaggi di una sequenza di attività sono operazioni più dinamiche. Ad esempio è possibile modificare le configurazioni e le app installate nella sequenza di attività, senza dover ricreare l'immagine del dispositivo.  

#### <a name="default-image-disadvantages"></a>Svantaggi dell'immagine predefinita

- L'installazione del sistema operativo può richiedere più tempo. L'installazione delle applicazioni e altre configurazioni si verificano al termine dell'installazione del sistema operativo.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> Immagine acquisita da un computer di riferimento

Per creare un'immagine del sistema operativo personalizzata, creare un computer di riferimento con il sistema operativo desiderato. Quindi installare le applicazioni e configurare le impostazioni desiderate. Acquisire l'immagine del sistema operativo dal computer di riferimento per creare il file con estensione wim. Creare manualmente il computer di riferimento oppure usare una sequenza di attività per automatizzare alcune o tutte le istruzioni di creazione. Per altre informazioni, vedere [Customize OS images](customize-operating-system-images.md) (Personalizzare le immagini del sistema operativo).  

#### <a name="captured-image-advantages"></a>Vantaggi dell'immagine acquisita

- L'installazione può essere più rapida rispetto all'uso dell'immagine predefinita. Ad esempio è possibile preinstallare le applicazioni con l'immagine acquisita del sistema operativo. Quindi non è necessario installare le stesse applicazioni in un secondo momento usando i passaggi della sequenza di attività.  

#### <a name="captured-image-disadvantages"></a>Svantaggi dell'immagine predefinita

- Le dimensioni dell'immagine sono potenzialmente maggiori di quelle dell'immagine predefinita.  

- Se sono necessari aggiornamenti per le applicazioni e gli strumenti, sarà necessario creare una nuova immagine.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> Aggiungere un'immagine del sistema operativo  

Prima di poter usare un'immagine del sistema operativo, è necessario aggiungerla al sito di Configuration Manager.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Immagini del sistema operativo**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi immagine del sistema operativo**. Questa azione avvia l'Aggiunta guidata immagine del sistema operativo.  

3. Nella pagina **Origine dati** specificare le informazioni seguenti:

    - **Percorso** di rete al file di immagine del sistema operativo. Ad esempio, `\\server\share\path\image.wim`

    - **Estrai un indice delle immagini specifico dal file WIM specificato** e selezionare un indice delle immagini dall'elenco.<!--3719699--> A partire dalla versione 1902, questa opzione importa automaticamente un solo indice anziché tutti gli indici delle immagini nel file. L'uso di questa opzione genera un file di immagine più piccolo e un'installazione offline più rapida. Supporta anche il processo [Servizio immagini ottimizzato](#bkmk_resetbase) che genera un file di immagine più piccolo dopo l'applicazione degli aggiornamenti software.  

        > [!Note]  
        > Configuration Manager non modifica il file di immagine di origine. Crea un nuovo file di immagine nella stessa directory di origine.
        >
        > Questo processo di estrazione può non riuscire per i file di immagine di dimensioni molto elevate, ad esempio oltre i 60 GB. L'errore DISM è `Not enough storage is available to process this command.` La riga di comando usata da Configuration Manager è nei file smsprov.log e dism.log. Eseguire manualmente lo stesso comando e quindi importare l'immagine.<!-- SCCMDocs-pr issue 3502 -->  

    - A partire dalla versione 1906, se si vuole memorizzare anticipatamente il contenuto nella cache in un client, specificare **Architettura** e **Lingua** dell'immagine. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. Nella pagina **Generale** specificare le informazioni seguenti. Queste informazioni sono utili per scopi di identificazione quando sono presenti più immagini del sistema operativo.  

    - **Nome**: nome univoco per l'immagine. Per impostazione predefinita il nome deriva dal nome del file con estensione wim.  

    - **Versione**: identificatore di versione facoltativo. Questa proprietà non deve corrispondere alla versione del sistema operativo dell'immagine. Si tratta spesso della versione assegnata dall'organizzazione al pacchetto.  

    - **Commento**: breve descrizione facoltativa.  

5. Completare la procedura guidata.  

Per il cmdlet di PowerShell equivalente a questa procedura guidata della console, vedere [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Quindi distribuire l'immagine del sistema operativo ai punti di distribuzione.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> Distribuire contenuti ai punti di distribuzione  

Distribuire le immagini del sistema operativo nei punti di distribuzione, con le stesse modalità usate per altri contenuti. Prima di distribuire la sequenza di attività, distribuire l'immagine del sistema operativo ad almeno un punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> Preparare l'immagine del sistema operativo per le distribuzioni multicast  

Usare le distribuzioni multicast per consentire a più computer di scaricare simultaneamente un'immagine del sistema operativo. Il punto di distribuzione esegue il multicast dell'immagine nei client e, evitando che ogni client scarichi una copia dell'immagine dal punto di distribuzione con una connessione separata. Quando si sceglie come metodo di distribuzione del sistema operativo l'[uso del multicast per distribuire Windows in rete](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), configurare l'immagine del sistema operativo in modo che supporti il multicast. Quindi distribuire l'immagine ai punti di distribuzione abilitati per il multicast.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Immagini del sistema operativo**.  

2. Selezionare l'immagine del sistema operativo che si desidera distribuire a un punto di distribuzione abilitato per il multicast.  

3. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

4. Passare alla scheda **Impostazioni distribuzione** e configurare le seguenti opzioni:  

    - **Consenti trasferimento del pacchetto via multicast (solo WinPE)** : selezionare questa opzione per abilitare la distribuzione simultanea delle immagini del sistema operativo da parte di Configuration Manager tramite multicast.  

    - **Crittografa pacchetti multicast**: specificare se il sito deve crittografare l'immagine prima di inviarla al punto di distribuzione. Usare questa opzione se l'immagine contiene informazioni riservate. Se l'immagine non è crittografata, il relativo contenuto è visibile in rete come testo non crittografato. Un utente non autorizzato può intercettare e visualizzare il contenuto dell'immagine.  

    - **Trasferisci il pacchetto solo via multicast**: Specificare se si vuole che il punto di distribuzione distribuisca l'immagine solo durante una sessione multicast.  

         Se si seleziona l'opzione **Trasferisci il pacchetto solo via multicast**, è necessario specificare anche l'opzione di distribuzione della sequenza attività **Scaricare il contenuto localmente quando necessario eseguendo la sequenza attività**. Per altre informazioni, vedere [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md).  

5. Selezionare **OK** per salvare le impostazioni e chiudere le proprietà dell'immagine.  
