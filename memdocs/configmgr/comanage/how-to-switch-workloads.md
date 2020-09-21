---
title: Trasferire i carichi di lavoro con co-gestione
titleSuffix: Configuration Manager
description: Informazioni su come passare i carichi di lavoro attualmente gestiti da Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/15/2020
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 52a08549087338d0609aafc26f2cc1b3b697d6ba
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568574"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Come trasferire i carichi di lavoro di Configuration Manager a Intune

Uno dei vantaggi della co-gestione è il trasferimento dei carichi di lavoro da Configuration Manager a Microsoft Intune. Quando un dispositivo Windows 10 ha il client di Configuration Manager ed è registrato in Intune, si ottengono i vantaggi di entrambi i servizi. È possibile stabilire per quali carichi di lavoro trasferire eventualmente l'autorità da Configuration Manager a Intune. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro che non vengono trasferiti a Intune, e tutte le altre funzionalità di Configuration Manager non supportate dalla co-gestione.

Se si trasferisce un carico di lavoro a Intune, ma in seguito si cambia idea, è possibile tornare a Configuration Manager.

Per altre informazioni sui carichi di lavoro supportati, vedere [Carichi di lavoro](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Trasferire i carichi di lavoro a partire dalla versione 1906
<!--3555750 FKA 1357954 -->
A partire dalla versione 1906, è possibile configurare raccolte pilota diverse per ognuno dei carichi di lavoro con co-gestione. La possibilità di usare raccolte pilota diverse consente di adottare un approccio più granulare durante il trasferimento dei carichi di lavoro. È possibile trasferire i carichi di lavoro quando si abilita la co-gestione o in seguito, al momento opportuno. Se non è ancora stata abilitata la co-gestione, eseguire prima di tutto questa operazione. Per altre informazioni, vedere [Come abilitare la co-gestione](how-to-enable.md). Dopo aver abilitato la co-gestione, modificare le impostazioni nelle proprietà di co-gestione.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  
2. Selezionare l'oggetto co-gestione e quindi scegliere **Proprietà** nella barra multifunzione.  
3. Passare alla scheda **Carichi di lavoro**. Per impostazione predefinita, a tutti i carichi di lavoro è applicata l'impostazione **Configuration Manager**. Per trasferire un carico di lavoro, spostare il dispositivo di scorrimento relativo al carico di lavoro sull'impostazione desiderata.  

    ![Screenshot della scheda Carichi di lavoro nella pagina delle proprietà di co-gestione](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Configuration Manager continua a gestire questo carico di lavoro.  

    - **Intune pilota**: trasferire questo carico di lavoro solo per i dispositivi nella raccolta pilota. È possibile modificare le **raccolte pilota** nella scheda **Gestione temporanea** della pagina delle proprietà di co-gestione.  

    - **Intune**: trasferire questo carico di lavoro per tutti i dispositivi Windows 10 registrati nella co-gestione.  

4. Passare alla scheda **Gestione temporanea** e modificare la **raccolta pilota** per alcuni carichi di lavoro, se necessario.
  
   ![Screenshot della scheda Gestione temporanea nella pagina delle proprietà di co-gestione](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Prima di trasferire eventuali carichi di lavoro, assicurarsi di configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.
> - A partire da Configuration Manager versione 1806, quando si trasferisce un carico di lavoro con co-gestione, i dispositivi con co-gestione sincronizzano automaticamente i criteri MDM da Microsoft Intune. <!--7087526-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Trasferire i carichi di lavoro nella versione 1902 e versioni precedenti

È possibile trasferire i carichi di lavoro quando si abilita la co-gestione o in seguito, al momento opportuno. Se non è ancora stata abilitata la co-gestione, eseguire prima di tutto questa operazione. Per altre informazioni, vedere [Come abilitare la co-gestione](how-to-enable.md). Dopo aver abilitato la co-gestione, modificare le impostazioni nelle proprietà di co-gestione.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  

2. Selezionare l'oggetto co-gestione e quindi scegliere **Proprietà** nella barra multifunzione.
   - Verrà richiesto di accedere ad Azure AD. Questa richiesta non impedisce l'aggiornamento dell'onboarding. Tuttavia, la richiesta verrà visualizzata ogni volta che si apre la pagina **Proprietà** fino a quando non si esegue l'accesso.

3. Passare alla scheda **Carichi di lavoro**. Per impostazione predefinita, a tutti i carichi di lavoro è applicata l'impostazione **Configuration Manager**. Per trasferire un carico di lavoro, spostare il dispositivo di scorrimento relativo al carico di lavoro sull'impostazione desiderata.  

    ![Screenshot della scheda Carichi di lavoro nella pagina delle proprietà di co-gestione, versione 1902](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager continua a gestire questo carico di lavoro.  

    - **Intune pilota**: trasferire questo carico di lavoro solo per i dispositivi nella raccolta pilota. È possibile modificare la **raccolta pilota** nella scheda **Gestione temporanea** della pagina delle proprietà di co-gestione.  

    - **Intune**: trasferire questo carico di lavoro per tutti i dispositivi Windows 10 registrati nella co-gestione.  

4. Nella scheda **Gestione temporanea** della pagina delle proprietà di co-gestione cambiare la **raccolta pilota** per i carichi di lavoro, se necessario.

5. Fare clic su **OK** per salvare e chiudere le proprietà di co-gestione.

> [!Important]  
> - Prima di trasferire eventuali carichi di lavoro, assicurarsi di configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi. 
> - A partire da Configuration Manager versione 1806, quando si trasferisce un carico di lavoro con co-gestione, i dispositivi con co-gestione sincronizzano automaticamente i criteri MDM da Microsoft Intune. <!--7087526-->

## <a name="next-steps"></a>Passaggi successivi

[Monitorare la co-gestione](how-to-monitor.md)
