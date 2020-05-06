---
title: Definizioni malware di Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come configurare gli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni ai computer client.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126071"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Usare Configuration Manager per recapitare gli aggiornamenti delle definizioni

*Si applica a: Configuration Manager (Current Branch)*

È possibile configurare gli aggiornamenti software di Configuration Manager per recapitare automaticamente gli aggiornamenti delle definizioni ai computer client. Prima di iniziare a creare regole di distribuzione automatica, assicurarsi di configurare gli aggiornamenti software di Configuration Manager. Per altre informazioni, vedere [Introduzione agli aggiornamenti software](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Questa procedura è specifica per Endpoint Protection. Per altre informazioni generali sulle regole di distribuzione automatica, vedere [Distribuire automaticamente gli aggiornamenti software](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Aggiornamenti software** e quindi selezionare **Regole di distribuzione automatica**.

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea regola di distribuzione automatica**.

1. Nella pagina **Generale** della **Creazione guidata delle regole di distribuzione automatica**specificare le informazioni seguenti:

    - **Nome**: immettere un nome univoco per la regola di distribuzione automatica.

    - **Raccolta**: selezionare la raccolta di dispositivi in cui si vogliono distribuire gli aggiornamenti delle definizioni.

        > [!NOTE]
        > Non è possibile distribuire gli aggiornamenti delle definizioni in una raccolta utenti.

1. Selezionare **Aggiungi a un gruppo di aggiornamenti software**.

1. Selezionare **Abilita la distribuzione dopo l'esecuzione della regola**.

1. Nella pagina **Impostazioni distribuzione** della procedura guidata, in **Livello dettaglio** selezionare **Solo messaggi di errore**.

    > [!NOTE]
    > Quando si seleziona **Solo messaggi di errore** viene ridotto il numero di messaggi di stato inviati dalla distribuzione della definizione. Questa configurazione consente di ridurre l'elaborazione CPU nei server di Configuration Manager.

1. Nella pagina **Aggiornamenti software**:

    1. Selezionare il filtro proprietà **Classificazione aggiornamento**. Nell'elenco **Criteri di ricerca** selezionare **<elementi da trovare\>** .

        Nella finestra **Criteri di ricerca** selezionare **Aggiornamenti della definizione** e quindi selezionare **OK**.

    1. Selezionare il filtro proprietà **Prodotto**. Nell'elenco **Criteri di ricerca** selezionare **<elementi da trovare\>** .

        Nella finestra **Criteri di ricerca** selezionare **System Center Endpoint Protection** per Windows 8.1 e versioni precedenti o **Windows Defender** per Windows 10 e versioni successive e quindi selezionare **OK**.

    > [!NOTE]
    > Facoltativamente, è possibile filtrare gli aggiornamenti sostituiti. Selezionare il filtro proprietà **Sostituito**. Nell'elenco **Criteri di ricerca** selezionare **<elementi da trovare\>** . Nella finestra **Criteri di ricerca** selezionare **No** e quindi selezionare **OK**.

1. Nella pagina **Pianificazione valutazione** della procedura guidata selezionare **Esegui la regola dopo la sincronizzazione di un punto di aggiornamento software**.

1. Nella pagina **Pianificazione della distribuzione** della procedura guidata configurare le impostazioni seguenti:

    - **Tempo basato su**: per fare in modo che tutti i client installino le definizioni più aggiornate contemporaneamente, selezionare **UTC**. Il tempo di installazione effettivo può variare all'interno di una finestra di due ore.

    - **Tempo disponibile software**: specificare il tempo disponibile per la distribuzione creata da questa regola. Il tempo specificato deve essere almeno un'ora dopo l'esecuzione della regola di distribuzione automatica. Questa configurazione consente di assicurarsi che il contenuto abbia tempo sufficiente per la replica nei punti di distribuzione. Alcuni aggiornamenti delle definizioni possono includere anche aggiornamenti del motore antimalware, che potrebbero richiedere più tempo per raggiungere i punti di distribuzione.

    - **Scadenza installazione**: Selezionare **Appena possibile**.

        > [!NOTE]
        > Le scadenze degli aggiornamenti software variano entro un periodo di due ore. Questo comportamento impedisce che tutti i client richiedano un aggiornamento nello stesso momento.

1. Nella pagina **Esperienza utente** della procedura guidata selezionare **Nascondi in Software Center e nascondi tutte le notifiche** in **Notifiche utente**. Con questa configurazione gli aggiornamenti delle definizioni vengono installati automaticamente.

1. Nella pagina **Pacchetto di distribuzione** della procedura guidata selezionare un pacchetto di distribuzione esistente o crearne uno nuovo.

    > [!NOTE]
    > È consigliabile inserire gli aggiornamenti delle definizioni in un pacchetto che non contenga altri aggiornamenti software. In questo modo, le dimensioni del pacchetto di aggiornamenti delle definizioni resteranno contenute, consentendo una replica più veloce nei punti di distribuzione.

1. Se si crea un nuovo pacchetto di distribuzione, nella pagina **Punti di distribuzione** della procedura guidata selezionare uno o più punti di distribuzione. Il sito copia il contenuto del pacchetto in questi punti di distribuzione.

1. Nella pagina **Percorso download** selezionare **Scarica aggiornamenti software da Internet**.

1. Nella pagina **Selezione lingua** selezionare ogni versione linguistica degli aggiornamenti da scaricare.

1. Nella pagina **Impostazioni download** selezionare il comportamento di download degli aggiornamenti software necessario.

1. Completare la procedura guidata.

Verificare che la nuova regola venga visualizzata nel nodo **Regole di distribuzione automatica** della console di Configuration Manager.

> [!div class="nextstepaction"]
> [Creare e distribuire criteri antimalware](endpoint-antimalware-policies.md)
