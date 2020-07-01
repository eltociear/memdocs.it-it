---
title: Certificati per il gateway di gestione cloud
titleSuffix: Configuration Manager
description: Informazioni sui diversi certificati digitali da usare con il gateway di gestione cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: b5a9a4a7f23942ac06dc16a0b54b657c7fd617a9
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715612"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificati per il gateway di gestione cloud

*Si applica a: Configuration Manager (Current Branch)*

In base allo scenario in cui si gestiscono i client su Internet con il gateway di gestione cloud, è necessario usare uno o più dei seguenti certificati digitali:  

- [Certificato di autenticazione server del gateway di gestione cloud](#bkmk_serverauth)  
  - [Certificato radice trusted del gateway di gestione cloud per i client](#bkmk_cmgroot)  
  - [Certificato di autenticazione server rilasciato da un provider pubblico](#bkmk_serverauthpublic)  
  - [Certificato di autenticazione server rilasciato da un'infrastruttura a chiave pubblica di tipo Enterprise](#bkmk_serverauthpki)  

- [Certificato di autenticazione client](#bkmk_clientauth)
  - [Punto di connessione di CMG](#bkmk_cmgcp)
  - [Certificato radice trusted del client per il gateway di gestione cloud](#bkmk_clientroot)  

- [Abilitare i punti di gestione per HTTPS](#bkmk_mphttps)  

- [Certificato di gestione di Azure](#bkmk_azuremgmt)  

Per altre informazioni sui diversi scenari, vedere [Pianificare il gateway di gestione cloud](plan-cloud-management-gateway.md).

## <a name="general-information"></a>Informazioni generali

<!--SCCMDocs issue #779-->
I certificati per Cloud Management Gateway supportano le configurazioni seguenti:  

- Lunghezza della chiave 2048 o 4096 bit

- Provider di archiviazione chiavi per le chiavi private dei certificati. Per altre informazioni, vedere [Panoramica dei certificati CNG](../../../plan-design/network/cng-certificates-overview.md).  

- Quando si configura Windows con i criteri seguenti: **Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma**  

- **TLS 1.2**. Per altre informazioni, vedere [Come abilitare TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a> Certificato di autenticazione server del gateway di gestione cloud

*Questo certificato è necessario in tutti gli scenari.*

Usare questo certificato quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Il gateway di gestione cloud crea un servizio HTTPS a cui si connettono i client basati su Internet. Il server richiede un certificato di autenticazione server per compilare il canale sicuro. Acquisire un certificato per questo scopo da un provider pubblico o inviarlo dall'infrastruttura a chiave pubblica. Per altre informazioni, vedere [Certificato radice trusted del gateway di gestione cloud per i client](#bkmk_cmgroot).

> [!NOTE]
> Il certificato di autenticazione server di Cloud Management Gateway supporta i caratteri jolly. Alcune autorità di certificazione rilasciano certificati in cui viene usato un carattere jolly per il nome host. Ad esempio, `*.contoso.com` Alcune organizzazioni usano certificati con caratteri jolly per semplificare l'infrastruttura a chiave pubblica e ridurre i costi di manutenzione.<!--491233-->  
>
> Per altre informazioni su come usare un certificato con caratteri jolly con CMG, vedere [Impostare un Cloud Management Gateway](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->  

Questo certificato richiede un nome univoco globale per identificare il servizio in Azure. Prima di richiedere un certificato, verificare che il nome di dominio di Azure sia univoco. Ad esempio, *GraniteFalls.CloudApp.Net*.

1. Accedere al [portale di Azure](https://portal.azure.com).
1. Selezionare **Tutte le risorse** e quindi **Aggiungi**.
1. Cercare **Servizio cloud**. Selezionare **Crea**.
1. Digitare il prefisso desiderato nel campo **Nome DNS**, ad esempio *GraniteFalls*. L'interfaccia indica se il nome di dominio è disponibile o se è già in uso in un altro servizio.

    > [!Important]  
    > Non creare il servizio nel portale, ma usare questo processo solo per verificare la disponibilità del nome.

Se si abilita anche Cloud Management Gateway per il contenuto, verificare che il nome del servizio CMG sia anche un nome di account di archiviazione di Azure univoco. Se il nome del servizio cloud CMG è univoco ma il nome dell'account di archiviazione non lo è, Configuration Manager non riesce a effettuare il provisioning del servizio in Azure. Ripetere questa procedura nel portale di Azure con le modifiche seguenti:

- Cercare **Account di archiviazione**
- Testare il nome nel campo **Nome account di archiviazione**

Il prefisso del nome DNS, ad esempio *GraniteFalls*, deve avere una lunghezza compresa tra i 3 e i 24 caratteri e usare solo caratteri alfanumerici. Non usare i caratteri speciali, ad esempio il trattino (`-`).<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a> Certificato radice trusted del gateway di gestione cloud per i client

I client devono considerare attendibile il certificato di autenticazione server del gateway di gestione cloud. Esistono due metodi per confermare l'attendibilità:

- Usare un certificato di un provider pubblico considerato attendibile a livello globale. Ad esempio, tra gli altri, DigiCert, Thawte, o VeriSign. I client Windows includono le autorità di certificazione (CA) che rilasciano i certificati radice trusted da questi provider. Usando un certificato di autenticazione server rilasciato da uno di questi provider, i client confermano automaticamente l'attendibilità.  

- Usare un certificato rilasciato da un'autorità di certificazione globale (enterprise) dall'infrastruttura a chiave pubblica. Nella maggior parte delle implementazioni di infrastruttura a chiave pubblica di tipo Enterprise le autorità di certificazione radice attendibili vengono aggiunte ai client di Windows. Ad esempio, usando i servizi certificati Active Directory con criteri di gruppo. Se si rilascia il certificato di autenticazione server per il gateway di gestione cloud da un'autorità di certificazione che i client non considerano automaticamente attendibile, aggiungere il certificato radice trusted di tale autorità ai client basati su Internet.  

  - È inoltre possibile usare i profili dei certificati di Configuration Manager per eseguire il provisioning dei certificati nei client. Per altre informazioni, vedere l'[introduzione alle raccolte](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).

  - Se si intende [installare il client di Configuration Manager da Intune](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client), è anche possibile usare i profili certificato di Intune per eseguire il provisioning dei certificati nei client. Per altre informazioni, vedere [Configurare un profilo di certificato](../../../../../intune/protect/certificates-configure.md).

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a> Certificato di autenticazione server rilasciato da un provider pubblico

Un provider di certificati di terze parti non può creare un certificato per CloudApp.net, perché il dominio è di proprietà di Microsoft. È possibile ottenere solo un certificato emesso per un dominio di cui si è proprietari. Il motivo principale per l'acquisizione di un certificato da un provider di terze parti è che i client già considerano attendibile il certificato radice del provider.

Usare la seguente procedura per creare un alias DNS:

1. Creare un record di nome canonico (CNAME) nel DNS pubblico dell'organizzazione. Questo record crea un alias per il gateway di gestione cloud con un nome descrittivo usato dall'utente nel certificato pubblico.

    Ad esempio, Contoso assegna al proprio CMG il nome **GraniteFalls**. Questo nome diventa **GraniteFalls.CloudApp.Net** in Azure. Nello spazio dei nomi contoso.com del DNS pubblico di Contoso l'amministratore DNS crea un nuovo record CNAME **GraniteFalls.Contoso.com** per il nome host effettivo, **GraniteFalls.CloudApp.net**.  

2. Richiedere un certificato di autenticazione server da un provider pubblico usando il nome comune dell'alias CNAME.
Ad esempio, Contoso usa **GraniteFalls.Contoso.com** per il nome comune del certificato.  

3. Creare il gateway di gestione cloud nella console di Configuration Manager usando questo certificato. Nella pagina **Impostazioni** della Creazione guidata del gateway di gestione cloud:  

    - Quando si aggiunge il certificato del server per questo servizio cloud (da **File di certificato**), la procedura guidata estrae il nome host dal nome comune del certificato come nome del servizio.  

    - Aggiunge quindi tale nome host a **cloudapp.net** o **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti come FQDN del servizio per creare il servizio in Azure.  

    - Ad esempio, quando Contoso crea il gateway di gestione cloud, Configuration Manager estrae il nome host **GraniteFalls** dal nome comune del certificato. Azure crea il servizio effettivo come **GraniteFalls.CloudApp.net**.  

Quando si crea l'istanza CMG in Configuration Manager, mentre il certificato ha GraniteFalls.Contoso.com, Configuration Manager estrae solo il nome host, ad esempio: GraniteFalls. Questo nome host viene accodato a CloudApp.net, che Azure richiede quando crea un servizio cloud. L'alias CNAME nello spazio dei nomi DNS per il dominio, Contoso.com, esegue il mapping dei due nomi di dominio completi. Configuration Manager offre ai client i criteri per accedere al CMG, il mapping DNS li collega in modo che possano accedere in modo sicuro al servizio in Azure.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a> Certificato di autenticazione server rilasciato da un'infrastruttura a chiave pubblica di tipo Enterprise

Creare un certificato SSL personalizzato per il gateway di gestione cloud identico a quello di un punto di distribuzione cloud. Seguire le istruzioni per la [distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) procedendo in modo diverso per le operazioni seguenti:

- Quando si richiede il certificato del server Web personalizzato, specificare un FQDN per il nome comune del certificato. Il nome può essere un nome di dominio pubblico di cui si è proprietari o è possibile usare il dominio cloudapp.net. Se si usa il proprio dominio pubblico, fare riferimento al processo sopra descritto per la creazione di un alias DNS nel DNS pubblico dell'organizzazione.  

- Quando si usa il dominio pubblico cloudapp.net per il certificato CMG del server Web:  

  - Nel cloud pubblico di Azure usare un nome che termina con **cloudapp.net**  

  - Usare un nome che termina con **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a> Certificato di autenticazione client

Requisiti per il certificato di autenticazione client:

- Questo certificato è necessario per i client basati su Internet che eseguono Windows 8.1 e i dispositivi Windows 10 non aggiunti ad Azure Active Directory (Azure AD).
- Potrebbe essere necessario per il punto di connessione di CMG. Per altre informazioni, vedere [Punto di connessione di CMG](#bkmk_cmgcp).
- Non è necessario per i client Windows 10 aggiunti ad Azure AD.
- Se la versione del sito è 2002 o successiva, i dispositivi possono usare un token rilasciato dal sito. Per altre informazioni, vedere [Autenticazione basata su token per CMG](../../deploy/deploy-clients-cmg-token.md).

I client usano questo certificato per l'autenticazione con il gateway di gestione cloud. I dispositivi Windows 10 ibridi o aggiunti a un dominio cloud non richiedono questo certificato perché usano Azure AD per l'autenticazione.

Eseguire il provisioning del certificato all'esterno del contesto di Configuration Manager. Ad esempio, usare Servizi certificati Active Directory e i criteri di gruppo per rilasciare i certificati di autenticazione client. Per altre informazioni, vedere [Distribuzione del certificato client per computer Windows](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

> [!NOTE]
> Microsoft consiglia di aggiungere i dispositivi ad Azure AD. I dispositivi basati su Internet possono usare Azure AD per l'autenticazione con Configuration Manager. Sono inoltre supportati scenari di dispositivi e utenti in cui il dispositivo è connesso a Internet o è connesso alla rete interna. Per altre informazioni, vedere [Installare e registrare il client usando l'identità di Azure AD](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> A partire dalla versione 2002,<!--5686290--> Configuration Manager estende il supporto per i dispositivi basati su Internet che non si connettono spesso alla rete interna, non possono essere aggiunti ad Azure AD e non hanno un metodo per installare un certificato rilasciato dall'infrastruttura a chiave pubblica. Per altre informazioni, vedere [Autenticazione basata su token per CMG](../../deploy/deploy-clients-cmg-token.md).

### <a name="cmg-connection-point"></a><a name="bkmk_cmgcp"></a> Punto di connessione di CMG

Per inoltrare in modo sicuro le richieste client, il punto di connessione di CMG richiede una connessione sicura con il punto di gestione. A seconda della modalità di configurazione dei dispositivi e dei punti di gestione, si determina la configurazione del punto di connessione di CMG.

- Il punto di gestione è HTTPS

  - I client hanno un certificato di autenticazione client: Il punto di connessione di CMG richiede un certificato di autenticazione client che corrisponda al certificato di autenticazione server nel punto di gestione HTTPS.

  - I client usano l'autenticazione di Azure AD o un token di Configuration Manager: Questo certificato non è necessario.

- Se si configura il punto di gestione per HTTP avanzato: Questo certificato non è necessario.

Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](#bkmk_mphttps).

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a> Certificato radice trusted del client per il gateway di gestione cloud

*Questo certificato è necessario quando si usano i certificati di autenticazione client. Quando tutti i client usano Azure AD per l'autenticazione, questo certificato non è obbligatorio.*

Usare questo certificato quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Il gateway di gestione client deve considerare attendibile il certificato di autenticazione del client. Per confermare l'attendibilità, specificare la catena di certificati radice trusted. Assicurarsi di aggiungere tutti i certificati nella catena di certificati. Ad esempio, se il certificato di autenticazione client viene emesso da una CA intermedia, aggiungere sia il certificato della CA intermedia che il certificato della CA radice.

> [!NOTE]  
> Quando si crea un CMG, non è più necessario specificare un certificato radice trusted nella pagina Impostazioni. Questo certificato non è necessario se si usa Azure AD per l'autenticazione client. Era richiesto nella procedura guidata. Se si usano certificati di autenticazione client PKI, è comunque necessario aggiungere un certificato radice trusted al CMG.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> Nella versione 1902 e nelle versioni precedenti è possibile aggiungere solo due autorità di certificazione radice attendibili e quattro autorità intermedie (subordinate).

#### <a name="export-the-client-certificates-trusted-root"></a>Esportare la radice attendibile del certificato client

Dopo aver emesso un certificato di autenticazione client per un computer, usare questo processo in tale computer per esportare la radice attendibile.

1. Aprire il menu Start. Digitare "esegui" per aprire la finestra di esecuzione. Aprire `mmc`.  

2. Dal menu file scegliere **Aggiungi/Rimuovi snap-in**.  

3. Nella finestra di dialogo Aggiungi o rimuovi snap-in selezionare **Certificati**, quindi selezionare **Aggiungi**.  

    1. Nella finestra di dialogo Snap-in certificati selezionare **Account del computer** e selezionare **Avanti**.  

    1. Nella finestra di dialogo Selezione computer selezionare **Computer locale** e quindi **Fine**.  

    1. Nella finestra di dialogo Aggiungi o rimuovi snap-in selezionare **OK**.  

4. Espandere **Certificati**, espandere **Personale** e selezionare **Certificati**.  

5. Selezionare un certificato il cui scopo designato è **Autenticazione client**.  

    1. Dal menu Azione selezionare **Apri**.  

    1. Passare alla scheda **Percorso certificazione**.  

    1. Selezionare il certificato successivo procedendo verso l'alto nella catena, quindi selezionare **Visualizza certificato**.  

6. Nella nuova finestra di dialogo Certificato passare alla scheda **Dettagli**. Selezionare **Copia su file**.  

7. Completare l'Esportazione guidata certificati usando il formato di certificato predefinito, **DER encoded binary X.509 (.CER)** . Prendere nota del nome e del percorso del certificato esportato.  

8. Esportare tutti i certificati presenti nel percorso di certificazione del certificato di autenticazione client originale. Prendere nota dei certificati esportati che rappresentano autorità di certificazione intermedie e di quelli che rappresentano autorità radice attendibili.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a> Abilitare i punti di gestione per HTTPS

Eseguire il provisioning del certificato all'esterno del contesto di Configuration Manager. Ad esempio, usare Servizi certificati Active Directory e i criteri di gruppo per rilasciare un certificato del server Web. Per altre informazioni, vedere [Requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md) e [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

Quando si usa l'opzione del sito **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**, il punto di gestione può essere HTTP. Per altre informazioni, vedere [HTTP migliorato](../../../plan-design/hierarchy/enhanced-http.md).

> [!TIP]
> Se non si usa il protocollo HTTP migliorato e l'ambiente include più punti di gestione, non è necessario abilitare HTTPS per tutti i punti per il gateway di gestione cloud. Configurare i punti di gestione abilitati per il gateway di gestione cloud come **Solo Internet**. I client locali non tenteranno di usarli.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Certificato HTTP migliorato per i punti di gestione

Quando si abilita il protocollo HTTP migliorato, il server del sito genera un certificato autofirmato denominato **SMS Role SSL Certificate**, (Certificato SSL ruolo SMS) emesso dal certificato Emissione SMS radice. Il punto di gestione aggiunge questo certificato al sito Web predefinito IIS associato alla porta 443.

### <a name="management-point-client-connection-mode-summary"></a>Riepilogo delle modalità di connessione client ai punti di gestione

Queste tabelle offrono un riepilogo che indica se il punto di gestione richiede HTTP o HTTPS, a seconda del tipo di client e di versione del sito.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Per i client basati su Internet che comunicano con il gateway di gestione cloud

Configurare un punto di gestione locale per consentire le connessioni dal gateway di gestione cloud con la modalità di connessione client indicata di seguito:

| Tipo di client   | Punto di gestione |
|------------------|------------------|
| Gruppo di lavoro        | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, HTTPS |
| Aggiunto a un dominio AD | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, HTTPS |
| Aggiunto ad Azure AD  | E-HTTP, HTTPS |
| Aggiunto ad AD ibrido    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Nota 1**: questa configurazione richiede che il client usi un [certificato di autenticazione client](#bkmk_clientauth) e supporti solo scenari incentrati sui dispositivi.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Per i client locali che comunicano con il punto di gestione locale

Configurare un punto di gestione locale con la modalità di connessione client indicata di seguito:

| Tipo di client   | Punto di gestione |
|------------------|------------------|
| Gruppo di lavoro        | HTTP, HTTPS |
| Aggiunto a un dominio AD | HTTP, HTTPS |
| Aggiunto ad Azure AD  | HTTPS       |
| Aggiunto ad AD ibrido    | HTTP, HTTPS |

> [!NOTE]  
> I client aggiunti a un dominio AD supportano sia gli scenari incentrati sui dispositivi, sia quelli incentrati sull'utente che comunicano con un punto di gestione HTTP o HTTPS.  
>
> I client aggiunti ad Azure AD e AD ibrido possono comunicare via HTTP per gli scenari incentrati sui dispositivi, ma devono usare E-HTTP o HTTPS per abilitare gli scenari incentrati sull'utente. In caso contrario, si comportano come client del gruppo di lavoro.  

#### <a name="legend-of-terms"></a>Legenda dei termini

- *Gruppo di lavoro*: il dispositivo non è stato aggiunto a un dominio o ad Azure AD, ma ha un [certificato di autenticazione client](#bkmk_clientauth).
- *Aggiunto a un dominio AD*: il dispositivo viene aggiunto a un dominio di Active Directory locale.
- *Aggiunto ad Azure AD*: (o aggiunto al dominio cloud) il dispositivo viene aggiunto a un tenant di Azure AD. Per altre informazioni, vedere [Dispositivi aggiunti ad Azure AD](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join).
- *Aggiunto ad AD ibrido*: il dispositivo viene aggiunto ad Active Directory locale e registrato con Azure AD. Per altre informazioni, vedere [Dispositivi aggiunti ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid).
- *HTTP*: nelle proprietà del punto di gestione le connessioni client sono impostate su **HTTP**.
- *HTTPS*: nelle proprietà del punto di gestione le connessioni client sono impostate su **HTTPS**.
- *E-HTTP*: nella scheda **Sicurezza delle comunicazioni** delle proprietà del sito configurare le impostazioni di sistema del sito per **HTTPS o HTTP** e abilitare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**. Si configura il punto di gestione per il protocollo HTTP. Il punto di gestione HTTP è pronto per la comunicazione HTTP e HTTPS (scenari di autenticazione basata su token).

    > [!Note]
    > Nella versione 1902 e in quelle precedenti questa scheda è denominata **Comunicazione computer client**.<!-- SCCMDocs#1645 -->

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a> Certificato di gestione di Azure

*Questo certificato è obbligatorio per le distribuzioni di servizi classiche. Non è necessario per le distribuzioni di Azure Resource Manager.*

> [!Important]  
> A partire dalla versione 1810, le distribuzioni classiche del servizio in Azure sono deprecate in Configuration Manager. Iniziare a usare le distribuzioni di Azure Resource Manager per il gateway di gestione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](plan-cloud-management-gateway.md#azure-resource-manager).
>
> A partire da Configuration Manager versione 1902, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze di Cloud Management Gateway. Questo certificato non è necessario in Configuration Manager versione 1902 o successive.<!-- 3605704 -->

Specificare questo certificato nel portale di Azure quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Per creare il gateway di gestione cloud in Azure, il punto di connessione del servizio Configuration Manager deve prima eseguire l'autenticazione alla sottoscrizione di Azure. Quando si usa una distribuzione classica del servizio, per l'autenticazione viene usato il certificato di gestione di Azure. Un amministratore di Azure carica questo certificato nella sottoscrizione dell'utente. Quando si crea il gateway di gestione cloud nella console di Configuration Manager specificare questo certificato.

Per altre informazioni e istruzioni su come caricare un certificato di gestione, vedere gli articoli seguenti nella documentazione di Azure:

- [Servizi cloud e certificati di gestione](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Caricare un certificato di gestione dei servizi di Azure](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Assicurarsi di copiare l'ID sottoscrizione associato al certificato di gestione. Usare questo certificato per creare il gateway di gestione cloud nella console di Configuration Manager.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare il gateway di gestione cloud](setup-cloud-management-gateway.md)  

- [Domande frequenti sul gateway di gestione cloud](cloud-management-gateway-faq.md)  

- [Sicurezza e privacy per il gateway di gestione del cloud](security-and-privacy-for-cloud-management-gateway.md)  
