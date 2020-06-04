---
title: Gestire la sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Informazioni su come gli amministratori della sicurezza possono usare il nodo di sicurezza degli endpoint per gestire la sicurezza dei dispositivi e risolvere i problemi dei dispositivi in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 99ac1e069386c69011543ac40878dd62a0d50527
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990818"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Gestire la sicurezza degli endpoint in Microsoft Intune

Come amministratore della sicurezza, usare il nodo *Sicurezza degli endpoint* in Intune per configurare la sicurezza del dispositivo e gestire le attività di sicurezza per i dispositivi quando tali dispositivi sono a rischio. I criteri di sicurezza degli endpoint sono progettati per consentire all'utente di concentrarsi sulla sicurezza dei dispositivi e di attenuare i rischi. Le attività disponibili consentono di identificare i dispositivi a rischio, correggere i dispositivi e ripristinarli in uno stato conforme o più sicuro.

Il nodo Sicurezza degli endpoint raggruppa gli strumenti disponibili tramite Intune che verranno usati per proteggere i dispositivi:

- **Controllare lo stato di tutti i dispositivi gestiti**. Usare la vista [Tutti i dispositivi](#manage-devices) in cui è possibile visualizzare la conformità dei dispositivi da un livello elevato e quindi analizzare i dispositivi specifici per comprendere quali criteri di conformità non sono soddisfatti, in modo da poterli risolvere.

- **Distribuire le baseline di sicurezza che stabiliscono le configurazioni di sicurezza delle procedure consigliate per i dispositivi**. Intune include [baseline di sicurezza](#manage-security-baselines) per i dispositivi Windows e un elenco in continua crescita di applicazioni, ad esempio Microsoft Defender Advanced Threat Protection (Defender ATP) e Microsoft Edge. Le baseline di sicurezza sono gruppi preconfigurati di impostazioni di Windows che consentono di applicare un gruppo di impostazioni e valori predefiniti noti, consigliati dai team di sicurezza pertinenti.

- **Gestire le configurazioni di sicurezza nei dispositivi mediante criteri strettamente mirati**.  Ogni [criterio di sicurezza degli endpoint](#use-policies-to-manage-device-security) si concentra sugli aspetti della sicurezza dei dispositivi, ad esempio antivirus, crittografia del disco, firewall e diverse aree rese disponibili tramite l'integrazione con Defender ATP.

- **Definire i requisiti per i dispositivi e gli utenti tramite i criteri di conformità**. Con i [criteri di conformità](../protect/device-compliance-get-started.md), è possibile impostare le regole che i dispositivi e gli utenti devono soddisfare per essere considerati conformi. Le regole possono includere le versioni del sistema operativo, i requisiti per le password, i livelli di minaccia del dispositivo e altro ancora.

  Quando si integrano con Azure Active Directory (Azure AD) i [criteri di accesso condizionale](#configure-conditional-access) per applicare i criteri di conformità, è possibile controllare l'accesso alle risorse aziendali per i dispositivi gestiti e i dispositivi che non sono ancora gestiti.

- **Integrare Intune con il team di Microsoft Defender ATP**. Grazie all'[integrazione con Defender ATP](#set-up-integration-with-defender-atp) si ottiene l'accesso alle [attività di sicurezza](#review-security-tasks-from-defender-atp). Le attività di sicurezza sono strettamente associate a Defender ATP e Intune per consentire al team di sicurezza di identificare i dispositivi a rischio e le procedure di correzione dettagliate per gli amministratori di Intune che possono intervenire.

Le sezioni seguenti di questo articolo illustrano le diverse attività che è possibile eseguire dal nodo Sicurezza degli endpoint dell'interfaccia di amministrazione e le autorizzazioni di controllo degli accessi in base al ruolo (RBAC) necessarie per usarle.

## <a name="manage-devices"></a>Gestire dispositivi

Il nodo Sicurezza degli endpoint include la vista *Tutti i dispositivi*, in cui è possibile visualizzare un elenco di tutti i dispositivi da Azure AD disponibili in Microsoft Endpoint Manager.

Da questa vista è possibile selezionare i dispositivi di cui eseguire un'analisi approfondita per ottenere altre informazioni, ad esempio i criteri a cui un dispositivo non è conforme. È anche possibile usare l'accesso da questa vista per correggere i problemi relativi a un dispositivo, ad esempio riavviare un dispositivo, eseguire la ricerca di malware o ruotare le chiavi di BitLocker in un dispositivo Windows 10.

Per altre informazioni, vedere [Gestire i dispositivi con la sicurezza degli endpoint in Microsoft Intune](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Gestire le baseline di sicurezza

Le baseline di sicurezza in Intune sono gruppi pre-configurati di impostazioni che rappresentano indicazioni sulle procedure consigliate dei team di sicurezza Microsoft pertinenti per il prodotto. Intune supporta le baseline di sicurezza per le impostazioni dei dispositivi Windows 10, Microsoft Edge, Microsoft Defender Advanced Threat Protection e altro ancora.

È possibile usare le baseline di sicurezza per distribuire rapidamente una configurazione di *procedure consigliate* delle impostazioni del dispositivo e dell'applicazione per proteggere gli utenti e i dispositivi. Le baseline di sicurezza sono supportate per i dispositivi che eseguono Windows 10 versione 1809 e successive.

Per altre informazioni, vedere [Usare le baseline di sicurezza per configurare i dispositivi Windows 10 in Intune](../protect/security-baselines.md).

Le baseline di sicurezza sono uno dei diversi metodi di Intune per configurare le impostazioni nei dispositivi. Quando si gestiscono le impostazioni, è importante comprendere quali altri metodi sono in uso nell'ambiente per configurare i dispositivi in modo che sia possibile evitare conflitti. Vedere [Evitare conflitti di criteri](#avoid-policy-conflicts) più avanti in questo articolo.

## <a name="review-security-tasks-from-defender-atp"></a>Esaminare le attività di sicurezza da Defender ATP

Quando si integra Intune con Microsoft Defender Advanced Threat Protection (Defender ATP), è possibile esaminare le *attività di sicurezza* in Intune che identificano i dispositivi a rischio e specificano i passaggi per attenuare il rischio. È quindi possibile usare le attività per segnalare a Defender ATP quando questi rischi vengono attenuati correttamente.

- Il team di Defender ATP determina i dispositivi a rischio e passa tali informazioni al team di Intune come attività di sicurezza. Con pochi clic, viene creata un'attività di sicurezza per Intune che identifica i dispositivi a rischio, la vulnerabilità e fornisce indicazioni su come attenuare il rischio.

- Gli amministratori di Intune ricontrollano le attività di sicurezza e quindi agiscono in Intune per correggere tali attività. Una volta attenuato, l'attività viene impostata su completa, comunicando tale stato al team Defender ATP.

Attraverso le attività di sicurezza entrambi i team rimangono sincronizzati su quali dispositivi sono a rischio e su come e quando tali rischi vengono corretti.

Per altre informazioni sull'uso delle attività di sicurezza, vedere [Usare Intune per risolvere le vulnerabilità identificate da Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Usare i criteri per gestire la sicurezza dei dispositivi

Come amministratore della sicurezza, usare i criteri di sicurezza disponibili in *Gestisci* nel nodo Sicurezza degli endpoint. Con questi criteri è possibile configurare la sicurezza del dispositivo senza l'overhead associato all'esplorazione del corpo e della gamma più ampi di impostazioni dai profili di configurazione dei dispositivi e dalle baseline di sicurezza.

![Gestire i criteri](./media/endpoint-security/endpoint-security-policies.png)

Per altre informazioni sull'uso di questi criteri di sicurezza, vedere [Gestire la sicurezza dei dispositivi con i criteri di sicurezza degli endpoint](../protect/endpoint-security-policy.md).

I criteri di sicurezza degli endpoint sono uno dei diversi metodi di Intune per configurare le impostazioni nei dispositivi. Quando si gestiscono le impostazioni, è importante comprendere quali altri metodi sono in uso nell'ambiente per configurare i dispositivi ed evitare i conflitti. Vedere [Evitare conflitti di criteri](#avoid-policy-conflicts) più avanti in questo articolo.

In *Gestisci* sono anche disponibili i criteri di *Conformità del dispositivo* e *Accesso condizionale*. Questi tipi di criteri non sono criteri di sicurezza mirati per la configurazione degli endpoint, ma sono strumenti importanti per la gestione dei dispositivi e l'accesso alle risorse aziendali.

## <a name="use-device-compliance-policy"></a>Usare i criteri di conformità dei dispositivi

Usare i criteri di conformità dei dispositivi per stabilire le condizioni in base alle quali i dispositivi e gli utenti sono autorizzati ad accedere alla rete e alle risorse aziendali.

Le [impostazioni di conformità disponibili](../protect/device-compliance-get-started.md#next-steps) dipendono dalla piattaforma utilizzata, ma le regole dei criteri comuni includono:

- Richiedere che i dispositivi eseguano una versione del sistema operativo minima o specifica
- Impostare i requisiti per le password
- Specificare un livello di minaccia massimo consentito per il dispositivo, determinato da Defender ATP o da un altro partner di Mobile Threat Defense

Oltre alle regole dei criteri, i criteri di conformità supportano:

- [Posizioni](../protect/use-network-locations.md) definite in Intune. Quando si usano le posizioni con un criterio di conformità, il criterio può garantire che i dispositivi siano connessi a una rete aziendale per essere conformi.
- [Azioni per la mancata conformità](../protect/actions-for-noncompliance.md). Queste azioni sono una sequenza temporale di azioni da applicare ai dispositivi non conformi. Le azioni includono l'invio di messaggi di posta elettronica o notifiche per avvisare gli utenti del dispositivo sulla mancata conformità, il blocco remoto dei dispositivi o anche il ritiro di dispositivi non conformi e la rimozione di eventuali dati aziendali che potrebbero essere presenti sullo stesso.

Quando si integra Intune con i [criteri di accesso condizionale](#configure-conditional-access) di Azure AD per applicare i criteri di conformità, l'accesso condizionale può usare i dati di conformità per controllare l'accesso alle risorse aziendali sia per i dispositivi gestiti sia per i dispositivi non gestiti.

Per altre informazioni, vedere [Impostare regole sui dispositivi per consentire l'accesso alle risorse dell'organizzazione tramite Intune](../protect/device-compliance-get-started.md).

I criteri di conformità dei dispositivi sono uno dei diversi metodi di Intune per configurare le impostazioni nei dispositivi. Quando si gestiscono le impostazioni, è importante comprendere quali altri metodi sono in uso nell'ambiente per configurare i dispositivi ed evitare i conflitti. Vedere [Evitare conflitti di criteri](#avoid-policy-conflicts) più avanti in questo articolo.

## <a name="configure-conditional-access"></a>Configurare l'accesso condizionale

Per proteggere i dispositivi e le risorse aziendali, è possibile usare i criteri di accesso condizionale di Azure Active Directory (Azure AD) con Intune.

Intune passa i risultati dei criteri di conformità del dispositivo ad Azure AD, che quindi usa i criteri di accesso condizionale per stabilire quali dispositivi e app possono accedere alle risorse aziendali. I criteri di accesso condizionale consentono di controllare l'accesso per i dispositivi che non sono gestiti da Intune. È anche possibile usare i dettagli di conformità dai [partner di Mobile Threat Defense](../protect/mobile-threat-defense.md) integrati con Intune.

Di seguito sono riportati due metodi comuni per l'uso dell'accesso condizionale con Intune:

- **Accesso condizionale basato su dispositivo**, per garantire che solo i dispositivi gestiti e conformi possano accedere alle risorse di rete.
- **Accesso condizionale basato su app**, che usa i criteri di protezione delle app per gestire l'accesso alle risorse di rete da parte degli utenti nei dispositivi che non vengono gestiti con Intune.

Per altre informazioni sull'uso dell'accesso condizionale con Intune, vedere [Informazioni sull'accesso condizionale e su Intune](../protect/conditional-access.md).

## <a name="set-up-integration-with-defender-atp"></a>Configurare l'integrazione con Defender ATP

Quando si integra Microsoft Defender Advanced Threat Protection (Defender ATP) con Intune, si migliora la capacità di identificare e rispondere ai rischi.

Sebbene Intune possa integrarsi con diversi [partner di Mobile Threat Defense](../protect/mobile-threat-defense.md), quando si usa Defender ATP si ottiene una stretta integrazione tra Defender ATP e Intune con accesso a opzioni approfondite di protezione dei dispositivi, tra cui:

- Attività di sicurezza: comunicazione senza discontinuità tra gli amministratori di ATP e Intune sui dispositivi a rischio, come risolvere i problemi e conferma quando questi rischi vengono attenuati.
- Onboarding semplificato per Defender ATP sui client.
- Uso dei segnali di rischio del dispositivo ATP nei criteri di conformità di Intune.
- Accesso alle funzionalità di *Protezione antimanomissione*.

 Per altre informazioni sull'uso di Defender ATP con Intune, vedere [Applicare la conformità per Microsoft Defender ATP con l'accesso condizionale in Intune](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Requisiti per il controllo degli accessi in base al ruolo

Per gestire le attività nel nodo Sicurezza degli endpoint dell'interfaccia di amministrazione di Microsoft Endpoint Manager, un account deve:

- Avere assegnata una licenza per Intune.
- Disporre delle autorizzazioni di controllo degli accessi in base al ruolo (RBAC) equivalenti alle autorizzazioni fornite dal ruolo predefinito di Intune di **Endpoint Security Manager**. Il ruolo *Endpoint Security Manager* concede l'accesso all'interfaccia di amministrazione di Microsoft Endpoint Manager. Questo ruolo può essere usato da utenti che gestiscono le funzionalità di sicurezza e conformità, tra cui le baseline di sicurezza, la conformità dei dispositivi, l'accesso condizionale e Microsoft Defender ATP.

Per altre informazioni, vedere [Controllo degli accessi in base al ruolo (RBAC) con Microsoft Intune](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Autorizzazioni concesse dal ruolo *Endpoint Security Manager*

È possibile visualizzare l'elenco di autorizzazioni seguente nell'interfaccia di amministrazione di Microsoft Endpoint Manager accedendo ad **Amministrazione del tenant** > **Ruoli** > **Tutti i ruoli**, selezionare **Endpoint Security Manager** > **Proprietà**.

**Autorizzazioni:**

- **Android for Work**
  - Lettura
- **Dati di controllo**
  - Lettura
- **Identificatori dei dispositivi aziendali**
  - Lettura
- **Criteri di conformità dei dispositivi**
  - Assegnazione
  - Creazione
  - Elimina
  - Lettura
  - Aggiornamento
  - Visualizzare i report
- **Configurazioni del dispositivo**
  - Lettura
- **Manager di registrazione dispositivi**
  - Lettura
- **Report di Endpoint Protection**
  - Lettura
- **Programmi di registrazione**
  - Lettura del dispositivo
  - Lettura del profilo
  - Lettura del token
- **Data warehouse di Intune**
  - Lettura
- **App gestite**
  - Lettura
- **Dispositivi gestiti**
  - Elimina
  - Lettura
  - Impostazione utente primario
  - Aggiornamento
- **App per dispositivi mobili**
  - Lettura
- **Organizzazione**
  - Lettura
- **Set di criteri**
  - Lettura
- **Assistenza remota**
  - Lettura
- **Attività remote**
  - Ottieni la chiave del FileVault.
- **Ruoli**
  - Lettura
- **Baseline di sicurezza**
  - Assegnazione
  - Creazione
  - Elimina
  - Lettura
  - Aggiornamento
- **Attività di sicurezza**
  - Lettura
  - Aggiornamento
- **Spese per telecomunicazioni**
  - Lettura
- **Termini e condizioni**
  - Lettura

## <a name="avoid-policy-conflicts"></a>Evitare conflitti di criteri

Molte delle impostazioni che è possibile configurare per i dispositivi possono essere gestite da diverse funzionalità di Intune. Queste funzionalità includono, tra le altre:

- Criteri di sicurezza degli endpoint
- Baseline di sicurezza
- Criteri di configurazione del dispositivo
- Criteri di registrazione di Windows 10

Ad esempio, le impostazioni disponibili nei criteri di sicurezza degli endpoint sono un subset delle impostazioni disponibili nei profili di *protezione degli endpoint* e *restrizioni dei dispositivi* nei criteri di configurazione del dispositivo e che vengono gestiti anche tramite diverse baseline di sicurezza.

Un modo per evitare conflitti consiste nel non usare diverse baseline, istanze della stessa baseline o tipi di criteri e istanze diversi per gestire le stesse impostazioni in un dispositivo. Questa operazione richiede la pianificazione dei metodi che verranno usati per distribuire le configurazioni a dispositivi diversi. Quando si usano più metodi o istanze dello stesso metodo per configurare la stessa impostazione, assicurarsi che i diversi metodi accettino o non vengano distribuiti negli stessi dispositivi.

In caso di conflitti, è possibile usare gli strumenti incorporati di Intune per identificare e risolvere l'origine dei conflitti. Per altre informazioni, vedere:

- [Risolvere problemi relativi a criteri e profili in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorare le baseline di sicurezza](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Passaggi successivi

Configurare:

- [Baseline di sicurezza](../protect/security-baselines.md)
- [Criteri di conformità](../protect/device-compliance-get-started.md)
- [Criteri di accesso condizionale](#configure-conditional-access)
- [Integrazione con Defender ATP](../protect/advanced-threat-protection.md)
