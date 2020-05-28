---
title: Installare punti di distribuzione basati sul cloud
titleSuffix: Configuration Manager
description: Usare questa procedura per configurare un punto di distribuzione cloud in Configuration Manager.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35379aed71544a25a98ec4dfa421be70c1bae851
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427691"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Installare un punto di distribuzione cloud per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> È stata modificata l'implementazione per la condivisione del contenuto da Azure. Usare un gateway di gestione cloud abilitato per il contenuto abilitando l'opzione **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure**. Per altre informazioni, vedere [Modify a CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg) (Modificare un gateway di gestione cloud).
>
> Non sarà possibile creare un punto di distribuzione cloud tradizionale in futuro. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

In questo articolo è illustrata in dettaglio la procedura per installare un punto di distribuzione cloud di Configuration Manager in Microsoft Azure. Include le sezioni seguenti:

- [Prima di iniziare](#bkmk_before)
- [Configurare](#bkmk_setup)
- [Configurare DNS](#bkmk_dns)
- [Configurare il proxy server](#bkmk_proxy)
- [Distribuire il contenuto e configurare i client](#bkmk_client)
- [Gestire e monitorare](#bkmk_monitor)
- [Modifica](#bkmk_modify)
- [Risoluzione dei problemi avanzata](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> Prima di iniziare

Per iniziare, leggere l'articolo [Usare un punto di distribuzione cloud](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md), in cui viene descritto come pianificare e progettare i punti di distribuzione cloud.

Usare l'elenco di controllo seguente per assicurarsi di avere le informazioni e i prerequisiti necessari per la creazione di un punto di distribuzione cloud:  

- Il server del sito può connettersi ad Azure. Se la rete usa un proxy, [configurare il ruolo del sistema del sito](#bkmk_proxy).  

- **Ambiente Azure** da usare. Ad esempio il cloud pubblico di Azure o il cloud di Azure Governo degli Stati Uniti.  

- A partire dalla versione 1806 (*versione consigliata*), usare la **distribuzione di Azure Resource Manager**. I requisiti della distribuzione sono i seguenti:<!--1322209-->  

    - Integrazione con [Azure Active Directory](azure-services-wizard.md) per **Gestione cloud**. L'individuazione utenti di Azure AD non è necessaria.  

    - **ID sottoscrizione** di Azure.  

    - **Gruppo di risorse** di Azure.  

    - Durante la procedura guidata un **account amministratore della sottoscrizione** deve eseguire l'accesso.  

- Un **certificato di autenticazione server**, esportato come file PFX.  

- Un **nome di servizio** univoco globale per il punto di distribuzione cloud.  

    > [!TIP]  
    > Prima di richiedere il certificato di autenticazione server che usa questo nome di servizio, verificare che il nome di dominio di Azure desiderato sia univoco, ad esempio *WallaceFalls.CloudApp.Net*.
    >
    > 1. Accedere al [portale di Azure](https://portal.azure.com).
    > 1. Selezionare **Tutte le risorse** e quindi **Aggiungi**.
    > 1. Cercare **Servizio cloud**. Selezionare **Crea**.
    > 1. Digitare il prefisso desiderato nel campo **Nome DNS**, ad esempio *WallaceFalls*. L'interfaccia indica se il nome di dominio è disponibile o se è già in uso in un altro servizio.
    >
    > Non creare il servizio nel portale, ma usare questo processo solo per verificare la disponibilità del nome.

- **Area** di Azure per questa distribuzione.  

- Se occorre ancora usare la **distribuzione classica del servizio** di Azure in Configuration Manager versione 1810 o precedenti, sono necessari i requisiti seguenti:  

    > [!Important]  
    > A partire dalla versione 1810, le distribuzioni classiche del servizio in Azure sono deprecate in Configuration Manager. Iniziare a usare le distribuzioni di Azure Resource Manager per il punto di distribuzione cloud. Per altre informazioni, vedere [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > A partire da Configuration Manager versione 1902, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze del punto di distribuzione cloud.<!-- 3605704 -->

    - **ID sottoscrizione** di Azure.  

    - Un **certificato di gestione** di Azure, esportato come file CER e PFX. Un amministratore della sottoscrizione di Azure deve aggiungere il certificato di gestione CER alla sottoscrizione nel [portale di Azure](https://portal.azure.com).  

### <a name="branchcache"></a>BranchCache

Per consentire l'uso di Windows BranchCache a un punto di distribuzione cloud, installare la funzionalità BranchCache nel server del sito.<!-- SCCMDocs-pr#4054 -->

- Se il server del sito ha il ruolo del sistema del sito di punto di distribuzione locale, configurare l'opzione nelle proprietà del ruolo per **abilitare e configurare BranchCache**. Per altre informazioni, vedere [Configurare un punto di distribuzione](install-and-configure-distribution-points.md#bkmk_config-general).

- Se il server del sito non ha il ruolo di punto di distribuzione, installare la funzionalità BranchCache in Windows. Per altre informazioni, vedere [Installare la funzionalità BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Se è già stato distribuito contenuto a un punto di distribuzione cloud e quindi si decide di abilitare BranchCache, installare prima di tutto la funzionalità. Ridistribuire quindi il contenuto nel punto di distribuzione cloud.

> [!NOTE]  
> In Configuration Manager versione 1810 e versioni precedenti, in presenza di più di un punto di distribuzione cloud, è necessario impostare manualmente la passphrase della chiave BranchCache. Per altre informazioni, vedere l'[articolo del supporto tecnico Microsoft KB 4458143](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a> Configurare  

Eseguire questa procedura nel sito per ospitare il punto di distribuzione cloud, come stabilito nella [progettazione](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare **Punti di distribuzione del cloud**. Nella barra multifunzione selezionare **Crea punto di distribuzione cloud**.  

2. Nella pagina **Generale** della procedura guidata per la creazione del punto di distribuzione cloud, configurare le impostazioni seguenti:  

    1. Specificare prima l'**ambiente di Azure**.  

    2. A partire dalla versione 1806 (*versione consigliata*), selezionare **Distribuzione di Azure Resource Manager** come metodo di distribuzione. Selezionare **Accedi** per eseguire l'autenticazione con un account amministratore della sottoscrizione di Azure. La procedura guidata compila automaticamente i campi rimanenti in base alle informazioni archiviate durante il prerequisito di integrazione di Azure AD. Se si hanno più sottoscrizioni, selezionare l'**ID sottoscrizione** di quella che si vuole usare.  

    > [!Note]  
    > A partire dalla versione 1810, le distribuzioni classiche del servizio in Azure sono deprecate in Configuration Manager.
    >
    > Se è necessario usare una distribuzione classica del servizio, selezionare l'opzione in questa pagina. Immettere l'**ID sottoscrizione** di Azure. Quindi selezionare **Sfoglia** e scegliere il file PFX del certificato di gestione di Azure.  

3. Selezionare **Avanti**. Attendere che il sito completi il test della connessione ad Azure.  

4. Nella pagina **Impostazioni** specificare le impostazioni seguenti e quindi selezionare **Avanti**:  

    - **Area**: selezionare l'area di Azure in cui si vuole creare il punto di distribuzione cloud.  

    - **Gruppo di risorse** (solo metodo di distribuzione di Azure Resource Manager)  

        - **Usa esistente**: selezionare un gruppo di risorse esistente nell'elenco a discesa.  

        - **Crea nuovo**: immettere il nome del nuovo gruppo di risorse da creare nella sottoscrizione di Azure.  

    - **Sito primario**: selezionare il sito primario per distribuire contenuto in questo punto di distribuzione.

    - **File di certificato**: selezionare **Sfoglia** e scegliere il file PFX per il certificato di autenticazione server di questo punto di distribuzione cloud. Il nome comune di questo certificato popola i campi obbligatori **FQDN servizio** e **Nome servizio**.  

        > [!NOTE]  
        > Il certificato di autenticazione server del punto di distribuzione cloud supporta i caratteri jolly. Se si usa un certificato con caratteri jolly, sostituire l'asterisco (`*`) nel campo **FQDN servizio** con il nome host desiderato per il servizio.  

5. Nella pagina **Avvisi** impostare le quote di archiviazione, le quote di trasferimento e la percentuale delle quote necessaria affinché Configuration Manager generi gli avvisi. Selezionare quindi **Avanti**.  

6. Completare la procedura guidata.  

### <a name="monitor-installation"></a>Monitorare l'installazione  

Il sito inizia a creare un nuovo servizio ospitato per il punto di distribuzione cloud. Al termine della procedura guidata, monitorare l'avanzamento dell'installazione del punto di distribuzione cloud nella console di Configuration Manager. Monitorare anche il file **CloudMgr.log** nel server del sito primario. Se necessario, monitorare il provisioning del servizio cloud nel portale di Azure.  

> [!NOTE]  
> Il provisioning di un nuovo punto di distribuzione in Azure può richiedere fino a 30 minuti. Il file **CloudMgr.log** ripete il messaggio seguente finché non viene eseguito il provisioning dell'account di archiviazione:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Dopo il provisioning dell'account di archiviazione, il servizio viene creato e configurato.  

### <a name="verify-installation"></a>Verificare l'installazione

Usare i metodi seguenti per verificare il completamento dell'installazione del punto di distribuzione cloud:  

- Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Punti di distribuzione del cloud**. Individuare il nuovo punto di distribuzione cloud nell'elenco. Il valore nella colonna Stato dovrebbe essere **Pronto**.  

- Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Espandere **Stato del sistema** e selezionare il nodo **Stato componente**. Visualizzare tutti i messaggi del componente **SMS_CLOUD_SERVICES_MANAGER** e cercare l'ID messaggio di stato **9409**.  

- Se necessario, passare al portale di Azure. Nel portale di Azure lo stato visualizzato della **Distribuzione** per il punto di distribuzione cloud è **Pronto**.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> Configurare DNS  

Per poter usare il punto di distribuzione cloud, i client devono essere in grado di risolverne il nome in un indirizzo IP gestito da Azure. Il punto di gestione fornisce ai client il **FQDN servizio** del punto di distribuzione cloud. Il punto di distribuzione cloud è presente in Azure come **Nome servizio**. Visualizzare questi valori nella scheda **Impostazioni** delle proprietà del punto di distribuzione cloud.

> [!Note]  
> Il nodo **Punti di distribuzione del cloud** nella console include una colonna denominata **Nome servizio**, che in realtà mostra il valore di **FQDN servizio**. Per visualizzare entrambi i valori, aprire **Proprietà** per il punto di distribuzione cloud e passare alla scheda **Impostazioni**.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Il nome comune del certificato di autenticazione server deve includere il nome di dominio. Tale nome è obbligatorio quando si acquista un certificato da un provider pubblico. È consigliato quando il certificato viene rilasciato da PKI, Ad esempio, `WallaceFalls.contoso.com` Quando si specifica questo certificato in Crea procedura guidata punto di distribuzione cloud, in **FQDN servizio** viene inserito il nome comune (`WallaceFalls.contoso.com`). In **Nome servizio** viene accettato lo stesso nome host (`WallaceFalls`), che viene aggiunto al nome di dominio di Azure `cloudapp.net`. In questo scenario i client devono risolvere la proprietà **FQDN servizio** del dominio (`WallaceFalls.contoso.com`) nella proprietà **Nome servizio** di Azure (`WallaceFalls.cloudapp.net`). Creare un alias CNAME per eseguire il mapping di questi nomi.

### <a name="create-cname-alias"></a>Creare l'alias CNAME

Creare un record di nome canonico (CNAME) nel DNS pubblico con connessione Internet dell'organizzazione. Questo record crea un alias per la proprietà **FQDN servizio** del punto di distribuzione cloud ricevuta dai client nella proprietà **Nome servizio** di Azure. Creare, ad esempio, un nuovo record CNAME per `WallaceFalls.contoso.com` in `WallaceFalls.cloudapp.net`.  

### <a name="client-name-resolution-process"></a>Processo di risoluzione del nome client

Il processo seguente illustra in che modo un client risolve il nome del punto di distribuzione cloud:  

1. Il client ottiene il valore di **FQDN servizio** del punto di distribuzione cloud nell'elenco delle origini di contenuto, Ad esempio, `WallaceFalls.contoso.com`  

2. Interroga DNS, che risolve il FQDN servizio usando il nome CNAME nel **Nome servizio**  di Azure, Ad esempio, `WallaceFalls.cloudapp.net`  

3. Interroga di nuovo DNS, che risolve il nome servizio di Azure nell'indirizzo IP pubblico di Azure.  

4. Il client usa questo indirizzo IP per avviare le comunicazioni con il punto di distribuzione cloud.  

5. Il punto di distribuzione cloud presenta il certificato di autenticazione server al client. Il client usa la catena di certificati del certificato da convalidare.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> Configurare il proxy server  

Il server del sito primario che gestisce il punto di distribuzione cloud deve comunicare con Azure. Se l'organizzazione usa un server proxy per controllare l'accesso a Internet, configurare il server del sito primario per l'uso di questo proxy.  

Per altre informazioni, vedere [Supporto dei server proxy](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> Distribuire il contenuto e configurare i client

Distribuire il contenuto nel punto di distribuzione cloud in modo analogo a qualsiasi altro punto di distribuzione locale. Il punto di gestione non include il punto di distribuzione cloud nell'elenco dei percorsi di contenuto a meno che non includa il contenuto richiesto dai client. Per altre informazioni, vedere [Distribuire e gestire contenuto](deploy-and-manage-content.md).

Gestire un punto di distribuzione cloud in modo analogo a qualsiasi altro punto di distribuzione locale. Queste azioni includono l'assegnazione del punto a un gruppo di punti di distribuzione e la gestione dei pacchetti di contenuto. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](install-and-configure-distribution-points.md).

Con le impostazioni client predefinite i client vengono abilitati automaticamente all'uso dei punti di distribuzione cloud. Per controllare l'accesso a tutti i punti di distribuzione cloud nella gerarchia, usare le impostazioni client seguenti:  

- Nel gruppo **Impostazioni cloud** modificare l'impostazione **Consentire accesso al punto di distribuzione cloud**.  

    - Per impostazione predefinita, il valore di questa impostazione è **Sì**.  

    - Modificare e distribuire questa impostazione per utenti e dispositivi.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> Gestire e monitorare  

Monitorare il contenuto distribuito in un punto di distribuzione cloud in modo analogo a qualsiasi altro punto di distribuzione locale. Per altre informazioni, vedere [Monitorare il contenuto distribuito](monitor-content-you-have-distributed.md).

Quando l'elenco dei punti di distribuzione cloud è visualizzato nella console, è possibile aggiungervi altre colonne. La colonna **Dati in uscita**, ad esempio, visualizza la quantità di client dati scaricati dal servizio negli ultimi 30 giorni.<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a> Avvisi  

Configuration Manager controlla periodicamente il servizio di Azure. Se il servizio non è attivo o se sono presenti problemi relativi al certificato o alla sottoscrizione, Configuration Manager genera un avviso.

Configurare le soglie per la quantità di dati da archiviare nel punto di distribuzione cloud e per la quantità di dati che si vuole far scaricare ai client dal punto di distribuzione. Usare gli avvisi per queste soglie che consentono di decidere quando arrestare o eliminare il servizio cloud, regolare il contenuto archiviato nel punto di distribuzione cloud o modificare i client che possono usare il servizio.

- **Soglia di avviso di archiviazione**: la soglia di avviso di archiviazione imposta un limite massimo, espresso in GB, per la quantità di dati o contenuto da archiviare nel punto di distribuzione cloud. Per impostazione predefinita, questa soglia è pari a 2.000 GB. Configuration Manager genera avvisi e avvisi critici quando lo spazio libero rimanente raggiunge i livelli specificati. Per impostazione predefinita, questi avvisi vengono generati al 50% e al 90% della soglia.  

- **Soglia di avviso del trasferimento mensile**: la soglia di avviso del trasferimento mensile consente di monitorare la quantità di contenuto trasferita dal punto di distribuzione ai client per un periodo di 30 giorni. Per impostazione predefinita, questa soglia è pari a 10.000 GB. Il sito genera avvisi ed avvisi critici avvisi quando i trasferimenti raggiungono i valori definiti. Per impostazione predefinita, questi avvisi vengono generati al 50% e al 90% della soglia.  

    > [!IMPORTANT]  
    > Configuration Manager monitora il trasferimento dei dati, ma non lo interrompe quando viene superata la soglia di avviso di trasferimento specificata.  

Specificare le soglie per ogni punto di distribuzione cloud durante l'installazione oppure usare la scheda **Avvisi** delle proprietà del punto di distribuzione cloud.  

> [!NOTE]  
> Gli avvisi per un punto di distribuzione cloud dipendono dalle statistiche di utilizzo di Azure, che possono richiedere fino a 24 ore per diventare disponibili. Per altre informazioni su Analisi archiviazione per Azure, vedere [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics) (Analisi archiviazione).  

In un ciclo orario il sito primario che monitora il punto di distribuzione cloud scarica i dati delle transazioni da Azure e li archivia nel file `CloudDP-<ServiceName>.log` nel server del sito. Configuration Manager valuta quindi queste informazioni in rapporto alle quote di trasferimento e archiviazione per ogni punto di distribuzione cloud. Quando il trasferimento dei dati raggiunge o supera il volume specificato per gli avvisi o gli avvisi critici, Configuration Manager genera l'avviso appropriato.  

> [!WARNING]  
> Dal momento che il sito scarica le informazioni sui trasferimenti dei dati da Azure ogni ora, l'utilizzo di tali dati potrebbe superare una soglia di avviso o critica prima che Configuration Manager possa accedere ai dati e generare un avviso.  


## <a name="modify"></a><a name="bkmk_modify"></a> Modificare

È possibile visualizzare informazioni di carattere generale sul punto di distribuzione nel nodo **Punti di distribuzione del cloud** in **Servizi cloud** nell'area di lavoro **Amministrazione** della console di Configuration Manager. Selezionare un punto di distribuzione e scegliere **Proprietà** per visualizzare maggiori dettagli.  

Quando si modificano le proprietà di un punto di distribuzione cloud, le tabelle seguenti includono impostazioni da modificare:  

#### <a name="settings"></a>Impostazioni

- **Descrizione**  

- **File di certificato**: prima della scadenza del certificato di autenticazione server, rilasciare un nuovo certificato con lo stesso nome comune. Aggiungere quindi qui il nuovo certificato per iniziare a usare il servizio. Se il certificato scade, i client non considerano attendibile il servizio e non lo usano.  

#### <a name="alerts"></a>Avvisi

Regolare le soglie dei dati per gli avvisi relativi all'archiviazione e ai trasferimenti mensili.  

#### <a name="content"></a>Content

Gestire il contenuto in modo analogo a un punto di distribuzione locale.  

### <a name="redeploy-the-service"></a>Ridistribuire il servizio

Altre modifiche significative, ad esempio le configurazioni seguenti, richiedono la ridistribuzione del servizio:

- Metodo di distribuzione classico ad Azure Resource Manager
- Sottoscrizione
- Nome del servizio
- PKI da privato a pubblico
- Area di Azure

A partire dalla versione 1806, se è presente un punto di distribuzione cloud esistente nel metodo distribuzione classico, per poter usare il metodo di distribuzione di Azure Resource Manager è necessario distribuire un nuovo punto di distribuzione cloud. Sono disponibili due opzioni:

- Per riusare lo stesso nome di servizio:  

    1. Eliminare prima il punto di distribuzione cloud classico. Se non esiste un altro punto di distribuzione cloud, è possibile che i client non riescano a ottenere il contenuto.  

    2. Creare un nuovo punto di distribuzione cloud usando una distribuzione Resource Manager. Riusare lo stesso certificato di autenticazione server.  

    3. Distribuire il contenuto del pacchetto software necessario nel nuovo punto di distribuzione cloud.  

- Per usare un nuovo nome del servizio:  

    1. Creare un nuovo punto di distribuzione cloud usando una distribuzione Resource Manager. Usare un nuovo certificato di autenticazione server.  

    2. Distribuire il contenuto del pacchetto software necessario nel nuovo punto di distribuzione cloud.  

    3. Eliminare il punto di distribuzione cloud classico.

> [!Tip]  
> Per determinare il modello di distribuzione corrente di un punto di distribuzione cloud:<!--SCCMDocs issue #611-->  
>
> 1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Punti di distribuzione del cloud**.  
> 2. Aggiungere l'attributo **Modello di distribuzione** come colonna alla visualizzazione elenco. Per una distribuzione di Resource Manager, questo attributo è **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Arrestare o avviare il servizio cloud su richiesta

Arrestare un punto di distribuzione cloud in qualsiasi momento nella console di Configuration Manager. Questa azione impedisce immediatamente ai client di scaricare contenuto aggiuntivo dal servizio. Riavviare il servizio cloud dalla console di Configuration Manager per ripristinare l'accesso per i client. Arrestare un servizio cloud, ad esempio, quando viene raggiunta una soglia dei dati.  

Quando si arresta un punto di distribuzione cloud, il servizio cloud non elimina il contenuto dall'account di archiviazione, né impedisce al server del sito di trasferire contenuto aggiuntivo al punto di distribuzione cloud. Il punto di gestione restituisce comunque il punto di distribuzione cloud ai client come origine di contenuto valida.

Usare la procedura seguente per arrestare un punto di distribuzione cloud:  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Punti di distribuzione del cloud**.  

2. Selezionare il punto di distribuzione cloud. Per arrestare il servizio cloud eseguito in Azure, selezionare **Arresta servizio**.  

3. Selezionare **Avvia servizio** per riavviare il punto di distribuzione cloud.  

### <a name="delete-a-cloud-distribution-point"></a>Eliminare un punto di distribuzione cloud

Per disinstallare un punto di distribuzione cloud, selezionare il punto di distribuzione nella console di Configuration Manager e quindi scegliere **Elimina**.  

Quando un punto di distribuzione cloud viene eliminato da una gerarchia, Configuration Manager rimuove il contenuto dal servizio cloud in Azure.

La rimozione manuale di componenti in Azure crea incoerenze nel sistema. Questo stato produce dati orfani e può dare origine a comportamenti imprevisti.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> Risoluzione dei problemi avanzata

Se è necessario raccogliere la registrazione diagnostica dalle macchine virtuali di Azure per facilitare la risoluzione dei problemi relativi al punto di distribuzione cloud, usare l'esempio di PowerShell seguente per abilitare l'estensione di diagnostica del servizio per la sottoscrizione:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

L'esempio seguente è un file **diagnostics.wadcfgx** di esempio cui viene fatto riferimento nella variabile **public_config** nello script di PowerShell precedente. Per altre informazioni, vedere [Versioni e cronologia degli schemi di configurazione dell'estensione di Diagnostica di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
