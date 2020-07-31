---
title: Crittografare i dispositivi Windows 10 con BitLocker in Intune
titleSuffix: Microsoft Intune
description: Crittografare i dispositivi con il metodo di crittografia predefinito BitLocker e gestire le chiavi di ripristino per tali dispositivi crittografati all'interno del portale di Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
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
ms.openlocfilehash: a9fad599342cf358409c7be09ebb8b4eb1c0c4a5
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334624"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Gestire i criteri BitLocker per Windows 10 in Intune

Usare Intune per configurare Crittografia unità BitLocker nei dispositivi che eseguono Windows 10.

BitLocker è disponibile nei dispositivi che eseguono Windows 10 o versioni successive. Per alcune impostazioni di BitLocker è necessario che il dispositivo disponga di un TPM supportato.

Usare uno dei tipi di criteri seguenti per configurare BitLocker nei dispositivi gestiti

- **[Criteri di crittografia del disco per la sicurezza degli endpoint per BitLocker di Windows 10](#create-an-endpoint-security-policy-for-bitlocker)** . Il profilo BitLocker in *Endpoint security* (Sicurezza degli endpoint) è un gruppo in evidenza di impostazioni dedicato alla configurazione di BitLocker.

  Visualizzare le impostazioni di BitLocker disponibili in [Profili BitLocker dai criteri di crittografia del disco](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Profilo di configurazione del dispositivo per Endpoint Protection per BitLocker di Windows 10](#create-an-endpoint-security-policy-for-bitlocker)** . Le impostazioni di BitLocker sono una delle categorie di impostazioni disponibili per Endpoint Protection di Windows 10.

  Visualizzare le impostazioni di BitLocker disponibili per [BitLocker nei profili di Endpoint Protection dai criteri di configurazione del dispositivo](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune offre un [report di crittografia](encryption-monitor.md) predefinito con i dettagli sullo stato della crittografia in tutti i dispositivi gestiti. Dopo che Intune ha crittografato un dispositivo Windows 10 con BitLocker, è possibile visualizzare e recuperare le chiavi di ripristino di BitLocker visualizzando il report di crittografia.
>
> È anche possibile accedere a informazioni importanti per BitLocker dai dispositivi, come indicato in Azure Active Directory (Azure AD).
[Report crittografia](encryption-monitor.md) offre dettagli sullo stato della crittografia in tutti i dispositivi gestiti.

## <a name="permissions-to-manage-bitlocker"></a>Autorizzazioni per la gestione di BitLocker

Per gestire BitLocker in Intune, l'account deve disporre delle autorizzazioni di [controllo degli accessi in base al ruolo](../fundamentals/role-based-access-control.md) di Intune applicabili.

Di seguito sono riportate le autorizzazioni di BitLocker, che fanno parte della categoria Attività remote, e i ruoli predefiniti di controllo degli accessi in base al ruolo che concedono l'autorizzazione:

- **Ruotare le chiavi di BitLocker**
  - Help Desk Operator

## <a name="create-and-deploy-policy"></a>Creare e distribuire criteri

Per creare il tipo di criterio preferito usare una delle procedure seguenti.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Creare un criterio di sicurezza degli endpoint per BitLocker

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security**(Sicurezza degli endpoint) > **Crittografia del disco** > **Crea criterio**.

3. Impostare le opzioni seguenti:
   1. **Piattaforma**: Windows 10 o versioni successive
   2. **Profilo**: BitLocker

   ![Selezionare il profilo BitLocker](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. Nella pagina **Impostazioni di configurazione** configurare le impostazioni per BitLocker in base alle esigenze aziendali.  

   Per abilitare BitLocker automaticamente, vedere [Abilitare automaticamente BitLocker nei dispositivi](#silently-enable-bitlocker-on-devices), in questo articolo per altri prerequisiti e per le configurazioni delle impostazioni specifiche che è necessario usare.

   Selezionare **Avanti**.

5. Nella pagina **Ambito (tag)** scegliere **Selezionare i tag di ambito** per aprire il riquadro Seleziona tag per assegnare tag di ambito al profilo.

   Selezionare **Avanti** per continuare.

6. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere Assegnare profili utente e dispositivo.

   Selezionare **Avanti**.

7. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Creare un profilo di configurazione del dispositivo per BitLocker

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Impostare le opzioni seguenti:
   1. **Piattaforma**: Windows 10 e versioni successive
   2. **Tipo di profilo**: Protezione degli endpoint

   ![Selezionare il profilo BitLocker](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Selezionare **Impostazioni** > **Crittografia di Windows**.

   ![Impostazioni di BitLocker](./media/encrypt-devices/bitlocker-settings.png)

5. Configurare le impostazioni per BitLocker in base alle esigenze aziendali.

   Per abilitare BitLocker automaticamente, vedere [Abilitare automaticamente BitLocker nei dispositivi](#silently-enable-bitlocker-on-devices), in questo articolo per altri prerequisiti e per le configurazioni delle impostazioni specifiche che è necessario usare.

6. Selezionare **OK**.

7. Completare la configurazione delle impostazioni aggiuntive e quindi salvare il profilo.

## <a name="manage-bitlocker"></a>Gestire BitLocker

Per visualizzare le informazioni sui dispositivi che ricevono i criteri BitLocker, vedere [Monitorare la crittografia del disco](../protect/encryption-monitor.md). È inoltre possibile visualizzare e recuperare le chiavi di ripristino di BitLocker visualizzando il report di crittografia.

### <a name="silently-enable-bitlocker-on-devices"></a>Abilitare automaticamente BitLocker nei dispositivi

È possibile configurare un criterio BitLocker che abilita automaticamente BitLocker in un dispositivo. Questo significa che BitLocker viene abilitato correttamente senza presentare alcuna interfaccia utente all'utente finale, anche quando l'utente non è un amministratore locale del dispositivo.

**Prerequisiti del dispositivo**:

un dispositivo deve soddisfare le condizioni seguenti perché sia idoneo per l'abilitazione automatica di BitLocker:

- I dispositivi devono eseguire Windows 10 versione 1809 o successiva
- Il dispositivo deve essere aggiunto ad Azure AD  

**Configurazione dei criteri di BitLocker**:

Le due impostazioni seguenti per *Impostazioni di base di BitLocker* devono essere configurate nei criteri di BitLocker:

- **Avviso per la crittografia dischi di altro tipo** = *Blocca*.
- **Consenti agli utenti standard di abilitare la crittografia durante un'aggiunta ad Azure AD** = *Consenti*

I criteri di BitLocker **non devono richiedere** l'uso di un PIN di avvio o di una chiave di avvio. Quando *sono richiesti* un PIN di avvio o una chiave di avvio TPM, BitLocker non può essere abilitato automaticamente ed è richiesta l'interazione con l'utente finale.  Questo requisito viene soddisfatto tramite le seguenti tre *impostazioni dell'unità del sistema operativo BitLocker* nello stesso criterio:

- L'opzione **PIN di avvio TPM compatibile** non deve essere impostata su *Richiedi PIN di avvio con TPM*
- L'opzione **Chiave di avvio TPM compatibile** non deve essere impostata su *Richiedi la chiave di avvio con TPM*
- L'opzione **Chiave di avvio e PIN TPM compatibile** non deve essere impostata su *Richiedi la chiave di avvio e il PIN con TPM*

### <a name="view-details-for-recovery-keys"></a>Visualizzare i dettagli per le chiavi di ripristino

Intune offre l'accesso al pannello di Azure AD per BitLocker, per consentire di visualizzare gli ID delle chiavi di BitLocker e le chiavi di ripristino per i dispositivi Windows 10 dal portale di Intune. Per essere accessibile, il dispositivo deve avere le chiavi depositate in Azure AD.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Tutti i dispositivi**.

3. Selezionare un dispositivo nell'elenco e in *Monitoraggio* selezionare **Chiavi di ripristino**.
  
   Quando le chiavi sono presenti in Azure AD, sono disponibili le informazioni seguenti:
   - ID chiave BitLocker
   - Chiave di ripristino di BitLocker
   - Tipo unità

   Quando le chiavi non sono presenti in Azure AD, Intune visualizzerà il messaggio *Non sono state trovate chiavi BitLocker per questo dispositivo*.

Le informazioni per BitLocker vengono ottenute tramite il [provider di servizi di configurazione BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp). Il provider di servizi di configurazione (CSP) BitLocker è supportato in Windows 10 versione 1703 e successive e in Windows 10 Pro versione 1809 e successive.

### <a name="rotate-bitlocker-recovery-keys"></a>Ruotare le chiavi di ripristino di BitLocker

È possibile usare un'azione del dispositivo Intune per ruotare in modalità remota la chiave di ripristino di BitLocker di un dispositivo che esegue Windows 10 versione 1909 o successiva.

#### <a name="prerequisites"></a>Prerequisiti

Per supportare la rotazione della chiave di ripristino di BitLocker, è necessario che i dispositivi soddisfino i seguenti prerequisiti:

- I dispositivi devono eseguire Windows 10 versione 1909 o successiva

- Per i dispositivi aggiunti ad Azure AD e ad AD ibrido, il supporto per la rotazione delle chiavi deve essere abilitato tramite la configurazione dei criteri di BitLocker:

  - **Rotazione password di ripristino basata sul client** per *abilitare la rotazione nei dispositivi aggiunti ad Azure AD* o *abilitare la rotazione nei dispositivi aggiunti ad Azure AD e AD ibrido*
  - **Salva le informazioni di ripristino di BitLocker in Azure Active Directory** su *Abilitata*
  - **Archivia le informazioni di ripristino in Azure Active Directory prima di abilitare BitLocker** su *Obbligatorio*

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>Per ruotare la chiave di ripristino di BitLocker

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Tutti i dispositivi**.

3. Nell'elenco dei dispositivi gestiti selezionare un dispositivo, selezionare **Altro** e quindi selezionare l'azione remota del dispositivo **Rotazione delle chiavi BitLocker**.

4. Nella pagina  **Panoramica** del dispositivo selezionare **Rotazione delle chiavi BitLocker**. Se questa opzione non è presente, selezionare i puntini di sospensione ( **...** ) per visualizzare le opzioni aggiuntive, quindi selezionare l'azione remota del dispositivo **Rotazione delle chiavi BitLocker**.

   ![Selezionare i puntini di sospensione per visualizzare altre opzioni](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Passaggi successivi

[Gestire i criteri FileVault](../protect/encrypt-devices-filevault.md)

[Monitorare la crittografia del disco](../protect/encryption-monitor.md)
