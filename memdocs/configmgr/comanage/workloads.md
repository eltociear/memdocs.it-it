---
title: Carichi di lavoro con co-gestione
titleSuffix: Configuration Manager
description: Informazioni sui carichi di lavoro che è possibile trasferire da Configuration Manager a Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 928ef8a8ebc90807912f22901743725df9aa67e7
ms.sourcegitcommit: 79fb3b0f0486de1644904be348b7e08048e93b18
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82842224"
---
# <a name="co-management-workloads"></a>Carichi di lavoro con co-gestione

Non è obbligatorio trasferire i carichi di lavoro oppure è possibile procedere singolarmente al momento opportuno. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro che non vengono trasferiti a Intune, e tutte le altre funzionalità di Configuration Manager non supportate dalla co-gestione.

Se si trasferisce un carico di lavoro a Intune, ma in seguito si cambia idea, è possibile tornare a Configuration Manager.

La co-gestione supporta i carichi di lavoro seguenti:

- [Criteri di conformità](#compliance-policies)  

- [Criteri di Windows Update](#windows-update-policies)  

- [Criteri di accesso alle risorse](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configurazione del dispositivo](#device-configuration)  

- [App A portata di clic di Office](#office-click-to-run-apps)  

- [App client](#client-apps)  

## <a name="compliance-policies"></a>Criteri di conformità

I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. Usare tali criteri anche per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale. A partire dalla versione 1910 di Configuration Manager, è possibile aggiungere la valutazione delle linee di base di configurazione personalizzate come regola di valutazione dei criteri di conformità. Per altre informazioni, vedere [Includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Per altre informazioni sulla funzionalità Intune, vedere [Criteri di conformità dei dispositivi](https://docs.microsoft.com/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Criteri di Windows Update

I criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende.

Per altre informazioni sulla funzionalità Intune, vedere [Configurare i criteri di rinvio di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Criteri di accesso alle risorse

I criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi.

Per altre informazioni sulla funzionalità Intune, vedere [Distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> Il carico di lavoro di accesso alle risorse fa parte anche della configurazione del dispositivo. Questi criteri vengono gestiti da Intune quando si passa al carico di lavoro [Configurazione del dispositivo](#device-configuration).

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

Il carico di lavoro di Endpoint Protection include l'insieme di funzionalità di protezione antimalware di Windows Defender:

- Windows Defender Antimalware
- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Crittografia di Windows
- Windows Defender Exploit Guard  
- Controllo delle applicazioni di Windows Defender  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection (ora denominato Microsoft Defender Threat Protection)

Per altre informazioni sulla funzionalità Intune, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> Quando si passa a questo carico di lavoro, i criteri di Configuration Manager vengono mantenuti nel dispositivo fino a quando non vengono sovrascritti dai criteri di Intune. Questo comportamento garantisce che il dispositivo abbia i criteri di protezione anche durante la transizione.
>
> Il carico di lavoro Endpoint Protection fa parte anche della configurazione del dispositivo. Lo stesso comportamento si applica quando si passa al carico di lavoro [Configurazione del dispositivo](#device-configuration).<!-- SCCMDocs.nl-nl issue #4 --> Quando si passa al carico di lavoro di configurazione del dispositivo, sono inclusi anche i criteri per la funzionalità Information Protection di Windows, che non è inclusa nel carico di lavoro di Endpoint Protection.<!-- 4184095 -->
>
> Le impostazioni di Microsoft Defender antivirus che fanno parte del tipo di profilo Limitazioni del dispositivo per la configurazione del dispositivo Intune non sono incluse nell'ambito del dispositivo di scorrimento Endpoint Protection. Per gestire Microsoft Defender Antivirus per i dispositivi con co-gestione con il dispositivo di scorrimento Endpoint Protection abilitato, usare i nuovi criteri antivirus in **Interfaccia di amministrazione di Microsoft Endpoint Manager** > **Endpoint Security** > **Antivirus**. Per il nuovo tipo di criteri sono disponibili opzioni nuove e migliorate e sono supportate tutte le stesse impostazioni disponibili nel profilo Limitazioni del dispositivo. <!--6609171-->
>
> La funzionalità Crittografia di Windows include la gestione di BitLocker. Per altre informazioni sul comportamento di questa funzionalità con la co-gestione, vedere [Distribuire la gestione di BitLocker](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Configurazione del dispositivo

<!--1357903-->

Il carico di lavoro di configurazione dei dispositivi include le impostazioni gestite per i dispositivi dell'organizzazione. Trasferendo questo carico di lavoro vengono spostati anche i carichi di lavoro **Accesso alla risorsa** ed **Endpoint Protection**.

È comunque possibile continuare a distribuire le impostazioni da Configuration Manager ai dispositivi con co-gestione, anche se Intune è l'autorità di configurazione del dispositivo. Questa eccezione può essere usata per configurare le impostazioni richieste dall'organizzazione, ma non ancora disponibili in Intune. Specificare questa eccezione in una [linea di base di configurazione di Configuration Manager](../compliance/deploy-use/create-configuration-baselines.md). Abilitare l'opzione **Applica sempre questa baseline anche per client con co-gestione** quando si crea la baseline. È possibile modificarla in un secondo momento nella scheda **Generale** delle proprietà di una baseline esistente.  

Per altre informazioni sulla funzionalità Intune, vedere [Creare un profilo di dispositivo in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  

> [!NOTE]
> Quando si passa al carico di lavoro di configurazione del dispositivo, sono inclusi anche i criteri per la funzionalità Information Protection di Windows, che non è inclusa nel carico di lavoro di Endpoint Protection.<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>App A portata di clic di Office

<!--1357841-->

Questo carico di lavoro consente di gestire le app di Office 365 nei dispositivi con co-gestione.

- Dopo lo spostamento del carico di lavoro, l'app viene visualizzata nel **portale aziendale** sul dispositivo  

- Gli aggiornamenti di Office possono richiedere circa 24 ore prima di essere visualizzati nei client, a meno che i dispositivi non vengano riavviati  

- È disponibile una nuova condizione globale che determina se **le applicazioni di Office 365 sono gestite da Intune nel dispositivo**. Questa condizione viene aggiunta per impostazione predefinita come requisito alle nuove applicazioni di Office 365. Durante la transizione di questo carico di lavoro, i client in co-gestione non soddisfano il requisito relativo all'applicazione. Non installano quindi Office 365 distribuito da Configuration Manager.  

Per altre informazioni sulla funzionalità Intune, vedere [Assegnare le app di Office 365 ai dispositivi Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

## <a name="client-apps"></a>App client

<!--1357892-->

Usare Intune per gestire le app client e gli script di PowerShell in dispositivi Windows 10 con co-gestione. Dopo la transizione di questo carico di lavoro, qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale. Le app distribuite da Configuration Manager sono disponibili in Software Center.

Per altre informazioni sulla funzionalità Intune, vedere [Informazioni sulla gestione delle app in Microsoft Intune](https://docs.microsoft.com/intune/app-management).

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1806 come [funzionalità di una versione non definitiva](../core/servers/manage/pre-release-features.md). A partire dalla versione 2002, non è più una funzionalità di versione non definitiva.  
>
> Questa funzionalità può essere visualizzata nell'elenco di funzionalità come **App per dispositivi mobili per dispositivi con co-gestione**.<!-- 5849669 -->

A partire dalla versione 1910, quando si abilita Microsoft Connected Cache nei punti di distribuzione di Configuration Manager, questi possono essere usati per gestire le app Win32 di Microsoft Intune nei client con co-gestione. Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Diagramma per i carichi di lavoro delle app

![Diagramma dei carichi di lavoro delle app di co-gestione](media/co-management-apps.svg)

[Visualizzare il diagramma per intero](media/co-management-apps.svg)

## <a name="known-issues"></a>Problemi noti

Quando il carico di lavoro Endpoint Protection viene spostato in Intune, il client può comunque rispettare i criteri impostati da Configuration Manager e Microsoft Defender. <!--5024559-->

Per risolvere questo problema, applicare CleanUpPolicy.xml usando ConfigSecurityPolicy.exe dopo che i criteri di Intune sono stati ricevuti dal client, usando la procedura seguente:

1. Copiare il testo seguente e salvarlo come `CleanUpPolicy.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. Aprire un prompt dei comandi con privilegi elevati in `ConfigSecurityPolicy.exe`. Questo file eseguibile si trova in genere in una delle directory seguenti:
   - C:\Programmi\Windows Defender
   - C:\Programmi\Microsoft Security Client
1. Al prompt dei comandi passare il file xml per pulire i criteri. Ad esempio, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`  

## <a name="next-steps"></a>Passaggi successivi

[Come trasferire i carichi di lavoro](how-to-switch-workloads.md)  
