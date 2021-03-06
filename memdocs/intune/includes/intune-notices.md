---
title: includere il file
description: Includere file
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: e63bb965b8fed4c0266e359493bbfa67100862cb
ms.sourcegitcommit: f575b13789185d3ac1f7038f0729596348a3cf14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/12/2020
ms.locfileid: "90045056"
---
Questi avvisi forniscono importanti informazioni utili per prepararsi per le modifiche e le funzionalità di Intune future.

### <a name="updated-end-user-experience-for-android-device-administrator-wi-fi-profiles---7662680----"></a>Aggiornamento dell'esperienza utente finale per i profili Wi-Fi con amministratore di dispositivi Android<!-- 7662680  -->
A causa di una modifica apportata da Google, l'esperienza dell'utente finale per i nuovi profili Wi-Fi è significativamente diversa a partire dalla versione di ottobre dell'app Portale aziendale. Gli utenti dovranno accettare altre autorizzazioni e accettare in modo esplicito le configurazioni Wi-Fi quando vengono distribuite. Le configurazioni Wi-Fi non verranno visualizzate nell'elenco delle reti Wi-Fi note, ma si connetteranno automaticamente quando sono nel campo. Non sono state apportate modifiche al comportamento per i profili Wi-Fi esistenti. Non sono state apportate modifiche neanche all'esperienza di amministrazione nell'interfaccia di amministrazione di Endpoint Manager.

Si applica a:
- Amministratore di dispositivi Android, Android 10 e versioni successive

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Microsoft Intune termina il supporto per Windows Phone 8.1 e Windows 10 Mobile<!-- 3544938, 3544909 -->
Il supporto Mainstream di Microsoft per Windows Phone 8.1 è terminato a luglio 2017 e il supporto "Extended" è terminato a giugno 2019. L'app Portale aziendale per Windows Phone 8.1 è inattiva da ottobre 2017. Microsoft Intune ha inoltre terminato il supporto per Windows Phone 8.1 il 20 febbraio 2020. 

Il supporto Mainstream Microsoft per Windows 10 Mobile è terminato nel dicembre 2019. Come indicato nel'informativa sul supporto, gli utenti di Windows 10 Mobile non saranno più idonei a ricevere nuovi aggiornamenti della sicurezza, hotfix non di sicurezza, opzioni di supporto tecnico gratuite o aggiornamenti del contenuto tecnico online da Microsoft. In base al supporto del sistema operativo per dispositivi mobili, Microsoft Intune termina il supporto del Portale aziendale sia per l'app Windows 10 Mobile che per il sistema operativo Windows 10 Mobile il 10 agosto 2020.

A partire dal 10 agosto, le registrazioni per i dispositivi Windows Phone 8.1 e Windows 10 Mobile avranno esito negativo e i tipi di profilo Windows Mobile verranno rimossi dall'interfaccia utente di Intune. I dispositivi già registrati non eseguiranno più la sincronizzazione con il servizio Intune e i dati dei dispositivi e dei criteri verranno eliminati.

### <a name="end-of-support-for-legacy-pc-management"></a>Termine del supporto per la gestione dei PC legacy

La gestione dei PC legacy non sarà più supportata a partire dal 15 ottobre 2020. Aggiornare i dispositivi a Windows 10 e registrarli nuovamente come dispositivi MDM perché continuino a essere gestiti da Intune.

[Altre informazioni](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Passare all'interfaccia di amministrazione di Microsoft Endpoint Manager per tutte le attività di gestione di Intune
Nel post MC208118 pubblicato lo scorso marzo è stato introdotto un nuovo URL semplice per Microsoft Endpoint Manager - Amministrazione Intune: [https://endpoint.microsoft.com](https://endpoint.microsoft.com). Microsoft Endpoint Manager è una piattaforma unificata che include Microsoft Intune e Configuration Manager. **A partire dal 1° agosto 2020**, l'amministrazione di Intune viene rimossa in [https://portal.azure.com](https://portal.azure.com) e si consiglia di usare invece [https://endpoint.microsoft.com](https://endpoint.microsoft.com) per tutte le attività di gestione degli endpoint. 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Riduzione del supporto per l'amministratore di dispositivi Android<!--7371518-->
La gestione degli amministratori di dispositivi Android è stata rilasciata in Android 2.2 come modo per gestire i dispositivi Android. Quindi, a partire da Android 5, è stato rilasciato il framework di gestione moderna di [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (per i dispositivi che possono connettersi in modo affidabile a Google Mobile Services). Google incoraggia l'abbandono della gestione di tipo amministratore di dispositivi riducendo il supporto per la gestione nelle nuove versioni di Android.

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?
A causa di queste modifiche di Google, a ottobre 2020 non saranno più disponibili funzionalità di gestione estese nei dispositivi interessati gestiti dall'amministratore del dispositivo. 

> [!NOTE]
> La data comunicata in precedenza era il quarto trimestre del 2020, ma è stata spostata in base alle [informazioni più recenti di Google](https://www.blog.google/products/android-enterprise/da-migration/).

##### <a name="device-types-that-will-be-impacted"></a>Tipi di dispositivi interessati
I dispositivi che saranno interessati dalla riduzione del supporto per l'amministratore del dispositivo sono quelli ai quali si applicano tutte e tre le condizioni seguenti:
- Registrato nella gestione di tipo amministratore di dispositivi.
- Esecuzione di Android 10 o versione successiva.
- Tutti i produttori Android, tranne Samsung.

I dispositivi non saranno interessati se hanno le caratteristiche seguenti:
- Non registrato nella gestione di tipo amministratore di dispositivi.
- Esecuzione di una versione di Android precedente a Android 10.
- Dispositivi Samsung. I dispositivi Samsung Knox non saranno interessati in questo intervallo di tempo perché viene fornito il supporto esteso tramite l'integrazione di Intune con la piattaforma Knox. Si ottiene così più tempo per pianificare la transizione dalla gestione di tipo amministratore di dispositivi per i dispositivi Samsung.

##### <a name="settings-that-will-be-impacted"></a>Impostazioni interessate
La [riduzione del supporto dell'amministratore del dispositivo di Google](https://developers.google.com/android/work/device-admin-deprecation) impedisce che la configurazione di queste impostazioni venga applicata ai dispositivi interessati.

###### <a name="configuration-profile-device-restriction-settings"></a>Impostazioni delle restrizioni relative ai dispositivi del profilo di configurazione

- Blocca **fotocamera**
- Impostare **Lunghezza minima password**
- Impostare **Numero di errori di accesso prima della cancellazione dei dati del dispositivo** (non si applica ai dispositivi senza una password impostata, ma si applica ai dispositivi con una password)
- Impostare **Scadenza password (giorni)**
- Impostare **Tipo di password richiesto**
- Impostare **Impedisci riutilizzo delle password precedenti**
- Blocca **Smart Lock e altri agenti di attendibilità**

###### <a name="compliance-policy-settings"></a>Impostazioni dei criteri di conformità

- Impostare **Tipo di password richiesto**
- Impostare **Lunghezza minima password**
- Impostare **Numero di giorni rimanenti prima della scadenza della password**
- Impostare **Numero di password precedenti di cui impedire il riutilizzo**


![Screenshot della pagina dei criteri di conformità di Android](../fundamentals/media/notices/android-compliance-settings.png)

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>Esperienza utente delle impostazioni interessate nei dispositivi interessati

Impostazioni di configurazione interessate:
- Per i dispositivi già registrati per cui sono già state applicate le impostazioni, le impostazioni di configurazione interessate continueranno a essere applicate.
- Per i nuovi dispositivi registrati, le nuove impostazioni assegnate e le impostazioni aggiornate, le impostazioni di configurazione interessate non verranno applicate (ma verranno applicate tutte le altre impostazioni di configurazione).

Impostazioni di conformità interessate:
- per i dispositivi già registrati per cui sono già state applicate le impostazioni, le impostazioni di conformità interessate verranno comunque visualizzate come motivi per la mancata conformità nella pagina "Aggiorna impostazioni del dispositivo", il dispositivo non sarà conforme e i requisiti per le password verranno comunque applicati nell'app Impostazioni.
- Per i nuovi dispositivi registrati, le nuove impostazioni assegnate e le impostazioni aggiornate, le impostazioni di conformità interessate verranno comunque visualizzate come motivi per la mancata conformità nella pagina "Aggiorna impostazioni del dispositivo" e il dispositivo non sarà conforme, ma i requisiti per le password più restrittivi non verranno applicati nell'app Impostazioni.

Ulteriore modifica dell'esperienza utente per i profili Wi-Fi
- Gli utenti dovranno accettare altre autorizzazioni e accettare in modo esplicito le configurazioni Wi-Fi quando vengono distribuite. Le configurazioni Wi-Fi non verranno visualizzate nell'elenco delle reti Wi-Fi note, ma si connetteranno automaticamente quando sono nel campo. Non sono state apportate modifiche al comportamento per i profili Wi-Fi esistenti. Non sono state apportate modifiche neanche all'esperienza di amministrazione nell'interfaccia di amministrazione di Endpoint Manager.  

#### <a name="cause-of-impact"></a>Causa degli effetti 
I dispositivi inizieranno a essere interessati a ottobre 2020. A questo punto, verrà reso disponibile un aggiornamento dell'app Portale aziendale che aumenterà l'API di Portale aziendale di destinazione dal livello 28 al livello 29 ([come richiesto da Google](https://www.blog.google/products/android-enterprise/da-migration/)). 

A questo punto, i dispositivi con gestione di tipo amministratore di dispositivi non prodotti da Samsung saranno interessati quando l'utente esegue entrambe le azioni seguenti:
- Aggiornamento ad Android 10 o versioni successive.
- Aggiornamento dell'app Portale aziendale alla versione destinata al livello API 29.

#### <a name="additional-impacts-based-on-android-os-version"></a>Ulteriori conseguenze in base alla versione del sistema operativo Android 
**Android 10**: per tutti i dispositivi con gestione di tipo amministratore di dispositivi (inclusi Samsung) con Android 10 e versioni successive, Google ha limitato la capacità degli agenti di gestione di tipo amministratore di dispositivi, come il Portale aziendale, di accedere alle informazioni relative all'identificatore del dispositivo. Dopo l'aggiornamento di un dispositivo ad Android 10 o versione successiva, questa limitazione influisce sulle funzionalità di Intune seguenti: 
- Il controllo di accesso alla rete per la rete VPN non funzionerà più 
- L'identificazione dei dispositivi come di proprietà dell'azienda con l'IMEI o il numero di serie non contrassegnerà automaticamente i dispositivi come di proprietà dell'azienda 
- L'IMEI e il numero di serie non saranno più visibili agli amministratori IT in Intune 

**Android 11**: di seguito sono indicate le modifiche che avranno effetto sul dispositivo gestito dall'amministratore dei dispositivi con l'aggiornamento ad Android 11: 
- Per i dispositivi con amministratore di dispositivi (escluso Samsung) che eseguono Android 11 e versioni successive, Google ha rimosso la possibilità per gli agenti di gestione come Portale aziendale di imporre il blocco della fotocamera, anche prima dell'aggiornamento di ottobre dell'app Portale aziendale. I criteri di blocco della fotocamera applicati ai dispositivi prima dell'aggiornamento ad Android 11 continueranno a essere applicati.  
- Con Android 11 i certificati radice attendibili non possono più essere distribuiti nei dispositivi registrati con amministratore di dispositivi, ad eccezione dei dispositivi Samsung. Gli utenti devono installare manualmente il certificato radice attendibile nel dispositivo. Con il certificato radice attendibile installato manualmente in un dispositivo, è quindi possibile usare SCEP per effettuare il provisioning dei certificati nel dispositivo. In questo scenario è comunque necessario creare e distribuire criteri di certificato attendibile nel dispositivo e collegare tali criteri al profilo di certificato SCEP. 
    - Se il certificato radice attendibile è disponibile nel dispositivo, il profilo di certificato SCEP verrà installato correttamente.  
    - Se non è possibile trovare il certificato attendibile, l'installazione del profilo di certificato SCEP avrà esito negativo. 


#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica
Per evitare la riduzione di funzionalità prevista a ottobre 2020, è consigliabile attenersi alle indicazioni seguenti:
- **Nuove registrazioni**: eseguire l'onboarding di nuovi dispositivi nella gestione [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (dove disponibile) e/o con [criteri di protezione delle app](../apps/app-protection-policies.md). Evitare l'onboarding di nuovi dispositivi nella gestione di tipo amministratore di dispositivi. 
- **Dispositivi registrati in precedenza**: se un dispositivo con gestione di tipo amministratore di dispositivi esegue Android 10 o versione successiva oppure può eseguire l'aggiornamento a Android 10 o versione successiva (soprattutto se non è un dispositivo Samsung), spostarlo dalla gestione di tipo amministratore di dispositivi alla gestione [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) e/o con [criteri di protezione delle app](../apps/app-protection-policies.md). È possibile sfruttare il flusso semplificato per [passare i dispositivi Android dalla gestione di tipo amministratore di dispositivi alla gestione con profilo di lavoro](../enrollment/android-move-device-admin-work-profile.md).
- **Configurare la complessità della password**: per i dispositivi interessati che eseguono Android 10 e versioni successive, un'impostazione futura denominata Complessità password consente di continuare a applicare le restrizioni e la conformità delle password. La complessità delle password è una misura del livello di sicurezza delle password costituito da tipo, lunghezza e qualità della password.

#### <a name="what-if-i-have-non-samsung-devices-that-cannot-move-to-android-enterprise"></a>Cosa accade per i dispositivi non Samsung che non possono essere spostati in Android Enterprise? 
Alcuni dispositivi non possono passare dalla gestione con amministratore di dispositivi alla gestione con Android Enterprise. Ad esempio, [Google non ha reso disponibile Android Enterprise in alcuni mercati](https://support.google.com/work/android/answer/6270910?hl=en). È comunque possibile continuare a usare Intune per gestire i dispositivi non Samsung con l'amministratore di dispositivi, ma verranno applicate le modifiche apportate alle funzionalità indicate in questo post. Per informazioni sulla gestione dei dispositivi quando Android Enterprise non è disponibile, vedere [Come usare Intune in ambienti senza i servizi Google Mobile Services](../apps/manage-without-gms.md). 


#### <a name="additional-information"></a>Informazioni aggiuntive
- [Aggiornare i dispositivi Android da amministratore di dispositivi alla gestione del profilo di lavoro](../enrollment/android-move-device-admin-work-profile.md)
- [Configurare la registrazione dei dispositivi con profilo di lavoro Android Enterprise](../enrollment/android-work-profile-enroll.md)
- [Configurare la registrazione di dispositivi Android Enterprise dedicati](../enrollment/android-kiosk-enroll.md)
- [Configurare la registrazione in Intune di dispositivi Android Enterprise completamente gestiti](../enrollment/android-fully-managed-enroll.md)
- [Come creare e assegnare criteri di protezione delle app](../apps/app-protection-policies.md)
- [Come usare Intune in ambienti senza i servizi Google Mobile Services](../apps/manage-without-gms.md)
- [Informazioni sui criteri di protezione delle app e i profili di lavoro nei dispositivi Android Enterprise](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Blog di Google sulle informazioni che è necessario conoscere sulla deprecazione della gestione di tipo amministratore di dispositivi](https://www.blog.google/products/android-enterprise/da-migration/)
- [Indicazioni di Google per la migrazione da amministratore di dispositivi ad Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Documentazione di Google relativa alle API dell'amministratore di dispositivi deprecate](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>Modifica prevista: Aggiornamento del flusso di registrazione di Intune per Registrazione automatica dei dispositivi di Apple per iOS/iPadOS
Nella versione di luglio di Portale aziendale verrà modificato il flusso di registrazione di iOS/iPadOS per Registrazione automatica dei dispositivi di Apple (funzionalità nota in precedenza come DEP). La modifica del flusso di registrazione viene rilevata solo durante il flusso "Registra con affinità utente". In precedenza, se si imposta "Installare l'app Portale aziendale" su "No" come parte della configurazione, gli utenti potrebbero comunque installare l'app Portale aziendale dallo Store e in questo modo verrebbe attivata la registrazione durante la quale l'utente aggiungerebbe il numero di serie appropriato. Con questa prossima versione di Portale aziendale, verrà rimossa la schermata di conferma del numero di serie. Sarà invece consigliabile creare un criterio di configurazione dell'app corrispondente da inviare insieme all'app Portale aziendale per assicurarsi che gli utenti possano eseguire correttamente la registrazione o impostare "Installare l'app Portale aziendale" su "Sì" come parte della configurazione. 
 - Per altre informazioni, vedere il post [qui](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629).
