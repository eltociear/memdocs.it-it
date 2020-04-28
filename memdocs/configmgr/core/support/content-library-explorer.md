---
title: Content Library Explorer
titleSuffix: Configuration Manager
description: Content Library Explorer consente di visualizzare la raccolta contenuto in un punto di distribuzione di Configuration Manager e di risolvere eventuali problemi.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aa92fb143815faf693f6c2629c3f6436546c5080
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078533"
---
# <a name="content-library-explorer"></a>Content Library Explorer

*Si applica a: Configuration Manager (Current Branch)*

Content Library Explorer è uno degli [strumenti di Configuration Manager](tools.md). È possibile usarlo per le attività seguenti:  

- Esplorare la raccolta contenuto in un punto di distribuzione specifico  

- Risolvere i problemi della raccolta contenuto  

- Copiare pacchetti, contenuto, cartelle e file dalla raccolta contenuto  

- Ridistribuire pacchetti al punto di distribuzione  

- Convalidare pacchetti nei punti di distribuzione remoti  



## <a name="requirements"></a>Requisiti

- Eseguire lo strumento usando un account dotato di accesso amministrativo per:  

    - Il punto di distribuzione di destinazione  

    - Il provider di WMI nel server del sito  

    - Il provider di Configuration Manager  

- Soltanto i ruoli di **Amministratore completo** e **Analista di sola lettura** dispongono di diritti sufficienti per visualizzare tutte le informazioni disponibili con lo strumento.  

    - Altri ruoli, ad esempio **Amministratore applicazione**, possono visualizzare solo informazioni parziali. Per altre informazioni, vedere [Pacchetti disabilitati](#bkmk_disabled-packages).  

    - Il ruolo di **Analista di sola lettura** non può usare lo strumento per ridistribuire pacchetti.  

- Eseguire lo strumento da qualsiasi computer, a condizione che consenta la connessione a:  

    - Il punto di distribuzione di destinazione  

    - Il server del sito primario  

    - Il provider di Configuration Manager  

- Se il punto di distribuzione si trova nel server del sito, è comunque necessario disporre dell'accesso amministrativo al server del sito.  



## <a name="usage"></a>Utilizzo 

All'avvio di **ContentLibraryExplorer.exe**, immettere il nome di dominio completo (FQDN) del punto di distribuzione di destinazione. Lo strumento si connette quindi al punto di distribuzione. Se il punto di distribuzione fa parte di un sito secondario, verrà richiesto il FQDN del server del sito primario e il codice del sito primario.

Nel riquadro a sinistra vengono visualizzati i pacchetti distribuiti a questo punto di distribuzione. Espandere i pacchetti ed esplorare la struttura di cartelle, che corrisponde alla struttura con la quale è stato creato il pacchetto.

Quando si seleziona una cartella, nel riquadro a destra vengono visualizzati tutti i file che questa contiene. La visualizzazione include le informazioni seguenti: 
- Nome file
- Dimensione del file
- Unità in cui si trova il file
- Altri pacchetti che usano lo stesso file nell'unità
- Ultima modifica apportata al file nel punto di distribuzione

Lo strumento si connette anche al provider di Configuration Manager. La connessione consente di determinare quali pacchetti vengono distribuiti al punto di distribuzione e se effettivamente si trovano o meno nella raccolta contenuto del punto di distribuzione. Ad esempio, un pacchetto la cui distribuzione è sospesa potrebbe non essere ancora presente nella raccolta contenuto. Un pacchetto di questo tipo viene visualizzato dallo strumento come "in sospeso", con nessuna azione abilitata.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a> Pacchetti disabilitati

Alcuni pacchetti sono presenti nel punto di distribuzione ma non sono visibili nella console di Configuration Manager. Questi pacchetti sono contrassegnati con un asterisco (\*). Su di essi non è possibile eseguire alcuna azione. Anche altri pacchetti possono essere contrassegnati da un asterisco e le azioni a loro riservate disabilitate. 

La disabilitazione dei pacchetti è causata da tre ragioni principali:  

- Il pacchetto è l'aggiornamento del client di Configuration Manager. Il pacchetto include il file "ccmsetup.exe".  

- L'account utente non può accedere al pacchetto, probabilmente a causa del ruolo amministrativo di cui dispone. Ad esempio, il ruolo **Autore applicazioni** non può visualizzare i pacchetti di driver nella console, che pertanto vengono contrassegnati come disabilitati nel punto di distribuzione.  

- Il pacchetto nel punto di distribuzione è orfano.  


### <a name="validate-packages"></a>Convalidare i pacchetti

Convalidare i pacchetti usando le opzioni **Pacchetto** > **Convalida** sulla barra degli strumenti. Selezionare innanzitutto un nodo pacchetto nel riquadro a sinistra. Non selezionare un contenuto o una cartella. Lo strumento esegue la connessione al provider di WMI nel punto di distribuzione per l'azione richiesta. All'avvio dello strumento, i pacchetti a cui mancano uno o più contenuti vengono contrassegnati come non validi. La convalida del pacchetto individua il contenuto che non è presente. Se tutti i contenuti sono presenti ma i dati sono danneggiati, l'azione di convalida rileva il danneggiamento.


### <a name="redistribute-packages"></a>Ridistribuire i pacchetti

Ridistribuire i pacchetti usando le opzioni **Pacchetto** > **Ridistribuisci** sulla barra degli strumenti. Selezionare innanzitutto un nodo pacchetto nel riquadro a sinistra. Per questa azione è necessaria l'autorizzazione per la ridistribuzione di pacchetti.


### <a name="other-actions"></a>Altre azioni

Usare le opzioni **Modifica** > **Copia** per copiare pacchetti, contenuti, cartelle e file dalla raccolta contenuto a una cartella specificata. Non è possibile copiare la raccolta contenuto. È possibile selezionare più di un file, ma non più cartelle.

Eseguire una ricerca nei pacchetti usando le opzioni **Modifica** > **Find Package** (Trova pacchetto). Questa azione esegue la ricerca nel nome e nell'ID del pacchetto.



## <a name="limitations"></a>Limitazioni

- Lo strumento non consente di modificare direttamente la raccolta contenuto. Le modifiche alla raccolta contenuto potrebbero causare malfunzionamenti.  

- Lo strumento consente di ridistribuire i pacchetti, ma soltanto nel punto di distribuzione di destinazione.  

- Se il punto di distribuzione si trova nel server del sito, non è possibile convalidare i dati del pacchetto. In questo caso usare la console di Configuration Manager. Lo strumento ispeziona il pacchetto per verificare che tutto il contenuto sia presente, ma non ne valuta l'integrità.  

- Inoltre, non consente di eliminare contenuti.



## <a name="see-also"></a>Vedere anche

- [Concetti di base sulla gestione dei contenuti](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Raccolta contenuto](../plan-design/hierarchy/the-content-library.md)
