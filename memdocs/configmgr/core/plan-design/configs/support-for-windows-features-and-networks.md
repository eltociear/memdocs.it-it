---
title: Supporto per funzionalità di Windows
titleSuffix: Configuration Manager
description: Informazioni su quali funzionalità di Windows e di rete sono supportate in Configuration Manager.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e8e65571a3902661176ca3840690c159faef416
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688589"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Supporto per le funzionalità e le reti Windows in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra il supporto di Configuration Manager per funzionalità comuni di Windows e di rete.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  

È possibile usare Windows BranchCache con Configuration Manager quando si abilita BranchCache nei punti di distribuzione e configurare i client per l'uso di BranchCache in modalità cache distribuita.

È possibile configurare le impostazioni di BranchCache su un tipo di distribuzione per le applicazioni, sulla distribuzione per un pacchetto e per le sequenze attività. A partire dalla versione 1802, BranchCache è abilitato per impostazione predefinita.

Quando vengono soddisfatti i requisiti per BranchCache, questa funzionalità abilita i client in remoto per ottenere contenuti dai client locali che hanno una cache corrente del contenuto.  

Ad esempio, quando il primo client abilitato per BranchCache richiede contenuto da un punto di distribuzione configurato come server BranchCache, il client scarica il contenuto e lo memorizza nella cache. Il contenuto viene quindi reso disponibile ai client presenti nella stessa subnet da cui è stato richiesto il contenuto

e viene memorizzato nella cache dei client. Altri client nella stessa subnet non devono scaricare contenuto dal punto di distribuzione. Il contenuto viene distribuito tra più client per trasferimenti futuri.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Requisiti per supportare BranchCache con Configuration Manager

#### <a name="configure-distribution-points"></a>Configurare i punti di distribuzione

Aggiungere la funzionalità **Windows BranchCache** al server di sistema del sito configurato come un punto di distribuzione.

- I punti di distribuzione nei server configurati per supportare BranchCache non richiedono alcuna configurazione aggiuntiva.
- Non è possibile aggiungere Windows BranchCache a un punto di distribuzione basato sul cloud. I punti di distribuzione basati sul cloud supportano il download del contenuto da parte dei client configurati per Windows BranchCache.  

#### <a name="configure-clients"></a>Configurare i client

- I client che possono supportare BranchCache devono essere configurati per la modalità cache distribuita di BranchCache.  
- L'impostazione del sistema operativo per le impostazioni client BITS deve essere abilitata per supportare BranchCache.  

Per informazioni, vedere [Configurare i client per BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) nella documentazione di Windows.

Tutte le versioni supportate di Configuration Manager di Windows supportano BranchCache per impostazione predefinita.

Per altre informazioni, vedere [BranchCache per Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) nella documentazione di Windows Server.  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Computer in gruppi di lavoro  

Configuration Manager offre il supporto per i client in gruppi di lavoro.  

- Configuration Manager supporta lo spostamento di un client da un gruppo di lavoro a un dominio o da un dominio a un gruppo di lavoro. Per ulteriori informazioni, vedere [Come installare i client di Configuration Manager sui computer dei gruppi di lavoro](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]
> Anche se i client sono supportati nei gruppi di lavoro, tutti i sistemi del sito devono essere membri di un dominio Active Directory supportato.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a> Deduplicazione dati

Configuration Manager supporta l'uso della deduplicazione dati con punti di distribuzione in Windows Server 2012 o versioni successive.

> [!IMPORTANT]  
> Non è possibile contrassegnare i file di origine del pacchetto host per la deduplicazione dei dati perché la deduplicazione dati usa reparse point e Configuration Manager non supporta l'uso di un percorso di origine del contenuto con file archiviati nei reparse point.  

Per altre informazioni, vedere i post seguenti:

- [Punti di distribuzione di Configuration Manager e deduplicazione dati di Windows Server 2012](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) nel blog del team di Configuration Manager

- [Panoramica della deduplicazione dati](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) nella documentazione di Windows Server

## <a name="directaccess"></a><a name="bkmk_DA"></a> DirectAccess  

Configuration Manager supporta la funzionalità DirectAccess per la comunicazione tra client e sistemi server del sito.  

- Quando vengono soddisfatti tutti i requisiti per DirectAccess, i client di Configuration Manager su Internet possono comunicare con il relativo sito assegnato come se fossero nella Intranet.  

- Per le azioni avviate dal server, ad esempio il controllo remoto e l'installazione push client, il computer di origine deve eseguire IPv6. Questo protocollo deve essere supportato da tutti i dispositivi di rete interessati.  

Configuration Manager non supporta le funzionalità seguenti su DirectAccess:  

- Distribuzione del sistema operativo

- Comunicazione tra siti di Configuration Manager  

- Comunicazione tra server del sistema del sito di Configuration Manager all'interno di un sito  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a> Computer ad avvio doppio  

Configuration Manager non può gestire più di un sistema operativo in un singolo computer. Se in un computer è presente più di un sistema operativo da gestire, regolare i metodi di individuazione del sito e di installazione client usati per accertarsi che il client di Configuration Manager sia installato solo sul sistema operativo che deve essere gestito.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a> IPv6  

Oltre a al protocollo IP versione 4 (IPv4), Configuration Manager supporta il protocollo IPv6, con le eccezioni seguenti:  

|Funzione| Eccezione per il supporto di IPv6|  
|--------------|-------------------------------|  
|Punti di distribuzione basati su cloud|IPv4 è necessario per supportare Microsoft Azure e i punti di distribuzione basati su cloud.|  
|Gateway di gestione cloud|IPv4 è necessario per supportare Microsoft Azure e il gateway di gestione cloud.|  
|Dispositivi mobili registrati da Microsoft Intune e Microsoft Service Connector|IPv4 è necessario per supportare i dispositivi mobili registrati da Microsoft Intune e da Microsoft Service Connector.|  
|Individuazione rete|IPv4 è obbligatorio quando si configura un server DHCP per la ricerca nell'individuazione di rete.|  
|Distribuzione del sistema operativo|Nella versione 1802 e precedenti, IPv4 è necessario per supportare la distribuzione del sistema operativo.  </br> </br> A partire dalla versione 1806, è possibile abilitare un risponditore PXE in un punto di distribuzione senza Servizi di distribuzione Windows. Questo nuovo servizio risponditore PXE supporta IPv6. Altri aspetti della funzionalità di distribuzione del sistema operativo, ad esempio l'acquisizione o impostazione di indirizzi IP statici durante la sequenza di attività, continuano a richiedere IPv4. |  
|Comunicazione del proxy di riattivazione|IPv4 è necessario per supportare i pacchetti proxy di riattivazione del client.|  
|Windows CE|IPv4 è necessario per supportare il client di Configuration Manager nei dispositivi Windows CE.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a> Network Address Translation  

Network Address Translation (NAT) è supportato in Configuration Manager solo se il sito supporta i client presenti in Internet e il client rileva che è connesso a Internet. Per altre informazioni sulla gestione client basata su Internet, vedere [Pianificare la gestione dei client basati su Internet](../../clients/manage/plan-internet-based-client-management.md).  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a> Tecnologia di archiviazione specializzata  

Configuration Manager funziona con qualsiasi hardware certificato nell'Hardware Compatibility List di Windows per la versione del sistema operativo su cui è installato il componente di Configuration Manager.

I ruoli del server del sito richiedono il file system NTFS, per consentire a Configuration Manager di impostare le autorizzazioni per directory e file. Configuration Manager presuppone di avere la proprietà completa di un'unità logica. I sistemi dei siti eseguiti in computer separati non possono condividere una partizione logica con alcuna tecnologia di archiviazione. Tuttavia, ogni computer può usare una partizione logica separata nella stessa partizione fisica di un dispositivo di archiviazione condivisa.  

### <a name="support-considerations"></a>Considerazioni sul supporto

- **Rete di archiviazione**: Una rete SAN (Storage Area Network) è supportata quando un server basato su Windows supportato è collegato direttamente al volume ospitato dalla SAN.  

- **Single Instance Storage**: Configuration Manager non supporta la configurazione di cartelle di pacchetto punto di distribuzione e firma in un volume compatibile con Single Instance Storage (SIS).  

     La cache di un client di Configuration Manager non è supportata in un volume compatibile con SIS.  

- **Unità disco rimovibile**: Configuration Manager non supporta l'installazione dei sistemi del sito o dei client di Configuration Manager in un'unità disco rimovibile.  
