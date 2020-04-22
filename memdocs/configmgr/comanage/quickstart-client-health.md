---
title: Integrità del client con co-gestione
titleSuffix: Configuration Manager
description: Mantenere la visibilità dell'integrità del client di Configuration Manager da Intune nel portale di Azure
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690829"
---
# <a name="client-health-with-co-management"></a>Integrità del client con co-gestione

L'integrità della rete è direttamente connessa all'integrità dei dispositivi che entrano ed escono dalla rete. Intune può comunicare con un client non integro, anche quando non si trova all'interno della rete. Usare la co-gestione per combinare questa funzionalità con la capacità di Configuration Manager di individuare il 98% dei client integri noti. È quindi possibile rilevare, valutare e ottenere visibilità su tutti i client in tempo reale. Intune aggiunge anche il supporto necessario per gli aggiornamenti di conformità in tutti i client connessi.

Nel video seguente il Senior Program Manager Rob York e il Product Marketing Manager Locky Ainley trattano e illustrano l'integrità dei client con co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Vantaggi

La valutazione dell'integrità del client è una priorità indiscussa. System Center 2012 Configuration Manager ha aggiunto **CCMeval**. Si tratta di un'utilità esterna al client di Configuration Manager. Offre il monitoraggio dell'integrità del client e la correzione automatica. Questa funzionalità di report si basa tuttavia sulla presenza fisica o virtuale di un dispositivo nella rete interna. La co-gestione consente di risolvere il problema.

Con la co-gestione, Intune può inviare report sullo stato di integrità dei client. Fornisce informazioni relative al timestamp per la validità dei dati. Queste informazioni indicano se i dispositivi sono integri, se sono in grado di connettersi, di installare le app o di eseguire l'aggiornamento alle build del sistema operativo necessarie. 

Per una panoramica dettagliata di questa funzionalità, vedere il video seguente registrato durante la sessione [Novità di Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) presentata a Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quando Configuration Manager indica come stato del dispositivo che il client è installato ma in realtà non lo è, Intune può fornire altre informazioni senza doversi connettere al client. Le informazioni sull'integrità del dispositivo in Intune sono facilmente comprensibili. Se lo stato è diverso da **Integro**, offre consigli e indica i passaggi successivi per risolvere il problema.

> [!Note]  
> Per una versione futura sono previsti i vantaggi seguenti:
> - Configuration Manager includerà funzionalità aggiuntive in CCMeval  
> - Sarà più semplice identificare i computer potenzialmente non integri sia in Configuration Manager sia in Intune  
> - È possibile raggruppare i dati sull'integrità del client in Intune  



## <a name="value-proposition"></a>Proposta di valore

Questa funzionalità consente di avere un'origine dati esterna con Intune. Consente anche di determinare i passaggi successivi durante la risoluzione di una vasta gamma di problemi relativi al client. Non è più necessario creare altri report o usare altri strumenti per recuperare i dati del client.

Se i client sono integri, vuol dire che è stata aggiornata la conformità delle patch. Maggiore è la conformità delle patch, maggiore è la sicurezza.



## <a name="configure"></a>Configurazione

Per iniziare a usare questa funzionalità, eseguire i passaggi seguenti:

- Aggiornare i dispositivi a Windows 10, versione 1709 o successive  

- [Abilitare la co-gestione](how-to-enable.md)  
    - Non è necessario trasferire carichi di lavoro a Intune  

- Aggiornare il sito e i client di Configuration Manager alla *versione 1806* o successiva  


### <a name="review-configuration-manager-client-health-in-intune"></a>Verificare l'integrità del client di Configuration Manager in Intune

1. Accedere al [portale Azure](https://portal.azure.com/).  

2. Scegliere **Tutti i servizi** > **Intune**. Intune si trova nella sezione **Monitoraggio e gestione**.  

3. Dopo aver aperto il riquadro **Microsoft Intune** nel menu disponibile in **Guida e supporto tecnico** accedere alla pagina **Risoluzione dei problemi**.  

4. Usare l'opzione **Seleziona utente**, individuare il dispositivo specifico nell'elenco **Dispositivi** e selezionarlo per aprire la pagina del dispositivo.  

5. Le informazioni sulla co-gestione sono visualizzate nella parte inferiore della pagina del dispositivo. Queste informazioni includono i campi seguenti relativi all'integrità del client:  
    - **Stato dell'agente di Configuration Manager**  
    - **Ora dell'ultima sincronizzazione dell'agente di Configuration Manager**  

> [!Tip]  
> I dispositivi registrati in Intune si connettono al servizio cloud tre volte al giorno, all'incirca ogni otto ore. 
