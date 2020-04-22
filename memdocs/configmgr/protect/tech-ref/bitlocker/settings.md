---
title: Informazioni di riferimento sulle impostazioni di BitLocker
titleSuffix: Configuration Manager
description: Tutte le impostazioni di gestione di BitLocker disponibili in Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6a9c566fec22e69c0a4a7fde01b911330ec1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708619"
---
# <a name="bitlocker-settings-reference"></a>Informazioni di riferimento sulle impostazioni di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!-- 5925683 -->

I criteri di gestione di BitLocker in Configuration Manager includono i gruppi di criteri seguenti:

- Installazione
- unità del sistema operativo
- Unità fissa
- Unità rimovibile
- Gestione dei client

Le sezioni seguenti descrivono e suggeriscono le configurazioni per le impostazioni in ogni gruppo.

> [!NOTE]
> Queste impostazioni sono basate su Configuration Manager versione 2002. La versione 1910 non include tutte queste impostazioni.

## <a name="setup"></a>Installazione

Le impostazioni in questa pagina consentono di configurare le opzioni di crittografia di BitLocker globali.

### <a name="drive-encryption-method-and-cipher-strength"></a>Metodo di crittografia dell'unità e livello di codifica

*Configurazione consigliata*: **Abilitato** con il metodo di crittografia predefinito o superiore.

> [!NOTE]
> La pagina delle proprietà **Installazione** include due gruppi di impostazioni per le diverse versioni di Windows. In questa sezione vengono descritti entrambi.

#### <a name="windows-81-devices"></a>Dispositivi Windows 8.1

Per i dispositivi Windows 8.1, abilitare l'opzione **Metodo di crittografia dell'unità e livello di codifica** e selezionare uno dei metodi di crittografia seguenti:

- AES a 128 bit con diffusione
- AES a 256 bit con diffusione
- AES a 128 bit (impostazione predefinita)
- AES a 256 bit

#### <a name="windows-10-devices"></a>Dispositivi Windows 10

Per i dispositivi Windows 10, abilitare l'opzione **Metodo di crittografia dell'unità e livello di codifica (Windows 10)** . Selezionare quindi singolarmente uno dei metodi di crittografia seguenti per le unità del sistema operativo, le unità dati fisse e le unità dati rimovibili:

- AES-CBC a 128 bit
- AES-CBC a 256 bit
- XTS-AES a 128 bit (impostazione predefinita)
- XTS-AES a 256 bit

> [!TIP]
> BitLocker usa Advanced Encryption Standard (AES) come algoritmo di crittografia con lunghezze di chiave configurabili di 128 o 256 bit. Nei dispositivi Windows 10 la crittografia AES supporta la modalità Cipher Block Chaining (CBC) o Ciphertext Stealing (XTS).
>
> Se è necessario usare un'unità rimovibile nei dispositivi che non eseguono Windows 10, usare AES-CBC.

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Note sull'utilizzo generale per la crittografia dell'unità e il livello di codifica

- Se queste impostazioni vengono disabilitate o non sono configurate, BitLocker userà il metodo di crittografia predefinito.

- Configuration Manager applica queste impostazioni quando si attiva BitLocker.

- Se l'unità è già crittografata o la crittografia è in corso, qualsiasi modifica apportata a queste impostazioni di criteri non cambia la crittografia dell'unità nel dispositivo.

- Se si usa il valore predefinito, nel report Conformità computer BitLocker il livello di codifica può essere visualizzato come **sconosciuto**. Per risolvere il problema, abilitare questa impostazione e impostare un valore esplicito per il livello di codifica.

### <a name="prevent-memory-overwrite-on-restart"></a>Non sovrascrivere la memoria al riavvio

*Configurazione consigliata*: **Non configurato**

Configurare questo criterio per migliorare le prestazioni di riavvio senza sovrascrivere i segreti BitLocker in memoria al riavvio.

Quando questo criterio non viene configurato, BitLocker rimuove i relativi segreti dalla memoria al riavvio del computer.

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Convalida conformità a regola di utilizzo dei certificati smart card

*Configurazione consigliata*: **Non configurato**

Configurare questo criterio per usare la protezione BitLocker basata su certificati smart card. Specificare quindi il certificato **Identificatore oggetto**.

Quando questo criterio non viene configurato, BitLocker usa l'identificatore oggetto predefinito `1.3.6.1.4.1.311.67.1.1` per specificare un certificato.

### <a name="organization-unique-identifiers"></a>Identificatori univoci dell'organizzazione

*Configurazione consigliata*: **Non configurato**

Configurare questo criterio per usare un agente di recupero dati basato su certificati o il lettore BitLocker To Go.

Quando questo criterio non viene configurato, BitLocker non usa il campo **Identificazione**.

Se l'organizzazione richiede misure di sicurezza più elevate, configurare il campo **Identificazione**. Impostare questo campo su tutti i dispositivi USB di destinazione e allinearlo con questa impostazione.

## <a name="os-drive"></a>Unità del sistema operativo

Le impostazioni in questa pagina consentono di configurare le impostazioni di crittografia per l'unità in cui è installato Windows.

### <a name="operating-system-drive-encryption-settings"></a>Impostazioni di crittografia per l'unità del sistema operativo

*Configurazione consigliata*: **Enabled**

Se si abilita questa impostazione, l'utente deve proteggere unità del sistema operativo e BitLocker crittografa l'unità. Se viene disabilitata, l'utente non può proteggere l'unità. Se non si configura questo criterio, non è necessaria la protezione BitLocker nell'unità del sistema operativo.

> [!NOTE]
> Se l'unità è già crittografata e si disabilita questa impostazione, BitLocker esegue la decrittografia dell'unità.  

Se si dispone di dispositivi privi di [TPM (Trusted Platform Module)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node), usare l'opzione **Consenti BitLocker senza TPM compatibile (password obbligatoria)** . Questa impostazione consente a BitLocker di crittografare l'unità del sistema operativo, anche se il dispositivo è privo di TPM. Se si consente questa opzione, Windows chiede all'utente di specificare una password di BitLocker.

Nei dispositivi con un TPM compatibile, all'avvio possono essere usati due tipi di metodi di autenticazione per fornire ulteriore protezione ai dati crittografati. Quando il computer viene avviato, è possibile usare solo il TPM per l'autenticazione oppure può anche essere necessario inserire un PIN. Configurare le seguenti impostazioni:

- **Select protector for operating system drive** (Selezionare la protezione per l'unità del sistema operativo): Configurarla per usare un TPM e un PIN oppure solo il TPM.

- **Configura lunghezza minima PIN per l'avvio**: Se si richiede un PIN, questo valore è la lunghezza più breve che l'utente può specificare. L'utente immette il PIN all'avvio del computer per sbloccare l'unità. Per impostazione predefinita, la lunghezza minima del PIN è `4`.

> [!TIP]
> Per una maggiore sicurezza, quando si abilitano dispositivi con protezione TPM e PIN, è consigliabile *disabilitare* le impostazioni di Criteri di gruppo seguenti in **Sistema** > **Risparmio energia** > **Impostazioni relative alla modalità sospensione**:
>
> - Consenti stati di standby (S1-S3) durante la sospensione (Alimentazione da rete elettrica)
>
> - Consenti stati di standby (S1-S3) durante la sospensione (A batteria)

### <a name="allow-enhanced-pins-for-startup"></a>Consenti PIN avanzati per l'avvio

*Configurazione consigliata*: **Non configurato**

Configurare BitLocker per l'uso di PIN avanzati per l'avvio. Questi I PIN consentono l'uso di caratteri aggiuntivi quali lettere in maiuscolo e minuscolo, simboli, numeri e spazi. Questa impostazione viene applicata quando si attiva BitLocker.

> [!IMPORTANT]
> Non tutti i computer supportano PIN avanzati nell'ambiente di preavvio. Prima di abilitarne l'uso, valutare se i dispositivi sono compatibili con questa funzionalità.

Se si abilita questa impostazione, tutti i nuovi PIN di avvio di BitLocker consentono all'utente di creare PIN avanzati.

- **Richiedi PIN solo ASCII**: consente di rendere i PIN avanzati maggiormente compatibili con i computer che limitano il tipo o il numero di caratteri che è possibile immettere nell'ambiente di preavvio.

Se si disabilita o non si configura l'impostazione di questo criterio, BitLocker non usa PIN avanzati.

### <a name="operating-system-drive-password-policy"></a>Criteri delle password per l'unità del sistema operativo

*Configurazione consigliata*: **Non configurato**

Usare queste impostazioni per impostare i vincoli per le password per sbloccare le unità del sistema operativo protette tramite BitLocker. Se si consentono protezioni non TPM nelle unità del sistema operativo, configurare le impostazioni seguenti:

- **Configurazione complessità della password per unità del sistema operativo**: per applicare i requisiti di complessità della password, selezionare **Richiedi complessità della password**.

- **Lunghezza minima password per unità del sistema operativo**: per impostazione predefinita, la lunghezza minima è `8`.

- **Richiedi password solo ASCII per unità del sistema operativo rimovibili**

Se si abilita l'impostazione di questo criterio, gli utenti possono configurare una password che soddisfi i requisiti definiti.

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Note sull'utilizzo generale per i criteri per le password dell'unità del sistema operativo

- Perché queste impostazioni dei requisiti di complessità abbiano effetto, abilitare anche l'impostazione di Criteri di gruppo **Le password devono essere conformi ai requisiti di complessità** in **Configurazione computer** > **Impostazioni di Windows** > **Impostazioni sicurezza** > **Criteri account** > **Criteri password**.

- BitLocker applica queste impostazioni quando viene attivato, non quando si sblocca un volume. BitLocker consente agli utenti di sbloccare un'unità con qualsiasi protezione disponibile.

- Se si usano i criteri di gruppo per abilitare algoritmi FIPS compatibili per crittografia, hash e firma, non si possono consentire le password come protezione per BitLocker.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Reimposta i dati di convalida della piattaforma dopo il ripristino di BitLocker

*Configurazione consigliata*: **Non configurato**

Controllare se Windows aggiorna i dati di convalida della piattaforma all'avvio dopo il ripristino di BitLocker.

Se si abilita o non si configura questa impostazione, Windows aggiorna i dati di convalida della piattaforma in questa situazione.

Se si disabilita l'impostazione di questo criterio, Windows non aggiorna i dati di convalida della piattaforma in questa situazione.

### <a name="pre-boot-recovery-message-and-url"></a>URL e messaggio di ripristino prima dell'avvio

*Configurazione consigliata*: **Non configurato**

Quando BitLocker blocca l'unità del sistema operativo, usare questa impostazione per visualizzare un URL o un messaggio di ripristino personalizzato nella schermata di ripristino di BitLocker prima dell'avvio. Questa impostazione si applica solo ai dispositivi Windows 10.

Quando si abilita questa impostazione, selezionare una delle opzioni seguenti per il messaggio di ripristino prima dell'avvio:

- **Usa URL e messaggio di ripristino predefiniti**: visualizzare l'URL e il messaggio di ripristino di BitLocker predefiniti nella schermata di ripristino di BitLocker prima dell'avvio. Se in precedenza è stato configurato un URL o un messaggio di ripristino personalizzato, usare questa opzione per ripristinare il messaggio predefinito.

- **Usa messaggio di ripristino personalizzato**: consente di includere un messaggio personalizzato nella schermata di ripristino di BitLocker prima dell'avvio.

  - **Opzione messaggio di recupero personalizzato**: digitare il messaggio personalizzato da visualizzare. Se si vuole specificare anche un URL di ripristino, includerlo come parte di questo messaggio di ripristino personalizzato. La lunghezza massima della stringa è 32.768 caratteri.

- **Usa URL di ripristino personalizzato**: consente di sostituire l'URL predefinito visualizzato nella schermata di ripristino di BitLocker prima dell'avvio.

  - **Opzione URL di recupero personalizzato**: digitare l'URL da visualizzare. La lunghezza massima della stringa è 32.768 caratteri.

> [!NOTE]
> Non tutti i caratteri e le lingue sono supportati prima dell'avvio. Testare innanzitutto il messaggio o l'URL personalizzato per assicurarsi che venga visualizzato correttamente nella schermata di ripristino di BitLocker prima dell'avvio.

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Impostazioni di imposizione dei criteri di crittografia (unità del sistema operativo)

*Configurazione consigliata*: **Enabled**

Configurare il numero di giorni per cui gli utenti possono posticipare la conformità di BitLocker per l'unità del sistema operativo. Il **periodo di tolleranza di non conformità** inizia quando Configuration Manager lo rileva per la prima volta come non conforme. Allo scadere di questo periodo di tolleranza, gli utenti non possono rimandare l'azione richiesta o richiedere un'esenzione.

Se il processo di crittografia richiede input utente, verrà visualizzata una finestra di dialogo in Windows che gli utenti non possono chiudere finché non specificano le informazioni necessarie. Le notifiche future per gli errori o lo stato non avranno questa restrizione.

Se BitLocker non richiede l'intervento dell'utente per aggiungere una protezione, allo scadere del periodo di tolleranza BitLocker avvia la crittografia in background.

Se si disabilita o non si configura questa impostazione, Configuration Manager non richiede che gli utenti siano conformi ai criteri di BitLocker.

Per applicare immediatamente il criterio, impostare un periodo di tolleranza di `0`.

## <a name="fixed-drive"></a>Unità fissa

Le impostazioni in questa pagina consentono di configurare la crittografia per le unità dati aggiuntive in un dispositivo.

### <a name="fixed-data-drive-encryption"></a>Crittografia dell'unità dati fissa

*Configurazione consigliata*: **Enabled**

Gestire i requisiti per la crittografia delle unità dati fisse. Se si abilita questa impostazione, BitLocker richiede agli utenti di proteggere tutte le unità dati fisse, quindi crittografa le unità dati.

Quando si abilita questo criterio, abilitare lo sblocco automatico o le impostazioni per **Criteri delle password per le unità dati fisse**.

- **Configura lo sblocco automatico per l'unità dati fissa**: consentire o richiedere a BitLocker di sbloccare automaticamente qualsiasi unità dati crittografata. Per usare lo sblocco automatico, è inoltre necessario che BitLocker crittografi l'[unità del sistema operativo](#os-drive).

Se non si configura questa impostazione, BitLocker non richiede agli utenti di proteggere le unità dati fisse.

Se si disabilita questa impostazione, gli utenti non potranno proteggere le unità dati fisse con BitLocker. Se si disabilita questo criterio dopo che BitLocker crittografa le unità dati fisse, BitLocker decrittografa le unità dati fisse.

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Nega accesso in scrittura per unità fisse non protette da BitLocker

*Configurazione consigliata*: **Non configurato**

Richiedere la protezione BitLocker per Windows per la scrittura di dati nelle unità fisse del dispositivo. BitLocker applica questo criterio quando lo si attiva.

Quando si abilita questa impostazione:

- Se BitLocker protegge un'unità dati fissa, Windows la monta con accesso in lettura e scrittura.

- Le unità dati fisse non protette con BitLocker vengono montate da Windows come di sola lettura.

Quando non si configura questa impostazione, Windows monta tutte le unità dati fisse con accesso in lettura e scrittura.

<!-- ### Allow access to BitLocker-protected fixed drives from earlier versions of Windows -->

### <a name="fixed-data-drive-password-policy"></a>Criteri delle password per le unità dati fisse

*Configurazione consigliata*: **Non configurato**

Usare queste impostazioni per impostare i vincoli per le password per sbloccare le unità dati fisse protette tramite BitLocker.

Se si abilita questa impostazione, gli utenti possono configurare una password che soddisfi i requisiti definiti.

Per una maggiore sicurezza, abilitare questa impostazione e quindi configurare le impostazioni seguenti:

- **Richiedi password per unità dati fissa**: gli utenti devono specificare una password per sbloccare un'unità dati fissa protetta tramite BitLocker.

- **Configurazione complessità della password per unità dati fisse**: per applicare i requisiti di complessità della password, selezionare **Richiedi complessità della password**.

- **Lunghezza minima password per unità dati fissa**: per impostazione predefinita, la lunghezza minima è `8`.

Se si disabilita questa impostazione, gli utenti non potranno configurare una password.

Quando il criterio non è configurato, BitLocker supporta le password con le impostazioni predefinite. Le impostazioni predefinite non includono i requisiti di complessità della password e richiedono solo otto caratteri.

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Note sull'utilizzo generale per i criteri per le password dell'unità dati fissa

- Perché queste impostazioni dei requisiti di complessità abbiano effetto, abilitare anche l'impostazione di Criteri di gruppo **Le password devono essere conformi ai requisiti di complessità** in **Configurazione computer** > **Impostazioni di Windows** > **Impostazioni sicurezza** > **Criteri account** > **Criteri password**.

- BitLocker applica queste impostazioni quando viene attivato, non quando si sblocca un volume. BitLocker consente agli utenti di sbloccare un'unità con qualsiasi protezione disponibile.

- Se si usano i criteri di gruppo per abilitare algoritmi FIPS compatibili per crittografia, hash e firma, non si possono consentire le password come protezione per BitLocker.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Impostazioni di imposizione dei criteri di crittografia (unità dati fissa)

*Configurazione consigliata*: **Enabled**

Configurare il numero di giorni per cui gli utenti possono posticipare la conformità di BitLocker per le unità dati fisse. Il **periodo di tolleranza di non conformità** inizia quando Configuration Manager rileva per la prima volta l'unità dati fissa come non conforme. Non impone i criteri per l'unità dati fissa finché l'unità del sistema operativo è conforme. Allo scadere del periodo di tolleranza, gli utenti non possono rimandare l'azione richiesta o richiedere un'esenzione.

Se il processo di crittografia richiede input utente, verrà visualizzata una finestra di dialogo in Windows che gli utenti non possono chiudere finché non specificano le informazioni necessarie. Le notifiche future per gli errori o lo stato non avranno questa restrizione.

Se BitLocker non richiede l'intervento dell'utente per aggiungere una protezione, allo scadere del periodo di tolleranza BitLocker avvia la crittografia in background.

Se si disabilita o non si configura questa impostazione, Configuration Manager non richiede che gli utenti siano conformi ai criteri di BitLocker.

Per applicare immediatamente il criterio, impostare un periodo di tolleranza di `0`.

## <a name="removable-drive"></a>Unità rimovibile

Le impostazioni in questa pagina consentono di configurare la crittografia per le unità rimovibili, come le chiavi USB.

### <a name="removable-data-drive-encryption"></a>Crittografia delle unità dati rimovibili

*Configurazione consigliata*: **Enabled**

Questa impostazione consente di controllare l'uso di BitLocker nelle unità rimovibili.

- **Consenti agli utenti di applicare la protezione BitLocker su unità dati rimovibili**: gli utenti possono attivare la protezione BitLocker per un'unità rimovibile.

- **Consenti agli utenti di sospendere e decrittografare BitLocker su unità dati rimovibili**: gli utenti possono rimuovere o sospendere temporaneamente la Crittografia unità BitLocker da un'unità rimovibile.

Quando si abilita questa impostazione e si consente agli utenti di applicare la protezione BitLocker, il client di Configuration Manager salva le informazioni di ripristino sulle unità rimovibili nel servizio di ripristino nel punto di gestione. Questo comportamento consente agli utenti di ripristinare l'unità se dimenticano o perdono la protezione (password).

Quando si abilita questa impostazione:

- Abilitare le impostazioni per **Criteri delle password per le unità dati rimovibili**

- *Disabilitare* le impostazioni di Criteri di gruppo seguenti in **Sistema** > **Accesso agli archivi rimovibili** per le configurazioni di utenti e computer:

  - **Tutte le classi di archivi rimovibili: nega tutti gli accessi**
  - **Dischi rimovibili: nega accesso in scrittura**
  - **Dischi rimovibili: nega accesso in lettura**

Se si disabilita questa impostazione, gli utenti non potranno usare BitLocker nelle unità rimovibili.

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Nega accesso in scrittura per unità rimovibili non protette da BitLocker

*Configurazione consigliata*: **Non configurato**

Richiedere la protezione BitLocker per Windows per la scrittura di dati nelle unità rimovibili del dispositivo. BitLocker applica questo criterio quando lo si attiva.

Quando si abilita questa impostazione:

- Se BitLocker protegge un'unità rimovibile, Windows la monta con accesso in lettura e scrittura.

- Le unità rimovibili non protette con BitLocker vengono montate da Windows come di sola lettura.

- Se si abilita l'opzione **Non consentire accesso in scrittura ai dispositivi configurati in un'altra organizzazione**, BitLocker concede solo l'accesso in scrittura alle unità rimovibili con campi di identificazione corrispondenti ai campi di identificazione consentiti. Definire questi campi con le impostazioni globali **Identificatori univoci dell'organizzazione** nella pagina [Installazione](#setup).

Quando si disabilita o non si configura questa impostazione, Windows monta tutte le unità rimovibili con accesso in lettura e scrittura.

> [!NOTE]
> È possibile eseguire l'override di questa impostazione con le impostazioni di Criteri di gruppo in **Sistema** > **Accesso agli archivi rimovibili**. Se si abilita l'impostazione di Criteri di gruppo **Dischi rimovibili: nega accesso in scrittura**, BitLocker ignora questa impostazione di Configuration Manager.

<!-- ### Allow access to BitLocker-protected removable data drives from earlier versions of Windows -->

### <a name="removable-data-drive-password-policy"></a>Criteri delle password per le unità dati rimovibili

*Configurazione consigliata*: **Enabled**

Usare queste impostazioni per impostare i vincoli per le password per sbloccare le unità rimovibili protette tramite BitLocker.

Se si abilita questa impostazione, gli utenti possono configurare una password che soddisfi i requisiti definiti.

Per una maggiore sicurezza, abilitare questa impostazione e quindi configurare le impostazioni seguenti:

- **Richiedi password per unità dati rimovibile**: gli utenti devono specificare una password per sbloccare un'unità rimovibile protetta tramite BitLocker.

- **Configurazione complessità della password per unità dati rimovibili**: per applicare i requisiti di complessità della password, selezionare **Richiedi complessità della password**.

- **Lunghezza minima password per unità dati rimovibile**: per impostazione predefinita, la lunghezza minima è `8`.

Se si disabilita questa impostazione, gli utenti non potranno configurare una password.

Quando il criterio non è configurato, BitLocker supporta le password con le impostazioni predefinite. Le impostazioni predefinite non includono i requisiti di complessità della password e richiedono solo otto caratteri.

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Note sull'utilizzo generale per i criteri per le password dell'unità dati rimovibile

- Perché queste impostazioni dei requisiti di complessità abbiano effetto, abilitare anche l'impostazione di Criteri di gruppo **Le password devono essere conformi ai requisiti di complessità** in **Configurazione computer** > **Impostazioni di Windows** > **Impostazioni sicurezza** > **Criteri account** > **Criteri password**.

- BitLocker applica queste impostazioni quando viene attivato, non quando si sblocca un volume. BitLocker consente agli utenti di sbloccare un'unità con qualsiasi protezione disponibile.

- Se si usano i criteri di gruppo per abilitare algoritmi FIPS compatibili per crittografia, hash e firma, non si possono consentire le password come protezione per BitLocker.

## <a name="client-management"></a>Gestione dei client

Le impostazioni in questa pagina consentono di configurare i client e i servizi di gestione di BitLocker.

### <a name="bitlocker-management-services"></a>Servizi di gestione di BitLocker

*Configurazione consigliata*: **Enabled**

Quando si abilita questa impostazione, Configuration Manager esegue in modo automatico e invisibile all'utente il backup delle informazioni di ripristino delle chiavi nel database del sito. Se si disabilita o non si configura questa impostazione, Configuration Manager non salva le informazioni di ripristino delle chiavi.

- **Selezionare le informazioni di ripristino di BitLocker da archiviare**: configurare il servizio di ripristino delle chiavi per eseguire il backup delle informazioni di ripristino di BitLocker. Fornisce un metodo amministrativo per il ripristino dei dati crittografati da BitLocker, che consente di evitare che vadano persi per mancanza di informazioni sulle chiavi.

- **Consenti l'archiviazione delle informazioni di ripristino come testo normale**: senza un certificato di crittografia di gestione di BitLocker per SQL Server, Configuration Manager archivia le informazioni di ripristino delle chiavi in testo normale. Per altre informazioni, vedere [Crittografare i dati di ripristino](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **Immettere la frequenza della verifica dello stato del client (minuti)** : in base alla frequenza configurata, il client controlla i criteri di protezione BitLocker e lo stato nel computer. Esegue inoltre il backup della chiave di ripristino del client. Per impostazione predefinita, il client di Configuration Manager aggiorna le informazioni di ripristino di BitLocker ogni 90 minuti.

### <a name="user-exemption-policy"></a>Criterio di esenzione utenti

*Configurazione consigliata*: **Non configurato**

Configurare un metodo di contatto per consentire agli utenti di richiedere un'esenzione dalla crittografia BitLocker.

Se si abilita l'impostazione di questo criterio, specificare le informazioni seguenti:

- **Numero massimo di giorni per il posticipo**: il numero di giorni per cui l'utente può posticipare un criterio applicato. Per impostazione predefinita, questo valore è `7` giorni (una settimana).

- **Metodo di contatto**: specificare il modo in cui gli utenti possono richiedere un'esenzione: URL, indirizzo e-mail o numero di telefono.

- **Contatto**: specificare l'URL, l'indirizzo e-mail o il numero di telefono. Quando un utente richiede un'esenzione dalla protezione BitLocker, viene visualizzata una finestra di dialogo di Windows con le istruzioni per la richiesta. Configuration Manager non convalida le informazioni immesse.

  - **URL**: usare il formato di URL standard, `https://website.domain.tld`. Windows visualizza l'URL come collegamento ipertestuale.

  - **Indirizzo di posta elettronica**: usare il formato di indirizzo e-mail standard, `user@domain.tld`. Windows visualizza l'indirizzo sotto forma del collegamento ipertestuale seguente: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`.

  - **Numero di telefono**: specificare il numero che si vuole venga chiamato dagli utenti. Windows visualizza il numero con la descrizione seguente: `Please call <your number> for applying exemption`.

Se si disabilita o non si configura questa impostazione, Windows non visualizza le istruzioni per la richiesta di esenzione per gli utenti.

> [!NOTE]
> BitLocker gestisce le esenzioni per utente, non per computer. Se più utenti effettuano l'accesso allo stesso computer e uno degli utenti non è esente, BitLocker crittografa il computer.

### <a name="url-for-the-security-policy-link"></a>URL per il collegamento ai criteri di sicurezza

*Configurazione consigliata*: **Enabled**

Specificare un URL da visualizzare agli utenti come **Criteri di sicurezza della società** in Windows. Usare questo collegamento per fornire agli utenti informazioni sui requisiti di crittografia. Viene visualizzato quando BitLocker chiede all'utente di crittografare un'unità.

Se si abilita questa impostazione, configurare l'**URL per il collegamento ai criteri di sicurezza**.

Se si disabilita o non si configura questa impostazione, BitLocker non visualizza il collegamento ai criteri di sicurezza.
