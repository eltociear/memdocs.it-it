---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Usare Deployment Monitoring Tool per risolvere i problemi di distribuzione del software in un client di Configuration Manager.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707829"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*Si applica a: Configuration Manager (Current Branch)*

Deployment Monitoring Tool è uno [strumento di Configuration Manager](tools.md). È un'interfaccia utente grafica progettata per assistere nella risoluzione dei problemi dell'applicazione, negli aggiornamenti software e nelle distribuzioni della linea di base di configurazione in un client di Configuration Manager. Lo strumento è di sola lettura perché non modifica alcuno stato nel client. È possibile usarlo in modo sicuro per diagnosticare gli scenari di distribuzione comuni.


## <a name="features"></a>Caratteristiche

- Eseguirlo come amministratore per risolvere i problemi di distribuzione in un client locale.  

- Risolvere i problemi di distribuzione in un client remoto. Avviare lo strumento e connettersi a un computer remoto come amministratore.  

- Esportare in formato XML tutti i dati raccolti nello strumento. Condividere il file XML con altri utenti e usarlo come piattaforma comune per discutere della risoluzione dei problemi di distribuzione.  

- Importare i dati esportati precedentemente in un computer diverso e usarlo per eseguire lo strumento in modalità offline.   


## <a name="usage"></a>Utilizzo

Deployment Monitoring Tool supporta solo l'interfaccia utente grafica. Per avviare lo strumento, eseguire **DeploymentMonitoringTool.exe** come amministratore. Sono disponibili tre viste:  

- **Proprietà client**: elenco di attributi utili relativi al dispositivo e al client di Configuration Manager. Questa vista è quella predefinita.   

- **Distribuzioni**: visualizzazione di tutte le distribuzioni di destinazione correnti. Selezionare una distribuzione nel riquadro dei risultati per visualizzare altre informazioni nel riquadro dei dettagli.  

- **Tutti gli aggiornamenti**: visualizzazione di tutti gli aggiornamenti software e del relativo stato.  

Per copiare i dati in qualsiasi visualizzazione, selezionare una cella e premere **CTRL** + **C**.


### <a name="actions-menu"></a>Menu Azioni

Nel menu **Azioni** sono disponibili le seguenti azioni:  

- **Connect to remote machine** (Connettersi a un computer remoto): selezionare un computer a cui connettersi. Se non si specifica un nome utente e password, usa le credenziali correnti. Fare clic su **Salva** per connettersi a un computer remoto.  

- **Esporta dati**: selezionare il file in cui scrivere i dati e fare clic su **Salva**. Usare il file XML esportato per la risoluzione remota dei problemi in un computer diverso.  

- **Importa dati**: selezionare un file da importare nello strumento.  

- **Visualizza registro**: consente di aprire un file di log associato, a seconda della visualizzazione:  
    - Proprietà client: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Distribuzioni: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Tutti gli aggiornamenti: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Vedere anche

- [Distribuire applicazioni](../../apps/deploy-use/deploy-applications.md)
- [Distribuire gli aggiornamenti software](../../sum/deploy-use/deploy-software-updates.md)
- [Distribuire linee di base di configurazione](../../compliance/deploy-use/deploy-configuration-baselines.md)
