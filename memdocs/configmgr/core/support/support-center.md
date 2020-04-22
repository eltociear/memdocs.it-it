---
title: Support Center
titleSuffix: Configuration Manager
description: Risolvere i problemi dei client di Configuration Manager con Support Center.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21279eb2f7d7962d1286d60a599411912d38313a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701319"
---
# <a name="support-center-for-configuration-manager"></a>Support Center per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357489-->
A partire dalla versione 1810, è possibile usare il Supporto tecnico per risolvere i problemi dei client, visualizzare i log in tempo reale o acquisire lo stato di un client di Configuration Manager per l'analisi successiva. Support Center è un singolo strumento che consolida numerosi strumenti di risoluzione dei problemi per gli amministratori.


## <a name="about"></a>Informazioni su

Scopo di Support Center è ridurre problematiche e difficoltà che si riscontrano durante la risoluzione dei problemi che riguardano i computer client di Configuration Manager. In precedenza, quando si lavorava con il supporto alla risoluzione di un problema relativo ai client di Configuration Manager, era necessario raccogliere manualmente i file di log e altre informazioni necessarie. Era facile dimenticare accidentalmente un file di log fondamentale, causando altri problemi sia all'utente che al personale del supporto.

Support Center consente di semplificare la procedura e di eseguire le attività seguenti:

- Creare un bundle di risoluzione dei problemi (file con estensione zip) contenente i file di log del client di Configuration Manager. In questo modo sarà necessario inviare un solo file al personale del supporto.  

- Visualizzare file di log, certificati, impostazioni del Registro di sistema, dump del debug, criteri client di Configuration Manager.  

- Usare funzionalità di diagnostica in tempo reale dell'inventario (sostituisce Client Spy), dei criteri (sostituisce Policy Spy) e della cache del client.  

### <a name="support-center-viewer"></a>Support Center Viewer

Support Center include Support Center Viewer, un visualizzatore che consente al personale di aprire il bundle di file creato con Support Center. L'agente di raccolta dati di Support Center raccoglie i log di diagnostica da un client locale e remoto di Configuration Manager e crea un pacchetto. Per visualizzare i bundle dell'agente di raccolta dati, usare l'applicazione per la visualizzazione.

### <a name="support-center-log-file-viewer"></a>Visualizzatore di file di log di Support Center

Support Center include un visualizzatore di log moderno. Questo strumento sostituisce CMTrace e include un'interfaccia personalizzabile, con il supporto per schede e finestre ancorabili. Offre un livello di presentazione veloce e può caricare file di log di grandi dimensioni in pochi secondi.

### <a name="support-center-onetrace-preview"></a>Supporto tecnico OneTrace (anteprima)

<!--3555962-->
A partire dalla versione 1906 **OneTrace** è un nuovo visualizzatore log del Supporto tecnico. Funziona in modo analogo a CMTrace, con miglioramenti. Per altre informazioni, vedere [Supporto tecnico OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>Cmdlet di PowerShell

Support Center include anche [i cmdlet di Windows PowerShell](https://go.microsoft.com/fwlink/?linkid=397830). Questi cmdlet consentono di creare una connessione remota a un altro client di Configuration Manager, configurare le opzioni di raccolta dati e avviare la raccolta dei dati.


## <a name="prerequisites"></a>Prerequisiti

Installare i componenti seguenti nel server o nel computer client in cui è installato Support Center:

- Una versione del sistema operativo supportata da Configuration Manager. Per altre informazioni, vedere [Versioni dei sistemi operativi per client](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). Support Center non supporta i dispositivi mobili.  

- È necessario .NET framework 4.5.2 nel computer in cui viene eseguito Support Center e i relativi componenti.  


## <a name="install"></a>Installazione

Individuare il programma di installazione di Support Center nel server del sito nel percorso seguente: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Dopo averlo installato, cercare gli elementi seguenti nel menu Start nel gruppo **Microsoft System Center**:  

- Support Center (ConfigMgrSupportCenter.exe)  
- Visualizzatore dei file di log di Support Center (CMLogViewer.exe)  
- Support Center Viewer (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>Problemi noti

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>Non è possibile installare la versione più recente se è già installata una versione precedente

<!--SCCMDocs-pr issue #3090-->
*Si applica alle versioni 1810 e 1902*

Se è già stata installata una versione precedente del Supporto tecnico, il nuovo programma di installazione ha esito negativo. Questo problema è dovuto alla modalità di controllo delle versioni dei file, tra la versione originale e la versione più recente. Per risolvere questo problema, disinstallare prima di tutto la versione meno recente di Support Center. Quindi installare la versione più recente.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Le connessioni remote devono includere il nome del computer o il dominio come parte del nome utente

Se ci si connette a un client remoto da Support Center, al momento di stabilire la connessione è necessario specificare il nome del computer o il nome di dominio per l'account utente. Se si usa un nome computer o un nome di dominio abbreviato (ad esempio `.\administrator`), la connessione avrà esito positivo, ma Support Center non raccoglierà i dati dal client.

Per evitare questo problema, usare i formati di nome utente seguenti per connettersi a un client remoto:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Potrebbe essere necessario rimuovere le connessioni SMB con script ai client remoti

Quando ci si connette ai client remoti usando il cmdlet [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) di PowerShell, Support Center crea una connessione SMB a ogni client remoto. Tali connessioni vengono mantenute dopo aver completato la raccolta dei dati. Per evitare di superare il numero massimo di connessioni remote per Windows, usare il comando `net use` per visualizzare il set di connessioni remote attualmente attivo. A questo punto, disabilitare tutte le connessioni non necessarie usando il comando seguente: `net use <connection_name> /d`,
dove `<connection_name>` è il nome della connessione remota.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>La richiesta del ciclo di valutazione della distribuzione dell'applicazione non viene inviata correttamente ai computer remoti

<!--2849356-->
*Si applica alla versione 1810*

Nel Supporto tecnico, se si seleziona **Application deployment evaluation** (Valutazione distribuzione applicazione) dall'azione **Invoke trigger** (Richiama trigger) nella scheda **Content** (Contenuto), questa azione avvia un'attività che valuta le applicazioni distribuite. Se si è connessi a un client locale, vengono valutate le distribuzioni delle applicazioni sia per computer che per utente. Se si è connessi a un client remoto, invece, vengono valutate solo le distribuzioni delle applicazioni per computer.


## <a name="next-steps"></a>Passaggi successivi

[Guida introduttiva di Support Center](support-center-quickstart.md)
