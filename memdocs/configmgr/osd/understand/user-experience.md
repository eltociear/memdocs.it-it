---
title: Esperienze utente per la distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni su esperienze utente come lo stato della sequenza di attività e la creazione guidata del supporto per la distribuzione del sistema operativo in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703219"
---
# <a name="user-experiences-for-os-deployment"></a>Esperienze utente per la distribuzione del sistema operativo

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver [distribuito una sequenza di attività](../deploy-use/deploy-a-task-sequence.md), gli utenti possono interagire con la distribuzione in diversi modi, a seconda dello scenario. Questo articolo descrive le esperienze utente principali con le distribuzioni del sistema operativo e illustra come è possibile configurarle:

- Notifica utente di Software Center per una distribuzione a impatto elevato
- Esperienza di avvio PXE di esempio
- Creazione guidata sequenza di attività da un supporto
- Finestra di stato durante l'esecuzione della sequenza di attività
- Finestra di errore quando la sequenza di attività non riesce

## <a name="software-center"></a>Software Center

Per una distribuzione a impatto elevato, è possibile personalizzare il messaggio visualizzato da Software Center. Quando l'utente apre la distribuzione del sistema operativo in Software Center, viene visualizzato un messaggio simile a quello nella finestra seguente:

![Notifica di sequenza di attività personalizzata per l'utente finale da Software Center](../media/user-notification-enduser.png)

Per altre informazioni su come personalizzare il messaggio in questa finestra, vedere [Creare una notifica personalizzata per le distribuzioni ad alto rischio](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

Si può anche personalizzare il nome dell'organizzazione nella parte superiore della finestra. L'esempio riportato sopra mostra il valore predefinito, `IT Organization`. Cambiare l'impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#computer-agent) (Informazioni sulle impostazioni client).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Per altre informazioni, vedere [Usare Software Center per distribuire Windows in rete](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Le esperienze per PXE variano a seconda dei modelli hardware. Per l'avvio in rete, i dispositivi basati su UEFI usano in genere il tasto `Enter`, mentre i dispositivi basati su BIOS usano il tasto `F12`.

L'esempio seguente illustra l'esperienza PXE di Hyper-V Gen1 (BIOS):

![Esempio di schermata PXE del BIOS da una macchina virtuale Hyper-V](media/hyperv-pxe.png)

Dopo essere stato avviato correttamente tramite PXE, il dispositivo si comporta in modo analogo a un supporto di avvio. Per altre informazioni, vedere la sezione successiva [Creazione guidata sequenza di attività](#task-sequence-wizard).

Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

> [!WARNING]
> Se si usano distribuzioni PXE e si configura l'hardware dei dispositivi con la scheda di rete come primo dispositivo di avvio, questi dispositivi possono avviare automaticamente una sequenza di attività di distribuzione del sistema operativo senza l'intervento dell'utente. Questa configurazione non viene gestita dalla procedura di verifica della distribuzione. Se da un lato questa configurazione può semplificare il processo e ridurre l'interazione dell'utente, dall'altro aumenta il rischio di ricreazione accidentale dell'immagine del dispositivo.

## <a name="task-sequence-wizard"></a>Creazione guidata sequenza di attività

Quando si usa un [supporto per sequenza di attività](../deploy-use/create-task-sequence-media.md), viene eseguita la creazione guidata sequenza di attività per guidare il processo.

### <a name="welcome-to-the-task-sequence-wizard"></a>Finestra Creazione guidata sequenza di attività

![Screenshot della pagina principale della Creazione guidata sequenza di attività](media/welcome-task-sequence-wizard.png)

- Se il supporto è protetto da una password, l'utente deve immetterla in questa pagina di benvenuto.

- Selezionare **Configura impostazioni di rete** per specificare un indirizzo IP statico o altre impostazioni di rete personalizzate. In caso contrario, il dispositivo usa DHCP per impostazione predefinita.

- Se la rete richiede un proxy, selezionare **Configura impostazioni proxy**.

### <a name="select-a-task-sequence-to-run"></a>Selezionare una sequenza di attività da eseguire

Se si distribuiscono più sequenze di attività nel dispositivo, viene visualizzata questa pagina in cui selezionare una sequenza di attività. Assicurarsi di usare per la sequenza di attività un nome e una descrizione che gli utenti possano comprendere facilmente.

![Screenshot della pagina di selezione della sequenza di attività della Creazione guidata sequenza di attività](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Modificare le variabili della sequenza di attività

Se una o più variabili della sequenza di attività hanno valori vuoti, nella creazione guidata viene visualizzata una pagina in cui modificare i valori delle variabili.

![Screenshot della pagina Modifica variabili della sequenza di attività della Creazione guidata sequenza di attività](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Comandi di preavvio

È possibile personalizzare il supporto per sequenza di attività o le immagini di avvio per eseguire un comando di preavvio. Un comando di preavvio viene eseguito prima dell'avvio della sequenza di attività. Alcune delle azioni più comuni sono:

- Richiedere all'utente l'immissione di valori dinamici, ad esempio il nome computer
- Specificare la configurazione di rete
- Impostare l'affinità utente-dispositivo

Il comando di preavvio è una riga di comando specificata con uno script o un programma. L'esperienza utente è univoca per tale script o programma.

Per altre informazioni, vedere gli articoli seguenti:

- [Comandi di preavvio per supporti per sequenza di attività](prestart-commands-for-task-sequence-media.md)
- [Gestire le immagini di avvio](../get-started/manage-boot-images.md#customization)
- [Supporto per sequenza di attività](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Sequenza attività - Progresso

Quando viene eseguita la sequenza di attività, viene visualizzata la finestra **Stato dell'installazione**:

![Esempio della finestra Stato dell'installazione della sequenza di attività](media/task-sequence-progress.png)

- Questa finestra è sempre in primo piano. È possibile spostarla, ma non chiuderla o ridurla a icona.

- Si può personalizzare il nome dell'organizzazione nella parte superiore della finestra. L'esempio riportato sopra mostra il valore predefinito, `IT Organization`. Cambiare l'impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md#computer-agent) (Informazioni sulle impostazioni client).

    > [!TIP]
    > La sequenza di attività archivia questo valore nella variabile di sola lettura [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName).

- È possibile personalizzare il sottotitolo. L'esempio riportato sopra mostra il valore predefinito, `Running: <task sequence name>`. Nelle proprietà della sequenza di attività selezionare l'opzione **Usa il testo personalizzato** per il testo della notifica di stato. Il testo non deve superare i 255 caratteri.

- **Azione in esecuzione**: la prima riga mostra il nome del passaggio della sequenza di attività corrente. L'indicatore di stato sotto mostra il completamento complessivo della sequenza di attività.

- La seconda riga viene visualizzata solo per alcuni passaggi che forniscono uno stato di avanzamento più dettagliato.

- Usare la variabile della sequenza di attività [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) per controllare la visualizzazione dello stato di avanzamento della sequenza di attività.

    Per disabilitare completamente la finestra di stato, disabilitare l'opzione **Mostra stato sequenza di attività** nella pagina **Esperienza utente** della distribuzione della sequenza di attività.

A partire dalla versione 2002, la finestra di stato della sequenza di attività include i miglioramenti seguenti:<!--5932692-->

- Possibilità di visualizzare il numero del passaggio corrente, il numero totale di passaggi e la percentuale di completamento

- Ingrandimento della finestra per offrire più spazio per mostrare meglio il nome dell'organizzazione su un'unica riga

![Esempio di finestra di stato della sequenza di attività](media/2356386-task-sequence-progress.png)

Per impostazione predefinita, la finestra di stato della sequenza di attività usa il testo esistente. Se non vengono apportate modifiche, il funzionamento continua a essere lo stesso della versione 1910 e delle versioni precedenti. Per visualizzare le nuove informazioni sullo stato di avanzamento, specificare la variabile della sequenza di attività [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel).

Il numero e la percentuale di completamento sono progettati per offrire solo un'indicazione generale. Questi valori sono basati sul numero totale di passaggi nella sequenza di attività. Per una sequenza di attività più complessa con passaggi eseguiti in modo condizionale in base alla logica della sequenza di attività, lo stato di avanzamento potrebbe essere non lineare.

Il conteggio dei passaggi totali non include gli elementi seguenti nella sequenza di attività:

- Gruppi. Questo elemento è un contenitore per altri passaggi, non è un passaggio.

- Istanze del passaggio **Eseguire la sequenza di attività**. Questo passaggio è un contenitore per altri passaggi.

- Passaggi che vengono disabilitati in modo esplicito. Un passaggio disabilitato non viene eseguito durante la sequenza di attività.

    > [!NOTE]
    > I passaggi abilitati in un gruppo disabilitato sono ancora inclusi nel conteggio totale.

## <a name="task-sequence-error"></a>Errore di sequenza di attività

Se la sequenza di attività non riesce, viene visualizzata la finestra **Errore di sequenza di attività**.

![Esempio di finestra Errore di sequenza di attività](media/task-sequence-error.png)

- Le informazioni dell'intestazione possono essere personalizzate allo stesso modo della finestra di stato della sequenza di attività.

- Vengono visualizzati il nome della sequenza di attività, un codice di errore e un messaggio generale per gli utenti, ad esempio `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- La finestra si chiude automaticamente dopo un periodo di timeout. Per impostazione predefinita, questo timeout è di 15 minuti. È possibile personalizzare questo valore con la variabile della sequenza di attività [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout).
