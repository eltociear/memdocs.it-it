---
title: Risolvere i problemi di Package Conversion Manager
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi relativi a Package Conversion Manager in Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877632"
---
# <a name="troubleshoot-package-conversion-manager"></a>Risolvere i problemi di Package Conversion Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357861-->

Usare le informazioni in questo articolo per risolvere i problemi relativi all'uso di Package Conversion Manager.



## <a name="sms-provider"></a>Provider SMS

Package Conversion Manager usa il provider SMS. Per altre informazioni, vedere [Piano per il provider SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).

Se il provider SMS non funziona correttamente, la console di Configuration Manager, incluso Package Conversion Manager, non funziona.



## <a name="package-readiness"></a>Conformità del pacchetto

Prima di convertire un pacchetto in un'applicazione, analizzare il pacchetto usando la funzione **Analizza** di Package Conversion Manager. Dopo l'analisi, aggiungere la colonna **Conformità** nel nodo **Pacchetti** della console di Configuration Manager. L'elenco di pacchetti indica uno degli stati di conformità seguenti per il pacchetto analizzato:

- **Automatico**: il pacchetto può essere convertito direttamente usando la funzione **Converti**.      

  > [!NOTE]  
  > Una conversione automatica non converte le query WQL in requisiti dell'applicazione. Per convertire queste query, usare il processo **Correggi e converti**.  

- **Manuale**: il pacchetto richiede aggiunte o modifiche prima di poter essere convertito usando la funzione **Correggi e converti**.  

- **Non applicabile**: il pacchetto non è adatto per la conversione. È possibile risolvere eventuali errori del pacchetto oppure continuare a distribuirlo come pacchetto.  

- **Errore**: il pacchetto contiene errori. Correggere manualmente questi errori prima di procedere con l'analisi e la conversione.  

Nel riquadro dei dettagli del nodo **Pacchetti** nella console di Configuration Manager sono indicati eventuali problemi di conformità. Selezionare un pacchetto e quindi selezionare la scheda **Riepilogo** nel riquadro dei dettagli.



## <a name="log-files"></a>File di registro

### <a name="enable-logging"></a>Abilitare la registrazione

Quando si abilita la registrazione per Package Conversion Manager, vengono registrati tutti gli errori, le operazioni e le eccezioni.

Per abilitare la registrazione per questo componente in Configuration Manager, modificare **Microsoft.ConfigurationManagement.exe.Config**. Per impostazione predefinita, questo file di configurazione si trova nel percorso seguente:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> A partire dalla versione 1910, questo percorso è stato modificato in modo da usare la cartella `Microsoft Endpoint Manager`. Assicurarsi di non usare una versione precedente del file che potrebbe esistere in un'altra cartella.

Inserire gli elementi XML **switches** e **trace** seguenti nell'elemento **system.diagnostics** dopo l'ultimo elemento **sources**:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Questo esempio usa il file **PCMTrace.log**. Questo log si trova nel computer che esegue la console di Configuration Manager nel percorso seguente:  
`%UserProfile%\AppData\Local\Temp`

Per configurare il livello di dettaglio, modificare l'impostazione dell'opzione di traccia **PcmLogging**. Impostare questo valore su uno dei quattro livelli di dettaglio, dal meno dettagliato (`1`) al più dettagliato (`4`).


### <a name="smsprovlog"></a>SMSProv.log

In alcuni casi, le informazioni relative alla risoluzione dei problemi del processo di conversione dei pacchetti si trovano nel file **SMSProv.log**. Questo file acquisisce le informazioni dal provider SMS di Configuration Manager.

Per impostazione predefinita, questo file di log si trova nel server del sito di Configuration Manager nel percorso seguente:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Se viene visualizzato uno dei messaggi di errore seguenti, il file **SMSProv.log** potrebbe contenere informazioni utili per la risoluzione dei problemi:

- `The SMS Provider reported an error`

- `Generic Failure`

Questi messaggi di errore indicano in genere che si è verificato un errore nel server del sito e che le informazioni sull'errore non sono state inviate alla console di Configuration Manager.

Per altre informazioni, vedere [Informazioni tecniche sui messaggi di errore di Package Conversion Manager](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Modifica degli attributi del pacchetto in seguito all'analisi

Dopo aver analizzato un pacchetto il cui stato di conformità è **Automatico** o **Manuale**, il processo di conversione potrebbe non riuscire se si cambiano gli attributi rilevanti.

Si analizza ad esempio un pacchetto il cui stato di conformità è **Automatico**. Si aggiunge quindi un altro programma al pacchetto. La conversione del pacchetto potrebbe non riuscire.

Se è necessario apportare modifiche a un pacchetto dopo l'analisi, eseguire di nuovo l'analisi prima della conversione. 



## <a name="see-also"></a>Vedere anche

[Informazioni tecniche sui messaggi di errore di Package Conversion Manager](error-messages.md)
