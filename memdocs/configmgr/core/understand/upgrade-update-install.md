---
title: Informazioni su upgrade, aggiornamento e installazione
titleSuffix: Configuration Manager
description: Informazioni sulla differenza tra i termini installazione, aggiornamento e upgrade per la gestione dell'infrastruttura di Configuration Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706719"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Informazioni su upgrade, aggiornamento e installazione per l'infrastruttura del sito e della gerarchia

*Si applica a: Configuration Manager (Current Branch)*

Quando si gestisce l'infrastruttura della gerarchia e dei siti di Configuration Manager, i termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti distinti.

## <a name="upgrade"></a>Upgrade

Il termine *upgrade* o *upgrade sul posto* viene usato per indicare la conversione del sito o della gerarchia di Configuration Manager 2012 in un sito o una gerarchia che esegue Configuration Manager Current Branch.

Quando si esegue l'upgrade di System Center 2012 Configuration Manager a Configuration Manager Current Branch, si continuano a usare gli stessi server per ospitare i siti e i server dei siti e si mantengono i dati e le configurazioni esistenti per Configuration Manager.  Questo comportamento è diverso dalla [migrazione](../migration/migrate-data-between-hierarchies.md), che è un modo per mantenere le configurazioni e i dati sui dispositivi gestiti usando però i nuovi siti di Configuration Manager Current Branch installati nel nuovo hardware.

Per altre informazioni, vedere [Eseguire l'aggiornamento a Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).



## <a name="update"></a>Aggiornamento
Il termine *aggiornamento* viene usato per indicare l'installazione di aggiornamenti nella console per Configuration Manager e gli aggiornamenti fuori banda che non possono essere distribuiti dall'interno della console di Configuration Manager. Gli aggiornamenti nella console possono modificare la versione del sito Current Branch (o Technical Preview) in modo da eseguire una versione successiva. Se ad esempio il sito esegue una versione 1806, è possibile installare un aggiornamento per la versione 1810. Gli aggiornamenti possono inoltre installare correzioni per un problema noto, senza modificare la versione dei siti.      

In genere, gli aggiornamenti aggiungono correzioni per la sicurezza, miglioramenti della qualità e nuove funzionalità alla distribuzione esistente. Se si usa il ramo Technical Preview, un aggiornamento può installare una versione più recente della Technical Preview.
- È l'utente stesso a scegliere quando installare l'aggiornamento nella console, a partire dal sito di livello superiore della gerarchia.
- È possibile installare qualsiasi aggiornamento disponibile dall'interno della console. Se ad esempio il sito esegue la versione 1802 e sono disponibili sia la 1806 sia la 1810, può essere opportuno installare la 1810 perché ogni versione include le funzionalità che sono state prima introdotte nelle versioni rilasciate in precedenza.
- Al termine dell'installazione di un nuovo aggiornamento nel sito di livello superiore, i siti primari figlio avviano automaticamente il processo di aggiornamento. È tuttavia possibile impostare [intervalli di servizio](../servers/manage/service-windows.md) per controllare i tempi di esecuzione degli aggiornamenti.
- I siti secondari non installano gli aggiornamenti automaticamente. Spetta all'utente avviare manualmente l'aggiornamento dall'interno della console di Configuration Manager.

Per altre informazioni, vedere [Aggiornamenti per Configuration Manager](../servers/manage/updates.md) e [Technical Preview per Configuration Manager](../get-started/technical-preview.md).



## <a name="install"></a>Installazione
Il termine *installazione* viene usato quando si crea una gerarchia di Configuration Manager completamente nuova o si aggiungono altri siti a una gerarchia esistente.  

Quando si installa un nuovo sito primario o di amministrazione centrale, il percorso del file setup.exe e dei file di origine correlati varia a seconda dello scenario di installazione.

Per altre informazioni, vedere [Preparare l'installazione di siti](../servers/deploy/install/prepare-to-install-sites.md).
