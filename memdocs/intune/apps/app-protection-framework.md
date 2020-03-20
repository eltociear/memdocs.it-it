---
title: Framework di protezione dei dati con criteri di protezione delle app
titleSuffix: Microsoft Intune
description: Informazioni su come i criteri di protezione delle app garantiscono che i dati di un'organizzazione rimangano protetti o contenuti in un'app gestita, indipendentemente dal fatto che il dispositivo sia registrato.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: cfb0012dfc2cedb72c64a54c16b567dffff84c9e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342296"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>Framework di protezione dei dati con criteri di protezione delle app 

Poiché più organizzazioni implementano strategie per l'accesso ai dati dell'azienda o dell'istituto di istruzione da dispositivi mobili, la protezione dalla perdita di dati assume un'importanza fondamentale. Per la protezione dalla perdita di dati, Intune offre una soluzione di gestione delle applicazioni mobili basata sui criteri di protezione delle app. Si tratta di regole che assicurano che i dati di un'organizzazione rimangano protetti o contenuti in un'app gestita, indipendentemente dal fatto che il dispositivo sia registrato. Per altre informazioni, vedere [Panoramica dei criteri di protezione app](app-protection-policy.md).

Quando si configurano i criteri di protezione delle app, le diverse impostazioni e opzioni consentono alle organizzazioni di adattare la protezione alle esigenze specifiche. Grazie a questa flessibilità, potrebbe non essere semplice individuare quale permutazione delle impostazioni dei criteri è necessaria per implementare uno scenario completo. Per consentire alle organizzazioni di definire le priorità per la protezione avanzata degli endpoint client, Microsoft ha introdotto una nuova tassonomia per le [configurazioni di sicurezza in Windows 10](https://aka.ms/secconframework) e Intune adotta una tassonomia simile per il framework di protezione dei dati con criteri di protezione delle app per la gestione delle app per dispositivi mobili.  

Il framework di configurazione per la protezione dei dati con criteri di protezione delle app è organizzato in tre scenari di configurazione distinti:

- Livello 1 - Protezione di base dei dati aziendali: Microsoft consiglia questa configurazione come configurazione di protezione dei dati minima per un dispositivo aziendale.

- Livello 2 - Protezione avanzata dei dati aziendali: Microsoft consiglia questa configurazione per i dispositivi in cui gli utenti accedono a informazioni riservate. Questa configurazione è applicabile alla maggior parte degli utenti di dispositivi mobili che accedono ai dati aziendali o dell'istituto di istruzione. Alcuni dei controlli possono influire sull'esperienza utente.

- Livello 3 - Protezione elevata dei dati aziendali: Microsoft consiglia questa configurazione per i dispositivi gestiti da un'organizzazione con un team di sicurezza più ampio o più sofisticato oppure per utenti o gruppi specifici che sono esposti a un rischio particolarmente elevato, ad esempio nel caso di un'organizzazione con utenti che gestiscono dati il cui furto ha un impatto diretto e significativo sulla quotazione azionaria. È probabile che un'organizzazione esposta agli attacchi di avversari ben finanziati e sofisticati sia interessata ad adottare questa configurazione.

## <a name="app-data-protection-framework-deployment-methodology"></a>Metodologia di distribuzione del framework di protezione dei dati con criteri di protezione delle app

Come per qualsiasi distribuzione di nuovo software, funzionalità o impostazioni, Microsoft consiglia di investire in una metodologia ad anelli per eseguire una convalida di test prima di distribuire il framework di protezione dei dati con criteri di protezione delle app. La definizione degli anelli di distribuzione è in genere un evento singolo (o almeno poco frequente), ma il personale IT deve rivedere questi gruppi per assicurarsi che la sequenziazione sia ancora corretta.

Microsoft consiglia il seguente approccio basato su anelli di distribuzione per il framework di protezione dei dati con criteri di protezione delle app:

| Anello di distribuzione  | Tenant  | Team di valutazione  | Output  | Sequenza temporale  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Controllo di qualità  | Tenant di pre-produzione  | Proprietari della capacità mobile, sicurezza, valutazione dei rischi, privacy, esperienza utente  | Convalida dello scenario funzionale, bozza della documentazione  | Da 0 a 30 giorni  |
| Anteprima  | Tenant di produzione  | Proprietari della capacità mobile, esperienza utente  | Convalida dello scenario per utenti finali, documentazione per l'utente  | Da 7 a 14 giorni, dopo controllo di qualità  |
| Produzione  | Tenant di produzione  | Proprietari della capacità mobile, help desk IT  | N/D  | Da 7 giorni a diverse settimane, dopo anteprima  |

Come indicato nella tabella, è necessario eseguire tutte le modifiche apportate ai criteri di protezione delle app in un ambiente di pre-produzione per comprendere le implicazioni legate all'impostazione dei criteri. Al termine del test, le modifiche possono essere spostate nell'ambiente di produzione e applicate a un subset di utenti di produzione, in genere il reparto IT e altri gruppi pertinenti. L'implementazione può infine essere estesa al resto della community degli utenti di dispositivi mobili. L'implementazione nell'ambiente di produzione può richiedere più tempo a seconda del livello di impatto delle modifiche. Se non è previsto un impatto sugli utenti, l'implementazione delle modifiche dovrebbe essere rapida. Se invece le modifiche hanno un impatto sugli utenti, l'implementazione potrebbe essere più lenta a causa della necessità di comunicare le modifiche a tutti gli utenti.

Durante il test delle modifiche ai criteri di protezione delle app, tenere presenti i [tempi di distribuzione](app-protection-policy-delivery.md). Lo stato della distribuzione dei criteri di protezione delle app per un determinato utente può essere monitorato. Per altre informazioni, vedere [Come monitorare i criteri di protezione delle app](app-protection-policies-monitor.md).

Le singole impostazioni dei criteri di protezione per ogni app possono essere convalidate nei dispositivi tramite Edge e l'URL *about:Intunehelp*. Per altre informazioni, vedere [Esaminare i log di protezione delle app client](app-protection-policy-settings-log.md) e [Gestire l'accesso Web usando Microsoft Edge con Microsoft Intune](manage-microsoft-edge.md#use-microsoft-edge-on-ios-to-access-managed-app-logs).

## <a name="app-data-protection-framework-settings"></a>Impostazioni del framework di protezione dei dati con criteri di protezione delle app

Le impostazioni dei criteri di protezione delle app riportate di seguito devono essere abilitate per le app applicabili e assegnate a tutti gli utenti di dispositivi mobili. Per altre informazioni su ogni impostazione di criteri, vedere [Impostazioni dei criteri di protezione delle app per iOS](app-protection-policy-settings-ios.md) e [Impostazioni dei criteri di protezione delle app per Android](app-protection-policy-settings-android.md).

Microsoft consiglia di esaminare e categorizzare gli scenari di utilizzo e quindi di configurare gli utenti applicando le linee guida definite per tale livello. Come per qualsiasi framework, potrebbe essere necessario modificare le impostazioni del livello corrispondente in base alle esigenze dell'organizzazione, perché la protezione dei dati deve valutare l'ambiente di minaccia, l'entità del rischio e l'impatto sull'usabilità.  

### <a name="apps-to-include-in-the-app-protection-policies"></a>App da includere nei criteri di protezione delle app  

Per i singoli criteri di protezione delle app, è necessario includere le principali app Microsoft seguenti:

- Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- Microsoft To-Do
- Word
- Microsoft SharePoint

I criteri dovrebbero includere altre app Microsoft in base alle esigenze aziendali, altre app pubbliche di terze parti in cui è integrata la versione di Intune SDK usata presso l'organizzazione, nonché app line-of-business in cui è integrato [Intune SDK](../developer/app-sdk.md) (o di cui è stato eseguito il wrapping).

### <a name="level-1-enterprise-basic-data-protection"></a>Livello 1 - Protezione di base dei dati aziendali

Il livello 1 è la configurazione di protezione dei dati minima per un dispositivo mobile aziendale. Questa configurazione sostituisce la necessità di definire criteri di accesso di base ai dispositivi di Exchange Online, richiedendo un PIN per accedere ai dati aziendali o dell'istituto di istruzione, crittografando tali dati e offrendo la possibilità di eliminarli in modo selettivo. A differenza dei criteri di accesso ai dispositivi di Exchange Online, tuttavia, le impostazioni dei criteri di protezione delle app riportate di seguito si applicano a tutte le app selezionate nei criteri, garantendo in tal modo la protezione dell'accesso ai dati anche in scenari diversi dalla messaggistica per dispositivi mobili.

I criteri di livello 1 applicano un livello di accesso ai dati ragionevole, riducendo al minimo l'effetto sugli utenti, e rispecchiano le impostazioni predefinite di accesso e protezione dei dati quando si creano criteri di protezione delle app in Microsoft Endpoint Manager.  

#### <a name="data-protection"></a>Protezione dati

| Impostazione | Descrizione dell'impostazione |             Valore  |             Piattaforma        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Trasferimento di dati |             Esegui il backup dei dati dell'organizzazione in…  |             Consenti  |             iOS/iPadOS, Android        |
| Trasferimento di dati |       Invia i dati dell'organizzazione ad altre app  |             Tutte le app  |             iOS/iPadOS, Android        |
| Trasferimento di dati |       Ricevi dati da altre app  |             Tutte le app  |             iOS/iPadOS, Android        |
| Trasferimento di dati |       Limita le operazioni taglia, copia e incolla tra altre app  |             Qualsiasi app  |             iOS/iPadOS, Android        |
| Trasferimento di dati |       Tastiere di terze parti  |             Consenti  |             iOS/iPadOS        |
| Trasferimento di dati |       Tastiere approvate  |             Non richiesto  |             Android        |
| Trasferimento di dati |       Acquisizione di schermata e Assistente Google  |             Consenti  |             Android        |
| Crittografia |             Crittografa i dati dell'organizzazione  |             Richiedi  |             iOS/iPadOS, Android        |
| Crittografia |       Crittografa i dati dell'organizzazione nei dispositivi registrati  |             Richiedi  |             Android        |
| Funzionalità  |             Sincronizza l'app con l'app contatti nativa  |             Consenti  |             iOS/iPadOS, Android        |
| Funzionalità  |       Stampa dei dati dell'organizzazione  |             Consenti  |             iOS/iPadOS, Android        |
| Funzionalità  |       Limita il trasferimento di contenuto Web con altre app  |             Qualsiasi app  |             iOS/iPadOS, Android        |
| Funzionalità  |       Notifiche sui dati dell'organizzazione  |             Consenti  |             iOS/iPadOS, Android        |

#### <a name="access-requirements"></a>Requisiti per l'accesso 

| Impostazione  | Valore  | Piattaforma  | Note  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PIN per l'accesso  | Richiedi  | iOS/iPadOS, Android  |   |
| Tipo di PIN  | Numerico  | iOS/iPadOS, Android  |   |
| PIN semplice  | Consenti  | iOS/iPadOS, Android  |   |
| Selezionare la lunghezza minima del PIN  | 4  | iOS/iPadOS, Android  |   |
| Credenziali biometriche invece del PIN per l'accesso  | Consenti  | iOS/iPadOS, Android  |   |
| Override di credenziali biometriche invece del PIN per l'accesso  | Richiedi  | iOS/iPadOS, Android  |   |
| Timeout (minuti di inattività)  | 720  | iOS/iPadOS, Android  |   |
| Face ID invece del PIN per l'accesso  | Consenti  | iOS/iPadOS  |   |
| Numero di giorni di attesa prima della reimpostazione del PIN  | No  | iOS/iPadOS, Android  |   |
| PIN dell'app quando il PIN del dispositivo è configurato  | Richiedi  | iOS/iPadOS, Android  | Se il dispositivo è registrato in Intune, gli amministratori possono considerare la possibilità di impostare questa opzione su "Non obbligatorio" se applicano un PIN del dispositivo sicuro tramite criteri di conformità del dispositivo.  |
| Credenziali dell'account aziendale o dell'istituto di istruzione per l'accesso  | Non richiesto  | iOS/iPadOS, Android  |   |
| Controlla di nuovo i requisiti di accesso dopo (minuti di inattività)  | 30  | iOS/iPadOS, Android  |   |

#### <a name="conditional-launch"></a>Avvio condizionale 

| Impostazione | Descrizione dell'impostazione |          Valore/Azione  |          Piattaforma        | Note |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Condizioni dell'app |       Numero massimo di tentativi di PIN  |          5/Reimposta PIN  |          iOS/iPadOS, Android  |                  |
| Condizioni dell'app |       Periodo di prova offline  |          720/Blocca l'accesso (minuti)  |          iOS/iPadOS, Android  |                  |
| Condizioni dell'app |       Periodo di prova offline  |          90/Cancella i dati (giorni)  |          iOS/iPadOS, Android  |                  |
| Condizioni del dispositivo  |       Dispositivi jailbroken/rooted  |        Blocca l'accesso  |          iOS/iPadOS, Android  |                  |
| Condizioni del dispositivo  |       Attestazione del dispositivo SafetyNet  |          Integrità di base e dispositivi certificati/Blocca l'accesso  |          Android  |          <p>Questa impostazione configura l'attestazione SafetyNet di Google nei dispositivi degli utenti finali. L'integrità di base convalida l'integrità del dispositivo. Dispositivi rooted, emulatori, dispositivi virtuali e dispositivi con segni di manomissione non superano la verifica dell'integrità di base. </p><p> L'opzione Integrità di base e dispositivi certificati convalida la compatibilità del dispositivo con i servizi Google. Solo i dispositivi non modificati che hanno ottenuto la certificazione di Google possono superare questo controllo.</p>  |
| Condizioni del dispositivo  |       Rendi obbligatoria l'analisi delle minacce nelle app  |        Blocca l'accesso  |          Android  |          Questa impostazione garantisce che l'analisi di verifica delle app di Google sia attivata per i dispositivi degli utenti finali. Se l'opzione è configurata, all'utente finale non sarà consentito l'accesso fino a quando non attiverà l'analisi delle app di Google nel dispositivo Android.        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>Livello 2 - Protezione avanzata dei dati aziendali

Il livello 2 è la configurazione di protezione dei dati consigliata come standard per i dispositivi da cui gli utenti accedono a informazioni più riservate. Questi dispositivi sono attualmente un bersaglio classico nelle aziende. I consigli offerti a questo livello non presuppongono la presenza di numerosi addetti alla sicurezza altamente qualificati e pertanto dovrebbero essere accessibili alla maggior parte delle organizzazioni aziendali. Questa configurazione estende la configurazione del livello 1 limitando gli scenari di trasferimento dei dati e richiedendo una versione minima del sistema operativo.

Le impostazioni dei criteri applicate nel livello 2 includono tutte le impostazioni dei criteri consigliate per il livello 1 e aggiungono o aggiornano solo le impostazioni dei criteri riportate di seguito per implementare più controlli e una configurazione più sofisticata rispetto al livello 1. Anche se queste impostazioni possono avere un impatto leggermente maggiore sugli utenti o sulle applicazioni, applicano un livello di protezione dei dati più adeguato ai rischi per corrono gli utenti accedendo a informazioni riservate nei dispositivi mobili.

#### <a name="data-protection"></a>Protezione dati

| Impostazione | Descrizione dell'impostazione |             Valore  |             Piattaforma        | Note |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Trasferimento dati |       Esegui il backup dei dati dell'organizzazione in…  |          Blocca  |          iOS/iPadOS, Android  |                  |
| Trasferimento dati |       Invia i dati dell'organizzazione ad altre app  |          App gestite da criteri  |          iOS/iPadOS, Android  |          <p>Con iOS/iPadOS, gli amministratori possono configurare questo valore come "App gestite da criteri", "App gestite da criteri con condivisione del sistema operativo" o "App gestite da criteri con filtro basato su Apri in/Condividi". </p><p>App gestite da criteri con condivisione del sistema operativo è disponibile quando il dispositivo viene registrato anche con Intune. Questa impostazione consente il trasferimento dei dati ad altre app gestite da criteri e i trasferimenti di file ad altre app gestite da Intune. </p><p>App gestite da criteri con filtro basato su Apri in/Condividi consente di applicare un filtro alle finestre di dialogo Apri in/Condividi del sistema operativo per visualizzare solo le app gestite da criteri. </p><p> Per altre informazioni, vedere [Impostazioni dei criteri di protezione delle app per iOS](app-protection-policy-settings-ios.md).</p> |
| Trasferimento dati |       Salva copie dei dati dell'organizzazione  |          Blocca  |          iOS/iPadOS, Android  |                  |
| Trasferimento dati |       Consenti all'utente di salvare copie nei servizi selezionati  |          OneDrive for Business, SharePoint Online |          iOS/iPadOS, Android  |                  |
| Trasferimento dati |       Limita le operazioni taglia, copia e incolla tra altre app  |          App gestite da criteri con Incolla in  |          iOS/iPadOS, Android  |                  |
| Trasferimento dati |       Acquisizione di schermata e Assistente Google  |          Blocca  |          Android  |                  |
| Funzionalità |       Limita il trasferimento di contenuto Web con altre app  |          Microsoft Edge  |          iOS/iPadOS, Android  |                  |
| Funzionalità |       Notifiche sui dati dell'organizzazione  |          Blocca i dati dell'organizzazione  |          iOS/iPadOS, Android  |          Per un elenco delle app che supportano questa impostazione, vedere [Impostazioni dei criteri di protezione delle app per iOS](app-protection-policy-settings-ios.md) e [Impostazioni dei criteri di protezione delle app per Android](app-protection-policy-settings-android.md).       |

#### <a name="conditional-launch"></a>Avvio condizionale

| Impostazione | Descrizione dell'impostazione |          Valore/Azione  |          Piattaforma        | Note |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Condizioni del dispositivo  |       Versione minima del sistema operativo  |          *Formato: Principale.Secondaria.Build <br>Esempio:   12.4.4*/Blocca l'accesso |          iOS/iPadOS        | Microsoft consiglia di configurare la versione principale minima di iOS in modo che corrisponda alle versioni di iOS supportate per le app Microsoft.   Le app Microsoft supportano un approccio N-1, dove N è l'attuale versione principale di iOS. Per i valori di versione secondaria e di build, Microsoft consiglia di verificare che i dispositivi siano aggiornati con i rispettivi aggiornamenti della sicurezza. Per i consigli più recenti di Apple, vedere [Aggiornamenti della sicurezza di Apple](https://support.apple.com/en-us/HT201222) |
| Condizioni del dispositivo  |       Versione minima del sistema operativo  |          *Formato: Principale.Secondaria<br>   Esempio: 8.0*/Blocca l'accesso   |          Android        | Microsoft consiglia di configurare la versione principale minima di Android in modo che corrisponda alle versioni di Android supportate per le app Microsoft. Gli OEM e i dispositivi che rispettano i requisiti consigliati per Android Enterprise devono supportare la versione corrente con l'aggiornamento di una sola lettera.   Attualmente Android consiglia Android 8.0 e versioni successive per i knowledge worker.   Per i consigli più recenti su Android, vedere [Requisiti di Android Enterprise Recommended](https://www.android.com/enterprise/recommended/requirements/) |
| Condizioni del dispositivo  |       Versione minima della patch  |          *Formato:   AAAA-MM-GG <br> Esempio: 2020-01-01*/Blocca l'accesso  |          Android        | I dispositivi Android possono ricevere patch di sicurezza mensili, ma la versione dipende dagli OEM e/o dai gestori telefonici. Prima di implementare questa impostazione, le organizzazioni devono assicurarsi che i dispositivi Android distribuiti ricevano gli aggiornamenti della sicurezza. Per le versioni di patch più recenti, vedere i [bollettini sulla sicurezza di Android](https://source.android.com/security/bulletin/).  |

#### <a name="level-3-enterprise-high-data-protection"></a>Livello 3 - Protezione elevata dei dati aziendali 

Il livello 3 è la configurazione di protezione dei dati consigliata come standard per le organizzazioni con sistemi di sicurezza sofisticati di ampia portata oppure per utenti e gruppi specifici che possono essere facilmente bersaglio di attacchi. Tali organizzazioni sono in genere esposte agli attacchi di avversari ben finanziati e sofisticati e pertanto hanno bisogno dei vincoli e dei controlli aggiuntivi descritti di seguito. Questa configurazione estende la configurazione del livello 2 limitando altri scenari di trasferimento dei dati, aumentando la complessità della configurazione del PIN e introducendo il rilevamento delle minacce per dispositivi mobili.  

Le impostazioni dei criteri applicate nel livello 3 includono tutte le impostazioni dei criteri consigliate per i livelli 2 e 1 e aggiungono o aggiornano solo le impostazioni dei criteri seguenti per implementare controlli e configurazione di protezione dei dati rigorosi. Queste impostazioni dei criteri possono avere un impatto potenzialmente significativo su utenti o applicazioni, applicando un livello di sicurezza adeguato ai rischi che devono affrontare le organizzazioni.  

#### <a name="data-protection"></a>Protezione dati

| Impostazione | Descrizione dell'impostazione |             Valore  |             Piattaforma        | Note |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Trasferimento di dati |       Ricevi dati da altre app  |          App gestite da criteri  |          iOS/iPadOS, Android         |  |
| Trasferimento di dati |       Tastiere di terze parti  |          Blocca  |          iOS/iPadOS        | In iOS questa operazione impedisce il funzionamento di tutte le tastiere di terze parti all'interno dell'app.  |
| Trasferimento di dati |       Tastiere approvate  |          Richiedi  |          Android        | Con Android, le tastiere devono essere selezionate per poter essere usate in base ai dispositivi Android distribuiti.  |
| Trasferimento di dati |       Selezionare le tastiere da approvare  |          *Aggiungi/Rimuovi tastiere*  |          Android        | Con Android, le tastiere devono essere selezionate per poter essere usate in base ai dispositivi Android distribuiti.  |
| Funzionalità |       Stampa dei dati dell'organizzazione  |          Blocca  |          iOS/iPadOS, Android         |  |

#### <a name="access-requirements"></a>Requisiti per l'accesso

|       Impostazione  |          Valore  |          Piattaforma  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       PIN semplice  |          Blocca  |          iOS/iPadOS, Android  |
|       Selezionare la lunghezza minima del PIN  |          6  |          iOS/iPadOS, Android  |
|       Numero di giorni di attesa prima della reimpostazione del PIN  |          Sì  |          iOS/iPadOS, Android  |
|       Numero di giorni  |          365  |          iOS/iPadOS, Android  |

#### <a name="conditional-launch"></a>Avvio condizionale

| Impostazione | Descrizione dell'impostazione |          Valore/Azione  |          Piattaforma        | Note |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Condizioni del dispositivo  |          Dispositivi jailbroken/rooted  |        ND/Cancella i dati  |          iOS/iPadOS, Android        |  |
|       Condizioni del dispositivo  |          Livello di minaccia massimo consentito  |          Protetto/Blocca l'accesso  |          iOS/iPadOS, Android        | <p>I dispositivi non registrati possono essere controllati per individuare eventuali minacce usando Mobile Threat Defense. Per altre informazioni, vedere [Mobile Threat Defense per i dispositivi non registrati](https://aka.ms/mtdmamdocs).      </p><p>     Se il dispositivo è registrato, questa impostazione può essere ignorata a favore della distribuzione di Mobile Threat Defense per i dispositivi registrati. Per altre informazioni, vedere [Mobile Threat Defense per i dispositivi registrati](../protect/mtd-device-compliance-policy-create.md).</p> |

## <a name="next-steps"></a>Passaggi successivi

Gli amministratori possono incorporare i livelli di configurazione illustrati all'interno della metodologia di distribuzione ad anelli per il test e l'uso in produzione importando i [modelli JSON di esempio del framework di configurazione con criteri di protezione delle app di Intune](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) tramite gli [script PowerShell di Intune](https://github.com/microsoftgraph/powershell-intune-samples).

## <a name="see-also"></a>Vedere anche

- [Come creare e distribuire i criteri di protezione delle app con Microsoft Intune](app-protection-policies.md)
- [Impostazioni dei criteri di protezione delle app di Android disponibili con Microsoft Intune](app-protection-policy-settings-android.md)
- [Impostazioni dei criteri di protezione delle app per iOS/iPadOS disponibili con Microsoft Intune](app-protection-policy-settings-ios.md)
- Le app di terze parti, ad esempio l'app per dispositivi mobili Salesforce, interagiscono con Intune in modi specifici per proteggere i dati aziendali. Per altre informazioni sul funzionamento dell'app Salesforce con Intune (incluse le impostazioni di configurazione delle app MDM), vedere [Salesforce App and Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf) (App Salesforce e Microsoft Intune).
