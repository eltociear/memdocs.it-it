---
title: Proprietà e parametri di installazione client
titleSuffix: Configuration Manager
description: Informazioni sui parametri e le proprietà della riga di comando ccmsetup per l'installazione del client di Configuration Manager.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1de2cd1645687740986cc62514dbc990461cbbf6
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240576"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Informazioni sui parametri e le proprietà di installazione del client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare il comando CCMSetup.exe per disinstallare il client di Configuration Manager. I *parametri* di installazione client specificati nella riga di comando consentono di modificare il comportamento dell'installazione, mentre le *proprietà* modificano la configurazione iniziale dell'agente client installato.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Informazioni su CCMSetup.exe

Il comando CCMSetup.exe consente di scaricare i file necessari per installare il client da un punto di gestione o da un percorso di origine. Questi file possono includere:  

- Il pacchetto client.msi di Windows Installer che consente di installare il software client

- Prerequisiti client

- Aggiornamenti e correzioni per il client di Configuration Manager

> [!NOTE]
> Non è possibile installare direttamente il file client.msi.  

CCMSetup.exe fornisce *parametri* della riga di comando per la personalizzazione dell'installazione. I parametri sono preceduti da una barra (`/`) e per convenzione sono in minuscolo. È possibile specificare il valore di un parametro quando necessario, usando due punti (`:`) seguiti dal valore. Per altre informazioni, vedere [Parametri della riga di comando di CCMSetup.exe](#ccmsetupexe-command-line-parameters).

È anche possibile specificare *proprietà* nella riga di comando di CCMSetup.exe per modificare il comportamento di client.msi. Le proprietà vengono specificate per convenzione in lettere maiuscole. Specificare un valore per una proprietà con un segno di uguale (`=`) seguito immediatamente dal valore. Per altre informazioni, vedere [Proprietà Client.msi](#clientMsiProps).

> [!IMPORTANT]  
> Specificare le proprietà di CCMSetup prima di specificare le proprietà per client.msi.  

CCMSetup.exe e i relativi file di supporto si trovano nel server del sito, nella cartella **Client** della cartella di installazione di Configuration Manager. Configuration Manager condivide la cartella in rete nella condivisione del sito. Ad esempio, `\\SiteServer\SMS_ABC\Client`

Al prompt dei comandi, il comando CCMSetup.exe usa il seguente formato:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Ad esempio:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Questo comando di esempio esegue le azioni seguenti:  

- Specifica il punto di gestione denominato SMSMP01 per richiedere un elenco di punti di distribuzione per il download dei file di installazione del client.  

- Specifica che è necessario interrompere l'installazione se nel computer esiste già una versione del client.  

- Indica a client.msi di assegnare il client al codice del sito S01.  

- Indica a client.msi di usare il punto di stato di fallback denominato SMSFP01.  

> [!TIP]  
> Se un valore di parametro include spazi, racchiuderlo tra virgolette.  

Se si estende lo schema di Active Directory per Configuration Manager, il sito pubblica molte proprietà di installazione client in Servizi di dominio Active Directory. Il client di Configuration Manager legge automaticamente queste proprietà. Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory](about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="ccmsetupexe-command-line-parameters"></a>Parametri della riga di comando di CCMSetup.exe

### <a name=""></a><a name="bkmk_help"></a> /?

Mostra i parametri della riga di comando disponibili per ccmsetup.exe.  

Esempio: `ccmsetup.exe /?`

### <a name="source"></a>/source

Specifica il percorso da cui scaricare i file. È possibile usare un percorso locale o UNC. Il dispositivo scarica i file usando il protocollo SMB (Server Message Block). Per usare **/source**, l'account utente Windows per l'installazione client deve avere le autorizzazioni **Lettura** per il percorso.

Per altre informazioni su come ccmsetup scarica il contenuto, vedere la [sezione relativa all'installazione client nell'articolo sui gruppi di limiti](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup), che include anche informazioni dettagliate sul comportamento di ccmsetup se si usano entrambi i parametri **/mp** e **/source**.

> [!TIP]  
> È possibile usare più volte il parametro **/source** in una riga di comando per specificare percorsi alternativi per il download.  

Esempio: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

Specifica un punto di gestione origine al quale possono connettersi i computer. I computer usano questo punto di gestione per trovare il punto di distribuzione più vicino per i file di installazione. Se non sono presenti punti di distribuzione o se i computer non riescono a scaricare i file dai punti di distribuzione dopo 4 ore, scaricano i file dal punto di gestione specificato.  

Per altre informazioni su come ccmsetup scarica il contenuto, vedere la [sezione relativa all'installazione client nell'articolo sui gruppi di limiti](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup), che include anche informazioni dettagliate sul comportamento di ccmsetup se si usano entrambi i parametri **/mp** e **/source**.

> [!IMPORTANT]  
> Questo parametro specifica un punto di gestione iniziale che consente ai computer di individuare un'origine per il download. Può trattarsi di un punto di gestione qualsiasi in un sito qualsiasi. Non implica l'*assegnazione* del client al punto di gestione specificato.

I computer scaricano i file tramite una connessione HTTP o HTTPS, a seconda della configurazione del ruolo del sistema del sito per le connessioni client. Il download può anche usare la limitazione BITS, se configurata. Se si configurano tutti i punti di distribuzione e di gestione solo per le connessioni client HTTPS, verificare che il computer client disponga di un certificato client valido.  

È possibile usare il parametro della riga di comando **/mp** per specificare più punti di gestione. Se il computer non riesce a connettersi al primo punto di gestione, prova a connettersi al successivo nell'elenco specificato. Quando si specificano più punti di gestione, è necessario separare i valori tramite punto e virgola.

Se il client si connette a un punto di gestione mediante HTTPS, specificare l'FQDN anziché il nome computer. Il valore deve corrispondere al **soggetto** o al **nome alternativo soggetto** del certificato PKI del punto di gestione. Nonostante Configuration Manager supporti l'uso di un nome computer nel certificato per le connessioni sulla rete Intranet, è consigliabile usare un FQDN.

Esempio con il nome del computer: `ccmsetup.exe /mp:SMSMP01`  

Esempio con il nome di dominio completo: `ccmsetup.exe /mp:smsmp01.contoso.com`  

Questo parametro può anche specificare l'URL di Cloud Management Gateway (CMG). Usare questo URL per installare il client in un dispositivo basato su Internet. Per ottenere il valore di questo parametro, seguire questa procedura:

- Creare un CMG. Per altre informazioni, vedere [Impostare un Cloud Management Gateway](../manage/cmg/setup-cloud-management-gateway.md).
- In un client attivo aprire un prompt dei comandi Windows PowerShell come amministratore.
- Eseguire il comando seguente:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- Aggiungere il prefisso `https://` da usare con il parametro **/mp**.

Esempio per l'uso dell'URL del gateway di gestione cloud: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Quando si specifica l'URL di un gateway di gestione cloud per il parametro **/mp**, l'URL deve iniziare con `https://`.

### <a name="regtoken"></a>/regtoken

<!--5686290-->

A partire dalla versione 2002, usare questo parametro per fornire un token di registrazione in blocco. Un dispositivo basato su Internet usa questo token nel processo di registrazione tramite un Cloud Management Gateway (CMG). Per altre informazioni, vedere [Autenticazione basata su token per CMG](deploy-clients-cmg-token.md).

Quando si usa questo parametro, includere anche i parametri e le proprietà seguenti:

- [ **/mp**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

La riga di comando di esempio seguente include le altre proprietà e i parametri di installazione necessari:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

Se CCMSetup.exe non riesce a scaricare i file di installazione, usare questo parametro per specificare l'intervallo tra i tentativi in minuti. CCMSetup continua a tentare fino a quando non raggiunge il limite specificato nel parametro [ **/downloadtimeout**](#downloadtimeout).

Esempio: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Questo parametro impedisce l'esecuzione di CCMSetup come servizio, ovvero l'impostazione predefinita. Quando CCMSetup funziona come servizio, viene eseguito nel contesto dell'account di sistema locale del computer. Questo account potrebbe non avere diritti sufficienti per l'accesso alle risorse di rete necessarie per l'installazione. Con **/noservice**, CCMSetup.exe viene eseguito nel contesto dell'account utente usato per avviare l'installazione.

Esempio: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Specifica che CCMSetup deve essere eseguito come un servizio che usa l'account di sistema locale.  

> [!TIP]
> Se si usa uno script per eseguire CCMSetup.exe con il parametro **/service**, CCMSetup.exe viene chiuso dopo l'avvio del servizio. Potrebbe non segnalare correttamente i dettagli di installazione allo script.

Esempio: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Usare questo parametro per disinstallare il client di Configuration Manager. Per altre informazioni, vedere [Disinstallare il client](../manage/manage-clients.md#BKMK_UninstalClient).

Esempio: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Specifica che l'installazione del client deve essere interrotta se è già installata una versione del client.  

Esempio: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Usare questo parametro per forzare il riavvio del computer, se necessario per completare l'installazione. Se questo parametro non viene specificato, quando è necessario un riavvio CCMSetup interrompe l'esecuzione. L'esecuzione viene ripresa dopo il successivo riavvio manuale.

Esempio: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

Quando il dispositivo scarica i file di installazione client tramite una connessione HTTP, usare questo parametro per specificare la priorità di download. Specificare uno dei valori possibili seguenti:

- `FOREGROUND`

- `HIGH`

- `NORMAL` (impostazione predefinita)

- `LOW`

Esempio: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

Se CCMSetup non è in grado di scaricare i file di installazione client, questo parametro specifica il timeout massimo in minuti. Dopo questo timeout, CCMSetup smette di provare a scaricare i file di installazione. Il valore predefinito è **1440** minuti (un giorno).

Usare il parametro [ **/retry**](#retry) per specificare l'intervallo tra i tentativi di ripetizione.

Esempio: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

Specificare questo parametro affinché il client usi un certificato di autenticazione client PKI. Se non si include questo parametro o se il client non trova un certificato valido, il client usa una connessione HTTP con un certificato autofirmato.

Esempio: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> In alcuni scenari non è necessario specificare questo parametro, ma si usa comunque un certificato client. Ad esempio, un'installazione del client basata su push del client e aggiornamento software. Usare questo parametro quando si installa manualmente un client e si usa il parametro **/mp** con un punto di gestione abilitato per HTTPS.
>
> Specificare questo parametro anche quando si installa un client per le comunicazioni solo con Internet. Usare la proprietà **CCMALWAYSINF=1** insieme alle proprietà per il punto di gestione basato su Internet (**CCMHOSTNAME**) e il codice del sito (**SMSSITECODE**). Per altre informazioni sulla gestione client in Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

### <a name="nocrlcheck"></a>/NoCRLCheck

Specifica che un client non deve verificare l'elenco di revoche di certificati (CRL) in caso di comunicazione tramite HTTPS con un certificato PKI. Quando non si specifica questo parametro, il client controlla il CRL prima di stabilire una connessione HTTPS. Per altre informazioni sul controllo dell'elenco di revoche di certificati (CRL) da parte del client, vedere [Pianificazione di revoche di certificati PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Esempio: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Questo parametro specifica un file di testo che elenca le proprietà di installazione client.

- Se CCMSetup viene eseguito come servizio, posizionare questo file nella cartella di sistema CCMSetup: `%Windir%\Ccmsetup`.

- Se si specifica il parametro [ **/noservice**](#noservice), posizionare questo file nella stessa cartella di CCMSetup.exe.

Esempio: `CCMSetup.exe /config:"configuration file name.txt"`

Per specificare il formato corretto del file, usare il file **mobileclienttemplate.tcf** nella cartella `\bin\<platform>` nella directory di installazione di Configuration Manager nel server del sito. Questo file contiene commenti sulle sezioni e su come usarle. Specificare le proprietà di installazione client nella sezione `[Client Install]` dopo il testo seguente: `Install=INSTALL=ALL`.

Esempio di voce della sezione `[Client Install]`: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

Questo parametro specifica che CCMSetup.exe non installa il prerequisito specificato. È possibile immettere più di un valore. Usare il punto e virgola (`;`) per separare i valori.

Esempi:

- `CCMSetup.exe /skipprereq:filename.exe`

- `CCMSetup.exe /skipprereq:filename1.exe;filename2.exe`

Per altre informazioni sui prerequisiti dei client, vedere [prerequisiti per i client Windows](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="forceinstall"></a>/forceinstall

Specifica che CCMSetup.exe disinstalla tutti i client esistenti e installa un nuovo client.  

### <a name="excludefeatures"></a>/ExcludeFeatures

Questo parametro specifica che CCMSetup.exe non installa la funzionalità specificata.

Esempio: `CCMSetup.exe /ExcludeFeatures:ClientUI` non installa Software Center nel client.  

> [!NOTE]  
> `ClientUI` è l'unico valore supportato dal parametro **/ExcludeFeatures**.

### <a name="alwaysexcludeupgrade"></a>/AlwaysExcludeUpgrade

Questo parametro specifica se un client verrà aggiornato automaticamente quando si abilita [**Aggiornamento client automatico**](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Valori supportati:

- `TRUE`: Il client non verrà aggiornato automaticamente
- `FALSE`: Il client viene aggiornato automaticamente (impostazione predefinita)

Ad esempio:  

`CCMSetup.exe /AlwaysExcludeUpgrade:TRUE`

Per altre informazioni, vedere [Client di interoperabilità estesa](../../understand/interoperability-client.md).

> [!NOTE]  
> Quando si usa il parametro **/AlwaysExcludeUpgrade**, l'aggiornamento automatico è comunque in esecuzione. Tuttavia, quando CCMSetup tenta di eseguire l'aggiornamento, verifica che è stato impostato il parametro **/AlwaysExcludeUpgrade** e registra la riga seguente in **ccmsetup.log**:
>
> `Client is stamped with /alwaysexcludeupgrade. Stop proceeding.`
>
> CCMSetup si chiude immediatamente e non viene eseguito alcun aggiornamento.

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Codici restituiti di CCMSetup.exe

Il comando CCMSetup.exe fornisce i seguenti codici restituiti. Per risolvere i problemi, esaminare il file `%WinDir%\ccmsetup\ccmsetup.log` nel client per informazioni di contesto e dettagliate sui codici restituiti.

|Codice restituito|Significato|  
|-----------|-------|  
|0|Operazione completata|  
|6|Errore|  
|7|Riavvio richiesto|  
|8|Installazione già in esecuzione|  
|9|Errore di valutazione dei prerequisiti|  
|10|Errore di convalida dell'hash manifesto di installazione|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a> Proprietà di Ccmsetup.msi

Le proprietà seguenti possono modificare il comportamento dell'installazione di ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Usare questa proprietà di ccmsetup.*msi* per passare ulteriori proprietà e parametri della riga di comando a ccmsetup.*exe*. Racchiudere altri parametri e proprietà tra virgolette (`"`). Usare questa proprietà quando si esegue il bootstrap del client di Configuration Manager tramite il [metodo di installazione della gestione dei dispositivi mobili ibrida di Intune](plan/client-installation-methods.md#microsoft-intune-mdm-installation).

Esempio: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune limita la riga di comando a 1024 caratteri.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a> Proprietà di Client.msi

Le proprietà seguenti possono modificare il comportamento dell'installazione di client.msi, installato da ccmsetup.exe. Se si usa il [metodo di installazione push del client](plan/client-installation-methods.md#client-push-installation), specificare queste proprietà nella scheda **Client** di **Proprietà installazione push client** nella console di Configuration Manager.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Specifica l'identificatore dell'app client Azure Active Directory (Azure AD). L'app client viene creata o importata quando si [configurano i servizi Azure](../../servers/deploy/configure/azure-services-wizard.md) per la gestione cloud. Gli amministratori di Azure possono ottenere il valore di questa proprietà dal portale di Azure. Per altre informazioni, vedere [Ottenere l'ID applicazione e la chiave di autenticazione](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Per la proprietà **AADCLIENTAPPID** l'ID applicazione è relativo al tipo di applicazione **Nativo**.

Esempio: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Specifica l'identificatore dell'app server Azure AD. L'app server viene creata o importata quando si [configurano i servizi Azure](../../servers/deploy/configure/azure-services-wizard.md) per la gestione cloud. Quando si crea l'app server, nella finestra Crea un'applicazione server questa proprietà è l'**URI ID App**.

Gli amministratori di Azure possono ottenere il valore di questa proprietà dal portale di Azure. In **Azure Active Directory** trovare l'app server in **Registrazioni app**. Cercare il tipo di applicazione **App Web/API**. Aprire l'app, selezionare **Impostazioni** e quindi selezionare **Proprietà**. Usare il valore **URI ID App** per questa proprietà dell'installazione client **AADRESOURCEURI**.

Esempio: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Specifica l'identificatore de tenant di Azure AD. Configuration Manager si collega questo tenant quando si [configurano i servizi Azure](../../servers/deploy/configure/azure-services-wizard.md) per la gestione cloud. Per ottenere il valore di questa proprietà procedere come segue:

- In un dispositivo Windows 10 unito allo stesso tenant di Azure AD aprire un prompt dei comandi.
- Eseguire il comando seguente: `dsregcmd.exe /status`
- Nella sezione Stato dispositivo trovare il valore **TenantId**. Ad esempio: `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Gli amministratori di Azure possono anche ottenere questo valore nel portale di Azure. Per altre informazioni, vedere [Ottenere l'ID tenant](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Esempio: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Specifica uno o più gruppi o account utente di Windows per ottenere l'accesso ai criteri e le impostazioni del client. Questa proprietà è utile quando non si hanno credenziali amministrative locali nel computer client. Specificare un elenco di account separati da un punto e virgola (`;`).

Esempio: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Se necessario, consentire il riavvio automatico del computer dopo l'installazione del client.

> [!IMPORTANT]  
> Quando si usa questa proprietà, il computer viene riavviato senza avvisi. Questo comportamento si verifica anche se un utente ha eseguito l'accesso a Windows.

Esempio: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Per specificare che il client è sempre basato su Internet e non si connette mai all'Intranet, impostare il valore di questa proprietà su `1`. Il tipo di connessione del client visualizza **Sempre Internet**.  

Usare questa proprietà con [**CCMHOSTNAME**](#ccmhostname) per specificare il nome di dominio completo del punto di gestione basato su Internet. Usarla anche con il parametro di CCMSetup [ **/UsePKICert**](#usepkicert) e con il codice del sito ([**SMSSITECODE**](#smssitecode)).

Per altre informazioni sulla gestione client in Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).

Esempio: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Usare questa proprietà per specificare l'elenco di autorità di certificazione. Questo elenco include informazioni sui certificati per le autorità di certificazione radice attendibili (CA) considerate attendibili dal sito di Configuration Manager.  

Il valore è una corrispondenza con distinzione maiuscole/minuscole per gli attributi del soggetto presenti nel certificato CA radice. Separare gli attributi con una virgola (`,`) o un punto e virgola (`;`). Per specificare più certificati CA radice, usare una barra di separazione (`|`).

Esempio: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Usare il valore dell'attributo **CertificateIssuers** nel file **mobileclient.tcf** per il sito. Questo file è disponibile nella cartella `\bin\<platform>` della directory di installazione di Configuration Manager nel server del sito.

Per altre informazioni sull'elenco delle autorità di certificazione e sulle relative modalità d'uso da parte dei client durante il processo di selezione dei certificati, vedere [Pianificazione della selezione del certificato client PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

Se il client ha più di un certificato per la comunicazione HTTPS, questa proprietà specifica i criteri per la selezione di un certificato di autenticazione client valido.

Usare le parole chiave seguenti per cercare il nome del soggetto o il nome alternativo del soggetto del certificato:

- **Oggetto**: trovare una corrispondenza esatta
- **SubjectStr**: trovare una corrispondenza parziale

Esempi:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: cercare un certificato con una corrispondenza esatta al nome computer `computer1.contoso.com` in Nome soggetto o in Nome alternativo soggetto.

- `CCMCERTSEL="SubjectStr:contoso.com"`: cercare un certificato che contiene `contoso.com` in Nome soggetto o in Nome alternativo soggetto.

Usare la parola chiave **SubjectAttr** per cercare l'identificatore di oggetto (OID) o gli attributi del nome distinto negli attributi Nome oggetto o Nome alternativo oggetto.

Esempi:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: cercare l'attributo dell'unità organizzativa espresso come un identificatore di oggetto e denominato `Computers`.

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: cercare l'attributo dell'unità organizzativa espresso come un nome distinto e denominato `Computers`.

> [!IMPORTANT]
> Se si usa la casella Nome soggetto, la parola chiave **Subject** distingue tra maiuscole e minuscole, mentre la parola chiave **SubjectStr** non esegue la distinzione.
>
> Se si usa la casella Nome alternativo soggetto, entrambe le parole chiave **Subject** e **SubjectStr** non distinguono tra maiuscole e minuscole.

Per l'elenco completo degli attributi che è possibile usare per la selezione dei certificati, vedere [Valori attributi supportati per i criteri di selezione del certificato PKI](#BKMK_attributevalues).

Se più di un certificato corrisponde alla ricerca e si imposta [**CCMFIRSTCERT**](#ccmfirstcert) su `1`, il programma di installazione del client seleziona il certificato con il periodo di validità più lungo.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Se il programma di installazione del client non è in grado di individuare un certificato valido nell'archivio certificati predefinito **Personale** per il computer, usare questa proprietà per specificare un nome alternativo per l'archivio certificati.

Esempio: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Questa proprietà abilita la registrazione di debug quando viene installato il client. Questa proprietà fa in modo che il client registri le informazioni di basso livello per la risoluzione dei problemi. Evitare di usare questa proprietà nei siti di produzione. La proprietà può dare origine a un volume eccessivo di registrazioni e quindi rendere difficile l'individuazione delle informazioni desiderate nei file di log. Abilitare anche [**CCMENABLELOGGING**](#ccmenablelogging).

Valori supportati:

- `0`: disattiva la registrazione di debug (impostazione predefinita)
- `1`: attiva la registrazione di debug

Esempio: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Per altre informazioni, vedere [Informazioni sui file di log](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager abilita la registrazione per impostazione predefinita.

Valori supportati:

- `TRUE`: attiva la registrazione (impostazione predefinita)
- `FALSE`: disattiva la registrazione

Esempio: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Per altre informazioni, vedere [Informazioni sui file di log](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

Frequenza in minuti con cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe). Specificare un valore intero compreso tra `1` e `1440`. Per impostazione predefinita, ccmeval viene eseguito una volta al giorno (1440 minuti).

Esempio: `CCMSetup.exe CCMEVALINTERVAL=1440`

Per altre informazioni sulla valutazione dell'integrità dei client, vedere [Monitorare i client](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmevalhour"></a>CCMEVALHOUR

Ora del giorno in cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe). Specificare un valore intero compreso tra `0` (mezzanotte) e `23` (23:00). Per impostazione predefinita, ccmeval viene eseguito a mezzanotte.

Per altre informazioni sulla valutazione dell'integrità dei client, vedere [Monitorare i client](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Se si imposta questa proprietà su `1`, il client seleziona il certificato PKI con il periodo di validità più lungo.

Esempio: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Se il client viene gestito in Internet, specifica l'FQDN del punto di gestione basato su Internet.  

Non specificare questa opzione con la proprietà di installazione **SMSSITECODE=AUTO**. Assegnare direttamente i client basati su Internet a un sito basato su Internet.

Esempio: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Questa proprietà può specificare l'indirizzo di un Cloud Management Gateway (CMG). Per ottenere il valore di questa proprietà procedere come segue:

- Creare un CMG. Per altre informazioni, vedere [Impostare un Cloud Management Gateway](../manage/cmg/setup-cloud-management-gateway.md).
- In un client attivo aprire un prompt dei comandi Windows PowerShell come amministratore.
- Eseguire il comando seguente:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Con la proprietà **CCMHOSTNAME** usare il valore restituito senza modificarlo.

ad esempio `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Quando si specifica l'indirizzo di un CMG per la proprietà **CCMHOSTNAME**, non aggiungere un prefisso, ad esempio `https://`. Usare questo prefisso solo con l'URL **/mp** di un CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Specifica la porta che il client deve usare per la comunicazione tramite HTTP con i server del sistema del sito. Per impostazione predefinita, questo valore è `80`.

Esempio: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Specifica la porta che il client deve usare per la comunicazione tramite HTTPS con i server del sistema del sito. Per impostazione predefinita, questo valore è `443`.

Esempio: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Usare questa proprietà per impostare la cartella in cui installare i file del client di Configuration Manager. Per impostazione predefinita, usa `%WinDir%\CCM`.

> [!TIP]
> Indipendentemente dalla posizione in cui vengono installati i file client, il file **ccmcore.dll** viene sempre installato nella cartella `%WinDir%\System32`. In un sistema operativo a 64 bit viene installata una copia di ccmcore.dll nella cartella `%WinDir%\SysWOW64`. Questo file supporta le applicazioni a 32 bit che usano la versione a 32 bit delle API client di Configuration Manager SDK.

Esempio: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Usare questa proprietà per specificare il livello di dettagli da scrivere nei file di log di Configuration Manager.

Valori supportati:

- `0`: Dettagliato
- `1`: Predefinito
- `2`: Avvisi ed errori
- `3`: Solo errori

Esempio: `CCMSetup.exe CCMLOGLEVEL=0`

Per altre informazioni, vedere [Informazioni sui file di log](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando un file di log di Configuration Manager raggiunge la dimensione massima, il client lo rinomina come file di backup e crea un nuovo file di log. Questa proprietà specifica il numero di versioni precedenti del file di log da mantenere. Il valore predefinito è `1`. Se si imposta il valore su `0`, il client non mantiene la cronologia dei file di log.

Esempio: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Per altre informazioni, vedere [Informazioni sui file di log](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Questa proprietà specifica la dimensione massima del file di log in byte. Quando un log raggiunge la dimensione specificata, il client lo rinomina come file di cronologia e ne crea uno nuovo. Le dimensioni predefinite sono pari a 250.000 byte e la dimensione minima è 10.000 byte.

Esempio: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300.000 byte)

### <a name="disablesiteopt"></a>DISABLESITEOPT

Impostare questa proprietà su `TRUE` per impedire agli amministratori di modificare il sito assegnato nel pannello di controllo di Configuration Manager.

Esempio: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se impostata su TRUE, questa proprietà non consente agli utenti amministratori di modificare le impostazioni della cartella cache client nel pannello di controllo **Configuration Manager**.  

Esempio: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Specifica un dominio DNS usato dai client per individuare i punti di gestione pubblicati in DNS. Quando il client individua un punto di gestione, tale punto fornisce informazioni al client in merito ad altri punti di gestione nella gerarchia. Questo comportamento indica che il punto di gestione che il client rileva dal DNS può essere uno qualsiasi nella gerarchia.

> [!NOTE]
> Non è necessario specificare questa proprietà se il client si trova nello stesso dominio del punto di gestione pubblicato. In questo caso il dominio del client viene usato automaticamente per la ricerca dei punti di gestione nel DNS.

Per altre informazioni sulla pubblicazione DNS come metodo di posizione del servizio per i client Configuration Manager, vedere [Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).

> [!NOTE]  
> Per impostazione predefinita, Configuration Manager non abilita la pubblicazione DNS.

Esempio: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Specificare il punto di stato di fallback che riceve ed elabora i messaggi di stato inviati dai client di Configuration Manager.

Per altre informazioni, vedere [Stabilire se è necessario un punto di stato di fallback](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).

Esempio: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Se si imposta questa proprietà su `TRUE`, il programma di installazione del client non controlla la versione minima richiesta di Microsoft Application Virtualization (App-V).

> [!IMPORTANT]  
> Se si installa il client di Configuration Manager senza installare App-V non è possibile [distribuire applicazioni virtuali](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Esempio: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Quando si abilita questa proprietà, che il client segnala lo stato, ma non risolve i problemi rilevati.

Esempio: `CCMSetup.exe NOTIFYONLY=TRUE`

Per altre informazioni, vedere [Come configurare lo stato del client](configure-client-status.md).

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

A partire dalla versione 2002, usare questa proprietà per avviare una sequenza di attività in un client dopo la corretta registrazione nel sito.

> [!NOTE]
> Se la sequenza di attività installa aggiornamenti software o applicazioni, i client devono disporre di un certificato di autenticazione client valido. L'autenticazione del token da sola non funziona. Per altre informazioni, vedere [Note sulla versione - Distribuzione del sistema operativo](../../servers/deploy/install/release-notes.md#os-deployment).<!--7527072-->
      
Ad esempio, è possibile effettuare il provisioning di un nuovo dispositivo Windows 10 con Windows Autopilot, registrarlo automaticamente in Microsoft Intune e quindi installare il client di Configuration Manager per la co-gestione. Se si specifica questa nuova opzione, il client appena sottoposto a provisioning esegue una sequenza di attività. Questo processo offre una maggiore flessibilità per l'installazione di applicazioni e aggiornamenti software o per la configurazione delle impostazioni.


Usare il processo seguente:

1. [Creare una sequenza di attività di distribuzione non del sistema operativo](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) per installare le app, installare gli aggiornamenti software e configurare le impostazioni.

1. [Distribuire questa sequenza di attività](../../../osd/deploy-use/deploy-a-task-sequence.md) nella nuova raccolta predefinita **Tutti i dispositivi con provisioning**. Prendere nota dell'ID di distribuzione della sequenza di attività, ad esempio `PRI20001`.

1. [Installare il client di Configuration Manager](deploy-clients-to-windows-computers.md#BKMK_Manual) in un dispositivo e includere la proprietà seguente: `PROVISIONTS=PRI20001`. Impostare il valore di questa proprietà come ID di distribuzione della sequenza di attività.

    - Se si installa il client da Intune durante la registrazione di co-gestione, vedere [Come preparare i dispositivi basati su Internet per la co-gestione](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Questo metodo può avere prerequisiti aggiuntivi. Ad esempio, la registrazione del sito in Azure Active Directory o la creazione di un gateway di gestione cloud abilitato per il contenuto.

Dopo l'installazione e la registrazione corretta del client nel sito, viene avviata la sequenza di attività a cui si fa riferimento. Se la registrazione del client non riesce, la sequenza di attività non viene avviata.



### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Se un client ha la chiave radice attendibile di Configuration Manager non corretta, non può contattare un punto di gestione attendibile per ricevere la nuova chiave radice attendibile. Usare questa proprietà per rimuovere la chiave radice attendibile precedente. Questa situazione può verificarsi quando si sposta un client da una gerarchia del sito a un'altra. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Esempio: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Consente la riassegnazione automatica del sito per gli aggiornamenti client se usata con [SMSSITECODE=AUTO](#smssitecode).

Esempio: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Specifica il percorso della cartella cache client nel computer client. Per impostazione predefinita, il percorso della cache è `%WinDir%\ccmcache`.

Esempio: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Usare questa proprietà con la proprietà [**SMSCACHEFLAGS**](#smscacheflags) per controllare il percorso della cartella cache client. Ad esempio, per installare la cartella cache client nell'unità disco del client più grande disponibile: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Usare questa proprietà per specificare ulteriori dettagli sull'installazione per la cartella cache client. È possibile usare le proprietà **SMSCACHEFLAGS** singolarmente o combinate, separate da punti e virgola (`;`).

Se non si include questa proprietà:

- Il client installa la cartella della cache in base alla proprietà [**SMSCACHEDIR**](#smscachedir)
- La cartella non è compressa
- Il client usa la proprietà [**SMSCACHESIZE**](#smscachesize) come limite delle dimensioni in MB della cache

Quando si aggiorna un client esistente, il programma di installazione del client ignora questa proprietà.

#### <a name="values-for-the-smscacheflags-property"></a>Valori per la proprietà SMSCACHEFLAGS

- **PERCENTDISKSPACE**: impostare le dimensioni della cache come percentuale dello spazio su disco *totale*. Se si specifica questa proprietà, impostare anche [**SMSCACHESIZE**](#smscachesize) su un valore percentuale.

- **PERCENTFREEDISKSPACE**: impostare le dimensioni della cache come percentuale dello spazio *libero* su disco. Se si specifica questa proprietà, impostare anche [**SMSCACHESIZE**](#smscachesize) come valore percentuale. Ad esempio, il disco dispone di 10 MB di spazio libero e si specifica `SMSCACHESIZE=50`. Il programma di installazione del client imposta le dimensioni della cache su 5 MB. Non è possibile usare questa proprietà con la proprietà **PERCENTDISKSPACE**.

- **MAXDRIVE**: consente di installare la cache nel disco più grande disponibile. Se si specifica un percorso con la proprietà [**SMSCACHEDIR**](#smscachedir), il programma di installazione del client ignora questo valore.

- **MAXDRIVESPACE**: consente di installare la cache nell'unità disco con maggiore spazio libero. Se si specifica un percorso con la proprietà [**SMSCACHEDIR**](#smscachedir), il programma di installazione del client ignora questo valore.

- **NTFSONLY**: consente di installare la cache solo in un'unità disco in formato NTFS. Se si specifica un percorso con la proprietà [**SMSCACHEDIR**](#smscachedir), il programma di installazione del client ignora questo valore.

- **COMPRESS**: consente di archiviare la cache in un formato compresso.

- **FAILIFNOSPACE**: se non è disponibile spazio sufficiente per installare la cache, rimuovere il client di Configuration Manager.

Esempio: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Sono disponibili impostazioni client per specificare le dimensioni della cartella cache del client. Queste nuove impostazioni client sostituiscono in modo efficace l'uso di SMSCACHESIZE come proprietà di client.msi per specificare le dimensioni della cache del client. Per altre informazioni, vedere [le impostazioni client per le dimensioni della cache](about-client-settings.md#client-cache-settings).  

Quando si aggiorna un client esistente, il programma di installazione del client ignora questa impostazione. Il client ignora anche le dimensioni della cache durante il download degli aggiornamenti software.

Esempio: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Se si reinstalla un client, non è possibile usare **SMSCACHESIZE** o **SMSCACHEFLAGS** per ridurre la cache a una dimensione inferiore a quella precedente. Le dimensioni precedenti corrispondono al valore minimo.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Usare questa proprietà per specificare la posizione e l'ordine in cui il programma di installazione del client verifica le impostazioni di configurazione. Si tratta di una stringa composta da uno o più caratteri, ognuno dei quali definisce un'origine di configurazione specifica:

- `R`: verifica le impostazioni di configurazione nel Registro di sistema.

  Per altre informazioni, vedere [Effettuare il provisioning delle proprietà di installazione client](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: verifica le impostazioni di configurazione nelle proprietà di installazione dalla riga di comando.

- `M`: verifica le impostazioni esistenti quando si aggiorna un client precedente.

- `U`: aggiorna il client installato a una versione più recente e usa il codice del sito assegnato.

Per impostazione predefinita, il programma di installazione del client usa `PU`. Verifica prima di tutto le proprietà di installazione (`P`) e quindi le impostazioni esistenti (`U`).  

Esempio: `CCMSetup.exe SMSCONFIGSOURCE=RP`

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

Specifica se il client può usare Windows Internet Name Service (WINS) per trovare un punto di gestione che accetti le connessioni HTTP. I client usano questo metodo quando non riescono a trovare un punto di gestione in Servizi di dominio Active Directory o in DNS.

Questa proprietà non influisce sull'uso di WINS da parte del client per la risoluzione dei nomi.

È possibile configurare due diverse modalità per questa proprietà:

- **NOWINS**: questo valore è l'impostazione più sicura per questa proprietà. Impedisce ai client di trovare un punto di gestione in WINS. Quando si usa questa impostazione, i client devono usare un metodo alternativo per individuare un punto di gestione nella rete Intranet, ad esempio la pubblicazione in Active Directory Domain Services o DNS.

- **WINSSECURE** (predefinita): in questa modalità, un client che usa la comunicazione HTTP può usare WINS per trovare un punto di gestione. Tuttavia, il client deve disporre di una copia della chiave radice attendibile prima di potersi connettere al punto di gestione. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Esempio: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Specifica un punto di gestione iniziale usato dal client di Configuration Manager.  

> [!IMPORTANT]  
> Se il punto di gestione accetta solo connessioni client su HTTPS, aggiungere al nome del punto di gestione il prefisso `https://`.

Esempi:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Se il client non è in grado di ottenere la chiave radice attendibile di Configuration Manager da Active Directory Domain Services, usare questa proprietà per specificare la chiave. Questa proprietà viene applicata ai client che usano la comunicazione HTTP e HTTPS. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Esempio: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Ottenere il valore per la chiave radice attendibile del sito dal file mobileclient.tcf nel server del sito. Per altre informazioni, vedere [Eseguire il pre-provisioning di un client con la chiave radice attendibile tramite file](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Usare questa proprietà per reinstallare la chiave radice attendibile di Configuration Manager. Specifica il percorso completo e il nome di un file che contiene la chiave radice attendibile. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Esempio: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Specifica il percorso completo e il nome del certificato autofirmato esportato nel server del sito. Il server del sito archivia il certificato nell'archivio certificati **SMS**. Il Nome soggetto è **Server del sito** e il nome descrittivo è **Certificato di firma del server del sito**.

Esempio: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Questa proprietà specifica un sito di Configuration Manager a cui assegnare il client. Il valore può essere un codice del sito con tre caratteri o la parola `AUTO`. Se si specifica `AUTO` o se questa proprietà non viene specificata, il client prova a determinare l'assegnazione del sito da Active Directory Domain Services o da un punto di gestione specificato. Per abilitare `AUTO` per gli aggiornamenti client, impostare anche [SITEREASSIGN = TRUE](#sitereassign).

> [!NOTE]  
> Se si specifica anche un punto di gestione basato su Internet con la proprietà [**CCMHOSTNAME**](#ccmhostname), non usare `AUTO` con **SMSSITECODE**. Assegnare direttamente il client al relativo sito specificando il codice del sito.

Esempio: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Valori di attributo per i criteri di selezione del certificato

Configuration Manager supporta i valori seguenti di attributi per i criteri di selezione del certificato PKI:

|Attributo OID|Attributo del nome distinto|Definizione di attributo|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Componente del dominio|  
|1.2.840.113549.1.9.1|E o E-mail|Indirizzo di posta elettronica|  
|2.5.4.3|CN|Nome comune|  
|2.5.4.4|SN|Nome oggetto|  
|2.5.4.5|SERIALNUMBER|Numero di serie|  
|2.5.4.6|C|Codice paese|  
|2.5.4.7|L|Località|  
|2.5.4.8|S o ST|Nome di provincia o stato|  
|2.5.4.9|STREET|Indirizzo|  
|2.5.4.10|O|Nome organizzazione|  
|2.5.4.11|OU|Unità organizzativa|  
|2.5.4.12|T o Title|Titolo|  
|2.5.4.42|G o GN o GivenName|Nome specificato|  
|2.5.4.43|I o Initials|Iniziali|  
|2.5.29.17|(nessun valore)|Nome alternativo soggetto|  
