---
title: Note sulla versione
titleSuffix: Configuration Manager
description: Informazioni su problemi urgenti non ancora risolti nel prodotto o trattati in un articolo della Knowledge Base del supporto tecnico Microsoft.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a29c165e13e82144d7fea767ca719a0c84c88023
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512649"
---
# <a name="release-notes-for-configuration-manager"></a>Note sulla versione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager le note sulla versione del prodotto sono limitate ai problemi urgenti. Questi problemi non sono ancora stati risolti nel prodotto né trattati in dettaglio in un articolo della Knowledge Base del supporto tecnico Microsoft.  

La documentazione specifica delle funzionalità include informazioni sui problemi noti che interessano gli scenari di base.  

Questo articolo include note sulla versione per l'edizione Current Branch di Configuration Manager. Per informazioni sul Technical Preview Branch, vedere [Technical Preview](../../../get-started/technical-preview.md)  

Per informazioni sulle nuove funzionalità introdotte con le diverse versioni, vedere gli articoli seguenti:

- [Novità della versione 2006](../../../plan-design/changes/whats-new-in-version-2006.md)
- [Novità della versione 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Novità della versione 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Novità della versione 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  

Per informazioni sulle nuove funzionalità di Desktop Analytics, vedere [Novità di Desktop Analytics](../../../../desktop-analytics/whats-new.md).

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Configurazione e aggiornamento  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>L'aggiornamento automatico del client avviene immediatamente per tutti i client

<!-- 6040412 -->

*Si applica alla versione 1910*

Se il sito usa l'[aggiornamento automatico del client](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade), quando si aggiorna il sito alla versione 1910, tutti i client vengono immediatamente aggiornati dopo che il sito è stato aggiornato correttamente. L'unica impostazione casuale è quando i client ricevono i criteri, cosa che per impostazione predefinita avviene ogni ora. Per un sito di grandi dimensioni con molti client, questo comportamento può comportare l'utilizzo di una quantità significativa di traffico di rete e un sovraccarico dei punti di distribuzione.

Per altre informazioni sulle versioni interessate, vedere [Aggiornamento client per Configuration Manager Current Branch, versione 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Il server del sito in modalità passiva non aggiorna configuration.mof

<!-- 5787848 -->

*Si applica alla versione 1910*

Se il sito include un [server del sito in modalità passiva](../configure/site-server-high-availability.md), quando si aggiorna il sito è possibile che le personalizzazioni dell'inventario vadano perse. Quando si esegue il failover dei server del sito, il sito non sincronizza il file configuration.mof.

Per risolvere questo problema, eseguire manualmente il backup e il ripristino del file configuration.mof del sito.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Avviso di prerequisito di installazione relativo al livello di funzionalità del dominio nell'edizione Server 2019

<!-- 4904376 -->

*Si applica alla versione 1906*

Quando si installa l'aggiornamento per la versione 1906 in un ambiente con controller di dominio che eseguono Windows Server 2019, il controllo dei prerequisiti per il livello di funzionalità del dominio restituisce l'avviso seguente:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Per risolvere il problema, ignorare l'avviso.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>L'individuazione utenti e la sincronizzazione delle raccolte con i gruppi di Azure AD non funzionano dopo l'espansione del sito

<!-- 4797313 -->
*Si applica alla versione 1906*

Dopo aver configurato una delle funzionalità seguenti:

- Individuazione dei gruppi utenti in Azure Active Directory
- Sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory

se si espande un sito primario autonomo a una gerarchia con un sito di amministrazione centrale, verrà visualizzato l'errore seguente in SMS_AZUREAD_DISCOVERY_AGENT. log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Per risolvere il problema, rinnovare la chiave associata alla registrazione dell'app in Azure AD. Per altre informazioni, vedere [Rinnovare la chiave privata](../configure/azure-services-wizard.md#bkmk_renew).

## <a name="role-based-administration"></a>Amministrazione basata su ruoli

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Gli ambiti di protezione per alcune cartelle non vengono replicati dal sito di amministrazione centrale ai siti primari
<!--6306759-->
*Si applica alla versione 1910*

Dopo l'aggiornamento alla versione 1910, gli [ambiti di protezione per le cartelle](../configure/configure-role-based-administration.md#bkmk_config-folder) nelle raccolte utenti e nelle raccolte dispositivi non vengono replicati dal sito di amministrazione centrale ai siti primari.

## <a name="application-management"></a>Gestione delle applicazioni

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Errore "Non è possibile ottenere il certificato per PowerShell" durante la distribuzione di Microsoft Edge versione 77 e successive
<!--5769384-->
*Si applica a: Configuration Manager versione 1910*

Se si esegue la console di Configuration Manager in un sistema operativo in lingua svedese, ungherese o giapponese, durante la distribuzione di Microsoft Edge, versione 77 e successive, verrà restituito l'errore seguente:

`Unable to get certificate for Powershell`

Questo errore si verifica perché non esiste una cartella `scripts` nella directory `AdminConsole\bin` per la lingua svedese, ungherese o giapponese. In queste lingue del sistema operativo la cartella scripts è localizzata.

Per risolvere il problema, creare una cartella denominata `scripts` nella directory `AdminConsole\bin`. Copiare i file dalla cartella localizzata nella nuova cartella `scripts` creata. Distribuire Microsoft Edge, versione 77 e successive, dopo aver copiato i file.

## <a name="os-deployment"></a>Distribuzione del sistema operativo

### <a name="client-policy-error-when-you-deploy-a-task-sequence"></a>Errore dei criteri client quando si distribuisce una sequenza di attività

<!-- 7970134 -->

*Si applica a: Configuration Manager versione 2006, anello di aggiornamento anticipato*

Quando si distribuisce una sequenza di attività a un client, una sequenza di attività obbligatoria non viene installata entro la scadenza e in Software Center non viene visualizzata una sequenza di attività disponibile. Viene visualizzato il messaggio di stato 10803 con una descrizione analoga al messaggio di errore seguente:

*Il client non riesce a scaricare il criterio. Il servizio di trasferimento dei dati ha restituito "Errore BITS: 'Risposta del server non valida. Il protocollo seguito dal server non era quello definito. (-2145386469).*

Questo problema si verifica quando si configura il punto di gestione per HTTPS e il dispositivo usa la versione1906 o precedente del client di Configuration Manager.

Per risolvere questo problema, aggiornare il client di Configuration Manager nel dispositivo alla versione 1910 o successiva.

### <a name="task-sequences-cant-run-over-cmg"></a>Le sequenze di attività non possono essere eseguite su Cloud Management Gateway

*Si applica a: Configuration Manager versione 2002*

Esistono due casi in cui le sequenze di attività non possono essere eseguite in un dispositivo che comunica tramite Cloud Management Gateway (CMG):

- Si configura il sito per HTTP migliorato e il punto di gestione è HTTP.<!-- 6358851 -->

    Per risolvere il problema, eseguire l'aggiornamento alla versione 2006. In alternativa, configurare il punto di gestione per HTTPS.

- Il client è stato installato e registrato con un token di registrazione in blocco per l'autenticazione.<!-- 6377921 -->

    Per risolvere il problema, eseguire l'aggiornamento alla versione 2006. In alternativa, usare uno dei metodi di autenticazione seguenti:

  - Preregistrare il dispositivo nella rete interna
  - Configurare il dispositivo con un certificato di autenticazione client
  - Aggiungere il dispositivo ad Azure AD

## <a name="software-updates"></a>Aggiornamenti software

### <a name="security-roles-are-missing-for-phased-deployments"></a>Non sono presenti ruoli di sicurezza per le distribuzioni in più fasi

<!--3479337, SCCMDocs-pr issue 3095-->
*Si applica a: Configuration Manager versioni 1810, 1902*

Il ruolo di sicurezza predefinito **Gestione distribuzione del sistema operativo** dispone di autorizzazioni per le [distribuzioni in più fasi](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). I ruoli seguenti non dispongono di queste autorizzazioni:  

- **Amministratore applicazione**  
- **Gestione distribuzione applicazioni**  
- **Amministratore aggiornamento software**  

Per il ruolo **Autore di app** potrebbero risultare alcune autorizzazioni per le distribuzioni in più fasi, ma questo ruolo non dovrebbe essere in grado di creare distribuzioni.

Un utente con uno di questi ruoli può avviare la procedura guidata Crea una distribuzione in più fasi e visualizzare distribuzioni in più fasi per un'applicazione o un aggiornamento software. Non sarà tuttavia in grado di completare la procedura guidata o apportare modifiche a una distribuzione esistente.

Per risolvere il problema, creare un ruolo di sicurezza personalizzato. Copiare un ruolo di sicurezza esistente e aggiungere le autorizzazioni seguenti nella classe oggetto **Distribuzione in più fasi**:

- Creazione  
- Delete  
- Modifica  
- Lettura  

Per altre informazioni, vedere [Creare ruoli di sicurezza personalizzati](../configure/configure-role-based-administration.md#BKMK_CreateSecRole).

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a> A causa di una patch di sicurezza estesa per Windows 7 viene indicato che **non è possibile registrare** i dispositivi

<!-- 7283186 -->
_Si applica a: Configuration Manager versioni 2002 e precedenti_

La patch di sicurezza estesa di aprile 2020 per Windows 7 ha modificato la versione minima richiesta di diagtrack.dll da 10586 a 10240. A causa di questa modifica, per i dispositivi Windows 7 viene indicato che **non è possibile eseguire la registrazione** nel dashboard **Integrità connessione** di Desktop Analytics. Quando si esegue il drill-down nella visualizzazione del dispositivo per questo stato, la proprietà **Configurazione del servizio DiagTrack** visualizza lo stato seguente: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

Non è necessario trovare una soluzione alternativa per questo problema. Non disinstallare la patch di sicurezza di aprile. Se configurati correttamente, i dispositivi Windows 7 continuano a segnalare dati diagnostici al servizio Desktop Analytics e ad essere visualizzati nel portale.

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Se si usa l'inventario hardware per le viste distribuite, non è possibile eseguire l'onboarding in Desktop Analytics

<!-- 4950335 -->
*Si applica a: Configuration Manager versione 1902 con aggiornamento cumulativo e versione 1906*

Se si ha una gerarchia e si abilitano i dati del sito **Inventario hardware** per le [viste distribuite](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) sui collegamenti di replica siti, dopo aver configurato la connessione a Desktop Analytics in Configuration Manager verrà visualizzato l'errore seguente in M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Per risolvere il problema, disabilitare i dati del sito **Inventario hardware** per le viste distribuite su tutti i collegamenti di replica siti.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>La console si chiude in modo imprevisto durante la rimozione di raccolte

<!-- 4749443 -->
*Si applica a: Configuration Manager versione 1902 con aggiornamento cumulativo*

Dopo aver connesso il sito a [Desktop Analytics](../../../../desktop-analytics/connect-configmgr.md), è possibile abilitare l'opzione can **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**. Se si rimuove una raccolta e si applicano le modifiche, l'aggiunta immediata di una nuova raccolta causa un'eccezione non gestita. La console si chiude in modo imprevisto.

Per risolvere il problema, quando si rimuove una raccolta scegliere **OK** per chiudere la finestra delle proprietà. Aprire quindi di nuovo la finestra delle proprietà per aggiungere una nuova raccolta nella scheda **Connessione di Desktop Analytics** .

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>Il riquadro dello stato della distribuzione pilota visualizza alcuni dispositivi come 'non definiti'

<!-- 4547783 -->
*Si applica a: Configuration Manager versione 1902 con aggiornamento cumulativo*

Quando si usa la console di Configuration Manager per monitorare lo stato della distribuzione pilota, i dispositivi pilota aggiornati nella versione di destinazione di Windows per il piano di distribuzione vengono visualizzati come **non definiti** nel riquadro dello stato della distribuzione pilota.  

Questi dispositivi **non definiti** sono **aggiornati** con la versione di destinazione del sistema operativo per il piano di distribuzione. Non sono richieste ulteriori azioni.

## <a name="cloud-services"></a>Servizi cloud

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>Il servizio di Azure per il cloud per enti pubblici degli Stati Uniti viene visualizzato come cloud pubblico

<!-- 6036748 -->

*Si applica alla versione 1910*

Se si crea una connessione a un servizio di Azure e si imposta l'**ambiente Azure** sul cloud per enti pubblici, le proprietà della connessione visualizzano l'ambiente come cloud pubblico di Azure. Si tratta solo di un problema di visualizzazione nella console, il servizio si trova nel cloud per enti pubblici. Per confermare la configurazione, eseguire la query SQL seguente nel database del sito:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

Per il cloud per enti pubblici, il risultato di questa query è `2` per il tenant specifico.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Non è possibile scaricare contenuti da un gateway di gestione cloud abilitato per TLS 1.2

<!-- 5771680 -->

*Si applica alle versioni 1906, 1910 anello di aggiornamento anticipato*

Se si abilita un gateway di gestione cloud in modo che **funzioni come punto di distribuzione cloud e gestisca i contenuti di Archiviazione di Azure** ed **Enforce TLS 1.2**, è possibile che il download dei contenuti non riesca.

Nel file DataTransferService.log del client verranno riportati gli errori seguenti:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Nel file CMGContentService.log del server verranno riportati gli errori seguenti:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Come soluzione alternativa a questo problema:

- Aggiornare il sito alla versione disponibile a livello globale 1910, rilasciata il 20 dicembre 2019. Se in precedenza è stato eseguito l'aggiornamento all'anello di aggiornamento anticipato della versione 1910, è necessario eseguire l'aggiornamento a questa build quando è disponibile.

- In alternativa, usare un [punto di distribuzione cloud](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) tradizionale. Tale ruolo non impone l'uso di TLS 1.2, ma è compatibile con i client che richiedono TLS 1.2.

## <a name="protection"></a>Protezione

### <a name="bitlocker-management-appears-in-version-1906"></a>La gestione di BitLocker viene visualizzata nella versione 1906

*Si applica alla versione 1906*

<!-- 5984688 -->

Dopo il 21 novembre 2019, se si esegue l'aggiornamento alla versione 1906 dalla versione 1902 o precedente la funzionalità di gestione di BitLocker sarà attivata e disponibile. Si tratta di una funzionalità facoltativa a partire dalla versione 1910. Non è supportata nella versione 1906. Se si tenta di usarla nella versione 1906, potrebbero verificarsi risultati imprevisti. Se non si usa la funzionalità, non vi è alcun impatto.

Per usare la [funzionalità di gestione di BitLocker](../../../../protect/plan-design/bitlocker-management.md), eseguire l'aggiornamento alla versione 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
