---
title: Sicurezza e privacy delle raccolte
titleSuffix: Configuration Manager
description: Informazioni sulle procedure consigliate per la sicurezza e la privacy delle raccolte in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695529"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Sicurezza e privacy per le raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo argomento vengono illustrate le procedure consigliate e le informazioni sulla privacy per le raccolte in Configuration Manager.  

 In Configuration Manager non sono disponibili informazioni sulla privacy specifiche per le raccolte. Le raccolte sono contenitori di risorse, quali utenti e dispositivi. L'appartenenza a una raccolta dipende spesso dalle informazioni che Configuration Manager raccoglie durante il funzionamento standard. Ad esempio, con le informazioni sulle risorse raccolte tramite individuazione o inventario è possibile configurare una raccolta contenente i dispositivi che soddisfano criteri specifici. Le raccolte possono anche basarsi sulle informazioni sullo stato corrente delle operazioni di gestione client, ad esempio la distribuzione di software e la verifica della conformità. Oltre a queste raccolte basate su query, gli utenti amministrativi anche possono aggiungere risorse a raccolte.  

 Per altre informazioni sulle raccolte, vedere [Introduzione alle raccolte](../../../../core/clients/manage/collections/introduction-to-collections.md). Per altre informazioni sulle procedure di sicurezza consigliate e le informazioni sulla privacy per le operazioni di Configuration Manager che è possibile usare per configurare l'appartenenza a una raccolta, vedere [Procedure consigliate per la sicurezza e informazioni sulla privacy per Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Procedure di sicurezza consigliate per le raccolte  
 Usare la seguente procedura di sicurezza consigliata per le raccolte.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Quando si esporta o si importa una raccolta mediante un file MOF (Managed Object Format) salvato in un percorso di rete, proteggere il percorso stesso e il canale di rete.|Limita l'accesso alla cartella di rete.<br /><br /> Usare la firma SMB (Server Message Block) o IPsec (Internet Protocol Security) tra il percorso di rete e il server del sito per impedire a un utente malintenzionato di manomettere i dati della raccolta esportati. Utilizzare IPsec per crittografare i dati sulla rete per impedire la divulgazione di informazioni.|  

### <a name="security-issues-for-collections"></a>Problemi di sicurezza per le raccolte  
 Le raccolte presentano i problemi di sicurezza seguenti:  

-   Se si usano le variabili raccolta, gli amministratori locali saranno in grado di leggere informazioni potenzialmente riservate.  

     È possibile usare variabili di raccolta quando si distribuisce un sistema operativo.  
