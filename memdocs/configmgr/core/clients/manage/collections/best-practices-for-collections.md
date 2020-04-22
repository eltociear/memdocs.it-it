---
title: Procedure consigliate per le raccolte
titleSuffix: Configuration Manager
description: Visualizzare le procedure consigliate per le raccolte in Configuration Manager.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695239"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Procedure consigliate per le raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le procedure consigliate seguenti per le raccolte in Configuration Manager.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a> Non usare gli aggiornamenti incrementali con un numero di raccolte elevato

Quando si abilita l'opzione **Utilizza aggiornamenti incrementali per questa raccolta** , questa configurazione potrebbe provocare ritardi di valutazione se l'opzione viene abilitata per più raccolte. La soglia è pari a circa 200 raccolte nella gerarchia. Il numero esatto dipende dai fattori seguenti:  

- Il numero totale di raccolte  

- La frequenza di aggiunta e modifica delle nuove risorse nella gerarchia  

- Il numero di client nella gerarchia  

- La complessità delle regole di appartenenza alla raccolta nella gerarchia  

## <a name="maintenance-window-size-for-software-updates"></a>Dimensioni della finestra di manutenzione degli aggiornamenti software

È possibile configurare le finestre di manutenzione per le raccolte di dispositivi al fine di limitare il numero di possibili installazioni del software da parte di Configuration Manager su questi dispositivi. Se si configurano dimensioni insufficienti della finestra di manutenzione, il client potrebbe non essere in grado di installare aggiornamenti software critici, rendendo il client vulnerabile ad attacchi altrimenti limitati dall'aggiornamento software.

> [!Tip]
> Durante la pianificazione delle finestre di manutenzione tenere presenti le seguenti considerazioni importanti:
>
> - Il tempo di esecuzione massimo per l'aggiornamento software predefinito è di 60 minuti.
> - Quando Configuration Manager calcola se è possibile installare un aggiornamento, aggiunge cinque minuti al tempo di esecuzione massimo per un riavvio.
> - La durata rimanente di una finestra di manutenzione deve essere superiore al tempo di esecuzione massimo dell'aggiornamento software a cui vanno aggiunti cinque minuti.
