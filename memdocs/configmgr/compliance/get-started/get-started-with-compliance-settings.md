---
title: Introduzione alle impostazioni di conformità
titleSuffix: Configuration Manager
description: Informazioni sui concetti di base e sul funzionamento delle impostazioni di conformità
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 59b0b799fd54e0e613f78b11b48b53b19d20ddbf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692289"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Introduzione alle impostazioni di conformità in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di creare le impostazioni di conformità di Configuration Manager, è necessario apprendere i concetti di base e comprenderne il funzionamento.  



## <a name="how-compliance-settings-work"></a>Funzionamento delle impostazioni di conformità  
Con le impostazioni di conformità è possibile gestire la configurazione e la conformità dei client nell'organizzazione.  

Gli elementi di configurazione rientrano in due categorie principali:  

- **Impostazioni per dispositivi gestiti con il client di Configuration Manager**: in genere i dispositivi in cui è stato installato il software client di Configuration Manager con il quale è possibile gestire il dispositivo.  

- **Impostazioni per dispositivi gestiti senza il client di Configuration Manager**: in genere i dispositivi gestiti con Microsoft Intune o con la gestione dei dispositivi locale di Configuration Manager.  



## <a name="what-devices-are-supported"></a>Quali dispositivi sono supportati?  

| Tipo di dispositivo | Altre informazioni |  
|------------|----------------------|  
| PC Windows con il client di Configuration Manager | Creare elementi di configurazione personalizzati per valutare oggetti come chiavi del Registro di sistema, file e attributi di Active Directory.<br /><br /> Quando si usa il tipo di elemento di configurazione Windows 10, è possibile selezionare le impostazioni da un elenco predefinito. |  
| PC Windows (registrati con MDM in locale) | Selezionare le impostazioni da un elenco predefinito. |  
| Dispositivi Windows Phone (registrati con MDM in locale) | Selezionare le impostazioni da un elenco predefinito. |  
| Computer Mac con il client di Configuration Manager | Creare elementi di configurazione personalizzati per valutare oggetti, ad esempio le preferenze di macOS e i risultati restituiti da uno script. |  



## <a name="what-is-a-configuration-item"></a>Cos'è un elemento di configurazione?  
Un elemento di configurazione è un contenitore che archivia informazioni specifiche. Le informazioni configurate dipendono dal tipo di elemento di configurazione. Gli elementi di configurazione possono includere le informazioni seguenti:

- **Informazioni sul metodo di rilevamento** è riservato agli elementi di configurazione Windows che contengono impostazioni dell'applicazione. Rilevano se un'applicazione è installata. Questo rilevamento utilizza il programma di installazione di Windows per l'applicazione o uno script personalizzato.  

- Le **impostazioni** rappresentano le condizioni aziendali o tecniche usate per valutare la conformità nei dispositivi client. Configurare una nuova impostazione o selezionare un'impostazione esistente in un computer di riferimento.  

- Le **regole di conformità** consentono di specificare le condizioni che definiscono la conformità dell'impostazione di un elemento di configurazione. Prima che il client possa valutare la conformità di un'impostazione, è necessario che tale impostazione disponga almeno di una regola di conformità. Alcune impostazioni monitorano e aggiornano i valori non conformi. Creare nuove regole o passare a un'impostazione esistente in qualsiasi elemento di configurazione e selezionare le regole in essa contenute.  

- Le **piattaforme supportate** sono le piattaforme di dispositivo definite su cui il client valuta la conformità degli elementi di configurazione. Se si distribuisce un elemento di configurazione in un dispositivo non incluso nell'elenco delle piattaforme supportate, la conformità non verrà valutata.  



## <a name="what-is-a-configuration-baseline"></a>Cos'è una linea di base di configurazione?  
Definire una linea di base di configurazione che includa gli elementi di configurazione da valutare. Includere anche le impostazioni e le regole che descrivono il livello di conformità necessario. Importare questi dati di configurazione dai pacchetti di configurazione di Configuration Manager. Questi pacchetti di configurazione sono definiti da Microsoft e da altri fornitori. In alternativa, creare nuovi elementi e linee di base di configurazione.  

Dopo aver definito una linea di base di configurazione, distribuirla a raccolte di dispositivi e utenti. Il client valuterà quindi la conformità delle impostazioni della linea di base in base alla pianificazione. È possibile distribuire ai dispositivi più di una linea di base di configurazione. La granularità assicura un maggiore controllo della conformità. 

I dispositivi client valutano la conformità rispetto a ogni linea di base di configurazione distribuita e segnalano immediatamente i risultati al sito usando messaggi sullo stato attuale e messaggi di stato. Se un dispositivo è attualmente disconnesso dalla rete ma la linea di base di configurazione è stata scaricata, la valutazione della conformità degli elementi della configurazione verrà comunque effettuata. Le informazioni sulla conformità verranno inviate quando il dispositivo si riconnette.  

### <a name="monitoring-configuration-baselines"></a>Monitoraggio delle linee di base di configurazione
- Monitorare i risultati della valutazione della conformità nella console di Configuration Manager nell'area di lavoro **Monitoraggio**, nodo **Distribuzioni**. Ad esempio:
  - Cause più comuni di non conformità
  - Errori
  - Il numero di dispositivi e utenti interessati
- Eseguire report sulle impostazioni di conformità con dettagli aggiuntivi. Ad esempio:
  - Quali sono i dispositivi conformi o non conformi
  - Quale elemento della linea di base di configurazione rende un computer non conforme
- Visualizzare i risultati di valutazione di conformità dai computer Windows che eseguono il client di Configuration Manager. Aprire il pannello di controllo di **Configuration Manager** e passare alla scheda **Configurazioni**.  



## <a name="user-data-and-profiles-configuration-items"></a>Elementi di configurazione di profili e dati utente  
Gli elementi di configurazione per i dati utente e i profili includono impostazioni che controllano in che modo gli utenti dei computer che eseguono Windows 8 e versioni successive gestiscono:  
- Reindirizzamento cartelle
- File non in linea
- Profili mobili  

Distribuire questi elementi di configurazione alle raccolte di utenti. Monitorarne la conformità dal nodo **Monitoraggio** della console di Configuration Manager. A differenza di altri elementi di configurazione, non vanno aggiunti alle linee di base di configurazione prima di distribuirli. Distribuirli direttamente facendo clic su **Distribuisci** nella barra multifunzione.  

Per altre informazioni, vedere [Creare elementi di configurazione dei profili e di dati utente](../deploy-use/create-user-data-and-profiles-configuration-items.md).  



## <a name="remote-connection-profiles"></a>Profili di connessione remota  
I profili di connessione remota in forniscono un set di strumenti e risorse che consentono di creare, distribuire e monitorare le impostazioni di connessione remota. Distribuendo queste impostazioni ai dispositivi, viene ridotto al minimo lo sforzo necessario degli utenti finali per connettersi ai computer nella rete aziendale.  

Per altre informazioni, vedere [Creare profili di connessione remota](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Aggiornamento dell'edizione Windows
I criteri di aggiornamento edizione aggiornano automaticamente i dispositivi che eseguono alcune versioni di Windows 10 a un'edizione più recente. Questi criteri forniscono un nuovo codice Product Key o file di licenza che il dispositivo utilizza per eseguire l'aggiornamento.

Per altre informazioni, vedere [Upgrade Windows devices with the edition upgrade policy](../deploy-use/upgrade-windows-version.md) (Aggiornare i dispositivi Windows con i criteri di aggiornamento edizione)



## <a name="microsoft-edge-browser-profiles"></a>Profili del browser Microsoft Edge
<!-- 1357310 -->
A partire dalla versione 1802 i clienti che usano il Web browser [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) nei client Windows 10 possono creare un criterio delle impostazioni di conformità per definire diverse impostazioni di Microsoft Edge. 

Per altre informazioni, vedere [Profili del browser Microsoft Edge](../deploy-use/browser-profiles.md).

