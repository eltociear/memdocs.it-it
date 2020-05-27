---
title: Usare il controllo degli accessi in base al ruolo e i tag di ambito per ambienti IT distribuiti in Intune | Microsoft Docs
description: Usare i tag di ambito per filtrare i profili di configurazione in base a ruoli specifici.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c447c9187696a8e918886117847dde6421b4014
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990736"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Usare il controllo degli accessi in base al ruolo e i tag di ambito per ambienti IT distribuiti

È possibile usare il controllo degli accessi in base al ruolo e i tag di ambito per assicurarsi che gli amministratori appropriati abbiano accesso e visibilità per gli oggetti di Intune corretti. I ruoli determinano quale accesso hanno gli amministratori a quali oggetti. I tag di ambito determinano quali oggetti possono vedere gli amministratori.

Ad esempio, si supponga che un amministratore della filiale di Milano abbia il ruolo di gestore dei criteri e dei profili. Si vuole che questo amministratore possa visualizzare e gestire solo i profili e i criteri applicabili esclusivamente ai dispositivi di Milano. Per configurare questo accesso, è necessario:

1. Creare un tag di ambito denominato Milano.
2. Creare un'assegnazione di ruolo per il ruolo di gestore dei criteri e dei profili: 
    - Membri (gruppi) = un gruppo di sicurezza denominato Amministratori IT Milano. Tutti gli amministratori in questo gruppo saranno autorizzati a gestire i criteri e i profili per gli utenti/dispositivi in Ambito (gruppi).
    - Ambito (gruppi) = un gruppo di sicurezza denominato Utenti Milano. I profili e i criteri per tutti gli utenti/dispositivi in questo gruppo possono essere gestiti dagli amministratori in Membri (gruppi). 
    - Ambito (tag) = Milano. Gli amministratori in Membri (gruppi) possono vedere gli oggetti di Intune che hanno anche il tag di ambito Milano.
3. Aggiungere il tag di ambito Milano ai criteri e profili a cui si vuole abbiano accesso gli amministratori in Membri (gruppi).
4. Aggiungere il tag di ambito Milano ai dispositivi che si vuole siano visibili per gli amministratori in Membri (gruppi). 

## <a name="default-scope-tag"></a>Tag di ambito predefinito
Il tag di ambito predefinito viene aggiunto automaticamente a tutti gli oggetti senza tag che supportano i tag di ambito.

La funzionalità per il tag di ambito predefinito è simile alla funzionalità degli ambiti di sicurezza in Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>Per creare un tag di ambito

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Amministrazione del tenant** > **Ruoli** > **Ambito (tag)**  > **Crea**.
2. Nella pagina **Informazioni di base** specificare un **Nome** e una **Descrizione** facoltativa. Scegliere **Avanti**.
3. Nella pagina **Assegnazioni** scegliere i gruppi contenenti i dispositivi a cui assegnare questo tag di ambito. Scegliere **Avanti**.
4. Nella pagina **Rivedi e crea** scegliere **Crea**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>Per assegnare un tag di ambito a un ruolo

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Amministrazione del tenant** > **Ruoli** > **Tutti i ruoli** > scegliere un ruolo > **Assegnazioni** > **Assegna**.
2. Nella pagina **Informazioni di base** specificare **Nome dell'assegnazione** e **Descrizione**. Scegliere **Avanti**.
3. Nella pagina **Gruppi di amministratori** scegliere **Selezionare i gruppi da includere** e selezionare i gruppi che dovranno fare parte di questa assegnazione. Gli utenti in questi gruppi saranno autorizzati a gestire gli utenti e i dispositivi nell'ambito (gruppi). Scegliere **Avanti**.

    ![Screenshot della selezione dei gruppi membri.](./media/scope-tags/select-member-groups.png)

4. Nella pagina **Gruppi di ambiti** selezionare una delle opzioni seguenti per **Assegna a**
    - **Gruppi selezionati**: selezionare i gruppi che contengono gli utenti o i dispositivi da gestire. Tutti gli utenti e i dispositivi nei gruppi selezionati verranno gestiti dagli utenti nei gruppi di amministratori.
    - **Tutti gli utenti**: tutti gli utenti possono essere gestiti dagli utenti nei gruppi di amministratori.
    - **Tutti i dispositivi**: tutti i dispositivi possono essere gestiti dagli utenti nei gruppi di amministratori.
    - **Tutti gli utenti e i dispositivi**: tutti gli utenti e i dispositivi possono essere gestiti dagli utenti nei gruppi di amministratori.

5. Scegliere **Avanti**
6. Nella pagina **Tag di ambito** selezionare i tag da aggiungere a questo ruolo. Gli utenti in Gruppi di amministratori avranno accesso agli oggetti di Intune con lo stesso tag di ambito. È possibile assegnare a un ruolo fino a 100 tag di ambito.
7. Scegliere **Avanti** per passare alla pagina **Rivedi e crea** e quindi scegliere **Crea**.

## <a name="assign-scope-tags-to-other-objects"></a>Assegnare i tag di ambito ad altri oggetti

Per gli oggetti che li supportano, i tag di ambito vengono in genere visualizzati in **Proprietà**. Ad esempio, per assegnare un tag scope a un profilo di configurazione, seguire questa procedura:

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Profili di configurazione** > scegliere un profilo.

2. Scegliere **Proprietà** > **Ambito (tag)**  > **Modifica** > **Selezionare i tag di ambito** > scegliere i tag da aggiungere al profilo. È possibile assegnare a un oggetto fino a 100 tag di ambito.
4. Scegliere **Seleziona** > **Verifica e salva**.

## <a name="scope-tag-details"></a>Dettagli dei tag di ambito
Quando si lavora con i tag di ambito, tenere presente questi dettagli: 

- È possibile assegnare tag di ambito a un tipo di oggetto di Intune se il tenant può avere più versioni di tale oggetto (ad esempio, assegnazioni di ruolo o app).
  Gli oggetti di Intune seguenti sono eccezioni a questa regola e attualmente non supportano i tag di ambito:
    - Profili ESP di Windows
    - Categorie di dispositivi
    - Restrizioni di registrazione
    - Identificatori dei dispositivi aziendali
    - Dispositivi di Autopilot
    - Posizioni di conformità dei dispositivi
    - Dispositivi Jamf
- Le app VPP e gli eBook associati al token VPP ereditano i tag di ambito assegnati al token VPP associato.
- I dispositivi DEP (Device Enrollment Program) e i profili DEP associati al token DEP ereditano i tag di ambito assegnati al token DEP associato.
- Quando un amministratore crea un oggetto in Intune, tutti i tag di ambito assegnati a tale amministratore verranno assegnati automaticamente al nuovo oggetto.
- Il controllo degli accessi in base al ruolo di Intune non si applica ai ruoli di Azure Active Directory. I ruoli di amministratore del servizio e amministratore globale di Intune hanno quindi accesso amministrativo completo a Intune, indipendentemente dai tag di ambito assegnati.
- Se un'assegnazione di ruolo non ha tag di ambito, l'amministratore IT può visualizzare tutti gli oggetti in base alle autorizzazioni degli amministratori IT. Gli amministratori senza tag di ambito hanno essenzialmente tutti i tag di ambito.
- È solo possibile assegnare un tag di ambito incluso nelle assegnazioni di ruolo.
- I gruppi di destinazione possono essere solo quelli inclusi in Ambito (gruppi) nell'assegnazione di ruolo.
- Se al ruolo è assegnato un tag di ambito, non è possibile eliminare tutti i tag di ambito per un oggetto di Intune. È necessario almeno un tag di ambito.

## <a name="next-steps"></a>Passaggi successivi

Informazioni sul comportamento dei tag di ambito quando sono presenti [più assegnazioni di ruolo](role-based-access-control.md#multiple-role-assignments).
Gestire i propri [ruoli](role-based-access-control.md) e [profili](../configuration/device-profile-assign.md).


