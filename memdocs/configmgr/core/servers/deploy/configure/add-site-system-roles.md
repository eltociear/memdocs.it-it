---
title: Aggiungere ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Informazioni sui ruoli del sistema del sito di Configuration Manager e su come aggiungerli per estendere la funzionalità e la capacità del sito.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8a4ef1c4377e7b5ffba4ab0f04394ff1253c40df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704899"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>Aggiungere ruoli del sistema del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Ogni sito di Configuration Manager supporta più ruoli del sistema del sito, ognuno dei quali estende la funzionalità e la capacità del sito per fornire servizi al sito e per gestire dispositivi e utenti. Ogni ruolo del sistema del sito in un server del sistema del sito deve provenire dallo stesso sito.

Configuration Manager non supporta i ruoli del sistema del sito per più siti in un unico server di sistema del sito.

> [!TIP]
> Se non si ha familiarità con i concetti di base relativi ai ruoli del sistema del sito o non si conosce la differenza tra server del sito, server del sistema del sito e ruoli del sistema del sito, vedere [Nozioni fondamentali di Configuration Manager](../../../understand/fundamentals.md).

Gli articoli seguenti descrivono le procedure e i relativi dettagli per l'installazione dei ruoli del sistema del sito:

- [Installare i ruoli del sistema del sito](install-site-system-roles.md): indicazioni di base su come usare le due procedure guidate nella console per installare nuovi ruoli del sistema del sito.

- [Installare punti di distribuzione basati sul cloud](install-cloud-based-distribution-points-in-microsoft-azure.md): usare Microsoft Azure per ospitare il contenuto distribuito ai client.

- [Installare ruoli del sistema del sito per Gestione dispositivi mobili (MDM) locali](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md): configurare correttamente i ruoli del sistema del sito in modo da supportare la gestione dei dispositivi moderni con MDM locale di Configuration Manager.

- [Opzioni di configurazione per i ruoli del sistema del sito](configuration-options-for-site-system-roles.md): Alcuni ruoli del sistema del sito supportano configurazioni che richiedono un numero di dettagli superiore a quello che può illustrare l'interfaccia utente.

- [Rimuovere un ruolo del sistema del sito](../install/uninstall-sites-and-hierarchies.md#bkmk_role): linee guida e procedure per rimuovere i ruoli dai server del sistema del sito.
