---
title: Preparare l'installazione di siti
titleSuffix: Configuration Manager
description: Se si prevede di installare più siti di Configuration Manager, queste informazioni consentono di risparmiare tempo ed evitare errori.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700719"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Preparare l'installazione di siti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per prepararsi a una corretta distribuzione di uno o più siti di Configuration Manager, acquisire familiarità con i dettagli in questo articolo. Questi passaggi possono aiutare a risparmiare tempo durante l'installazione di più siti ed evitare errori che potrebbero richiedere una nuova installazione di uno o più siti.

> [!TIP]
> Quando si gestisce l'infrastruttura della gerarchia e dei siti di Configuration Manager, i termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti distinti. Per informazioni su come viene usato ogni termine, vedere [Informazioni su upgrade, aggiornamento e installazione](../../../understand/upgrade-update-install.md).

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Opzioni per l'installazione di diversi tipi di siti
Quando si installa un nuovo sito di Configuration Manager, la versione dei file di origine che è possibile usare dipende dalla versione dei siti che si trovano già nella gerarchia, se presenti. I metodi di installazione disponibili dipendono dal tipo di sito che si vuole installare.  

Prima di installare un sito verificare di aver pianificato la gerarchia e di aver definito il tipo di sito che si vuole installare. Per altre informazioni, vedere [Progettare una gerarchia di siti](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Primo sito
Il primo sito che si installa in una gerarchia è un sito di amministrazione centrale o un sito primario autonomo.

**Supporti di installazione**: per installare un sito di amministrazione centrale o un sito primario autonomo come primo sito di una nuova gerarchia, è necessario [usare una versione di base](../../../../core/servers/manage/updates.md#bkmk_Baselines) di Configuration Manager. Non installare il primo sito di una nuova gerarchia usando i file di origine aggiornati presenti nella [cartella CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) di qualsiasi sito.

**Metodo di installazione**: è possibile installare uno dei tipi di sito tramite l'[Installazione guidata di System Center Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) oppure è possibile configurare uno script da usare con un'[installazione dalla riga di comando con script](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Siti aggiuntivi
Dopo aver installato il sito iniziale, è possibile aggiungere altri siti in qualsiasi momento. Sono disponibili le opzioni seguenti per aggiungere i siti (fino ai [limiti supportati ](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Siti attualmente disponibili|Tipo di sito aggiuntivo che è possibile installare|
|---|---|
|Sito di amministrazione centrale|Sito primario figlio|
|Sito primario figlio|Sito secondario|
|Sito primario autonomo|Sito secondario (è possibile espandere il sito primario, che converte il sito primario autonomo in un sito primario figlio)|

**Supporti di installazione**: quando si installa un sito di amministrazione centrale per espandere un sito primario autonomo o si installa un nuovo sito primario figlio in una gerarchia esistente, è necessario usare il supporto di installazione (che contiene i file di origine) corrispondente alla versione del sito o dei siti esistenti.

> [!IMPORTANT]
> Se sono stati installati gli aggiornamenti nella console che hanno modificato la versione di siti installati in precedenza, non usare i supporti di installazione originale. In uno scenario di questo tipo usare invece i file di origine della [cartella CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) di un sito aggiornato. Configuration Manager richiede l'uso di file di origine corrispondenti alla versione del sito esistente a cui si connetterà il nuovo sito.

Un sito secondario deve essere installato dalla console di Configuration Manager. In questo modo, i siti secondari vengono sempre installati usando i file di origine del sito primario padre.

**Metodo di installazione**: il metodo usato per installare altri siti dipende dal tipo di sito che si vuole installare.
- **Aggiunta di un sito di amministrazione centrale**:  è possibile usare l'Installazione guidata di Configuration Manager o una riga di comando con script per installare il nuovo sito di amministrazione centrale come sito padre per il sito primario autonomo esistente. Per altre informazioni, vedere [Espansione di un sito primario autonomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Aggiunta di sito primario figlio**:  è possibile usare l'Installazione guidata di Configuration Manager o un'installazione da riga di comando per aggiungere un sito primario figlio sotto un sito di amministrazione centrale.
- **Aggiunta di un sito secondario**:  per installare un sito secondario come sito figlio al di sotto del sito primario, usare la console di Configuration Manager. Altri metodi non sono supportati per l'aggiunta di siti secondari.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a> Attività comuni da completare prima di avviare un'installazione
- **Esaminare la topologia della gerarchia che verrà usata per la distribuzione**    
Per altre informazioni, vedere [Progettare una gerarchia di siti per Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Preparare e configurare singoli server per soddisfare i prerequisiti e le configurazioni supportate per l'uso con Configuration Manager**         
Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

- **Installare e configurare SQL Server per ospitare il database del sito**     
Per altre informazioni, vedere [Supporto per le versioni di SQL Server per Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Preparare l'ambiente di rete per supportare Configuration Manager**      
Per altre informazioni, vedere [Configurare firewall, porte e domini per System Center Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Se si usa un'infrastruttura a chiave pubblica (PKI), preparare l'infrastruttura e i certificati**      
Per altre informazioni, vedere [Requisiti dei certificati PKI per Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Installare gli ultimi aggiornamenti sulla sicurezza nei computer che verranno usati come server del sito o server di sistema del sito e avviarli quando è necessario**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Informazioni su nomi e codici dei siti
I codici e i nomi dei siti dei vengono usati per identificare e gestire i siti in una gerarchia di Configuration Manager. Nella console di Configuration Manager il codice e il nome del sito vengono visualizzati nel formato &lt;*codice sito*\> - &lt;*nome sito*\>. È necessario che ogni codice di sito usato nella gerarchia sia univoco. Se lo schema di Active Directory viene esteso a Configuration Manager e i siti pubblicano dati, i codici di sito usati in una foresta di Active Directory devono essere univoci, anche se vengono usati in una gerarchia diversa di Configuration Manager o sono stati usati in installazioni precedenti di Configuration Manager. Assicurarsi di pianificare con attenzione i codici e i nomi di sito prima della distribuzione della gerarchia.

### <a name="specify-a-site-code-and-site-name"></a>Specificare un codice e un nome del sito
Quando si esegue l'installazione di Configuration Manager vengono richiesti un codice e un nome di sito per il sito di amministrazione centrale e per ogni installazione di sito primario e secondario. Un codice del sito deve identificare in modo univoco ogni sito nella gerarchia. Poiché il codice del sito viene usato nei nomi di cartella, non usare mai i nomi seguenti per il codice del sito, che includono nomi riservati di Configuration Manager e di Windows:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Il programma di installazione di Configuration Manager non verifica se il codice del sito specificato è già in uso.

Per specificare il codice per un sito durante l'installazione di Configuration Manager, è necessario immettere tre caratteri alfanumerici. Solo le lettere dalla *A* alla *Z* e i numeri da *0* a *9*, in qualsiasi combinazione, sono consentiti nei codici di sito. La sequenza di lettere o numeri non ha alcun effetto sulla comunicazione tra siti. Ad esempio, non è necessario denominare un sito primario *ABC* e un sito secondario *DEF*.

Il nome del sito è un identificatore di nome descrittivo per il sito. È possibile usare solo i caratteri dalla *A* alla *Z*, dalla *a* alla *z*, da *0* a *9* e il trattino ( *-* ) nei nomi di sito.

> [!IMPORTANT]
> La modifica del codice o del nome del sito dopo l'installazione del sito non è supportata.

### <a name="reuse-a-site-code"></a>Riutilizzare un codice del sito
I codici di sito non possono essere usati più di una volta in una gerarchia di Configuration Manager per un sito di amministrazione centrale o un sito primario, anche se il sito di origine e il codice del sito sono stati disinstallati. Se si usa di nuovo un codice di sito, si rischiano conflitti tra ID di oggetti nella gerarchia. È possibile riusare il codice del sito per un sito secondario se il sito secondario e il codice del sito non sono più in uso nella gerarchia di Configuration Manager o nella foresta di Active Directory.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limiti e restrizioni per i siti installati
Prima di installare un sito, è importante capire le limitazioni seguenti che si applicano a siti e gerarchie di siti:
- Dopo avere eseguito l'installazione non è possibile modificare le seguenti proprietà del sito senza disinstallare il sito e quindi reinstallarlo usando i nuovi valori:  
  - Directory di installazione dei file di programma  
  - Codice sito  
  - Descrizione sito  
- Se la gerarchia include un sito di amministrazione centrale:  
  - Configuration Manager non consente di spostare un sito primario figlio da una gerarchia per creare un sito primario autonomo o aggiungerlo a un'altra gerarchia. Disinstallare invece il sito primario figlio e reinstallarlo come nuovo sito primario autonomo o come sito figlio del sito di amministrazione centrale di un'altra gerarchia.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a> Passaggi facoltativi prima di eseguire l'installazione
**Eseguire manualmente il [downloader di installazione](../../../../core/servers/deploy/install/setup-downloader.md)**

È possibile eseguire il downloader di installazione per scaricare i file di installazione aggiornati per Configuration Manager. Se il computer in cui si eseguirà l'installazione non è connesso a Internet o se si prevede di installare più server del sito, considerare l'uso del downloader di installazione per scaricare gli aggiornamenti necessari per l'installazione. Altre informazioni:
- Per impostazione predefinita, il programma di installazione si connette a Internet per scaricare i file di installazione aggiornati.
- Per impostazione predefinita, i file vengono archiviati nella cartella Redist.
- È possibile indirizzare il programma di installazione a un percorso nella rete in cui è stata precedentemente memorizzata una copia di questi file.

**Eseguire manualmente il [controllo dei prerequisiti](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Per identificare e correggere i problemi prima di eseguire il programma di installazione per installare un sito e prima di installare un ruolo del sistema del sito in un server, è possibile eseguire il controllo dei prerequisiti. Il controllo dei prerequisiti consente di garantire che il computer soddisfi i requisiti per ospitare il sito o il ruolo del sistema del sito. Altre informazioni:
- Per impostazione predefinita, il programma di installazione esegue il controllo dei prerequisiti.
- In caso di errori, il programma di installazione si interrompe finché il problema non è risolto.

**Identificare le porte facoltative**

È possibile identificare le porte facoltative da usare per i client e i sistemi del sito. Altre informazioni:
- Per impostazione predefinita, i client e i sistemi del sito usano porte predefinite per la comunicazione.
- Durante l'installazione è possibile configurare porte alternative.

Per altre informazioni, vedere [Porte usate](../../../../core/plan-design/hierarchy/ports.md).
