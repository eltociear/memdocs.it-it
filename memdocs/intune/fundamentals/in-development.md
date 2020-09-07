---
title: In fase di sviluppo - Microsoft Intune
titleSuffix: ''
description: Funzionalità di Microsoft Intune in fase di sviluppo
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: feb277f30401f31ddb400f5e3f6cd7709fa31c0b
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286238"
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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Aggiornamento alle icone del dispositivo nel Portale aziendale e nelle app di Intune in Android<!-- 6057023  -->
Viene eseguito un aggiornamento delle icone del dispositivo nel Portale aziendale e nelle app di Intune nei dispositivi Android per creare un aspetto più moderno e in linea con Microsoft Fluent Design System. Per informazioni correlate, vedere [Aggiornamento delle icone nell'app Portale aziendale per iOS/iPadOS e macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>Il Portale aziendale per iOS supporterà la registrazione automatica dei dispositivi di Apple senza affinità utente<!-- 7282707  --> 
Il Portale aziendale per iOS sarà supportato nei dispositivi registrati con la registrazione automatica dei dispositivi di Apple senza richiedere un utente assegnato. L'utente finale può accedere al Portale aziendale per iOS per specificarsi come utente primario in un dispositivo iOS/iPadOS registrato senza affinità dispositivo. Per altre informazioni sulla registrazione automatica dei dispositivi, vedere [Registrare automaticamente i dispositivi iOS/iPadOS con Registrazione automatica del dispositivo di Apple](../enrollment/device-enrollment-program-enroll-ios.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Configurazione del dispositivo

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Creare nuovi profili dei certificati PKCS per dispositivi Android Enterprise completamente gestiti (COBO)<!-- 4839686 -->
È possibile creare profili dei certificati PKCS per distribuire certificati ai proprietari di dispositivi Android Enterprise e a dispositivi con profilo di lavoro (**Dispositivi** > **Profili di configurazione**  > **Crea profilo** > **Android Enterprise > Solo proprietario del dispositivo** oppure **Android Enterprise > Solo profilo di lavoro** per la piattaforma > **PKCS** per il profilo).

A breve sarà possibile creare nuovi profili dei certificati PKCS per dispositivi Android Enterprise completamente gestiti. Il connettore di certificati PFX di Intune è obbligatorio. Se non si usa SCEP e si usa solo PKCS, è possibile rimuovere il connettore NDES dopo aver installato il nuovo connettore PFX. Il nuovo connettore PFX importa i file PFX e distribuisce i certificati PKCS a tutte le piattaforme.

Per altre informazioni sui certificati PKCS, vedere [Configurare e usare i certificati PKCS con Intune](../protect/certficates-pfx-configure.md).

Si applica a:
- Android Enterprise completamente gestito (COBO)

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>Supporto per certificati con dimensioni della chiave 4096 nei dispositivi iOS e macOS<!-- 7659175   -->
Intune supporterà presto l'uso delle dimensioni della chiave 4096 bit per i profili di certificato SCEP. (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > *selezionare una piattaforma* > *Profilo* = **Certificato SCEP**)

Il supporto per chiavi a 4096 bit sarà disponibile per le piattaforme seguenti: 
- iOS 14 e versioni successive
- macOS 11 e versioni successive    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Nuova impostazione per la complessità delle password per Android 10 e versioni successive<!-- 7992114  -->
Per supportare le nuove opzioni per Android 10 e versioni successive, verrà aggiunta una nuova impostazione denominata **Complessità password** sia ai criteri di *conformità del dispositivo* sia ai criteri di *restrizione del dispositivo*. (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Restrizioni del dispositivo** e **Dispositivi** > **Criteri di conformità** > **Crea criterio**) Con questa impostazione sarà possibile gestire una misura di complessità della password che tenga conto del tipo, della lunghezza e della qualità della password. 

Verranno supportati i livelli di complessità seguenti:
- **Nessuno** - Nessuna password
- **Basso** - La password soddisfa uno dei criteri seguenti:
  - Modello
  - PIN con sequenze ripetute (4444) o ordinate (1234, 4321, 2468)
- **Medio** - La password soddisfa uno dei criteri seguenti:
  - PIN senza sequenze ripetute (4444) o ordinate (1234, 4321, 2468), lunghezza minima 4
  - Alfabetica, lunghezza minima 4
  - Alfanumerica, lunghezza minima 4
- **Alto** - La password soddisfa uno dei criteri seguenti:
  - PIN senza sequenze ripetute (4444) o ordinate (1234, 4321, 2468), lunghezza minima 8
  - Alfabetica, lunghezza minima 6
  - Alfanumerica, lunghezza minima 6

La complessità delle password non si applica ai dispositivi Samsung Knox che eseguono Android 10 e versioni successive. In questi dispositivi le impostazioni per la lunghezza della password e/o il tipo di password sono prioritarie rispetto alla complessità della password.

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>Aggiornamento dell'anteprima per i dispositivi COPE: nuove impostazioni per la creazione di requisiti per la password del profilo di lavoro per i dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro<!--7088355 -->
Le impostazioni future offriranno agli amministratori la possibilità di impostare i requisiti per la password del profilo di lavoro per i dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro.  (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale** > **Restrizioni del dispositivo** per il profilo > **Password del profilo di lavoro**):

- Tipo di password richiesto
- Lunghezza minima password
- Numero di giorni rimanenti prima della scadenza della password
- Numero di password obbligatorie prima che un utente possa riutilizzare una password
- Numero di errori di accesso prima della cancellazione dei dati del dispositivo


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>Nuove impostazioni per l'uso di VPN per app o VPN su richiesta nei dispositivi iOS/iPadOs e macOS<!-- 7758772 7758837 7758886  -->
- **Prevent users from disabling automatic VPN** (Impedisci agli utenti di disabilitare la VPN automatica): quando si crea una connessione automatica **VPN per app** o **VPN su richiesta**, è possibile imporre agli utenti di mantenere abilitata e in esecuzione la VPN automatica.
- **Domini associati**: quando si crea una connessione automatica **VPN per app**, è possibile specificare i domini associati nel profilo VPN che avviano automaticamente la connessione VPN. 
- **Domini esclusi**: quando si crea una connessione automatica **VPN per app**, è possibile creare un elenco di domini che possono ignorare la connessione VPN quando viene connessa la VPN per app.

È possibile configurare i profili di VPN automatica in **Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** o **macOS** per la piattaforma > **VPN** per il profilo > **VPN automatico**.

Per altre informazioni sui domini associati, vedere [Domini associati](../configuration/device-features-configure.md#associated-domains).

Per visualizzare le impostazioni che è possibile configurare, vedere [Configurare una rete privata virtuale (VPN) per app per dispositivi iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Si applica a:
- iOS/iPadOS 14 e versioni successive
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>Aggiornamento dell'anteprima per i dispositivi COPE: nuove impostazioni per configurare il profilo personale per i dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro<!-- 7086356  -->
Per i dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro, è possibile configurare nuove impostazioni che si applicano solo al profilo personale (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** per la piattaforma > **Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale** > **Restrizioni del dispositivo** per il profilo > **Profilo personale**):

- **Fotocamera**: usare questa impostazione per bloccare l'accesso alla fotocamera durante l'utilizzo personale.
- **Acquisizione schermo**: usare questa impostazione per bloccare le acquisizioni di schermate durante l'utilizzo personale.
- **Consenti agli utenti di abilitare l'installazione di app da origini sconosciute nel profilo personale**: usare questa impostazione per consentire agli utenti di installare app da origini sconosciute nel profilo personale. 

Per visualizzare le impostazioni correnti configurabili, vedere [Impostazioni dei dispositivi Android Enterprise per consentire o limitare funzionalità](../configuration/device-restrictions-android-for-work.md).

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>Bloccare App Clips in iOS/iPadOs e rinviare gli aggiornamenti software non del sistema operativo nei dispositivi macOS<!-- 7518422  -->
Quando si crea un profilo di restrizioni dei dispositivi nei dispositivi iOS/iPadOs e macOS, sono disponibili alcune nuove impostazioni:

**iOS/iPadOS 14.0+ Blocca app clip**
- Si applica a iOS/iPadOs 14.0 e versioni successive.
- I dispositivi devono essere registrati con la registrazione del dispositivo o la registrazione automatica dei dispositivi (dispositivi con supervisione).
- L'impostazione **Blocca app clip** blocca App Clips nei dispositivi gestiti (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Restrizioni del dispositivo** per il profilo > **Generale**). Quando il blocco è attivo, gli utenti non possono aggiungere App Clips e le eventuali App Clips esistenti vengono rimosse dal dispositivo.  

**macOS 11+ Rinvia gli aggiornamenti software**
- Si applica a: macOS 11 e versioni successive. Nei dispositivi macOS con supervisione, il dispositivo deve avere la registrazione del dispositivo approvata dall'utente o essere registrato tramite la registrazione automatica dei dispositivi.
- L'impostazione **Rinvia gli aggiornamenti software** ritarda la visibilità degli aggiornamenti software non del sistema operativo per gli utenti (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **macOS** per la piattaforma > **Restrizioni del dispositivo** per il profilo > **Generale**). Se si rinviano questi aggiornamenti, i nuovi aggiornamenti rilasciati non saranno visibili per gli utenti fino al termine del periodo di rinvio, configurato con le impostazioni **Posticipa la visibilità degli aggiornamenti software**. Il rinvio degli aggiornamenti software non del sistema operativo non influisce sugli aggiornamenti pianificati.
- L'impostazione **Rinvia gli aggiornamenti software** esistente viene combinata con questa nuova impostazione. Usando la nuova impostazione, è possibile rinviare gli aggiornamenti software del sistema operativo e gli aggiornamenti software non del sistema operativo. È possibile continuare a usare l'impostazione **Posticipa la visibilità degli aggiornamenti software** per impostare il numero di giorni, che verrà applicato a entrambe le impostazioni per il rinvio degli aggiornamenti software.
- Il comportamento dei criteri esistenti non viene modificato, interessato o eliminato. Verrà eseguita automaticamente la migrazione dei criteri esistenti alla nuova impostazione con la stessa configurazione.

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>Disabilitare l'assegnazione casuale di indirizzi MAC nelle reti Wi-Fi nei dispositivi iOS/iPadOs<!-- 7758689  -->
A partire da iOS/iPadOs 14, per impostazione predefinita, i dispositivi presentano un indirizzo MAC casuale quando si connettono a una rete anziché l'indirizzo MAC fisico. Questo comportamento è consigliato per la privacy, perché è più difficile rintracciare un dispositivo in base al relativo indirizzo MAC. Con questa funzionalità non funzionano più i meccanismi basati su un indirizzo MAC statico, incluso il controllo di accesso alla rete (NAC). 

È possibile disabilitare l'assegnazione casuale di indirizzi MAC per ogni singola rete nei profili Wi-Fi (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPadOS** per la piattaforma > **Wi-Fi** per il profilo > **Basic** o **Enterprise** per il tipo Wi-Fi).

Per visualizzare le impostazioni che è attualmente possibile configurare, passare a [Aggiungere le impostazioni Wi-Fi per dispositivi iOS e iPadOS](../configuration/wi-fi-settings-ios.md).

Si applica a:
- iOS/iPadOS 14 e versioni successive

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>Impostare l'unità massima di trasmissione per le connessioni VPN IKEv2 nei dispositivi iOS/iPadOs<!-- 7758937  -->
A partire da iOS/iPadOs 14 e nei dispositivi più recenti, è possibile configurare un'unità massima di trasmissione personalizzata quando si usano connessioni VPN IKEv2 (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **iOS/iPad** per la piattaforma > **VPN** per il profilo -> IKEv2 per il tipo di connessione).

Per altre informazioni sulle impostazioni che è possibile configurare, vedere [Impostazioni IKEv2](../configuration/vpn-settings-ios.md#ikev2-settings).

Si applica a:
- iOS/iPadOS 14 e versioni successive

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>Connessione VPN per account per i profili di posta elettronica nei dispositivi iOS/iPadOs<!-- 7759116  -->
A partire da iOS/iPadOs 14, il traffico di posta elettronica per l'app di posta elettronica nativa può essere instradato tramite una VPN in base all'account usato dall'utente. È ora possibile specificare un profilo VPN per app da usare per questa connessione VPN basata sull'account.  La connessione VPN per app viene attivata automaticamente quando gli utenti usano il proprio account aziendale nell'app di posta elettronica.

Per visualizzare le impostazioni che è attualmente possibile configurare, passare ad [Aggiungere le impostazioni di posta elettronica per dispositivi iOS e iPadOS](../configuration/email-settings-ios.md).

Si applica a:
- iOS/iPadOS 14 e versioni successive

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Usare NetMotion come tipo di connessione VPN per i dispositivi con profilo di lavoro Android Enterprise<!-- 7764263 -->
Quando si crea un profilo VPN, NetMotion è disponibile come tipo di connessione VPN (**Dispositivi** > **Configurazione dispositivo** > **Crea profilo** > **Profilo di lavoro Android Enterprise** per la piattaforma > **VPN** per il profilo > **NetMotion** per il tipo di connessione).

Per altre informazioni sui profili VPN in Intune, vedere [Creare profili VPN per la connessione ai server VPN](../configuration/vpn-settings-configure.md).

Si applica a:
- Profilo di lavoro di Android Enterprise

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Modifiche per le impostazioni della password nei profili di restrizione dei dispositivi per l'amministratore di dispositivi Android<!-- 7662279  --> 
Sono state introdotte alcune modifiche per le impostazioni della password per i criteri di *restrizione del dispositivo* e di *conformità* per l'*amministratore di dispositivi Android*. (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Restrizioni del dispositivo** e **Dispositivi** > **Criteri di conformità** > **Crea criterio**) Queste modifiche consentono a Intune di integrare le modifiche in Android versione 10 e successive, per garantire che le impostazioni per le password continuino a essere applicate ai dispositivi come previsto.
 
Le modifiche includono:
- Rimozione dell'opzione di primo livello per **Password**.  
- Le impostazioni verranno riorganizzate in sezioni in base ai dispositivi a cui si applicano.
- L'impostazione **Lunghezza minima password** verrà disabilitata per l'uso, a meno che l'impostazione **Tipo password** non sia configurata su un valore a cui si applica la lunghezza della password.
- Altri aggiornamenti per le etichette e il testo di esempio.

Queste modifiche si applicano all'interfaccia utente per le impostazioni e non influiscono sui profili esistenti. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Registrazione del dispositivo

### <a name="ending-support-for-ios-11--7327321---"></a>Termine del supporto per iOS 11<!--7327321 -->
Dopo il rilascio di iOS 14, la registrazione di Intune e l'app Portale aziendale supporteranno iOS versione 12 e successive. Le versioni precedenti non saranno supportate ma continueranno a ricevere i criteri.

### <a name="ending-support-for-macos-1012--7327326---"></a>Termine del supporto per macOS 10.12<!--7327326 -->
Dopo il rilascio di macOS 11, la registrazione di Intune e l'app Portale aziendale supporteranno macOS versione 10.13 e successive. Le versioni precedenti non saranno supportate.


<!-- ***********************************************-->
## <a name="device-management"></a>Gestione dei dispositivi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Supporto degli script di PowerShell per dispositivi BYOD<!-- 1862833  -->
Gli script di PowerShell supporteranno i dispositivi registrati con Azure AD in Intune. Per altre informazioni su PowerShell, vedere [Usare gli script di PowerShell nei dispositivi Windows 10 in Intune](../apps/intune-management-extension.md). Questa funzionalità non supporta i dispositivi che eseguono Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics includerà il log dei dettagli del dispositivo<!--6014987  -->
I log dei dettagli dei dispositivi di Intune saranno disponibili in **Report** > **Log Analytics**. È possibile correlare i dettagli dei dispositivi per creare query personalizzate e cartelle di lavoro di Azure.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Collegamento di tenant: sequenza temporale dispositivo nell'interfaccia di amministrazione<!--7220536, CM7141381 -->
Quando Configuration Manager sincronizza un dispositivo con Microsoft Endpoint Manager tramite il collegamento al tenant, è possibile visualizzare una sequenza temporale degli eventi. Questa sequenza temporale mostra le attività precedenti eseguite sul dispositivo che possono risultare utili per la risoluzione dei problemi. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Collegamento di tenant: installare un'applicazione dall'interfaccia di amministrazione<!-- 7220536, CM6024389 -->
Sarà possibile avviare l'installazione di un'applicazione in tempo reale per un dispositivo collegato al tenant dall'interfaccia di amministrazione di Microsoft Endpoint Management. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Collegamento di tenant: CMPivot dall'interfaccia di amministrazione<!--7220536, CM6024392 -->
Sarà possibile sfruttare la potenza di [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono avviare query in tempo reale dal cloud su un singolo dispositivo gestito da ConfigMgr e restituire i risultati all'interfaccia di amministrazione. In questo modo è possibile usufruire di tutti i vantaggi tradizionali di CMPivot, che consente agli amministratori IT e ad altri utenti designati di valutare rapidamente lo stato dei dispositivi nel proprio ambiente e di intervenire di conseguenza. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Collegamento di tenant: eseguire script dall'interfaccia di amministrazione<!--7220536, CM6234688 -->
Sarà possibile sfruttare la potenza della funzionalità locale di Configuration Manager per [l'esecuzione di script](../../configmgr/apps/deploy-use/create-deploy-scripts.md) nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Altri utenti tipo, ad esempio il personale del supporto tecnico, possono eseguire script di PowerShell dal cloud su un singolo dispositivo gestito di Configuration Manager. In questo modo è possibile usufruire di tutti i vantaggi tradizionali degli script di PowerShell che sono già stati definiti e approvati dall'amministratore di Configuration Manager nel nuovo ambiente. Per altre informazioni, vedere [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Distribuire gli aggiornamenti software nei dispositivi macOS <!-- 3194876 -->
Sarà possibile distribuire gli aggiornamenti software a gruppi di dispositivi macOS. Questa funzionalità include aggiornamenti critici, firmware, file di configurazione e altri aggiornamenti. Sarà possibile inviare aggiornamenti alla successiva sincronizzazione del dispositivo oppure selezionare una pianificazione settimanale per distribuire gli aggiornamenti entro o al di fuori degli intervalli di tempo impostati. Ciò può risultare utile quando si vuole aggiornare i dispositivi al di fuori delle ore di lavoro standard o quando l'help desk occupa tutto il personale. Si otterrà anche un report dettagliato di tutti i dispositivi macOS a cui sono stati distribuiti gli aggiornamenti. È possibile esaminare il report per ogni singolo dispositivo per visualizzare lo stato di specifici aggiornamenti.

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>Aggiornamento dell'anteprima per i dispositivi COPE: reimpostare la password del profilo di lavoro per i dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro <!--7217228 -->
Una futura azione di amministrazione consentirà agli amministratori di reimpostare la password del profilo di lavoro nei dispositivi di proprietà dell'azienda Android Enterprise con un profilo di lavoro.

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>Rinominare un dispositivo co-gestito aggiunto ad Azure Active Directory<!--7728043 -->
Sarà possibile rinominare un dispositivo co-gestito aggiunto ad Azure AD. A tale scopo, passare a MEM > **Dispositivi** > **Tutti i dispositivi** > scegliere un dispositivo > **...**  > **Rinomina dispositivo**.

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Supporto di batterie PowerPrecision e PowerPrecision+ per i dispositivi Zebra<!--3724987 -->
Nella pagina dei dettagli hardware del dispositivo sarà possibile visualizzare le informazioni seguenti sui dispositivi Zebra che usano batterie PowerPrecision e PowerPrecision+:
- Valutazione dello stato di integrità determinato da Zebra (solo batterie PowerPrecision+)
- Numero di cicli di ricarica completi utilizzati
- Data dell'ultima sincronizzazione per l'ultima batteria trovata nel dispositivo
- Numero di serie dell'ultima batteria trovata nel dispositivo

<!-- ***********************************************-->
## <a name="intune-apps"></a>App di Intune

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Distribuzione unificata di applicazioni Azure AD Enterprise e Office Online nel Portale aziendale di Windows<!-- 1817861  -->
Nella versione 2006 è stata annunciata la [distribuzione unificata di applicazioni Azure AD Enterprise e Office Online nel Portale aziendale](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal). Questa funzionalità sarà supportata nell'app Portale aziendale di Windows. Nel riquadro **Personalizzazione** di Intune sarà possibile selezionare **Nascondi** o **Mostra** sia per le**applicazioni aziendali di Azure AD** che per le **applicazioni di Office Online** nel Portale aziendale di Windows. Ogni utente visualizzerà l'intero catalogo applicazioni dal servizio Microsoft scelto. Per impostazione predefinita, ogni origine di app aggiuntiva verrà impostata su **Nascondi**. Per trovare questa impostazione di configurazione, nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Amministrazione del tenant** > **Personalizzazione**. Per informazioni correlate, vedere [Come personalizzare le app Portale aziendale Intune, il sito Web Portale aziendale e l'app Intune](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Monitorare e risolvere i problemi

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Modello di report di conformità Power BI V2.0<!-- 636958  -->
Gli amministratori potranno aggiornare il modello di report di conformità di Power BI da V1.0 a V2.0. V2.0 includerà una struttura migliorata e modifiche ai calcoli e ai dati esposti come parte del modello. Per informazioni correlate, vedere [Connettersi al data warehouse con Power BI](../developer/reports-proc-get-a-link-powerbi.md).


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Report nuovi e migliorati di Microsoft Defender Antivirus per Windows 10 e versioni successive<!-- 6018169  -->
Verranno aggiunti quattro nuovi report di Microsoft Defender antivirus in Windows 10, in **Sicurezza degli endpoint** > **Antivirus**.
- Due report operativi: *Dispositivi con malware rilevato* e *Stato dell'agente*.
- Due report dell'organizzazione: *Malware rilevato* e *Stato dell'agente*.

Ad esempio, il report operativo *Stato dell'agente* mostrerà il nome del dispositivo, il nome dell'utente, l'indirizzo di posta elettronica e l'UPN dell'utente, oltre a indicare se è abilitata la protezione in tempo reale e la protezione della rete. Quando questi report saranno disponibili per l'uso, verranno condivisi altri dettagli.

Per altre informazioni sulla sicurezza degli endpoint in Intune, vedere [Gestire la sicurezza degli endpoint in Microsoft Intune](../protect/endpoint-security.md).

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>Analizzare gli oggetti Criteri di gruppo locali usando Analisi di Criteri di gruppo (anteprima)<!--7200950 -->
In **Dispositivi** > **Analisi di Criteri di gruppo (anteprima)** è possibile importare gli oggetti Criteri di gruppo nell'interfaccia di amministrazione di Endpoint Manager. Quando si importa, Intune analizza automaticamente l'oggetto Criteri di gruppo e mostra i criteri con impostazioni equivalenti in Intune. Vengono mostrati anche gli oggetti Criteri di gruppo deprecati o non più supportati.

Si applica a:
- Windows 10 e versioni successive

#### <a name="new-windows-10-feature-update-report---6473121-----"></a>Nuovo report per gli aggiornamenti delle funzionalità di Windows 10<!-- 6473121   -->
Il report **Errori degli aggiornamenti delle funzionalità** fornirà dettagli sugli errori per i dispositivi a cui sono destinati i criteri **Aggiornamenti delle funzionalità di Windows 10** e che hanno tentato di eseguire un aggiornamento. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Dispositivi** > **Monitoraggio** > **Errori degli aggiornamenti delle funzionalità** per visualizzare questo report.

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Nuovo report per gli aggiornamenti delle funzionalità di Windows 10<!-- 6473128  -->
Il report **Aggiornamenti delle funzionalità di Windows** fornirà una visualizzazione generale della conformità per i dispositivi a cui sono destinati i criteri **Aggiornamenti delle funzionalità di Windows 10**. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Report** > **Aggiornamenti di Windows (anteprima)**  > **Errori degli aggiornamenti delle funzionalità** per visualizzare il riepilogo per questo report. Per visualizzare i report relativi a criteri specifici, selezionare la scheda **Report** e aprire il **report Aggiornamenti delle funzionalità di Windows**. 

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicurezza

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Supporto dei criteri di protezione delle app per Symantec Endpoint Security e Check Point Sandblast<!--  4452423, 4731168 -->

Nell'ottobre 2019 i criteri di protezione delle app di Intune hanno aggiunto la capacità per usare i dati di alcuni dei partner MTD (Microsoft Threat Defense). Verrà aggiunto il supporto per i partner seguenti per usare un criterio di protezione delle app per bloccare o cancellare in modo selettivo i dati aziendali dell'utente in base all'integrità di un dispositivo:

- **Check Point Sandblast** in Android, iOS e iPadOS
- **Symantec Endpoint Security** in Android, iOS e iPadOS

Per informazioni sull'uso dei criteri di protezione delle app con i partner MTD, vedere [Creare criteri di protezione delle app Mobile Threat Defense con Intune](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP crea un'attività di sicurezza di Endpoint Manager con i dettagli sulle vulnerabilità<!-- 5568193  -->
Lo strumento di gestione delle minacce e delle vulnerabilità in Microsoft Defender ATP rileva le impostazioni di sicurezza che non sono configurate correttamente nei dispositivi. Gli amministratori usano queste informazioni per aggiornare i dispositivi vulnerabili.

A breve Microsoft Defender ATP potrà generare un'attività di sicurezza di Endpoint Manager (**Endpoint Manager** > **Sicurezza degli endpoint** > **Attività di sicurezza**) con i dettagli sulle vulnerabilità e visualizzare i dispositivi interessati. Gli amministratori IT possono accettare l'attività di sicurezza e distribuire la configurazione richiesta. 

Per altre informazioni sulle attività di sicurezza, vedere [Usare Intune per risolvere le vulnerabilità identificate da Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Distribuzione migliorata dei certificati per Android Enterprise <!-- 6296499  -->
I dispositivi che eseguono i profili di lavoro completamente gestiti, dedicati e di proprietà aziendale di Android Enterprise saranno presto in grado di usare i certificati S/MIME per Outlook senza che un utente del dispositivo debba consentire l'accesso. I certificati S/MIME vengono distribuiti usando il profilo di certificato importato PKCS per la configurazione del dispositivo. (**Dispositivi** > **Profili di configurazione** > **Crea profilo** > **Android Enterprise** > **Certificato importato PKCS** nella categoria *Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale*).

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>Le opzioni a tre stati per le impostazioni provengono da criteri firewall di sicurezza degli endpoint<!-- 6586159   -->
Verrà aggiunto un terzo stato di configurazione per le impostazioni nei criteri firewall di sicurezza degli endpoint in cui la piattaforma (Windows o macOS) può supportare l'opzione aggiuntiva (**Sicurezza degli endpoint** > **Firewall**).

Ad esempio, se un'impostazione offre attualmente le opzioni **Non configurata** e **Sì**, se supportata dalla piattaforma, verrà aggiunta l'opzione **No**.

### <a name="new-security-baseline-for-office---3150261----"></a>Nuova baseline della sicurezza per Office<!-- 3150261  -->
Verrà aggiunta una nuova baseline di sicurezza (**Sicurezza degli endpoint** > **Baseline di sicurezza**) per gestire le impostazioni per *Microsoft Office O365*. Le impostazioni nella baseline includeranno le configurazioni per le app di Office, come *Gestione componenti aggiuntivi*, *Gestione MIME* e altre ancora.

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>Dettagli sullo stato migliorati nei report delle baseline della sicurezza<!-- 7221051    -->
Sono stati migliorati i dettagli sullo stato mostrati quando si visualizzano i risultati delle baseline di sicurezza distribuite. (**Sicurezza degli endpoint** > **Baseline di sicurezza** >  *selezionare un tipo di baseline di sicurezza, come*  **Baseline di sicurezza di Windows 10** > **Profili** > *selezionare un'istanza del profilo per visualizzarne lo stato* > *selezionare un report del profilo, come*  **Stato del dispositivo**)

I miglioramenti includeranno la modifica delle etichette e delle definizioni comuni usate per lo stato per adattarsi meglio alle finalità dello stato. Ad esempio:
- **Corrisponde alla baseline** diventerà **Matches default settings** (Corrisponde alle impostazioni predefinite), che descrive meglio l'intento di appurare quando una configurazione di dispositivi corrisponde alla configurazione della baseline predefinita (non modificata).
- L'opzione **Configurazione non valida** verrà suddivisa in dettagli più specifici, ad esempio **Errore**, **Conflitto** e **In sospeso**. I nuovi stati saranno coerenti con altre aree della console.

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>Autorizzazioni RBAC estese per il ruolo di sicurezza degli endpoint<!--7312374  idstaged -->
Il ruolo **Endpoint Security Manager** per Intune riceve le autorizzazioni di controllo degli accessi in base al ruolo aggiuntive per le attività remote. Questo ruolo concede l'accesso all'interfaccia di amministrazione di Microsoft Endpoint Manager e può essere usato da utenti che gestiscono le funzionalità di sicurezza e conformità, inclusi le baseline di sicurezza, la conformità dei dispositivi, l'accesso condizionale e Microsoft Defender Advanced Threat Protection.

Per visualizzare l'autorizzazione per un ruolo di controllo degli accessi in base al ruolo di Intune, passare a (**Amministratore tenant** > **Ruoli di Intune** > *selezionare un ruolo* > **Autorizzazioni**).

Le autorizzazioni estese per le attività remote sono le seguenti:

- Riavvia ora
- Blocco remoto
- Rotate BitLockerKeys (Preview) (Ruota le chiavi di BitLocker - anteprima)
- Rotate FileVault key
- Sync devices (Sincronizza dispositivi)
- Microsoft Defender
- Initiate Configuration Manger action (Avvia azione di Configuration Manager)

### <a name="updates-for-security-baselines---7102146-7103916----"></a>Aggiornamenti per le baseline di sicurezza<!-- 7102146, 7103916  -->
Verranno presto rilasciati aggiornamenti per le baseline di sicurezza seguenti (**Sicurezza degli endpoint** > **Baseline di sicurezza**):
- **Baseline di sicurezza di MDM** (sicurezza di Windows 10)
- **Baseline di Microsoft Defender ATP**

Le versioni aggiornate delle baseline offrono il supporto per le impostazioni recenti, consentendo di implementare le configurazioni consigliate dai rispettivi team di prodotto.

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>Usare i dettagli di configurazione della sicurezza degli endpoint per identificare l'origine dei conflitti di criteri per i dispositivi<!-- 7567503  idstaged  -->
Per facilitare la risoluzione dei conflitti, sarà presto possibile eseguire il drill-through in un profilo di baseline di sicurezza per visualizzare la *configurazione di sicurezza degli endpoint* per un dispositivo selezionato. Da qui sarà possibile selezionare le impostazioni che mostrano un *conflitto* o un *errore* e proseguire nell'esplorazione per visualizzare un elenco di dettagli che include i profili e i criteri che fanno parte del conflitto. Se poi si seleziona un criterio che rappresenta l'origine di un conflitto, Intune apre il riquadro Panoramica dei criteri da cui è possibile esaminare o modificare la configurazione dei criteri. (**Dispositivi** > *selezionare un dispositivo* > **Configurazione della sicurezza degli endpoint** > *selezionare un profilo o una baseline* > *selezionare un'impostazione nell'elenco di impostazioni applicate al dispositivo*).

I tipi di criteri seguenti possono essere identificati come un'origine di conflitto quando si esamina una baseline di sicurezza:
- Criterio di configurazione del dispositivo
- Criteri di sicurezza degli endpoint

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>Nuovi dettagli nella configurazione di sicurezza degli endpoint per un dispositivo<!-- 7745029   -->
Sono stati aggiunti nuovi dettagli per i dispositivi disponibili per la visualizzazione come parte di una configurazione di sicurezza degli endpoint dei dispositivi. (**Sicurezza degli endpoint** > **Baseline di sicurezza** > *baseline selezionata* > **Profili** > *profilo selezionato* > **Stato dispositivo** > **Configurazione della sicurezza degli endpoint**). I nuovi dettagli sono:

- **UPN** (nome dell'entità utente): l'UPN identifica il profilo di sicurezza degli endpoint assegnato a un determinato utente nel dispositivo. Questa informazione è utile per distinguere tra più utenti in un dispositivo e più voci di un profilo o di una baseline assegnata al dispositivo. 
- **Worst status** (Stato peggiore): questo dettaglio identifica la condizione di stato meno favorevole per il dispositivo. Quando questo stato è **Success** (Corretto), il dispositivo non presenta conflitti o errori dei criteri.

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>In Android 11 è deprecata la distribuzione di certificati radice attendibili nei dispositivi registrati dell'amministratore di dispositivi<!--7662775  -->
Con Android 11 i certificati radice attendibili non possono più essere distribuiti nei dispositivi registrati come *Amministratore di dispositivi Android*. Questa modifica non influisce sui dispositivi Samsung Knox grazie all'integrazione di Intune con la piattaforma Knox. Per i dispositivi non Samsung, gli utenti devono installare manualmente il certificato radice attendibile nel dispositivo. 

Con il certificato radice attendibile installato manualmente in un dispositivo, è quindi possibile usare SCEP per effettuare il provisioning dei certificati nel dispositivo. In questo scenario è comunque necessario creare e distribuire criteri di *certificato attendibile* nel dispositivo e collegare tali criteri al profilo di *certificato SCEP*.

- Se il certificato radice attendibile è disponibile nel dispositivo, il profilo di certificato SCEP verrà installato correttamente. 
- Se non è possibile trovare il certificato attendibile, l'installazione del profilo di certificato SCEP avrà esito negativo.

<!-- ***********************************************-->
## <a name="notices"></a>Notifiche

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sugli ultimi sviluppi, vedere [Novità di Microsoft Intune](whats-new.md).