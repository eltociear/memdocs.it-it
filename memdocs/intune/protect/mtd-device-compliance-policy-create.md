---
title: Creare criteri di conformità dei dispositivi Mobile Threat Defense (MTD) con Microsoft Intune
titleSuffix: Microsoft Intune
description: Creare criteri di conformità dei dispositivi di Intune che usano i livelli di minaccia del partner MTD per determinare se un dispositivo mobile può accedere alle risorse aziendali.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 265b92229d687c7dafb2c6de196990c29ffc0cb8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996096"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Creare criteri di conformità dei dispositivi Mobile Threat Defense (MTD) con Intune

Intune con MTD consente di rilevare le minacce e valutare il rischio nei dispositivi mobili. Per ogni dispositivo Intune è possibile creare una regola dei criteri di conformità che consenta di valutare i rischi e determinare se il dispositivo è conforme o meno. È quindi possibile usare [criteri di accesso condizionale](create-conditional-access-intune.md) per bloccare l'accesso ai servizi in base alla conformità dei dispositivi.

> [!NOTE]
> Queste informazioni si applicano a tutti i partner Mobile Threat Defense.

## <a name="before-you-begin"></a>Prima di iniziare

Nell'ambito della configurazione di MTD, nella console partner di MTD sono stati creati criteri per la classificazione delle varie minacce come ad alto, medio o basso rischio. Impostare quindi il livello di Mobile Threat Defense nei criteri di conformità dei dispositivi Intune.

Prerequisiti dei criteri di conformità dei dispositivi con MTD:

- Configurazione dell'integrazione di MTD con Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>Per creare criteri di conformità per dispositivi MTD

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Sicurezza degli endpoint** > **Conformità del dispositivo** > **Crea un criterio**.

3. Selezionare **Piattaforma**, quindi **Crea**.

4. In **Informazioni di base** specificare i criteri di conformità del dispositivo **Nome** e **Descrizione** (facoltativo). Selezionare **Avanti** per continuare.


5. In **Impostazioni di conformità** espandere e configurare **Integrità del dispositivo**. Scegliere il livello di minaccia per dispositivi mobili nell'elenco a discesa in **Richiedi che il dispositivo si trovi al massimo al livello di minaccia del dispositivo**.

   - **Protetti**: questo livello è il più sicuro. Nel dispositivo non possono essere presenti minacce per poter accedere alle risorse aziendali. Se viene rilevata qualsiasi minaccia, il dispositivo viene valutato come non conforme.

   - **Bassa**: il dispositivo è conforme se sono presenti solo minacce di livello basso. In presenza di minacce di livello più alto, il dispositivo verrà messo in stato di non conformità.

   - **Media**: il dispositivo è conforme se le minacce presenti nel dispositivo sono di livello basso o medio. Se viene rilevata la presenza di minacce di livello alto, il dispositivo viene determinato come non conforme.

   - **Alta**: Questo livello di minaccia è il meno sicuro e consente tutti i livelli di minaccia, usando Mobile Threat Defense solo a scopo di report. È necessario che nei dispositivi l'app MTD sia attivata con questa impostazione.

6. Selezionare **Avanti** per passare ad **Assegnazioni**. Selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

   Selezionare **Avanti**.

7. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il nuovo profilo viene visualizzato nell'elenco quando si seleziona il tipo di criterio per il profilo creato.

> [!IMPORTANT]
> Se si creano criteri di accesso condizionale per Microsoft 365 o altri servizi, viene eseguita la valutazione della conformità dei dispositivi e per i dispositivi non conformi viene bloccato l'accesso alle risorse aziendali fino alla risoluzione della condizione di minaccia nei dispositivi interessati.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Per assegnare criteri di conformità per dispositivi MTD

Per assegnare o modificare l'assegnazione dei criteri di conformità dei dispositivi agli utenti:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Sicurezza degli endpoint** > **Conformità del dispositivo**.

3. Selezionare i criteri da assegnare agli utenti, quindi selezionare **Proprietà**.

4. Selezionare **Modifica** per Assegnazioni, quindi usare le opzioni disponibili per *includere* ed *escludere* i gruppi che riceveranno questo criterio.  

5. Selezionare **Verifica e salva** per completare l'assegnazione. Quando si salva l'assegnazione, i criteri vengono distribuiti agli utenti selezionati e i relativi dispositivi vengono valutati per la conformità.

## <a name="next-steps"></a>Passaggi successivi

[Abilitare MTD con Intune](mtd-connector-enable.md)
