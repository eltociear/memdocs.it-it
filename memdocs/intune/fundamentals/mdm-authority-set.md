---
title: Impostare l'autorità di gestione dei dispositivi mobili
titleSuffix: Microsoft Intune
description: Impostare l'autorità di gestione dei dispositivi mobili in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 676e7a4db54558eaea87ad2fa8efbe8af546f035
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996572"
---
# <a name="set-the-mobile-device-management-authority"></a>Impostare l'autorità di gestione dei dispositivi mobili

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

L'impostazione dell'autorità di gestione dei dispositivi mobili (MDM) determina la modalità di gestione dei dispositivi. L'amministratore IT deve impostare un'autorità MDM prima che gli utenti possano registrare i dispositivi per la gestione.

Le configurazioni possibili sono:

- **Intune autonomo**: gestione solo cloud, che viene configurata tramite il portale di Azure. Include il set completo di funzionalità offerte da Intune. [Impostare l'autorità MDM nella console di Intune](#set-mdm-authority-to-intune).

- **Co-gestione di Intune**: integrazione della soluzione cloud di Intune con Configuration Manager per dispositivi Windows 10. Intune viene configurato tramite la console di Configuration Manager. [Configurare la registrazione automatica dei dispositivi in Intune](/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune). 

- **Mobilità e sicurezza di base per Microsoft 365**: se è stata attivata questa configurazione, l'autorità MDM sarà impostata su "Microsoft 365". Se si vuole iniziare a usare Intune, sarà necessario acquistare licenze di Intune.

- **[Coesistenza](#coexistence) con la funzionalità di mobilità e sicurezza di base per Microsoft 365**: è possibile aggiungere Intune al tenant se si usa già la funzionalità di mobilità e sicurezza di base per Microsoft 365 e impostare l'autorità di gestione su Intune o su questa funzionalità per ogni utente per determinare quale servizio verrà usato per gestire i dispositivi registrati in MDM. L'autorità di gestione di ogni utente è definita in base alla licenza assegnata all’utente. Se l'utente ha solo una licenza per Microsoft 365 Basic o Standard, i dispositivi saranno gestiti dalla funzionalità di mobilità e sicurezza di base per Microsoft 365. Se, invece, dispone di una licenza che applica Intune, i dispositivi saranno gestiti da Intune. Se si aggiunge una licenza che applica Intune a un utente precedentemente gestito dalla funzionalità di mobilità e sicurezza di base per Microsoft 365, i dispositivi passeranno alla gestione di Intune. Assicurarsi di aver assegnato agli utenti le configurazioni di Intune per sostituire la funzionalità di mobilità e sicurezza di base per Microsoft 365 prima di trasferirli su Intune. In caso contrario, i dispositivi degli utenti perderanno la configurazione della funzionalità di mobilità e sicurezza di base per Microsoft 365 e non riceveranno alcuna sostituzione da Intune.

## <a name="set-mdm-authority-to-intune"></a>Impostare l'autorità MDM su Intune

Per i tenant che usano la versione del servizio 1911 e versioni successive, l'autorità MDM viene impostata automaticamente su Intune.

Per i tenant con versione del servizio precedente a 1911, se l'autorità MDM non è stata ancora impostata, seguire questa procedura.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare l'intestazione arancione per aprire l’impostazione **Autorità di gestione dei dispositivi mobili**. L'intestazione arancione viene visualizzata solo se l'autorità MDM non è stata ancora impostata.
2. In **Autorità di gestione dei dispositivi mobili** scegliere una delle opzioni seguenti per l'autorità MDM:
  - **Autorità MDM Intune**
  - **Nessuno**

  ![Immagine della schermata di impostazione dell’autorità di gestione dei dispositivi mobili di Intune](./media/mdm-authority-set/set-mdm-auth.png)

  Un messaggio indica che l'autorità MDM è stata impostata su Intune.

### <a name="workflow-of-intune-administration-ui"></a>Flusso di lavoro dell'interfaccia utente di amministrazione di Intune
Quando è abilitata la gestione dei dispositivi Android o Apple, Intune invia informazioni sul dispositivo e sull'utente da integrare con i servizi di terze parti per la gestione dei rispettivi dispositivi.

Gli scenari con il consenso alla condivisione dei dati vengono inclusi se:
- Si abilitano i profili di lavoro Android.
- Si abilitano e caricano i certificati per le notifiche push MDM Apple.
- Si abilita uno dei servizi Apple, ad esempio Device Enrollment Program, School Manager o Volume Purchasing Program.

In ogni caso, il consenso è strettamente correlato all'esecuzione di un servizio di gestione dei dispositivi mobili. Ad esempio, verificare che l'amministratore IT abbia autorizzato la registrazione di dispositivi Google o Apple. La documentazione da consultare per sapere quali informazioni vengono condivise quando vengono pubblicati i nuovi flussi di lavoro è disponibile nelle posizioni seguenti:
- [Dati inviati da Intune a Google](https://aka.ms/Data-intune-sends-to-google)
- [Dati inviati da Intune ad Apple](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Considerazioni principali
Dopo il passaggio alla nuova autorità MDM, è probabile che vi sia un tempo di transizione (fino a otto ore) prima dell'archiviazione del dispositivo e della sua sincronizzazione con il servizio. È necessario configurare le impostazioni nella nuova autorità MDM per fare in modo che i dispositivi registrati continuino a essere gestiti e protetti dopo la modifica. 
- I dispositivi devono connettersi con il servizio dopo la modifica, in modo che le impostazioni dalla nuova autorità MDM (versione autonoma di Intune) sostituiscano le impostazioni esistenti nel dispositivo.
- Dopo aver cambiato l'autorità MDM, alcune impostazioni di base dell'autorità MDM precedente, come ad esempio i profili, rimarranno nel dispositivo per un massimo di sette giorni o fino a quando il dispositivo stesso non si connetterà al servizio per la prima volta. È consigliabile configurare le app e le impostazioni (ad esempio criteri, profili e app) nella nuova autorità MDM appena possibile e distribuire le impostazioni ai gruppi di utenti in cui sono presenti utenti che hanno già dispositivi registrati. Non appena un dispositivo si connette al servizio dopo che l'autorità MDM è stata cambiata, riceve le nuove impostazioni dall'autorità MDM impedendo che vi siano vuoti nella gestione e protezione.
- Per i dispositivi senza utenti associati (in genere con il Device Enrollment Program per dispositivi iOS/iPadOS o con scenari di registrazione in blocco) non viene eseguita la migrazione alla nuova autorità MDM. Per tali dispositivi è necessario chiamare il supporto tecnico per chiedere assistenza nel passaggio alla nuova autorità MDM.

## <a name="coexistence"></a>Coexistence

L'abilitazione della coesistenza consente di usare Intune per un nuovo set di utenti continuando allo stesso tempo a usare la funzionalità di mobilità e sicurezza di base per gli utenti esistenti. Si ha il controllo dei dispositivi gestiti da Intune tramite l'utente. Se un utente ha una licenza di Intune assegnata o usa la co-gestione di Intune con Configuration Manager, tutti i suoi dispositivi registrati verranno gestiti da Intune. In caso contrario, l'utente viene gestito dalla funzionalità di mobilità e sicurezza di base.

La coesistenza viene abilitata con tre passaggi principali:
1. Preparazione
2. Aggiungere l'autorità MDM Intune
3. Migrazione di utenti e dispositivi (facoltativo).

### <a name="preparation"></a>Preparazione

Prima di abilitare la coesistenza con la funzionalità di mobilità e sicurezza di base, considerare i punti seguenti:
- Assicurarsi di avere un numero di [licenze di Intune](licenses.md) sufficiente per gli utenti da gestire tramite Intune.
- Verificare a quali utenti sono assegnate licenze di Intune. Dopo aver abilitato la coesistenza, i dispositivi degli utenti a cui è già stata assegnata una licenza di Intune passeranno a Intune. Per evitare cambi di dispositivi imprevisti, è consigliabile non assegnare licenze di Intune fino a quando non è stata abilitata la coesistenza.
- Creare e distribuire i criteri di Intune per sostituire i criteri di sicurezza dei dispositivi originariamente distribuiti tramite il portale Sicurezza e conformità di Office 365. Questa sostituzione deve essere eseguita per tutti gli utenti che si prevede di spostare dalla funzionalità di mobilità e sicurezza di base a Intune. Se non sono assegnati criteri di Intune a questi utenti, l'abilitazione della coesistenza può comportare la perdita delle impostazioni di mobilità e sicurezza di base. Queste impostazioni andranno perse senza sostituzione, come ad esempio i profili di posta elettronica gestiti. Anche se si sostituiscono i criteri di sicurezza dei dispositivi con i criteri di Intune, gli utenti potrebbero ricevere la richiesta di ripetere l'autenticazione dei loro profili di posta elettronica dopo lo spostamento dei dispositivi nella gestione di Intune.

### <a name="add-intune-mdm-authority"></a>Aggiungere l'autorità MDM Intune

Per abilitare la coesistenza, è necessario aggiungere Intune come autorità MDM per l'ambiente in uso:

1. Accedere a endpoint.microsoft.com con i diritti di amministratore del servizio Intune o di amministratore globale di Azure AD.
2. Passare a **Dispositivi**.
3. Viene visualizzato il pannello **Aggiungi autorità MDM**.
4. Per cambiare l'autorità MDM da *Office 365* a *Intune* e abilitare la coesistenza, selezionare **Autorità MDM Intune** > **Aggiungi**.
  ![Screenshot della schermata Aggiungi autorità MDM](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>Eseguire la migrazione di utenti e dispositivi (facoltativo)

Una volta abilitata l'autorità MDM Intune, viene attivata la coesistenza e si può iniziare a gestire gli utenti tramite Intune. Se si vuole che i dispositivi precedentemente gestiti dalla funzionalità di mobilità e sicurezza di base vengano ora gestiti da Intune, assegnare agli utenti corrispondenti una licenza di Intune. I dispositivi degli utenti passeranno a Intune alla successiva sincronizzazione di MDM. Le impostazioni applicate a questi dispositivi tramite la funzionalità di mobilità e sicurezza di base non verranno più applicate e verranno rimosse dai dispositivi.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Pulizia dei dispositivi mobili dopo la scadenza del certificato MDM

Il certificato MDM viene rinnovato automaticamente quando i dispositivi mobili comunicano con il servizio Intune. In caso di cancellazione dei dati dei dispositivi mobili o se questi non riescono a comunicare con il servizio Intune per un determinato periodo di tempo, il certificato MDM non verrà rinnovato. Il dispositivo viene rimosso dal portale di Azure 180 giorni dopo la scadenza del certificato MDM.

## <a name="remove-mdm-authority"></a>Rimuovere l'autorità MDM

Non è possibile reimpostare l'autorità MDM su Sconosciuto. L'autorità MDM è usata dal servizio per determinare il portale di registrazione a cui fanno riferimento i dispositivi (Microsoft Intune o la funzionalità di mobilità e sicurezza di base per Microsoft 365).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>Conseguenze della modifica dell'autorità MDM

- Quando il servizio Intune rileva che l'autorità MDM di un tenant è cambiata, invia un messaggio di notifica a tutti i dispositivi registrati perché eseguano l'archiviazione e la sincronizzazione con il servizio (questa notifica è al di fuori delle normali archiviazioni pianificate). Di conseguenza, dopo la modifica dell'autorità MDM per il tenant da Intune autonomo, tutti i dispositivi accesi e online si connetteranno al servizio, riceveranno la nuova autorità MDM e da quel momento saranno gestiti dall'autorità MDM. La gestione e la protezione di questi dispositivi non subisce alcuna interruzione.
- Anche se i dispositivi sono accesi e online durante (o immediatamente dopo) la modifica nell'autorità MDM, ci sarà un ritardo massimo di otto ore (a seconda del momento della successiva archiviazione periodica pianificata) prima che i dispositivi siano registrati per il servizio con la nuova autorità MDM.  

 > [!IMPORTANT]  
 > Tra il momento in cui si cambia l'autorità MDM e quello in cui viene caricato il certificato rinnovato del servizio APN per la nuova autorità, le nuove registrazioni e le nuove sincronizzazioni di dispositivi iOS/iPadOS hanno esito negativo. Pertanto è importante analizzare e caricare il certificato APN per la nuova autorità al più presto dopo la modifica nell'autorità MDM.

- Gli utenti possono passare rapidamente alla nuova autorità MDM avviando manualmente un'archiviazione dal dispositivo al servizio. Possono farlo facilmente usando l'app Portale aziendale e avviando un controllo di conformità del dispositivo.
- Per verificare che tutto funzioni correttamente dopo che i dispositivi sono stati archiviati e sincronizzati con il servizio dopo la modifica dell'autorità MDM, cercare i dispositivi nella nuova autorità MDM.
- Ci sarà un periodo intermedio da quando un dispositivo è offline durante il cambio dell'autorità MDM a quando il dispositivo viene sincronizzato con il servizio. Per garantire che il dispositivo rimanga protetto e funzionale durante questo periodo, i profili seguenti rimangono nel dispositivo per un massimo di sette giorni o fino a quando il dispositivo non si connette con la nuova autorità MDM e riceve le nuove impostazioni che sovrascrivono quelle esistenti:
   - Profilo di posta elettronica
   - Profilo VPN
   - Profilo certificato
   - Profilo Wi-Fi
   - Profili di configurazione
- Dopo il passaggio alla nuova autorità MDM, i dati di conformità nella console di amministrazione di Microsoft Intune possono richiedere fino a una settimana per un reporting preciso. Tuttavia, gli stati di conformità in Azure Active Directory e nel dispositivo sono accurati. Il dispositivo, quindi, è comunque protetto.
- Verificare che le nuove impostazioni che devono sovrascrivere quelle esistenti abbiano lo stesso nome delle precedenti per garantire che le impostazioni precedenti vengano sovrascritte. In caso contrario, i dispositivi potrebbero finire con criteri e profili ridondanti.  

 > [!TIP]  
 > Come procedura consigliata è necessario creare tutte le impostazioni di gestione e le configurazioni, nonché le distribuzioni, subito dopo aver completato la modifica dell'autorità MDM. Questo contribuisce a garantire la protezione e la gestione attiva dei dispositivi durante il periodo intermedio.

- Dopo aver modificato l'autorità MDM, eseguire la procedura seguente per verificare che i nuovi dispositivi siano registrati correttamente con la nuova autorità:  
 - Registrare un nuovo dispositivo
 - Assicurarsi che il dispositivo appena registrato sia visualizzato nell'autorità MDM.
 - Eseguire un'azione, ad esempio il blocco remoto, dalla console di amministrazione al dispositivo. Se l'azione ha esito positivo, il dispositivo è gestito dalla nuova autorità MDM.
- Nel caso di problemi con dispositivi specifici, è possibile annullare e ripetere la registrazione dei dispositivi in modo che siano connessi alla nuova autorità e gestiti il più rapidamente possibile.

## <a name="next-steps"></a>Passaggi successivi

Con il set di autorità MDM, è possibile iniziare la [registrazione dei dispositivi](../enrollment/device-enrollment.md).