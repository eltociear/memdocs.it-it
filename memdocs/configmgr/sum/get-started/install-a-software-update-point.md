---
title: installare e configurare un punto di aggiornamento software
titleSuffix: Configuration Manager
description: I siti primari richiedono un punto di aggiornamento software nel sito di amministrazione centrale per la valutazione della conformità degli aggiornamenti software e per la distribuzione degli aggiornamenti software nei client.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 1f3ab3c108a7f8481aee84b6df5cd41b4b186246
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718842"
---
# <a name="install-and-configure-a-software-update-point"></a>installare e configurare un punto di aggiornamento software  

*Si applica a: Configuration Manager (Current Branch)*


> [!IMPORTANT]  
>  Prima di installare il ruolo del sistema del sito del punto di aggiornamento software, è necessario verificare che il server soddisfi le dipendenze richieste e stabilisca l'infrastruttura del punto di aggiornamento software nel sito. Per altre informazioni su come pianificare gli aggiornamenti software e stabilire l'infrastruttura del punto di aggiornamento software, vedere [Plan for software updates](../plan-design/plan-for-software-updates.md) (Pianificare aggiornamenti software).  

 Il punto di aggiornamento software è richiesto nel sito di amministrazione centrale e nei siti primari per abilitare la valutazione della conformità degli aggiornamenti software e per distribuire gli aggiornamenti software ai client. Il punto di aggiornamento software è facoltativo nei siti secondari. Il ruolo del sistema sito del punto di aggiornamento software deve essere creato in un server in cui è installato WSUS. Il punto di aggiornamento software interagisce con i servizi WSUS per configurare le impostazioni di aggiornamento software e per richiedere la sincronizzazione dei metadati degli aggiornamenti software. Nel caso di una gerarchia di Configuration Manager, installare e configurare il punto di aggiornamento software prima nel sito di amministrazione centrale, quindi nei siti primari figli e infine, facoltativamente, nei siti secondari. Nel caso di un sito primario autonomo, non un sito di amministrazione centrale, installare e configurare il punto di aggiornamento software prima nel sito primario e facoltativamente nei siti secondari. Alcune impostazioni sono disponibili solo quando si configura il punto di aggiornamento software in un sito di livello superiore. Esistono diverse opzioni che è necessario considerare in base a dove è installato il punto di aggiornamento software.  

> [!IMPORTANT]  
>  È possibile installare più di un punto di aggiornamento software in un sito. Il primo punto di aggiornamento software installato viene configurato come origine della sincronizzazione che sincronizza gli aggiornamenti da Microsoft Update o da un'origine di sincronizzazione upstream. Gli altri punti di aggiornamento software nel sito sono configurati come repliche del primo punto di aggiornamento software. Pertanto, alcune impostazioni non sono disponibili dopo aver installato e configurato il punto di aggiornamento software iniziale.  

> [!IMPORTANT]  
>  Non è supportata l'installazione del ruolo del sistema del sito per il punto di aggiornamento software in un server che è stato configurato e usato come server WSUS autonomo o l'uso di un punto di aggiornamento software per gestire direttamente i client WSUS. I server WSUS esistenti sono supportati solo come origini di sincronizzazione upstream per il punto di aggiornamento software attivo. Vedere [Sincronizza da un percorso di origine dati upstream](#BKMK_wsussync)

 È possibile aggiungere il ruolo del sistema sito del punto di aggiornamento software a un server del sistema del sito esistente oppure è possibile crearne uno nuovo. Nella pagina **Selezione ruolo del sistema** della **Creazione guidata server del sistema sito** o dell'**Aggiunta guidata ruoli del sistema del sito**, a seconda che si aggiunga il ruolo del sistema del sito a un server del sito nuovo o esistente, selezionare **Punto di aggiornamento software** e quindi configurare le impostazioni del punto di aggiornamento software nella procedura guidata. Le impostazioni sono diverse a seconda della versione di Configuration Manager che si usa. Per altre informazioni su come installare i ruoli del sistema del sito, vedere [Installare ruoli del sistema del sito](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Utilizzare le sezioni seguenti per informazioni sulle impostazioni del punto di aggiornamento software in un sito.  

## <a name="proxy-server-settings"></a>Impostazioni del server proxy  
 È possibile configurare le impostazioni del server proxy all'interno di pagine diverse della **Creazione guidata server del sistema sito** o dell'**Aggiunta guidata ruoli del sistema del sito** in base alla versione di Configuration Manager in uso.  

-   È necessario configurare il server proxy e quindi specificare quando utilizzare il server proxy per gli aggiornamenti software. Configurare le seguenti impostazioni:  

    -   Configurare le impostazioni del server proxy nella pagina **Proxy** della procedura guidata o nella scheda **Proxy** in Proprietà sistema del sito. Le impostazioni del server proxy sono specifiche del sistema del sito, pertanto tutti i ruoli del sistema del sito usano le impostazioni del server proxy specificate.  

    -   Specificare se usare un server proxy quando Configuration Manager sincronizza gli aggiornamenti software e scarica contenuti tramite una regola di distribuzione automatica. Configurare le impostazioni del server proxy nel punto di aggiornamento software nella pagina **Impostazioni proxy e account** della procedura guidata o nella scheda **Impostazioni proxy e account** in Proprietà punto di aggiornamento software.  

        > [!NOTE]  
        >  L'impostazione **Utilizzare un server proxy quando si scaricano contenuti tramite le regole di distribuzione automatica** è disponibile ma non viene utilizzata per un punto di aggiornamento software in un sito secondario. Solo il punto di aggiornamento software nel sito di amministrazione centrale e nel sito primario scarica i contenuti dalla pagina di Microsoft Update.  

> [!IMPORTANT]  
>  Per impostazione predefinita, l'account **Sistema locale** per il server in cui è stata creata una regola di distribuzione automatica viene utilizzato per connettersi a Internet e scaricare gli aggiornamenti software quando sono in esecuzione le regole di distribuzione automatica. Quando questo account non dispone di accesso a Internet, non è possibile scaricare gli aggiornamenti software e in ruleengine.log viene registrata la seguente voce: **Impossibile scaricare l'aggiornamento da Internet. Errore = 12007**. Configurare le credenziali per la connessione al server proxy quando l'account di sistema locale non dispone di accesso a Internet.  


## <a name="wsus-settings"></a>Impostazioni di WSUS  
 È necessario configurare le impostazioni WSUS in diverse pagine della **Creazione guidata server del sistema sito** o dell'**Aggiunta guidata ruoli del sistema del sito** in base alla versione di Configuration Manager in uso e, in alcuni casi, solo nelle proprietà per il punto di aggiornamento software, note anche come Proprietà del componente del punto di aggiornamento software. Utilizzare le informazioni nelle sezioni riportate di seguito per configurare le impostazioni WSUS.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>Impostazioni della porta WSUS  
 È necessario configurare le impostazioni della porta di WSUS nella pagina Punto di aggiornamento software della procedura guidata o nelle proprietà del punto di aggiornamento software. Usare la procedura seguente per determinare le impostazioni della porta usate da Windows Server Update Services.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Per determinare le impostazioni della porta usate in IIS  

 1.  Nel server WSUS aprire Gestione Internet Information Services (IIS).  

 2.  Espandere **Siti**, fare clic con il pulsante destro del mouse sul server WSUS e quindi su **Modifica binding**. Nella finestra di dialogo Binding sito i valori di porta HTTP e HTTPS vengono visualizzati nella colonna **Porta** .


### <a name="configure-ssl-communications-to-wsus"></a>Configurare le comunicazioni SSL in WSUS  
 È possibile configurare la comunicazione SSL nella pagina **Generale** della procedura guidata o nella scheda **Generale** nelle proprietà del punto di aggiornamento software.  

 Per altre informazioni sull'uso di SSL, vedere [Decidere se configurare WSUS per l'uso di SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL) e [Configurare un punto di aggiornamento software per l'uso di TLS/SSL con un certificato PKI](../get-started/software-update-point-ssl.md).  

### <a name="wsus-server-connection-account"></a>Account di connessione al server WSUS  
 È possibile configurare un account che il server del sito utilizzerà per connettersi a WSUS in esecuzione nel punto di aggiornamento software. Se non si configura questo account, Configuration Manager si connette a WSUS tramite l'account computer del server del sito. Configurare l'account di connessione al server WSUS nella pagina **Impostazioni proxy e account** della procedura guidata o nella scheda **Impostazioni proxy e account** nelle proprietà del punto di aggiornamento software.  È possibile configurare l'account nelle pagine della procedura guidata a seconda della versione di Configuration Manager in uso.  

 Per altre informazioni sugli account di Configuration Manager, vedere [Account usati](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Origine di sincronizzazione  
 È possibile configurare l'origine sincronizzazione upstream per la sincronizzazione degli aggiornamenti software nella pagina **Origine sincronizzazione** della procedura guidata oppure nella scheda **Impostazioni di sincronizzazione** in Proprietà del componente del punto di aggiornamento software. Le opzioni per l'origine di sincronizzazione variano a seconda del sito.  

 Utilizzare la seguente tabella per le opzioni disponibili quando si configura il punto di aggiornamento software in un sito.  

|Sito|Opzioni dell'origine di sincronizzazione disponibili|  
|----------|----------------------------------------------|  
|- Sito di amministrazione centrale<br />- Sito primario autonomo|- Sincronizza dal sito Web Microsoft Update<br />- Sincronizza da un percorso di origine dati upstream<br />- Non eseguire la sincronizzazione da Microsoft Update o origine dati upstream|  
|- Punti di aggiornamento software aggiuntivi in un sito<br />- Sito primario figlio<br />- Sito secondario|- Sincronizza da un percorso di origine dati upstream|  

 Nell'elenco seguente vengono fornite ulteriori informazioni su ciascuna opzione utilizzabile come origine di sincronizzazione:  

-   **Sincronizza da Microsoft Update**: Utilizzare questa impostazione per sincronizzare i metadati degli aggiornamenti software da Microsoft Update. Il sito di amministrazione centrale deve avere accesso a Internet; in caso contrario, la sincronizzazione avrà esito negativo. Questa impostazione è disponibile solo quando si configura il punto di aggiornamento software nel sito di livello superiore.  

    > [!NOTE]  
    >  Se è presente un firewall tra il punto di aggiornamento software e Internet, potrebbe essere necessario configurarlo per accettare le porte HTTP e HTTPS usate per il sito Web WSUS. È inoltre possibile limitare l'accesso al firewall a determinati domini. Per altre informazioni sulla pianificazione di un firewall che supporta aggiornamenti software, vedere [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **<a name="BKMK_wsussync"></a>Sincronizza da un percorso di origine dati upstream**: utilizzare questa impostazione per sincronizzare i metadati degli aggiornamenti software dall'origine sincronizzazione upstream. I siti primari figlio e i siti secondari vengono configurati automaticamente per l'utilizzo dell'URL del sito padre per questa impostazione. È possibile sincronizzare gli aggiornamenti software da un server WSUS esistente. Specificare un URL, ad esempio `https://WSUSServer:8531`, dove 8531 è la porta usata per connettersi al server WSUS.  

-   **Non eseguire la sincronizzazione da Microsoft Update o origine dati upstream**: utilizzare questa impostazione per sincronizzare manualmente gli aggiornamenti software quando il punto di aggiornamento software nel sito di livello superiore viene disconnesso da Internet. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Se è presente un firewall tra il punto di aggiornamento software e Internet, potrebbe essere necessario configurarlo per accettare le porte HTTP e HTTPS usate per il sito Web WSUS. È inoltre possibile limitare l'accesso al firewall a determinati domini. Per altre informazioni sulla pianificazione di un firewall che supporta aggiornamenti software, vedere [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Nella pagina **Origine di sincronizzazione** della procedura guidata oppure nella scheda **Impostazioni di sincronizzazione** in Proprietà del componente del punto di aggiornamento software è anche possibile scegliere se creare eventi di reporting WSUS. Configuration Manager non usa tali eventi. Pertanto, in genere si sceglie l'impostazione predefinita **Non creare eventi di reporting WSUS**.  

## <a name="synchronization-schedule"></a>Pianificazione della sincronizzazione  
 Configurare la pianificazione della sincronizzazione nella pagina **Pianificazione della sincronizzazione** della procedura guidata o in Proprietà del componente del punto di aggiornamento software. Questa impostazione viene configurata solo nel punto di aggiornamento software nel sito di livello superiore.  

 Se si abilita la pianificazione, è possibile configurare una pianificazione della sincronizzazione semplice ricorrente o personalizzata. Quando si configura una pianificazione semplice, l'ora di avvio corrisponde all'ora locale del computer in cui è in esecuzione la console di Configuration Manager al momento della creazione della pianificazione. La configurazione dell'ora di avvio per una pianificazione personalizzata si basa sull'ora locale del computer in cui è in esecuzione la console di Configuration Manager.  

> [!TIP]  
>  Pianificare la sincronizzazione degli aggiornamenti software da eseguire usando un intervallo di tempo appropriato per l'ambiente. Un tipico scenario è quello che prevede di impostare l'esecuzione della pianificazione della sincronizzazione degli aggiornamenti poco dopo il normale rilascio di aggiornamenti della protezione Microsoft il secondo martedì di ogni mese, noto come Patch martedì. Un altro scenario frequente prevede di impostare l'esecuzione giornaliera della pianificazione della sincronizzazione degli aggiornamenti software quando si utilizzano tali aggiornamenti per fornire aggiornamenti del motore e delle definizioni di Endpoint Protection.  

> [!NOTE]  
>  Quando si sceglie di non abilitare la sincronizzazione degli aggiornamenti software su una pianificazione, è possibile sincronizzare manualmente tali aggiornamenti dal nodo **Tutti gli aggiornamenti software** o **Gruppi di aggiornamenti software** nell'area di lavoro Raccolta software. Per altre informazioni, vedere [Synchronize software updates from a disconnected software update point](synchronize-software-updates.md) (Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso).  

## <a name="supersedence-rules"></a>Regole di sostituzione  
 Configurare le impostazioni di sostituzione nella pagina **Regole di sostituzione** della procedura guidata o nella scheda **Regole di sostituzione** in Proprietà del componente del punto di aggiornamento software. È possibile configurare le regole di sostituzione solo nel sito di livello superiore. A partire dalla versione 1810 è possibile specificare il comportamento delle regole di sostituzione per gli **aggiornamenti delle funzionalità** separatamente dagli **aggiornamenti non delle funzionalità**. <!--3098809, 2977644-->

 In questa pagina è possibile specificare di applicare immediatamente la scadenza agli aggiornamenti software sostituiti, impedendo in tal modo che siano inclusi nelle nuove distribuzioni e contrassegnando le distribuzioni esistenti per indicare che gli aggiornamenti software sostituiti contengono uno o più aggiornamenti scaduti. In alternativa, è possibile specificare un periodo di tempo prima della scadenza degli aggiornamenti software sostituiti, che consente di continuare a distribuirli. Per altre informazioni, vedere [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  La pagina **Regole di sostituzione** della procedura guidata è disponibile solo quando si configura il primo punto di aggiornamento software nel sito. Questa pagina non viene visualizzata quando si installano punti di aggiornamento software aggiuntivi.  

## <a name="classifications"></a>Classificazioni  
 Configurare le impostazioni delle classificazioni nella pagina **Classificazioni** della procedura guidata o nella scheda **Classificazioni** in Proprietà del componente del punto di aggiornamento software. Per altre informazioni sulle classificazioni degli aggiornamenti software, vedere [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  La pagina **Classificazioni** della procedura guidata è disponibile solo quando si configura il primo punto di aggiornamento software nel sito. Questa pagina non viene visualizzata quando si installano punti di aggiornamento software aggiuntivi.  

> [!TIP]  
>  Durante la prima installazione del punto di aggiornamento software nel sito di livello superiore, cancellare tutte le classificazioni degli aggiornamenti software. Dopo la sincronizzazione iniziale degli aggiornamenti software, configurare le classificazioni da un elenco aggiornato e quindi riavviare la sincronizzazione. Questa impostazione viene configurata solo nel punto di aggiornamento software nel sito di livello superiore.  

## <a name="products"></a>Prodotti  
 Configurare le impostazioni dei prodotti nella pagina **Prodotti** della procedura guidata o nella scheda **Prodotti** in Proprietà del componente del punto di aggiornamento software.  

> [!NOTE]  
>  La pagina **Prodotti** della procedura guidata è disponibile solo quando si configura il primo punto di aggiornamento software nel sito. Questa pagina non viene visualizzata quando si installano punti di aggiornamento software aggiuntivi.  

> [!TIP]  
>  Durante la prima installazione del punto di aggiornamento software nel sito di livello superiore, deselezionare tutti i prodotti. Dopo la sincronizzazione iniziale degli aggiornamenti software, configurare i prodotti da un elenco aggiornato e quindi riavviare la sincronizzazione. Questa impostazione viene configurata solo nel punto di aggiornamento software nel sito di livello superiore.  

## <a name="languages"></a>Lingue  
 Configurare le impostazioni delle lingue nella pagina **Lingue** della procedura guidata o nella scheda **Lingue** in Proprietà del componente del punto di aggiornamento software. Specificare le lingue per cui si desidera sincronizzare i file di aggiornamento software e i dettagli di riepilogo. L'impostazione **File di aggiornamento software** è configurata in ogni punto di aggiornamento software della gerarchia di Configuration Manager. Le impostazioni **Dettagli di riepilogo** sono configurate solo nel punto di aggiornamento software di livello superiore. Per ulteriori informazioni, vedere [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  La pagina **Lingue** della procedura guidata è disponibile solo quando si installa il punto di aggiornamento software nel sito di amministrazione centrale. È possibile configurare le lingue del File di aggiornamento software nei siti figlio dalla scheda **Lingue** in Proprietà del componente del punto di aggiornamento software.  

## <a name="third-party-updates"></a>Aggiornamenti di terze parti
A partire da Configuration Manager versione 1802, è possibile abilitare gli aggiornamenti di terze parti per i client di Configuration Manager. Quando si abilitano gli aggiornamenti software di terze parti nelle proprietà del componente del punto di aggiornamento software, quest'ultimo scaricherà il certificato di firma usato da WSUS per gli aggiornamenti di terze parti. Questa opzione non è disponibile durante l'installazione del punto di aggiornamento software e deve essere configurata dopo l'installazione. Per abilitare le impostazioni client per gli aggiornamenti di terze parti, vedere l'articolo [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates).

## <a name="next-steps"></a>Passaggi successivi
Il punto di aggiornamento software è stato installato dal sito più in alto della gerarchia di Configuration Manager. Ripetere le procedure descritte in questo articolo per installare il punto di aggiornamento software nei siti figlio.

Dopo aver installato i punti di aggiornamento software, passare a [sincronizzare gli aggiornamenti software](synchronize-software-updates.md).
