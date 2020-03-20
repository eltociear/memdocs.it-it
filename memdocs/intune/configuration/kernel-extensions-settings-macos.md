---
title: Impostazioni per l'estensione del kernel macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere, configurare o creare impostazioni nei dispositivi macOS per usare le estensioni del kernel. Consentire inoltre agli utenti di eseguire l'override delle estensioni approvate, consentire tutte le estensioni da un identificatore di team o consentire estensioni o app specifiche in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/10/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa471beb5929a6c5b39267871518f560fe6978f6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343427"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>Impostazioni dei dispositivi macOS per configurare e usare le estensioni del kernel in Intune



Questo articolo elenca e descrive le diverse impostazioni di estensione del kernel che è possibile controllare nei dispositivi macOS. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per aggiungere e gestire le estensioni del kernel sui dispositivi.

Per altre informazioni sulle estensioni del kernel in Intune e sugli eventuali prerequisiti, vedere [Aggiungere le estensioni del kernel macOS](kernel-extensions-overview-macos.md).

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi macOS.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle estensioni del kernel del dispositivo](kernel-extensions-overview-macos.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di macOS](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Estensioni del kernel

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi con approvazione utente automatica

- **Consenti gli override degli utenti**: **Consenti** permette agli utenti di approvare le estensioni del kernel non incluse nel profilo di configurazione. **Non configurato** (impostazione predefinita) impedisce agli utenti di consentire le estensioni non incluse nel profilo di configurazione. Sono quindi consentite solo le estensioni incluse nel profilo di configurazione.

  Per altre informazioni su questa funzionalità, vedere [user-approved kernel extension loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (Caricamento di estensioni del Kernel con approvazione utente) nel sito Web di Apple.

- **Identificatori del team consentiti**: usare questa impostazione per consentire uno o più ID del team. Tutte le estensioni del kernel firmate con gli ID del team immessi sono consentite e attendibili. In altre parole, usare questa opzione per consentire tutte le estensioni del kernel nello stesso ID del team, che può corrispondere a uno sviluppatore o partner specifico.

  **Aggiungere** un identificatore del team di estensioni del kernel valide e firmate che si vuole caricare. È possibile aggiungere più identificatori del team. L'identificatore del team deve essere alfanumerico (lettere e numeri) e contenere 10 caratteri. Immettere ad esempio `ABCDE12345`.

  Una volta aggiunto, un identificatore del team può anche essere eliminato.

  Per altre informazioni, vedere [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Individuare l'ID del team) nel sito Web di Apple.

- **Estensioni del kernel consentite**: usare questa impostazione per consentire estensioni del kernel specifiche. Solo le estensioni del kernel immesse sono consentite o attendibili.

  **Aggiungere** l'identificatore dell'aggregazione e l'identificatore del team di un'estensione del kernel che si vuole caricare. Per le estensioni del kernel legacy non firmate, usare un identificatore del team vuoto. È possibile aggiungere più estensioni del kernel. L'identificatore del team deve essere alfanumerico (lettere e numeri) e contenere 10 caratteri. Immettere, ad esempio, `com.contoso.appname.macos` per **ID bundle** e `ABCDE12345` per **Identificatore del team**.

  > [!TIP]
  > Per ottenere l'ID di aggregazione di un'estensione del kernel (Kext) in un dispositivo macOS, è possibile:
  >
  > 1. Nel terminale eseguire `kextstat | grep -v com.apple` e prendere nota dell'output. Installare il software o l'estensione Kext desiderata. Eseguire di nuovo `kextstat | grep -v com.apple` e cercare le modifiche.
  >
  >    Nel terminale `kextstat` elenca tutte le estensioni del kernel nel sistema operativo. 
  >
  > 2. Sul dispositivo aprire il file di elenco delle proprietà delle informazioni (Info.plist) per un'estensione Kext. Viene visualizzato l'ID dell'aggregazione. All'interno di ogni Kext è archiviato un file Info.plist.

> [!NOTE]
> Non è necessario aggiungere gli identificatori del team e le estensioni del kernel. È possibile configurare gli uni o le altre.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
