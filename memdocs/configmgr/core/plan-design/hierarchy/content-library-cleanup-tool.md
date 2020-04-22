---
title: Strumento di pulizia della raccolta contenuto
titleSuffix: Configuration Manager
description: Usare lo strumento di pulizia della raccolta contenuto per rimuovere contenuto orfano non più associato a una distribuzione di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703629"
---
# <a name="content-library-cleanup-tool"></a>Strumento di pulizia della raccolta contenuto

*Si applica a: Configuration Manager (Current Branch)*

Usare lo strumento da riga di comando per la pulizia della raccolta contenuto per rimuovere il contenuto non più associato a un pacchetto o a un'applicazione in un punto di distribuzione. Questo tipo di contenuto è detto *contenuto orfano*. Questo strumento sostituisce le versioni precedenti di strumenti simili rilasciati per i prodotti Configuration Manager precedenti.  

Lo strumento interessa solo il contenuto presente nel punto di distribuzione che viene specificato quando si esegue lo strumento stesso. Quest'ultimo non può rimuovere contenuto dalla raccolta contenuto nel server del sito.

Trovare **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` sul server del sito.



## <a name="requirements"></a>Requisiti  

- Eseguire lo strumento solo in un singolo punto di distribuzione alla volta.  

- Eseguirlo direttamente nel computer che ospita il punto di distribuzione da pulire oppure in remoto da un altro computer.  

- L'account utente che esegue lo strumento deve avere le stesse autorizzazioni del ruolo di sicurezza **Amministratore completo** in Configuration Manager.  



## <a name="modes-of-operation"></a>Modalità di funzionamento

Eseguire lo strumento nelle due modalità seguenti: [simulazione](#what-if-mode) ed [eliminazione](#delete-mode).

> [!Tip]  
> Iniziare con la modalità di *simulazione*. Dopo aver ottenuto i risultati desiderati, eseguire lo strumento in modalità di *eliminazione*.  


### <a name="what-if-mode"></a>Modalità di simulazione   

Se non si specifica il parametro `/delete`, lo strumento viene eseguito in modalità di simulazione. Questa modalità identifica il contenuto che verrebbe eliminato dal punto di distribuzione.

- Quando viene eseguito in questa modalità, lo strumento non elimina alcun dato.  

- Lo strumento scrive nel file di log le informazioni sul contenuto da eliminare. Non viene richiesto di confermare ogni eliminazione potenziale.  


### <a name="delete-mode"></a>Modalità di eliminazione   

Se si attiva il parametro `/delete`, lo strumento viene eseguito in modalità di eliminazione.

- Se si esegue lo strumento in questa modalità, il contenuto orfano trovato nel punto di distribuzione specificato può essere eliminato dalla raccolta contenuto del punto di distribuzione stesso.  

- Prima di eliminare ogni file, confermare che lo strumento debba eliminarlo. Selezionare **S** per Sì, **N** per No o **Sì a tutti** per ignorare le altre richieste di conferma ed eliminare tutto il contenuto orfano.  


### <a name="log-file"></a>File di log

Quando lo strumento viene eseguito in una delle due modalità, crea automaticamente un log. Denomina il file di log con le informazioni seguenti: 
- Modalità di esecuzione dello strumento  
- Nome del punto di distribuzione  
- Data e ora dell'operazione  

Al termine dell'esecuzione dello strumento, il file di log si apre automaticamente in Windows. 

Per impostazione predefinita, lo strumento scrive il file di log nella cartella temp dell'account utente che esegue lo strumento. Questo percorso si trova sul computer in cui si esegue lo strumento, che non è sempre la destinazione dello strumento. Usare il parametro `/log` per reindirizzare il file di log a un'altra posizione, compresa una condivisione di rete.



## <a name="run-the-tool"></a>Eseguire lo strumento

Per eseguire lo strumento: 

1. Aprire un prompt dei comandi come amministratore. Sostituire la directory con la cartella contenente **ContentLibraryCleanup.exe**.  

2. Immettere una riga di comando che includa i [parametri della riga di comando](#bkmk_params) obbligatori e i parametri facoltativi che si vogliono usare.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a> Parametri della riga di comando  

Usare questi parametri della riga di comando in qualsiasi ordine.   

### <a name="required-parameters"></a>Parametri obbligatori

|Parametro|Dettagli|
|---------|-------|
| `/dp <distribution point FQDN>`  | Specificare il nome di dominio completo (FQDN) del punto di distribuzione da pulire. |
| `/ps <primary site FQDN>` | *Obbligatorio* solo per la pulizia del contenuto di un punto di distribuzione in un sito secondario. Lo strumento si connette al sito primario padre per eseguire query sul provider SMS. Queste query consentono allo strumento di determinare quale contenuto deve trovarsi nel punto di distribuzione e quindi di identificare il contenuto orfano da rimuovere. La connessione al sito primario padre deve essere eseguita per i punti di distribuzione in un sito secondario, perché i dettagli necessari non sono disponibili direttamente dal sito secondario.|
| `/sc <primary site code>`  | *Obbligatorio* solo per la pulizia del contenuto di un punto di distribuzione in un sito secondario. Specificare il codice del sito primario padre. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Esempio: analizzare e registrare il contenuto da eliminare (simulazione)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Esempio: analizzare e registrare il contenuto per un punto di distribuzione in un sito secondario
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Parametri facoltativi

|Parametro|Dettagli|
|---------|-------|
|`/delete`| Usare questo parametro se si è pronti per eliminare il contenuto dal punto di distribuzione. Viene chiesta conferma prima di eliminare il contenuto. </br></br> Quando non si usa questo parametro, lo strumento registra i risultati sul contenuto da eliminare. Senza questo parametro, il contenuto non viene effettivamente eliminato dal punto di distribuzione. |
| `/q` | Questo parametro esegue lo strumento in modalità non interattiva, che elimina tutti i prompt. Questi prompt includono quando eliminare il contenuto. Neppure il file di log viene aperto automaticamente. |
| `/ps <primary site FQDN>` | Facoltativo solo per la pulizia del contenuto di un punto di distribuzione in un sito primario. Specificare il nome di dominio completo del sito primario a cui appartiene il punto di distribuzione. |
| `/sc <primary site code>` | Facoltativo solo per la pulizia del contenuto di un punto di distribuzione in un sito primario. Specificare il codice del sito primario a cui appartiene il punto di distribuzione. |
| `/log <log file directory>` | Specificare il percorso in cui lo strumento scrive il file di log. Questo percorso può essere un'unità locale o una condivisione di rete.</br></br> Quando non si usa questo parametro, lo strumento inserisce il file di log nella directory temporanea dell'utente sul computer in cui lo strumento viene eseguito.|

#### <a name="example-delete-content"></a>Esempio: eliminare il contenuto 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Esempio: eliminare il contenuto senza prompt
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Esempio: eseguire la registrazione nell'unità locale
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Esempio: eseguire la registrazione nella condivisione di rete
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Problema noto

Quando un pacchetto o una distribuzione non è riuscita o è in corso, lo strumento potrebbe restituire l'errore seguente: `System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Non esiste una soluzione alternativa per questo problema. Lo strumento non riesce a identificare in modo affidabile i file orfani quando la distribuzione del contenuto è in corso o ha avuto esito negativo. Lo strumento non consentirà di pulire il contenuto fino a quando il problema non sarà stato risolto.
