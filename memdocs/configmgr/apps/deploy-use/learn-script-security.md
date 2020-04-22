---
title: Informazioni sulla sicurezza degli script PowerShell
titleSuffix: Configuration Manager
description: Risorse per ottenere informazioni sulla sicurezza degli script PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a0edf83c736c2737f4af2f040159a71bb0348aee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689309"
---
# <a name="learn-more-about-powershell-script-security"></a>Informazioni sulla sicurezza degli script PowerShell

*Si applica a: Configuration Manager (Current Branch)*

È responsabilità dell'amministratore convalidare il linguaggio PowerShell proposto e l'uso dei parametri PowerShell nell'ambiente. Di seguito sono disponibili risorse utili che gli amministratori possono usare per conoscere i punti di forza di PowerShell e le possibili aree di rischio. In questo modo è possibile ridurre le possibili aree di rischio e consentire l'uso di script sicuri.

## <a name="powershell-script-security"></a>Sicurezza degli script PowerShell
In Esecuzione script è disponibile una funzionalità che consente di rivedere visivamente e approvare gli script che devono essere eseguiti nell'ambiente. È importante che gli amministratori sappiano che PowerShell può contenere script offuscato. Si tratta di script dannoso e difficilmente rilevabile con un controllo visivo durante il processo di approvazione dello script. Oltre a rivedere visivamente gli script di PowerShell, è consigliabile usare alcuni strumenti di controllo per rilevare problemi che riguardano script sospetti. Questi strumenti non sempre riconoscono la finalità dell'autore PowerShell e pertanto può essere rilevato uno script sospetto. L'uso di tali strumenti richiede tuttavia l'intervento dell'amministratore che deve valutare se la sintassi dello script è dannosa o intenzionale.

## <a name="recommendations"></a>Indicazioni
- Acquisire familiarità con le procedure consigliate per la sicurezza PowerShell usando i vari collegamenti indicati di seguito.
- **Firmare gli script**: un altro modo per garantire che gli script siano sicuri consiste nell'esaminarli e firmarli prima che siano importati e usati.
- Non archiviare segreti (ad esempio password) negli script PowerShell e informarsi su come gestire i segreti.


## <a name="general-information-about-powershell-security-best-practices"></a>Informazioni generali sulle procedure consigliate per la sicurezza PowerShell

Di seguito sono stati raccolti alcuni collegamenti che gli amministratori di Configuration Manager possono usare come punto di partenza per scoprire le procedure consigliate per la sicurezza PowerShell.  

[Introduzione alle procedure consigliate per la sicurezza PowerShell](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerPoint sulle procedure consigliate per la sicurezza PowerShell](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Blog del team PowerShell sulla difesa da attacchi PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Tweet di Lee Holmes, esperto di sicurezza Microsoft PowerShell, sulla difesa da attacchi PowerShell](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Blog sulla protezione da code injection dannoso](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[Blue Team PowerShell: discussione su registrazione blocco script approfondita, registrazione eventi protetti, interfaccia di analisi antimalware, API di generazione codice sicuro](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[API per un'interfaccia di analisi antimalware disponibile in Windows 10](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Sicurezza dei parametri PowerShell
Il passaggio dei parametri garantisce flessibilità agli script e consente di rimandare le decisioni in fase di esecuzione. Lascia però spazio a un'altra area di rischio. Di seguito sono riportate le procedure consigliate per evitare parametri dannosi o script injection:

- Consentire solo l'uso di parametri predefiniti.
- Usare l'espressione regolare per convalidare i parametri consentiti.
    - Esempio: se è consentito solo un determinato intervallo di valori, usare un'espressione regolare per verificare che siano presenti solo quei caratteri o valori che possono costituire l'intervallo.
    - Convalidare i parametri per evitare l'uso di determinati caratteri di escape, ad esempio le virgolette. Tenere presente che possono esistere più tipi di virgolette. Può quindi essere più semplice usare le espressioni regolari per convalidare i caratteri consentiti, anziché definire tutti gli input non consentiti.
- Usare il modulo ["hunter injection"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) di PowerShell in PowerShell Gallery.
    - Potrebbero essere riscontrati falsi positivi. Controllare quindi la finalità nel caso in cui siano contrassegnati casi sospetti per determinare se si tratta effettivamente di un problema. 
- Microsoft Visual Studio offre un analizzatore di script che può essere usato per controllare la sintassi di PowerShell.
- Questo video intitolato: "DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server"(DEF CON 25 - Lee Holmes - Colpito e affondato: Attacco ai danni di Windows Server) offre una panoramica dei tipi di problemi da cui è possibile proteggersi (in particolare la sezione compresa tra 12:20 e 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Consigli relativi all'ambiente
Consigli generali per gli amministratori di PowerShell.
1. Distribuire la versione più recente di PowerShell, ad esempio la versione 5 o successiva, inclusa in Windows 10. In alternativa, è possibile distribuire [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616). 
2. Abilitare e raccogliere log PowerShell, includendo facoltativamente la registrazione eventi protetti. Incorporare questi log nelle firme e nei flussi di lavoro di ricerca e di risposta a eventi imprevisti.
3. Implementare Just Enough Administration in sistemi importanti per eliminare o ridurre l'accesso senza vincoli come amministratore a questi sistemi.
4. Distribuire i criteri di Controllo di applicazioni di Windows Defender per consentire alle attività amministrative pre-approvate di usare tutte le funzionalità del linguaggio PowerShell, limitando al tempo stesso l'uso interattivo e non approvato a un sottoinsieme limitato del linguaggio PowerShell.
5. Distribuire Windows 10 per consentire al provider dell'applicazione antivirus accesso completo a tutti i contenuti (incluso il contenuto generato o deoffuscato in fase di esecuzione) elaborato dalle istanze di Windows Scripting Host che includono PowerShell.
