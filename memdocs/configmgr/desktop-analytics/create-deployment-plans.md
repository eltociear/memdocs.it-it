---
title: Come creare i piani di distribuzione
titleSuffix: Configuration Manager
description: Guida pratica per la creazione di piani di distribuzione in Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c42576f35d285fc7285466c4208d7ccaf370daa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708299"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Come creare i piani di distribuzione in Desktop Analytics

Questo articolo illustra la procedura per creare un piano di distribuzione in Desktop Analytics. Prima di iniziare, leggere le [informazioni sui piani di distribuzione](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Creare un piano per Windows 10

Seguire la procedura descritta in questa sezione per usare Desktop Analytics per creare un piano di distribuzione per Windows 10.

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics). Usare credenziali con almeno le autorizzazioni **Collaboratori dell'area di lavoro**.  

2. Selezionare **Piani di distribuzione** nel gruppo Gestisci.  

3. Nel riquadro **Piani di distribuzione** selezionare **Crea**.  

4. Nella riquadro **Crea piano di distribuzione** configurare le impostazioni seguenti:  

    - **Nome**: nome univoco per il piano di distribuzione  

    - **Prodotti e versioni**: scegliere la versione di Windows 10 da distribuire. Microsoft consiglia di creare piani di distribuzione che usano la versione più recente.  

    - **Gruppi di dispositivi**: selezionare uno o più gruppi dalla stessa gerarchia. Questi gruppi sono [raccolte di dispositivi](connect-configmgr.md#bkmk_Collections) sincronizzate da Configuration Manager.

        Se si connettono più gerarchie di Configuration Manager alla stessa istanza di Desktop Analytics, viene aggiunto un nome visualizzato per la gerarchia come prefisso al nome della raccolta nella configurazione pilota globale. Si tratta della proprietà **Nome visualizzato** nella connessione di Desktop Analytics nella console di Configuration Manager.<!-- 4814075 -->

        > [!NOTE]
        > Il supporto di più gerarchie richiede Configuration Manager versione 1910 o successiva.
        >
        > Se si selezionano raccolte per più gerarchie, nel portale viene visualizzato un avviso. Non è possibile creare il piano di distribuzione con raccolte da più gerarchie.<!-- 4814075 -->

    - **Regole di idoneità**: queste regole consentono di individuare i dispositivi idonei per l'aggiornamento. Per altre informazioni, vedere [Regole di idoneità](#readiness-rules).  

    - **Data completamento**: scegliere la data entro cui Windows deve essere completamente distribuito in tutti i dispositivi di destinazione.  

5. Selezionare **Crea**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione durante l'elaborazione. Per velocizzare l'elaborazione, richiedere un aggiornamento dati su richiesta. Per altre informazioni, vedere [Domande frequenti su Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Aprire il piano di distribuzione selezionandone il nome.  

7. Nel menu del piano di distribuzione nel gruppo **Preparazione** selezionare **Identificazione dell'importanza**.  

    1. Nella scheda **App** selezionare l'opzione per visualizzare solo le risorse **Non riviste**.  

    2. Selezionare ogni app, quindi selezionare **Modifica**. È possibile selezionare più app da modificare contemporaneamente.  

    3. Scegliere un livello di importanza dall'elenco **Importanza**. Se si vuole che l'app venga convalidata da Desktop Analytics durante il progetto pilota, selezionare **Critica** o **Importante**. Non viene eseguita la convalida delle app contrassegnate come **Non importante**. Quando si assegnano i livelli di importanza, valutare la [compatibilità](compat-assessment.md) e altre informazioni dettagliate sui piani.  

        Quando si assegnano i livelli di importanza è anche possibile scegliere la decisione di aggiornamento.  

    4. Al termine, selezionare **Salva**.  

8. Nel menu del piano di distribuzione nel gruppo **Preparazione** selezionare **Identifica gruppo pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e scegliere **Aggiungi al gruppo pilota**. Se non si è d'accordo con quanto consigliato, selezionare **Sostituisci**.  

        Per altre informazioni sui consigli di Desktop Analytics, selezionare l'icona Informazioni nell'angolo superiore destro del riquadro **Identifica gruppo pilota**.

## <a name="readiness-rules"></a>Regole di idoneità

Queste regole consentono di individuare i dispositivi idonei per l'aggiornamento sul posto. È possibile impostare queste regole quando si crea il piano di distribuzione o modificarle in un secondo momento.

Per modificare le regole di idoneità:

1. Nel portale di Desktop Analytics selezionare il piano di distribuzione.
1. Accanto al nome selezionare **Modifica**.
1. Selezionare **Regole di idoneità**.
1. Selezionare **Sistema operativo Windows**.
1. Apportare le modifiche necessarie e selezionare **Salva**.

Per aggiornamenti del **Sistema operativo Windows**, sono disponibili due regole: driver di dispositivo e applicazioni Windows.

### <a name="device-drivers"></a>Driver di dispositivo

Configurare se i dispositivi ricevono i driver da Windows Update. Per impostazione predefinita, questo valore è impostato su **Disattivata**. Abilitare questa regola quando si usa Windows Update per le aziende per gestire gli aggiornamenti, inclusi i driver. Se si usa Configuration Manager per gestire gli aggiornamenti software, impostare questa regola su **Disattivata**.

### <a name="windows-applications"></a>Applicazioni Windows

Le app ritenute *importanti* da Desktop Analytics si basano sulla soglia del numero di installazioni basso. Impostare questa soglia nelle regole di idoneità per il piano di distribuzione. Per impostazione predefinita, questa soglia è **2.0%** . È possibile modificare il valore da `0.0` a `10.0`.


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per eseguire la distribuzione nei dispositivi pilota.
> [!div class="nextstepaction"]  
> [Distribuire nel progetto pilota](deploy-pilot.md)  
