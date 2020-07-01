---
title: Configurare classificazioni e prodotti
titleSuffix: Configuration Manager
description: Seguire questi passaggi per configurare i prodotti e le classificazioni degli aggiornamenti software per la sincronizzazione nella console di Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 4f13ff305ba5fc2b5c5080bafb6fed2412ff8366
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614076"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>configurare le classificazioni e i prodotti per la sincronizzazione  

*Si applica a: Configuration Manager (Current Branch)*

I metadati degli aggiornamenti software vengono recuperati durante il processo di sincronizzazione in Configuration Manager in base alle impostazioni specificate nelle proprietà del componente punto di aggiornamento software. Dopo la sincronizzazione degli aggiornamenti software per la prima volta o al rilascio di nuovi prodotti e classificazioni, è necessario passare alle proprietà per selezionare i nuovi elementi. Utilizzare la procedura seguente per configurare le classificazioni e i prodotti per la sincronizzazione.  

> [!NOTE]  
> Attenersi alla procedura descritta in questa sezione solo nel sito di livello superiore.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Per configurare le classificazioni e i prodotti per la sincronizzazione  

1. Nella console di **Configuration Manager** passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.

2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.  

3. Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**.

4. Nella scheda **Classificazioni** specificare le classificazioni degli aggiornamenti software per cui si desidera sincronizzare gli aggiornamenti software.  

    Ogni aggiornamento software viene definito in base a una classificazione di aggiornamento che consente di organizzare i diversi tipi di aggiornamenti. Durante il processo di sincronizzazione, verranno sincronizzati i metadati degli aggiornamenti software per le classificazioni selezionate. Configuration Manager consente di sincronizzare gli aggiornamenti software con le classificazioni di aggiornamento seguenti:  

     - **Aggiornamenti critici**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico, per un bug critico, non correlato alla sicurezza.  
     - **Aggiornamenti delle definizioni**: specifica un aggiornamento software frequente rilasciato pubblicamente che contiene aggiunte al database che contiene la definizione del prodotto.  
     - **Feature Pack**: specifica le nuove funzionalità del prodotto che vengono distribuite prima al di fuori del rilascio di un prodotto e che in genere sono incluse nella successiva versione completa del prodotto.  
     - **Aggiornamenti della sicurezza**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico del prodotto, correlato alla sicurezza.  
     - **Service Pack**: specifica un insieme cumulativo e testato di tutti gli aggiornamenti rapidi, gli aggiornamenti della sicurezza, gli aggiornamenti critici e gli aggiornamenti che vengono applicati a un prodotto. I Service Pack possono contenere anche aggiornamenti aggiuntivi per problemi rilevati internamente dopo il rilascio del prodotto.  
     - **Strumenti**: specifica un'utilità o una funzionalità che consente di completare una o più attività.  
     - **Aggiornamenti cumulativi**: specifica un insieme cumulativo e testato di aggiornamenti rapidi, aggiornamenti della sicurezza, aggiornamenti critici e aggiornamenti riuniti in un unico pacchetto per semplificarne la distribuzione. Un aggiornamento cumulativo interessa in genere un'area specifica, ad esempio la sicurezza o un componente del prodotto.  
     - **Aggiornamenti**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico. Un aggiornamento risolve un bug non critico, non correlato alla sicurezza.  
     - **Aggiornamento**: specifica un aggiornamento per le caratteristiche e le funzionalità di Windows 10. Per ottenere la classificazione di [aggiornamento](https://support.microsoft.com/kb/3095113), i punti di aggiornamento software e i siti devono eseguire WSUS 6.2 con l'**hotfix 3095113**. Per ulteriori informazioni sull'installazione di questo aggiornamento e altri **aggiornamenti** per gli aggiornamenti, vedere [prerequisiti per gli aggiornamenti software](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).
    
    > [!NOTE]
    > Per sincronizzare i driver di Microsoft Surface, è possibile selezionare la casella di controllo **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware**.<!--1098490--> Tutti i punti di aggiornamento software devono eseguire Windows Server 2016 o versione successiva per sincronizzare correttamente i driver di Surface. Se si abilita un punto di aggiornamento software in un computer che esegue Windows Server 2012 dopo aver abilitato i driver per Surface, i risultati dell'analisi per gli aggiornamenti dei driver non saranno accurati. Questo comportamento causa la visualizzazione di dati di conformità non corretti nella console di Configuration Manager e nei report di Configuration Manager. Per altre informazioni, vedere [Gestire i driver di Surface con Configuration Manager](../deploy-use/surface-drivers.md).

5. Nella scheda **Prodotti** specificare i prodotti per cui si desidera sincronizzare gli aggiornamenti software e quindi fare clic su **Chiudi**.  

    - Configuration Manager archivia un elenco di prodotti e di famiglie di prodotti tra cui è possibile scegliere quando si installa per la prima volta il punto di aggiornamento software. È possibile che i prodotti e le famiglie di prodotti pubblicati dopo il rilascio di Configuration Manager non siano disponibili per la selezione finché non si completa la sincronizzazione degli aggiornamenti software, che aggiorna l'elenco di prodotti e famiglie di prodotti disponibili tra cui è possibile scegliere.  

    - I metadati per ogni aggiornamento software definiscono i prodotti per i quali l'aggiornamento è applicabile. Un prodotto è un'edizione specifica di un sistema operativo o di un'applicazione, ad esempio Windows Server 2012. Una famiglia di prodotti è il sistema operativo o l'applicazione di base da cui derivano i singoli prodotti. Un esempio di famiglia di prodotti è Windows, di cui Windows Server 2012 è membro. È possibile specificare una famiglia di prodotti o singoli prodotti all'interno di una famiglia di prodotti. Il tempo necessario per sincronizzare gli aggiornamenti software è direttamente proporzionale al numero di prodotti selezionati.  

    - Quando gli aggiornamenti software sono applicabili a più prodotti e almeno uno dei prodotti è stato selezionato per la sincronizzazione, tutti i prodotti vengono visualizzati nella console di Configuration Manager, anche se alcuni non sono stati selezionati. Se, ad esempio, Windows Server 2012 è l'unico sistema operativo selezionato e se un aggiornamento software si applica a Windows 8 e a Windows Server 2012, entrambi i prodotti vengono visualizzati nella console di Configuration Manager.  

    > [!NOTE]  
    > **Windows 10 versione 1903 e successive** è stato aggiunto a Microsoft Update come prodotto a sé stante, anziché all'interno del prodotto **Windows 10** come le versioni precedenti. A causa di questa modifica è necessario eseguire una serie di passaggi manuali per assicurarsi che i client visualizzino questi aggiornamenti. Si è cercato di ridurre il numero di passaggi manuali che è necessario eseguire per il nuovo prodotto in Configuration Manager versione 1906. <!--4682946-->
    >
    > Quando si esegue l'aggiornamento a Configuration Manager versione 1906 e il prodotto **Windows 10** è selezionato per la sincronizzazione, vengono eseguite automaticamente le azioni seguenti:
    > - Il prodotto **Windows 10 versione 1903 e successive** viene aggiunto per la sincronizzazione.
    > - Le [regole di distribuzione automatica](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) contenenti il prodotto **Windows 10** verranno aggiornate in modo da includere **Windows 10 versione 1903 e successive**.
    > - I [piani di manutenzione](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) vengono aggiornati in modo che includano il prodotto **Windows 10 versione 1903 e successive**.


## <a name="configuring-products-for-versions-of-windows-10"></a>Configurazione dei prodotti per le versioni di Windows 10

### <a name="windows-10-version-1909"></a>Windows 10, versione 1909

Windows 10, versione 1909, condivide un sistema operativo di base comune con Windows 10, versione 1903. La manutenzione di entrambe le versioni viene eseguita con gli stessi aggiornamenti cumulativi. Per altre informazioni su Windows 10, versione 1909, vedere il post di blog [Windows 10, version 1909 delivery options](https://aka.ms/1909mechanics) (Opzioni di recapito per Windows 10, versione 1909).

Per assicurarsi che i client Windows 10 versione 1909 e Windows 10 versione 1903 installino gli aggiornamenti da Configuration Manager:

- Approvare gli aggiornamenti per entrambe le versioni 1909 e 1903 di Windows 10.
  - Gli aggiornamenti prevedono regole di applicabilità e titoli diversi per ogni versione del sistema operativo.
  - L'approvazione di ogni aggiornamento per ogni versione e architettura del sistema operativo fa parte del normale processo di approvazione per gli amministratori.
- I file di installazione dell'aggiornamento cumulativo sono gli stessi per entrambe le versioni 1909 e 1903 di Windows 10.
  - Configuration Manager scaricherà i file di origine dell'aggiornamento una sola volta.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Aggiornamenti delle funzionalità per Windows 10 versione 1909

Quando si approvano gli aggiornamenti delle funzionalità per Windows 10, versione 1909, sono disponibili diverse opzioni:

- Ai client Windows 10, versione 1903 viene offerto un [pacchetto di abilitazione](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package), rilasciato il 12 novembre 2019.
  - Il pacchetto di abilitazione è un file piccolo e rapido da installare che attiva le funzionalità di Windows 10, versione 1909 e riavvia il dispositivo.
  - I prerequisiti per il pacchetto di abilitazione includono:
    - Aggiornamento cumulativo minimo [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389), rilasciato l'8 ottobre 2019.
    - Aggiornamento dello stack di manutenzione minimo [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390), rilasciato il 24 settembre 2019.
  - Questo aggiornamento, come qualsiasi altro aggiornamento delle funzionalità, non è disponibile per l'importazione da `https:\\catalog.update.microsoft.com`.
  - L'aggiornamento verrà sincronizzato automaticamente con WSUS se per la sincronizzazione sono selezionati il prodotto **Windows 10, versione 1903 e successive** e la classificazione **Aggiornamenti**.
  - Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Manutenzione pacchetti di Windows 10** e selezionare il nodo **Aggiornamenti di tutte le piattaforme Windows 10**. Cercare i termini "abilitazione" o "4517245".

    > [!TIP]
    > Poiché si tratta di aggiornamenti delle funzionalità, non sono inclusi nel nodo **Tutti gli aggiornamenti software**.

- Windows 10, versione 1809 e client precedenti vengono aggiornati con un singolo aggiornamento delle funzionalità diretto.
  - Questa è la stessa procedura valida per tutte le altre installazioni precedenti per gli aggiornamenti delle funzionalità eseguite per Windows 10.

> [!NOTE]
> Sia il pacchetto di abilitazione che l'aggiornamento delle funzionalità tradizionale per Windows 10, versione 1909, vengono visualizzati come "Installati" nei report, indipendentemente dal percorso usato per l'installazione.

### <a name="windows-10-version-1903-and-later"></a>Windows 10 versione 1903 e successive

**Windows 10 versione 1903 e successive** è stato aggiunto a Microsoft Update come prodotto a sé stante, anziché all'interno del prodotto **Windows 10** come le versioni precedenti. A causa di questa modifica è necessario eseguire una serie di passaggi manuali per assicurarsi che i client visualizzino questi aggiornamenti. Si è cercato di ridurre il numero di passaggi manuali che è necessario eseguire per il nuovo prodotto in Configuration Manager versione 1906. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, versione 1903 e versioni successive con Configuration Manager versione 1906
Quando si esegue l'aggiornamento a Configuration Manager versione 1906 e il prodotto **Windows 10** è selezionato per la sincronizzazione, vengono eseguite automaticamente le azioni seguenti:
- Il prodotto **Windows 10 versione 1903 e successive** viene aggiunto per la sincronizzazione.
- Le [regole di distribuzione automatica](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) contenenti il prodotto **Windows 10** verranno aggiornate in modo da includere **Windows 10 versione 1903 e successive**.
- I [piani di manutenzione](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) vengono aggiornati in modo che includano il prodotto **Windows 10 versione 1903 e successive**.

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, versione 1903 e versioni successive con Configuration Manager versione 1902
Se si usa Configuration Manager 1902 con i client Windows 10, versione 1903, sarà necessario:
- Selezionare il prodotto **Windows 10 versione 1903 e successive** per la sincronizzazione.
- Aggiornare eventuali [regole di distribuzione automatica](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) per i client Windows 10, versione 1903.
- Aggiornare i [piani di manutenzione](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) per i client Windows 10, versione 1903.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Programma Windows Insider
<!--3556023-->
A partire da settembre 2019 è possibile eseguire la manutenzione e l'aggiornamento dei dispositivi che eseguono build di Windows Insider Preview con Configuration Manager. Questa modifica significa che è possibile gestire questi dispositivi senza modificare i normali processi o abilitare Windows Update per le aziende. È possibile scaricare gli aggiornamenti delle funzionalità e gli aggiornamenti cumulativi per le build di Windows Insider Preview in Configuration Manager esattamente come qualsiasi altro aggiornamento di Windows 10. Per altre informazioni, vedere il post di blog [Publishing pre-release Windows 10 Feature Updates to WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) (Pubblicazione di aggiornamenti delle funzionalità di Windows 10 in WSUS).

Per altre informazioni sul supporto di Windows insider in Configuration Manager, vedere [Supporto per Windows 10](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Prerequisiti

- Configuration Manager versione 1906 o successiva, configurato per la [gestione degli aggiornamenti software](../plan-design/plan-for-software-updates.md).
- Dispositivi Windows 10 che eseguono la [build di anteprima Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started).
- Raccolta contenente i dispositivi Windows Insider.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Abilitare gli aggiornamenti di Windows Insider

È necessario abilitare i prodotti e le classificazioni per gli aggiornamenti di Windows Insider. Gli aggiornamenti delle funzionalità, gli aggiornamenti cumulativi e gli altri aggiornamenti per Windows Insider sono inclusi nella categoria di prodotto **Versione preliminare di Windows Insider**.

1. Nella console di **Configuration Manager** passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.  
3. Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**.
4. Nella scheda **Prodotti** assicurarsi che siano selezionati i prodotti seguenti per la sincronizzazione:
    - Versione preliminare di Windows Insider
    - Windows 10 versione 1903 e successive
5. Nella scheda **Classificazioni** assicurarsi che siano selezionate le classificazioni seguenti per la sincronizzazione:
    - Aggiornamenti
    - Aggiornamenti della sicurezza
    - Aggiornamenti (facoltativo)
6. Fare clic su **OK** per chiudere **Proprietà del componente del punto di aggiornamento software**.

### <a name="upgrading-windows-insider-devices"></a>Aggiornamento dei dispositivi Windows Insider

Dopo aver sincronizzato gli aggiornamenti per Windows Insider, è possibile visualizzarli in **Raccolta software** > **Manutenzione pacchetti di Windows 10** > **Tutti gli aggiornamenti di Windows 10**.

![Aggiornamenti delle funzionalità di Windows Insider per la manutenzione di Windows 10](media/3556023-windows-insiders-pre-release-feature-update.png)

Distribuire gli aggiornamenti delle funzionalità per Windows Insider nella raccolta di destinazione in modo analogo a qualsiasi altro aggiornamento. Tuttavia, quando si distribuiscono gli aggiornamenti delle funzionalità, è opportuno tenere presente quanto segue:

- Questi aggiornamenti saranno applicabili a tutti i client Windows 10 1903 o versioni precedenti, con architettura, edizione e lingua corrispondenti.
- Esistono condizioni di licenza che devono essere accettate dalla distribuzione per procedere all'installazione.
- Valutare la possibilità di usare la [priorità dei thread nelle impostazioni client](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority).
- L'aggiornamento dinamico installa automaticamente gli aggiornamenti critici, incluso l'aggiornamento cumulativo più recente, direttamente da Microsoft Update. Questo comportamento inizia con gli aggiornamenti delle funzionalità per Windows 10 versione 1903. 
  - È possibile [disabilitare in modo esplicito l'aggiornamento dinamico nelle impostazioni client](../../core/clients/deploy/about-client-settings.md#bkmk_du) o con un [file setupconfig.ini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Per altre informazioni, vedere il post di blog [Windows 10 Dynamic Update](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) (Aggiornamento dinamico di Windows 10).

Per altre informazioni su come distribuire gli aggiornamenti, vedere [Gestire Windows come servizio](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Mantenere aggiornati i dispositivi Insider

Gli aggiornamenti cumulativi per Windows Insider saranno disponibili per WSUS e per estensione per Configuration Manager. Questi aggiornamenti cumulativi verranno rilasciati con una frequenza simile a quella degli aggiornamenti cumulativi di Windows 10 versione 1903. Gli aggiornamenti cumulativi per Windows Insider sono disponibili nella categoria di prodotto **Versione preliminare di Windows Insider** e vengono classificati come **Aggiornamenti della sicurezza** o **Aggiornamenti**. È possibile distribuire gli aggiornamenti cumulativi per Windows Insider usando il normale processo di aggiornamento software con le [regole di distribuzione automatica](../deploy-use/automatically-deploy-software-updates.md) o le [distribuzioni in più fasi](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Aggiornamenti della sicurezza estesa e Configuration Manager

Gli [aggiornamenti della sicurezza estesa (ESU, Extended Security Updates) ](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) sono un'ultima soluzione per i clienti che devono eseguire alcuni prodotti Microsoft legacy oltre la fine del supporto. Il programma ESU include aggiornamenti della sicurezza critici e/o importanti definiti dal [Microsoft Security Response Center (MSRC) ](https://www.microsoft.com/msrc) per un massimo di tre anni dopo la data di fine del supporto "Extended" del prodotto.

I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Sono inclusi tutti i prodotti coperti dal programma ESU. Ad esempio, Windows 7. Gli aggiornamenti della sicurezza rilasciati nel programma ESU verranno pubblicati in Windows Server Update Services (WSUS). Gli aggiornamenti saranno visualizzati nella console di Configuration Manager. Mentre i prodotti coperti dal programma ESU non sono più supportati per l'uso con Configuration Manager, è possibile usare la [versione più recente di Configuration Manager (Current Branch)](../../core/servers/manage/updates.md#version-details) per distribuire e installare gli aggiornamenti della sicurezza di Windows rilasciati nel programma. La versione rilasciata più recente può essere usata anche per distribuire Windows 10 nei dispositivi che eseguono Windows 7.

Le funzionalità di gestione client che non sono correlate alla gestione degli aggiornamenti software Windows o alla distribuzione del sistema operativo non vengono più testate nei sistemi operativi coperti dal programma ESU e non si garantisce che continueranno a funzionare. È consigliabile eseguire l'aggiornamento o la migrazione a una versione corrente dei sistemi operativi appena possibile per ricevere supporto per la gestione dei client.


## <a name="next-steps"></a>Passaggi successivi

Avviare la sincronizzazione degli aggiornamenti software per recuperare gli aggiornamenti software in base ai nuovi criteri. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md).
