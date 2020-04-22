---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come gestire i criteri antimalware e la sicurezza di Windows Firewall per i client.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b74a8c1daff31a8ffca8a38e6449aeeef1bb9b2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697179"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*

Endpoint Protection gestisce i criteri antimalware e la sicurezza di Windows Firewall per i computer client nella gerarchia di Configuration Manager.  

> [!IMPORTANT]  
>  Per gestire i client nella gerarchia di Configuration Manager è necessario avere la licenza per l'uso di Endpoint Protection.  

 L'uso di Endpoint Protection con Configuration Manager offre i vantaggi seguenti:  

-   Configurare criteri antimalware e impostazioni di Windows Firewall e gestire Microsoft Defender Advanced Threat Protection per gruppi di computer selezionati  
-   Usare gli aggiornamenti software di Configuration Manager per scaricare i file definizioni antimalware più recenti e mantenere aggiornati i computer client  
-   Inviare notifiche tramite posta elettronica, usare il monitoraggio integrato nella console e visualizzare i report. Queste azioni informano gli utenti amministratori quando viene rilevato malware nei computer client.  

A partire da Windows 10 e Windows Server 2016, Windows Defender è già installato nei computer. Per questi sistemi operativi, quando si installa il client di Configuration Manager viene installato anche un client di gestione di Windows Defender. Nei computer con Windows 8.1 e versioni precedenti, il client di Endpoint Protection viene installato con il client di Configuration Manager. Windows Defender e il client di Endpoint Protection hanno le funzionalità seguenti:  

-   Rilevamento e correzione di spyware e malware  
-   Rilevamento e correzione di rootkit  
-   Valutazione delle vulnerabilità critiche e aggiornamenti automatici del motore e delle definizioni  
-   Rilevamento delle vulnerabilità di rete con Network Inspection System  
-   Integrazione con Cloud Protection Service per segnalare malware a Microsoft. Se si partecipa a questo servizio, il client di Endpoint Protection o Windows Defender scarica le definizioni più recenti da Malware Protection Center quando in un computer viene rilevato malware non identificato.  

> [!NOTE]  
>  Il client di Endpoint Protection può essere installato in un server che esegue Hyper-V e nelle macchine virtuali guest con sistemi operativi supportati. Per evitare un uso eccessivo della CPU, le azioni di Endpoint Protection hanno un ritardo casuale predefinito che impedisce l'esecuzione contemporanea dei servizi.  

 Con Endpoint Protection nella console di Configuration Manager si gestiscono anche le impostazioni di Windows Firewall.  

 [Example scenario: uso di Endpoint Protection in System Center per proteggere i computer da malware](scenarios-endpoint-protection.md) Endpoint Protection e Windows Firewall.  


## <a name="managing-malware-with-endpoint-protection"></a>Gestione del malware con Endpoint Protection  
 Endpoint Protection in Configuration Manager consente di creare criteri antimalware che contengono impostazioni per le configurazioni del client di Endpoint Protection. Distribuire questi criteri antimalware ai computer client, quindi monitorare la conformità nel nodo **Stato Endpoint Protection** di **Sicurezza** nell'area di lavoro **Monitoraggio**. Usare anche i report di Endpoint Protection nel nodo **Report**.  

 Altre informazioni:  

-   [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md): creare, distribuire e monitorare criteri antimalware con un elenco di impostazioni da configurare  

-   [Come monitorare Endpoint Protection](monitor-endpoint-protection.md): monitoraggio dei report sull'attività, dei computer client infetti e altro.  

-   [Come gestire i criteri antimalware e le impostazioni del firewall per Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md): riparazione di malware rilevato nei computer client  

-   [File di log per Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gestione di Windows Firewall con Endpoint Protection  
 Endpoint Protection in Configuration Manager offre funzionalità di gestione di base per Windows Firewall nei computer client. Per ogni profilo di rete è possibile configurare le impostazioni seguenti:  

-   Abilitare o disabilitare Windows Firewall.  

-   Bloccare le connessioni in ingresso, comprese quelle nell'elenco dei programmi consentiti.  

-   Notificare all'utente quando Windows Firewall blocca un nuovo programma.  

> [!NOTE]  
>  Endpoint Protection supporta solo la gestione di Windows Firewall.  


 Per altre informazioni, vedere [Creare e distribuire criteri di Windows Firewall per Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection esegue la gestione e il monitoraggio di Microsoft Defender Advanced Threat Protection (ATP), denominato in precedenza Windows Defender ATP. Il servizio Microsoft Defender ATP consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti aziendali. Per altre informazioni, vedere [Microsoft Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flusso di lavoro di Endpoint Protection  
 Vedere il diagramma seguente per capire il flusso di lavoro per l'implementazione di Endpoint Protection nella gerarchia di Configuration Manager.  

 ![Flusso di lavoro di Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Client di Endpoint Protection per computer Mac e server Linux  

> [!Important]  
> Il supporto di System Center Endpoint Protection (SCEP) per Mac e Linux (tutte le versioni) termina il 31 dicembre 2018. La disponibilità di nuove definizioni di virus per SCEP per Mac e SCEP per Linux potrebbe essere sospesa alla fine del supporto. Per altre informazioni, vedere il [post del blog sulla fine del supporto](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection include un client di Endpoint Protection per Linux e per i computer Mac. Questi client non sono inclusi in Configuration Manager. Scaricare i prodotti seguenti da [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx):  

-   System Center Endpoint Protection per Mac  

-   System Center Endpoint Protection per Linux  


> [!Note]  
>  Per scaricare i file di installazione di Endpoint Protection per Linux e Mac occorre essere titolari di un contratto multilicenza Microsoft.  

 Questi prodotti non possono essere gestiti dalla console di Configuration Manager. Con i file di installazione viene fornito un Management Pack di System Center Operations Manager che consente di gestire il client per Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Come ottenere il client di Endpoint Protection per computer Mac e server Linux

Usare questa procedura per scaricare il file di immagine contenente il software client di Endpoint Protection e la documentazione per computer Mac e server Linux.
1. Accedere al [Centro servizi per contratti multilicenza](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selezionare la scheda  **Download e codici** in alto nel sito Web.
3. Filtrare in base al prodotto **System Center Endpoint Protection (Current Branch)** .
4. Fare clic sul collegamento **Download**.
5. Fare clic su **Continue**. Dovrebbero essere visualizzati vari file, tra i quali uno con il nome **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**.
6. Per scaricare il file, fare clic sull'icona a forma di freccia. Il nome del file è **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

Questo aggiornamento di febbraio 2018 (X21-67050) include le versioni seguenti:

- System Center Endpoint Protection per Mac 4.5.32.0 (supporto per macOS 10.13 High Sierra)
- System Center Endpoint Protection per Linux 4.5.20.0 

  Per altre informazioni su come installare e gestire i client di Endpoint Protection per i computer Mac e Linux, usare la documentazione di accompagnamento di questi prodotti. Tale documentazione si trova nella cartella **Documentation** del file ISO.
