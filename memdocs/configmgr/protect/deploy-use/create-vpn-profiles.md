---
title: Come creare profili VPN
titleSuffix: Configuration Manager
description: Informazioni sulla creazione dei profili VPN in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694249"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Come creare profili VPN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta più tipi di connessione VPN. Per altre informazioni sui tipi di connessione disponibili per le diverse piattaforme per dispositivi, vedere [Profili VPN](vpn-profiles.md).

Per le connessioni VPN di terze parti, distribuire l'app VPN prima di distribuire il profilo VPN. Se si non distribuisce l'app, verrà richiesto agli utenti di farlo quando tentano di connettersi alla VPN. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>Creare un profilo VPN

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità**, espandere **Accesso risorse aziendali** e selezionare il nodo **Profili VPN**.

1. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere **Crea profilo VPN**.

1. Nella pagina **Generale** della Creazione guidata profilo VPN specificare le informazioni seguenti:

    - **Nome**: immettere un nome univoco per identificare il profilo VPN nella console.

        > [!NOTE]
        > Non usare i caratteri seguenti nel nome del profilo VPN: `\/:*?<>|; `. Il profilo VPN di Windows non supporta questi caratteri speciali.

    - **Descrizione**: facoltativamente, immettere una descrizione per specificare altre informazioni sul profilo VPN.

    - **Tipo di profilo VPN**: selezionare la piattaforma appropriata.

        Se si seleziona la piattaforma di **Windows 8.1**, è anche possibile scegliere **Importa da file**. Questa azione importa le informazioni del profilo VPN da un file XML. Se si seleziona questa opzione, il resto della procedura guidata include semplicemente le pagine seguenti: **Piattaforme supportate** e **Importa profilo VPN**.

1. Nella pagina **Piattaforme supportate** selezionare le versioni del sistema operativo supportate dal profilo VPN.

1. Nella pagina **Connessione** specificare le informazioni seguenti:

    - **Tipo di connessione**: Selezionare il tipo di connessione VPN. Per altre informazioni sui tipi supportati, vedere [Profili VPN](vpn-profiles.md).

    - **Elenco server**: aggiungere un nuovo server da usare per la connessione VPN. In base al tipo di connessione è possibile aggiungere uno o più server VPN e specificare il server predefinito.

    - **Ignora VPN se connessa alla rete aziendale**: configurare i client in modo da non usare la VPN quando si trovano nella rete interna. Se necessario, specificare un nome DNS specifico della connessione.

1. Nella pagina **Metodo di autenticazione** della procedura guidata scegliere un metodo supportato dal tipo di connessione. Le impostazioni e le opzioni disponibili in questa pagina variano a seconda del tipo di connessione selezionato. Per altre informazioni, vedere [Informazioni di riferimento sul metodo di autenticazione](#bkmk_auth).

1. Nella pagina **Impostazioni proxy**, se la VPN usa un server proxy, selezionare una delle opzioni in base a quanto appropriato per l'ambiente. Fornire quindi le informazioni di configurazione per il proxy.

1. La pagina **Applicazioni** si applica solo ai profili Windows 10. Aggiungere app desktop e universali che si connettono automaticamente alla VPN. Il tipo di app determina l'identificatore dell'app:

    - Per un'*app desktop*, specificare il percorso file dell'app.

    - Per un'*app universale*, specificare il nome della famiglia di pacchetti (PFN). Per sapere come individuare il nome PFN per un'app, vedere la sezione relativa al [reperimento di un nome di famiglia di pacchetti per la VPN per app](find-a-pfn-for-per-app-vpn.md).

    È anche possibile configurare l'opzione **Solo le app elencate possono usare questa VPN**.

    > [!IMPORTANT]
    > Proteggere tutti gli elenchi di app associate compilate per la configurazione di una VPN per app. Se l'elenco viene modificato da un utente non autorizzato e quindi lo si importa nell'elenco di app della VPN per app, si autorizza potenzialmente l'accesso alla VPN da parte di app che non devono potervi accedere.

1. La pagina **Limiti** si applica solo ai profili Windows 10 per la configurazione dei limiti della VPN. È possibile aggiungere le opzioni seguenti:

    - **Regole del traffico di rete**: impostare i protocolli, la porta locale, la porta remota e gli intervalli di indirizzi per l'abilitazione della connessione VPN.  

        > [!Note]
        > Se non si crea una regola del traffico di rete, verranno abilitati tutti i protocolli, le porte e gli intervalli di indirizzi. Dopo la creazione di una regola, vengono usati dalla connessione VPN solo i protocolli, le porte e gli intervalli di indirizzi specificati in tale regola o nelle regole aggiuntive.

    - **Nomi e server DNS**: server DNS usati dalla connessione VPN dopo che il dispositivo ha stabilito la connessione.

    - **Route**: route di rete che usano la connessione VPN. La creazione di più di 60 route può causare errori dei criteri.

1. Completare la procedura guidata.

Il nuovo profilo VPN viene visualizzato nel nodo **Profili VPN** dell'area di lavoro **Asset e conformità** .

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a> Informazioni di riferimento sul metodo di autenticazione

I metodi di autenticazione VPN disponibili dipendono dal tipo di connessione:

### <a name="certificates"></a>Certificati

Se il certificato client esegue l'autenticazione in un server RADIUS, ad esempio un server dei criteri di rete, impostare il nome alternativo del soggetto nel certificato sul nome dell'entità utente.

Tipi di connessione supportati:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- VPN mobile Check Point

### <a name="username-and-password"></a>Nome utente e password

Tipi di connessione supportati:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- VPN mobile Check Point

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Tipi di connessione supportati:

- Microsoft SSL (SSTP)
- Microsoft Automatico
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft PEAP (Protected EAP)

Tipi di connessione supportati:

- Microsoft SSL (SSTP)
- Microsoft Automatico
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Password protetta Microsoft (EAP-MSCHAP v2)

Tipi di connessione supportati:

- Microsoft SSL (SSTP)
- Microsoft Automatico
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Smart card o altro certificato

Tipi di connessione supportati:

- Microsoft SSL (SSTP)
- Microsoft Automatico
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Tipi di connessione supportati:

- Microsoft SSL (SSTP)
- Microsoft Automatico
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Usa certificati computer

Tipi di connessione supportati:

- IKEv2

### <a name="additional-authentication-options"></a>Opzioni di autenticazione aggiuntive

Quando la versione del client Windows lo supporta, è disponibile l'opzione **Configura** per il metodo di autenticazione. Questa opzione consente di aprire la finestra delle proprietà di Windows per configurare il metodo di autenticazione.

A seconda delle opzioni selezionate, può essere necessario specificare altre informazioni, ad esempio:

- **Memorizza le credenziali utente a ogni accesso**: le credenziali utente vengono memorizzate in modo che gli utenti non debbano immetterle ogni volta che si connettono.  

- **Selezionare un certificato client per l'autenticazione client**: selezionare un profilo del certificato SCEP client creato in precedenza per autenticare la connessione VPN. Per altre informazioni, vedere [Creare profili certificato PFX](create-certificate-profiles.md).

## <a name="next-steps"></a>Passaggi successivi

- Per le connessioni VPN di terze parti, distribuire l'app VPN prima di distribuire il profilo VPN. Se si non distribuisce l'app, verrà richiesto agli utenti di farlo quando tentano di connettersi alla VPN. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../apps/deploy-use/deploy-applications.md).

- Distribuire il profilo VPN. Per altre informazioni vedere [Come distribuire i profili](deploy-wifi-vpn-email-cert-profiles.md).
