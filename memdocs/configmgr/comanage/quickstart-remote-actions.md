---
title: Azioni remote con la co-gestione
titleSuffix: Configuration Manager
description: Eseguire azioni remote da Intune per i dispositivi con co-gestione
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075320"
---
# <a name="remote-actions-with-co-management"></a>Azioni remote con la co-gestione

È necessario assicurarsi che tutti i dispositivi gestiti siano raggiungibili, indipendentemente da dove si trovano, ogni volta che si connettono. È anche necessario fornire a ogni utente le informazioni necessarie per rimanere produttivi, pur continuando a proteggere app e dati. Con le azioni per i dispositivi supportate da Intune, è possibile gestire in modo remoto queste funzioni critiche.

Nel video seguente il Principal Program Manager Heidi Cheng e il Senior Program Manager Danny Guillory trattano e illustrano le azioni remote con la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Vantaggi

Le azioni remote per i dispositivi offrono controlli di gestione nel dispositivo senza interferenze con i dati personali. Queste azioni remote per i dispositivi consentono di: 
- Eliminare i dati aziendali in dispositivi persi o rubati  
- Rinominare un dispositivo  
- Riavviare un dispositivo  
- Esaminare l'inventario dei dispositivi  
- Controllare un dispositivo in remoto  
- Cancellano le app OEM preinstallate con un riavvio Fresh Start  
- Eseguire un ripristino delle impostazioni predefinite in qualsiasi dispositivo Windows 10  

Queste funzioni sono un modo semplice e importante per proteggere i dati aziendali archiviati in tali dispositivi, sia nella posta elettronica che in OneDrive.

Per altre informazioni su queste azioni, vedere [Azioni remote disponibili](#available-remote-actions). 



## <a name="case-studies"></a>Case study

La società di consulenza globale Avanade usa regolarmente le azioni remote per gestire i dispositivi usati dai 30.000 dipendenti. In un [post di blog recente](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), il CIO di Avanade si è così espresso:

> *Il grande vantaggio immediato ottenuto dalle funzionalità di Intune è la possibilità di reimpostare in modalità remota Windows in un computer. Questo è importante per i computer persi o rubati, che è un evento più comune per la nostra forza lavoro in mobilità.* 
> *Altrimenti, avremmo dovuto integrare e gestire questa funzionalità in un pacchetto di Configuration Manager personalizzato.*

Per altre informazioni su come usare queste azioni remote, vedere [Azioni del dispositivo disponibili](../../intune/remote-actions/device-management.md#available-device-actions).


## <a name="value-proposition"></a>Proposta di valore

Quando un dispositivo di Configuration Manager è con co-gestione, vengono aggiunte immediatamente queste funzioni non disponibili in modo nativo in Configuration Manager. A questo punto è possibile eseguire qualsiasi azione remota supportata da Intune. 

Con la co-gestione, i dispositivi di Configuration Manager sono ora esattamente come qualsiasi altro dispositivo gestito da Intune. Ad esempio, hanno una presenza completa nel cloud e sono raggiungibili a condizione che abbiano accesso a Internet. È possibile eseguire tutte queste azioni senza eseguire passaggi aggiuntivi oltre all'abilitazione della co-gestione.

Dato che il processo di registrazione automatica è trasparente all'utente, non vi è alcun impatto sulla produttività. L'utente non deve eseguire alcuna operazione.


### <a name="available-remote-actions"></a>Azioni remote disponibili

Usare queste azioni remote da Intune dopo aver [abilitato la co-gestione](how-to-enable.md) in Configuration Manager.

#### <a name="remove-devices"></a>Rimuovere i dispositivi
- **Ritira**: questa azione rimuove le app e i dati gestiti (se applicabile), le impostazioni e i profili di posta elettronica assegnati al dispositivo. Il dispositivo viene quindi rimosso dalla gestione di Intune. Questo processo viene eseguito alla successiva archiviazione del dispositivo, quando riceve l'azione remota di ritiro. La funzione Ritira lascia i dati personali dell'utente nel dispositivo.  

- **Cancella**: questa azione ripristina le impostazioni predefinite di un dispositivo. Se si sceglie l'opzione **Mantieni lo stato della registrazione e l'account utente**, i dati dell'utente vengano mantenuti. In caso contrario, l'unità viene cancellata in modo sicuro.  

- **Elimina**: se si vogliono rimuovere i dispositivi da Intune nel portale di Azure, eliminarli dal riquadro del dispositivo specifico. Alla successiva archiviazione del dispositivo verranno rimossi tutti i dati dell'organizzazione in esso archiviati.  

Per altre informazioni, vedere [Rimuovere i dispositivi con la cancellazione, la disattivazione o l'annullamento manuale della registrazione](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Cancellazione selettiva
<!--SCCMDocs issue 973-->
Quando si sceglie l'opzione **Cancellazione selettiva di app**, vengono rimossi i dati delle app aziendali senza rimuovere i dati personali. Usare questa azione quando viene segnalato lo smarrimento o il furto di un dispositivo. 

Per altre informazioni, vedere [Come cancellare solo i dati aziendali dalle app gestite da Intune](../../intune/apps/apps-selective-wipe.md.

#### <a name="sync"></a>Sincronizza
L'azione del dispositivo **Sincronizza** forza il dispositivo selezionato a eseguire immediatamente l'archiviazione in Intune. Quando un dispositivo esegue l'archiviazione, riceve immediatamente le eventuali azioni in sospeso o i criteri assegnati.

Questa funzionalità consente di convalidare i criteri assegnati e risolvere eventuali problemi immediatamente, senza attendere la successiva archiviazione pianificata.

Per altre informazioni, vedere [Sincronizzare i dispositivi per ottenere i criteri e le azioni più recenti con Intune](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Riavvia
L'azione del dispositivo **Riavvia** consente di riavviare il dispositivo scelto. Questa azione è utile quando è presente un riavvio in sospeso, ma l'utente non è disponibile per eseguire questa operazione.

Per altre informazioni, vedere [Riavviare i dispositivi in remoto con Intune](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Fresh Start
L'azione del dispositivo **Fresh Start** rimuove tutte le app installate in un dispositivo che esegue Windows 10, versione 1703 o successive. Fresh Start consente di rimuovere le app (OEM) preinstallate in genere fornite con un nuovo dispositivo.

Se si sceglie di non conservare i dati utente, viene ripristinato lo stato predefinito del dispositivo. Viene annullata la registrazione del dispositivo da Azure AD e MDM.

In presenza di standard predeterminati in merito alle app che devono essere presenti nel dispositivo, questa azione elimina quelle che non soddisfano i criteri specificati.

Per altre informazioni, vedere [Usare Fresh Start per ripristinare i dispositivi Windows 10 con Intune](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Controllo remoto
I dispositivi gestiti da Intune possono essere amministrati in remoto mediante [TeamViewer](https://www.teamviewer.com/). TeamViewer è un programma di terze parti acquistabile separatamente.

Per altre informazioni, vedere [Usare TeamViewer per l'amministrazione remota dei dispositivi di Intune](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Configura

Oltre al controllo remoto tramite TeamViewer, per iniziare a usare queste azioni remote per i dispositivi in Intune, non sono necessarie ulteriori impostazioni dopo aver [abilitato la co-gestione](how-to-enable.md).

Per altre informazioni sull'uso di TeamViewer per il controllo remoto, vedere [Usare TeamViewer per l'amministrazione remota dei dispositivi di Intune](../../intune/remote-actions/teamviewer-support.md).
