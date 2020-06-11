---
title: Configurare una VPN per i dispositivi Android Enterprise
titleSuffix: Microsoft Intune
description: Usare un criterio di protezione delle app per configurare una VPN per i dispositivi Android Enterprise.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347418"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>Configurare una VPN per i dispositivi Android Enterprise

Questo argomento descrive come creare un criterio di configurazione delle app, che può essere distribuito insieme a un client VPN su dispositivi Android Enterprise. Questa configurazione consentirà al traffico di rete per le applicazioni scelte di accedere alle risorse aziendali.

> [!NOTE]
> La piattaforma Android attualmente non supporta l'attivazione automatica di una connessione client VPN quando viene aperta una delle applicazioni scelte. La connessione VPN deve essere prima avviata manualmente oppure è possibile usare una [VPN Always On](../configuration/vpn-settings-android-enterprise.md).

I prerequisiti per la creazione di un criterio di configurazione per accedere correttamente a una VPN includono la capacità del client VPN scelto di supportare i profili di configurazione delle applicazioni gestite. Attualmente, i client VPN che supportano i criteri di configurazione delle app di Intune includono:
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Palo Alto Global Connect
- Pulse Secure
- SonicWall Mobile Connect

Se il metodo per l'accesso con autenticazione all'endpoint VPN richiede l'uso di certificati client, è necessario creare i profili certificato in anticipo per popolare i valori richiesti per i criteri di configurazione delle app.

> [!NOTE]
> Benché gli scenari dei profili di lavoro di Android Enterprise supportino sia i certificati SCEP che PKCS, gli scenari dei proprietari di dispositivi Android Enterprise supportano attualmente solo i certificati SCEP. 

Il flusso di base per la creazione e il test del profilo VPN per app prevede i passaggi seguenti:
1.  Scegliere l'applicazione client VPN appropriata per l'infrastruttura.
2.  Identificare gli ID pacchetto dell'applicazione delle app di produttività da usare con la connessione VPN.
3.  Distribuire eventuali profili certificato richiesti per soddisfare i requisiti di autenticazione della connessione VPN. Assicurarsi di verificare la corretta distribuzione.
4.  Distribuire l'applicazione client VPN.
5.  Preparare il profilo VPN basato sulla configurazione dell'app usando le informazioni raccolte durante i passaggi precedenti.
6.  Distribuire il profilo VPN appena creato.
7.  Verificare che l'app client VPN si connetta correttamente all'infrastruttura del server VPN.
8.  Verificare che il traffico proveniente dalle app di produttività scelte transiti correttamente attraverso la VPN quando è attiva.

## <a name="get-the-app-package-id"></a>Ottenere l'ID pacchetto dell'app

Identificare l'ID pacchetto per ogni applicazione a cui si vuole concedere l'accesso alla VPN. Per le applicazioni disponibili pubblicamente, prendere in considerazione la possibilità di ottenere gli ID pacchetto per ognuna delle applicazioni in Google Play Store. L'URL visualizzato per ogni applicazione include l'ID pacchetto. Ad esempio, l'ID pacchetto per la versione Android del browser Microsoft Edge è `com.microsoft.emmx`. L'ID pacchetto è incluso come parte dell'URL.

![Esempio di ricerca dell'ID pacchetto dell'app.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

Per le app line-of-business, chiedere al fornitore o al team di sviluppo dell'applicazione di fornire l'ID pacchetto pertinente.

## <a name="certificates"></a>Certificati

In questo argomento si presuppone che la connessione VPN userà l'autenticazione basata su certificati e che siano stati distribuiti correttamente tutti i certificati nella catena necessari per la riuscita dell'autenticazione client. In genere, si tratta del certificato client, dei certificati intermedi e del certificato radice.
Per altre informazioni sulla distribuzione di certificati per Android Enterprise, iniziare rivedendo l'argomento [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).

Dopo aver distribuito il profilo certificato di autenticazione client, sono necessari alcuni dettagli sul profilo per creare i criteri di configurazione dell'app VPN.
Se non si ha familiarità con la creazione dei profili di configurazione delle app, vedere l'argomento [Aggiungere criteri di configurazione delle app per i dispositivi Android gestiti](../apps/app-configuration-policies-use-android.md).
 

## <a name="build-the-vpn-profile"></a>Creare il profilo VPN

Esistono due modi per creare i criteri di configurazione dell'app per l'app VPN. È possibile usare la **finestra di progettazione della configurazione** o l'opzione **Dati JSON**. L'opzione **Dati JSON** è necessaria quando non sono disponibili tutte le impostazioni VPN richieste nel metodo basato sulla **finestra di progettazione della configurazione**. Consultare il fornitore della VPN se si appura che è richiesta l'opzione JSON per il supporto. In questo argomento verranno illustrati esempi di entrambi i metodi. In entrambi i metodi basati sui **dati JSON** e sulla **finestra di progettazione della configurazione** è possibile incorporare correttamente l'autenticazione basata su certificati. Quando si usa il metodo basato sui **dati JSON**, è possibile iniziare usando la **finestra di progettazione della configurazione** per estrarre i valori del profilo necessari.

> [!NOTE]
> Benché molti dei parametri di configurazione del client VPN siano simili, ogni app dispone di chiavi e opzioni univoche. In caso di dubbi, consultare il fornitore della VPN. 

## <a name="use-the-configuration-designer-flow"></a>Usare il flusso Progettazione configurazione

1.  Per iniziare, aggiungere un nuovo criterio di configurazione dell'app per **Dispositivi gestiti**.
2.  Immettere un nome appropriato.
3.  Selezionare **Android Enterprise** come piattaforma.
4.  Selezionare **Solo profilo di lavoro** o **Solo proprietario del dispositivo** come tipo di profilo se è richiesta l'autenticazione basata su certificati. L'opzione **Profilo di lavoro e profilo di Proprietario del dispositivo** non è compatibile con l'autenticazione basata su certificati.
5.  Per l'app di destinazione, selezionare il client VPN distribuito. In questo esempio viene usato il client VPN Cisco AnyConnect distribuito in precedenza.

  ![Esempio di creazione di un criterio di configurazione dell'app - Informazioni di base.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. Nella pagina successiva usare l'elenco a discesa Impostazioni di configurazione e selezionare l'opzione **Usa progettazione configurazione**.

  ![Esempio di uso del flusso Progettazione configurazione - Impostazioni.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. Fare clic su **Aggiungi** per visualizzare l'elenco delle chiavi di configurazione.
8.  Selezionare tutte le chiavi di configurazione necessarie per la configurazione scelta. In questo esempio si usa un elenco minimo da impostare per una VPN AnyConnect, incluse l'autenticazione basata su certificati e la VPN per app.
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. Immettere i valori appropriati per le chiavi **Nome connessione**, **Host** e **Protocollo**.

  ![Esempio di uso del flusso Progettazione configurazione - Selezione delle chiavi di configurazione.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > I nomi di queste chiavi possono variare a seconda dell'applicazione client VPN per cui si crea il criterio.

10. Immettere gli ID pacchetto dell'applicazione raccolti in precedenza nella chiave **Per App VPN Allowed Apps** (App consentite VPN per app).

  ![Esempio di uso del flusso Progettazione configurazione - ID pacchetto dell'app.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. Nella chiave **KeyChain Certificate Alias** (Alias certificato KeyChain) (facoltativo) cambiare il **Tipo di valore** da **stringa** a **certificato**. In questo modo sarà possibile scegliere il profilo certificato client corretto da usare con l'autenticazione VPN.

  ![Esempio di uso del flusso Progettazione configurazione - Aggiornamento dell'alias certificato KeyChain.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. Nella pagina successiva scegliere eventuali tag di ambito appropriati.
13. Nella pagina successiva immettere i gruppi appropriati a cui si vogliono distribuire i criteri di configurazione dell'app.
14. Selezionare **Crea** per completare la creazione e la distribuzione dei criteri.

  ![Esempio di uso del flusso Progettazione configurazione - Revisione.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>Usare il flusso JSON

Creare un profilo temporaneo:
1.  Per iniziare, aggiungere un nuovo criterio di configurazione dell'app per **Dispositivi gestiti**.
2.  Immettere un nome appropriato (l'uso di questo profilo è temporaneo perché NON verrà salvato).
3.  Selezionare **Android Enterprise** come piattaforma.
4.  Per l'app di destinazione, selezionare il client VPN distribuito.
5.  Selezionare **Solo profilo di lavoro** o **Solo proprietario del dispositivo** come tipo di profilo se è richiesta l'autenticazione basata su certificati. L'opzione **Profilo di lavoro e profilo di Proprietario del dispositivo** non è compatibile con l'autenticazione basata su certificati.

  ![Esempio di uso del flusso JSON - Informazioni di base.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  Nella pagina successiva usare l'elenco a discesa **Impostazioni di configurazione** e selezionare l'opzione **Usa progettazione configurazione**.

  ![Esempio di uso del flusso JSON - Formato delle impostazioni di configurazione.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  Fare clic su **Aggiungi** per visualizzare l'elenco delle chiavi di configurazione.
8.  Selezionare una delle chiavi con un **Tipo di valore** **stringa** e fare clic su **OK**.

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  Modificare ora il **Tipo di valore** da **stringa** a **certificato**. In questo modo sarà possibile scegliere il profilo certificato client corretto da usare con l'autenticazione VPN.

  ![Esempio di uso del flusso JSON - Nome connessione.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. Modificare immediatamente il **Tipo di valore** di nuovo in **stringa**. Si noti che il **Valore di configurazione** viene modificato in un token di formato `{{cert:GUID}}`.
11. Selezionare e copiare la rappresentazione del token del certificato in una posizione alternativa, ad esempio un editor di testo.

  ![Esempio di uso del flusso JSON - Valore di configurazione.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. Rimuovere il profilo da creare: l'unico scopo dei passaggi precedenti è stato determinare il token del certificato.

### <a name="create-the-vpn-profile"></a>Creare il profilo VPN

1.  Per iniziare, aggiungere un nuovo profilo di configurazione dell'applicazione per **Dispositivi gestiti**.
2.  Immettere un nome appropriato.
3.  Selezionare **Android Enterprise** come piattaforma.
4.  Per l'app di destinazione, selezionare il client VPN distribuito.
5.  Selezionare **Solo profilo di lavoro** o **Solo proprietario del dispositivo** come tipo di profilo se è richiesta l'autenticazione basata su certificati. L'opzione **Profilo di lavoro e profilo di Proprietario del dispositivo** non è compatibile con l'autenticazione basata su certificati.
6.  Usare l'elenco a discesa **Impostazioni di configurazione** e selezionare l'opzione **Immettere i dati JSON**.
7.  È possibile modificare direttamente il codice JSON o, se si preferisce, usare il pulsante **Download del modello JSON** per scaricare e modificare il modello in un editor esterno a propria scelta. Prestare attenzione agli editor di testo che includono l'opzione per l'uso delle **virgolette curve**, perché la loro inclusione renderebbe il codice JSON non valido.

  ![Esempio di uso del flusso JSON - Modifica JSON.](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  Indipendentemente dal metodo usato, dopo aver popolato i valori richiesti per la configurazione desiderata, è necessario rimuovere tutte le impostazioni rimanenti con un valore "STRING_VALUE" o STRING_VALUE nell'intero codice JSON.

#### <a name="example-json-for-f5-access-vpn"></a>Esempio di codice JSON per la VPN F5 Access

Di seguito è riportato un esempio di dati JSON per la VPN F5 Access.

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

## <a name="summary"></a>Riepilogo

L'uso di un criterio di configurazione delle app per i dispositivi registrati Android Enterprise consente di sfruttare il comportamento della VPN per app, nonostante l'assenza del supporto diretto nella piattaforma. 

## <a name="additional-information"></a>Informazioni aggiuntive

Per altre informazioni, vedere gli argomenti seguenti:
- [Aggiungere criteri di configurazione delle app per i dispositivi Android gestiti](../apps/app-configuration-policies-use-android.md)
- [Impostazioni del dispositivo Android Enterprise per la configurazione della rete privata virtuale (VPN) in Intune](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>Passaggi successivi

- [Creare profili VPN per la connessione ai server VPN in Intune](../configuration/vpn-settings-configure.md)
