---
title: Informativa sulla privacy per i cmdlet
titleSuffix: Configuration Manager
description: Informazioni su come Microsoft raccoglie e usa i dati correlati ai cmdlet di Configuration Manager
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695749"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Informativa sulla privacy per la libreria di cmdlet di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questa informativa sulla privacy riguarda le funzionalità di Configuration Manager Cmdlet Library.  

## <a name="usage-data"></a>Dati di utilizzo  

#### <a name="what-this-feature-does"></a>Descrizione della funzionalità:

La libreria di cmdlet di Configuration Manager consente di usare i cmdlet e gli script di Windows PowerShell per gestire una gerarchia di Configuration Manager. Oltre a raccogliere informazioni sul modo in cui vengono usati i cmdlet della libreria per individuare le tendenze e i modelli di utilizzo, la libreria di cmdlet raccoglie anche i tipi e i numeri degli errori ricevuti durante l'uso dei cmdlet.  

#### <a name="information-collected-processed-or-transmitted"></a>Informazioni raccolte, elaborate o trasmesse
   
I dati di utilizzo raccolti includono quelli sull'avvio, sull'arresto e sull'interruzione di cmdlet e sull'esecuzione di metriche di attività e di cmdlet deprecati per le operazioni dei provider SMS correlate ai cmdlet. Si tratta di informazioni che non consentono di identificare l'utente. Le informazioni sugli errori raccolte includono gli errori restituiti dai cmdlet e i dettagli relativi agli errori delle eccezioni. Alcune segnalazioni con i dettagli sugli errori possono inavvertitamente includere identificatori individuali, come il numero di serie di un dispositivo connesso al computer. La libreria dei cmdlet filtra e rende anonime le informazioni nelle segnalazioni errori, al fine di rimuovere gli identificatori individuali prima della trasmissione a Microsoft.  

#### <a name="use-of-information"></a>Utilizzo delle informazioni
   
Microsoft usa queste informazioni per migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi offerti.  

#### <a name="choicecontrol"></a>Scelta e controllo   

La funzionalità Dati di Utilizzo è abilitata per impostazione predefinita. La libreria di cmdlet di Configuration Manager ha due chiavi del Registro di sistema che controllano questa funzionalità.  

 Per rifiutare esplicitamente e completamente, impostare questi due valori di chiave del Registro di sistema, relativi a ognuno dei provider Event Tracing for Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (consente di rifiutare esplicitamente la funzionalità Dati di utilizzo per il provider dell'unità)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (consente di rifiutare esplicitamente la funzionalità Dati di utilizzo per i cmdlet)  

  Le modifiche alle impostazioni relative ai dati di utilizzo sono specifiche per il computer in cui vengono apportate.  


## <a name="next-steps"></a>Passaggi successivi

[Documentazione della libreria di cmdlet di Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
