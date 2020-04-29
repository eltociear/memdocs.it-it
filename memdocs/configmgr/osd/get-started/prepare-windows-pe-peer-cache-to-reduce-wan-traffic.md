---
title: Preparare la peer cache di Windows PE per ridurre il traffico WAN
titleSuffix: Configuration Manager
description: La peer cache di Windows PE viene usata in Windows PE per ottenere il contenuto da un peer locale e ridurre al minimo il traffico della rete WAN se non c'è nessun punto di distribuzione locale.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708779"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Preparare la peer cache di Windows PE per ridurre il traffico della rete WAN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si distribuisce un nuovo sistema operativo in Configuration Manager, i computer che eseguono la sequenza di attività possono usare la peer cache di Windows PE per ottenere contenuto da un peer locale (un'origine peer cache) anziché scaricarlo da un punto di distribuzione. In tal modo il traffico WAN viene ridotto al minimo negli scenari con le filiali, in cui non esiste un punto di distribuzione locale.  

 La peer cache di Windows PE è simile a [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), ma funziona in Ambiente preinstallazione di Windows (Windows PE). Per descrivere i client che usano la peer cache di Windows PE vengono usati i termini seguenti:  

-   Un **client peer cache** è un computer configurato per utilizzare Peer cache di Windows PE.  

-   Un’ **origine peer cache** è un client configurato per la peer cache e che rende il contenuto disponibile ad altri client peer cache che lo richiedono.  

Usare le sezioni seguenti per gestire la peer cache.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a> Oggetti archiviati in un'origine peer cache  
 Una sequenza di attività configurata per l'uso della peer cache di Windows PE può ottenere gli oggetti contenuto seguenti durante l'esecuzione in Windows PE:  

- Immagine del sistema operativo  

- Pacchetto driver  

- Pacchetti e programmi (quando il client continua a eseguire la sequenza di attività nel sistema operativo completo, ottiene questo contenuto da un’origine peer cache se la sequenza di attività è stata configurata in origine per la peer cache in esecuzione in Windows PE).  

- Immagini di avvio aggiuntive  

  Gli oggetti contenuto seguenti non vengono mai trasferiti tramite peer cache. Vengono invece trasferiti da un punto di distribuzione o mediante Windows BranchCache se è configurato nell'ambiente:  

- Applicazioni  

- Aggiornamenti software  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a> Come funziona la peer cache di Windows PE?  
 Si consideri uno scenario con una filiale che non dispone di un punto di distribuzione ma che invece dispone di vari client abilitati all'uso della peer cache di Windows PE. Si distribuisce la sequenza di attività configurata per l'uso della peer cache in diversi client che sono configurati come parte dell'origine peer cache. Il primo client a eseguire la sequenza di attività trasmette una richiesta di un peer con il contenuto. Poiché non ne trova uno, ottiene il contenuto da un punto di distribuzione attraverso la rete WAN. Il client installa la nuova immagine e archivia il contenuto nella relativa cache del client di Configuration Manager in modo che funzioni come origine peer cache per altri client. Quando il client successivo esegue la sequenza di attività, trasmette una richiesta nella subnet per un’origine peer cache, e il primo client risponde rendendo disponibile il contenuto memorizzato nella cache.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a> Determinare quali client faranno parte dell'origine peer cache di Windows PE  
 Per determinare quali computer selezionare come origine peer cache di Windows PE, è necessario considerare diversi elementi:  

-   L'origine peer cache di Windows PE deve essere un computer desktop che è sempre acceso e disponibile per i client peer cache.  

-   La peer cache di Windows PE ha una dimensione della cache client sufficiente per archiviare le immagini.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a> Requisiti per l'uso di un'origine peer cache di Windows PE da parte di un client  
 Per poter usare un'origine peer cache di Windows PE, i client devono soddisfare i requisiti seguenti:  

-   Il client di Configuration Manager deve essere in grado di comunicare attraverso le porte seguenti della rete:  

    -   Porta per la trasmissione di rete iniziale, per trovare un’origine peer cache. Per impostazione predefinita, è la porta UDP 8004.  

    -   Porta per il download del contenuto da un'origine peer cache (HTTP e HTTPS). Per impostazione predefinita, è la porta TCP 8003.  
    
        Per altre informazioni, vedere [Porte usate per le connessioni](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  I client useranno HTTPS per scaricare il contenuto quando è disponibile. Tuttavia, lo stesso numero di porta viene usato per HTTP o HTTPS.  

-   [Configurare la cache del client per i client di Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) nei client per garantire che dispongano di spazio sufficiente a contenere e archiviare le immagini distribuite. La peer cache di Windows PE non influisce sulla configurazione o sul comportamento della cache client.  

-   Le opzioni di distribuzione per la distribuzione della sequenza di attività devono essere configurate come Scarica contenuto localmente quando richiesto dalla sequenza di attività.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a> Configurare la peer cache di Windows PE  
 È possibile usare i metodi seguenti per eseguire il provisioning di contenuto peer cache per un client, in modo che possa servire come origine peer cache:  

- Un client peer cache che non è in grado di trovare un'origine peer cache con il contenuto lo scaricherà da un punto di distribuzione.  Se il client riceve le impostazioni client che abilitano la peer cache e la sequenza di attività viene configurata in modo da preservare il contenuto memorizzato nella cache, il client diventa un'origine peer cache.  

- Un client peer cache peer può ottenere contenuto da un altro client peer cache (un’origine peer cache).  Poiché il client è configurato per peer cache, quando esegue una sequenza di attività configurata in modo da preservare il contenuto memorizzato nella cache, il client diventa un'origine peer cache.  

- Un client esegue una sequenza di attività che include il passaggio facoltativo, [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent), usato per pre-installare contenuto di rilievo incluso nella sequenza di attività della peer cache di Windows PE. Quando si utilizza questo metodo:  

  -   Non è necessario che nel client venga installata l’immagine in corso di distribuzione.  

  -   Oltre all'opzione **Scarica il contenuto del pacchetto** , per la sequenza di attività è necessario usare anche l'opzione **Cache client Gestione configurazione** . Utilizzare questa opzione per archiviare il contenuto nella cache dei client in modo che il client possa funzionare da origine peer cache per altri client peer cache.  

  Nelle procedure riportate di seguito sarà possibile configurare Peer cache di Windows PE sui client e configurare le sequenze di attività che supportano la peer cache.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Per configurare i computer dell'origine peer cache di Windows PE  

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client**e creare un nuovo oggetto **Impostazioni dispositivo client personalizzate** o modificare un oggetto impostazioni esistente. È possibile anche eseguire questa configurazione per l’oggetto **Impostazioni client predefinite** .  

   > [!TIP]  
   >  Utilizzare un oggetto impostazioni personalizzate per gestire i client che ricevono questa configurazione. È possibile, ad esempio, evitare questa configurazione sui portatili degli utenti che si trovano spesso in viaggio. Un sistema altamente mobile può essere un'origine insufficiente a fornire contenuto ad altri client peer cache.  
   >   
   >  Ricordare anche che quando si configura questa impostazione come parte di **Impostazioni client predefinite**, la configurazione si applica a tutti i client dell'ambiente in uso.  

2. In **Impostazioni della cache del client** impostare **Abilita client di Configuration Manager nel sistema operativo completo a condividere contenuto** su **Sì**.  

   -   Per impostazione predefinita, è abilitato solo HTTP. Se si desidera abilitare i client a scaricare il contenuto in HTTPS, impostare **Abilitare HTTPS per la comunicazione peer client** su **Sì**.  

   -   Per impostazione predefinita, la porta per le trasmissioni è impostata su 8004 e la porta per il download del contenuto è impostata su 8003. È possibile modificare entrambe.  

3. Salvare e distribuire le impostazioni client ai client selezionati come origine cache peer.  

   Dopo aver configurato un dispositivo con questo oggetto impostazioni, il dispositivo viene configurato per funzionare da origine peer cache. Queste impostazioni devono essere distribuite ai potenziali client peer cache per configurare le porte e i protocolli richiesti.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Configurare una sequenza di attività per la peer cache di Windows PE  
 Quando si configura la sequenza di attività, usare le seguenti variabili della sequenza di attività come variabili di raccolta per la raccolta in cui viene distribuita la sequenza di attività:  

- **SMSTSPeerDownload**  

   Valore:  TRUE  

   Consente al client di utilizzare Peer cache di Windows PE.  

- **SMSTSPeerRequestPort**  

   Valore: <numero porta\>  

   Quando non si usano le porte predefinite configurate in Impostazioni client (8004), è necessario configurare questa variabile con un valore personalizzato della porta di rete da usare per la trasmissione iniziale.  

- **SMSTSPreserveContent**  

   Valore: TRUE  

   Ciò contrassegna il contenuto nella sequenza di attività per essere mantenuto nella cache del client di Configuration Manager dopo la distribuzione. Questa operazione è diversa rispetto all'uso di SMSTSPersisContent che mantiene il contenuto solo per la durata della sequenza di attività e usa la cache della sequenza di attività, ma non la cache del client di Configuration Manager.  

  Per altre informazioni, vedere [Variabili della sequenza di attività](../understand/task-sequence-variables.md).  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a> Convalidare l'esito positivo dell'uso della peer cache di Windows PE  
 Dopo aver usato la peer cache di Windows PE per distribuire e installare una sequenza di attività, è possibile verificare che la peer cache sia stata usata correttamente nel processo visualizzando **smsts.log** sul client che ha eseguito la sequenza di attività.  

 Individuare nel log una voce simile alla seguente, dove <*NomeServerOrigine*> identifica il computer da cui il client ha ottenuto il contenuto. Tale computer deve essere un'origine peer cache e non un server punto di distribuzione. Altri dettagli variano in base all'ambiente locale e alle configurazioni.  

-   *<![LOG[Downloaded file from http:// <SourceServerName\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
