---
title: HTTP avanzato
titleSuffix: Configuration Manager
description: Usare l'autenticazione moderna per proteggere le comunicazioni client senza dover usare certificati PKI.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79b4119a12826596fcc91fa1b4ead4e151e2ddd8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262099"
---
# <a name="enhanced-http"></a>HTTP avanzato

*Si applica a: Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1806 come [funzionalità di una versione non definitiva](../../servers/manage/pre-release-features.md). A partire dalla versione 1810, questa funzionalità non è più in versione non definitiva.  

Microsoft consiglia l'uso delle comunicazioni HTTPS per tutti i percorsi di comunicazione di Configuration Manager, ma alcuni clienti possono avere difficoltà a causa del sovraccarico di gestione dei certificati PKI.

Configuration Manager versione 1806 include miglioramenti per le modalità di comunicazione dei client con i sistemi del sito. Questi miglioramenti hanno due obiettivi principali:  

- Proteggere le comunicazioni client sensibili senza dover usare certificati di autenticazione server PKI.  

- I client possono accedere in modo sicuro al contenuto dai punti di distribuzione senza la necessità di un account di accesso alla rete, di un certificato PKI del client e dell'autenticazione di Windows.  

Tutte le altre comunicazioni client sono su HTTP. Usare HTTP avanzato non è come abilitare HTTPS per la comunicazione client o un sistema del sito.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> I certificati PKI rimangono un'opzione valida per i clienti con i requisiti seguenti:  
>
> - Tutte le comunicazioni client sono su HTTPS  
> - Controllo avanzato dell'infrastruttura di firma
>
> Inoltre, se si sta già usando l'infrastruttura a chiave pubblica (PKI), il certificato PKI associato in IIS verrà usato anche se è attivato HTTP avanzato.



## <a name="scenarios"></a><a name="bkmk_scenario"></a> Scenari

Gli scenari seguenti traggono vantaggio da questi miglioramenti:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> Scenario 1: Da client a punto di gestione

<!--1356889-->
I [dispositivi aggiunti ad Azure Active Directory (Azure AD)](/azure/active-directory/devices/concept-azure-ad-join) e i dispositivi con un [token emesso di Configuration Manager](../../clients/deploy/deploy-clients-cmg-token.md) possono comunicare con un punto di gestione configurato per HTTP se si abilita il protocollo HTTP avanzato per il sito. Con il protocollo HTTP avanzato abilitato, il server del sito genera un certificato per il punto di gestione in modo che possa comunicare tramite un canale sicuro.

> [!Note]  
> Questo scenario non richiede l'uso di un punto di gestione abilitato per HTTPS, ma è supportato come alternativa all'uso di HTTP avanzato. Per altre informazioni sull'uso di un punto di gestione abilitato per HTTPS, vedere [Abilitare i punti di gestione per HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> Scenario 2: Da client a punto di distribuzione

<!--1358228-->
Un gruppo di lavoro o un client aggiunto ad Azure AD può eseguire l'autenticazione e scaricare contenuto usando un canale sicuro da un punto di distribuzione configurato per HTTP. Questi tipi di dispositivi possono eseguire l'autenticazione e scaricare contenuto anche da un punto di distribuzione configurato per HTTPS senza richiedere un certificato PKI sul client. L'aggiunta di un certificato di autenticazione client a un gruppo di lavoro o un client aggiunto ad Azure AD è un'operazione complessa.

Questo comportamento comprende gli scenari di distribuzione del sistema operativo con una sequenza di attività eseguita da supporti di avvio, PXE o Software Center. Per altre informazioni, vedere [Account di accesso alla rete](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> Scenario 3: Identità del dispositivo di Azure AD

<!--1358460-->
Un dispositivo aggiunto ad Azure AD o un [dispositivo di Azure AD ibrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) senza un utente di Azure AD connesso può comunicare in modo sicuro con il relativo sito assegnato. L'identità del dispositivo basata sul cloud è ora sufficiente per l'autenticazione con il gateway di gestione cloud e il punto di gestione negli scenari incentrati sui dispositivi. Un token utente è comunque necessario negli scenari incentrati sull'utente.  


## <a name="features"></a>Caratteristiche

Le seguenti funzionalità di Configuration Manager supportano o richiedono HTTP avanzato:

- [Gateway di gestione cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Distribuzione del sistema operativo senza un account di accesso alla rete](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Abilitare la co-gestione per nuovi dispositivi Windows 10 basati su Internet](../../../comanage/tutorial-co-manage-new-devices.md)
- [Approvazioni di app tramite posta elettronica](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Servizio di amministrazione](../../../develop/adminservice/overview.md)
- [Visualizzare le console connesse di recente](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Il punto di aggiornamento software e gli scenari correlati hanno sempre supportato il traffico HTTP sicuro con i client, nonché con il gateway di gestione cloud. Usano un meccanismo con il punto di gestione diverso dall'autenticazione basata sui certificati o sui token.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Prerequisiti  

- Un punto di gestione configurato per connessioni client HTTP. Impostare questa opzione nella scheda **Generale** delle proprietà del ruolo del punto di gestione.  

- Un punto di distribuzione configurato per connessioni client HTTP. Impostare questa opzione nella scheda **Comunicazioni** delle proprietà del ruolo del punto di distribuzione. Non abilitare l'opzione **Consenti connessione anonima dei client**.  

- Eseguire l'onboarding del sito in Azure AD per la gestione del cloud.  

- *Solo per lo [scenario 3](#bkmk_scenario3)* : un client che esegue Windows 10 versione 1803 o successiva e aggiunto ad Azure AD. Il client richiede questa configurazione per l'autenticazione del dispositivo Azure AD.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Configurare il sito

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Siti**. Selezionare il sito e scegliere **Proprietà** nella barra multifunzione.  

2. Passare alla scheda **Comunicazione computer client**.

    > [!Note]
    > A partire dalla versione 1906, questa scheda è denominata **Communication Security** (Sicurezza comunicazione).<!-- SCCMDocs#1645 -->  

    Selezionare l'opzione **HTTPS o HTTP**. Quindi abilitare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**.

> [!Tip]
> Attendere fino a 30 minuti che il punto di gestione riceva e configuri il nuovo certificato del sito.

<!--3798957-->
A partire dalla versione 1902, è anche possibile abilitare HTTP avanzato per il sito di amministrazione centrale. Usare lo stesso processo e aprire le proprietà del sito di amministrazione centrale. Questa azione HTTP avanzato solo per i ruoli Provider SMS nel sito di amministrazione centrale. Non è un'impostazione globale valida per tutti i siti nella gerarchia.

È possibile visualizzare questi certificati nella console di Configuration Manager. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e selezionare il nodo **Certificati**. Cercare il certificato radice **Emissione SMS**, nonché i certificati di ruolo del server del sito emessi dalla radice di emissione SMS.

Per altre informazioni sul modo in cui il client comunica con il punto di gestione e il punto di distribuzione in questa configurazione, vedere [Comunicazioni da client a sistemi e servizi del sito](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>Vedere anche

- [Pianificare la sicurezza](../security/plan-for-security.md)  

- [Sicurezza e privacy per i client di Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurare la sicurezza](../security/configure-security.md)  

- [Comunicazioni tra gli endpoint](communications-between-endpoints.md)  
