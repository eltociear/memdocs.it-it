---
title: Configurare una VPN o una VPN per app per i dispositivi Android Enterprise in Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Usare criteri di configurazione app per aggiungere o creare un profilo VPN o VPN per app per i dispositivi Android Enterprise in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262898"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>Usare una VPN e criteri VPN per app nei dispositivi Android Enterprise in Microsoft Intune

Le reti private virtuali (VPN) consentono agli utenti di accedere alle risorse dell'organizzazione in remoto, ad esempio da casa o da un hotel, un caffè e così via. In Microsoft Intune è possibile configurare le app client VPN nei dispositivi Android Enterprise usando criteri di configurazione app. Quindi è possibile distribuire questi criteri con la relativa configurazione VPN nei dispositivi dell'organizzazione.

È anche possibile creare criteri VPN usati da app specifiche. Questa funzionalità è denominata VPN per app. Quando l'app è attiva, può connettersi alla VPN e accedere alle risorse tramite la VPN. Quando l'app non è attiva, la VPN non viene usata.

Questa funzionalità si applica a:

- Android Enterprise

Esistono due modi per creare i criteri di configurazione app per l'app client VPN:

- Progettazione configurazione
- Dati JSON

Questo articolo illustra come creare una VPN per app e criteri di configurazione app VPN usando entrambe le opzioni.

> [!NOTE]
> Molti parametri di configurazione del client VPN sono simili. Tuttavia, ogni app dispone di chiavi e opzioni univoche. In caso di dubbi, rivolgersi al fornitore della VPN.

## <a name="before-you-begin"></a>Prima di iniziare

- Android non attiva automaticamente una connessione client VPN quando si apre un'app. La connessione VPN deve essere avviata manualmente. In alternativa è possibile usare la [VPN sempre attiva](../configuration/vpn-settings-android-enterprise.md) per avviare la connessione.

- I client VPN seguenti supportano i criteri di configurazione app di Intune:

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - SonicWall Mobile Connect

- Quando si creano i criteri VPN in Intune è necessario selezionare chiavi diverse per la configurazione. I nomi di queste chiavi variano a seconda delle diverse app client VPN. Pertanto i nomi delle chiavi nell'ambiente in uso possono essere diversi dagli esempi in questo articolo.

- Progettazione configurazione e i dati JSON possono usare l'autenticazione basata sui certificati. Se l'autenticazione VPN richiede certificati client, creare i profili certificato prima di creare i criteri VPN. I criteri di configurazione app VPN usano i valori dei profili certificato.

  I dispositivi del profilo di lavoro Android Enterprise supportano i certificati SCEP e PKCS. I dispositivi del profilo di lavoro Android Enterprise completamente gestiti, dedicati e di proprietà dell'azienda supportano solo i certificati SCEP. Per altre informazioni, vedere [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).

## <a name="per-app-vpn-overview"></a>Panoramica della VPN per app

Quando si crea e si esegue il testing di una VPN per app, il flusso di lavoro di base include i passaggi seguenti:

1. Selezionare l'applicazione client VPN. [Prima di iniziare](#before-you-begin) (in questo articolo) elenca le app supportate.
2. Ottenere gli ID pacchetto dell'applicazione per le app che useranno la connessione VPN. [Ottenere l'ID pacchetto dell'app](#get-the-app-package-id) (in questo articolo) illustra come fare.
3. Se si usano certificati per autenticare la connessione VPN, creare e distribuire i profili certificato prima di distribuire i criteri VPN. Verificare la corretta distribuzione dei profili certificato. Per altre informazioni, vedere [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).
4. Aggiungere l'[applicazione client VPN](apps-add-android-for-work.md) a Intune e distribuire l'app agli utenti e ai dispositivi.
5. Creare i criteri di configurazione app VPN. Usare gli ID pacchetto dell'app e le informazioni sui certificati nei criteri.
6. Distribuire i nuovi criteri VPN.
7. Verificare che l'app client VPN si connetta correttamente al server VPN.
8. Quando l'app è attiva, verificare che il traffico proveniente dall'app attraversi correttamente la VPN.

## <a name="get-the-app-package-id"></a>Ottenere l'ID pacchetto dell'app

Ottenere l'ID pacchetto per ogni applicazione che userà la VPN. Per le applicazioni disponibili pubblicamente, è possibile ottenere l'ID pacchetto dell'app in Google Play Store. L'URL visualizzato per ogni applicazione include l'ID pacchetto.

Nell'esempio seguente, l'ID pacchetto dell'app browser Microsoft Edge è `com.microsoft.emmx`. L'ID pacchetto è incluso nell'URL:

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="Ottenere l'ID pacchetto dell'app nell'URL in Google Play Store.":::

Per le app line-of-business (LOB), ottenere l'ID pacchetto dal fornitore o dallo sviluppatore di applicazioni.

## <a name="certificates"></a>Certificati

Questo articolo presuppone che la connessione VPN usi l'autenticazione basata su certificati. Presuppone anche che siano stati distribuiti correttamente nella catena tutti i certificati necessari per l'autenticazione dei client. In genere questa catena di certificati include il certificato client, gli eventuali certificati intermedi e il certificato radice.

Per altre informazioni sui certificati, vedere [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).

Quando il profilo del certificato di autenticazione client viene distribuito, crea un token del certificato nel profilo del certificato. Questo token viene usato per creare i criteri di configurazione app VPN.

Se non si ha familiarità con la creazione dei criteri di configurazione app, vedere [Aggiungere criteri di configurazione delle app per i dispositivi Android gestiti](app-configuration-policies-use-android.md).

## <a name="use-the-configuration-designer"></a>Usare la finestra di progettazione della configurazione

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Criteri di configurazione dell'app** > **Aggiungi** > **Dispositivi gestiti**.
3. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criteri valido è **Criteri di configurazione dell'app: Criteri VPN Cisco AnyConnect per dispositivi del profilo di lavoro Android Enterprise**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: selezionare **Android Enterprise**.
    - **Tipo di profilo**: Le opzioni disponibili sono:
      - **Tutti i tipi di profilo**: questa opzione supporta l'autenticazione con nome utente e password. Se si usa l'autenticazione basata su certificato, non usare questa opzione.
      - **Solo profilo di lavoro completamente gestito, dedicato e di proprietà aziendale**: questa opzione supporta l'autenticazione basata su certificati e l'autenticazione con nome utente e password.
      - **Solo profilo di lavoro**: questa opzione supporta l'autenticazione basata su certificati e l'autenticazione con nome utente e password.
    - **App interessate**: selezionare l'app client VPN aggiunta in precedenza. Nell'esempio seguente viene usata l'app client VPN Cisco AnyConnect:

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="Creare criteri di configurazione app per configurare VPN o VPN per app in Microsoft Intune":::

4. Selezionare **Avanti**.
5. In **Impostazioni** immettere le proprietà seguenti:

    - **Formato delle impostazioni di configurazione**: selezionare **Usa progettazione configurazione**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="Creare criteri di configurazione app VPN in Microsoft Intune usando Progettazione configurazione - Esempio.":::

    - **Aggiungi**: visualizza l'elenco delle chiavi di configurazione. Selezionare tutte le chiavi di configurazione necessarie per la configurazione > Scegliere **OK**.

      In questo esempio è stato selezionato un elenco minimo per una VPN AnyConnect, che include l'autenticazione basata su certificati e la VPN per app:
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="Aggiungere chiavi di configurazione ai criteri di configurazione app VPN in Microsoft Intune usando Progettazione configurazione - Esempio.":::

    - **Valore di configurazione**: immettere i valori delle chiavi di configurazione selezionate. Tenere presente che i nomi delle chiavi variano a seconda dell'app client VPN in uso. Nelle chiavi selezionate nell'esempio:

      - **Per App VPN Allowed Apps** (VPN per app - App consentite): immettere l'ID o gli ID pacchetto dell'applicazione raccolti in precedenza. Ad esempio:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="Immettere gli ID pacchetto dell'applicazione consentiti in criteri di configurazione app VPN in Microsoft Intune usando Progettazione configurazione - Esempio.":::

      - **KeyChain Certificate Alias** (Alias certificato Keychain) (facoltativo): Modificare **Tipo di valore** da **stringa** a **certificato**. Selezionare il profilo di certificato client da usare con l'autenticazione VPN. Ad esempio:

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="Modificare l'alias del certificato client keychain nei criteri di configurazione app VPN in Microsoft Intune usando Progettazione configurazione - Esempio.":::

      - **Protocollo**: Selezionare il protocollo di tunneling **SSL** o **IPsec** della VPN.
      - **Nome connessione**: immettere un nome descrittivo per la connessione VPN. Gli utenti visualizzano questo nome connessione nei dispositivi. Immettere ad esempio `ContosoVPN`.
      - **Host**: immettere l'URL del nome host per il router centralina. Immettere ad esempio `vpn.contoso.com`.

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="Esempi di protocollo, nome connessione e nome host nei criteri di configurazione app VPN in Microsoft Intune con Progettazione configurazione":::

6. Selezionare **Avanti**.
7. In **Assegnazioni** selezionare i gruppi a cui assegnare i criteri di configurazione app VPN.

    Selezionare **Avanti**.

8. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea** le modifiche vengono salvate e i criteri vengono distribuiti ai gruppi. I criteri vengono visualizzati anche nell'elenco dei criteri di configurazione app.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="Esaminare i criteri di configurazione app usando il flusso Progettazione configurazione in Microsoft Intune - Esempio.":::

## <a name="use-json"></a>Usare JSON

Usare questa opzione se non si hanno o non si conoscono tutte le impostazioni VPN richieste e usate nella **finestra di progettazione di configurazione**. Per assistenza, rivolgersi al fornitore della VPN.

### <a name="get-the-certificate-token"></a>Ottenere il token del certificato

In questi passaggi si creeranno criteri temporanei. I criteri non verranno salvati. Lo scopo è copiare il token del certificato. Questo token verrà usato durante la creazione dei criteri VPN con JSON (sezione successiva).

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Criteri di configurazione dell'app** > **Aggiungi** > **Dispositivi gestiti**.
2. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome qualsiasi. Questi criteri sono temporanei e non verranno salvati.
    - **Piattaforma**: selezionare **Android Enterprise**.
    - **Tipo di profilo**: selezionare **Solo profilo di lavoro**.
    - **App interessate**: selezionare l'app client VPN aggiunta in precedenza.

3. Selezionare **Avanti**.
4. In **Impostazioni** immettere le proprietà seguenti:

    - **Formato delle impostazioni di configurazione**: selezionare **Usa progettazione configurazione**.
    - **Aggiungi**: visualizza l'elenco delle chiavi di configurazione. Selezionare una chiave con **Tipo di valore** corrispondente a **stringa**. Selezionare **OK**.

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="In Progettazione configurazione selezionare una chiave con tipo di valore stringa nei criteri di configurazione app VPN di Microsoft Intune":::

5. Modificare **Tipo di valore** da **stringa** a **certificato**. Questo passaggio consente di selezionare il profilo di certificato client corretto che autentica la VPN:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="Modificare il nome della connessione nei criteri di configurazione app VPN in Microsoft Intune - Esempio":::

6. Modificare immediatamente il **Tipo di valore** di nuovo in **stringa**. **Valore di configurazione** diventa un token `{{cert:GUID}}`:

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="Il valore di configurazione visualizza il token del certificato nei criteri di configurazione app VPN in Microsoft Intune":::

7. Copiare e incollare questo token del certificato in un altro file, ad esempio in un editor di testo.

8. Ignorare questi criteri. Non salvarli. Sono necessari solo per copiare e incollare il token del certificato.

### <a name="create-the-vpn-policy-using-json"></a>Creare i criteri VPN usando JSON

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **App** > **Criteri di configurazione dell'app** > **Aggiungi** > **Dispositivi gestiti**.

2. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criteri valido è **Criteri di configurazione dell'app: criteri VPN Cisco AnyConnect JSON per dispositivi del profilo di lavoro Android Enterprise nell'intera azienda**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: selezionare **Android Enterprise**.
    - **Tipo di profilo**: Le opzioni disponibili sono:
      - **Tutti i tipi di profilo**: questa opzione supporta l'autenticazione con nome utente e password. Se si usa l'autenticazione basata su certificato, non usare questa opzione.
      - **Solo profilo di lavoro completamente gestito, dedicato e di proprietà aziendale**: questa opzione supporta l'autenticazione basata su certificati e l'autenticazione con nome utente e password.
      - **Solo profilo di lavoro**: questa opzione supporta l'autenticazione basata su certificati e l'autenticazione con nome utente e password.
    - **App interessate**: selezionare l'app client VPN aggiunta in precedenza. 

3. Selezionare **Avanti**.
4. In **Impostazioni** immettere le proprietà seguenti:

    - **Formato delle impostazioni di configurazione**: selezionare **Immettere i dati JSON**. È possibile modificare direttamente il codice JSON.
    - **Download del modello JSON**: usare questa opzione per scaricare e aggiornare il modello in qualsiasi editor esterno. Prestare attenzione con gli editor di testo che usano le **virgolette inglesi**, perché potrebbero creare codice JSON non valido.

    Dopo aver immesso i valori necessari per la configurazione, rimuovere tutte le impostazioni contenenti `"STRING_VALUE"` o `STRING_VALUE`.

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="Esempio di uso del flusso JSON - Modifica JSON.":::

5. Selezionare **Avanti**.
6. In **Assegnazioni** selezionare i gruppi a cui assegnare i criteri di configurazione app VPN.

    Selezionare **Avanti**.

7. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea** le modifiche vengono salvate e i criteri vengono distribuiti ai gruppi. I criteri vengono visualizzati anche nell'elenco dei criteri di configurazione app.

#### <a name="json-example-for-f5-access-vpn"></a>Esempio JSON per VPN F5 Access

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>Informazioni aggiuntive

- [Aggiungere criteri di configurazione delle app per i dispositivi Android gestiti](app-configuration-policies-use-android.md)
- [Impostazioni del dispositivo Android Enterprise per la configurazione della rete privata virtuale (VPN) in Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Passaggi successivi

- [Creare profili VPN per la connessione ai server VPN in Intune](../configuration/vpn-settings-configure.md)
