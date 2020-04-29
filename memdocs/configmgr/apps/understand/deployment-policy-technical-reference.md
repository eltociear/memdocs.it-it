---
title: Guida di riferimento tecnico sui criteri di distribuzione delle applicazioni
titleSuffix: Configuration Manager
description: Guida di riferimento tecnico per la risoluzione dei problemi relativi ai criteri di distribuzione delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688829"
---
# <a name="application-deployment-policy"></a>Criteri di distribuzione delle applicazioni

*Si applica a: Configuration Manager (Current Branch)*

## <a name="policy-creation"></a>Creazione di criteri

Quando si distribuisce un'applicazione, viene creata un'istanza della classe [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) che rappresenta l'assegnazione di un'applicazione a una raccolta. Questa attività può essere rilevata in **SMSProv.log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

Nel database di Configuration Manager queste informazioni vengono archiviate nella tabella `CI_CIAssignments`, in cui `AssignmentType` 2 rappresenta la distribuzione di un'applicazione. Quando viene creata l'assegnazione, il componente di monitoraggio database SMS rileva una modifica nella tabella e quindi invia una notifica al gestore della replica degli oggetti in modo che elabori i criteri di assegnazione CI. Il componente di gestione della replica degli oggetti crea quindi i criteri per l'assegnazione dell'applicazione nel database, archiviati nella tabella `Policy` del database. L'ID dei criteri è basato sull'ID univoco dell'applicazione. Questa attività può essere rilevata in **objreplmgr.log** facendo riferimento all'ID univoco di assegnazione, che può essere ottenuto dalla query SQL a cui viene fatto riferimento nella sezione [Prima di iniziare](app-deployment-technical-reference.md#before-you-begin).

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

I criteri per l'assegnazione dell'applicazione possono essere visualizzati nel database usando una query SQL simile alla seguente.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Destinazione dei criteri

Dopo la generazione dei criteri, il componente del provider di criteri assegna i criteri alle risorse nella raccolta di destinazione della distribuzione dell'applicazione. Le informazioni sulla destinazione dei criteri vengono archiviate nella tabella `ResPolicyMap` del database. È possibile usare il PADBID restituito dalla query precedente per rilevare questa attività in **policypv.log**. Tuttavia, il PADBID registrato nel log potrebbe non corrispondere sempre al PADBID restituito dalla query precedente se vengono elaborati più criteri simultaneamente.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> La tabella `ResPolicyMap` non contiene informazioni di destinazione per le applicazioni distribuite con stato **Disponibile** per le raccolte di utenti. Software Center esegue una query su un elenco di queste applicazioni dal punto di gestione e le informazioni di destinazione dei criteri per queste applicazioni vengono generate in modo dinamico quando un utente richiede un'applicazione da Software Center.

## <a name="next-steps"></a>Passaggi successivi

- [Distribuzione di applicazioni in raccolte di dispositivi](device-deployment-technical-reference.md)
- [Distribuzione di applicazioni in raccolte di utenti](user-deployment-technical-reference.md)
