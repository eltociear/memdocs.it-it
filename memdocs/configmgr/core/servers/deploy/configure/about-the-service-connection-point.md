---
title: punto di connessione del servizio
titleSuffix: Configuration Manager
description: Informazioni sul ruolo di sistema del sito di Configuration Manager e pianificazione della gamma di usi.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704949"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Informazioni sul punto di connessione del servizio in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il punto di connessione del servizio è un ruolo del sistema del sito che svolge diverse funzioni importanti per la gerarchia. Prima di configurare il punto di connessione del servizio, esaminare e pianificare i diversi usi. La pianificazione dell'utilizzo potrebbe influire sulla modalità di configurazione di questo ruolo del sistema del sito:

- Scaricare gli aggiornamenti applicabili all'infrastruttura di Configuration Manager: vengono resi disponibili solo gli aggiornamenti rilevanti per l'infrastruttura, in base ai dati di utilizzo caricati.

- Caricare i dati di utilizzo dall'infrastruttura di Configuration Manager: è possibile controllare il livello di dettaglio dei dati caricati. Per altre informazioni, vedere [Impostazioni e livelli per i dati di utilizzo](../install/setup-reference.md#bkmk_usage).

- Distribuire un'istanza di [Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md) in Azure

- Sincronizzare le app da [Microsoft Store per le aziende e la formazione](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Individuare utenti e gruppi in [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc)

- Usare [Desktop Analytics](../../../../desktop-analytics/overview.md) per ottenere informazioni dettagliate sull'aggiornamento e l'idoneità delle app per Windows 10

Ogni gerarchia supporta una sola istanza di questo ruolo. Può essere installato solo nel sito di livello più alto della gerarchia, ovvero in un sito di amministrazione centrale (CAS) o in un sito primario autonomo. Se si espande un sito primario autonomo in una gerarchia più ampia, disinstallare questo ruolo dal sito primario e quindi installarlo nel CAS.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a> Modalità di funzionamento

Il punto di connessione del servizio supporta due modalità di funzionamento:

- **Online**: il punto di connessione del servizio controlla automaticamente ogni 24 ore se sono presenti aggiornamenti. Scarica quindi i nuovi aggiornamenti disponibili per la versione corrente del prodotto e dell'infrastruttura, rendendoli disponibili nella console di Configuration Manager.

- **Offline**: il punto di connessione del servizio non si connette al servizio cloud Microsoft. Per importare manualmente gli aggiornamenti disponibili, usare lo [strumento di connessione del servizio](../../manage/use-the-service-connection-tool.md).

### <a name="change-mode"></a>Cambia modalità

Se si passa dalla modalità online a quella offline o viceversa dopo aver installato il punto di connessione del servizio, riavviare il thread **SMS_DMP_DOWNLOADER** del servizio SMS_Executive. Il riavvio di questo thread rende effettiva la modifica. Per riavviare questo thread, usare Configuration Manager Service Manager.

> [!TIP]
> È anche possibile riavviare il servizio SMS_Executive per Configuration Manager che riavvia la maggior parte dei componenti del sito. In alternativa, attendere l'esecuzione di un'attività pianificata, ad esempio un backup del sito che arresta e riavvia il servizio SMS_Executive.

Per usare Configuration Manager Service Manager per riavviare il thread SMS_DMP_DOWNLOADER:

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Stato componente**. Nella barra multifunzione scegliere **Avvia** e quindi selezionare **Configuration Manager Service Manager**.

1. Nel riquadro di spostamento di Service Manager espandere il sito, quindi espandere **Componenti** e infine scegliere il componente da riavviare: **SMS_DMP_DOWNLOADER**.

1. Passare al menu **Componente** e scegliere **Query**.

1. Confermare lo stato corrente del componente. Passare quindi al menu **Componente** e scegliere **Arresta**.  

1. Ripetere la **query** sul componente per verificare che sia stato arrestato. Scegliere quindi l'azione del componente **Avvia** per riavviarlo.

## <a name="remote-site-system-requirements"></a>Requisiti del sistema del sito remoto

Quando si installa il punto di connessione del servizio in un server del sistema del sito remoto rispetto al server del sito, configurare i requisiti seguenti:

- L'account computer del server del sito deve essere un amministratore locale sul computer che ospita un punto di connessione del servizio remoto.

- Configurare il server del sistema del sito che ospita questo ruolo con un [account di installazione del sistema del sito](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). Il responsabile della distribuzione nel server del sito usa l'account di installazione del sistema del sito per trasferire gli aggiornamenti dal punto di connessione del servizio.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a> Requisiti per l'accesso a Internet

Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, è necessario consentire al punto di connessione del servizio di accedere agli endpoint Internet.

Per altre informazioni, vedere i [requisiti di accesso Internet](../../../plan-design/network/internet-endpoints.md#bkmk_scp).

## <a name="install"></a>Installazione

Quando si esegue il **programma di installazione** per installare il sito di livello superiore di una gerarchia, è possibile installare il punto di connessione del servizio.

Al termine dell'installazione o se si reinstalla il ruolo, usare l'**Aggiunta guidata ruoli del sistema del sito** o la **Creazione guidata server del sistema sito** (installare solo il punto di connessione del servizio nel sito di livello superiore della gerarchia). Per altre informazioni, vedere [Installare i ruoli del sistema del sito](install-site-system-roles.md).

## <a name="move-the-role"></a><a name="bkmk_move"></a> Spostare il ruolo

<!-- SCCMDocs#922 -->
Esistono diversi scenari in cui potrebbe essere necessario spostare il punto di connessione del servizio in un altro server:

- [Ripristino](../../manage/recover-sites.md)
- [Disponibilità elevata del server del sito](site-server-high-availability.md)
- [Espansione del sito](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Dopo aver spostato il punto di connessione del servizio, verificare il funzionamento del sito. Ad esempio, potrebbe essere necessario rinnovare la chiave privata per le connessioni ai tenant di Azure Active Directory (Azure AD). Per altre informazioni, vedere [Rinnovare la chiave privata](azure-services-wizard.md#bkmk_renew).

## <a name="log-files"></a>File di registro

Per visualizzare informazioni sui caricamenti in Microsoft, visualizzare **Dmpuploader.log** nel server che esegue il punto di connessione del servizio. Per lo stato di avanzamento dei download degli aggiornamenti, visualizzare **Dmpdownloader.log**. Per l'elenco completo dei log correlati al punto di connessione del servizio, vedere [File di log - Punto di connessione del servizio](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog).

## <a name="next-steps"></a>Passaggi successivi

Usare i diagrammi di flusso seguenti per comprendere il flusso del processo e le voci di log chiave. Questo processo include i download degli aggiornamenti e la replica degli aggiornamenti in altri siti.

- [Diagramma di flusso - scaricare gli aggiornamenti](../../manage/download-updates-flowchart.md)

- [Diagramma di flusso - replica di aggiornamento](../../manage/update-replication-flowchart.md)
