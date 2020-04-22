---
title: Supporto tecnico OneTrace (anteprima)
titleSuffix: Configuration Manager
description: OneTrace è un nuovo visualizzatore log disponibile nel Supporto tecnico che include miglioramenti rispetto a CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707449"
---
# <a name="support-center-onetrace-preview"></a>Supporto tecnico OneTrace (anteprima)

<!--3555962-->

A partire dalla versione 1906, OneTrace è un nuovo visualizzatore log incluso nel Supporto tecnico. Funziona in modo analogo a CMTrace, con i miglioramenti seguenti:

- Una visualizzazione a schede
- Finestre ancorabili
- Funzionalità di ricerca migliorate
- Possibilità di abilitare i filtri senza uscire dalla visualizzazione del log
- Hint della barra di scorrimento per identificare rapidamente i cluster di errori
- Apertura veloce del log per i file di grandi dimensioni

[![Screenshot del visualizzatore log OneTrace](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace funziona con molti tipi di file di log, ad esempio:

- Log client di Configuration Manager
- Log del server di Configuration Manager
- Messaggi di stato
- File di log ETW di Windows Update in Windows 10
- File di log di Windows Update in Windows 7 e Windows 8.1

## <a name="prerequisites"></a>Prerequisiti

- .NET Framework versione 4.6 o successiva

## <a name="install"></a>Installazione

OneTrace viene installato con il Supporto tecnico. Individuare il programma di installazione di Support Center nel server del sito nel percorso seguente: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Per impostazione predefinita, l'applicazione OneTrace viene installata in `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!Note]  
> Support Center e OneTrace usano Windows Presentation Foundation (WPF). Questo componente non è disponibile in Windows PE. Continuare a usare CMTrace nelle immagini d'avvio con le distribuzioni di sequenze di attività.  

## <a name="log-groups"></a>Log groups

<!--5559993-->

A partire dalla versione 2002, OneTrace supporta gruppi di log personalizzabili, in modo analogo alla funzionalità in Support Center. I gruppi di log consentono di aprire tutti i file di log per un singolo scenario. OneTrace include attualmente gruppi per gli scenari seguenti:

- Gestione delle applicazioni
- Impostazioni di conformità (definite anche gestione configurazione desiderata)
- Aggiornamenti software

Per visualizzare i gruppi di log, andare al menu **Visualizza** visualizzazione e selezionare **Gruppi di log**.

![Screenshot del gruppo di log di OneTrace per la gestione delle applicazioni](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Personalizzare i gruppi di log

È possibile personalizzare questi gruppi modificando il codice XML di configurazione, che per impostazione predefinita si trova nel percorso seguente: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`.

L'esempio seguente è una parte del file di configurazione predefinito:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

La proprietà `GroupType` accetta i valori seguenti:

- `0`: sconosciuto o altro
- `1`: Log client di Configuration Manager
- `2`: Log del server di Configuration Manager

La proprietà `GroupFilePath` può includere un percorso esplicito per i file di log. Se è vuoto, OneTrace si basa sulla configurazione del Registro di sistema per il tipo di gruppo. Ad esempio, se si imposta `GroupType=1`, per impostazione predefinita OneTrace cercherà automaticamente i log del gruppo in `C:\Windows\CCM\Logs`. In questo esempio non è necessario specificare `GroupFilePath`.

## <a name="see-also"></a>Vedere anche

- [Visualizzatore log del Supporto tecnico](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
