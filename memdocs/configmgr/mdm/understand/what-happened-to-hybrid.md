---
title: Che ne è stato della gestione di dispositivi mobili ibrida?
titleSuffix: Configuration Manager
description: Informazioni sulla deprecazione di gestione di dispositivi mobili (MDM) ibrida in Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724655"
---
# <a name="what-happened-to-hybrid-mdm"></a>Che ne è stato della gestione di dispositivi mobili ibrida?

*Si applica a: Configuration Manager (Current Branch)*

> [!WARNING]
> Microsoft ha ritirato l'offerta di servizio MDM ibrido a partire dal 1 ° settembre 2019. Tutti i dispositivi MDM ibridi rimanenti non riceveranno i criteri, le app o gli aggiornamenti della sicurezza.

## <a name="remove-hybrid-mdm"></a>Rimuovi MDM ibrida

Se il sito di Configuration Manager dispone di una sottoscrizione Microsoft Intune, è necessario rimuoverlo.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Sottoscrizione a Microsoft Intune**. Eliminare la sottoscrizione di Intune esistente.

1. Nella **procedura guidata rimuovi Microsoft Intune sottoscrizione**selezionare l'opzione per **rimuovere Microsoft Intune sottoscrizione da Configuration Manager**, quindi fare clic su **Avanti**.

1. Completare la procedura guidata.

## <a name="deprecation-announcement"></a>Annuncio di deprecazione

La nota seguente è l'annuncio originale di deprecazione:

> [!NOTE]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). A partire dalla versione 1902 del servizio Intune, prevista per la fine di febbraio 2019, i nuovi clienti non possono creare una nuova connessione ibrida.
> <!--Intune feature 2683117-->  
> Dopo il lancio in Azure oltre un anno fa, sono state aggiunte a Intune centinaia di nuove funzionalità del servizio leader di settore e richieste dai clienti. Il servizio offre ora molte più funzionalità di quelle offerte nella gestione di dispositivi mobili (MDM) ibrida. Intune in Azure offre un'esperienza amministrativa più integrata e semplificata per le esigenze di mobilità aziendale.
>
> La maggior parte dei clienti sceglie di conseguenza Intune in Azure piuttosto che la soluzione MDM ibrida. Sempre meno clienti usano la soluzione MDM ibrida, mentre il numero di quelli che passano al cloud è in continuo aumento. L'1 settembre 2019, Microsoft ritirerà quindi l'offerta di servizio MDM ibrido.
>
> Questa modifica non incide su Configuration Manager locale o sulla [co-gestione per i dispositivi Windows 10](../../comanage/overview.md). Per sapere se si sta usando la gestione dei dispositivi mobili ibrida, passare all'area di lavoro **Amministrazione** della console di Configuration Manager, espandere **Servizi Cloud**e selezionare **Microsoft Intune sottoscrizioni**. Se è configurata una sottoscrizione di Microsoft Intune, il tenant è configurato per la soluzione MDM ibrida.
>
> **Quali sono le conseguenze di questa modifica?**
>
> - Microsoft supporterà l'utilizzo di MDM ibrido per il prossimo anno. La funzionalità continuerà a ricevere le principali correzioni di bug. Microsoft supporterà le funzionalità esistenti nelle nuove versioni del sistema operativo, ad esempio la registrazione in iOS 12. Non saranno disponibili nuove funzionalità per la soluzione MDM ibrida.  
>
> - Se si esegue la migrazione a Intune in Azure prima della fine dell'offerta MDM ibrida, non ci sarà alcun impatto sugli utenti finali.  
>
> - L'1 settembre 2019, i dispositivi MDM ibridi rimanenti non riceveranno più criteri, app o aggiornamenti della sicurezza.  
>
> - Le licenze rimangono invariate. Le licenze di Intune in Azure sono incluse con la soluzione MDM ibrida.  
>
> - La funzionalità MDM locale in Configuration Manager non è deprecata. A partire da Configuration Manager versione 1810, è possibile usare MDM locale senza una connessione a Intune. Per altre informazioni, vedere la pagina relativa a [una connessione Intune non è più necessaria per le nuove distribuzioni MDM locali](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - La funzionalità di accesso condizionale locale di Configuration Manager è anche deprecata con MDM ibrida. Se si usa l'accesso condizionale nei dispositivi gestiti con il client di Configuration Manager, assicurarsi che siano protetti prima della migrazione.
>     1. Configurare i criteri di accesso condizionale in Azure
>     2. Configurare i criteri di conformità nel portale di Intune
>     3. Terminare la migrazione ibrida e impostare l'autorità MDM su Intune
>     4. Abilitare la co-gestione
>     5. Spostare il carico di lavoro di co-gestione dei criteri di conformità in Intune
>
>     Per altre informazioni, vedere [Accesso condizionale con la co-gestione](../../comanage/quickstart-conditional-access.md).
>
> **Operazioni di preparazione alla modifica**
>
> - Iniziare a pianificare la migrazione della soluzione MDM dalla console di ConfigMgr ad Azure. Molti clienti, incluso Microsoft IT, hanno completato questo processo. Per altre informazioni, vedere questo [case study di Microsoft](https://aka.ms/Intune_MSFT).  
>
> - Contattare il Partner of Record o il partner di FastTrack per assistenza. [FastTrack per Microsoft 365](https://aka.ms/hybrid_fasttrack) può agevolare la migrazione dalla soluzione MDM ibrida a Intune in Azure.
>
> Per altre informazioni, vedere [il post di Blog relativo al supporto di Intune](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle funzionalità supportate per la gestione dei dispositivi MDM, vedere gli articoli seguenti:

- [Informazioni su Microsoft Intune](https://docs.microsoft.com/intune/what-is-intune)
- [Che cos'è MDM locale?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Gestione di dispositivi con Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
