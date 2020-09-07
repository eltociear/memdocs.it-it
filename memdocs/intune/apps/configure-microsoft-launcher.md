---
title: Configurare Microsoft Launcher per Android Enterprise con Intune
titleSuffix: ''
description: Usare i criteri di configurazione di Intune con Microsoft Launcher.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d9fe4c3a48cbf333fffd83d013b6a2d5fcf4ed9
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281133"
---
# <a name="configure-microsoft-launcher"></a>Configurare Microsoft Launcher

Microsoft Launcher è un'applicazione Android che consente agli utenti di personalizzare il telefono, rimanere organizzati in viaggio e trasferire il lavoro dal telefono al proprio PC. 

Nei dispositivi Android Enterprise completamente gestiti Microsoft Launcher consente agli amministratori IT aziendali di personalizzare le schermate iniziali dei dispositivi gestiti, selezionando lo sfondo, le app e le posizioni delle icone. In questo modo è possibile standardizzare l'aspetto di tutti i dispositivi Android gestiti se sono in uso vari dispositivi OEM e diverse versioni di sistema. 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>Come configurare l'app Microsoft Launcher 

Dopo che l'applicazione Microsoft Launcher è stata [aggiunta a Intune](../apps/apps-add.md), passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selezionare **App** > **Criteri di configurazione dell'app**. Aggiungere un criterio di configurazione per i **Dispositivi gestiti** che eseguono **Android** e scegliere **Microsoft Launcher** come app associata. Fare clic su **Impostazioni di configurazione** per configurare le varie impostazioni di Microsoft Launcher disponibili. 

## <a name="choosing-a-configuration-settings-format"></a>Scelta di un formato delle impostazioni di configurazione 

È possibile usare due metodi per definire le impostazioni di configurazione per Microsoft Launcher: 

- **Progettazione configurazione** consente di configurare le impostazioni con un'interfaccia utente intuitiva tramite la quale è possibile attivare o disattivare le funzionalità e impostare i valori. Con questo metodo, alcune chiavi di configurazione sono disabilitate con un tipo di valore BundleArray. Queste chiavi di configurazione possono essere configurate solo immettendo dati JSON. 

- **Dati JSON** consente di definire tutte le chiavi di configurazione possibili usando uno script JSON. 

Se si aggiungono proprietà con **Progettazione configurazione**, è possibile convertirle automaticamente in JSON scegliendo **Immettere i dati JSON** dal menu a discesa **Formato delle impostazioni di configurazione** come illustrato di seguito.

   ![Formato delle impostazioni di configurazione - Usa progettazione configurazione](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > Dopo aver configurato le proprietà tramite Progettazione configurazione, anche i dati JSON verranno aggiornati in modo da riflettere solo queste proprietà. Per aggiungere ulteriori chiavi di configurazione nei dati JSON, usare l'[esempio di script JSON](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example) per copiare le righe necessarie per ogni chiave di configurazione. 

Quando si modificano criteri di configurazione delle app creati in precedenza, se sono state configurate proprietà complesse, il processo di modifica visualizza l'editor di dati JSON. Tutte le impostazioni configurate in precedenza verranno mantenute e sarà possibile passare alla finestra di progettazione della configurazione per modificare le impostazioni supportate.

## <a name="using-configuration-designer"></a>Uso di Progettazione configurazione

Progettazione configurazione consente di selezionare impostazioni prepopolate e i rispettivi valori associati.

   ![Formato delle impostazioni di configurazione - Immettere i dati JSON](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

La tabella seguente contiene un elenco delle chiavi di configurazione di Microsoft Launcher disponibili, con i tipi di valore, i valori predefiniti e le descrizioni. La descrizione indica il comportamento previsto del dispositivo in base ai valori selezionati. Le chiavi di configurazione disabilitate in Progettazione configurazione non sono elencate nella tabella.

|    Chiave Configuration    |    Tipo valore    |    Valore predefinito    |    Descrizione     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Enrollment Type (Tipo di registrazione)    |    Stringa     |    Predefinito    |    Consente di impostare il tipo di registrazione a cui applicare i criteri. Attualmente il valore **predefinito** si riferisce a **CorporateOwnedBuisnessOnly**. Al momento non sono supportati altri tipi di registrazione.        Nome chiave JSON: management_mode_key        |
|    Home Screen App Order User Change   Allowed (Consentita modifica dell'ordine delle app della schermata iniziale da parte dell'utente)    |    Boolean    |    True    |    Consente di specificare se l'impostazione **Home Screen App Order** (Ordine app schermata iniziale) può essere modificata dall'utente finale.<ul><li>Se è impostata su **True**, l'ordine delle app definito nei criteri verrà applicato solo per la distribuzione iniziale. Successivamente, i criteri non verranno applicati per rispettare le eventuali modifiche apportate dall'utente.</li><li>Se è impostata su **False**, l'ordine dell'app verrà applicato a ogni sincronizzazione.</li></ul><br>**Nota:** L'ordine delle app della schermata iniziale può essere configurato solo nell'editor JSON.<br><br>Nome chiave JSON:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    Set Grid Size (Imposta dimensioni griglia)    |    Stringa    |    Auto    |    Consente di impostare le dimensioni della griglia per le app da posizionare nella schermata iniziale. È possibile specificare il numero di righe e colonne di app per definire le dimensioni della griglia nel formato `columns;rows`. Se si definiscono le dimensioni della griglia, il numero di righe impostate corrisponde al numero massimo di app che verranno visualizzate in una riga e il numero di colonne impostate al numero massimo di app che verranno visualizzate in una colonna.<br><br>        Nome chiave JSON:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Set Device Wallpaper (Imposta sfondo dispositivo)    |    Stringa    |    Null    |    Consente di impostare uno sfondo a scelta immettendo l'URL dell'immagine da usare come sfondo.<br><br>Nome chiave JSON:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Set Device Wallpaper User Change   Allowed (Consentita modifica dello sfondo del dispositivo da parte dell'utente)    |    Bool    |    True    |    Consente di specificare se l'impostazione Set Device Wallpaper (Imposta sfondo dispositivo) può essere modificata dall'utente finale.<ul><li>Se è impostata su **True**, lo sfondo indicato nei criteri verrà applicato solo per la distribuzione iniziale. Successivamente, i criteri non verranno applicati per rispettare le eventuali modifiche apportate dall'utente.</li><li>Se è impostata su **False**, lo sfondo verrà applicato a ogni sincronizzazione.</li></ul><br>Nome chiave JSON:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Feed Enable (Abilitazione feed)    |    Boolean    |    True    |    Consente di abilitare il feed di Microsoft Launcher nel dispositivo quando l'utente scorre a destra sulla schermata iniziale.<ul><li>Se è impostata su **True**, il feed viene abilitato.</li><li>Se è impostata su **False**, il feed viene disattivato.</li></ul><br>Nome chiave JSON:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Feed Enable User Change Allowed (Consentita modifica dell'abilitazione del feed da parte dell'utente)    |    Boolean    |    True    |     Consente di specificare se l'impostazione **Feed Enable** (Abilitazione feed) può essere modificata dall'utente finale.<ul><li>Se è impostata su **True**, il feed verrà applicato solo per la distribuzione iniziale. Successivamente, i criteri non verranno applicati per rispettare le eventuali modifiche apportate dall'utente.</li><li>Se è impostata su **False**, il feed app verrà applicato a ogni sincronizzazione.</li></ul><br>Nome chiave JSON:`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    Search Bar Placement (Posizione barra di ricerca)   |    Stringa    |    Ultimo    |  Consente di specificare la **posizione della barra di ricerca** nella schermata iniziale. <ul><li>Con l'impostazione **Bottom** (In basso) la barra di ricerca verrà posizionata nella parte inferiore della schermata iniziale.</li><li>Con l'impostazione **Top** (In alto) la barra di ricerca verrà posizionata nella parte superiore della schermata iniziale.</li><li>Con l'impostazione **Hidden** (Nascosta), la barra di ricerca verrà rimossa dalla schermata iniziale.</li></ul><br>Nome chiave JSON:<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    Search Bar Placement User Change Allowed (Utente autorizzato a modificare la posizione della barra di ricerca)   |    Bool    |    True    |  Consente di specificare se l'impostazione **Search Bar Placement** (Posizione barra di ricerca) può essere modificata dall'utente finale. <ul><li>Se è impostata su **True**, la posizione della barra di ricerca verrà applicata solo per la distribuzione iniziale. Successivamente, i criteri non verranno applicati per rispettare le eventuali modifiche apportate dall'utente.</li><li>Se è impostata su **false**, la posizione della barra di ricerca verrà applicata a ogni sincronizzazione.</li></ul><br>Nome chiave JSON:<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`<p>**NOTA:** per Microsoft Launcher versione 6.2 e successive, questa impostazione non verrà più applicata. Di conseguenza, l'impostazione di questo valore su `True` non avrà alcun effetto. Gli utenti finali non saranno in grado di personalizzare il posizionamento della barra di ricerca nel dispositivo.    |
|    Dock Mode (Modalità di ancoraggio)  |    Stringa    |    Mostra    | Consente di abilitare l'ancoraggio nel dispositivo quando l'utente scorre a destra sulla schermata iniziale.<ul><li>Con l'impostazione **Show** (Mostra) l'ancoraggio sarà abilitato.</li><li>Con l'impostazione **Hidden** (Nascosto) l'ancoraggio verrà nascosto dalla schermata iniziale, ma l'utente potrà visualizzarlo quando necessario.</li><li>Con l'impostazione **Disabled** (Disabilitato) l'ancoraggio sarà disabilitato.</li></ul><br>Nome chiave JSON:<br>`com.microsoft.launcher.Dock.Mode`    |
|   Dock Mode User Change Allowed (Utente autorizzato a modificare la modalità di ancoraggio)   |    Stringa    |    True    |  Consente di specificare se l'impostazione Dock Mode (Modalità di ancoraggio) può essere modificata dall'utente finale.<ul><li>Se è impostata su **True**, l'impostazione della modalità di ancoraggio verrà applicata solo per la distribuzione iniziale. Successivamente, i criteri non verranno applicati per rispettare le eventuali modifiche apportate dall'utente.</li><li>Se è impostata su **False**, l'impostazione della modalità di ancoraggio verrà applicata a ogni sincronizzazione.</li></ul><br>Nome chiave JSON:<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>Immettere dati JSON

Immettere dati JSON per configurare tutte le impostazioni disponibili per Microsoft Launcher, oltre alle impostazioni disabilitate in **Progettazione configurazione**, come illustrato di seguito.

   ![Progettazione configurazione - Dati JSON](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

In aggiunta all'elenco di impostazioni configurabili riportato nella tabella Progettazione configurazione precedente, la tabella seguente include le chiavi di configurazione che è possibile configurare solo usando i dati JSON.

|    Chiave Configuration    |    Tipo valore    |    Valore predefinito    |    Descrizione     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Set Allow-Listed Applications (Imposta applicazioni dell'elenco elementi consentiti)<br>Chiave JSON:`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | Vedere: [Impostare le applicazioni dell'elenco degli elementi consentiti](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    Consente di definire il set di app visibili nella schermata iniziale tra le app installate nel dispositivo. Per definire le app, immettere il nome del pacchetto delle app da rendere visibili, ad esempio `com.android.settings` rende le impostazioni accessibili nella schermata iniziale. Le app che si aggiungono all'elenco degli elementi consentiti in questa sezione devono essere già installate nel dispositivo perché siano visibili nella schermata iniziale.<p>Proprietà:<ul><li>**Pacchetto:** Nome del pacchetto dell'applicazione</li><li>**Classe:** Attività dell'applicazione, che è specifica per una determinata pagina dell'app. Se questo valore è vuoto, viene usata la pagina predefinita dell'app.</li></ul>      |
|    Home Screen App Order (Ordine app schermata iniziale)<br>Chiave JSON: `com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    Vedere: [Ordine delle app nella schermata iniziale](configure-microsoft-launcher.md#home-screen-app-order)      |    Consente di specificare l'ordine delle app nella schermata iniziale.<p>Proprietà:<br><ul><li>**Tipo:** se si vogliono specificare le posizioni delle app, l'unico tipo supportato è `application`. Se si vogliono specificare le posizioni dei collegamenti Web, il tipo è `weblink`.</li><li>**Posizione:** specifica lo slot dell'icona dell'applicazione nella schermata iniziale. Inizia dalla posizione 1 in alto a sinistra e va da sinistra a destra, dall'alto verso il basso.</li><li>**Pacchetto:** nome del pacchetto dell'applicazione usato per specificare l'ordine delle app.</li><li>**Classe:** un'attività dell'applicazione, specifica per una determinata pagina dell'app. Se questo valore è vuoto, viene usata la pagina predefinita dell'app. Questa proprietà viene usata per l'app.</li><li>**Etichetta:** un'attività dell'applicazione, specifica per una determinata pagina dell'app. Se questo valore è vuoto, viene usata la pagina predefinita dell'app. Questa proprietà viene usata per l'app.</li><li>**Collegamento:** URL da avviare quando l'utente finale fa clic sull'icona del collegamento Web. Questa proprietà viene usata per il collegamento Web.</li></ul>    |
|    Set Pinned Web Links (Imposta collegamenti Web aggiunti)<br>Chiave JSON: `com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    Vedere: [Set Pinned Web Links](configure-microsoft-launcher.md#set-pinned-web-link) (Imposta collegamenti Web aggiunti)      |    Questa chiave consente di aggiungere il sito Web alla schermata iniziale come icona di avvio rapido. In questo modo è possibile assicurarsi che l'utente finale possa accedere in modo semplice e rapido ai siti web essenziali. È possibile modificare la posizione dell'icona di ogni collegamento Web nella configurazione "Home Screen App Order" (Ordine app schermata iniziale).<p>Proprietà:<br><ul><li>**Etichetta:** titolo del collegamento Web visualizzato nella schermata iniziale di Microsoft Launcher.</li><li>**Collegamento:** URL da avviare quando l'utente finale fa clic sull'icona del collegamento Web.</li></ul>    |


### <a name="set-allow-listed-applications"></a>Set allow-listed applications (Imposta applicazioni nell'elenco elementi consentiti)

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>Ordine delle app nella schermata iniziale

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>Set Pinned Web Link (Imposta collegamento Web aggiunto)

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Esempio di configurazione di Microsoft Launcher

Di seguito è riportato un esempio di script JSON con tutte le chiavi di configurazione disponibili incluse:

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueString": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sui dispositivi Android Enterprise completamente gestiti, vedere [Configurare la registrazione in Intune per dispositivi Android Enterprise completamente gestiti](../enrollment/android-fully-managed-enroll.md).
