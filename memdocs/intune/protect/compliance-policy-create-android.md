---
title: Impostazioni di conformità di Android in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare un elenco di tutte le impostazioni che è possibile usare durante l'impostazione della conformità per i dispositivi Android in Microsoft Intune. Impostare le regole delle password, scegliere una versione minima o massima del sistema operativo, creare restrizioni per app specifiche, impedire il riutilizzo della password e così via.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729221"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Impostazioni di Android per contrassegnare un dispositivo come conforme o non conforme in Intune

Questo articolo elenca e descrive le diverse impostazioni di conformità che è possibile configurare nei dispositivi Android in Intune. Nella soluzione di gestione di dispositivi mobili (MDM), usare queste impostazioni per contrassegnare i dispositivi rooted (Jailbroken) come non conformi, impostare un livello di rischio consentito, abilitare Protezione di Google Play e così via.

Questa funzionalità si applica a:

- Amministratore dispositivo Android

Come amministratore di Intune, usare queste impostazioni di conformità per proteggere le risorse dell'organizzazione. Per altre informazioni sui criteri di conformità e sul loro funzionamento, vedere [Introduzione ai criteri di conformità dei dispositivi](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare i criteri di conformità](create-compliance-policy.md#create-the-policy). Per **Piattaforma** selezionare **Amministratore di dispositivi Android**.

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **Richiedi che il dispositivo si trovi al massimo al punteggio di rischio del computer**  

  Selezionare il punteggio di rischio del computer massimo consentito per i dispositivi valutati da Microsoft Defender ATP. I dispositivi con un punteggio superiore vengono contrassegnati come non conformi.
  - **Non configurato** (*impostazione predefinita*)
  - **Cancella**
  - **Bassa**
  - **Media**
  - **Alta**

## <a name="device-health"></a>Integrità dispositivi

- **Dispositivi gestiti con amministratore di dispositivi**  
  Le funzionalità di *amministratore dei dispositivi* sono state sostituite da Android Enterprise.

  - **Non configurato** (*impostazione predefinita*)
  - **Blocca** - Il blocco dell'amministratore di dispositivi consentirà agli utenti di passare in modo guidato alla gestione del profilo di lavoro di Android Enterprise per ottenere nuovamente l'accesso.

- **Dispositivi rooted**  
  Consente di impedire ai dispositivi rooted di avere l'accesso aziendale. (Questo controllo di conformità è supportato per Android 4.0 e versioni successive.)

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Blocca**: contrassegnare i dispositivi rooted (jailbroken) come non conformi.

- **Richiedi che il dispositivo si trovi al massimo al livello di minaccia del dispositivo**  
  usare questa impostazione per considerare la valutazione del rischio di un servizio Mobile Threat Defense connesso come condizione di conformità.

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Protetto**: questa opzione è la più sicura poiché il dispositivo non può avere minacce. Se viene rilevata la presenza di minacce di qualsiasi livello, il dispositivo viene considerato non conforme.
  - **Basso**: il dispositivo viene valutato come conforme se sono presenti solo minacce di livello basso. In presenza di minacce di livello più alto, il dispositivo verrà messo in stato di non conformità.
  - **Medio**: il dispositivo viene valutato come conforme se le minacce esistenti nel dispositivo sono di livello basso o medio. Se viene rilevata la presenza di minacce di livello alto, il dispositivo viene considerato come non conforme.
  - **Alto**: questa opzione è la meno sicura e consente tutti i livelli di minaccia. Potrebbe essere utile usare questa soluzione solo per la creazione di report.

### <a name="google-play-protect"></a>Protezione di Google Play

- **Google Play Services è configurato**  
  Google Play Services consente gli aggiornamenti della sicurezza e rappresenta una dipendenza di base per molte funzionalità di sicurezza nei dispositivi Google certificati.

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.  
  - **Rendi obbligatorio**: richiedere l'installazione e l'abilitazione dell'app Google Play Services.  

- **Provider di sicurezza aggiornato**

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Rendi obbligatorio**: richiedere un provider di sicurezza aggiornato che può proteggere un dispositivo dalle vulnerabilità note.

- **Analisi delle minacce nelle app**

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Rendi obbligatorio**: richiedere l'abilitazione della funzionalità **Verifica app** di Android.

  > [!NOTE]
  > Nella piattaforma Android legacy, questa funzionalità è un'impostazione di conformità. Intune consente solo di verificare se questa impostazione è abilitata a livello di dispositivo.

- **Attestazione del dispositivo SafetyNet**  
  immettere il livello di [attestazione di SafetyNet](https://developer.android.com/training/safetynet/attestation.html) che deve essere raggiunto. Le opzioni disponibili sono:

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Verifica l'integrità di base**
  - **Verifica l'integrità di base e i dispositivi certificati**

> [!NOTE]
> Per configurare Protezione di Google Play con i criteri di protezione delle app, vedere [Impostazioni dei criteri di protezione delle app di Android in Intune](../apps/app-protection-policy-settings-android.md#conditional-launch).

## <a name="device-properties"></a>Proprietà dispositivo

### <a name="operating-system-version"></a>Versione del sistema operativo

- **Versione minima del sistema operativo**  
  quando un dispositivo non soddisfa il requisito relativo alla versione minima del sistema operativo, viene segnalato come non conforme. Viene visualizzato un collegamento con informazioni su come eseguire l'aggiornamento. L'utente finale può scegliere di aggiornare il dispositivo e quindi ottenere l'accesso alle risorse aziendali.

  *Per impostazione predefinita, non viene configurata alcuna versione*.

- **Versione massima del sistema operativo**  
  quando un dispositivo usa una versione del sistema operativo successiva rispetto a quella specificata nella regola, l'accesso alle risorse aziendali viene bloccato. All'utente viene richiesto di contattare l'amministratore IT. Finché la regola non viene modificata in modo da consentire la versione del sistema operativo usata dal dispositivo, quest'ultimo non può accedere alle risorse aziendali.

  *Per impostazione predefinita, non viene configurata alcuna versione*.

## <a name="system-security"></a>Protezione del sistema

### <a name="password"></a>Password

- **Richiedi una password per sbloccare i dispositivi mobili**  
  *Supportato in Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.*

  Questa impostazione specifica se richiedere agli utenti di immettere una password per poter accedere alle informazioni sui propri dispositivi mobili. Valore consigliato: Richiedi  

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Rendi obbligatorio**: gli utenti devono immettere una password prima di accedere al dispositivo.

- **Tipo di password richiesto**  
  *Supportato in Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.*

  scegliere se una password deve essere composta solo da caratteri numerici oppure da una combinazione di numeri e altri caratteri.

  - **Impostazione predefinita dispositivo**: per valutare la conformità delle password, assicurarsi di selezionare un livello di complessità della password diverso da **Impostazione predefinita dispositivo**.
  - **Protezione biometrica bassa**
  - **Almeno numerico**
  - **Complessa numerica**: i numeri consecutivi o ripetuti, ad esempio `1111` o `1234`, non sono consentiti.
  - **Almeno alfabetico**
  - **Almeno alfanumerico**
  - **Almeno alfanumerico con simboli**

  In base alla configurazione di questa impostazione, sono disponibili una o più delle opzioni seguenti:

  - **Lunghezza minima password**  
    *Supportato in Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.*

    Immettere il numero minimo di cifre o caratteri che la password dell'utente deve avere.

  - **Numero massimo di minuti di inattività prima che venga richiesta la password**  
    *Supportato in Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.*

    immettere il tempo di inattività prima che l'utente debba immettere nuovamente la password. Se si sceglie **Non configurato** (impostazione predefinita), questa impostazione non viene tenuta in considerazione per la valutazione della conformità.

  - **Numero di giorni rimanenti prima della scadenza della password**  
  *Supportato in Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.*

  Selezionare il numero di giorni che mancano alla scadenza della password, quando l'utente deve creare una nuova password.

  - **Numero di password precedenti di cui impedire il riutilizzo**  
    immettere il numero di password recenti che non è possibile riutilizzare. Usare questa impostazione per impedire all'utente di creare password già usate in precedenza. (Supportata per Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.)

### <a name="encryption"></a>Crittografia

- **Crittografia dell'archivio dati nel dispositivo**  
  *Supportato in Android 4.0 e versioni successive o KNOX 4.0 e versioni successive.*

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Rendi obbligatorio**: crittografa l'archivio dati nei dispositivi. I dispositivi vengono crittografati se si sceglie l'impostazione **Richiedi una password per sbloccare i dispositivi mobili**.

### <a name="device-security"></a>Sicurezza del dispositivo

- **Blocca app da origini sconosciute**  
  *Supportata in Android 4.0 ad Android 7.x. Non supportata da Android 8.0 e versioni successive*

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Blocca**: blocca i dispositivi con origini abilitate di tipo **Sicurezza > Origini sconosciute** (*supportato in Android da 4.0 a 7.x. Non supportato in Android 8.0 e versioni successive*).

  Per trasferire localmente le app, devono essere consentite le origini sconosciute. Se non si esegue il sideload di app Android, abilitare questi criteri di conformità impostando questa funzionalità su **Blocca**.

  > [!IMPORTANT]
  > Le applicazioni trasferite localmente richiedono l'abilitazione dell'impostazione **Blocca app da origini sconosciute**. Imporre questi criteri di conformità solo se non si esegue il sideload di app Android nei dispositivi.

- **Integrità del runtime dell'app Portale aziendale**
  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Rendi obbligatorio**: scegliere *Rendi obbligatorio* per assicurarsi che l'app Portale aziendale soddisfi tutti i requisiti seguenti:

    - Ha l'ambiente di runtime predefinito installato
    - È firmata correttamente
    - Non è in modalità di debug
    - È installata da un'origine nota

- **Blocca il debug USB nel dispositivo**  
  *(Supportata in Android 4.2 o versioni successive)*

  - **Non configurato** (*impostazione predefinita*): questa impostazione non viene valutata per la conformità o la non conformità.
  - **Blocca**: impedire ai dispositivi di usare la funzionalità di debug USB.

- **Livello minimo di patch di protezione**  
  *(Supportata in Android 6.0 o versione successiva)*

  selezionare il livello di patch di sicurezza meno recente consentito per un dispositivo. I dispositivi che non presentano almeno questo livello di patch vengono considerati non conformi. La data deve essere immessa nel formato `YYYY-MM-DD`.

  *Per impostazione predefinita, non viene configurata alcuna data*.

- **App con restrizioni**  
  immettere **Nome app** e **ID bundle dell'app** per le app a cui devono essere applicate restrizioni, quindi selezionare **Aggiungi**. Un dispositivo in cui è installata almeno un'app con restrizioni viene contrassegnato come non conforme.

## <a name="next-steps"></a>Passaggi successivi

- [Aggiungere azioni per i dispositivi non conformi](actions-for-noncompliance.md) e [Usare i tag di ambito per filtrare i criteri](../fundamentals/scope-tags.md).
- [Monitorare i criteri di conformità](compliance-policy-monitor.md).
- Vedere [Impostazioni dei criteri di conformità peri dispositivi Android Enterprise](compliance-policy-create-android-for-work.md).
