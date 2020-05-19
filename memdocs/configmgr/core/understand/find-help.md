---
title: Ottenere informazioni
titleSuffix: Configuration Manager
description: Trovare risorse per altre informazioni su Configuration Manager.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bae98a8df1d8b8ff843bd333083c4c6ad68848c
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343185"
---
# <a name="find-help-for-using-configuration-manager"></a>Reperire informazioni sull'uso di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo include le sezioni seguenti con diverse risorse per reperire informazioni sull'uso di Configuration Manager:  

- [Documentazione del prodotto](#bkmk_Info)  

- [Condivisione di commenti e suggerimenti sul prodotto](#product-feedback)  

- [Seguire il blog del team di Configuration Manager](#BKMK_ProductGroupBlog)  

- [Opzioni di supporto e risorse per la community](#BKMK_SupportOptions)  

Per informazioni sull'accessibilità, vedere [Funzionalità di accessibilità](accessibility-features.md).  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> Documentazione del prodotto  

Per accedere alla documentazione più recente del prodotto, iniziare dall'[indice](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Per suggerimenti sulle ricerche, l'invio di commenti e suggerimenti e altre informazioni sull'uso della documentazione del prodotto, vedere [Come usare la documentazione](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> Commenti e suggerimenti sul prodotto a partire dalla versione 1806

A partire da Configuration Manager versione 1806, è possibile inviare commenti e suggerimenti sul prodotto direttamente dalla console. Se è necessario allegare log, usare [Hub di Feedback](#BKMK_FeedbackHub). È possibile eseguire le operazioni seguenti: <!--1357542-->

- **Invia smile**: inviare commenti e suggerimenti su ciò che si è apprezzato.
- **Invia faccia imbronciata**: inviare commenti e suggerimenti su ciò che non si è apprezzato.
- **Invia un suggerimento**: consente di accedere al [sito Web UserVoice](https://configurationmanager.uservoice.com/) per condividere la propria opinione.

  ![Inviare commenti e suggerimenti in Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Inviare uno smile o una faccia imbronciata

Per inviare commenti e suggerimenti su elementi che si sono apprezzati, seguire queste istruzioni:

1. Nell'angolo superiore destro della console fare clic sullo smile.
2. Nel menu a discesa selezionare **Invia smile** o **Invia faccia imbronciata**.
3. Usare la casella di testo per spiegare cosa si è apprezzato o meno. 
4. Scegliere se si vuole condividere il proprio indirizzo di posta elettronica e uno screenshot.
5. Fare clic su **Invia commenti e suggerimenti**.
     - Se non è disponibile una connessione Internet, fare clic su **Salva** in basso. Per l'invio a Microsoft, seguire le istruzioni riportate nella sezione [Inviare in seguito commenti e suggerimenti salvati a tale scopo](#BKMK_NoInternet). 

![Modulo per l'invio di commenti e suggerimenti in Configuration Manager 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Messaggi di stato per l'invio di smile
<!--5891852-->
A partire da Configuration Manager 2002, quando si **invia uno smile** o si **invia una faccia imbronciata**, con l'invio del feedback viene creato un messaggio di stato. Questo miglioramento consente di registrare le informazioni seguenti:
- Quando sono stati inviati commenti e suggerimenti
- Chi ha inviato i commenti e suggerimenti
- L'ID dei commenti e suggerimenti
- Se l'invio di commenti e suggerimenti ha avuto esito positivo o negativo
   - 53900 per un invio riuscito.
   - 53901 per un invio non riuscito.

Visualizzare i messaggi di stato da **Monitoraggio** > **Stato del sistema** > **Query messaggi di stato**. Iniziare con la query **Tutti i messaggi di stato** e selezionare l'intervallo di tempo. Quando i messaggi si caricano, fare clic sul pulsante **Filtra messaggi** e filtrare per il messaggio con ID 53900 o 53901.

I messaggi di stato non vengono creati se si [inviano commenti e suggerimenti salvati per inviarli in seguito](find-help.md#BKMK_NoInternet).

[![Messaggio di stato per l'invio corretto di commenti e suggerimenti](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Inviare un suggerimento

Quando si usa **Invia un suggerimento**, si viene indirizzati a [UserVoice](https://configurationmanager.uservoice.com/), un sito Web di terze parti in cui è possibile condividere l'idea. Il team di prodotto di Configuration Manager usa i valori di stato di UserVoice seguenti:

- **Noted** (Annotato): la richiesta è appropriata ed è stata aggiunta al backlog.
- **Planned** (Pianificato): è stata avviata la scrittura del codice per questa funzionalità. Si prevede sarà disponibile in una versione di anteprima Tech nei prossimi mesi.
- **Started** (Avviato): la funzionalità è ora disponibile in un'anteprima Tech. È possibile esaminarla e inviare commenti e suggerimenti. Informare Microsoft se la funzionalità è corretta o meno. Inserire altri commenti e suggerimenti nella sezione dei commenti della richiesta originale perché altri utenti possano visualizzare e inviare commenti sulla funzionalità. Il feedback verrà letto e usato per migliorare la funzionalità.
- **Completed** (Completato): la prima versione della funzionalità è disponibile in una build di produzione. Questo stato non significa che la funzionalità è stata interamente completata e che non sarà sottoposta a miglioramenti. Significa invece che la prima versione della funzionalità è inclusa in una build di produzione e può essere usata in un ambiente reale. Viene contrassegnata come se fosse completata per i motivi seguenti:
  - È importante sapere che la funzionalità può essere usata in un ambiente di produzione.
  - I voti di UserVoice devono essere restituiti per poter essere usati per altri elementi.
  - È possibile archiviare nuove richieste di modifica di progettazione per questa funzionalità in modo tale che Microsoft sappia quale sarà il prossimo miglioramento più importante di questa funzionalità.

### <a name="information-sent-with-feedback"></a>Informazioni inviate con commenti e suggerimenti

Quando si usano **Invia smile** o **Invia faccia imbronciata**, vengono inviate le informazioni seguenti insieme ai commenti e suggerimenti:

- Informazioni sulla build del sistema operativo
- ID della gerarchia di Configuration Manager
- Informazioni sulla build del prodotto
- Informazioni sulla lingua
- Identificatore del dispositivo 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> Inviare in seguito commenti e suggerimenti salvati a tale scopo

1. Fare clic su **Salva** nella parte inferiore della finestra **Commenti e suggerimenti**. 
2. Salvare il file ZIP. Se il computer locale non ha accesso a Internet, copiare il file in un computer connesso a Internet. 
3. Se necessario, copiare la cartella UploadOfflineFeedback, disponibile in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - Per altre informazioni sulla cartella CD.Latest, vedere [Cartella CD.Latest](../servers/manage/the-cd.latest-folder.md)

4. In un computer connesso a Internet aprire il prompt dei comandi. 
5. Eseguire il comando seguente: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Facoltativamente, è possibile specificare i parametri seguenti:
        -  `-t, --timeout`: timeout in secondi per l'invio dei dati. 0 corrisponde a senza limiti. Il valore predefinito è 30.
        - `-s --silent`: nessuna registrazione nella console (non è combinabile con --verbose)
        - `-v, --verbose`: registrazione dettagliata dell'output nella console (non è combinabile con --silent)
        - `--help`: visualizza la schermata della Guida
    
    - A partire dalla versione 1910, l'utilità UploadOfflineFeedback supporta l'uso di un server proxy. È possibile specificare i parametri seguenti:
        - `-x, --proxy` Consente di specificare un server proxy per la connessione a Internet.
        - `-o, --port` Consente di specificare la porta del server proxy per la connessione a Internet.
        - `-u, --user` Consente di specificare un nome utente per il server proxy per la connessione a Internet.
        - `-w, --password` Consente di specificare la password per il server proxy per la connessione a Internet. Digitare un asterisco (&#42;) per generare la richiesta della password. La password non viene visualizzata quando la si digita al prompt della password. È consigliabile usare un asterisco (&#42;) per generare una richiesta di immissione della password perché il testo normale nella riga di comando è meno sicuro.
        - `-i` Consente di ignorare il controllo della connessione: ignora il controllo della connessione di rete, limitandosi a caricare il feedback con le impostazioni specificate.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> Conferma di commenti e suggerimenti della console

<!--3556010-->
A partire dalla versione 1902, quando si inviano commenti e suggerimenti tramite la console di Configuration Manager o tramite UploadOfflineFeedback.exe, viene visualizzato un messaggio di conferma. Questo messaggio include un **ID dei commenti**, che è possibile comunicare a Microsoft come identificatore per la tracciabilità.

- Per copiare l'**ID dei commenti**, selezionare l'icona di copia accanto all'ID oppure usare la combinazione di tasti **CTRL** + **C**.
  - L'ID non viene archiviato nel computer. Assicurarsi di copiarlo prima di chiudere la finestra.
- Facendo clic su **Non visualizzare più questo messaggio**, la finestra di dialogo sarà chiusa e non sarà più visualizzata in futuro.

   ![Conferma di commenti e suggerimenti nella console di Configuration Manager 1902](media/1902-feedback-id-example.png)
- Lo strumento di comando di **UploadOfflineFeedback** scrive il valore di **FeedbackID** nella console a meno che si usino -s o --silent.

  ![Conferma di commenti e suggerimenti di UploadOfflineFeedback in Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> Commenti e suggerimenti sul prodotto per la versione 1802 e precedenti

Per segnalare errori del prodotto potenziali è possibile usare l'[app Hub di Feedback](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporata in Windows 10. Quando si sceglie **Aggiungi nuovo feedback**, assicurarsi di selezionare la categoria **Enterprise Management** e di scegliere una delle sottocategorie seguenti:
- Client di Configuration Manager
- Console di Configuration Manager
- Distribuzione del sistema operativo di Configuration Manager
- Server di Configuration Manager

Continuare a usare la [pagina UserVoice](https://configurationmanager.uservoice.com/) per votare nuove idee per le funzionalità di Configuration Manager. Il team di prodotto di Configuration Manager usa i valori di stato di UserVoice seguenti:

- **Noted** (Annotato): la richiesta è appropriata ed è stata aggiunta al backlog.
- **Planned** (Pianificato): è stata avviata la scrittura del codice per questa funzionalità. Si prevede sarà disponibile in una versione di anteprima Tech nei prossimi mesi.
- **Started** (Avviato): la funzionalità è ora disponibile in un'anteprima Tech. È possibile esaminarla e inviare commenti e suggerimenti. Informare Microsoft se la funzionalità è corretta o meno. Inserire altri commenti e suggerimenti nella sezione dei commenti della richiesta originale perché altri utenti possano visualizzare e inviare commenti sulla funzionalità. Il feedback verrà letto e usato per migliorare la funzionalità.
- **Completed** (Completato): la prima versione della funzionalità è disponibile in una build di produzione. Questo stato non significa che la funzionalità è stata interamente completata e che non sarà sottoposta a miglioramenti. Significa invece che la prima versione della funzionalità è inclusa in una build di produzione e può essere usata in un ambiente reale. Viene contrassegnata come se fosse completata per i motivi seguenti:
  - È importante sapere che la funzionalità può essere usata in un ambiente di produzione.
  - I voti di UserVoice devono essere restituiti per poter essere usati per altri elementi.
  - È possibile archiviare nuove richieste di modifica di progettazione per questa funzionalità in modo tale che Microsoft sappia quale sarà il prossimo miglioramento più importante di questa funzionalità.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Blog del team di Configuration Manager  

I team di progettazione e i team associati di Configuration Manager usano il blog [Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) per offrire informazioni tecniche e altre notizie su Configuration Manager e le relative tecnologie. I post di questo blog integrano le informazioni di supporto e la documentazione relativa al prodotto.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> Opzioni di supporto e risorse per la community  

I seguenti collegamenti consentono di accedere a informazioni sulle opzioni di supporto e le risorse per la community:  

-   [Supporto tecnico Microsoft](https://aka.ms/cmcbsupport)  

-   [Community di Configuration Manager: Guida essenziale di Configuration Manager Current Branch](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Pagina dei forum di Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
