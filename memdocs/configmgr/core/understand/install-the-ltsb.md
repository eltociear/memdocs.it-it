---
title: 'Installare un sito usando il supporto di base della versione 1606 '
titleSuffix: Configuration Manager
description: Installare o aggiornare Long-Term Servicing Branch per System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707009"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Eseguire l'installazione e l'aggiornamento con il supporto di base della versione 1606

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Quando si esegue il programma di installazione dal supporto di base della versione 1606 per Configuration Manager, è possibile installare un sito Long-Term Servicing Branch di System Center Configuration Manager.

Il supporto di base è disponibile su DVD come parte di Microsoft System Center 2016 o in System Center Configuration Manager Long-Term Servicing Branch versione 1606. Per informazioni sui supporti di base, vedere [Baseline and update versions](../servers/manage/updates.md#bkmk_Baselines) (Versioni base e di aggiornamento).


Quando si usa il supporto di base della versione 1606, il sito che si installa o a cui si esegue l'aggiornamento è:
- Un *sito Current Branch* equivalente a un sito installato in precedenza con il supporto di base della versione 1511 e quindi aggiornato alla versione 1606 con l'hotfix rollup 1606 (KB3186654).
- Un *sito LTSB* equivalente al sito Current Branch che esegue la versione 1606 con l'hotfix rollup 1606 (KB3186654). Il supporto di base include già l'hotfix rollup.  Ma LTSB non supporta tutte le funzionalità e tutte le caratteristiche disponibili con Current Branch, come descritto in dettaglio in [Introduzione a Long-Term Servicing Branch di System Center Configuration Manager](introduction-to-the-ltsb.md).

Se non si ha familiarità con i diversi rami di Configuration Manager, vedere [Scelta del ramo di Configuration Manager da usare](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Modifiche all'installazione con il supporto di base della versione 1606
Il supporto di base della versione 1606 introduce nel programma di installazione per Configuration Manager le modifiche seguenti.

### <a name="branch-and-edition"></a>Ramo ed edizione
Quando si esegue il programma di installazione, viene ora visualizzata una pagina di gestione licenze in cui è possibile selezionare il ramo di Configuration Manager da installare. È possibile scegliere di installare con licenza Current Branch o LTSB oppure è possibile scegliere una copia di valutazione di Current Branch come installazione senza licenza.

Per altre informazioni, vedere [Licenze e rami per Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Scadenza di Software Assurance
Durante l'installazione, è possibile immettere il valore della **data di scadenza di Software Assurance**. Questo è un valore facoltativo, che è possibile specificare come utile promemoria.

> [!NOTE]
> Microsoft non convalida la data di scadenza immessa e non userà tale data per la convalida della licenza.  È possibile invece usarla come promemoria della data di scadenza. Configuration Manager infatti verifica periodicamente online la disponibilità di nuovi aggiornamenti software. Per usufruire di questi aggiornamenti aggiuntivi, è necessario che lo stato della licenza di Software Assurance sia regolare.    

- È possibile specificare il valore della data nella pagina **Codice Product Key** dell'Installazione guidata quando si esegue il programma di installazione dal supporto di base di Configuration Manager versione 1606.
- È anche possibile specificare la data selezionando **Proprietà delle impostazioni di gerarchia** > **Gestione licenze** nella console di Configuration Manager.

Per altre informazioni, vedere "Contratti Software Assurance" in [Licenze e rami per Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configurazioni aggiuntive pre-aggiornamento
Prima di avviare un aggiornamento di System Center Configuration Manager 2012 a LTSB, è necessario eseguire la procedura aggiuntiva seguente nell'ambito dell'elenco di controllo pre-aggiornamento.  
Disinstallare i ruoli del sistema del sito che LTSB non supporta:
- Punto di sincronizzazione di Asset Intelligence
- Connettore Microsoft Intune
- Punti di distribuzione basati su cloud

Per altre informazioni, vedere [Eseguire l'aggiornamento a Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Nuove opzioni di installazione tramite script
Il supporto di base della versione 1606 supporta una nuova chiave di file di script di installazione automatica per le installazioni tramite script di un nuovo sito di livello superiore. Ciò vale per l'installazione di un nuovo sito primario autonomo o per l'aggiunta di un sito di amministrazione centrale nell'ambito di uno scenario di espansione del sito.

Quando si usa uno script automatico per installare un ramo con licenza, è necessario aggiungere la sezione, i nomi delle chiavi e i valori seguenti nella sezione Opzioni dello script. Non è necessario usare questi valori per lo script di installazione di una copia di valutazione Current Branch:  

 **SABranchOptions**
- **Nome chiave: SAActive**
  - Valori possibili: 0 o 1.  
  - Dettagli:  0 installa una copia di valutazione senza licenza di Current Branch, 1 installa una versione con licenza.   

- **CurrentBranch**
  - Valori possibili: 0 o 1.  
  - Dettagli:  0 installa Long-Term Servicing Branch, 1 installa Current Branch.  

Ad esempio, per installare una versione con licenza di Current Branch si usa:

**Nome chiave: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** funziona solo con il programma di installazione del supporto di base. Non è applicabile quando si esegue il programma di installazione dalla cartella CD.Latest di un sito installato in precedenza tramite il supporto di base della versione 1606.
>
> **SABranchOptions** non si applica agli aggiornamenti tramite script da System Center Configuration Manager 2012 e installa sempre Current Branch.

Per altre informazioni, vedere [Usare una riga di comando per installare i siti di Configuration Manager](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Installare un nuovo sito
Quando si usa il supporto di base della versione 1606 per installare un nuovo sito di uno dei due rami, usare le procedure di pianificazione, preparazione e installazione del sito documentate nell'argomento [Installazione dei siti di Configuration Manager](../servers/deploy/install/installing-sites.md), con l'aggiunta delle considerazioni seguenti per l'installazione:

- Durante l'installazione è necessario scegliere il ramo di Configuration Manager che si vuole installare specificando i dettagli del contratto Software Assurance.
- Tutti i siti di una gerarchia devono eseguire lo stesso ramo. Non è supportata una gerarchia con una combinazione di LTSB e Current Branch in siti diversi.
- Nuova installazione tramite script. Per altre informazioni, tornare a "Nuove opzioni di installazione tramite script" in questo articolo.

## <a name="expand-a-stand-alone-primary-site"></a>Espandere un sito primario autonomo
È possibile espandere un sito primario autonomo in cui è in esecuzione LTSB.  Il processo non è diverso rispetto a quello usato per un sito di Current Branch, con un'avvertenza:

- Quando si installa il nuovo sito di amministrazione centrale è necessario usare il programma di installazione dal supporto originale usato per installare il sito di LTSB. L'esecuzione del programma di installazione dalla cartella CD.Latest non è supportata per questo scenario.

Per altre informazioni sull'espansione di un sito, vedere "Espandere un sito primario autonomo" in [Usare l'installazione guidata per installare i siti di System Center Configuration Manager](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Eseguire l'aggiornamento da System Center Configuration Manager 2012
Quando si esegue l'aggiornamento da Configuration Manager 2012, usare le attività di pianificazione e preparazione del sito e le procedure documentate nell'argomento [Eseguire l'aggiornamento a System Center Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md), ma con le modifiche seguenti:

**Aggiornamento a Current Branch:**
- Durante l'installazione è necessario scegliere Current Branch, specificando i dettagli del contratto Software Assurance.
- Nuova installazione tramite script. Per altre informazioni, tornare a "Nuove opzioni di installazione tramite script" in questo articolo.

**Aggiornamento a LTSB:**  
- Passaggi aggiuntivi da seguire nell'elenco di controllo pre-aggiornamento.
- Durante l'installazione è necessario scegliere LTSB, specificando i dettagli del contratto Software Assurance.
- È possibile aggiornare un sito che esegue System Center 2012 Configuration Manager con Service Pack 1, System Center 2012 Configuration Manager con Service Pack 2, System Center 2012 R2 Configuration Manager con Service Pack 1 o System Center 2012 R2 Configuration Manager senza service pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Percorsi di aggiornamento sul posto per il supporto di base della versione 1606
È possibile usare il supporto di base della versione 1606 per aggiornare a una versione con licenza di Configuration Manager i prodotti seguenti:
- System Center Configuration Manager 2012 R2 con Service Pack 1
- System Center 2012 R2 Configuration Manager senza Service Pack (richiede l'uso del supporto di base della versione 1606 rilasciato il 15 dicembre 2016).
- System Center 2012 Configuration Manager con Service Pack 2
- System Center 2012 Configuration Manager con Service Pack 1 (richiede l'uso del supporto di base della versione 1606 rilasciato il 15 dicembre 2016).


È anche possibile usare questo supporto per aggiornare una versione di valutazione senza licenza di Current Branch a una versione con licenza completa di Current Branch.

Questo supporto non supporta l'aggiornamento di:
- Altre versioni di System Center Configuration Manager 2012.
- Configuration Manager 2007 o versioni precedenti.
- L'installazione di una versione finale candidata di Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Informazioni sulla cartella CD.Latest e su LTSB
Di seguito sono riportate le limitazioni per l'uso del supporto che Configuration Manager crea nella cartella CD.Latest nel server del sito. Questi limiti si applicano ai siti che eseguono LTSB.

Il supporto nella cartella CD.Latest è supportato per:
- Ripristino del sito.
- Manutenzione del sito.
- Installazione di siti primari figlio aggiuntivi.

Il supporto nella cartella CD.Latest non è supportato per:  
- Installazione di un sito di amministrazione centrale nell'ambito di uno scenario di espansione del sito.

Per altre informazioni, vedere [Cartella CD.Latest per System Center Configuration Manager](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Backup, ripristino e manutenzione del sito per LTSB
Per eseguire il backup e il ripristino o eseguire la manutenzione di un sito che esegue LTSB, seguire le linee guida e le procedure in [Backup e ripristino per Configuration Manager](../servers/manage/backup-and-recovery.md).  

Usare il programma di installazione di Configuration Manager della cartella CD.Latest del backup del sito LTSB.
