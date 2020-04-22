---
title: Elenco di controllo amministratore per il risparmio energia
titleSuffix: Configuration Manager
description: Usare l'elenco di controllo per gli amministratori per pianificare e implementare il risparmio energia in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696659"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Elenco di controllo per gli amministratori per il risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo elenco di controllo per gli amministratori fornisce le procedure consigliate per l'uso della funzionalità di risparmio energia di Configuration Manager all'interno dell'organizzazione.  

## <a name="configuring-power-management"></a>Configurazione del risparmio energia  
 Usare questa procedura per configurare la gerarchia per raccogliere le informazioni relative al risparmio energia dai computer client.  

> [!IMPORTANT]  
>  Per applicare combinazioni per il risparmio di energia ai computer inclusi nella gerarchia, attendere di aver raccolto e analizzato i dati relativi al risparmio energia dei computer client. Se si applicano nuove impostazioni di risparmio energia ai computer senza prima esaminare le impostazioni esistenti, ciò potrebbe causare un aumento del consumo di energia.  

|Attività|Dettagli|  
|----------|-------------|  
|Rivedere i concetti relativi al risparmio energia nella raccolta di documentazione di Configuration Manager.|Vedere [Introduzione al risparmio energia](introduction-to-power-management.md).|  
|Rivedere i prerequisiti relativi al risparmio energia nella raccolta di documentazione di Configuration Manager.|Vedere [Prerequisiti per il risparmio energia](prerequisites-for-power-management.md).|  
|Rivedere le procedure consigliate per il risparmio energia.|Vedere [Procedure consigliate per il risparmio energia](best-practices-for-power-management.md).|  
|Configurare le raccolte per la gestione del consumo di energia dai computer all'interno dell'ambiente.|Usare **Raccolta per creazione di report relativi ai dati di base**, **Raccolta per creazione di report relativi ai dati di base**, **Raccolta di computer che non supportano il risparmio energia**, **Raccolte di computer a cui sono applicate combinazioni per il risparmio di energia**, **Raccolte di computer a cui sono applicate combinazioni per il risparmio di energia** e **Raccolte di computer che eseguono Windows Server** per gestire le impostazioni di risparmio energia per i computer della gerarchia. È possibile creare più raccolte e applicare diverse combinazioni per il risparmio di energia a ogni raccolta.|  
|Abilitare il risparmio energia.|Prima di iniziare a usare il risparmio energia, è necessario abilitarlo e configurare le impostazioni client richieste. Per altre informazioni, vedere [Configurare il risparmio energia](configuring-power-management.md).|  
|Raccogliere informazioni sul risparmio energia dai computer client.|I dati relativi al risparmio energia vengono segnalati dai client tramite l'inventario hardware di Configuration Manager. In base alla pianificazione dell'inventario hardware configurata, il recupero dell'inventario da tutti i computer client potrebbe richiedere tempo.|  

## <a name="monitoring-and-planning-phase"></a>Fase di monitoraggio e pianificazione  

|Attività|Dettagli|  
|----------|-------------|  
|Eseguire il report **Attività computer**.|Il report **Attività computer** visualizza un grafico che mostra l'attività di monitor, computer e utente per una raccolta specificata in un periodo di tempo specificato. Questo report è collegato al report **Dettagli attività computer** , che visualizza le funzionalità di sospensione e riattivazione dei computer inclusi nella raccolta specificata. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Consumo energia** o **Consumo energia per giorno**.|I report **Consumo energia** e **Consumo energia per giorno** visualizzano il consumo totale di energia mensile (in kWh) per una raccolta specificata in un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Impatto ambientale** o  **impatto ambientale per giorno**.|I report **Impatto ambientale** e **Impatto ambientale giornaliero** visualizzano un grafico che mostra l'emissione di anidride carbonica (CO2) risparmiata da una raccolta di computer specificata in un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Costo energia** o **Costo energia per giorno**.|I report **Costo energia** e **Costo energia per giorno** visualizzano il costo totale dei consumi energetici per un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Funzionalità alimentazione**.|Il report **Funzionalità alimentazione** visualizza le capacità di gestione energia dei computer nella raccolta specificata. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Impostazioni risparmio energia**.|Il report **Impostazioni risparmio energia** visualizza un elenco aggregato delle impostazioni correnti per il risparmio di energia usate dai computer in una raccolta specificata. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Escludere qualsiasi raccolta di computer dal risparmio energia.|Vedere [Configurazione del risparmio energia](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Assicurarsi di salvare le informazioni dei report relativi al risparmio di energia generati durante la fase di pianificazione e monitoraggio. È possibile confrontare questi dati con le informazioni sul risparmio di energia restituite durante le fasi di imposizione e conformità a supporto della valutazione del risparmio a livello di consumo di energia, costi energetici e impatto ambientale generato dall'applicazione di una combinazione per il risparmio di energia ai computer inclusi nella gerarchia.  

## <a name="enforcement-phase"></a>Fase di imposizione  

|Attività|Dettagli|  
|----------|-------------|  
|Selezionare le combinazioni per il risparmio di energia esistenti o crearne di nuove per le raccolte di computer nell'organizzazione.|Vedere [How to create and apply power plans](create-and-apply-power-plans.md) (Come creare e applicare combinazioni per il risparmio di energia).|  
|Applicare queste combinazioni per il risparmio di energia ai computer.|Vedere [How to create and apply power plans](create-and-apply-power-plans.md) (Come creare e applicare combinazioni per il risparmio di energia).|  

## <a name="compliance-phase"></a>Fase di verifica della conformità  

|Attività|Dettagli|  
|----------|-------------|  
|Eseguire il report **Attività computer**.|Il report **Attività computer** visualizza un grafico che mostra l'attività di monitor, computer e utente per una raccolta specificata in un periodo di tempo specificato. Questo report è collegato al report **Risparmio energia - Dettagli attività computer** , che visualizza le funzionalità di sospensione e riattivazione dei computer inclusi nella raccolta specificata. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Consumo energia** o **Consumo energia per giorno**.|I report **Consumo energia** e **Consumo energia per giorno** visualizzano il consumo totale di energia mensile (in kWh) per una raccolta specificata in un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Impatto ambientale** o **impatto ambientale per giorno**.|I report **Impatto ambientale** e **Impatto ambientale giornaliero** visualizzano un grafico che mostra l'emissione di anidride carbonica (CO2) risparmiata da una raccolta di computer specificata in un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Eseguire il report **Costo energia** o **Costo energia per giorno**.|I report **Costo energia** e **Costo energia per giorno** visualizzano il costo totale dei consumi energetici per un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  

## <a name="troubleshooting"></a>Troubleshooting  

|Attività|Dettagli|  
|----------|-------------|  
|Se nei computer della gerarchia non sono in modalità sospensione o ibernazione, eseguire il report **Report errore sospensione** per visualizzare le possibili cause.|Il **Report errore sospensione** visualizza un elenco di cause comuni che hanno impedito ai computer di entrare in stato di sospensione o di ibernazione e il numero di computer interessati da ogni causa per un periodo di tempo specificato. Per altre informazioni, vedere [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).|  
|Se a un computer sono applicate più combinazioni per il risparmio di energia, viene applicata la combinazione meno restrittiva. Eseguire il report **Computer con più combinazioni per il risparmio di energia** per visualizzare i computer a cui sono applicate più combinazioni di risparmio di energia.|Vedere **Computer con più combinazioni per il risparmio di energia** nell'argomento [Come monitorare e pianificare il risparmio energia](monitor-and-plan-for-power-management.md).|  
