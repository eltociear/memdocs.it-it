---
title: Sito Web di amministrazione e monitoraggio BitLocker
titleSuffix: Configuration Manager
description: Come usare il sito Web di amministrazione e monitoraggio BitLocker (portale dell'help desk) in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf9301e4fcb279b7d79a6f6c3d0a90ab3d15e277
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697314"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Sito Web di amministrazione e monitoraggio BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Il sito Web di amministrazione e monitoraggio è un'interfaccia amministrativa di Crittografia unità BitLocker. Viene anche indicato come portale dell'help desk. Usare questo sito Web per esaminare i report, ripristinare le unità degli utenti e gestire i TPM del dispositivo.

[![Screenshot del sito Web di amministrazione e monitoraggio BitLocker predefinito](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Prima di poterlo usare, installare questo componente in un server Web. Per altre informazioni, vedere [Configurare i report e i portali di BitLocker](setup-websites.md).

Accedere al sito Web di amministrazione e monitoraggio tramite l'URL seguente: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> È possibile visualizzare il **report Controllo ripristino** dal sito Web di amministrazione e monitoraggio. Aggiungere altri report di gestione di BitLocker al punto di Reporting Services. Per altre informazioni, vedere [Visualizzare i report di BitLocker](view-reports.md).

## <a name="groups"></a>Gruppi

Per accedere ad aree specifiche del sito Web di amministrazione e monitoraggio, è necessario che l'account utente sia in uno dei gruppi seguenti. Creare questi gruppi in Active Directory usando il nome desiderato. Quando si installa il sito Web, è necessario specificare questi nomi di gruppo. Per altre informazioni, vedere [Configurare i report e i portali di BitLocker](setup-websites.md).

|Gruppo|Descrizione|
|--- |--- |
|Amministratori help desk di BitLocker|Fornisce l'accesso a tutte le aree del sito Web di amministrazione e monitoraggio. Quando si aiuta un utente a ripristinare le unità, immettere solo la chiave di ripristino e non il dominio e il nome utente. Se un utente è membro sia di questo gruppo sia del gruppo di utenti dell'help desk di BitLocker, le autorizzazioni del gruppo di amministratori sostituiscono le autorizzazioni del gruppo di utenti.|
|Utenti dell'help desk di BitLocker|Fornisce l'accesso alle aree **Manage TPM** (Gestisci TPM) e **Drive Recovery** (Ripristino unità) nel sito Web di amministrazione e monitoraggio. Quando si usa quest'area, è necessario compilare tutti i campi, inclusi il dominio e il nome dell'account dell'utente. Se un utente è membro sia di questo gruppo sia del gruppo di amministratori dell'help desk di BitLocker, le autorizzazioni del gruppo di amministratori sostituiscono le autorizzazioni del gruppo di utenti.|
|Utenti report di BitLocker|Fornisce l'accesso all'area **Reports** nel sito Web di amministrazione e monitoraggio.|

## <a name="manage-tpm"></a>Manage TPM (Gestisci TPM)

Se un utente immette un PIN errato per un numero eccessivo di volte, può verificarsi un blocco del TPM. Il numero di volte in cui un utente può immettere un PIN errato prima del blocco del TPM varia in base al produttore. Dall'area **Manage TPM** (Gestisci TPM) del sito Web di amministrazione e monitoraggio accedere al sistema dati di recupero chiavi centralizzato.

Per altre informazioni sulla proprietà del TPM, vedere [Configurare MBAM per depositare il TPM e archiviare le password OwnerAuth](/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> A partire da Windows 10, versione 1607, Windows non mantiene la password del proprietario del TPM durante il provisioning del TPM.

1. Andare al sito Web di amministrazione e monitoraggio nel Web browser, ad esempio `https://webserver.contoso.com/HelpDesk`.

1. Nel riquadro sinistro selezionare l'area **Manage TPM** (Gestisci TPM).

    ![Pagina Manage TPM (Gestisci TPM) del sito Web di amministrazione e monitoraggio BitLocker](media/bitlocker-admin-manage-tpm.png)

1. Immettere il nome di dominio completo e il nome del computer.

1. Se necessario, immettere il dominio dell'utente e il nome utente per recuperare il file di password del proprietario del TPM.

1. Scegliere una delle opzioni seguenti per **Reason for requesting TPM owner password file** (Motivo per la richiesta del file password proprietario TPM):

    - Reset PIN lockout (Reimposta blocco PIN)
    - Turn on TPM (Attiva TPM)
    - Turn off TPM (Disattiva TPM)
    - (Change TPM password) Modifica password TPM
    - Clear TPM (Cancella TPM)
    - Altro

    Dopo aver **inviato** il modulo, il sito Web restituisce una delle risposte seguenti:

    - Se non è possibile trovare un file di password del proprietario del TPM corrispondente, viene restituito un messaggio di errore.

    - Verrà restituito il file di password del proprietario del TPM per il computer interessato

    Dopo aver recuperato il file di password del proprietario del TPM, il sito Web visualizza la password del proprietario.

1. Per salvare la password in un file, selezionare **Salva**.

1. Nell'area **Manage TPM** (Gestisci TPM) selezionare l'opzione **Reimposta blocco TPM** e specificare il file di password del proprietario del TPM.

    Il blocco del TPM viene reimpostato. BitLocker ripristina l'accesso dell'utente al dispositivo.

    > [!IMPORTANT]
    > Non condividere il valore hash TPM o il file di password del proprietario del TPM.

## <a name="drive-recovery"></a>Drive recovery (Ripristino unità)

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> Ripristinare un'unità in modalità di ripristino

Le unità entrano in modalità di ripristino negli scenari seguenti:

- L'utente perde o dimentica il PIN o la password
- Il TPM rileva le modifiche apportate al BIOS o ai file di avvio del computer

Per ottenere una password di ripristino, usare l'area **Drive recovery** (Ripristino unità) del sito Web di amministrazione e monitoraggio.

> [!IMPORTANT]
> Le password di ripristino scadono dopo un singolo uso. Nelle unità del sistema operativo e nelle unità dati fisse, la regola del singolo utilizzo viene applicata automaticamente. Nelle unità rimovibili viene applicata quando si rimuove e si inserisce nuovamente l'unità.

1. Andare al sito Web di amministrazione e monitoraggio nel Web browser, ad esempio `https://webserver.contoso.com/HelpDesk`.

1. Nel riquadro sinistro selezionare l'area **Drive Recovery** (Ripristino unità).

    ![Pagina Drive Recovery (Ripristino unità) del sito Web di amministrazione e monitoraggio BitLocker](media/bitlocker-admin-drive-recovery.png)

1. Se necessario, immettere il dominio dell'utente e il nome utente per visualizzare le informazioni sul ripristino.

1. Per visualizzare un elenco di possibili chiavi di ripristino corrispondenti, immettere le prime otto cifre dell'ID della chiave di ripristino. Per ottenere la chiave di ripristino esatta, immettere l'intero ID della chiave di ripristino.

1. Scegliere una delle opzioni seguenti per **Reason for Drive Unlock** (Motivo per lo sblocco dell'unità):

    - Operating system boot order changed (Ordine di avvio del sistema operativo modificato)
    - BIOS changed (BIOS modificato)
    - Operating system files modified (File del sistema operativo modificati)
    - Lost startup key (Chiave di avvio persa)
    - Lost PIN (PIN perso)
    - TPM reset (Reimpostazione TPM)
    - Lost passphrase (Passphrase persa)
    - Lost smartcard (Smart card persa)
    - Altro

    Dopo aver **inviato** il modulo, il sito Web restituisce una delle risposte seguenti:

    - Se l'utente ha più password di ripristino corrispondenti, vengono restituite più corrispondenze possibili.

    - La password di ripristino e il relativo pacchetto per l'utente interessato.

        > [!NOTE]
        > Se si ripristina un'unità danneggiata, l'opzione del pacchetto di ripristino fornisce a BitLocker le informazioni critiche necessarie per il ripristino dell'unità.

    - Se non è possibile trovare una password di ripristino corrispondente, viene restituito un messaggio di errore.

    Dopo il recupero della password di ripristino e del relativo pacchetto, il sito Web visualizza la password di ripristino.

1. Per copiare la password, selezionare **Copia chiave**. Per salvare la password di ripristino in un file, selezionare **Salva**.

Per sbloccare l'unità, immettere la password di ripristino o usare il pacchetto di ripristino.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> Ripristinare un'unità spostata

Quando si sposta un'unità in un nuovo computer, poiché il TPM è diverso, BitLocker non accetta il PIN precedente. Per ripristinare l'unità spostata, ottenere l'ID chiave di ripristino per recuperare la password di ripristino.

Per ripristinare un'unità spostata, usare l'area **Drive recovery** (Ripristino unità) del sito Web di amministrazione e monitoraggio.

1. Nel computer con l'unità spostata, avviare il computer in modalità Ambiente ripristino Windows (WinRE).

1. In WinRE, BitLocker considera l'unità del sistema operativo spostata come un'unità dati fissa. BitLocker visualizza l'ID della password di ripristino dell'unità e richiede la password di ripristino.

    > [!NOTE]
    > In alcuni casi, durante il processo di avvio selezionare **Ho dimenticato il PIN** se l'opzione è disponibile. Passare quindi alla modalità di ripristino per visualizzare l'ID chiave di ripristino.

1. Usare l'ID chiave di ripristino per recuperare la password di ripristino dal sito Web di amministrazione e monitoraggio. Per altre informazioni, vedere [Ripristinare un'unità in modalità di ripristino](#bkmk_recovery).

Se l'unità spostata è stata configurata per l'uso di un chip TPM nel computer originale, attenersi alla procedura seguente. In caso contrario, il processo di ripristino è terminato.

1. Dopo aver sbloccato l'unità, avviare il computer in modalità WinRE. Aprire un prompt dei comandi in WinRE e usare il comando `manage-bde` per decrittografare l'unità. Questo strumento costituisce l'unico modo per rimuovere la protezione **TPM più PIN** senza il chip TPM originale. Per altre informazioni su questo comando, vedere [Manage-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Al termine, avviare normalmente il computer. Configuration Manager procederà ad applicare i criteri di BitLocker per crittografare l'unità con la configurazione TPM più PIN del nuovo computer.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> Ripristinare un'unità danneggiata

Usare l'ID chiave di ripristino per recuperare un pacchetto della chiave di ripristino dal sito Web di amministrazione e monitoraggio. Per altre informazioni, vedere [Ripristinare un'unità in modalità di ripristino](#bkmk_recovery).

1. Salvare il **Pacchetto della chiave di ripristino** nel computer e quindi copiarlo nel computer con l'unità danneggiata.

1. Aprire un prompt dei comandi come amministratore e digitare il comando seguente:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Sostituire i valori seguenti:

    - `<corrupted drive>`: Lettera unità dell'unità danneggiata, ad esempio `D:`
    - `<fixed drive>`: Lettera unità di un'unità disco rigido disponibile di dimensioni simili o maggiori rispetto all'unità danneggiata. BitLocker ripristina e sposta i dati sull'unità danneggiata nell'unità specificata. Tutti i dati in tale unità vengono sovrascritti.
    - `<key package>`: Percorso del pacchetto della chiave di ripristino
    - `<recovery password>`: Password di ripristino associata

    Ad esempio:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Per altre informazioni su questo comando, vedere [Repair-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Report

Il sito Web di amministrazione e monitoraggio include il **report Controllo del ripristino**. Altri report sono disponibili dal punto di Reporting Services di Configuration Manager. Per altre informazioni, vedere [Visualizzare i report di BitLocker](view-reports.md).

1. Andare al sito Web di amministrazione e monitoraggio nel Web browser, ad esempio `https://webserver.contoso.com/HelpDesk`.

1. Nel riquadro sinistro selezionare l'area **Report**.

1. Nella barra dei menu nella parte superiore selezionare il **report Controllo del ripristino**.

Per altre informazioni su questo report, vedere [report Controllo del ripristino](view-reports.md#bkmk-audit)

> [!TIP]
> Per salvare i risultati del report, selezionare **Esporta** nella barra dei menu **Report**.