---
title: Supporto Unicode e ASCII
titleSuffix: Configuration Manager
description: Informazioni sul supporto di caratteri Unicode e ASCII in oggetti di Configuration Manager.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699899"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Supporto di Unicode e ASCII in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager crea la maggior parte degli oggetti usando caratteri Unicode. Tuttavia, numerosi oggetti supportano solo caratteri ASCII o hanno altre limitazioni.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a> Oggetti che usano i caratteri ASCII

Configuration Manager supporta solo il set di caratteri ASCII quando vengono creati gli oggetti seguenti:  

- Codice sito  

- Tutti i nomi di computer del server di sistema del sito  

- I seguenti account di Configuration Manager:  

    > [!NOTE]  
    > Questi account supportano caratteri ASCII e RUS in un sito eseguito in russo.  

    - Account di installazione push client  

    - Account di connessione al database del punto di gestione  

    - Account di accesso alla rete  

    - Account di accesso al pacchetto  

    - Account mittente standard  

    - Account di installazione del sistema del sito  

    - Account di connessione al punto di aggiornamento software  

    - Account del server proxy del punto di aggiornamento software  

    > [!NOTE]  
    > L'account specificato per l'amministrazione basata su ruoli supporta Unicode.  
    >
    > L'account del punto di Reporting Services supporta Unicode, ad eccezione dei caratteri RUS.  

- Nome di dominio completo (FQDN) per i server del sito e per i sistemi del sito  

- Percorso di installazione per Configuration Manager  

- Nomi di istanza di SQL Server  

- Il percorso per i seguenti ruoli di sistema del sito:  

    - Punto di registrazione  

    - Punto proxy di registrazione  

    - Punto di Reporting Services  

    - Punto di migrazione stato  

- Il percorso delle seguenti cartelle:  

    - La cartella che archivia i dati di migrazione dello stato del client  

    - La cartella che contiene i report di Configuration Manager  

    - La cartella che archivia il backup di Configuration Manager  

    - La cartella che archivia i file di origine dell'installazione per l'impostazione del sito  

    - La cartella che archivia i download dei prerequisiti per l'uso da parte dell'impostazione  

- Il percorso dei seguenti oggetti:  

    - Sito Web IIS  

    - Percorso di installazione dell'applicazione virtuale  

    - Nome dell'applicazione virtuale  

- Nomi file ISO dei supporti di avvio  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a> Limitazioni aggiuntive

Di seguito vengono riportate ulteriori limitazioni per i set di caratteri e le versioni delle lingue supportati:  

- Configuration Manager non supporta la modifica delle impostazioni locali del computer del server del sito.  

- Un'autorità di certificazione dell'organizzazione (enterprise) non supporta i nomi dei computer client che usano set di caratteri DBCS. I nomi dei computer client che è possibile utilizzare sono limitati dalla limitazione PKI del set di caratteri IA5. Configuration Manager non supporta i nomi di autorità di certificazione (CA) o i valori del nome soggetto che usano DBCS.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a> Oggetti che non sono localizzati

Il database di Configuration Manager supporta Unicode per la maggior parte degli oggetti archiviati. Quando possibile, visualizza queste informazioni nella lingua del sistema operativo che corrisponde alle impostazioni locali di un computer. Affinché l'interfaccia client o la console di Configuration Manager visualizzi le informazioni nella lingua del sistema operativo del computer, le impostazioni locali del computer devono corrispondere alla lingua di un client o di un server installato in un sito.  

Molti oggetti di Configuration Manager non supportano Unicode. Vengono archiviati nel database tramite ASCII o presentano limitazioni aggiuntive per la lingua. Queste informazioni vengono sempre visualizzate usando il seti di caratteri ASCII o nella lingua in uso al momento della creazione dell'oggetto.  
