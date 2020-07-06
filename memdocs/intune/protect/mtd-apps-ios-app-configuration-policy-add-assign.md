---
title: Aggiungere e assegnare app MTD a Microsoft Intune
titleSuffix: Microsoft Intune
description: Usare Intune per aggiungere app Mobile Threat Defense (MTD), l'app Microsoft Authenticator e criteri di configurazione di iOS nel portale di Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03dbdccd1626db5ad97bc230a3d6b9a82060ee2e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590491"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Aggiungere e assegnare app Mobile Threat Defense (MTD) con Intune

È possibile usare Intune per aggiungere e distribuire app Mobile Threat Defense (MTD), consentendo così agli utenti finali di ricevere notifiche quando viene identificata una minaccia nei dispositivi mobili e per ricevere indicazioni per risolvere le minacce.

> [!NOTE]
> Questo articolo si applica a tutti i partner Mobile Threat Defense.

## <a name="before-you-begin"></a>Prima di iniziare

Completare la procedura seguente in Intune. Assicurarsi di avere familiarità con le procedure seguenti:

- [Aggiunta di un'app in Intune](../apps/apps-add.md).
- [Aggiunta dei criteri di configurazione delle app iOS in Intune](../apps/app-configuration-policies-use-ios.md).
- [Assegnazione di un'app con Intune](../apps/apps-deploy.md).

> [!TIP]
> Nei dispositivi Android il portale aziendale Intune funge da broker per la verifica dell'identità degli utenti da parte di Azure AD.

## <a name="configure-microsoft-authenticator-for-ios"></a>Configurare Microsoft Authenticator per iOS

Per i dispositivi iOS, perché gli utenti possano eseguire la verifica della propria identità in Azure AD, è necessario [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to). Sono anche necessari i criteri di configurazione delle app iOS, che impostano l'app iOS MTD da usare con Intune.

Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store di Microsoft Authenticator ](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) durante la configurazione di **Informazioni sull'app**.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>Configurare le app MTD con i criteri di configurazione di un'app

Per semplificare l'onboarding degli utenti, le app Mobile Threat Defense nei dispositivi gestiti da MDM usano la configurazione dell'app. Poiché per i dispositivi non registrati la configurazione dell'app basata su MDM non è disponibile, vedere [Aggiungere app Mobile Threat Defense a dispositivi non registrati](../protect/mtd-add-apps-unenrolled-devices.md).

### <a name="lookout-for-work-app-configuration-policy"></a>Criteri di configurazione delle app Lookout for Work

Creare i criteri di configurazione delle app iOS come descritto nell'articolo relativo all'[uso dei criteri di configurazione delle app per iOS](../apps/app-configuration-policies-use-ios.md).

### <a name="sep-mobile-app-configuration-policy"></a>Criteri di configurazione delle app SEP Mobile

Usare lo stesso account di Azure AD configurato in precedenza nella [console di gestione di Symantec Endpoint Protection Management](https://aad.skycure.com) che deve corrispondere all'account usato per accedere a Intune.

- **Scaricare** il file dei criteri di configurazione delle app iOS:
  - Passare alla [console di gestione di Symantec Endpoint Protection Management](https://aad.skycure.com) e accedere con le credenziali di amministratore.

  - Andare a **Settings** (Impostazioni) e sotto **Integrations** (Integrazioni) scegliere **Intune**. Scegliere **EMM Integration Selection** (Selezione integrazione EMM). Scegliere **Microsoft** e quindi salvare la selezione.

  - Fare clic sul collegamento **Integration setup files** (File di installazione dell'integrazione) e salvare il file \*.zip generato. Il file con estensione zip contiene il file * **.plist** che verrà usato per creare i criteri di configurazione dell'app iOS in Intune.

  - Vedere le istruzioni per [l'uso di criteri di configurazione di app Microsoft Intune per iOS](../apps/app-configuration-policies-use-ios.md) per aggiungere i criteri di configurazione dell'app SEP Mobile per iOS.

    - Per **Formato delle impostazioni di configurazione** selezionare **Immettere i dati XML**, copiare il contenuto del file ***con estensione plist** e incollare il contenuto nel corpo dei criteri di configurazione.

> [!NOTE]
> Se non è possibile recuperare i file, contattare il [supporto aziendale per Symantec Endpoint Protection Mobile](https://support.symantec.com/en_US/contact-support.html).

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Criteri di configurazione delle app Check Point SandBlast Mobile

Vedere le istruzioni per l'[uso dei criteri di configurazione di app Microsoft Intune per iOS](../apps/app-configuration-policies-use-ios.md) per aggiungere i criteri di configurazione dell'app Check Point SandBlast Mobile per iOS.

- Per **Formato delle impostazioni di configurazione** selezionare **Immettere i dati XML**, copiare il contenuto seguente e incollarlo nel corpo dei criteri di configurazione.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Criteri di configurazione delle app Zimperium

Vedere le istruzioni per [l'uso di criteri di configurazione di app Microsoft Intune per iOS](../apps/app-configuration-policies-use-ios.md) per aggiungere i criteri di configurazione delle app di Zimperium per iOS.

- Per **Formato delle impostazioni di configurazione** selezionare **Immettere i dati XML**, copiare il contenuto seguente e incollarlo nel corpo dei criteri di configurazione.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Criteri di configurazione delle app Pradeo

Pradeo non supporta i criteri di configurazione delle applicazioni in iOS/iPadOS.  In alternativa, per ottenere un'app configurata, collaborare con Pradeo per implementare file IPA o APK personalizzati e preconfigurati con le impostazioni desiderate.

### <a name="better-mobile-app-configuration-policy"></a>Criteri di configurazione delle app Better Mobile

Vedere le istruzioni per [l'uso di criteri di configurazione di app Microsoft Intune per iOS](../apps/app-configuration-policies-use-ios.md) per aggiungere i criteri di configurazione dell'app Better Mobile per iOS.

- Per **Formato delle impostazioni di configurazione** selezionare **Immettere i dati XML**, copiare il contenuto seguente e incollarlo nel corpo dei criteri di configurazione. Sostituire l'URL `https://client.bmobi.net` con l'URL della console appropriato.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Criteri di configurazione delle app Sophos Mobile

Creare i criteri di configurazione delle app iOS come descritto nell'articolo relativo all'[uso dei criteri di configurazione delle app per iOS](../apps/app-configuration-policies-use-ios.md). Per altre informazioni, vedere [Sophos Intercept X for Mobile iOS - Available managed settings](https://community.sophos.com/kb/133963) (Sophos Intercept X for Mobile iOS - Impostazioni gestite disponibili) nella Knowledge base di Sophos.

### <a name="wandera-app-configuration-policy"></a>Criteri di configurazione dell'app Wandera

> [!NOTE]
> Per i test iniziali, usare un gruppo di test quando si assegnano utenti e dispositivi nella sezione Assegnazioni dei criteri di configurazione. 

- **Android**
  - Vedere le istruzioni per [l'uso di criteri di configurazione di app Microsoft Intune per Android](../apps/app-configuration-policies-use-android.md) per aggiungere i criteri di configurazione dell'app Wandera per Android usando le informazioni seguenti quando richiesto.

1. Nel **potale di Wandera RADAR** fare clic sul pulsante **Add+** (Aggiungi) nel formato **Configuration settings** (Impostazioni configurazione).
2. Selezionare **Activation Profile URL** (URL profilo attivazione) dall'elenco **Configuration Keys** (Chiavi configurazione). Fare clic su **OK**.
3. Per **Activation Profile URL** (URL profilo attivazione) selezionare **string** (stringa) dal menu **Value type** (Tipo valore) quindi copiare e incollare **Shareable Link URL** (URL collegamento condivisibile) dal profilo di attivazione desiderato in RADAR.
4. In **Settings** (Impostazioni) definire **Configuration settings format > Use Configuration Designer** (Formato Impostazioni configurazione > Usa progettazione configurazione) ed eseguire i passaggi seguenti.

> [!NOTE] 
> A differenza di iOS, è necessario definire un criterio di configurazione delle app Android Enterprise univoco per ogni profilo di attivazione Wandera. Se non sono necessari più profili di attivazione Wandera, è possibile usare una sola configurazione di app Android per tutti i dispositivi di destinazione. Quando si creano i profili di attivazione in Wandera, assicurarsi di selezionare "Azure Active Directory" nella configurazione Associated User (Utente associato) per assicurarsi che Wandera sia in grado di sincronizzare il dispositivo con Microsoft Endpoint Manager tramite UEM Connect.

- **iOS**
  - Vedere le istruzioni per [l'uso di criteri di configurazione di app Microsoft Intune per iOS](../apps/app-configuration-policies-use-ios.md) per aggiungere i criteri di configurazione dell'app Wandera per iOS usando le informazioni seguenti quando richiesto.

1. Nel **portale Wandera RADAR** passare a **Devices > Activations** (Dispositivi > Attivazioni) e selezionare un profilo di attivazione. Fare clic su **Deployment Strategies > Managed Devices > Microsoft Intune** (Strategie distribuzione > Dispositivi gestiti > Microsoft Intune) e individuare **iOS App Configuration settings** (Impostazioni configurazione app iOS).  
2. Espandere la casella per visualizzare il codice XML di configurazione dell'app iOS e copiarlo negli Appunti di sistema.  
3. In **Settings** (Impostazioni) definire **Configuration settings format > Enter XML data** (Formato Impostazioni configurazione > Immetti dati XML) ed eseguire i passaggi seguenti:
4. Incollare il codice XML nella casella di testo della configurazione app in Microsoft Endpoint Manager.

> [!NOTE]
> Un singolo criterio di configurazione iOS può essere usato in tutti i dispositivi di cui è necessario eseguire il provisioning con Wandera.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Assegnazione di app Mobile Threat Defense agli utenti finali tramite Intune

Per installare l'app Mobile Threat Defense nel dispositivo dell'utente finale, è possibile eseguire i passaggi seguenti nel portale di Azure. Assicurarsi di avere familiarità con le procedure seguenti:

- [Assegnazione di app ai gruppi con Intune](../apps/apps-deploy.md)

Scegliere la sezione corrispondente al provider MTD:

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Assegnazione di Lookout for Work

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store Google per l'app Lookout for Work](https://play.google.com/store/apps/details?id=com.lookout.enterprise) per **URL di App Store**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store iOS per l'app Lookout for Work](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) per **URL di App Store**.

- **App Lookout for Work al di fuori dell'Apple Store**
  - Firmare di nuovo l'app Lookout for Work per iOS. Lookout distribuisce la sua app Lookout for Work per iOS esternamente all'App Store iOS. Prima di distribuire l'app, è necessario firmare di nuovo l'app usando il proprio iOS Enterprise Developer Certificate.  
  - Per istruzioni dettagliate su come firmare di nuovo l'app Lookout for Work per iOS, vedere [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) (Processo per firmare di nuovo l'app Lookout for Work per iOS) nel sito Web Lookout.

  - **Abilitare l'autenticazione di Azure AD per gli utenti dell'app Lookout for Work per iOS.**

    1. Passare al [Portale di Azure](https://portal.azure.com), accedere con le credenziali personali e quindi passare alla pagina dell'applicazione.

    2. Aggiungere l'**app Lookout for Work per iOS** come **applicazione client nativa**.

    3. Sostituire a **com.lookout.enterprise.nomeazienda** l'ID bundle cliente selezionato alla firma dell'IPA.

    4. Aggiungere l'URI di reindirizzamento aggiuntivo: **&lt;portaleaziendale://code/>** seguito da una versione con codifica URL dell'URI di reindirizzamento originale.

    5. Aggiungere le **autorizzazioni delegate** all'app.

    > [!NOTE]
    > Per altri dettagli, vedere [Configurare un'applicazione client nativa con Azure AD](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).

  - **Aggiungere il file ipa di Lookout for Work.**

    - Caricare il file con estensione ipa nuovamente firmato come descritto nell'articolo [Aggiungere un'app line-of-business per iOS a Microsoft Intune](../apps/lob-apps-ios.md). È anche necessario impostare la versione iOS minima su iOS 8.0 o successiva.

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Assegnazione di Symantec Endpoint Protection Mobile

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app SEP Mobile](https://play.google.com/store/apps/details?id=com.skycure.skycure) per **URL di App Store**.  Per **Sistema operativo minimo** selezionare **Android 4.0 (Ice Cream Sandwich)** .

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app SEP Mobile](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) per **URL di App Store**.

### <a name="assigning-check-point-sandblast-mobile"></a>Assegnazione di Check Point SandBlast Mobile

- **Android**  
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app Check Point SandBlast Mobile](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) per **URL di App Store**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app Check Point SandBlast Mobile](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) per **URL di App Store**.  

### <a name="assigning-zimperium"></a>Assegnazione di Zimperium

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app Zimperium](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) per **URL di App Store**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app Zimperium](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) per **URL di App Store**.  
 
### <a name="assigning-pradeo"></a>Assegnazione di Pradeo

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app Pradeo](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) per **URL di App Store**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app Pradeo](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) per **URL di App Store**.

### <a name="assigning-better-mobile"></a>Assegnazione di Better Mobile

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app Active Shield](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) per **URL di App Store**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app Active Shield](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) per **URL di App Store**.

### <a name="assigning-sophos"></a>Assegnazione di Sophos

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app Sophos](https://play.google.com/store/apps/details?id=com.sophos.smsec) per **URL di App Store**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app Active Shield](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) per **URL di App Store**.

### <a name="assigning-wandera"></a>Assegnazione di Wandera

- **Android**
  - Vedere le istruzioni per [aggiungere app di Android Store a Microsoft Intune](../apps/store-apps-android.md). Usare questo [URL dell'App Store per l'app Wandera Mobile](https://play.google.com/store/apps/details?id=com.wandera.android) per **URL di App Store**. Per **Sistema operativo minimo** selezionare **Android 5.0**.

- **iOS**
  - Vedere le istruzioni per [aggiungere app dello Store iOS a Microsoft Intune](../apps/store-apps-ios.md). Usare questo [URL dell'App Store per l'app Wandera Mobile](https://itunes.apple.com/app/wandera/id605469330) per **URL di App Store**.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare i criteri di conformità dei dispositivi per MTD](mtd-device-compliance-policy-create.md)
