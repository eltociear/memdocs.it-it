---
title: Test e convalida di Intune
titleSuffix: Microsoft Intune
description: Come testare e convalidare la soluzione Intune solo cloud nell'ambiente in uso.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 3/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4f82ee0c-4bd6-4623-9b10-9249d316ccf5
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: aeca72af3eadf55174f1ad97c1e294f48f131801
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79357233"
---
# <a name="intune-testing-and-validation"></a>Test e convalida di Intune

Quando si testa l'implementazione di Microsoft Intune, prendere in considerazione la convalida funzionale e la convalida in base a casi d'uso. La convalida funzionale comprende il test di ogni componente e configurazione per determinare che funzioni correttamente. La convalida in base a casi d'uso prevede di eseguire i test per verificare che gli scenari che comportano una serie di attività funzionino come previsto. 

È consigliabile incorporare il personale help desk e di supporto IT nella fase di test, in modo che venga creata la documentazione di supporto e il personale help desk e di supporto IT acquisisca familiarità con il supporto del prodotto. Se un componente o uno scenario non funziona in base ai casi d'uso, assicurarsi di documentare le modifiche necessarie e includere il motivo per cui è stata apportata una modifica.

## <a name="before-you-begin"></a>Prima di iniziare

È consigliabile documentare quanto segue:

- **Criteri di test:** identificare i benchmark rispetto ai quali eseguire le misurazioni.

- **Componenti di progettazione:** devono essere presenti in almeno un criterio di test.

Se un componente di progettazione non è presente in almeno un criterio di test allineato a un requisito o uno scenario, valutare se il componente di progettazione è necessario o meno. Assicurarsi inoltre di avere i seguenti elementi:

- **Account:** account di test che dispongono delle licenze per EMS e Office 365 per testare tutti gli scenari dei casi d'uso.

- **Dispositivi:** dispositivi di test di cui è possibile eseguire la cancellazione dei dati o il ripristino delle impostazioni predefinite.

- **Componenti di integrazione:** tutti i componenti di integrazione (connettori di certificati e Intune Exchange Connector locale) devono essere installati e configurati, se necessario.

Possono essere necessarie modifiche di progettazione per far fronte a difficoltà impreviste. Inoltre, tutte le modifiche di progettazione devono essere completamente documentate con il motivo per ogni modifica. Ecco un esempio per illustrare una possibile modifica:

<blockquote>Si rileva che i requisiti del Servizio Registrazione dispositivi di rete (NDES) non sono soddisfatti e che è possibile configurare i profili VPN e Wi-Fi con una CA radice che soddisfa gli stessi requisiti senza un'implementazione di NDES.</blockquote>

Durante il processo di test e convalida si potrebbero riscontrare difficoltà o problemi che richiedono indicazioni tecniche o procedure specializzate di risoluzione dei problemi. È consigliabile richiedere assistenza tramite i canali di supporto Microsoft.

- [Informazioni su come ottenere supporto per Intune](get-support.md)

- [Come contattare il supporto telefonico assistito per Microsoft Intune](get-support.md)

## <a name="functional-validation-testing"></a>Test di convalida funzionale

La convalida funzionale comprende il test di ogni componente e configurazione per determinare che funzioni correttamente. Un esempio di test di convalida è riportato nella tabella seguente.

![Tabella 1 sezione 9](./media/planning-guide-test-validation/section-9-image-1-table.PNG)

## <a name="use-case-validation-testing"></a>Test di convalida dei casi d'uso

Eseguire il test di convalida dei casi d'uso per verificare che gli scenari siano completi e funzionali. Esistono due tipi di scenari dei casi d'uso: amministratore IT e utente finale.

### <a name="it-admin"></a>Amministratore IT

Eseguire il test di convalida per l'amministratore IT per convalidare il corretto funzionamento delle azioni amministrative eseguite su un dispositivo o un utente. Di seguito è riportato un esempio di uno scenario di convalida end-to-end per l'amministratore IT.

![Tabella 2 sezione 9](./media/planning-guide-test-validation/section-9-image-2-table.PNG)

### <a name="end-user"></a>End user (Utente finale)

Eseguire il test di convalida per l'utente finale per convalidare che l'esperienza utente finale sia come previsto e venga presentata correttamente in tutte le comunicazioni per gli utenti. È importante convalidare che l'esperienza dell'utente finale sia corretta. Un errore di convalida può causare una riduzione dei tassi di adozione e un aumento del volume di chiamate all'help desk.

![Tabella 3 sezione 9](./media/planning-guide-test-validation/section-9-image-3-table.PNG)

## <a name="next-steps"></a>Passaggi successivi

Dopo avere testato e convalidato gli scenari funzionali e per i casi d'uso di Intune, si è pronti per l'[implementazione di Intune in produzione](planning-guide-rollout-plan.md).

Per altre informazioni e modelli di pianificazione, vedere la sezione [Risorse aggiuntive](planning-guide-resources.md).
