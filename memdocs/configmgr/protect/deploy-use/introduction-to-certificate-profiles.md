---
title: Introduzione ai profili certificato
titleSuffix: Configuration Manager
description: Informazioni sul funzionamento dei profili certificato in Configuration Manager con Servizi certificati Active Directory.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3598c95d1431915431d96b16c10c7c913741fe3d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699994"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Introduzione ai profili certificato in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I profili certificato vengono usati con Servizi certificati Active Directory e il ruolo del servizio Registrazione dispositivi di rete (NDES). È possibile creare e distribuire certificati di autenticazione per i dispositivi gestiti, in modo che gli utenti possano accedere facilmente alle risorse dell'organizzazione. Ad esempio, è possibile creare e distribuire profili certificato per fornire i certificati di cui gli utenti hanno bisogno per connettersi a connessioni VPN e wireless.

I profili certificato possono configurare automaticamente i dispositivi utente per l'accesso alle risorse dell'organizzazione, ad esempio reti Wi-Fi e server VPN. Gli utenti possono accedere a queste risorse senza installare manualmente i certificati o usare un processo fuori banda. I profili certificato sono utili per proteggere le risorse perché vengono usate più impostazioni di sicurezza supportate dall'infrastruttura a chiave pubblica (PKI). Ad esempio, è possibile richiedere l'autenticazione server per tutte le connessioni Wi-Fi e VPN perché i certificati richiesti sono stati distribuiti nei dispositivi gestiti.

I profili di certificato forniscono le seguenti funzionalità di gestione:  

- Registrazione e rinnovo del certificato da un'autorità di certificazione (CA) per i dispositivi che eseguono diversi tipi e versioni di sistemi operativi. Questi certificati possono poi essere usati per le connessioni Wi-Fi e VPN.  

- Distribuzione di certificati della CA radice attendibili e certificati della CA intermedi. Questi certificati configurano una catena di certificati nei dispositivi per le connessioni VPN e Wi-Fi quando è richiesta l'autenticazione del server.  

- Monitoraggio e creazione di report per i certificati installati.  

**Esempio 1**: Tutti i dipendenti devono accedere agli hotspot Wi-Fi in più uffici aziendali. Per consentire agli utenti di connettersi con facilità, distribuire per prima cosa i certificati necessari per la connessione Wi-Fi, quindi distribuire i profili Wi-Fi che fanno riferimento al certificato.  

**Esempio 2**: è disponibile un'infrastruttura a chiave pubblica (PKI). e si vuole passare a un metodo più flessibile e sicuro di distribuzione dei certificati. Gli utenti devono essere in grado di accedere alle risorse dell'organizzazione dai loro dispositivi personali, senza compromettere la sicurezza. Configurare i profili certificato con le impostazioni e i protocolli supportati per la piattaforma per dispositivi specifica. I dispositivi possono quindi richiedere automaticamente questi certificati a un server di registrazione con connessione Internet. Configurare quindi i profili VPN per usare questi certificati, in modo che il dispositivo possa accedere alle risorse dell'organizzazione.  

## <a name="types"></a>Tipi

Esistono tre tipi di profilo certificato:  

- **Certificato CA attendibile**: Consente di distribuire un certificato della CA radice attendibile o un certificato della CA intermedio. Questi certificati formano una catena di certificati quando il dispositivo deve eseguire l'autenticazione a un server.  

- **Simple Certificate Enrollment Protocol (SCEP)** : Consente di richiedere un certificato per un dispositivo o un utente usando il protocollo SCEP. Questo tipo richiede il ruolo del servizio Registrazione dispositivi di rete (NDES) in un server che esegue Windows Server 2012 R2 o versione successiva.

    Per creare un profilo certificato di tipo **Simple Certificate Enrollment Protocol (SCEP)** , creare prima un profilo **Certificato CA attendibile**.

- **Scambio informazioni personali (.pfx)** : Consente di richiedere un certificato PFX (noto anche come PKCS #12) per un dispositivo o un utente.<!--1321368--> Esistono due metodi per creare profili certificato PFX:

  - [Importare le credenziali](../../mdm/deploy-use/import-pfx-certificate-profiles.md) da certificati esistenti
  - [Definire un'autorità di certificazione](../../mdm/deploy-use/create-pfx-certificate-profiles.md) per elaborare le richieste

  > [!Note]  
  > Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

  È possibile usare Microsoft o Entrust come CA per i certificati di **scambio di informazioni personali (PFX)** .

## <a name="requirements"></a>Requisiti

Per distribuire i profili certificato che usano SCEP, installare il punto di registrazione certificati in un server del sistema del sito. Installare anche un modulo criteri per il servizio Registrazione dispositivi di rete (NDES), il Modulo criteri di Configuration Manager, in un server che esegue Windows Server 2012 R2 o versione successiva. Questo server richiede il ruolo Servizi certificati Active Directory. Richiede anche un servizio Registrazione dispositivi di rete (NDES) funzionante e accessibile ai dispositivi che richiedono i certificati. Se i dispositivi devono esetguire la registraizone per i certificati da Internet, il server NDES deve essere accessibile da Internet. Ad esempio, per abilitare in modo sicuro il traffico verso il server NDES da Internet è possibile usare [Azure Application Proxy](/azure/active-directory/manage-apps/application-proxy).

Anche i certificati PFX richiedono un punto di registrazione certificati. Specificare inoltre la CA per il certificato e le credenziali di accesso pertinenti. È possibile specificare Microsoft o Entrust come autorità di certificazione.  

Per altre informazioni sul modo in cui il servizio Registrazione dispositivi di rete supporta moduli criteri per consentire la distribuzione di certificati da parte di Configuration Manager, vedere [Uso di un modulo criteri con il servizio Registrazione dispositivi di rete](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\)).

A seconda dei requisiti, Configuration Manager supporta la distribuzione dei certificati in più archivi certificati in diversi tipi di dispositivi e sistemi operativi. Sono supportati i dispositivi e i sistemi operativi seguenti:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Usare software MDM Configuration Manager locale per gestire Windows Phone 8.1 e Windows 10 Mobile. Per altre informazioni, vedere [Software MDM locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Uno scenario tipico per Configuration Manager è l'installazione di certificati CA radice attendibili per autenticare i server Wi-Fi e VPN. Le connessioni tipiche usano i protocolli seguenti:

- Protocolli di autenticazione: EAP-TLS, EAP-TTLS e PEAP
- Protocolli di tunneling VPN: IKEv2, L2TP/IPsec e Cisco IPsec

Un certificato della CA radice aziendale deve essere installato nel dispositivo prima che il dispositivo possa richiedere i certificati usando un profilo certificato SCEP.  

È possibile specificare le impostazioni in un profilo certificato SCEP per richiedere certificati personalizzati per diversi ambienti o requisiti di connettività. La **Creazione guidata profilo certificato** ha due pagine per i parametri di registrazione. La prima, **Registrazione SCEP**, include le impostazioni per la richiesta di registrazione e la posizione in cui installare il certificato. Il secondo, **Proprietà certificato**, descrive il certificato richiesto stesso.  

## <a name="deploy"></a>Distribuisci

Quando si distribuisce un profilo certificato SCEP il client Configuration Manager elabora i criteri. Quindi richiede una password di verifica SCEP nel punto di gestione. Il dispositivo crea una coppia di chiavi pubblica/privata e genera una richiesta di firma del certificato (CSR). La richiesta viene inviata al server NDES. Il server NDES invia la richiesta al sistema del sito del punto di registrazione certificati tramite il modulo dei criteri NDES. Il punto di registrazione certificati convalida la richiesta, convalida la password di verifica SCEP e controlla che la richiesta non sia stata manomessa. Quindi approva o rifiuta la richiesta. Se approvata, il server registrazione dispositivi invia la richiesta di firma all'autorità di certificazione (CA) connessa per la firma. L'autorità di certificazione firma la richiesta e quindi restituisce il certificato al dispositivo richiedente.

Distribuire i profili certificato a raccolte di utenti o di dispositivi. È possibile specificare l'archivio di destinazione per ogni certificato. Le regole di applicabilità determinano se il dispositivo può installare il certificato.

Quando si distribuisce un profilo certificato in una raccolta utenti, l'[affinità utente-dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) stabilisce quale dei dispositivi degli utenti installa i certificati. Quando si distribuisce un profilo certificato con un certificato utente a una raccolta di dispositivi, per impostazione predefinita il dispositivo principale di ogni utente installa i certificati. Per installare il certificato in tutti i dispositivi degli utenti, modificare questo comportamento nella pagina **Registrazione SCEP** della **Creazione guidata profilo certificato**. Se i dispositivi fanno parte di un gruppo di lavoro, Configuration Manager non distribuisce i certificati utente.  

## <a name="monitor"></a>Monitoraggio

È possibile monitorare le distribuzioni dei profili certificato visualizzando i risultati o i report di conformità. Per altre informazioni, vedere [Come monitorare i profili certificato](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Revoca automatica

Configuration Manager revoca automaticamente i certificati utente e computer che sono stati distribuiti usando profili certificato nelle circostanze seguenti:  

- Il dispositivo è stato ritirato dalla gestione di Configuration Manager.  

- Il dispositivo è stato bloccato dalla gerarchia di Configuration Manager.  

Per revocare i certificati, il server del sito invia un comando di revoca all'autorità di certificazione emittente. Il motivo della revoca è **Termine operazione**.

> [!NOTE]
> Per revocare correttamente un certificato, l'account computer per il sito di livello superiore della gerarchia deve disporre dell'autorizzazione di **emissione e gestione certificati** nell'autorità di certificazione.
>
> Per maggiore sicurezza è anche possibile limitare i responsabili dell'autorità di certificazione nell'autorità stessa. Quindi assegnare solo a questo account le autorizzazioni per il modello di certificato specifico usato per i profili SCEP nel sito.

## <a name="next-steps"></a>Passaggi successivi

- [Come creare i profili certificato in Configuration Manager](create-certificate-profiles.md)

- [Configurare l'infrastruttura di certificazione](certificate-infrastructure.md)