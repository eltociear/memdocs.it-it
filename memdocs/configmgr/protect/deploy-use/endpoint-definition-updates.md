---
title: Configurare gli aggiornamenti delle definizioni
titleSuffix: Configuration Manager
description: Informazioni su come selezionare e configurare metodi con Endpoint Protection in Configuration Manager per mantenere aggiornate le definizioni antimalware nei computer client.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697349"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Configurare gli aggiornamenti delle definizioni per Endpoint Protection  

*Si applica a: Configuration Manager (Current Branch)*

 Con Endpoint Protection in Configuration Manager è possibile usare uno dei vari metodi disponibili per mantenere aggiornate le definizioni antimalware nei computer client della gerarchia. Le informazioni in questo argomento possono essere utili per scegliere questi metodi e configurarli.

 Per aggiornare le definizioni antimalware, è possibile usare uno o più dei metodi seguenti:

- [Aggiornamenti distribuiti da Configuration Manager](endpoint-definitions-configmgr.md): questo metodo usa gli aggiornamenti software di Configuration Manager per recapitare aggiornamenti del motore e delle definizioni ai computer della gerarchia.

- [Aggiornamenti distribuiti da Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md): questo metodo usa l'infrastruttura di WSUS per recapitare aggiornamenti del motore e delle definizioni ai computer.

- [Aggiornamenti distribuiti da Microsoft Update](endpoint-definitions-microsoft-updates.md): questo metodo consente ai computer di connettersi direttamente a Microsoft Update per scaricare gli aggiornamenti del motore e delle definizioni. Questo metodo può essere utile per i computer che spesso non sono connessi alla rete aziendale.

- [Aggiornamenti distribuiti da Microsoft Malware Protection Center](endpoint-definitions-protection-center.md): questo metodo scarica gli aggiornamenti delle definizioni da Microsoft Malware Protection Center.

- [Aggiornamenti dalle condivisioni file UNC](endpoint-definitions-network.md): con questo metodo è possibile salvare gli aggiornamenti più recenti del motore e delle definizioni in una condivisione in rete. I client possono quindi accedere alla rete per installare gli aggiornamenti.

  È possibile configurare più origini degli aggiornamenti delle definizioni e controllare l'ordine in cui vengono valutate e applicate. Questa operazione può essere eseguita nella finestra di dialogo **Configura origini aggiornamenti definizioni** quando si crea un criterio antimalware.

> [!IMPORTANT]
>  Per i computer che eseguono Windows 10, è necessario configurare Endpoint Protection per aggiornare le definizioni di malware per Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Come configurare le origini degli aggiornamenti delle definizioni
 Usare la procedura seguente per configurare le origini degli aggiornamenti delle definizioni da usare per ogni criterio antimalware.

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection**e quindi fare clic su **Criteri antimalware**.

3.  Aprire la pagina delle proprietà relativa a **Criterio antimalware predefinito** o creare un nuovo criterio antimalware. Per altre informazioni su come creare criteri antimalware, vedere [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md).

4.  Nella sezione **Aggiornamenti dell'intelligence per la sicurezza** della finestra di dialogo delle proprietà antimalware fare clic su **Imposta origine**.
    - La sezione **Aggiornamenti delle definizioni** è stata rinominata in **Aggiornamenti dell'intelligence per la sicurezza** a partire da Configuration Manager versione 1902.

5.  Nella finestra di dialogo **Configura origini aggiornamenti definizioni** selezionare le origini da usare per gli aggiornamenti delle definizioni. È possibile fare clic su **Su** o **Giù** per modificare l'ordine in cui le origini vengono usate.

6.  Fare clic su **OK** per chiudere la finestra di dialogo **Configura origini aggiornamenti definizioni** .

## <a name="configure-endpoint-protection-definitions"></a>Configurare le definizioni di Endpoint Protection

-   [Aggiornamenti distribuiti da Configuration Manager](endpoint-definitions-configmgr.md): questo metodo usa gli aggiornamenti software di Configuration Manager per recapitare aggiornamenti del motore e delle definizioni ai computer della gerarchia.

-   [Aggiornamenti distribuiti da Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md): questo metodo usa l'infrastruttura di WSUS per recapitare aggiornamenti del motore e delle definizioni ai computer.

-   [Aggiornamenti distribuiti da Microsoft Update](endpoint-definitions-microsoft-updates.md): questo metodo consente ai computer di connettersi direttamente a Microsoft Update per scaricare gli aggiornamenti del motore e delle definizioni. Questo metodo può essere utile per i computer che spesso non sono connessi alla rete aziendale.

-   Aggiornamenti distribuiti da Microsoft Malware Protection Center: questo metodo consente di scaricare gli aggiornamenti delle definizioni da Microsoft Malware Protection Center.

-   [Aggiornamenti dalle condivisioni file UNC](endpoint-definitions-network.md): con questo metodo è possibile salvare gli aggiornamenti più recenti del motore e delle definizioni in una condivisione in rete. I client possono quindi accedere alla rete per installare gli aggiornamenti.
