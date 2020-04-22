---
title: Policy Spy
titleSuffix: Configuration Manager
description: Usare Policy Spy per visualizzare e risolvere i problemi del sistema di criteri nei client Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707549"
---
# <a name="policy-spy"></a>Policy Spy

*Si applica a: Configuration Manager (Current Branch)*

Policy Spy è uno [strumento di Configuration Manager](tools.md). È uno strumento per la visualizzazione e la risoluzione dei problemi del sistema di criteri nei client Configuration Manager. Eseguire **PolicySpy.exe** per aprire l'interfaccia utente. Per altre informazioni sull'utilizzo della riga di comando, vedere [Sintassi della riga di comando](#bkmk_policyspy-syntax).

> [!Important]  
> Eseguire Policy Spy come amministratore. Se non lo si **esegue come amministratore**, viene visualizzato l'errore seguente nelle informazioni client:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a> Sintassi della riga di comando

Policy Spy è destinato principalmente all'uso tramite l'interfaccia utente. Fornisce opzioni della riga di comando limitate per supportare l'automazione e l'elaborazione batch.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Opzione: `/export`
Questa opzione esporta automaticamente i criteri del computer locale o remoto. `<ExportFilename>` è il nome file con cui lo strumento salva i criteri XML esportati. Se si specifica l'opzione `<computername>`, Policy Spy esporta i criteri di tale computer invece che quelli del computer locale.

> [!Note]  
> Questa opzione della riga di comando non consente di specificare le credenziali utente. Per usare credenziali alternative per accedere a un computer remoto, usare il comando **runas** per aprire un nuovo prompt dei comandi con le credenziali di sicurezza necessarie.  


## <a name="usage"></a>Utilizzo

### <a name="tools-menu"></a>Menu Strumenti

Nel menu **Strumenti** sono disponibili le azioni seguenti:  

- **Open Remote** (Apri remoto): si connette ai criteri client di Configuration Manager in un computer remoto. Usare la finestra di dialogo Connetti per recuperare il nome del computer remoto e le credenziali utente facoltative. Se la connessione non riesce, vengono visualizzate informazioni sull'errore nel riquadro Client Info (Informazioni client). Se la connessione ha di nuovo esito negativo, provare a connettersi scegliendo **Aggiorna** dal menu **Modifica** o premendo F5.  

- **Open File** (Apri file): apre un file di esportazione dei criteri (XML) creato dall'opzione **Export Policy** (Esporta criteri). Lo strumento visualizza i criteri esportati esattamente come un criterio attivo. Disabilita alcune funzionalità che si applicano solo quando ci si connette a un client effettivo.  

- **Request Machine Assignments** (Richiesta assegnazioni computer): attiva una richiesta di assegnazioni dei criteri del computer nel computer di destinazione. Questa funzionalità è disabilitata quando si visualizzano criteri esportati.  

- **Evaluate Machine Policy** (Valuta criteri computer): attiva una valutazione dei criteri del computer nel computer di destinazione. Questa funzionalità è disabilitata quando si visualizza un criterio esportato.  

- **Request User Assignments** (Richiedi assegnazioni utente): attiva una richiesta di assegnazioni dei criteri utente per l'utente attualmente connesso. Questa funzionalità è disponibile solo quando si visualizza un criterio nel computer locale.  

- **Evaluate User Policy** (Valuta criteri utente): attiva una valutazione dei criteri utente per l'utente attualmente connesso. Questa funzionalità è disponibile solo quando si visualizza un criterio nel computer locale.  

- **Reset Policy** (Reimposta criteri): rimuove tutti i criteri non predefiniti e reimposta i cookie dei criteri per il sito, quindi attiva una richiesta di assegnazioni dei criteri del computer. Questa funzionalità è disabilitata quando si visualizza un criterio esportato.  

- **Export Policy** (Esporta criteri): esporta i criteri del computer di destinazione in un file XML. Visualizzare questo file in un computer con Policy Spy. Per aprire il file di esportazione, scegliere **Apri file** dal menu **Strumenti**. Questa funzionalità è disabilitata quando si visualizza un criterio esportato.  


### <a name="edit-menu"></a>Menu Modifica

Nel menu **Modifica** sono disponibili le azioni seguenti:  

- **Elimina**: elimina l'istanza selezionata nel riquadro dei risultati. Questa azione è supportata solo per le istanze dei criteri. Se si prova eliminare elementi diversi dalle istanze dei criteri, lo strumento visualizza un messaggio di errore. Questa funzionalità è disabilitata quando si visualizza un criterio esportato.  

- **Aggiornare**: aggiorna tutti i risultati per visualizzare le informazioni più recenti. Tutti i nodi dell'albero espansi prima dell'aggiornamento vengono automaticamente espansi anche dopo. Se Policy Spy non è riuscito a connettersi ai criteri del computer di destinazione, prova a connettersi di nuovo. Questa funzionalità è disabilitata quando si visualizza un criterio esportato.  

- **Cancella eventi**: cancella tutti gli elementi dalla scheda Eventi.  



## <a name="results-pane"></a>Riquadro dei risultati

Il riquadro dei risultati offre viste diverse del sistema di criteri nel computer di destinazione. Per accedere a queste viste, fare clic su una delle quattro schede seguenti: 
- [Actual](#bkmk_policyspy-actual) (Effettivi)
- [Requested](#bkmk_policyspy-requested) (Richiesti)
- [Impostazione predefinita](#bkmk_policyspy-default)
- [Eventi](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a> Actual (Effettivi)

Questa scheda visualizza i criteri correnti del client. I criteri correnti determinano il comportamento di un client e quello degli agenti client, ad esempio la distribuzione e l'inventario software. La scheda visualizza i risultati in formato albero con un nodo radice per lo spazio dei nomi del computer e lo spazio dei nomi specifico di ogni utente. Espandere il nodo di uno spazio dei nomi per visualizzare un elenco di classi. Espandere una classe per visualizzare un elenco delle istanze. L'elenco di classi include solo le classi con istanze.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a> Requested (Richiesti)

Questa scheda visualizza le assegnazioni dei criteri che il client ha recuperato dal sito assegnato. La scheda visualizza i risultati in formato albero con un nodo radice per lo spazio dei nomi del computer e lo spazio dei nomi specifico di ogni utente. Espandendo il nodo di uno spazio dei nomi, vengono visualizzati i nodi seguenti:  

- **Configuration** (Configurazione): visualizza un elenco di classi di configurazione derivate da CCM_Policy_Config, che include oggetto criteri, assegnazioni e altre.  

- **Settings** (Impostazioni): visualizza tutte le impostazioni attive generate dai criteri. Le impostazioni vengono visualizzate sotto il nodo Configurazione. 

> [!Note]   
> Possono esistere più istanze con lo stesso nome perché il client non ha unito queste impostazioni in un set risultante finale. Policy Spy visualizza le istanze sotto questo nodo usando le proprietà RealKey invece delle vere chiavi dei criteri. Correlare queste istanze al set risultante visualizzato nella scheda Actual (Effettivi).  


### <a name="default"></a><a name="bkmk_policyspy-default"></a> Default

Questa scheda visualizza le stesse informazioni della scheda **Requested** (Richiesti). Include anche i contenuti degli spazi dei nomi DefaultMachine DefaultUser.


### <a name="events"></a><a name="bkmk_policyspy-events"></a> Eventi

Questa scheda visualizza gli eventi dell'agente criteri non appena si verificano. La vista crea una sottoscrizione di eventi WMI per tutti gli eventi derivati da CCM_PolicyAgent_Event. La vista mostra un massimo di 200 eventi. Rimuove gli eventi meno recenti dall'inizio dell'elenco, se necessario. Se si seleziona l'ultimo elemento dell'elenco, l'elenco scorre automaticamente verso il basso mentre vengono aggiunti i nuovi eventi. In caso contrario, la vista mantiene la posizione corrente ed è necessario scorrere verso il basso o premere FINE per visualizzare i nuovi eventi. Questa vista è sempre vuota quando si visualizza un criterio esportato.



## <a name="client-info-pane"></a>Riquadro Client Info (Informazioni client)
Il riquadro Client Info (Informazioni client) visualizza un elenco di proprietà del computer di destinazione. Se disponibili, visualizza le proprietà seguenti:  
- Name
- ID
- Version
- Sito
- Assigned MP
- Resident MP
- Proxy MP
- Proxy State



## <a name="details-pane"></a>Riquadro dei dettagli
Il riquadro Dettagli visualizza informazioni dettagliate sulla selezione corrente. Se nessuna selezione è attiva, visualizza informazioni su Policy Spy, inclusa la versione. In caso contrario, visualizza una rappresentazione Manage Object Format (MOF) dell'elemento selezionato.

Policy Spy usa la propria routine di generazione MOF per creare una visualizzazione HTML più semplice da usare della visualizzazione MOF di testo normale generata da WMI. Questo comportamento consente a Policy Spy di aggiungere le funzionalità seguenti per rendere la visualizzazione MOF più leggibile:  

- Evidenziazione della sintassi  

- Oggetti e matrici con rientro  

- Le proprietà vengono disposte in gruppi di sistema, ereditati e locali. Per impostazione predefinita, comprime i gruppi di sistema ed ereditati. È possibile visualizzare immediatamente quali proprietà vengono effettivamente usate dall'istanza.  

- Copiare MOF o copiare MOF di testo normale negli Appunti. Questa funzionalità è utile per incollare la visualizzazione MOF in altre applicazioni chiamando direttamente lo strumento MofComp.  

Per le istanze degli oggetti criteri derivati da CCM_Policy_Policy, il riquadro dei dettagli visualizza il corpo dei criteri sotto la rappresentazione MOF visualizzata. Se il client non ha scaricato il corpo dei criteri, Policy Spy visualizza un collegamento ipertestuale. Fare clic sul collegamento per scaricare il corpo dei criteri direttamente dal punto di gestione del client. Se lo strumento riesce a scaricare il corpo dei criteri, sostituisce il collegamento ipertestuale con i contenuti della risposta. In caso contrario, Policy Spy aggiorna la visualizzazione indicando che la richiesta ha avuto esito negativo.

