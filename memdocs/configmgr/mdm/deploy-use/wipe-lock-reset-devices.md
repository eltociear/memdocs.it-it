---
title: Gestire i dispositivi con MDM locale
titleSuffix: Configuration Manager
description: Proteggere i dati dei dispositivi con cancellazione completa, cancellazione selettiva, blocco remoto o reimpostazione del codice usando Configuration Manager gestione di dispositivi mobili (MDM) locale.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724725"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Gestire i dispositivi e proteggere i dati con MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I dispositivi mobili possono archiviare dati sensibili e fornire un accesso facile a numerose risorse aziendali. Per proteggere i dispositivi e i dati, usare Configuration Manager per le seguenti azioni di gestione dei dispositivi:

- **Cancellazione completa**: ripristinare le impostazioni di fabbrica del dispositivo

- **Cancellazione selettiva**: rimuovere solo i dati dell'organizzazione

- **Reimpostazione del codice**: rimuovere o reimpostare il codice quando un utente lo dimentica

- **Blocco remoto**: proteggere un dispositivo che potrebbe andare perso

## <a name="full-wipe"></a>Cancellazione completa  

Quando è necessario proteggere un dispositivo perso o quando si ritira un dispositivo dall'uso attivo, è possibile avviare una cancellazione completa su di esso. Questa azione consente di ripristinare le impostazioni predefinite del dispositivo. Vengono rimossi tutti i dati e le impostazioni dell'organizzazione e dell'utente.

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** e scegliere il nodo **dispositivi** . È anche possibile scegliere **Raccolte dispositivi** e selezionare una raccolta di cui il dispositivo è membro.

1. Selezionare il dispositivo che si desidera eliminare.

1. Sulla barra multifunzione, nel gruppo dispositivo selezionare **azioni dispositivo remoto**, quindi scegliere **ritira/Cancella**.

1. Nella finestra **ritira da Configuration Manager** selezionare l'opzione per **la cancellazione del dispositivo mobile e il ritiro da Configuration Manager**.

## <a name="selective-wipe"></a>Cancellazione selettiva

Per rimuovere solo i dati aziendali da un dispositivo, avviare una cancellazione selettiva.

### <a name="behaviors-by-os-version"></a>Comportamenti in base alla versione del sistema operativo

Le tabelle seguenti descrivono i dati che vengono rimossi e l'effetto sui dati che rimangono nel dispositivo dopo una cancellazione selettiva.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT

|Contenuto|Comportamento di cancellazione selettiva|  
|-------|--------|
|App e dati associati installati da Configuration Manager|Disinstalla le app e rimuove le chiavi di sideload. Revoca la chiave di crittografia per le app che usano la cancellazione selettiva di Windows e i dati non sono più accessibili.|
|Profili VPN e Wi-Fi|Rimuove i profili|
|Certificati|Rimuove e revoca i certificati|
|Impostazioni|Rimuove i requisiti|
|Profili di posta elettronica|Rimuove la posta elettronica abilitata per EFS, che include l'app di posta elettronica per i messaggi di posta elettronica e gli allegati di Windows.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1

|Contenuto|Comportamento di cancellazione selettiva|  
|-------|--------|
|App aziendali e dati associati installati da Configuration Manager|Disinstalla le app e rimuove i dati dell'app aziendale.|
|Profili VPN e Wi-Fi|Rimuove i profili per Windows 10 mobile e Windows Phone 8,1|
|Certificati|Rimuove i certificati per Windows Phone 8,1|
|Profili di posta elettronica|Rimuove i profili (eccetto Windows Phone 8,0)|

Le seguenti impostazioni vengono inoltre rimosse dai dispositivi Windows 10 Mobile e Windows Phone 8.1:  

- **Richiedi una password per sbloccare i dispositivi mobili**  
- **Consenti password semplici**  
- **Lunghezza minima password**  
- **Tipo di password richiesto**
- **Scadenza password (giorni)**  
- **Ricorda cronologia password**  
- **Numero di errori di accesso ripetuti consentiti prima della cancellazione del dispositivo**  
- **Minuti di inattività prima che venga richiesta la password**  
- **Tipo di password richiesto - numero minimo di set di caratteri**  
- **Consenti dispositivo foto/video**
- **Richiedi crittografia sui dispositivi mobili**  
- **Consenti archivi rimovibili**  
- **Consenti browser Web**  
- **Consenti archivio applicazioni**  
- **Consenti acquisizione schermo**  
- **Consenti georilevazione**  
- **Consenti account Microsoft**  
- **Consenti copia e incolla**  
- **Consenti tethering Wi-Fi**  
- **Consenti connessione automatica agli hotspot Wi-Fi gratuiti**  
- **Consenti creazione report degli hotspot Wi-Fi**  
- **Consenti ripristino impostazioni predefinite**
- **Consenti Bluetooth**  
- **Consenti NFC**
- **Consenti Wi-Fi**

### <a name="start-a-selective-wipe"></a>Avviare una cancellazione selettiva

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** e scegliere il nodo **dispositivi** . È anche possibile scegliere **Raccolte dispositivi** e selezionare una raccolta di cui il dispositivo è membro.

1. Selezionare il dispositivo che si desidera eliminare.

1. Sulla barra multifunzione, nel gruppo dispositivo selezionare **azioni dispositivo remoto**, quindi scegliere **ritira/Cancella**.

1. Nella finestra **ritira da Configuration Manager** selezionare la seguente opzione: **Cancella contenuto aziendale e ritira il dispositivo mobile da Configuration Manager**.

### <a name="recommendations-for-selective-wipe"></a>Suggerimenti per la cancellazione selettiva

- Per una cancellazione corretta della posta elettronica, configurare i profili di posta elettronica per i dispositivi Windows Phone 8,1.

- Per cancellare correttamente le app, assicurarsi che le app vengano distribuite con la gestione delle app per dispositivi mobili.

## <a name="passcode-reset"></a>Reimpostazione del passcode

Se un utente dimentica il proprio codice, usare questa azione per forzare un nuovo codice temporaneo nel dispositivo. È anche possibile rimuovere completamente il codice di accesso. La tabella seguente illustra il funzionamento della reimpostazione del passcode su diverse piattaforme per dispositivi mobili.

| Versione sistema operativo | Reimpostazione del passcode |
|------------|----------------|
| Windows 10 | Non supportate |
| Windows 10 Mobile | Supportato, esclusi i dispositivi aggiunti a Azure Active Directory |
| Windows Phone 8 e Windows Phone 8.1 | Supportato |
| Windows RT 8.1 | Non supportate |
| Windows 8.1 | Non supportate |

> [!Note]
> Avviare l'azione di reimpostazione del codice dal sito di livello superiore. Se ad esempio si usa un sito di amministrazione centrale, è possibile eseguire l'azione solo in tale sito. Se si usa un sito primario autonomo, è possibile eseguire l'azione solo da tale sito.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Reimpostare in modalità remota il codice di accesso in un dispositivo mobile

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** e scegliere il nodo **dispositivi** . È anche possibile scegliere **Raccolte dispositivi** e selezionare una raccolta di cui il dispositivo è membro.

1. Selezionare il dispositivo o i dispositivi per cui si desidera reimpostare il passcode.

1. Sulla barra multifunzione, nel gruppo dispositivo selezionare **azioni dispositivo remoto**, quindi scegliere **reimpostazione del codice**.  

### <a name="show-the-state-of-the-passcode-reset"></a>Mostra lo stato della reimpostazione del codice  

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** e scegliere il nodo **dispositivi** . È anche possibile scegliere **Raccolte dispositivi** e selezionare una raccolta di cui il dispositivo è membro.

1. Selezionare il dispositivo o i dispositivi per cui si desidera mostrare lo stato della reimpostazione del passcode.

1. Sulla barra multifunzione, nel gruppo dispositivo selezionare **azioni dispositivo remoto**, quindi scegliere **Mostra stato di codice**.  

## <a name="remote-lock"></a>Blocco remoto

Se un utente perde il dispositivo, è possibile bloccare il dispositivo in modalità remota. Nella tabella seguente è illustrato il funzionamento del blocco remoto su diverse piattaforme per dispositivi mobili.  

|Versione sistema operativo|Blocco remoto|
|----------|-----------|
|Windows 10|Non supportate|
|Windows Phone 8 e Windows Phone 8.1|Supportato|
|Windows RT 8.1|Supportato se l'utente corrente del dispositivo è lo stesso utente che ha registrato il dispositivo.|
|Windows 8.1|Supportato se l'utente corrente del dispositivo è lo stesso utente che ha registrato il dispositivo.|

> [!Note]
> Avviare l'azione di blocco remoto dal sito di livello superiore. Se ad esempio si usa un sito di amministrazione centrale, è possibile eseguire l'azione solo in tale sito. Se si usa un sito primario autonomo, eseguire l'azione da tale sito.

### <a name="remotely-lock-a-mobile-device"></a>Bloccare in remoto un dispositivo mobile

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** e scegliere il nodo **dispositivi** . È anche possibile scegliere **Raccolte dispositivi** e selezionare una raccolta di cui il dispositivo è membro.

1. Selezionare il dispositivo o i dispositivi da bloccare.

1. Nel gruppo dispositivo della barra multifunzione selezionare **azioni dispositivo remoto**, quindi scegliere **blocco remoto**. Confermare l'azione.

### <a name="show-the-state-of-the-remote-lock"></a>Mostra lo stato del blocco remoto

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** e scegliere il nodo **dispositivi** . È anche possibile scegliere **Raccolte dispositivi** e selezionare una raccolta di cui il dispositivo è membro.

1. Selezionare il dispositivo per cui si desidera mostrare lo stato del blocco remoto.

1. Sulla barra multifunzione, nel gruppo dispositivo selezionare **azioni dispositivo remoto**, quindi scegliere **Mostra stato blocco remoto**.
