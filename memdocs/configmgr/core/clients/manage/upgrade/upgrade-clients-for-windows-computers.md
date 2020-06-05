---
title: Aggiornare i client in Windows
titleSuffix: Configuration Manager
description: Aggiornare i client di Configuration Manager in computer Windows.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b0a69b07a3be633434203f93b0724cec4ea88a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347143"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Come aggiornare i client per i computer Windows in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Aggiornare il client Configuration Manager in computer Windows usando i metodi di installazione client o le funzionalità di aggiornamento client automatico. I metodi di installazione client seguenti sono validi per aggiornare il software client nei computer Windows:  

- Installazione con Criteri di gruppo  

- Installazione tramite script di accesso  

- Installazione manuale  

- Aggiornare l'installazione  

Per altre informazioni, vedere [Come distribuire i client nei computer Windows](../../deploy/deploy-clients-to-windows-computers.md).

Escludere client dall'aggiornamento specificando una raccolta di esclusioni. Per altre informazioni, vedere [Come evitare l'aggiornamento dei client](exclude-clients-windows.md). I client esclusi scaricano ed eseguono comunque CCMSETUP, ma non saranno aggiornati.

> [!TIP]  
> Se si aggiorna l'infrastruttura server da una versione precedente di Configuration Manager, completare gli aggiornamenti del server prima di aggiornare i client Configuration Manager. Questo processo include l'installazione di tutti gli aggiornamenti Current Branch. L'aggiornamento Current Branch più recente contiene la versione più recente del client. Aggiornare i client dopo aver installato tutti gli aggiornamenti di Configuration Manager.

> [!NOTE]
> Se si prevede di riassegnare il sito dei client durante l'aggiornamento, specificare il nuovo sito tramite la proprietà client.msi `SMSSITECODE`. Se si usa il valore `AUTO` per `SMSSITECODE`, specificare anche `SITEREASSIGN=TRUE`. Questa proprietà consente la riassegnazione automatica del sito durante l'aggiornamento. Per altre informazioni, vedere [Proprietà di installazione del client - SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a> Informazioni sull'aggiornamento client automatico

Configurare il sito per l'aggiornamento automatico dei client alla versione di Configuration Manager più recente. Quando Configuration Manager rileva che la versione di un client assegnato è precedente alla versione della gerarchia, aggiorna automaticamente il client. Questo scenario include l'aggiornamento del client all'ultima versione durante il tentativo di assegnazione a un sito di Configuration Manager.  

È possibile aggiornare automaticamente un client negli scenari seguenti:  

- La versione client è precedente a quella usata nella gerarchia.  

- Nel client sul sito di amministrazione centrale è installato un Language Pack non presente nel client esistente.  

- Un prerequisito client nella gerarchia prevede una versione differente rispetto a quella installata sul client.  

- Uno o più file di installazione client hanno una versione diversa.  

> [!NOTE]  
> Per individuare le diverse versioni del client di Configuration Manager nella gerarchia, è possibile eseguire il report **Conteggio dei client di Configuration Manager per versioni client** nella cartella report **Sito - Informazioni client**.  

Per impostazione predefinita Configuration Manager crea un pacchetto di aggiornamento. Invia automaticamente il pacchetto a tutti i punti di distribuzione nella gerarchia. Se si apportano modifiche al pacchetto client nel sito di amministrazione centrale, Configuration Manager aggiorna automaticamente il pacchetto e lo ridistribuisce. Una modifica di esempio è quando si aggiunge un Language Pack client. Se si abilita l'aggiornamento client automatico, il nuovo Language Pack client sarà installato automaticamente su tutti i client.

Abilitare l'aggiornamento client automatico nell'intera gerarchia. Questa configurazione consente di mantenere i client aggiornati con il minimo sforzo.  

Se si gestiscono anche i sistemi del sito di Configuration Manager come client, determinare se includerli come parte del processo di aggiornamento automatico. È possibile escludere tutti i server o una raccolta specifica dall'aggiornamento del client. Alcuni ruoli del sito di Configuration Manager condividono il framework client. Ad esempio, il punto di gestione e il punto di distribuzione pull. Questi ruoli vengono aggiornati quando si aggiorna il sito, in modo che la versione del client in questi server venga aggiornata contemporaneamente.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a> Configurare l'aggiornamento automatico del client

Usare la procedura seguente per configurare l'aggiornamento client automatico nel sito di amministrazione centrale. Questa configurazione si applica a tutti i client nella gerarchia.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Siti**.  

1. Nella scheda **Home** della barra multifunzione selezionare **Impostazioni gerarchia** nel gruppo **Siti**.  

1. Passare alla scheda **Aggiornamento client**. Verificare la versione e la data del client di produzione. Assicurarsi che sia la versione che si vuole usare per aggiornare i client. Se la versione del client non è quella prevista, potrebbe essere necessario alzare il livello del client di preproduzione a client di produzione. Per altre informazioni, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione](test-client-upgrades.md).  

1. Selezionare **Aggiorna tutti i client nella gerarchia usando il client di produzione**. Selezionare **OK** per confermare.  

1. Se non si vuole che gli aggiornamenti client si applichino ai server, selezionare **Non aggiornare i server**.  

1. Specificare il numero di giorni entro i quali i dispositivi devono aggiornare il client. Dopo che il dispositivo ha ricevuto i criteri, aggiorna il client con un intervallo casuale entro il numero di giorni specificato. Questo comportamento impedisce l'aggiornamento simultaneo di un numero elevato di client.

    > [!NOTE]
    > Per eseguire l'aggiornamento del client, è necessario che un computer sia in esecuzione. Se invece il computer non è esecuzione nel momento in cui è pianificata la ricezione dell'aggiornamento, l'aggiornamento non sarà eseguito. Quando il computer viene acceso e riceve i criteri, pianifica l'aggiornamento per un periodo casuale entro il numero di giorni consentito. Se i giorni per eseguire l'aggiornamento sono scaduti, l'aggiornamento sarà pianificato per essere eseguito in un momento casuale entro 24 ore dall'accensione del computer.
    >
    > Dato tale comportamento, è possibile che i computer che vengono regolarmente arrestati impieghino più tempo del previsto per eseguire l'aggiornamento se il momento casuale dell'aggiornamento pianificato non rientra nelle normali ore lavorative.

1. Per escludere i client dall'aggiornamento, selezionare **Escludi i client specificati dall'aggiornamento** e specificare la raccolta da escludere. Per altre informazioni, vedere [Escludere i client dall'aggiornamento](exclude-clients-windows.md).

1. Se si vuole che il pacchetto di installazione venga copiato nei punti di distribuzione che sono stati abilitati per i [contenuti in versione di preproduzione](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent), selezionare l'opzione **Distribuisci automaticamente il pacchetto di installazione client nei punti di distribuzione abilitati per i contenuti in versione di preproduzione**.  

1. Selezionare **OK** per salvare le impostazioni e chiudere le Proprietà delle impostazioni di gerarchia.

I client ricevono queste impostazioni al successivo download dei criteri.

> [!NOTE]
> Per gli aggiornamenti client vengono rispettate tutte le finestre di manutenzione di Configuration Manager configurate. Il thread execmgr esegue solo il programma di bootstrap dell'installazione client (ccmsetup.exe) durante una finestra di manutenzione. Se il dispositivo esegue un'edizione di Windows con un filtro di scrittura, ccmsetup tenta di eseguire download e installazione allo stesso tempo. In caso contrario, ccmsetup sceglie in modo casuale un orario per scaricare il contenuto. Dopo aver scaricato il contenuto e compilato i criteri locali, execmgr pianifica l'aggiornamento del client durante la finestra di manutenzione successiva.<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>Passaggi successivi

Per metodi alternativi per aggiornare i client, vedere [Come distribuire i client nei computer Windows](../../deploy/deploy-clients-to-windows-computers.md).

Escludere client specifici dall'aggiornamento automatico. Per altre informazioni, vedere [Come evitare l'aggiornamento dei client](exclude-clients-windows.md).
