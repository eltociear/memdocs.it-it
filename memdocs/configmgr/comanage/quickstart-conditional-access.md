---
title: Accesso condizionale con la co-gestione
titleSuffix: Configuration Manager
description: Controllare l'accesso utente alle risorse dell'organizzazione in base alle regole di conformità da Intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691259"
---
# <a name="conditional-access-with-co-management"></a>Accesso condizionale con la co-gestione

L'accesso condizionale assicura che solo gli utenti attendibili possano accedere alle risorse dell'organizzazione in dispositivi attendibili usando app attendibili. Questo scenario viene realizzato da zero nel cloud. Sia che si voglia gestire i dispositivi con Intune o estendere la distribuzione di Configuration Manager con la co-gestione, il funzionamento è lo stesso.

Nel video seguente il Senior Program Manager Joey Glocke e il Product Marketing Manager Locky Ainley trattano e illustrano l'accesso condizionale con la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Con la co-gestione, Intune valuta tutti i dispositivi nella rete per determinare il grado di attendibilità. La valutazione viene eseguita nei due modi seguenti:

1. Intune si assicura che un dispositivo o un'app sia gestito e configurato in modo sicuro. Questa verifica dipende dalla modalità di impostazione dei criteri di conformità dell'organizzazione. Ad esempio, si assicura che la crittografia sia abilitata in tutti i dispositivi e che i dispositivi non siano jailbroken.  

    - Questa valutazione avviene prima di una violazione della sicurezza ed è basata sulla configurazione  

    - Per i dispositivi con co-gestione, Configuration Manager esegue anche una valutazione basata sulla configurazione. Ad esempio, gli aggiornamenti richiesti o la conformità delle app. Intune combina questi controlli con la propria valutazione.  

2. Intune rileva gli eventi imprevisti di sicurezza attivi in un dispositivo. Usa la sicurezza intelligente di [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (in precedenza Windows Defender ATP) e altri [provider di Mobile Threat Defense](https://www.lookout.com/about/partners/microsoft). Questi partner eseguono analisi del comportamento in modo continuativo sui dispositivi. Queste analisi rilevano gli eventi imprevisti attivi e quindi passano queste informazioni a Intune per la valutazione della conformità in tempo reale.  

    - Questa valutazione avviene dopo una violazione della sicurezza ed è basata sugli eventi imprevisti  

Il vicepresidente di Microsoft Brad Anderson illustra l'accesso condizionale in modo approfondito con demo live durante il suo intervento a Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

L'accesso condizionale offre anche una posizione centralizzata per visualizzare l'integrità di tutti i dispositivi connessi alla rete. Si ottengono i vantaggi della scalabilità del cloud, particolarmente preziosi per i test delle istanze di produzione di Configuration Manager.


## <a name="benefits"></a>Vantaggi

Per tutti i team IT la sicurezza della rete è di primaria importanza. È fondamentale assicurarsi che ogni dispositivo soddisfi i requisiti aziendali e di sicurezza prima dell'accesso alla rete. Grazie all'accesso condizionale, è possibile determinare i fattori seguenti: 
- Se tutti i dispositivi sono crittografati  
- Se è installato malware  
- Se le impostazioni sono aggiornate  
- Se il dispositivo è jailbroken o rooted  

L'accesso condizionale combina il controllo granulare dei dati dell'organizzazione con un'esperienza utente in grado di ottimizzare la produttività su qualsiasi dispositivo da qualsiasi posizione.

Il video seguente illustra come è possibile integrare [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) in scenari comuni:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Con la co-gestione, Intune può incorporare le responsabilità di Configuration Manager per valutare la conformità agli standard di sicurezza degli aggiornamenti o delle app richiesti. Questo comportamento è importante per qualsiasi organizzazione IT che vuole continuare a usare Configuration Manager per la gestione complessa di app e patch.

L'accesso condizionale è anche un aspetto essenziale dello sviluppo dell'[architettura di rete Zero Trust](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/). Con l'accesso condizionale i controlli di accesso per i dispositivi conformi offrono una copertura per i livelli fondamentali della rete Zero Trust. Questa funzionalità è una parte importante del modo in cui verranno protette le organizzazioni in futuro.

Per altre informazioni, vedere il post di blog [Enhancing conditional access with machine-risk data from Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559) (Ottimizzazione dell'accesso condizionale con i dati sui rischi dei computer da Microsoft Defender Advanced Threat Protection).



## <a name="case-studies"></a>Case study

La società di consulenza IT Wipro usa l'accesso condizionale per proteggere e gestire i dispositivi usati da tutti i 91.000 dipendenti. In un recente case study, il vicepresidente del settore IT di Wipro ha affermato:

> *L'implementazione dell'accesso condizionale è una grande conquista per Wipro. Tutti i nostri dipendenti hanno ora accesso mobile alle informazioni su richiesta.* 
> *Abbiamo migliorato la sicurezza e la produttività dei dipendenti. I 91.000 dipendenti possono ora usufruire dell'accesso con sicurezza elevata a più di 100 app da qualsiasi dispositivo, ovunque.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Altri esempi includono: 

- Nestlé, che usa l'accesso condizionale basato su app per oltre 150.000 dipendenti  

- La società produttrice di software di automazione Cadence, che può ora essere certa che "solo i dispositivi gestiti abbiano accesso ad app di Office 365 come Teams e alla rete Intranet aziendale." Possono anche offrire alla forza lavoro "accesso più sicuro ad altre app basate sul cloud, ad esempio Workday e Salesforce." Per altre informazioni sull'esperienza di Cadence con Intune, vedere [Cadence increases the pace of business with mobile collaboration tools in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365) (Cadence aumenta la produttività con gli strumenti per la collaborazione per dispositivi mobili in Microsoft 365).

Intune supporta anche l'integrazione completa con prodotti dei partner come Cisco ISE, Aruba Clear Pass e Citrix NetScaler. Con la collaborazione di questi partner è possibile usare i controlli di accesso basati sulla registrazione in Intune e lo stato di conformità del dispositivo su queste altre piattaforme.

Per altre informazioni, vedere i video seguenti:
- [Brad Anderson demos conditional access in detail](https://youtu.be/8321obNofgM?t=547) (Brain Anderson presenta in dettaglio l'accesso condizionale)  
- [Additional detail from Endpoint Zone 1805](https://youtu.be/f-ILlEuBFZg?t=196) (Altri dettagli da Endpoint Zone 1805)  


## <a name="value-proposition"></a>Proposta di valore

Con l'accesso condizionale e l'integrazione di ATP si rafforza un componente fondamentale di tutte le organizzazioni IT: la protezione dell'accesso al cloud.

In più del 63% di tutte le violazioni della sicurezza dei dati, gli utenti malintenzionati ottengono l'accesso alla rete dell'organizzazione tramite credenziali utente deboli, impostate come predefinite o rubate. Poiché l'accesso condizionale è incentrato sulla protezione dell'identità dell'utente, limita il furto di credenziali. L'accesso condizionale gestisce e protegge le identità con privilegi o senza privilegi. Non esiste un modo migliore per proteggere i dispositivi e i dati al loro interno.

Dato che l'accesso condizionale è un componente essenziale di Enterprise Mobility + Security (EMS), non sono richieste configurazioni o un'architettura specifica in locale. Con Intune e Azure Active Directory (Azure AD) è possibile configurare rapidamente l'accesso condizionale nel cloud. Se attualmente si usa Configuration Manager, è possibile estendere facilmente l'ambiente al cloud con la co-gestione e iniziare subito a usarlo.

Per altre informazioni sull'integrazione di ATP, vedere il post di blog [Microsoft Defender ATP device risk score exposes new cyberattack, drives Conditional access to protect networks](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/) (Il punteggio di rischio dei dispositivi Microsoft Defender ATP espone al rischio di nuovi attacchi cibernetici e promuove l'uso dell'accesso condizionale per proteggere le reti). In questo post viene descritto in dettaglio come un gruppo di hacker avanzati ha usato strumenti mai visti in precedenza. L'attacco è stato rilevato e bloccato dal cloud Microsoft perché gli utenti designati usavano l'accesso condizionale. L'intrusione ha attivato i criteri di accesso condizionale basati sul rischio del dispositivo. Anche se l'autore dell'attacco era già riuscito a penetrare la rete, ai computer interessati è stato automaticamente impedito l'accesso ai servizi e ai dati dell'organizzazione gestiti da Azure AD.



## <a name="configure"></a>Configura

L'accesso condizionale è facile da usare quando si [abilita la co-gestione](how-to-enable.md). È richiesto lo spostamento del carico di lavoro **Criteri di conformità** in Intune. Per altre informazioni, vedere [Come passare i carichi di lavoro di Configuration Manager a Intune](how-to-switch-workloads.md). 

Per altre informazioni sull'uso dell'accesso condizionale, vedere gli articoli seguenti: 

- [Che cos'è l'accesso condizionale in Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Criteri di conformità dei dispositivi in Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Accesso condizionale basato su app con Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Le funzionalità di accesso condizionale diventano disponibili immediatamente per i dispositivi aggiunti ad Azure AD ibrido. Queste funzionalità includono l'autenticazione a più fattori e il controllo di accesso per l'aggiunta ad Azure AD join ibrido. Questo comportamento deriva dal fatto che sono basate sulle proprietà di Azure AD. Per sfruttare la valutazione basata sulla configurazione di Intune e Configuration Manager, abilitare la co-gestione. Questa configurazione consente di usufruire del controllo di accesso direttamente da Intune per i dispositivi conformi. Offre inoltre la funzionalità di valutazione dei criteri di conformità di Intune.  

