---
title: Gestire punti di distribuzione
titleSuffix: Configuration Manager
description: Usare i punti di distribuzione per ospitare il contenuto distribuito a utenti e dispositivi.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1d93dd446a65fda0b259bb10e0c944780d41059
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347092"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Installare e configurare punti di distribuzione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Installando i punti di distribuzione di Configuration Manager è possibile ospitare i file di contenuto da distribuire a utenti e dispositivi. È anche possibile creare gruppi di punti di distribuzione per semplificare la gestione dei punti di distribuzione e la distribuzione di contenuto agli stessi.  

È possibile *installare un nuovo punto di distribuzione* usando l'installazione guidata. Per altre informazioni, vedere [Installare un punto di distribuzione](#bkmk_install). Per *gestire le proprietà di un punto di distribuzione esistente* è possibile modificare tali proprietà. Per altre informazioni, vedere [Configurare un punto di distribuzione](#bkmk_configs).

La maggior parte delle impostazioni del punto di distribuzione possono essere configurate con entrambi i metodi. Alcune impostazioni sono disponibili solo durante l'installazione o la modifica, ma non in entrambi i casi:  

- Impostazioni disponibili solo quando si installa un punto di distribuzione:  

    - **Consentire a Configuration Manager di installare IIS nel computer del punto di distribuzione**

    - **Configurare le impostazioni dello spazio dell'unità per il punto di distribuzione**  

- Impostazione disponibili solo quando si modificano le proprietà di un punto di distribuzione:  

    - **Gestire le relazioni del gruppo di punti di distribuzione**  

    - **Visualizzare il contenuto distribuito nel punto di distribuzione**  

    - **Configurare i limiti di velocità per i trasferimenti di dati ai punti di distribuzione**  

    - **Configurare le pianificazioni per i trasferimenti di dati ai punti di distribuzione**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a> Installare un punto di distribuzione  

Prima che il contenuto possa essere reso disponibile nei computer client, è necessario scegliere un server del sistema del sito come punto di distribuzione. Assegnare un punto di distribuzione ad almeno un [gruppo di limiti](boundary-groups.md#distribution-points) prima che i computer client locali possano usare tale punto di distribuzione come percorso di origine per il contenuto. Aggiungere il ruolo del punto di distribuzione a un server di sistema del sito nuovo oppure già esistente.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a> Prerequisiti

Quando si installa un nuovo punto di distribuzione, si usa un'installazione guidata che illustra le impostazioni disponibili. Prima di iniziare, tenere presente i prerequisiti seguenti:  

- È necessario disporre delle seguenti autorizzazioni di sicurezza per creare e configurare un punto di distribuzione:  

    - **Lettura** per l'oggetto **Punto di distribuzione**  

    - **Copia nel punto di distribuzione** per l'oggetto **Punto di distribuzione**  

    - **Modifica** per l'oggetto **Sito**  

    - **Gestisci certificati per distribuzione sistema operativo** per l'oggetto **Sito**  

- Installare Internet Information Services (IIS) nel server Windows che ospita il punto di distribuzione. In alternativa, Configuration Manager può eseguire l'installazione e la configurazione di IIS quando si installa il ruolo del sistema del sito.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a>Per installare un punto di distribuzione  

Usare questa procedura per aggiungere un nuovo punto di distribuzione. Per modificare la configurazione di un punto di distribuzione esistente, vedere la sezione [Configurare un punto di distribuzione](#bkmk_configs).  

Iniziare con la procedura per [installare i ruoli del sistema del sito](install-site-system-roles.md). Selezionare il ruolo di **punto di distribuzione** nella pagina **Selezione ruolo del sistema** della Creazione guidata server del sistema sito. Questa azione aggiunge alla procedura guidata le pagine seguenti:  

- [Punto di distribuzione](#bkmk_config-general)
- [Comunicazioni](#bkmk_config-comm)
- [Impostazioni unità](#bkmk_config-drive)
- [Punto di distribuzione pull](#bkmk_config-pull)
- [Impostazioni PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Convalida contenuto](#bkmk_config-valid)
- [Gruppi di limiti](#bkmk_config-boundary)

> [!Important]  
> Le impostazioni seguenti sono disponibili solo durante l'installazione di un punto di distribuzione:  
>
> - **Consentire a Configuration Manager di installare IIS nel computer del punto di distribuzione**  
>
> - **Configurare le impostazioni dello spazio dell'unità per il punto di distribuzione**  

Per altre informazioni sulle pagine della procedura guidata specifica per il ruolo di punto di distribuzione, vedere la sezione [Configurare un punto di distribuzione](#bkmk_configs). Se, ad esempio, si vuole installare il punto di distribuzione come [punto di distribuzione pull](#bkmk_config-pull), selezionare l'opzione **Abilita il pull di contenuti di questo punto di distribuzione da altri punti di distribuzione**. Eseguire quindi le configurazioni aggiuntive richieste dai punti di distribuzione pull.  

Dopo aver completato la Creazione guidata server del sistema sito, il ruolo del punto di distribuzione viene aggiunto al server di sistema del sito.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Gestire i gruppi di punti di distribuzione  

I gruppi di punti di distribuzione offrono un raggruppamento logico dei punti di distribuzione per la distribuzione del contenuto. È possibile usarli per gestire e monitorare il contenuto dei punti di distribuzione che si estendono su più siti da una posizione centrale. Tenere presente quanto segue:

- Aggiungere uno o più punti di distribuzione da qualsiasi sito nella gerarchia a un gruppo di punti di distribuzione.  

- Aggiungere un punto di distribuzione a più di un gruppo di punti di distribuzione.  

- Quando si distribuisce il contenuto a un gruppo di punti di distribuzione, Configuration Manager lo distribuisce a tutti i punti di distribuzione membri del gruppo.  

- Se si aggiunge un punto di distribuzione al gruppo dopo una distribuzione iniziale del contenuto, Configuration Manager distribuisce automaticamente il contenuto al nuovo membro del punto di distribuzione.  

- Associare una raccolta a un gruppo di punti di distribuzione. Quando si distribuisce il contenuto alla raccolta, Configuration Manager stabilisce quali gruppi sono associati alla raccolta. Il contenuto viene quindi distribuito a tutti i punti di distribuzione che sono membri di tali gruppi.  

    > [!NOTE]  
    > Dopo la distribuzione di contenuto a una raccolta, se si associa la raccolta a un nuovo gruppo di punti di distribuzione, sarà necessario ridistribuire il contenuto alla raccolta prima che il contenuto sia distribuito al nuovo gruppo di punti di distribuzione.  

Le sezioni seguenti elencano le procedure relative alle azioni seguenti per la gestione dei gruppi di punti di distribuzione:  

- [Creare e configurare un nuovo gruppo di punti di distribuzione](#bkmk_dpgroup-create)
- [Modificare un gruppo di punti di distribuzione esistente](#bkmk_dpgroup-modify)
- [Aggiungere i punti di distribuzione selezionati a gruppi di punti di distribuzione esistenti](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a>Per creare e configurare un nuovo gruppo di punti di distribuzione  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Gruppi di punti di distribuzione**.  

2. Nella barra multifunzione selezionare **Crea gruppo**.  

3. Nella finestra Crea nuovo gruppo di punti di distribuzione immettere il **Nome** e, facoltativamente, una **Descrizione** per il gruppo.  

4. Nella scheda **Membri** selezionare **Aggiungi**.  

5. Nella finestra Aggiungi punti di distribuzione selezionare uno o più punti di distribuzione da aggiungere come membri del gruppo. Scegliere quindi **OK**.  

6. Se necessario, passare alla scheda **Raccolte** della finestra Crea nuovo gruppo di punti di distribuzione e selezionare **Aggiungi**.  

7. Nella scheda Seleziona raccolte selezionare le raccolte da associare al gruppo di punti di distribuzione e quindi scegliere **OK**.  

8. Nella finestra Crea nuovo gruppo di punti di distribuzione scegliere **OK** per creare il gruppo.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Creare un nuovo gruppo da un punto di distribuzione esistente

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**. Selezionare uno o più punti di distribuzione da aggiungere a un nuovo gruppo di punti di distribuzione.  

2. Nella barra multifunzione selezionare **Aggiungi elementi selezionati** e quindi **Aggiungi elementi selezionati a nuovo gruppo di punti di distribuzione**.  

Questo processo popola automaticamente la scheda **Membri** della finestra Crea nuovo gruppo di punti di distribuzione con i server selezionati.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a>Per modificare un gruppo di punti di distribuzione esistente  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Gruppi di punti di distribuzione**.  

2. Selezionare il gruppo di punti di distribuzione esistente che si vuole modificare. Nella barra multifunzione selezionare **Proprietà**.  

3. Per associare nuove raccolte al gruppo, passare alla scheda **Raccolte** e scegliere **Aggiungi**. Selezionare le raccolte e scegliere **OK**.  

4. Per aggiungere nuovi punti di distribuzione al gruppo, passare alla scheda **Membri** e scegliere **Aggiungi**. Selezionare i punti di distribuzione e scegliere **OK**.  

5. Scegliere **OK** per salvare le modifiche apportate al gruppo di punti di distribuzione.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a>Per aggiungere i punti di distribuzione selezionati ai gruppi di punti di distribuzione esistenti  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**. Selezionare uno o più punti di distribuzione da aggiungere a un gruppo esistente.  

2. Nella barra multifunzione selezionare **Aggiungi elementi selezionati** e quindi **Aggiungi elementi selezionati a gruppi di punti di distribuzione esistenti**.  

3. In **Gruppi di punti di distribuzione disponibili** selezionare i gruppi ai quali aggiungere i punti di distribuzione selezionati come membri. Scegliere quindi **OK**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a> Riassegnare un punto di distribuzione

<!-- 1306937 -->

Molti clienti hanno infrastrutture di Configuration Manager di grandi dimensioni e stanno diminuendo i siti primari o secondari per semplificare il proprio ambiente. Per distribuire il contenuto ai client gestiti, questi clienti devono comunque mantenere i punti di distribuzione nelle succursali. Questi punti di distribuzione spesso includono più terabyte di contenuto. La distribuzione di questo contenuto ai server remoti è dispendiosa in termini di tempo e larghezza di banda di rete.

Questa funzionalità consente di riassegnare un punto di distribuzione a un altro sito primario senza ridistribuire il contenuto. Questa azione aggiorna l'assegnazione del sistema del sito mantenendo tutto il contenuto nel server. Se è necessario riassegnare più punti di distribuzione, eseguire prima questa azione su un singolo punto di distribuzione, quindi procedere con gli altri server uno alla volta.

> [!IMPORTANT]  
> Il server di destinazione può ospitare solo il ruolo del punto di distribuzione. Se il server del sistema del sito ospita un altro ruolo del server di Configuration Manager, ad esempio il punto di migrazione stato, non sarà possibile riassegnare il punto di distribuzione. Non è possibile riassegnare un punto di distribuzione cloud.

Prima di riassegnare un punto di distribuzione, aggiungere l'account del computer del server del sito di destinazione al gruppo Administrator locale nel server del punto di distribuzione di destinazione.

Per riassegnare un punto di distribuzione, seguire questa procedura:

1. Nella console di Configuration Manager connettersi al sito di amministrazione centrale.  

2. Passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**.  

3. Fare clic con il pulsante destro del mouse sul punto di distribuzione di destinazione e selezionare **Riassegna punto di distribuzione**.  

4. Selezionare il server e il codice del sito di destinazione a cui si vuole riassegnare il punto di distribuzione.  

Monitorare la riassegnazione come quando si aggiunge un nuovo ruolo. Il metodo più semplice consiste nell'aggiornare la visualizzazione della console dopo alcuni minuti. Aggiungere la colonna di codice del sito alla visualizzazione. Questo valore cambia quando Configuration Manager riassegna il server. Se si tenta di eseguire un'altra azione nel server di destinazione prima di aggiornare la visualizzazione della console, viene generato un errore "oggetto non trovato". Verificare che il processo sia stato completato e aggiornare la visualizzazione della console prima di avviare tutte le altre azioni nel server.

Dopo aver riassegnato un punto di distribuzione, aggiornare il certificato del server. Il nuovo server del sito crittografa di nuovo questo certificato usando la chiave pubblica e lo archivia nel database del sito. Per altre informazioni, vedere l'impostazione **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point** (Creare un certificato autofirmato o importare un certificato client di infrastruttura a chiave pubblica (PKI) per il punto di distribuzione) nella scheda [Generale](#bkmk_config-general) delle proprietà del punto di distribuzione.

- Per i certificati PKI, non è necessario creare un nuovo certificato. Importare lo stesso file con estensione pfx e immettere la password.  

- Per i certificati autofirmati, rettificare la data o l'ora della scadenza per aggiornarli.  

- Se non si aggiorna il certificato, il punto di distribuzione offre ancora contenuto, ma le funzioni seguenti non vengono eseguite:  

    - Messaggi di convalida del contenuto (il file distmgr.log non può decrittografare il certificato)  

    - Supporto PXE per i client  

### <a name="tips"></a>Suggerimenti

- Eseguire questa azione dal sito di amministrazione centrale. Questa procedura consente la replica nei siti primari.  

- Non distribuire il contenuto al server di destinazione e in seguito provare a riassegnarlo. La distribuzione di attività in corso potrebbe non riuscire durante il processo di riassegnazione. Riprovare in seguito.  

- Se il server è anche un client di Configuration Manager, assicurarsi di riassegnare anche il client al nuovo sito primario. Questo passaggio è particolarmente importante per i punti di distribuzione pull, che usano i componenti client per scaricare il contenuto.  

- Questo processo rimuove il punto di distribuzione dal gruppo di limiti predefinito del sito precedente. Se necessario, aggiungerlo manualmente al gruppo di limiti predefinito del nuovo sito. Tutte le altre assegnazioni di gruppi di limiti rimangono invariate.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a> Modalità di manutenzione

<!--3555754-->

A partire dalla versione 1902, è possibile impostare un punto di distribuzione in modalità di manutenzione. Abilitare la modalità di manutenzione quando si installano aggiornamenti software o quando si modifica l'hardware del server.

Quando il punto di distribuzione è in modalità di manutenzione, ha i comportamenti seguenti:

- Il sito non distribuisce nessun contenuto al punto di distribuzione.  

- I punti di gestione non restituiscono la posizione del punto di distribuzione ai client.

- Quando si aggiorna il sito, un punto di distribuzione in modalità di manutenzione viene comunque aggiornato.

- Le proprietà del punto di distribuzione sono di sola lettura. Ad esempio non è possibile modificare il certificato o aggiungere gruppi di limiti.  

- Qualsiasi operazione pianificata, ad esempio la convalida del contenuto, viene eseguita con la pianificazione esistente.

Prestare attenzione quando si abilita la modalità di manutenzione su più punti di distribuzione. Questa azione può influire sulle prestazioni degli altri punti di distribuzione. A seconda delle configurazioni dei gruppi di limiti, i client potrebbero registrare tempi di download più lunghi o non essere in grado di scaricare il contenuto.

La modalità di manutenzione non deve essere uno stato a lungo termine per qualsiasi punto di distribuzione. Per le azioni con una durata prolungata, è consigliabile rimuovere prima il ruolo del punto di distribuzione.

> [!NOTE]
> Quando il punto di distribuzione è in modalità di manutenzione, non eseguire le azioni seguenti:<!-- SCCMDocs-pr #4699 -->
>
> - Rimuovere il ruolo
> - Riassegnare un punto di distribuzione

### <a name="enable-maintenance-mode"></a>Abilitare la modalità di manutenzione

Per impostare un punto di distribuzione sulla modalità di manutenzione, l'account utente richiede l'autorizzazione **Modifica** per la classe **Sito**. I ruoli predefiniti **Amministratore infrastruttura** e **Amministratore completo**, ad esempio, hanno questa autorizzazione.<!-- SCCMDocs-pr issue #3407 -->

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**.  

2. Selezionare il nodo **Punti di distribuzione**.  

3. Selezionare il punto di distribuzione di destinazione e scegliere **Abilita la modalità manutenzione** nella barra multifunzione.  

Per visualizzare lo stato corrente dei punti di distribuzione, aggiungere la colonna "Modalità manutenzione" al nodo **Punti di distribuzione** nella console.

Per altre informazioni sull'automazione di questo processo con Configuration Manager SDK, vedere [Metodo SetDPMaintenanceMode nella classe SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a> Configurare un punto di distribuzione  

I singoli punti di distribuzione supportano un'ampia gamma di configurazioni diverse. Tuttavia, non tutti i tipi di punto di distribuzione supportano tutte le configurazioni. Ad esempio, i punti di distribuzione cloud non supportano le distribuzioni abilitate per PXE o per multicast. Per altre informazioni sui limiti specifici, vedere gli articoli seguenti:  

- [Usare un punto di distribuzione cloud](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Usare un punto di distribuzione pull](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

Le sezioni seguenti descrivono che è possibile selezionare quando si [installa un nuovo punto di distribuzione](#bkmk_install-procedure) oppure si [modificano le proprietà di un punto di distribuzione esistente](#bkmk_change-procedure):  

- [Impostazioni generali](#bkmk_config-general)
- [Comunicazioni](#bkmk_config-comm)
- [Impostazioni unità](#bkmk_config-drive)
- [Impostazioni del firewall](#bkmk_firewall)
- [Punto di distribuzione pull](#bkmk_config-pull)
- [Impostazioni PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Convalida contenuto](#bkmk_config-valid)
- [Gruppi di limiti](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a> Per modificare un punto di distribuzione

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**.  

2. Selezionare il punto di distribuzione da configurare. Nella barra multifunzione scegliere **Proprietà**.  

3. Quando si modificano le proprietà del punto di distribuzione, usare le informazioni contenute nelle sezioni seguenti.  

4. Dopo aver apportato le modifiche desiderate, selezionare **OK** per salvare le impostazioni e chiudere la finestra delle proprietà del punto di distribuzione.  

### <a name="general"></a><a name="bkmk_config-general"></a> Generale  

> [!Note]  
> Nella versione 1902 e precedenti, questa pagina contiene impostazioni aggiuntive per HTTP/HTTPS e i certificati. A partire dalla versione 1906, queste impostazioni sono disponibili nella pagina [Comunicazioni](#bkmk_config-comm).

Le impostazioni seguenti si trovano nella pagina **Punto di distribuzione** della Creazione guidata server del sistema sito e nella scheda **Generali** della finestra delle proprietà del punto di distribuzione:  

- **Descrizione**: descrizione facoltativa del ruolo del punto di distribuzione.  

- **Installa e configura IIS, se richiesto da Configuration Manager**: se IIS non è già installato nel server, Configuration Manager lo installa e lo configura. IIS deve essere installato su tutti i punti di distribuzione. Se IIS non è installato nel server e non viene selezionata questa impostazione, per poter installare correttamente il punto di distribuzione è necessario installare prima IIS.  

    > [!NOTE]  
    > Questa opzione è disponibile solo nella pagina **Punto di distribuzione** della Creazione guidata server del sistema sito e soltanto quando si [installa un nuovo punto di distribuzione](#bkmk_install-procedure).  

- **Abilita e configura BranchCache per questo punto di distribuzione**: scegliere questa impostazione per consentire a Configuration Manager di configurare Windows BranchCache nel server del punto di distribuzione. Per altre informazioni, vedere [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Regola la velocità del download per usare la larghezza di banda di rete inutilizzata (Windows LEDBAT)**<!--1358112-->: a partire dalla versione 1806, abilitare punti di distribuzione per l'uso del controllo di congestione della rete. Per altre informazioni, vedere [LEDBAT Windows](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Requisiti minimi per il supporto di LEDBAT:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager versione 1806 (aggiornamento pubblico)  

        - Windows Server versione 1709 o successiva  

    - Configuration Manager versione 1806 con aggiornamento cumulativo (4462978) o versione successiva  

        - Windows Server versione 1709 o successiva
        - Windows Server 2016 con gli aggiornamenti seguenti:
           - Aggiornamento cumulativo KB4132216, rilasciato il 21 giugno 2018 o un aggiornamento cumulativo successivo.
           - Aggiornamento dello stack di manutenzione KB4284833, rilasciato il 18 maggio 2018 o un aggiornamento dello stack di manutenzione successivo.

    - Configuration Manager versione 1810 o successiva

        - Windows Server versione 1709 o successiva
        - Windows Server 2016 con gli aggiornamenti seguenti:
           - Aggiornamento cumulativo KB4132216, rilasciato il 21 giugno 2018 o un aggiornamento cumulativo successivo.
           - Aggiornamento dello stack di manutenzione KB4284833, rilasciato il 18 maggio 2018 o un aggiornamento dello stack di manutenzione successivo.
        - Windows Server 2019  

- **Abilita questo punto di distribuzione per il contenuto pre-installato**: questa impostazione consente di aggiungere contenuto al server prima di distribuire il software. Poiché si trovano già nella raccolta, i file di contenuto non vengono trasferiti attraverso la rete quando si distribuisce il software. Per altre informazioni, vedere [Contenuto pre-installato](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).  

- **Abilita l'uso di questo punto di distribuzione come server di Microsoft Connected Cache**: a partire dalla versione 1906, è possibile installare un server di Microsoft Connected Cache nei punti di distribuzione. Memorizzando nella cache questo contenuto in locale, i client possono trarre vantaggio dalla funzionalità di Ottimizzazione recapito, tuttavia è possibile contribuire a proteggere i collegamenti WAN. Per altre informazioni, inclusa la descrizione delle impostazioni aggiuntive, vedere [Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a> Comunicazioni

> [!Note]  
> A partire dalla versione 1906, le impostazioni seguenti sono disponibili nella scheda **Comunicazioni**. Nella versione 1902 e precedenti, queste impostazioni sono disponibili nella scheda [Generale](#bkmk_config-general).

Le impostazioni seguenti si trovano nella pagina **Comunicazioni** della Creazione guidata server del sistema sito e nella finestra delle proprietà del punto di distribuzione:  

- **Configure how client devices communicate with the distribution point** (Configurare in che modo i dispositivi client comunicano con questo punto di distribuzione): esistono vantaggi e svantaggi associati all'uso di **HTTP** o **HTTPS**. Per altre informazioni, vedere [Procedure di sicurezza consigliate per la gestione del contenuto](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

- **Consenti connessione anonima dei client**: questa impostazione permette di specificare se il punto di distribuzione consentirà connessioni anonime dai client di Configuration Manager alla raccolta contenuto.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Creare un certificato autofirmato o importare un certificato client PKI**: Configuration Manager usa questo certificato per gli scopi seguenti:  

    - Consente l'autenticazione tra il punto di distribuzione e un punto di gestione prima che il punto di distribuzione invii messaggi di stato.  

    - Quando si seleziona **Abilita supporto PXE per i client** nella pagina **Impostazioni PXE**, il punto di distribuzione invia il certificato ai computer avviati da PXE, che lo usano durante il processo di distribuzione del sistema operativo per connettersi a un punto di gestione.  

    Se tutti i punti di gestione nel sito sono configurati per il protocollo HTTP, selezionare l'opzione **Crea certificato autofirmato**. Quando i punti di gestione sono configurati per HTTPS, usare l'opzione **Importa certificato** da PKI.  

    Per importare il certificato, individuare un file Public Key Cryptography Standard (PKCS #12) valido. Questo file, con estensione pfx o cer, dispone del certificato PKI dotate dei requisiti seguenti per Configuration Manager:  

    - Lo scopo designato include l'autenticazione client.  

    - La chiave privata deve essere abilitata per l'esportazione.  

    > [!TIP]  
    > Non sono previsti requisiti specifici per l'oggetto certificato o il nome alternativo oggetto (SAN). Se necessario, usare lo stesso certificato per più punti di distribuzione.  

    Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    Per un esempio di distribuzione di questo certificato, vedere [Distribuire il certificato client per punti di distribuzione](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a>Impostazioni unità  

> [!NOTE]  
> Queste opzioni sono disponibili solo quando si installa un nuovo punto di distribuzione.  

Specificare le impostazioni unità per il punto di distribuzione. Configurare fino a due unità disco per la raccolta contenuto e due unità disco per la condivisione dei pacchetti. Configuration Manager può usare unità aggiuntive nel caso in cui le prime due raggiungano il limite di spazio riservato nell'unità configurata. Nella pagina **Impostazioni unità** è possibile configurare la priorità per le unità disco e la quantità di spazio disponibile su disco da conservare su ciascuna unità disco.  

- **Spazio riservato nell'unità (MB)** : questo valore determina la quantità di spazio disponibile in un'unità prima che Configuration Manager scelga un'altra unità e continui il processo di copia su tale unità. I file di contenuto possono estendersi su più unità.  

- **Percorsi contenuto**: specificare i percorsi per la condivisione di pacchetti e raccolte di contenuti su questo punto di distribuzione. Per impostazione predefinita, tutti i percorsi contenuto sono impostati su **Automatico**. Configuration Manager copia i contenuti nel percorso del contenuto principale finché la quantità di spazio libero raggiunge il valore specificato per **Riserva spazio su disco (MB)** . Quando si seleziona **Automatico**, Configuration Manager imposta il percorso primario del contenuto sull'unità disco con più spazio al momento dell'installazione. I percorsi secondari vengono quindi assegnati all'unità disco con la seconda maggiore quantità di spazio disponibile. Quando i percorsi primario e secondario raggiungono il limite di spazio riservato, Configuration Manager seleziona un'altra unità disponibile con la maggiore quantità di spazio libero e continua il processo di copia.  

> [!Tip]  
> Per evitare l'installazione di Configuration Manager in un'unità specifica, creare un file vuoto denominato **no_sms_on_drive.sms** e copiarlo nella cartella radice dell'unità prima dell'installazione del punto di distribuzione.  

Per altre informazioni, vedere [Raccolta contenuto](../../../plan-design/hierarchy/the-content-library.md).

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a> Impostazioni del firewall

Il punto di distribuzione deve avere le regole in ingresso seguenti configurate nel firewall di Windows:

- Strumentazione gestione Windows (DCOM-In)
- Strumentazione gestione Windows (WMI-In)

Senza queste regole i client visualizzeranno l'errore 0x801901F4 in DataTransferService.log durante il tentativo di scaricare il contenuto.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a> Punto di distribuzione pull  

Scegliendo l'opzione **Abilita il pull di contenuti di questo punto di distribuzione da altri punti di distribuzione**, si ottiene un punto di distribuzione pull. Viene modificato il comportamento con il quale il punto di distribuzione ottiene il contenuto distribuito dall'utente. Per altre informazioni, vedere [Usare un punto di distribuzione pull](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

Per ogni punto di distribuzione pull configurato, specificare uno o più punti di distribuzione di origine dai quali viene ottenuto il contenuto:  

- Scegliere **Aggiungi** e quindi selezionare uno o più punti di distribuzione disponibili come origine.  

- Usare i pulsanti freccia per modificare la priorità. Quando si tenta di trasferire il contenuto, tale priorità rappresenta l'ordine con cui il punto di distribuzione pull contatta i punti di distribuzione di origine. Quelli con il valore più basso vengono contattati per primi.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a> PXE  

Specificare se abilitare PXE nel punto di distribuzione. Usare PXE per avviare le distribuzioni del sistema operativo nei client. Per altre informazioni su come usare PXE in Configuration Manager, vedere [Usare PXE per distribuire Windows in rete](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

Quando si abilita PXE, Configuration Manager installa i Servizi di distribuzione Windows (WDS) nel server, se necessario. WDS è il servizio che esegue l'avvio di PXE per installare i sistemi operativi. Dopo aver completato la procedura guidata per creare il punto di distribuzione, Configuration Manager installa un provider in WDS che usa le funzioni di avvio di PXE.

A partire dalla versione 1806 è possibile abilitare PXE in un punto di distribuzione senza WDS.

Selezionare l'opzione **Abilita supporto PXE per i client** e configurare le impostazioni seguenti:  

> [!Note]  
> Selezionare **Sì** nella finestra di dialogo **Controllare le porte richieste per PXE** per confermare che si vuole abilitare PXE. Configuration Manager configura automaticamente le porte predefinite nel firewall di Windows. Se si usa un firewall diverso è necessario configurare manualmente le porte.  
>
> Se WDS e DHCP sono installati nello stesso server, configurare WDS per l'ascolto su una porta diversa. Per impostazione predefinita, DHCP è in ascolto sulla stessa porta. Per altre informazioni, vedere [Considerazioni in presenza di Servizi di distribuzione Windows e DHCP nello stesso server](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

- **Consenti a questo punto di distribuzione di rispondere alle richieste PXE in ingresso**: specificare se si vuole abilitare WDS in modo che risponda alle richieste di servizio PXE. Usare questa impostazione per attivare e disattivare il servizio senza rimuovere la funzionalità PXE dal punto di distribuzione.  

- **Abilita supporto per computer sconosciuti**: specificare se si vuole abilitare il supporto per i computer non gestiti da Configuration Manager. Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

- **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**: A partire dalla versione 1806, con questa opzione è possibile abilitare un risponditore PXE nel punto di distribuzione, che non richiede Servizi di distribuzione Windows (WDS). Il risponditore PXE supporta le reti IPv6. Se si abilita questa opzione in un punto di distribuzione che già supporta PXE, Configuration Manager sospende l'esecuzione del servizio WDS. Se si disabilita questa opzione ma si lascia selezionata l'opzione **Abilita supporto PXE per i client**, il punto di distribuzione abilita di nuovo Servizi di distribuzione Windows.<!--1357580-->  

    > [!Note]  
    > Nella versione 1810 e precedenti non è supportato l'uso del risponditore PXE senza WDS nei server che eseguono anche un server DHCP.
    >
    > A partire dalla versione 1902, quando si abilita un risponditore PXE in un punto di distribuzione senza i Servizi di distribuzione Windows, è ora possibile abilitarlo sullo stesso server del servizio DHCP. <!--3734270-->  

- **Richiedi password quando i computer usano PXE**: per una maggiore sicurezza delle distribuzioni PXE, specificare una password complessa.  

- **Affinità utente dispositivo**: specificare come associare gli utenti al computer di destinazione tramite il punto di distribuzione per le distribuzioni PXE. Scegliere una delle seguenti opzioni:  

  - **Consenti affinità utente dispositivo con approvazione automatica**: scegliere questa impostazione per associare automaticamente gli utenti al computer di destinazione senza attendere l'approvazione.  

  - **Consenti approvazione amministratore in sospeso per affinità utente dispositivo**: scegliere questa impostazione per attendere l'approvazione di un utente amministratore prima che gli utenti siano associati al computer di destinazione.  

  - **Non consentire affinità utente dispositivo**: scegliere questa impostazione per specificare che gli utenti non sono associati al computer di destinazione. È l'impostazione predefinita.  

    Per altre informazioni sull'affinità utente dispositivo, vedere l'argomento [Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Collegare utenti e dispositivi con l'affinità utente dispositivo in System Center Configuration Manager).  

- **Interfacce di rete**: specificare se il punto di distribuzione risponde alle richieste PXE da tutte le interfacce di rete o da interfacce di rete specifiche. Se il punto di distribuzione risponde a specifiche interfacce di rete, è necessario fornire l'indirizzo MAC per ogni interfaccia di rete.  

    > [!Note]  
    > Quando si modifica l'interfaccia di rete, riavviare il servizio WDS per verificare che la configurazione venga salvata in modo corretto. A partire dalla versione 1806, quando si usa il servizio risponditore PXE è necessario riavviare il **servizio risponditore PXE di ConfigMgr** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Specificare il ritardo risposta del server PXE (secondi)** : specificare il tempo di attesa in secondi del punto di distribuzione abilitato per PXE prima che risponda alle richieste dei computer quando vengono usati più server PXE. Per impostazione predefinita, il punto di distribuzione abilitato per PXE di Configuration Manager risponde immediatamente.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a> Multicast  

Specificare se abilitare multicast nel punto di distribuzione. Le distribuzioni multicast consentono di risparmiare larghezza di banda inviando contemporaneamente i dati a più client di Configuration Manager. Senza multicast, il server invia una copia dei dati a ogni client in una connessione separata. Per altre informazioni sull'uso del multicast per la distribuzione di sistemi operativi, vedere [Usare il multicast per distribuire Windows in rete](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

Quando si abilita il multicast, Configuration Manager installa Servizi di distribuzione Windows (WDS) nel server, se necessario.  

Selezionare l'opzione **Abilita multicast per inviare contemporaneamente dati a più client** e configurare le impostazioni seguenti:  

- **Account di connessione multicast**: specificare l'account da usare quando si configurano le connessioni del database di Configuration Manager per il multicast. Per altre informazioni, vedere [Account di connessione multicast](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Impostazioni indirizzo multicast**: specificare gli indirizzi IP usati per l'invio dei dati ai computer di destinazione. Per impostazione predefinita, l'indirizzo IP viene ottenuto da un server DHCP abilitato per la distribuzione di indirizzi multicast. A seconda dell'ambiente di rete, è possibile specificare un intervallo di indirizzi IP compreso tra 239.0.0.0 e 239.255.255.255.  

    > [!IMPORTANT]  
    > Gli indirizzi IP configurati devono essere accessibili ai computer di destinazione che richiedono l'immagine del sistema operativo. Verificare che i router e firewall consentano il traffico multicast tra il computer di destinazione e il punto di distribuzione.  

- **Intervallo di porte UDP per multicast**: specificare l'intervallo di porte UDP usate per inviare dati ai computer di destinazione.  

    > [!IMPORTANT]  
    > Le porte UDP devono essere accessibili ai computer di destinazione che richiedono l'immagine del sistema operativo. Verificare che i router e firewall consentano il traffico multicast tra il computer di destinazione e il server del sito.  

- **Numero massimo di client**: specificare il numero massimo di computer di destinazione per cui è possibile scaricare l'immagine del sistema operativo da questo punto di distribuzione.  

- **Abilita multicast pianificato**: specificare come Configuration Manager esegue i controlli per avviare la distribuzione dei sistemi operativi ai computer di destinazione. Configurare le opzioni seguenti:  

    - **Ritardo avvio sessione (minuti)** : specificare il numero di minuti che Configuration Manager deve attendere prima di rispondere alla prima richiesta di distribuzione.  

    - **Dimensione minima sessione (client)** : specificare il numero di richieste che Configuration Manager deve ricevere prima di avviare la distribuzione del sistema operativo.  

> [!IMPORTANT]  
> A partire dalla versione 1806, per abilitare e configurare il multicast nella scheda **Multicast** delle proprietà del punto di distribuzione, il punto di distribuzione deve usare il servizio WDS.  
>
> - Se si seleziona **Abilita supporto PXE per i client** e **Abilita multicast per inviare contemporaneamente dati a più client**, non è possibile selezionare anche **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**.  
>
> - Se si seleziona **Abilita supporto PXE per i client** e **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**, non è possibile selezionare anche **Abilita multicast per inviare contemporaneamente dati a più client**.  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a> Relazioni del gruppo  

> [!NOTE]  
> Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente.  

Gestire i gruppi di punti di distribuzione di cui il punto di distribuzione è un membro.  

Per aggiungere questo punto di distribuzione come membro di un gruppo di punti di distribuzione esistente, scegliere **Aggiungi**. Nella finestra Aggiungi ai gruppi di punti di distribuzione selezionare un gruppo quindi scegliere **OK**.  

Per rimuovere il punto di distribuzione da un gruppo di punti di distribuzione, selezionare il gruppo dall'elenco e quindi scegliere **Rimuovi**. La rimozione del punto di distribuzione da un gruppo di punti di distribuzione non rimuove alcun contenuto dal punto di distribuzione.

### <a name="content"></a><a name="bkmk_config-content"></a> Contenuto  

> [!NOTE]  
> Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente.  

Gestire il contenuto distribuito al punto di distribuzione. Selezionare un pacchetto di distribuzione dall'elenco ed eseguire le azioni seguenti:  

- **Convalida**: avvia il processo per convalidare l'integrità dei file di contenuto nel software. Per visualizzare i risultati del processo di convalida del contenuto, nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione** e quindi scegliere il nodo **Stato contenuto**. Per altre informazioni, vedere [Convalidare il contenuto](deploy-and-manage-content.md#validate-content).  

- **Ridistribuisci**: copia nel punto di distribuzione tutti i file di contenuto del software selezionato e sovrascrive i file esistenti. Questa operazione viene in genere usata per ripristinare i file di contenuto. Per altre informazioni, vedere [Ridistribuire il contenuto](deploy-and-manage-content.md#redistribute-content).  

- **Rimuovi**: rimuove i file di contenuto del software dal punto di distribuzione. Per altre informazioni, vedere [Rimuovere il contenuto](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a> Convalida contenuto  

Impostare una pianificazione per convalidare l'integrità dei file di contenuto nel punto di distribuzione. Quando si abilita la convalida del contenuto in base a una pianificazione, Configuration Manager avvia il processo all'orario pianificato Verifica tutto il contenuto nel punto di distribuzione in base alla classe SMS_PackagesInContLib SCCMDP locale. È inoltre possibile configurare la priorità di convalida del contenuto. Per impostazione predefinita, la priorità è impostata su **Minima**. All'incremento della priorità può corrispondere un aumento dell'uso del disco e del processore sul server durante il processo di convalida, ma il processo è più rapido.

Per visualizzare i risultati del processo di convalida del contenuto, nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione** e quindi scegliere il nodo **Stato contenuto**. Viene visualizzato il contenuto per ogni tipo di software, ad esempio applicazione, pacchetto di aggiornamento software e immagine di avvio.  

> [!WARNING]  
> Anche se la pianificazione della convalida del contenuto viene specificata usando l'ora locale per il computer, la pianificazione viene visualizzata nella console di Configuration Manager in formato UTC.  

Per altre informazioni, vedere [Convalidare il contenuto](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a> Gruppi di limiti  

Gestire i gruppi di limiti ai quali viene assegnato il punto di distribuzione. Aggiungere il punto di distribuzione ad almeno un gruppo di limiti. Durante la distribuzione del contenuto, i client devono trovarsi in un gruppo di limiti associato a un punto di distribuzione per usare tale punto di distribuzione come percorso di origine per il contenuto.

Configurare il gruppo di limiti *Relazioni* che definisce quando e in quali gruppi di limiti un client può eseguire il fallback per individuare il contenuto. Per altre informazioni, vedere [Gruppi di limiti](boundary-groups.md).

Scegliere **Aggiungi** e selezionare dall'elenco un gruppo di limiti esistente.

Per creare un nuovo gruppo di limiti per il punto di distribuzione, scegliere **Crea**. Per altre informazioni su come creare e configurare un gruppo di limiti, vedere [Procedure per i gruppi di limiti](boundary-group-procedures.md).

Quando si modificano le proprietà di un punto di distribuzione installato precedentemente, selezionare l'opzione in modo da **abilitare la distribuzione su richiesta**. Questa opzione consente a Configuration Manager di distribuire automaticamente contenuto a questo server su richiesta del client. Per altre informazioni, vedere [Distribuzione di contenuto su richiesta](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="schedule"></a><a name="bkmk_config-sched"></a> Pianificazione  

> [!NOTE]  
> Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente.
>
> Questa scheda è disponibile solo quando si modificano le proprietà di un punto di distribuzione remoto rispetto al computer del server del sito.  

Configurare una pianificazione che stabilisca quando Configuration Manager può trasferire i dati al punto di distribuzione. È possibile limitare i dati per priorità o chiudere la connessione per periodi di tempo selezionati.

Per limitare i dati, selezionare il periodo di tempo nella griglia e quindi scegliere una delle impostazioni seguenti per **Disponibilità**:  

- **Apri per tutte le proprietà**: specifica che Configuration Manager deve inviare i dati al punto di distribuzione senza restrizioni. Questo è l'impostazione predefinita per tutti i periodi di tempo.  

- **Consenti priorità media e alta**: specifica che Configuration Manager deve inviare al punto di distribuzione solo i dati con priorità media e alta.  

- **Consenti solo priorità alta**: specifica che Configuration Manager deve inviare al punto di distribuzione solo i dati con priorità alta.  

- **Chiusa**: specifica che Configuration Manager non deve inviare dati al punto di distribuzione.  

Configurare la **Priorità di distribuzione** del software nella scheda **Impostazioni distribuzione** delle proprietà del software.

> [!IMPORTANT]  
> La pianificazione è basata sul fuso orario del sito di invio, non del punto di distribuzione.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a> Limiti di velocità  

> [!NOTE]  
> Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente.  
>
> Questa scheda è disponibile solo quando si modificano le proprietà di un punto di distribuzione remoto rispetto al computer del server del sito.  

Configurare i limiti di velocità per controllare la larghezza di banda di rete usata da Configuration Manager durante il trasferimento di contenuto al punto di distribuzione. È possibile scegliere una delle opzioni seguenti:  

- **Illimitato per l'invio a questa destinazione**: Configuration Manager invia il contenuto al punto di distribuzione senza restrizioni in termini di limiti di velocità. È l'impostazione predefinita.  

- **Modalità a impulsi**: specifica la dimensione dei blocchi di dati inviati dal server del sito al punto di distribuzione. È inoltre possibile specificare un ritardo tra l'invio di ogni blocco di dati. Usare questa opzione quando è necessario inviare i dati attraverso una connessione di rete con larghezza di banda molto bassa al punto di distribuzione. È possibile, ad esempio, che si sia vincolati a inviare 1 KB di dati ogni cinque secondi, indipendentemente dalla velocità del collegamento o dall'utilizzo in un determinato momento.  

- **Limitato alle velocità di trasferimento massime specificate per ora**: specificare questa impostazione se si vuole che un sito invii i dati a un punto di distribuzione usando solo la percentuale di tempo configurata. Quando si usa questa opzione, Configuration Manager non identifica la larghezza di banda disponibile della rete, ma divide in intervalli il periodo di tempo in cui può inviare i dati. Il server invia i dati per un breve periodo di tempo, seguito da periodi in cui i dati non vengono inviati. Se, ad esempio, l'opzione **Limita larghezza di banda disponibile** è impostata su **50%** , Configuration Manager trasmette i dati per un periodo di tempo seguito da un periodo di tempo uguale in cui non viene inviato alcun dato. Non vengono gestite né la quantità effettiva di dati né la dimensione del blocco di dati, ma solo la quantità di tempo durante il quale avviene l'invio dei dati.  
