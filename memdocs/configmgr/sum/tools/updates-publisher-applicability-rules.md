---
title: Regole di applicabilità
titleSuffix: Configuration Manager
description: Gestire le regole di applicabilità per System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2a3d810fa2a3b8630b50b702e03ab9666661560d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700149"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Gestire le regole di applicabilità in Updates Publisher

*Si applica a: System Center Updates Publisher*

Con Updates Publisher le regole di applicabilità definiscono i requisiti che è necessario soddisfare per consentire a un dispositivo di installare un aggiornamento. Le regole vengono usate anche per determinare se nel computer è installato un aggiornamento. Una regola di applicabilità complessa e composta da più parti viene denominata set di regole.

Le aggregazioni di aggiornamenti non usano regole di applicabilità.

## <a name="overview-of-applicability-rules"></a>Panoramica delle regole di applicabilità
Le regole di applicabilità vengono gestite nell'**area di lavoro Regole**. Quando si crea una regola, si specificano una o più condizioni. Quando si specificano più condizioni, è possibile configurare relazioni tra di esse. In questo modo, le relazioni vengono valutate in modo sequenziale oppure combinate in istruzioni logiche di tipo **And** o **Or**.

Nell'esempio seguente viene illustrato un set di regole contenente tre regole. La prima regola verifica che il file *MyFile* esista, mentre la seconda e terza regola verificano che la lingua del sistema operativo Windows sia l'inglese o il giapponese.

``` Example
And  
  File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Tutti gli aggiornamenti richiedono almeno una regola di applicabilità. Per gli aggiornamenti in fase di importazione sono già attive regole di applicabilità. Quando si creano aggiornamenti personalizzati, è necessario aggiungere ad essi una o più regole. È possibile modificare ed espandere le regole per qualsiasi aggiornamento in Updates Publisher.

Per visualizzare le regole create, nell'**area di lavoro Regole** selezionare una regola dall'elenco **My saved rules** (Regole personali salvate). Le singole condizioni e operazioni logiche per una regola vengono visualizzate nel riquadro **Applicability Rules** (Regole di applicabilità) della console. Le regole per un aggiornamento in fase di importazione possono essere visualizzate e modificate solo quando si modifica tale aggiornamento.

È possibile creare regole in due posizioni in Updates Publisher:

-   Nell'**area di lavoro Regole** vengono creati e **salvati** set di regole che è possibile usare in un secondo momento. Quando si modifica o si crea un aggiornamento, è possibile selezionare **Saved rule** (Regola salvata) come **Tipo di regola** e quindi eseguire una selezione da un elenco di set di regole creati in precedenza.

-   È anche possibile creare nuove regole al momento della creazione o della modifica di un aggiornamento. Le regole create in questo modo non vengono salvate per uso futuro.

## <a name="create-applicability-rule"></a>Creare una regola di applicabilità
Le informazioni seguenti sono simili a quelle per la creazione di regole nella [Creazione guidata aggiornamento](create-updates-with-updates-publisher.md#use-the-create-update-wizard). A differenza di quanto si verifica nella procedura guidata, però, è possibile salvare i set di regole per un uso futuro.

1. Nell'**area di lavoro Regole** scegliere **Crea** per aprire la **Creazione guidata regola**.

2. Specificare un nome per la regola, quindi fare clic su ![Nuova regola](media/newrule.png). Verrà visualizzata la pagina **Applicability Rule** (Regola di applicabilità) in cui è possibile configurare le regole.

3. Per **Tipo di regole** selezionare una delle opzioni seguenti. Le opzioni che è necessario configurare variano per ogni tipo:

   - **File**: usare questa regola per indicare che, per poter eseguire l'aggiornamento, nel dispositivo deve essere presente un file con proprietà che soddisfano uno o più dei criteri specificati.

   - **Registro di sistema**: usare questo tipo per specificare i dettagli del Registro di sistema che devono essere presenti per consentire l'installazione dell'aggiornamento nel dispositivo.

   - **Sistema**: questa regola usa i dettagli relativi al sistema per determinare l'applicabilità. È possibile scegliere tra la definizione di una versione di Windows, un linguaggio di Windows o l'architettura del processore. In alternativa, è possibile specificare una query WMI per identificare il sistema operativo dei dispositivi.

   - **Windows Installer**: usare questa regola per determinare l'applicabilità in base a una patch installata Windows Installer o con estensione msi. È anche possibile determinare se funzionalità o componenti specifici vengono installati come parte del requisito.

     > [!IMPORTANT]   
     > Nel dispositivi gestiti, l'agente di Windows Update non è in grado di rilevare i pacchetti del programma di installazione di Windows installati per utente. Quando si usa questo tipo di regola, configurare regole di applicabilità aggiuntive, come le versioni del file o i valori della chiave del Registro di sistema, in modo che il pacchetto Windows Installer possa essere rilevato correttamente sia in base a un criterio "per utente" che in base a un criterio "per sistema".

   - **Saved rule** (Regola salvata): questa regola consente di trovare e usare regole precedentemente configurate e salvate.

4. Continuare ad aggiungere e configurare regole aggiuntive in base alle esigenze.

5. Usare i pulsanti corrispondenti alle operazioni logiche per ordinare e raggruppare regole differenti in modo da creare controlli dei requisiti più complessi.

6. Quando il set di regole è completo, fare clic su **OK** per salvarlo. Il set di regole viene ora visualizzato nell'elenco **My saved rules** (Regole personali salvate).

## <a name="edit-applicability-rule-sets"></a>Modificare set di regole di applicabilità
Per modificare una regola di applicabilità, nell'**area di lavoro Regole** selezionare una regola presente nell'elenco **My saved rules** (Regole personali salvate), quindi scegliere il pulsante **Modifica** dalla barra multifunzione. Viene avviata la **Modifica guidata regola**.

La **Modifica guidata regola** visualizza le regole correnti per il set di regole. La procedura per la modifica delle regole è analoga a quella per la creazione di nuove regole con la **Creazione guidata regola**. È possibile usare questa procedura guidata per rinominare il set di regole, eliminare regole, riordinare regole e relazioni o aggiungere nuove regole.

Dopo aver apportato le modifiche, scegliere **OK** per salvarle e chiudere la procedura guidata.

Per altri dettagli sull'uso della Creazione guidata regola, vedere il **Passaggio 7**, relativo alla pagina Applicabilità, della [Creazione guidata aggiornamento](create-updates-with-updates-publisher.md#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Eliminare regole di applicabilità
Per eliminare una regola di applicabilità salvata, nell'**area di lavoro Regole** selezionare la regola o il set di regole dall'elenco **My saved rules** (Regole personali salvate), quindi scegliere **Elimina** dalla barra multifunzione. Questa operazione rimuove da Updates Publisher la regola o il set di regole salvato.

Per eliminare una regola da un aggiornamento specifico, è necessario [modificare tale aggiornamento](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).
