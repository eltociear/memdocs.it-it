---
title: Registrare automaticamente i dispositivi Android usando Knox Mobile Enrollment di Samsung
titleSuffix: Microsoft Intune
description: Informazioni su come registrare i dispositivi Android usando Samsung Knox Mobile Enrollment
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: ''
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 30df0f9e-6e9e-4d75-a722-3819e33d480d
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d7ec41361571647cc417dc34ad29522d50477eb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339566"
---
# <a name="automatically-enroll-android-devices-by-using-samsungs-knox-mobile-enrollment"></a>Registrare automaticamente i dispositivi Android usando Knox Mobile Enrollment di Samsung

Questo argomento consente di configurare Intune per registrare i dispositivi Android supportati usando Samsung Knox Mobile Enrollment (KME). Usando Intune con Samsung KME, è possibile registrare un numero elevato di dispositivi Android aziendali quando gli utenti finali attivano i dispositivi per la prima volta e si connettono a una rete WiFi o cellulare. I dispositivi possono anche essere registrati usando Bluetooth o NFC quando si usa l'app Knox Deployment.

Per abilitare la registrazione di Intune con Samsung KME, si usano entrambi i portali di Intune e di Samsung Knox in quest'ordine:

1. Nel portale di Knox:
    1. [Creare un profilo MDM](#create-mdm-profile)
    2. [Aggiungere dispositivi](#add-devices)
    3. [Assegnare un profilo MDM ai dispositivi](#assign-an-mdm-profile-to-devices)
2. Nel portale di Knox [configurare l'accesso degli utenti finali](#configure-how-end-users-sign-in).
3. [Distribuire i dispositivi](#distribute-devices).


Un elenco di identificatori di dispositivo (numeri di serie e IMEI) viene automaticamente aggiunto al portale di Knox quando si acquistano dispositivi da rivenditori autorizzati che partecipano a Knox Deployment Program.


## <a name="prerequisites"></a>Prerequisiti

Per la registrazione in Intune con KME, è prima necessario registrare la società nel portale di Samsung Knox seguendo questa procedura:
1. [Verificare che KME sia disponibile nel paese o nell'area geografica di residenza](https://www.samsungknox.com/en/solutions/it-solutions/knox-configure/available-countries): KME è disponibile in più di 55 paesi/aree geografiche. Assicurarsi che il paese/l'area geografica di distribuzione sia supportato.

2. [Dispositivi supportati](https://www.samsungknox.com/en/knox-platform/supported-devices/2.4+): KME è disponibile in tutti i dispositivi Samsung con almeno Knox 2.4 per la registrazione di Android e almeno Knox 2.8 per la registrazione di Android Enterprise.

3. [Requisiti di rete](https://docs.samsungknox.com/KME-Getting-Started/Content/firewall_exceptions.htm): verificare che le regole di accesso alla rete e del firewall necessarie siano consentite nella rete.

4. [Registrazione di un account Samsung](https://www2.samsungknox.com/en/user/register): è necessario un account Samsung per registrare e abilitare KME e per gestire tutti i diritti Knox Enterprise in un'unica posizione.

5. Verifica della registrazione: dopo che il profilo è stato completato e inviato, Samsung esegue una verifica della richiesta e la approva immediatamente o ne imposta lo stato di verifica in sospeso che richiede ulteriori attività di completamento. Dopo l'approvazione dell'account, è possibile continuare con i passaggi successivi.

## <a name="create-mdm-profile"></a>Creare il profilo MDM

Quando la società è registrata correttamente, è possibile creare il profilo MDM per Microsoft Intune nel portale di Knox usando le informazioni seguenti. È possibile creare profili MDM sia per Android che per Android Enterprise nel portale di Knox.
- Per creare un profilo MDM per Android, selezionare **Device Admin** (Amministratore del dispositivo) come tipo di profilo nel portale di Knox. 
- Per creare un profilo MDM per Android Enterprise, selezionare **Device Owner** (Proprietario dispositivo) come tipo di profilo nel portale di Knox.  

### <a name="for-android"></a>Per Android

| Campi del profilo MDM| Necessaria? | Valori | 
|-------------------|-----------|-------| 
|Nome profilo       | Sì       |Immettere il nome profilo preferito. |
|Descrizione        | No        |Immettere la descrizione del profilo. |
|MDM Information (Informazioni MDM)     | Sì        |Scegliere **Server URI not required for my MDM** (URI del server non obbligatorio per il profilo MDM).| 
|MDM Agent APK (APK agente MDM)      | Sì       |https://aka.ms/intune_kme_deviceowner| 
|Custom JSON (JSON personalizzato)        | Sì*        |{"com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "Immettere la stringa del token di registrazione di Intune"}. Informazioni su come creare un token di registrazione per [dispositivi dedicati](android-kiosk-enroll.md) e [dispositivi completamente gestiti](android-fully-managed-enroll.md). |
|Skip Setup wizard (Ignora configurazione guidata)  | No        |Scegliere questa opzione per ignorare i prompt della procedura di configurazione dei dispositivi standard per l'utente finale.|
|Allow End User to Cancel Enrollment (Consenti all'utente finale di annullare la registrazione) | No | Scegliere questa opzione per consentire agli utenti di annullare KME.|
| Privacy Policy, EULAs and Terms of Service (Informativa sulla privacy, condizioni di licenza e condizioni d'uso) | No | Lasciarlo vuoto. |
| Support contact details (Dettagli contatto supporto) | Sì | Scegliere Edit (Modifica) per aggiornare i dettagli del contatto |
|Associate a Knox license with this profile (Associa una licenza Knox a questo profilo) | No | Lasciare questa opzione deselezionata. Per la registrazione in Intune con KME non è necessaria una licenza Knox.|

\* Questo campo non è obbligatorio per completare la creazione del profilo nel portale di Knox. È tuttavia necessario compilare questo campo in modo che il profilo possa registrare correttamente il dispositivo in Intune.

### <a name="for-android-enterprise"></a>Per Android Enterprise

Per indicazioni dettagliate, vedere le istruzioni per la [creazione del profilo Samsung](https://docs.samsungknox.com/KME-Getting-Started/Content/create-profiles.htm).

| Campi del profilo MDM| Necessaria? | Valori |
|-------------------|-----------|-------|
|Nome profilo       | Sì       |Immettere il nome profilo preferito.|
|Descrizione        | No        |Immettere la descrizione del profilo.|
|Pick your MDM (Seleziona il profilo MDM) | Sì | Scegliere Microsoft Intune. |
|MDM Agent APK (APK agente MDM)      | Sì       |https://aka.ms/intune_kme|
|MDM Server URI (URI server MDM)     | No        |Lasciarlo vuoto.|
|Custom JSON Data (Dati JSON personalizzati)        | No        |Lasciarlo vuoto.|
|Dual DAR (DAR doppio) | No | Lasciarlo vuoto.|
|QR code for enrollment (Codice a matrice per la registrazione) | No | È possibile aggiungere un codice a matrice per velocizzare la registrazione.|
|System applications (Applicazioni di sistema) | Sì | Scegliere l'opzione **Leave all system apps enabled** (Lascia tutte le app di sistema abilitate) per assicurarsi che tutte le app siano abilitate e disponibili per il profilo. Se questa opzione non è selezionata, viene visualizzato solo un set molto limitato di app di sistema nella barra delle app del dispositivo. Alcune app, ad esempio l'app di posta elettronica, rimangono nascoste. |
|Privacy Policy, EULAs and Terms of Service (Informativa sulla privacy, condizioni di licenza e condizioni d'uso) | No | Lasciarlo vuoto.|
|Nome società | Sì | Questo nome verrà visualizzato durante la registrazione del dispositivo. |

## <a name="add-devices"></a>Aggiungere dispositivi

Per assegnare i profili MDM ai dispositivi, i dispositivi Samsung Knox supportati devono essere aggiunti al portale di Knox usando uno dei metodi seguenti:
- **Uso di rivenditori approvati da Samsung:** usare questo metodo se si acquistano i dispositivi da uno dei rivenditori approvati da Samsung. I rivenditori possono caricare automaticamente i dispositivi una volta approvati. [Per informazioni su come aggiungere i rivenditori, vedere il manuale dell'utente sulla registrazione di Samsung Knox](https://docs.samsungknox.com/KME-Getting-Started/Content/Register_resellers.htm).

- **Uso dell'app Knox Deployment:** usare questo metodo se è necessario registrare dispositivi esistenti con KME. È possibile usare Bluetooth o NFC per aggiungere i dispositivi al portale di Knox con questo metodo. [Per informazioni sull'uso dell'app Knox Deployment, vedere il manuale dell'utente sulla registrazione di Samsung Knox](https://docs.samsungknox.com/KME-Getting-Started/Content/add-device-info.htm).

## <a name="assign-an-mdm-profile-to-devices"></a>Assegnare un profilo MDM ai dispositivi
È necessario assegnare un profilo MDM ai dispositivi aggiunti nel portale di Knox per poterli registrare. [Per informazioni sulla configurazione dei dispositivi, vedere il manuale dell'utente sulla registrazione di Samsung Knox](https://docs.samsungknox.com/KME-Getting-Started/Content/configure-devices.htm).

## <a name="configure-how-end-users-sign-in"></a>Configurare la modalità di accesso degli utenti finali

Per i dispositivi registrati in Intune con KME per Android, è possibile configurare la modalità di accesso degli utenti finali come segue:

- **Senza associazione del nome utente:** nel portale di Knox, in **Device details** (Dettagli dispositivo), lasciare vuoti i campi **User ID** (ID utente) e **Password** per i dispositivi aggiunti. Con questa opzione l'utente finale dovrà immettere sia il nome utente che la password durante la registrazione in Intune.

- **Con associazione del nome utente:** nel portale di Knox, in **Device details** (Dettagli dispositivo), immettere un **ID utente** (ad esempio un nome utente per l'utente assegnato o un account [Manager di registrazione dispositivi](device-enrollment-manager-enroll.md)) per i dispositivi aggiunti. Con questa opzione il nome utente verrà prepopolato e l'utente finale dovrà immettere una password durante la registrazione in Intune.

> [!NOTE]
>
>L'associazione dell'utente si applica solo alla registrazione di tipo amministratore di dispositivi Android. Quando l'associazione utente è definita, solo gli utenti associati possono registrare il dispositivo con KME. Ciò vale anche dopo un ripristino delle impostazioni predefinite del dispositivo. Quando non sono definite associazioni utente nel portale di Knox, qualsiasi utente con una licenza di Intune valida può registrare il dispositivo con KME.
>Per i dispositivi Android Enterprise completamente gestiti, anche se definita, l'associazione dell'utente non verrà passata al dispositivo o non collegherà il dispositivo all'utente.
>

## <a name="distribute-devices"></a>Distribuire i dispositivi

Dopo avere creato e assegnato un profilo MDM, avere associato un nome utente e identificato i dispositivi come di proprietà dell'azienda in Intune, è possibile distribuire i dispositivi agli utenti.

Serve ancora assistenza? Vedere il [manuale dell'utente completo di KME](https://docs.samsungknox.com/KME-Getting-Started/Content/get-started.htm).

## <a name="frequently-asked-questions"></a>Domande frequenti

- **Supporto proprietario del dispositivo:**  - **Supporto proprietario del dispositivo:** Intune supporta la registrazione di dispositivi dedicati e completamente gestiti tramite il portale di KME. Altre modalità proprietario del dispositivo di Android Enterprise saranno supportate man mano che diventano disponibili in Intune.

- **Nessun supporto del profilo di lavoro:** KME è un metodo di registrazione dei dispositivi aziendali e la registrazione dei dispositivi nel profilo di lavoro di Android assicura che i dati di lavoro restino separati da quelli personali nei dispositivi personali. Per questo motivo, la registrazione dei dispositivi nel profilo di lavoro con KME non è uno scenario supportato in Intune.

- **Ripristino delle impostazioni predefinite per la registrazione in Android Enterprise:** in caso di reimpiego di dispositivi che sono già stati configurati, è necessario ripristinare le impostazioni predefinite dei dispositivi quando si effettua la registrazione in Android Enterprise.

- **Aggiornamenti tramite account Google Play:** l'account Google Play non è necessario per registrare il dispositivo in Microsoft Intune, ma per le registrazioni di tipo amministratore di dispositivi Android i futuri aggiornamenti dell'app Portale aziendale di Intune potrebbero richiedere un account Google Play nel dispositivo. Per la registrazione nel proprietario del dispositivo Google non è obbligatorio usare un account Google Play.

- **Il campo "Password" viene ignorato:** se il campo **password** viene popolato in **Device details** (Dettagli dispositivo) nel portale di Knox, viene ignorato dall'app Portale aziendale Intune durante la registrazione in Android. L'utente finale deve immettere una password nel dispositivo per completare la registrazione del dispositivo.


## <a name="getting-support"></a>Richiesta di assistenza
Sono disponibili altre informazioni su come [ottenere assistenza per Samsung KME](https://docs.samsungknox.com/KME-Getting-Started/Content/to-get-kme-support.htm).


