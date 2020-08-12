---
title: Configurare la pagina relativa allo stato della registrazione
titleSuffix: Microsoft Intune
description: Configurare una pagina introduttiva per gli utenti che registrano i dispositivi Windows 10.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75f6585144f62636033c94f701a57cb70e018c26
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051588"
---
# <a name="set-up-the-enrollment-status-page"></a>Configurare la pagina relativa allo stato della registrazione
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
La pagina relativa allo stato della registrazione (ESP) visualizza lo stato di avanzamento del provisioning dopo la registrazione di un nuovo dispositivo, nonché quando i nuovi utenti eseguono l'accesso al dispositivo.  Ciò consente agli amministratori IT di impedire (bloccare) facoltativamente l'accesso al dispositivo fino a quando non ne viene eseguito il provisioning completo, fornendo allo stesso tempo agli utenti informazioni sulle attività rimanenti durante il processo di provisioning.

La pagina relativa allo stato della registrazione può essere usata come parte di qualsiasi scenario di provisioning di [Windows Autopilot](../../autopilot/index.yml) e può anche essere usata separatamente da Windows Autopilot come parte dell'esperienza predefinita per Azure AD Join, nonché per tutti i nuovi utenti che accedono al dispositivo per la prima volta.

È possibile creare più profili della pagina relativa allo stato della registrazione con configurazioni diverse che specificano:

- Visualizzazione dello stato dell'installazione
- Blocco dell'accesso fino al completamento del processo di provisioning
- Limiti di tempo
- Operazioni di risoluzione dei problemi consentite

Questi profili sono specificati in ordine di priorità. Verrà usato quello con la priorità più alta applicabile.  Ogni profilo ESP può essere destinato a gruppi che contengono dispositivi o utenti.  Quando si determina il profilo da usare, verranno seguiti i criteri seguenti:

- Verrà usato per primo il profilo con la priorità più alta destinato al dispositivo.
- In assenza di profili assegnati al dispositivo, verrà usato il profilo con priorità più alta assegnato all'utente corrente.  Questo vale solo negli scenari in cui è presente un utente. Negli scenari con trattamento esclusivo e di distribuzione automatica è possibile usare solo i dispositivi come destinazione.
- Se non sono presenti profili destinati a gruppi specifici, verrà usato il profilo ESP predefinito.

## <a name="available-settings"></a>Impostazioni disponibili

È possibile configurare le impostazioni seguenti per personalizzare il comportamento della pagina relativa allo stato della registrazione:

<table>
<th align="left">Impostazione<th align="left">Sì<th align="left">No
<tr><td>Mostra lo stato dell'installazione di app e profili<td>La pagina relativa allo stato della registrazione viene visualizzata.<td>La pagina relativa allo stato della registrazione non viene visualizzata.
<tr><td>Impedisci l'uso del dispositivo fino al completamento dell'installazione di tutte le app e di tutti i profili<td>Le impostazioni in questa tabella sono rese disponibili per personalizzare il comportamento della pagina relativa allo stato della registrazione, in modo che l'utente possa risolvere potenziali problemi di installazione.
<td>La pagina relativa allo stato della registrazione viene visualizzata senza opzioni aggiuntive per risolvere gli errori di installazione.
<tr><td>Consenti agli utenti di reimpostare il dispositivo se si verifica un errore di installazione<td>Se si verifica un errore di installazione, viene visualizzato un pulsante <b>Reimposta dispositivo</b>.<td>Se si verifica un errore di installazione, il pulsante <b>Reimposta dispositivo</b> non viene visualizzato.
<tr><td>Consenti agli utenti di usare il dispositivo se si verifica un errore di installazione<td>Se si verifica un errore di installazione, viene visualizzato un pulsante <b>Continua comunque</b>.<td>Se si verifica un errore di installazione, il pulsante <b>Continua comunque</b> non viene visualizzato.
<tr><td>Mostra un errore se l'installazione richiede più tempo rispetto al numero di minuti specificato<td colspan="2">Specificare il numero di minuti di attesa per il completamento dell'installazione. Viene immesso un valore predefinito di 60 minuti.
<tr><td>Mostra messaggio personalizzato in caso di errore<td>Viene visualizzata una casella di testo in cui è possibile specificare un messaggio personalizzato da visualizzare se si verifica un errore di installazione.<td>Viene visualizzato il messaggio predefinito: <br><b>L'installazione ha superato il limite di tempo configurato dall'organizzazione. Riprovare o contattare il responsabile del supporto IT per ottenere assistenza.<b>
<tr><td>Consenti agli utenti di raccogliere log sugli errori di installazione<td>Se si verifica un errore di installazione, viene visualizzato un pulsante <b>Raccogli i log</b>. <br>Se l'utente fa clic su questo pulsante, viene chiesto di scegliere un percorso dove salvare il file di log <b>MDMDiagReport. cab</b><td>Se si verifica un errore di installazione, il pulsante <b>Raccogli i log</b> non viene visualizzato.
<tr><td>Blocca l'uso del dispositivo fino all'installazione delle app necessarie in caso di assegnazione a un utente/dispositivo<td colspan="2">Scegliere <b>Tutte</b> o <b>Selezionate</b>. <br><br>Se si sceglie <b>Selezionate</b>, viene visualizzato un pulsante <b>Selezionare le app</b> che consente di scegliere le app da installare prima di abilitare il dispositivo.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>Attivare la pagina relativa allo stato della registrazione predefinita per tutti gli utenti

Per attivare la pagina relativa allo stato della registrazione, eseguire i passaggi descritti di seguito.
 
1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Windows** > **Registrazione Windows** > **Pagina relativa allo stato della registrazione**.
2. Nel pannello **Enrollment Status Page** (Pagina stato registrazione) scegliere **Predefinito** > **Impostazioni**.
3. Per **Show app and profile installation progress** (Visualizza stato di avanzamento installazione app e profilo), scegliere **Sì**.
4. Scegliere le altre impostazioni che si vuole attivare e selezionare **Salva**.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Creare il profilo della pagina relativa allo stato della registrazione e assegnarlo a un gruppo

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Windows** > **Registrazione Windows** > **Pagina relativa allo stato della registrazione** > **Crea profilo**.
2. Specificare un **nome** e una **descrizione**.
3. Scegliere **Crea**.
4. Scegliere il nuovo profilo nell'elenco **Pagina relativa allo stato della registrazione**.
5. Scegliere **Assegnazioni** > **Selezionare i gruppi** > scegliere i gruppi che devono adottare questo profilo > **Seleziona** > **Salva**.
6. Scegliere **Impostazioni** > scegliere le impostazioni che si vuole applicare a questo profilo > **Salva**.

## <a name="set-the-enrollment-status-page-priority"></a>Impostare la priorità della pagina dello stato della registrazione

Un dispositivo o un utente può essere incluso in più gruppi e avere più profili della pagina relativa allo stato della registrazione. Per controllare quali profili vengono considerati per primi, è possibile impostare le priorità per ogni profilo. Quelli con priorità più alta vengono considerati per primi.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Windows** > **Registrazione Windows** > **Pagina relativa allo stato della registrazione**.
2. Passare il mouse sul profilo nell'elenco.
3. Usando i tre punti verticali, trascinare il profilo sulla posizione desiderata nell'elenco.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Impedire l'accesso a un dispositivo fino a quando non viene installata un'applicazione specifica

È possibile specificare quali app devono essere installate prima del completamento della pagina relativa allo stato della registrazione (ESP).

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Windows** > **Registrazione Windows** > **Pagina relativa allo stato della registrazione**.
2. Scegliere un profilo > **Impostazioni**.
3. Scegliere **Sì** per **Mostra lo stato dell'installazione di app e profili**.
4. Scegliere **Sì** per **Impedisci l'uso del dispositivo fino al completamento dell'installazione di tutte le app e di tutti i profili**.
5. Scegliere **Selezionate** per **Blocca l'uso del dispositivo fino all'installazione delle app necessarie in caso di assegnazione a un utente/dispositivo**.
6. Scegliere **Selezionare le app** > scegliere le app > **Seleziona** > **Salva**.

Le app incluse in questo elenco vengono usate da Intune per filtrare l'elenco da considerare per il blocco.  Non specifica quali app devono essere installate.  Se, ad esempio, si configura questo elenco in modo da includere "App 1", "App 2" e "App 3" e "App 3" e "App 4" sono assegnate al dispositivo o all'utente, nella pagina relativa allo stato della registrazione verrà rilevata solo "App 3".  "App 4" verrà comunque installata, ma la pagina relativa allo stato della registrazione non attende il completamento.

È possibile specificare al massimo 100 app.

## <a name="enrollment-status-page-tracking-information"></a>Informazioni incluse nella pagina relativa allo stato della registrazione

La pagina relativa allo stato della registrazione consente di tenere traccia delle informazioni relative a tre fasi: preparazione del dispositivo, configurazione del dispositivo e configurazione dell'account.

### <a name="device-preparation"></a>Preparazione del dispositivo

Per la preparazione del dispositivo, la pagina relativa allo stato della registrazione tiene traccia di quanto segue:

- Attestazione delle chiavi TPM (Trusted Platform Module) (se applicabile)
- Processo di aggiunta ad Azure Active Directory
- Registrazione in Intune (MDM)
- Installazione delle estensioni di gestione di Intune (usate per installare le app Win32)

### <a name="device-setup"></a>Configurazione del dispositivo

La pagina relativa allo stato della registrazione tiene traccia degli elementi seguenti di configurazione del dispositivo:

- Criteri di sicurezza
  - Un provider di servizi di configurazione per tutte le registrazioni.
  - I provider di servizi di configurazione configurati da Intune non vengono tracciati qui.
- Applicazioni
  - App line-of-business di identità del servizio gestita per computer.
  - App dello Store line-of-business con contesto di installazione = dispositivo.
  - App dello Store offline e line-of-business con contesto di installazione = dispositivo.
  - Applicazioni Win32 (solo Windows 10 versione 1903 e successive) 
- Profili di connettività
  - I profili VPN o Wi-Fi sono assegnati a **tutti i dispositivi** o un gruppo di dispositivi di cui il dispositivo di registrazione è membro, ma solo per i dispositivi di Autopilot
- I profili di certificato sono assegnati a **tutti i dispositivi** o un gruppo di dispositivi di cui il dispositivo di registrazione è membro, ma solo per i dispositivi di Autopilot

### <a name="account-setup"></a>Configurazione dell'account

Per la configurazione dell'account, la pagina relativa allo stato della registrazione tiene traccia degli elementi seguenti, se vengono assegnati all'utente attualmente connesso:

- Criteri di sicurezza
  - Un provider di servizi di configurazione per tutte le registrazioni.
  - I provider di servizi di configurazione configurati da Intune non vengono tracciati qui.
- Applicazioni
  - Le app line-of-business di identità del servizio gestita per utente assegnate a tutti i dispositivi, a tutti gli utenti o a un gruppo di utenti di cui l'utente che registra il dispositivo è membro.
  - Le app line-of-business di identità del servizio gestita per computer assegnate a tutti gli utenti o a un gruppo di utenti di cui l'utente che registra il dispositivo è membro.
  - App dello store line-of-business, app dello store online e app dello store offline che vengono assegnate a uno degli oggetti seguenti:
    - Tutti i dispositivi
    - Tutti gli utenti
    - Un gruppo utenti in cui l'utente che registra il dispositivo è un membro con il contesto di installazione impostato su Utente.
  - Applicazioni Win32 (solo Windows 10 versione 1903 e successive) 
- Profili di connettività
  - I profili VPN o Wi-Fi assegnati a tutti gli utenti o a un gruppo di utenti di cui l'utente che registra il dispositivo è membro.
- Certificati
  - I profili di certificato assegnati a tutti gli utenti o a un gruppo di utenti di cui l'utente che registra il dispositivo è membro.

### <a name="troubleshooting"></a>Risoluzione dei problemi

Di seguito sono riportate alcune domande comuni per la risoluzione dei problemi correlati alla pagina relativa allo stato della registrazione.

- Perché le applicazioni non sono state installate e tracciate tramite la pagina Stato registrazione?
  - Per assicurarsi che le applicazioni vengano installate e tracciate tramite la pagina Stato registrazione, verificare che:
      - Le app siano assegnate a un gruppo di Azure AD contenente il dispositivo (per le app destinate ai dispositivi) o l'utente (per le app destinate agli utenti), usando un'assegnazione "obbligatoria".  Le app destinate ai dispositivi vengono tracciate durante la fase dispositivo di ESP, mentre le app destinate agli utenti vengono registrate durante la fase utente di ESP.
      - È possibile specificare **Impedisci l'uso del dispositivo fino al completamento dell'installazione di tutte le app e di tutti i profili** o includere l'app nell'elenco **Blocca l'uso del dispositivo fino all'installazione delle app necessarie**.
      - Le app vengono installate in un contesto di dispositivo e non hanno regole di applicabilità del contesto utente.

- Perché viene visualizzata la pagina relativa allo stato della registrazione per le distribuzioni non di Autopilot, ad esempio quando un utente accede per la prima volta a un dispositivo di Configuration Manager registrato in co-gestione?  
  - La pagina relativa allo stato della registrazione indica lo stato dell'installazione per tutti i metodi di registrazione, tra cui
      - AutoPilot
      - Co-gestione di Configuration Manager
      - quando un nuovo utente accede al dispositivo a cui vengono applicati i criteri della pagina relativa allo stato della registrazione per la prima volta
      - quando l'impostazione **Mostra la pagina solo ai dispositivi sottoposti a provisioning dalla Configurazione guidata** è attiva e il criterio è impostato, solo il primo utente che accede al dispositivo riceve la pagina Stato della registrazione

- Come si disabilita la pagina relativa allo stato della registrazione se è stata configurata nel dispositivo?
  - I criteri della pagina relativa allo stato della registrazione vengono impostati per un dispositivo al momento della registrazione. Per disabilitare la pagina relativa allo stato della registrazione, è necessario disabilitare le sezioni Pagina relativa allo stato della registrazione di dispositivi e utenti. Le sezioni vengono disabilitate creando impostazioni URI OMA personalizzate con le configurazioni seguenti.

      Disabilitare la pagina relativa allo stato della registrazione dell'utente:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Disabilitare la pagina relativa allo stato della registrazione del dispositivo:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- Come si raccolgono i file di log?
  - Esistono due modi per raccogliere i file di log della pagina relativa allo stato della registrazione:
      - Consentire agli utenti di raccogliere i log nei criteri ESP. Quando si verifica un timeout nella pagina relativa allo stato della registrazione, l'utente finale può scegliere di **raccogliere i log**. Se si inserisce un'unità USB, i file di log possono essere copiati nell'unità
      - Aprire un prompt dei comandi immettendo la sequenza di tasti MAIUSC-F10, quindi immettere la seguente riga di comando per generare i file di log: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>Problemi noti

Di seguito sono riportati i problemi noti correlati alla pagina relativa allo stato della registrazione.

- La disabilitazione del profilo ESP non comporta la rimozione dei criteri ESP dai dispositivi e gli utenti ottengono comunque ESP quando accedono al dispositivo per la prima volta. I criteri non vengono rimossi quando il profilo ESP è disabilitato. Per disabilitare ESP, è necessario distribuire URI OMA. Vedere sopra per le istruzioni su come disabilitare ESP usando URI OMA. 
- Un riavvio durante la configurazione del dispositivo obbliga l'utente a immettere le proprie credenziali prima di passare alla fase di configurazione dell'account. Le credenziali utente non vengono mantenute durante il riavvio. Chiedere all'utente di immettere le credenziali, quindi la pagina relativa allo stato della registrazione può continuare. 
- La pagina relativa allo stato della registrazione raggiunge sempre il timeout durante l'aggiunta di un account aziendale e dell'istituto di istruzione nelle versioni di Windows 10 precedenti alla 1903. La pagina relativa allo stato della registrazione attende il completamento della registrazione di Azure AD. Il problema è risolto in Windows 10 versione 1903 e successive.  
- In Azure AD ibrido la distribuzione di Autopilot con ESP richiede più tempo rispetto alla durata del timeout definita nel profilo ESP. Nelle distribuzioni di Autopilot di Azure AD ibrido ESP richiede 40 minuti in più rispetto al valore impostato nel profilo ESP. Questo ritardo concede tempo al connettore AD locale per creare il nuovo record del dispositivo per Azure AD. 
- La pagina di accesso di Windows non viene preventivamente popolata con il nome utente nella modalità definita dall'utente di Autopilot. Se avviene un riavvio durante la fase di configurazione del dispositivo di ESP:
  - le credenziali utente non vengono mantenute
  - l'utente deve immettere di nuovo le credenziali prima di procedere dalla fase di configurazione del dispositivo alla fase di configurazione dell'account
- ESP è bloccato per molto tempo o non completa mai la fase di identificazione. Intune calcola i criteri di ESP durante la fase di identificazione. Un dispositivo non può mai completare l'elaborazione dei criteri ESP se all'utente corrente non è assegnata una licenza di Intune.  
- La configurazione del controllo di applicazioni di Microsoft Defender comporta una richiesta di riavvio durante la fase di Autopilot. Per la configurazione dell'applicazione Microsoft Defender (provider del servizio di crittografia AppLocker) è necessario un riavvio. Quando questo criterio è configurato, può causare il riavvio di un dispositivo durante la fase di Autopilot. Attualmente non è possibile impedire o posticipare il riavvio.
- Quando il criterio DeviceLock (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) è abilitato come parte di un profilo ESP, il file OOBE o l'accesso automatico al desktop utente potrebbe non riuscire in modo inaspettato per due motivi.
  - Se il dispositivo non è stato riavviato prima di uscire dalla fase di configurazione del dispositivo di ESP, all'utente può essere richiesto di immettere le credenziali di Azure AD. Questa richiesta si verifica al posto di un accesso automatico con esito positivo in cui l'utente visualizza la prima animazione dell'accesso di Windows.
  - L'accesso automatico avrà esito negativo se il dispositivo è stato riavviato dopo che l'utente ha immesso le proprie credenziali di Azure AD ma prima di uscire dalla fase di configurazione del dispositivo di ESP. Questo errore si verifica perché la fase di configurazione del dispositivo di ESP non è mai stata completata. La soluzione alternativa consiste nel reimpostare il dispositivo.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato le pagine di registrazione di Windows, è necessario imparare a gestire i dispositivi Windows. Per altre informazioni, vedere [Informazioni sulla gestione dei dispositivi in Microsoft Intune](../remote-actions/device-management.md).
