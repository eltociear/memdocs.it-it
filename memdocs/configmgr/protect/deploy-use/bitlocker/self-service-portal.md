---
title: Portale self-service di BitLocker
titleSuffix: Configuration Manager
description: Come usare il portale self-service degli utenti in Configuration Manager per il ripristino di BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699689"
---
# <a name="bitlocker-self-service-portal"></a>Portale self-service di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Dopo aver [installato il portale self-service di BitLocker](setup-websites.md), se BitLocker blocca il dispositivo di un utente, l'utente può accedere ai propri computer in modo indipendente. Per il portale self-service non è richiesta l'assistenza del personale dell'help desk.

[![Screenshot del portale self-service di BitLocker predefinito](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Per ottenere una chiave di ripristino dal portale self-service, un utente deve aver eseguito correttamente l'accesso al computer almeno una volta. Questo accesso deve essere locale nel dispositivo e non in una sessione remota. In caso contrario, è necessario contattare l'help desk per il recupero della chiave. Un amministratore dell'help desk può usare il [sito Web di amministrazione e monitoraggio](helpdesk-portal.md) per richiedere la chiave di ripristino.

BitLocker può bloccare il dispositivo nelle situazioni seguenti:

- L'utente dimentica la password o il PIN di BitLocker

- È stata apportata una modifica ai file del sistema operativo, al BIOS o al modulo TPM (Trusted Platform Module) del dispositivo

Per richiedere la chiave di ripristino di BitLocker dal portale self-service:

1. Quando BitLocker blocca un dispositivo, viene visualizzata la schermata di ripristino di BitLocker durante l'avvio. Prendere nota dell'ID della chiave di ripristino di BitLocker di 32 cifre.

1. In un altro computer, accedere al portale self-service nel Web browser, ad esempio `https://webserver.contoso.com/SelfService`.

1. Leggere e accettare il contratto.

1. Nel campo **ID chiave di ripristino** immettere le prime otto cifre dell'ID chiave di ripristino di BitLocker. Se corrisponde a più chiavi, immettere tutte le 32 cifre.

1. Come **Motivo** della richiesta scegliere una delle opzioni seguenti:

    - BIOS/TPM changed (BIOS/TPM modificato)
    - OS filed modified (Sistema operativo archiviato modificato)
    - Lost PIN/passphrase (PIN/passphrase persi)

1. Selezionare **Ottieni chiave**. Il portale self-service visualizza la **chiave di ripristino di BitLocker** di 48 cifre.

1. Immettere questo codice di 48 cifre nella schermata di ripristino di BitLocker nel computer.

> [!NOTE]
> È possibile che il portale self-service di BitLocker scada dopo un periodo di inattività. Ad esempio, dopo cinque minuti potrebbe essere visualizzato un avviso di timeout con un contatore di 60 secondi.
>
> ![Avviso di timeout del portale self-service di BitLocker](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Se non si risponde al conto alla rovescia, la sessione scadrà.
>
> ![Pagina scadenza della sessione del portale self-service di BitLocker](media/bitlocker-self-service-portal-session-expired.png)
