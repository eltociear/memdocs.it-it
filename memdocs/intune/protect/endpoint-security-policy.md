---
title: Gestire i criteri di sicurezza degli endpoint in Microsoft Intune | Microsoft Docs
description: Informazioni su come gli amministratori della sicurezza possono usare i criteri di sicurezza degli endpoint e i profili per concentrarsi sulla configurazione della sicurezza dei dispositivi in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 9c2e6f742610eb8f2f526c6fc7a5afabfbadcbbf
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990857"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Gestire la sicurezza dei dispositivi con i criteri di sicurezza degli endpoint in Microsoft Intune

In qualità di amministratore della sicurezza è possibile usare i criteri di sicurezza da *Sicurezza degli endpoint* di Intune per configurare la sicurezza dei dispositivi senza l'overhead correlato all'esplorazione del corpo più ampio e della gamma di impostazioni presenti nei profili di configurazione dei dispositivi e nelle baseline di sicurezza.

Ogni tipo di criterio supporta uno o più profili. I profili consentono di configurare le impostazioni e di raggruppare le impostazioni per piattaforme diverse o per aree di interesse diverse nell'area dei criteri più ampia.

Questi criteri sono disponibili in *Gestione* nel nodo **Endpoint security** (Sicurezza degli endpoint) dell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

![Gestire i criteri](./media/endpoint-security-policy/endpoint-security-policies.png)

Di seguito sono riportate brevi descrizioni di ogni tipo di criterio di sicurezza degli endpoint. Per altre informazioni sui tipi di criteri e sui profili disponibili per ognuno di essi, seguire i collegamenti al contenuto dedicato a ogni tipo di criterio:

- [Antivirus](../protect/endpoint-security-antivirus-policy.md): i criteri antivirus consentono agli amministratori della sicurezza di concentrarsi sulla gestione del gruppo specifico di impostazioni antivirus per i dispositivi gestiti. Per usare i criteri antivirus, integrare Intune con Microsoft Defender Advanced Threat Protection (Defender ATP) come soluzione Mobile Threat Defense.

- [Crittografia del disco](../protect/endpoint-security-disk-encryption-policy.md): i profili di crittografia del disco per la sicurezza degli endpoint si concentrano solo sulle impostazioni rilevanti per un metodo di crittografia predefinito dei dispositivi, ad esempio FileVault o BitLocker. Questo focus consente agli amministratori della sicurezza di gestire in modo semplice le impostazioni di crittografia del disco senza dover passare in un host di impostazioni non correlate.

- [Firewall](../protect/endpoint-security-firewall-policy.md): usare i criteri firewall per la sicurezza degli endpoint in Intune per configurare un firewall predefinito dei dispositivi per i dispositivi che eseguono macOS e Windows 10. I firewall predefiniti includono BitLocker per i dispositivi Windows e FileVault per macOS.

- [Rilevamento di endpoint e risposta](../protect/endpoint-security-edr-policy.md): quando si integra Defender ATP con Intune, è possibile usare i criteri di sicurezza degli endpoint per il rilevamento di endpoint e risposta (EDR) per gestire le impostazioni EDR ed eseguire l'onboarding di dispositivi in Defender ATP.

- [Riduzione della superficie di attacco](../protect/endpoint-security-asr-policy.md): quando l'antivirus Defender viene usato nei dispositivi Windows 10, è possibile usare i criteri di sicurezza degli endpoint per la riduzione della superficie di attacco di Intune per gestire le impostazioni per i dispositivi.

- [Protezione account](../protect/endpoint-security-account-protection-policy.md): i criteri di protezione account consentono di proteggere l'identità e gli account degli utenti. I criteri di protezione account sono incentrati sulle impostazioni per Windows Hello e Credential Guard, che fanno parte della gestione di identità e accessi di Windows.

Le sezioni seguenti si applicano a tutti i criteri di sicurezza degli endpoint.

## <a name="create-an-endpoint-security-policy"></a>Creare un criterio di sicurezza degli endpoint

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint security** (Sicurezza degli endpoint), quindi selezionare il tipo di criterio da configurare e selezionare **Crea criterio**. Scegliere uno dei tipi di criteri seguenti:
   - Antivirus
   - Crittografia del disco
   - Firewall
   - Rilevamento di endpoint e risposta
   - Riduzione della superficie di attacco
   - Protezione account

3. Immettere le proprietà seguenti:
   - **Piattaforma**: Scegliere la piattaforma per cui si stanno creando i criteri. Le opzioni disponibili dipendono dal tipo di criterio selezionato:
     - macOS
     - Windows 10 e versioni successive
   - **Profilo**: Scegliere tra i profili disponibili per la piattaforma selezionata. Per informazioni sui profili, vedere la sezione dedicata in questo articolo per il tipo di criterio scelto.

4. Selezionare **Crea**.

5. Nella pagina **Informazioni di base** immettere un nome e una descrizione per il profilo, quindi scegliere **Avanti**.

6. Nella pagina **Impostazioni di configurazione** espandere ogni gruppo di impostazioni e configurare quelle da gestire con questo profilo.

   Al termine della configurazione delle impostazioni, selezionare **Avanti**.

7. Nella pagina **Tag di ambito** scegliere **Selezionare i tag di ambito** per aprire il riquadro *Seleziona tag* per assegnare tag di ambito al profilo.
  
   Selezionare **Avanti** per continuare.

8. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

   Selezionare **Avanti**.

9. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

## <a name="duplicate-a-policy"></a>Duplicare un criterio

I criteri di sicurezza degli endpoint supportano la duplicazione per creare una copia dei criteri originali. La duplicazione di un criterio può essere utile quando è necessario assegnare criteri simili a gruppi diversi ma non si vuole ricreare manualmente tutti i criteri. È invece possibile duplicare i criteri originali e quindi introdurre solo le modifiche richieste dai nuovi criteri. È possibile modificare solo un'impostazione specifica e il gruppo a cui sono assegnati i criteri.

Quando si crea un duplicato, si assegna alla copia un nuovo nome. La copia viene creata con le stesse configurazioni di impostazione e tag di ambito dell'originale, ma non avrà assegnazioni. Per creare assegnazioni è necessario modificare i nuovi criteri in un secondo momento.  

I tipi di criteri seguenti supportano la duplicazione:

- Antivirus
- Crittografia del disco
- Firewall
- Rilevamento di endpoint e risposta
- Riduzione della superficie di attacco
- Protezione account

Dopo aver creato i nuovi criteri, rivederli e modificarli per apportare modifiche alla relativa configurazione.

### <a name="to-duplicate-a-policy"></a>Per duplicare un criterio

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare il criterio da copiare. Selezionare quindi **Duplica** oppure selezionare i puntini di sospensione ( **...** ) a destra del criterio e selezionare **Duplica**.
3. Specificare un **Nuovo nome** per il criterio e quindi selezionare **Salva**.

### <a name="to-edit-a-policy"></a>Per modificare un criterio

1. Selezionare il nuovo criterio, quindi selezionare **Proprietà**.
2. Selezionare Impostazioni per espandere un elenco delle impostazioni di configurazione nel criterio. Non è possibile modificare le impostazioni da questa visualizzazione, ma è possibile esaminare il modo in cui sono state configurate.
3. Per modificare il criterio, selezionare **Modifica** per ogni categoria in cui si vuole apportare una modifica:
   - Informazioni di base
   - Assignments
   - Tag di ambito
   - Impostazioni di configurazione
4. Dopo aver apportato le modifiche, selezionare **Salva** per salvare le modifiche.  È necessario salvare le modifiche apportate a una categoria prima di poter introdurre modifiche a categorie aggiuntive.

## <a name="manage-conflicts"></a>Gestire i conflitti

Molte delle impostazioni del dispositivo che è possibile gestire con i criteri di sicurezza degli endpoint (criteri di sicurezza) possono essere gestite tramite altri tipi di criteri in Intune. Questi altri tipi di criteri includono criteri di *configurazione del dispositivo* e *baseline di sicurezza*. Poiché è possibile gestire un'impostazione con diversi tipi di criteri o più istanze dello stesso tipo di criteri, è necessario prepararsi per identificare e risolvere i conflitti tra criteri nel caso in cui un dispositivo non sia conforme alle configurazioni previste.

- Le baseline di sicurezza possono impostare un valore non predefinito per un'impostazione per motivi di conformità con la configurazione consigliata per la baseline.
- Per impostazione predefinita, gli altri tipi di criteri, inclusi i criteri di sicurezza degli endpoint, impostano il valore *Non configurato*. Per questi altri tipi di criteri è necessario configurare in modo esplicito le impostazioni nei criteri.

Indipendentemente dal metodo dei criteri, la gestione della stessa impostazione sullo stesso dispositivo tramite più tipi di criteri oppure tramite più istanze dello stesso tipo di criteri può causare conflitti che devono essere evitati.

Per identificare e risolvere i conflitti, usare le informazioni disponibili nei collegamenti seguenti:

- [Risolvere problemi relativi a criteri e profili in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorare le baseline di sicurezza](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Passaggi successivi

[Gestire la sicurezza degli endpoint in Intune](../protect/endpoint-security.md)
