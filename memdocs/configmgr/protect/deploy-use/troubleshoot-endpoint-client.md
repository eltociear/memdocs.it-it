---
title: Risolvere i problemi di Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi con Windows Defender ed Endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709419"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Risolvere i problemi di Windows Defender o del client Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*

In caso di difficoltà con Windows Defender o Endpoint Protection, usare questo articolo per risolvere i problemi seguenti:  

- [Aggiornamento di Windows Defender o Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [Avvio del servizio di Windows Defender o Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
- [Problemi di connessione a Internet](#internet-connection-issues)  
- [Minaccia rilevata che non è possibile correggere](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>Aggiornamento di Windows Defender o Endpoint Protection

### <a name="symptoms"></a>Sintomi

Windows Defender o Endpoint Protection interagisce automaticamente con Microsoft Update assicurando in tal modo che le definizioni di virus e spyware siano sempre aggiornate.  

Questa sezione illustra i problemi più comuni relativi agli aggiornamenti automatici, incluse le situazioni seguenti:  

- Vengono visualizzati messaggi di errore per indicare che gli aggiornamenti non sono riusciti.  

- Durante la verifica della disponibilità degli aggiornamenti viene visualizzato un messaggio di errore in cui si informa che non è possibile verificare, scaricare o installare gli aggiornamenti delle definizioni di virus e spyware.  

- Gli aggiornamenti non riescono anche se il dispositivo è connesso a Internet.  

- Gli aggiornamenti non vengono installati automaticamente come pianificato.  

### <a name="causes"></a>Cause

Le cause più comuni dei problemi di aggiornamento sono correlate a problemi di connettività Internet. Se si è certi che il dispositivo sia connesso a Internet perché è possibile esplorare altri siti Web, il problema potrebbe dipendere da conflitti nelle impostazioni Internet in Windows.  

### <a name="options-to-resolve"></a>Opzioni per la risoluzione

#### <a name="step-1-reset-your-internet-settings"></a>Passaggio 1: Reimpostare le impostazioni Internet  

1. Chiudere tutti i programmi aperti, incluso il browser Web.  

    > [!NOTE]  
    > Quando si reimpostano le impostazioni Internet, è possibile che i file temporanei, i cookie, la cronologia esplorazioni e le password online del browser vengano eliminati. Non vengono eliminati i preferiti.  

2. Passare al menu **Start** e aprire `inetcpl.cpl`.  

3. Passare alla scheda **Avanzate**.  

4. Nella sezione per **reimpostare le impostazioni di Internet Explorer** selezionare **Reimposta**, quindi selezionare di nuovo **Reimposta** per confermare.  

5. Selezionare **OK** quando le impostazioni vengono reimpostate.

6. Provare ad aggiornare di nuovo Windows Defender.

Se il problema persiste, procedere con il passaggio successivo.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Passaggio 2: Verificare che data e ora siano impostate correttamente nel computer  

Se il messaggio di errore contiene il codice 0x80072f8f, è molto probabile che il problema dipenda dall'impostazione errata della data o dell'ora nel computer. Passare al menu **Start**, selezionare **Impostazioni**, selezionare **Ora e lingua** e selezionare **Data e ora**.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Passaggio 3: Rinominare la cartella Distribuzione software nel computer  

1. Arrestare il servizio **Windows Update**.  

    1. Passare a **Start** e aprire **services.msc**.  

    2. Selezionare il servizio **Windows Update**. Passare al menu **Azione** e selezionare **Arresta**.

2. Rinominare la directory **SoftwareDistribution**.  

    1. Aprire un prompt dei comandi come amministratore.  

    2. Immettere il comando seguente:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Riavviare il servizio **Windows Update**.

    1. Tornare alla finestra **Servizi**.  

    2. Selezionare il servizio **Windows Update**. Passare al menu **Azione** e selezionare **Avvia**.

    3. Chiudere la finestra Servizi.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Passaggio 4: Reimpostare il motore di aggiornamento dell'antivirus Microsoft nel computer  

1. Aprire un prompt dei comandi come amministratore.

2. Immettere il comando seguente:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Riavviare il computer.  

4. Provare ad aggiornare di nuovo Windows Defender.

Se il problema persiste, procedere con il passaggio successivo.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Passaggio 5: Installare manualmente gli aggiornamenti delle definizioni  

[Scaricare manualmente gli aggiornamenti più recenti](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>Passaggio 6: Contattare il supporto tecnico Microsoft  

Se la procedura non ha risolto il problema, contattare il supporto tecnico Microsoft. Per altre informazioni, vedere [Opzioni di supporto e risorse per la community](../../core/understand/find-help.md#BKMK_SupportOptions).  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>Avvio del servizio di Windows Defender o Endpoint Protection

### <a name="symptom"></a>Sintomo

Viene visualizzato il messaggio seguente: **Il computer non è monitorato da Windows Defender or Endpoint Protection perché il servizio del programma è stato arrestato. È necessario riavviarlo.**

### <a name="solution"></a>Soluzione

#### <a name="step-1-restart-your-computer"></a>Passaggio 1: Riavviare il computer

Chiudere tutte le applicazioni e riavviare il computer.  

#### <a name="step-2-check-the-windows-service"></a>Passaggio 2: Controllare il servizio di Windows

1. Passare a **Start** e aprire **services.msc**.  

2. Selezionare **Servizio Windows Defender Antivirus**.  

3. Verificare che**Tipo di avvio** sia impostato su **Automatico**.

4. Passare al menu **Azione** e selezionare **Avvia**.

    1. Se questa azione non è disponibile, selezionare **Arresta**. Attendere l'arresto del servizio, quindi selezionare l'azione **Avvia** per riavviare il servizio.  

Prendere nota di eventuali errori che possono verificarsi durante questo processo. [Contattare il supporto tecnico Microsoft](../../core/understand/find-help.md#BKMK_SupportOptions) e specificare le informazioni sull'errore.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Passaggio 3: Rimuovere eventuali programmi per la sicurezza di terze parti  

> [!NOTE]  
> Alcune applicazioni per la sicurezza non vengono disinstallate completamente. È possibile che sia necessario scaricare ed eseguire un'utilità di pulitura per rimuovere completamente l'applicazione di sicurezza precedente.  

1. Passare al menu **Start** e aprire **appwiz.cpl**.  

2. Nell'elenco dei programmi installati disinstallare tutti i programmi per la sicurezza di terze parti.

3. Riavviare il computer.  

> [!CAUTION]  
> Quando si rimuovono i programmi per la sicurezza, il computer potrebbe non essere protetto. Se si verificano problemi durante l'installazione di Windows Defender dopo aver rimosso i programmi per la sicurezza esistenti, contattare il [supporto tecnico Microsoft](https://support.microsoft.com/supportforbusiness/productselection). Selezionare la famiglia di prodotti **Sicurezza**, quindi scegliere il prodotto **Windows Defender**.

## <a name="internet-connection-issues"></a>Problemi di connessione a Internet

Affinché il computer riceva gli aggiornamenti più recenti da Windows Update, è necessario che sia connesso a Internet.  

1. Passare a **Start** e aprire **ncpa.cpl**.  

2. Aprire il nome della connessione per visualizzare lo **Stato** della connessione.  

3. Se il computer è connesso, lo stato di **Connettività IPv4** e/o **Connettività IPv6** è **Internet**.  

4. Se il computer non sembra essere connesso, selezionare il nome della connessione e scegliere **Esegui diagnosi della connessione**.

Chiudere eventuali programmi aperti e riavviare il computer.  

## <a name="detected-threat-cant-be-remediated"></a>Minaccia rilevata che non è possibile correggere

Quando Windows Defender o Endpoint Protection rileva una potenziale minaccia, tenta di attenuare la minaccia mettendola in quarantena o rimuovendola. Queste minacce possono essere nascoste all'interno di un archivio compresso (`.zip`) o di una condivisione di rete.

### <a name="remove-or-scan-the-file"></a>Rimuovere o analizzare il file  

- Se la minaccia rilevata era all'interno di un file di archivio compresso, individuare il file. Eliminare il file o analizzarlo manualmente. Fare clic con il pulsante destro del mouse sul file e selezionare **Analizza con Windows Defender**. Se Windows Defender rileva altre minacce nel file, viene inviata una notifica all'utente. A questo punto è possibile scegliere un'azione appropriata.  

- Se la minaccia rilevata era all'interno di una condivisione di rete, aprire la condivisione e analizzarla manualmente. Fare clic con il pulsante destro del mouse sul file e selezionare **Analizza con Windows Defender**. Se Windows Defender rileva altre minacce nella condivisione di rete, viene inviata una notifica all'utente. A questo punto è possibile scegliere un'azione appropriata.  

- Se non si è certi dell'origine del file, eseguire una scansione completa del computer. L'analisi completa potrebbe richiedere molto tempo.  

## <a name="see-also"></a>Vedere anche

[Endpoint Protection client frequently asked questions](endpoint-protection-client-faq.md) (Domande frequenti relative al client Endpoint Protection)

[Guida del client di Endpoint Protection](endpoint-protection-client-help.md)
