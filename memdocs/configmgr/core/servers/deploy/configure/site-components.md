---
title: Componenti del sito
titleSuffix: Configuration Manager
description: Informazioni su come configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700929"
---
# <a name="site-components-for-configuration-manager"></a>Componenti del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per ogni sito di Configuration Manager è possibile configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito. Le configurazioni dei componenti del sito si applicano a un sito e a ogni istanza di un ruolo del sistema del sito applicabile nel sito.  

Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare un sito. Nel gruppo **Impostazioni** della barra multifunzione scegliere **Configura componenti del sito**. Selezionare una delle opzioni seguenti:

- [Distribuzione del software](#software-distribution)  
- [Punto di aggiornamento software](#software-update-point) 
- [Distribuzione del sistema operativo:](#operating-system-deployment)
- [Punto di gestione](#management-point)  
- [Creazione di report sullo stato](#status-reporting)  
- [Notifica di posta elettronica](#email-notification)
- [Valutazione dell'appartenenza alla raccolta](#bkmk_colleval)


## <a name="about-site-components"></a>Informazioni sui componenti del sito  

 La maggior parte delle opzioni per i diversi componenti del sito risulta di facile comprensione quando viene visualizzata nella console di Configuration Manager. Le informazioni riportate di seguito possono illustrare meglio alcune delle configurazioni più complesse oppure indirizzano a contenuti aggiuntivi.  

> [!Note]  
> Le opzioni disponibili per alcuni componenti variano a seconda se si seleziona il sito di amministrazione centrale, un sito primario o un sito secondario. Alcuni componenti non sono per nulla disponibili per determinati tipi di siti.  



### <a name="software-distribution"></a>Distribuzione del software  

#### <a name="content-distribution-settings"></a>Impostazioni per la distribuzione del contenuto
Nella scheda **Generali** è possibile specificare le impostazioni che modificano il modo in cui il server del sito trasferisce il contenuto ai relativi punti di distribuzione. Quando si aumentano i valori usati per le impostazioni di distribuzione simultanea, la distribuzione del contenuto potrebbe usare una maggiore larghezza della banda di rete.  

#### <a name="pull-distribution-point"></a>Punto di distribuzione pull
Per altre informazioni, vedere [Usare un punto di distribuzione pull](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

#### <a name="network-access-account"></a>Account di accesso alla rete
Per altre informazioni, vedere [Account di accesso alla rete](../../../plan-design/hierarchy/accounts.md#network-access-account).  


### <a name="software-update-point"></a>Punto di aggiornamento software  

Per altre informazioni, vedere [Install a software update point](../../../../sum/get-started/install-a-software-update-point.md) (Installare un punto di aggiornamento software).  


### <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

Per altre informazioni, vedere [Specificare l'unità per l'installazione offline dell'immagine del sistema operativo](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive).


### <a name="management-point"></a>Punto di gestione  

Nella scheda **Generali** impostare il sito per pubblicare informazioni sui punti di gestione in Active Directory Domain Services.  

I client di Configuration Manager usano punti di gestione per individuare i servizi e per trovare informazioni sul sito, ad esempio l'appartenenza al gruppo di limiti e le opzioni di selezione del certificato PKI. I client usano anche punti di gestione per trovare altri punti di gestione nel sito, nonché i punti di distribuzione da cui scaricare il software. I punti di gestione consentono ai client di completare l'assegnazione del sito e scaricare informazioni sul client.  

Il metodo più sicuro per i client per individuare i punti di gestione è pubblicarli in Active Directory Domain Services. Questo metodo di individuazione del servizio richiede i seguenti elementi:

- Questo schema è esteso per Configuration Manager.
- È disponibile un contenitore di **Gestione del sistema** con autorizzazioni di sicurezza appropriate per il server del sito per pubblicare in tale contenitore.
- Il sito di Configuration Manager è impostato per pubblicare in Active Directory Domain Services.
- I client appartengano alla stessa foresta di Active Directory del server del sito.  

Quando i client nella Intranet non sono in grado di usare Active Directory Domain Services per individuare i punti di gestione, usare la pubblicazione [DNS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

Per informazioni generali sulla posizione del servizio, vedere [Informazioni su come i client trovano i servizi e le risorse del sito](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Pubblicare i punti di gestione intranet selezionati in DNS
Specificare questa opzione quando i client nella Intranet non sono in grado di rilevare i punti di gestione in Active Directory Domain Services. Possono invece usare un record di risorse del percorso del servizio DNS (SRV RR) per trovare un punto di gestione nel sito assegnato.  

Affinché Configuration Manager pubblichi i punti di gestione Intranet in DNS, è necessario che vengano soddisfatte tutte le condizioni seguenti:  

-   La versione di BIND dei server DNS è 8.1.2 o successiva.  

-   I server DNS sono impostati per eseguire aggiornamenti automatici e supportano i record di risorse del percorso del servizio.  

-   I nomi di domini completamente qualificati (FQDN) specificati per i punti di gestione in Configuration Manager hanno voci host (record A o AAA) in DNS.  

> [!WARNING]  
>  Affinché i client trovino punti di gestione pubblicati in DNS, è necessario assegnare i client a un sito specifico invece di usare l'assegnazione sito automatica. Impostare questi client per usare il codice del sito con il suffisso del dominio del relativo punto di gestione. Per altre informazioni, vedere [Individuazione dei punti di gestione](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points).  

Se i client di Configuration Manager non possono usare Active Directory Domain Services o DNS per trovare i punti di gestione nella Intranet, useranno [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Il primo punto di gestione installato per il sito viene automaticamente pubblicato in WINS quando viene impostato per accettare le connessioni client HTTP nell'Intranet.  


### <a name="status-reporting"></a>Creazione di report sullo stato  

Queste opzioni impostano direttamente il livello di dettaglio incluso nei report sullo stato dei siti e dei client.  


### <a name="email-notification"></a>Notifica con posta elettronica  

Specificare i dettagli dell'account e del server di posta elettronica per abilitare Configuration Manager per l'invio di notifiche via posta elettronica per gli avvisi.  

Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato](../../manage/use-alerts-and-the-status-system.md).


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a> Valutazione dell'appartenenza alla raccolta  

Usare questo componente per impostare la frequenza con cui l'appartenenza alla raccolta viene valutata in modo incrementale. La valutazione incrementale aggiorna l'appartenenza alla raccolta solo con risorse nuove o modificate.  

Per altre informazioni, vedere [Procedure consigliate per le raccolte](../../../clients/manage/collections/best-practices-for-collections.md).



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Usare Configuration Manager Service Manager per gestire i componenti del sito  

È possibile usare Configuration Manager Service Manager per controllare i servizi di Configuration Manager e per visualizzare lo stato di qualsiasi servizio o thread di lavoro di Configuration Manager. Questi servizi e thread sono definiti collettivamente componenti di Configuration Manager. I componenti di Configuration Manager presentano le caratteristiche riportate di seguito:  

-   I componenti possono essere eseguiti su ogni sistema del sito.  

-   I componenti vengono gestiti allo stesso modo dei servizi in Windows. È possibile avviare, arrestare, sospendere, riprendere o eseguire query nei componenti di Configuration Manager.  

Un servizio di Configuration Manager viene eseguito quando c'è un'operazione che deve eseguire, ad esempio se un file di configurazione viene scritto nella posta in arrivo di un componente. 


### <a name="use-the-configuration-manager-service-manager"></a>Usare Configuration Manager Service Manager  

1.  Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Stato componente**.  

2.  Nel gruppo **Componente** selezionare **Avvia**, quindi scegliere **Configuration Manager Service Manager**.  

3.  All'apertura di Configuration Manager Service Manager, connettersi al sito che si desidera gestire.  

     Se il sito che si vuole gestire non viene visualizzato, passare al menu **Sito** e selezionare **Connetti**. Quindi immettere il nome del server del sito per il sito corretto.  

4.  Espandere il sito e passare a **Componenti** o **Server**in base alla posizione dei componenti che si desidera gestire.  

5.  Nel riquadro a destra selezionare uno o più componenti. Nel menu **Componente** selezionare **Query** per aggiornare lo stato della selezione.  

6.  Dopo aver aggiornato lo stato del componente, usare una delle quattro opzioni basate su azioni nel menu **Componente** per modificare il funzionamento dei componenti. Dopo aver richiesto un'azione, è necessario eseguire una query sul componente per visualizzare il nuovo stato del componente.  

7.  Chiudere Configuration Manager Service Manager al termine della modifica dello stato operativo dei componenti.  
