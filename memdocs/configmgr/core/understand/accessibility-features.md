---
title: Accessibilità
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità che rendono Configuration Manager accessibile a tutti.
ms.date: 05/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1b25b0137e24212cbad2ba688735e45d9fe9aac0
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556031"
---
# <a name="accessibility-features-in-configuration-manager"></a>Funzionalità di accessibilità in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


Configuration Manager include funzionalità che lo rendono accessibile a tutti.

> [!Note]  
> A partire dalla versione 1902, per migliorare le funzionalità di accessibilità della console di Configuration Manager, aggiornare .NET alla versione 4.7 o successiva nel computer che esegue la console. <!-- SCCMDocs-pr issue #3228 -->  
> 
> Per altre informazioni sulle modifiche all'accessibilità apportate in .NET 4.7.1 e 4.7.2, vedere [Nuove funzionalità di accessibilità in .NET Framework](https://docs.microsoft.com/dotnet/framework/whats-new/whats-new-in-accessibility).  



## <a name="keyboard-shortcuts"></a>Tasti di scelta rapida

### <a name="console-workspaces"></a>Aree di lavoro della console

Per accedere a un'area di lavoro, utilizzare i seguenti tasti di scelta rapida:  

|Tasti di scelta rapida| Area di lavoro|
|--------|--------|  
|CTRL+1| Asset e conformità|
|CTRL+2|  Raccolta software|
|CTRL+3|  Monitoraggio|
|CTRL+4|  Amministrazione|


### <a name="other-console-shortcuts"></a>Altri collegamenti della console

|Tasti di scelta rapida|  Scopo|
|--------|--------|  
|Ctrl + M|Imposta lo stato attivo sul riquadro principale (centrale).|
|Ctrl + T|Imposta lo stato attivo sul nodo principale nel riquadro di spostamento. Se il focus era già in questo riquadro, viene impostato sull'ultimo nodo visitato.|
|Ctrl + I|Imposta lo stato attivo sulla barra di navigazione, sotto la barra multifunzione.|
|Ctrl + L|Imposta lo stato attivo sul campo **Ricerca**, se disponibile.|
|Ctrl + D|Imposta lo stato attivo sul riquadro dei dettagli, se disponibile.|
|ALT     |Sposta lo stato attivo all'interno e al di fuori della barra multifunzione.|

### <a name="cmpivot-shortcuts"></a><a name="bkmk_cmpshortcuts"></a> Collegamenti CMPivot

La maggior parte dei [tasti di scelta rapida del Web browser](https://support.microsoft.com/help/17456/windows-internet-explorer-ease-of-access-options) funziona in CMPivot.

|Tasti di scelta rapida|Scopo|
|--------|--------|  
|CTRL+1|Impostare lo stato attivo sulla prima scheda.|
|ALT + &lt;|Per tornare all'indirizzo|


## <a name="other-accessibility-features"></a>Altre funzionalità di accessibilità

- Per muoversi nel riquadro di spostamento, digitare le lettere del nome di un nodo.

- Lo spostamento tramite tastiera nella vista principale e nella barra multifunzione avviene in modo circolare.

- Lo spostamento tramite tastiera nel riquadro dei dettagli avviene in modo circolare. Per tornare al riquadro o all'oggetto precedente, è possibile usare Ctrl + D e poi MAIUSC + TAB.

- Dopo l'aggiornamento di una vista dell'area di lavoro, il focus è impostato nel riquadro principale dell'area di lavoro.

- Per accedere a un menu dell'area di lavoro, premere TAB fino a quando l'icona Espandi/comprimi non viene attivata. Premere quindi FRECCIA GIÙ per accedere al menu dell'area di lavoro.  

- Per spostarsi all'interno di un menu dell'area di lavoro, utilizzare i tasti di direzione.  

- Per accedere ad aree diverse dell'area di lavoro, utilizzare il tasto TAB e i tasti MAIUSC+TAB. Per spostarsi all'interno di un'area dell'area di lavoro, ad esempio la barra multifunzione, utilizzare i tasti di direzione.  

- Per accedere alla barra degli indirizzi quando lo stato attivo si trova nel nodo della struttura, usare MAIUSC+TAB tre volte.  

- In una pagina della creazione guidata o delle proprietà, è possibile spostarsi tra le caselle con i tasti di scelta rapida. Premere ALT più il carattere di sottolineatura (ALT+_) per selezionare una casella specifica.     

- Per spostarsi tra i vari nodi di un'area di lavoro è sufficiente immettere la prima lettera del nome di un nodo. Quando si preme il tasto, il cursore si sposta sul nodo successivo che inizia con tale lettera. Se si usa un'utilità per la lettura dello schermo, verrà letto il nome del nodo.



## <a name="see-also"></a>Vedere anche

Per altre informazioni sui concetti fondamentali relativi allo spostamento nelle interfacce utente di Configuration Manager, vedere gli articoli seguenti:
- [Uso della console di Configuration Manager](../servers/manage/admin-console.md)
- [Manuale dell'utente di Software Center](software-center.md)

> [!NOTE]  
> Le informazioni in questo articolo sono valide solo per gli utenti che acquistano una licenza di prodotti Microsoft negli Stati Uniti. Se il prodotto non è stato acquistato negli Stati Uniti, è possibile usare la scheda informativa della filiale inclusa nel pacchetto software oppure visitare il [sito Web Microsoft sull'accessibilità](https://www.microsoft.com/accessibility/) per informazioni di contatto per i servizi di supporto Microsoft. È possibile contattare la filiale locale per stabilire se i tipi di prodotti e servizi illustrati in questa sezione sono disponibili nell'area di interesse. Le informazioni sull'accessibilità sono disponibili anche in altre lingue, compreso il giapponese e il francese.  

