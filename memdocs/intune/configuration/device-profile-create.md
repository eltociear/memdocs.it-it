---
title: Creare profili di dispositivo in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o configurare un profilo di configurazione del dispositivo in Microsoft Intune. Selezionare il tipo di piattaforma, configurare le impostazioni e aggiungere un tag di ambito.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74e365e50d73bb14f20376c92b43061b12d00003
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988458"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Creare un profilo di dispositivo in Microsoft Intune

I profili di dispositivo consentono di aggiungere e configurare impostazioni e quindi di eseguire il push di queste impostazioni nei dispositivi dell'organizzazione. Per informazioni più dettagliate e procedure, vedere [Applicare le impostazioni delle funzionalità nei dispositivi usando i profili dei dispositivi in Microsoft Intune](device-profiles.md).

Questo articolo:

- Elenca i passaggi da eseguire per creare un profilo.
- Illustra come aggiungere un tag di ambito per "filtrare" il profilo.
- Descrive le regole di applicabilità nei dispositivi Windows 10 e illustra come creare una regola.
- Elenca la frequenza dei cicli di aggiornamento quando i dispositivi ricevono i profili e i relativi aggiornamenti.

## <a name="create-the-profile"></a>Creare il profilo

I profili si creano nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). In questa interfaccia di amministrazione selezionare **Dispositivi**. Sono disponibili le seguenti opzioni:

- **Panoramica**: elenca lo stato dei profili e offre dettagli aggiuntivi sui profili assegnati a utenti e dispositivi.
- **Monitoraggio**: consente di verificare lo stato dei profili e le operazioni riuscite e non riuscite, nonché di visualizzare i log per i profili.
- **Per piattaforma**: consente di creare e visualizzare criteri e profili in base alla propria piattaforma. Questa visualizzazione può anche mostrare le funzionalità specifiche della piattaforma. Selezionare, ad esempio, **Windows**. Verranno visualizzate le funzionalità specifiche di Windows, ad esempio **anelli di aggiornamento di Windows 10** e **script di PowerShell**.
- **Policy** (Criteri): consente di creare profili di dispositivo, caricare [script di PowerShell](../apps/intune-management-extension.md) personalizzati da eseguire nei dispositivi e di aggiungere piani dati ai dispositivi che usano [eSIM](esim-device-configuration.md).

Quando si crea un profilo (**Profili di configurazione** > **Crea profilo**), scegliere la piattaforma:

- **Amministratore di dispositivi Android**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 e versioni successive**
- **Windows 8.1 e versioni successive**
- **Windows Phone 8.1**

Quindi, scegliere il tipo di profilo. Le impostazioni configurabili variano in base alla piattaforma scelta. Gli articoli seguenti descrivono le impostazioni per i vari tipi di profilo:

- [Modelli amministrativi (Windows)](administrative-templates-windows.md)
- [Personalizzato](custom-settings-configure.md)
- [Ottimizzazione recapito (Windows)](delivery-optimization-windows.md)
- [Credenziali derivate (Android Enterprise, iOS, iPadOS)](../protect/derived-credentials.md)
- [Funzionalità del dispositivo (macOS, iOS, iPadOS)](device-features-configure.md)
- [Firmware del dispositivo (Windows)](device-firmware-configuration-interface-windows.md)
- [Restrizioni dei dispositivi](device-restrictions-configure.md)
- [Aggiunta a un dominio (Windows)](domain-join-configure.md)
- [Aggiornamento dell'edizione e cambio di modalità (Windows)](edition-upgrade-configure-windows-10.md)
- [Formazione (iOS, iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [Posta elettronica](email-settings-configure.md)
- [Endpoint Protection (macOS, Windows)](../protect/endpoint-protection-configure.md)
- [Estensioni (macOS)](kernel-extensions-overview-macos.md)
- [Protezione dell'identità (Windows)](../protect/identity-protection-configure.md)
- [Modalità tutto schermo](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [Profilo Mobility Extensions (MX) (Amministratore di dispositivi Android)](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [Certificato PKCS](../protect/certficates-pfx-configure.md)
- [Certificato importato PKCS](../protect/certificates-imported-pfx-configure.md)
- [File delle preferenze (macOS)](preference-file-settings-macos.md)
- [Certificato SCEP](../protect/certificates-scep-configure.md)
- [Valutazione sicura (Education) (Windows)](education-settings-configure.md)
- [Dispositivi multiutente condivisi (Windows)](shared-user-device-settings.md)
- [Spese per telecomunicazioni (Amministratore di dispositivi Android, iOS, iPadOS)](telecom-expenses-monitor.md)
- [Certificato attendibile](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)

Se ad esempio si seleziona come piattaforma **iOS/iPadOS**, le opzioni del profilo sono simili a quelle del profilo seguente:

:::image type="content" source="./media/device-profile-create/create-device-profile.png" alt-text="Creare un profilo iOS/iPados in Microsoft Intune.":::

## <a name="scope-tags"></a>Tag di ambito

Dopo aver aggiunto le impostazioni, si può anche aggiungere un tag di ambito al profilo. I tag di ambito filtrano i profili per gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Inoltre, vengono usati nell'IT distribuito.

Per altre informazioni sui tag di ambito e le relative procedure, vedere [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito).

## <a name="applicability-rules"></a>Regole di applicabilità

Si applica a:

- Windows 10 e versioni successive

Le regole di applicabilità consentono agli amministratori di fare riferimento a dispositivi in un gruppo che soddisfano criteri specifici. Ad esempio, si crea un profilo di restrizioni del dispositivo che si applica al gruppo **Tutti i dispositivi Windows 10**. Si vuole che il profilo venga assegnato solo ai dispositivi che eseguono Windows 10 Enterprise.

Per eseguire questa attività, creare una **regola di applicabilità**. Queste regole sono utili per gli scenari seguenti:

- Si usa Windows 10 Education (EDU). Nel Bellows College, l'obiettivo è raggiungere tutti i dispositivi Windows 10 EDU con versioni comprese tra RS3 e RS4.
- In Contoso si vuole raggiungere tutti gli utenti del reparto Risorse umane, ma solo i dispositivi con Windows 10 Professional o Enterprise.

Per affrontare questi scenari, è necessario:

- Creare un gruppo di dispositivi che include tutti i dispositivi del Bellows College. Nel profilo aggiungere una regola di applicabilità che viene implementata se la versione minima del sistema operativo è `16299` e la versione massima è `17134`. Assegnare questo profilo al gruppo di dispositivi del Bellows College.

  Quando viene assegnato, il profilo viene applicato ai dispositivi con una versione compresa tra la versione minima e la versione massima specificate. Per i dispositivi la cui versione non è inclusa tra le versioni minima e massima specificate, lo stato visualizzato è **Non applicabile**.

- Creare un gruppo di utenti che include tutti gli utenti del reparto Risorse umane (HR) di Contoso. Nel profilo aggiungere una regola di applicabilità che seleziona i dispositivi che eseguono Windows 10 Professional o Enterprise. Assegnare questo profilo al gruppo di utenti HR.

  Quando viene assegnato, il profilo si applica ai dispositivi che eseguono Windows 10 Professional o Enterprise. Per i dispositivi che non eseguono queste edizioni, lo stato visualizzato è **Non applicabile**.

- Se sono presenti due profili con le stesse impostazioni esatte, viene applicato il profilo che non include una regola di applicabilità. 

  Ad esempio, ProfileA è destinato al gruppo dispositivi Windows 10, abilita BitLocker e non ha una regola di applicabilità. ProfileB è destinato allo stesso gruppo di dispositivi Windows 10, abilita BitLocker e ha una regola di applicabilità per cui il profilo viene applicato solo a Windows 10 Enterprise.

  Quando sono assegnati entrambi i profili viene applicato ProfileA, perché non ha una regola di applicabilità. 

Quando si assegna il profilo ai gruppi, le regole di applicabilità fanno da filtro e si applicano solo i dispositivi che soddisfano i criteri.

### <a name="add-a-rule"></a>Aggiungere una regola

1. Selezionare **Regole di applicabilità**. È possibile scegliere la **Regola** e la **Proprietà**:

    :::image type="content" source="./media/device-profile-create/applicability-rules.png" alt-text="Aggiungere una regola di applicabilità al profilo di configurazione di un dispositivo Windows 10 in Microsoft Intune.":::

2. In **Regola** scegliere se si vuole includere o escludere utenti o gruppi. Le opzioni disponibili sono:

    - **Assegna un profilo se**: include utenti o gruppi che soddisfano i criteri immessi.
    - **Non assegnare un profilo se**: esclude utenti o gruppi che soddisfano i criteri immessi.

3. In **Proprietà** scegliere il filtro. Le opzioni disponibili sono: 

    - **Edizione del sistema operativo**: nell'elenco selezionare le edizioni di Windows 10 che si vuole includere (o escludere) nella regola.
    - **Versione del sistema operativo**: immettere i numeri di versione **Min** e **Max** di Windows 10 che si vuole includere (o escludere) nella regola. Entrambi i valori sono obbligatori.

      Ad esempio è possibile immettere `10.0.16299.0` (RS3 o 1709) per la versione minima e `10.0.17134.0` (RS4 o 1803) per la versione massima. In alternativa è possibile adottare una granularità maggiore e immettere `10.0.16299.001` per la versione minima e `10.0.17134.319` per la versione massima.

4. Selezionare **Aggiungi** per salvare le modifiche.

## <a name="refresh-cycle-times"></a>Frequenza dei cicli di aggiornamento

Intune usa cicli di aggiornamento diversi per verificare la disponibilità di aggiornamenti per i profili di configurazione. Se il dispositivo è stato registrato di recente, il controllo viene eseguito con maggiore frequenza. [Cicli di aggiornamento di criteri e profili](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) elenca i tempi di aggiornamento stimati.

Gli utenti possono aprire in qualsiasi momento l'app Portale aziendale e sincronizzare il dispositivo per controllare immediatamente la disponibilità di aggiornamenti del profilo.

## <a name="recommendations"></a>Indicazioni

Durante la creazione dei profili, tenere presenti le indicazioni seguenti:

- Assegnare un nome ai criteri in modo da sapere quali sono e qual è la loro funzione. Tutti i [criteri di conformità](../protect/create-compliance-policy.md) e i [profili di configurazione](../configuration/device-profile-create.md) hanno una proprietà **Descrizione** facoltativa. In **Descrizione** immettere informazioni specifiche che consentano agli altri utenti di individuare la funzione dei criteri.

  Di seguito alcuni esempi di profilo di configurazione:

  **Nome profilo**: Modello amministrativo: profilo di configurazione OneDrive per tutti gli utenti di Windows 10  
  **Descrizione profilo**: Profilo del modello amministrativo di OneDrive che include le impostazioni minime e di base per tutti gli utenti di Windows 10. Creato da user@contoso.com per impedire agli utenti di condividere i dati dell'organizzazione con account OneDrive personali.

  **Nome profilo**: Profilo VPN per tutti gli utenti iOS/iPadOS  
  **Descrizione profilo**: Profilo VPN che include le impostazioni minime e di base per tutti gli utenti iOS/iPadOS per connettersi alla VPN Contoso. Creato da user@contoso.com in modo che gli utenti eseguano automaticamente l'autenticazione alla VPN, anziché richiedere loro nome utente e password.

- Creare il profilo in base all'attività, ad esempio configurare le impostazioni di Microsoft Edge, abilitare le impostazioni antivirus di Microsoft Defender, bloccare i dispositivi iOS/iPadOS jailbroken e così via.

- Creare profili che si applicano a gruppi specifici, ad esempio marketing, vendite, amministratori IT o in base alla posizione o al sistema dell'istituto di istruzione.

- Separare i criteri utente dai criteri del dispositivo.

  Ad esempio [Modelli amministrativi in Intune](administrative-templates-windows.md) contiene migliaia di impostazioni ADMX. Questi modelli indicano se un'impostazione si applica a utenti o dispositivi. Quando si creano modelli amministrativi, assegnare le impostazioni degli utenti a un gruppo di utenti e assegnare le impostazioni dei dispositivi a un gruppo di dispositivi.

  Nell'immagine seguente viene illustrato un esempio di impostazione che può essere applicata agli utenti e/o ai dispositivi:

  :::image type="content" source="./media/device-profile-create/setting-applies-to-user-and-device.png" alt-text="Modello amministrativo di Intune applicato a utenti e dispositivi.":::

- Ogni volta che si creano criteri restrittivi, comunicare questa modifica agli utenti. Ad esempio, se si modifica il requisito per il passcode da 4 a 6 caratteri, informare gli utenti prima di assegnare i criteri.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
