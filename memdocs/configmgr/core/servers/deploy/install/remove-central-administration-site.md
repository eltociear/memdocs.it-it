---
title: Rimuovere il sito di amministrazione centrale
titleSuffix: Configuration Manager
description: Rimuovere il sito di amministrazione centrale (CAS) per semplificare l'infrastruttura di Configuration Manager riducendola a un singolo sito primario autonomo.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6704075d707306f55a50a937185c9bdd28b18cc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700619"
---
# <a name="remove-the-central-administration-site"></a>Rimuovere il sito di amministrazione centrale

*Si applica a: Configuration Manager (Current Branch)*

<!-- 3607277 -->

A partire dalla versione 2002, se la gerarchia è costituita dal sito di amministrazione centrale (CAS) e da un singolo sito primario figlio, è possibile rimuovere il sito di amministrazione centrale. Questa azione semplifica l'infrastruttura di Configuration Manager riducendola a un singolo sito primario autonomo. Elimina le complessità della replica da sito a sito e concentra le attività di gestione sul singolo sito.

> [!IMPORTANT]
> In questa versione di Configuration Manager questa funzionalità è in versione non definitiva e non è abilitata per impostazione predefinita. È attualmente disponibile per i clienti Microsoft Premier.
>
> Per abilitare questa funzionalità, contattare il technical account manager per assistenza:
>
> - Il technical account manager apre un caso di consulenza, che userà le ore di Microsoft Premier.
> - Non è possibile modificare il livello di gravità del caso.
> - Il servizio di supporto tecnico Microsoft assisterà questi casi di consulenza durante i normali orari di ufficio dei giorni feriali.

## <a name="plan"></a>Pianificazione

- La gerarchia deve essere costituita dal sito di amministrazione centrale (CAS) e da un singolo sito primario figlio. Il sito primario può avere siti secondari. Per rimuovere altri siti primari figlio dalla gerarchia, esaminare i passaggi di pianificazione e i prerequisiti in [Pianificare la disinstallazione di un sito primario](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Verificare che il sito primario figlio soddisfi i requisiti di dimensioni e scalabilità per un [sito primario autonomo](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Spostare o ritirare tutti i ruoli del sito presenti nel sito di amministrazione centrale, eccetto il punto di connessione del servizio e il punto di aggiornamento software. Questi due ruoli vengono gestiti dal programma di installazione di Configuration Manager quando si rimuove il sito di amministrazione centrale.

  I ruoli seguenti sono quelli più comuni nel sito di amministrazione centrale che devono essere ritirati o spostati nel sito primario:

  - Punto di sincronizzazione di Asset Intelligence
  - Punto di Endpoint Protection
  - Punto di Reporting Services
  - Punto di servizio del data warehouse
  - Cloud Management Gateway

    > [!NOTE]
    > Se è stato abilitato Cloud Management Gateway per il contenuto, pianificare la ridistribuzione del contenuto dopo aver ricreato Cloud Management Gateway nel sito primario.<!-- 6608659 -->

- Disattivare le viste distribuite.

- Configuration Manager gestisce automaticamente i percorsi di origine del pacchetto per i pacchetti predefiniti, come il client Gestione configurazione. Esaminare tutti gli altri percorsi di origine dei contenuti per assicurarsi che non usino una condivisione nel sito di amministrazione centrale.

- Arrestare gli eventuali processi di migrazione attivi e rimuovere tutte le configurazioni per la migrazione. Per altre informazioni, vedere [Arrestare la migrazione attiva da un'altra gerarchia](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Se si usano le regole di distribuzione automatica per gli aggiornamenti software, ricrearle nel sito primario figlio.

- Se si usa Configuration Manager o System Center Updates Publisher per gestire gli [aggiornamenti software di terze parti](../../../../sum/deploy-use/third-party-software-updates.md), esportare il certificato di firma WSUS dal punto di aggiornamento software nel sito di amministrazione centrale.

  - Prima di rimuovere il sito di amministrazione centrale, attendere la scadenza di tutte le distribuzioni di aggiornamenti software di terze parti necessarie. I client scaricano anticipatamente il contenuto per le distribuzioni necessarie e quando si cambia il punto di aggiornamento software, l'hash del contenuto cambia con la *pubblicazione locale* degli aggiornamenti software. Questo comportamento non ha alcun impatto sugli altri tipi di contenuto, ma solo sulla pubblicazione locale di aggiornamenti software di terze parti. Se si rimuove il sito di amministrazione centrale con queste distribuzioni necessarie ancora in corso, genereranno un errore di mancata corrispondenza dell'hash sui client.

- Verificare i prodotti software di terze parti che potrebbero avere una dipendenza dal sito di amministrazione centrale.

## <a name="prerequisites"></a>Prerequisiti

- L'utente amministratore che esegue il programma di installazione di Configuration Manager deve avere i privilegi di protezione seguenti:

  - Diritti di **amministratore** locale sul server CAS

  - Se il server di database CAS è remoto rispetto al server del sito primario, diritti di **amministratore** locale sul server di database del sito remoto per il sito di amministrazione centrale (CAS).

  - Diritti di **amministratore di sistema** sul database del sito CAS

  - Diritti di **amministratore** locale sul server del sito primario

  - Se il server di database del sito primario è remoto rispetto al server del sito primario, diritti di **amministratore** locale sul server di database del sito remoto per il sito primario.

  - Diritti di **amministratore di sistema** sul database del sito primario

  - Ruolo di sicurezza **Amministratore infrastruttura** o **Amministratore completo** nel sito di amministrazione centrale e nel sito primario

- Un solo sito primario figlio nella gerarchia. Per altre informazioni, vedere [Disinstallare un sito primario](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Processo

1. Avviare il programma di installazione di Configuration Manager nel server del sito di amministrazione centrale usando uno dei metodi seguenti:

    - Nel menu**Start** selezionare **Installazione di Configuration Manager**.

    - Nella directory dei *supporti di installazione* di Configuration Manager aprire `\SMSSETUP\BIN\X64\setup.exe`. Verificare che la versione corrisponda a quella del sito.

    - Nella directory in cui è *installato* Configuration Manager aprire `\BIN\X64\setup.exe`.

1. Leggere le informazioni nella pagina **Prima di iniziare**.

1. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**.

1. Nella pagina **Manutenzione sito** selezionare **Rimuovi il sito di amministrazione centrale**. <!-- or is it still "delete"? -->

1. Nella pagina **Riconfigurazione dei ruoli di sistema esistenti del sito**:

    - **Punto di connessione del servizio**: immettere il nome di dominio completo del sistema del sito nel sito primario che deve ospitare questo ruolo obbligatorio. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../configure/about-the-service-connection-point.md).

    - **Punto di aggiornamento software**: selezionare un punto di aggiornamento software esistente nel sito primario. Il programma di installazione configura questo punto di aggiornamento software in modo che la sincronizzazione corrisponda alla configurazione del sito di amministrazione centrale.

    Il programma di installazione verifica che i server specificati soddisfino i prerequisiti. Selezionare **Inizia installazione** quando si è pronti per continuare.

Se si verifica un problema durante l'installazione, usare la procedura guidata per ripetere il processo.

Al termine dell'installazione, il sito primario viene reimpostato. Per altre informazioni, vedere [Eseguire una reimpostazione del sito](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>Monitoraggio e verifica

Esaminare i log seguenti durante il processo di installazione:

- `C:\ConfigMgrSetup.log` nel server CAS

- **hman.log** nella directory dei log di Configuration Manager nel server del sito primario

Usare il nodo **Gerarchia siti** nell'area di lavoro **Monitoraggio** per visualizzare le modifiche apportate alla gerarchia. Ad esempio, la grafica seguente mostra il confronto tra il prima e il dopo del sito di amministrazione centrale **SHY**, del sito primario **HAW** e del sito secondario **VWT**:

| Prima  | Dopo   |
|---------|---------|
|![Esempio di visualizzazione della gerarchia siti di un sito di amministrazione centrale, un sito primario e un sito secondario](media/3607277-cas-primary-secondary.png)|![Esempio di visualizzazione della gerarchia siti di un sito primario e un sito secondario](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Attività successive all'installazione

Dopo aver rimosso il sito di amministrazione centrale, esaminare i passaggi seguenti in base all'ambiente in uso.

- Rimuovere manualmente l'account computer del server CAS dai gruppi locali del sito primario.

- La chiave radice attendibile è stata modificata e potrebbe quindi richiedere azioni aggiuntive:

  - Aggiornare le immagini d'avvio della distribuzione del sistema operativo in modo da includere i file binari di Configuration Manager più recenti.

  - Ricreare i [supporti di distribuzione del sistema operativo](../../../../osd/deploy-use/create-task-sequence-media.md).

- Se si esegue la connessione di Configuration Manager con [Monitoraggio di Azure](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context), è necessario reimpostare la connessione. La prima cosa da fare per risolvere eventuali problemi è [rinnovare la chiave privata](../configure/azure-services-wizard.md#bkmk_renew). Se il problema persiste, ricreare la connessione.<!-- 5584635 -->

- Nella versione 2002, se si abilita la sincronizzazione dei driver di Surface, riconfigurare questa funzionalità dopo aver rimosso il sito di amministrazione centrale. Per altre informazioni, vedere [Includere i driver di Microsoft Surface e gli aggiornamenti del firmware](../../../../sum/get-started/configure-classifications-and-products.md#bkmk_Surface).<!-- 5728727 -->

- Se si gestiscono gli aggiornamenti software di terze parti:

  1. Esportare il certificato di firma WSUS dal punto di aggiornamento software nel sito di amministrazione centrale, se non è già stato fatto.

  1. Prima di creare nuove distribuzioni, rimuovere l'aggiornamento dalle distribuzioni e dai pacchetti di aggiornamento software esistenti.

  1. Per ripristinare i metadati degli aggiornamenti software in uno stato utilizzabile, risincronizzare i cataloghi sottoscritti. È anche possibile attendere che Configuration Manager venga risincronizzato automaticamente.

  1. Avviare o attendere l'esecuzione di un normale processo di sincronizzazione degli aggiornamenti software per aggiornare Configuration Manager con lo stato corrente da WSUS. Se si vuole, usare i cmdlet SCUP o WSUS di PowerShell per eliminare e aggiungere di nuovo gli aggiornamenti.

  1. Ripubblicare il contenuto degli aggiornamenti da distribuire.
