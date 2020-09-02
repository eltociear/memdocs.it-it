---
title: Usare Microsoft Defender ATP in Microsoft Intune - Azure | Microsoft Docs
description: Usare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Intune, incluse le operazioni di installazione e configurazione, nonché l'onboarding dei dispositivi Intune in ATP e quindi usare una valutazione dei rischi ATP dei dispositivi con i criteri di conformità e accesso condizionale del dispositivo Intune per proteggere le risorse di rete.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1420bf03fe236decba0345e299eb5d5893f96c93
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915110"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Applicare la conformità per Microsoft Defender ATP con l'accesso condizionale in Intune

È possibile integrare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Microsoft Intune come soluzione Mobile Threat Defense per impedire violazioni della sicurezza e limitare l'impatto delle violazioni all'interno di un'organizzazione.

Microsoft Defender ATP funziona con i dispositivi che eseguono Windows 10 o versioni successive e con i dispositivi Android.

Per un funzionamento corretto, verranno usate le configurazioni seguenti:

- **Stabilire una connessione da servizio a servizio fra Intune e Microsoft Defender ATP**. Questa connessione consente a Microsoft Defender ATP di raccogliere dati sul rischio del computer dai dispositivi supportati gestiti con Intune.
- **Usare un profilo di configurazione del dispositivo per eseguire l'onboarding dei dispositivi in Microsoft Defender ATP**. L'onboarding viene eseguito al fine di configurare i dispositivi per comunicare con Microsoft Defender ATP e rendere disponibili i dati che consentono di valutarne il livello di rischio.
- **Usare criteri di conformità del dispositivo per impostare il livello di rischio che si vuole consentire**. I livelli di rischio sono segnalati da Microsoft Defender ATP. I dispositivi che superano il livello di rischio consentito sono identificati come non conformi.
- **Usare criteri di accesso condizionale** per impedire agli utenti di accedere alle risorse aziendali da dispositivi non conformi.

Quando si integra Intune con Microsoft Defender ATP, è possibile sfruttare i vantaggi della gestione di minacce e vulnerabilità di Microsoft Defender ATP e [usare Intune per risolvere le vulnerabilità degli endpoint identificate dalla gestione stessa](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Esempio d'uso di Microsoft Defender ATP con Intune

L'esempio seguente illustra come queste soluzioni interagiscano per contribuire alla protezione dell'organizzazione. Per questo esempio, Microsoft Defender ATP e Intune sono già integrati.

Si consideri un evento in cui qualcuno invia un allegato di Word con codice dannoso incorporato a un utente all'interno dell'organizzazione.

- L'utente apre l'allegato e abilita il contenuto.
- Viene così avviato un attacco con privilegi elevati, che assegna a un utente malintenzionato che opera da un computer remoto diritti di amministratore sul dispositivo della vittima.
- L'utente malintenzionato accede quindi in remoto agli altri dispositivi dell'utente. Questa violazione della sicurezza può avere ripercussioni sull'intera organizzazione.

Microsoft Defender ATP può aiutare a risolvere eventi di sicurezza simili a quelli descritti in questo scenario.

- In questo esempio Microsoft Defender ATP rileva che il dispositivo ha eseguito codice anomalo, ha sperimentato un'elevazione dei privilegi per un processo, ha inserito codice dannoso e ha eseguito un comando sospetto da shell remota.
- In base a queste azioni del dispositivo, Microsoft Defender ATP [classifica il dispositivo come ad alto rischio](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) e include un report dettagliato delle attività sospette nel portale Microsoft Defender Security Center.

È possibile integrare Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) con Microsoft Intune come soluzione Mobile Threat Defense per impedire violazioni della sicurezza e limitare l'impatto delle violazioni all'interno di un'organizzazione.

Poiché sono presenti criteri di conformità dei dispositivi Intune per classificare come non conformi i dispositivi con un livello di rischio *Medio* o *Alto*, il dispositivo compromesso viene classificato come non conforme. Questa classificazione consente di attivare i criteri di accesso condizionale e di bloccare l'accesso dal dispositivo alle risorse aziendali.

Per i dispositivi che eseguono Android, è possibile usare i criteri di Intune per modificare la configurazione di Microsoft Defender ATP in Android. Per altre informazioni, vedere [Protezione Web di Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md).

## <a name="prerequisites"></a>Prerequisiti

Per usare Microsoft Defender ATP con Intune, verificare che gli elementi seguenti siano configurati e pronti per l'uso:

- Tenant con licenza per Enterprise Mobility + Security E3 e Windows E5 (o Microsoft 365 Enterprise E5)
- Ambiente Microsoft Intune, con dispositivi Windows 10 o Android [gestiti da Intune](../enrollment/windows-enroll.md) che siano anche aggiunti ad Azure AD
- Ambiente [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), che fornisce l'accesso a Microsoft Defender Security Center (portale ATP)

> [!NOTE]
> Microsoft Defender ATP non è supportato con i criteri di protezione delle app di Intune per iOS/iPadOS e Android.

## <a name="next-steps"></a>Passaggi successivi

- Per connettere Microsoft Defender ATP a Intune, eseguire l'onboarding dei dispositivi e configurare i criteri di accesso condizionale, vedere [Configurare Microsoft Defender ATP in Intune](../protect/advanced-threat-protection-configure.md).

Per altre informazioni, vedere la documentazione di Intune:

- [Usare le attività di sicurezza con Vulnerability Management di ATP per risolvere i problemi nei dispositivi](atp-manage-vulnerabilities.md)
- [Introduzione ai criteri di conformità dei dispositivi](device-compliance-get-started.md)

Per altre informazioni, vedere la documentazione di Microsoft Defender ATP:

- [Accesso condizionale di Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Dashboard dei rischi di Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)