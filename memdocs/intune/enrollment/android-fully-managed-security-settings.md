---
title: Configurazioni di sicurezza di dispositivi Android Enterprise completamente gestiti
titleSuffix: Microsoft Intune
description: Informazioni sulle impostazioni consigliate per la sicurezza di base, avanzata ed elevata dei dispositivi Android Enterprise completamente gestiti.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
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
ms.openlocfilehash: a4c2a9aa48d17b9cb2b386a4e4cb4df8fb36caac
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502988"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Configurazioni di sicurezza di dispositivi Android Enterprise completamente gestiti

Come parte del [framework di configurazione della sicurezza di Android Enterprise](android-configuration-framework.md), applicare le impostazioni seguenti per gli utenti di dispositivi mobili Android Enterprise completamente gestiti. Per altre informazioni sull'impostazione di ogni criterio, vedere [Impostazioni del proprietario del dispositivo Android Enterprise per contrassegnare i dispositivi come conformi o non conformi tramite Intune](../protect/compliance-policy-create-android-for-work.md#device-owner) e [Impostazioni dei dispositivi Android Enterprise per consentire o limitare l'uso delle funzionalità tramite Intune](../configuration/device-restrictions-android-for-work.md#device-owner-only).

Quando si scelgono le impostazioni, assicurarsi di esaminare e classificare gli scenari di utilizzo. Quindi configurare gli utenti seguendo le istruzioni per il livello di sicurezza scelto. È possibile modificare le impostazioni suggerite in base alle esigenze dell'organizzazione. Assicurarsi che il team di sicurezza valuti l'ambiente di minaccia, la propensione al rischio e l'impatto sull'usabilità.

Per i dispositivi completamente gestiti di proprietà dell'azienda sono disponibili tre framework di configurazione della sicurezza consigliati:

- [Sicurezza di base completamente gestita (livello 1)](#fully-managed-basic-security) 
- [Sicurezza avanzata completamente gestita (livello 2)](#fully-managed-enhanced-security)
- [Sicurezza elevata completamente gestita (livello 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Sicurezza di base completamente gestita

Il livello 1 è la configurazione di sicurezza minima consigliata per i dispositivi mobili di proprietà dell'organizzazione.

I criteri del livello 1 applicano un livello di accesso ai dati ragionevole riducendo al minimo l'effetto sugli utenti. Questa operazione viene eseguita applicando criteri password, una versione minima del sistema operativo, l'attestazione del dispositivo SafetyNet e la disabilitazione di determinate funzioni del dispositivo (ad esempio i trasferimenti di file USB). 

### <a name="device-compliance"></a>Conformità del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Richiedi che il dispositivo si trovi al massimo al punteggio di rischio del computer | Non configurato ||
| Integrità dispositivi | Richiedi che il dispositivo si trovi al massimo al livello di minaccia del dispositivo | Non configurato||
| Integrità dispositivi | Attestazione del dispositivo SafetyNet | Verifica l'integrità di base e i dispositivi certificati | Questa impostazione configura l'attestazione SafetyNet di Google nei dispositivi degli utenti finali. L'integrità di base convalida l'integrità del dispositivo. Dispositivi rooted, emulatori, dispositivi virtuali e dispositivi con segni di manomissione non superano la verifica dell'integrità di base.<br>L'opzione Integrità di base e dispositivi certificati convalida la compatibilità del dispositivo con i servizi Google. Solo i dispositivi non modificati che hanno ottenuto la certificazione di Google possono superare questo controllo. |
| Proprietà dispositivo | Versione minima del sistema operativo | Formato: Major.Minor<br>Esempio: 8.0| Microsoft consiglia di configurare la versione principale minima di Android in modo che corrisponda alle versioni di Android supportate per le app Microsoft. Gli OEM e i dispositivi che rispettano i requisiti consigliati per Android Enterprise devono supportare la versione corrente con l'aggiornamento di una sola lettera. Attualmente Android consiglia Android 8.0 e versioni successive per i knowledge worker. Per i consigli più recenti su Android, vedere [Requisiti di Android Enterprise Recommended](https://www.android.com/enterprise/recommended/requirements/). |
| Proprietà dispositivo | Versione massima del sistema operativo | Non configurato ||
| Proprietà dispositivo | Livello minimo di patch di protezione | Non configurato | I dispositivi Android possono ricevere patch di sicurezza mensili, ma la versione dipende dagli OEM e/o dai gestori telefonici. Prima di implementare questa impostazione, le organizzazioni devono assicurarsi che i dispositivi Android distribuiti ricevano gli aggiornamenti della sicurezza. Per le versioni di patch più recenti, vedere i [bollettini sulla sicurezza di Android](https://source.android.com/security/bulletin/). |
| Protezione del sistema | Richiedi una password per sbloccare i dispositivi mobili | Richiedi ||
| Protezione del sistema | Tipo di password richiesto | Complessa numerica | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Lunghezza minima password | 6 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema | Numero massimo di minuti di inattività prima che venga richiesta la password| 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password.|
| Protezione del sistema | Numero di giorni rimanenti prima della scadenza della password| Non configurato ||
| Protezione del sistema |    Numero di password obbligatorie prima che un utente possa riutilizzare una password | Non configurato ||
| Protezione del sistema | Crittografia dell'archivio dati nel dispositivo | Richiedi ||
| Azioni per la mancata conformità | Contrassegna il dispositivo come non conforme | Immediatamente | Per impostazione predefinita, i criteri sono configurati per contrassegnare il dispositivo come non conforme. Sono disponibili altre azioni. Per altre informazioni, vedere [Configurare azioni per i dispositivi non conformi in Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Limitazioni del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Generale | Acquisizione schermo | Non configurato ||
| Generale | Fotocamera | Non configurato ||
| Generale | Criteri di autorizzazione predefiniti | Impostazione predefinita dispositivo ||
| Generale | Modifiche a data e ora | Non configurato ||
| Generale | Modifiche al volume | Non configurato ||
| Generale | Ripristino delle impostazioni di fabbrica | Blocca ||
| Generale | Modalità provvisoria | Blocca ||
| Generale | Status bar | Non configurato ||
| Generale | Servizi per dati in roaming | Non configurato ||
| Generale | Modifiche alle impostazioni Wi-Fi | Non configurato ||
| Generale | Configurazione Bluetooth | Non configurato ||
| Generale | Tethering e accesso a hotspot | Non configurato ||
| Generale | Archiviazione USB | Non configurato ||
| Generale | Trasferimento di file su USB | Blocca ||
| Generale | Supporti esterni | Blocca ||
| Generale | Trasmetti dati con NFC | Non configurato ||
| Generale | Funzionalità di debug | Non configurato ||
| Generale | Regolazione del microfono | Non configurato ||
| Generale | Indirizzi di posta elettronica per la protezione dal ripristino delle impostazioni predefinite | Non configurato ||
| Generale | Rete di emergenza | Non configurato ||
| Generale | Aggiornamento del sistema | Automatico ||
| Generale | Finestre di notifica | Non configurato ||
| Generale | Ignora suggerimenti al primo utilizzo | Non configurato ||
| Protezione del sistema | Analisi delle minacce nelle app |Richiedi ||
| Esperienza del dispositivo | Tipo di profilo di registrazione | Completamente gestito ||
| Esperienza del dispositivo | Imposta Microsoft Launcher come utilità di avvio predefinita | Non configurato | Le organizzazioni possono scegliere di implementare Microsoft Launcher per garantire un'esperienza della schermata iniziale coerente nei dispositivi completamente gestiti. Per altre informazioni, vedere [Come configurare Microsoft Launcher nei dispositivi Android Enterprise completamente gestiti con Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) |
| Password | Disabilita la schermata di blocco | Non configurato ||
| Password | Funzionalità disabilitate della schermata di blocco | 0 selezionato ||
| Password | Tipo di password richiesto | Complessa numerica ||
| Password | Lunghezza minima password | 6 ||
| Password | Numero di giorni rimanenti prima della scadenza della password | Non configurato ||
| Password | Numero di password obbligatorie prima che un utente possa riutilizzare una password | Non configurato ||
| Password | Numero di errori di accesso prima della cancellazione dei dati del dispositivo | 10 ||
| Impostazioni di risparmio energia | Tempo per la schermata di blocco | 5 ||
| Impostazioni di risparmio energia | Schermata attivata con dispositivo collegato | Non configurato ||
| Utenti e account | Aggiungi nuovi utenti | Non configurato ||
| Utenti e account | Rimozione degli utenti | Non configurato ||
| Utenti e account | Modifiche dell'account (solo per dispositivi dedicati) | Non configurato ||
| Utenti e account | Account Google personale | Non configurato ||
| Utenti e account | L'utente può configurare le credenziali | Blocca ||
| Applicazioni | Consenti l'installazione da origini sconosciute | Non configurato ||
| Applicazioni | Consenti l'accesso a tutte le app in Google Play Store | Non configurato | Per impostazione predefinita, gli utenti non possono installare app personali da Google Play Store nei dispositivi completamente gestiti. Se le organizzazioni vogliono consentire l'uso personale dei dispositivi completamente gestiti, provare a modificare questa impostazione. |
| Applicazioni | Aggiornamenti automatici delle app | Solo Wi-Fi | Le organizzazioni devono modificare questa impostazione in base alle esigenze poiché possono verificarsi addebiti del piano dati se gli aggiornamenti delle app vengono eseguiti sulla rete cellulare. |

## <a name="fully-managed-enhanced-security"></a>Sicurezza avanzata completamente gestita

Il livello 2 è la configurazione consigliata per i dispositivi usati per accedere a informazioni più sensibili. Questi dispositivi sono attualmente un bersaglio classico nelle aziende. Queste impostazioni non presuppongono un numero elevato di personale di sicurezza altamente qualificato. Pertanto, dovrebbero essere accessibili alla maggior parte delle organizzazioni aziendali. Questa configurazione si espande alla configurazione nel livello 1 applicando criteri password più avanzati e disabilitando le funzionalità utente/account.

Le impostazioni di livello 2 includono tutte le impostazioni dei criteri consigliate per il livello 1. Tuttavia, le impostazioni elencate di seguito includono solo le impostazioni aggiunte o modificate. Queste impostazioni possono avere un effetto leggermente maggiore sugli utenti o sulle applicazioni. Consentono di applicare un livello di sicurezza più appropriato per i rischi per gli utenti che accedono a informazioni sensibili sui dispositivi mobili.

### <a name="device-compliance"></a>Conformità del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Protezione del sistema | Numero di giorni rimanenti prima della scadenza della password | 365 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Protezione del sistema |    Numero di password obbligatorie prima che un utente possa riutilizzare una password | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |

### <a name="device-restrictions"></a>Limitazioni del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Generale | Indirizzi di posta elettronica per la protezione dal ripristino delle impostazioni predefinite | Indirizzi di posta elettronica dell'account Google ||
| Generale | Elenco di indirizzi di posta elettronica (opzione solo per gli indirizzi di posta elettronica dell'account Google) | example@gmail.com | Aggiornare manualmente questo criterio per specificare gli indirizzi di posta elettronica di Google degli amministratori di dispositivi che possono sbloccare i dispositivi dopo che sono stati cancellati. |
| Password del dispositivo | Numero di giorni rimanenti prima della scadenza della password | 365 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Numero di password obbligatorie prima che un utente possa riutilizzare una password | 5 | È possibile che le organizzazioni debbano aggiornare questa impostazione in modo che corrisponda ai criteri delle password. |
| Password del dispositivo | Numero di errori di accesso prima della cancellazione dei dati del dispositivo | 5 ||
| Utenti e account | Aggiungi nuovi utenti | Blocca ||
| Utenti e account | Rimozione degli utenti | Blocca ||
| Utenti e account | Account Google personale | Blocca ||

## <a name="fully-managed-high-security"></a>Sicurezza elevata completamente gestita

Il livello 3 è la configurazione consigliata per:
- organizzazioni con sistemi di sicurezza sofisticati di ampia portata.
- utenti e gruppi specifici che possono essere facilmente bersaglio di attacchi.
Questo tipo di organizzazioni sono in genere esposte agli attacchi di avversari ben finanziati e sofisticati. Per questa ragione, hanno bisogno dei vincoli e dei controlli aggiuntivi descritti di seguito.

Questa configurazione si espande al livello 2:
- richiedendo una versione minima del sistema operativo superiore.
- assicurandosi che il dispositivo sia conforme applicando il livello di Microsoft Defender ATP o Mobile Threat Defense più sicuro.
- richiedendo una versione minima del sistema operativo superiore.
- applicando restrizioni del dispositivo aggiuntive, ad esempio la disabilitazione delle notifiche non modificate nella schermata di blocco.
- richiedendo che le app siano sempre aggiornate. 

Le impostazioni di criteri applicate nel livello 3 includono tutte le impostazioni di criteri consigliate per il livello 2. Le impostazioni elencate di seguito includono solo le impostazioni aggiunte o modificate. Queste impostazioni possono avere un impatto significativo sugli utenti o sulle applicazioni. Applicano un livello di sicurezza più adeguato ai rischi che devono affrontare le organizzazioni.


### <a name="device-compliance"></a>Conformità del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Richiedi che il dispositivo si trovi al massimo al punteggio di rischio del computer | Cancella | Questa impostazione richiede Microsoft Defender ATP. Per altre informazioni, vedere [Applicare la conformità per Microsoft Defender ATP con l'accesso condizionale in Intune](../protect/advanced-threat-protection.md).<p> I clienti dovrebbero prendere in considerazione l'implementazione di Microsoft Defender ATP o di una soluzione Mobile Threat Defense. Non è necessario distribuire entrambe le soluzioni. |
| Integrità dispositivi | Richiedi che il dispositivo si trovi al massimo al livello di minaccia del dispositivo | Protetto | Questa impostazione richiede un prodotto Mobile Threat Defense. Per altre informazioni, vedere [Mobile Threat Defense per i dispositivi registrati](../protect/mtd-device-compliance-policy-create.md).<p>I clienti dovrebbero prendere in considerazione l'implementazione di Microsoft Defender ATP o di una soluzione Mobile Threat Defense. Non è necessario distribuire entrambe le soluzioni.|
| Proprietà dispositivo | Versione minima del sistema operativo | Formato: Major.Minor<br>Esempio: 10.0| Microsoft consiglia di configurare la versione principale minima di Android in modo che corrisponda alle versioni di Android supportate per le app Microsoft. Gli OEM e i dispositivi che rispettano i requisiti consigliati per Android Enterprise devono supportare la versione corrente con l'aggiornamento di una sola lettera. Attualmente Android consiglia Android 8.0 e versioni successive per i knowledge worker. Per i consigli più recenti su Android, vedere Requisiti di Android Enterprise Recommended |

### <a name="device-restrictions"></a>Limitazioni del dispositivo

| Sezione | Impostazione | Valore | Note |
| ----- | ----- | ----- | ----- |
| Generale | Modifiche a data e ora | Blocca ||
| Generale | Tethering e accesso a hotspot | Blocca ||
| Generale | Trasmetti dati con NFC | Blocca ||
| Password del dispositivo | Funzionalità disabilitate della schermata di blocco | Ritieni attendibili gli agenti, Notifiche non modificate ||
| Applicazioni | Aggiornamenti automatici delle app | Sempre | Le organizzazioni devono modificare questa impostazione in base alle esigenze poiché possono verificarsi addebiti del piano dati se gli aggiornamenti delle app vengono eseguiti sulla rete cellulare. |


## <a name="next-steps"></a>Passaggi successivi

Gli amministratori possono incorporare i livelli di configurazione illustrati all'interno della metodologia di distribuzione ad anelli per il test e l'uso in produzione importando i [modelli JSON di esempio del framework di configurazione della sicurezza di Android Enterprise](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) con gli [script PowerShell di Intune](https://github.com/microsoftgraph/powershell-intune-samples).
