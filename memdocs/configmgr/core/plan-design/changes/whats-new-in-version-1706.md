---
title: Nuova versione 1706
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1706 di Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9b70850a8ef52c97c4fb7d78537fbc559701210d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702579"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Novità della versione 1706 di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1706 per Configuration Manager Current Branch è disponibile come aggiornamento nella console per siti precedentemente installati che eseguono la versione 1606, 1610 o 1702.

> [!TIP]  
> Per installare un nuovo sito, è necessario usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:    
> - [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx) (Installare nuovi siti)  
> - [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx) (Installare aggiornamenti nei siti)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines) (Versioni di base e di aggiornamento)  

Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1706 di Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruttura del sito

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Supporto della peer cache del client per i file di installazione rapida per Windows 10 e Office 365  
<!-- 1352486 -->
A partire da questa versione, la peer cache supporta la distribuzione dei file di installazione rapida del contenuto per Windows 10 e dei file di aggiornamento per Office 365. Non sono richieste configurazioni aggiuntive per supportare questa modifica.

### <a name="updates-for-the-data-warehouse"></a>Aggiornamenti per il data warehouse
<!-- 1277922 -->
Il data warehouse non è più una funzionalità di una versione non definitiva. Sono anche stati aggiornati i prerequisiti per includere il supporto per il database nei gruppi di disponibilità AlwaysOn di SQL Server e i cluster di failover. Per altre informazioni, vedere [Punto di servizio del data warehouse](../../servers/manage/data-warehouse.md).

### <a name="accessibility-improvements"></a>Miglioramenti all'accessibilità
<!-- 1253000 -->
Sono stati aggiunti altri miglioramenti all'accessibilità per la console di Configuration Manager. Per informazioni dettagliate, vedere [Funzionalità di accessibilità](../../understand/accessibility-features.md).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Miglioramenti per i gruppi di disponibilità Always On di SQL Server
<!-- 1352094 -->
Con questa versione è ora possibile usare le repliche con commit asincrono nei gruppi di disponibilità Always On di SQL Server usati con Configuration Manager. Ciò significa che è possibile aggiungere repliche aggiuntive ai gruppi di disponibilità da usare come backup remoti, e quindi usarli in caso di ripristino di emergenza.  
- Configuration Manager supporta l'uso della replica con commit asincrono per ripristinare la replica sincrona. Vedere le [opzioni di ripristino del database del sito](../../servers/manage/recover-sites.md#site-database-recovery-options) nell'argomento Backup e ripristino per informazioni su come eseguire questa operazione.
- Questa versione non supporta il failover per l'uso della replica con commit asincrono come database del sito.
Per altre informazioni, vedere [Preparare l'uso di gruppi di disponibilità Always On](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="update-reset-tool"></a>Strumento di reimpostazione dell'aggiornamento
<!-- 1324589 -->
A partire dalla versione 1706, i siti primari e i siti di amministrazione centrale di Configuration Manager includono lo strumento di reimpostazione dell'aggiornamento di Configuration Manager, **CMUpdateReset.exe**. Usare questo strumento con tutte le versioni di Current Branch supportate, per correggere gli errori quando gli aggiornamenti nella console presentano problemi durante il download o la replica. Per altre informazioni, vedere [Update reset tool](../../servers/manage/update-reset-tool.md) (Strumento di reimpostazione dell'aggiornamento).

### <a name="high-dpi-console-support"></a>Supporto per console con DPI elevato  
<!-- 1353476 -->
In questa versione sono state risolte le problematiche legate a come la console di Configuration Manager ridimensiona e visualizza diverse parti dell'interfaccia utente su dispositivi con DPI elevato, ad esempio un Surface Book.

### <a name="improved-boundary-groups-for-software-update-points"></a>Gruppi di limiti migliorati per i punti di aggiornamento software
<!-- 1324591 -->
Questa versione include dei miglioramenti per il funzionamento dei punti di aggiornamento del software con i gruppi di limiti. Di seguito viene riepilogato il nuovo comportamento di fallback:
- Il fallback per i punti di aggiornamento del software usa attualmente un tempo configurabile per il fallback a gruppi di limiti adiacenti.
- Indipendentemente dalla configurazione di fallback, un client tenta di raggiungere l'ultimo punto di aggiornamento del software che ha usato per 120 minuti. Dopo l'esito negativo nel raggiungere il server per 120 minuti, il client controlla quindi il proprio pool di punti di aggiornamento del software disponibili, per poterne trovare uno nuovo.
- Dopo l'esito negativo nel raggiungere il server originale per due ore, il client passa a un ciclo più breve per contattare un nuovo punto di aggiornamento del software. Ciò significa che se un client non riesce a connettersi con un nuovo server, seleziona rapidamente il server successivo dal relativo pool di server disponibili e cerca di contattarne uno nuovo.

Per altre informazioni, vedere la sezione [Punti di aggiornamento software](../../servers/deploy/configure/boundary-groups.md#software-update-points) nell'argomento Gruppi di limiti e relazioni per il Current Branch.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integrazione di Azure AD con Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Con questa versione, è stata migliorata l'integrazione di Configuration Manager e di Azure Active Directory (Azure AD).  Questi miglioramenti semplificano la configurazione dei servizi di Azure usati con Configuration Manager e consentono di gestire i client e gli utenti che eseguono l'autenticazione tramite Azure AD.

Il miglioramento dell'integrazione rende possibile quanto segue:  
- Procedura guidata per i servizi di Azure: questa procedura guidata offre un'esperienza di configurazione comune che sostituisce i singoli flussi di lavoro per configurare i servizi di Azure seguenti usati con Configuration Manager.
  - **Gestione cloud** Consente ai client di eseguire l'autenticazione usando Azure Active Directory (Azure AD). È anche possibile configurare l'individuazione utenti di Azure AD.
  - **Connettore Log Analytics** Connette ad Azure Log Analytics e sincronizza i dati della raccolta.
  - **Preparazione aggiornamenti** Connette a Preparazione aggiornamenti e visualizza i dati relativi alla compatibilità con l'aggiornamento per il client.
  - **Windows Store per le aziende** Connette allo store online di Windows Store per le aziende e ottiene le app per l'organizzazione che è possibile distribuire con Configuration Manager.


  Questo risultato si ottiene usando un'[app Web del server Azure](/azure/app-service/app-service-authentication-overview) per fornire i dettagli di sottoscrizione e configurazione, che in caso contrario devono essere immessi ogni volta che si configura un nuovo componente o servizio di Configuration Manager con Azure. Per altre informazioni, vedere [Procedura guidata per i servizi di Azure](../../servers/deploy/configure/azure-services-wizard.md).

- Usare Azure AD per autenticare i client in Internet per l'accesso ai siti di Configuration Manager. Azure AD evita di dover configurare e usare i certificati di autenticazione client. Per questo è necessario il ruolo del sistema del sito del gateway di gestione cloud. Per altre informazioni, vedere [Install and assign Configuration Manager clients from the Internet using Azure AD for authentication](../../clients/deploy/deploy-clients-cmg-azure.md) (Installare e assegnare i client di Configuration Manager da Internet usando Azure AD per l'autenticazione).

- Installare e gestire il client di Configuration Manager nei computer che si trovano in Internet. Per questo è necessario l'uso del ruolo del sistema del sito del gateway di gestione cloud. Per altre informazioni, vedere [Install and assign Configuration Manager clients from the Internet using Azure AD for authentication](../../clients/deploy/deploy-clients-cmg-azure.md) (Installare e assegnare i client di Configuration Manager da Internet usando Azure AD per l'autenticazione).

- Configurare l'individuazione utenti di Azure AD.  Usare la Procedura guidata Servizi di Azure per configurare questo nuovo metodo di individuazione, che cerca nell'istanza di Azure AD i dati utente che è quindi possibile usare con i dati di individuazione tradizionali.  Sono supportate sia la sincronizzazione completa che quella delta.  Per altre informazioni, vedere [Individuazione utente Azure AD](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="peer-cache-improvements"></a>Miglioramenti della peer cache
<!-- 1252345 -->
La peer cache non usa l'account di accesso alla rete per autenticare le richieste di download dai peer. Esiste un'avvertenza a questo proposito quando l'account continua a essere richiesto dai client. Rimane un requisito per i client che vengono avviati in WinPE e quindi accedono al contenuto da un'origine di peer cache. Per altre informazioni, vedere [Requisiti e considerazioni per la peer cache](../hierarchy/client-peer-cache.md#requirements).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Impostazioni di conformità

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Nuove impostazioni di configurazione per dispositivi Windows 10 non gestiti con il client di Configuration Manager
<!-- 1354715 -->
In questa versione sono state aggiunte nuove impostazioni degli elementi di configurazione per i dispositivi Windows 10 registrati con Intune o gestiti in locale da Configuration Manager. Le impostazioni sono le seguenti:

- **Password**
  - Crittografia dispositivo
- **Dispositivo**
  - Modifica delle impostazioni dell'area (solo desktop)
  - Modifica delle impostazioni di risparmio energia e sospensione
  - Modifiche alle impostazioni della lingua
  - Modifica dell'ora di sistema
  - Modifica del nome dispositivo
- **Store**
  - Aggiorna automaticamente le app dallo Store
  - Usa solo lo Store privato
  - Avvio di app originate dallo Store
- **Microsoft Edge**
  - Blocca l'accesso ai flag Informazioni su
  - Override del prompt SmartScreen
  - Override del prompt SmartScreen per i file
  - Indirizzo IP localhost WebRTC
  - Motore di ricerca predefinito
  - URL XML OpenSearch
  - Homepages (desktop only) (Home page - solo desktop)

Per informazioni dettagliate su tutte le impostazioni di Windows 10, vedere [Come creare elementi di configurazione per dispositivi Windows 10 e Windows 8.1 gestiti senza il client Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-device-compliance-policy-rules"></a>Nuove regole per i criteri di conformità dei dispositivi

* **Tipo di password richiesto**. Specificare se gli utenti devono creare una password alfanumerica o una password numerica. Per le password alfanumeriche, si specifica anche il numero minimo di set di caratteri che la password deve contenere. I quattro set di caratteri sono: lettere minuscole, lettere maiuscole, simboli e numeri.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **Blocca il debug USB nel dispositivo**. Non è necessario configurare questa impostazione poiché l'esecuzione del debug dell'USB è già stata disabilitata in Android per i dispositivi di lavoro.

  **Supportato in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Blocca app da origini sconosciute**. Obbligare i dispositivi a impedire l'installazione di app da origini sconosciute. Non è necessario configurare questa impostazione poiché Android per i dispositivi di lavoro limita sempre l'installazione da origini sconosciute.

  **Supportato in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Rendi obbligatoria l'analisi delle minacce nelle app**. Questa impostazione specifica che la funzionalità dell'app di verifica è abilitata nel dispositivo.

  **Supportato in:**
  * Android da 4.2 a 4.4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>Gestione delle applicazioni

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Eseguire script di PowerShell dalla console di Configuration Manager
<!-- 1236459 -->

In Configuration Manager, è possibile distribuire script ai dispositivi client tramite pacchetti e programmi. In questa versione sono state aggiunte nuove funzionalità che consentono di intraprendere le azioni seguenti:

- Importare gli script di PowerShell in Configuration Manager
- Modificare gli script dalla console di Configuration Manager (solo per script non firmati)
- Contrassegnare gli script come Approvato o Rifiutato per migliorare la sicurezza
- Eseguire gli script nelle raccolte di PC client Windows e nei PC Windows gestiti in locale. Gli script non vengono distribuiti ma eseguiti quasi in tempo reale sui dispositivi client.
- Esaminare i risultati restituiti dallo script nella console di Configuration Manager.

Per altre informazioni, vedere [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nuove impostazioni dei criteri di gestione delle applicazioni mobili    
<!--1324760-->
A partire da questa versione, è possibile usare tre nuove impostazioni di criteri di gestione delle applicazioni per dispositivi mobili (MAM):

- **Blocca acquisizione schermo (solo per dispositivi Android):** Specifica che le funzionalità di acquisizione schermo del dispositivo vengono bloccate quando si usa questa app.


## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

### <a name="hardware-inventory-collects-secure-boot-information"></a>L'inventario hardware raccoglie le informazioni di Avvio protetto
L'inventario hardware ora raccoglie informazioni sull'attivazione di Avvio protetto nei client. Queste informazioni sono archiviate nella classe **SMS_Firmware** (introdotta nella versione 1702) e abilitate nell'inventario hardware per impostazione predefinita. Per altre informazioni sull'inventario hardware, vedere [Come configurare l'inventario hardware](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="collapsible-task-sequence-groups"></a>Gruppi di sequenze di attività comprimibili
Questa versione introduce la possibilità di espandere e comprimere i gruppi di sequenze di attività. È possibile espandere o comprimere singoli gruppi oppure espandere o comprimere tutti i gruppi in una sola volta.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Ricaricare immagini di avvio con la versione corrente di Windows PE
Quando si esegue **Aggiorna punti di distribuzione** su un'immagine d'avvio selezionata, ora è possibile scegliere di ricaricare nell'immagine d'avvio la versione più recente di Windows PE (dalla directory di installazione di Windows ADK). Per altre informazioni, vedere [Aggiornare il contenuto nei punti di distribuzione](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Aggiornamenti software

### <a name="improvements-to-express-update-download-time"></a>Miglioramenti al tempo di download degli aggiornamenti rapidi
In questa versione è stato considerevolmente migliorato il tempo di download per gli aggiornamenti rapidi. Per altre informazioni, vedere [Gestire i file di installazione rapida per gli aggiornamenti di Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### <a name="manage-microsoft-surface-driver-updates"></a>Gestire gli aggiornamenti dei driver di Microsoft Surface
<!-- 1098490 -->
È ora possibile usare Configuration Manager per gestire gli aggiornamenti dei driver di Microsoft Surface.    


#### <a name="prerequisites"></a>Prerequisiti
- Tutti i punti di aggiornamento software devono eseguire Windows Server 2016.    
- Questa funzionalità è di una versione non definitiva ed è necessario attivarla per renderla disponibile. Per altre informazioni, vedere la sezione relativa all'[abilitazione delle funzionalità facoltative dagli aggiornamenti](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Per gestire gli aggiornamenti dei driver di Surface

1. Abilitare la sincronizzazione per i driver di Microsoft Surface. Usare la procedura in [Configurare le classificazioni e i prodotti per la sincronizzazione](../../../sum/get-started/configure-classifications-and-products.md) e selezionare la casella di controllo **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** nella scheda **Classificazioni** per abilitare i driver di Surface.
2. [Sincronizzare i driver di Microsoft Surface](../../../sum/get-started/synchronize-software-updates.md).
3. [Distribuire i driver di Microsoft Surface sincronizzati](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configurare i criteri di rinvio di Windows Update for Business
<!-- 1290890 -->
È ora possibile configurare i criteri di rinvio dei dispositivi per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità di Windows 10 gestiti direttamente da Windows Update for Business. È possibile gestire i criteri di rinvio nel nuovo nodo **Criteri di Windows Update for Business** in **Libreria Software** > **Manutenzione pacchetti di Windows 10**.

Per informazioni dettagliate, vedere [Integrazione con Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Notifiche utente migliorate per gli aggiornamenti di Office 365
Sono stati apportati miglioramenti per usare l'esperienza utente a portata di clic di Office quando un client installa un aggiornamento di Office 365. I miglioramenti includono le notifiche a comparsa e in-app e un conto alla rovescia. Per altre informazioni, vedere [Comportamento di riavvio e notifiche client per gli aggiornamenti di Office 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>Reporting

### <a name="use-windows-analytics-with-configuration-manager"></a>Usare Windows Analytics con Configuration Manager
<!-- 1318608 -->
Windows Analytics è un set di soluzioni che consentono di ottenere indicazioni sullo stato corrente dell'ambiente. I dispositivi dell'ambiente segnalano i dati di telemetria di Windows. I dati sono accessibili tramite il portale di Azure. Nel caso di Preparazione aggiornamenti i dati sono direttamente disponibili nel nodo di monitoraggio della console di Configuration Manager.


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestione di dispositivi mobili

### <a name="updates-to-android-for-work-sharing-configuration"></a>Aggiornamenti della configurazione della condivisione di Android for Work
<!-- 1338403 -->
In questa versione sono stati aggiornati i valori per l'impostazione **Consenti la condivisione dei dati tra i profili di lavoro e personali** nel gruppo di impostazioni **Profilo di lavoro**. È anche stata aggiunta un'impostazione personalizzata per bloccare il copia e incolla tra i profili di lavoro e personali.


### <a name="android-and-ios-enrollment-restrictions"></a>Restrizioni di registrazione di Android e iOS
<!-- 1290826 -->
Con questa versione, è ora specificare che gli utenti non possono registrare dispositivi Android o iOS personali. Le nuove impostazioni per la restrizione dei dispositivi permettono di limitare la registrazione dei dispositivi Android ai soli dispositivi predichiarati. Per i dispositivi iOS, è possibile bloccare la registrazione di tutti i dispositivi tranne quelli registrati tramite Device Enrollment Program di Apple, Apple Configurator o l'account del manager di registrazione dispositivi di Intune.

## <a name="protect-devices"></a>Proteggere i dispositivi

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Includere attendibilità per file e cartelle specifici in un criterio di Device Guard
<!--1324676-->
In questa versione sono state aggiunte altre funzionalità alla gestione del criterio di Device Guard.

Ora è possibile aggiungere facoltativamente attendibilità per file e cartelle specifici in un criterio di Device Guard. Ciò consente di:

- Risolvere i problemi relativi ai comportamenti del programma di installazione gestito
- Rendere attendibili le app line-of-business che non possono essere distribuite con Configuration Manager
- Rendere attendibili le app incluse in un'immagine di distribuzione del sistema operativo

Per altre informazioni, vedere [Gestione di Device Guard con Configuration Manager](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
