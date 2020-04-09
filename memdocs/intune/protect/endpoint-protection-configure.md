---
title: Configurare le impostazioni di Endpoint Protection in Microsoft Intune - Azure | Microsoft Docs
description: Creare le impostazioni di Endpoint Protection quando si crea un profilo del dispositivo macOS o Windows 10 in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 6b5d0f88222c8d48da4f91ff3cf8d4628ccb179d
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551585"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Aggiungere le impostazioni di Endpoint Protection in Intune

Con Intune, è possibile usare profili di configurazione dei dispositivi per la gestione delle comuni funzionalità di sicurezza di Endpoint Protection nei dispositivi, tra cui:

- Firewall
- BitLocker
- App consentite e bloccate
- Microsoft Defender e crittografia

Ad esempio, è possibile creare un profilo di Endpoint Protection che consente solo agli utenti macOS di installare le app dal Mac App Store. In alternativa, abilitare Windows SmartScreen durante l'esecuzione di app nei dispositivi Windows 10.

Prima di creare un profilo, rivedere gli articoli seguenti che illustrano in dettaglio le impostazioni di Endpoint Protection che Intune può gestire per ogni piattaforma supportata:

- [Impostazioni macOS](endpoint-protection-macos.md)
- [Impostazioni Windows 10](endpoint-protection-windows-10.md)

> [!NOTE]
> L'interfaccia utente di Intune verrà aggiornata a un'esperienza a schermo intero. Questa operazione può richiedere alcune settimane. Fino a quando il tenant in uso non riceve l'aggiornamento, il flusso di lavoro per la creazione o la modifica delle impostazioni descritte in questo articolo sarà leggermente diverso.

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Creare un profilo del dispositivo contenente le impostazioni di Endpoint Protection

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le proprietà seguenti:

    - **Piattaforma**: scegliere la piattaforma dei dispositivi. Le opzioni disponibili sono:

        - **macOS**
        - **Windows 10 e versioni successive**

    - **Profilo**: selezionare **Endpoint Protection**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **macOS: profilo di Endpoint Protection che configura il firewall per tutti i dispositivi macOS**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Scegliere la piattaforma per le impostazioni dettagliate:

   - [Impostazioni macOS](endpoint-protection-macos.md)
   - [Impostazioni Windows 10](endpoint-protection-windows-10.md)

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Aggiungere regole del firewall personalizzate per dispositivi Windows 10

Quando si configura Microsoft Defender Firewall come parte di un profilo che include regole di Endpoint Protection per Windows 10, è possibile configurare regole personalizzate per i firewall. Le regole personalizzate consentono di espandere il set predefinito di regole firewall supportate per Windows 10.

Quando si pianificano profili con regole del firewall personalizzate tenere presenti le informazioni seguenti, che potrebbero influire sulla scelta della modalità di raggruppamento delle regole del firewall nei profili:

- Ogni profilo supporta fino a 150 regole del firewall. Quando si usano più di 150 regole creare profili aggiuntivi, ognuno con un limite di 150 regole.

- Per ogni profilo, se non è possibile applicare una singola regola, nessuna delle regole in tale profilo viene eseguita e nessuna delle regole viene applicata al dispositivo.

- Quando non è possibile applicare una regola, tutte le regole nel profilo vengono segnalate come non riuscite. Intune non è in grado di identificare quale singola regola non è andata a buon fine.  

Le regole del firewall che Intune può gestire sono descritte in dettaglio nel [provider del servizio di configurazione (CSP) firewall](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) di Windows. Per esaminare l'elenco delle impostazioni personalizzate del firewall per i dispositivi Windows 10 supportati da Intune, vedere [Regole del firewall personalizzate](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Per aggiungere regole del firewall personalizzate a un profilo Endpoint Protection

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. In *Piattaforma* selezionare **Windows 10 e versioni successive** e in *Profilo* selezionare **Endpoint Protection**.

    Selezionare **Crea**.

4. Immettere un **Nome** per il profilo > **Avanti**.
5. In **Impostazioni di configurazione** selezionare **Microsoft Defender Firewall**. In *Regole del firewall* selezionare **Aggiungi** per aprire la pagina **Crea regola**.

6. Specificare le impostazioni per la regola del firewall e quindi fare clic su **OK** per salvarle. Per esaminare le opzioni di regole del firewall personalizzate disponibili nella documentazione, vedere [Regole del firewall personalizzate](endpoint-protection-windows-10.md#firewall-rules).

    1. La regola viene visualizzata nella pagina *Microsoft Defender Firewall* nell'elenco di regole.
    2. Per modificare una regola, selezionare la regola nell'elenco per aprire la pagina **Modifica regola**.
    3. Per eliminare una regola da un profilo, selezionare i puntini di sospensione **(…)** per la regola e quindi selezionare **Elimina**.
    4. Per modificare l'ordine di visualizzazione delle regole selezionare l'icona *freccia su o freccia giù* nella parte superiore dell'elenco regole.

7. Selezionare **Avanti** fino a raggiungere **Rivedi e crea**. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma potrebbe non essere ancora operativo. [Assegnare il profilo](../configuration/device-profile-assign.md) e [monitorarne lo stato](../configuration/device-profile-monitor.md).
