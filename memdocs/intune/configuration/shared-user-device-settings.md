---
title: Impostazioni dei dispositivi condivisi o multiutente in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere e usare dispositivi Windows 10 e Windows Holographic for Business condivisi o usati da più utenti in Microsoft Intune. Visualizzare un elenco di tutte le impostazioni e delle loro funzioni nei dispositivi, inclusi i dispositivi Microsoft HoloLens. Controllare gli account Guest, gestire gli account ed eliminare quelli inattivi, consentire o impedire il salvataggio nella risorsa di archiviazione locale, impostare le opzioni di alimentazione e sospensione, scegliere quando installare gli aggiornamenti e usare i dispositivi in ambienti di formazione in un profilo di configurazione del dispositivo.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984002"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Controllare l'accesso, gli account e le funzionalità di risparmio energia nei PC condivisi o nei dispositivi multiutente con Intune

I dispositivi con più utenti, detti dispositivi condivisi, rappresentano una parte comune delle soluzioni di gestione di dispositivi mobili (MDM, Mobile Device Management). Con Microsoft Intune è possibile personalizzare i dispositivi condivisi che eseguono le piattaforme seguenti:

- Windows 10 Professional e versioni successive
- Windows 10 Enterprise e versioni successive
- Windows Holographic for Business, ad esempio HoloLens

Gli istituti di istruzione, ad esempio, hanno dispositivi usati in genere da molti studenti. Con questa impostazione l'amministratore di Intune dell'istituto di istruzione può attivare la funzionalità Computer condiviso per consentire un utente alla volta. Gli studenti non possono passare da un account connesso a un altro nel dispositivo. Quando lo studente si disconnette, tutte le impostazioni specifiche dell'utente vengono rimosse.

Gli utenti finali possono accedere a tali dispositivi condivisi con un account Guest. Quando un utente esegue l'accesso, le credenziali corrispondenti vengono memorizzate nella cache e durante l'uso del dispositivo può accedere solo alle funzionalità consentite dall'amministratore. È l'amministratore a scegliere, ad esempio, quando il dispositivo passa in modalità sospensione, se gli utenti possono visualizzare e salvare file in locale, abilitare o disabilitare impostazioni di risparmio energia e altro ancora. L'amministratore controlla anche se l'account Guest viene eliminato quando l'utente si disconnette e se gli account inattivi vengono eliminati quando la soglia viene raggiunta.

Questo articolo illustra come creare un profilo di configurazione e include collegamenti alle impostazioni disponibili e alle relative descrizioni.

Quando il profilo viene creato in Intune, l'amministratore lo distribuisce o lo assegna ai gruppi di dispositivi nell'organizzazione. Il profilo può anche essere assegnato a gruppi di dispositivi contenenti tipi di dispositivo e versioni del sistema operativo diversi.

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

   - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
   - **Profilo**: Selezionare **Dispositivo multiutente condiviso**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

   - **Nome**: immettere un nome descrittivo per il nuovo profilo.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Scegliere la piattaforma per le impostazioni dettagliate:

    - [Windows 10 e versioni successive](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare il gruppo di dispositivi che riceverà il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

    > [!NOTE]
    > Assicurarsi di assegnare il profilo ai gruppi di dispositivi dell'organizzazione.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

Alla successiva sincronizzazione di ogni dispositivo viene applicato il criterio.

## <a name="next-steps"></a>Passaggi successivi

- Visualizzare tutte le impostazioni per [Windows 10 e versioni successive](shared-user-device-settings-windows.md) e [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
- Dopo l'[assegnazione del profilo](device-profile-assign.md) [monitorarne lo stato](device-profile-monitor.md).
