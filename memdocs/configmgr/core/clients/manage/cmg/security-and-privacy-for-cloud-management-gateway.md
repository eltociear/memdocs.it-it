---
title: Sicurezza e privacy per il gateway di gestione cloud
titleSuffix: Configuration Manager
description: Informazioni su indicazioni e consigli per la sicurezza e la privacy con il gateway di gestione cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 93427cb34b2216bf16f713818481e69573a4b0de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693239"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Sicurezza e privacy per il gateway di gestione cloud

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene informazioni relative alla sicurezza e alla privacy per il gateway di gestione cloud di Configuration Manager (CMG). Per altre informazioni, vedere [Plan for cloud management gateway](plan-cloud-management-gateway.md) (Pianificare il gateway di gestione cloud).

## <a name="cmg-security-details"></a>Dettagli relativi alla sicurezza per il gateway di gestione cloud

- Il gateway di gestione cloud accetta e gestisce le connessioni dai relativi punti di connessione. Usa l'autenticazione SSL reciproca tramite certificati e ID connessione.
- Il gateway di gestione cloud accetta e inoltra le richieste client usando i metodi seguenti:
    - Preautentica le connessioni usando l'autenticazione SSL reciproca tramite il certificato di autenticazione client basato su infrastruttura a chiave pubblica (PKI) o Azure AD.
      - IIS nelle istanze di macchina virtuale del gateway di gestione cloud verifica il percorso del certificato in base ai certificati radice trusted caricati nel gateway di gestione cloud.
      - IIS nell'istanza di macchina virtuale verifica anche la revoca del certificato client, se abilitata. Per altre informazioni, vedere [Pubblicare l'elenco di revoche di certificati (CRL)](#bkmk_crl).
    - L'elenco di revoche di certificati (CRL) controlla la radice del certificato di autenticazione client. Esegue anche la stessa convalida del punto di gestione per il client. Per altre informazioni, vedere [Rivedere le voci dell'elenco scopi consentiti ai certificati del sito](#bkmk_ctl).
    - Convalida e filtra le richieste client (URL) per verificare se un punto di connessione del gateway di gestione cloud può soddisfare la richiesta.  
    - Controlla la lunghezza del contenuto per ogni endpoint di pubblicazione.
    - Usa l'approccio round robin per bilanciare il carico tra i punti di connessione del gateway di gestione cloud nello stesso sito.
- Il punto di connessione del gateway di gestione cloud usa i metodi seguenti:
    - Crea connessioni HTTP/TCP coerenti con tutte le istanze virtuali del gateway di gestione cloud. Controlla e gestisce queste connessioni ogni minuto.
    - Usa l'autenticazione SSL reciproca con il gateway di gestione cloud tramite certificati.
    - Inoltra le richieste client in base ai mapping di URL.
    - Segnala lo stato della connessione per visualizzare lo stato di integrità del servizio nella console.
    - Genera un report sul traffico per ogni endpoint ogni cinque minuti.

### <a name="configuration-manager-client-facing-roles"></a>Ruoli destinati al client di Configuration Manager

Il punto di gestione e l'aggiornamento software ospitano gli endpoint in IIS che possono soddisfare le richieste client. Il gateway di gestione cloud non espone tutti gli endpoint interni. Ogni endpoint pubblicato del gateway di gestione cloud ha un mapping di URL.

- L'URL esterno è quello usato dal client per comunicare con il gateway di gestione cloud.
- L'URL interno è il punto di connessione del gateway di gestione cloud usato per inoltrare le richieste al server interno.

#### <a name="url-mapping-example"></a>Esempio di mapping di URL

Quando si abilita il traffico del gateway di gestione cloud in un punto di gestione, Configuration Manager crea un set interno di mapping di URL per ogni server del punto di gestione, ad esempio ccm_system, ccm_incoming e sms_mp. L'URL esterno dell'endpoint ccm_system del punto di gestione può essere simile a quanto segue:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
L'URL è univoco per ogni punto di gestione. Il client di Configuration Manager inserisce quindi il nome del punto di gestione abilitato per il gateway di gestione cloud nel relativo elenco di punti di gestione Internet. Il nome può essere simile a quanto segue:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
Il sito carica automaticamente tutti gli URL esterni pubblicati nel gateway di gestione cloud. In questo modo il gateway di gestione cloud potrà filtrare gli URL. Tutti i mapping di URL vengono replicati nel punto di connessione del gateway di gestione cloud. A questo punto, la comunicazione viene inoltrata ai server interni in base all'URL esterno dalla richiesta client.


## <a name="security-guidance-for-cmg"></a>Indicazioni relative alla sicurezza per il gateway di gestione cloud

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Pubblicare l'elenco di revoche di certificati (CRL)

Perché i client basati su Internet possano accedere, è necessario pubblicare l'elenco di revoche di certificati (CRL) dell'infrastruttura a chiave pubblica (PKI). Se il gateway di gestione cloud viene distribuito tramite l'infrastruttura a chiave pubblica (PKI), configurare il servizio per **verificare la revoca di certificato client** nella scheda Impostazioni. Questa impostazione consente al servizio di usare un elenco di revoche di certificati (CRL). Per altre informazioni, vedere [Pianificare revoche di certificati PKI](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Questa opzione CMG verifica il certificato di autenticazione client.

- Se il client usa l'autenticazione Azure AD, il CRL non è rilevante.
- Se si usa l'infrastruttura a chiave pubblica e si pubblica esternamente il CRL, abilitare questa opzione (scelta consigliata).
- Se si usa l'infrastruttura a chiave pubblica, non pubblicare il CRL, quindi disabilitare questa opzione.
- Se questa opzione non è configurata correttamente, può causare un aumento del traffico dai client al CMG. Questo traffico aggiuntivo può aumentare i dati in uscita di Azure e quindi i relativi costi.<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Rivedere le voci dell'elenco scopi consentiti ai certificati del sito

<!--503739-->
Ogni sito di Configuration Manager include un elenco di autorità di certificazione radice attendibili, vale a dire l'elenco scopi consentiti ai certificati. Per visualizzare e modificare l'elenco, accedere all'area di lavoro Amministrazione, espandere Configurazione del sito e selezionare Siti. Selezionare un sito e fare clic su Proprietà nella barra multifunzione. Passare alla scheda **Comunicazione computer client** e fare clic su **Imposta** in Autorità di certificazione radice attendibili.

> [!Note]
> A partire dalla versione 1906, questa è la scheda della **sicurezza della comunicazione**.<!-- SCCMDocs#1645 -->  

Usare un elenco scopi consentiti più restrittivo per un sito con un gateway di gestione cloud che usa l'autenticazione client PKI. In caso contrario, i client con certificati di autenticazione client emessi da qualsiasi radice attendibile che esiste già nel punto di gestione vengono automaticamente accettati per la registrazione del client.

Questo sottoinsieme conferisce agli amministratori maggiore controllo sulla sicurezza. L'elenco scopi consentiti limita il server ad accettare solo i certificati client che vengono emessi dalle autorità di certificazione nell'elenco scopi consentiti. Ad esempio, Windows viene fornito con un numero di certificati di autorità di certificazione di terze parti ben note, come VeriSign e Thawte. Per impostazione predefinita, il computer su cui è in esecuzione IIS ritiene attendibili i certificati concatenati a queste autorità di certificazione ben note. Se ISS non viene configurato con un elenco scopi consentiti, tutti i computer che hanno un certificato client emesso da una di queste autorità di certificazione vengono accettati come client di Configuration Manager validi. Se IIS viene configurato con un elenco scopi consentiti che non comprendeva queste autorità di certificazione, le connessioni client vengono rifiutate se il certificato è concatenato a tali autorità.

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a> Applicare TLS 1.2

<!-- SCCMDocs-pr#4021 -->

A partire dalla versione 1906, usare l'impostazione CMG per **applicare TLS 1.2**. Si applica solo alla macchina virtuale del servizio cloud di Azure. Non si applica ad alcun client o server del sito di Configuration Manager locale. Per altre informazioni su TLS 1.2, vedere [Come abilitare TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Passaggi successivi

- [Pianificare il gateway di gestione cloud](plan-cloud-management-gateway.md)
- [Configurare il gateway di gestione cloud](setup-cloud-management-gateway.md)
- [Domande frequenti sul gateway di gestione cloud](cloud-management-gateway-faq.md)
- [Certificati per il gateway di gestione del cloud](certificates-for-cloud-management-gateway.md)
