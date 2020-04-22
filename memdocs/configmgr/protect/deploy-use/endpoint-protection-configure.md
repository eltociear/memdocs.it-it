---
title: Configurare Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come configurare Configuration Manager per aggiornare e distribuire le definizioni dei malware per Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704519"
---
# <a name="configure-endpoint-protection"></a>Configurare Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*

Prima di poter usare Endpoint Protection per gestire la sicurezza e i malware nei computer client di Configuration Manager, è necessario eseguire i passaggi di configurazione descritti in questo articolo.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Come configurare Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager ha relazioni esterne e relazioni all'interno del prodotto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Passaggi per la configurazione di Endpoint Protection in Configuration Manager  
 Usare la tabella seguente per passaggi, dettagli e altre informazioni su come configurare Endpoint Protection.  

> [!IMPORTANT]  
>  Se si gestisce Endpoint Protection per i computer Windows 10, è necessario configurare Configuration Manager per aggiornare e distribuire le definizioni dei malware per Windows Defender. Windows Defender è incluso in Windows 10 ma è necessario che sia installato SCEPInstall e le impostazioni client personalizzate per Endpoint Protection (**Passaggio 5** sotto) sono comunque necessarie. </br> </br>
> A partire da Configuration Manager 1802 non è più necessario che nei dispositivi Windows 10 sia installato l'agente di Endpoint Protection (SCEPInstall). Se è già installato nei dispositivi Windows 10, Configuration Manager lo rimuoverà. Gli amministratori possono rimuovere l'agente di Endpoint Protection nei dispositivi Windows 10 che eseguono almeno la versione client 1802. È possibile che SCEPInstall.exe sia ancora presente in alcuni computer in C:\Windows\ccmsetup. Non scaricarlo nelle nuove installazioni client. Per Endpoint Protection sono ancora necessarie impostazioni client personalizzate (**Passaggio 5** riportato di seguito). <!--503654-->

|Passaggi|Dettagli|  
|-----------|-------------|  
|**Passaggio 1:** [Creare un ruolo del sistema del sito del punto di Endpoint Protection](endpoint-protection-site-role.md)|Prima di poter usare Endpoint Protection, è necessario installare il ruolo del sistema del sito Punto di Endpoint Protection. Il ruolo deve essere installato in un solo server di sistema del sito, al livello superiore della gerarchia in un sito di amministrazione centrale o un sito primario autonomo. |  
|**Passaggio 2:** [Configurare gli avvisi per Endpoint Protection](endpoint-configure-alerts.md)|Gli avvisi informano l'amministratore quando si verificano eventi specifici, ad esempio un'infezione causata da un malware. Gli avvisi vengono visualizzati nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** oppure possono essere inviati via posta elettronica a utenti specifici. |  
|**Passaggio 3:** [Configurare le origini degli aggiornamenti delle definizioni per i client di Endpoint Protection](endpoint-definition-updates.md)|È possibile configurare Endpoint Protection per usare più origini per il download degli aggiornamenti delle definizioni. |  
|**Passaggio 4:** [Configurare il criterio antimalware predefinito e creare criteri antimalware personalizzati](endpoint-antimalware-policies.md)|Il criterio antimalware predefinito viene applicato quando viene installato il client di Endpoint Protection. Eventuali criteri personalizzati distribuiti vengono applicati per impostazione predefinita, entro 60 minuti dalla distribuzione del client. Verificare di aver configurato i criteri antimalware prima di distribuire il client Endpoint Protection. |  
|**Passaggio 5:** [Configurare le impostazioni client personalizzate per Endpoint Protection](endpoint-protection-configure-client.md)|Usare impostazioni client personalizzate per configurare le impostazioni di Endpoint Protection per le raccolte di computer nella gerarchia.<br /><br /> Nota: configurare le impostazioni client predefinite per Endpoint Protection solo se si è certi di voler applicare tali impostazioni a tutti i computer nella gerarchia. |  
