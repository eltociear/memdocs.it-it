---
title: Strumento di amministrazione basata su ruoli
titleSuffix: Configuration Manager
description: Usare Role-based Administration and Auditing Tool per modellare e controllare i ruoli di sicurezza e gli ambiti di protezione in Configuration Manager.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4cf9d4d3f9d1b2f439d2e87d41cc280e7af0805a
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239709"
---
# <a name="role-based-administration-and-auditing-tool"></a>Role-based Administration and Auditing Tool

*Si applica a: Configuration Manager (Current Branch)*

Role-based Administration and Auditing Tool è uno degli [strumenti di Configuration Manager](tools.md). Usare questo strumento per le attività seguenti:

- Modellare i ruoli di sicurezza con autorizzazioni specifiche  

- Controllare gli ambiti di protezione e i ruoli di sicurezza degli altri utenti



## <a name="requirements"></a>Requisiti

- Eseguirlo nello stesso computer del server del sito di Configuration Manager 

- Avere il ruolo **Amministratore completo**, **Analista di sola lettura** o **Amministratore della protezione**  

- Assegnare l'account all'ambito di protezione **Tutti** e a tutte le raccolte  

- (*Facoltativo*) Per analizzare il report sulla sicurezza delle cartelle, è necessario avere l'accesso a SQL  

- (*Facoltativo*) Per analizzare il report drill-through, eseguire questo strumento nel server del sistema del sito con il ruolo Punto di reporting



## <a name="procedures"></a>Procedure


### <a name="model-permissions-for-a-new-role"></a>Modellare le autorizzazioni per un nuovo ruolo

Usare la procedura seguente per modellare le autorizzazioni per un nuovo ruolo che si vuole creare: 

1. Eseguire **RBAViewer.exe**.  

2. Selezionare i ruoli di sicurezza di base per la compilazione o iniziare da un set di autorizzazioni vuoto. Selezionare le autorizzazioni necessarie.  

3. Fare clic su **Analizza** per visualizzare l'interfaccia utente che verrà visualizzata da questo ruolo personalizzato.  

    > [!Note]  
    > Per verificare se esiste già un ruolo di sicurezza che soddisfa i requisiti, passare alla scheda **Somiglianza**.  

4. Fare clic su **Esporta** per salvare il ruolo come file XML, quindi importarlo nella console di Configuration Manager. Per altre informazioni, vedere [Creare ruoli di sicurezza personalizzati](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Controllare gli ambiti di protezione esistenti

Usare la procedura seguente per controllare tutti gli utenti amministratori, le raccolte e gli ambiti di protezione esistenti in Configuration Manager:

1. Eseguire **RBAViewer.exe**.  

2. Selezionare il pulsante **Audit RBA** (Controlla RBA) nella barra degli strumenti.  

    1. Per visualizzare le relazioni limitate a raccolte in una visualizzazione struttura ad albero, passare alla scheda **Collection Summary** (Riepilogo raccolte).  

    2. Per visualizzare gli oggetti assegnati a un ruolo di sicurezza, passare alla scheda **Riepilogo ambito**.  


### <a name="audit-a-specific-user"></a>Controllare un utente specifico

Usare la procedura seguente per controllare la configurazione dell'amministrazione basata su ruoli per un utente specifico:

1. Eseguire **RBAViewer.exe**.  

2. Selezionare il pulsante **Esegui come** nella barra degli strumenti.  

3. Immettere il nome utente specifico per controllare le autorizzazioni per l'account.  

4. Lo strumento visualizza i ruoli di sicurezza assegnati all'utente o il gruppo di sicurezza a cui l'utente appartiene. Visualizza anche gli oggetti che questo utente può visualizzare e le azioni che può eseguire nella console.  



## <a name="see-also"></a>Vedere anche

- [Nozioni fondamentali sull'amministrazione basata su ruoli](../understand/fundamentals-of-role-based-administration.md)
- [Configurare un'amministrazione basata su ruoli](../servers/deploy/configure/configure-role-based-administration.md)
