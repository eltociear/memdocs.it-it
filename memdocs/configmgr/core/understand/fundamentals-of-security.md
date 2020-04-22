---
title: Nozioni fondamentali sulla sicurezza
titleSuffix: Configuration Manager
description: Informazioni sui livelli di sicurezza in Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707059"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Nozioni fondamentali sulla sicurezza di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra i componenti di sicurezza fondamentali seguenti di qualsiasi ambiente Configuration Manager:
- [Livelli di sicurezza](#bkmk_layers)
- [Amministrazione basata su ruoli](#bkmk_rba)
- [Protezione degli endpoint client](#bkmk_endpoints)
- [Account e gruppi di Configuration Manager](#bkmk_accounts)
- [Privacy](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> Livelli di sicurezza

La sicurezza in Configuration Manager è costituita dai livelli seguenti: 
- [Sicurezza di rete e del sistema operativo Windows](#bkmk_layer-windows)
- [Infrastruttura di rete: firewall, identificazione delle intrusioni, infrastruttura a chiave pubblica (PKI)](#bkmk_layer-network)
- [Controlli di sicurezza di Configuration Manager](#bkmk_layer-cm)
- [Provider SMS](#bkmk_layer-provider)
- [Autorizzazioni per il database del sito](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Sicurezza di rete e del sistema operativo Windows
Il primo livello è offerto dalle funzionalità di sicurezza di Windows per il sistema operativo e la rete. Questo livello include i componenti seguenti:  

-   Condivisione di file per il trasferimento di file tra componenti di Configuration Manager  

-   Elenchi di controllo di accesso (ACL) per agevolare la protezione dei file e delle chiavi del Registro di sistema  

-   Internet Protocol Security (IPSec) per proteggere le comunicazioni  

-   Criteri di gruppo per impostare criteri di sicurezza  

-   Autorizzazioni DCOM (Distributed Component Object Model) per applicazioni distribuite, ad esempio la console di Configuration Manager  

-   Servizi di dominio Active Directory per memorizzare le entità di protezione  

-   Protezione account di Windows, inclusi alcuni gruppi creati da Configuration Manager durante l'installazione  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> Infrastruttura di rete

Componenti di sicurezza aggiuntivi, ad esempio firewall e identificazione delle intrusioni, contribuiscono alla difesa dell'intero ambiente. I certificati emessi dalle implementazioni di infrastruttura a chiave pubblica (PKI) standard per il settore consentono di offrire autenticazione, firma e crittografia.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Controlli di sicurezza di Configuration Manager

Oltre alla sicurezza offerta dall'infrastruttura di rete e server Windows, Configuration Manager controlla l'accesso alla propria console e alle proprie risorse in diversi modi. Per impostazione predefinita, solo gli amministratori locali hanno i diritti per i file e le chiavi del Registro di sistema necessari per la console di Configuration Manager nei computer in cui è installata.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> Provider SMS

Il livello successivo di protezione si basa sull'accesso tramite Windows Management Instrumentation (WMI), in particolare sul provider SMS. Il provider SMS è un componente di Configuration Manager che concede a un utente l'accesso per eseguire query nel database del sito per informazioni. Per impostazione predefinita, l'accesso al provider è limitato ai membri del gruppo SMS Admins locale. Questo gruppo contiene inizialmente solo l'utente che ha installato Configuration Manager. Per concedere altre autorizzazioni account al repository Common Information Model (CIM) e al provider SMS, aggiungere altri account al gruppo SMS Admins.  

A partire dalla versione 1810, è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. <!--1357013-->  

Per altre informazioni, vedere [Piano per il provider SMS](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> Autorizzazioni per il database del sito

Il livello di protezione finale si basa sulle autorizzazioni per gli oggetti nel database del sito. Per impostazione predefinita, l'account di sistema locale e l'account utente usato per l'installazione di Configuration Manager possono amministrare tutti gli oggetti nel database di sito. Concedere e limitare le autorizzazioni per altri utenti amministratori nella console di Configuration Manager usando l'amministrazione basata su ruoli.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a> Amministrazione basata su ruoli  

 Configuration Manager usa l'amministrazione basata su ruoli per consentire la protezione di oggetti quali raccolte, distribuzioni e siti. Questo modello di amministrazione definisce e gestisce centralmente le impostazioni di accesso di protezione a livello di gerarchia per tutti i siti e le impostazioni del sito. 

 Un amministratore assegna *ruoli di sicurezza* a utenti amministratori e autorizzazioni di gruppo. Le autorizzazioni sono collegate a diversi tipi di oggetto di Configuration Manager, ad esempio per creare o modificare le impostazioni client. 

 Gli *ambiti di sicurezza* raggruppano istanze specifiche di oggetti che un utente amministratore ha la responsabilità di gestire, ad esempio un'applicazione che installa Microsoft Office. 

 La combinazione di ruoli di sicurezza, ambiti di sicurezza e raccolte consente di definire gli oggetti che possono essere visualizzati e gestiti da un utente amministrativo. Configuration Manager installa alcuni ruoli di sicurezza predefiniti per le attività di gestione comuni. È possibile creare ruoli di sicurezza personalizzati per supportare requisiti aziendali specifici.  

 Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> Protezione degli endpoint client  

 Configuration Manager protegge la comunicazione dei client ai ruoli del sistema del sito usando certificati autofirmati o PKI oppure token di Azure Active Directory (Azure AD). Alcuni scenari richiedono l'uso di certificati PKI. Ad esempio, la [gestione client basata su Internet](../clients/manage/plan-internet-based-client-management.md) e i [client dispositivo mobile](../../mdm/plan-design/plan-on-premises-mdm.md).  

 È possibile configurare i ruoli del sistema del sito ai quali si connettono i client per la comunicazione client di tipo HTTPS o HTTP. I computer client comunicano sempre usando il metodo più sicuro disponibile. I computer client passano all'uso del metodo di comunicazione meno sicuro solo se sono disponibili ruoli del sistema del sito che consentono le comunicazioni HTTP.  

 Per altre informazioni, vedere [Pianificare la sicurezza](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Account e gruppi di Configuration Manager  

 Configuration Manager usa l'account di sistema locale per la maggior parte delle operazioni del sito. Per alcune attività di gestione potrebbe essere necessario creare e gestire altri account. Durante l'installazione, Configuration Manager crea diversi gruppi predefiniti e ruoli di SQL Server. Potrebbe essere necessario aggiungere manualmente account computer o account utente ai gruppi e ai ruoli di SQL Server predefiniti.  

 Per altre informazioni, vedere [Account usati in Configuration Manager](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a> Privacy  

 Prima di implementare Configuration Manager, valutare i requisiti relativi alla tutela della privacy. Anche se i prodotti di gestione aziendale offrono molti vantaggi derivanti dalla possibilità di gestire un numero elevato di client, il software potrebbe influire sulla privacy degli utenti all'interno dell'organizzazione. Configuration Manager include molti strumenti per la raccolta dei dati e il monitoraggio dei dispositivi. Alcuni strumenti potrebbero avere implicazioni a livello di privacy nell'organizzazione.  

 Ad esempio, l'installazione del client di Configuration Manager abilita per impostazione predefinita molte impostazioni di gestione. Questa configurazione comporta l'invio, da parte del software client, di informazioni al sito di Configuration Manager. Il sito archivia le informazioni del client nel proprio database. Le informazioni del client non vengono inviate direttamente a Microsoft. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Vedere anche

- [Pianificare la sicurezza](../plan-design/security/plan-for-security.md)  

- [Sicurezza e privacy per i client di Configuration Manager](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurare la sicurezza](../plan-design/security/configure-security.md)   

- [Comunicazioni tra gli endpoint](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Riferimento tecnico per i controlli crittografici](../plan-design/security/cryptographic-controls-technical-reference.md)  
