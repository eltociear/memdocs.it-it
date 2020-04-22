---
title: Proteggere i computer dal malware
titleSuffix: Configuration Manager
description: Informazioni su come implementare Endpoint Protection in Configuration Manager per proteggere i computer da attacchi malware.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706419"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Scenario di esempio: Usare Endpoint Protection per proteggere i computer dal malware

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra uno scenario d'esempio di implementazione di Endpoint Protection in Configuration Manager per proteggere i computer dell'organizzazione da attacchi malware.  



## <a name="scenario-overview"></a>Panoramica dello scenario

 Configuration Manager è installato e usato presso la Woodgrove Bank. La banca attualmente usa System Center Endpoint Protection per proteggere i computer dagli attacchi malware. Inoltre, la banca usa Criteri di gruppo di Windows per garantire che Windows Firewall sia abilitato in tutti i computer dell'azienda e che venga visualizzata una notifica agli utenti quando Windows Firewall blocca un nuovo programma.  

Agli amministratori di Configuration Manager è stato chiesto di aggiornare il software antimalware di Woodgrove Bank con System Center Endpoint Protection, in modo che la banca possa trarre vantaggio dalle funzionalità antimalware più recenti e sia in grado di gestire in modo centralizzato la soluzione antimalware dalla console di Configuration Manager. 


## <a name="business-requirements"></a>Requisiti aziendali

Questa implementazione presenta i requisiti seguenti:  

- Usare Configuration Manager per gestire le impostazioni di Windows Firewall che sono attualmente gestite tramite i criteri di gruppo.  

- Usare gli aggiornamenti software di Configuration Manager per scaricare le definizioni malware nei computer. Se gli aggiornamenti software non sono disponibili, ad esempio se il computer non è connesso alla rete aziendale, i computer devono scaricare gli aggiornamenti delle definizioni da Microsoft Update.  

- I computer degli utenti devono eseguire un'analisi rapida del malware ogni giorno. I server devono invece eseguire un'analisi completa ogni sabato, fuori dall'orario lavorativo, alle ore 1:00.  

- Inviare un messaggio di avviso ogni volta che si verifica uno dei seguenti eventi:  

  -   Viene rilevato malware su qualsiasi computer  

  -   Viene rilevata la stessa minaccia di tipo malware in più del 5% dei computer  

  -   Viene rilevata la stessa minaccia di tipo malware più di 5 volte nell'arco di 24 ore  

  -   Vengono rilevati più di 3 tipi diversi di malware nell'arco di 24 ore  

  A questo punto gli amministratori eseguono la procedura seguente per implementare Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a>Passaggi per l'implementazione di Endpoint Protection  

|Processo|Riferimento|  
|-------------|---------------|  
|Gli amministratori rivedono le informazioni disponibili sui concetti di base per Endpoint Protection in Configuration Manager.|Per informazioni generali su Endpoint Protection, vedere [Endpoint Protection](endpoint-protection.md).|  
|Gli amministratori esaminano e implementano i prerequisiti necessari per l'uso di Endpoint Protection.|Per informazioni sui prerequisiti per Endpoint Protection, vedere [Pianificazione di Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|Gli amministratori installano il ruolo di sistema del sito di Endpoint Protection in un solo server di sistema del sito, nella parte superiore della gerarchia di Woodgrove Bank.|Per altre informazioni su come installare il ruolo di sistema del sito di Endpoint Protection, vedere "Prerequisiti" in [Configurare Endpoint Protection](endpoint-protection-configure.md).|  
|Gli amministratori configurano Configuration Manager per l'uso di un server SMTP per l'invio degli avvisi di posta elettronica.<br /><br /> **Nota:** è necessario configurare un server SMTP solo se si vuole ricevere una notifica tramite posta elettronica quando viene generato un avviso di Endpoint Protection.|Per altre informazioni, vedere [Configurare gli avvisi in Endpoint Protection](endpoint-configure-alerts.md).|  
|Gli amministratori creano una raccolta di dispositivi che contiene tutti i computer e i server in cui installare il client di Endpoint Protection. Assegnano a questa raccolta il nome **Tutti i computer protetti da Endpoint Protection**.<br /><br /> **Suggerimento:** non è possibile configurare avvisi per raccolte di utenti.|Per altre informazioni sulle raccolte, vedere [Come creare le raccolte](../../core/clients/manage/collections/create-collections.md)|  
|Gli amministratori configurano gli avvisi seguenti per la raccolta: <br /><br />1) **Malware rilevato**: gli amministratori configurano **Critico** come gravità dell'avviso. <br /><br />2) **Stesso tipo di malware rilevato in diversi computer**: gli amministratori configurano **Critico** come gravità dell'avviso e specificano che l'avviso viene generato quando in più del 5% dei computer viene rilevato malware. <br /><br />3) **Stesso tipo di malware rilevato ripetutamente nell'intervallo specificato in un computer**: gli amministratori configurano Critico come gravità dell'avviso e specificano che l'avviso viene generato quando viene rilevato malware più di 5 volte nell'arco di 24 ore. <br /><br />4) **Più tipi di malware rilevati nello stesso computer con l'intervallo specificato**: gli amministratori configurano Critico come gravità dell'avviso e specificano che l'avviso viene generato quando vengono rilevati più di 3 tipi di malware nell'arco di 24 ore.<br /><br /> Il valore di **Gravità avviso** indica il livello di avviso che verrà visualizzato nella console di Configuration Manager e negli avvisi ricevuti in un messaggio di posta elettronica.<br /><br /> Gli amministratori selezionano anche l'opzione **Visualizza questa raccolta nel dashboard di Endpoint Protection** in modo da poter monitorare gli avvisi nella console di Configuration Manager.|Vedere "Configurare gli avvisi per Endpoint Protection" in [Configurazione di Endpoint Protection](endpoint-configure-alerts.md).|  
|Gli amministratori configurano gli aggiornamenti software di Configuration Manager per scaricare e distribuire gli aggiornamenti delle definizioni tre volte al giorno tramite una regola di distribuzione automatica.|Per altre informazioni, vedere la sezione "Uso degli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni" in [Usare gli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni](endpoint-definitions-configmgr.md).|  
|Gli amministratori verificano le impostazioni nel criterio antimalware predefinito, che contiene le impostazioni di sicurezza consigliate da Microsoft. Per consentire ai computer di eseguire un'analisi rapida ogni giorno, modificano le impostazioni seguenti:<br /><br /> 1) **Eseguire un'analisi rapida giornaliera dei computer client**: **Sì**.<br /><br /> 2) **Ora pianificazione analisi rapida giornaliera**:  **9:00**.<br /><br /> Gli amministratori notano che **Aggiornamenti distribuiti da Microsoft Update** è selezionata per impostazione predefinita come origine di aggiornamento della definizione. Ciò soddisfa il requisito aziendale per cui i computer devono scaricare le definizioni da Microsoft Update quando non possono ricevere gli aggiornamenti software di Configuration Manager.|Vedere [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md).|  
|Gli amministratori creano una raccolta che contiene solo i server di Woodgrove Bank, denominata **Server di Woodgrove Bank**.|Vedere [Come creare le raccolte](../../core/clients/manage/collections/create-collections.md)|  
|Gli amministratori creano un criterio antimalware personalizzato, denominato **Criterio server di Woodgrove Bank**. Aggiungono solo le impostazioni per **Analisi pianificate** e apportano le modifiche seguenti:<br /><br /> **Tipo di analisi**:  **Completa**<br /><br /> **Giorno analisi**:  **Sabato**<br /><br /> **Ora analisi**: **1:00**<br /><br /> **Eseguire un'analisi rapida giornaliera dei computer client**:  **No**.|Vedere [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md).|  
|Gli amministratori distribuiscono il criterio antimalware personalizzato **Criterio server di Woodgrove Bank** nella raccolta **Server di Woodgrove Bank**.|Vedere "Distribuire criteri antimalware ai computer client" nell'articolo [Come creare e distribuire criteri antimalware per Endpoint Protection](endpoint-antimalware-policies.md).|  
|Gli amministratori creano un nuovo set di impostazioni dei dispositivi client personalizzate per Endpoint Protection a cui assegnano il nome **Impostazioni di Endpoint Protection per Woodgrove Bank**.<br /><br /> **Nota:** se non si vuole installare e abilitare Endpoint Protection in tutti i client nella gerarchia, verificare che le opzioni **Gestire il client Endpoint Protection nei computer client** e **Installare il client Endpoint Protection nei computer client** siano entrambe impostate su **No** nelle impostazioni client predefinite.|Per altre informazioni, vedere [Configurare le impostazioni client personalizzate per Endpoint Protection](endpoint-protection-configure-client.md).|  
|Configurano le impostazioni seguenti per Endpoint Protection:<br /><br /> **Gestire il client Endpoint Protection nei computer client**:  **Sì**<br /><br /> Questa impostazione e il relativo valore assicurano che tutti i client di Endpoint Protection esistenti installati vengano gestiti da Configuration Manager.<br /><br /> **Installare il client Endpoint Protection nei computer client**:  **Sì**.</br></br>**Nota**: a partire da Configuration Manager 1802 non è più necessario che nei dispositivi Windows 10 sia installato l'agente Endpoint Protection. Se nei dispositivi Windows 10 l'agente è già installato, Configuration Manager non lo rimuove. Gli amministratori possono rimuovere l'agente di Endpoint Protection nei dispositivi Windows 10 che eseguono almeno la versione client 1802.|Per altre informazioni, vedere [Configurare le impostazioni client personalizzate per Endpoint Protection](endpoint-protection-configure-client.md).|  
|Gli amministratori distribuiscono le impostazioni client **Impostazioni di Endpoint Protection di Woodgrove Bank** alla raccolta **Tutti i computer protetti da Endpoint Protection**.|Vedere "Configurare le impostazioni client personalizzate per Endpoint Protection" in [Configurazione di Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md).|  
|Gli amministratori usano la Creazione guidata criteri di Windows Firewall per creare un criterio configurando le impostazioni seguenti per il profilo di dominio:<br /><br /> 1) **Abilitare Windows Firewall**: **Sì**<br /><br /> 2)<br />                    **Notifica all'utente quando Windows Firewall blocca un nuovo programma**: **Sì**|Vedere [Come creare e distribuire criteri di Windows Firewall per Endpoint Protection](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|Gli amministratori distribuiscono i nuovi criteri firewall alla raccolta **Tutti i computer protetti da Endpoint Protection** che hanno creato in precedenza.|Vedere "Per distribuire criteri di Windows Firewall" in [Come creare e distribuire criteri di Windows Firewall per Endpoint Protection](create-windows-firewall-policies.md)|  
|Gli amministratori usano le attività di gestione disponibili per Endpoint Protection per gestire i criteri antimalware e di Windows Firewall, per eseguire analisi su richiesta dei computer quando necessario, per imporre ai computer di scaricare le definizioni più recenti e per specificare altre azioni da eseguire quando viene rilevato malware.|Vedere [Come gestire i criteri antimalware e le impostazioni del firewall per Endpoint Protection](endpoint-antimalware-firewall.md)|  
|Gli amministratori usano i metodi seguenti per monitorare lo stato di Endpoint Protection e le azioni eseguite da Endpoint Protection:<br /><br /> 1) Tramite il nodo **Stato Endpoint Protection** di **Sicurezza** nell'area di lavoro **Monitoraggio**.<br /><br /> 2) Tramite il nodo **Endpoint Protection** nell'area di lavoro **Asset e conformità**.<br /><br /> 3) Tramite i report predefiniti di Configuration Manager.|Vedere [Come monitorare Endpoint Protection](monitor-endpoint-protection.md)|  

 Gli amministratori comunicano la corretta implementazione di Endpoint Protection al loro manager e confermano che i computer di Woodgrove Bank sono ora protetti dalla funzionalità antimalware, in base ai requisiti aziendali che sono stati specificati. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Come configurare Endpoint Protection](endpoint-protection-configure.md)