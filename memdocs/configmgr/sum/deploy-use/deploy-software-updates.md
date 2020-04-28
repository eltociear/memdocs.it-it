---
title: Distribuire gli aggiornamenti software
titleSuffix: Configuration Manager
description: Informazioni su come distribuire manualmente o automaticamente gli aggiornamenti software nella console di Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 00accfc5150226830b68beb194fa168c08148b84
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110424"
---
# <a name="deploy-software-updates"></a>Distribuire gli aggiornamenti software  

*Si applica a: Configuration Manager (Current Branch)*

La fase di distribuzione degli aggiornamenti software è il processo di distribuzione degli aggiornamenti software. Indipendentemente dalla modalità di distribuzione degli aggiornamenti software, il sito:
- Aggiunge gli aggiornamenti software a un gruppo di aggiornamento software
- Distribuisce il contenuto degli aggiornamenti nei punti di distribuzione
- Distribuisce il gruppo di aggiornamento ai client  

Dopo aver creato la distribuzione, il sito invia un criterio di aggiornamento software associato ai client di destinazione. I client scaricano i file di contenuto degli aggiornamenti software da un'origine del contenuto alla cache locale. I client connessi a Internet scaricano sempre il contenuto dal servizio cloud Microsoft Update. Gli aggiornamenti software sono quindi disponibili per l'installazione da parte del client.   

> [!Tip]  
>  Se un punto di distribuzione non è disponibile, i client nella Intranet possono anche scaricare gli aggiornamenti software da Microsoft Update.  

> [!NOTE]  
>  A differenza di altri tipi di distribuzione, tutti gli aggiornamenti software vengono scaricati nella cache del client. Questa operazione viene eseguita indipendentemente dall'impostazione per la dimensione massima della cache sul client. Per altre informazioni sull'impostazione della cache client, vedere [Configurare la cache del client per i client di Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Se si configura una distribuzione degli aggiornamenti software necessaria, gli aggiornamenti software vengono installati automaticamente alla scadenza programmata. In alternativa, l'utente del computer client può pianificare o avviare l'installazione dell'aggiornamento software prima della scadenza. Dopo il tentativo di installazione, i computer client inviano messaggi di stato al server del sito per segnalare se l'installazione dell'aggiornamento software è stata eseguita correttamente. Per altre informazioni sulle distribuzioni degli aggiornamenti software, vedere [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Esistono tre scenari principali per la distribuzione degli aggiornamenti software: 
- [Distribuzione manuale](#BKMK_ManualDeployment)  
- [Distribuzione automatica](#bkmk_auto)  
- [Distribuzione in più fasi](#bkmk_phased)  

In genere, si effettua inizialmente la distribuzione manuale degli aggiornamenti software per creare una baseline per i client e quindi si gestiscono gli aggiornamenti software sui client usando la distribuzione automatica o la distribuzione in più fasi.  

> [!Note]  
> Non è possibile usare una regola di distribuzione automatica con una distribuzione in più fasi.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Distribuire manualmente gli aggiornamenti software
Scegliere gli aggiornamenti software nella console di Configuration Manager per avviare manualmente il processo di distribuzione. Questo metodo di distribuzione viene usato in genere per:  

- Mantenere aggiornati i client con gli aggiornamenti software obbligatori prima di creare regole di distribuzione automatiche che gestiscono le distribuzioni mensili  

- Distribuire gli aggiornamenti software fuori banda  


Il seguente elenco descrive il flusso di lavoro generale per la distribuzione manuale degli aggiornamenti software:  

1. Filtrare gli aggiornamenti software che usano requisiti specifici. Ad esempio, fornire criteri per il recupero di tutti gli aggiornamenti software critici o della sicurezza necessari su più di 50 client.  

2. Creare un gruppo di aggiornamenti software che contenga gli aggiornamenti software.  

3. Scaricare il contenuto per gli aggiornamenti software nel gruppo di aggiornamenti software.  

4. Distribuire manualmente il gruppo di aggiornamenti software.  

Per altre informazioni e per la procedura dettagliata, vedere [Distribuire manualmente gli aggiornamenti software](manually-deploy-software-updates.md).

> [!Note]
> - A partire dal 21 aprile 2020 Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). È comunque possibile che vengano ancora visualizzati riferimenti al nome precedente nella console di Configuration Manager e nella documentazione di supporto mentre la console viene aggiornata.
> - Quando vengono distribuiti manualmente, gli aggiornamenti del client Office 365 sono disponibili nel nodo **Aggiornamenti di Office 365** in **Gestione client di Office 365** dell'area di lavoro **Raccolta software**. 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Distribuire automaticamente gli aggiornamenti software

Per configurare la distribuzione automatica degli aggiornamenti software, si usa con una regola di distribuzione automatica. Si tratta di un metodo comune di distribuzione per gli aggiornamenti software mensili ("Patch Tuesday") e per la gestione degli aggiornamenti delle definizioni. Per automatizzare il processo di distribuzione, si definiscono i criteri per una regola di distribuzione automatica. L'elenco seguente descrive il flusso di lavoro generale per la distribuzione automatica degli aggiornamenti software:  

1.  Creare una regola di distribuzione automatica che specifica le impostazioni di distribuzione.  

2.  Il sito aggiunge gli aggiornamenti software a un gruppo di aggiornamento software.  

3.  Il sito distribuisce il gruppo di aggiornamento software nei client della raccolta di destinazione.  

Determinare in primo luogo la strategia di distribuzione automatica degli aggiornamenti software. Ad esempio, creare la regola di distribuzione automatica in modo da destinare gli aggiornamenti a una raccolta di client di prova. Dopo aver verificato che gli aggiornamenti software sono stati correttamente installati nel gruppo di prova, aggiungere una nuova distribuzione alla regola. È anche possibile cambiare la raccolta di destinazione nella distribuzione esistente, specificandone una che include un set di client più esteso. Per decidere la strategia da usare, tenere in considerazione i comportamenti seguenti:  

- È possibile modificare le proprietà degli oggetti aggiornamento software creati dalla regola di distribuzione automatica.   

- La regola di distribuzione automatica distribuisce gli aggiornamenti software ai clienti quando questi vengono aggiunti alla raccolta di destinazione.  

- Quando l'utente o la regola di distribuzione automatica aggiunge nuovi aggiornamenti software al gruppo di aggiornamento software, il sito li distribuisce automaticamente ai client nella raccolta di destinazione.  

- Abilitare o disabilitare le distribuzioni in qualsiasi momento per la regola di distribuzione automatica.  


Dopo aver creato una regola di distribuzione automatica, aggiungere altre distribuzioni alla regola. Questa azione consente di gestire la complessità della distribuzione di aggiornamenti diversi in raccolte diverse. Ogni nuova distribuzione dispone dell'intera gamma di funzionalità e dell’esperienza di monitoraggio della distribuzione.  

Ogni nuova distribuzione aggiunta presenta le seguenti caratteristiche:  

- Usa lo stesso gruppo e lo stesso pacchetto di aggiornamento creato durante la prima esecuzione della regola di distribuzione automatica  
- Può essere destinata a una raccolta diversa  
- Supporta proprietà di distribuzione univoca tra cui:  
  -   Ora attivazione  
  -   Scadenza  
  -   Esperienza utente  
  -   Avvisi separati per ogni distribuzione  


Per altre informazioni e per la procedura dettagliata, vedere [Distribuire automaticamente gli aggiornamenti software](automatically-deploy-software-updates.md).



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Distribuire gli aggiornamenti software in più fasi

<!--1358146-->
A partire dalla versione 1810, creare distribuzioni in più fasi per gli aggiornamenti software. Le distribuzioni in più fasi consentono di orchestrare un'implementazione coordinata e in sequenza del software basata su criteri e gruppi personalizzabili.

Per altre informazioni, vedere [Creare distribuzioni in più fasi](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

