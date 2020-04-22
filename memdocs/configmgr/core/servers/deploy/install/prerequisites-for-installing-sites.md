---
title: Prerequisiti per i siti
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per l'installazione di diversi tipi di siti di Configuration Manager.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8362dbf5cf7264c19f683ce5a224f1e0ec348b36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700669"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Prerequisiti per l'installazione di siti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di iniziare l'installazione di un sito, informarsi sui prerequisiti per l'installazione di diversi tipi di siti di Configuration Manager.


## <a name="primary-sites-and-the-central-administration-site"></a>Siti primari e sito di amministrazione centrale

I prerequisiti seguenti si applicano all'installazione di uno dei tipi seguenti:

- Un sito di amministrazione centrale come primo sito di una gerarchia
- Un sito primario autonomo
- Un sito primario figlio

Se si installa un sito di amministrazione centrale come parte di un'espansione della gerarchia, vedere [Espansione di un sito primario autonomo](#bkmk_expand).

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Prerequisiti per l'installazione di un sito primario o un sito di amministrazione centrale  

- Installare i ruoli, le funzionalità e i componenti di Windows Server necessari. Per altre informazioni, vedere [Prerequisiti del sistema del sito](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq)  

- L'account utente che installa il sito deve disporre dei diritti seguenti:  

    - **Amministratore** nei server seguenti:  
        - Server del sito  
        - Ogni server che ospita il **database del sito**  
        - Ogni istanza del **provider SMS** per il sito  

    - **Amministratore di sistema** nell'istanza di SQL Server che ospita il database del sito  

        > [!IMPORTANT]  
        > Al termine dell'installazione di Configuration Manager, l'account computer server del sito deve mantenere i diritti di amministratore di sistema di SQL Server. Non rimuovere i diritti di amministratore di sistema di SQL da questo account.  

- Quando si installa un sito primario, sono necessari i diritti aggiuntivi seguenti:  

    - **Amministratore** in altri server in cui si installano il punto di gestione iniziale e il punto di distribuzione, se non sono installati nel server del sito  

- Se si installa un nuovo sito primario figlio all'interno di un sito di amministrazione centrale, sono necessari i diritti aggiuntivi seguenti:  

    - **Amministratore** nel server che ospita il sito di amministrazione centrale  

    - Diritti di amministrazione basata su ruoli in Configuration Manager equivalenti al ruolo di sicurezza **Amministratore infrastruttura** o **Amministratore completo**  

- Usare i file di origine di installazione corretti ed eseguire il programma di installazione da tale percorso. Per informazioni sui file di origine corretti da usare per installare i diversi tipi di siti, vedere [Opzioni per l'installazione di diversi tipi di siti](prepare-to-install-sites.md#bkmk_options).  

- Il server del sito deve avere accesso ai file di installazione aggiornati offerti da Microsoft in uno dei modi seguenti:  

    - Prima di iniziare l'installazione, scaricare e archiviare una copia di questi file nella rete locale. Per altre informazioni, vedere [Setup Downloader](setup-downloader.md) (Downloader di installazione).  

    - Se non è disponibile una copia locale di questi file, il server del sito deve avere accesso a Internet. Il server scarica questi file da Microsoft durante l'installazione.  

- Il server del sito e i server di database del sito devono soddisfare tutte le configurazioni dei prerequisiti. Prima di avviare il programma di installazione di Configuration Manager, [eseguire manualmente Controllo prerequisiti](prerequisite-checker.md) per identificare e risolvere eventuali problemi.  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Prerequisiti per l'espansione di un sito primario autonomo

Un sito primario autonomo deve soddisfare i seguenti prerequisiti ai fini dell'espansione in una gerarchia con un sito di amministrazione centrale:

#### <a name="source-file-version-matches-site-version"></a>La versione dei file di origine corrisponde alla versione del sito

Installare il nuovo sito di amministrazione centrale usando i file multimediali inclusi in una cartella CD.Latest che corrisponde alla versione del sito primario autonomo. Per verificare che le versioni corrispondano, usare i file di origine presenti nella [cartella CD.Latest](../../manage/the-cd.latest-folder.md) del sito primario autonomo.

Per altre informazioni sui file di origine corretti da usare per installare siti diversi, vedere [Opzioni per l'installazione di diversi tipi di siti](prepare-to-install-sites.md#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Arrestare la migrazione attiva da un'altra gerarchia

Non è possibile configurare il sito primario autonomo per eseguire la migrazione dei dati da un'altra gerarchia di Configuration Manager. Arrestare la migrazione attiva al sito primario autonomo da altre gerarchie di Configuration Manager e rimuovere tutte le configurazioni per la migrazione. Queste configurazioni includono:

- Processi di migrazione non completati  
- Raccolta dati  
- Configurazione della gerarchia di origine attiva  

Questa configurazione è necessaria perché Configuration Manager esegue la migrazione dei dati dal sito principale della gerarchia. Quando si espande un sito primario autonomo, le configurazioni per la migrazione non vengono trasferite al sito di amministrazione centrale.  

Se si riconfigura la migrazione nel sito primario dopo l'espansione del sito primario autonomo, le operazioni di migrazione vengono eseguite dal sito di amministrazione centrale.

Per altre informazioni sulla configurazione della migrazione, vedere [Configurare gerarchie di origine e siti di origine per la migrazione](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

#### <a name="computer-account-as-administrator"></a>Account del computer come amministratore

L'account computer del server che ospita il nuovo sito di amministrazione centrale deve essere un membro del gruppo **Amministratori** nel server del sito primario autonomo.

Per espandere correttamente il sito primario autonomo, l'account computer del nuovo sito di amministrazione centrale deve avere diritti di **Amministratore** nel sito primario autonomo. Ciò è richiesto solo durante l'espansione del sito. Al termine dell'espansione del sito, è possibile rimuovere l'account dal gruppo utenti nel sito primario.  

#### <a name="installation-account-permissions"></a>Autorizzazioni dell'account di installazione

L'account utente che esegue il programma di installazione di Configuration Manager per installare il nuovo sito di amministrazione centrale deve avere i diritti di amministrazione basata su ruoli nel sito primario autonomo.

Per installare un sito di amministrazione centrale come parte di un'espansione del sito, l'account utente che esegue il programma di installazione per installare il sito di amministrazione centrale deve essere definito nell'amministrazione basata su ruoli nel sito primario autonomo come **Amministratore completo** o **Amministratore infrastruttura**.

Per altre informazioni, incluso l'elenco completo delle autorizzazioni necessarie, vedere [Account di installazione sito](../../../plan-design/hierarchy/accounts.md#site-installation-account).

#### <a name="top-level-site-roles"></a>Ruoli del sito principale

Prima di espandere il sito, disinstallare i ruoli del sistema del sito seguenti dal sito primario autonomo:

- Punto di sincronizzazione di Asset Intelligence  
- Punto di Endpoint Protection  
- punto di connessione del servizio  

Configuration Manager supporta solo questi ruoli nel sito principale della gerarchia. Disinstallare questi ruoli del sistema del sito prima di espandere il sito primario autonomo. Al termine dell'espansione, reinstallare questi ruoli del sistema del sito nel sito di amministrazione centrale.  

Tutti gli altri ruoli del sistema del sito possono rimanere installati nel sito primario.  

#### <a name="open-the-sql-server-service-broker-port"></a>Aprire la porta di SQL Server Service Broker

La porta di rete deve essere aperta per SQL Server Service Broker (SSB) tra il sito primario autonomo e il server per il sito di amministrazione centrale.  

Per replicare correttamente i dati tra un sito di amministrazione centrale e un sito primario, Configuration Manager richiede una porta aperta tra i due siti per SSB. Quando si installa un sito di amministrazione centrale e si espande un sito primario autonomo, il controllo dei prerequisiti non verifica che la porta specificata per SSB sia aperta nel sito primario.  

#### <a name="known-issues-with-azure-services"></a>Problemi noti con i servizi di Azure

Dopo aver espanso il sito è necessario riconfigurare i servizi di Azure seguenti con Configuration Manager:

- [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  
- [Microsoft Store per le aziende](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Gateway di gestione cloud](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

Nella versione 1806 e successive rinnovare la chiave privata del tenant di Azure Active Directory. Per altre informazioni, vedere [Rinnovare la chiave privata](../configure/azure-services-wizard.md#bkmk_renew).

In alternativa, rimuovere e quindi ricreare la connessione al servizio:

1. Nella console di Configuration Manager eliminare il servizio di Azure dal nodo **Servizi di Azure**.  

2. Nel portale di Azure eliminare il tenant associato al servizio dal nodo dei tenant di Azure Active Directory. Questa azione elimina anche l'app Web di Azure AD associata al servizio.  

3. Riconfigurare la connessione al servizio di Azure per l'uso con Configuration Manager.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a> Siti secondari

Di seguito vengono elencati i prerequisiti per l'installazione di siti secondari:  

- Installare i ruoli, le funzionalità e i componenti di Windows Server necessari. Per altre informazioni, vedere [Prerequisiti del sistema del sito](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq)  

- L'amministratore che configura l'installazione del sito secondario nella console di Configuration Manager deve avere i diritti di amministrazione basata su ruoli equivalenti al ruolo di sicurezza di **Amministratore infrastruttura** o **Amministratore completo**.  

- L'account computer del sito primario padre deve essere un **amministratore** nel server del sito secondario.  

- Quando il sito secondario usa un'istanza di SQL Server installata in precedenza per ospitare il database del sito secondario:  

    - L'account computer del sito primario padre deve avere i diritti di **amministratore di sistema** per l'istanza di SQL Server nel server del sito secondario.  

    - L'account di **sistema locale** del computer server del sito secondario deve avere i diritti di **amministratore di sistema** per l'istanza di SQL Server nel server del sito secondario.  

        > [!IMPORTANT]  
        > Al termine dell'installazione di Configuration Manager, entrambi gli account devono mantenere diritti di amministratore di sistema per SQL Server. Non rimuovere i diritti di amministratore di sistema da questi account.  

- Il server del sito secondario deve soddisfare tutte le configurazioni dei prerequisiti. Queste configurazioni includono i ruoli del sistema del sito predefiniti e di SQL Server del punto di gestione e del punto di distribuzione.  


## <a name="next-steps"></a>Passaggi successivi

Dopo aver verificato i prerequisiti, si è pronti per eseguire il programma di installazione. Per altre informazioni, vedere [Usare l'installazione guidata per installare i siti di Configuration Manager](use-the-setup-wizard-to-install-sites.md).
