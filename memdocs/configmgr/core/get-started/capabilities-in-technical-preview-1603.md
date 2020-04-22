---
title: Funzionalità nella Technical Preview 1603
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1603 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a60134e33449f2de181dd2dd39f4783383a889d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705639"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1603 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1603. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. In alternativa, quando si usa System Center Technical Preview 5, questa versione viene installata come una versione di base di Configuration Manager Technical Preview. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.  

 **Problemi noti di questa versione Technical Preview:**  

- Questa versione include gli aggiornamenti per le funzionalità rilasciate in precedenza ma non vengono introdotte nuove funzionalità. La pagina delle funzionalità della procedura guidata di aggiornamento sarà quindi vuota se in precedenza è stato eseguito l'aggiornamento alla versione 1602 e sono state abilitate tutte le funzionalità incluse nella versione 1602.  

- Dopo gli aggiornamenti del server del sito alla Technical Preview 1603, i client non possono usare le funzionalità di controllo remoto fino a quando non vengono anch'essi aggiornati alla versione 1603.  

  **Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a> Miglioramenti a Software Center  

### <a name="new-tiled-view-for-apps"></a>Nuova visualizzazione affiancata per le app  
 Gli utenti finali possono ora scegliere tra un elenco di app o una visualizzazione affiancata delle app nella scheda **Applicazioni** di Software Center.  

### <a name="select-multiple-updates-in-software-center"></a>Selezionare più aggiornamenti in Software Center  
 Nella scheda **Aggiornamenti** di Software Center è ora possibile selezionare più aggiornamenti oppure selezionare **Aggiorna tutto** per iniziare a installare più aggiornamenti contemporaneamente.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a> Miglioramenti del controllo remoto  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Limitare l'accesso agli Appunti condivisi in una sessione di controllo remoto  
 È ora possibile abilitare la nuova impostazione client degli strumenti remoti, **Richiedere all'utente l'autorizzazione per il trasferimento di file negli Appunti condivisi**, per limitare l'accesso agli Appunti condivisi in una sessione di controllo remoto.  

 Quando questa impostazione è abilitata, l'utente finale che condivide una sessione remota deve concedere le autorizzazioni a chi visualizza tale sessione in modo che questi utenti possano trasferire file dalla sessione al proprio computer locale usando gli Appunti condivisi.  

 Viene così aggiunto un livello di protezione per l'utente finale perché in precedenza, se all'utente che visualizzava veniva concesso il controllo completo sul computer dell'utente finale, questo poteva usare gli Appunti condivisi per trasferire i file dalla sessione al computer locale in modo completamente trasparente all'utente finale.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE  
 Nella Technical Preview 1603 è possibile personalizzare le dimensioni della finestra e del blocco TFTP RamDisk per i punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout perché le dimensioni del blocco o della finestra sono troppo grandi. La personalizzazione delle dimensioni della finestra e del blocco TFTP RamDisk consentono di ottimizzare il traffico TFTP quando si usa PXE per soddisfare requisiti di rete specifici.   
È necessario testare le impostazioni personalizzate nel proprio ambiente per stabilire quale sia la scelta più efficiente.  

-   **Dimensioni del blocco TFTP**: le dimensioni del blocco corrispondono alle dimensioni dei pacchetti di dati che vengono inviati dal server al client che sta scaricando il file (come descritto in RFC 2347). Dimensioni maggiori del blocco consentono al server di inviare meno pacchetti e di conseguenza si verificano meno ritardi per il round trip tra il server e client. Dimensioni del blocco grandi, tuttavia, comportano la creazione di pacchetti frammentati, che non sono supportati dalla maggior parte delle implementazioni di client PXE.  

-   **Dimensioni della finestra TFTP**: TFTP richiede un pacchetto di acknowledgment (ACK) per ogni blocco di dati inviato. Il server non invia il blocco successivo nella sequenza finché non riceve il pacchetto ACK per il blocco precedente. L'uso di finestre TFTP è una funzionalità di Servizi di distribuzione Windows che consente di definire quanti blocchi di dati sono necessari per riempire una finestra. Il server invia i blocchi di dati back-to-back fino a riempire la finestra e quindi il client invia un pacchetto ACK. Aumentando le dimensioni di questa finestra si riduce il numero di ritardi di round trip tra il client e il server, nonché il tempo complessivo necessario per scaricare un'immagine di avvio.  

### <a name="try-it-out"></a>Prova subito!  
 Provare a completare le attività seguenti e quindi usare il collegamento per l'invio di commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

-   È possibile personalizzare le dimensioni della finestra TFTP RamDisk nel punto di distribuzione abilitato per PXE.  

-   È possibile personalizzare le dimensioni del blocco TFTP RamDisk nel punto di distribuzione abilitato per PXE.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Per modificare le dimensioni della finestra TFTP RamDisk  

- Aggiungere la chiave del Registro di sistema seguente nei punti di distribuzione abilitati per PXE per personalizzare le dimensioni della finestra TFTP RamDisk:  

   **Location** (Percorso): HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nome: RamDiskTFTPWindowSize  

   **Tipo**: REG_DWORD  

   **Valore**: &lt;dimensioni finestra personalizzate\>  

  Il valore predefinito è 1 (1 blocco di dati riempie la finestra)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Per modificare le dimensioni del blocco TFTP RamDisk  

- Aggiungere la chiave del Registro di sistema seguente nei punti di distribuzione abilitati per PXE per personalizzare le dimensioni della finestra TFTP RamDisk:  

   **Location** (Percorso): HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nome: RamDiskTFTPBlockSize  

   **Tipo**: REG_DWORD  

   **Valore**: &lt;dimensioni blocco personalizzate\>  

  Il valore predefinito è 4096 (4k).  
