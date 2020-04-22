---
title: Installazione da riga di comando
titleSuffix: Configuration Manager
description: Informazioni su come eseguire il programma di installazione di Configuration Manager al prompt dei comandi per vari tipi di installazione di siti.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700399"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Usare la riga di comando per installare siti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 È possibile eseguire il programma di installazione di Configuration Manager al prompt dei comandi per installare vari tipi di siti.

## <a name="supported-tasks-for-command-line-installations"></a>Attività supportate per le installazioni da riga di comando
 Questo metodo di installazione supporta le seguenti attività di installazione e manutenzione del sito:

- **Installare un sito di amministrazione centrale o un sito primario da un prompt dei comandi**  
  Visualizzare le [opzioni della riga di comando per il programma di installazione](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Modificare le lingue in uso in un sito di amministrazione centrale o in un sito primario**  
   Per modificare le lingue installate in un sito da un prompt dei comandi (comprese le lingue per i dispositivi mobili), è necessario:  

  - Eseguire il programma di installazione da **&lt;PercorsoInstallazioneConfigMgr\>\Bin\X64** nel server del sito,
  - usare l'opzione della riga di comando **/MANAGELANGS**,
  - specificare un file script che definisca le lingue che si vuole aggiungere o rimuovere.  

    Ad esempio, usare la sintassi del comando seguente: **setupwpf.exe /MANAGELANGS &lt;file script delle lingue\>**  

    Per creare il file script delle lingue, usare le informazioni relative alle [opzioni della riga di comando per la gestione delle lingue](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

- **Usare un file script di installazione per le installazioni automatiche del sito o per il ripristino del sito**  
   È possibile eseguire il programma di installazione da un prompt dei comandi usando uno script di installazione ed eseguire un'installazione automatica del sito. È anche possibile usare questa opzione per ripristinare un sito.    

   Per usare uno script con il programma di installazione:  

  - Eseguire il programma di installazione con l'opzione della riga di comando **/SCRIPT** e specificare un file script.  

  - Il file script deve essere configurato con le chiavi e i valori necessari.  

    Per un'installazione automatica di un sito di amministrazione centrale o di un sito primario, il file script deve avere le sezioni seguenti:  

  - Identification    
  - Options    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    Per ripristinare un sito, è necessario includere anche le sezioni seguenti del file script:  

  - Identification  
  - Modello di

Per altre informazioni, vedere [Ripristino automatico del sito per Configuration Manager](../../manage/unattended-recovery.md).  

Per un elenco di chiavi e valori da usare in un file script di un'installazione automatica, vedere [Chiavi di file script di installazione automatica](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Informazioni sul file script della riga di comando  
 Per le installazioni automatiche di Configuration Manager è possibile eseguire il programma di installazione con l'opzione della riga di comando **/SCRIPT** e specificare un file script che contiene le opzioni di installazione. Le attività seguenti sono supportate da questo metodo:  

-   Installare un sito di amministrazione centrale  
-   Installare un sito primario  
-   Installare una console di Configuration Manager  
-   Ripristinare un sito  

> [!NOTE]  
>  Non è possibile usare il file script di installazione automatica per aggiornare un sito di valutazione a un'installazione con licenza di Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>Nome chiave CDLatest
Quando si usano supporti dalla cartella CD.Latest per eseguire un'installazione controllata da script delle quattro opzioni di installazione seguenti, è necessario che lo script includa la chiave **CDLatest** con valore **1**:
- Install a new central administration site (Installa un nuovo sito di amministrazione centrale)
- Install a new primary site (Installa un nuovo sito primario)
- Recover a central administration site (Ripristina un sito di amministrazione centrale)
- Recover a primary site (Ripristina un sito primario)

Non è possibile usare questo valore con supporti di installazione ottenuti dal sito Microsoft Volume License.
Vedere [Opzioni della riga di comando](command-line-options-for-setup.md) per informazioni su come usare questo nome chiave nel file di script.



### <a name="create-the-script"></a>Creare lo script
Lo script di installazione viene creato automaticamente quando si [esegue il programma di installazione per installare un sito usando l'interfaccia utente](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando si confermano le impostazioni nella pagina **Riepilogo** della procedura guidata, verranno eseguite le operazioni seguenti:  

-   Il programma di installazione crea lo script **%TEMP%\ConfigMgrAutoSave.ini**.  È possibile rinominare il file prima di usarlo, ma è necessario conservare l'estensione di file ini.  
-   Lo script di installazione automatica contiene le impostazioni selezionate nella procedura guidata.  
-   Al termine della creazione dello script, è possibile modificare lo script per installare altri siti nella gerarchia.  
-   È quindi possibile usare questo script per eseguire un'installazione automatica di Configuration Manager.  

Questo file script fornisce le stesse informazioni richieste dall'Installazione guidata, ma non prevede impostazioni predefinite.   
È necessario specificare tutti i valori per le chiavi di installazione che si applicano al tipo di installazione in uso.   

Quando il programma di installazione crea lo script di installazione automatica, viene inserito il valore del codice Product Key immesso durante l'installazione. Può trattarsi di un codice Product Key valido o **EVAL** se si installa una versione di valutazione di Configuration Manager. Il valore del codice Product Key viene inserito nello script per completare il controllo dei prerequisiti.   

Quando il programma di installazione avvia l'installazione del sito effettiva, lo script creato automaticamente viene riscritto per cancellare il valore del codice Product Key nello script creato. Prima di usare lo script per l'installazione automatica di un nuovo sito, è possibile modificare lo script per specificare un codice Product Key valido o un'installazione della versione di valutazione di Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Nomi di sezione, nomi di chiavi e valori
Lo script contiene nomi di sezione, nomi delle chiavi e valori. Tenere presente le informazioni seguenti:
-   I nomi delle chiavi di sezione richiesti variano a seconda del tipo di installazione per cui si crea lo script.
-   L'ordine delle chiavi all'interno delle sezioni e l'ordine delle sezioni all'interno del file non è rilevante.     
-   Alle chiavi non viene applicata la distinzione tra maiuscole e minuscole.  
-   Quando si specificano i valori per le chiavi, il nome della chiave deve essere seguito dal segno uguale (=) e dal valore della chiave.    

> [!TIP]  
>  Per visualizzare il set completo di opzioni, vedere la sezione relativa alle [opzioni della riga di comando per il programma di installazione e gli script](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Usare l'opzione /SCRIPT della riga di comando del programma di installazione

-   È necessario usare un file script di installazione e specificare il nome del file dopo l'opzione **/SCRIPT** della riga di comando del programma di installazione. Tenere presente le informazioni seguenti:   
    -   Il nome del file deve avere l'estensione **INI**.  
    -   Quando si fa riferimento al file script di installazione al prompt dei comandi, è necessario specificare il percorso completo del file. Se, ad esempio, il file di inizializzazione dell'installazione è denominato Setup.ini e viene archiviato nella cartella C:\Setup, al prompt dei comandi digitare:  **setup /script c:\setup\setup.ini**.  

-   L'account che esegue il programma di installazione deve avere diritti di **amministratore** nel computer. Quando si esegue il programma di installazione con lo script automatico, aprire la finestra del prompt dei comandi usando l'opzione **Esegui come amministratore**.   
