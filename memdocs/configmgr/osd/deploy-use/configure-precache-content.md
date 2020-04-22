---
title: Configurare la pre-cache del contenuto
titleSuffix: Configuration Manager
description: Informazioni su come i client possono scaricare il contenuto della distribuzione di un sistema operativo prima che venga installata la sequenza di attività.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 184bdc58ac6dc0e311875cc1ddab8c605d8eec32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704209"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Configurare la pre-cache del contenuto per sequenze di attività

*Si applica a: Configuration Manager (Current Branch)*

<!--1021244-->
La funzionalità pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare il contenuto pertinente prima che un utente installi la sequenza di attività. Il client può usare la funzionalità di pre-cache del contenuto per le sequenze di attività che [aggiornano un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) o [installano un'immagine del sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).

> [!Note]  
> Nella versione 1910 Configuration Manager abilita questa funzionalità per impostazione predefinita. Nella versione 1906 o nelle versioni precedenti Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

Si supponga, ad esempio, di volere una sola sequenza di attività di aggiornamento sul posto per tutti gli utenti, pur avendo molte architetture e lingue diverse. Nelle versioni precedenti il download del contenuto inizia quando l'utente installa una distribuzione di sequenze di attività disponibile da Software Center. Questo ritardo aggiunge ulteriore tempo prima che l'installazione sia pronta per essere avviata. Tutto il contenuto a cui viene fatto riferimento nella sequenza di attività viene scaricato. Questo contenuto include il pacchetto di aggiornamento del sistema operativo per tutte le lingue e tutte le architetture. Se ogni pacchetto di aggiornamento è circa 3 GB, il contenuto totale è molto elevato.

Con la funzionalità pre-cache del contenuto è possibile consentire al client di scaricare solo il contenuto applicabile e tutto il contenuto a cui si fa riferimento non appena riceve la distribuzione. Quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto. L'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale.

In Configuration Manager versione 1902 e precedenti, questo comportamento si applica solo al *pacchetto di aggiornamento del sistema operativo*. Tale pacchetto è il solo il contenuto per il quale si specifica la lingua o l'architettura corrispondente. Ad esempio, se la sequenza di attività fa riferimento anche a più pacchetti driver, il client li scarica tutti. Il motore della sequenza di attività valuta le condizioni per i passaggi quando la sequenza di attività viene eseguita, non prima. Il client usa i tag nelle proprietà del pacchetto per determinare per quale contenuto eseguire la funzione pre-cache.

A partire dalla versione 1906,<!--4224642--> è ora possibile usarla per ridurre il consumo di larghezza di banda dei tipi di contenuto seguenti:

- Pacchetti di aggiornamento del sistema operativo
- Immagini dei sistemi operativi
- Pacchetti driver
- Pacchetti

## <a name="configure-pre-caching"></a>Configurare la funzionalità di pre-cache

La configurazione della funzionalità di pre-cache prevede tre passaggi:

1. [Creare e configurare i pacchetti](#bkmk_createpkg)
2. [Creare una sequenza di attività con passaggi condizionali](#bkmk_createts)
3. [Distribuire la sequenza di attività e abilitare la funzionalità di pre-cache](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a> 1. Creare e configurare i pacchetti

Il client valuta gli attributi dei pacchetti per determinare per quale contenuto eseguire la funzione pre-cache.  

#### <a name="os-upgrade-package"></a>Pacchetto di aggiornamento del sistema operativo

Creare [pacchetti di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) per lingue e architetture specifiche. Specificare i valori per **Architettura** e **Lingua** nella scheda **Origine dati** delle proprietà.

#### <a name="os-image"></a>Immagine del sistema operativo

Creare [immagini del sistema operativo](../get-started/manage-operating-system-images.md) per lingue e architetture specifiche. Specificare i valori per **Architettura** e **Lingua** nella scheda **Origine dati** delle proprietà.

#### <a name="driver-package"></a>Pacchetto driver

Creare [pacchetti driver](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) per modelli di hardware specifici. Specificare il **Modello** nella scheda **Generale** delle rispettive proprietà.

Per determinare quale pacchetto di driver scaricare durante la memorizzazione anticipata nella cache, il client valuta il modello rispetto alla proprietà **Name** della classe WMI **Win32_ComputerSystemProduct**.

> [!TIP]
> La query effettiva usa un'istruzione `LIKE` con caratteri jolly: `select * from win32_computersystemproduct where name like "%yourstring%"`. Se, ad esempio, si specifica `Surface` come modello, la query corrisponde a tutti i modelli che includono questa stringa.<!-- 6315551 -->

#### <a name="package"></a>Pacchetto

Creare [pacchetti](../../apps/deploy-use/packages-and-programs.md) per lingue e architetture specifiche. Specificare i valori per **Architettura** e **Lingua** nella scheda **Generale** delle proprietà.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a> 2. Creare una sequenza di attività

Creare una sequenza di attività con passaggi condizionali per le diverse lingue e architetture o per i diversi modelli di hardware per i pacchetti di driver.

|Content|Passaggio|
|---------|---------|
|Pacchetto di aggiornamento del sistema operativo|[Aggiornare il sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|Immagine del sistema operativo|[Applicare un'immagine del sistema operativo](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Pacchetto driver|[Applica pacchetto di driver](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Pacchetto|[Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Ad esempio, il passaggio di **aggiornamento del sistema operativo** seguente usa la versione in lingua inglese:  

![Editor delle sequenze di attività in cui sono visualizzati più passaggi di aggiornamento del sistema operativo per ENU, DEU e JPN](../media/precacheproperties2.png)

![Editor delle sequenze di attività, scheda Opzioni, in cui è visualizzata la query WQL WMI per Locale e OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> La query WMI seguente è consigliata per il sistema operativo in lingua inglese (Stati Uniti) e un'architettura a 64 bit:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Per prima cosa, aggiungere la lingua selezionando la condizione **Lingua del sistema operativo**. Modificare quindi la query WMI in modo da includere la clausola Architecture.


### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a> 3. Distribuire la sequenza di attività

[Distribuire la sequenza di attività](deploy-a-task-sequence.md). Per la funzionalità di pre-cache configurare le impostazioni seguenti:  

- Nella scheda **Generale** selezionare **Pre-download del contenuto per questa sequenza di attività**.  

- Nella scheda **Impostazioni di distribuzione** configurare la sequenza di attività selezionando **Disponibile**.  

- Nella scheda **Pianificazione** scegliere l'ora attualmente selezionata per l'impostazione **Pianifica quando questa distribuzione diventerà disponibile**. Il client avvia la funzionalità di pre-cache del contenuto nell'orario disponibile della distribuzione. Quando un client di destinazione riceve questo criterio, l'orario disponibile cade nel passato, quindi il download di pre-cache inizia immediatamente. Se il client riceve questo criterio ma l'orario disponibile è nel futuro, il client non avvia la funzionalità di pre-cache del contenuto fino all'orario disponibile.  

- Nella scheda **Punti di distribuzione** configurare le impostazioni **Opzioni di distribuzione**. Se non viene eseguita la funzione pre-cache prima che l'utente avvii l'installazione, il client usa queste impostazioni.  

    > [!Important]  
    > Per una sequenza di attività che installa un'immagine del sistema operativo, non usare l'opzione di distribuzione per **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività**. Se la sequenza di attività cancella il disco prima di applicare l'immagine del sistema operativo, la cache del client viene rimossa. Poiché il contenuto è andato perso, la sequenza di attività avrà esito negativo.<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>Esperienza utente

- Quando il client riceve i criteri di distribuzione, avvia la funzionalità pre-cache del contenuto dopo l'orario disponibile della distribuzione. Questo contenuto include tutti i pacchetti a cui si fa riferimento, ma solo il pacchetto di aggiornamento del sistema operativo che corrisponde agli attributi di architettura e lingua del pacchetto.  

- Quando il cliente rende disponibile la distribuzione agli utenti, una notifica informa gli utenti della nuova distribuzione e la sequenza di attività diventa visibile in Software Center. Per avviare l'installazione l'utente può passare a Software Center e fare clic su **Installa**.  

- Se la funzionalità di pre-cache del contenuto non è stata completamente eseguita quando l'utente installa la sequenza di attività, il client usa le impostazioni specificate nella scheda **Opzione di distribuzione** della distribuzione.  


## <a name="see-also"></a>Vedere anche

- [Creare una sequenza di attività per aggiornare un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Scenario di aggiornamento di Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)
