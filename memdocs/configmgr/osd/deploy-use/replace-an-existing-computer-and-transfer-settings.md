---
title: Sostituire un computer esistente e trasferire le impostazioni
titleSuffix: Configuration Manager
description: In Configuration Manager, scegliere un metodo di distribuzione, ad esempio supporti di avvio, multicast o Software Center, per sostituire un computer esistente con uno nuovo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 860ee3aeb255921ccd8bf3b1695a9647b514752f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124869"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Sostituire un computer esistente e trasferire le impostazioni con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento illustra la procedura generale di Configuration Manager per sostituire un computer esistente con uno nuovo. Per questo scenario è possibile scegliere tra i numerosi e diversi metodi di distribuzione disponibili, ad esempio supporti di avvio, multicast o Software Center. È anche possibile scegliere di installare un punto di migrazione stato per archiviare le impostazioni e quindi ripristinarle nel nuovo sistema operativo dopo l'installazione. Se non si è sicuri che questo sia lo scenario di distribuzione del sistema operativo più adatto alle esigenze, vedere [Scenari per distribuire sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md).  

 Per informazioni su come aggiornare un computer esistente con una nuova versione di Windows, vedere le sezioni seguenti.  

##  <a name="plan"></a><a name="BKMK_Plan"></a> Pianificazione  

-   **Pianificare e implementare i requisiti di infrastruttura**  

     Per poter distribuire i sistemi operativi, è necessario soddisfare diversi requisiti di infrastruttura, ad esempio Windows ADK, Utilità di migrazione stato utente (USMT), Servizi di distribuzione Windows (WDS), configurazioni supportate del disco rigido e così via. Per altre informazioni, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

-   **Installare un punto di migrazione stato, obbligatorio solo se si trasferiscono le impostazioni**  

     Quando si prevede di acquisire le impostazioni dal computer esistente e quindi di ripristinarle nel nuovo sistema operativo, è necessario installare un punto di migrazione stato. Per altre informazioni, vedere [Punto di migrazione dello stato](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="configure"></a><a name="BKMK_Configure"></a> Configura  

1.  **Preparare un'immagine d'avvio**  

     Le immagini d'avvio avviano un computer in un ambiente Windows PE (un sistema operativo minimo con componenti e servizi limitati) che può quindi installare un sistema operativo Windows completo nel computer. Quando si distribuiscono sistemi operativi, è necessario selezionare un'immagine d'avvio da usare e distribuirla in un punto di distribuzione. Per preparare l'immagine d'avvio, vedere quanto segue:  

    -   Per altre informazioni sulle immagini d'avvio, vedere [Gestire le immagini di avvio](../get-started/manage-boot-images.md).  

    -   Per altre informazioni su come personalizzare un'immagine di avvio, vedere [Personalizzare immagini di avvio](../get-started/customize-boot-images.md).  

    -   Distribuire l'immagine d'avvio nei punti di distribuzione. Per ulteriori informazioni, vedere [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparare un'immagine del sistema operativo**  

     L'immagine del sistema operativo contiene i file necessari per installare il sistema operativo nel computer di destinazione. Per preparare l'immagine del sistema operativo, vedere quanto segue:  

    -   Per altre informazioni su come creare un'immagine del sistema operativo, vedere [Gestire immagini del sistema operativo](../get-started/manage-operating-system-images.md).  

    -   Distribuire l'immagine del sistema operativo nei punti di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Creare una sequenza di attività per distribuire sistemi operativi nella rete**  

     Usare una sequenza di attività per automatizzare l'installazione del sistema operativo nella rete. Usare i passaggi in [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) per creare la sequenza di attività per distribuire il sistema operativo. A seconda del metodo di distribuzione scelto, potrebbero essere necessarie considerazioni aggiuntive per la sequenza di attività.  

    > [!NOTE]  
    >  In questo scenario, se si acquisisce e si ripristinano le impostazioni e i file dell'utente, è possibile scegliere di usare un punto di migrazione stato o salvare i file in locale. Per altre informazioni, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> Distribuisci  

-   Usare uno dei metodi di distribuzione seguenti per distribuire il sistema operativo:  

    -   [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md) (Usare Software Center per distribuire Windows tramite la rete)  

    -   [Usare i supporti di avvio per distribuire Windows in rete](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Usare il multicast per distribuire Windows in rete](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Monitoraggio  

-   **Monitorare la distribuzione della sequenza di attività**  

     Per monitorare la distribuzione della sequenza di attività per l'installazione del sistema operativo, vedere [Monitorare le distribuzioni del sistema operativo](monitor-operating-system-deployments.md).  
