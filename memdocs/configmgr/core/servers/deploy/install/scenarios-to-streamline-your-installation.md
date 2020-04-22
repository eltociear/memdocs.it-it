---
title: Scenari di installazione
titleSuffix: Configuration Manager
description: Informazioni sulle tecniche di installazione di una nuova gerarchia di Configuration Manager durante l'aggiornamento di un sito.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700599"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Scenari per semplificare l'installazione di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con il rilascio di versioni di aggiornamento per Configuration Manager (Current Branch), diventano disponibili nuovi scenari per semplificare l'installazione di una nuova gerarchia in una versione di aggiornamento, ad esempio l'aggiornamento 1610, e per l'aggiornamento da Microsoft System Center 2012 Configuration Manager.

Gli scenari supportati includono:  

**Installare una nuova gerarchia di Configuration Manager (Current Branch)** che esegua una versione di aggiornamento.  

-   Installare solo il sito di livello superiore e quindi installare immediatamente un aggiornamento per aggiornare il sito alla versione di aggiornamento che verrà usata. Sarà possibile in seguito installare altri siti direttamente con la versione di aggiornamento.  
-   In questo scenario viene evitato il processo di installazione di siti aggiuntivi a un livello di base e il loro aggiornamento alla versione di aggiornamento che si vuole usare.  
-   In questo scenario viene evitato il processo di installazione di client in una versione di base e la loro reinstallazione al momento dell'aggiornamento a una versione più recente.  

**Aggiornare l'infrastruttura di Microsoft System Center 2012 Configuration Manager** a una versione di aggiornamento di Configuration Manager.  

-   Prima di installare una versione di aggiornamento, ad esempio la versione 1610, aggiornare manualmente il sito di amministrazione centrale e ogni sito primario a una versione di base, ad esempio alla versione 1606.  
-   Non aggiornare i siti secondari da Microsoft System Center 2012 Configuration Manager finché i siti primari non eseguono la versione di aggiornamento da usare.  
-   Non aggiornare i client da Microsoft System Center 2012 Configuration Manager finché i siti primari non eseguono la versione di aggiornamento da usare.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Scenario: installare una nuova gerarchia in una versione di aggiornamento  
In questo scenario di esempio si installa il primo sito di una gerarchia usando una versione di base di Configuration Manager, ad esempio la versione 1610. Quindi si installa l'aggiornamento 1610 prima di distribuire altri siti o client.  

-   Poiché si prevede di usare una versione di aggiornamento, ad esempio la versione 1610, anziché una versione di base, ad esempio la versione 1606, non è necessario installare altri siti e quindi aggiornarli. Ciò si applica anche ai client.  
-   Non installare siti secondari con la versione 1606 per poi aggiornarli alla versione 1610. Installare invece i siti secondari dopo che i siti primari eseguono la versione 1610.  

Seguire questa sequenza:  

1. **Installare un sito principale per la nuova gerarchia** usando il supporto di base.  

   -   È possibile usare il supporto di base solo per installare il primo sito di una nuova gerarchia.  
   -   Ad esempio, installare un sito principale usando la versione di base 1606. Per altre informazioni, vedere [Usare l'installazione guidata per installare i siti](use-the-setup-wizard-to-install-sites.md).  

   Dopo questo passaggio, il sito principale eseguirà la versione 1606.  

2. **Usare gli aggiornamenti nella console per aggiornare il sito principale a una versione più recente.**  

   -   Prima di installare eventuali client o siti figlio, aggiornare il sito principale alla versione di aggiornamento che si intende usare.  
   -   Ad esempio, un sito principale che esegue la versione 1606 può essere aggiornato alla versione 1610. Per altre informazioni, vedere [Aggiornamenti per Configuration Manager](../../../../core/servers/manage/updates.md).  

   Dopo questo passaggio, il sito principale eseguirà la versione 1610.  

3. **Installare nuovi siti primari figlio in un sito di amministrazione centrale.**  

   - Usare il supporto di installazione disponibile nella cartella CD.Latest sul server del sito di amministrazione centrale per installare i siti primari figlio. Per altre informazioni, vedere [Cartella CD.Latest per Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Questo supporto di origine è necessario per assicurare che i nuovi siti primari figlio corrispondano alla versione del sito di amministrazione centrale.  

   Dopo questo passaggio, i nuovi siti primari figlio eseguiranno la versione 1610.  

4. **In ogni sito primario usare l'opzione nella console per installare nuovi siti secondari.**  

   -   Poiché i siti secondari non sono stati installati quando i siti primari eseguivano la versione 1606, non è necessario aggiornarli.  
   -   Installare invece nuovi siti secondari che eseguono la versione 1610. Per altre informazioni, vedere la sezione relativa all'installazione di un [sito secondario](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) nell'argomento sull'[installazione dei siti con System Center Configuration Manager](use-the-setup-wizard-to-install-sites.md).  

   Dopo questo passaggio, verranno installati i nuovi siti secondari che eseguiranno la versione 1610.  

5. **Installare nuovi client nel sito primario.**  

   -   Poiché i client non sono stati installati quando i siti primari eseguivano la versione 1606, non è necessario aggiornarli dalla versione 1606 alla versione 1610.  
   -   Installare invece i nuovi client che eseguono la versione 1610. Per altre informazioni, vedere [Distribuire i client](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Dopo questo passaggio, verranno installati i nuovi client che eseguono la versione 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Scenario: aggiornare System Center 2012 Configuration Manager a una versione di aggiornamento di Configuration Manager (Current Branch)  

In questo scenario di esempio l'infrastruttura di System Center 2012 Configuration Manager viene aggiornata a una versione di aggiornamento di Configuration Manager (Current Branch), ad esempio la versione 1610.  

-   Il sito di amministrazione centrale e ogni sito primario devono eseguire l'aggiornamento alla versione di base 1606 prima di installare l'aggiornamento per la versione 1610.  
-   I siti secondari e i client non vengono aggiornati o installati con la versione 1606. Vengono invece spostati direttamente da System Center 2012 Configuration Manager a Configuration Manager (Current Branch) versione 1610.  

Seguire questa sequenza:  

1. **Aggiornare il sito principale di System Center 2012 Configuration Manager** a una versione Current Branch di base, ad esempio la versione 1606, usando i supporti di origine per Configuration Manager. Per altre informazioni, vedere [Eseguire l'aggiornamento a Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Come per gli scenari di aggiornamento tradizionali, si aggiorna sempre prima il sito principale della gerarchia e quindi i siti figlio.  

   Dopo questo passaggio, il sito principale eseguirà la versione 1606.  

2. **Aggiornare ogni sito primario figlio nella gerarchia** alla stessa versione di base.  

   -   Quando si esegue l'aggiornamento da Microsoft System Center 2012 Configuration Manager, è necessario aggiornare manualmente ogni sito primario a una versione di base Current Branch.  
   -   In questa fase non vengono aggiornati i siti secondari.  

   Dopo questo passaggio, ogni sito primario eseguirà la versione 1606.  

3. **Impostare le finestre di manutenzione nei siti primari figlio.** Dopo aver aggiornato tutti i siti primari alla versione di base, pianificare la configurazione di finestre di manutenzione per controllare quando quei siti installano aggiornamenti dell'infrastruttura. Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../../../core/clients/manage/collections/use-maintenance-windows.md).  Le finestre di manutenzione sono chiamate *intervalli di servizio* nella versione 1606.  

   -   Un sito primario figlio installa gli stessi aggiornamenti installati in un sito di amministrazione centrale.  
   -   I siti secondari non installano le nuove versioni automaticamente. È necessario aggiornarli manualmente dall'interno della console.  

   Dopo questo passaggio, quando si installano aggiornamenti nel sito di amministrazione centrale, verranno installati solo siti primari figlio che vengono aggiornati quando consentito dalla rispettiva finestra di manutenzione.  

4. **Installare la versione di aggiornamento nel sito principale.** Il sito principale viene aggiornato. Dopo che un sito di amministrazione centrale installa la versione di aggiornamento, ogni sito primario figlio installa automaticamente l'aggiornamento a meno che l'installazione non sia bloccata da una finestra di manutenzione.  

   -   Ad esempio, è possibile aggiornare il sito principale dalla versione 1606 alla versione 1610. Per altre informazioni, vedere [Aggiornamenti per Configuration Manager](../../../../core/servers/manage/updates.md).  

   Dopo questo passaggio, il sito di amministrazione centrale e ogni sito primario eseguirà la versione 1610.  

5. **Aggiornare i siti secondari.** Dopo che un sito primario installa l'aggiornamento ed esegue la versione 1610, usare l'opzione nella console per aggiornare i siti secondari.  

   -   In questo modo i siti secondari vengono aggiornati da Microsoft System Center 2012 Configuration Manager alla versione di aggiornamento installata nel sito primario.  
   -   Per informazioni sull'aggiornamento di un sito secondario, vedere [Aggiornare i siti](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) nell'argomento [Eseguire l'aggiornamento a Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6. **Aggiornare i client.** Per aggiornare i client, usare le informazioni in [Come aggiornare i client per i computer Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   In questo modo i client vengono aggiornati direttamente da Microsoft System Center 2012 Configuration Manager alla versione di aggiornamento installata nel sito primario.  

   Dopo questo passaggio, i client vengono aggiornati alla versione 1610 senza eseguire prima l'aggiornamento alla versione 1606.
