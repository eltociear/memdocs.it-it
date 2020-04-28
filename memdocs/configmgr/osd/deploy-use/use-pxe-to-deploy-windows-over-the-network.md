---
title: Usare PXE per le distribuzioni del sistema operativo in rete
titleSuffix: Configuration Manager
description: Usare le distribuzioni del sistema operativo avviate da PXE per aggiornare il sistema operativo di un computer o per installare una nuova versione di Windows in un nuovo computer.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11045ff31dc3832ac97d62f491561b3cf989813c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079349"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usare PXE per distribuire Windows in rete con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le distribuzioni del sistema operativo avviate da Pre-Boot eXecution Environment (PXE) in Configuration Manager consentono ai client di richiedere e distribuire sistemi operativi in rete. In questo scenario di distribuzione, l'immagine del sistema operativo e le immagini d'avvio vengono inviate a un punto di distribuzione avviato da PXE.

> [!NOTE]  
> Quando si crea una distribuzione del sistema operativo destinata solo a computer BIOS x64, nel punto di distribuzione devono essere disponibili sia l'immagine di avvio x64 che l'immagine di avvio x86.

È possibile usare distribuzioni del sistema operativo avviate da PXE negli scenari seguenti:

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

Eseguire i passaggi di uno degli scenari di distribuzione del sistema operativo e quindi usare le sezioni di questo articolo per preparare le distribuzioni avviate da PXE.

> [!WARNING]
> Se si usano distribuzioni PXE e si configura l'hardware dei dispositivi con la scheda di rete come primo dispositivo di avvio, questi dispositivi possono avviare automaticamente una sequenza di attività di distribuzione del sistema operativo senza l'intervento dell'utente. Questa configurazione non viene gestita dalla procedura di verifica della distribuzione. Se da un lato questa configurazione può semplificare il processo e ridurre l'interazione dell'utente, dall'altro aumenta il rischio di ricreazione accidentale dell'immagine del dispositivo.

## <a name="configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Configurare almeno un punto di distribuzione per accettare le richieste PXE

Per distribuire i sistemi operativi ai client di Configuration Manager che eseguono richieste di avvio PXE, è necessario configurare uno o più punti di distribuzioni per accettare le richieste PXE. Dopo la configurazione, il punto di distribuzione risponde alle richieste di avvio PXE e stabilisce l'azione appropriata da eseguire per la distribuzione. Per altre informazioni, vedere [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe) (Installare o modificare un punto di distribuzione).  

> [!NOTE]  
> Se si configura un singolo punto di distribuzione che supporta PXE per più subnet, questo non può essere usato per l'applicazione delle opzioni DHCP. Configurare gli helper IP sui router per consentire l'inoltro delle richieste PXE ai punti di distribuzione che supportano PXE.
>
> Nella versione 1810 non è supportato l'uso del risponditore PXE senza WDS nei server che eseguono anche un server DHCP.
>
> A partire dalla versione 1902, quando si abilita un risponditore PXE in un punto di distribuzione senza i Servizi di distribuzione Windows, è ora possibile abilitarlo sullo stesso server del servizio DHCP.<!--3734270, SCCMDocs-pr #3416--> Aggiungere le impostazioni seguenti per supportare questa configurazione:  
>
> - Impostare il valore DWord **DoNotListenOnDhcpPort** su `1` nella chiave del Registro di sistema seguente: `HKLM\Software\Microsoft\SMS\DP`.
> - Impostare l'opzione DHCP 60 su `PXEClient`.  
> - Riavviare i servizi SCCMPXE e DHCP nel server.  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparare un'immagine d'avvio che supporta PXE

Per usare PXE per distribuire un sistema operativo, è necessario avere immagini d'avvio che supportano PXE sia x86 sia x64, distribuite in uno o più punti di distribuzione che supportano PXE. Usare le informazioni per abilitare PXE in un'immagine d'avvio e distribuirla nei punti di distribuzione:

- Per abilitare PXE in un'immagine d'avvio, selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE** nella scheda **Origine dati** nelle proprietà dell'immagine d'avvio.

- Se si modificano le proprietà per l'immagine d'avvio, aggiornarla e ridistribuirla nei punti di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Gestire gli identificatori di hardware duplicati

Configuration Manager potrebbe riconoscere più computer come un unico dispositivo se presentano attributi SMBIOS duplicati o si usa una scheda di rete condivisa. Attenuare questi problemi gestendo gli identificatori di hardware duplicati nelle impostazioni della gerarchia. Per altre informazioni, vedere [Gestire gli identificatori di hardware duplicati](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Creare un elenco di esclusione per le distribuzioni PXE

> [!Note]  
> In alcuni casi può risultare più semplice [gestire gli identificatori di hardware duplicati](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).<!-- SCCMDocs issue 802 -->
>
> I comportamenti di ognuno possono portare a risultati diversi in alcuni scenari. L'elenco di esclusione non determina in nessun caso l'avvio di un client con l'indirizzo MAC elencato.
>
> L'elenco di ID duplicati non usa l'indirizzo MAC per trovare i criteri della sequenza di attività per un client. Se corrisponde all'ID SMBIOS o se sono presenti criteri della sequenza di attività per computer sconosciuti, il client continua a essere avviato.

Quando si distribuiscono sistemi operativi con PXE, è possibile creare un elenco di esclusione in ogni punto di distribuzione. Aggiungere gli indirizzi MAC all'elenco di esclusione dei computer che si vuole vengano ignorati dal punto di distribuzione. I computer elencati non ricevono le sequenze di attività di distribuzione usate da Configuration Manager per la distribuzione PXE.

### <a name="process-to-create-the-exclusion-list"></a>Processo per creare l'elenco di esclusione

1. Creare un file di testo nel punto di distribuzione che supporta PXE. Ad esempio, assegnare al file di testo il nome **pxeExceptions.txt**.  

2. Usare un editor di testo semplice, ad esempio Blocco note, e aggiungere gli indirizzi MAC dei computer che il punto di distribuzione che supporta PXE deve ignorare. Separare i valori degli indirizzi MAC con i due punti e immettere ogni indirizzo in una riga separata. ad esempio `01:23:45:67:89:ab`  

3. Salvare il file di testo nel server del sistema del sito del punto distribuzione che supporta PXE. Il file di testo può essere salvato in qualsiasi posizione nel server.  

4. Modificare il Registro di sistema del punto di distribuzione che supporta PXE per creare una chiave del Registro di sistema **MACIgnoreListFile**. Aggiungere il valore della stringa del percorso completo per il file di testo nel server del sistema del sito del punto distribuzione che supporta PXE. Utilizzare il seguente percorso del Registro di sistema:  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > L'uso non corretto dell'editor del Registro di sistema può provocare gravi problemi che potrebbero richiedere la reinstallazione di Windows. La risoluzione dei problemi derivanti dall'uso errato dell'editor del Registro di sistema non è garantita. L'uso dell'editor del Registro di sistema è di sola responsabilità dell'utente.  

5. Dopo aver apportato questa modifica al Registro di sistema, riavviare il servizio WDS o il servizio risponditore PXE. Non è necessario riavviare il server.<!--512129-->  

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a> Dimensioni del blocco e della finestra TFTP RamDisk

È possibile personalizzare le dimensioni della finestra e del blocco TFTP RamDisk per i punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout, perché le dimensioni del blocco o della finestra sono eccessive. La personalizzazione delle dimensioni della finestra e del blocco TFTP RamDisk consentono di ottimizzare il traffico TFTP quando si usa PXE per soddisfare i requisiti di rete specifici. Per individuare la scelta più efficiente, è necessario testare le impostazioni personalizzate nel proprio ambiente. Per altre informazioni, vedere [Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione

Per usare la distribuzione del sistema operativo avviata da PXE, configurarla per rendere disponibile il sistema operativo per le richieste di avvio PXE. Configurare i sistemi operativi disponibili nella scheda **Impostazioni distribuzione** nelle proprietà di distribuzione. Per l'impostazione **Rendi disponibile per**, selezionare una delle opzioni seguenti:

- Client di Configuration Manager, supporti e PXE

- Solo supporti e PXE

- Solo supporti e PXE (nascosto)

## <a name="option-82-during-pxe-dhcp-handshake"></a>Opzione 82 durante l'handshake PXE DHCP
A partire dalla versione 1906, l'opzione 82 durante l'handshake DHCP PXE è supportata con il risponditore PXE senza WDS. Se è richiesta l'opzione 82, assicurarsi di usare il risponditore PXE senza WDS. L'opzione 82 non è supportata con WDS.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuire la sequenza di attività

Distribuire il sistema operativo in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](deploy-a-task-sequence.md). Quando si distribuiscono sistemi operativi tramite PXE, è possibile specificare se la distribuzione è obbligatoria o disponibile.

- **Distribuzione richiesta**: le distribuzioni richieste usano PXE senza alcun intervento da parte dell'utente. L'utente non può ignorare l'avvio PXE. Tuttavia, se l'utente annulla l'avvio di PXE prima della risposta del punto di distribuzione, il sistema operativo non viene distribuito.

- **Distribuzione disponibile**: le distribuzioni disponibili richiedono la presenza dell'utente nel computer di destinazione. L'utente deve premere **F12** per continuare il processo di avvio PXE. Se l'utente non è presente per premere **F12**, il computer esegue l'avvio nel sistema operativo corrente oppure dal successivo dispositivo di avvio disponibile.

È possibile ridistribuire una distribuzione PXE richiesta cancellando lo stato dell'ultima distribuzione PXE assegnato a una raccolta di Configuration Manager o a un computer. Per altre informazioni sull'azione **Cancella distribuzioni PXE richieste**, vedere [Gestire i client](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) o [Come gestire le raccolte di dispositivi](../../core/clients/manage/collections/manage-collections.md#bkmk_device). Questa azione consente di reimpostare lo stato di quella distribuzione e reinstalla le distribuzioni richieste più recenti.

> [!IMPORTANT]  
> Il protocollo PXE non è sicuro. Assicurarsi che il server PXE e il client PXE si trovino in una rete fisicamente sicura, come ad esempio in un data center, per evitare l'accesso non autorizzato al sito.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>Come viene selezionata l'immagine d'avvio per PXE

Quando un client viene avviato con PXE Configuration Manager rende disponibile per il client un'immagine di avvio. Configuration Manager usa un'immagine di avvio con un'architettura esattamente corrispondente. Se non è disponibile un'immagine di avvio con l'architettura esatta, Configuration Manager usa un'immagine di avvio con un'architettura compatibile.

L'elenco seguente contiene informazioni dettagliate sulle modalità di selezione di un'immagine d'avvio per i client avviati con PXE:  

1. Configuration Manager cerca nel database del sito il record di sistema corrispondente all'indirizzo MAC o al valore SMBIOS del client che sta tentando di eseguire l'avvio.  

    > [!NOTE]  
    > Se un computer assegnato a un sito viene avviato in PXE per un sito diverso, i criteri non sono visibili per il computer. Ad esempio, se un client è già assegnato al sito A, il punto di gestione e il punto di distribuzione per il sito B non sono in grado di accedere ai criteri dal sito A. Il client non riuscirà a completare l'avvio di PXE.  

2. Configuration Manager cerca le sequenze di attività che vengono distribuite nel record di sistema menzionato nel passaggio 1.  

3. Nell'elenco di sequenze di attività trovato nel passaggio 2, Configuration Manager cerca un'immagine d'avvio corrispondente all'architettura del client che sta tentando di eseguire l'avvio. Se viene trovata un'immagine di avvio con la stessa architettura, verrà usata quell'immagine.  

    Se viene rilevata più di un'immagine d'avvio, viene usato l'ID distribuzione della sequenza di attività *massimo* o il più recente. Nel caso di una gerarchia a più siti, il sito con la lettera *più alta* avrà la precedenza nel confronto tra stringhe. Se ad esempio entrambi hanno un'altra corrispondenza, viene scelta una distribuzione dal sito ZZZ di un anno prima rispetto a una distribuzione dal sito AAA del giorno prima.<!-- SCCMDocs issue 877 -->  

4. Se non viene trovata un'immagine d'avvio con la stessa architettura, Configuration Manager cerca un'immagine d'avvio compatibile con l'architettura del client. Esegue la ricerca nell'elenco di sequenze di attività indicato nel passaggio 2. Ad esempio, un client BIOS/MBR a 64 bit è compatibile con immagini di avvio a 32 bit e 64 bit. Un client BIOS/MBR a 32 bit è compatibile solo con le immagini di avvio a 32 bit. I client UEFI sono compatibili solo con l'architettura corrispondente. Un client UEFI a 64 bit è compatibile solo con le immagini d'avvio a 64 bit e un client UEFI a 32 bit è compatibile solo con le immagini d'avvio a 32 bit.
