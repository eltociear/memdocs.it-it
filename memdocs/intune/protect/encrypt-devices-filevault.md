---
title: Crittografare i dispositivi macOS con la crittografia del disco FileVault in Intune
titleSuffix: Microsoft Intune
description: Crittografare i dispositivi macOS con il metodo di crittografia predefinito FileVault e gestire le chiavi di ripristino per tali dispositivi crittografati all'interno del portale di Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 1f2a6955a430427fe3f4e2791da6bbaecdd90523
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353573"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Usare la crittografia del disco FileVault di macOS con Intune

Intune supporta la crittografia del disco FileVault di macOS. FileVault è un programma di crittografia per dischi interi incluso in macOS. È possibile usare Intune per configurare FileVault nei dispositivi che eseguono **macOS 10.13 o versione successiva**.

Usare uno dei tipi di criteri seguenti per configurare FileVault nei dispositivi gestiti:

- **[Criteri di sicurezza degli endpoint per FileVault di macOS](#create-endpoint-security-policy-for-filevault)** . Il profilo FileVault in *Endpoint security* (Sicurezza degli endpoint) è un gruppo in evidenza di impostazioni dedicato alla configurazione di FileVault.

  Visualizzare le [impostazioni di FileVault disponibili nei profili per i criteri di crittografia del disco](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Profilo di configurazione del dispositivo per Endpoint Protection per FileVault di macOS](#create-endpoint-security-policy-for-filevault)** . Le impostazioni di FileVault sono una delle categorie di impostazioni disponibili per Endpoint Protection di macOS. Per altre informazioni sull'uso di un profilo di configurazione del dispositivo, vedere [Creare un profilo di dispositivo in Intune](../configuration/device-profile-create.md).

  Visualizzare le [impostazioni di FileVault disponibili nei profili di Endpoint Protection dai criteri di configurazione del dispositivo](../protect/endpoint-protection-macos.md#filevault).

Per gestire BitLocker per Windows 10, vedere [Gestire i criteri BitLocker](../protect/encrypt-devices.md).

> [!TIP]
> Intune offre un [report di crittografia](encryption-monitor.md) predefinito con i dettagli sullo stato della crittografia in tutti i dispositivi gestiti.

È quindi necessario creare criteri di crittografia dei dispositivi con FileVault. Tali criteri vengono applicati ai dispositivi in due fasi. Prima il dispositivo viene preparato in modo da consentire a Intune di recuperare la chiave di ripristino ed eseguirne il backup. Questa azione è detta deposito. Dopo il deposito della chiave, è possibile avviare la crittografia del disco.

La registrazione del dispositivo approvata dall'utente è necessaria per il funzionamento di FileVault in un dispositivo. L'utente deve approvare manualmente il profilo di gestione dalle preferenze di sistema perché la registrazione sia considerata approvata dall'utente.

## <a name="permissions-to-manage-filevault"></a>Autorizzazioni per la gestione di FileVault

Per gestire FileVault in Intune, l'account deve disporre delle autorizzazioni di [controllo degli accessi in base al ruolo](../fundamentals/role-based-access-control.md) di Intune applicabili.

Di seguito sono riportati le autorizzazioni di FileVault, che fanno parte della categoria **Attività remote**, e i ruoli predefiniti di controllo degli accessi in base al ruolo che concedono l'autorizzazione:

- **Get FileVault key**:
  - Help Desk Operator
  - Endpoint security manager

- **Rotate FileVault key**
  - Help Desk Operator

## <a name="create-endpoint-security-policy-for-filevault"></a>Creare criteri di sicurezza degli endpoint per FileVault

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** (Sicurezza degli endpoint)  > **Crittografia del disco** > **Crea criterio**.

3. Nella pagina **Dati principali** immettere le proprietà seguenti e quindi scegliere **Avanti**.
   - **Piattaforma**: macOS
   - **Profilo**: FileVault

   ![Selezionare il profilo FileVault](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. Nella pagina **Impostazioni di configurazione**:
   1. Impostare *Abilita FileVault* su **Sì**.
   2. Per *Tipo di chiave di ripristino* è supportata solo l'opzione **Chiave di ripristino personale**.
   3. Configurare impostazioni aggiuntive in base alle esigenze.

   Considerare la possibilità di aggiungere un messaggio per facilitare agli utenti il recupero della chiave di ripristino del dispositivo. Queste informazioni possono essere utili per gli utenti se si usa l'impostazione Rotazione della chiave di ripristino personale, che periodicamente può generare in modo automatico una nuova chiave di ripristino per un dispositivo.

   Ad esempio: per recuperare una chiave di ripristino smarrita o ruotata di recente, accedere al sito Web Portale aziendale di Intune da qualsiasi dispositivo. Nel portale passare a Dispositivi, selezionare il dispositivo con FileVault abilitato e quindi selezionare *Ottieni la chiave di ripristino*. Verrà visualizzata la chiave di ripristino corrente.

5. Al termine della configurazione delle impostazioni, selezionare **Avanti**.

6. Nella pagina **Ambito (tag)** scegliere **Selezionare i tag di ambito** per aprire il riquadro Seleziona tag per assegnare tag di ambito al profilo.

   Selezionare **Avanti** per continuare.

7. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere Assegnare profili utente e dispositivo.
Selezionare **Avanti**.

8. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

## <a name="create-device-configuration-policy-for-filevault"></a>Creare criteri di configurazione del dispositivo per FileVault

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Nella pagina **Crea un profilo** impostare le opzioni seguenti e quindi fare clic su **Crea**:
   - **Piattaforma**: macOS
   - **Profilo**: Protezione degli endpoint

   ![Selezionare il profilo FileVault](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Nella pagina **Informazioni di base** immettere le proprietà seguenti:

   - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido potrebbe includere il tipo di profilo e la piattaforma.

   - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

5. Nella pagina **Impostazioni di configurazione** selezionare **FileVault** per espandere le impostazioni disponibili:

   > [!div class="mx-imgBorder"]
   > ![Impostazioni di FileVault](./media/encrypt-devices-filevault/filevault-settings.png)

6. Configurare le seguenti impostazioni:
  
   - Per *Abilita FileVault* selezionare **Sì**.

   - Per *Tipo di chiave di ripristino* selezionare **Chiave personale**.

   - Per *Descrizione della posizione del deposito della chiave di ripristino personale* aggiungere un messaggio per aiutare gli utenti a recuperare la chiave di ripristino per il proprio dispositivo. Queste informazioni possono essere utili per gli utenti se si usa l'impostazione Rotazione della chiave di ripristino personale, che periodicamente può generare in modo automatico una nuova chiave di ripristino per un dispositivo.

     Ad esempio: per recuperare una chiave di ripristino smarrita o ruotata di recente, accedere al sito Web Portale aziendale di Intune da qualsiasi dispositivo. Nel portale passare a *Dispositivi*, selezionare il dispositivo con FileVault abilitato e quindi selezionare *Ottieni la chiave di ripristino*. Verrà visualizzata la chiave di ripristino corrente.

   Configurare le [impostazioni di FileVault](endpoint-protection-macos.md#filevault) rimanenti in base alle esigenze aziendali e quindi selezionare **Avanti**.

7. Nella pagina **Ambito (tag)** scegliere **Selezionare i tag di ambito** per aprire il riquadro Seleziona tag per assegnare tag di ambito al profilo.

   Selezionare **Avanti** per continuare.

8. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere Assegnare profili utente e dispositivo.
Selezionare **Avanti**.

9. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

## <a name="manage-filevault"></a>Gestire FileVault

Per visualizzare le informazioni sui dispositivi che ricevono i criteri FileVault, vedere [Monitorare la crittografia del disco](../protect/encryption-monitor.md).

Quando Intune esegue per la prima volta la crittografia di un dispositivo macOS con FileVault, viene creata una chiave di ripristino personale. Al momento della crittografia, il dispositivo visualizza la chiave personale una sola volta per l'utente del dispositivo.

Per i dispositivi gestiti, Intune può depositare una copia della chiave di ripristino personale. Il deposito delle chiavi consente agli amministratori di Intune di ruotare le chiavi per favorire la protezione dei dispositivi e agli utenti di recuperare una chiave di ripristino personale smarrita o ruotata.

Dopo che Intune ha crittografato un dispositivo macOS con FileVault:

- Gli amministratori possono visualizzare e gestire le chiavi di ripristino di FileVault con il report di crittografia di Intune.
- Gli utenti possono visualizzare la chiave di ripristino personale di un dispositivo dal Portale aziendale Web sul dispositivo. All'interno del Portale aziendale Web scegliere il dispositivo macOS crittografato e quindi scegliere "Ottieni la chiave di ripristino" come azione del dispositivo remoto.

> [!IMPORTANT]
> I dispositivi crittografati dagli utenti e non da Intune non possono essere gestiti da Intune. Questo significa che Intune non può depositare la chiave di ripristino personale di questi dispositivi, né gestire la rotazione delle chiavi di ripristino. Perché Intune possa gestire FileVault e le chiavi di ripristino dei dispositivi, gli utenti devono decrittografare i dispositivi e quindi consentire a Intune di crittografarli.

### <a name="retrieve-personal-recovery-key"></a>Recuperare una chiave di ripristino personale

Per un dispositivo macOS crittografato da Intune, gli utenti finali possono recuperare la chiave di ripristino personale (chiave di FileVault) usando l'app Portale aziendale iOS, l'app Portale aziendale Android o l'app Intune Android.

Il dispositivo con la chiave di ripristino personale deve essere registrato in Intune e crittografato con FileVault in Intune. Usando l'app Portale aziendale iOS, l'app Portale aziendale Android, l'app Intune Android o il sito Web Portale aziendale, l'utente può visualizzare la chiave di ripristino di **FileVault** necessaria per accedere ai dispositivi Mac.

Gli utenti del dispositivo possono selezionare **Dispositivi** > *il dispositivo macOS crittografato e registrato* > **Ottieni la chiave di ripristino**. Il browser visualizzerà il Portale aziendale Web e la chiave di ripristino.

### <a name="rotate-recovery-keys"></a>Ruotare le chiavi di ripristino

Intune supporta più opzioni per la rotazione e il ripristino delle chiavi di ripristino personali. È opportuno eseguire la rotazione delle chiavi se la chiave personale corrente viene smarrita o si ritiene che sia a rischio.

- **Rotazione automatica**: un amministratore può configurare l'impostazione di FileVault Rotazione della chiave di ripristino personale in modo da generare periodicamente nuove chiavi di ripristino in modo automatico. Quando viene generata una nuova chiave per un dispositivo, la chiave non viene visualizzata per l'utente. L'utente deve invece ottenere la chiave da un amministratore o tramite l'app Portale aziendale.

- **Rotazione manuale**: un amministratore può visualizzare le informazioni relative ai dispositivi gestiti con Intune e crittografati con FileVault. Può quindi scegliere di ruotare manualmente le chiavi di ripristino per i dispositivi aziendali. Non è possibile ruotare le chiavi di ripristino per i dispositivi personali.

  Per ruotare una chiave di ripristino:

  1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Selezionare **Dispositivi** > **Tutti i dispositivi**.

  3. Dall'elenco dei dispositivi selezionare il dispositivo crittografato di cui si vuole ruotare la chiave, quindi in Monitoraggio selezionare **Chiavi di ripristino**.
  
  4. Nel riquadro Chiavi di ripristino selezionare **Ruota la chiave di ripristino di FileVault**.

     Alla successiva sincronizzazione del dispositivo con Intune la chiave personale verrà ruotata. Quando necessario, l'utente può ottenere la nuova chiave tramite il portale aziendale.

### <a name="recover-recovery-keys"></a>Ripristinare chiavi di ripristino

- **Amministratore**: gli amministratori non possono visualizzare le chiavi di ripristino personali per i dispositivi crittografati con FileVault.

- **Utente finale**: gli utenti finali possono usare il sito Web Portale aziendale da qualsiasi dispositivo per visualizzare la chiave di ripristino personale corrente per tutti i propri dispositivi gestiti. Non è possibile visualizzare le chiavi di ripristino dall'app Portale aziendale.

  Per visualizzare una chiave di ripristino:
  
  1. Da un qualsiasi dispositivo accedere al *Portale aziendale Intune*.

  2. Nel portale passare a **Dispositivi** e selezionare il dispositivo macOS crittografato con FileVault.

  3. Selezionare **Ottieni la chiave di ripristino**. Verrà visualizzata la chiave di ripristino corrente.

## <a name="next-steps"></a>Passaggi successivi

[Gestire i criteri BitLocker](../protect/encrypt-devices.md)

[Monitorare la crittografia del disco](../protect/encryption-monitor.md)
