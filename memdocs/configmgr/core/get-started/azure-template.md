---
title: Creare un lab in Azure
titleSuffix: Configuration Manager
description: Automatizzare la creazione di un lab di Configuration Manager Technical Preview o di un lab di valutazione del ramo corrente usando i modelli di Azure
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 23cc7d0c642637a310f53280bafed6a2a28d2834
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406680"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Creare un lab di Configuration Manager in Azure

*Si applica a: Configuration Manager (Current Branch, Technical Preview Branch)*

<!--3556017-->

Questa guida descrive come compilare un ambiente lab per Configuration Manager in Microsoft Azure. Vengono usati modelli di Azure per semplificare e automatizzare la creazione di un lab con le risorse di Azure. Sono disponibili due modelli di Azure: 

- Il modello di Azure di Configuration Manager Technical Preview installa l'ultima versione del ramo di Configuration Manager Technical Preview.
- Il modello di Azure del ramo corrente di Configuration Manager installa la valutazione della versione più recente di Configuration Manager Current Branch. 

Per altre informazioni, vedere [Configuration Manager in Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Prerequisiti

Questo processo richiede una sottoscrizione di Azure in cui è possibile creare gli oggetti seguenti: 
- Due macchine virtuali Standard_B2s per il controller di dominio, il punto di gestione e il punto di distribuzione.
- Una macchina virtuale Standard_B2ms per il server del sito primario e il server di database SQL.
- Account di archiviazione Standard_LRS

> [!Tip]  
> Per determinare i costi potenziali, vedere il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/).  



## <a name="process"></a>Processo

1. Passare al [modello di Configuration Manager Technical Preview](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) o al [modello del ramo corrente di Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Selezionare **Distribuisci in Azure**. Si aprirà il portale di Azure.  

3. Completare il modello di avvio rapido di Azure con le informazioni seguenti:

    - Informazioni di base  

        - **Sottoscrizione**: Nome della sottoscrizione in cui creare le macchine virtuali  

        - **Gruppo di risorse**: Selezionare un gruppo di risorse da usare con le macchine virtuali  

        - **Location** (Percorso): Selezionare un data center di Azure per ospitare questo ambiente lab  

    - Impostazioni  

        - **Prefisso:** : Nome del prefisso delle macchine. Per altre informazioni, vedere [Informazioni sulle macchine virtuali di Azure](#azure-vm-info).  

        - **Nome utente amministratore**: Nome di un utente nelle macchine virtuali con diritti amministrativi. Questo utente viene usato per accedere alle macchine virtuali.  

        - **Password amministratore**: La password deve soddisfare i requisiti di complessità di Azure. Per altre informazioni, vedere [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Azure richiede le impostazioni seguenti. Usare i valori predefiniti. Non modificarli.  
    > 
    > - **\_artifacts Location** (Percorso Artifacts): Percorso degli script per questo modello <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_artifacts Location Sas Token** (token SAS percorso Artifacts): Il token SAS è necessario per accedere al percorso Artifacts  
    > 
    > - **Location** (Percorso): Percorso di tutte le risorse

4. Leggere i termini e le condizioni. Se si accettano, selezionare **Accetto le condizioni riportate sopra**, quindi selezionare **Acquista** per continuare. 

Azure convalida le impostazioni e inizia la distribuzione. Controllare lo stato della distribuzione nel portale di Azure. 

> [!NOTE]
> Il processo può durare 2/4 ore. L'esecuzione degli script di configurazione continua anche quando nel portale di Azure viene specificato che la distribuzione è stata completata. Non riavviare le macchine virtuali durante il processo.

Per visualizzare lo stato degli script di configurazione, collegarsi al server `<prefix>PS1` e visualizzare il file`%windir%\TEMP\ProvisionScript\PS1.json` seguente. Se tutti i passaggi sono stati completati, il processo è terminato.

Per connettersi alle macchine virtuali, ottenere prima gli indirizzi IP pubblici per ogni macchina virtuale dal portale di Azure. Quando ci si connette alla macchina virtuale, il nome di dominio è `contoso.com`. Usare le credenziali specificate nel modello di distribuzione. Per altre informazioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informazioni sulle macchine virtuali di Azure

Le specifiche di tutte le tre macchine virtuali sono le seguenti:
- 150 GB di spazio su disco
- Sia un indirizzo IP pubblico che uno privato. Gli indirizzi IP pubblici si trovano in un gruppo di sicurezza di rete che consente solo connessioni desktop remote alla porta TCP 3389. 

Il prefisso specificato nel modello di distribuzione è il prefisso del nome della macchina virtuale. Ad esempio se si imposta il prefisso "contoso", il nome del computer del controller di dominio sarà `contosoDC`.


### `<prefix>DC01`

- Controller di dominio Active Directory
- Standard_B2s con due processori e 4 GB di memoria
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- Active Directory Domain Services (ADDS)
- .NET
- Compressione differenziale remota


### `<prefix>PS01`

- Standard_B2ms con due processori e 8 GB di memoria
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows 10 ADK con Windows PE 
- Sito primario di Configuration Manager

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- .NET
- Compressione differenziale remota 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- Standard_B2s con due processori e 4 GB di memoria
- Windows Server 2019 Datacenter Edition
- Punto di distribuzione
- Punto di gestione

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- .NET
- Compressione differenziale remota 
- Internet Information Service (IIS)
- Servizio trasferimento intelligente in background (BITS)

### `<prefix>CL01`

- Solo per il modello di valutazione del ramo corrente di Configuration Manager
- Windows 10
- Client di Configuration Manager
