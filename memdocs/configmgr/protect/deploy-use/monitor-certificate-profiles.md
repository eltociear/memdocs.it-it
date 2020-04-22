---
title: Monitorare i profili certificato
titleSuffix: Configuration Manager
description: Informazioni su come monitorare lo stato di conformità dei profili certificato di Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706309"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Come monitorare i profili certificato in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visualizzare i risultati di conformità nella console di Configuration Manager  

Per monitorare la conformità dei certificati SCEP, usare i [report](#view-compliance-results-by-using-reports) invece della console. 

1. Nella console di Configuration Manager scegliere **Monitoraggio**>  **Distribuzioni**.  

2. Selezionare la distribuzione del profilo certificato desiderata.  

3. Controllare le informazioni di riepilogo sulla conformità del certificato nella pagina principale. Per informazioni più dettagliate, selezionare il profilo certificato, quindi nella scheda **Home**, nel gruppo **Distribuzione**, scegliere **Visualizza stato** per aprire la pagina **Stato distribuzione** .  

    La pagina **Stato distribuzione** contiene le seguenti schede:  

   -   **Conforme**: Visualizza la conformità del profilo certificato in base al numero degli asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti gli utenti che sono conformi al profilo del certificato. Il riquadro **Dettagli asset** visualizza anche gli utenti che sono conformi a questo profilo. Fare doppio clic su un utente nell'elenco per visualizzare altre informazioni.  

       > [!IMPORTANT]  
       >  Un profilo certificato non viene valutato se non è applicabile a un dispositivo client. Tuttavia, viene restituito come conforme.  

   -   **Errore**: Visualizza un elenco di tutti gli errori per la distribuzione del profilo certificato selezionata in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti gli utenti che hanno generato errori con questo profilo. Quando si seleziona un utente, il riquadro **Dettagli asset** visualizza gli utenti interessati dal problema selezionato. Fare doppio clic su un utente nell'elenco per visualizzare altre informazioni.  

   -   **Non conforme**: Visualizza un elenco di tutte le regole non conformi nel profilo certificato in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti gli utenti che non sono conformi a questo profilo. Quando si seleziona un utente, il riquadro **Dettagli asset** visualizza gli utenti interessati dal problema selezionato. Fare doppio clic su un utente nell'elenco per visualizzare informazioni aggiuntive sul problema.  

   -   **Sconosciuto**: Visualizza un elenco di tutti gli utenti che non sono conformi alla distribuzione del profilo certificato selezionata insieme allo stato client corrente dei dispositivi.  

4. Nella pagina **Stato distribuzione** esaminare le informazioni dettagliate sulla conformità del profilo certificato distribuito. Viene creato un nodo temporaneo nel nodo **Distribuzioni** che consente di ritrovare rapidamente queste informazioni.  

    Lo stato di registrazione del certificato viene visualizzato come un numero. Utilizzare la tabella seguente per comprendere il significato di ciascun numero:  


   | Stato registrazione |                                                                                                                   Descrizione                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         La registrazione ha avuto esito positivo e il certificato è stato rilasciato.                                                                                          |
   |    0x00000002     |                                                                    La richiesta è stata inviata e la registrazione è in sospeso o la richiesta è stata emessa fuori banda.                                                                    |
   |    0x00000004     |                                                                                                          La registrazione deve essere rinviata.                                                                                                           |
   |    0x00000010     |                                                                                                               Si è verificato un errore.                                                                                                                |
   |    0x00000020     |                                                                                                        Lo stato di registrazione è sconosciuto.                                                                                                        |
   |    0x00000040     | Le informazioni sullo stato sono state ignorate. Ciò può verificarsi se un'autorità di certificazione (collegamento ipertestuale "<https://msdn.microsoft.com/windows/ms721572>" \l "_security_certification_authority_gly") non è valida o non è stata selezionata per il monitoraggio. |
   |    0x00000100     |                                                                                                           La registrazione è stata negata.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Visualizzare i risultati di conformità usando i report

Le impostazioni di conformità in Configuration Manager includono report incorporati che è possibile usare per monitorare le informazioni sui profili certificato. Tali report dispongono della categoria report di **Gestione conformità e impostazioni**.  

> [!IMPORTANT]  
>  È necessario utilizzare un carattere jolly (%) quando si utilizzano i parametri **Filtro dispositivo** e **Filtro utente** nei report per le impostazioni di conformità.  

Per monitorare la conformità dei certificati SCEP, usare questi report sui certificati disponibili nel nodo dei report **Accesso risorse aziendali**:  

-   Cronologia di rilascio dei certificati  
-   Elenco degli asset con certificati prossimi alla scadenza  
-   Elenco degli asset per stato di rilascio del certificato  



 Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).  
