---
title: Gestire Office per iOS e Android con Intune
titleSuffix: ''
description: Usare i criteri di protezione e di configurazione delle app di Intune con Office per iOS e Android per garantire che l'accesso alle esperienze di collaborazione venga sempre eseguito con misure di sicurezza applicate.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d23eaeee839122bad46cd9619a790b9ca6332a6
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383258"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>Gestire le esperienze di collaborazione con Office per iOS e Android con Microsoft Intune

Office per iOS e Android offre diversi vantaggi principali, tra cui:

- Combinazione di Word, Excel e PowerPoint in modo da semplificare l'esperienza con un minor numero di app da scaricare o alternare. Richiede molto meno spazio di archiviazione del telefono rispetto all'installazione di singole app, mantenendo al tempo stesso praticamente tutte le funzionalità delle app per dispositivi mobili esistenti che gli utenti già conoscono e usano.
- Integrazione della tecnologia Office Lens per sbloccare le potenzialità della fotocamera con funzionalità come la conversione di immagini in documenti di Word ed Excel modificabili, la scansione di file PDF e l'acquisizione di lavagne con miglioramenti digitali automatici per semplificare la lettura del contenuto.
- Aggiunta di nuove funzionalità per le attività comuni spesso svolte dalle persone al telefono, come la creazione di note rapide, la firma di file PDF, la scansione di codici QR e il trasferimento di file tra dispositivi.

Le funzionalità di protezione più complete e più ampie per i dati di Office 365 sono disponibili con l'abbonamento alla suite Enterprise Mobility + Security, che include funzionalità di Microsoft Intune e Azure Active Directory Premium, come l'accesso condizionale. Come minimo, è consigliabile distribuire criteri di accesso condizionale che consentono di connettersi a Office per iOS e Android solo dai dispositivi mobili e criteri di protezione delle app di Intune che garantiscono la protezione dell'esperienza di collaborazione.

## <a name="apply-conditional-access"></a>Applicare l'accesso condizionale
Le organizzazioni possono usare i criteri di accesso condizionale di Azure AD per assicurarsi che gli utenti possano accedere solo ai contenuti aziendali o dell'istituto di istruzione usando Office per iOS e Android. A tale scopo, è necessario disporre di criteri di accesso condizionale destinati a tutti i potenziali utenti. Per informazioni dettagliate sulla creazione di questi criteri, vedere [Richiedere i criteri di protezione delle app per l'accesso alle app cloud con accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Seguire "Passaggio 1: configurare criteri di accesso condizionale di Azure AD per Office 365"in [Scenario 1: le app di Office 365 richiedono app approvate con i criteri di protezione delle app](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), che consente l'uso di Office per iOS e Android, ma impedisce ad altri client per dispositivi mobili che supportano OAuth di terze parti di connettersi agli endpoint Office 365.

   >[!NOTE]
   > Questo criterio garantisce che gli utenti di dispositivi mobili possano accedere a tutti gli endpoint di Office usando le app applicabili.

## <a name="create-intune-app-protection-policies"></a>Creare criteri di protezione delle app di Intune

I criteri di protezione delle app definiscono quali app sono consentite e le azioni che queste possono eseguire con i dati dell'organizzazione. Le scelte disponibili sull'APP consentono alle organizzazioni di adattare la protezione alle loro esigenze specifiche. Per alcuni utenti potrebbe non essere semplice individuare le impostazioni dei criteri necessarie per implementare uno scenario completo. Per aiutare le organizzazioni a dare la priorità alla protezione avanzata degli endpoint di client mobili, Microsoft ha introdotto la tassonomia per il framework di protezione dei dati dell'APP per la gestione di dispositivi mobili iOS e Android.

Il framework di protezione dei dati dell'APP è organizzato in tre livelli di configurazione distinti, ognuno dei quali si basa sul livello precedente:

- **Protezione di base dei dati aziendali** (livello 1) garantisce che le app siano protette con un PIN e crittografate ed esegue operazioni di cancellazione selettiva. Per i dispositivi Android questo livello convalida l'attestazione dei dispositivi Android. Si tratta di una configurazione a livello di voce che offre un controllo simile di protezione dei dati nei criteri della cassetta postale di Exchange Online e introduce l'IT e la popolazione di utente nell'APP.
- **Protezione avanzata dei dati aziendali** (livello 2) introduce i meccanismi di protezione della perdita dei dati aziendali dell'APP e i requisiti minimi del sistema operativo. Questa configurazione è applicabile alla maggior parte degli utenti di dispositivi mobili che accedono ai dati aziendali o dell'istituto di istruzione.
- **Protezione elevata dei dati aziendali** (livello 3) introduce meccanismi avanzati per la protezione dei dati, configurazione del PIN avanzata e Mobile Threat Defense dell'APP. Questa configurazione è utile per gli utenti che accedono a dati ad alto rischio.

Per visualizzare le raccomandazioni specifiche per ogni livello di configurazione e le app minime che devono essere protette, consultare il [Framework di protezione dei dati con criteri di protezione delle app](app-protection-framework.md).

Indipendentemente dal fatto che il dispositivo sia registrato in una soluzione di gestione unificata degli endpoint (UEM), è necessario creare un criterio di protezione delle app di Intune per le app iOS e Android, seguendo la procedura descritta in [Come creare e assegnare criteri di protezione delle app](app-protection-policies.md). Questi criteri, come minimo, devono soddisfare le condizioni seguenti:

1. Sono incluse tutte le app Microsoft 365 per dispositivi mobili, ad esempio Microsoft Edge, Outlook, OneDrive, Office o Teams, in modo da garantire che gli utenti possano accedere e modificare i dati aziendali o dell'istituto di istruzione in qualsiasi app Microsoft in modo sicuro.

2. Sono assegnati a tutti gli utenti. Ciò garantisce che tutti gli utenti siano protetti, indipendentemente dal fatto che usino Office per iOS o Android.

3. Determinare il livello di framework che soddisfa i requisiti. La maggior parte delle organizzazioni deve implementare le impostazioni definite in **Protezione avanzata dei dati aziendali** (livello 2), in quanto consente di controllare i requisiti di protezione e accesso ai dati.

Per altre informazioni sulle impostazione disponibili, vedere gli articoli [Impostazioni dei criteri di protezione delle app di Android](app-protection-policy-settings-android.md) e [Impostazioni dei criteri di protezione delle app per iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Per applicare i criteri di protezione delle app di Intune alle app nei dispositivi Android che non sono registrati in Intune, l'utente deve anche installare il Portale aziendale Intune. Per altre informazioni, consultare l'articolo [Aspettative relative alla gestione dell'app per Android con criteri di protezione delle app](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Utilizzare la configurazione delle app

Office per iOS e Android supporta le impostazioni dell'app che consentono agli amministratori della gestione unificata degli endpoint, ad esempio Microsoft Endpoint Manager, di personalizzare il comportamento dell'app.

La configurazione dell'app può essere eseguita tramite il canale di gestione di dispositivi mobili (MDM) del sistema operativo sui dispositivi registrati (canale [Configurazione delle app gestite](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) per iOS o [Android nel canale Enterprise](https://developer.android.com/work/managed-configurations) per Android) o tramite il canale Criteri di protezione delle app (APP) di Intune. Office per iOS e Android supporta gli scenari di configurazione seguenti:

- Ammettere solo account aziendali o di un istituto di istruzione
- Impostazioni di protezione dati

> [!IMPORTANT]
> Per gli scenari di configurazione che richiedono la registrazione del dispositivo in Android, i dispositivi devono essere registrati in Android Enterprise e Office per Android deve essere distribuito tramite la versione gestita di Google Play Store. Per altre informazioni, vedere gli articoli [Configurare la registrazione dei dispositivi con profilo di lavoro Android Enterprise](../enrollment/android-work-profile-enroll.md) e [Criteri di configurazione delle app per Microsoft Intune](app-configuration-policies-use-android.md).

Ogni scenario di configurazione evidenzia i propri requisiti specifici. Ad esempio, se lo scenario di configurazione richiede la registrazione del dispositivo e quindi funziona con qualsiasi provider UEM o richiede criteri di Protezione app di Intune.

> [!NOTE]
> Con Microsoft Endpoint Manager, la configurazione dell'app eseguita tramite il canale MDM del sistema operativo è indicata come Criteri di configurazione delle app (ACP) per **dispositivi gestiti**; la configurazione dell'app eseguita tramite il canale Criteri di protezione delle app è denominata Criteri di configurazione delle app per**app gestite**.

## <a name="only-allow-work-or-school-accounts"></a>Ammettere solo account aziendali o di un istituto di istruzione

Il rispetto dei criteri di conformità e sicurezza dei dati dei clienti principali e altamente regolamentati è un elemento fondamentale del valore di Microsoft 365. Alcune società hanno la necessità di acquisire tutte le informazioni sulle comunicazioni all'interno dell'ambiente aziendale, nonché di assicurarsi che i dispositivi vengano usati solo per le comunicazioni aziendali. Per supportare questi requisiti, è possibile configurare Office per Android nei dispositivi registrati in modo da consentire il provisioning di un singolo account aziendale nell'app.

Per altre informazioni sulla configurazione delle impostazioni della modalità degli account dell'organizzazione consentiti, vedere:

- [Impostazione Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Questo scenario di configurazione funziona solo con i dispositivi registrati. Tuttavia, sono supportati tutti i provider UEM. Se non si usa Microsoft Endpoint Manager, è necessario consultare la documentazione di UEM per informazioni su come implementare queste chiavi di configurazione.

> [!NOTE]
> Al momento, solo Office per Android supporta la modalità account consentiti dell'organizzazione.

## <a name="data-protection-app-configuration-scenarios"></a>Scenari di configurazione dell'app per la protezione dei dati

Office per iOS e Android supporta i criteri di configurazione delle app per le seguenti impostazioni di protezione dati quando l'app viene gestita da Microsoft Endpoint Manager con criteri di protezione delle app di Intune applicati all'account aziendale o dell'istituto di istruzione che ha eseguito l'accesso all'app:

- Gestione dei trasferimenti di file tramite l'azione Trasferisci file
- Gestire i trasferimenti di file tramite l'azione Condividi nelle vicinanze

Queste impostazioni possono essere implementate nell'app indipendentemente dallo stato di registrazione del dispositivo.

### <a name="manage-file-transfers"></a>Gestire i trasferimenti di file

Per impostazione predefinita, Office per iOS e Android consente agli utenti di condividere contenuto usando un'ampia gamma di meccanismi:

- Se il file è ospitato in OneDrive o SharePoint, gli utenti possono avviare una richiesta di condivisione direttamente all'interno del file.
- Gli utenti possono trasferire file ai sistemi desktop usando l'azione **Trasferisci file**.
- Gli utenti possono condividere file con dispositivi mobili adiacenti usando l'azione **Condividi nelle vicinanze**.

Le azioni **Trasferisci file** e **Condividi nelle vicinanze** funzionano solo con i file multimediali, i file locali e i file non protetti da criteri di protezione dell'app. 

|    Chiave    |    Valore    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.ShareNearby.IsAllowed.IntuneMAMOnly    |    **true** (impostazione predefinita) abilita la funzionalità Condividi nelle vicinanze per l'account aziendale o dell'istituto di istruzione<br>**false** disabilita la funzionalità Condividi nelle vicinanze per l'account aziendale o dell'istituto di istruzione    |
|    com.microsoft.office.TransferFiles.IsAllowed.IntuneMAMOnly    |    **true** (impostazione predefinita) abilita la funzionalità Trasferisci file per l'account aziendale o dell'istituto di istruzione<br>**false** disabilita la funzionalità Trasferisci file per l'account aziendale o dell'istituto di istruzione    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Implementare scenari di configurazione delle app con Microsoft Endpoint Manager

Se si usa Microsoft Endpoint Manager come provider di gestione delle app per dispositivi mobili, vedere [Aggiungere criteri di configurazione delle app per le app gestite senza registrazione dei dispositivi](app-configuration-policies-managed-app.md) per informazioni come creare un criterio di configurazione delle app gestite per gli scenari di configurazione delle app per la protezione dei dati. Dopo aver creato la configurazione, è possibile assegnare i criteri a gruppi di utenti.

## <a name="next-steps"></a>Passaggi successivi

- [Che cosa sono i criteri di protezione delle app?](app-protection-policy.md) 
- [Criteri di configurazione delle app per Microsoft Intune](app-configuration-policies-overview.md)