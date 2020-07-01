---
title: Gestire gli aggiornamenti rapidi di Windows 10
titleSuffix: Configuration Manager
description: Configuration Manager supporta file di installazione rapida per Windows 10, garantendo download più contenuti e tempi di installazione più rapidi per i client.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: ff018bc81ecdb3d11ebb71f1850804a5679c67f7
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746579"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gestire i file di installazione rapida per gli aggiornamenti di Windows 10

Configuration Manager supporta i file di installazione rapida per gli aggiornamenti di Windows 10. Configurare il client per scaricare solo le modifiche tra l'aggiornamento qualitativo cumulativo di Windows 10 del mese corrente e quello del mese precedente. Senza i file di installazione rapida, i client di Configuration Manager scaricano ogni mese l'aggiornamento cumulativo completo di Windows 10, che include tutti gli aggiornamenti dei mesi precedenti. Grazie ai file di installazione rapida sono possibili download più brevi e tempi di installazione più rapidi per i client.

Per informazioni su come usare Configuration Manager per gestire il contenuto di aggiornamento in modo da rimanere aggiornati con Windows 10, vedere [Ottimizzare il recapito degli aggiornamenti di Windows 10](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> Il supporto del client del sistema operativo è disponibile in Windows 10, versione 1607, con un aggiornamento dell'agente di Windows Update. Questo aggiornamento è incluso negli aggiornamenti rilasciati in data 11 aprile 2017. Per altre informazioni su questi aggiornamenti, vedere l'[articolo del supporto tecnico 4015217](https://support.microsoft.com/kb/4015217). Gli aggiornamenti futuri sfrutteranno i file di installazione rapida per download di dimensioni più contenute. Le versioni precedenti di Windows 10 e Windows 10 versione 1607 senza questo aggiornamento non supportano i file di installazione rapida.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Abilitare il sito per il download dei file di installazione rapida per gli aggiornamenti di Windows 10
Per avviare la sincronizzazione dei metadati per i file di installazione rapida di Windows 10, abilitarla nelle proprietà del punto di aggiornamento software.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.  

3. Nella barra multifunzione fare clic su **Configura componenti del sito** e quindi fare clic su **Punto di aggiornamento software**. Passare alla scheda **File di aggiornamento** e selezionare **Scarica i file completi per tutti gli aggiornamenti approvati e i file dell'installazione rapida per Windows 10**.

> [!NOTE]    
> Non è possibile configurare il componente del punto di aggiornamento software per scaricare *solo* gli aggiornamenti rapidi.  Il sito scarica i file di installazione rapida oltre ai file completi. In questo modo aumenta la quantità di contenuto archiviato nella raccolta contenuto e distribuito e archiviato nei punti di distribuzione.

> [!Tip]  
> Per determinare lo spazio effettivo usato su disco dal file, vedere la proprietà **Dimensioni su disco** del file. La proprietà Dimensioni su disco dovrebbe essere notevolmente inferiore rispetto al valore Dimensioni. Per altre informazioni, vedere [FAQs to optimize Windows 10 update delivery](optimize-windows-10-update-delivery.md#bkmk_faq).  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Abilitare i client per il download e l'installazione dei file di installazione rapida
Per abilitare il supporto dei file di installazione rapida per i client, abilitare i file di installazione rapida nel gruppo **Aggiornamenti software** delle impostazioni del client. Questa impostazione crea un nuovo listener HTTP che attende le richieste di download dei file di installazione rapida sulla porta specificata.

> [!NOTE]    
> Si tratta di una porta locale usata dai client per restare in ascolto delle richieste da Ottimizzazione recapito o dal Servizio trasferimento intelligente in background (BITS) per scaricare il contenuto rapido dal punto di distribuzione. Non è necessario aprire la porta nei firewall perché tutto il traffico è nel computer locale.  

Dopo aver distribuito le impostazioni client per abilitare questa funzionalità nel client, la funzionalità tenterà di scaricare le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. I client devono eseguire una versione di Windows 10 che supporti i file di installazione rapida.  

1. Abilitare il supporto per i file di installazione rapida nelle proprietà del componente del punto di aggiornamento software (procedura precedente).  

2. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare **Impostazioni client**.  

3. Selezionare le impostazioni client appropriate e fare clic su **Proprietà** sulla barra multifunzione.  

4. Selezionare il gruppo **Aggiornamenti software**. Specificare **Sì** per l'impostazione **Abilita l'installazione di file per l'installazione rapida nei client**. Configurare la **porta usata per scaricare il contenuto per gli aggiornamenti rapidi** con la porta usata dal listener HTTP nel client.
    - Nella versione 1902 **Abilita l'installazione di aggiornamenti rapidi nei client** è stato modificato in **Consenti ai client di scaricare contenuto differenziale quando disponibile**.
    - Nella versione 1902 l'impostazione **Porta usata per scaricare il contenuto per gli aggiornamenti rapidi** è stata modificata in **Porta usata dai client per ricevere richieste per contenuto differenziale**.
    

## <a name="next-steps"></a>Passaggi successivi

[Distribuire gli aggiornamenti software](deploy-software-updates.md)
