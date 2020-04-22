---
title: Configurare l'inventario software
titleSuffix: Configuration Manager
description: Configurare l'inventario software ed escludere cartelle dall'inventario software in Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74436eb95166ae9bc78d7ae22881b709349bf847
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695439"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Come configurare l'inventario software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questa procedura consente di configurare le impostazioni client predefinite per l'inventario software e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta. Per altre informazioni su come creare le impostazioni personalizzate del dispositivo, vedere [Come configurare le impostazioni client](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Per configurare l'inventario software  

1. Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** **Impostazioni client predefinite**.  

2. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

3. Nella finestra di dialogo **Impostazioni predefinite** scegliere **Inventario software**.  

4. Nell'elenco **Impostazioni dispositivo** configurare i valori seguenti:  

   -   **Abilitare inventario software nei client**: selezionare **Vero** dall'elenco a discesa.  

   -   **Pianificare inventario software e raccolta file**: consente di configurare l'intervallo di raccolta di file e inventario software da parte dei client.   

5. Configurare le impostazioni client necessarie. La sezione [Inventario software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) nell'articolo [Informazioni sulle impostazioni client](../../../../core/clients/deploy/about-client-settings.md) contiene un elenco delle impostazioni client.  

   I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per iniziare il recupero dei criteri per un singolo client, vedere [Come gestire i client](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Il codice di errore 80041006 in inventoryprovider.log significa che il provider WMI ha esaurito la memoria. Ciò significa che è stato raggiunto il limite di quota di memoria per un provider e il provider di inventario non può continuare.
   > In questo caso, l'agente di inventario crea un report con 0 voci in modo che non venga segnalato alcun articolo di inventario. <br/>
   > Una possibile soluzione per questo errore è ridurre l'ambito della raccolta inventario software. Nelle circostanze in cui l'errore si verifica dopo la limitazione dell'ambito di inventario, una soluzione può essere aumentare la proprietà [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) definita nella classe[_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671).

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Per escludere cartelle dall'inventario software  

1.  Usando Notepad.exe, creare un file vuoto denominato **Skpswi.dat**.  

2.  Fare clic con il pulsante destro del mouse sul file **Skpswi.dat** e quindi scegliere **Proprietà**. Nelle proprietà per il file Skpswi.dat selezionare l'attributo **Hidden** .  

3.  Inserire il file **Skpswi.dat** nella radice di ogni disco rigido o struttura di cartelle del client che si vuole escludere dall'inventario software.  

> [!NOTE]  
>  L'inventario software non effettua l'inventario dell'unità del client a meno che questo file non venga eliminato dall'unità nel computer client.
