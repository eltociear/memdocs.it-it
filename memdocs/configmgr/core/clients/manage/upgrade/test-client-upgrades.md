---
title: Testare gli aggiornamenti client in una raccolta di pre-produzione
titleSuffix: Configuration Manager
description: Testare gli aggiornamenti client in una raccolta di pre-produzione in Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696839"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Come testare gli aggiornamenti client in una raccolta di pre-produzione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile testare una nuova versione del client di Configuration Manager in una raccolta di pre-produzione prima di aggiornare il resto del sito.  In questo caso, solo i dispositivi che fanno parte della raccolta di pre-produzione vengono aggiornati. Dopo aver testato il client, è possibile alzarlo di livello. In questo modo la nuova versione del software client viene resa disponibile per il resto del sito.

> [!NOTE]
> Per alzare di livello un client di test per renderlo disponibile per la produzione, è necessario eseguire l'accesso con un account utente con il ruolo di sicurezza **amministratore completo** e l'ambito di protezione **Tutto**. Per altre informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](../../../understand/fundamentals-of-role-based-administration.md). È anche necessario accedere a un server connesso al sito di amministrazione centrale o a un sito primario autonomo di livello superiore.

 Per testare i client in modalità di pre-produzione sono previsti 3 passaggi di base.  

1.  Configurare gli aggiornamenti automatici del client per usare una raccolta di pre-produzione.  

2.  Installare un aggiornamento di Configuration Manager che include una nuova versione del client.  

3.  Alzare il nuovo client al livello di produzione.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Per configurare gli aggiornamenti automatici del client per usare una raccolta di pre-produzione  
> [!IMPORTANT]
> La distribuzione di client di pre-produzione non è supportata per i computer di gruppi di lavoro poiché non possono usare l'autenticazione necessaria per il punto di distribuzione per accedere al pacchetto client di pre-produzione.  Quando viene promosso a client di produzione, riceveranno il client più recente.

1. [Impostare una raccolta](../collections/create-collections.md) che contiene i computer nei quali si vuole distribuire il client di pre-produzione.   

2. Nella console di Configuration Manager aprire **Amministrazione** > **Configurazione del sito** > **Siti** e scegliere **Impostazioni gerarchia**.  

    Nella scheda **Aggiornamento client** di **Proprietà impostazioni gerarchia**, eseguite le seguenti operazioni:  

   -   Selezionare **Aggiornare tutti i client della raccolta di preproduzione automaticamente utilizzando il client preproduzione**  

   -   Immettere il nome di una raccolta da utilizzare come raccolta preproduzione  

![Aggiornamenti automatici del client](media/test-client-upgrades.png)

>[!NOTE]
>Per modificare queste impostazioni, l'account deve essere un membro del ruolo di sicurezza **Amministratore completo** e dell'ambito di protezione **Tutti**.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Per installare un aggiornamento di Configuration Manager che include una nuova versione del client  

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Aggiornamenti e manutenzione**, selezionare un aggiornamento **Disponibile** e quindi scegliere **Installa pacchetto di aggiornamento**. Nelle versioni precedenti la 1702, Aggiornamenti e manutenzione si trova in **Amministrazione** > **Servizi cloud**.

     Per altre informazioni sull'installazione degli aggiornamenti, vedere [Aggiornamenti per Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante l'installazione dell'aggiornamento, nella pagina **Opzioni client** della procedura guidata selezionare **Convalida in una raccolta di pre-produzione**.  

3.  Completare il resto della procedura guidata e installare il pacchetto di aggiornamento.  

     Dopo aver completato la procedura guidata, i client nella raccolta di pre-produzione inizieranno a distribuire il client aggiornato. È possibile monitorare la distribuzione dei client aggiornati passando a **Monitoraggio** > **Stato del client** > **Distribuzione client di pre-produzione**. Per altre informazioni, vedere [Come monitorare lo stato di distribuzione dei client](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Lo stato della distribuzione nei computer che ospitano i ruoli del sistema del sito in una raccolta di pre-produzione può essere indicato come **Non conforme** anche quando il client è stato distribuito correttamente. Quando si promuove il client al livello di produzione, lo stato della distribuzione è segnalato in modo corretto.

##  <a name="to-promote-the-new-client-to-production"></a>Per alzare di livello il nuovo client al livello di produzione  

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Aggiornamenti e manutenzione** e quindi scegliere **Alza di livello il client di pre-produzione**. Nelle versioni precedenti la 1702, Aggiornamenti e manutenzione si trova in **Amministrazione** > **Servizi cloud**.

    > [!TIP]
    > Il pulsante **Alza di livello il client di pre-produzione** è disponibile anche durante il monitoraggio delle distribuzioni dei client nella console da **Monitoraggio** > **Stato del client** > **Distribuzione client di pre-produzione**.

2.  Rivedere le versioni client in produzione e pre-produzione, verificare che sia specificata la raccolta di pre-produzione corretta, fare clic su **Alza di livello** e poi su **Sì**.  

3.  Quando si chiude la finestra di dialogo, la versione aggiornata del client sostituirà quella attualmente in uso nella gerarchia. Sarà quindi possibile aggiornare i client per l'intero sito. Per altre informazioni, vedere [Come aggiornare i client per i computer Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

>[!NOTE]
>Per abilitare il client pre-produzione o per promuovere un client pre-produzione a un client di produzione, l'account deve essere un membro del ruolo di sicurezza che ha le autorizzazioni **Lettura** e **Modifica** per l'oggetto **Pacchetti di aggiornamento**.
>Per gli aggiornamenti client vengono rispettate tutte le finestre di manutenzione di Configuration Manager configurate.
