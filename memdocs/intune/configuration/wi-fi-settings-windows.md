---
title: Impostazioni Wi-Fi per dispositivi Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Aggiungere o creare un profilo di configurazione Wi-Fi usando le impostazioni Wi-Fi per dispositivi Windows 10 e versioni successive in Microsoft Intune. È possibile configurare impostazioni di base o impostazioni a livello aziendale.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.reviewer: tycast
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bfa28a6b4df30c6303f75d4a5cf91c20ce4e827
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820630"
---
# <a name="add-wi-fi-settings-for-windows-10-and-later-devices-in-intune"></a>Aggiungere le impostazioni Wi-Fi per dispositivi Windows 10 e versioni successive in Intune

È possibile creare un profilo con impostazioni Wi-Fi specifiche. Distribuire quindi questo profilo nei dispositivi Windows 10 e versioni successive. Microsoft Intune offre numerose funzionalità, tra cui l'autenticazione nella rete, l'uso di una chiave precondivisa e altro ancora.

Questo articolo descrive queste impostazioni.

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di dispositivo](wi-fi-settings-configure.md).

## <a name="basic-profile"></a>Profilo di base

I profili di base o personali usano WPA/WPA2 per proteggere la connessione Wi-Fi nei dispositivi. In genere, WPA/WPA2 viene usato nelle reti domestiche o personali. È anche possibile aggiungere una chiave precondivisa per autenticare la connessione.

- **Tipo Wi-Fi**: Scegliere **Basic**. 

- **Nome Wi-Fi (SSID)** : acronimo di Service Set Identifier, identificatore del set di servizi. Questo valore è il nome reale della rete wireless a cui si connettono i dispositivi. Quando scelgono la connessione, tuttavia, gli utenti vedono solo il **nome della connessione** configurata.

- **Nome della connessione**: immettere un nome descrittivo per la connessione Wi-Fi. Il testo immesso è il nome che gli utenti vedono quando visualizzano le connessioni disponibili nel dispositivo.

- **Connetti automaticamente quando la rete è disponibile**: se impostata su **Sì**, i dispositivi si connettono automaticamente quando la rete è disponibile. Se impostata su **No**, i dispositivi non si connettono automaticamente.

  - **Connetti alla rete preferita se disponibile**: se per i dispositivi è disponibile una rete preferita, scegliere **Sì** per usare la rete preferita. Scegliere **No** per usare la rete Wi-Fi in questo profilo di configurazione.

    Si supponga ad esempio di creare una rete Wi-Fi **ContosoCorp** e di usare **ContosoCorp** all'interno di questo profilo di configurazione. Nel raggio di copertura è disponibile anche una rete Wi-Fi **ContosoGuest**. Quando si trovano nel raggio di copertura, i dispositivi aziendali devono connettersi automaticamente a **ContosoCorp**. In questo scenario impostare la proprietà **Connetti alla rete preferita se disponibile** su **No**.

  - **Consente di stabilire la connessione a questa rete anche se non trasmette il rispettivo SSID**: scegliere **Sì** per indicare al profilo di configurazione di connettersi automaticamente alla rete, anche quando la rete è nascosta, ovvero quando il relativo SSID non viene trasmesso pubblicamente. Scegliere **No** se non si vuole che il profilo di configurazione si connetta alla rete nascosta.

- **Limite per la connessione a consumo**: l'amministratore può scegliere come viene misurato il traffico di rete. Le applicazioni possono quindi modificare il comportamento del traffico di rete in base a questa impostazione. Le opzioni disponibili sono:

  - **Senza restrizioni**: impostazione predefinita. La connessione non è a consumo e non sono previste restrizioni sul traffico.
  - **Fisso**: usare questa opzione se la rete è configurata con un limite fisso per il traffico di rete. Quando viene raggiunto questo limite, l'accesso alla rete non viene più consentito.
  - **Variabile**: usare questa opzione se il traffico di rete viene addebitato per byte (costo per byte).

- **Tipo di sicurezza wireless**: immettere il protocollo di sicurezza usato per l'autenticazione dei dispositivi in rete. Le opzioni disponibili sono:
  - **Apri (nessuna autenticazione)** : usare questa opzione solo se la rete non è protetta.
  - **WPA/WPA2-Personale**: opzione che offre maggiore protezione in genere usata per la connettività Wi-Fi. Per maggiore sicurezza, è anche possibile immettere una password chiave precondivisa o una chiave di rete.

    - **Chiave precondivisa** (PSK): Facoltativo. Visualizzato quando si sceglie **WPA/WPA2-Personal** come tipo di sicurezza. Quando viene configurata la rete dell'organizzazione, viene configurata anche una password o una chiave di rete. Immettere questa password o chiave di rete per il valore di chiave precondivisa. Immettere una stringa con un numero di caratteri compreso tra 8 e 64. Se la password o la chiave di rete è di 64 caratteri, immettere caratteri esadecimali.

      > [!IMPORTANT]
      > La chiave precondivisa è la stessa per tutti i dispositivi impostati come destinazione del profilo. Se la chiave è compromessa, può essere usata da qualsiasi dispositivo per connettersi alla rete Wi-Fi. Proteggere le chiavi precondivise per evitare accessi non autorizzati.

- **Impostazioni del proxy aziendale**: scegliere questa impostazione per usare le impostazioni proxy all'interno dell'organizzazione. Le opzioni disponibili sono:
  - **Nessuno**: non sono state configurate impostazioni proxy.
  - **Configura manualmente**: immettere l'**indirizzo IP del server proxy** e il relativo **numero di porta**.
  - **Configura automaticamente**: immettere l'URL che punta a uno script di configurazione automatica del proxy. Immettere ad esempio `http://proxy.contoso.com/proxy.pac`.

## <a name="enterprise-profile"></a>Profilo enterprise

I profili aziendali usano il protocollo EAP (Extensible Authentication Protocol) per autenticare le connessioni Wi-Fi. EAP viene spesso usato dalle aziende, perché è possibile usare i certificati per autenticare e proteggere le connessioni e configurare più opzioni di sicurezza.

- **Tipo Wi-Fi**: scegliere **Enterprise**.

- **Nome Wi-Fi (SSID)** : acronimo di Service Set Identifier, identificatore del set di servizi. Questo valore è il nome reale della rete wireless a cui si connettono i dispositivi. Quando scelgono la connessione, tuttavia, gli utenti vedono solo il **nome della connessione** configurata.

- **Nome della connessione**: immettere un nome descrittivo per la connessione Wi-Fi. Il testo immesso è il nome che gli utenti vedono quando visualizzano le connessioni disponibili nel dispositivo.

- **Connetti automaticamente quando la rete è disponibile**: se impostata su **Sì**, i dispositivi si connettono automaticamente quando la rete è disponibile. Se impostata su **No**, i dispositivi non si connettono automaticamente.
  - **Connetti alla rete preferita se disponibile**: se per i dispositivi è disponibile una rete preferita, scegliere **Sì** per usare la rete preferita. Scegliere **No** per usare la rete Wi-Fi in questo profilo di configurazione.

    Si supponga ad esempio di creare una rete Wi-Fi **ContosoCorp** e di usare **ContosoCorp** all'interno di questo profilo di configurazione. Nel raggio di copertura è disponibile anche una rete Wi-Fi **ContosoGuest**. Quando si trovano nel raggio di copertura, i dispositivi aziendali devono connettersi automaticamente a **ContosoCorp**. In questo scenario impostare la proprietà **Connetti alla rete preferita se disponibile** su **No**.

- **Consente di stabilire la connessione a questa rete anche se non trasmette il rispettivo SSID**: scegliere **Sì** per indicare al profilo di configurazione di connettersi automaticamente alla rete, anche quando la rete è nascosta, ovvero quando il relativo SSID non viene trasmesso pubblicamente. Scegliere **No** se non si vuole che il profilo di configurazione si connetta alla rete nascosta.

- **Limite per la connessione a consumo**: l'amministratore può scegliere come viene misurato il traffico di rete. Le applicazioni possono quindi modificare il comportamento del traffico di rete in base a questa impostazione. Le opzioni disponibili sono:

  - **Senza restrizioni**: impostazione predefinita. La connessione non è a consumo e non sono previste restrizioni sul traffico.
  - **Fisso**: usare questa opzione se la rete è configurata con un limite fisso per il traffico di rete. Quando viene raggiunto questo limite, l'accesso alla rete non viene più consentito.
  - **Variabile**: usare questa opzione se il traffico di rete viene addebitato per byte.

- **Accesso Single Sign-On (SSO)** : consente di configurare l'accesso Single Sign-On (SSO) in cui le credenziali vengono condivise per l'accesso al computer e alla rete Wi-Fi. Le opzioni disponibili sono:
  - **Disabilita**: disabilita il comportamento SSO. L'utente deve eseguire l'autenticazione alla rete separatamente.
  - **Abilita prima dell'accesso dell'utente al dispositivo**: usare SSO per l'autenticazione in rete prima della procedura di accesso dell'utente.
  - **Abilita dopo l'accesso dell'utente al dispositivo**: usare SSO per l'autenticazione in rete dopo il completamento della procedura di accesso dell'utente.
  - **Tempo massimo per l'autenticazione prima del timeout**: immettere il numero massimo di secondi di attesa prima dell'autenticazione in rete, da 1 a 120 secondi.
  - **Consenti a Windows di richiedere credenziali di autenticazione aggiuntive all'utente**: se si sceglie **Sì**, il sistema Windows potrà chiedere credenziali aggiuntive all'utente, se il metodo di autenticazione lo richiede. Scegliere **No** per nascondere questi prompt.

- **Consenti memorizzazione nella cache Pairwise Master Key (PMK)** : selezionare **Sì** per memorizzare nella cache la chiave PMK usata nell'autenticazione. La memorizzazione nella cache in genere consente una procedura di autenticazione in rete più rapida. Scegliere **No** per imporre l'handshake di autenticazione ogni volta che l'utente si connette alla rete Wi-Fi. Per usare l'impostazione **Abilita la preautenticazione**, selezionare **Sì**.

  - **Durata massima dell'archiviazione di un PMK nella cache**: immettere il numero di minuti di memorizzazione di una chiave PMK (Pairwise Master Key) nella cache, da 5 a 1440 minuti.
  - **Numero massimo di PMK archiviati nella cache**: immettere il numero di chiavi archiviate nella cache, da 1 a 255.

- **Abilita la preautenticazione**: la preautenticazione consente l'autenticazione del profilo presso tutti i punti di accesso alla rete nel profilo prima della connessione. Quando si passa da un punto di accesso a un altro, la preautenticazione riconnette più rapidamente l'utente o i dispositivi. Scegliere **Sì** per consentire l'autenticazione del profilo presso tutti i punti di accesso alla rete inclusi nel raggio di copertura. Scegliere **No** per chiedere all'utente o al dispositivo di eseguire separatamente l'autenticazione a ogni punto di accesso.

  Per usare questa impostazione, impostare **Consenti memorizzazione nella cache Pairwise Master Key (PMK)** su **Sì**.

  - **Numero massimo di tentativi di preautenticazione**: immettere il numero di tentativi di preautenticazione, da 1 a 16.

- **Tipo EAP**: scegliere il tipo di protocollo EAP (Extensible Authentication Protocol) per autenticare le connessioni wireless protette. Le opzioni disponibili sono:

  - **EAP-SIM**
  - **EAP-TLS**
  - **EAP-TTLS**
  - **PEAP** (Protected EAP)

    **Impostazioni EAP-TLS, EAP-TTLS e PEAP aggiuntive**:

    > [!NOTE]
    > Quando si usa un tipo EAP, sono supportati solo i profili di certificato SCEP e PKCS.

    **SERVER TRUST**  

    - **Nomi dei server per certificati**: da usare con i tipi **EAP-TLS**, **EAP-TTLS** o **PEAP**. Immettere uno o più nomi comuni usati nei certificati emessi dall'autorità di certificazione (CA) attendibile. Se si immettono queste informazioni, è possibile ignorare la finestra di dialogo relativa al trust dinamico visualizzata nei dispositivi degli utenti quando si connettono alla rete Wi-Fi.  

    - **Certificato radice per la convalida server**: da usare con i tipi **EAP-TLS**, **EAP-TTLS** o **PEAP**. Scegliere il profilo del certificato radice attendibile usato per autenticare la connessione.  

    - **Privacy dell'identità (identità esterna)** : da usare con il tipo EAP **PEAP**. Immettere il testo inviato in risposta a una richiesta di identità EAP. Questo testo può essere costituito da qualsiasi valore. Durante l'autenticazione, viene inviata inizialmente questa identità anonima, seguita da quella effettiva inviata tramite un tunnel sicuro.  

    - **Esegui la convalida del server nella fase 1 di PEAP**: se questa opzione è impostata su **Sì** nella fase 1 di negoziazione PEAP i dispositivi eseguono la convalida del certificato e verificano il server. Selezionare **No** per bloccare o impedire questa convalida. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

      Se si seleziona **Sì**, configurare anche:

      **Disabilita le richieste utente per la convalida del server nella fase 1 di PEAP**: se questa opzione è impostata su **Sì** nella fase 1 di negoziazione PEAP, non vengono visualizzate le richieste utente che richiedono di autorizzare nuovi server PEAP per le autorità di certificazione attendibili. Selezionare **No** per visualizzare le richieste. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

    - **Richiedi cryptobinding**: **Sì** impedisce le connessioni ai server PEAP che non usano cryptobinding durante la negoziazione PEAP. **No** non richiede cryptobinding. Quando questa opzione è impostata su **Non configurato**, Intune non modifica o aggiorna questa impostazione.

    **AUTENTICAZIONE CLIENT**

    - **Certificato client per l'autenticazione client (certificato di identità)** : da usare con il tipo EAP **EAP-TLS**. Scegliere il profilo di certificato usato per autenticare la connessione.

    - **Metodo di autenticazione**: da usare con il tipo EAP **EAP-TTLS**. Selezionare il metodo di autenticazione per la connessione:  

      - **Certificati**: selezionare il certificato client che corrisponde al certificato di identità presentato al server.
      - **Nome utente e password**: immettere un **metodo non EAP (identità interna)** per l'autenticazione. Le opzioni disponibili sono:

        - **Password Authentication Protocol (PAP)**
        - **Challenge Handshake (CHAP)**
        - **Microsoft CHAP (MS-CHAP)**
        - **Microsoft CHAP versione 2 (MS-CHAP v2)**

    - **Privacy dell'identità (identità esterna)** : da usare con il tipo EAP **EAP-TTLS**. Immettere il testo inviato in risposta a una richiesta di identità EAP. Questo testo può essere costituito da qualsiasi valore. Durante l'autenticazione, viene inviata inizialmente questa identità anonima, seguita da quella effettiva inviata tramite un tunnel sicuro.

- **Impostazioni del proxy aziendale**: scegliere questa impostazione per usare le impostazioni proxy all'interno dell'organizzazione. Le opzioni disponibili sono:
  - **Nessuno**: non sono state configurate impostazioni proxy.
  - **Configura manualmente**: immettere l'**indirizzo IP del server proxy** e il relativo **numero di porta**.
  - **Configura automaticamente**: immettere l'URL che punta a uno script di configurazione automatica del proxy. Immettere ad esempio `http://proxy.contoso.com/proxy.pac`.

- **Imponi la conformità del profilo Wi-Fi con lo standard FIPS (Federal Information Processing Standard)** : scegliere **Sì** quando si esegue la convalida in base allo standard FIPS 140-2. Questo standard è richiesto per tutte le agenzie governative federali degli Stati Uniti che usano sistemi di sicurezza basati su crittografia per proteggere informazioni sensibili ma non classificate archiviate in modalità digitale. Scegliere **No** per non essere conformi a FIPS.

## <a name="use-an-imported-settings-file"></a>Usare un file di impostazioni importato

Per le impostazioni non disponibili in Intune, è possibile esportare le impostazioni Wi-Fi da un altro dispositivo Windows. Questa esportazione crea un file XML contenente tutte le impostazioni. Importare quindi il file in Intune e usarlo come profilo Wi-Fi. Vedere [Esportare e importare impostazioni Wi-Fi per i dispositivi Windows](wi-fi-settings-import-windows-8-1.md).

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma potrebbe non essere operativo. Assicurarsi di [assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

## <a name="more-resources"></a>Altre risorse

- [Impostazioni Wi-Fi di Windows 8.1](wi-fi-settings-import-windows-8-1.md)
- [Panoramica delle impostazioni Wi-Fi](wi-fi-settings-configure.md), incluse altre piattaforme
