---
title: Siti di disinstallazione
titleSuffix: Configuration Manager
description: Guida per la rimozione dei ruoli e la disinstallazione di siti e gerarchie
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700529"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Disinstallare ruoli, siti e gerarchie in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare questo articolo come guida per la disinstallazione di un ruolo del sistema del sito, un sito o una gerarchia di Configuration Manager.

A partire dalla versione 2002, è anche possibile rimuovere il sito di amministrazione centrale da una gerarchia, mantenendo però il sito primario.

## <a name="site-system-role"></a><a name="bkmk_role"></a> Ruolo del sistema del sito

Potrebbe essere necessario rimuovere un ruolo da un server del sistema del sito per i motivi seguenti:

- Modifica dell'infrastruttura a un livello più ampio, ad esempio a livello di percorsi di rete o posizioni fisiche
- Rimozione delle autorizzazioni del server sottostante
- Consolidamento dei ruoli per ridurre i costi e la complessità
- Riconfigurazione o riprogettazione dei ruoli del sito
- Interruzione dell'utilizzo della funzionalità supportata dal ruolo

Quando si decide che un ruolo deve essere rimosso, rispondere prima di tutto alle domande seguenti:

- Il ruolo è ancora necessario nel sito? Se lo è, un altro sistema del sito dispone già del ruolo?

- Altri sistemi del sito con questo ruolo sono dimensionati correttamente per supportare i requisiti aziendali in termini di prestazioni e disponibilità?

- Tutti i client sono già stati riconfigurati per l'uso di un altro ruolo? Ci si baserà sui comportamenti client predefiniti per eseguire il fallback o individuare un altro server?

### <a name="procedure-to-remove-a-site-system-role"></a>Procedura per rimuovere un ruolo del sistema del sito

Per rimuovere un ruolo, seguire questa procedura:

1. Nella console di **Configuration Manager** passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e quindi selezionare il nodo **Server e ruoli del sistema del sito**.

1. Selezionare il server del sistema del sito con il ruolo da rimuovere. Nel riquadro dei dettagli **Ruoli sistema del sito** selezionare il ruolo di destinazione.

1. Sulla barra multifunzione, nel gruppo **Ruolo del sito** della scheda **Ruolo del sito**, selezionare **Rimuovi ruolo**. Confermare che si vuole rimuovere il ruolo.

### <a name="additional-information-for-specific-roles"></a>Informazioni aggiuntive per ruoli specifici

Per alcuni ruoli possono valere considerazioni e passaggi aggiuntivi.

#### <a name="software-update-point"></a>Punto di aggiornamento software

Dopo la rimozione del punto di aggiornamento software, Configuration Manager aggiorna i criteri client per rimuoverlo dall'elenco. Una volta rimosso l'ultimo punto di aggiornamento software nel sito, l'elenco dei punti di aggiornamento software non conterrà più alcuna voce. Senza ruoli disponibili, la gestione degli aggiornamenti software è essenzialmente disabilitata nel sito.

Quando sono presenti più punti di aggiornamento software in un sito primario e si rimuove il punto di aggiornamento software che corrisponde all'origine della sincronizzazione, occorre scegliere un altro punto di aggiornamento software nel sito come nuova origine della sincronizzazione.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a> Sito secondario  

Oltre alla [rimozione delle autorizzazioni di una gerarchia](#bkmk_hierarchy), il motivo principale per rimuovere un sito secondario è dovuto a una modifica dell'infrastruttura a un livello più ampio, ad esempio a livello di percorsi di rete o posizioni fisiche. Esaminare anche i motivi per [scegliere un sito secondario](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

Quando si decide che un sito secondario deve essere rimosso, rispondere prima di tutto alle domande seguenti:

- Sono stati rimossi tutti i ruoli del sistema del sito dal server del sito?

- Al sito secondario sono associati limiti o gruppi di limiti? Riconfigurare i limiti prima di rimuovere il sito.

- Sono ancora presenti dei client?

- Sono state configurate altre opzioni di gestione dei contenuti, ad esempio il processo di [peer caching](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)?

### <a name="options-to-delete-secondary-sites"></a>Opzioni per eliminare i siti secondari

Non è possibile spostare un sito secondario o riassegnarlo a un altro sito primario. Quando si rimuove un sito secondario dal sito padre diretto, si può solo scegliere se disinstallarlo o eliminarlo.

#### <a name="uninstall-the-secondary-site"></a>Disinstallare il sito secondario

Usare questa opzione per rimuovere un sito secondario funzionante accessibile dalla rete. Questa opzione disinstalla Configuration Manager dal server del sito secondario. Elimina quindi tutte le informazioni sul sito e sulle relative risorse dal sito di Configuration Manager.

Se Configuration Manager ha installato SQL Server Express per il sito secondario, disinstalla anche SQL Server Express. Se SQL Server Express è stato installato prima di installare il sito secondario, Configuration Manager non lo disinstalla.

#### <a name="delete-the-secondary-site"></a>Eliminare il sito secondario

Usare questa opzione nelle situazioni seguenti:

- L'installazione non è riuscita

- Dopo la disinstallazione, il sito secondario continua a essere visualizzato nella console di Configuration Manager

    Questa opzione elimina tutte le informazioni sul sito e sulle relative risorse dalla gerarchia di Configuration Manager, ma non apporta alcuna modifica sul server del sito.

    > [!TIP]
    >  È anche possibile usare lo strumento di manutenzione gerarchia con l'opzione **/DELSITE** per eliminare un sito secondario. Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>Prerequisiti per l'eliminazione di un sito secondario

L'utente amministratore che esegue il programma di installazione di Configuration Manager deve avere i privilegi di protezione seguenti:

- Diritti di **amministratore** locale nel server del sito secondario

- Se il server di database del sito primario è remoto rispetto al server del sito primario, diritti di **amministratore** locale sul server di database del sito remoto per il sito primario.

- Ruolo di sicurezza **Amministratore infrastruttura** o **Amministratore completo** nel sito primario padre

- Diritti di **amministratore di sistema** sul database del sito secondario

### <a name="procedure-to-delete-a-secondary-site"></a>Procedura per eliminare un sito secondario

Per disinstallare o eliminare un sito secondario, seguire questa procedura:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Siti**.

1. Selezionare il server del sito secondario che si vuole rimuovere. Sulla barra multifunzione, nel gruppo **Sito** della scheda **Home**, selezionare **Elimina**.

1. Nella pagina **Generale** specificare se si vuole disinstallare o eliminare il sito secondario.

1.  Completare la procedura guidata.

## <a name="primary-site"></a><a name="bkmk_primary"></a> Sito primario  

Potrebbe essere necessario disinstallare un sito primario dalla gerarchia per i motivi seguenti:

- Consolidamento dei siti per ridurre i costi e la complessità
- Riconfigurazione o riprogettazione dei siti della gerarchia

Prima di disinstallare un sito primario figlio che usa [viste distribuite](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) per il collegamento di replica al sito di amministrazione centrale, disattivare le viste distribuite nella gerarchia. Per ulteriori informazioni, vedere [Disinstallare un sito primario configurato con viste distribuite](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a> Pianificare la disinstallazione di un sito primario

Prima di disinstallare un sito primario, esaminare le attività seguenti:

- Rivedere i limiti, i gruppi di limiti e le relazioni di fallback. Se si assegnano client a un nuovo sito ma non si modificano i limiti, potrebbero essere considerati in roaming. Per altre informazioni, vedere [Definire i limiti del sito e i gruppi di limiti](../configure/define-site-boundaries-and-boundary-groups.md).

- Verificare che tutti i client attivi vengano riassegnati a un altro sito primario nella gerarchia, altrimenti i client non saranno gestiti dopo la disinstallazione del sito. Per altre informazioni, vedere [Come assegnare i client a un sito](../../../clients/deploy/assign-clients-to-a-site.md).

  - Esaminare l'elenco dei ruoli del sito per assicurarsi che il nuovo sito fornisca lo stesso livello di servizio.

  - Verificare di aver ridimensionato correttamente gli altri sistemi del sito con questo ruolo nell'altro sito. Dovranno supportare i requisiti aziendali di prestazioni e disponibilità con i client aggiuntivi.

  - Se il sito ha molti client, riassegnarli in fasi. Monitorare la replica di database mentre i client aggiornano l'inventario completo e altri dati specifici del sito. Se si gestiscono gli aggiornamenti software, i client verranno assegnati a un nuovo punto di aggiornamento software. Questo comportamento causa un'analisi completa della conformità degli aggiornamenti.

  - La riassegnazione del client può avere un impatto sui report e sulle query che si basano sui dati di inventario e sulla conformità basata sullo stato. Prendere in considerazione la regolazione temporanea dei cicli di client durante la transizione.

  - Esaminare tutti i metodi di assegnazione dei client per verificare che nessuno faccia riferimento a questo sito primario.

- Controllare se sono presenti oggetti usati attivamente nella gerarchia che contengono riferimenti statici al codice del sito, ad esempio query di raccolta, sequenze di attività o script amministrativi.

- Se la gerarchia usa un [sito di fallback](../configure/boundary-group-procedures.md#bkmk_site-fallback) per l'assegnazione sito automatica, verificare che non faccia riferimento a questo sito primario.

- Riconfigurare gli eventuali [metodi di installazione client](../../../clients/deploy/plan/client-installation-methods.md) che potrebbero fare riferimento a un codice del sito statico.

- Se il sito primario dispone di servizi collegati al cloud specifici del sito, rimuoverli. Se le risorse cloud sono ancora necessarie, spostarle in un altro sito primario nella gerarchia. Rimuoverle dal sito primario che si vuole disinstallare e aggiungerle a un altro sito primario.

- Se il sito primario dispone di [metodi di individuazione](../configure/run-discovery.md) per la gerarchia, spostarli in un altro sito.

- Ritirare gli eventuali [supporti di distribuzione del sistema operativo](../../../../osd/deploy-use/create-task-sequence-media.md) basati su sito.

- Disinstallare tutti i ruoli del sistema del sito dal sito e dal server del sito. Per altre informazioni, vedere [Disinstallare i ruoli del sistema del sito](#bkmk_role). Sebbene questo passaggio di preparazione non sia obbligatorio, consente di identificare eventuali altre dipendenze prima di disinstallare il sito.

- Disinstallare tutti i siti secondari di questo sito primario. Per altre informazioni, vedere la sezione [Sito secondario](#bkmk_secondary).

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a> Prerequisiti per la disinstallazione di un sito primario

L'utente amministratore che esegue il programma di installazione di Configuration Manager deve avere i privilegi di protezione seguenti:

- Diritti di **amministratore** locale sul server CAS

- Se il server di database CAS è remoto rispetto al server del sito primario, diritti di **amministratore** locale sul server di database del sito remoto per il sito di amministrazione centrale (CAS).

- Diritti di **amministratore di sistema** sul database del sito CAS

- Diritti di **amministratore** locale sul server del sito primario

- Se il server di database del sito primario è remoto rispetto al server del sito primario, diritti di **amministratore** locale sul server di database del sito remoto per il sito primario.

- Ruolo di sicurezza **Amministratore infrastruttura** o **Amministratore completo** nel sito di amministrazione centrale

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a> Procedura per disinstallare un sito primario

Eseguire il programma di installazione di Configuration Manager per disinstallare un sito primario a cui non è associato un sito secondario. Usare la procedura seguente per disinstallare un sito primario:

> [!TIP]
> Se il server del sito primario non è più disponibile, usare lo strumento di manutenzione gerarchia nel sito di amministrazione centrale per eliminare il sito primario dal database del sito. Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Avviare il programma di installazione di Configuration Manager sul server del sito primario usando uno dei metodi seguenti:

    - Nel menu**Start** selezionare **Installazione di Configuration Manager**.

    - Nella directory dei *supporti di installazione* di Configuration Manager aprire `\SMSSETUP\BIN\X64\setup.exe`. Verificare che la versione corrisponda a quella del sito.

    - Nella directory in cui è *installato* Configuration Manager aprire `\BIN\X64\setup.exe`.

1. Leggere le informazioni nella pagina **Prima di iniziare**.

1. Nella pagina **Riquadro attività iniziale** selezionare **Disinstalla un server di sito di Configuration Manager**.

    > [!IMPORTANT]  
    >  Quando un sito secondario è collegato al sito principale, è necessario rimuovere il sito secondario prima di disinstallare il sito principale.  

1. Nella pagina **Disinstalla il sito di Configuration Manager** entrambe le opzioni seguenti sono abilitate per impostazione predefinita:

    - Rimuovere il database del sito dal server del sito primario
    - Rimuovere la console di Configuration Manager dal computer

1. Fare clic su **Sì** per confermare la disinstallazione del sito primario di Configuration Manager.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a> Disinstallare un sito primario che usa le viste distribuite

1. Prima di disinstallare un sito primario figlio, disattivare le viste distribuite in ogni collegamento della gerarchia tra il sito di amministrazione centrale e un sito primario.

1. Dopo avere disattivato le viste distribuite in ogni collegamento, assicurarsi che la reinizializzazione dei dati del sito primario venga completata nel sito di amministrazione centrale. Per monitorare l'inizializzazione dei dati, vedere [Monitorare la replica](../../manage/monitor-replication.md).

1. Dopo la corretta reinizializzazione dei dati con il sito di amministrazione centrale, è possibile [disinstallare il sito primario](#bkmk_pri-process).

1. Dopo la disinstallazione del sito primario, è possibile riconfigurare le viste distribuite nei collegamenti dal sito di amministrazione centrale ad altri siti primari.

    > [!IMPORTANT]
    > Se si disinstalla il sito primario prima di disattivare le viste distribuite in ogni sito oppure prima della reinizializzazione corretta dei dati dal sito primario nel sito di amministrazione centrale, la replica dei dati potrebbe non riuscire.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a> Rimuovere le autorizzazioni di una gerarchia

Alcune organizzazioni hanno più gerarchie a causa di fusioni, acquisizioni, ambienti di test o altri requisiti aziendali. Consolidando la gestione in una singola gerarchia si può contribuire a ridurre i costi e la complessità. Un altro motivo per rimuovere le autorizzazioni della gerarchia è che si sta eseguendo la migrazione a un servizio di gestione solo cloud, come Microsoft Intune, e si è pronti a rimuovere l'infrastruttura locale.

Per rimuovere le autorizzazioni da una gerarchia con più siti, la sequenza di rimozione è importante. Iniziare dalla disinstallazione dei siti dai livelli bassi della gerarchia e procedere verso i livelli alti:

1. Rimuovere i siti secondari collegati a siti primari.
2. Disinstallare i siti primari.
3. Dopo aver disinstallato tutti i siti primari, è possibile disinstallare il sito di amministrazione centrale.

Per altre informazioni, vedere le sezioni seguenti:

- [Rimuovere un sito secondario](#bkmk_secondary)
- [Disinstallare un sito primario](#bkmk_primary)
- [Disinstallare il sito di amministrazione centrale](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a> Disinstallare il sito di amministrazione centrale

Il passaggio finale per rimuovere le autorizzazioni di una gerarchia consiste nel disinstallare il sito di amministrazione centrale. Eseguire il programma di installazione di Configuration Manager per disinstallare il sito di amministrazione centrale che non ha siti primari figlio.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Prerequisiti per disinstallare il sito di amministrazione centrale

L'utente amministratore che esegue il programma di installazione di Configuration Manager deve avere i privilegi di protezione seguenti:

- Diritti di **amministratore** locale sul server CAS

- Se il server di database CAS è remoto rispetto al server del sito primario, diritti di **amministratore** locale sul server di database del sito remoto per il sito di amministrazione centrale (CAS).

#### <a name="procedure-to-uninstall-the-cas"></a>Procedura per disinstallare il sito di amministrazione centrale

1. Avviare il programma di installazione di Configuration Manager nel server del sito di amministrazione centrale usando uno dei metodi seguenti:

    - Nel menu**Start** selezionare **Installazione di Configuration Manager**.

    - Nella directory dei *supporti di installazione* di Configuration Manager aprire `\SMSSETUP\BIN\X64\setup.exe`. Verificare che la versione corrisponda a quella del sito.

    - Nella directory in cui è *installato* Configuration Manager aprire `\BIN\X64\setup.exe`.

1. Leggere le informazioni nella pagina **Prima di iniziare**.

1. Nella pagina **Riquadro attività iniziale** selezionare **Disinstalla un server di sito di Configuration Manager**.

    > [!IMPORTANT]  
    >  Rimuovere tutti i siti primari figlio prima di disinstallare il sito di amministrazione centrale.  

1. Nella pagina **Disinstalla il sito di Configuration Manager** entrambe le opzioni seguenti sono abilitate per impostazione predefinita:

    - Rimuovere il database del sito dal server del sito di amministrazione centrale
    - Rimuovere la console di Configuration Manager dal computer

1. Selezionare **Sì** per confermare la disinstallazione del sito di amministrazione centrale (CAS) di Configuration Manager.

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a> Rimuovere il sito di amministrazione centrale

<!-- 3607277 -->

A partire dalla versione 2002, se la gerarchia è costituita dal sito di amministrazione centrale e da un singolo sito primario figlio, è possibile rimuovere il sito di amministrazione centrale. Questa azione semplifica l'infrastruttura di Configuration Manager riducendola a un singolo sito primario autonomo. Elimina le complessità della replica da sito a sito e concentra le attività di gestione sul singolo sito.

Per altre informazioni, vedere [Rimuovere il sito di amministrazione centrale](remove-central-administration-site.md).
