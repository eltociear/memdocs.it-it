---
title: Rinominare un dispositivo con Microsoft Intune - Azure | Microsoft Docs
description: Rinominare un dispositivo usando Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ff0e650a3eccf057158d3faf28875e42ed90a4d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325035"
---
# <a name="rename-a-device-in-intune"></a>Rinominare un dispositivo in Intune

L'azione **Rinomina dispositivo** consente di rinominare un dispositivo registrato in Intune. Il nome del dispositivo viene cambiato in Intune e nel dispositivo.

È possibile creare i tipi di dispositivo seguenti:
- Windows di proprietà dell'azienda 
- iOS/iPadOS con supervisione
- macOS 10 di proprietà dell'azienda

Questa funzionalità non supporta attualmente la ridenominazione di dispositivi Windows di Azure AD ibridi.

## <a name="rename-a-device"></a>Rinominare un dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Scegliere **Dispositivi** > **Tutti i dispositivi** > scegliere un dispositivo > **...**  > **Rinomina dispositivo**.
4. Nel pannello **Rinomina dispositivo** digitare il nuovo nome nella casella di testo. È possibile usare lettere, numeri e trattini. Il nome deve contenere almeno una lettera o un trattino.
5. Se si vuole riavviare il dispositivo dopo averlo rinominato, scegliere **Sì** accanto a **Riavvia dopo la ridenominazione**.
6. Scegliere **Rinomina**.

## <a name="windows-device-rename-rules"></a>Regole di ridenominazione del dispositivo Windows
Quando si rinomina un dispositivo Windows, il nuovo nome deve rispettare le regole seguenti:
- Massimo 15 caratteri (deve essere minore o uguale a 63 byte, escluso il valore NULL finale)
- Non è Null o una stringa vuota
- Caratteri ASCII consentiti: lettere (a-z, A-Z), numeri (0-9) e trattini
- Caratteri Unicode consentiti: >= 0x80, devono essere caratteri UTF8 validi, devono essere mappabili a IDN (ovvero RtlIdnToNameprepUnicode ha esito positivo; vedere RFC 3492)
- I nomi non possono essere composti esclusivamente da numeri
- Non sono consentiti spazi nel nome
- Caratteri non consentiti: { | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *)


## <a name="next-steps"></a>Passaggi successivi

Per visualizzare lo stato dell'azione **Rinomina dispositivo**, controllare la pagina **Panoramica** del dispositivo.
