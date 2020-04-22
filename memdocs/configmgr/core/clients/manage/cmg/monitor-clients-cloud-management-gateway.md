---
title: Monitorare il gateway di gestione cloud
titleSuffix: Configuration Manager
description: Monitorare i client e il traffico di rete attraverso il gateway di gestione di cloud.
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695149"
---
# <a name="monitor-cloud-management-gateway"></a>Monitorare il gateway di gestione cloud

*Si applica a: Configuration Manager (Current Branch)*

Se il gateway di gestione cloud (CMG) è in esecuzione e i client si connettono attraverso di esso, è possibile monitorare i client e il traffico di rete per controllare le prestazioni del servizio.


## <a name="monitor-clients"></a>Monitorare i client

I client connessi attraverso il CMG vengono visualizzati nella console di Configuration Manager allo stesso modo dei client locali. Per altre informazioni, vedere [Come monitorare i client in System Center Configuration Manager](../monitor-clients.md).


## <a name="monitor-traffic-in-the-console"></a>Monitorare il traffico nella console

Monitorare il traffico attraverso il CMG usando la console di Configuration Manager:

1. Accedere all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Cloud Management Gateway**.  

2. Selezionare il CMG nel riquadro dell'elenco.  

3. Visualizzare le informazioni sul traffico nel riquadro dei dettagli per il punto di connessione del CMG e per i ruoli del sistema del sito ai quali è connesso. Queste statistiche mostrano le richieste dei client che arrivano in questi ruoli. Le richieste includono criteri, posizione, registrazione, contenuto, inventario e notifiche client.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Configurare gli avvisi del traffico in uscita

Gli avvisi del traffico in uscita consentono di sapere quando il traffico di rete sta per raggiungere un livello di soglia di 14 giorni. Quando si crea il CMG, è possibile impostare avvisi relativi al traffico. Se questa operazione non è stata eseguita, è possibile configurare gli avvisi anche dopo che il servizio è in esecuzione. È possibile regolare le impostazioni degli avvisi in qualsiasi momento.

1. Accedere all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Cloud Management Gateway**.  

2. Selezionare il CMG nel riquadro elenco e quindi selezionare **Proprietà** nella barra multifunzione.  

3. Passare alla scheda **Avvisi** per abilitare la soglia e gli avvisi. Specificare la soglia di 14 giorni per i dati in gigabyte (GB). Specificare anche le percentuali della soglia in corrispondenza delle quali devono essere generati i diversi livelli di avviso.  

4. Al termine selezionare **OK**.  


## <a name="monitor-logs"></a>Monitorare i log

Il CMG genera voci in diversi file di log. Per altre informazioni, vedere [Log in Configuration Manager](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Dashboard di gestione del cloud

<!--1358461-->
A partire dalla versione 1806, il dashboard di gestione del cloud offre una visualizzazione centralizzata per l'uso del CMG. Dopo l'onboarding del sito nei [servizi di Azure](../../../servers/deploy/configure/azure-services-wizard.md) per la gestione del cloud, il dashboard visualizza anche dati sugli utenti e i dispositivi del cloud.  

Lo screenshot seguente illustra una parte del dashboard di gestione del cloud che mostra due dei riquadri disponibili:  
![Riquadri del dashboard di gestione del cloud: traffico CMG e Client online correnti](media/1358461-cmg-dashboard.png)

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Selezionare il nodo **Gestione cloud** e visualizzare i riquadri del dashboard.  


## <a name="connection-analyzer"></a>Analizzatore della connessione

A partire dalla versione 1806, usare l'analizzatore della connessione CMG per verifiche in tempo reale a supporto della risoluzione dei problemi. L'utilità inclusa nella console controlla lo stato corrente del servizio e il canale di comunicazione dal punto di connessione CMG a tutti i punti di gestione che consentono il traffico CMG.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Gateway di gestione cloud**.  

2. Selezionare l'istanza di CMG di destinazione e quindi selezionare **Analizzatore della connessione** sulla barra multifunzione.  

3. Nella finestra dell'analizzatore della connessione CMG selezionare una delle opzioni seguenti per l'autenticazione nel servizio:  

     1. **Utente di Azure AD**: usare questa opzione per simulare la comunicazione di un'identità utente basata sul cloud che ha eseguito l'accesso a un dispositivo Windows 10 aggiunto ad Azure AD. Fare clic su **Accedi** per immettere le credenziali per questo account utente di Azure AD in modo sicuro.  

     2. **Certificato client**: usare questa opzione per simulare la comunicazione di un client di Configuration Manager con un [certificato di autenticazione client](certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Selezionare **Avvia** per avviare l'analisi. La finestra dell'analizzatore visualizza i risultati. Selezionare una voce per visualizzare ulteriori dettagli nel campo Descrizione.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a> Arrestare il servizio CMG al superamento di una soglia

<!--3735092-->
A partire dalla versione 1902 Configuration Manager ora può arrestare un servizio CMG quando il trasferimento dei dati totale supera il limite. Usare gli [avvisi](#set-up-outbound-traffic-alerts) per attivare le notifiche quando l'utilizzo raggiunge livelli di avviso o critici. Per ridurre l'incidenza di costi di Azure non previsti a causa di un picco di utilizzo, questa opzione consente di disattivare il servizio cloud.

> [!Important]  
> Anche se il servizio non è in esecuzione, vi sono comunque costi associati al servizio cloud. L'arresto del servizio non elimina tutti i relativi costi di Azure. Per rimuovere tutti i costi per il servizio cloud, [rimuovere il gateway di gestione cloud](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> Quando il servizio gateway di gestione cloud viene arrestato, i client basati su Internet non possono comunicare con Configuration Manager.  

Il trasferimento dati totale (in uscita) include i dati del servizio cloud dell'account di archiviazione. Questi dati provengono dai flussi seguenti:

- Dal gateway di gestione cloud verso il client  
- Dal gateway di gestione cloud verso il sito, inclusi i file di log del gateway di gestione cloud  
- Se si abilita il gateway di gestione cloud per il contenuto, dall'account di archiviazione al client  

Per altre informazioni sui flussi di dati, vedere [Porte e flusso di dati](plan-cloud-management-gateway.md#ports-and-data-flow).

La soglia di avviso per l'archiviazione è diversa. Questo avviso consente di monitorare la capacità dell'istanza di archiviazione di Azure.

Quando si seleziona l'istanza del gateway di gestione cloud nel nodo **Cloud Management Gateway** nella console è possibile visualizzare il trasferimento totale dei dati nel riquadro dei dettagli.

Configuration Manager controlla il valore di soglia ogni sei minuti. Se si verifica un picco di utilizzo improvviso, Configuration Manager può impiegare fino a sei minuti per rilevare il superamento della soglia e arrestare il servizio.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Processo di arresto del servizio cloud al superamento di una soglia

1. [Configurare gli avvisi del traffico in uscita](#set-up-outbound-traffic-alerts).  

2. Nella scheda **Avvisi** della finestra delle proprietà del servizio CMG abilitare l'opzione **Arresta questo servizio quando viene superata la soglia critica** .  

Per testare questa funzionalità, ridurre temporaneamente uno dei valori seguenti:  

- **Soglia per il trasferimento di dati in uscita per 14 giorni (GB)** . Il valore predefinito è `10000`.  

- **Percentuale di soglia per la generazione di un avviso di tipo Critico**. Il valore predefinito è `90`.  
