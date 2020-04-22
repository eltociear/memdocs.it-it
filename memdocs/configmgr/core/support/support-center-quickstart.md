---
title: Guida introduttiva di Support Center
titleSuffix: Configuration Manager
description: Acquisire rapidamente lo stato di un client di Configuration Manager per la risoluzione dei problemi.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707459"
---
# <a name="support-center-quickstart-guide"></a>Guida introduttiva di Support Center

*Si applica a: Configuration Manager (Current Branch)*

Support Center offre funzionalità avanzate, tra cui la risoluzione dei problemi e la visualizzazione di log in tempo reale. Può essere usato per acquisire in pochi minuti lo stato di un computer client di Configuration Manager. Questa funzionalità prevede l'accesso a client remoti.

Creare un file di *bundle di risoluzione dei problemi* (con estensione zip) per acquisire lo stato del client. Il bundle non contiene solo i file di log. Può includere altri tipi di dati, ad esempio le impostazioni del Registro di sistema e le configurazioni del client. Inviare il bundle a un tecnico del supporto che usa Support Center Viewer.



## <a name="prerequisites"></a>Prerequisiti

- Diritti amministrativi locali per un client di Configuration Manager  

- Programma di installazione di Support Center. Il file si trova nel server del sito nel percorso `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Per altre informazioni, vedere [Support Center - Installazione](support-center.md#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Passaggio 1: Creare un bundle di dati in un client locale

1.  Installare Support Center nel client di Configuration Manager.  

2.  Passare al menu **Start** e selezionare **Support Center** nel gruppo **Microsoft System Center**  

3.  Nella scheda Home della barra multifunzione selezionare **Collect Selected Data** (Raccogli dati selezionati). Per impostazione predefinita, Support Center raccoglie solo il set di dati minimo, vale a dire file di log, configurazione client e sistema operativo.  

4.  Salvare il file di bundle di risoluzione dei problemi (con estensione zip) in una cartella del computer. Per impostazione predefinita, il nome file sarà simile all'esempio seguente: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Passaggio 2: Visualizzare l'aggregazione di dati usando Support Center Viewer

1.  Avviare **Support Center Viewer**. È possibile avviarlo in qualsiasi computer in cui è installato Support Center.  

2.  Selezionare **Open bundle** (Apri bundle), scegliere il file di bundle e selezionare **Open** (Apri).  

3.  Quando Support Center Viewer ha elaborato il file, aprire ogni scheda disponibile. Visualizzare i tipi di dati che Support Center raccoglie per impostazione predefinita:  

    - **Configuration** (Configurazione)  

        - Configurazione del client di Configuration Manager  

        - Sistema operativo  

        - Computer  

        - Servizi  

        - Schede di rete  

    - **Logs** (Log): scegliere una o più voci nell'elenco e selezionare **Open** (Apri). Si apriranno i file di log selezionati in Log Viewer. Usare questa funzionalità per cercare codici di errore e usare filtri avanzati per analizzare più rapidamente i file di log.  



## <a name="collect-more-data"></a>Raccogliere altri dati

Oltre a queste funzionalità di base, Support Center può raccogliere un'ampia gamma di altre informazioni sullo stato del client. Aprire **Support Center** e selezionare **Collect All Data** (Raccogli tutti i dati). Questo processo dura in genere alcuni minuti, anche nei computer più moderni. Support Center raccoglie i dati aggiuntivi seguenti:

- **Policy** (Criteri): informazioni sulle impostazioni dei criteri di Configuration Manager, comprese le configurazioni dei criteri richieste e la configurazione dei criteri effettiva  

- **Certificati**: informazioni sulle chiavi pubbliche per i certificati client. Support Center non raccoglie chiavi private per i certificati.  

- **Client registry** (Registro di sistema client): raccoglie informazioni di configurazione del client dal Registro di sistema. Support Center raccoglie solo le informazioni del Registro di sistema relative a Configuration Manager.  

- **Client WMI** (WMI client): informazioni di configurazione del client da WMI. Support Center non raccoglie criteri client.  

- **Troubleshooting** (Risoluzione dei problemi): dati in tempo reale di risoluzione dei problemi che agevolano la diagnosi dei problemi più comuni dei client con Active Directory, punti di gestione, reti, assegnazioni di criteri e registrazione.  

- **Debug dumps** (Dump del debug): esegue il dump del debug del client e dei processi correlati. I dump del debug possono essere di grandi dimensioni. Abilitare questa opzione solo durante la risoluzione dei problemi di prestazioni del client.  

