---
title: Domande frequenti su prodotto e licenze
titleSuffix: Configuration Manager
description: Risposte alle domande frequenti sul prodotto e le licenze per Configuration Manager.
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b2c785fb41fa78ea0bd5d480560d45a3a7a7eda
ms.sourcegitcommit: efe89408a3948b79b38893174cb19268ee37c8f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854423"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Domande frequenti relative ai rami e alle licenze di Configuration Manager

*Si applica a: Configuration Manager (Current Branch) e System Center Configuration Manager (Long-Term Servicing Branch)*

Queste domande frequenti includono domande comuni sulle licenze in relazione alle versioni Current Branch e Long-Term Servicing Branch (LTSB) di Configuration Manager, disponibili tramite programmi Microsoft Volume Licensing. Questo articolo ha finalità puramente informative e non sostituisce la documentazione relativa alla gestione delle licenze di Configuration Manager. Per altre informazioni, vedere le [condizioni di licenza del prodotto](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). I termini per i prodotti descrivono le condizioni per l'utilizzo di tutti i prodotti Microsoft nell'ambito dei programmi per i contratti multilicenza.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a> Che cos'è Current Branch?

Current Branch è la build pronta per la produzione di Configuration Manager che offre un modello di servizio attivo. Questo modello di servizio è simile all'esperienza con Windows 10. Questo metodo supporta i clienti che si muovono al ritmo del cloud e vogliono un'innovazione più rapida. Con il modello di servizio Current Branch, è possibile continuare a ricevere nuove caratteristiche e funzionalità. Per questo motivo, solo i clienti con una sottoscrizione Software Assurance attiva per le licenze di Configuration Manager o con diritti di sottoscrizione equivalenti possono installare e usare la versione Current Branch di Configuration Manager.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a> Che cos'è Long Term Servicing Branch (LTSB)?  

LTSB è una build pronta per la produzione di Configuration Manager. È destinata ai clienti che lasciano scadere la sottoscrizione Software Assurance o diritti di sottoscrizione equivalenti. Rispetto a Current Branch, LTSB include [funzionalità ridotte](introduction-to-the-ltsb.md#features-that-arent-available). I clienti che lasciano scadere una sottoscrizione Software Assurance o diritti di sottoscrizione equivalenti devono disinstallare la versione Current Branch di Configuration Manager. I clienti che dispongono di diritti di licenza perpetui per Configuration Manager possono quindi installare e usare la build LTSB della versione di Configuration Manager corrente al momento della scadenza.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a> Che cosa significano gli acronimi *SA* e *L&SA* in relazione a Configuration Manager?

**Software Assurance** (SA) e **Licenza e Software Assurance** (L&SA) sono opzioni di licenza che concedono i diritti necessari per usare Configuration Manager. SA è un'opzione per un cliente che rinnova la copertura SA da un contratto precedente. L&SA è un'opzione per il cliente che acquista una nuova licenza e la copertura Software Assurance.

- **Software Assurance (SA)** : i clienti devono disporre di sottoscrizione SA attiva per licenze di Configuration Manager o di diritti di sottoscrizione equivalenti per poter installare e usare l'opzione Current Branch di Configuration Manager.

  Benché la sottoscrizione SA sia facoltativa per alcuni prodotti Microsoft, l'unico modo per ottenere i diritti di utilizzo di Configuration Manager Current Branch è con SA *o con diritti di sottoscrizione equivalenti*. Per altre informazioni, vedere le [domande frequenti su Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Licenza Microsoft e Software Assurance (L&SA)** : i clienti che acquistano nuove licenze per Configuration Manager devono acquisire una sottoscrizione L&SA (la copertura Licenza e Software Assurance).

  - La sottoscrizione SA concede i diritti di utilizzo di Current Branch.

  - Se la sottoscrizione SA scade e si possiede ancora una licenza per Configuration Manager, non è più possibile usare Current Branch. Per altre informazioni, vedere la domanda frequente [Che cosa ricevo se la mia copertura SA scade e ho una L&SA?](#bkmk_sa-expires)

Per altre informazioni sulle offerte di licenze, vedere [Modalità di acquisto](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) e le [condizioni di licenza del prodotto](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a> Che cosa sono le *sottoscrizioni equivalenti*?

Le sottoscrizioni equivalenti si riferiscono a programmi come [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) o [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Esistono anche altri programmi, ma questi sono i più comuni. Nei termini per i contratti multilicenza Microsoft questi programmi sono denominati licenze equivalenti a licenze di gestione.

Configuration Manager è incluso nei piani seguenti:

- Licenza di sottoscrizione utente (USL) di Intune
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F1

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager non è incluso nel piano di [Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business).

### <a name="what-changes-with-licensing-for-co-management-in-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> Quali modifiche sono state apportate alle licenze per la co-gestione in Microsoft Endpoint Manager?

<!-- 7202432 -->

La licenza di co-gestione consente ai clienti di Configuration Manager con Software Assurance di ottenere i diritti di gestione dei PC Intune senza dover acquistare e assegnare singole licenze di Intune agli utenti. Questa licenza consente di gestire più facilmente i dispositivi Windows con Microsoft Endpoint Manager.

- I dispositivi già gestiti da Configuration Manager e registrati in Intune per la co-gestione hanno quasi gli stessi diritti di un PC gestito autonomamente da Intune. Se si reimposta Windows in questo dispositivo, non è possibile effettuarne il provisioning con Windows Autopilot. Per Autopilot è richiesta una licenza completa di Intune.

- Se si registra un dispositivo Windows 10 in Intune con altri mezzi, è comunque necessaria una licenza completa di Intune. Ad esempio, si usa Autopilot per effettuare il provisioning di un dispositivo o un utente esegue manualmente la registrazione self-service.

- Per la registrazione di dispositivi gestiti da Configuration Manager esistenti in Intune per la co-gestione su larga scala senza interazione con l'utente, la co-gestione usa una funzionalità di Azure Active Directory (Azure AD) denominata registrazione automatica di Windows 10. Per la registrazione automatica è necessaria una licenza di Azure AD Premium (AADP1), separata da Microsoft Endpoint Manager. Per consentire il funzionamento della co-gestione in questo scenario, era necessario assegnare una licenza di AADP1 e una licenza di Intune a ogni singolo utente. Le licenze di co-gestione sono cambiate a partire dal 1° dicembre 2019. Ora non è più necessario assegnare singole licenze di Intune per questo scenario, ma sono comunque necessarie in altri scenari di registrazione. Il requisito della licenza di AADP1 rimane invariato per il funzionamento della registrazione automatica e della co-gestione.

- Se si vuole usare Intune per la gestione di dispositivi iOS, Android o macOS, è necessario ottenere una sottoscrizione di Intune appropriata tramite una licenza autonoma di Intune, Enterprise Mobility + Security (EMS) o Microsoft 365.

- Se non è disponibile alcun piano di sottoscrizione correlato a Intune, per supportare la co-gestione è necessario acquistare almeno una licenza di Intune. Questa licenza consente a un amministratore di accedere all'interfaccia di amministrazione di Microsoft Endpoint Manager.

- Se si usa la funzionalità di [mobilità e sicurezza di base](https://support.microsoft.com/office/capabilities-of-built-in-mobile-device-management-for-microsoft-365-a1da44e5-7475-4992-be91-9ccec25905b0) predefinita di Microsoft 365, non è possibile usare la nuova licenza di co-gestione per un utente che dispone anche di dispositivi gestiti dalla funzionalità di mobilità e sicurezza di base. Per usare la licenza di co-gestione per il dispositivo gestito da Configuration Manager dell'utente, eseguire una delle operazioni seguenti:

  - Assegnare una licenza di Intune completa all'utente e gestire i dispositivi tramite Intune.
  - Annullare la registrazione dei dispositivi dalla funzionalità di mobilità e sicurezza di base.

- Le licenze precedentemente disponibili per System Center Configuration Manager sono ancora applicabili a Microsoft Endpoint Configuration Manager. Se si installa un nuovo sito, usare i codici Product Key esistenti.

|Funzionalità | Licenza di co-gestione | Licenza di Intune completa |
|---------|---------|---------|
|Registrazione di Windows 10|Sì (solo per i dispositivi esistenti gestiti da ConfigMgr)|Sì|
|Registrazione di iOS, Android, macOS|No|Sì|
|AutoPilot|No|Sì|
|Gestione di applicazioni mobili (MAM)|No|Sì|
|Accesso condizionale<br>(richiesta licenza di AADP1 aggiuntiva)|Sì|Sì|
|Profili di dispositivo|Sì|Sì|
|Gestione degli aggiornamenti software|Sì|Sì|
|Argomento|Sì|Sì|
|Gestione delle app|Sì|Sì|
|Assistenza remota<br>(richiesta licenza di TeamViewer)|Sì|Sì|
|Desktop Analytics<br>(richieste licenze di sottoscrizione Windows)|Sì|N/D|
|Collegamento di tenant|Sì|N/D|
|Analisi degli endpoint|Sì|Sì|

Per altre informazioni, vedere gli articoli seguenti:

- [Prerequisiti per la co-gestione](../../comanage/overview.md#prerequisites)
- [Requisiti di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)
- [Prerequisiti per Desktop Analytics](../../desktop-analytics/overview.md#prerequisites)
- [Prerequisiti per il collegamento del tenant](../../tenant-attach/device-sync-actions.md#prerequisites)
- [Prerequisiti per le licenze di Analisi degli endpoint](../../../analytics/overview.md#licensing-prerequisites)
- [Usare l'accesso condizionale con Intune](../../../intune/protect/conditional-access.md#use-conditional-access-with-intune)
- [Prerequisiti di TeamViewer](../../../intune/remote-actions/teamviewer-support.md#prerequisites)

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a> Possiedo Enterprise Mobility + Security ed è scaduto, cosa devo fare?  

EMS concede i diritti di utilizzo di Configuration Manager Current Branch e Long-Term Service Branch. Alla scadenza di questi diritti, non è più possibile usare nessuno dei due rami ed è necessario disinstallarli.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a> Che cosa ricevo se la mia copertura SA scade e ho una L&SA?

Se la sottoscrizione SA è scaduta dopo il 1° ottobre 2016, a seconda del programma nell'ambito del quale è stata acquisita la sottoscrizione L&SA, è possibile mantenere una licenza perpetua per l'uso di Long-Term Servicing Branch (LTSB). Se attualmente si usa la versione Current Branch, è necessario disinstallarla e quindi installare LTSB. Non è previsto alcun supporto per la migrazione o la conversione in LTSB da Current Branch.

Se la sottoscrizione SA è scaduta prima del 1° ottobre 2016 e si è mantenuta una licenza perpetua per Configuration Manager, l'unica opzione disponibile per continuare a usarla è installare e usare System Center 2012 R2 Configuration Manager e i relativi Service Pack disponibili. È necessario disinstallare Current Branch alla scadenza della sottoscrizione SA e reinstallare la versione precedente del prodotto. Non è previsto alcun supporto per la migrazione o il downgrade da Configuration Manager Current Branch a versioni precedenti di Configuration Manager.

Se si usa System Center Endpoint Protection e la sottoscrizione SA scade, è necessario disinstallarlo. System Center Endpoint Protection non offre diritti *L (Licenza)* né diritti perpetui.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a> Ogni utente è "proprietario" di Current Branch?

No. Current Branch viene concesso in licenza d'uso per il periodo durante il quale si è in possesso di una sottoscrizione SA attiva. Ad esempio, alla scadenza della sottoscrizione *SA*, tramite *L&SA* si possiedono solo i diritti *L (licenza)* , che non includono i diritti di utilizzo di Current Branch. Se la licenza offre diritti perpetui, è possibile usare Configuration Manager LTSB al posto di Current Branch. Se la sottoscrizione SA è scaduta prima del 1° ottobre 2016, è anche possibile usare System Center 2012 R2 Configuration Manager.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a> È possibile acquistare Configuration Manager in modo autonomo senza SA?

No. L'unico modo per ottenere i diritti di utilizzo di Configuration Manager è attraverso l'acquisto di una licenza con SA o tramite una sottoscrizione equivalente. Sono disponibili programmi per sviluppatori come MSDN, in cui Configuration Manager viene offerto per scopi di sviluppo e test, ma non per l'uso in ambienti di produzione.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> Un ambiente non di produzione per il test o lo sviluppo richiede una licenza esplicita?

<!-- SCCMDocs#1848 -->

- Se si usa lo stesso software Current Branch dell'ambiente di produzione, è necessaria una licenza esplicita. Rivolgersi al team dell'account per determinare se lo specifico contratto di licenza in uso copre più istanze in più ambienti.

- Alcuni programmi per sviluppatori come MSDN offrono prodotti come Configuration Manager per il test e lo sviluppo, ma non per l'uso in ambienti di produzione.

- Per un ambiente temporaneo, è possibile usare la [versione di valutazione](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) per 180 giorni.

- Per un ambiente lab, è possibile usare [Technical Preview Branch](../get-started/technical-preview.md). Technical Preview ha la stessa funzionalità di Current Branch, ma presenta alcune limitazioni in termini di scalabilità e piattaforme supportate.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> Ho i diritti necessari per l'installazione degli aggiornamenti nella console di Configuration Manager?

Se si è in possesso di una sottoscrizione *SA* attiva, la risposta è sì.

In caso contrario, disinstallare Current Branch e quindi installare la build LTSB di Configuration Manager. LTSB non riceve aggiornamenti per le versioni incrementali di Configuration Manager, ma riceve gli aggiornamenti della sicurezza in base al ciclo di vita del supporto.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a> Se si è acquistato EMS o Microsoft 365 tramite un Cloud Solution Provider, si possiedono i diritti necessari per usare Configuration Manager?

Sì, si possiedono i diritti necessari per usare Configuration Manager per gestire i client coperti dalla licenza EMS. Scaricare e installare innanzitutto il [software di valutazione](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Quindi contattare il supporto tecnico Microsoft per ottenere il codice di licenza.<!--issue472--> Quando si parla con il supporto tecnico Microsoft, chiedere di fare riferimento all'ID articolo interno 4033838.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a> La data di fine sottoscrizione corrisponde alla data di scadenza della SA?

Se *SA* o la sottoscrizione è attiva, si dispone dei diritti di utilizzo per Configuration Manager Current Branch. Una sottoscrizione attiva equivale a una *SA* attiva, ma non a una *"L" (licenza)* perpetua. Quando la sottoscrizione termina, disinstallare Current Branch. A questo punto, non si dispone più dei diritti necessari per usare LTSB.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a> Quali sono i diritti di utilizzo associati alla tecnologia SQL inclusa in Configuration Manager?

Configuration Manager include la tecnologia SQL Server. Le condizioni di licenza di Microsoft per questo prodotto consentono l'uso della tecnologia SQL Server solo per il supporto dei componenti di Configuration Manager. Non sono necessarie Licenze CAL (Client Access License) di SQL Server per tale uso.

I diritti di utilizzo approvati per le funzionalità SQL con Configuration Manager includono:

- Ruolo Database del sito
- Windows Server Update Services (WSUS) per il ruolo Punto di aggiornamento software
- SQL Server Reporting Services (SSRS) per il ruolo Punto di reporting
- Ruolo Punto di servizio del data warehouse
- Ruolo Repliche di database per i punti di gestione

La licenza di SQL Server inclusa con Configuration Manager supporta ogni istanza di SQL Server installata per ospitare un database per Configuration Manager. Tuttavia, solo i database per Configuration Manager nell'elenco precedente possono essere eseguiti in tale sistema SQL Server quando si usa questa licenza. Se un database per un'applicazione Microsoft aggiuntiva o un prodotto di terze parti condivide il sistema SQL Server, è necessaria una licenza distinta per tale istanza di SQL Server.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a> Per la gestione di dispositivi mobili (MDM) in locale è necessaria una sottoscrizione di Intune?

Per iniziare a usare MDM in locale nella versione 1806 e precedenti, è necessaria una sottoscrizione di Microsoft Intune. La sottoscrizione è necessaria solo per tenere traccia delle licenze dei dispositivi e non viene usata per gestire o archiviare le informazioni di gestione per i dispositivi. Tutti i dati di gestione vengono archiviati nell'organizzazione tramite l'infrastruttura di Configuration Manager locale.  

A partire dalla versione 1810, una connessione a Intune non è più necessaria per le nuove distribuzioni MDM locali.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).
