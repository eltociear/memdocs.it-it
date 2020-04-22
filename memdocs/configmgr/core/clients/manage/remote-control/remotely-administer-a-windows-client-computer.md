---
title: Gestire computer Windows in remoto
titleSuffix: Configuration Manager
description: Amministrare un computer client Windows da posizione remota tramite Configuration Manager.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696409"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Come amministrare in remoto un computer client Windows tramite Configuration Manager

*Si applica a: Configuration Manager (Current Branch)* Configuration Manager consente di connettersi ai computer client che usano **Controllo remoto di Configuration Manager**. Prima di iniziare a usare il controllo remoto, assicurarsi di aver letto le informazioni negli articoli seguenti:  

-   [Prerequisiti per il controllo remoto](prerequisites-for-remote-control.md)  

-   [Configurazione del controllo remoto](configuring-remote-control.md)  

Di seguito vengono elencati tre modi per avviare il visualizzatore controllo remoto:  

-   Dalla console di Configuration Manager.  

-   A un prompt dei comandi di Windows.  

-   Dal menu **Start** di Windows, in un computer che esegue la console di Configuration Manager, nel gruppo di programmi **Microsoft System Center**.  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Per amministrare un computer client in remoto dalla console di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Dispositivi** oppure **Raccolte di dispositivi**.  

3.  Selezionare il computer che si vuole gestire in remoto e quindi nel gruppo **Dispositivo** della scheda **Home** selezionare **Avvia** > **Controllo remoto**.  

    > [!IMPORTANT]  
    >  Se l'impostazione client **Richiedere all'utente l'autorizzazione di controllo remoto** è impostata su **True**, la connessione si avvia solo quando l'utente del computer remoto risponde affermativamente alla richiesta del controllo remoto. Per altre informazioni, vedere [Configurazione del controllo remoto](configuring-remote-control.md).  

4.  Quando la finestra **Controllo remoto di Configuration Manager** si apre, è possibile amministrare il computer client in remoto. Per configurare la connessione, usare le opzioni seguenti.  

    > [!NOTE]  
    >  Se il computer a cui ci si connette ha diversi monitor, nella finestra del controllo remoto viene visualizzato ciò che compare su tutti i monitor.  

    -   **File**
        - **Connetti** - Esegue la connessione a un altro computer. Questa opzione non è disponibile quando è attiva una sessione di controllo remoto.  
        -   **Disconnetti** - Disconnette la sessione di controllo remoto attiva ma non chiude la finestra **Controllo remoto di Configuration Manager**.  
        - **Esci** - Disconnette la sessione di controllo remoto attiva e chiude la finestra **Controllo remoto di Configuration Manager**.  

        > [!NOTE]  
        >  Quando si disconnette una sessione di controllo remoto, il contenuto degli Appunti di Windows nel computer che si sta visualizzando viene eliminato.


    - **Visualizza**
      - **Intensità colore** - Scegliere 16 bit o 32 bit per pixel.
      -  **Schermo intero** - Ingrandisce al massimo la finestra **Controllo remoto di Configuration Manager**. Per uscire dalla modalità schermo intero, premere CTRL+ALT+INTERR.  
      - **Ottimizza per connessione a larghezza di banda ridotta** - Selezionare questa opzione se la connessione ha larghezza di banda ridotta.
      - **Schermo:**
        - **Tutti gli schermi** - Opzione aggiunta in Configuration Manager 1902. Se il computer a cui ci si connette ha diversi monitor, nella finestra del controllo remoto viene visualizzato ciò che compare su tutti i monitor. **Tutti gli schermi** è l'unica visualizzazione per i computer con più monitor prima della versione 1902.
        -  **Primo schermo** - Opzione aggiunta in Configuration Manager 1902. Il *primo schermo* è quello visualizzato in alto all'estrema sinistra nelle impostazioni dello schermo di Windows. Non è possibile selezionare uno schermo specifico. Quando si cambia la configurazione del visualizzatore, riconnettersi alla sessione remota. Il visualizzatore salva le preferenze per le connessioni future.
        -  **Adatta** - Ridimensiona la visualizzazione del computer remoto in modo da adattarla alle dimensioni della finestra **Controllo remoto di Configuration Manager**.
        - **Barra di stato** - Attiva e disattiva la visualizzazione della barra di stato della finestra **Controllo remoto di Configuration Manager**.  

       > [!NOTE]  
       >  Il visualizzatore salva le preferenze per le connessioni future.

    -   **Azione**
        - **Invia CTRL+ALT+CANC** - Invia la combinazione di tasti CTRL+ALT+CANC al computer remoto. 
        - **Abilita condivisione Appunti** - Consente di copiare e incollare elementi nel e dal computer remoto. Se si modifica questo valore, per rendere effettiva la modifica è necessario riavviare la sessione di controllo remoto.   
          - Se non si vuole abilitare la condivisione degli Appunti nella console di Configuration Manager, impostare il valore della chiave del Registro di sistema **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** su **0** nel computer che esegue la console.
        - **Abilita tastiera e traduzione** - Converte il layout di tastiera del computer che esegue la console al layout del dispositivo connesso.
        - **Blocca tastiera e mouse remoti** - Blocca la tastiera e il mouse remoti per impedire all'utente di eseguire operazioni nel computer remoto.  

    -   **?**
        - **Informazioni su Controllo remoto** - Visualizza la versione corrente del visualizzatore.  

5.  Gli utenti del computer remoto possono visualizzare altre informazioni sulla sessione di controllo remoto facendo clic sull'icona **Controllo remoto** di Configuration Manager. L'icona è nell'area di notifica Windows o sulla barra della sessione di controllo remoto.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Per avviare il visualizzatore controllo remoto dalla riga di comando di Windows  

-   Al prompt dei comandi di Windows, digitare _<cartella di installazione di Configuration Manager\>_ **\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe supporta le opzioni da riga di comando seguenti:  

- *Indirizzo*: specifica il nome NetBIOS, il nome di dominio completo (FQDN) o l'indirizzo IP del computer client a cui ci si vuole connettere.
- *Nome del server del sito*: specifica il nome del server del sito di Configuration Manager al quale si vogliono inviare messaggi di stato relativi alla sessione di controllo remoto.
- **/?** : visualizza le opzioni da riga di comando per il visualizzatore controllo remoto.  
     
**Esempio: CmRcViewer.exe** *<Indirizzo\>* *<\\\Nome del server del sito>* 

> [!NOTE]  
> Il visualizzatore controllo remoto è supportato in tutti i sistemi operativi supportati per la console di Configuration Manager. Per altre informazioni, vedere [Configurazioni supportate per le console di Configuration Manager](../../../plan-design/configs/supported-operating-systems-consoles.md) e [Prerequisiti per il controllo remoto](prerequisites-for-remote-control.md).

## <a name="next-steps"></a>Passaggi successivi

[Controllare l'uso del controllo remoto](audit-remote-control-usage.md)
