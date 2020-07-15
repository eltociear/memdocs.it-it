---
title: Framework di configurazione della sicurezza di Android Enterprise
titleSuffix: Microsoft Intune
description: Informazioni sulle restrizioni e le impostazioni consigliate per la sicurezza di base ed elevata dei dispositivi Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05d0cb3db60ed0f54a66bc4128e5528e789537a8
ms.sourcegitcommit: d647eefa23c8849f49584442df568284d51d7525
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86195702"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Configurazioni di sicurezza del profilo di lavoro Android

Come parte del [framework di configurazione della sicurezza di Android Enterprise](android-configuration-framework.md), applicare le impostazioni seguenti per gli utenti di dispositivi mobili del profilo di lavoro di Android Enterprise. Per altre informazioni sull'impostazione di ogni criterio, vedere [Impostazioni di Android Enterprise per contrassegnare un dispositivo come conforme o non conforme in Intune](../protect/compliance-policy-create-android-for-work.md#work-profile) e [Impostazioni dei dispositivi Android Enterprise per consentire o limitare l'uso delle funzionalità tramite Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Quando si scelgono le impostazioni, assicurarsi di esaminare e classificare gli scenari di utilizzo. Quindi configurare gli utenti seguendo le istruzioni per il livello di sicurezza scelto. È possibile modificare le impostazioni suggerite in base alle esigenze dell'organizzazione. Assicurarsi che il team di sicurezza valuti l'ambiente di minaccia, la propensione al rischio e l'impatto sull'usabilità.

Per i dispositivi del profilo di lavoro di proprietà personale sono disponibili due framework di configurazione della sicurezza consigliati:

- [Sicurezza di base del profilo di lavoro (livello 1)](#work-profile-basic-security) 
- [Sicurezza elevata del profilo di lavoro (livello 3)](#work-profile-high-security) 

> [!Note]
> A causa delle impostazioni disponibili per i dispositivi di profilo di lavoro Android Enterprise, non esiste un'offerta di sicurezza avanzata (livello 2). Le impostazioni disponibili non giustificano una differenza tra il livello 1 e il livello 2.

## <a name="work-profile-basic-security"></a>Sicurezza di base del profilo di lavoro

Il livello 1 è la configurazione di sicurezza minima consigliata per i dispositivi personali in cui gli utenti accedono ai dati aziendali o dell'istituto di istruzione. Questa configurazione può essere applicata alla maggior parte degli utenti di dispositivi mobili. Alcuni dei controlli possono influire sull'esperienza utente.

### <a name="device-compliance"></a>Conformità del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Richiedi che il dispositivo si trovi al massimo al punteggio di rischio del computer | Non configurato ||
| Integrità dispositivi | Dispositivi rooted | Blocca ||
| Integrità dispositivi | Richiedi che il dispositivo si trovi al massimo al livello di minaccia del dispositivo | Non configurato||
| Integrità dispositivi | Google Play Services è configurato | Richiedi ||
| Integrità dispositivi | Provider di sicurezza aggiornato | Richiedi ||
| Integrità dispositivi | Attestazione del dispositivo SafetyNet | Verifica l'integrità di base e i dispositivi certificati | Questa impostazione configura l'attestazione SafetyNet di Google nei dispositivi degli utenti finali. L'integrità di base convalida l'integrità del dispositivo. Dispositivi rooted, emulatori, dispositivi virtuali e dispositivi con segni di manomissione non superano la verifica dell'integrità di base.<p>L'opzione Integrità di base e dispositivi certificati convalida la compatibilità del dispositivo con i servizi Google. Solo i dispositivi non modificati che hanno ottenuto la certificazione di Google possono superare questo controllo. |
| Proprietà dispositivo | Versione minima del sistema operativo | Formato: Major.Minor<br>Esempio: 5.0| Microsoft consiglia di configurare la versione principale minima di Android in modo che corrisponda alle versioni di Android supportate per le app Microsoft. Gli OEM e i dispositivi che rispettano i requisiti consigliati per Android Enterprise devono supportare la versione corrente con l'aggiornamento di una sola lettera. Attualmente Android consiglia Android 8.0 e versioni successive per i knowledge worker. Per i consigli più recenti su Android, vedere [Requisiti di Android Enterprise Recommended](https://www.android.com/enterprise/recommended/requirements/). |
| Proprietà dispositivo | Versione massima del sistema operativo | Non configurato ||
| Protezione del sistema | Richiedi una password per sbloccare i dispositivi mobili | Richiedi ||
| Protezione del sistema | Tipo di password richiesto | Complessa numerica | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Lunghezza minima password | 6 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Numero massimo di minuti di inattività prima che venga richiesta la password| 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password.|
| Protezione del sistema | Numero di giorni rimanenti prima della scadenza della password| Non configurato | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Numero di password precedenti di cui impedire il riutilizzo | Non configurato | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Crittografia dell'archivio dati nel dispositivo | Richiedi ||
| Protezione del sistema | Blocca app da origini sconosciute | Blocca ||
| Protezione del sistema | Integrità del runtime dell'app Portale aziendale | Richiedi ||
| Protezione del sistema | Blocca il debug USB nel dispositivo | Blocca | Sebbene questa impostazione blocchi il debug usando un dispositivo USB, disabilita anche la possibilità di raccogliere log che possono risultare utili per la risoluzione dei problemi. |
| Protezione del sistema | Livello minimo di patch di protezione | Non configurato | I dispositivi Android possono ricevere patch di sicurezza mensili, ma la versione dipende dagli OEM e/o dai gestori telefonici. Prima di implementare questa impostazione, le organizzazioni devono assicurarsi che i dispositivi Android distribuiti ricevano gli aggiornamenti della sicurezza. Per le versioni di patch più recenti, vedere i [bollettini sulla sicurezza di Android](https://source.android.com/security/bulletin/). |
| Azioni per la mancata conformità | Contrassegna il dispositivo come non conforme | Immediatamente | Per impostazione predefinita, i criteri sono configurati per contrassegnare il dispositivo come non conforme. Sono disponibili altre azioni. Per altre informazioni, vedere [Configurare azioni per i dispositivi non conformi in Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Limitazioni del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Impostazioni del profilo di lavoro | Copia e incolla tra il profilo di lavoro e il profilo personale | Blocca ||
| Impostazioni del profilo di lavoro | Condivisione dei dati tra i profili di lavoro e personali | Le app nel profilo di lavoro possono gestire una richiesta di condivisione dal profilo personale ||
| Impostazioni del profilo di lavoro | Notifiche del profilo di lavoro durante il blocco del dispositivo | Non configurato | Il blocco di questa impostazione garantisce che i dati sensibili non siano esposti nelle notifiche del profilo di lavoro, impedendo effetti sull'usabilità. |
| Impostazioni del profilo di lavoro | Autorizzazioni delle app predefinite | Impostazione predefinita dispositivo | Gli amministratori devono esaminare e modificare le autorizzazioni concesse dalle app che distribuiscono. |
| Impostazioni del profilo di lavoro | Aggiungi o rimuovi account | Blocca ||
| Impostazioni del profilo di lavoro | Contact sharing via Bluetooth (Contatto condivisione tramite Bluetooth) | Abilitare | Per impostazione predefinita, l'accesso ai contatti di lavoro non è disponibile in altri dispositivi, ad esempio in automobile tramite l'integrazione Bluetooth. L'abilitazione di questa impostazione migliora le esperienze utente in viva voce. Tuttavia, il dispositivo Bluetooth può memorizzare nella cache i contatti alla prima connessione. Quando viene implementata questa impostazione, le organizzazioni devono trovare un equilibrio tra scenari di usabilità e problemi di protezione dei dati. |
| Impostazioni del profilo di lavoro | Acquisizione schermo | Blocca ||
| Impostazioni del profilo di lavoro | Visualizzare l'ID chiamante del contatto di lavoro nel profilo personale | Non configurato ||
| Impostazioni del profilo di lavoro | Cerca contatti di lavoro dal profilo personale | Non configurato | Impedire agli utenti di accedere ai contatti di lavoro dal profilo personale può avere effetto in determinati scenari di usabilità, ad esempio le esperienze di messaggistica e di connessione all'interno del profilo personale. Quando viene implementata questa impostazione, le organizzazioni devono trovare un equilibrio tra scenari di usabilità e problemi di protezione dei dati. |
| Impostazioni del profilo di lavoro | Fotocamera | Non configurato ||
| Impostazioni del profilo di lavoro | Consenti i widget dalle app nel profilo di lavoro | Abilitare ||
| Impostazioni del profilo di lavoro | Richiedi la password del profilo di lavoro | Richiedi ||
| Impostazioni del profilo di lavoro | Lunghezza minima password | 6 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Numero massimo di minuti di inattività fino al blocco del profilo di lavoro| 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Numero di errori di accesso prima della cancellazione del profilo di lavoro| 10 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Scadenza password (giorni) | Non configurato | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Tipo di password richiesto | Complessa numerica ||
| Impostazioni del profilo di lavoro | Impedisci riutilizzo delle password precedenti | Non configurato | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password.|
| Impostazioni del profilo di lavoro | Sblocco con impronta digitale | Non configurato ||
| Impostazioni del profilo di lavoro | Smart Lock e altri agenti di attendibilità | Non configurato |||
| Password del dispositivo | Lunghezza minima password | 6 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Numero massimo di minuti di inattività fino al blocco dello schermo | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Numero di errori di accesso prima della cancellazione dei dati del dispositivo | 10 | Questa impostazione attiva una cancellazione del profilo di lavoro e non una cancellazione del dispositivo. |
| Password del dispositivo | Scadenza password (giorni) | Non configurato | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Tipo di password richiesto | Complessa numerica ||
| Password del dispositivo | Impedisci riutilizzo delle password precedenti | Non configurato | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Sblocco con impronta digitale | Non configurato ||
| Password del dispositivo | Smart Lock e altri agenti di attendibilità | Non configurato ||
| Protezione del sistema | Analisi delle minacce nelle app | Richiedi | Questa impostazione garantisce che l'analisi di verifica delle app di Google sia attivata per i dispositivi degli utenti finali. Se l'opzione è configurata, all'utente finale non sarà consentito l'accesso fino a quando non attiva l'analisi delle app di Google nel dispositivo Android. |
| Protezione del sistema | Impedisci le installazioni di app da origini sconosciute nel profilo personale | Blocca ||

> [!Note]
> Quando è abilitato il profilo di lavoro di Android Enterprise, per impostazione predefinita viene configurato "One Lock" per combinare i passcode del dispositivo e del profilo di lavoro. Se necessario, è possibile disabilitare One Lock per separare i passcode del dispositivo e del profilo di lavoro nelle impostazioni del profilo di lavoro.

## <a name="work-profile-high-security"></a>Sicurezza elevata del profilo di lavoro

Il livello 3 è la configurazione consigliata per i dispositivi usati da utenti o gruppi che sono esposti a un rischio particolarmente elevato, ad esempio utenti che gestiscono dati sensibili la cui divulgazione non autorizzata causa una perdita materiale considerevole. Un'organizzazione esposta agli attacchi di avversari ben finanziati e sofisticati necessita dei vincoli aggiuntivi descritti di seguito. Questa configurazione si espande alla configurazione nel livello 1:
- implementando Mobile Threat Defense o Microsoft Defender ATP.
- limitando gli scenari di dati del profilo di lavoro.
- applicando criteri password più avanzati.

Le impostazioni di criteri applicate nel livello 3 includono tutte le impostazioni di criteri consigliate per il livello 1. Tuttavia, le impostazioni elencate di seguito includono solo le impostazioni aggiunte o modificate. Queste impostazioni possono avere un effetto leggermente maggiore sugli utenti o sulle applicazioni. Consentono di applicare un livello di sicurezza più appropriato per i rischi per gli utenti che accedono a informazioni sensibili sui dispositivi mobili.

### <a name="device-compliance"></a>Conformità del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Richiedi che il dispositivo si trovi al massimo al punteggio di rischio del computer | Cancella | Questa impostazione richiede Microsoft Defender ATP. Per altre informazioni, vedere [Applicare la conformità per Microsoft Defender ATP con l'accesso condizionale in Intune](../protect/advanced-threat-protection.md).<p>I clienti dovrebbero prendere in considerazione l'implementazione di Microsoft Defender ATP o di una soluzione Mobile Threat Defense. Non è necessario distribuire entrambe le soluzioni. |
| Integrità dispositivi | Richiedi che il dispositivo si trovi al massimo al livello di minaccia del dispositivo | Protetto | Questa impostazione richiede un prodotto Mobile Threat Defense. Per altre informazioni, vedere [Mobile Threat Defense per i dispositivi registrati](../protect/mtd-device-compliance-policy-create.md).<p>I clienti dovrebbero prendere in considerazione l'implementazione di Microsoft Defender ATP o di una soluzione Mobile Threat Defense. Non è necessario distribuire entrambe le soluzioni.|
| Proprietà dispositivo | Versione minima del sistema operativo | Formato: Major.Minor<br>Esempio: 8.0| Microsoft consiglia di configurare la versione principale minima di Android in modo che corrisponda alle versioni di Android supportate per le app Microsoft. Gli OEM e i dispositivi che rispettano i requisiti consigliati per Android Enterprise devono supportare la versione corrente con l'aggiornamento di una sola lettera. Attualmente Android consiglia Android 8.0 e versioni successive per i knowledge worker. Per i consigli più recenti su Android, vedere Requisiti di Android Enterprise Recommended |
| Protezione del sistema | Numero di giorni rimanenti prima della scadenza della password | 365 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Numero di password precedenti di cui impedire il riutilizzo | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |


### <a name="device-restrictions"></a>Limitazioni del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Impostazioni del profilo di lavoro | Notifiche del profilo di lavoro durante il blocco del dispositivo | Blocca | Il blocco di questa impostazione garantisce che i dati sensibili non siano esposti nelle notifiche del profilo di lavoro, impedendo effetti sull'usabilità. |
| Impostazioni del profilo di lavoro | Contact sharing via Bluetooth (Contatto condivisione tramite Bluetooth) | Non configurato | Per impostazione predefinita, l'accesso ai contatti di lavoro non è disponibile in altri dispositivi, ad esempio in automobile tramite l'integrazione Bluetooth. L'abilitazione di questa impostazione migliora le esperienze utente in viva voce. Tuttavia, il dispositivo Bluetooth può memorizzare nella cache i contatti alla prima connessione. Quando viene implementata questa impostazione, le organizzazioni devono trovare un equilibrio tra scenari di usabilità e problemi di protezione dei dati. |
| Impostazioni del profilo di lavoro | Cerca contatti di lavoro dal profilo personale | Blocca | Impedire agli utenti di accedere ai contatti di lavoro dal profilo personale può avere effetto in determinati scenari di usabilità, ad esempio le esperienze di messaggistica e di connessione all'interno del profilo personale. Quando viene implementata questa impostazione, le organizzazioni devono trovare un equilibrio tra scenari di usabilità e problemi di protezione dei dati. |
| Impostazioni del profilo di lavoro | Consenti i widget dalle app nel profilo di lavoro | Non configurato ||
| Impostazioni del profilo di lavoro | Numero di errori di accesso prima della cancellazione del profilo di lavoro | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Scadenza password (giorni) | 365 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Impedisci riutilizzo delle password precedenti | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Impostazioni del profilo di lavoro | Smart Lock e altri agenti di attendibilità | Blocca ||
| Password del dispositivo | Numero di errori di accesso prima della cancellazione dei dati del dispositivo | 5 | Questa impostazione attiva una cancellazione del profilo di lavoro e non una cancellazione del dispositivo. |
| Password del dispositivo | Scadenza password (giorni) | 365 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Impedisci riutilizzo delle password precedenti | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |

## <a name="next-steps"></a>Passaggi successivi

Gli amministratori possono incorporare i livelli di configurazione illustrati all'interno della metodologia di distribuzione ad anelli per il test e l'uso in produzione importando i [modelli JSON di esempio del framework di configurazione della sicurezza di Android Enterprise](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) con gli [script PowerShell di Intune](https://github.com/microsoftgraph/powershell-intune-samples).
