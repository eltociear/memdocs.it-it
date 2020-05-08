---
title: Impostazioni della baseline di sicurezza di Intune per Microsoft Edge
titleSuffix: Microsoft Intune
description: Impostazioni della baseline di sicurezza supportate da Intune per la gestione del browser Microsoft Edge
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 861d7f526711f2169e8fd03b3df09659440523b9
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693450"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Impostazioni della baseline di Microsoft Edge per Intune

Visualizzare le impostazioni della baseline del Web browser Microsoft Edge supportate da Microsoft Intune. Le impostazioni predefinite della baseline di Microsoft Edge rappresentano la configurazione consigliata per i browser Microsoft Edge e potrebbero non corrispondere ai valori predefiniti della baseline per altre baseline di sicurezza.

::: zone pivot="edge-october-2019"

> [!NOTE]
> La baseline di Microsoft Edge per ottobre 2019 è in anteprima pubblica.

::: zone-end
::: zone pivot="edge-april-2020"

*Questa nuova baseline verrà implementata nei tenant nelle prossime settimane. Si prevede che la nuova baseline sarà disponibile per tutti i tenant all'inizio di maggio.*
Per scoprire cosa è cambiato in questa versione della baseline rispetto alle versioni precedenti, usare l'azione [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Confronta baseline) disponibile quando si visualizza il riquadro *Versioni* per questa baseline. Per scoprire cosa è cambiato in questa versione della baseline rispetto alle versioni precedenti, usare l'azione [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Confronta baseline) disponibile quando si visualizza il riquadro *Versioni* per questa baseline.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Schemi di autenticazione supportati**  
  Specifica gli schemi di autenticazione HTTP supportati. È possibile configurare i criteri usando i valori seguenti: *basic*, *digest*, *ntlm* e *negotiate*. Separare più valori con virgole. Se non si configura questo criterio, vengono usati tutti e quattro gli schemi.

  - **Abilitato** (*predefinito*): vengono usati gli schemi selezionati.
  - **Disabilitato**
  - **Non configurato**: vengono usati tutti e quattro gli schemi.
  
  Quando è impostato su *Abilitato* è possibile configurare l'impostazione seguente in cui si seleziona l'autenticazione da usare:

  - **Schemi di autenticazione supportati**  
    Selezionare una delle opzioni seguenti:
    - **Basic**
    - **Digest**
    - **NTLM** *(selezionato per impostazione predefinita)*
    - **Negotiate** *(selezionato per impostazione predefinita)*

- **Impostazione predefinita di Adobe Flash**  
  CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) e [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Abilitare l'accesso all'impostazione seguente, in cui è possibile configurare il comportamento per l'esecuzione del plug-in Adobe Flash.  

  - **Abilitato** (*impostazione predefinita*)
  - **Disabilitato**
  - **Non configurato**

  Se impostato su *Abilitato*, è possibile configurare l'impostazione seguente.

  - **Impostazione predefinita di Adobe Flash**

    - **Blocca il plug-in Adobe Flash** (*impostazione predefinita*): blocca Adobe Flash in tutti i siti
    - **Fare clic per riprodurre**: viene eseguito Adobe Flash, ma l'utente deve selezionare l'opzione per avviarlo.

- **Controlla le estensioni che non possono essere installate**  
  Abilita l'utilizzo di un elenco che specifica le estensioni che gli utenti non possono installare in Microsoft Edge. Quando l'elenco è in uso, tutte le impostazioni dell'elenco installate in precedenza sono disabilitate e l'utente non può abilitarle. Se si rimuove una voce dall'elenco di estensioni bloccate, l'estensione corrispondente viene automaticamente riabilitata nella posizione in cui è stata installata in precedenza.

  - **Abilitato** (*impostazione predefinita*): abilita l'utilizzo dell'elenco per bloccare le estensioni.
  - **Disabilitato**
  - **Non configurato**: gli utenti possono installare qualsiasi estensione in Microsoft Edge.
  
  Quando è impostato su *Abilitato*, è possibile configurare l'impostazione seguente che definisce l'elenco di estensioni da bloccare.

  - **ID di estensione la cui installazione deve essere impedita agli utenti (o * per tutti)**

    Selezionare **Aggiungi** e specificare altre estensioni. **\*** è selezionata per impostazione predefinita.

- **Consenti gli host di messaggistica nativi a livello utente (installazione senza autorizzazioni di amministratore)**  
  Consente di abilitare l'installazione a livello utente degli host di messaggistica nativi.

  - **Enabled**
  - **Disabilitato** (*impostazione predefinita*): Microsoft Edge userà solo gli host di messaggistica nativi installati a livello di sistema.
  - **Non configurato**: per impostazione predefinita, Microsoft Edge consente l'uso di host di messaggistica nativi a livello di utente.

- **Abilita il salvataggio di password nello strumento per la gestione delle password**  
  CSP di Microsoft Edge: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Consente a Microsoft Edge di salvare le password utente.

  - **Abilitato**: gli utenti possono salvare le rispettive password in Microsoft Edge. Alla visita successiva al sito, Microsoft Edge immetterà automaticamente la password. Gli utenti non possono modificare o eseguire l'override di questi criteri in Microsoft Edge.
  - **Disabilitato** (*impostazione predefinita*): gli utenti non possono salvare nuove password, ma possono continuare a usare le password salvate in precedenza. Gli utenti non possono modificare o eseguire l'override di questi criteri in Microsoft Edge.
  - **Non configurato**: gli utenti possono salvare le password e disattivare questa funzionalità.

- **Impedisci di ignorare le richieste di Microsoft Defender SmartScreen per i siti**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Decidere se gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen su siti Web potenzialmente dannosi.

  - **Abilitato** (*impostazione predefinita*): gli utenti non possono ignorare gli avvisi di Microsoft Defender SmartScreen e non possono visitare il sito.
  - **Disabilitato**: gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen e visitare il sito.
  - **Non configurato**: gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen e visitare il sito

- **Impedisci di ignorare gli avvisi di Microsoft Defender SmartScreen sui download**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Determinare se gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen sui download non verificati.

  - **Abilitato** (*impostazione predefinita*): gli utenti non possono ignorare gli avvisi di Microsoft Defender SmartScreen né completare i download non verificati.
  - **Disabilitato**: gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen e completare i download non verificati.
  - **Non configurato**: gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen e completare i download non verificati.

- **Abilita l'isolamento sito per ogni sito**  
  Configurare l'isolamento del sito per impedire agli utenti di rifiutare esplicitamente il comportamento predefinito che prevede l'isolamento di tutti i siti.
  
  - **Abilitato** (*impostazione predefinita*): gli utenti non possono rifiutare esplicitamente il comportamento predefinito in cui ogni sito esegue il rispettivo processo.
  - **Disabilitato**: gli utenti possono rifiutare esplicitamente l'isolamento del sito. L'isolamento del sito non è disattivato.
  - **Non configurato**: gli utenti possono rifiutare esplicitamente l'isolamento del sito. L'isolamento del sito non è disattivato.

  Microsoft Edge supporta anche il criterio [IsolateOrigins](https://docs.microsoft.com/deployedge/microsoft-edge-policies#isolateorigins) in grado di isolare origini aggiuntive a granularità fine.  Intune non supporta la configurazione del criterio IsolateOrigins.
  
- **Configura Microsoft Defender SmartScreen**  
  CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen visualizza messaggi di avviso che contribuiscono a proteggere gli utenti da tentativi di phishing e software dannoso. Per impostazione predefinita, Microsoft Defender SmartScreen è attivato.
  
  - **Abilitato** (*impostazione predefinita*): Microsoft Defender SmartScreen viene attivato e gli utenti non possono disattivarlo.
  - **Disabilitato**: Microsoft Defender SmartScreen viene disattivato e gli utenti non possono attivarlo.
  - **Non configurato**: gli utenti possono scegliere se usare Microsoft Defender SmartScreen.

  Questo criterio è disponibile solo nelle istanze di Windows aggiunte a un dominio di Microsoft Active Directory oppure in istanze di Windows 10 Pro o Enterprise registrate per la gestione dei dispositivi.

- **Configura Microsoft Defender SmartScreen per il blocco di app potenzialmente indesiderate**  
    Configurare il comportamento di Microsoft Defender SmartScreen in modo da bloccare le app potenzialmente indesiderate. Microsoft Defender SmartScreen può visualizzare un messaggio di avviso che contribuisce a proteggere gli utenti da adware, coin miner, bundleware e altre app a bassa reputazione ospitate da siti Web. Il blocco delle app potenzialmente indesiderate in Microsoft Defender SmartScreen è disattivato per impostazione predefinita.

  - **Abilitato** (*impostazione predefinita*): le app potenzialmente indesiderate sono bloccate.
  - **Disabilitato**: le app potenzialmente indesiderate non sono bloccate.
  - **Non configurato**: gli utenti possono scegliere se usare il blocco delle app potenzialmente indesiderate in Microsoft Defender SmartScreen.

  Questo criterio è disponibile solo nelle istanze di Windows aggiunte a un dominio di Microsoft Active Directory oppure in istanze di Windows 10 Pro o Enterprise registrate per la gestione dei dispositivi.

- **Consenti agli utenti di continuare dalla pagina di avviso di SSL**  
   CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge mostra una pagina di avviso quando gli utenti visitano siti che presentano errori di SSL.
  - **Abilitato**: gli utenti possono fare clic nelle pagine di avviso.
  - **Disabilitato** (*impostazione predefinita*): gli utenti non possono fare clic nelle pagine di avviso.
  - **Non configurato**: gli utenti possono fare clic nelle pagine di avviso.

- **Versione minima SSL abilitata**  
  Abilitare l'opzione per l'impostazione di una versione minima supportata di SSL.

  - **Abilitato** (*impostazione predefinita*): abilitare l'accesso all'impostazione successiva in cui viene specificata la versione minima di TLS da usare.
  - **Disabilitato**
  - **Non configurato**: Microsoft Edge usa una versione minima predefinita di *TLS 1.0*.

  Se impostato su *Abilitato*, è possibile configurare TLS usando l'impostazione seguente.

  - **Versione minima SSL abilitata**: impostare la versione minima di TLS da usare. Microsoft Edge non userà alcuna versione di SSL/TLS precedente alla versione specificata.
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** (*impostazione predefinita*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Impedisci di ignorare le richieste di Microsoft Defender SmartScreen per i siti**  
  **Impostazione predefinita**: Abilitato  
  CSP di Microsoft Edge: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Questa impostazione dei criteri consente di decidere se gli utenti possono eseguire l'override degli avvisi di Microsoft Defender SmartScreen su siti Web potenzialmente dannosi. 
  - Se si abilita questa impostazione, gli utenti non potranno ignorare gli avvisi di Microsoft Defender SmartScreen e non potranno visitare il sito. 
  - Se si disabilita o non si configura questa impostazione, gli utenti possono ignorare gli avvisi di Microsoft Defender SmartScreen e visitare il sito.

- **Versione minima SSL abilitata**  
  **Impostazione predefinita**: Abilitato  

  Consente di impostare una versione minima supportata di SSL. Se si imposta questo criterio su *Non configurato*, Microsoft Edge usa una versione minima predefinita di *TLS 1.0*. Se il criterio è impostato su *Abilitato*, è possibile selezionare una versione minima tra i valori seguenti:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Versione minima SSL abilitata**  
    **Impostazione predefinita**: TLS 1.2

- **Impedisci di ignorare gli avvisi di Microsoft Defender SmartScreen sui download**  
  **Impostazione predefinita**: Abilitato  
  CSP di Microsoft Edge: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Questo criterio consente di determinare se gli utenti possono eseguire l'override degli avvisi di Microsoft Defender SmartScreen sui download non verificati.
  - Se si abilita questo criterio, gli utenti dell'organizzazione non potranno ignorare gli avvisi di Microsoft Defender SmartScreen né completare i download non verificati.
  - Se si disabilita o non si configura questo criterio, gli utenti potranno ignorare gli avvisi di Microsoft Defender SmartScreen e completare i download non verificati.

- **Consenti agli utenti di continuare dalla pagina di avviso di SSL**  
  **Impostazione predefinita**: Disabilitato  
  CSP di Microsoft Edge: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge mostra una pagina di avviso quando gli utenti visitano siti che presentano errori di SSL. Se si imposta questo criterio su *Abilitato* o *Non configurato*, gli utenti potranno fare clic per chiudere le pagine di avviso. Se il criterio viene impostato su *Disabilitato*, gli utenti non potranno fare clic per chiudere le pagine di avviso. 

- **Impostazione predefinita di Adobe Flash**  
  **Impostazione predefinita**: Abilitato  
  CSP di Microsoft Edge: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) e [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Determina se i siti Web non coperti da "PluginsAllowedForUrls" o "PluginsBlockedForUrls" possono eseguire automaticamente il plug-in Adobe Flash. 

  - Selezionare "BlockPlugins" per bloccare Adobe Flash in tutti i siti
  - Selezionare "ClickToPlay" per consentire l'esecuzione di Adobe Flash, chiedendo però all'utente di fare clic sul segnaposto per avviarlo.
  
  In ogni caso, i criteri "PluginsAllowedForUrls" e "PluginsBlockedForUrls" hanno la precedenza su "DefaultPluginsSetting". La riproduzione automatica è consentita solo per i domini elencati in modo esplicito nel criterio "PluginsAllowedForUrls". 
   Se si vuole abilitare la riproduzione automatica per tutti i siti, aggiungere http://* e https://* all'elenco.

  - Se si imposta questo criterio su *Non configurato*, l'utente potrà modificare manualmente questa impostazione. * 2 = Blocca il plug-in Adobe Flash * 3 = Fare clic per riprodurre. L'opzione "1" precedente consentiva di impostare il valore allow-all, ma questa funzionalità è ora gestita solo dal criterio "PluginsAllowedForUrls". I criteri esistenti che usano "1" adotteranno la modalità Fare clic per riprodurre.  

  - **Impostazione predefinita di Adobe Flash**  
    **Impostazione predefinita**: Blocca il plug-in Adobe Flash

- **Abilita l'isolamento sito per ogni sito**  
  **Impostazione predefinita**: Abilitato  

  Il criterio "SitePerProcess" può essere usato per impedire agli utenti di rifiutare esplicitamente il comportamento predefinito che richiede l'isolamento di tutti i siti. È anche possibile usare il criterio IsolateOrigins per isolare origini aggiuntive a granularità fine.

  - Se si imposta questo criterio su *Abilitato*, gli utenti non potranno rifiutare esplicitamente il comportamento predefinito in base al quale ogni sito esegue il rispettivo processo. 
  - Se si imposta il criterio su *Disabilitato* o *Non configurato*, un utente potrà rifiutare esplicitamente l'isolamento del sito, ad esempio usando la voce "Disabilita l'isolamento sito" in edge://flags. Se si disabilita o non si configura il criterio, l'opzione Isolamento sito non verrà disattivata.

- **Schemi di autenticazione supportati**  
  **Impostazione predefinita**: Abilitato  

  Specifica gli schemi di autenticazione HTTP supportati. È possibile configurare il criteri usando i valori seguenti: "basic", "digest", "NTLM" e "negotiate". Separare più valori con virgole. Se non si configura questo criterio, vengono usati tutti e quattro gli schemi.

  - **Schemi di autenticazione supportati**  
    Selezionare una delle opzioni seguenti:
    - Di base
    - Digest
    - NTLM *(selezionato per impostazione predefinita)*
    - Negotiate *(selezionato per impostazione predefinita)*

- **Abilita il salvataggio di password nello strumento per la gestione delle password**  
  **Impostazione predefinita**: Disabilitato  
  CSP di Microsoft Edge: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Consente a Microsoft Edge di salvare le password utente.
  - Se si abilita questo criterio, gli utenti potranno salvare le rispettive password in Microsoft Edge. Alla visita successiva al sito, Microsoft Edge immetterà automaticamente la password.
  - Se si disabilita questo criterio, gli utenti non potranno salvare nuove password, ma potranno comunque usare le password salvate in precedenza.
  
  Se si imposta questo criterio su *Abilitato* o *Disabilitato*, gli utenti non potranno modificare o eseguire l'override del criterio in Microsoft Edge.
  
  Se si imposta il criterio su *Non configurato*, gli utenti potranno salvare le password e disattivare questa funzionalità.

- **Controlla le estensioni che non possono essere installate**  
  **Impostazione predefinita**: Abilitato  

  Elenca le estensioni specifiche che gli utenti non possono installare in Microsoft Edge. Quando si distribuisce questo criterio, le estensioni presenti in questo elenco che sono state installate vengono disabilitate e l'utente non sarà in grado di abilitarle. Se si rimuove una voce dall'elenco di estensioni bloccate, l'estensione corrispondente viene automaticamente riabilitata nella posizione in cui è stata installata in precedenza.
  
  Usare **\*** per bloccare tutte le estensioni non elencate in modo esplicito nell'elenco delle estensioni consentite. Se questo criterio viene impostato su *Non configurato*, gli utenti possono installare qualsiasi estensione in Microsoft Edge.
  
  Valore di esempio: extension_id1 extension_id2.  
  <br>
  - **ID di estensione la cui installazione deve essere impedita agli utenti (o * per tutti)**  
    Selezionare **Aggiungi** e specificare altre estensioni. **\*** è selezionata per impostazione predefinita.

- **Configura Microsoft Defender SmartScreen**  
  **Impostazione predefinita**: Abilitato  
  CSP di Microsoft Edge: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Questa impostazione dei criteri consente di stabilire se attivare Microsoft Defender SmartScreen. Microsoft Defender SmartScreen fornisce messaggi di avviso che contribuiscono a proteggere gli utenti da tentativi di phishing e software dannoso.
  
  - Per impostazione predefinita, Microsoft Defender SmartScreen è attivato. Se si abilita questa impostazione, Microsoft Defender SmartScreen viene attivato e gli utenti non possono disattivarlo.
  - Se si disabilita questa impostazione, Microsoft Defender SmartScreen viene disattivato e gli utenti non possono attivarlo.
  - Se si imposta questo criterio su *Non configurato*, gli utenti possono scegliere se usare Microsoft Defender SmartScreen.
  
  Questo criterio è disponibile solo nelle istanze di Windows aggiunte a un dominio di Microsoft Active Directory oppure in istanze di Windows 10 Pro o Enterprise registrate per la gestione dei dispositivi.

- **Consenti gli host di messaggistica nativi a livello utente (installazione senza autorizzazioni di amministratore)**  
  **Impostazione predefinita**: Disabilitato

  Consente di abilitare l'installazione a livello utente degli host di messaggistica nativi. 
  - Se si disabilita questo criterio, Microsoft Edge userà solo gli host di messaggistica nativi installati a livello di sistema. Per impostazione predefinita, se non si configura questo criterio Microsoft Edge consentirà l'utilizzo degli host di messaggistica nativi a livello utente.

::: zone-end

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sulle baseline di sicurezza](security-baselines.md)
- [Evitare conflitti](security-baselines.md#avoid-conflicts)
- [Risolvere problemi relativi a criteri e profili in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
