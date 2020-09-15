---
title: Pianificare per Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
description: Pianificare i criteri antimalware e la sicurezza di Windows Firewall
ms.openlocfilehash: 2e3904b7b7232e92fd4a246d2e0519ef32fb67f6
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606842"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Pianificazione per Endpoint Protection in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


Endpoint Protection in Configuration Manager consente di gestire i criteri antimalware e la sicurezza di Windows Firewall per i computer client nella gerarchia di Configuration Manager.  

> [!IMPORTANT]  
>  Per gestire i client nella gerarchia di Configuration Manager è necessario avere la licenza per l'uso di Endpoint Protection.  

L'uso di Endpoint Protection con Configuration Manager offre i vantaggi seguenti:  

-   Configurare criteri antimalware e impostazioni di Windows Firewall e gestire Microsoft Defender Advanced Threat Protection per gruppi di computer selezionati  

-   Usare gli aggiornamenti software di Configuration Manager per scaricare i file definizioni antimalware più recenti e mantenere aggiornati i computer client  

-   Inviare notifiche di posta elettronica, usare il monitoraggio integrato nella console e visualizzare report per mantenere gli utenti amministratori informati quando viene rilevato malware nei computer client  

I computer Windows 10 non richiedono client aggiuntivi per la gestione di Endpoint Protection. In computer con Windows 8.1 e versioni precedenti, viene installato il client di Endpoint Protection oltre al client di Configuration Manager. Il client di Endpoint Protection ha le funzionalità seguenti:  

-   Rilevamento e correzione di spyware e malware  

-   Rilevamento e correzione di rootkit  

-   Valutazione delle vulnerabilità critiche e aggiornamenti automatici del motore e delle definizioni  

-   Rilevamento delle vulnerabilità di rete con Network Inspection System  

-   Integrazione con Cloud Protection Service per segnalare malware a Microsoft. Se si partecipa a questo servizio, il client di Endpoint Protection o Windows Defender può scaricare le definizioni più recenti da Malware Protection Center se in un computer viene rilevato malware non identificato.  

> [!NOTE]  
>  Il client di Endpoint Protection può essere installato in un server che esegue Hyper-V e nelle macchine virtuali guest con sistemi operativi supportati. Per evitare un utilizzo eccessivo della CPU, le azioni di Endpoint Protection hanno un ritardo casuale predefinito che impedisce l'esecuzione contemporanea dei servizi.  

  Endpoint Protection in Configuration Manager consente anche di gestire le impostazioni di Windows Firewall nella console di Configuration Manager.  

 [Example scenario: uso di Endpoint Protection in System Center per proteggere i computer da malware ](../deploy-use/scenarios-endpoint-protection.md) illustra come si può configurare e gestire Endpoint Protection e Windows Firewall.  

## <a name="managing-malware-with-endpoint-protection"></a>Gestione del malware con Endpoint Protection  

Endpoint Protection in Configuration Manager consente di creare criteri antimalware che contengono impostazioni per le configurazioni del client di Endpoint Protection. È quindi possibile distribuire tali criteri antimalware nei computer client e monitorarli nel nodo **Stato di Endpoint Protection** dell'area di lavoro **Monitoraggio** oppure usando i report di Configuration Manager.  

 Altre informazioni:  

-   [Creare e distribuire criteri antimalware per Endpoint Protection](../deploy-use/endpoint-antimalware-policies.md): creare, distribuire e monitorare criteri antimalware con un elenco di impostazioni da configurare  

-   [Monitorare Endpoint Protection](../deploy-use/monitor-endpoint-protection.md): monitoraggio dei report sull'attività, dei computer client infetti e altro.   

-   [Gestire criteri antimalware e impostazioni del firewall per Endpoint Protection](../deploy-use/endpoint-antimalware-firewall.md): è possibile modificare la priorità dei criteri per [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) o [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [correggere i malware trovati nei computer client](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware) e altre attività

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gestione di Windows Firewall con Endpoint Protection  
 Endpoint Protection in Configuration Manager offre funzionalità di gestione di base per Windows Firewall nei computer client. Per ogni profilo di rete è possibile configurare le impostazioni seguenti:  

-   Abilitare o disabilitare Windows Firewall.  

-   Bloccare le connessioni in ingresso, comprese quelle nell'elenco dei programmi consentiti.  

-   Notificare all'utente quando Windows Firewall blocca un nuovo programma.  

> [!NOTE]  
>  Endpoint Protection supporta solo la gestione di Windows Firewall.  

  Per altre informazioni su come creare e distribuire i criteri di Windows Firewall per Endpoint Protection, vedere [Come creare e distribuire criteri di Windows Firewall per Endpoint Protection](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

A partire dalla versione 1606 di Configuration Manager (Current Branch), Endpoint Protection consente di gestire e monitorare Microsoft Defender Advanced Threat Protection (ATP), noto in precedenza come Windows Defender ATP. Microsoft Defender ATP è un servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti. Vedere [Microsoft Defender Advanced Threat Protection](../deploy-use/defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flusso di lavoro di Endpoint Protection  
 Vedere il diagramma seguente per capire il flusso di lavoro per l'implementazione di Endpoint Protection nella gerarchia di Configuration Manager.  

 ![Flusso di lavoro di Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Client di Endpoint Protection per computer Mac e server Linux  
 System Center include un client di Endpoint Protection per Linux e per i computer Mac. Questi client non vengono installati con Configuration Manager. È necessario invece scaricare i prodotti seguenti da [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Per scaricare i file di installazione di Endpoint Protection per Linux e Mac occorre essere titolari di un contratto multilicenza Microsoft.  

 Questi prodotti non possono essere gestiti dalla console di Configuration Manager. Con i file di installazione, tuttavia, viene fornito un Management Pack di System Center Operations Manager, che consente di gestire il client per Linux usando Operations Manager.  

 Per altre informazioni su come installare e gestire i client di Endpoint Protection per i computer Mac e Linux, usare la documentazione di accompagnamento di questi prodotti, disponibile nella cartella **Documentazione** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Procedure consigliate per Endpoint Protection in Configuration Manager  
 Usare le procedure consigliate seguenti per Endpoint Protection in System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurare le impostazioni client personalizzate per Endpoint Protection  
 Quando si configurano le impostazioni client per Endpoint Protection, non usare le impostazioni client predefinite perché applicano le impostazioni a tutti i computer nella gerarchia. Al contrario, configurare le impostazioni client personalizzate e assegnare queste impostazioni a raccolte di computer nella gerarchia.  

 Quando si configurano le impostazioni client personalizzate, è possibile effettuare le operazioni seguenti:  

-   Personalizzare le impostazioni antimalware e sicurezza per le diverse parti dell'organizzazione.  
-   Testare gli effetti dell'esecuzione Endpoint Protection in un piccolo gruppo di computer prima di distribuirlo all'intera gerarchia.  
-   Aggiungere successivamente più client per cadenzare la distribuzione del client di Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribuire gli aggiornamenti delle definizioni tramite gli aggiornamenti software  
 Se si usano gli aggiornamenti software di Configuration Manager per distribuire gli aggiornamenti delle definizioni, è consigliabile inserirli in un pacchetto che non contenga altri aggiornamenti software. In questo modo le dimensioni del pacchetto di aggiornamento definizione più piccoli che consente la replica nei punti di distribuzione più rapidamente.
