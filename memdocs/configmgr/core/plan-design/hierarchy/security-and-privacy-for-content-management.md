---
title: Sicurezza e privacy per la gestione dei contenuti
titleSuffix: Configuration Manager
description: Ottimizzare la sicurezza e la privacy per la gestione dei contenuti in Configuration Manager
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704479"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Sicurezza e privacy per la gestione dei contenuti in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene informazioni sulla sicurezza e sulla privacy per la gestione dei contenuti in Configuration Manager. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Procedure di sicurezza consigliate per la gestione del contenuto  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Vantaggi e svantaggi di HTTPS o HTTP per i punti di distribuzione in Intranet
Per i punti di distribuzione in Intranet, considerare i vantaggi e gli svantaggi dell'uso di HTTPS e HTTP. Nella maggior parte degli scenari, l'utilizzo di HTTP e degli account di accesso al pacchetto per l'autorizzazione fornisce una maggiore protezione rispetto all'utilizzo di HTTPS con la crittografia senza autorizzazione. Se tuttavia sono presenti dati sensibili nel contenuto da crittografare durante il trasferimento, utilizzare HTTPS.  

-   **Quando si usa HTTPS per un punto di distribuzione**, Configuration Manager non usa gli account di accesso al pacchetto per autorizzare l'accesso al contenuto, ma il contenuto viene crittografato durante il trasferimento in rete.  

-   **Quando si usa HTTP per un punto di distribuzione**, è possibile usare gli account di accesso al pacchetto per l'autorizzazione, ma il contenuto non viene crittografato durante il trasferimento in rete.  

A partire dalla versione 1806, considerare la possibilità di abilitare **HTTP migliorato** per il sito. Questa funzionalità consente ai client di usare l'autenticazione di Azure Active Directory per comunicare in modo sicuro con un punto di distribuzione HTTP. Per altre informazioni, vedere [HTTP migliorato](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>Proteggere il file del certificato di autenticazione client
Se si utilizza un certificato di autenticazione client PKI al posto di un certificato autofirmato per il punto di distribuzione, proteggere il file del certificato (con estensione PFX) con una password complessa. Se si archivia il file in rete, proteggere il canale di rete durante l'importazione del file in Configuration Manager.

Impostando la richiesta di una password per importare il certificato di autenticazione client usato per la comunicazione tra il punto di distribuzione e i punti di gestione, il certificato viene protetto da utenti malintenzionati. Usare la firma Server Message Block (SMB) o IPsec tra il percorso di rete e il server del sito per impedire a utenti malintenzionati di manomettere il file di certificato.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Rimuovere il ruolo del punto di distribuzione dal server del sito
Per impostazione predefinita, Configuration Manager installa un punto di distribuzione nel server del sito. I client non devono comunicare direttamente con il server del sito. Per ridurre quindi la superficie di attacco, assegnare il ruolo del punto di distribuzione ad altri sistemi del sito e rimuoverlo dal server del sito.  

#### <a name="secure-content-at-the-package-access-level"></a>Proteggere il contenuto a livello di accesso al pacchetto
La condivisione del punto di distribuzione consente l'accesso in lettura a tutti gli utenti. Per limitare gli utenti che possono accedere al contenuto, utilizzare gli account di accesso al pacchetto durante la configurazione del punto di distribuzione per HTTP. Questa configurazione non viene applicata ai punti di distribuzione cloud, che non supportano gli account di accesso al pacchetti. Per altre informazioni, vedere [Account di accesso al pacchetto](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Configurare IIS nel ruolo del punto di distribuzione
Se Configuration Manager installa IIS durante l'aggiunta di un ruolo del sistema del sito del punto di distribuzione, rimuovere Reindirizzamento HTTP e Strumenti e script di gestione IIS quando l'installazione del punto di distribuzione è completata. Il punto di distribuzione non richiede Reindirizzamento HTTP e Strumenti e script di gestione IIS. Per ridurre la superficie di attacco, rimuovere questi servizi ruolo per il ruolo server Web.  Per altre informazioni sui servizi ruolo per il ruolo server Web per i punti di distribuzione, vedere [Prerequisiti del sito e del sistema del sito](../configs/site-and-site-system-prerequisites.md).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Impostare le autorizzazioni di accesso al pacchetto durante la creazione del pacchetto
Poiché le modifiche apportate agli account di accesso nei file del pacchetto diventano effettive solo quando il pacchetto viene ridistribuito, impostare con attenzione le autorizzazioni di accesso al pacchetto durante la creazione del pacchetto. Questa configurazione è importante quando il pacchetto è di grandi dimensioni o viene distribuito a molti punti di distribuzione, nonché quando la capacità della larghezza di banda di rete per la distribuzione del contenuto è limitata.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementare i controlli di accesso per proteggere i supporti che contengono il contenuto pre-installato
Il contenuto pre-installato viene compresso ma non crittografato. Un utente malintenzionato potrebbe leggere e modificare i file che vengono scaricati nei dispositivi. I client di Configuration Manager rifiutano i contenuti manomessi, ma li scaricano ugualmente.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importare i contenuti in versione di preproduzione con ExtractContent
I contenuti in versione di preproduzione possono essere importati solo usando lo strumento da riga di comando ExtractContent.exe. Per evitare la manomissione e l'elevazione dei privilegi, usare solo lo strumento da riga di comando autorizzato disponibile in Configuration Manager.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Proteggere il canale di comunicazione tra il server del sito e il percorso di origine del pacchetto
Usare la firma SMB o IPsec tra il server del sito e il percorso di origine del pacchetto quando si creano applicazioni e pacchetti. In questo modo è possibile impedire all'utente malintenzionato di manomettere i file di origine.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Rimuovere le directory virtuali predefinite per il sito Web personalizzato con il ruolo del punto di distribuzione
Se si modifica l'opzione di configurazione del sito per usare un sito Web personalizzato al posto del sito Web predefinito dopo l'installazione di un punto di distribuzione, rimuovere le directory virtuali predefinite. Quando si passa dal sito Web predefinito a un sito Web personalizzato, Configuration Manager non rimuove le vecchie directory virtuali. Rimuovere le directory virtuali seguenti che Configuration Manager aveva originariamente creato nel sito Web predefinito:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Per i punti di distribuzione cloud, proteggere i certificati e i dettagli della sottoscrizione di Azure
Quando si usano punti di distribuzione cloud, proteggere gli elementi importanti seguenti:
- Nome utente e password per la sottoscrizione di Azure
- Certificato di gestione di Azure 
- Certificato di servizio del punto di distribuzione cloud

Archiviare i certificati in modo protetto. Se vengono selezionati dalla rete durante la configurazione del punto di distribuzione cloud, usare la firma SMB o IPsec tra il server del sistema del sito e il percorso di origine.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Per la continuità del servizio, monitorare la data di scadenza dei certificati del punto di distribuzione cloud
Configuration Manager non avvisa l'utente quando i certificati importati per il punto di distribuzione cloud stanno per scadere. Monitorare le date di scadenza in modo indipendente da Configuration Manager e assicurarsi di rinnovare e quindi importare i nuovi certificati prima della data di scadenza. Si tratta di un'azione importante nel caso in cui un certificato di autenticazione server venga acquisito da un provider esterno pubblico, poiché i tempi di acquisizione del certificato rinnovato potrebbero essere più lunghi.  

 Se un certificato scade, Gestione servizi cloud genera l'ID messaggio di stato **9425**. Il file CloudMgr.log contiene una voce a indicare che il certificato **è scaduto**, con la data di scadenza registrata anche nel formato UTC.  



## <a name="security-considerations-for-content-management"></a>Considerazioni sulla sicurezza per la gestione del contenuto  

Durante la pianificazione della gestione dei contenuti, tenere presente i punti seguenti:  

-   I client convalidano i contenuti solo dopo che sono stati scaricati.  

     I client di Configuration Manager convalidano l'hash nel contenuto solo dopo che è stato scaricato nella cache del client. Se un utente malintenzionato manomette l'elenco dei file da scaricare o il contenuto stesso, il processo di download può richiedere una larghezza di banda di rete considerevole solo affinché il client scarti il contenuto quando incontra l'hash non valido.  

-   Quando si usano i punti di distribuzione cloud, l'accesso al contenuto viene automaticamente limitato all'azienda e non è possibile limitarlo ulteriormente a gruppi o utenti selezionati.  

-   Quando si usano i punti di distribuzione cloud, i client vengono autenticati dal punto di gestione e quindi usano un token di Configuration Manager per accedere ai punti di distribuzione cloud. Il token è valido per 8 ore. Di conseguenza, se si blocca un client perché non è più attendibile, il client può continuare a scaricare i contenuti da un punto di distribuzione cloud finché il periodo di validità del token non scade. Al termine di questo periodo, il punto di gestione non creerà un altro token per il client perché il client è bloccato.  

     Per impedire che un client bloccato scarichi i contenuti durante le 8 ore, arrestare il servizio cloud. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Punti di distribuzione del cloud**.  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Informazioni sulla privacy per la gestione dei contenuti  

 Configuration Manager non include dati utente nei file di contenuto, tuttavia un utente amministratore può scegliere di inserirli.  



## <a name="see-also"></a>Vedere anche

- [Concetti di base sulla gestione dei contenuti](fundamental-concepts-for-content-management.md)  

- [Sicurezza e privacy per la gestione delle applicazioni](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Sicurezza e privacy per gli aggiornamenti software](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Sicurezza e privacy per la distribuzione del sistema operativo](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
