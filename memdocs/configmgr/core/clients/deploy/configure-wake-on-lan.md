---
title: Configurare la riattivazione LAN
titleSuffix: Configuration Manager
description: Selezionare le impostazioni di riattivazione LAN in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 512d942d79d11178f010c4f0adb41a25ee432743
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694119"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Come configurare la riattivazione LAN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Specificare le impostazioni di riattivazione LAN per Configuration Manager quando si vogliono riattivare i computer da uno stato di sospensione.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a> Riattivazione LAN a partire dalla versione 1810
<!--3607710-->
A partire da Configuration Manager 1810, è disponibile una nuova funzionalità per riattivare i computer sospesi. È ora possibile riattivare un client dalla console di Configuration Manager anche se il client non si trova nella stessa subnet del server del sito. Se è necessario eseguire attività di manutenzione o query nei dispositivi, i client remoti in stato di sospensione non costituiranno un limite per le operazioni. Il server del sito usa il canale di notifica client per identificare altri client attivi nella stessa subnet remota e usa tali client per inviare una richiesta di riattivazione LAN (Magic Packet). L'uso del canale di notifica client consente di evitare instabilità negli indirizzi MAC, che potrebbero causare l'arresto della porta da parte del router. La nuova versione di Riattivazione LAN può essere abilitata contemporaneamente alla [versione precedente](#bkmk_wol-previous).

### <a name="limitations"></a>Limitazioni

- Almeno un client nella subnet di destinazione deve essere attivo.
- Questa funzionalità non supporta le tecnologie di rete seguenti:
   - IPv6
   - Autenticazione di rete 802.1x
    >[!NOTE]
    > L'autenticazione di rete 802.1x può funzionare con una configurazione aggiuntiva in base all'hardware e alla relativa configurazione.
- I computer si riattivano solo quando ricevono la notifica client **Riattiva**.
    - Per eseguire la riattivazione in base a una scadenza, viene usata la versione precedente di Riattivazione LAN.
    -  Se la versione precedente non è abilitata, la riattivazione dei client non si verifica per le distribuzioni create con le impostazioni **Utilizza riattivazione LAN per riattivare i client per le distribuzioni richieste** o **Invia pacchetti di riattivazione**.  

> [!IMPORTANT]
> La funzionalità di riattivazione LAN è consigliata per l'uso solo in una quantità limitata di dispositivi (100) alla volta.
>
> Quando si usa la funzionalità di riattivazione LAN per riattivare i computer dalla console di amministrazione di Configuration Manager, le richieste di riattivazione vengono inserite in una coda interna condivisa da altre funzionalità di azione in tempo reale. Esempi di queste altre funzionalità sono l'esecuzione di script, CMPivot e altre notifiche client con canale rapido. A seconda delle prestazioni dei sistemi del sito, le azioni di riattivazione potrebbero richiedere una quantità di tempo prolungata e ritardare altre azioni in tempo reale. Si consiglia di non riattivare più di 100 computer alla volta. Per sapere se si sta creando un backlog in quest'area che può causare ritardi, è possibile verificare se nella directory ...\inboxes\objmgr.box se è presente un numero elevato di file con estensione OPA.


### <a name="security-role-permissions"></a>Autorizzazioni del ruolo di sicurezza

- **Invia una notifica alla risorsa** nella categoria Raccolta

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Configurare i client per l'uso di Riattivazione LAN a partire dalla versione 1810

In precedenza era necessario abilitare manualmente il client per la riattivazione LAN nelle proprietà della scheda di rete. Configuration Manager 1810 include una nuova impostazione client, **Consenti l'attivazione della rete**. Configurare e distribuire questa impostazione invece di modificare le proprietà della scheda di rete.

1. In **Amministrazione** passare a **Impostazioni client**.
1. Selezionare le impostazioni client da modificare oppure creare nuove impostazioni client personalizzate da distribuire. Per altre informazioni, vedere [Come configurare le impostazioni client](configure-client-settings.md).
1. Nelle impostazioni client **Risparmio energia** selezionare **Abilita** per l'opzione **Consenti l'attivazione della rete**. Per altre informazioni su questa impostazione, vedere [Informazioni sulle impostazioni client](about-client-settings.md#power-management).

4. A partire da Configuration Manager 1902, la nuova versione di Riattivazione LAN rispetta la porta UDP personalizzata specificata per l'[impostazione client](about-client-settings.md#power-management) **Numero di porta di riattivazione LAN (UDP)** . Questa impostazione viene condivisa sia dalla nuova versione di Riattivazione LAN che da quella precedente.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Riattivare un client con la notifica client a partire dalla versione 1810
 
È possibile riattivare un singolo client oppure tutti i client sospesi in una raccolta. Per i dispositivi già attivi nella raccolta, non vengono eseguite azioni. La richiesta Riattivazione LAN verrà inviata solo ai client sospesi. Per altre informazioni su come notificare la riattivazione a un client, vedere [Notifica client](../manage/client-notification.md).

- **Per riattivare un singolo client:** fare clic con il pulsante destro del mouse sul client, scegliere **Notifica client**, quindi selezionare **Riattiva**.

   ![Notifica client Riattiva nella console](media/wol-wake-up-client-notification.png)

- **Per riattivare tutti i client sospesi in una raccolta:** fare clic con il pulsante destro del mouse sulla raccolta di dispositivi client, scegliere **Notifica client**, quindi selezionare **Riattiva**.
   - Questa operazione non può essere eseguita sulle raccolte predefinite.
   - Se una raccolta include una combinazione di client sospesi e attivi, la richiesta Riattivazione LAN viene inviata solo ai client sospesi.
   - A partire da Configuration Manager 2002, questa azione è disponibile da una console connessa a un sito di amministrazione centrale, a un sito autonomo o a un sito primario figlio.
   - Nelle versioni 1910 e precedenti, questa azione è attiva solo quando la console di Configuration Manager è connessa a un sito primario autonomo o figlio. Quando si è connessi a un sito di amministrazione centrale, l'azione non è disponibile.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Comportamento previsto quando è abilitata solo la nuova versione di Riattivazione LAN

Se è abilitata solo la nuova versione di Riattivazione LAN, sarà abilitata solo la notifica client **Riattiva**. Ai client non viene inviata una notifica quando si riceve una scadenza nelle distribuzioni, come sequenze di attività, distribuzioni di software o installazione di aggiornamenti software. Quando un computer sospeso torna online, questo stato si riflette nella console durante la sincronizzazione con il punto di gestione.

A partire da Configuration Manager versione 1902, è possibile specificare la porta di Riattivazione LAN. Questa impostazione viene condivisa sia dalla nuova versione di Riattivazione LAN che da quella precedente.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Comportamento previsto quando sono abilitate entrambe le versioni di Riattivazione LAN

Se sono abilitate entrambe le versioni di Riattivazione LAN, è possibile usare la notifica client **Riattiva** e la riattivazione in corrispondenza di una scadenza. Il funzionamento della notifica client è leggermente diverso rispetto alla versione tradizionale di Riattivazione LAN. Per una breve descrizione del funzionamento della notifica client, vedere la sezione [Riattivazione LAN a partire dalla versione 1810](#bkmk_wol-1810). La nuova impostazione client **Consenti la riattivazione della rete** cambia le proprietà della scheda di interfaccia di rete per abilitare Riattivazione LAN. Non è più necessario cambiarle manualmente per i nuovi computer aggiunti all'ambiente. Le altre funzionalità di Riattivazione LAN non sono cambiate.

A partire dalla versione 1902, la notifica client **Riattiva** rispetta l'attuale impostazione di **Numero di porta di riattivazione LAN (UDP)** .


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a> Riattivazione LAN per la versione1806 e precedenti

Specificare le impostazioni di riattivazione LAN per Configuration Manager quando si vogliono riattivare i computer da uno stato di sospensione per installare il software necessario, come aggiornamenti software, applicazioni, sequenze di attività e programmi.

È possibile integrare la riattivazione LAN usando le impostazioni client proxy di riattivazione. Prima di utilizzare il proxy di riattivazione è tuttavia necessario attivare la riattivazione LAN per il sito e specificare **Utilizza solo pacchetti di riattivazione** e l'opzione **Unicast** per il metodo di trasmissione riattivazione LAN. Questa soluzione di riattivazione supporta anche connessioni ad hoc, ad esempio una connessione desktop remoto.

Utilizzare la prima procedura per configurare un sito primario per la riattivazione LAN. Usare quindi la seconda procedura per configurare le impostazioni client proxy di riattivazione. Questa seconda procedura consente di configurare le impostazioni client predefinite per le impostazioni proxy di riattivazione da applicare a tutti i computer nella gerarchia. Se si desidera applicare queste impostazioni solo ad alcuni computer, creare un'impostazione dispositivo personalizzata e assegnarla a una raccolta che contenga i computer che si desidera configurare per il proxy di riattivazione. Per altre informazioni su come creare impostazioni client personalizzate, vedere [Come configurare le impostazioni client](../../../core/clients/deploy/configure-client-settings.md).

Un computer che riceve le impostazioni client proxy di riattivazione sospenderà probabilmente la connessione di rete per 1-3 secondi. Ciò si verifica perché il client deve reimpostare la scheda di interfaccia di rete per abilitare il driver proxy di riattivazione.

> [!WARNING]
> Per evitare interruzioni impreviste dei servizi di rete, valutare prima il proxy di riattivazione in un'infrastruttura di rete isolata e rappresentativa. Utilizzare quindi le impostazioni client personalizzate per espandere la verifica a un gruppo selezionato di computer in diverse subnet. Per altre informazioni sul funzionamento del proxy di riattivazione, vedere [Pianificare la riattivazione dei client](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Per configurare Riattivazione LAN per un sito per la versione 1806 e precedenti

 Per usare Riattivazione LAN, è necessario abilitarla per ogni sito di una gerarchia.

1. Nella console di Configuration Manager passare ad **Amministrazione > Configurazione del sito > Siti**.
2. Fare clic sul sito primario da configurare, quindi su **Proprietà**.
3. Fare clic nella scheda **Riattivazione LAN**, quindi configurare le opzioni necessarie per questo sito. Per il supporto del proxy di riattivazione, selezionare **Utilizza solo pacchetti di riattivazione** e **Unicast**. Per altre informazioni, vedere [Pianificare la riattivazione dei client](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Fare clic su **OK** e ripetere questa procedura per tutti i siti primari nella gerarchia.

![Abilitare Riattivazione LAN nelle proprietà del sito](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Per configurare le impostazioni client proxy di riattivazione

1. Nella console di Configuration Manager scegliere **Amministrazione > Impostazioni client**.
2. Fare clic su **Impostazioni client predefinite**, quindi su **Proprietà**.
3. Selezionare **Risparmio energia** e quindi scegliere **Sì** per **Abilitare il proxy di riattivazione**.
4. Riesaminare e, se necessario, configurare le altre impostazioni proxy di riattivazione. Per altre informazioni su queste impostazioni, vedere [Impostazioni di risparmio energia](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Fare clic su **OK** per chiudere la finestra di dialogo e su **OK** per chiudere la finestra di dialogo Impostazioni client predefinite.

È possibile utilizzare i seguenti report di riattivazione LAN per monitorare l'installazione e la configurazione del proxy di riattivazione:

- Riepilogo dello stato della distribuzione del proxy di riattivazione
- Dettagli dello stato della distribuzione del proxy di riattivazione

> [!TIP]
> Per verificare il funzionamento del proxy di riattivazione, verificare una connessione a un computer in sospensione. Ad esempio, connettersi a una cartella condivisa nel computer o tentare di connettersi al computer tramite Desktop remoto. Se si usa Direct Access, controllare il funzionamento dei prefissi IPv6 eseguendo le stesse verifiche per un computer in sospensione attualmente in Internet.
