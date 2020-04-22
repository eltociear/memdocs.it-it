---
title: Infrastruttura di rete
titleSuffix: Configuration Manager
description: Configurare firewall, porte e domini per la prepararsi per le comunicazioni di Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703089"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Considerazioni sull'infrastruttura di rete per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per preparare la rete per supportare Configuration Manager, potrebbe essere necessario configurare alcuni componenti dell'infrastruttura. Potrebbe ad esempio essere necessario aprire porte del firewall per passare le comunicazioni usate da Configuration Manager.  

## <a name="ports-and-protocols"></a>Porte e protocolli

Le diverse funzionalità di Configuration Manager usano porte di rete diverse. Alcune porte sono obbligatorie, mentre altre possono essere personalizzate.

La maggior parte delle comunicazioni di Configuration Manager usa porte comuni, ad esempio la porta 80 per HTTP o la 443 per HTTPS. Alcuni ruoli del sistema del sito supportano l'uso di siti Web personalizzati e porte personalizzate. Per altre informazioni, vedere [Siti Web per i server del sistema del sito](websites-for-site-system-servers.md).

Prima di distribuire Configuration Manager, identificare le porte da usare e configurare i firewall in base alle esigenze.

Dopo aver installato Configuration Manager, se è necessario modificare una porta, non trascurare l'aggiornamento dei firewall sui dispositivi e nella rete. Modificare anche la configurazione della porta in Configuration Manager.

Per altre informazioni, vedere gli articoli seguenti:

- [Come configurare le porte di comunicazione client](../../clients/deploy/configure-client-communication-ports.md)
- [Porte usate in Configuration Manager](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Requisiti per l'accesso a Internet

Alcune caratteristiche di Configuration Manager hanno bisogno della connettività Internet per funzionare completamente. Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, assicurarsi di consentire l'accesso degli endpoint necessari.

Per altre informazioni, vedere i [requisiti di accesso Internet](internet-endpoints.md).


## <a name="proxy-servers"></a>Server proxy

È possibile specificare i server proxy per diversi client e server di sistema del sito. Queste configurazioni si effettuano quando si installa un client o un ruolo del sistema del sito o li si modifica in seguito in base alle esigenze.

Per altre informazioni, vedere [Supporto dei server proxy](proxy-server-support.md).
