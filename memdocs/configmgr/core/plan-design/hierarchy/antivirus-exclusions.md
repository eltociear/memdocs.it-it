---
title: Esclusioni dell'antivirus
titleSuffix: Configuration Manager
description: Informazioni sulle esclusioni dell'antivirus consigliate da usare per la risoluzione dei problemi.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703739"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Esclusioni dell'antivirus consigliate per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene raccomandazioni che consentono a un amministratore di determinare la causa della potenziale instabilità di un computer che esegue una versione supportata dei server del sito di Configuration Manager, dei sistemi del sito e dei client quando viene usato insieme a software antivirus.

> [!IMPORTANT]
>
> - Si consiglia di applicare temporaneamente queste procedure per valutare un sistema. Se le prestazioni o la stabilità del sistema vengono migliorate dall'applicazione delle raccomandazioni indicate in questo articolo, rivolgersi al fornitore del software antivirus per istruzioni o per una versione aggiornata del software antivirus.
> - Questo articolo contiene informazioni che illustrano come ridurre le impostazioni di sicurezza o come disattivare temporaneamente le funzionalità di sicurezza in un computer. È possibile apportare queste modifiche per comprendere la natura di un problema specifico. Prima di apportare queste modifiche, è consigliabile valutare i rischi associati all'implementazione di questa soluzione alternativa nell'ambiente specifico.

## <a name="possible-symptoms"></a>Possibili sintomi 

La protezione in tempo reale dell'antivirus può causare molti problemi nei server del sito di Configuration Manager, nei sistemi del sito e nei client.

Di seguito è riportato un elenco non completo dei possibili sintomi:

- I componenti di sistema del sito remoto non sono installati. SiteComp.log, Distmgr.log, hman.log o altri file di log di Configuration Manager possono contenere errori, ad esempio l'errore 80070005.
- Non è possibile installare i client di Configuration Manager usando push client.
- Le informazioni di inventario client sono inesatte, mancanti o non aggiornate.
- I backlog si verificano nelle cartelle *Install_Directory*\Programmi\Microsoft Configuration Manager\Inboxes.
- Software Center non è popolato dal software distribuito nei sistemi client o non viene avviato. Inoltre, il file CCMRepair.log può contenere errori simili all'esempio seguente:

  > Verifica del database non riuscita con risultato: 0x80004005 ma è stato possibile aprire il database: C:\Windows\CCM\filename.sdf ignorando il ripristino del database.

- Non è possibile installare il software distribuito ai client.
- I dati di conformità per le distribuzioni software non sono accurati.

## <a name="exclusions"></a>Esclusioni

Per evitare questi problemi, è consigliabile aggiungere le esclusioni di protezione in tempo reale seguenti:

### <a name="default-installation-folders"></a>Cartelle di installazione predefinite

|  |  |
| - | - |
|*Cartella di installazione di ConfigMgr*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*Cartella di installazione di MP*  |%ProgramFiles%\SMS_CCM  |  
|*Cartella di installazione client*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Esclusioni di cartelle per i server del sito

- *Cartella di installazione di ConfigMgr*\Inboxes
- *Cartella di installazione di ConfigMgr*\Logs
- *Cartella di installazione di ConfigMgr*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>Esclusioni di cartelle per i sistemi del sito

- Punti di gestione
  - *Cartella di installazione di MP*\ServiceData
  - Una delle cartelle seguenti:
    - *Cartella di installazione di ConfigMgr*\MP\OUTBOXES
    - *Unità di installazione*\SMS\MP\OUTBOXES
- Punti di distribuzione
  - *Cartella di installazione client*\ServiceData
  - *ContentLib_Drive*\SMS_DP$
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- Server di database del sito
  - [Come scegliere il software antivirus da eseguire nei computer che eseguono SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Esclusioni di cartelle per i client

- *Cartella di installazione client*\\\*.sdf
- *Cartella di installazione client*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Cartella di installazione client*\Logs

### <a name="file-exclusions-for-mps"></a>Esclusioni di file per MP

- POL00000.pol in
  - *Cartella di installazione di MP*\PolReqStaging

### <a name="process-exclusions"></a>Esclusioni dei processi

Le esclusioni dei processi sono necessarie solo se i programmi antivirus aggressivi considerano i file di programma di Configuration Manager (file con estensione exe) come processi ad alto rischio.

- *Cartella di installazione di ConfigMgr*\bin\64\Smsexec.exe
- Uno dei processi seguenti:
  - *Cartella di installazione client*\Ccmexec.exe
  - *Cartella di installazione di MP*\Ccmexec.exe
- *Cartella di installazione client*\CmRcService.exe (lato client)
- *Cartella di installazione di ConfigMgr*\bin\64\Sitecomp.exe
- *Cartella di installazione di ConfigMgr*\bin\64\Smswriter.exe
- *Cartella di installazione di ConfigMgr*\bin\64\Smssqlbkup.exe o SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *Cartella di installazione di ConfigMgr*\bin\64\Cmupdate.exe
- *Cartella di installazione client*\Ccmrepair.exe (lato client)
- %*windir*%\CCMSetup\Ccmsetup.exe (lato client)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle esclusioni dell'antivirus, vedere gli articoli seguenti:

[Configuration Manager Current Branch Antivirus Exclusions - System Center Premier Field Engineer Blog](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/) (Esclusioni dell'antivirus per Configuration Manager Current Branch - Blog System Center Premier Field Engineer)

[Updated System Center 2012 Configuration Manager Antivirus Exclusions with more details on OSD and Boot Images](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/) (Esclusioni dell'antivirus per System Center 2012 Configuration Manager aggiornate con altri dettagli su immagini OSD e di avvio)

[Come scegliere il software antivirus da eseguire nei computer che eseguono SQL Server](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Raccomandazioni per la ricerca di virus per computer aziendali che eseguono versioni attualmente supportate di Windows](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
