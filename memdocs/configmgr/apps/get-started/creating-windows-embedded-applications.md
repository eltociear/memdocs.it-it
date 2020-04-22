---
title: Creare applicazioni Windows Embedded
titleSuffix: Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Windows Embedded.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689839"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Creare applicazioni Windows Embedded con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni per i dispositivi Windows Embedded è necessario tenere presente quanto segue.  

## <a name="general-considerations"></a>Considerazioni generali  

-   Quando si distribuiscono applicazioni a dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare se disabilitare il filtro di scrittura sul dispositivo durante la distribuzione dell'app. È quindi possibile scegliere di riavviare il filtro di scrittura al termine della distribuzione dell'app. Se il filtro di scrittura non è disabilitato, il software viene distribuito a una sovrapposizione temporanea. Questo vuol dire che, a meno che un'altra distribuzione non forzi le modifiche per renderle permanenti, il software non verrà più installato al riavvio del dispositivo.  

-   Quando si distribuisce un'applicazione in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata. Ciò consente di decidere quando abilitare o disabilitare il filtro di scrittura nonché quando riavviare il dispositivo.  

-   L'impostazione che consente di controllare il comportamento del filtro di scrittura è una casella di controllo denominata **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** .  

## <a name="tips-for-deploying-applications"></a>Suggerimenti per la distribuzione di applicazioni  

**Usare le applicazioni richieste al posto delle applicazioni disponibili per i dispositivi con Windows Embedded con i filtri di scrittura abilitati.** Poiché gli utenti non possono installare le app da Software Center in un dispositivo con Windows Embedded con i filtri di scrittura abilitati, distribuire sempre le applicazioni con uno scopo della distribuzione **richiesto** al posto di **disponibile** per questi dispositivi. Questo problema in genere non dovrebbe verificarsi perché i computer che eseguono un sistema operativo Windows Embedded spesso eseguono una singola applicazione che deve essere eseguita allo stesso modo per più utenti. Per questo motivo, tali dispositivi vengono gestiti in modo avanzato e vengono bloccati dal reparto IT. Le applicazioni richieste sono particolarmente adatte per questo scenario.

 Se tuttavia gli utenti eseguono più di un'applicazione nei dispositivi incorporati con i filtri di scrittura attivati, illustrare a tali utenti le seguenti limitazioni:  

-   Gli utenti non possono installare il software richiesto da Software Center.  

-   Gli utenti non possono modificare l'orario di ufficio nella scheda Opzioni di Software Center.  

-   Gli utenti non possono rimandare l'installazione di un'applicazione richiesta.  

Gli utenti con diritti limitati inoltre non possono eseguire l'accesso durante un periodo di manutenzione se Configuration Manager sta eseguendo delle modifiche per gli aggiornamenti e le installazioni software. Durante questo periodo, viene visualizzato un messaggio che informa gli utenti che il dispositivo non è disponibile perché è in fase di manutenzione.  

**Se le applicazioni richiedono all'utente di accettare le condizioni di licenza, non distribuire tali applicazioni ai dispositivi con Windows Embedded con filtri di scrittura abilitati.** Quando i filtri di scrittura vengono disabilitati per consentire a Configuration Manager di installare software nei dispositivi incorporati, gli utenti con diritti limitati non possono eseguire l'accesso al dispositivo. Se l'installazione richiede all'utente di accettare le condizioni di licenza, non sarà possibile eseguire questa operazione e l'installazione avrà esito negativo. Assicurarsi di non distribuire software ai dispositivi con Windows Embedded se l'installazione richiede l'interazione dell'utente. È possibile usare l'elenco Piattaforme applicabili per filtrare questi sistemi operativi.  
