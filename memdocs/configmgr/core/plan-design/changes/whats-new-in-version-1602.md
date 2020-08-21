---
title: Novità della versione 1602
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1602 di Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9a54ee5fb427f276ec755e748513b178d0c026ab
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698572"
---
# <a name="what39s-new-in-version-1602-of-configuration-manager"></a>Novità della versione 1602 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


L'aggiornamento 1602 per Configuration Manager è disponibile solo come aggiornamento nella console per i siti installati in precedenza che eseguono la versione 1511. La versione 1511 è la versione di base iniziale usata per installare nuovi siti di Configuration Manager.  


> [!TIP]  
> Sono disponibili altre informazioni su:  
>   
> - [Installing new sites](../../servers/deploy/install/prepare-to-install-sites.md) (Installazione di nuovi siti) (con una versione di base, ad esempio 1511)  
> - [Installing updates at sites](../../servers/manage/updates.md) (Installazione di aggiornamenti nei siti) (ad esempio versione 1602)  

 Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1602 di Configuration Manager.  

## <a name="site-infrastructure"></a>Infrastruttura del sito  

###  <a name="in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a>Aggiornamento sul posto del sistema operativo dei server del sito che eseguono Windows Server 2008 R2  
 I siti di Configuration Manager che eseguono la versione 1602 o versioni successive supportano l'aggiornamento sul posto del sistema operativo dei server del sito da Windows Server 2008 R2 a Windows Server 2012 R2.  

> [!WARNING]  
>  Prima di eseguire l'aggiornamento a Windows Server 2012 R2, è necessario disinstallare WSUS 3.2 dal server.  
>   
>  Per altre informazioni su questo passaggio critico, vedere la sezione "Funzionalità nuove e modificate" in [Panoramica di Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

 Per aggiornare un server, usare le procedure di aggiornamento di Windows Server 2012 R2. Non è necessario eseguire un ripristino del server del sito di Configuration Manager dopo l'aggiornamento. Per le procedure di aggiornamento, vedere [Opzioni di aggiornamento per Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) nella documentazione di Windows Server.  

###  <a name="sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> Gruppi di disponibilità SQL Server AlwaysOn  
 È possibile usare i gruppi di disponibilità SQL Server AlwaysOn per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale come soluzione a disponibilità elevata e di ripristino di emergenza.  

 Per informazioni dettagliate, vedere [SQL Server AlwaysOn per database del sito a disponibilità elevata per Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo  

### <a name="windows-10-servicing"></a>Manutenzione di Windows 10  
 In Configuration Manager versione 1602 sono stati aggiunti i miglioramenti seguenti per la manutenzione di Windows 10:  

-   Sono disponibili nuove opzioni di filtro per i piani di manutenzione che consentono di filtrare per **Lingua**, **Richiesto** e **Titolo**. Verranno aggiunti alla distribuzione associata solo gli aggiornamenti che soddisfano i criteri specificati.  

-   Quando si seleziona la classificazione **Aggiornamenti** per la sincronizzazione degli aggiornamenti software, viene visualizzato un avviso. Questo avviso segnala che è necessario l'[hotfix 3095113](https://support.microsoft.com/kb/3095113) per Windows Server Update Services (WSUS) 4.0 prima di poter sincronizzare correttamente gli aggiornamenti software e per il corretto funzionamento della manutenzione di Windows 10. Dal messaggio di avviso è possibile passare all'articolo della Knowledge Base associato.  

-   Gli aggiornamenti disponibili di Windows 10 vengono visualizzati ora solo nel nodo **Manutenzione di Windows 10** \ **Tutti gli aggiornamenti di Windows 10** della console di Configuration Manager. Questi aggiornamenti non vengono più visualizzati nel nodo **Aggiornamenti software** \ **Tutti gli aggiornamenti software** della console.  

-   Un piano di manutenzione è considerato una distribuzione ad alto rischio e la finestra **Seleziona raccolta** visualizza solo le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito. Per altre informazioni, vedere [Impostazioni per gestire le distribuzioni ad alto rischio per Configuration Manager](../../servers/manage/settings-to-manage-high-risk-deployments.md).  

-   Gli utenti che avviano un pacchetto di aggiornamento di Windows 10 ricevono ora un messaggio che li informa che stanno per aggiornare il proprio sistema operativo.  

## <a name="application-management"></a>Gestione delle applicazioni  

### <a name="ios-app-configuration-policies"></a>Criteri di configurazione delle app iOS  
 Usare i criteri di configurazione delle app di Configuration Manager per specificare le impostazioni che potrebbero essere necessarie quando l'utente esegue un'app iOS. Un'applicazione potrebbe richiedere all'utente di specificare valori personalizzati per un numero di porta, una lingua, impostazioni di sicurezza o impostazioni personalizzazione, ad esempio un logo aziendale. Se queste impostazioni vengono immesse in modo non corretto, si può avere un aumento del carico dell'help desk rallentando inoltre l'adozione di nuove app.  

 I criteri di configurazione delle app permettono di evitare questi problemi consentendo di distribuire tali impostazioni agli utenti in un criterio prima dell'esecuzione dell'app. Le impostazioni vengono quindi specificate automaticamente e l'utente non deve intraprendere alcuna azione.

### <a name="manage-volume-purchased-ios-apps"></a>Gestire le app iOS acquistate con Volume Purchase Program  
 Configuration Manager semplifica la distribuzione e la gestione delle app acquistate con Volume Purchase Program (VPP) di Apple. Configuration Manager importa le informazioni di licenza dall'App Store e tiene traccia del numero di licenze usate.  


### <a name="automatic-creation-of-office-mobile-apps"></a>Creazione automatica di app di Office per dispositivi mobili  
 Quando si esegue l'aggiornamento alla versione 1602 dalla versione 1511, Configuration Manager crea automaticamente le seguenti app di Microsoft Office per dispositivi mobili Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (solo iOS)  

-   Microsoft Outlook  

Queste app si trovano nel nodo **Applicazioni** della console di Configuration Manager.  

 Per altre informazioni sulla distribuzione di applicazioni, vedere [Come distribuire applicazioni con Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Aggiornamenti software  

### <a name="manage-office-365-client-updates"></a>Gestire gli aggiornamenti del client di Office 365  
 Configuration Manager permette di gestire gli aggiornamenti del client di Office 365 usando il flusso di lavoro Gestione aggiornamenti software. Per altre informazioni, vedere [Gestire gli aggiornamenti di Office 365 ProPlus con Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).  

## <a name="compliance-settings"></a>Impostazioni di conformità  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Impostazioni di conformità per i dispositivi che eseguono Windows 10 Team  
 Sono state aggiunte nuove impostazioni all'elemento di configurazione **Windows 8.1 e Windows 10**. Queste impostazioni consentono di controllare i dispositivi che eseguono Windows 10 Team, ad esempio un dispositivo Surface Hub.  

 Per informazioni dettagliate, vedere [Come creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Impostazioni della modalità tutto schermo per i dispositivi Android Samsung KNOX Standard  
 La modalità tutto schermo consente di bloccare un dispositivo per consentire solo alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello dimostrativo di un dispositivo o per un dispositivo dedicato all'esecuzione di una sola funzione, ad esempio un dispositivo POS. In Configuration Manager è ora possibile specificare le impostazioni della modalità tutto schermo per i dispositivi Samsung KNOX Standard.  


## <a name="conditional-access"></a>Accesso condizionale  

### <a name="conditional-access-for-pcs-managed-by-configuration-manager"></a>Accesso condizionale per i PC gestiti da Configuration Manager  
 Prima di questa versione, per configurare l'accesso condizionale per un PC era necessario che il PC fosse registrato in Intune o aggiunto a un dominio. A partire dall'aggiornamento 1602, è supportato l'accesso condizionale per i PC gestiti da Configuration Manager. Per i PC gestiti da Configuration Manager, è possibile limitare l'accesso a Exchange Online e SharePoint Online solo ai dispositivi che soddisfano i criteri di conformità impostati.  


### <a name="restricting-access-based-on-the-health-of-devices"></a>Limitazione dell'accesso in base allo stato di integrità dei dispositivi  
 È ora possibile limitare l'accesso alla posta elettronica e ai servizi di Office 365 in base all'integrità dei dispositivi, come segnalato dal Servizio di attestazione dell'integrità. Inoltre, i dispositivi gestiti da Intune sono inclusi nei report sull'integrità del dispositivo.  

 La console di Configuration Manager offre una nuova regola di conformità che consente di specificare se l'accesso deve essere consentito o negato ai dispositivi in base al loro stato di integrità. Per informazioni dettagliate sul servizio di attestazione dell'integrità e su come viene segnalata l'integrità dei dispositivi in Intune, vedere [Attestazione dell'integrità per Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Nuove regole dei criteri di conformità  
 Sono state aggiunte nuove regole dei criteri di conformità, come gli aggiornamenti automatici e la richiesta di una password per sbloccare i dispositivi, per supportare requisiti di sicurezza migliori.


### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Assicurarsi che i dispositivi registrati e conformi abbiano sempre accesso a Exchange locale  
 Quando si seleziona l'opzione seguente, i dispositivi registrati in Intune e conformi ai criteri di conformità possono accedere a Exchange locale: **Sostituzione della regola predefinita: consenti sempre l'accesso a Exchange ai dispositivi conformi e registrati in Intune**. Questa regola è disponibile nella pagina **Generale** della **Configurazione guidata dei criteri di accesso condizionale** per Exchange locale.

 Questa regola sostituisce la regola predefinita, ossia anche se si definisce per la regola predefinita l'impostazione per la quarantena o il blocco dell'accesso, i dispositivi registrati e conformi potranno comunque accedere a Exchange locale. Usare questa impostazione quando si vuole che i dispositivi registrati e conformi abbiano sempre accesso alla posta elettronica tramite Exchange locale.   

 Per la procedura dettagliata, vedere [Gestire l'accesso alla posta elettronica](../../../mdm/understand/what-happened-to-hybrid.md).  

## <a name="client-management"></a>Gestione dei client  

### <a name="client-online-status"></a>Stato online del client  
 È disponibile un nuovo stato per i client per monitorare se un computer è online o meno. Un computer viene considerato online se è connesso al relativo punto di gestione assegnato. Per indicare che il computer è online, il client invia messaggi di tipo ping al punto di gestione. Se il punto di gestione non riceve alcun messaggio per 5 minuti, lo stato del client viene considerato offline.  

 Per informazioni dettagliate, vedere [Come monitorare i client](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aggiornare i criteri di computer e utenti da Software Center  
 È stata aggiunta una nuova opzione, **Criteri sincronizzazione**, alla pagina **Opzioni** > **Manutenzione computer** di Software Center che consente al PC di aggiornare i criteri di computer e utenti di Configuration Manager.  

### <a name="software-center-branding-changes"></a>Modifiche di personalizzazione di Software Center  
 È possibile modificare il colore, il nome dell'organizzazione e l'icona visualizzati in Software Center. Queste impostazioni vengono applicate in base alle regole seguenti:  

- Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni non è installato, Software Center visualizza il nome dell'organizzazione specificato nell'impostazione **Nome organizzazione visualizzato in Software Center** del client **Agente computer**.  

- Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni è installato, Software Center visualizza il nome dell'organizzazione e il colore specificati nelle proprietà del ruolo del server del sito punto per siti Web del Catalogo applicazioni.  

- Se una sottoscrizione di Microsoft Intune è configurata e connessa all'ambiente Configuration Manager, Software Center visualizza il nome dell'organizzazione, il colore e il logo aziendale specificati nelle proprietà della sottoscrizione di Intune.  

### <a name="health-attestation"></a>Attestazione dell'integrità  
 Gli amministratori possono visualizzare l'attestazione dell'integrità del dispositivo di Windows 10 nella console di Configuration Manager. Questa funzionalità è disponibile per Configuration Manager e Configuration Manager con Microsoft Intune. L'attestazione dell'integrità dei dispositivi consente all'amministratore di assicurare che nei computer client siano abilitate le seguenti configurazioni attendibili di BIOS, TPM e software di avvio:  

-   Antimalware ad esecuzione anticipata  

-   BitLocker  

-   Avvio protetto  

-   Integrità del codice  

Per informazioni dettagliate, vedere [Attestazione dell'integrità per Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Miglioramenti delle impostazioni antimalware di Endpoint Protection  
 Nella versione 1602 sono state aggiunte le nuove impostazioni seguenti nei criteri antimalware di Endpoint Protection per Windows Defender:  

-   Protezione in tempo reale: Abilita la protezione per le applicazioni potenzialmente indesiderate al download o prima dell'installazione.  

-   Impostazioni di analisi: Analizza le unità di rete mappate durante un'analisi completa.  

-   Impostazioni per l'invio automatico dei file di esempio:  

     Il motore antimalware può richiedere l'invio a Microsoft di file di esempio per un'ulteriore analisi. Per impostazione predefinita, viene sempre visualizzata una richiesta prima dell'invio di tali campioni. Gli amministratori ora possono gestire le impostazioni seguenti per configurare questo comportamento:  

    -   Avanzate: Abilitare l'invio automatico di file di esempio per consentire a Microsoft di determinare se alcuni elementi rilevati siano dannosi.  

    -   Avanzate: Consenti agli utenti di modificare le impostazioni di invio automatico dei file di esempio.  

    In più, nella sezione "Impostazioni di esclusione" dei criteri antimalware di Endpoint Protection, l'impostazione esistente **Exclude files and folders** (Escludi file e cartelle) ora consente l'esclusione di dispositivi.  

Per informazioni dettagliate, vedere [Come creare e distribuire criteri antimalware per Endpoint Protection](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestione di dispositivi mobili  

### <a name="ios-activation-lock"></a>Blocco attivazione di iOS  
 Configuration Manager consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Blocco attivazione viene abilitato automaticamente quando si usa l'app Trova il mio iPhone in un dispositivo. Una volta abilitato, richiede l'immissione di un ID Apple e una password dell'utente prima di poter:  

-   Disattivare Trova il mio iPhone.  

-   Cancellare il dispositivo.  

-   Riattivare il dispositivo.  

Configuration Manager può richiedere lo stato del blocco attivazione per i dispositivi con e senza supervisione che eseguono iOS 7.1 e versioni successive. Per i dispositivi con supervisione, Configuration Manager può recuperare il codice del bypass di Blocco attivazione e inviarlo direttamente al dispositivo.  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorare le distribuzioni di termini e condizioni  
 È possibile monitorare le distribuzioni di termini e condizioni nella console di Configuration Manager.  

 Selezionare la distribuzione di termini e condizioni nell'elenco delle distribuzioni. L'area di riepilogo mostra le statistiche seguenti:  

-   **Conforme**: gli utenti hanno accettato la versione più recente di termini e condizioni.  

-   **Erroree**  

-   **Non conforme**: gli utenti hanno accettato una versione di termini e condizioni, ma non la più recente.  

-   **Sconosciuto**: gli utenti non hanno mai accettato termini e condizioni, inclusi quelli senza un dispositivo registrato.