---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Panoramica del servizio Desktop Analytics integrato con Configuration Manager.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 23af311a78058240e6ebf8a2ca3c9e0fcdaf711f
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268556"
---
# <a name="what-is-desktop-analytics"></a>Che cos'è Desktop Analytics?

Desktop Analytics è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio offre dati analitici e intelligenza per consentire agli utenti di prendere decisioni più informate sull'idoneità degli aggiornamenti dei client Windows. Combina i dati dell'organizzazione con i dati aggregati di milioni di dispositivi connessi a servizi cloud Microsoft.

Usare Desktop Analytics con Configuration Manager per eseguire le operazioni seguenti:  

- Creare un inventario delle app in esecuzione nell'organizzazione  

- Valutare la compatibilità delle app con gli ultimi aggiornamenti delle funzionalità di Windows 10  

- Identificare i problemi di compatibilità e ricevere suggerimenti sulla mitigazione in base alle informazioni dettagliate sui dati abilitati per il cloud  

- Creare gruppi pilota che rappresentino l'intera applicazione e le proprietà del driver in un insieme minimo di dispositivi  

- Distribuire Windows 10 a dispositivi pilota e gestiti dalla produzione  

![Screenshot della home page di Desktop Analytics nel portale di Azure](media/portal-home.png)

Il video seguente è una sessione di Ignite 2019, che include altre informazioni su Desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Using Desktop Analytics and Configuration Manager to reduce Windows TCO through data-driven insights for management, servicing, and support](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions) (Uso di Desktop Analytics e Configuration Manager per ridurre il TCO di Windows grazie a informazioni dettagliate basate sui dati per la gestione, la manutenzione e il supporto)

passare al minuto 10:00 per una demo approfondita.

> [!Note]  
> Desktop Analytics è un successore di Windows Analytics, che è stato ritirato il 31 gennaio 2020.
>
> Le funzionalità di Windows Analytics sono combinate nel servizio Desktop Analytics. Desktop Analytics è anche ancora più strettamente integrato in Configuration Manager. Per altre informazioni, vedere [Domande frequenti per i clienti di Windows Analytics](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Vantaggi

Molti clienti hanno problemi a ottenere Windows 10 e a mantenerlo aggiornato. Il problema principale è quello di testare le applicazioni. Questo processo è in generalmente manuale. Per gli amministratori IT e i proprietari delle applicazioni analizzare continuamente le applicazioni esistenti e quindi correggere eventuali problemi è molto dispendioso in termini di tempo.

Desktop Analytics offre i vantaggi seguenti:

- **Inventario di dispositivi e software**: Inventario dei fattori chiave, ad esempio le app e le versioni di Windows.  

- **Identificazione del progetto pilota**: Identificazione dell'insieme minimo di dispositivi che consentono la più ampia copertura di fattori. Identifica i fattori ritenuti più importanti per un progetto pilota di aggiornamenti Windows. Assicurarsi che il progetto pilota sia ottimale per poter procedere in modo più rapido e sicuro a distribuzioni di grani dimensioni in ambiente di produzione.  

- **Identificazione dei problemi**: Usando congiuntamente i dati di mercato aggregati e i dati dell'ambiente, il servizio esegue una previsione dei potenziali problemi per ottenere Windows e mantenerlo aggiornato. Suggerisce quindi eventuali mitigazioni.  

- **Integrazione di Configuration Manager**: Il servizio cloud consente di abilitare l'infrastruttura locale esistente. Usare questi dati e queste analisi per distribuire e gestire Windows nei dispositivi.  

## <a name="prerequisites"></a>Prerequisiti

Per usare Desktop Analytics, verificare che l'ambiente soddisfi i prerequisiti seguenti.

### <a name="technical"></a>Prerequisiti tecnici

- Una sottoscrizione di Azure globale attiva con autorizzazioni di [Amministratore globale](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions). Gli [account Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) non sono supportati.  

    > [!Important]  
    > Desktop Analytics richiede attualmente la distribuzione di un servizio di Office 365 nel tenant di Azure AD. Non sarà un requisito in futuro.

    - Autorizzazioni di **Proprietario dell'area di lavoro** per **configurare l'area di lavoro** e i ruoli seguenti:  

      - Ruolo [**Amministratore di Desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions).

      - [**Collaboratore di Log Analytics**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) e [**Amministratore Accesso utenti**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) nel gruppo di risorse per usare un'area di lavoro esistente o crearne una nuova in un gruppo di risorse esistente.

      - Autorizzazioni di [**Proprietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) o [**Collaboratore**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) e [**Amministratore Accesso utenti**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) nella sottoscrizione per creare un'area di lavoro in un nuovo gruppo di risorse.  

    - Per accedere al portale dopo l'onboarding, sono necessari:

      - Il ruolo [**Amministratore Desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) e le autorizzazioni [**Proprietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) o [**Collaboratore**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) per il gruppo di risorse in cui è stata creata l'area di lavoro.

- Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva. Per altre informazioni, vedere [Aggiornare Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    - Ruolo [**Amministratore completo**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) in Configuration Manager  

    > [!NOTE]
    > Desktop Analytics supporta più gerarchie di Configuration Manager che dipendono da un singolo tenant di Azure AD.<!-- 4814075 --> Se nell'ambiente sono presenti più gerarchie, sono disponibili le opzioni seguenti:
    >
    > - Usare ID commerciali e tenant di Azure AD diversi.
    > - Configurare entrambe le gerarchie in modo da usare lo stesso ID commerciale per condividere il tenant di Azure AD e l'istanza di Desktop Analytics.

- Dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10  

    - Installare gli aggiornamenti più recenti. Per altre informazioni, vedere [Aggiornare i dispositivi](enroll-devices.md#update-devices).  

    - I dispositivi devono anche avere il client di Configuration Manager versione 1902 con aggiornamento cumulativo (4500571) o versione successiva. Per altre informazioni, vedere [Aggiornare Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics non supporta gli aggiornamenti a Windows 10 Long-Term Servicing Channel (LTSC). Per altre informazioni, vedere [Panoramica di Windows as a Service](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics è progettato per supportare al meglio lo scenario di aggiornamento sul posto. Se è necessario apportare modifiche principali, ad esempio passare da un'architettura a 32 bit a un'architettura a 64 bit, usare uno scenario di creazione dell'immagine. Le informazioni dettagliate di Desktop Analytics risultano comunque utili in questi classici scenari di distribuzione del sistema operativo, ma è possibile ignorare le indicazioni specifiche dell'aggiornamento sul posto. Per altre informazioni, vedere [Scenari per distribuire sistemi operativi aziendali con Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Dati di diagnostica di Windows. Per altre informazioni, vedere gli articoli seguenti:  

    - [Livelli dei dati di diagnostica](enable-data-sharing.md#diagnostic-data-levels)  

    - [Privacy di Desktop Analytics](privacy.md)  

- Connettività di rete dai dispositivi al cloud pubblico Microsoft. Per altre informazioni, vedere [Come abilitare la condivisione dei dati](enable-data-sharing.md).  

> [!Important]
> Microsoft è impegnata a offrire strumenti e risorse che consentono di controllare la privacy. Microsoft non raccoglie quindi i dati seguenti dai dispositivi che si trovano in paesi europei (SEE e Svizzera):
>
> - Dati di diagnostica di Windows da dispositivi Windows 8.1
> - Dati di uso delle app per Windows 7

### <a name="licensing-and-costs"></a>Licenze e costi

- Una sottoscrizione Azure globale attiva.

    > [!NOTE]
    > La maggior parte delle sottoscrizioni equivalenti per Configuration Manager include anche Azure AD. Vedere ad esempio i [piani Microsoft 365](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) e le [licenze Enterprise Mobility + Security](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- I dispositivi registrati in Desktop Analytics necessitano di una licenza di Configuration Manager valida. Per altre informazioni, vedere [Gestione delle licenze di Configuration Manager](../core/understand/product-and-licensing-faq.md).

- Per gli utenti del dispositivo è necessaria una delle licenze seguenti:

  - Windows 10 Enterprise E3 o E5 (incluso in Microsoft 365 F3, E3 o E5)

  - Windows 10 Education A3 o A5 (incluso in Microsoft 365 A3 o A5)

  - Accesso a Desktop virtuale Windows E3 o E5  

> [!NOTE]
> Oltre al costo di queste sottoscrizioni delle licenze, non sono previsti costi aggiuntivi per l'uso di Desktop Analytics con Azure Log Analytics. I tipi di dati inseriti da Desktop Analytics non sono soggetti ai costi di inserimento dati e conservazione di Log Analytics. Trattandosi di tipi di dati non fatturabili, questi dati non sono soggetti al limite di inserimento dati giornaliero di Log Analytics. Per altre informazioni, vedere [Utilizzo e costi di Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="next-steps"></a>Passaggi successivi

L'esercitazione seguente offre una guida dettagliata per iniziare a usare Desktop Analytics e Configuration Manager:
  
> [!div class="nextstepaction"]
> [Distribuire Windows 10 a un gruppo pilota](tutorial-windows10.md)
