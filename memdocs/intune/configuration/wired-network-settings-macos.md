---
title: Configurare le impostazioni della rete cablata per dispositivi macOS in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Creare o aggiungere un profilo di configurazione della rete cablata per i dispositivi macOS. Vedere le diverse impostazioni, aggiungere certificati, scegliere un tipo EAP e selezionare un metodo di autenticazione in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b11a29cdfd61382e68130479a1ab465bf354c6
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107428"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Aggiungere le impostazioni della rete cablata per dispositivi macOS in Microsoft Intune

È possibile creare un profilo con impostazioni della rete cablata specifiche, quindi distribuire questo profilo ai dispositivi macOS. Microsoft Intune offre numerose funzionalità, tra cui l'autenticazione in rete, l'aggiunta di un certificato PKCS o SCEP e altro ancora.

Questo articolo descrive le impostazioni che è possibile configurare.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione del dispositivo per la rete cablata](wired-networks-configure.md).

> [!NOTE]
> Queste impostazioni sono disponibili per tutti i tipi di registrazione. Per altre informazioni sui tipi di registrazione, vedere [Registrazione macOS](../enrollment/macos-enroll.md).

## <a name="wired-network"></a>Rete cablata

- **Interfaccia di rete**: Selezionare le interfacce di rete nel dispositivo a cui si applica il profilo, in base alla priorità dell'ordine di servizio. Le opzioni disponibili sono:
  
  - **Prima Ethernet attiva** (impostazione predefinita)
  - **Seconda Ethernet attiva**
  - **Terza Ethernet attiva**
  - **Prima Ethernet**
  - **Seconda Ethernet**
  - **Terza Ethernet**
  - **Qualsiasi Ethernet**

  Le opzioni con "attiva" nel titolo usano interfacce attivamente funzionanti nel dispositivo. Se non sono presenti interfacce attive, viene configurata l'interfaccia successiva nella priorità dell'ordine di servizio. Per impostazione predefinita, viene selezionata l'opzione **Prima Ethernet attiva**, che rappresenta anche l'impostazione predefinita configurata da macOS.

- **Tipo EAP**: selezionare il tipo di protocollo EAP (Extensible Authentication Protocol) per autenticare le connessioni cablate protette. Le opzioni disponibili sono:

  - **EAP-FAST**: immettere le **Impostazioni Protected Access Credential (PAC)** . Questa opzione usa credenziali di accesso protetto per creare un tunnel autenticato tra il client e il server di autenticazione. Le opzioni disponibili sono:
    - **Non usare (PAC)**
    - **Uso (PAC)** : se esiste un file PAC, usarlo.
    - **Uso e provisioning di PAC**: creare e aggiungere il file PAC ai dispositivi.
    - **Uso e provisioning di PAC in modo anonimo**: creare e aggiungere il file PAC ai dispositivi senza effettuare l'autenticazione nel server.

  - **EAP-TLS**: Specificare anche:

    - **Server trust** - **Nomi server di certificazione**: **aggiungere** uno o più nomi comuni usati nei certificati emessi dall'autorità di certificazione (CA) attendibile. Quando si immettono queste informazioni, è possibile ignorare la finestra relativa al trust dinamico visualizzata nei dispositivi degli utenti quando si connettono a questa rete.
    - **Certificato radice per la convalida server**: selezionare un profilo del certificato radice attendibile esistente. Questo certificato viene presentato al server quando il client si connette alla rete. Viene usato per autenticare la connessione.
    - **Autenticazione client** - **Certificati**: selezionare il profilo di certificato client SCEP o PKCS che viene distribuito nel dispositivo. Questo certificato corrisponde all'identità presentata dal dispositivo al server per autenticare la connessione.
    - **Privacy dell'identità (identità esterna)** : immettere il testo inviato in risposta a una richiesta di identità EAP. Questo testo può essere costituito da qualsiasi valore, ad esempio `anonymous`. Durante l'autenticazione, viene inviata inizialmente questa identità anonima, seguita da quella effettiva inviata tramite un tunnel sicuro.

  - **EAP-TTLS**: Specificare anche:

    - **Server trust** - **Nomi server di certificazione**: **aggiungere** uno o più nomi comuni usati nei certificati emessi dall'autorità di certificazione (CA) attendibile. Quando si immettono queste informazioni, è possibile ignorare la finestra relativa al trust dinamico visualizzata nei dispositivi degli utenti quando si connettono a questa rete.
    - **Certificato radice per la convalida server**: selezionare un profilo del certificato radice attendibile esistente. Questo certificato viene presentato al server quando il client si connette alla rete. Viene usato per autenticare la connessione.
    - **Autenticazione client**: selezionare un **metodo di autenticazione**. Le opzioni disponibili sono:
      - **Nome utente e password**: richiede all'utente di specificare nome utente e password per autenticare la connessione. Specificare anche:
        - **Metodo non EAP (identità interna)** : selezionare la modalità di autenticazione della connessione. Assicurarsi di scegliere lo stesso protocollo configurato nella rete. Le opzioni disponibili sono:
          - **Password Authentication Protocol (PAP)**
          - **Challenge Heshake Authentication Protocol (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP versione 2 (MS-CHAP v2)**
      - **Certificati**: selezionare il profilo di certificato client SCEP o PKCS che viene distribuito nel dispositivo. Questo certificato corrisponde all'identità presentata dal dispositivo al server per autenticare la connessione.
      - **Privacy dell'identità (identità esterna)** : immettere il testo inviato in risposta a una richiesta di identità EAP. Questo testo può essere costituito da qualsiasi valore, ad esempio `anonymous`. Durante l'autenticazione, viene inviata inizialmente questa identità anonima, seguita da quella effettiva inviata tramite un tunnel sicuro.

  - **LEAP**

  - **PEAP**: Specificare anche:

    - **Server trust** - **Nomi server di certificazione**: **aggiungere** uno o più nomi comuni usati nei certificati emessi dall'autorità di certificazione (CA) attendibile. Quando si immettono queste informazioni, è possibile ignorare la finestra relativa al trust dinamico visualizzata nei dispositivi degli utenti quando si connettono a questa rete.
    - **Certificato radice per la convalida server**: selezionare un profilo del certificato radice attendibile esistente. Questo certificato viene presentato al server quando il client si connette alla rete. Viene usato per autenticare la connessione.
    - **Autenticazione client**: selezionare un **metodo di autenticazione**. Le opzioni disponibili sono:
      - **Nome utente e password**: richiede all'utente di specificare nome utente e password per autenticare la connessione.
      - **Certificati**: selezionare il profilo di certificato client SCEP o PKCS che viene distribuito nel dispositivo. Questo certificato corrisponde all'identità presentata dal dispositivo al server per autenticare la connessione.
      - **Privacy dell'identità (identità esterna)** : immettere il testo inviato in risposta a una richiesta di identità EAP. Questo testo può essere costituito da qualsiasi valore, ad esempio `anonymous`. Durante l'autenticazione, viene inviata inizialmente questa identità anonima, seguita da quella effettiva inviata tramite un tunnel sicuro.

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma potrebbe non essere operativo. Assicurarsi di [assegnare questo profilo](device-profile-assign.md) e di [monitorarne lo stato](device-profile-monitor.md).
