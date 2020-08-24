---
title: Criteri di conformità dei dispositivi iOS in Microsoft Intune - Azure | Microsoft Docs
description: È possibile iniziare a usare criteri di conformità, incluse le impostazioni dei criteri di conformità e i criteri di conformità dispositivo per Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bb3397432f1c171418ea99510cb04f1bdefc639
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252793"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Usare i criteri di conformità per configurare regole per i dispositivi gestiti con Intune

Le soluzioni di gestione di dispositivi mobili (MDM, Mobile Device Management) come Intune consentono di proteggere i dati dell'organizzazione richiedendo agli utenti e ai dispositivi di soddisfare alcuni requisiti. In Intune questa funzionalità è definita *criteri di conformità*.

Criteri di conformità in Intune:

- Consentono di definire le regole e le impostazioni che gli utenti e i dispositivi devono soddisfare per adeguarsi ai criteri stessi.
- Includono azioni applicabili ai dispositivi non conformi. Le azioni per la non conformità possono inviare agli utenti avvisi relativi alle condizioni di non conformità e proteggere i dati nei dispositivi non conformi.
- Possono essere [combinati con l'accesso condizionale](#integrate-with-conditional-access), che può quindi bloccare utenti e dispositivi che non rispettano le regole.

I criteri di conformità in Intune sono costituiti da due parti:

- **Impostazioni dei criteri di conformità** - Impostazioni a livello di tenant analoghe a criteri di conformità predefiniti ricevuti da ogni dispositivo. Le impostazioni dei criteri di conformità definiscono una baseline per il funzionamento dei criteri di conformità nell'ambiente di Intune, ad esempio per stabilire se i dispositivi che non hanno ricevuto alcun criterio di conformità del dispositivo sono conformi o non conformi.

- **Criteri di conformità del dispositivo** - Regole specifiche della piattaforma da configurare e distribuire a gruppi di utenti o dispositivi.  Queste regole definiscono i requisiti per i dispositivi, ad esempio i sistemi operativi minimi o l'uso della crittografia del disco. Per essere considerati conformi, i dispositivi devono soddisfare queste regole.

Analogamente ad altri criteri di Intune, le valutazioni dei criteri di conformità per un dispositivo dipendono dal momento in cui il dispositivo esegue la sincronizzazione con Intune e dai [cicli di aggiornamento dei criteri e del profilo](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="compliance-policy-settings"></a>Impostazioni dei criteri di conformità

Le *impostazioni dei criteri di conformità* sono impostazioni a livello di tenant che consentono di determinare la modalità di interazione del servizio di conformità di Intune con i dispositivi dell'utente. Queste impostazioni sono distinte dalle impostazioni configurate in un criterio di conformità del dispositivo.

Per gestire le impostazioni dei criteri di conformità, accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e passare a **Sicurezza degli endpoint** > **Conformità del dispositivo** > **Impostazioni dei criteri di conformità**.

Le impostazioni dei criteri di conformità includono le impostazioni seguenti:

- **Contrassegna i dispositivi senza criteri di conformità assegnati come**

  Questa impostazione consente di determinare il modo in cui Intune gestisce i dispositivi a cui non è stato assegnato alcun criterio di conformità del dispositivo. Questa impostazione ha due valori:
  - **Conforme** (*impostazione predefinita*): questa funzionalità di sicurezza è disattivata. I dispositivi a cui non viene inviato alcun criterio di conformità del dispositivo vengono considerati *conformi*.
  - **Non conforme**: questa funzionalità di sicurezza è attivata. I dispositivi che non hanno ricevuto alcun criterio di conformità del dispositivo vengono considerati non conformi.

  Se si usa l'accesso condizionale con i criteri di conformità del dispositivo, è consigliabile modificare questa impostazione in **Non conforme** per assicurare che solo i dispositivi confermati come conformi possano accedere alle risorse.

  Se un utente finale non è conforme perché a tale utente non è stato assegnato alcun criterio, nell'[app Portale aziendale](../apps/company-portal-app.md) verrà mostrato il messaggio Non sono stati assegnati criteri di conformità.

- **Rilevamento ottimizzato per jailbreak** (*applicabile solo a iOS/iPadOS*)

  Questa impostazione funziona solo con i dispositivi a cui è assegnato un criterio di conformità del dispositivo che blocca i dispositivi jailbroken.  Vedere le impostazioni di [Integrità dispositivi](compliance-policy-create-ios.md#device-health) per iOS/iPadOS.

  Questa impostazione ha due valori:

  - **Disabilitato** (*impostazione predefinita*): questa funzionalità di sicurezza è disattivata. Questa impostazione non ha alcun effetto nei dispositivi che ricevono un criterio di conformità del dispositivo che blocca i dispositivi jailbroken.
  - **Attivata**: questa funzionalità di sicurezza è attivata. I dispositivi che ricevono un criterio di conformità del dispositivo per bloccare i dispositivi jailbroken usano l'opzione Rilevamento ottimizzato per jailbreak.

  Quando questa impostazione è abilitata in un dispositivo iOS/iPadOS applicabile, il dispositivo:

  - Abilita i servizi di posizione a livello di sistema operativo.
  - Consente sempre al Portale aziendale di usare i servizi di posizione.
  - Usa i servizi di posizione per attivare il rilevamento del jailbreak con maggiore frequenza in background. I dati relativi alla posizione dell'utente non vengono archiviati da Intune.

  La funzionalità Rilevamento ottimizzato per jailbreak esegue una valutazione quando:

  - L'app Portale aziendale viene aperta.
  - Il dispositivo si sposta fisicamente per una distanza significativa, che corrisponde circa ad almeno 500 metri. Intune non è in grado di garantire che ogni modifica significativa della posizione generi un controllo di rilevamento del jailbreak, poiché questo controllo dipende dalla connessione di rete di un dispositivo usata al momento.

  In iOS 13 e versioni successive, questa funzionalità richiede agli utenti di selezionare *Consenti sempre* ogni volta che il dispositivo richiede di continuare a consentire al Portale aziendale di usare la posizione in background. Se gli utenti non consentono sempre l'accesso alla posizione e hanno un criterio configurato con questa impostazione, il dispositivo verrà contrassegnato come non conforme.

- **Periodo di validità dello stato di conformità (giorni)**

  Specificare un periodo in cui i dispositivi devono inviare report correlati a tutti i criteri di conformità ricevuti. Se un dispositivo non segnala il rispettivo stato di conformità per un criterio prima della scadenza del periodo di validità, il dispositivo verrà considerato come non conforme.

  Per impostazione predefinita, questo periodo è di 30 giorni. È possibile configurare un periodo compreso tra 1 e 120 giorni.

  È possibile visualizzare i dettagli sulla conformità del dispositivo con l'impostazione del periodo di validità. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e passare a **Dispositivi** > **Monitoraggio** > **Conformità dell'impostazione**. Il nome dell'impostazione è **Attivo** nella colonna *Impostazione*.  Per altre informazioni su questa visualizzazione e sulle visualizzazioni correlate dello stato di conformità, vedere [Monitorare la conformità del dispositivo](compliance-policy-monitor.md).

## <a name="device-compliance-policies"></a>Criteri di conformità dei dispositivi

Criteri di conformità dei dispositivi in Intune:

- Consentono di definire le regole e le impostazioni che gli utenti e i dispositivi gestiti devono soddisfare per adeguarsi ai criteri stessi. Gli esempi di regole includono l'obbligo di esecuzione di una versione minima del sistema operativo per i dispositivi, l'esclusione di dispositivi jailbroken e rooted e il rispetto di un *livello di minaccia* in base a quanto specificato dal software di gestione delle minacce integrato con Intune.
- Supportano azioni applicabili ai dispositivi che non rispettano le regole di conformità. Gli esempi di azioni includono il blocco remoto o l'invio di messaggi di posta elettronica relativi allo stato all'utente del dispositivo per consentire la correzione dei problemi.
- Vengono distribuiti a utenti in gruppi di utenti o a dispositivi in gruppi di dispositivi. Quando un criterio di conformità viene distribuito a un utente, la conformità viene controllata su tutti i dispositivi dell'utente. L'uso di gruppi di dispositivi in questo scenario è utile per la creazione di report di conformità.

Se si usa l'accesso condizionale, i criteri di accesso condizionale possono usare i risultati della conformità del dispositivo per bloccare l'accesso alle risorse dai dispositivi non conformi.

Le impostazioni disponibili che è possibile specificare in un criterio di conformità del dispositivo dipendono dal tipo di piattaforma selezionato durante la creazione di un criterio. Diverse piattaforme per dispositivi supportano diverse impostazioni e ogni tipo di piattaforma richiede un criterio separato.  

Gli argomenti seguenti sono collegati ad articoli dedicati per diversi aspetti del criterio di configurazione.

- [**Azioni per la non conformità**](actions-for-noncompliance.md) - Ogni criterio di conformità del dispositivo include una o più azioni da eseguire in caso di mancata conformità. Queste azioni sono regole che vengono applicate ai dispositivi che non soddisfano le condizioni configurate nel criterio.

  Per impostazione predefinita, ogni criterio di conformità del dispositivo include l'azione per contrassegnare un dispositivo come non conforme se non rispetta una regola del criterio. Il criterio applica quindi al dispositivo eventuali azioni aggiuntive configurate per la non conformità, in base alle pianificazioni definite per queste azioni.

  Le azioni per la non conformità possono consentire di avvisare gli utenti quando il rispettivo dispositivo non è conforme o di proteggere i dati che potrebbero trovarsi in un dispositivo. Gli esempi di azioni includono:

  - **Invio di avvisi tramite posta elettronica** a utenti e gruppi con dettagli sul dispositivo non conforme. È possibile configurare il criterio per l'invio immediato di un messaggio di posta elettronica quando un dispositivo viene contrassegnato come non conforme e quindi per l'invio periodico fino a quando il dispositivo non diventa conforme.
  - **Blocco remoto dei dispositivi** che sono stati non conformi per un determinato periodo.
  - **Ritiro di dispositivi** dopo che sono rimasti non conformi per un determinato periodo. Questa azione rimuove il dispositivo dalla gestione di Intune e rimuove tutti i dati aziendali dal dispositivo.

- [**Configurazione dei percorsi di rete**](use-network-locations.md) - Questa impostazione è supportata dai dispositivi Android e consente di configurare i *percorsi di rete* e quindi di usare tali percorsi come regola di conformità del dispositivo. Questo tipo di regola può contrassegnare un dispositivo come non conforme quando è all'esterno o esce da una rete specificata. Per specificare una regola di posizione, è prima di tutto necessario configurare i percorsi di rete.

- [**Creazione di un criterio**](create-compliance-policy.md) - Le informazioni incluse in questo articolo consentono di esaminare i prerequisiti, visualizzare i dettagli relativi alle opzioni per la configurazione delle regole, specificare le azioni per la non conformità e assegnare il criterio a gruppi. Questo articolo include anche informazioni sul tempi di aggiornamento dei criteri.

  Vedere le impostazioni di conformità del dispositivo per le diverse piattaforme per dispositivi:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows 8.1 e versioni successive](compliance-policy-create-windows-8-1.md)
  - [Windows 10 e versioni successive](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Monitorare lo stato di conformità

Intune include un dashboard di conformità del dispositivo da usare per monitorare lo stato di conformità dei dispositivi e per visualizzare i dettagli di criteri e dispositivi per ottenere altre informazioni. Per altre informazioni su questo dashboard, vedere [Monitorare la conformità del dispositivo](compliance-policy-monitor.md).

## <a name="integrate-with-conditional-access"></a>Integrazione con l'accesso condizionale

Quando si usa l'accesso condizionale, è possibile configurare i criteri di accesso condizionale per l'uso dei risultati dei criteri di conformità del dispositivo per determinare quali dispositivi possono accedere alle risorse dell'organizzazione. Questo controllo di accesso è aggiuntivo e separato dalle azioni per la non conformità incluse nei criteri di conformità del dispositivo.

Quando un dispositivo si registra in Intune, viene registrato in Azure AD. Lo stato di conformità per i dispositivi viene segnalato ad Azure AD. Se i criteri di accesso condizionale includono controlli di accesso impostati su *Richiedi che i dispositivi siano contrassegnati come conformi*, l'accesso condizionale userà tale stato di conformità per determinare se concedere o bloccare l'accesso alla posta elettronica e ad altre risorse dell'organizzazione.

Se si prevede di usare lo stato di conformità del dispositivo con criteri di accesso condizionale, esaminare il modo in cui il tenant ha configurato l'opzione *Contrassegna i dispositivi senza criteri di conformità assegnati come*, che viene gestita in [Impostazioni dei criteri di conformità](#compliance-policy-settings).

Per altre informazioni sull'uso dell'accesso condizionale con i criteri di conformità del dispositivo, vedere [Accesso condizionale basato sul dispositivo](conditional-access-intune-common-ways-use.md#device-based-conditional-access).

Per altre informazioni sull'accesso condizionale, vedere la documentazione di Azure AD:

- [Che cos'è l'accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Che cos’è l'identità del dispositivo](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Informazioni di riferimento per la mancata conformità e l'accesso condizionale sulle diverse piattaforme

La tabella seguente descrive come vengono gestite le impostazioni non conformi quando si usano criteri di conformità con criteri di accesso condizionale.

- **Con correzione**: il sistema operativo del dispositivo impone la conformità. ad esempio, l'utente è obbligato a impostare un PIN.

- **In quarantena**: il sistema operativo del dispositivo non impone la conformità. Ad esempio, l'utente di dispositivi Android e Android Enterprise non è obbligato a crittografare il dispositivo. Se il dispositivo non è conforme, vengono eseguite le azioni seguenti:
  - Se all'utente si applica un criterio di accesso condizionale, il dispositivo viene bloccato.
  - L'app Portale aziendale segnala all'utente eventuali problemi di conformità.

---------------------------

|**Impostazione di criteri**| **Platform** |
| --- | ----|
| **Configurazione di PIN o password** | - **Android 4.0 e versioni successive**: In quarantena<br>- **Samsung KNOX Standard 4.0 e versioni successive**: In quarantena<br>- **Android Enterprise**: In quarantena  <br>  <br>- **iOS 8.0 e versioni successive**: Corretto<br>- **macOS 10.11 e versioni successive**: Corretto  <br>  <br>- **Windows 8.1 e versioni successive**: Corretto|
| **Crittografia dispositivo** | - **Android 4.0 e versioni successive**: In quarantena<br>- **Samsung KNOX Standard 4.0 e versioni successive**: In quarantena<br>- **Android Enterprise**: In quarantena<br><br>- **iOS 8.0 e versioni successive**: Corretto (impostando il PIN)<br>- **macOS 10.11 e versioni successive**: Corretto (impostando il PIN)<br><br>- **Windows 8.1 e versioni successive**: Non applicabile|
| **Dispositivo jailbroken o rooted** | - **Android 4.0 e versioni successive**: In quarantena (non è un'impostazione)<br>- **Samsung KNOX Standard 4.0 e versioni successive**: In quarantena (non è un'impostazione)<br>- **Android Enterprise**: In quarantena (non è un'impostazione)<br><br>- **iOS 8.0 e versioni successive**: In quarantena (non è un'impostazione)<br>- **macOS 10.11 e versioni successive**: Non applicabile<br><br>- **Windows 8.1 e versioni successive**: Non applicabile |
| **Profilo di posta elettronica** | - **Android 4.0 e versioni successive**: Non applicabile<br>- **Samsung KNOX Standard 4.0 e versioni successive**: Non applicabile<br>- **Android Enterprise**: Non applicabile<br><br>- **iOS 8.0 e versioni successive**: In quarantena<br>- **macOS 10.11 e versioni successive**: In quarantena<br><br>- **Windows 8.1 e versioni successive**: Non applicabile |
| **Versione minima del sistema operativo** | - **Android 4.0 e versioni successive**: In quarantena<br>- **Samsung KNOX Standard 4.0 e versioni successive**: In quarantena<br>- **Android Enterprise**: In quarantena<br><br>- **iOS 8.0 e versioni successive**: In quarantena<br>- **macOS 10.11 e versioni successive**: In quarantena<br><br>- **Windows 8.1 e versioni successive**: In quarantena|
| **Versione massima del sistema operativo** | - **Android 4.0 e versioni successive**: In quarantena<br>- **Samsung KNOX Standard 4.0 e versioni successive**: In quarantena<br>- **Android Enterprise**: In quarantena<br><br>- **iOS 8.0 e versioni successive**: In quarantena<br>- **macOS 10.11 e versioni successive**: In quarantena<br><br>- **Windows 8.1 e versioni successive**: In quarantena |
| **Attestazione dell'integrità di Windows** | - **Android 4.0 e versioni successive**: Non applicabile<br>- **Samsung KNOX Standard 4.0 e versioni successive**: Non applicabile<br>- **Android Enterprise**: Non applicabile<br><br>- **iOS 8.0 e versioni successive**: Non applicabile<br>- **macOS 10.11 e versioni successive**: Non applicabile<br><br>- **Windows 10**: In quarantena<br>- **Windows 8.1 e versioni successive**: In quarantena |

---------------------------

## <a name="next-steps"></a>Passaggi successivi

- [Configurare le posizioni](../protect/use-network-locations.md) da usare con i dispositivi Android
- [Creare e distribuire criteri](../protect/create-compliance-policy.md) ed esaminare i prerequisiti
- [Monitorare la conformità dei dispositivi](../protect/compliance-policy-monitor.md)
- [Domande e problemi comuni e soluzioni per i criteri e i profili dei dispositivi in Microsoft Intune](../configuration/device-profile-troubleshoot.md)
- Per informazioni sulle entità del criterio Data warehouse di Intune, vedere [Informazioni di riferimento per le entità della categoria Policy](../developer/reports-ref-policy.md)
