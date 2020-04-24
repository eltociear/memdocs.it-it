---
title: Configurare gli avvisi di Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come configurare gli avvisi di Endpoint Protection in Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074861"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurare gli avvisi di Endpoint Protection in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 È possibile configurare gli avvisi di Endpoint Protection in Microsoft Configuration Manager per notificare agli utenti amministratori se si verificano eventi specifici nella gerarchia, ad esempio un'infezione da malware. Le notifiche vengono visualizzate nel dashboard di Endpoint Protection della console di Configuration Manager nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** o possono essere inviate tramite posta elettronica agli utenti specificati.

 Seguire i passaggi e le procedure supplementari seguenti di questo argomento per configurare gli avvisi per Endpoint Protection in Configuration Manager.

> [!IMPORTANT]
>  Per configurare gli avvisi per Endpoint Protection, è necessario avere l'autorizzazione **Applicazione protezione** per le raccolte.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Procedura per configurare gli avvisi per Endpoint Protection in Configuration Manager

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.

3.  Nell'elenco **Raccolte dispositivi** selezionare la raccolta per cui configurare gli avvisi e quindi nel gruppo **Proprietà** della scheda **Home** fare clic su **Proprietà**.

    > [!NOTE]
    >  Non è possibile configurare avvisi per raccolte di utenti.

4.  Nella scheda **Avvisi** della finestra di dialogo **Proprietà** _<Nome raccolta\>_ selezionare **Visualizza questa raccolta nel dashboard di Endpoint Protection** se si vogliono visualizzare i dettagli sulle operazioni antimalware per la raccolta nell'area di lavoro **Monitoraggio** della console di Configuration Manager.

    > [!NOTE]
    >  Questa opzione non è disponibile per la raccolta **Tutti i sistemi** .

5.  Nella scheda **Avvisi** della finestra di dialogo **Proprietà** _\>Nome raccolta_ fare clic su **Aggiungi**.

6.  Nella sezione **Genera un avviso quando si applicano queste condizioni** della finestra di dialogo **Aggiungi avvisi nuova raccolta**, selezionare gli avvisi che devono essere generati da Configuration Manager se si verificano gli eventi di Endpoint Protection specificati e fare clic su **OK**.

7.  Nell'elenco  **Condizioni** della scheda **Avvisi** selezionare ogni avviso di Endpoint Protection e specificare le informazioni seguenti:

    -   **Nome avviso**: accettare il nome predefinito o immettere un nome nuovo per l'avviso.

    -   **Gravità avviso**: selezionare nell'elenco il livello di avviso da visualizzare nella console di Configuration Manager.

8.  A seconda dell'avviso selezionato, specificare le informazioni aggiuntive seguenti:

    -   **Rilevamento malware**: questo avviso viene generato se viene rilevato un malware in un computer della raccolta monitorata. **Soglia di rilevamento malware**: specifica i livelli di rilevamento di malware in base al quale viene generato questo avviso:

        -   **Alto - Tutti i rilevamenti**: l'avviso viene generato quando ci sono uno o più computer nella raccolta specificata in cui viene rilevato malware, indipendentemente dall'azione eseguita dal client di Endpoint Protection.

        -   **Medio - Rilevato, azione in sospeso**: l'avviso viene generato quando ci sono uno o più computer nella raccolta specificata in cui viene rilevato malware ed è necessario rimuovere il malware manualmente.

        -   **Basso - Rilevato, ancora attivo**: l'avviso viene generato quando ci sono uno o più computer nella raccolta specificata in cui viene rilevato malware ancora attivo.

    -   **Attacco malware**: questo avviso viene generato se viene rilevato malware specificato su una percentuale determinata di computer nella raccolta monitorata.

        -   **Percentuale di computer con rilevamento malware**: l'avviso viene generato quando la percentuale di computer della raccolta in cui viene rilevato malware supera la percentuale specificata. Specificare una percentuale compresa tra **1** e **99**.

            > [!NOTE]
            >  Il valore di percentuale è basato sul numero di computer nella raccolta, ma esclude i computer in cui non è installato un client di Configuration Manager. Include i computer in cui non è ancora installato il client di Endpoint Protection.

    -   **Rilevamento malware ripetuto**: questo avviso viene generato se viene rilevato un malware specifico un numero di volte superiore al numero specificato durante il numero di ore nei computer della raccolta monitorata. Per configurare questo avviso, specificare le informazioni seguenti:

        -   **Numero di rilevamenti malware** : l'avviso viene generato quando lo stesso malware viene rilevato nei computer nella raccolta per un numero di volte maggiore di quello specificato. Specificare un numero compreso tra **2** e **32**.

        -   **Intervallo per rilevamento (ore):** specificare l'intervallo di rilevamento (in ore) in cui deve essere raggiunto il numero di rilevamenti di malware. Specificare un numero compreso tra **1** e **168**.

    -   **Rilevamento di più malware**: questo avviso viene generato se più di un numero specificato di tipi di malware viene rilevato durante un numero determinato di ore nei computer della raccolta monitorata. Per configurare questo avviso, specificare le informazioni seguenti:

        -   **Numero di tipi di malware rilevato:** l'avviso viene generato quando viene rilevato il numero specificato di tipi diversi di malware nei computer nella raccolta. Specificare un numero compreso tra **2** e **32**.

        -   **Intervallo per rilevamento (ore):** specificare l'intervallo di rilevamento (in ore) in cui deve essere raggiunto il numero di rilevamenti di malware. Specificare un numero compreso tra **1** e **168**.

9. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà** _\>Nome raccolta_.  

## <a name="alert-for-outdated-malware-client"></a>Avviso per client malware obsoleto

A partire da Configuration Manager versione 1702, è possibile configurare un avviso per verificare che i client Endpoint Protection non siano obsoleti. Da qualsiasi raccolta di dispositivi è ora possibile aggiungere colonne all'elenco per gli attributi seguenti **Versione client antimalware** e **Stato distribuzione di Endpoint Protection**. Ad esempio, nella console passare ad **Asset e conformità** > **Panoramica** > **Raccolte dispositivi** > **Tutti i client desktop e di server**. Fare doppio clic sull'intestazione di colonna e selezionare le colonne da aggiungere. Per controllare un avviso, visualizzare **Avvisi** nell'area di lavoro **Monitoraggio**. Se più del 20% dei client gestiti esegue una versione scaduta del software antimalware, viene visualizzato l'avviso La versione del client antimalware è obsoleta. Questo avviso non viene visualizzato nella scheda **Monitoraggio** > **Panoramica**. Per aggiornare i client antimalware scaduti, abilitare gli aggiornamenti software per i client antimalware.

Per configurare la percentuale oltre la quale viene generato l'avviso, espandere **Monitoraggio** > **Avvisi** > **Tutti gli avvisi**, fare doppio clic su **I client antimalware sono obsoleti** e modificare l'opzione **Genera un avviso se la percentuale di client gestiti con una versione obsoleta del client antimalware è superiore a**.

> [!div class="button"]
> [Passaggio successivo >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Indietro >](endpoint-protection-site-role.md)
