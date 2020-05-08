---
title: Sicurezza e privacy per i profili certificato
titleSuffix: Configuration Manager
description: Informazioni sulle procedure di sicurezza consigliate per gestire i profili certificato per utenti e dispositivi in Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3825ef9b9b1efd576a31742e0fdbe7c2bc3b1628
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906842"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Sicurezza e privacy per i profili certificato in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Procedure consigliate per la protezione dei profili certificato  
 Utilizzare le seguenti procedure consigliate per la protezione durante la gestione di profili certificato per utenti e dispositivi.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Identificare e seguire eventuali procedure consigliate per la protezione per il servizio Registrazione dispositivi di rete, che include la configurazione del sito Web Servizio Registrazione dispositivi di rete in Internet Information Services (IIS) per richiedere SSL e ignorare certificati client.|Per altre informazioni, vedere [Linee guida per il Servizio Registrazione dispositivi di rete](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).|  
|Quando si configurano profili certificato SCEP, scegliere le opzioni più sicure che i dispositivi e l'infrastruttura sono in grado di supportare.|Identificare, implementare e seguire le procedure consigliate per la protezione per i dispositivi e l'infrastruttura.|  
|Specificare manualmente l'affinità utente dispositivo invece di consentire agli utenti di identificare il dispositivo principale. Inoltre, non abilitare la configurazione basata sulle statistiche di utilizzo.|Se si fa clic sull'opzione **Consenti registrazione dei certificati solo sul dispositivo primario dell'utente** in un profilo certificato SCEP, non considerare autorevoli le informazioni raccolte dagli utenti o dal dispositivo. Se si distribuiscono profili certificato SCEP con questa configurazione e l'affinità utente dispositivo non è specificata da un utente amministratore attendibile, utenti non autorizzati potrebbero ricevere privilegi elevati e potrebbero essere concessi loro certificati per effettuare l'autenticazione.<br /><br /> **Nota:** Se si abilita la configurazione basata sulle statistiche di utilizzo, queste informazioni vengono raccolte usando messaggi di stato che non sono protetti da Configuration Manager. Per limitare questo rischio, utilizzare la firma SMB o IPsec tra computer client e il punto di gestione.|  
|Non aggiungere autorizzazioni Lettura e Registrazione per utenti ai modelli di certificato, né configurare il punto di registrazione certificati per ignorare la verifica del modello di certificato.|Anche se Configuration Manager supporta il controllo aggiuntivo se si aggiungono le autorizzazioni di protezione Lettura e Registrazione per gli utenti e sebbene sia possibile configurare il punto di registrazione certificati per ignorare questo controllo quando l'autenticazione non è possibile, nessuna delle due configurazioni è una procedura consigliata per la protezione. Per altre informazioni, vedere l'articolo sulla [pianificazione delle autorizzazioni dei modelli di certificato per i profili certificato](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Informazioni sulla privacy per i profili certificato  
 È possibile utilizzare profili certificato per distribuire certificati da un'autorità di certificazione radice (CA) e client e quindi valutare se i dispositivi diventano conformi dopo che sono stati applicati i profili. Il punto di gestione invia informazioni sulla conformità al server del sito e Configuration Manager memorizza queste informazioni nel database del sito. Informazioni sulla conformità includono proprietà certificato, ad esempio il nome oggetto e l'identificazione personale. Le informazioni vengono crittografate quando i dispositivi le inviano al punto di gestione, ma non vengono memorizzate in forma crittografata nel database del sito. Il database conserva le informazioni fino alla relativa eliminazione nell'ambito dell'attività di manutenzione del sito **Elimina dati di gestione configurazione obsoleti** che viene effettuata all'intervallo predefinito di 90 giorni. È possibile configurare l'intervallo di eliminazione. Le informazioni sulla conformità non vengono inviate a Microsoft.  

 I profili certificato usano le informazioni che Configuration Manager raccoglie eseguendo l'individuazione. Per altre informazioni sulla privacy per l'individuazione, vedere la sezione **Informazioni sulla privacy per l'individuazione** in [Protezione e privacy per Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  I certificati che vengono rilasciati a utenti o dispositivi potrebbero consentire l'accesso a informazioni riservate.  

 Per impostazione predefinita, i dispositivi non valutano i profili certificato. Inoltre, è necessario configurare i profili certificato e quindi distribuirli agli utenti o ai dispositivi.  

 Prima di configurare i profili certificato, considerare i requisiti sulla privacy.  
