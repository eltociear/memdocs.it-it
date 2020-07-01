---
title: Gestire i client su Internet
titleSuffix: Configuration Manager
description: Informazioni sulla gestione dei client con gateway di gestione cloud e sulla gestione basata su Internet in Configuration Manager.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715595"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gestire i client in Internet con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager, la maggior parte dei computer e dei server gestiti si trovano in genere fisicamente nella stessa rete dei server del sistema del sito che eseguono le funzioni di gestione. Tuttavia, è possibile gestire i client esterni alla rete interna, quando sono connessi a internet. Questa possibilità non richiede che i client si connettano tramite VPN per raggiungere i server di sistema del sito.

Configuration Manager offre due modi per gestire i client connessi a Internet:

- Gateway di gestione cloud

- Gestione client basata su Internet

> [!NOTE]
> È possibile avere una combinazione di entrambi i servizi per un singolo sito. Se un dispositivo ottiene i criteri dal sito sia per la gestione client basata su Internet che per CMG, li seleziona in modo casuale per la comunicazione. L'unico meccanismo disponibile per controllare la comunicazione è l'autenticazione client. Ad esempio, se un client aggiunto ad Azure AD non considera attendibile il certificato di autenticazione server del punto di gestione basato su Internet, può usare solo CMG. Se un client aggiunto a un dominio non considera attendibile il certificato di autenticazione server CMG, può usare solo il punto di gestione basato su Internet.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Gateway di gestione cloud

Il gateway di gestione di cloud offre la gestione dei client basati su Internet. Usa una combinazione di un servizio cloud di Microsoft Azure e un ruolo del sistema del sito locale che comunica con il servizio. I client basati su Internet usano il servizio cloud per comunicare con Configuration Manager locale.

### <a name="cmg-advantages"></a>Vantaggi di CMG

- Nessun investimento aggiuntivo in infrastrutture locali.  

- Infrastruttura locale non esposta a Internet.  

- Macchine virtuali cloud che eseguono il servizio completamente gestite da Azure e senza necessità di manutenzione.  

- Facilità di impostazione e configurazione nella console di Configuration Manager.  

### <a name="cmg-disadvantages"></a>Svantaggi di CMG  

- Costo di sottoscrizione al servizio cloud.  

- Invio dei dati di gestione tramite il servizio cloud.  

Per altre informazioni, vedere [Plan for cloud management gateway](cmg/plan-cloud-management-gateway.md) (Pianificare il gateway di gestione cloud).  

## <a name="internet-based-client-management"></a>Gestione client basata su Internet

Questo metodo si basa sui server di sistema del sito con connessione a Internet con cui i client comunicano direttamente ai fini della gestione. Richiede che client e server di sistema del sito siano configurati per la gestione client basata su Internet.

### <a name="ibcm-advantages"></a>Vantaggi della gestione client basata su Internet

- Nessuna dipendenza del servizio cloud.  

- Nessun costo aggiuntivo associato alla sottoscrizione a un servizio cloud.  

- Controllo completo di server e ruoli che offrono il servizio.  

### <a name="ibcm-disadvantages"></a>Svantaggi della gestione client basata su Internet

- Necessità di un investimento aggiuntivo in infrastrutture.  

- Carico e costo operativo di un'infrastruttura aggiuntiva.  

- Necessità di esporre l'infrastruttura a Internet.  

Per altre informazioni, vedere [Pianificare la gestione client basata su Internet](plan-internet-based-client-management.md).  
