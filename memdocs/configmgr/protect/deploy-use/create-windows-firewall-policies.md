---
title: Criteri di Windows Firewall per Endpoint Protection
titleSuffix: Configuration Manager
description: Questo argomento spiega come creare e distribuire criteri di Windows Firewall per Endpoint Protection in System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696959"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Creare e distribuire criteri di Windows Firewall per Endpoint Protection in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I criteri di Windows Firewall per Endpoint Protection in Configuration Manager consentono di eseguire le attività di configurazione e manutenzione di base di Windows Firewall nei computer client della gerarchia. È possibile usare i criteri di Windows Firewall per le attività seguenti:  

-   Controllare se Windows Firewall è attivato o disattivato.  

-   Controllare se sono consentite le connessioni in ingresso ai computer client.  

-   Controllare se gli utenti vengono informati quando Windows Firewall blocca un nuovo programma.  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection** e quindi fare clic su **Criteri di Windows Firewall**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea criteri di Windows Firewall**.  

4.  Nella pagina **Generale** di **Creazione guidata criteri di Windows Firewall**specificare un nome e una descrizione facoltativa per il criterio firewall e quindi fare clic su **Avanti**.  

5.  Nella pagina **Impostazioni profilo** della procedura guidata configurare le impostazioni seguenti per ogni profilo di connessione remota:  

    > [!NOTE]  
    >  Per altre informazioni sui profili di rete, vedere la documentazione di Windows.  

    -   **Attiva Windows Firewall**  

        > [!NOTE]  
        >  Se **Attiva Windows Firewall** non è attivato, le altre impostazioni in questa pagina della procedura guidata non sono disponibili.  

    -   **Blocca tutte le connessioni in ingresso, comprese quelle nell'elenco dei programmi consentiti**  

    -   **Notifica all'utente quando Windows Firewall blocca un nuovo programma**  

6.  Nella pagina **Riepilogo** della procedura guidata, rivedere le azioni da eseguire, quindi completare la procedura.  

7.  Verificare che venga visualizzato il nuovo criterio di Windows Firewall nell'elenco **Criteri di Windows Firewall** .  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Per distribuire un criterio di Windows Firewall  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection** e quindi fare clic su **Criteri di Windows Firewall**.  

3.  Nell'elenco **Criteri di Windows Firewall** selezionare il criterio di Windows Firewall che si vuole distribuire.  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

5.  Nella finestra di dialogo **Distribuisci criteri di Windows Firewall** specificare la raccolta a cui si vuole assegnare il criterio di Windows Firewall e specificare una pianificazione assegnazione. Il criterio di Windows Firewall valuta la conformità usando questa pianificazione e le impostazioni di Windows Firewall sui client da riconfigurare per soddisfare il criterio di Windows Firewall.  

6.  Fare clic su **OK** per chiudere la finestra di dialogo **Distribuisci criteri di Windows Firewall** e per distribuire il criterio di Windows Firewall.  

    > [!IMPORTANT]  
    >  Quando si distribuisce un criterio di Windows Firewall in una raccolta, il criterio viene applicato ai computer in un ordine casuale per un periodo di 2 ore per evitare di sovraccaricare la rete.
