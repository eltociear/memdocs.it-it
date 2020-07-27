---
title: Crittografare i dispositivi macOS con la crittografia del disco FileVault in Intune
titleSuffix: Microsoft Intune
description: Crittografare i dispositivi macOS con il metodo di crittografia predefinito FileVault e gestire le chiavi di ripristino per tali dispositivi crittografati all'interno del portale di Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460485"
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

Oltre a usare i criteri di Intune per crittografare un dispositivo con FileVault, è possibile distribuire i criteri a un dispositivo gestito per consentire a Intune di [presupporre la gestione di FileVault quando il dispositivo è stato crittografato dall'utente](#assume-management-of-filevault-on-previously-encrypted-devices). Questo scenario richiede che il dispositivo riceva i criteri FileVault da Intune e che in seguito l'utente carichi la chiave di ripristino personale in Intune.

La registrazione del dispositivo approvata dall'utente è necessaria per il funzionamento di FileVault in un dispositivo. L'utente deve approvare manualmente il profilo di gestione dalle preferenze di sistema perché la registrazione sia considerata approvata dall'utente.

## <a name="permissions-to-manage-filevault"></a>Autorizzazioni per la gestione di FileVault

Per gestire FileVault in Intune, l'account deve disporre delle autorizzazioni di [controllo degli accessi in base al ruolo](../fundamentals/role-based-access-control.md) di Intune applicabili.

Di seguito sono riportati le autorizzazioni di FileVault, che fanno parte della categoria **Attività remote**, e i ruoli predefiniti di controllo degli accessi in base al ruolo che concedono l'autorizzazione:

- **Get FileVault key**:
  - Help Desk Operator
  - Endpoint security manager

- **Rotate FileVault key**
  - Help Desk Operator

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

   - Per *Descrizione della posizione del deposito della chiave di ripristino personale* aggiungere un messaggio per aiutare gli utenti a [recuperare la chiave di ripristino per il proprio dispositivo](#retrieve-a-personal-recovery-key). Queste informazioni possono essere utili per gli utenti se si usa l'impostazione Rotazione della chiave di ripristino personale, che periodicamente può generare in modo automatico una nuova chiave di ripristino per un dispositivo.

     Ad esempio: per recuperare una chiave di ripristino smarrita o ruotata di recente, accedere al sito Web Portale aziendale di Intune da qualsiasi dispositivo. Nel portale passare a *Dispositivi*, selezionare il dispositivo con FileVault abilitato e quindi selezionare *Ottieni la chiave di ripristino*. Verrà visualizzata la chiave di ripristino corrente.

   Configurare le [impostazioni di FileVault](endpoint-protection-macos.md#filevault) rimanenti in base alle esigenze aziendali e quindi selezionare **Avanti**.

7. Nella pagina **Ambito (tag)** scegliere **Selezionare i tag di ambito** per aprire il riquadro Seleziona tag per assegnare tag di ambito al profilo.

   Selezionare **Avanti** per continuare.

8. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere Assegnare profili utente e dispositivo.
Selezionare **Avanti**.

9. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

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

   Considerare la possibilità di aggiungere un messaggio per [facilitare agli utenti il recupero della chiave di ripristino](#retrieve-a-personal-recovery-key) del dispositivo. Queste informazioni possono essere utili per gli utenti se si usa l'impostazione Rotazione della chiave di ripristino personale, che periodicamente può generare in modo automatico una nuova chiave di ripristino per un dispositivo.

   Ad esempio: per recuperare una chiave di ripristino smarrita o ruotata di recente, accedere al sito Web Portale aziendale di Intune da qualsiasi dispositivo. Nel portale passare a Dispositivi, selezionare il dispositivo con FileVault abilitato e quindi selezionare *Ottieni la chiave di ripristino*. Verrà visualizzata la chiave di ripristino corrente.

5. Al termine della configurazione delle impostazioni, selezionare **Avanti**.

6. Nella pagina **Ambito (tag)** scegliere **Selezionare i tag di ambito** per aprire il riquadro Seleziona tag per assegnare tag di ambito al profilo.

   Selezionare **Avanti** per continuare.

7. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere Assegnare profili utente e dispositivo.
Selezionare **Avanti**.

8. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

## <a name="manage-filevault"></a>Gestire FileVault

Per visualizzare le informazioni sui dispositivi che ricevono i criteri FileVault, vedere [Monitorare la crittografia del disco](../protect/encryption-monitor.md).

Quando Intune esegue per la prima volta la crittografia di un dispositivo macOS con FileVault, viene creata una chiave di ripristino personale. Al momento della crittografia, il dispositivo visualizza la chiave personale una sola volta per l'utente del dispositivo.

Per i dispositivi gestiti, Intune può depositare una copia della chiave di ripristino personale. Il deposito delle chiavi consente agli amministratori di Intune di ruotare le chiavi per favorire la protezione dei dispositivi e agli utenti di recuperare una chiave di ripristino personale smarrita o ruotata.

Intune deposita una chiave di ripristino quando i criteri di Intune crittografano un dispositivo o dopo che un utente carica la chiave di ripristino personale per il dispositivo che ha crittografato manualmente.

Quando Intune deposita la chiave di ripristino personale:

- Gli amministratori possono gestire e ruotare le chiavi di ripristino di FileVault per qualsiasi dispositivo macOS gestito, usando il report di crittografia di Intune.
- Gli amministratori possono visualizzare la chiave di ripristino personale solo per i dispositivi macOS gestiti contrassegnati come *aziendali*. Non possono visualizzare la chiave di ripristino per i dispositivi personali.
- Gli utenti possono visualizzare e [recuperare la propria chiave di ripristino personale da una posizione supportata](#retrieve-a-personal-recovery-key). Dal sito Web di Portale aziendale, ad esempio, l'utente può scegliere l'azione remota del dispositivo *Ottieni la chiave di ripristino*.

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>Assumere la gestione di FileVault nei dispositivi precedentemente crittografati

Intune può gestire la crittografia del disco FileVault nei dispositivi macOS crittografati tramite l'uso dei criteri di Intune. Intune può anche assumere la gestione di FileVault nei dispositivi crittografati dagli utenti del dispositivo e non tramite i criteri di Intune.

#### <a name="prerequisites-to-assume-management-of-filevault"></a>Prerequisiti per assumere la gestione di FileVault

Per assumere la gestione di un dispositivo precedentemente crittografato, è necessario che siano soddisfatte le condizioni seguenti:

1. **Distribuire un criterio FileVault nel dispositivo**. Il dispositivo crittografato in precedenza deve ricevere un criterio da Intune che attiva la crittografia del disco FileVault.

   In questo scenario, il criterio non decrittografa o crittografa di nuovo il dispositivo. Al contrario, il criterio consente a Intune di assumere la gestione della crittografia FileVault già abilitata nel dispositivo.  Per crittografare i dispositivi con FileVault, è possibile usare i criteri di crittografia dei dischi di protezione degli endpoint o un criterio di protezione degli endpoint per la configurazione del dispositivo.

   Vedere [Creare e distribuire criteri](#create-device-configuration-policy-for-filevault).

2. **Gli utenti caricano la chiave di ripristino personale in Intune**.  Dopo che il dispositivo ha ricevuto il criterio FileVault, dare istruzioni all'utente del dispositivo che ha crittografato il dispositivo di caricare la chiave di ripristino personale in Intune. Se la chiave viene immessa correttamente, Intune assume la gestione della crittografia FileVault e viene creata una nuova chiave di ripristino personale per il dispositivo e l'utente.

   > [!IMPORTANT]
   > Intune non avvisa gli utenti che devono caricare la chiave di ripristino personale per completare la crittografia. Usare invece i normali canali di comunicazione IT per avvisare gli utenti che hanno precedentemente crittografato il proprio dispositivo macOS con FileVault che devono caricare la chiave di ripristino personale in Intune.  
   >
   > In base ai criteri di conformità, è possibile che ai dispositivi venga impedito l'accesso alle risorse aziendali fino a quando Intune non assume correttamente la gestione della crittografia FileVault nel dispositivo.

#### <a name="upload-a-personal-recovery-key"></a>Caricare una chiave di ripristino personale

Per consentire a Intune di gestire FileVault in un dispositivo precedentemente crittografato, l'utente del dispositivo deve usare il sito Web Portale aziendale per caricare la chiave di ripristino personale corrente per il dispositivo in Intune.  Al momento del caricamento, Intune ruota la chiave per creare una nuova chiave di ripristino personale, che viene quindi archiviata da Intune per ripristini futuri, se necessario.

Nel sito Web Portale aziendale l'utente individua il dispositivo macOS crittografato e seleziona l'opzione **Store recovery key** (Archivia chiave di ripristino). Non appena viene immessa la chiave di ripristino personale, Intune tenta di ruotare la chiave per generare una nuova chiave. La rotazione viene eseguita per verificare che la chiave immessa sia accurata per il dispositivo. Questa nuova chiave viene quindi archiviata e gestita da Intune per usi futuri, qualora l'utente debba ripristinare il dispositivo.

Se la rotazione della chiave ha esito negativo, il dispositivo non ha elaborato il criterio FileVault oppure la chiave immessa non è corretta per il dispositivo.

Una volta completata la rotazione, un utente può [recuperare la nuova chiave di ripristino personale da una posizione supportata](#retrieve-a-personal-recovery-key).

 Visualizzare il [contenuto dell'utente finale per il caricamento della chiave di ripristino personale](../user-help/store-recovery-key.md).

> [!IMPORTANT]
> Per un dispositivo crittografato da un utente e non da Intune, Intune non è in grado di gestire i dispositivi con crittografia FileVault fino a quando il dispositivo non riceve un criterio FileVault e l'utente del dispositivo carica correttamente la chiave di ripristino personale.

### <a name="retrieve-a-personal-recovery-key"></a>Recuperare una chiave di ripristino personale

Per un dispositivo macOS con la crittografia FileVault gestita da Intune, gli utenti finali possono recuperare la chiave di ripristino personale (chiave FileVault) dalle posizioni seguenti, usando qualsiasi dispositivo:

- sito Web del portale aziendale
- App Portale aziendale iOS/iPadOS
- App Portale aziendale Android
- App Intune

Gli amministratori possono visualizzare le chiavi di ripristino personali per i dispositivi macOS crittografati contrassegnati come dispositivo *aziendale*. Non possono visualizzare la chiave di ripristino per un dispositivo personale.

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
