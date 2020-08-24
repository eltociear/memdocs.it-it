---
title: Connettere Configuration Manager
titleSuffix: Configuration Manager
description: Guida pratica per la connessione di Configuration Manager a Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7015ab4c180ed56b00149ffbff99c9e5a8112e95
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126002"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Come connettere Configuration Manager a Desktop Analytics

Desktop Analytics è strettamente integrato con Configuration Manager. Assicurarsi innanzitutto che il sito sia aggiornato per supportare le funzionalità più recenti. Creare quindi la connessione a Desktop Analytics in Configuration Manager. Infine, monitorare l'integrità della connessione.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a> Aggiornare il sito

Assicurarsi prima di tutto che il sito di Configuration Manager esegua almeno la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](../core/servers/manage/install-in-console-updates.md).

È anche necessario installare l'aggiornamento cumulativo versione 1902 (4500571) per supportare l'integrazione con Desktop Analytics. Per altre informazioni su questo aggiornamento, vedere [Aggiornamento cumulativo per Configuration Manager Current Branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](../core/servers/manage/install-in-console-updates.md).

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a> Connettersi al servizio

> [!TIP]
> Prima di avviare la procedura guidata, creare la raccolta di destinazione menzionata nel passaggio 8, poiché non è possibile effettuare selezioni al di fuori della procedura guidata dopo averla avviata.

Usare questa procedura per connettere Configuration Manager a Desktop Analytics e configurare le impostazioni del dispositivo. Questa procedura è un processo singolo per l'associazione della gerarchia al servizio cloud.

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.

    > [!TIP]
    > Connettersi al servizio direttamente dal nodo **Manutenzione di Desktop Analytics**. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software** e selezionare il nodo **Manutenzione di Desktop Analytics**. Nella casella *Nuovo utente di Desktop Analytics?* selezionare il secondo collegamento *Connettere Configuration Manager al servizio Desktop Analytics*.

2. Nella pagina **Servizi di Azure** della Procedura guidata per i servizi di Azure configurare le impostazioni seguenti:

    - Specificare un **Nome** per l'oggetto in Configuration Manager.

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili.

   Selezionare **Avanti**.

3. Nella pagina **App** selezionare l'**Ambiente di Azure** appropriato. Quindi selezionare **Sfoglia** per l'app Web.

4. Se è disponibile un'app che si vuole riutilizzare per questo servizio, selezionarla dall'elenco e selezionare **OK**.

5. Nella maggior parte dei casi è possibile creare un'app per la connessione a Desktop Analytics con questa procedura guidata. Selezionare **Crea**.<!-- 3572123 -->

    > [!TIP]
    > Se non è possibile creare l'app da questa procedura guidata, è possibile creare manualmente l'app in Azure AD e quindi importarla in Configuration Manager. Per altre informazioni, vedere [Creare e importare app per Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. Configurare le impostazioni seguenti nella finestra **Crea un'applicazione server**:

    - **Nome applicazione**: nome descrittivo per l'app in Azure AD.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.

    Selezionare **Accedi**. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.

    > [!NOTE]
    > Completare questo passaggio come **Amministratore globale**. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo App server selezionare **OK**. Selezionare **Avanti** nella pagina App della Procedura guidata per i servizi di Azure.

7. Nella pagina **Dati di diagnostica** configurare le impostazioni seguenti:

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione. In caso contrario, assicurarsi che il server proxy sia configurato in modo da consentire tutti gli [endpoint](enable-data-sharing.md#endpoints) necessari prima di continuare. In alternativa, recuperare manualmente l'ID commerciale dal [portale di Desktop Analytics](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Livello dei dati di diagnostica di Windows 10**: selezionare almeno **Obbligatorio**. Per altre informazioni, vedere [Livelli dei dati di diagnostica](enable-data-sharing.md#diagnostic-data-levels).

        > [!TIP]
        > In Configuration Manager versione 2002 e precedenti, questo valore era chiamato **Base**.<!-- 7363467 -->

    - **Consenti il nome del dispositivo nei dati di diagnostica**: selezionare **Abilita**

        > [!NOTE]
        > A partire da Windows 10 versione 1803, il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se non si invia il nome del dispositivo, il dispositivo viene visualizzato in Desktop Analytics come "Sconosciuto". Questo comportamento può rendere difficile l'identificazione e la valutazione dei dispositivi.

   Selezionare **Avanti**. La pagina **Funzionalità disponibile** mostra la funzionalità Desktop Analytics disponibile con le impostazioni dei dati di diagnostica della pagina precedente. Selezionare **Avanti** per continuare o **Precedente** per apportare modifiche.

    ![Pagina Funzionalità disponibile di esempio nella Procedura guidata per i servizi di Azure](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. Nella pagina **Raccolte** configurare le impostazioni seguenti:

    - **Nome visualizzato**: Il portale di Desktop Analytics visualizza questa connessione a Configuration Manager usando questo nome. Usarlo per differenziare le diverse gerarchie e per identificare le collezioni da gerarchie separate. Usare i termini per distinguere facilmente più gerarchie nel proprio ambiente, ad esempio: *test lab* o *produzione*.

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager connette al servizio Desktop Analytics.

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**.

    - **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**: Selezionare **Aggiungi** per inserire ulteriori raccolte della gerarchia **Raccolta di destinazione**. Queste raccolte sono disponibili nel portale di Desktop Analytics per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte pilota e di esclusioni pilota.  <!-- 4097528 -->

        > [!TIP]
        > La finestra Seleziona raccolte visualizza solo le raccolte limitate dalla **Raccolta di destinazione**.
        >
        > Nell'esempio seguente si seleziona CollectionA come raccolta di destinazione. Quando si aggiungono altre raccolte, vengono visualizzate CollectionA, CollectionB e CollectionC. Non è possibile aggiungere CollectionD.
        >
        > - CollectionA: limitata dalla raccolta **Tutti i sistemi**
        >     - CollectionB: limitata da CollectionA
        >         - CollectionC: limitata da CollectionB
        > - CollectionD: limitata dalla raccolta **Tutti i sistemi**
        >
        > Per gestire le raccolte disponibili nel portale di Desktop Analytics per il raggruppamento con i piani di distribuzione, nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare la voce associata al servizio di Azure **Desktop Analytics** e aggiornare le impostazioni nella pagina **Desktop Analytics Collection** (Raccolta di Desktop Analytics).

        > [!IMPORTANT]
        > Queste raccolte continuano a essere sincronizzate quando viene modificata l'appartenenza. La raccolta di destinazione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, i dispositivi escono dalla raccolta e da Desktop Analytics.

9. Completare la procedura guidata.

Configuration Manager crea criteri di impostazioni per configurare i dispositivi nella raccolta di destinazione. Questi criteri includono le impostazioni dei dati di diagnostica per abilitare i dispositivi all'invio di dati a Microsoft. Per impostazione predefinita, i client aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere necessario attendere diverse ore prima che i dati siano disponibili in Desktop Analytics.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a> Monitorare l'integrità della connessione

Monitorare la configurazione dei dispositivi per Desktop Analytics. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere il nodo **Manutenzione di Desktop Analytics** e selezionare il dashboard **Integrità connessione**.

Per altre informazioni, vedere [Monitorare l'integrità della connessione](monitor-connection-health.md).

Configuration Manager sincronizza le raccolte entro 60 minuti dalla creazione della connessione. Nel portale di Desktop Analytics passare a **Pilota globale** e visualizzare le raccolte di dispositivi di Configuration Manager.

> [!NOTE]
> La connessione di Configuration Manager a Desktop Analytics si basa sul punto di connessione del servizio. Eventuali modifiche apportate a questo ruolo del sistema del sito possono avere effetto sulla sincronizzazione con il servizio cloud. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per registrare i dispositivi in Desktop Analytics.
> [!div class="nextstepaction"]
> [Registrare i dispositivi](enroll-devices.md)
