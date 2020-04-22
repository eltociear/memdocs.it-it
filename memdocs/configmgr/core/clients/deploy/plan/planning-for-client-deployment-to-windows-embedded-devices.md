---
title: Pianificazione della distribuzione dei client in dispositivi con Windows Embedded
titleSuffix: Configuration Manager
description: Pianificare la distribuzione dei client in dispositivi con Windows Embedded in Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623125ad64c7ed421ea209137eb68f17891d7a81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694849"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Pianificazione della distribuzione dei client in dispositivi con Windows Embedded in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a> Se il dispositivo con Windows Embedded non include il client di Configuration Manager, è possibile usare qualsiasi metodo di installazione client se il dispositivo soddisfa le dipendenze obbligatorie. Se il dispositivo incorporato supporta filtri di scrittura, è necessario disabilitare tali filtri prima di installare il client, quindi riabilitarli al termine dell'installazione del client e dell'assegnazione a un sito.  

 Se si disabilitano i filtri, prestare attenzione a non disabilitare i driver di filtro. In genere questi driver vengono eseguiti automaticamente all'avvio del computer. La disabilitazione dei driver impedisce l'installazione del client o interferisce con l'orchestrazione dei filtri di scrittura che provoca l'errore delle operazioni dei client. I servizi associati a ogni tipo di filtro di scrittura che deve rimanere in esecuzione sono:  

|Tipo di filtro di scrittura|Driver|Tipo|Descrizione|  
|-----------------------|------------|----------|-----------------|  
|EWF|ewf|Kernel|Impementa il reindirizzamento I/O a livello di settore nei volumi protetti.|  
|FBWF|fbwf|File system|Impementa il reindirizzamento I/O a livello di file nei volumi protetti.|  
|UWF|uwfreg|Kernel|Redirector del Registro di sistema UWF|  
|UWF|uwfs|File system|Redirector del file UWF|  
|UWF|uwfvol|Kernel|Gestore dei volumi UWF|  

 I filtri di scrittura controllano la modalità di aggiornamento del sistema operativo del dispositivo incorporato quando si apportano modifiche, ad esempio quando si installa il software. Quando i filtri di scrittura sono abilitati, anziché apportare i cambiamenti direttamente sul sistema operativo, tali modifiche vengono reindirizzate a una sovrapposizione temporanea. Se le modifiche vengono scritte solo sulla sovrapposizione, vengono perse all'arresto del dispositivo incorporato. Tuttavia, se i filtri di scrittura sono temporaneamente disabilitati, è possibile rendere permanenti le modifiche per evitare di applicarle nuovamente (o reinstallare il software) ad ogni riavvio del dispositivo incorporato. Tuttavia, la disabilitazione temporanea e la successiva riabilitazione dei filtri di scrittura richiede uno o più riavvi. Pertanto, si vorrà probabilmente controllare tale scenario tramite la configurazione di finestre di manutenzione che consentano di eseguire i riavvii al di fuori dell'orario di lavoro.  

 È possibile configurare opzioni per disabilitare e riabilitare automaticamente i filtri di scrittura quando si distribuisce software come applicazioni, sequenze di attività, aggiornamenti software e il client di Endpoint Protection. L'eccezione è per le linee di base della configurazione con elementi di configurazione che usano la correzione automatica. In questo scenario, la correzione si verifica sempre nella sovrapposizione, in modo che sia disponibile solo fino a quando il dispositivo viene riavviato. La correzione viene applicata di nuovo al successivo ciclo di valutazione, ma solo alla sovrapposizione, che viene cancellata al momento del riavvio. Per assicurarsi che Configuration Manager confermi le modifiche di correzione, è possibile distribuire la configurazione di base e quindi eseguire un'altra distribuzione software che supporti la conferma della modifica il prima possibile.  

 Se i filtri di scrittura sono disabilitati, è possibile installare il software sui dispositivi con Windows Embedded usando Software Center. Se sono tuttavia abilitati i filtri di scrittura, l'installazione non viene eseguita correttamente e Configuration Manager visualizza un messaggio di errore relativo ad autorizzazioni insufficienti per installare l'applicazione.  

> [!WARNING]  
>  Anche se non si selezionano le opzioni di Configuration Manager per confermare le modifiche, queste potrebbero essere confermate se viene eseguita un'altra installazione o modifica del software che consente la conferma delle modifiche. In questo scenario, le modifiche originali verranno confermate in aggiunta alle nuove modifiche.  

 Quando Configuration Manager disabilita i filtri di scrittura per eseguire le modifiche in modo permanente, solo gli utenti con diritti amministrativi locali possono accedere e usare il dispositivo integrato. Durante questo periodo, gli utenti con diritti limitati sono bloccati e visualizzano un messaggio che il computer non è disponibile perché è in fase di manutenzione. Ciò consente di proteggere il dispositivo mentre si trova in uno stato in cui le modifiche possono essere applicate in modo permanente e questo comportamento di blocco in modalità di manutenzione costituisce un altro motivo per configurare una finestra di manutenzione per il periodo in cui gli utenti non accederanno a questi dispositivi.  

 Configuration Manager supporta la gestione dei tipi di filtri di scrittura seguenti:  

- Filtro di scrittura basato su file (FBWF): per altre informazioni, vedere [Filtro di scrittura basato su file](https://go.microsoft.com/fwlink/?LinkID=204717).  

- RAM filtro di scrittura avanzato (EWF): per altre informazioni, vedere [Filtro di scrittura avanzato](https://go.microsoft.com/fwlink/?LinkId=204718).  

- Filtro di scrittura unificato (UWF): per altre informazioni, vedere [Filtro di scrittura unificato](https://go.microsoft.com/fwlink/?LinkId=309236).  

  Configuration Manager non supporta operazioni filtro di scrittura quando il dispositivo con Windows Embedded è in modalità registro RAM EWF.  

> [!IMPORTANT]
>  Se possibile, usare i filtri di scrittura basati su file con Configuration Manager per migliorare l'efficienza e la scalabilità.
> 
> **Per i dispositivi che usano solo FBWF:** configurare le eccezioni seguenti per salvare lo stato del client e i dati dell'inventario tra i riavvii del dispositivo:  
> 
> - CCMINSTALLDIR\\\*.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   I dispositivi che eseguono Windows Embedded 8.0 e versioni successive non supportano le esclusioni contenenti caratteri jolly. In questi dispositivi, è necessario configurare singolarmente le esclusioni seguenti:  
> 
> - Tutti i file in CCMINSTALLDIR con estensione sdf, in genere:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **Per i dispositivi che usano solo FBWF e UWF:** Quando i client in un gruppo di lavoro usano i certificati per l'autenticazione nei punti di gestione, è necessario escludere anche la chiave privata per assicurarsi che il client continui a comunicare con il punto di gestione. Configurare le eccezioni seguenti in questi dispositivi:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> Non sono richieste altre eccezioni dal client Configuration Manager diverse da quelle documentate nella casella **Importante** riportata sopra. L'aggiunta di altre eccezioni correlate a Configuration Manager o WMI (WBEM) possono causare errori di Configuration Manager, tra cui il blocco dei dispositivi in modalità di manutenzione o i cicli di riavvio dei dispositivi. Le eccezioni non necessarie includono la directory del client Configuration Manager, la directory CCMcache, la directory CCMSetup, la directory della cache della sequenza di attività, la directory WBEM e le chiavi del Registro di sistema correlate di Configuration Manager.

 Per uno scenario di esempio su come distribuire e gestire dispositivi con Windows Embedded abilitati per il filtro di scrittura in Configuration Manager, vedere [Scenario di esempio per la distribuzione e gestione dei client di Configuration Manager nei dispositivi con Windows Embedded](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Per altre informazioni su come costruire immagini per i dispositivi con Windows Embedded e configurare i filtri di scrittura, vedere la documentazione su Windows Embedded oppure contattare il proprio OEM.  

> [!NOTE]
>  Quando si selezionano le piattaforme applicabili per le distribuzioni software e gli elementi di configurazione, questi visualizzano anziché le famiglie Windows Embedded piuttosto che specifiche versioni. Usare l'elenco riportato di seguito per eseguire il mapping della versione specifica di Windows Embedded per le opzioni nella casella di riepilogo:  
> 
> - **Sistemi operativi Embedded basati su Windows XP (32 bit)** include quanto segue:  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded per punto di servizio  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Sistemi operativi Embedded basati su Windows 7 (32 bit)** include quanto segue:  
> 
>   -   Windows Embedded Standard 7 (32-bit)  
>   -   Windows Embedded POSReady 7 (32 bit)  
>   -   Windows ThinPC  
>   -   **Sistemi operativi Embedded basati su Windows 7 (64 bit)** include quanto segue:  
> 
>   -   Windows Embedded Standard 7 (64-bit)  
>   -   Windows Embedded POSReady 7 (64 bit)
