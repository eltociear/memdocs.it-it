---
title: Definire limiti
titleSuffix: Configuration Manager
description: Di seguito viene spiegato come definire i percorsi di rete nella intranet che possono contenere i dispositivi da gestire.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704849"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definire percorsi di rete come limiti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I limiti di Configuration Manager sono costituiti dai percorsi di rete in cui sono contenuti i dispositivi da gestire. Il limite di un dispositivo è equivalente al sito di Active Directory o all'indirizzo IP di rete identificato dal client Configuration Manager installato nel dispositivo.
- È possibile creare manualmente i singoli limiti. Configuration Manager, tuttavia, non supporta l'immissione diretta di una supernet come limite. È possibile, invece, usare il tipo di limite Intervallo di indirizzi IP.
- È possibile configurare il metodo [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) per il rilevamento automatico e la creazione di limiti per ogni subnet IP e sito Active Directory individuati. Quando l'individuazione foresta Active Directory individua una supernet assegnata a un sito di Active Directory, Configuration Manager converte la supernet in un limite Intervallo di indirizzi IP.  

Non è raro che un dispositivo usi un indirizzo IP sconosciuto all'amministratore di Configuration Manager. Se il percorso di rete del dispositivo non è chiaro, verificare il percorso indicato dal dispositivo usando il comando **IPCONFIG** nel dispositivo.  

Quando si crea un limite, viene assegnato automaticamente un nome basato sul tipo e sull'ambito del limite. È impossibile modificare questo nome. Specificare invece una descrizione per identificare più facilmente il limite nella console di Configuration Manager.  

Ogni limite può essere usato da tutti i siti compresi nella gerarchia. Dopo aver creato un limite, è possibile modificarne le proprietà per eseguire le operazioni seguenti:  
- Aggiungere il limite a uno o più gruppi di limiti.  
- Modificare il tipo o l'ambito del limite.  
- Visualizzare la scheda **Sistemi del sito** dei limiti per vedere quali server del sistema del sito (punti di distribuzione, punti di migrazione stato e punti di gestione) sono associati al limite.  

## <a name="to-create-a-boundary"></a>Per creare un limite  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** > **Limiti**  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea Boundary**.  

3.  Nella scheda **Generale** della finestra di dialogo Crea limite è possibile specificare una **Descrizione** per identificare il limite tramite un nome descrittivo o un riferimento.  

4.  Selezionare un **Tipo** per questo limite:  

    - Se si seleziona **Subnet IP**, è necessario specificare un **ID subnet** per questo limite.  
      > [!TIP]  
      > È possibile specificare la **Rete** e la **Subnet Mask** per specificare automaticamente l' **ID subnet** . Quando si salva il limite, viene salvato solo il valore ID subnet.  

    - Se si seleziona **Sito Active Directory**, è necessario specificare o utilizzare **Sfoglia** per selezionare un sito Active Directory nella foresta locale del server del sito.  
        
      - Quando si specifica un sito Active Directory per un limite, il limite include ogni subnet IP appartenente a quel sito Active Directory. Se la configurazione del sito Active Directory viene modificata in Active Directory, verranno modificati anche i percorsi di rete inclusi in questo limite.  

      - I limiti del sito Active Directory non sono validi per i client Azure AD puri. Se effettuano il roaming locale non rientreranno in alcun limite se definiti soltanto usando siti AD.

    - Se si seleziona **Prefisso IPv6**, è necessario specificare un **Prefisso** nel formato del prefisso IPv6.  

    - Se si seleziona **Intervallo indirizzi IP**, è necessario specificare un **Indirizzo IP iniziale** e un **Indirizzo IP finale** che includano parte di una subnet IP o di più subnet IP.    

5.  Fare clic su **OK** per salvare il nuovo limite.  

## <a name="to-configure-a-boundary"></a>Per configurare un limite  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** > **Limiti**  

2.  Selezionare il limite da modificare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** per il limite selezionare la scheda **Generale** per modificare la **Descrizione** o il **Tipo** per il limite. È inoltre possibile modificare l'ambito di un limite modificando i percorsi di rete per il limite. Per un limite del sito Active Directory è possibile ad esempio specificare un nuovo nome del sito Active Directory.  

5.  Selezionare la scheda **Sistemi del sito** per visualizzare i sistemi del sito associati a questo limite. È impossibile modificare questa configurazione dalle proprietà di un limite.  

    > [!TIP]  
    > Per elencare un server di sistema del sito come sistema del sito per un limite, è necessario associare tale server come server di sistema del sito per almeno un gruppo di limiti che include questo limite. Questo viene configurato nella scheda **Riferimenti** di un gruppo di limiti.  

6.  Selezionare la scheda **Gruppi di limiti** per modificare l'appartenenza al gruppo di limiti per questo limite:  

    - Per aggiungere questo limite a uno o più gruppi di limiti, fare clic su **Aggiungi**, selezionare la casella di controllo per uno o più gruppi di limiti e quindi fare clic su **OK**.  

    - Per rimuovere questo limite da un gruppo di limiti, selezionare il gruppo di limiti e fare clic su **Rimuovi**.  

7.  Fare clic su **OK** per chiudere le proprietà del limite e salvare la configurazione.  
