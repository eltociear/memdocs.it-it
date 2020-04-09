---
title: Usare script della shell nei dispositivi macOS in Microsoft Intune | Microsoft Docs
description: Creazione, assegnazione, monitoraggio e risoluzione dei problemi degli script della shell per dispositivi macOS in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
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
ms.openlocfilehash: ba099e3614c11e10ce4cd9ae94668a1648bfc150
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808047"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Usare script della shell nei dispositivi macOS in Intune (anteprima pubblica)

> [!NOTE]
> Gli script della shell per dispositivi macOS sono attualmente in anteprima. Prima di usare questa funzionalità, esaminare l'elenco dei [problemi noti nell'anteprima](macos-shell-scripts.md#known-issues).

Usare gli script della shell per estendere le funzionalità di gestione dei dispositivi in Intune oltre a quanto supportato dal sistema operativo macOS. 

## <a name="prerequisites"></a>Prerequisiti
Quando si creano e si assegnano script della shell a dispositivi macOS, assicurarsi che vengano soddisfatti i prerequisiti seguenti. 
 - I dispositivi devono eseguire macOS 10.12 o versione successiva.
 - I dispositivi devono essere gestiti da Intune. 
 - Gli script della shell devono iniziare con `#!` e devono trovarsi in un percorso valido, ad esempio `#!/bin/sh` o `#!/usr/bin/env zsh`.
 - Devono essere installati gli interpreti della riga di comando per le shell applicabili.

## <a name="important-considerations-before-using-shell-scripts"></a>Considerazioni importanti preliminari all'uso di script della shell
 - Per usare gli script della shell è necessario che l'agente MDM di Microsoft Intune sia installato correttamente nel dispositivo macOS. Per altre informazioni, vedere [Agente MDM di Microsoft Intune per macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
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
6. Selezionare **Assegnazioni** > **Selezionare i gruppi da includere**. Viene visualizzato un elenco di gruppi di Azure AD esistenti. Selezionare uno o più gruppi di dispositivi che includono gli utenti i cui dispositivi macOS devono ricevere lo script. Scegliere **Seleziona**. I gruppi selezionati vengono visualizzati nell'elenco e ricevono il criterio di script.
   > [!NOTE]
   > - Gli script della shell in Intune possono essere assegnati solo ai gruppi di sicurezza dei dispositivi di Azure AD. L'assegnazione a gruppi di utenti non è supportata nell'anteprima. 
   > - Aggiornando le assegnazioni per gli script della shell vengono aggiornate anche le assegnazioni per l'[agente MDM di Microsoft Intune per macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
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

## <a name="frequently-asked-questions"></a>Domande frequenti
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Perché gli script della shell assegnati non vengono eseguiti nel dispositivo?
I motivi possono essere molteplici:
* È possibile che l'agente debba eseguire la sincronizzazione per ricevere script nuovi o aggiornati. Questo processo di sincronizzazione viene eseguito ogni 8 ore ed è diverso dalla sincronizzazione di MDM. Verificare che il dispositivo sia attivo e connesso a una rete per la sincronizzazione corretta dell'agente e attendere che l'agente si sincronizzi.
* È possibile che l'agente non sia installato. Verificare che l'agente sia installato in `/Library/Intune/Microsoft Intune Agent.app` nel dispositivo macOS.
* È possibile che l'agente non sia in uno stato integro. L'agente tenterà di eseguire il ripristino per 24 ore, rimuovere se stesso e reinstallarsi se sono ancora assegnati script della shell.

### <a name="how-frequently-is-script-run-status-reported"></a>Con quale frequenza viene segnalato lo stato di esecuzione degli script?
Lo stato di esecuzione degli script viene segnalato nella console di amministrazione di Microsoft Endpoint Manager non appena ne viene completata l'esecuzione. Se uno script è programmato per l'esecuzione periodica a una frequenza impostata, lo stato viene segnalato solo la prima volta che viene eseguito.

### <a name="when-are-shell-scripts-run-again"></a>Quando viene ripetuta l'esecuzione degli script della shell?
Uno script viene eseguito di nuovo solo quando è configurata l'impostazione **Numero massimo di nuovi tentativi in caso di errore dello script** e l'esecuzione ha esito negativo. Se l'impostazione **Numero massimo di nuovi tentativi in caso di errore dello script** non è configurata e uno script ha esito negativo, non verrà eseguito nuovamente e lo stato segnalato dell'esecuzione sarà **non riuscita**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Quali autorizzazioni del ruolo di Intune sono necessarie per gli script della shell?
Il ruolo di Intune assegnato richiede autorizzazioni per le **configurazioni dei dispositivi** per eliminare, assegnare, creare, aggiornare o leggere script della shell.

## <a name="microsoft-intune-mdm-agent-for-macos"></a>Agente MDM di Microsoft Intune per macOS
 ### <a name="why-is-the-agent-required"></a>Perché è necessario l'agente?
 È necessario installare l'agente MDM di Microsoft Intune nei dispositivi macOS gestiti per abilitare funzionalità avanzate di gestione dei dispositivi non supportate dal sistema operativo macOS nativo.
 
 ### <a name="how-is-the-agent-installed"></a>Come si installa l'agente?
 L'agente viene installato automaticamente e in modalità invisibile all'utente nei dispositivi macOS gestiti da Intune a cui si assegna almeno uno script della shell nell'interfaccia di amministrazione di Microsoft Endpoint Manager. L'agente viene installato in `/Library/Intune/Microsoft Intune Agent.app` quando applicabile e non compare in **Finder** > **Applicazioni** nei dispositivi macOS. Durante l'esecuzione nei dispositivi macOS, l'agente appare come `IntuneMdmAgent` in **Monitoraggio Attività**.

### <a name="what-does-the-agent-do"></a>Che cosa fa l'agente?
 - L'agente esegue automaticamente l'autenticazione nei servizi di Intune prima della sincronizzazione per ricevere gli script della shell assegnati al dispositivo macOS.
 - L'agente riceve gli script della shell assegnati e li esegue in base alla pianificazione, al numero di tentativi, alle impostazioni di notifica e ad altre impostazioni configurate dall'amministratore.
 - L'agente controlla la presenza di script nuovi o aggiornati nei servizi di Intune in genere ogni 8 ore. Questo processo di sincronizzazione è indipendente dalla sincronizzazione di MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Come si può avviare manualmente la sincronizzazione di un agente da un Mac?
In un Mac gestito in cui è installato l'agente aprire **Terminale**, eseguire il comando `sudo killall IntuneMdmAgent` per terminare il processo `IntuneMdmAgent`. Il processo `IntuneMdmAgent` viene riavviato immediatamente, avviando una sincronizzazione con Intune.

In alternativa, è possibile eseguire queste operazioni:
1. Aprire **Monitoraggio attività** > **Visualizza** > *selezionare **Tutti i processi**.* 
2. Cercare i processi denominati `IntuneMdmAgent`. 
3. Uscire dal processo in esecuzione per l'utente **radice**. 

> [!NOTE]
> L'azione **Verifica le impostazioni** nel Portale aziendale e l'azione **Sincronizza** per i dispositivi nella console di amministrazione di Microsoft Endpoint Manager consentono di avviare una sincronizzazione MDM e non forzano la sincronizzazione di un agente.

 ### <a name="when-is-the-agent-removed"></a>Quando viene rimosso l'agente?
 Esistono svariate condizioni che possono causare la rimozione dell'agente dal dispositivo, ad esempio:
 - Al dispositivo non vengono più assegnati script della shell. 
 - Il dispositivo macOS non è più gestito.
 - L'agente resta in uno stato di errore irreversibile per più di 24 ore (tempo di riattivazione del dispositivo).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Come si può disattivare l'invio a Microsoft di dati di utilizzo per gli script della shell?
 Per disattivare l'invio dei dati di utilizzo a Microsoft da parte dell'agente MDM di Intune, aprire Portale aziendale, selezionare **Menu** > **Preferenze** >  *e deselezionare Consenti a Microsoft di raccogliere i dati di utilizzo*. L'invio dei dati di utilizzo viene disabilitato sia per l'agente MDM di Intune che per Portale aziendale.

## <a name="known-issues"></a>Problemi noti
- **Assegnazione a gruppi di utenti:** gli script della shell assegnati a gruppi di utenti non sono applicabili ai dispositivi. L'assegnazione a gruppi di utenti non è attualmente supportata nell'anteprima. Usare l'assegnazione a gruppi di dispositivi per assegnare gli script.
- **Raccogli i log:** l'azione "Raccogli log" è visibile. Tuttavia, quando si tenta di eseguire la raccolta dei log, viene visualizzato un messaggio che indica che si è verificato un errore e i log non vengono acquisiti. La raccolta di log non è attualmente supportata nell'anteprima.
- **Nessun stato di esecuzione dello script:** nel caso improbabile in cui un dispositivo riceva uno script e vada offline prima che venga segnalato lo stato dell'esecuzione, il dispositivo non segnalerà lo stato di esecuzione dello script nella console di amministrazione.
- **Report Stato dell'utente:** esiste un problema di report vuoto. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selezionare **Monitoraggio**. Lo stato utente mostra un report vuoto.

## <a name="next-steps"></a>Passaggi successivi

- [Creare criteri di conformità in Microsoft Intune](..\protect\create-compliance-policy.md)
