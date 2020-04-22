---
title: Monitorare profili di posta elettronica, Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Informazioni su come monitorare lo stato di conformità dei profili di posta elettronica, Wi-Fi e VPN in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709429"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Monitorare profili di posta elettronica, Wi-Fi e VPN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver distribuito i profili di posta elettronica, Wi-Fi o VPN in Configuration Manager agli utenti della gerarchia, è possibile usare le procedure seguenti per monitorare lo stato di conformità del profilo:  

-   [Come visualizzare i risultati di conformità nella console di Configuration Manager](#BKMK_console)  

-   [Come visualizzare i risultati di conformità usando i report](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Come visualizzare i risultati di conformità nella console di Configuration Manager  
 Seguire questa procedura per visualizzare i dettagli sulla conformità dei profili distribuiti nella console di Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Per visualizzare i risultati di conformità nella console di Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Distribuzioni**.  

3.  Nell'elenco **Distribuzioni** selezionare la distribuzione del profilo di cui si vuole verificare le informazioni sulla conformità.  

4.  È possibile vedere le informazioni di riepilogo sulla conformità della distribuzione del profilo nella pagina principale. Per visualizzare informazioni più dettagliate, selezionare la distribuzione del profilo, nella scheda **Home** del gruppo **Distribuzione**, fare clic su **Visualizza stato** per aprire la pagina **Stato distribuzione** .  

     La pagina **Stato distribuzione** contiene le seguenti schede:  

    -   **Conforme:** Visualizza la conformità del profilo in base al numero degli asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti conformi a questo profilo. Il riquadro **Dettagli asset** visualizza utenti che sono conformi al profilo. Fare doppio clic su un utente nell'elenco per visualizzare informazioni aggiuntive.  

        > [!IMPORTANT]  
        >  Un profilo non viene valutato se non è applicabile a un dispositivo client, però viene restituito come conforme.  

    -   **Errore:** Visualizza l'elenco di tutti gli errori per la distribuzione del profilo selezionata in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti che hanno generato errori con questo profilo. Quando si seleziona un utente, il riquadro **Dettagli asset** visualizza gli utenti interessati dal problema selezionato. Fare doppio clic su un utente nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Non conforme:** Visualizza un elenco di tutte le regole non conformi nel profilo in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti non conformi a questo profilo. Quando si seleziona un utente, il riquadro **Dettagli asset** visualizza gli utenti interessati dal problema selezionato. Fare doppio clic su un utente nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Sconosciuto:** Visualizza l'elenco di tutti gli utenti che non sono conformi con la distribuzione del profilo selezionato e lo stato client attuale dei dispositivi.  

5.  Nella pagina **Stato distribuzione** è possibile vedere informazioni dettagliate sulla conformità del profilo distribuito. Viene creato un nodo temporaneo nel nodo **Distribuzioni** che consente di ritrovare rapidamente queste informazioni.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> Come visualizzare i risultati di conformità usando i report  
 Le impostazioni di conformità, che includono profili in Configuration Manager, includono anche vari report predefiniti che consentono di monitorare le informazioni sui profili. Tali report dispongono della categoria report di **Gestione conformità e impostazioni**.  

> [!IMPORTANT]  
>  Usare un carattere jolly (%) quando si usano i parametri **Filtro dispositivo** e **Filtro utente** nei report delle impostazioni di conformità.  

 Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).  
