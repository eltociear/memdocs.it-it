---
title: Aggiungere impostazioni VPN per dispositivi in Microsoft Intune - Azure | Microsoft Docs
description: Sui dispositivi amministratore di dispositivi Android, Android Enterprise, iOS, iPadOS, macOS e Windows, usare le impostazioni predefinite per creare connessioni di rete privata virtuale (VPN) in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fff3485c7cda02edfe6a0de78b18bd9e582f54d2
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819984"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Creare profili VPN per la connessione ai server VPN in Intune

Le reti private virtuali (VPN) offrono agli utenti accesso remoto sicuro alla rete dell'organizzazione. I dispositivi usano un profilo di connessione VPN per avviare una connessione con il server VPN. I **profili VPN** in Microsoft Intune assegnano le impostazioni VPN agli utenti e ai dispositivi dell'organizzazione. Usare queste impostazioni in modo che gli utenti possano connettersi in modo semplice e sicuro alla rete aziendale.

Si supponga, ad esempio, di voler configurare i dispositivi iOS/iPadOS con le impostazioni necessarie per connettersi a una condivisione file nella rete dell'organizzazione. Si crea un profilo VPN che include queste impostazioni e si assegna questo profilo a tutti gli utenti che hanno un dispositivo iOS/iPadOS. Gli utenti visualizzeranno la connessione VPN nell'elenco delle reti disponibili e potranno connettersi con la massima facilità.

> [!NOTE]
> La registrazione utenti per iOS/iPadOS e macOS supporta solo [VPN per singole app](vpn-setting-configure-per-app.md).

> [!NOTE]
> È possibile usare [i criteri di configurazione personalizzati di Intune](custom-settings-configure.md) per creare profili VPN per le piattaforme seguenti:
>
> * Android 4 e versioni successive
> * Dispositivi registrati che eseguono Windows 8.1 e versioni successive
> * Dispositivi registrati che eseguono Windows 10 Desktop
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>Tipi di connessione VPN

È possibile creare i profili VPN tramite i tipi di connessione seguenti:

- Automatico
  - Windows 10

- Check Point Capsule VPN
  - Amministratore dispositivo Android
  - Profili di lavoro Android Enterprise
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1

- Cisco AnyConnect
  - Amministratore dispositivo Android
  - Profili di lavoro Android Enterprise
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Amministratore dispositivo Android
  - Profili di lavoro Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - Profili di lavoro completamente gestiti e di proprietà aziendale Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - Windows 10

- VPN personalizzata
  - iOS/iPadOS
  - macOS

  Creare profili VPN personalizzati usando le impostazioni URI in [Creare un profilo con impostazioni personalizzate](custom-settings-configure.md).

- F5 Access
  - Amministratore dispositivo Android
  - Profili di lavoro Android Enterprise
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- NetMotion Mobility
  - iOS/iPadOS
  - macOS

- Palo Alto Networks GlobalProtect
  - Profili di lavoro Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Amministratore dispositivo Android
  - Profili di lavoro Android Enterprise
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise
  - iOS/iPadOS
  - Windows 10
  - Windows 8.1

- SonicWall Mobile Connect
  - Amministratore dispositivo Android
  - Profili di lavoro Android Enterprise
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1

- Zscaler
  - Profili di lavoro Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - Profilo di lavoro completamente gestito e di proprietà aziendale Android Enterprise: Usare i [criteri di configurazione delle app](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS

> [!IMPORTANT]
> Prima di usare i profili VPN assegnati a un dispositivo, è necessario installare l'app VPN applicabile per il profilo. Per informazioni sull'assegnazione dell'app con Intune, vedere [Informazioni sulla gestione delle app in Microsoft Intune](../apps/app-management.md).  

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: scegliere la piattaforma dei dispositivi. Le opzioni disponibili sono:
      - **Amministratore di dispositivi Android**
      - **Android Enterprise** > **Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale**
      - **Android Enterprise** > **Profilo di lavoro**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 e versioni successive**
      - **Windows 8.1 e versioni successive**
    - **Profilo**: selezionare **VPN**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un buon nome di profilo è **Profilo VPN per l'intera azienda**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Per impostazioni dettagliate, scegliere la piattaforma:

    - [Amministratore di dispositivi Android](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (incluso Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)

8. Selezionare **Avanti**.
9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="secure-your-vpn-profiles"></a>Proteggere i profili VPN

I profili VPN possono usare numerosi tipi di connessione e protocolli diversi di produttori diversi. Queste connessioni vengono in genere protette mediante i metodi seguenti.

### <a name="certificates"></a>Certificati

Quando si crea il profilo VPN, è possibile scegliere un profilo certificato SCEP o PKCS creato precedentemente in Intune. Questo profilo è noto come certificato di identità. Viene usato per eseguire l'autenticazione in base a un profilo certificato attendibile, o *certificato radice*, creato per consentire all'utente del dispositivo di connettersi. Il certificato attendibile viene assegnato al computer che esegue l'autenticazione della connessione VPN, in genere il server VPN.

Se si usa l'autenticazione basata su certificati per il profilo VPN, è necessario implementare il profilo VPN, il profilo certificato e il profilo radice attendibile agli stessi gruppi. Questa assegnazione assicura che ogni dispositivo riconosca la legittimità dell'autorità di certificazione.

Per altre informazioni su come creare e usare i profili di certificato in Intune, vedere [Come configurare i certificati con Microsoft Intune](../protect/certificates-configure.md).

> [!NOTE]
> I certificati aggiunti usando il tipo di profilo **Certificato PKCS importato** non sono supportati per l'autenticazione VPN. I certificati aggiunti usando il tipo di profilo **Certificati PKCS** sono supportati per l'autenticazione VPN.


### <a name="user-name-and-password"></a>Nome utente e password

Per eseguire l'autenticazione al server VPN, l'utente deve specificare nome utente e password.

## <a name="next-steps"></a>Passaggi successivi

Dopo che il profilo è stato creato, non è ancora operativo. [Assegnare il profilo](device-profile-assign.md) ad alcuni dispositivi e [monitorarne lo stato](device-profile-monitor.md).

È anche possibile creare e usare VPN per app nei dispositivi [amministratore di dispositivi Android/Android Enterprise](android-pulse-secure-per-app-vpn.md) e [iOS/iPadOS](vpn-setting-configure-per-app.md).
