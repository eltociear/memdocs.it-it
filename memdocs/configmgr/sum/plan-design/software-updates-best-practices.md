---
title: Procedure consigliate per gli aggiornamenti software
titleSuffix: Configuration Manager
description: Usare queste procedure consigliate per aggiornamenti software in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: dc0d416fdd186dbbeb4c61d48b688072bb830485
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708709"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Procedure consigliate per aggiornamenti software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo include le procedure consigliate per aggiornamenti software in Configuration Manager. Le informazioni sono suddivise in procedure consigliate per l'installazione iniziale e procedure consigliate per le operazioni in corso.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> Procedure consigliate per l'installazione  

Usare le procedure consigliate seguenti durante l'installazione degli aggiornamenti software in Configuration Manager.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> Usare un database WSUS condiviso per punti di aggiornamento software  

In caso di installazione di più di un punto di aggiornamento software in un sito primario, utilizzare lo stesso database WSUS per ciascun punto di aggiornamento software nella stessa foresta Active Directory. Condividendo lo stesso database, si limita notevolmente, ma non si elimina completamente, l'impatto sulle prestazioni dei client e della rete che potrebbe essere avvertito quando i client passano a un nuovo punto di aggiornamento software. Quando un client esegue il passaggio a un nuovo punto di aggiornamento software che condivide un database con il punto di aggiornamento software precedente, viene comunque eseguita una scansione differenziale. Tuttavia, tale scansione è molto ridotta rispetto a come sarebbe se il server WSUS disponesse di un proprio database. Per altre informazioni sul passaggio a un nuovo punto di aggiornamento software, vedere la sezione [Passaggio a un nuovo punto di aggiornamento software](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  È necessario anche condividere le cartelle di contenuti WSUS locali quando si usa un database WSUS condiviso per i punti di aggiornamento software.  

Per altre informazioni sulla condivisione del database WSUS, vedere i post di blog seguenti:  

- [Come implementare un database SUSDB condiviso per i punti di aggiornamento software di Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Considerazioni per più istanze WSUS che condividono un database del contenuto quando si usa Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> Se Configuration Manager e WSUS usano la stessa istanza di SQL Server, configurarne una per l'utilizzo di un'istanza denominata e l'altra per l'utilizzo dell'istanza predefinita  

Se i database di WSUS e Configuration Manager condividono la stessa istanza di SQL Server, non è facile determinare l'utilizzo delle risorse tra le due applicazioni. Usare istanze di SQL Server diverse per Configuration Manager e WSUS. Questa configurazione consentirà di risolvere e diagnosticare più facilmente eventuali problemi relativi all'utilizzo delle risorse che potrebbero verificarsi in ogni applicazione.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> Specificare l'impostazione "Archivia aggiornamenti in locale"  

Quando si installa WSUS, selezionare l'impostazione **Archivia aggiornamenti in locale**. Questa impostazione fa in modo che WSUS scarichi le condizioni di licenza associate agli aggiornamenti software. Le condizioni vengono scaricate durante il processo di sincronizzazione e vengono archiviate nel disco rigido locale per il server WSUS. Se non si seleziona questa impostazione, i computer client potrebbero non completare le analisi di conformità per gli aggiornamenti software che hanno le condizioni di licenza. Il componente **Gestione sincronizzazione WSUS** del punto di aggiornamento software verifica che questa impostazione sia abilitata ogni 60 minuti, per impostazione predefinita.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> Procedure operative consigliate  

Utilizzare le seguenti procedure ottimali durante l'utilizzo degli aggiornamenti software:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> Limitare gli aggiornamenti software a 1.000 in un'unica distribuzione degli aggiornamenti software  

Limitare il numero di aggiornamenti software a 1.000 per ogni distribuzione degli aggiornamenti software. Quando viene creata una regola di distribuzione automatica, verificare che i criteri specificati non prevedano più di 1.000 aggiornamenti software. Se si esegue la distribuzione manuale degli aggiornamenti software, non selezionare più di 1.000 aggiornamenti.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> Creare un nuovo gruppo di aggiornamento software ogni volta che viene eseguita una regola di distribuzione automatica per il "Patch Tuesday" e per la distribuzione generale  

C'è un limite di 1.000 aggiornamenti software in una distribuzione. Quando si crea una regola di distribuzione automatica, specificare se usare un gruppo di aggiornamento esistente o se crearne uno nuovo ogni volta che viene eseguita la regola. Se si specificano i criteri in una regola di distribuzione automatica che comporta più aggiornamenti software e tale regola viene eseguita in base a una pianificazione ricorrente, creare un nuovo gruppo di aggiornamento software ogni volta che viene eseguita la regola. In questo modo la distribuzione non oltrepasserà il limite di 1.000 aggiornamenti software per ogni distribuzione.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> Usare un gruppo di aggiornamento software esistente per le regole di distribuzione automatica per gli aggiornamenti delle definizioni di Endpoint Protection  

Se si usa regolarmente una regola di distribuzione automatica per la distribuzione degli aggiornamenti delle definizioni di Endpoint Protection, usare sempre un gruppo di aggiornamento software esistente. In caso contrario, la regola di distribuzione automatica crea potenzialmente nel tempo centinaia di gruppi di aggiornamento software. In genere, gli autori degli aggiornamenti delle definizioni impostano tali aggiornamenti in modo che scadano nel momento in cui vengono sostituiti da quattro aggiornamenti più recenti. Il gruppo di aggiornamento software creato dalla regola di distribuzione automatica, pertanto, non conterrà mai più di quattro aggiornamenti delle definizioni per l'autore: uno attivo e tre sostituiti.  



## <a name="see-also"></a>Vedere anche  
 [Plan for software updates](plan-for-software-updates.md) (Pianificare gli aggiornamenti del software)
