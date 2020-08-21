---
title: Eseguire l'aggiornamento a Windows 10
titleSuffix: Configuration Manager
description: Aggiornare i dispositivi a Windows 10 versione 1709 o successive, ovvero le versioni richieste per la co-gestione
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d41a0806a33ac627eceaafab54c73c31ea013365
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694832"
---
# <a name="upgrade-windows-10-for-co-management"></a>Eseguire l'aggiornamento a Windows 10 per la co-gestione

Durante la preparazione per l'onboarding dell'organizzazione per la co-gestione, l'aggiornamento dell'ambiente può essere un ostacolo significativo per alcuni clienti. La co-gestione richiede [Windows 10 versione 1709](/windows/whats-new/whats-new-windows-10-version-1709) o successive. Dopo l'aggiornamento di Windows e la configurazione della registrazione automatica, i client vengono registrati automaticamente per la co-gestione.

Nel video seguente il Senior Program Manager Rob York e il Product Marketing Manager Locky Ainley trattano e illustrano l'aggiornamento a Windows 10 per la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Perché eseguire l'aggiornamento?

Tra gli altri miglioramenti della piattaforma, Windows 10 versione 1709 e successive supporta la registrazione automatica. Questo comportamento consente la registrazione automatica di un dispositivo in Intune quando viene aggiunto ad Azure Active Directory (Azure AD). 

Per altre informazioni, vedere [Abilitare la registrazione automatica di Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Come procedere

Di seguito sono riportati alcuni suggerimenti raccolti da Microsoft aiutando migliaia di clienti a gestire rapidamente gli aggiornamenti:

- Usare distribuzioni in più fasi per offrire questo aggiornamento agli utenti corretti nel momento più appropriato. Per altre informazioni, vedere [Creare distribuzioni in più fasi](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Usare la memorizzazione anticipata nella cache per ridurre i tempi di attesa degli utenti. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](../osd/deploy-use/configure-precache-content.md).  

- Usare il modello di sequenza di attività di aggiornamento sul posto predefinito. Configurare quindi i passaggi specifici pre e post-aggiornamento e le azioni in caso di errore. Per altre informazioni, vedere [Passaggi della sequenza di attività consigliati per la post-elaborazione](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- In ambienti con una forza lavoro molto mobile, Configuration Manager supporta l'aggiornamento sul posto tramite Cloud Management Gateway (CMG). Questa funzionalità consente di aggiornare i client Windows 10 basati su Internet. Per altre informazioni su CMG, vedere [Distribuire l'aggiornamento sul posto di Windows 10 mediante Cloud Management Gateway](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Offrire la possibilità di scegliere la co-gestione agli utenti che vogliono essere early adopter. Questo approccio accelera l'adozione iniziale. Identificando queste persone in anticipo, è possibile assicurarsi una buona copertura già nelle fasi iniziali di un'implementazione. Sarà anche possibile ottenere la convalida e commenti e suggerimenti di utenti che apprezzano i cambiamenti e sono interessati a ricevere nuove versioni più di frequente. I programmi per early adopter generano interesse per le nuove tecnologie e sono destinati ad ampliarsi nel corso del tempo.  


## <a name="case-studies"></a>Case study

Microsoft IT ha distribuito Windows 10 a 96.000 utenti distribuiti presso Microsoft. La distribuzione ha incluso sia gli utenti remoti che gli utenti nella rete aziendale. La distribuzione è stata completata in nove settimane. Per altre informazioni su questa esperienza, vedere [Distribuzione di Windows 10 in Microsoft come aggiornamento sul posto](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

Una grande azienda europea produttrice di software usa con successo un gruppo di early adopter. Dopo i gruppi per i test iniziali e i progetti pilota, circa 2.000 dipendenti ricevono il primo aggiornamento, gli aggiornamenti successivi e il software. Questo gruppo include il personale IT e alcuni volontari. Questo livello di engagement degli utenti offre un maggiore livello di fiducia durante i test e più credibilità quando vengono avviate le implementazioni di massa.



## <a name="contact-fasttrack"></a>Contattare FastTrack

Se è necessaria assistenza per l'aggiornamento a Windows 10 in qualsiasi punto del processo, passare a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), eseguire l'accesso e richiedere assistenza. 

Per altre informazioni, vedere [Ottenere assistenza da FastTrack](quickstart-fasttrack.md).