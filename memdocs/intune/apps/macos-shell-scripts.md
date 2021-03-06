---
title: Usare script della shell nei dispositivi macOS in Microsoft Intune | Microsoft Docs
description: Creazione, assegnazione, monitoraggio e risoluzione dei problemi degli script della shell per dispositivi macOS in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36b85fa6713af5679e59382efaeb354bb4949705
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990591"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune"></a>Usare script della shell nei dispositivi macOS in Intune

Usare gli script della shell per estendere le funzionalità di gestione dei dispositivi in Intune oltre a quanto supportato dal sistema operativo macOS. 

## <a name="prerequisites"></a>Prerequisiti
Quando si creano e si assegnano script della shell a dispositivi macOS, assicurarsi che vengano soddisfatti i prerequisiti seguenti. 
 - I dispositivi devono eseguire macOS 10.12 o versione successiva.
 - I dispositivi devono essere gestiti da Intune. 
 - Gli script della shell devono iniziare con `#!` e devono trovarsi in un percorso valido, ad esempio `#!/bin/sh` o `#!/usr/bin/env zsh`.
 - Devono essere installati gli interpreti della riga di comando per le shell applicabili.

## <a name="important-considerations-before-using-shell-scripts"></a>Considerazioni importanti preliminari all'uso di script della shell
 - Per usare gli script della shell è necessario che l'agente di gestione di Microsoft Intune sia installato correttamente nel dispositivo macOS. Per altre informazioni, vedere [Agente di gestione di Microsoft Intune per macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Gli script della shell vengono eseguiti in parallelo nei dispositivi come processi separati.
 - Gli script della shell eseguiti come utente connesso verranno eseguiti per tutti gli account utente attualmente connessi nel dispositivo al momento dell'esecuzione.
 - È necessario che un utente finale esegua l'accesso al dispositivo per eseguire gli script come utente connesso.
 - Se lo script richiede modifiche non consentite per un account utente standard, sono necessari i privilegi di utente ROOT.
 - Gli script della shell tenteranno l'esecuzione più spesso rispetto alla frequenza scelta in determinate condizioni, ad esempio se il disco è pieno, se il percorso di archiviazione viene manomesso, se la cache locale viene eliminata o se il dispositivo Mac viene riavviato.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Creare e assegnare un criterio di script della shell
1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **macOS** > **Script** > **Aggiungi**.
3. In **Informazioni di base** immettere le proprietà seguenti e selezionare **Avanti**:
   - **Nome**: immettere un nome per lo script della shell.
   - **Descrizione**: immettere una descrizione per lo script della shell. Questa impostazione è facoltativa ma consigliata.
4. In **Impostazioni script** immettere le proprietà seguenti e selezionare **Avanti**:
   - **Carica lo script**: passare allo script della shell. Le dimensioni del file di script devono essere inferiori a 200 KB.
   - **Esegui lo script come utente connesso**: selezionare **Sì** per eseguire lo script con le credenziali dell'utente nel dispositivo. Scegliere **No** (impostazione predefinita) per eseguire lo script come utente ROOT. 
   - **Nascondi le notifiche degli script nei dispositivi:** Per impostazione predefinita, le notifiche degli script vengono visualizzate per ogni script eseguito. Gli utenti finali visualizzano la notifica *Il reparto IT sta configurando il computer* di Intune nei dispositivi macOS.
   - **Frequenza dello script:** Selezionare la frequenza di esecuzione dello script. Scegliere **Non configurata** (impostazione predefinita) per eseguire uno script una sola volta.
   - **Numero massimo di nuovi tentativi in caso di errore dello script:** Selezionare il numero di esecuzioni dello script necessarie nel caso in cui venga restituito un codice di uscita diverso da zero (zero indica l'esito positivo). Scegliere **Non configurato** (impostazione predefinita) per non effettuare altri tentativi se lo script ha esito negativo.
5. In **Tag di ambito** aggiungere facoltativamente i tag di ambito per lo script e selezionare **Avanti**. È possibile usare i tag di ambito per determinare chi può visualizzare gli script in Intune. Per informazioni dettagliate complete sui tag di ambito, vedere [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Usare il controllo degli accessi in base al ruolo e i tag di ambito per l'IT distribuito).
6. Selezionare **Assegnazioni** > **Selezionare i gruppi da includere**. Viene visualizzato un elenco di gruppi di Azure AD esistenti. Selezionare uno o più gruppi di utenti o dispositivi per la ricezione dello script. Scegliere **Seleziona**. I gruppi selezionati vengono visualizzati nell'elenco e ricevono il criterio di script.
   > [!NOTE]
   > - Gli script della shell assegnati ai gruppi di utenti si applicano a qualsiasi utente che effettua l'accesso al Mac.  
   > - Aggiornando le assegnazioni per gli script della shell vengono aggiornate anche le assegnazioni per l'[agente MDM di Microsoft Intune per macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

7. In **Rivedi e aggiungi** viene visualizzato un riepilogo delle impostazioni configurate. Selezionare **Aggiungi** per salvare lo script. Quando si seleziona **Aggiungi** il criterio di script viene distribuito ai gruppi scelti.

Lo script creato ora compare nell'elenco di script. 

## <a name="monitor-a-shell-script-policy"></a>Monitorare i criteri di script della shell
È possibile monitorare lo stato di esecuzione di tutti gli script assegnati a utenti e dispositivi scegliendo uno dei report seguenti:
- **Script** > **selezionare lo script da monitorare** > **Stato dispositivo**
- **Script** > **selezionare lo script da monitorare** > **Stato dell'utente**

>[!IMPORTANT]
> Indipendentemente dalla **Frequenza dello script** selezionata, lo stato dell'esecuzione dello script viene segnalato solo la prima volta che uno script viene eseguito. Lo stato di esecuzione dello script non viene aggiornato nelle esecuzioni successive. Tuttavia, gli script aggiornati vengono considerati come nuovi script e ne verrà nuovamente segnalato lo stato di esecuzione.

Dopo l'esecuzione di uno script, viene restituito uno degli stati seguenti:
- Uno stato di esecuzione dello script **Operazione non riuscita** indica che lo script ha restituito un codice di uscita diverso da zero oppure che lo script non è valido. 
- Uno stato di esecuzione dello script di **Operazione riuscita** indica che lo script ha restituito il codice di uscita zero. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Risolvere i problemi dei criteri di script della shell macOS usando la raccolta dei log

È possibile raccogliere i log del dispositivo per risolvere i problemi di script nei dispositivi macOS. 

### <a name="requirements-for-log-collection"></a>Requisiti per la raccolta di log
Per raccogliere i log in un dispositivo macOS sono necessari gli elementi seguenti:
- Specificare il percorso assoluto completo dei file di log.
- I percorsi di file devono essere separati solo con un punto e virgola (;).
- La dimensione massima della raccolta di log per il caricamento è 60 MB (compressa) o 25 file, a seconda di quale condizione si verifica per prima.
- I tipi di file consentiti per la raccolta di log includono le estensioni seguenti: *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*

#### <a name="collect-device-logs"></a>Raccogliere i log dei dispositivi
1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Nel report **Stato dispositivo** o **Stato utente** selezionare un dispositivo.
3. Selezionare **Raccogli i log**, specificare i percorsi di cartella dei file di log separati solo da un punto e virgola (;) senza spazi o nuove righe tra i percorsi.<br>È possibile, ad esempio, scrivere più percorsi come `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Più percorsi di file di log separati da virgola, punto, nuova riga o virgolette con o senza spazi causeranno un errore della raccolta dei log. Anche gli spazi non sono consentiti come separatori tra i percorsi.

4. Selezionare **OK**. I log vengono raccolti alla successiva sincronizzazione con Intune dell'agente di gestione di Intune nel dispositivo. La sincronizzazione in genere avviene ogni 8 ore.

   >[!NOTE]
   > 
   > - I log raccolti vengono crittografati nel dispositivo, trasmessi e archiviati in Archiviazione di Microsoft Azure per 30 giorni. I log archiviati vengono decrittografati su richiesta e scaricati usando l'interfaccia di amministrazione di Microsoft Endpoint Manager.
   > - Oltre ai log specificati dall'amministratore, anche i log dell'agente di gestione di Intune vengono raccolti da queste cartelle: `/Library/Logs/Microsoft/Intune` e `~/Library/Logs/Microsoft/Intune`. I nomi dei file di log dell'agente sono `IntuneMDMDaemon date--time.log` e `IntuneMDMAgent date--time.log`. 
   > - Se un file specificato dall'amministratore è mancante o ha un'estensione di file errata, questi nomi di file sono elencati in `LogCollectionInfo.txt`.     

### <a name="log-collection-errors"></a>Errori di raccolta dei log
La raccolta dei log può non riuscire a causa di uno dei motivi indicati nella tabella seguente. Per risolvere questi errori, attenersi alla procedura di correzione.

| Codice di errore (esadecimale) | Codice di errore (decimale) | Messaggio di errore | Procedura di correzione |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Le dimensioni del file di log non possono essere superiori a 60 MB. | Verificare che le dimensioni dei log compressi siano inferiori a 60 MB. |
| 0X87D300D1 | 2016214831 | Il percorso del file di log specificato deve esistere. La cartella dell'utente di sistema non è un percorso valido per i file di log. | Verificare che il percorso del file specificato sia valido e accessibile. |
| 0X87D300D2 | 2016214830 | Non è stato possibile caricare il file di raccolta di log a causa della scadenza dell'URL di caricamento. | Ritentare l'azione **Raccogli i log**. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Non è stato possibile caricare il file di raccolta di log a causa di un errore di crittografia. Riprovare a caricare il log. | Ritentare l'azione **Raccogli i log**. |
| | 2016214828 | Il numero di file di log supera il limite consentito di 25 file. | È possibile raccogliere solo fino a 25 file di log alla volta. |
| 0X87D300D6 | 2016214826 | Non è stato possibile caricare il file di raccolta di log a causa di un errore di compressione. Riprovare a caricare il log. | Ritentare l'azione **Raccogli i log**. |
| | 2016214740 | Non è stato possibile crittografare i log perché non sono stati trovati log compressi. | Ritentare l'azione **Raccogli i log**. |
| | 2016214739 | I log sono stati raccolti ma non è stato possibile archiviarli. | Ritentare l'azione **Raccogli i log**. |

## <a name="frequently-asked-questions"></a>Domande frequenti
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Perché gli script della shell assegnati non vengono eseguiti nel dispositivo?
I motivi possono essere molteplici:
* È possibile che l'agente debba eseguire la sincronizzazione per ricevere script nuovi o aggiornati. Questo processo di sincronizzazione viene eseguito ogni 8 ore ed è diverso dalla sincronizzazione di MDM. Verificare che il dispositivo sia attivo e connesso a una rete per la sincronizzazione corretta dell'agente e attendere che l'agente si sincronizzi. È anche possibile richiedere all'utente finale di aprire il Portale aziendale nel Mac, selezionare il dispositivo e fare clic su **Controlla impostazioni**.
* È possibile che l'agente non sia installato. Verificare che l'agente sia installato in `/Library/Intune/Microsoft Intune Agent.app` nel dispositivo macOS.
* È possibile che l'agente non sia in uno stato integro. L'agente tenterà di eseguire il ripristino per 24 ore, rimuovere se stesso e reinstallarsi se sono ancora assegnati script della shell.

### <a name="how-frequently-is-script-run-status-reported"></a>Con quale frequenza viene segnalato lo stato di esecuzione degli script?
Lo stato di esecuzione degli script viene segnalato nella console di amministrazione di Microsoft Endpoint Manager non appena ne viene completata l'esecuzione. Se uno script è programmato per l'esecuzione periodica a una frequenza impostata, lo stato viene segnalato solo la prima volta che viene eseguito.

### <a name="when-are-shell-scripts-run-again"></a>Quando viene ripetuta l'esecuzione degli script della shell?
Uno script viene eseguito di nuovo solo quando è configurata l'impostazione **Numero massimo di nuovi tentativi in caso di errore dello script** e l'esecuzione ha esito negativo. Se l'impostazione **Numero massimo di nuovi tentativi in caso di errore dello script** non è configurata e uno script ha esito negativo, non verrà eseguito nuovamente e lo stato segnalato dell'esecuzione sarà **non riuscita**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Quali autorizzazioni del ruolo di Intune sono necessarie per gli script della shell?
Il ruolo di Intune assegnato richiede autorizzazioni per le **configurazioni dei dispositivi** per eliminare, assegnare, creare, aggiornare o leggere script della shell.

## <a name="microsoft-intune-management-agent-for-macos"></a>Agente di gestione di Microsoft Intune per macOS
 ### <a name="why-is-the-agent-required"></a>Perché è necessario l'agente?
È necessario installare l'agente di gestione di Microsoft Intune nei dispositivi macOS gestiti per abilitare funzionalità avanzate di gestione dei dispositivi non supportate dal sistema operativo macOS nativo.
 
 ### <a name="how-is-the-agent-installed"></a>Come si installa l'agente?
 L'agente viene installato automaticamente e in modalità invisibile all'utente nei dispositivi macOS gestiti da Intune a cui si assegna almeno uno script della shell nell'interfaccia di amministrazione di Microsoft Endpoint Manager. L'agente viene installato in `/Library/Intune/Microsoft Intune Agent.app` quando applicabile e non compare in **Finder** > **Applicazioni** nei dispositivi macOS. Durante l'esecuzione nei dispositivi macOS, l'agente appare come `IntuneMdmAgent` in **Monitoraggio Attività**.

### <a name="what-does-the-agent-do"></a>Che cosa fa l'agente?
 - L'agente esegue automaticamente l'autenticazione nei servizi di Intune prima della sincronizzazione per ricevere gli script della shell assegnati al dispositivo macOS.
 - L'agente riceve gli script della shell assegnati e li esegue in base alla pianificazione, al numero di tentativi, alle impostazioni di notifica e ad altre impostazioni configurate dall'amministratore.
 - L'agente controlla la presenza di script nuovi o aggiornati nei servizi di Intune in genere ogni 8 ore. Questo processo di sincronizzazione è indipendente dalla sincronizzazione di MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Come si può avviare manualmente la sincronizzazione di un agente da un Mac?
In un Mac gestito in cui è installato l'agente, aprire **Portale aziendale**, selezionare il dispositivo locale, fare clic su **Controlla impostazioni**. In questo modo si avvia una sincronizzazione MDM e una sincronizzazione di un agente.

In alternativa, aprire **Terminale**, eseguire il `sudo killall IntuneMdmAgent` comando per terminare il processo di `IntuneMdmAgent`. Il processo `IntuneMdmAgent` viene riavviato immediatamente, avviando una sincronizzazione con Intune.

> [!NOTE]
> L'azione **Sincronizza** per i dispositivi nella console di amministrazione di Microsoft Endpoint Manager consentono di avviare una sincronizzazione MDM e non forzano la sincronizzazione di un agente.

 ### <a name="when-is-the-agent-removed"></a>Quando viene rimosso l'agente?
 Esistono svariate condizioni che possono causare la rimozione dell'agente dal dispositivo, ad esempio:
 - Al dispositivo non vengono più assegnati script della shell. 
 - Il dispositivo macOS non è più gestito.
 - L'agente resta in uno stato di errore irreversibile per più di 24 ore (tempo di riattivazione del dispositivo).

 ### <a name="why-are-scripts-running-even-though-the-mac-is-no-longer-managed"></a>Perché gli script vengono eseguiti anche se il Mac non è più gestito?
 Quando un Mac con script assegnati non è più gestito, l'agente non viene rimosso immediatamente. L'agente rileva che il Mac non è gestito alla sincronizzazione successiva dell'agente (in genere ogni 8 ore) e annulla l'esecuzione degli script programmati. Tutti gli script archiviati localmente programmati per essere eseguiti con maggiore frequenza rispetto alla sincronizzazione successiva programmata dell'agente verranno quindi eseguiti. Quando l'agente non è in grado di eseguire la sincronizzare, riprova a eseguire la sincronizzare per un massimo di 24 ore (tempo di riattivazione del dispositivo) e quindi si rimuove dal Mac.
 
 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Come si può disattivare l'invio a Microsoft di dati di utilizzo per gli script della shell?
 Per disattivare l'invio dei dati di utilizzo a Microsoft da parte dell'agente di gestione di Intune, aprire Portale aziendale, selezionare **Menu** > **Preferenze** >  *e deselezionare Consenti a Microsoft di raccogliere i dati di utilizzo*. L'invio dei dati di utilizzo verrà così disattivato sia per l'agente di gestione di Intune che per Portale aziendale.

## <a name="known-issues"></a>Problemi noti
- **Nessun stato di esecuzione dello script:** nel caso improbabile in cui un dispositivo riceva uno script e vada offline prima che venga segnalato lo stato dell'esecuzione, il dispositivo non segnalerà lo stato di esecuzione dello script nella console di amministrazione.

## <a name="next-steps"></a>Passaggi successivi

- [Creare criteri di conformità in Microsoft Intune](..\protect\create-compliance-policy.md)
