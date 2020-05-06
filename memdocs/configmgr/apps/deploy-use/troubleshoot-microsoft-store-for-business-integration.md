---
title: Risolvere i problemi di integrazione con MSfB
titleSuffix: Configuration Manager
description: Offre suggerimenti e risoluzioni per alcuni dei problemi di integrazione di Microsoft Store per le aziende e la formazione più comuni.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149100"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Risolvere i problemi di integrazione di Microsoft Store per le aziende e la formazione con Configuration Manager

Questo articolo offre importanti suggerimenti e correzioni per la risoluzione di alcuni dei problemi principali che possono verificarsi durante l'integrazione di Microsoft Store per le aziende e la formazione (MSfB) con Configuration Manager.

Per altre informazioni sull'uso di Microsoft Store per le aziende e la formazione con Configuration Manager, vedere [Gestire app da Microsoft Store per le aziende e Microsoft Store per la formazione con Configuration Manager](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>Monitoraggio

### <a name="component-status"></a>Stato componente

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Stato componente**. Monitorare lo stato dei componenti seguenti:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Stato di sincronizzazione

Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**. Controllare la colonna **Stato ultima sincronizzazione**.

### <a name="view-synchronized-apps"></a>Visualizzare le app sincronizzate

Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione applicazioni** e selezionare il nodo **Informazioni di licenza per le app dello Store**.


## <a name="log-files"></a>File di registro

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

Questo file di log si trova nel punto di connessione del servizio, in `\Logs` nella directory di installazione Configuration Manager. Registra le informazioni relative alla comunicazione con il servizio cloud. Queste informazioni includono metadati, icone, pacchetti e recupero dei file di licenza.

Per modificare il livello di registrazione, impostare il valore di `LoggingLevel` su `0` nella chiave del Registro di sistema `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION`. Per altre informazioni, vedere [Configurare le opzioni di registrazione](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

Questo file di log si trova nel punto di connessione del servizio, in `\Logs` nella directory di installazione Configuration Manager. Se il servizio WSfBSyncWorker non viene avviato oppure viene avviato e arrestato ripetutamente, esaminare le voci presenti in questo file di log.

> [!NOTE]
> Questo file di log è condiviso con altre funzionalità.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

Questo file di log si trova nel server del sito per il sito di livello superiore nella gerarchia. Si trova in `\Logs` nella directory di installazione di Configuration Manager. Registra informazioni sui processi seguenti:

- Inserimento delle informazioni sui metadati sincronizzate dal componente BusinessAppProcessWorker nel database
- Elaborazione dei file in `\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

Questo file di log si trova nel server del sito per il sito di livello superiore nella gerarchia. Si trova in `\Logs` nella directory di installazione di Configuration Manager. Se il servizio BusinessAppProcessWorker non viene avviato oppure viene avviato e arrestato ripetutamente, esaminare le voci presenti in questo file di log.



## <a name="last-sync-failed"></a>L'ultima sincronizzazione non è riuscita

Quando lo stato dell'ultima sincronizzazione è *non riuscita*, esaminare prima di tutto i [file di log](#log-files) seguenti per identificare il sintomo:

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Quindi vedere una delle sezioni seguenti per informazioni sui problemi comuni:

- [Errore di autorizzazione](#bkmk_fail-symptom1)
- [Chiave privata non valida](#bkmk_fail-symptom2)
- [Errore di recupero token dell'applicazione](#bkmk_fail-symptom3)
- [Il percorso del contenuto non esiste o le autorizzazioni non sono corrette](#bkmk_fail-symptom4)
- [Errore durante la richiesta HTTP per la chiamata al metodo 'GET'](#bkmk_fail-symptom5)
- [Impossibile scrivere altri byte nel buffer](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a> Errore di autorizzazione

#### <a name="cause"></a>Causa

Questo problema può verificarsi se l'applicazione Azure Active Directory (Azure AD) configurata non ha le autorizzazioni necessarie per gestire Microsoft Store per le aziende e la formazione per questo tenant.

#### <a name="workaround"></a>Soluzione alternativa

1. Accedere come amministratore al portale di Microsoft Store per le aziende e la formazione.
1. Passare a **Impostazioni** e selezionare **Strumenti di gestione**.
1. Se l'applicazione non è inclusa nell'elenco, selezionare **Add a management tool** (Aggiungi uno strumento di gestione). Quindi cercare in base al nome e selezionare l'applicazione Azure AD associata con lo stesso ID client di Configuration Manager.
1. Se lo stato non indica **Attivo**, selezionare **Attiva** nella sezione **Azione**.
1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**. Eseguire la sincronizzazione con lo Store o attendere l'intervallo di sincronizzazione successivo.

> [!Tip]
> Per trovare l'ID client in Configuration Manager:
>
> 1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Tenant di Azure Active Directory**.
> 1. Selezionare il tenant usato per l'integrazione di Microsoft Store per le aziende e la formazione.
> 1. Nel riquadro dei risultati trovare l'applicazione corrispondente ed esaminare la colonna **ID client**.

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a> Chiave privata non valida

#### <a name="cause"></a>Causa

Questo problema può verificarsi se la chiave privata è scaduta nell'app Azure AD per la configurazione di Microsoft Store per le aziende e la formazione.

#### <a name="resolution"></a>Soluzione

Rinnovare la chiave privata per l'applicazione Azure AD. Per altre informazioni, vedere [Rinnovare la chiave privata](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a> Errore di recupero token dell'applicazione

#### <a name="cause"></a>Causa

Questo problema può verificarsi se l'app connessa non esiste più in Azure AD.

#### <a name="resolution"></a>Soluzione

Eliminare e creare di nuovo la connessione a Microsoft Store per le aziende e la formazione.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**.
1. Selezionare la connessione esistente.
1. Selezionare **Elimina** nella barra multifunzione.

Creare nuovamente la connessione. Per altre informazioni, vedere gli articoli seguenti:

- [Configurare i servizi di Azure](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Configurare la sincronizzazione di Microsoft Store per le aziende e la formazione](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a> Il percorso del contenuto non esiste o le autorizzazioni non sono corrette

#### <a name="cause"></a>Causa

Quando si configura la connessione di Microsoft Store per le aziende e la formazione viene specificata una condivisione di rete per l'archiviazione del contenuto sincronizzato. Questo problema può verificarsi se la condivisione non esiste o ha autorizzazioni non corrette. L'account computer per il punto di connessione del servizio deve essere il proprietario di questa directory e delle eventuali sottodirectory.<!-- memdocs#146 --> In caso contrario, verrà visualizzato un errore simile al seguente:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Per vedere il percorso configurato:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**.

1. Selezionare l'account e aprirne le **proprietà**.

1. Passare alla scheda **Configurazione**. L'impostazione **Percorso** indica il percorso di rete in cui archiviare il contenuto dell'applicazione scaricato da Microsoft Store per le aziende e la formazione.

#### <a name="workaround"></a>Soluzione alternativa

1. Se la condivisione non esiste ancora, crearla.

1. Controllare le autorizzazioni NTFS della cartella e le autorizzazioni della condivisione di rete. Concedere all'account del computer del punto di connessione del servizio autorizzazioni di **lettura** e **scrittura**.

Se si vuole riconfigurare il percorso, eliminare e creare di nuovo la connessione al nuovo percorso del contenuto.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a> Errore durante la richiesta HTTP per la chiamata al metodo 'GET'

#### <a name="cause"></a>Causa

Questo problema può verificarsi se la sincronizzazione delle applicazioni dallo Store ha richiesto troppo tempo e l'URL del contenuto è scaduto.

#### <a name="workaround"></a>Soluzione alternativa

Ripetere il processo di sincronizzazione

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**.
1. Selezionare la connessione. Nella barra multifunzione selezionare **Sincronizza da Microsoft Store per le aziende**.

A ogni tentativo, la sincronizzazione dovrebbe avanzare. Possono essere necessari diversi tentativi a seconda dei fattori seguenti:

- Numero di applicazioni offline
- Dimensione dei pacchetti
- Velocità di rete

A ogni tentativo, l'errore verrà visualizzato un minor numero di volte. Se il numero di errori non diminuisce, il problema è un altro.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a> Impossibile scrivere altri byte nel buffer

#### <a name="cause"></a>Causa

Questo problema può verificarsi se le dimensioni del pacchetto dell'applicazione sono superiori a 500 MB. Configuration Manager supporta la sincronizzazione automatica solo di applicazioni offline con pacchetti inferiori a 500 MB.

#### <a name="workaround"></a>Soluzione alternativa

Non è possibile sincronizzare automaticamente queste app, ma è possibile scaricare il contenuto e creare manualmente l'applicazione:

1. Ottenere l'ID dell'applicazione in stato di errore dalla riga seguente in **WSfbSynWorker.log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Accedere come amministratore al portale di Microsoft Store per le aziende e la formazione. Trovare la pagina dell'applicazione.

    > [!Tip]
    > L'URL della pagina è simile al seguente: `https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Selezionare **Offline**, se non è già selezionato. Quindi selezionare **Gestisci**.

    1. Creare una cartella separata nella condivisione del contenuto dell'applicazione per tutte le piattaforme supportate.

    1. Scaricare il pacchetto nella cartella del pacchetto.

    1. Scaricare il file di licenza codificato come file `.bin` nella cartella del pacchetto.

    1. Scaricare tutti i framework necessari nella cartella del pacchetto.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.

1. [Creare un'applicazione](create-applications.md) specificando manualmente le informazioni sull'applicazione.

    1. Creare un tipo di distribuzione per ogni piattaforma supportata precedentemente scaricata.

    1. Tipo: **Pacchetto app Windows (\*.appx, \*.appxbundle)**

    1. Specificare il file con estensione appx/appxbundle del pacchetto dell'app effettivo, non un pacchetto di dipendenze necessario.

Verificare i dettagli seguenti nella pagina **Importa informazioni** finale:

- **File di licenza:** specifica il file `.bin`. Questo file di licenza è necessario per le app offline.
- **Dipendenze applicazione Windows:** verifica che tutte le dipendenze necessarie siano scaricate per questo pacchetto.


## <a name="sync-doesnt-run"></a>La sincronizzazione non viene eseguita

Questa sezione illustra i problemi di sincronizzazione seguenti:

- Il processo di sincronizzazione viene avviato manualmente, ma non viene eseguito
- Il sito non viene sincronizzato automaticamente ogni giorno

Esaminare prima di tutto i [file di log](#log-files) per identificare il sintomo:

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Quindi vedere una delle sezioni seguenti per informazioni sui problemi comuni:

- [Sincronizzazione manuale non avviata](#bkmk_sync-symptom1)
- [Sincronizzazione giornaliera automatica non eseguita ed errore "arresto di # ruoli di lavoro" in SMS_BUSINESS_APP_PROCESS_MANAGER.log](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a> Sincronizzazione manuale non avviata

#### <a name="cause"></a>Causa

Questo problema può verificarsi se si avvia una sincronizzazione meno di 10 minuti dopo la sincronizzazione precedente. Non è possibile eseguire la sincronizzazione con una frequenza superiore a ogni 10 minuti.

#### <a name="resolution"></a>Soluzione

Attendere almeno 10 minuti prima di avviare un'altra sincronizzazione.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a> Sincronizzazione giornaliera automatica non eseguita ed errore "arresto di # ruoli di lavoro" in SMS_BUSINESS_APP_PROCESS_MANAGER.log

#### <a name="cause"></a>Causa

Questo problema può verificarsi se il componente SMS_BUSINESS_APP_PROCESS_MANAGER arresta il thread WsfbSyncWorker. L'errore può specificare `2` o `4` ruoli di lavoro.

#### <a name="workaround"></a>Soluzione alternativa

Riavviare il servizio **SMS_EXECUTIVE**.

Se non è possibile riavviare il servizio principale, arrestare entrambi i componenti con ruoli di lavoro MSfB e quindi avviare entrambi:

1. Aprire il Registro di sistema di Windows nel server che esegue il punto di connessione del servizio

1. Passare a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Impostare l'operazione richiesta su **Arresta**.

    1. Aggiornare per verificare lo stato corrente = **Arrestato**.

1. Passare a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Impostare l'operazione richiesta su **Arresta**.

    1. Aggiornare per verificare lo stato corrente = **Arrestato**.

1. In **SMS_CLOUDCONNECTION** impostare l'operazione richiesta su **Avvia**.

1. In **SMS_BUSINESS_APP_PROCESS_MANAGER** impostare l'operazione richiesta su **Avvia**.


## <a name="language-related-issues"></a>Problemi relativi alla lingua

Questa sezione include i problemi comuni seguenti:

- [Modifiche alla selezione della lingua non applicate](#bkmk_lang-symptom1)
- [Non tutte le lingue selezionate sono presenti per tutte le informazioni di licenza](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a> Modifiche alla selezione della lingua non applicate

#### <a name="cause"></a>Causa

Questo problema può verificarsi se la selezione della lingua è memorizzata nella cache e non viene cancellata dopo la modifica dei valori delle proprietà.

#### <a name="workaround"></a>Soluzione alternativa

Per risolvere questo problema, riavviare il servizio **SMS_Executive**.

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a> Non tutte le lingue selezionate sono presenti per tutte le informazioni di licenza

#### <a name="cause"></a>Causa

Questo problema può verificarsi se le informazioni di licenza dell'applicazione Microsoft Store per le aziende e la formazione non contengono dati localizzati per la lingua specificata.

#### <a name="workaround"></a>Soluzione alternativa

Aggiungere manualmente le lingue mancanti per le applicazioni create.


## <a name="offline-applications"></a>Applicazioni offline

Questa sezione include i problemi comuni seguenti:

- [Impossibile creare l'applicazione offline perché il contenuto non può essere verificato](#bkmk_off-symptom1)
- [Impossibile installare l'applicazione creata dalle informazioni di licenza offline](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a> Impossibile creare l'applicazione offline perché il contenuto non può essere verificato

#### <a name="cause"></a>Causa

Questo problema può verificarsi se il contenuto sincronizzato per l'applicazione offline è danneggiato o è stato modificato.

#### <a name="workaround"></a>Soluzione alternativa

Avviare una nuova sincronizzazione. Al termine della sincronizzazione, i file di contenuto non corretti verranno verificati e scaricati.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a> Impossibile installare l'applicazione creata dalle informazioni di licenza offline

#### <a name="cause"></a>Causa

Questo problema può verificarsi se l'applicazione viene distribuita a un client che esegue una versione di Windows 10 precedente alla versione 1511. Le app con licenza offline di Microsoft Store per le aziende e la formazione sono supportate solo in Windows 10 versione 1511 e successive.

#### <a name="resolution"></a>Soluzione

Installare l'ultima versione di Windows 10.


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Reperire informazioni sull'uso di Configuration Manager](../../core/understand/find-help.md).
