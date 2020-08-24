---
title: Dashboard di Gestione client di Office 365
titleSuffix: Configuration Manager
description: Esaminare le informazioni sul client Microsoft 365 Apps dal dashboard di Gestione client di Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: bae995b0704e2b2774d5f002cbf907777a3edcf0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697042"
---
# <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365

*Si applica a: Configuration Manager (Current Branch)*

> [!Note]
> A partire dal 21 aprile 2020, Office 365 ProPlus viene rinominato come **App di Microsoft 365 per grandi imprese**. Per altre informazioni, vedere [Modifica del nome di Office 365 ProPlus](/deployoffice/name-change). È comunque possibile che vengano ancora visualizzati riferimenti al nome precedente nella console di Configuration Manager e nella documentazione di supporto mentre la console viene aggiornata.

A partire da Configuration Manager versione 1802, è possibile esaminare le informazioni sul client Microsoft 365 Apps dal dashboard di Gestione client di Office 365. Il dashboard di Gestione client di Office 365 visualizza un elenco di dispositivi rilevanti quando vengono selezionate le sezioni del grafico. <!--1357281 -->

## <a name="prerequisites"></a>Prerequisiti

### <a name="enable-hardware-inventory"></a>Abilitare l'inventario hardware

I dati visualizzati nel dashboard di gestione client di Office 365 provengono dall'inventario hardware. Abilitare l'inventario hardware e selezionare la classe **Configurazioni di Office 365 ProPlus** di tale inventario per visualizzare i dati nel dashboard.
 
1. Abilitare l'inventario hardware, se non è ancora stato fatto. Per altri dettagli, vedere [Configurare l'inventario hardware](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. Nella console di Configuration Manager passare a **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  
3. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  
4. Nel **Impostazioni Client predefinite** nella finestra di dialogo fare clic su **l'inventario Hardware**.  
5. Nel **le impostazioni del dispositivo** elenco, fare clic su **Imposta classi**.  
6. Nella finestra di dialogo **Classi di inventario hardware** selezionare **Office 365 ProPlus Configurations**.  
7. Fare clic su **OK** per salvare le modifiche e chiudere il **classi di inventario Hardware** nella finestra di dialogo.

Il dashboard di Gestione client di Office 365 inizia a visualizzare i dati in base all'inventario hardware.

### <a name="connectivity-for-top-level-site-server"></a>Connettività per il server del sito di livello superiore

*(Prerequisito introdotto nella versione 1906)*

Il server del sito di livello superiore deve accedere all'endpoint seguente per scaricare il file di conformità:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> La connettività Internet non è necessaria per i dispositivi client per questi scenari.

### <a name="enable-data-collection-for-microsoft-365-apps"></a>Abilitare la raccolta dati per Microsoft 365 Apps

*(Prerequisito introdotto nella versione 1910)*

A partire dalla versione 1910, sarà necessario abilitare la raccolta dati per Microsoft 365 Apps per popolare le informazioni nel **dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus**. I dati vengono archiviati nel database del sito di Configuration Manager e non vengono inviati a Microsoft.

Questi dati sono diversi dai dati di diagnostica, descritti in [Dati di diagnostica inviati da Microsoft 365 Apps a Microsoft](/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft).

È possibile abilitare la raccolta dati usando Criteri di gruppo o modificando il Registro di sistema.

#### <a name="enable-data-collection-from-group-policy"></a>Abilitare la raccolta dati da Criteri di gruppo

1. Scaricare i [file del modello amministrativo più recenti dall'Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=49030).
2. Abilitare l'impostazione di criteri **Attiva la raccolta dati di telemetria** in `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard`.
    - In alternativa, applicare l'impostazione di criteri con il [servizio criteri cloud di Office](/DeployOffice/overview-office-cloud-policy-service).
    - L'impostazione di criteri viene usata anche dal dashboard di telemetria di Office, che non è necessario distribuire per questa raccolta dati.

#### <a name="enable-data-collection-from-the-registry"></a>Abilitare la raccolta dati dal Registro di sistema

Il comando seguente è un esempio di come abilitare la raccolta dati dal Registro di sistema:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visualizzazione del dashboard di Gestione client di Office 365

Per visualizzare il dashboard di Gestione client di Office 365, nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Gestione client di Office 365**. Nella parte superiore del dashboard, usare l'impostazione a discesa **Raccolta** per filtrare i dati del dashboard in base ai membri di una raccolta specifica. A partire da Configuration Manager versione 1802, il dashboard visualizza un elenco di dispositivi pertinenti quando vengono selezionate le sezioni del grafico.

Il dashboard di Gestione client di Office 365 presenta sotto forma di grafico le informazioni seguenti:

- Numero di client di Microsoft 365 Apps
- Versioni del client di Microsoft 365 Apps
- Lingue del client di Microsoft 365 Apps
- Canali del client di Microsoft 365 Apps Per altre informazioni, vedere [Panoramica dei canali di aggiornamento per Microsoft 365 Apps](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-microsoft-365-apps-readiness"></a><a name="bkmk_o365_readiness"></a> Integrazione per la conformità di Microsoft 365 Apps
<!--3735402-->
A partire da Configuration Manager versione 1902, è possibile usare il dashboard per identificare in modo attendibile i dispositivi pronti per l'aggiornamento a Microsoft 365 Apps. Questa integrazione offre informazioni dettagliate sui problemi di compatibilità potenziali con i componenti aggiuntivi e le macro nell'ambiente. Quindi è possibile usare Configuration Manager per distribuire Microsoft 365 Apps nei dispositivi pronti.

Il dashboard di Gestione client di Office 365 include un nuovo riquadro, **Preparazione aggiornamenti di Office 365 ProPlus**. Questo riquadro è un grafico a barre dei dispositivi negli stati seguenti:
- Valutazione non eseguita
- Pronto per l'aggiornamento
- Revisione necessaria

Selezionare uno stato per eseguire il drill-through a un elenco di dispositivi. Questo report di conformità visualizza altri dettagli sui dispositivi. Include colonne per lo stato di compatibilità di componenti aggiuntivi e macro.

### <a name="prerequisites-for-microsoft-365-apps-readiness-integration"></a>Prerequisiti per l'integrazione con la conformità di Microsoft 365 Apps

- Attivare l'inventario hardware nelle impostazioni client. Per altre informazioni, vedere la sezione [Prerequisiti](#prerequisites).  

- Il dispositivo richiede la connettività alla rete per la distribuzione di contenuti (CDN, Content Delivery Network) di Office per scaricare un file di conformità dei componenti aggiuntivi. Per altre informazioni, vedere [Reti per la distribuzione di contenuti](/office365/enterprise/content-delivery-networks). Se il dispositivo non riesce a scaricare questo file, lo stato dei componenti aggiuntivi è *Revisione necessaria*.  

    > [!Note]  
    > Per questa funzionalità non viene inviato nessun dato a Microsoft.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a> Conformità dettagliata per le macro

Per impostazione predefinita l'agente di analisi esamina l'elenco dei file usati di recente (MRU) in ogni dispositivo. Quindi conteggia i file di questo elenco che supportano le macro. I file possono essere dei tipi seguenti:
- Formati di file Office con attivazione macro, quali cartelle di lavoro di Excel con attivazione macro (file con estensione xlsm) o documenti di Word con attivazione macro (file con estensione docm)  
- Formati di Office meno recenti che non indicano se è presente contenuto con macro. Ad esempio una cartella di lavoro di Excel 97-2003 (file con estensione xls).

Se sono necessarie informazioni più dettagliate sulla compatibilità delle macro, distribuire **Readiness Toolkit per Office** per analizzare il codice all'interno dei file di macro. Controlla se sono presenti potenziali problemi di compatibilità. Ad esempio, il file potrebbe usare una funzione che è stata modificata in una versione più recente di Office. Dopo aver eseguito Readiness Toolkit per Office e selezionato l'opzione per i **documenti di Office usati più di recente e i componenti aggiuntivi installati nel computer** oppure dopo aver usato il flag `-mru` nella riga di comando, i risultati possono essere prelevati dall'agente di inventario hardware di Configuration Manager. Questi dati aggiuntivi migliorano i calcoli di conformità dei dispositivi. Per altre informazioni, vedere [Valutare la compatibilità delle applicazioni per Microsoft 365 Apps tramite Readiness Toolkit](https://aka.ms/readinesstoolkit).

Si noti che non è necessario installare Readiness Toolkit in tutti i dispositivi di destinazione per eseguire l'analisi. Per analizzare ogni dispositivo desiderato, è possibile usare l'opzione della riga di comando di esempio riportata di seguito.  Il flag di output è obbligatorio, ma i file non verranno usati per generare i risultati nel dashboard, quindi è possibile selezionare qualsiasi percorso valido.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Per altre informazioni, vedere [Recupero di informazioni di disponibilità per più utenti di un'organizzazione](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="microsoft-365-apps-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a> Dashboard di conformità di Microsoft 365 Apps

*(Funzionalità introdotta nella versione 1906)*

<!--4021125-->
Per individuare i dispositivi pronti per l'aggiornamento a Microsoft 365 Apps, a partire dalla versione 1906 è disponibile un dashboard di conformità. Include il riquadro **Preparazione aggiornamenti di Office 365 ProPlus** rilasciato in Configuration Manager Current Branch versione 1902. I nuovi riquadri seguenti di questo dashboard consentono di valutare la conformità di componenti aggiuntivi e macro:

- Distribuzione
- Idoneità del dispositivo
- Idoneità dei componenti aggiuntivi
- Dichiarazioni di supporto dei componenti aggiuntivi
- Componenti aggiuntivi principali in base al numero di versione
- Number of devices that have macros (Numero di dispositivi con macro)
- Idoneità delle macro
- Avvisi di macro

Il video seguente è una sessione di Ignite 2019, che include altre informazioni:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Procedure consigliate per la valutazione della compatibilità e gli aggiornamenti per Microsoft Office 365 ProPlus usando Office Readiness in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-microsoft-365-apps-upgrade-readiness-dashboard"></a>Uso del dashboard Preparazione aggiornamenti di Microsoft 365 Apps

Dopo aver verificato i [prerequisiti](#prerequisites), usare le istruzioni seguenti per usare il dashboard:
 
1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** ed espandere **Gestione client di Office 365**.
1. Selezionare il nodo **Preparazione aggiornamenti di Microsoft 365 Apps**.
1. Modificare le opzioni **Raccolta** e **Target Office Architecture** (Architettura di Office di destinazione) per modificare le informazioni inoltrate nel dashboard.

[![Dashboard Preparazione aggiornamenti di Microsoft 365 Apps](./media/4021125-office-365-upgrade-readiness-dashboard.png)](./media/4021125-office-365-upgrade-readiness-dashboard.png#lightbox)

[![Componenti aggiuntivi del dashboard Preparazione aggiornamenti di Microsoft 365 Apps](./media/4021125-office-365-to-add-ins.png)](./media/4021125-office-365-to-add-ins.png#lightbox)

[![Avvisi di macro del dashboard Preparazione aggiornamenti di Microsoft 365 Apps](./media/4021125-office-365-macro-advisories.png)](./media/4021125-office-365-macro-advisories.png#lightbox)

### <a name="device-readiness-information"></a>Informazioni sulla conformità dei dispositivi

Dopo la valutazione dell'inventario dei componenti aggiuntivi e delle macro in ogni dispositivo, i dispositivi vengono raggruppati in base alle informazioni. I dispositivi con stato **Pronto per l'aggiornamento** non hanno probabilmente problemi di compatibilità.

Selezionando la categoria **Pronto per l'aggiornamento** nel grafico vengono visualizzati altri dettagli sui dispositivi nella raccolta di limitazione. È possibile esaminare l'elenco dei dispositivi, effettuare selezioni in base ai requisiti aziendali e creare una nuova raccolta di dispositivi dalla selezione. Usare la nuova raccolta per distribuire Microsoft 365 Apps con Configuration Manager.

I dispositivi che potrebbero essere a rischio di problemi di compatibilità sono contrassegnati come **Verifica necessaria**. Per questi dispositivi può essere necessario intervenire prima di aggiornarli a Microsoft 365 Apps. Ad esempio, è possibile aggiornare i componenti aggiuntivi critici a una versione più recente.

### <a name="add-in-information"></a>Informazioni sui componenti aggiuntivi

 In ogni dispositivo viene raccolto un inventario di tutti i componenti aggiuntivi installati. L'inventario viene poi confrontato con le informazioni disponibili presso Microsoft sulle prestazioni dei componenti aggiuntivi in Microsoft 365 Apps. Se viene individuato un componente aggiuntivo che è probabile che causi problemi dopo l'aggiornamento, tutti i dispositivi con il componente aggiuntivo vengono contrassegnati per la verifica.

### <a name="macro-information"></a>Informazioni sulle macro

Configuration Manager esamina i file usati più di recente in ogni dispositivo. Conta i file in questo elenco che supportano le macro, inclusi i tipi seguenti:

- Formati di file di Office abilitati per le macro.
- Formati di Office meno recenti che non indicano se è presente contenuto con macro.

Questo report può essere usato per identificare i dispositivi che hanno usato di recente file che possono contenere macro. È quindi possibile distribuire **Readiness Toolkit per Office** usando Configuration Manager per analizzare tutti i dispositivi in cui sono necessarie informazioni più dettagliate e verificare se esistono potenziali problemi di compatibilità. Ad esempio, se il file usa una funzione che è stata modificata in una versione più recente di Microsoft 365 Apps.

Per altre informazioni su come eseguire l'analisi, vedere [Conformità dettagliata per le macro](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a> Dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus
<!--4488272, 4488301-->
*(Funzionalità introdotta nella versione 1910)*

A partire dalla versione 1910, il **dashboard per l'integrità e la distribuzione pilota di Office 365 ProPlus** consente di pianificare e distribuire Microsoft 365 Apps o di eseguirne una distribuzione pilota. Il dashboard fornisce informazioni dettagliate sull'integrità per i dispositivi con Microsoft 365 Apps per identificare i possibili problemi che potrebbero influire sui piani di distribuzione. Il **dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus** fornisce raccomandazioni per i dispositivi della distribuzione pilota in base all'inventario dei componenti aggiuntivi. Il dashboard include i riquadri seguenti:

- Genera la distribuzione pilota
- Dispositivi della distribuzione pilota consigliati
- Distribuisci la raccolta pilota
- Dispositivi che inviano dati sull'integrità
- Dispositivi che non soddisfano gli obiettivi di integrità
- Componenti aggiuntivi che non soddisfano gli obiettivi di integrità
- Macro che non soddisfano gli obiettivi di integrità

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Uso del dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus

Dopo aver verificato i [prerequisiti](#prerequisites), usare le istruzioni seguenti per usare il dashboard:

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** ed espandere **Gestione client di Office 365**.
1. Selezionare il nodo **Office 365 Pilot and Health** (Integrità e distribuzione pilota di Office 365).

![Dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Genera la distribuzione pilota

È ora possibile generare una raccomandazione pilota da una raccolta di limitazione facendo semplicemente clic su un pulsante. Non appena viene avviata l'azione, un'attività in background inizia a calcolare la raccolta pilota. La raccolta di limitazione deve contenere almeno un dispositivo con una versione di Office che non sia ProPlus.

### <a name="recommended-pilot-devices"></a>Dispositivi della distribuzione pilota consigliati

I **dispositivi della distribuzione pilota consigliati** sono un set minimo di dispositivi che rappresentano tutti i componenti aggiuntivi installati nella raccolta di limitazione usata durante la generazione della distribuzione pilota. Eseguire il drill-down per ottenere un elenco di questi dispositivi. Usare quindi i dettagli per escludere eventuali dispositivi dalla distribuzione pilota, se necessario. Se tutti i componenti aggiuntivi sono già presenti nei dispositivi Microsoft 365 Apps, i dispositivi con tali componenti aggiuntivi non verranno inclusi nel calcolo. Ciò significa che è anche possibile che non si ottenga alcun risultato nella raccolta pilota perché tutti i componenti aggiuntivi sono presenti nei dispositivi in cui è installato Microsoft 365 Apps.

### <a name="deploy-pilot"></a>Distribuisci la raccolta pilota

Dopo aver accettato i dispositivi della distribuzione pilota, distribuire Microsoft 365 Apps nella raccolta pilota usando la distribuzione guidata in più fasi. Gli amministratori possono definire la raccolta pilota e di limitazione nella procedura guidata per gestire le distribuzioni.

### <a name="health-data"></a>Dati sull'integrità

Dopo l'installazione di Microsoft 365 Apps, abilitare i dati sull'integrità nei dispositivi della distribuzione pilota. I dati sull'integrità forniscono informazioni dettagliate su quali componenti aggiuntivi e macro non soddisfano gli obiettivi di integrità. Il grafico **Dispositivi pronti per la distribuzione** identifica i dispositivi non pilota pronti per la distribuzione usando le informazioni sull'integrità. È possibile ottenere un conteggio dei dispositivi che inviano dati sull'integrità dal grafico **Dispositivi che inviano dati sull'integrità**.

### <a name="devices-not-meeting-health-goals"></a>Dispositivi che non soddisfano gli obiettivi di integrità

Questo riquadro riepiloga i dispositivi che presentano problemi con componenti aggiuntivi, macro o entrambi.

### <a name="add-ins-not-meeting-health-goals"></a>Componenti aggiuntivi che non soddisfano gli obiettivi di integrità

- Errori di caricamento: non è stato possibile avviare il componente aggiuntivo.
- Arresti anomali del sistema: errore del componente aggiuntivo durante l'esecuzione.
- Errore: il componente aggiuntivo ha segnalato un errore.
- Più problemi: il componente aggiuntivo presenta più di uno dei problemi descritti in precedenza.

### <a name="macros-not-meeting-health-goals"></a>Macro che non soddisfano gli obiettivi di integrità

- Errori di caricamento: non è stato possibile caricare il documento.
- Errori di runtime: si è verificato un errore durante l'esecuzione della macro. Questi errori possono dipendere dagli input e pertanto potrebbero non verificarsi in tutte le circostanze.
- Errori di compilazione: la macro non è stata compilata correttamente e quindi non tenterà l'esecuzione.
- Più problemi: la macro presenta più di uno dei problemi descritti in precedenza.

> [!NOTE]
> L'inventario delle macro viene popolato dai dati di Readiness Toolkit per Office e dei file di dati usati di recente. L'integrità della macro viene popolata dai dati sull'integrità. A causa delle origini dati diverse, è possibile che lo stato di integrità della macro sia **Verifica necessaria** quando lo stato dell'inventario delle macro è **Analisi non eseguita**. <!--5922845-->

### <a name="known-issues"></a>Problemi noti

Si è verificato un problema noto con il riquadro **Distribuisci la raccolta pilota**. Al momento non può essere usato per eseguire la distribuzione in un progetto pilota. La soluzione alternativa consiste nell'usare il flusso di lavoro esistente per la distribuzione di un'applicazione tramite la distribuzione guidata in più fasi. <!--5525871-->

## <a name="next-steps"></a>Passaggi successivi

[Gestire gli aggiornamenti di Microsoft 365 Apps con Configuration Manager](manage-office-365-proplus-updates.md)