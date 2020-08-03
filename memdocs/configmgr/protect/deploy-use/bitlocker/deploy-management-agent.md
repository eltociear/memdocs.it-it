---
title: Distribuire la gestione di BitLocker
titleSuffix: Configuration Manager
description: Distribuire l'agente di gestione di BitLocker per i client di Configuration Manager e il servizio di ripristino ai punti di gestione
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 786a7a528c027ab46237dac92378224705b0e026
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262830"
---
# <a name="deploy-bitlocker-management"></a>Distribuire la gestione di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

La gestione di BitLocker in Configuration Manager include i componenti seguenti:

- **Agente di gestione di BitLocker**: Configuration Manager abilita questo agente in un dispositivo quando si [crea un criterio](#create-a-policy) e [lo si distribuisce a una raccolta](#deploy-a-policy).

- **Servizio di ripristino**: componente server che riceve i dati di ripristino di BitLocker dai client. Per altre informazioni, vedere [Servizio di ripristino](#recovery-service).

Prima di creare e distribuire i criteri di gestione di BitLocker:

- Esaminare i [prerequisiti](../../plan-design/bitlocker-management.md#prerequisites)

- Se necessario, [crittografare le chiavi di ripristino](encrypt-recovery-data.md) nel database del sito

## <a name="create-a-policy"></a>Creare un criterio

Quando si crea e si distribuisce questo criterio, il client di Configuration Manager abilita l'agente di gestione di BitLocker nel dispositivo.

> [!NOTE]
> Per creare un criterio di gestione di BitLocker, è necessario il ruolo di **amministratore completo** in Configuration Manager.

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Endpoint Protection** e selezionare il nodo **Gestione di BitLocker**.

1. Nella barra multifunzione selezionare **Crea un criterio di controllo di gestione di BitLocker**.

1. Nella pagina **Generale** specificare un nome e una descrizione facoltativa. Selezionare i componenti da attivare nei client con questi criteri:  

    - **Unità sistema operativo**: Decidere se l'unità del sistema operativo è crittografata

    - **Unità fissa**: gestire la crittografia per altre unità dati in un dispositivo

    - **Unità rimovibile**: gestire la crittografia per le unità che è possibile rimuovere da un dispositivo, ad esempio una chiave USB

    - **Gestione dei client**: Gestire il backup del servizio di recupero chiave per le informazioni di ripristino di Crittografia unità BitLocker  

1. Nella pagina **Installazione** configurare le impostazioni globali seguenti per Crittografia unità BitLocker:

    > [!NOTE]
    > Configuration Manager applica queste impostazioni quando si abilita BitLocker. Se l'unità è già crittografata o la crittografia è in corso, qualsiasi modifica apportata a queste impostazioni di criteri non cambia la crittografia dell'unità nel dispositivo.
    >
    > Se queste impostazioni vengono disabilitate o non sono configurate, BitLocker userà il metodo di crittografia predefinito (AES 128 bit).

    - Per i dispositivi Windows 8.1, abilitare l'opzione **Metodo di crittografia dell'unità e livello di codifica**. Selezionare quindi il metodo di crittografia.

    - Per i dispositivi Windows 10, abilitare l'opzione **Metodo di crittografia dell'unità e livello di codifica (Windows 10)** . Selezionare quindi singolarmente il metodo di crittografia per le unità del sistema operativo, le unità dati fisse e le unità dati rimovibili.

    Per altre informazioni su queste e altre impostazioni in questa pagina, vedere [Informazioni di riferimento sulle impostazioni - Installazione](../../tech-ref/bitlocker/settings.md#setup).

1. Nella pagina **Unità sistema operativo** specificare le impostazioni seguenti:  

    - **Crittografia per le unità del sistema operativo**: Se si abilita questa impostazione, l'utente deve proteggere unità del sistema operativo e BitLocker crittografa l'unità. Se viene disabilitata, l'utente non può proteggere l'unità.  

    Nei dispositivi con un TPM compatibile, all'avvio possono essere usati due tipi di metodi di autenticazione per fornire ulteriore protezione ai dati crittografati. Quando il computer viene avviato, è possibile usare solo il TPM per l'autenticazione oppure può anche essere necessario inserire un PIN. Configurare le seguenti impostazioni:

    - **Select protector for operating system drive** (Selezionare la protezione per l'unità del sistema operativo): Configurarla per usare un TPM e un PIN oppure solo il TPM.

    - **Configura lunghezza minima PIN per l'avvio**: Se si richiede un PIN, questo valore è la lunghezza più breve che l'utente può specificare. L'utente immette il PIN all'avvio del computer per sbloccare l'unità. Per impostazione predefinita, la lunghezza minima del PIN è `4`.

    Per altre informazioni su queste e altre impostazioni in questa pagina, vedere [Informazioni di riferimento sulle impostazioni - Unità del sistema operativo](../../tech-ref/bitlocker/settings.md#os-drive).

1. Nella pagina **Unità fissa** specificare le impostazioni seguenti:

    - **Crittografia per le unità dati fisse**: se si abilita questa impostazione, BitLocker richiede agli utenti di proteggere tutte le unità dati fisse, quindi crittografa le unità dati. Quando si abilita questo criterio, abilitare lo sblocco automatico o le impostazioni per **Criteri delle password per le unità dati fisse**.

    - **Configura lo sblocco automatico per l'unità dati fissa**: consentire o richiedere a BitLocker di sbloccare automaticamente qualsiasi unità dati crittografata. Per usare lo sblocco automatico, è inoltre necessario che BitLocker crittografi l'unità del sistema operativo.

    Per altre informazioni su queste e altre impostazioni in questa pagina, vedere [Informazioni di riferimento sulle impostazioni - Unità fissa](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. Nella pagina **Unità rimovibile** specificare le impostazioni seguenti:

    - **Crittografia delle unità dati rimovibili**: quando si abilita questa impostazione e si consente agli utenti di applicare la protezione BitLocker, il client di Configuration Manager salva le informazioni di ripristino sulle unità rimovibili nel servizio di ripristino nel punto di gestione. Questo comportamento consente agli utenti di ripristinare l'unità se dimenticano o perdono la protezione (password).

    - **Consenti agli utenti di applicare la protezione BitLocker su unità dati rimovibili**: gli utenti possono attivare la protezione BitLocker per un'unità rimovibile.

    - **Criteri delle password per le unità dati rimovibili**: usare queste impostazioni per impostare i vincoli per le password per sbloccare le unità rimovibili protette tramite BitLocker.

    Per altre informazioni su queste e altre impostazioni in questa pagina, vedere [Informazioni di riferimento sulle impostazioni - Unità rimovibile](../../tech-ref/bitlocker/settings.md#removable-drive).

1. Nella pagina **Gestione dei client** specificare le impostazioni seguenti:

    > [!IMPORTANT]
    > Se non si dispone di un punto di gestione con un sito Web abilitato per HTTPS, non configurare questa impostazione. Per altre informazioni, vedere [Servizio di ripristino](#recovery-service).

    - **Configura i servizi di gestione di BitLocker**: quando si abilita questa impostazione, Configuration Manager esegue in modo automatico e invisibile all'utente il backup delle informazioni di ripristino delle chiavi nel database del sito. Se si disabilita o non si configura questa impostazione, Configuration Manager non salva le informazioni di ripristino delle chiavi.

        - **Selezionare le informazioni di ripristino di BitLocker da archiviare**: Configurare l'impostazione per usare un pacchetto di password e chiave di ripristino o semplicemente una password di ripristino.

        - **Consenti l'archiviazione delle informazioni di ripristino come testo normale**: senza un certificato di crittografia di gestione di BitLocker, Configuration Manager archivia le informazioni di ripristino della chiave in testo normale. Per altre informazioni, vedere [Crittografare i dati di ripristino](encrypt-recovery-data.md).

    Per altre informazioni su queste e altre impostazioni in questa pagina, vedere [Informazioni di riferimento sulle impostazioni - Gestione dei client](../../tech-ref/bitlocker/settings.md#client-management).

1. Completare la procedura guidata.

Per modificare le impostazioni di un criterio esistente, selezionarlo dall'elenco e selezionare **Proprietà**.

Quando si crea più di un criterio, è possibile configurarne la priorità relativa. Se si distribuiscono più criteri a un client, viene usato il valore di priorità per determinarne le impostazioni.

## <a name="deploy-a-policy"></a>Distribuire un criterio

1. Scegliere un criterio esistente nel nodo **Gestione di BitLocker**. Nella barra multifunzione selezionare **Distribuisci**.

1. Selezionare una raccolta di dispositivi come destinazione della distribuzione.

1. Se si vuole che il dispositivo sia in grado di crittografare o decrittografare le proprie unità in qualsiasi momento, selezionare l'opzione **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione**. Se la raccolta ha una finestra di manutenzione, risolve comunque questo criterio di BitLocker.

1. Configurare una pianificazione **Semplice** o **Personalizzata**. Il client valuta la conformità in base alle impostazioni specificate nella pianificazione.

1. Selezionare **OK** per distribuire il criterio.

È possibile creare più distribuzioni dello stesso criterio. Per visualizzare altre informazioni su ogni distribuzione, selezionare il criterio nel nodo **Gestione di BitLocker** e quindi nel riquadro dei dettagli passare alla scheda **Distribuzioni**.

## <a name="monitor"></a>Monitoraggio

Visualizzare le statistiche di conformità di base sulla distribuzione del criterio nel riquadro dei dettagli del nodo **Gestione di BitLocker**:

- Conteggio di conformità
- Conteggio errori
- Conteggio di mancata conformità

Passare alla scheda **Distribuzioni** per visualizzare la percentuale di conformità e l'azione consigliata. Selezionare la distribuzione e quindi nella barra multifunzione selezionare **Visualizza stato**. Questa azione cambia la visualizzazione sostituendola con l'area di lavoro **Monitoraggio**, nodo **Distribuzioni**. Analogamente alla distribuzione di altre distribuzioni dei criteri di configurazione, in questa vista è possibile visualizzare uno stato di conformità più dettagliato.

Per comprendere il motivo per cui i client risultano non conformi ai criteri di gestione di BitLocker, vedere [Codici di non conformità](../../tech-ref/bitlocker/non-compliance-codes.md).

Per altre informazioni sulla risoluzione dei problemi, vedere [Risolvere i problemi relativi a BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Usare i log seguenti per il monitoraggio e la risoluzione dei problemi:

### <a name="client-logs"></a>Log del client

- Registro eventi MBAM: nel Visualizzatore eventi di Windows, passare ad Applicazioni e servizi > Microsoft > Windows > MBAM.  Per altre informazioni, vedere [Informazioni sui registri eventi di BitLocker](../../tech-ref/bitlocker/about-event-logs.md) e [Registri eventi del client](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler.log** nel percorso dei log del client, `%WINDIR%\CCM\Logs` per impostazione predefinita

### <a name="management-point-logs-recovery-service"></a>Log del punto di gestione (servizio di ripristino)

- Registro eventi del servizio di ripristino: nel Visualizzatore eventi di Windows, passare ad Applicazioni e servizi > Microsoft > Windows > MBAM-Web. Per altre informazioni, vedere [Informazioni sui registri eventi di BitLocker](../../tech-ref/bitlocker/about-event-logs.md) e [Registri eventi del server](../../tech-ref/bitlocker/server-event-logs.md).

- Log di traccia del servizio di ripristino: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Servizio di ripristino

Il servizio di ripristino di BitLocker è un componente server che riceve i dati di ripristino di BitLocker dai client di Configuration Manager. Il sito distribuisce il servizio di ripristino quando si crea un criterio di gestione di BitLocker. Configuration Manager installa automaticamente il servizio di ripristino in ogni punto di gestione con un sito Web abilitato per HTTPS.

Configuration Manager archivia le informazioni di ripristino nel database del sito. Senza un certificato di crittografia di gestione di BitLocker, Configuration Manager archivia le informazioni di ripristino della chiave in testo normale.

Per altre informazioni, vedere [Crittografare i dati di ripristino](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Considerazioni sulla migrazione

Se attualmente si usa Microsoft BitLocker Administration and Monitoring (MBAM), è possibile eseguire facilmente la migrazione della gestione a Configuration Manager. Quando si distribuiscono i criteri di gestione di BitLocker in Configuration Manager, i client caricano automaticamente i pacchetti e le chiavi di ripristino nel servizio di ripristino di Configuration Manager.

> [!IMPORTANT]
> Quando si esegue la migrazione da MBAM autonomo alla gestione di BitLocker di Configuration Manager, se è necessaria la funzionalità esistente di MBAM autonomo, non riutilizzare i componenti o i server MBAM autonomi con la gestione di BitLocker di Configuration Manager. Se si riutilizzano questi server, MBAM autonomo smetterà di funzionare quando la gestione di BitLocker di Configuration Manager installa i relativi componenti in tali server. Non eseguire lo script MBAMWebSiteInstaller.ps1 per configurare i portali di BitLocker nei server MBAM autonomi. Quando si configura la gestione di BitLocker di Configuration Manager, usare server distinti.

### <a name="group-policy"></a>Criteri di gruppo

- Le impostazioni di gestione di BitLocker sono completamente compatibili con le impostazioni di Criteri di gruppo di MBAM. Se i dispositivi ricevono sia le impostazioni di Criteri di gruppo che i criteri di Configuration Manager, configurarli in modo che corrispondano.

  > [!NOTE]
  > Se per MBAM autonomo esiste un'impostazione di Criteri di gruppo, l'impostazione equivalente tentata da Configuration Manager verrà sostituita. MBAM autonomo usa Criteri di gruppo del dominio, mentre Configuration Manager imposta criteri locali per la gestione di BitLocker. I criteri di dominio sostituiranno i criteri di gestione di BitLocker Configuration Manager locali. Se i Criteri di gruppo di dominio per MBAM autonomo non corrispondono ai criteri di Configuration Manager, la gestione di BitLocker in Configuration Manager avrà esito negativo. Ad esempio, se esistono Criteri di gruppo di dominio che impostano il server MBAM autonomo per i servizi di ripristino chiavi, la gestione di BitLocker in Configuration Manager non può configurare la stessa impostazione per il punto di gestione. A causa di questo comportamento, i client non segnalano le chiavi di ripristino al servizio di recupero chiavi per la gestione di BitLocker in Configuration Manager nel punto di gestione.

- Configuration Manager non implementa tutte le impostazioni di Criteri di gruppo di MBAM. Se si configurano impostazioni aggiuntive in Criteri di gruppo, l'agente di gestione di BitLocker nei client di Configuration Manager rispetta queste impostazioni.

  > [!IMPORTANT]
  > Non impostare Criteri di gruppo per un'impostazione già specificata dalla gestione di BitLocker in Configuration Manager. Impostare Criteri di gruppo solo per le impostazioni attualmente non esistenti nella gestione di BitLocker in Configuration Manager. Configuration Manager versione 2002 offre parità delle funzionalità con MBAM autonomo. Con Configuration Manager versione 2002 e successive, nella maggior parte dei casi non dovrebbe essere necessario impostare Criteri di gruppo di dominio per configurare i criteri di BitLocker. Per evitare conflitti e problemi, evitare l'uso di Criteri di gruppo per BitLocker. Configurare tutte le impostazioni tramite i criteri di gestione di BitLocker in Configuration Manager.

### <a name="tpm-password-hash"></a>Hash della password TPM

- I client MBAM precedenti non caricano l'hash della password TPM in Configuration Manager. Il client carica l'hash della password TPM solo una sola volta.

- Se è necessario eseguire la migrazione di queste informazioni al servizio di ripristino di Configuration Manager, eliminare il TPM nel dispositivo. Dopo il riavvio, il nuovo hash della password TPM verrà caricato nel servizio di ripristino.

### <a name="re-encryption"></a>Nuova crittografia

Configuration Manager non crittografa nuovamente le unità che sono già protette con Crittografia unità BitLocker. Se si distribuisce un criterio di gestione di BitLocker che non corrisponde alla protezione corrente dell'unità, verrà segnalato come non conforme. L'unità è comunque protetta.

Ad esempio, è stato usato MBAM per crittografare l'unità con l'algoritmo di crittografia AES-XTS 128, ma i criteri di Configuration Manager richiedono AES-XTS 256. L'unità non è conforme ai criteri, anche se l'unità è crittografata.

Per risolvere questo problema, disabilitare prima di tutto BitLocker nel dispositivo. Quindi, distribuire un nuovo criterio con le nuove impostazioni.

## <a name="co-management-and-intune"></a>Co-gestione e Intune

<!-- SCCMDocs#2321 -->

Il gestore del client Gestione configurazione per BitLocker è dotato di riconoscimento della co-gestione. Se il dispositivo è co-gestito e si passa il [carico di lavoro Endpoint Protection](../../../comanage/workloads.md#endpoint-protection) a Intune, il client Configuration Manager ignora i criteri di BitLocker. Il dispositivo ottiene i criteri di crittografia di Windows da Intune.

Quando si cambiano le autorità di gestione della crittografia e viene modificato anche l'algoritmo di crittografia prescelto, è necessario pianificare una [nuova esecuzione della crittografia](#re-encryption).

Per altre informazioni sulla gestione di BitLocker con Intune, vedere gli articoli seguenti:

- [Usare la crittografia dei dispositivi con Intune](../../../../intune/protect/encrypt-devices.md)
- [Risolvere i problemi relativi ai criteri di BitLocker in Microsoft Intune](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Passaggi successivi

[Configurare i report e i portali di BitLocker](setup-websites.md)
