---
title: Configurare le impostazioni VPN per i dispositivi Windows 8.1 in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o creare un profilo di configurazione VPN usando le impostazioni di configurazione delle reti private virtuali (VPN), che include i dettagli della connessione e le impostazioni proxy per includere indirizzi IP o FQDN e porta TCP in Microsoft Intune sui dispositivi che eseguono Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556354"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Aggiungere impostazioni VPN per i dispositivi Windows 8.1 in Microsoft Intune

Questo articolo illustra le impostazioni di Intune che è possibile usare per configurare le connessioni VPN nei dispositivi che eseguono Windows 8.1.

A seconda delle impostazioni selezionate, non tutti i valori nell'elenco seguente sono configurabili.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo VPN di Windows 8.1](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Impostazioni VPN di base

- **Nome della connessione**: immettere un nome per la connessione. Questo nome viene visualizzato dagli utenti nel momento in cui esplorano l'elenco delle connessioni VPN disponibili nel dispositivo. Immettere ad esempio `Contoso VPN`.
- **Server**: aggiungere uno o più server VPN a cui si connettono i dispositivi. Quando si aggiunge un server, si immettono le informazioni seguenti:
  - **Descrizione**: immettere un nome descrittivo per il server, ad esempio **Server VPN Contoso**.
  - **Indirizzo IP o FQDN**: Immettere l'indirizzo IP o il nome di dominio completo (FQDN) del server VPN a cui si connetteranno i dispositivi. Ad esempio, immettere `192.168.1.1` o `vpn.contoso.com`.
  - **Server predefinito**: **True** imposta questo server come server predefinito usato dai dispositivi per stabilire la connessione. Impostare un solo server come server predefinito.
  - **Importa**: Selezionare un file con valori delimitati da virgole con l'elenco di server nel formato: descrizione, indirizzo IP o FQDN, server predefinito. Scegliere **OK** per importare i server nell'elenco **Server**.
  - **Esporta**: esporta l'elenco dei server in un file con valori delimitati da virgole (CSV).

- **Tipo di connessione**: selezionare il tipo di connessione VPN. Le opzioni disponibili sono:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Gruppo o dominio di accesso** (solo SonicWall Mobile Connect): Immettere il nome del gruppo di accesso o del dominio a cui connettersi.

- **Ruolo** (solo Pulse Secure): Immettere il nome del ruolo utente che può accedere a questa connessione. Un ruolo utente consente di definire le opzioni e le impostazioni personali, oltre ad abilitare o disabilitare alcune funzionalità di accesso.

- **Area di autenticazione** (solo Pulse Secure): Immettere il nome dell'area di autenticazione da usare. Un'area di autenticazione è un raggruppamento di risorse di autenticazione usate dal tipo di connessione Pulse Secure.

- **XML personalizzato**: immettere i comandi XML personalizzati per la configurazione della connessione VPN.

  **Esempio di Pulse Secure**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **Esempio di VPN CheckPoint Mobile**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **Esempio di SonicWall Mobile Connect**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **Esempio di F5 Edge Client**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Per altre informazioni su come scrivere comandi XML personalizzati, vedere la documentazione della VPN del produttore.

- **Split tunneling**: selezionare **Abilita** per consentire ai dispositivi di scegliere la connessione da usare in base al traffico. Ad esempio, un utente in un hotel userà la connessione VPN per accedere ai file di lavoro, ma userà la rete standard dell'hotel per la normale esplorazione sul Web. Se si vuole che tutto il traffico usi il tunnel VPN quando la connessione VPN è attiva, selezionare **Disabilita**.

## <a name="proxy-settings"></a>Impostazioni proxy

- **Script di configurazione automatica**: consente di usare un file per configurare il server proxy. Immettere l'**URL server proxy** che contiene il file di configurazione. Immettere ad esempio `http://proxy.contoso.com`.
- **Indirizzo**: Immettere l'indirizzo del server proxy, ad esempio un indirizzo IP o `vpn.contoso.com`.
- **Numero porta**: Immettere il numero della porta TCP usata dal server proxy.
- **Rileva automaticamente impostazioni proxy**: Se il server VPN richiede un server proxy per la connessione, scegliere se si desidera che i dispositivi rilevino automaticamente le impostazioni di connessione. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Abilita**: Rilevare automaticamente le impostazioni di connessione.
  - **Disabilita**: Non rilevare automaticamente le impostazioni di connessione.
- **Ignora proxy per indirizzi locali**: Scegliere di usare il server proxy per gli indirizzi locali. Le opzioni disponibili sono:
  - **Non configurato** (impostazione predefinita): Intune non modifica o aggiorna questa impostazione.
  - **Abilita**: Non usare un server proxy per gli indirizzi locali.
  - **Disabilita**: Usare un server proxy per gli indirizzi locali.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

Configurare le impostazioni VPN nei dispositivi [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md) e [Windows 10](vpn-settings-windows-10.md).
