---
title: Categorizzazione automatica dei dispositivi in raccolte
titleSuffix: Configuration Manager
description: Categorizzazione automatica dei dispositivi in raccolte.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695269"
---
# <a name="automatically-categorize-devices-into-collections"></a>Categorizzazione automatica dei dispositivi in raccolte

*Si applica a: Configuration Manager (Current Branch)*

È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi nelle raccolte di dispositivi quando si usa Configuration Manager con Microsoft Intune. Gli utenti devono quindi scegliere una categoria di dispositivi quando eseguono la registrazione di un dispositivo in Intune. È possibile modificare la categoria di un dispositivo dalla console di Configuration Manager.

> [!IMPORTANT]
>  Questa funzionalità può essere usata con la versione di Microsoft Intune di **giugno 2016** e versioni successive. Verificare che l'installazione sia aggiornata a questa versione prima di tentare tali procedure.

## <a name="create-device-categories"></a>Creare categorie di dispositivi

1.  Passare a **Asset e conformità** > **Panoramica** > **Raccolte dispositivi**.
2.  Nella scheda **Home**, nel gruppo **Raccolte di dispositivi**, scegliere **Gestire le categorie di dispositivi**.
3.  Creare, modificare o rimuovere le categorie.

## <a name="associate-a-collection-with-a-device-category"></a>Associare una raccolta a una categoria di dispositivo

Quando si associa una raccolta a una categoria di dispositivi, tutti i dispositivi in tale categoria verranno aggiunti alla raccolta. Non è possibile aggiungere una regola categoria di dispositivi a una raccolta predefinita come **Tutti i sistemi**.

1.  Nella scheda **Regole di appartenenza** della finestra di dialogo **Proprietà** per una raccolta di dispositivi scegliere **Aggiungi regola** > **Regola categoria di dispositivi**.
2.  Nella finestra di dialogo **Seleziona le categorie di dispositivi** selezionare una o più categorie di dispositivi che saranno applicate a tutti i dispositivi della raccolta.

## <a name="change-the-category-of-a-device"></a>Cambiare la categoria di un dispositivo

1.  In **Asset e conformità** > **Panoramica** > **Dispositivi** selezionare un dispositivo nell'elenco **Dispositivi**.
2.  Nella scheda **Home** nel gruppo **Dispositivo** scegliere **Modifica categoria**.
3.  Scegliere una categoria e quindi scegliere **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Visualizzare la categoria a cui un dispositivo appartiene

In **Asset e conformità** > **Panoramica** > **Dispositivi**, nell'elenco **Dispositivi** la categoria è visualizzata nella colonna **Categoria del dispositivo**.

Se la colonna **Categoria di dispositivi** non è visualizzata, fare clic con il pulsante destro del mouse sull'intestazione di una delle colonne nell'elenco **Dispositivi** (ad esempio **Nome**), quindi selezionare **Categoria di dispositivi**.

Se si assegna un dispositivo a una categoria e successivamente si elimina la categoria, il report **Elenco dei dispositivi registrati per utente in Microsoft Intune** mostrerà un GUID nella colonna **Categoria di dispositivi** anziché un nome di categoria.
