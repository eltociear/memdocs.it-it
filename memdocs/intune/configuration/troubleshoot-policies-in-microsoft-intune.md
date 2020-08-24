---
title: Risoluzione dei problemi dei criteri in Microsoft Intune - Azure | Microsoft Docs
description: Informazioni su come usare la funzione predefinita di risoluzione dei problemi e descrizione dei problemi più comuni, e delle relative soluzioni, che possono verificarsi quando si usano criteri di conformità e profili di configurazione in Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/2/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 99fb6db6-21c5-46cd-980d-50f063ab8ab8
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc307f22e3caa77357d8d3054a432c8d42c38fc4
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146508"
---
# <a name="troubleshoot-policies-and-profiles-and-in-intune"></a>Risolvere problemi relativi a criteri e profili in Intune

Microsoft Intune include alcune funzioni predefinite per la risoluzione dei problemi. Usare queste funzioni per risolvere i problemi di criteri di conformità e di profili di configurazione nell'ambiente.

Questo articolo elenca alcune tecniche di risoluzione dei problemi comuni e descrive alcuni problemi che possono verificarsi.

## <a name="check-tenant-status"></a>Controllare lo stato del tenant

Controllare lo [stato del tenant](../fundamentals/tenant-status.md) e verificare che la sottoscrizione sia attiva. È anche possibile visualizzare gli avvisi e i dettagli degli eventi imprevisti attivi che potrebbero influire sulla distribuzione del profilo o dei criteri.

## <a name="use-built-in-troubleshooting"></a>Usare la risoluzione dei problemi predefinita

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Risoluzione dei problemi e supporto** > **Risoluzione dei problemi**:

    :::image type="content" source="./media/troubleshoot-policies-in-microsoft-intune/help-and-support-troubleshoot.png" alt-text="Nell'interfaccia di amministrazione di Gestione Endpoint e in Intune passare a Risoluzione dei problemi e supporto.":::

2. Scegliere **Selezionare l'utente** > selezionare l'utente che ha un problema > **Seleziona**.
3. Verificare che vi sia un segno di spunta verde di fianco a **Licenza di Intune** e **Stato dell'account**:

    :::image type="content" source="./media/troubleshoot-policies-in-microsoft-intune/account-status-intune-license-show-green.png" alt-text="In Intune selezionare l'utente e verificare che vi sia un segno di spunta verde di fianco a Stato dell'account e Licenza di Intune.":::

    **Collegamenti utili**:

    - [Assegnare licenze agli utenti in modo che possano registrare i dispositivi in Intune](../fundamentals/licenses-assign.md)
    - [Aggiungere utenti a Intune](../fundamentals/users-add.md)

4. In **Dispositivi** individuare il dispositivo per cui si verifica il problema. Verificare le varie colonne:

    - **Gestito**: perché un dispositivo riceva i criteri di conformità o di configurazione, questa proprietà deve essere impostata su **MDM** oppure **EAS/MDM**.

        - Se il valore di **Gestito** non è **MDM** oppure **EAS/MDM**, il dispositivo non è registrato. E finché non è registrato, il dispositivo non riceve criteri di conformità o di configurazione.

        - I criteri di protezione delle app, per la gestione delle applicazioni per dispositivi mobili, non richiedono che i dispositivi siano registrati. Per altre informazioni, vedere [Come creare e assegnare criteri di protezione delle app](../apps/app-protection-policies.md).

    - **Tipo di join per Azure AD**: deve essere impostato su **Area di lavoro** oppure su **AzureAD**.
 
        - Se la colonna ha valore **Non registrato**, potrebbe esserci un problema con la registrazione. In genere, il problema si risolve annullando ed eseguendo nuovamente la registrazione del dispositivo.

    - **Conforme con Intune**: deve essere impostato su **Sì**. Se viene visualizzato **No**, potrebbe esserci un problema con i criteri di conformità o il dispositivo non si connette al servizio Intune. Ad esempio, il dispositivo potrebbe essere spento o non avere una connessione di rete. Infine, dopo 30 giorni il dispositivo diventa non conforme.

        Per altre informazioni, vedere [Introduzione ai criteri di conformità dei dispositivi in Intune](../protect/device-compliance-get-started.md).

    - **Conforme con Azure AD**: deve essere impostato su **Sì**. Se viene visualizzato **No**, potrebbe esserci un problema con i criteri di conformità o il dispositivo non si connette al servizio Intune. Ad esempio, il dispositivo potrebbe essere spento o non avere una connessione di rete. Infine, dopo 30 giorni il dispositivo diventa non conforme.

        Per altre informazioni, vedere [Introduzione ai criteri di conformità dei dispositivi in Intune](../protect/device-compliance-get-started.md).

    - **Ultima sincronizzazione**: devono essere indicate una data e un'ora recenti. Per impostazione predefinita, i dispositivi Intune si sincronizzano ogni 8 ore.

        - Se il valore di **Ultima sincronizzazione** è superiore a 24 ore, potrebbe esserci un problema con il dispositivo. Un dispositivo che non può essere sincronizzato non riceve i criteri da Intune.

        - Per forzare la sincronizzazione:
            - Nei dispositivi Android aprire l'app Portale aziendale > **Dispositivi** > scegliere il dispositivo dall'elenco > **Controlla le impostazioni del dispositivo**.
            - Nei dispositivi iOS/iPadOS aprire l'app Portale aziendale > **Dispositivi** > scegliere il dispositivo dall'elenco > **Verifica le impostazioni**.

        - Nei dispositivi Windows aprire **Impostazioni** > **Account** > **Access Work or School (Accedi all'azienda o all'istituto di istruzione)** > selezionare l'account o la registrazione MDM > **Informazioni** > **Sincronizzazione**.

    - Selezionare il dispositivo per visualizzare informazioni specifiche sui criteri.

        **Conformità del dispositivo** visualizza gli stati dei criteri di conformità assegnati al dispositivo.

        **Configurazione dispositivo** visualizza gli stati dei criteri di configurazione assegnati al dispositivo.

        Se i criteri previsti non vengono visualizzati in **Conformità del dispositivo** oppure in **Configurazione dispositivo**, i criteri non sono assegnati correttamente. Aprire i criteri e assegnarli all'utente o al dispositivo.

        **Stati dei criteri**:

        - **Non applicabile**: i criteri non sono supportati nella piattaforma. Ad esempio i criteri iOS/iPadOS non funzionano in Android. I criteri Samsung KNOX non funzionano nei dispositivi Windows.
        - **Conflitto**: nel dispositivo è presente un'impostazione di cui Intune non può eseguire l'override. Oppure, sono stati distribuiti due criteri con la stessa impostazione che usa valori diversi.
        - **Pending**: il dispositivo non è stato sincronizzato in Intune per ottenere i criteri. Oppure, il dispositivo ha ricevuto i criteri, ma non ha segnalato lo stato a Intune.
        - **Errori**: cercare gli errori e le risoluzioni possibili in [Risolvere i problemi di accesso alle risorse aziendali con Microsoft Intune](../fundamentals/troubleshoot-company-resource-access-problems.md).

        **Collegamenti utili**: 

        - [Modi per distribuire i criteri di conformità dei dispositivi](../protect/device-compliance-get-started.md)
        - [Monitorare i criteri di conformità dei dispositivi](../protect/compliance-policy-monitor.md)

## <a name="youre-unsure-if-a-profile-is-correctly-applied"></a>Non si è sicuri che i criteri siano stati applicati correttamente

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Tutti i dispositivi** > selezionare il dispositivo > **Configurazione del dispositivo**. 

    Vengono elencati i profili di tutti i dispositivi. Ogni profilo ha uno **Stato**. Lo stato si applica quando tutti i profili assegnati, tra cui le restrizioni e i requisiti hardware e del sistema operativo, vengono considerati insieme. Gli stati possibili comprendono:

    - **Conforme**: il dispositivo riceve il profilo e segnala a Intune che è conforme all'impostazione.

    - **Non applicabile**: l'impostazione del profilo non è applicabile. È ad esempio possibile che le impostazioni di posta elettronica per i dispositivi iOS/iPadOS non si applichino a un dispositivo Android.

    - **Pending**: il profilo viene inviato al dispositivo, ma lo stato non viene segnalato a Intune. Ad esempio, la crittografia in Android richiede l'abilitazione da parte dell'utente e può quindi comparire come in sospeso.

**Collegamento utile**: [Monitorare i profili di configurazione dei dispositivi in Microsoft Intune](../configuration/device-profile-monitor.md)

> [!NOTE]
> Quando due criteri con livelli di restrizione diversi vengono applicati allo stesso dispositivo o utente, viene applicato il criterio più restrittivo.

## <a name="policy-troubleshooting-resources"></a>Risorse per la risoluzione dei problemi relativi ai criteri

- [Risoluzione dei problemi relativi ai criteri iOS/iPadOS o Android che non si applicano ai dispositivi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-tip-Troubleshooting-iOS-or-Android-policies-not-applying/ba-p/280154) (apre un altro sito Microsoft)
- [Risoluzione degli errori relativi ai criteri di Intune in Windows 10](https://blogs.technet.microsoft.com/configmgrdogs/2018/08/09/troubleshooting-windows-10-intune-policy-failures/) (apre un blog)
- [Risolvere i problemi relativi alle impostazioni personalizzate CSP per Windows 10](https://support.microsoft.com/help/4055338/troubleshoot-csp-setting-windows-10-computer-intune) (apre un altro sito Microsoft)
- [Criteri di gruppo di Windows 10 e criteri MDM di Intune](https://blogs.technet.microsoft.com/cbernier/2018/04/02/windows-10-group-policy-vs-intune-mdm-policy-who-wins/) (apre un altro sito Microsoft)

## <a name="alert-saving-of-access-rules-to-exchange-has-failed"></a>Avviso: Il salvataggio delle regole di accesso in Exchange non è riuscito

**Problema**: viene visualizzato l'avviso **Il salvataggio delle regole di accesso in Exchange non è riuscito** nella console di amministrazione.

Se sono stati creati criteri nell'area di lavoro Criteri di Exchange locale con la console di amministrazione ma si usa Office 365, le impostazioni dei criteri configurate non vengono applicate da Intune. Si noti l'origine dei criteri nell'avviso. Nell'area di lavoro Criteri di Exchange locale eliminare le regole precedenti. Le regole precedenti sono regole globali di Exchange in Intune per Exchange locale e non sono rilevanti per Office 365. In seguito, creare nuovi criteri per Office 365.

L'articolo [Risolvere i problemi di Intune Exchange Connector locale](../protect/troubleshoot-exchange-connector.md) può essere una risorsa utile.

## <a name="cant-change-security-policies-for-enrolled-devices"></a>Non è possibile modificare i criteri di sicurezza per i dispositivi registrati

I dispositivi Windows Phone non consentono che la sicurezza dei criteri di sicurezza impostati tramite MDM o EAS venga ridotta dopo che i criteri sono stati configurati. Ad esempio, si imposta un **numero minimo di caratteri per la password** su 8 e poi si prova a ridurlo a 4. Vengono applicati al dispositivo i criteri più restrittivi.

I dispositivi Windows 10 non possono rimuovere i criteri di sicurezza quando si annulla l'assegnazione dei criteri (arresto della distribuzione). Potrebbe essere necessario lasciare i criteri assegnati, quindi modificare di nuovo le impostazioni di sicurezza sui valori predefiniti.

A seconda della piattaforma del dispositivo, se si vogliono modificare i criteri in un valore meno sicuro, può essere necessario reimpostare i criteri di sicurezza.

Ad esempio, in Windows 8.1, sul desktop scorrere verso destra per aprire la barra **Accessi**. Scegliere **Impostazioni** > **Pannello di controllo** > **Account utente**. A sinistra, selezionare il collegamento **Reimposta criteri di sicurezza** e scegliere **Reimposta criteri**.

È possibile che altre piattaforme, come Android e iOS/iPadOS, debbano essere ritirate e registrate nuovamente per applicare criteri meno restrittivi.

[Risolvere i problemi di registrazione dei dispositivi in Intune](../enrollment/troubleshoot-device-enrollment-in-intune.md) può rivelarsi una risorsa utile.

## <a name="pcs-using-the-intune-software-client---classic-portal"></a>PC che usando il client software di Intune - portale classico

> [!NOTE]
> Questa sezione si applica al portale classico. 

### <a name="microsoft-intune-policy-related-errors-in-policyplatformlog"></a>Errori relativi a criteri di Microsoft Intune in policyplatform.log

Per i PC Windows gestiti con il client software di Intune, gli errori dei criteri nel file `policyplatform.log` possono derivare da impostazioni non predefinite nel Controllo dell'account utente di Windows nel dispositivo. Alcune impostazioni non predefinite del Controllo dell'account utente possono influire sulle installazioni client di Microsoft Intune e sull'esecuzione dei criteri.

#### <a name="resolve-uac-issues"></a>Risolvere i problemi relativi al Controllo dell'account utente

1. Ritirare il computer. Vedere [Rimuovere i dispositivi](../remote-actions/devices-wipe.md).

2. Attendere 20 minuti che il software client venga rimosso.

    > [!NOTE]
    > Non provare a rimuovere il client da Programmi e funzionalità.

3. Nel menu Start digitare **Controllo dell'account utente** per aprire le impostazioni di Controllo dell'account utente.

4. Spostare il dispositivo di scorrimento di notifica sull'impostazione predefinita.

### <a name="error-cannot-obtain-the-value-from-the-computer-0x80041013"></a>ERRORE: Impossibile ottenere il valore dal computer, 0x80041013

Si verifica se l'ora nel sistema locale è fuori sincronia di 5 minuti o più. Se l'ora nel computer locale non è sincronizzata, le transazioni sicure hanno esito negativo perché i timestamp non sono validi.

Per risolvere il problema, impostare l'ora di sistema locale il più vicino possibile all'ora di Internet. Oppure, impostare l'ora di sistema locale sull'ora dei controller di dominio della rete.

## <a name="next-steps"></a>Passaggi successivi

[Problemi comuni e soluzioni per i profili di posta elettronica](../configuration/troubleshoot-email-profiles-in-microsoft-intune.md)

Ottenere [supporto da Microsoft](../fundamentals/get-support.md) o usare i [forum della community](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
