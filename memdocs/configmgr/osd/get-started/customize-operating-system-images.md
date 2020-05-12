---
title: 'Personalizzare le immagini del sistema operativo '
titleSuffix: Configuration Manager
description: Usare le sequenze di attività di acquisizione e compilazione, la configurazione manuale o una combinazione di entrambe per personalizzare un'immagine del sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 652a0c5e36ce7c4bacf40531a82fdf4e16197d95
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906923"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Personalizzare le immagini del sistema operativo con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le immagini del sistema operativo in Configuration Manager sono file WIM e rappresentano una raccolta compressa di cartelle e file di riferimento necessari per installare e configurare un sistema operativo in un computer. Un'immagine personalizzata del sistema operativo viene creata e acquisita da un computer di riferimento configurato con tutti gli strumenti, gli aggiornamenti software, i file di supporto, i file di sistema del sistema operativo necessari e altre applicazioni software. Il livello di configurazione manuale del computer di riferimento dipende dall'utente. È possibile automatizzare completamente la configurazione del computer di riferimento usando una sequenza di attività di creazione e acquisizione, configurare manualmente determinati aspetti del computer di riferimento e quindi automatizzare gli aspetti rimanenti usando sequenze di attività, oppure configurare manualmente il computer di riferimento senza usare le sequenze di attività. Usare le sezioni seguenti per personalizzare un sistema operativo.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a> Preparare il computer di riferimento  
 Prima di acquisire un'immagine del sistema operativo da un computer di riferimento occorre considerare vari aspetti.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a> Scegliere tra una configurazione automatizzata o manuale  
 Di seguito vengono illustrati vantaggi e svantaggi della configurazione automatizzata e manuale del computer di riferimento.  

#### <a name="automated-configuration"></a>Configurazione automatizzata  
 **Vantaggi**  

- La configurazione può essere completamente automatica, rendendo superflua la presenza di un amministratore o di un utente.  

- È possibile riutilizzare la sequenza attività per ripetere la configurazione di ulteriori computer di riferimento con un elevato livello di attendibilità.  

- È possibile modificare la sequenza attività per gestire le differenze nei computer di riferimento senza la necessità di ricreare l'intera sequenza attività.  

  **Svantaggi**  

- La fase iniziale di creazione e di testing di una sequenza attività può richiedere molto tempo.  

- Se i requisiti del computer di riferimento cambiano in modo significativo, ripetere la fase di creazione e di testing della sequenza attività può richiedere molto tempo.  

#### <a name="manual-configuration"></a>Configurazione manuale  
 **Vantaggi**  

- Non è necessario creare una sequenza attività o soffermarsi sulla verifica e sulla risoluzione dei problemi della sequenza attività.  

- È possibile eseguire l'installazione direttamente dai CD, senza inserire tutti i pacchetti software (compreso lo stesso Windows) in un pacchetto di Configuration Manager.  

  **Svantaggi**  

- La precisione della configurazione del computer di riferimento dipende dall'amministratore o dall'utente che configura il computer.  

- È comunque necessario verificare e testare la corretta configurazione del computer di riferimento.  

- È impossibile riutilizzare il metodo di configurazione.  

- Durante il processo è necessaria la presenza attiva di una persona.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a> Considerazioni per il computer di riferimento  
 Di seguito sono elencati gli elementi di base da prendere in considerazione durante la configurazione di un computer di riferimento.  

-   **Sistema operativo da distribuire**  

     Il computer di riferimento deve essere installato con il sistema operativo che si intende distribuire nei computer di destinazione. Per altre informazioni sui sistemi operativi che è possibile distribuire, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Service Pack appropriato**  

     Il computer di riferimento deve essere installato con il sistema operativo che si intende distribuire nei computer di destinazione.  

-   **Aggiornamenti software appropriati**  

     Installare tutte le applicazioni software che si desidera includere nell'immagine del sistema operativo acquisita dal computer di riferimento. È inoltre possibile installare le applicazioni software quando si distribuisce l'immagine del sistema operativo acquisita nei computer di destinazione.  

-   **Appartenenza al gruppo di lavoro**  

     Il computer di riferimento deve essere configurato come membro di un gruppo di lavoro.  

-   **Sysprep**  

     L'utilità preparazione sistema (Sysprep) è una tecnologia utilizzabile con altri strumenti di distribuzione per installare sistemi operativi Windows in nuovi dispositivi hardware. Sysprep prepara il computer per la creazione dell'immagine del disco o il recapito a un cliente configurando il computer per la creazione di un nuovo ID di sicurezza del computer (SID) al riavvio del computer. Sysprep esegue inoltre la pulizia delle impostazioni specifiche dell'utente e del computer, nonché dei dati da non copiare in un computer di destinazione.  

     È possibile eseguire manualmente Sysprep nel computer di riferimento mediante il seguente comando:  

     `Sysprep /quiet /generalize /reboot`  

     L'opzione /generalize indica a Sysprep di rimuovere i dati specifici del sistema dall'installazione di Windows. Le informazioni specifiche del sistema includono registri eventi, ID di sicurezza univoci (SID) e altre informazioni univoche. Dopo la rimozione delle informazioni di sistema univoche, il computer viene riavviato.  

     È possibile automatizzare Sysprep utilizzando il passaggio della sequenza attività [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) o mediante i supporti di acquisizione.  

    > [!IMPORTANT]  
    >  Il passaggio della sequenza attività [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) tenta di reimpostare la password dell'amministratore locale nel computer di riferimento su un valore vuoto prima dell'esecuzione di Sysprep. Se è attivato il criterio di protezione locale **La password deve soddisfare i requisiti di complessità** , questo passaggio della sequenza attività non consentirà di reimpostare la password dell'amministratore. In questo caso, disattivare il criterio prima di eseguire la sequenza attività.  

     Per altre informazioni su Sysprep, vedere [Panoramica di Sysprep (Utilità preparazione sistema)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).  

-   **Script e strumenti appropriati necessari per attenuare gli scenari di installazione**  

     Script e strumenti appropriati necessari per attenuare gli scenari di installazione  

-   **Personalizzazione desktop appropriata, ad esempio sfondi, personalizzazioni e profili utente predefiniti**  

     È possibile configurare il computer di riferimento con le proprietà di personalizzazione desktop che si desidera includere durante l'acquisizione dell'immagine del sistema operativo dal computer di riferimento. Le proprietà desktop includono sfondi, personalizzazioni organizzative e un profilo utente predefinito standard.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a> Creare manualmente un computer di riferimento  
 Usare la procedura seguente per creare manualmente computer di riferimento.  

> [!NOTE]  
>  Quando si crea il computer di riferimento manualmente, è possibile acquisire l'immagine del sistema operativo usando supporti di acquisizione. Per altre informazioni, vedere [Creare supporti di acquisizione](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Per creare manualmente il computer di riferimento  

1. Individuare il computer da utilizzare come computer di riferimento.  

2. Configurare il computer di riferimento con il sistema operativo appropriato e con il software necessario per creare l'immagine del sistema operativo che si desidera distribuire.  

   > [!WARNING]  
   >  Installare almeno il sistema operativo e il Service Pack appropriati, i driver di supporto e gli aggiornamenti software richiesti.  

3. Configurare il computer di riferimento per l'appartenenza a un gruppo di lavoro.  

4. Reimpostare la password dell'amministratore locale nel computer di riferimento in modo che il valore della password sia vuoto.  

5. Eseguire Sysprep usando il comando:  **sysprep /quiet /generalize /reboot**. L'opzione /generalize indica a Sysprep di rimuovere i dati specifici del sistema dall'installazione di Windows. Le informazioni specifiche del sistema includono registri eventi, ID di sicurezza univoci (SID) e altre informazioni univoche. Dopo la rimozione delle informazioni di sistema univoche, il computer viene riavviato.  

   Quando il computer di riferimento è pronto, usare una sequenza di attività per acquisire l'immagine del sistema operativo da tale computer.  Per informazioni dettagliate, vedere [Acquisire un'immagine del sistema operativo da un computer di riferimento esistente](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a> Usare una sequenza di attività per creare un computer di riferimento  
 È possibile automatizzare il processo di creazione di un computer di riferimento usando una sequenza di attività per distribuire il sistema operativo, i driver, le applicazioni e così via.  Usare i passaggi seguenti per creare il computer di riferimento e quindi acquisire l'immagine del sistema operativo da tale computer.  

-   Usare una sequenza di attività per creare e acquisire l'immagine dal computer di riferimento.  Per informazioni dettagliate sui passaggi da eseguire, vedere [Usare una sequenza di attività per creare e acquisire un computer di riferimento](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  
