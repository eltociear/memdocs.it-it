---
title: Creare criteri di protezione delle app MTD (Mobile Threat Defense) con Intune
titleSuffix: Microsoft Intune
description: Creare criteri di protezione delle app MTD (Mobile Threat Defense) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 132ac14dfcdb9cde21925911b438798a2c63260a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83991136"
---
# <a name="create-mobile-threat-defense-app-protection-policy-with-intune"></a>Creare criteri di protezione delle app Mobile Threat Defense con Intune

Intune con Mobile Threat Defense (MTD) consente di rilevare le minacce e valutare il rischio nei dispositivi mobili. È possibile creare criteri di protezione delle app di Intune che valutano i rischi per determinare se al dispositivo è consentito o meno l'accesso ai dati aziendali.

> [!NOTE]
> Questo articolo si applica a tutti i partner Mobile Threat Defense che supportano i criteri di protezione delle app:
>
> - Better Mobile (Android, iOS/iPadOS)
> - Zimperium (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS).

## <a name="before-you-begin"></a>Prima di iniziare

Nell'ambito della configurazione di MTD, nella console partner di MTD sono stati creati criteri per la classificazione delle varie minacce come ad alto, medio o basso rischio. È ora necessario impostare il livello di Mobile Threat Defense nei criteri di protezione delle app di Intune.

Prerequisiti per i criteri di protezione delle app con MTD:

- Configurare l'integrazione di MTD con Intune. Senza questa integrazione, i criteri di protezione delle app MTD non avranno alcun effetto.

## <a name="to-create-an-mtd-app-protection-policy"></a>Per creare un criterio di protezione delle app MTD

Usare la procedura per [creare i criteri di protezione delle app per iOS/iPadOS o Android](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps) e usare le informazioni seguenti nelle pagine *App*, *Avvio condizionale* e *Assegnazioni*:

- **App**: selezionare le app a cui si vogliono assegnare i criteri di protezione delle app. Per questo set di funzionalità, queste app vengono bloccate o cancellate selettivamente in base alla valutazione dei rischi del dispositivo dal fornitore di Mobile Threat Defense scelto.
- **Avvio condizionale**:  in *Condizioni del dispositivo* usare la casella di riepilogo a discesa per selezionare **Livello di minaccia massimo consentito del dispositivo**.

  Opzioni per **Valore** del livello di minaccia:

  - **Protetti**: questo livello è il più sicuro. Nel dispositivo non possono essere presenti minacce per poter accedere alle risorse aziendali. Se viene rilevata qualsiasi minaccia, il dispositivo viene valutato come non conforme.
  - **Bassa**: il dispositivo è conforme se sono presenti solo minacce di livello basso. In presenza di minacce di livello più alto, il dispositivo verrà messo in stato di non conformità.
  - **Media**: il dispositivo è conforme se le minacce presenti nel dispositivo sono di livello basso o medio. Se viene rilevata la presenza di minacce di livello alto, il dispositivo viene determinato come non conforme.
  - **Alta**: questo livello è il meno sicuro e consente tutti i livelli di minaccia, usando Mobile Threat Defense solo a scopo di report. È necessario che nei dispositivi l'app MTD sia attivata con questa impostazione.

  Opzioni per **Azione**:

  - **Blocca accesso**
  - **Cancella i dati**

- **Assegnazioni**: Assegnare i criteri ai gruppi di utenti.  I dispositivi usati dai membri del gruppo vengono valutati per l'accesso ai dati aziendali nelle app di destinazione tramite la protezione delle app di Intune.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni su [Mobile Threat Defense](mobile-threat-defense.md) in Microsoft Intune.
