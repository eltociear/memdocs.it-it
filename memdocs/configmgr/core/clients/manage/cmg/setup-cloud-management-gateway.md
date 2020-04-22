---
title: Configurare il Cloud Management Gateway
titleSuffix: Configuration Manager
description: Usare questa procedura dettagliata per configurare un Cloud Management Gateway (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: d087b3645de5e03936542e35c9261edd8609cd81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695289"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurare il gateway di gestione cloud per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo processo include i passaggi necessari per configurare un Cloud Management Gateway (CMG).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).


## <a name="before-you-begin"></a>Prima di iniziare

Iniziare leggendo l'articolo [Pianificare il gateway di gestione cloud](plan-cloud-management-gateway.md). Usare l'articolo per determinare la struttura del Cloud Management Gateway.

Usare l'elenco di controllo seguente per assicurarsi di avere le informazioni e i prerequisiti necessari per la creazione di un Cloud Management Gateway:  

- Ambiente Azure da usare. Ad esempio il cloud pubblico di Azure o il cloud di Azure Governo degli Stati Uniti.  

- A seconda della struttura pianificata saranno necessari uno o più certificati per Cloud Management Gateway. Per altre informazioni, vedere [Certificati per il gateway di gestione del cloud](certificates-for-cloud-management-gateway.md).  

- Per la distribuzione [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) del gateway di gestione cloud devono essere soddisfatti i requisiti seguenti:  

    - Integrazione con [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) per la **Gestione cloud**. L'individuazione utenti di Azure AD non è necessaria.  

    - I provider di risorse **Microsoft.ClassicCompute** & **Microsoft.Storage** devono essere registrati nella sottoscrizione di Azure. Per altre informazioni, vedere [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - Un amministratore della sottoscrizione deve effettuare l'accesso.  

- Un nome univoco globale per il servizio. Il nome deriva dal [certificato di autenticazione server del Cloud Management Gateway](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- Se si abilita Cloud Management Gateway come punto di distribuzione cloud, lo stesso nome univoco globale selezionato per il servizio Cloud Management Gateway deve essere disponibile anche come nome di account di archiviazione univoco globale. Il nome deriva dal [certificato di autenticazione server del Cloud Management Gateway](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- Area di Azure per questa distribuzione Cloud Management Gateway.  

- Numero di istanze di macchina virtuale necessarie per la scalabilità e la ridondanza.  

- Se occorre ancora usare la distribuzione classica del servizio di Azure in Configuration Manager versione 1810 o precedenti, sono necessari i requisiti seguenti:  

    > [!Important]  
    > A partire dalla versione 1810, le distribuzioni classiche del servizio in Azure sono deprecate in Configuration Manager. Usare le distribuzioni di Azure Resource Manager per il gateway di gestione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > A partire da Configuration Manager versione 1902, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze di Cloud Management Gateway.<!-- 3605704 -->

    - ID della sottoscrizione di Azure  

    - Certificato di gestione di Azure  


## <a name="set-up-a-cmg"></a>Impostare un Cloud Management Gateway

Eseguire questa procedura nel sito di livello superiore. Tale sito è un sito primario autonomo o il sito di amministrazione centrale.

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Cloud Management Gateway**.  

2. Selezionare **Crea un gateway di gestione cloud** sulla barra multifunzione.  

3. Nella pagina Generale della procedura guidata selezionare **Accedi**. Eseguire l'autenticazione con un account amministratore della sottoscrizione di Azure. La procedura guidata compila automaticamente i campi rimanenti in base alle informazioni archiviate durante il prerequisito di integrazione di Azure AD. Se si hanno più sottoscrizioni, selezionare l'**ID sottoscrizione** di quella che si vuole usare.

    > [!Note]  
    > A partire dalla versione 1810, le distribuzioni classiche del servizio in Azure sono state deprecate in Configuration Manager. Nella versione 1902 e nelle versioni precedenti selezionare **Distribuzione di Azure Resource Manager** come metodo di distribuzione del gateway di gestione cloud.
    >
    > Se è necessario usare una distribuzione classica del servizio, selezionare l'opzione in questa pagina. Immettere l'**ID sottoscrizione** di Azure. Quindi selezionare **Sfoglia** e scegliere il file PFX del certificato di gestione di Azure.

4. Specificare l'**ambiente di Azure** per il Cloud Management Gateway. Le opzioni nell'elenco a discesa possono variare a seconda del metodo di distribuzione.  

5. Selezionare **Avanti**. Attendere che il sito completi il test della connessione ad Azure.  

6. Nella pagina Impostazioni della procedura guidata, selezionare **Sfoglia** e scegliere il file PFX del certificato di autenticazione server per il Cloud Management Gateway. Il nome di questo certificato popola i campi obbligatori **FQDN servizio** e **Nome servizio**.  

   > [!NOTE]  
   > Il certificato di autenticazione server di Cloud Management Gateway supporta i caratteri jolly. Se si usa un certificato con caratteri jolly, sostituire l'asterisco (`*`) nel campo **FQDN servizio** con il nome desiderato per il Cloud Management Gateway.<!--491233-->  

7. Selezionare l'elenco a discesa **Area** per scegliere l'area di Azure per questo Cloud Management Gateway.  

8. Selezionare un'opzione **Gruppo di risorse**.
   1. Se si sceglie **Usa esistente** immettere il nome del nuovo gruppo di risorse o selezionare un gruppo di risorse esistente nell'elenco a discesa. Il gruppo di risorse selezionato deve essere già presente nell'area selezionata nel passaggio 7. Se si seleziona un gruppo di risorse esistente che si trova in un'area diversa da quella selezionata in precedenza, Cloud Management Gateway non riuscirà a effettuare il provisioning.
   2. Se si sceglie **Crea nuovo** immettere il nome del nuovo gruppo di risorse.

9. Nel campo **Istanza della macchina virtuale** immettere il numero di macchine virtuali per questo servizio. Il valore predefinito è uno, ma è possibile impostare fino a 16 macchine virtuali per Cloud Management Gateway.  

10. Selezionare **Certificati** per aggiungere i certificati radice trusted del client. Aggiungere tutti i certificati nella catena di certificati.  

    > [!Note]  
    > A partire dalla versione 1806, quando si crea un CMG non è più necessario specificare un certificato radice trusted nella pagina Impostazioni. Questo certificato non è obbligatorio se si usa Azure Active Directory (Azure AD) per l'autenticazione client, ma veniva richiesto nella procedura guidata. Se si usano certificati di autenticazione client PKI, è comunque necessario aggiungere un certificato radice trusted al CMG.<!--SCCMDocs-pr issue #2872-->  
    >
    > Nella versione 1902 e nelle versioni precedenti è possibile aggiungere solo due autorità di certificazione radice attendibili e quattro autorità intermedie (subordinate).<!-- SCCMDocs-pr#4022 -->

11. Per impostazione predefinita, la procedura guidata abilita l'opzione **Verifica la revoca del certificato client**. Per il funzionamento di questa verifica è necessario pubblicare in modalità pubblica un elenco di revoche di certificati (CRL). Per altre informazioni, vedere [Pubblicare l'elenco di revoche di certificati (CRL)](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. A partire dalla versione 1906, è possibile **applicare TLS 1.2**. Questa impostazione si applica solo alla macchina virtuale del servizio cloud di Azure. Non si applica ad alcun client o server del sito di Configuration Manager locale. Per altre informazioni su TLS 1.2, vedere [Come abilitare TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. A partire dalla versione 1806, per impostazione predefinita, la procedura guidata abilita l'opzione seguente: **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure**. Ora un CMG può anche trasferire il contenuto ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure.  

14. Selezionare **Avanti**.  

15. Per monitorare il traffico del Cloud Management Gateway con una soglia di 14 giorni, selezionare la casella di controllo per attivare l'avviso di soglia. Specificare quindi la soglia e le percentuali in corrispondenza delle quali verranno generati i diversi livelli di avviso. Al termine scegliere **Avanti**.  

16. Verificare le impostazioni e scegliere **Avanti**. Configuration Manager avvia la configurazione del servizio. Dopo l'esecuzione della procedura guidata saranno necessari da 5 a 15 minuti per completare il provisioning del servizio in Azure. Controllare la colonna **Stato** per la nuova istanza di Cloud Management Gateway per determinare quando il servizio è pronto.  

    > [!Note]  
    > Per la risoluzione dei problemi relativi alle distribuzioni di Cloud Management Gateway, usare **CloudMgr.log** e **CMGSetup.log**. Per altre informazioni, vedere [File di log](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurare il sito primario per l'autenticazione del certificato client

Se si usano i [certificati di autenticazione client](certificates-for-cloud-management-gateway.md#bkmk_clientauth) per l'autenticazione dei client con Cloud Management Gateway, seguire questa procedura per configurare ogni sito primario.  

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare il sito primario al quale sono assegnati i client basati su Internet e scegliere **Proprietà**.  

3. Passare alla scheda **Comunicazioni computer client** della finestra delle proprietà del sito primario e selezionare **Utilizza certificato client PKI (funzionalità di autenticazione client) quando disponibile**.  

    > [!Note]
    > A partire dalla versione 1906, questa scheda è denominata **Communication Security** (Sicurezza comunicazione).<!-- SCCMDocs#1645 -->  

4. Se non si pubblica un elenco di revoche di certificati (CRL, Certificate Revocation List) deselezionare l'opzione **Controllo client dell'elenco di revoche di certificati (CRL) per i sistemi del sito**.  


## <a name="add-the-cmg-connection-point"></a>Aggiungere il punto di connessione del Cloud Management Gateway

Il punto di connessione del Cloud Management Gateway è il ruolo di sistema del sito per la comunicazione con il Cloud Management Gateway. Per aggiungere il punto di connessione del Cloud Management Gateway, seguire le istruzioni generali per [installare i ruoli del sistema del sito](../../../servers/deploy/configure/install-site-system-roles.md). Nella pagina Selezione ruolo del sistema dell'Aggiunta guidata ruoli del sistema del sito selezionare **Punto di connessione del gateway di gestione cloud**. Quindi selezionare il **Nome del gateway di gestione cloud** al quale si connette il server. La procedura guidata visualizza l'area per il Cloud Management Gateway selezionato.

> [!Important]
> In determinati scenari il punto di connessione del Cloud Management Gateway deve avere un [certificato di autenticazione client](certificates-for-cloud-management-gateway.md#bkmk_clientauth).

Per la risoluzione dei problemi relativi all'integrità del Cloud Management Gateway, usare **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Per altre informazioni, vedere [File di log](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurare i ruoli lato client per il traffico del Cloud Management Gateway

Configurare il punto di gestione e il punto di aggiornamento software per accettare il traffico del Cloud Management Gateway. Eseguire questa procedura nel sito primario per tutti i punti di gestione e i punti di aggiornamento software che servono i client basati su Internet.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**. Nella scheda Home della barra multifunzione selezionare **Server con ruolo** nel gruppo Visualizzazione. Quindi selezionare **Punto di gestione** dall'elenco.  

2. Selezionare il server del sistema del sito da configurare per il traffico del Cloud Management Gateway. Selezionare il ruolo **Punto di gestione** nel riquadro dei dettagli e quindi **Proprietà** nella barra multifunzione.  

3. Nel pannello Proprietà punto di gestione, in Connessioni client selezionare la casella accanto a **Consenti il traffico del gateway di gestione cloud di Configuration Manager**.

    A seconda della progettazione del Cloud Management Gateway e della versione di Configuration Manager, potrebbe essere necessario abilitare l'opzione **HTTPS**. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Selezionare **OK** per chiudere la finestra delle proprietà del punto di gestione.  

Ripetere questi passaggi in base alle esigenze per i punti di gestione aggiuntivi e per gli eventuali punti di aggiornamento software.


## <a name="configure-boundary-groups"></a>Configurare gruppi di limiti

<!--3640932-->
A partire dalla versione 1902 è possibile associare un Cloud Management Gateway a un gruppo di limiti. Questa configurazione consente ai client di usare Cloud Management Gateway per impostazione predefinita o come fallback per le comunicazioni client in base alle relazioni del gruppo di limiti.

Per altre informazioni sui gruppi di limiti, vedere [Configurare gruppi di limiti](../../../servers/deploy/configure/boundary-groups.md).

Quando si [crea o configura un gruppo di limiti](../../../servers/deploy/configure/boundary-group-procedures.md), aggiungere un Cloud Management Gateway nella scheda **Riferimenti**. Questa azione consente di associare il Cloud Management Gateway a questo gruppo di limiti.


## <a name="configure-clients-for-cmg"></a>Configurare i client per il Cloud Management Gateway

Dopo che il Cloud Management Gateway e i ruoli del sistema del sito sono in esecuzione, i client recuperano automaticamente la posizione del servizio Cloud Management Gateway alla richiesta di posizione successiva. Per ricevere la posizione del servizio Cloud Management Gateway i client devono essere inclusi nell'intranet, salvo se si [installano e assegnano client Windows 10 usando Azure AD per l'autenticazione](../../deploy/deploy-clients-cmg-azure.md). Il ciclo di polling per le richieste di percorso è di 24 ore. Se non si vuole attendere la richiesta di percorso della normale pianificazione, è possibile forzare la richiesta riavviando il servizio host agenti di SMS (ccmexec.exe) nel computer.  

> [!Note]
> Per impostazione predefinita, tutti i client ricevono i criteri Cloud Management Gateway. È possibile controllare questo comportamento con l'impostazione client [Consenti ai client di usare un gateway di gestione cloud](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

Il client di Configuration Manager determina automaticamente se si trova sull'intranet o su Internet. Se il client riesce a contattare un controller di dominio o un punto di gestione locale, imposta il proprio tipo di connessione su **Ora intranet**. In caso contrario, passa all'impostazione **Ora Internet** e usa la posizione del servizio Cloud Management Gateway per comunicare con il sito.

>[!NOTE]
> È possibile forzare il client perché usi sempre il Cloud Management Gateway, sia che si trovi sull'intranet o su Internet. Questa configurazione è utile per l'esecuzione di test o per client ai quali si vuole imporre di usare sempre il servizio Cloud Management Gateway. Impostare la seguente chiave del Registro di sistema nel client:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> È anche possibile specificare questa impostazione durante l'installazione client usando la proprietà [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf).
>
> Questa impostazione viene applicata sempre, anche se il client si sposta in un percorso in cui le configurazioni del gruppo di limiti utilizzano risorse locali.


Per verificare che i client dispongano della proprietà che specifica il Cloud Management Gateway, aprire un prompt dei comandi di Windows PowerShell come amministratore nel computer client ed eseguire il comando seguente: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Questo comando visualizza tutti i punti di gestione basati su Internet rilevati dal client. Il Cloud Management Gateway non è tecnicamente un punto di gestione basato su Internet, ma i client lo rilevano come tale.

> [!Note]  
> Per la risoluzione dei problemi relativi al traffico client del Cloud Management Gateway, usare **CMGHttpHandler.log**, **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Per altre informazioni, vedere [File di log](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="modify-a-cmg"></a>Modificare un Cloud Management Gateway

Dopo la creazione di un Cloud Management Gateway è possibile modificarne alcune impostazioni. Selezionare il Cloud Management Gateway nella console di Configuration Manager e selezionare **Proprietà**. Configurare le impostazioni nelle schede seguenti:  

#### <a name="general"></a>Generale

- **Certificato di gestione di Azure**: modificare il certificato di gestione di Azure per il Cloud Management Gateway. Questa opzione è utile quando si aggiorna il certificato prima della scadenza.  

#### <a name="settings"></a>Impostazioni

- **File certificato**: cambiare il certificato di autenticazione server per il Cloud Management Gateway. Questa opzione è utile quando si aggiorna il certificato prima della scadenza.  

- **Istanza della macchina virtuale**: modificare il numero di macchine virtuali che il servizio usa in Azure. Questa impostazione consente di modificare dinamicamente le dimensioni del servizio in base a considerazioni sui costi o sull'uso.  

- **Certificati**: aggiungere o rimuovere certificati intermedi o certificati radice trusted dell'attività di certificazione (CA). Questa opzione è utile quando si aggiungono nuove autorità di certificazione o quando si ritirano i certificati scaduti.  

- **Verifica la revoca del certificato client**: se questa impostazione non viene abilitata al momento della creazione del Cloud Management Gateway, è possibile abilitarla in un secondo momento, dopo la pubblicazione dell'elenco CRL. Per altre informazioni, vedere [Pubblicare l'elenco di revoche di certificati (CRL)](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure**: a partire dalla versione 1806 questa nuova opzione è abilitata per impostazione predefinita. Ora un CMG può anche trasferire il contenuto ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure.<!--1358651-->  

#### <a name="alerts"></a>Avvisi

Riconfigurare gli avvisi in qualsiasi momento dopo la creazione del Cloud Management Gateway.


### <a name="redeploy-the-service"></a>Ridistribuire il servizio

Altre modifiche significative, ad esempio le configurazioni seguenti, richiedono la ridistribuzione del servizio:

- Metodo di distribuzione classico ad Azure Resource Manager
- Sottoscrizione
- Nome del servizio
- PKI da privato a pubblico
- Area

Mantenere sempre almeno un Cloud Management Gateway per consentire ai client basati su Internet di ricevere i criteri aggiornati. I client basati su Internet non possono comunicare con un Cloud Management Gateway rimosso. Inoltre i client non rilevano un nuovo servizio Cloud Management Gateway fino a quando non effettuano nuovamente il roaming all'intranet. Quando si crea una seconda istanza del Cloud Management Gateway per eliminare la prima, è necessario creare anche un altro punto di connessione del Cloud Management Gateway.

Per impostazione predefinita i client aggiornano i criteri ogni 24 ore. Pertanto, dopo aver creato un nuovo Cloud Management Gateway, attendere almeno un giorno prima di eliminare quello precedente. Se i client sono disattivati o non dispongono di una connessione a Internet il tempo di attesa può essere superiore.

Se è presente un gateway di gestione cloud esistente nel metodo di distribuzione classico, è necessario distribuire un nuovo gateway di gestione cloud per usare il metodo di distribuzione di Azure Resource Manager.<!--509753--> Sono disponibili due opzioni:  

- Per riusare lo stesso nome di servizio:  

    1. Eliminare la versione classica del Cloud Management Gateway, ricordando che è necessario avere almeno un Cloud Management Gateway sempre attivo per i client basati su Internet.  

    2. Creare un nuovo Cloud Management Gateway usando una distribuzione di Gestione risorse. Riusare lo stesso certificato di autenticazione server.  

    3. Riconfigurare il punto di connessione del Cloud Management Gateway in modo che usi la nuova istanza del Cloud Management Gateway.  

- Per usare un nuovo nome del servizio:  

    1. Creare un nuovo Cloud Management Gateway usando una distribuzione di Gestione risorse. Usare un nuovo certificato di autenticazione server.  

    2. Creare un nuovo punto di connessione del Cloud Management Gateway e collegarlo al nuovo Cloud Management Gateway.  

    3. Attendere almeno un giorno in modo che i client basati su Internet ricevano i criteri relativi al nuovo Cloud Management Gateway.  

    4. Eliminare il Cloud Management Gateway versione classica.  

> [!Tip]  
> Per determinare il modello di distribuzione corrente di un Cloud Management Gateway:<!--SCCMDocs issue #611-->  
>
> 1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Cloud Management Gateway**.  
> 2. Selezionare l'istanza di Cloud Management Gateway.  
> 3. Nel riquadro dei dettagli nella parte inferiore della finestra cercare l'attributo **Modello di distribuzione**. Per una distribuzione di Resource Manager, questo attributo è **Azure Resource Manager**. Il modello di distribuzione legacy con il certificato di gestione di Azure viene visualizzato come **Azure Service Manager**.
>
> È anche possibile aggiungere l'attributo **Modello di distribuzione** come colonna alla visualizzazione elenco.  

### <a name="modifications-in-the-azure-portal"></a>Modifiche nel portale di Azure

Modificare il Cloud Management Gateway solo dalla console di Configuration Manager. L'apporto di modifiche al servizio o alle macchine virtuali sottostanti direttamente in Azure non è supportato. Tali modifiche possono andare perdute senza preavviso. Come con qualsiasi PaaS, il servizio può ricompilare le macchine virtuali in qualsiasi momento. Le ricompilazioni possono verificarsi per la manutenzione dell'hardware back-end o per l'applicazione di aggiornamenti al sistema operativo delle macchine virtuali.

### <a name="delete-the-service"></a>Eliminare il servizio

Se è necessario eliminare il Cloud Management Gateway, eseguire questa operazione anche dalla console di Configuration Manager. La rimozione manuale di componenti in Azure crea incoerenze nel sistema. Questo stato produce dati orfani e può dare origine a comportamenti imprevisti.


## <a name="next-steps"></a>Passaggi successivi

- [Monitorare i client per il gateway di gestione cloud](monitor-clients-cloud-management-gateway.md)
- [Domande frequenti sul gateway di gestione cloud](cloud-management-gateway-faq.md)
