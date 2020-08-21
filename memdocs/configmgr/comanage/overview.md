---
title: Co-gestione per dispositivi Windows 10
titleSuffix: Configuration Manager
description: Informazioni su come gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/01/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: f9e1809447f8d8ea8f6e0382575b71bfdec71fac
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695053"
---
# <a name="what-is-co-management"></a>Informazioni sulla co-gestione

<!-- 1350871 -->
La co-gestione è uno dei modi principali per collegare la distribuzione di Configuration Manager esistente al cloud di Microsoft 365. Consente di avere a disposizione funzionalità aggiuntive basate sul cloud, come l'accesso condizionale.

Con la co-gestione è possibile gestire i dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune. Consente di collegare al cloud gli investimenti esistenti in Configuration Manager tramite l'aggiunta di nuove funzionalità. La co-gestione offre la flessibilità di usare la soluzione tecnologica più idonea all'organizzazione.

Quando un dispositivo Windows 10 ha il client di Configuration Manager ed è registrato in Intune, si ottengono i vantaggi di entrambi i servizi. È possibile stabilire per quali carichi di lavoro trasferire eventualmente l'autorità da Configuration Manager a Intune. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro che non vengono trasferiti a Intune, e tutte le altre funzionalità di Configuration Manager non supportate dalla co-gestione.

È anche possibile eseguire la distribuzione pilota di un carico di lavoro con una raccolta separata di dispositivi. La distribuzione pilota consente di testare la funzionalità di Intune con un subset di dispositivi prima di passare un gruppo più ampio.

![Diagramma della panoramica della co-gestione](media/co-management-overview.svg)

[Visualizzare il diagramma per intero](media/co-management-overview.svg)

> [!Note]  
> Quando si gestiscono i dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune, questa configurazione è detta *co-gestione*. Quando si gestiscono i dispositivi con Configuration Manager e ci si iscrive a un servizio MDM di terze parti, questa configurazione è detta *coesistenza*. La disponibilità di due autorità di gestione per un singolo dispositivo può essere problematica se non si implementa la corretta orchestrazione tra le due. Con la co-gestione, Configuration Manager e Intune bilanciano i [carichi di lavoro](#workloads) per assicurare che non si verifichino conflitti. Questa interazione non esiste con i servizi di terze parti, quindi le funzionalità di gestione della coesistenza presentano limitazioni. Per altre informazioni, vedere [Coesistenza di servizi MDM di terze parti con Configuration Manager](coexistence.md).

## <a name="paths-to-co-management"></a>Percorsi per la co-gestione

I percorsi principali per realizzare la co-gestione sono due:  

- **Client di Configuration Manager esistenti**: alcuni dispositivi Windows 10 sono già client di Configuration Manager. Configurare Azure AD ibrido e registrarli in Intune.  

- **Nuovi dispositivi basati su Internet**: nuovi dispositivi Windows 10 che vengono aggiunti ad Azure AD e automaticamente registrati in Intune. Per raggiungere uno stato di co-gestione, è necessario installare il client di Configuration Manager.  

Per altre informazioni sui percorsi, vedere [Percorsi per la co-gestione](quickstart-paths.md).

## <a name="benefits"></a>Vantaggi

Quando si registrano client di Configuration Manager esistenti per la co-gestione, si ottiene il valore immediato seguente:  

- Accesso condizionale con conformità del dispositivo  

- Azioni remote basate su Intune, ad esempio: riavvio, controllo remoto o ripristino delle impostazioni predefinite

- Visibilità centralizzata dell'integrità dei dispositivi  

- Collegare utenti, dispositivi e app con Azure Active Directory (Azure AD)  

- Provisioning moderno con Windows Autopilot  

- Azioni remote

Per altre informazioni sul valore immediato offerto dalla co-gestione, vedere la serie di articoli di avvio rapido [Connessione al cloud con la co-gestione](quickstarts.md).

La co-gestione supporta anche l'orchestrazione con Intune per diversi carichi di lavoro. Per altre informazioni, vedere la sezione [Carichi di lavoro](#workloads).

## <a name="prerequisites"></a>Prerequisiti

La co-gestione presenta questi prerequisiti nelle aree seguenti:

- [Licenza](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Ruoli e autorizzazioni](#permissions-and-roles)  

### <a name="licensing"></a>Licenza

- Azure AD Premium

    > [!Note]  
    > Una sottoscrizione di Enterprise Mobility + Security (EMS) include sia Azure Active Directory Premium sia Microsoft Intune.

- Almeno una licenza di Intune come amministratore per accedere al portale di Intune.

    > [!Tip]
    > Assicurarsi di assegnare una licenza di Intune all'account usato per accedere al tenant. In caso contrario, l'accesso avrà esito negativo con il messaggio di errore "Utente non riconosciuto".
    >
    > Potrebbe non essere più necessario acquistare e assegnare singole licenze di Intune o EMS ai propri utenti. Per altre informazioni, vedere [Domande frequenti su prodotto e licenze](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="configuration-manager"></a>Configuration Manager

La co-gestione richiede Configuration Manager versione 1710 o successive.

A partire da Configuration Manager versione 1806, è possibile connettere più istanze di Configuration Manager a un singolo tenant di Intune. <!--1357944-->  

Per abilitare la co-gestione, non è richiesto l'onboarding del sito in Azure AD. Per [lo scenario del secondo percorso](#paths-to-co-management), i client di Configuration Manager basati su Internet richiedono [Cloud Management Gateway](../core/clients/manage/cmg/plan-cloud-management-gateway.md). Cloud Management Gateway richiede l'[onboarding del sito in Azure AD per la gestione del cloud](../core/servers/deploy/configure/azure-services-wizard.md).

### <a name="azure-ad"></a>Azure AD

- I dispositivi Windows 10 devono essere connessi ad Azure AD. Possono essere di uno dei due tipi seguenti:  

  - [Aggiunto ad Azure AD ibrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid), il dispositivo è aggiunto ad Active Directory locale e registrato in Azure Active Directory.

  - [Aggiunto solo ad Azure AD](/azure/active-directory/devices/azureadjoin-plan). Questo tipo è anche noto come "aggiunto a un dominio cloud".<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Configurare Intune](/intune/setup-steps)  

- [Abilitare la registrazione automatica di Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Aggiornare i dispositivi a Windows 10, versione 1709 o successive. Per altre informazioni, vedere [Adozione di Windows distribuito come servizio](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> I dispositivi mobili Windows 10 non supportano la co-gestione.

### <a name="permissions-and-roles"></a>Ruoli e autorizzazioni

<!--SCCMDocs issue #667-->
| Action | Ruolo necessario |
|----|----|
| Configurare un Cloud Management Gateway in Configuration Manager | **Gestione di sottoscrizioni** di Azure |
| Creare app Azure AD da Configuration Manager | **Amministratore globale** di Azure AD |
| Importare le app di Azure in Configuration Manager | **Amministratore completo** di Configuration Manager<br>Non sono necessari altri ruoli di Azure |
| Abilitare la co-gestione in Configuration Manager | Un utente di Azure AD<br>**Amministratore completo** di Configuration Manager con diritti appartenenti all'ambito **Tutti**.<!--SCCMDoc issue 626--> |

Per altre informazioni sui ruoli di Azure, vedere [Informazioni sui diversi ruoli](/azure/role-based-access-control/rbac-and-directory-admin-roles).

Per altre informazioni sui ruoli di Configuration Manager, vedere [Nozioni fondamentali di amministrazione basata su ruoli](../core/understand/fundamentals-of-role-based-administration.md).

## <a name="workloads"></a>Carichi di lavoro

Non è obbligatorio trasferire i carichi di lavoro oppure è possibile procedere singolarmente al momento opportuno. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro che non vengono trasferiti a Intune, e tutte le altre funzionalità di Configuration Manager non supportate dalla co-gestione.

La co-gestione supporta i carichi di lavoro seguenti:

- Criteri di conformità  

- Criteri di Windows Update  

- Criteri di accesso alle risorse  

- Endpoint Protection  

- Configurazione del dispositivo  

- App A portata di clic di Office  

- App client  

Per altre informazioni, vedere [Carichi di lavoro](workloads.md).

## <a name="monitor-co-management"></a>Monitorare la co-gestione

Il dashboard di co-gestione consente di esaminare i computer con co-gestione presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.

![Screenshot del dashboard di co-gestione](media/co-management-dashboard.png)

Per altre informazioni, vedere [Come monitorare la co-gestione](how-to-monitor.md).

## <a name="next-steps"></a>Passaggi successivi

- [Altre informazioni sul valore immediato e guida introduttiva alla co-gestione](quickstarts.md)  

- [Esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistenti](tutorial-co-manage-clients.md)