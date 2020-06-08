---
title: Impostazioni per l'estensione macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Aggiungere, configurare o creare impostazioni nei dispositivi macOS per usare le estensioni di sistema e le estensioni del kernel. Consentire inoltre agli utenti di eseguire l'override delle estensioni approvate, consentire tutte le estensioni da un identificatore di team o consentire estensioni o app specifiche in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429522"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>Impostazioni dei dispositivi macOS per configurare e usare le estensioni del kernel e del sistema in Intune

> [!NOTE]
> Le estensioni del kernel macOS verranno sostituite con estensioni di sistema. Per altre informazioni, vedere [Suggerimento per il supporto: Uso delle estensioni di sistema anziché delle estensioni del kernel per macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Questo articolo elenca e descrive le diverse impostazioni di estensione del kernel e del sistema che è possibile controllare nei dispositivi macOS. Usare queste impostazioni nella propria soluzione di gestione di dispositivi mobili (MDM) per aggiungere e gestire le estensioni sui dispositivi.

Per altre informazioni sulle estensioni in Intune e sugli eventuali prerequisiti, vedere [Aggiungere le estensioni macOS](kernel-extensions-overview-macos.md).

Queste impostazioni vengono aggiunte a un profilo di configurazione del dispositivo in Intune e quindi assegnate o distribuite ai dispositivi macOS.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione delle estensioni macOS](kernel-extensions-overview-macos.md).

> [!NOTE]
> Queste impostazioni si applicano a diversi tipi di registrazione. Per altre informazioni sui diversi tipi di registrazione, vedere [Registrazione di macOS](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Estensioni del kernel

Questa funzionalità si applica a:

- macOS 10.13.2 e versioni successive
- È necessaria la registrazione dei dispositivi approvata dall'utente 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi approvata dall'utente e registrazione automatica dei dispositivi

- **Consenti gli override degli utenti**: **Sì** permette agli utenti di approvare le estensioni del kernel non incluse nel profilo di configurazione. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo impedisce agli utenti di consentire le estensioni non incluse nel profilo di configurazione. Sono quindi consentite solo le estensioni incluse nel profilo di configurazione.

  Per altre informazioni su questa funzionalità, vedere l'articolo [User-approved kernel extension loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (Caricamento di estensioni del Kernel con approvazione utente) nel sito Web di Apple.

- **Identificatori del team consentiti**: usare questa impostazione per consentire uno o più ID del team. Tutte le estensioni del kernel firmate con gli ID del team immessi sono consentite e attendibili. In altre parole, usare questa opzione per consentire tutte le estensioni del kernel nello stesso ID del team, che può corrispondere a uno sviluppatore o partner specifico.

  **Aggiungere** un identificatore del team di estensioni del kernel valide e firmate da caricare. È possibile aggiungere più identificatori del team. L'identificatore del team deve essere alfanumerico (lettere e numeri) e contenere 10 caratteri. Immettere ad esempio `ABCDE12345`.

  Una volta aggiunto, un identificatore del team può anche essere eliminato.

  Per altre informazioni, vedere [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Individuare l'ID del team) nel sito Web di Apple.

- **Estensioni del kernel consentite**: usare questa impostazione per consentire estensioni del kernel specifiche. Solo le estensioni del kernel immesse sono consentite o attendibili.

  **Aggiungere** l'identificatore dell'aggregazione e l'identificatore del team di un'estensione del kernel da caricare. Per le estensioni del kernel legacy non firmate, usare un identificatore del team vuoto. È possibile aggiungere più estensioni del kernel. L'identificatore del team deve essere alfanumerico (lettere e numeri) e contenere 10 caratteri. Immettere, ad esempio, `com.contoso.appname.macos` per **ID bundle** e `ABCDE12345` per **Identificatore del team**.

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

## <a name="system-extensions"></a>Estensioni di sistema

Questa funzionalità si applica a:

- macOS 10.15 e versioni successive
- È necessaria la registrazione dei dispositivi approvata dall'utente

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Le impostazioni si applicano a: Registrazione dei dispositivi approvata dall'utente e registrazione automatica dei dispositivi

- **Blocca gli override utente**: **Sì** impedisce agli utenti di approvare le estensioni di sistema non incluse nell'elenco di quelle consentite. Quando questa opzione è impostata su **Non configurato** (impostazione predefinita), Intune non modifica o aggiorna questa impostazione. Per impostazione predefinita, il sistema operativo potrebbe consentire agli utenti di approvare estensioni sconosciute non incluse nel profilo di configurazione. Questo significa che le estensioni non incluse nel profilo di configurazione non sono consentite.

- **Identificatori del team consentiti**: usare questa impostazione per consentire uno o più ID del team. Tutte le estensioni di sistema firmate con gli ID del team immessi sono sempre consentite e attendibili. In altre parole, usare questa opzione per consentire tutte le estensioni di sistema nello stesso ID del team, che può corrispondere a uno sviluppatore o partner specifico.

  **Aggiungere** un **identificatore del team** di estensioni di sistema valide e firmate da caricare. È possibile aggiungere più identificatori del team. L'identificatore del team deve essere alfanumerico (lettere e numeri) e contenere 10 caratteri. Immettere ad esempio `ABCDE12345`.

  Una volta aggiunto, un identificatore del team può anche essere eliminato.

  Per altre informazioni, vedere [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Individuare l'ID del team) nel sito Web di Apple.

- **Estensioni del sistema consentite**: usare questa impostazione per consentire sempre estensioni di sistema specifiche. Solo le estensioni di sistema immesse sono consentite o attendibili.

  **Aggiungere** l'**identificatore bundle** e l'**identificatore del team** di un'estensione di sistema da caricare. Per le estensioni di sistema legacy non firmate, usare un identificatore del team vuoto. È possibile aggiungere più estensioni di sistema. L'identificatore del team deve essere alfanumerico (lettere e numeri) e contenere 10 caratteri. Immettere, ad esempio, `com.contoso.appname.macos` per **ID bundle** e `ABCDE12345` per **Identificatore del team**.

- **Tipi di estensioni di sistema consentiti**: immettere l'ID del team e i tipi di estensioni di sistema per consentire tale ID del team:
  - **Identificatore del team**: immettere l'ID del team di un'altra estensione di sistema per cui si vogliono consentire tipi specifici di estensione. In alternativa, immettere un ID del team aggiunto all'elenco **Estensioni di sistema consentite**.
  - **Tipi di estensioni di sistema consentiti**: Selezionare i tipi di estensioni di sistema da consentire per ogni ID del team. Le opzioni disponibili sono:
    - Seleziona tutto
    - Estensioni del driver
    - Estensioni di rete
    - Estensioni di sicurezza degli endpoint

    Per altre informazioni su questi tipi di estensioni vedere [Estensioni del sistema](https://developer.apple.com/system-extensions/) nel sito Web di Apple.

    È possibile aggiungere un ID del team dall'elenco **Estensioni di sistema consentite** e consentire un tipo di estensione specifico. Se l'estensione è di un tipo non consentito è possibile che non venga eseguita.

    Per consentire tutti i tipi di estensione per un ID del team, aggiungere l'ID del team all'elenco **Estensioni di sistema consentite**. Non aggiungere l'ID del team all'elenco **Tipi di estensione di sistema consentiti**. In altre parole, se un ID del team si trova nell'elenco **Estensioni di sistema consentite** e non nell'elenco **Tipi di estensione di sistema consentiti** sono consentiti tutti i tipi di estensione per tale ID del team.

> [!NOTE]
> L'aggiunta dello stesso ID del team per l'elenco **Estensioni di sistema consentite** e l'elenco **Identificatori del team consentiti** può causare un errore e impedire la creazione del profilo. Non aggiungere lo stesso identico identificatore del team in entrambe le impostazioni. 

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).
