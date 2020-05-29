---
title: Percorsi per la co-gestione
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per i due metodi principali per configurare la co-gestione.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 27994107c32fac87a465240f07b68d57fddfc140
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983817"
---
# <a name="paths-to-co-management"></a>Percorsi per la co-gestione

Esistono due modi principali per configurare la co-gestione. È importante conoscere i prerequisiti per ogni percorso. Ognuno di essi richiede una combinazione di Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune e Windows 10. 

1. [Registrare automaticamente i dispositivi gestiti da Configuration Manager esistenti in Intune](#bkmk_path1)  
2. [Eseguire il bootstrap del client di Configuration Manager con provisioning moderno](#bkmk_path2)  

![Diagramma dei percorsi di co-gestione](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a> Percorso 1: Registrare automaticamente i client esistenti

Scegliendo questo percorso è possibile registrare rapidamente i dispositivi gestiti da Configuration Manager esistenti in Intune. La gestione di questi dispositivi da Configuration Manager non è diversa rispetto a prima di abilitare la co-gestione. In questo modo si ottengono tutti i vantaggi del cloud. Questo percorso è trasparente per gli utenti.

Prerequisiti per la configurazione:
- Azure AD ibrido
    - Una delle [opzioni di identità ibrida di Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin) seguenti:  
       - [Sincronizzazione dell'hash delle password](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) con l'[accesso Single Sign-On facile](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Autenticazione pass-through](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) con l'[accesso Single Sign-On facile](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [SSO federato (con Active Directory Federation Services (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Licenza Azure AD Premium
    - Configurare l'aggiunta ad Azure AD ibrido (scegliere una delle opzioni):
        - Per i domini gestiti
        - Per i domini federati
- Impostazione dell'agente client per l'aggiunta ad Azure AD ibrido
- Configurare la registrazione automatica dei dispositivi in Intune
- Abilitare la co-gestione in Configuration Manager

Per un'esercitazione dedicata a questo percorso, vedere [Esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistenti](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> Percorso 2: Eseguire il bootstrap con provisioning moderno

Prerequisiti per la configurazione:

1. [Configurare HTTP avanzato](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Creare i servizi cloud in Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Configurare il punto di gestione e i client per usare Cloud Management Gateway](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Usare Intune per distribuire il client di Configuration Manager](how-to-prepare-Win10.md)  

> [!Note]  
> Un'esercitazione per questo percorso sarà presto disponibile.

