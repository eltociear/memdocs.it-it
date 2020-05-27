---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764204"
---
# <a name="in-development-for-microsoft-intune"></a>In fase di sviluppo per Microsoft Intune

Per supportare gli utenti nella preparazione e pianificazione, questa pagina illustra gli aggiornamenti e le funzionalità dell'interfaccia utente di Intune che sono in fase di sviluppo ma non ancora rilasciati. Oltre alle informazioni contenute in questa pagina: 

- Se sono previste azioni prima di una modifica, verrà pubblicato un post complementare nel Centro messaggi di Office.
- Quando una funzionalità entra in produzione, sia in versione anteprima sia disponibile a livello generale, la descrizione della funzionalità viene spostata da questa pagina alla [pagina delle novità](whats-new.md).
- Questa pagina e la [pagina delle novità](whats-new.md) vengono aggiornate periodicamente. Consultarla a intervalli regolari per ulteriori aggiornamenti.
- Vedere la [roadmap di Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) per informazioni sulle sequenze temporali e i risultati finali strategici.

> [!NOTE]
> Questa pagina riflette le attuali previsioni su funzionalità di Intune che verranno introdotte in una versione futura. Le date e le singole funzionalità potrebbero cambiare. Questa pagina non descrive tutte le funzionalità in fase di sviluppo.

**Feed RSS**: è possibile sapere quando questa pagina viene aggiornata copiando e incollando l'URL seguente nel lettore di feed: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Questo articolo è stato aggiornato l'ultima volta nella data indicata sotto al titolo precedente**.

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Gestione delle app

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Il Portale aziendale per Android consente agli utenti di ottenere le app dopo la registrazione del profilo di lavoro <!-- 6103999  -->
È in corso il miglioramento delle linee guida all'interno del Portale aziendale, in modo da facilitare la ricerca e l'installazione di app per gli utenti.  Dopo aver eseguito la registrazione nella gestione del profilo di lavoro, gli utenti visualizzeranno un messaggio che informa che è possibile trovare le app suggerite nella versione con badge di Google Play. Gli utenti visualizzeranno anche un nuovo collegamento **Scarica app** nel cassetto del Portale aziendale sul lato sinistro. Per dare più spazio a queste esperienze nuove e migliorate, la scheda **App** verrà rimossa. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Le impostazioni e i valori del profilo di configurazione del dispositivo verranno aggiornati per le piattaforme Windows<!-- 4091122 -->
Quando si creano profili di configurazione dei dispositivi per le piattaforme Windows (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > qualsiasi opzione **Windows** per la piattaforma), alcune impostazioni e i relativi valori sono diversi da quelli del provider CSP e potrebbero generare confusione. I nomi delle impostazioni e i relativi valori verranno aggiornati in modo da essere più chiari.

Si applica a:

- Profilo di configurazione dei dispositivi Windows 10 e versioni successive
- Profili di configurazione dei dispositivi Windows Holographic for Business
- Profili di configurazione dei dispositivi Windows 8.1
- Profili di configurazione dei dispositivi Windows Phone 8.1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Nuova impostazione FileVault per i criteri di configurazione del dispositivo Endpoint Protection per macOS<!-- 5459801   -->
È in corso l'aggiunta di una nuova impostazione alla categoria FileVault nel modello di [Endpoint Protection per macOS](../protect/endpoint-protection-macos.md): Nascondi la chiave di ripristino (**Dispositivi** > **Profili di configurazione** > **Crea profilo**, selezionare **macOS** per *Piattaforma* e quindi **Endpoint Protection** per *Tipo di profilo*). Questa impostazione nasconde la chiave personale all'utente finale durante la crittografia FileVault 2. Un utente di un dispositivo può visualizzare la chiave di ripristino personale in qualsiasi momento dall'app Portale aziendale di iOS o dal sito Web del portale aziendale per il dispositivo macOS crittografato. Per visualizzare la chiave di ripristino personale, può passare ai dettagli del dispositivo e fare clic su *Ottieni la chiave di ripristino*.

Questa impostazione non sarà disponibile nei criteri creati in precedenza. Per configurare questa impostazione e poterla usare, sarà necessario ricreare i criteri di FileVault. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>I dispositivi BYOD (Bring Your Own Device) possono usare la VPN per la distribuzione<!--5015344 -->
È possibile che questa funzionalità venga posticipata.

### <a name="shared-ipads-for-business--6367326---"></a>IPad condivisi per le aziende<!--6367326 -->
Sarà possibile usare Intune e Apple Business Manager per configurare in modo semplice e sicuro l'iPad condiviso, in modo che più dipendenti possano condividere i dispositivi. [iPad condiviso](https://developer.apple.com/education/shared-ipad/) di Apple offre un'esperienza personalizzata per più utenti, pur proteggendo i dati dei singoli utenti. Tramite un ID Apple gestito gli utenti possono accedere alle loro app, ai dati e alle impostazioni personali dopo aver eseguito l'accesso a qualsiasi iPad condiviso nell'organizzazione. iPad condiviso funziona con le identità federate.

Per visualizzare questa funzionalità passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Dispositivi** > **iOS** > **Registrazione di iOS** > **Token del programma di registrazione** > scegliere un token** > **Profili** > **Crea profilo** > **iOS**. Nella pagina **Impostazioni di gestione** selezionare **Registra senza affinità utente**. Verrà visualizzata l'opzione **iPad condiviso**.

**Si applica a:** macOS 13.4 e versioni successive. In questa versione è stato aggiunto il supporto per le sessioni temporanee con iPad condiviso, in modo che gli utenti possano accedere a un dispositivo senza un ID Apple gestito. Al momento della disconnessione, il dispositivo cancella tutti i dati dell'utente e torna a essere immediatamente pronto per l'uso, eliminando la necessità di una cancellazione del dispositivo stesso. 

<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.


<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modello di report di conformità Power BI V2.0<!-- 636958  -->
Gli amministratori potranno aggiornare il modello di report di conformità di Power BI da V1.0 a V2.0. V2.0 includerà una struttura migliorata e aggiornamenti ai calcoli e ai dati esposti come parte del modello. Per informazioni correlate, vedere [Connettersi al data warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicurezza


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplicare i criteri in Endpoint Security<!-- 5892558   -->
Sarà possibile selezionare un criterio creato nel nodo Endpoint Security dell'interfaccia di amministrazione di Microsoft Endpoint Manager e quindi duplicarlo per creare una copia.  I criteri che è possibile duplicare includono quelli creati per: 

- Antivirus
- Crittografia del disco
- Firewall
- Rilevamento di endpoint e risposta
- Riduzione della superficie di attacco
- Protezione account

La duplicazione creerà una copia del criterio originale, che potrà quindi essere rinominato e modificato. La copia non includerà le assegnazioni dell'originale.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nuovo profilo per il criterio firewall di Endpoint Security<!-- 5653324   -->
Come anteprima, viene introdotto un profilo aggiuntivo per Windows 10 e versioni successive al criterio Firewall in Endpoint Security di Intune (**Endpoint Security** > **Firewall** > **Crea criterio** > selezionare **Windows 10 e versioni successive**). 

Ogni istanza di questo nuovo profilo supporta fino a 150 *regole Microsoft Defender Firewall* personalizzate. Il profilo delle regole Microsoft Defender Firewall consente di definire regole di Windows Firewall granulari, per autorizzare o bloccare le porte e le applicazioni in Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).



