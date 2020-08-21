---
title: Gestire le impostazioni per gli aggiornamenti software
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni client appropriate per gli aggiornamenti software nel sito successivi all'installazione del punto di aggiornamento software.
ms.date: 06/04/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e0395d41c2886bca1d623fb2736bfc86012f89b4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696753"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a> Gestire le impostazioni per gli aggiornamenti software  

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver sincronizzato gli aggiornamenti software in Configuration Manager, configurare e verificare le impostazioni nelle sezioni seguenti.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a> Impostazioni client per gli aggiornamenti software  
Dopo aver installato il punto di aggiornamento software, gli aggiornamenti software vengono abilitati sui client per impostazione predefinita e le impostazioni della pagina **Aggiornamenti software** nelle impostazioni client hanno valori predefiniti. Le impostazioni client sono usate a livello di sito e influiscono sui tempi di esecuzione dell'analisi degli aggiornamenti software ai fini della conformità e su come e quando gli aggiornamenti software vengono installati nei computer client. Prima di distribuire gli aggiornamenti software, verificare che le impostazioni client siano appropriate per gli aggiornamenti software del sito.  

> [!IMPORTANT]  
>  L'impostazione **Abilitare aggiornamento software nei client** è abilitata per impostazione predefinita. Se si deseleziona questa impostazione, Configuration Manager rimuoverà i criteri di distribuzione esistenti dal client.  

Per informazioni su come configurare le impostazioni client, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

Per altre informazioni sulle impostazioni client, vedere [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md).  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a> Impostazioni di Criteri di gruppo per gli aggiornamenti software  
Esistono impostazioni di Criteri di gruppo specifiche usate dall'agente di Windows Update (WUA) nei computer client per connettersi a WSUS in esecuzione nel punto di aggiornamento software. Queste impostazioni di Criteri di gruppo vengono usate anche per analizzare la conformità dell'aggiornamento software e per aggiornare automaticamente gli aggiornamenti software e l'agente WUA.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Criteri locali Specifica il percorso del servizio di aggiornamento Microsoft nella rete Intranet  
Quando viene creato il punto di aggiornamento software per un sito, i client ricevono criteri computer che forniscono il nome server del punto di aggiornamento software e configurano i criteri locali **Specifica il percorso del servizio di aggiornamento Microsoft nella rete Intranet** sul computer. L'agente WUA recupera il nome server specificato nell'impostazione **Impostare il servizio di aggiornamento nella rete Intranet per il rilevamento degli aggiornamenti** e quindi si connette a questo server quando analizza la conformità degli aggiornamenti software. Quando vengono creati i criteri dominio per l'impostazione **Specifica il percorso del servizio di aggiornamento Microsoft nella rete Intranet** , questi sovrascrivono i criteri locali e l'agente WUA potrebbe connettersi a un server diverso rispetto al punto di aggiornamento software. In questo caso, il client potrebbe analizzare la conformità degli aggiornamenti software in base ai diversi prodotti, classificazioni e lingue. Pertanto, non è consigliabile configurare i criteri di Active Directory per i computer client.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Criteri di gruppo Consenti contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet  
È necessario abilitare l'impostazione di Criteri di gruppo **Consenti contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet** prima che l'agente WUA sui computer analizzi gli aggiornamenti software creati e pubblicati con System Center Updates Publisher. Quando l'impostazione dei criteri viene abilitata, WUA accetterà gli aggiornamenti software ricevuti tramite un percorso Intranet se gli aggiornamenti software sono firmati nell'archivio certificati **Autori attendibili** sul computer locale. Per ulteriori informazioni sulle impostazioni di Criteri di gruppo necessarie per Updates Publisher, vedere [Updates Publisher 2011 Documentation Library (Libreria della documentazione di Updates Publisher 2011)](/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

### <a name="automatic-updates-configuration"></a>Configurazione di Aggiornamenti automatici  
Aggiornamenti automatici consente di ricevere aggiornamenti della sicurezza e altri download importanti sui computer client. Aggiornamenti automatici viene configurato tramite l'impostazione di Criteri di gruppo **Configura Aggiornamenti automatici** o tramite il Pannello di controllo sul computer locale. Quando Aggiornamenti automatici viene abilitato, i computer client riceveranno le notifiche degli aggiornamenti e, in base alle impostazioni configurate, i computer client scaricheranno e installeranno gli aggiornamenti necessari. Quando Aggiornamenti automatici coesiste con gli aggiornamenti software, su ogni computer client potrebbero essere visualizzate icone di notifica e notifiche popup per lo stesso aggiornamento. Inoltre, quando è necessario un riavvio, su ogni computer client potrebbe essere visualizzata una finestra di dialogo di riavvio per lo stesso aggiornamento.  

### <a name="self-update"></a>Aggiornamento automatico  
Quando Aggiornamenti automatici viene abilitato sui computer client, l'agente WUA esegue automaticamente un aggiornamento automatico quando è disponibile una versione più recente o quando si verificano problemi con un componente WUA. Quando Aggiornamenti automatici non è configurato o è disabilitato e i computer client dispongono di una versione precedente dell'agente WUA, i computer client devono eseguire il file di installazione WUA.  

## <a name="software-updates-properties"></a>Proprietà degli aggiornamenti software
Le proprietà degli aggiornamenti software forniscono informazioni sugli aggiornamenti software e sul contenuto associato. È inoltre possibile usare queste proprietà per configurare le impostazioni per gli aggiornamenti software. Quando si aprono le proprietà per più aggiornamenti software, vengono visualizzate solo le schede **Tempo di esecuzione massimo** e **Gravità personalizzata** .   

Usare la seguente procedura per aprire le proprietà degli aggiornamenti software.  

#### <a name="to-open-software-update-properties"></a>Per aprire le proprietà degli aggiornamenti software  

1. Nella console di Configuration Manager fare clic su **Raccolta software**.  
2. Nell'area di lavoro Raccolta software, espandere **Aggiornamenti software**, quindi fare clic su **Tutti gli aggiornamenti software**.  
3. Selezionare uno o più aggiornamenti software e quindi nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** .  

   > [!NOTE]  
   >  Nel nodo **Tutti gli aggiornamenti software** Configuration Manager visualizza solo gli aggiornamenti software con classificazione **Errore critico** e **Sicurezza** rilasciati negli ultimi 30 giorni.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a> Verificare le informazioni sugli aggiornamenti software  
Nelle proprietà degli aggiornamenti software, è possibile verificare le informazioni dettagliate su un aggiornamento software. Le informazioni dettagliate non vengono visualizzate quando si seleziona più di un aggiornamento software. Nelle seguenti sezioni vengono descritte le informazioni disponibili per un aggiornamento software selezionato.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a> Dettagli sugli aggiornamenti software  
Nella scheda **Dettagli aggiornamento** è possibile visualizzare le seguenti informazioni di riepilogo relative all'aggiornamento software selezionato:  

- **ID bollettino**: specifica l'ID bollettino associato agli aggiornamenti software di protezione. È possibile trovare i dettagli relativi al bollettino sulla sicurezza cercando l'ID bollettino nella pagina Web [Microsoft Security Response Center](https://portal.msrc.microsoft.com/).  

> [!NOTE]
> Il modo in cui Microsoft documenta gli aggiornamenti della sicurezza sta cambiando. Il modello precedente usava le pagine Web dei bollettini sulla sicurezza e includeva i numeri ID dei bollettini sulla sicurezza (ad esempio, MS16-XXX) come riferimento. Questa formato della documentazione degli aggiornamenti della sicurezza, inclusi i numeri ID dei bollettini, è in fase di ritiro e verrà sostituito con la guida agli aggiornamenti della sicurezza. Invece che sugli ID dei bollettini, la nuova guida si basa sui numeri ID delle vulnerabilità e sui numeri ID degli articoli della KB. Per altre informazioni, vedere le [domande frequenti sulla guida agli aggiornamenti della sicurezza](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **ID articolo**: specifica l'ID articolo per l'aggiornamento software. L'articolo di riferimento fornisce informazioni più dettagliate sull'aggiornamento software e il problema che l'aggiornamento software consente di correggere o migliorare.  

- **Data di revisione**: specifica la data dell'ultima modifica dell'aggiornamento software.  

- **Livello di gravità massimo**: specifica il livello di gravità definito dal fornitore per l'aggiornamento software.  

- **Descrizione**: fornisce una panoramica della condizione che l'aggiornamento software consente di correggere o migliorare.  

- **Lingue applicabili**: elenca le lingue per cui è applicabile l'aggiornamento software.  

- **Prodotti interessati**: elenca i prodotti per cui è applicabile l'aggiornamento software.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a> Informazioni sul contenuto  
Nella scheda **Informazioni sul contenuto** , esaminare le seguenti informazioni sul contenuto che è associato con l'aggiornamento software selezionato:  

-   **ID contenuto**: specifica l'ID contenuto per l'aggiornamento software.  

-   **Scaricato**: indica se Configuration Manager ha scaricato i file dell'aggiornamento software.  

-   **Lingua**: specifica le lingue per l'aggiornamento software.  

-   **Percorso di origine**: specifica il percorso ai file di origine dell'aggiornamento software.  

-   **Dimensione (MB)** : specifica le dimensioni dei file di origine dell'aggiornamento software.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> Informazioni sul bundle personalizzato  
Nella scheda **Informazioni sul bundle personalizzato** , esaminare le informazioni sul bundle personalizzato per l'aggiornamento software. Quando l'aggiornamento software selezionato contiene aggiornamenti software in bundle contenuti nel file di aggiornamento software, essi vengono visualizzati nella sezione **Informazioni sul bundle** . Questa scheda non visualizza gli aggiornamenti software in bundle che sono visualizzati nella scheda **Informazioni sul contenuto** , come i file di aggiornamento per le diverse lingue.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> Informazioni di sostituzione  
Nella scheda **Informazioni di sostituzione** , è possibile visualizzare le seguenti informazioni sulla sostituzione dell'aggiornamento software:  

- **Questo aggiornamento è stato sostituito dai seguenti aggiornamenti**: specifica gli aggiornamenti software che sostituiscono questo aggiornamento, il che significa che gli aggiornamenti elencati sono più recenti. Nella maggior parte dei casi, si distribuirà uno degli aggiornamenti software che sostituisce l'aggiornamento software in questione. Gli aggiornamenti software che vengono visualizzati nell'elenco contengono collegamenti ipertestuali a pagine Web che forniscono ulteriori informazioni sugli aggiornamenti software. Quando questo aggiornamento non viene sostituito, viene visualizzato **Nessuno** .  

- **Questo aggiornamento sostituisce i seguenti aggiornamenti**: specifica gli aggiornamenti software che sono sostituiti da questo aggiornamento software, il che significa che questo aggiornamento software è più recente. Nella maggior parte dei casi, si distribuirà questo aggiornamento software per sostituire gli aggiornamenti software sostituiti. Gli aggiornamenti software che vengono visualizzati nell'elenco contengono collegamenti ipertestuali a pagine Web che forniscono ulteriori informazioni sugli aggiornamenti software. Quando questo aggiornamento non sostituisce eventuali altri aggiornamenti, viene visualizzato **Nessuno** .  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> Configurare le impostazioni degli aggiornamenti software  
Nella proprietà, è possibile configurare le impostazioni degli aggiornamenti software per uno o più aggiornamenti software. È possibile configurare la maggior parte delle impostazioni degli aggiornamenti software solo nel sito di amministrazione centrale o nel sito primario autonomo. Le sezioni seguenti consentono di configurare le impostazioni per gli aggiornamenti software.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> Impostare il tempo di esecuzione massimo  
Nella scheda **Tempo di esecuzione massimo** , impostare la quantità massima di tempo assegnata per completare un aggiornamento software nei computer client. Se l'aggiornamento richiede più tempo del valore del tempo di esecuzione massimo, Configuration Manager crea un messaggio di stato e interrompe l'installazione degli aggiornamenti software. È possibile configurare questa impostazione solo nel sito di amministrazione centrale o in un sito primario autonomo.  

Configuration Manager usa inoltre questa impostazione per stabilire se avviare l'installazione dell'aggiornamento software all'interno di una finestra di manutenzione configurata. Se il valore del tempo di esecuzione massimo è maggiore del tempo rimanente disponibile nella finestra di manutenzione, l'installazione degli aggiornamenti software viene rimandata fino all'avvio della nuova finestra di manutenzione. Quando più aggiornamenti software devono essere installati su un computer client con una finestra di manutenzione configurata (intervallo di tempo), l'aggiornamento software con il tempo di esecuzione massimo più basso viene installato per primo, poi viene installato quello con il secondo tempo di esecuzione massimo più basso e così via. Prima dell'installazione di ogni aggiornamento software, il client verifica che la finestra di manutenzione disponibile fornirà un tempo sufficiente per installare l'aggiornamento software. Dopo l'avvio dell'installazione di un aggiornamento software, l'installazione continuerà anche se va oltre la fine della finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

Nella scheda **Tempo di esecuzione massimo** , è possibile visualizzare e configurare le seguenti impostazioni:  

- **Tempo di esecuzione massimo**: specifica il numero massimo di minuti assegnati per il completamento dell'installazione di un aggiornamento software prima che l'installazione stessa venga interrotta da Configuration Manager. Questa impostazione viene anche usata per stabilire se resta un tempo sufficiente a disposizione per installare l'aggiornamento prima della fine di una finestra di manutenzione. L'impostazione predefinita è 60 minuti per i Service Pack. Per altri tipi di aggiornamento software, il valore predefinito è 10 minuti se si è eseguito l'aggiornamento a Configuration Manager versione 1511 o successiva e 5 minuti se si è eseguito l'aggiornamento da una versione precedente. I valori possono variare da 5 a 9.999 minuti.  

> [!IMPORTANT]  
>  Assicurarsi di impostare un valore per il tempo di esecuzione massimo inferiore all'intervallo di tempo della finestra di manutenzione configurata o di aumentare l'intervallo di tempo della finestra di manutenzione impostandolo su un valore superiore al tempo di esecuzione massimo. In caso contrario, l'installazione dell'aggiornamento software non verrà mai avviata.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a> Impostare la gravità personalizzata  
Nelle proprietà dell'aggiornamento software, è possibile usare la scheda **Gravità personalizzata** per configurare i valori di gravità personalizzata per gli aggiornamenti software. Ciò può rivelarsi necessario se i valori di gravità predefiniti non soddisfano le relative esigenze. I valori personalizzati sono elencati nella colonna **Gravità personalizzata** nella console di Configuration Manager. È possibile filtrare gli aggiornamenti software per valori di gravità personalizzata definiti ed è possibile inoltre creare query e rapporti per filtrare questi valori. È possibile configurare questa impostazione solo nel sito di amministrazione centrale o in un sito primario autonomo.  

È possibile configurare le seguenti impostazioni nella scheda **Gravità personalizzata** .  

- **Gravità personalizzata**: imposta un valore di gravità personalizzato per gli aggiornamenti software. Selezionare **Errore critico**, **Importante**, **Medio**o **Basso** dall'elenco. Per impostazione predefinita, il valore di gravità personalizzato è vuoto.

## <a name="crl-checking-for-software-updates"></a>Controllo CRL per aggiornamenti software
Per impostazione predefinita, l'elenco di revoche di certificati (CRL) non viene controllato durante la verifica della firma negli aggiornamenti software di Configuration Manager. Il controllo dell'elenco CRL a ogni utilizzo del certificato offre una maggiore protezione dall'utilizzo di un certificato revocato, ma introduce un ritardo nella connessione e genera un'ulteriore elaborazione nel computer che esegue il controllo CRL.  

Se usato, è necessario attivare il controllo CRL nelle console di Configuration Manager che elaborano gli aggiornamenti software.  

#### <a name="to-enable-crl-checking"></a>Per attivare il controllo CRL  
Nel computer che esegue il controllo CRL eseguire quanto segue da un prompt dei comandi del DVD del prodotto: **\SMSSETUP\BIN\X64\\** <*lingua*> **\UpdDwnldCfg.exe /checkrevocation**.  

Per l'inglese (USA), ad esempio, eseguire **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**