---
title: Risolvere i problemi dell'uso di profili certificato PKCS per il provisioning di certificati con Microsoft Intune | Microsoft Docs
description: Risolvere i problemi relativi all'uso di profili coppia di chiavi pubblica e privata (PKCS) con i dispositivi per richiedere certificati da usare con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7667cf1d62040c4435f41ffbe377452d3666a3ec
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85343088"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Risoluzione dei problemi di distribuzione del certificato PKCS in Microsoft Intune

Le informazioni contenute in questo articolo possono essere utili per risolvere diversi problemi comuni quando si distribuiscono certificati coppia di chiavi pubblica e privata (PKCS) in Microsoft Intune. Prima di procedere alla risoluzione dei problemi, verificare di aver completato le attività seguenti come indicato in [Configurare e usare i certificati PKCS con Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca):

- Esaminare i [requisiti per l'uso di profili certificato PKCS](../protect/certficates-pfx-configure.md#requirements)
- Esportare il certificato radice dall'autorità di certificazione (CA) globale (enterprise)
- Configurare i modelli di certificato nell'autorità di certificazione
- Installare e configurare il Connettore di certificati di Intune
- Creare e distribuire un profilo certificato attendibile per distribuire il certificato radice
- Creare e distribuire un profilo certificato PKCS

La causa più comune dei problemi per i profili certificato PKCS è la configurazione del profilo certificato PKCS. Esaminare la configurazione dei profili e cercare errori di digitazione nei nomi dei server o nei nomi di dominio completi (FQDN) e verificare che l'**autorità di certificazione** e il **nome dell'autorità di certificazione** siano corretti.

- **Autorità di certificazione**: nome di dominio completo (FQDN) interno del computer dell'autorità di certificazione, ad esempio, server1.domain.local.
- **Nome dell'autorità di certificazione**: nome dell'autorità di certificazione visualizzato in MMC dell'autorità di certificazione. Guardare in **Autorità di certificazione (locale)**

Per verificare la correttezza dell'autorità di certificazione e del nome dell'autorità di certificazione, è possibile usare il [programma da riga di comando certutil](https://docs.microsoft.com/windows-server/administration/windows-commands/certutil) sulla CA.

## <a name="pkcs-communication-overview"></a>Panoramica della comunicazione PKCS

Il grafico seguente offre una panoramica di base del processo di distribuzione del certificato PKCS in Intune.

> [!div class="mx-imgBorder"]
> ![Flusso del profilo certificato PKCS](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. Un amministratore crea un profilo certificato PKCS in Intune.
2. Il servizio Intune richiede che Connettore di certificati di Intune locale crei un nuovo certificato per l'utente.
3. Connettore di certificati di Intune invia un BLOB PFX e una richiesta all'autorità di certificazione Microsoft.
4. L'autorità di certificazione rilascia e invia il certificato utente PFX a Connettore di certificati di Intune.
5. Connettore di certificati di Intune carica il certificato utente PFX crittografato in Intune.
6. Intune decrittografa il certificato utente PFX e ne esegue nuovamente la crittografia per il dispositivo usando il certificato di gestione dei dispositivi.  Intune invia quindi il certificato utente PFX al dispositivo.
7. Il dispositivo segnala lo stato del certificato a Intune.

## <a name="data-and-log-files"></a>File di dati e di log

Per identificare problemi con il flusso di lavoro di comunicazione e provisioning dei certificati, esaminare i file di log dell'infrastruttura server e dei dispositivi. Le sezioni successive per la risoluzione dei problemi con i profili certificato PKCS esaminano i file di log a cui si fa riferimento in questa sezione.

- [Log dell'infrastruttura e del server](#logs-for-on-premises-infrastructure)

I log del dispositivo dipendono dalla piattaforma del dispositivo:

- [iOS e iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Log per l'infrastruttura locale
  
L'infrastruttura locale che supporta l’uso dei profili certificato PKCS per le distribuzioni di certificati include Connettore di certificati di Microsoft Intune, il servizio NDES eseguito in un server Windows e l'autorità di certificazione.

I file di log per questi ruoli includono il Visualizzatore eventi di Windows, le console di certificazione e vari file di log specifici per il Connettore di certificati di Intune, il servizio Registrazione dispositivi di rete o altri ruoli e operazioni che fanno parte dell'infrastruttura locale.

- **NDESConnector_date_time.svclog**:

  questo log visualizza le comunicazioni dal Connettore di certificati di Microsoft Intune al servizio cloud di Intune. Per visualizzare questo log è possibile usare lo strumento [Visualizzatore di tracce dei servizi](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe).

  Chiave del Registro di sistema associata: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Percorso: Nel server che ospita il servizio Registrazione dispositivi di rete: *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time.svclog**:

  Questo log visualizza il modulo criteri del servizio Registrazione dispositivi di rete che riceve e verifica le richieste di certificati. Per visualizzare questo log è possibile usare lo strumento [Visualizzatore di tracce dei servizi](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe).

  Percorso: Nel server che ospita il servizio Registrazione dispositivi di rete: *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **NDESPlugin.log**:

  Questo log visualizza il passaggio delle richieste di certificati al punto di registrazione certificati e la verifica di tali richieste.

  Percorso: Nel server che ospita il servizio Registrazione dispositivi di rete: *%program_files%\Microsoft Intune\NDESPolicyModule\logs*

- **Registro applicazioni di Windows**:

  Percorso: Nel server che ospita il servizio Registrazione dispositivi di rete: Eseguire **eventvwr.msc** per aprire il Visualizzatore eventi di Windows

### <a name="logs-for-android-devices"></a>Log per dispositivi Android

Per i dispositivi che eseguono Android, usare il file di log dell’app **Portale aziendale Android** con nome **OMADM.log**. Prima di raccogliere ed esaminare i log, abilitare la [registrazione dettagliata](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md), quindi riprodurre il problema.

Per raccogliere il file OMADM.log da un dispositivo, vedere [Caricare e inviare per posta elettronica i log tramite un cavo USB](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

È anche possibile [caricare e inviare i log tramite posta elettronica](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) al supporto.

### <a name="logs-for-ios-and-ipados-devices"></a>Log per i dispositivi iOS e iPadOS

Per i dispositivi che eseguono iOS/iPadOS si usano i log di debug e **Xcode** eseguito in un computer Mac:

1. Connettere il dispositivo iOS/iPadOS al Mac, quindi passare ad **Applicazioni** > **Utility** per aprire l'app Console.

2. In **Azione** selezionare **Includi messaggi di informazioni** e **Includi messaggi di debug**.

   ![Selezionare le opzioni del log](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Riprodurre il problema e salvare i log in un file di testo:
   1. Selezionare **Modifica** > **Seleziona tutto** per selezionare tutti i messaggi nella schermata corrente, quindi selezionare **Modifica** > **Copia** per copiare i messaggi negli Appunti.
   2. Aprire l'applicazione TextEdit, incollare i log copiati in un nuovo file di testo e quindi salvare il file.

Il log di Portale aziendale per i dispositivi iOS e iPadOS non contiene informazioni sui profili certificato PKCS.

### <a name="logs-for-windows-devices"></a>Log per dispositivi Windows

Per i dispositivi che eseguono Windows, usare i Registri eventi di Windows per diagnosticare i problemi di registrazione o di gestione per i dispositivi gestiti con Intune.

Nel dispositivo aprire **Visualizzatore eventi** > **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Registri eventi di Windows](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="common-errors"></a>Errori comuni

Gli errori comuni seguenti sono trattati ognuno in una delle prossime sezioni:

- [Server RPC non disponibile 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [Impossibile individuare un server dei criteri di registrazione 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [L'invio è in sospeso](#the-submission-is-pending)
- [Parametro non corretto 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [Negato dal modulo criteri](#denied-by-policy-module)
- [Profilo certificato bloccato come In sospeso](#certificate-profile-stuck-as-pending)
- [Errore -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>Server RPC non disponibile 0x800706ba

Durante la distribuzione PFX, il certificato radice trusted compare sul dispositivo mentre il certificato PFX non compare. Il file di log di NDES Connector contiene la stringa **Server RPC non disponibile. 0x800706ba**, come illustrato nella prima riga dell'esempio seguente:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Causa 1: configurazione non corretta della CA in Intune

Questo problema può verificarsi quando il profilo certificato PKCS specifica un server errato o contiene errori di ortografia per il nome o il nome di dominio completo della CA. La CA è specificata nelle proprietà seguenti del profilo:

- Certification authoity
- Nome dell'autorità di certificazione

**Risoluzione**:

Esaminare le impostazioni seguenti e correggerle se non sono corrette:

- La proprietà **Autorità di certificazione** visualizza il nome FQDN interno del server della CA.
- La proprietà **Nome dell'autorità di certificazione** visualizza il nome della CA.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Causa 2: la CA non supporta il rinnovo del certificato per le richieste firmate da certificati CA precedenti

Se il nome FQDN e il nome della CA sono corretti nel profilo certificato PKCS, esaminare il registro applicazioni di Windows nel server dell'autorità di certificazione. Cercare un **ID evento 128** simile all'esempio seguente:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

Quando il certificato della CA si rinnova, deve firmare il certificato Firma risposta Protocollo di stato del certificato online (OCSP, Online Certificate Status Protocol). La firma abilita il certificato Firma risposta OCSP per la convalida di altri certificati tramite il controllo dello stato di revoca di questi. Questa firma non è abilitata per impostazione predefinita.

**Risoluzione**:

Forzare manualmente la firma del certificato:

1. Nel server della CA aprire un prompt dei comandi con privilegi elevati ed eseguire il comando seguente: **certutil -setreg ca\UseDefinedCACertInRequest 1**
2. Riavviare il servizio Servizi certificati.

Dopo il riavvio del servizio Servizi certificati, i dispositivi possono ricevere i certificati.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>Impossibile individuare un server dei criteri di registrazione 0x80094015

**Impossibile individuare un server dei criteri di registrazione** e **0x80094015**, come illustrato nell'esempio seguente:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Causa: nome del server dei criteri di registrazione certificato

Questo problema si verifica se il computer che ospita Intune NDES Connector non riesce a individuare un server dei criteri di registrazione certificato.

**Risoluzione**:

Configurare manualmente il nome del server dei criteri di registrazione certificati nel computer che ospita NDES Connector. Per configurare il nome, usare il cmdlet di PowerShell [Add-CertificateEnrollmentPolicyServer](https://docs.microsoft.com/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps).

### <a name="the-submission-is-pending"></a>L'invio è in sospeso

Dopo la distribuzione di un profilo certificato PKCS ai dispositivi mobili, i certificati non vengono acquisiti e il log di NDES Connector contiene la stringa **The submission is pending** (L'invio è in sospeso), come illustrato nell'esempio seguente:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

Nella cartella **Richieste in sospeso** del server dell'autorità di certificazione, poi, è possibile visualizzare la richiesta PFX:

> [!div class="mx-imgBorder"]
> ![Screenshot della cartella Richieste in sospeso dell'autorità di certificazione](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Causa: configurazione non corretta della gestione delle richieste

Questo problema si verifica se l'opzione **Imposta lo stato della richiesta certificato in modo che risulti in sospeso. Il certificato dovrà essere emesso dall'amministratore** è selezionata nella finestra di dialogo **Proprietà** > **Modulo criterio** > **Proprietà** dell'autorità di certificazione.

> [!div class="mx-imgBorder"]
> ![Screenshot delle proprietà di Modulo criterio](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Risoluzione**:

Modificare le proprietà Modulo criterio per impostare: **Utilizza le impostazioni contenute nel modello di certificato. Altrimenti, emetti automaticamente il certificato.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>Parametro non corretto 0x80070057

Con il Connettore di certificati di Intune installato e configurato correttamente, i dispositivi non ricevono certificati PKCS e il log di NDES Connector contiene la stringa **The parameter is incorrect. 0x80070057** (Parametro non corretto. 0x80070057), come illustrato nell'esempio seguente:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Causa: configurazione del profilo PKCS

Questo problema si verifica se il profilo PKCS in Intune non è configurato correttamente. Di seguito sono descritti errori di configurazione comuni:

- Il profilo include un nome non corretto per la CA.
- Il nome alternativo del soggetto (SAN, Subject Alternative Name) è configurato per l'indirizzo di posta elettronica, ma l'utente di destinazione non ha ancora di un indirizzo di posta elettronica valido. Questa combinazione restituisce un valore Null per il nome SAN, che non è valido.

**Risoluzione**:

Verificare le configurazioni seguenti per il profilo PKCS e quindi attendere l'aggiornamento dei criteri nel dispositivo:

- Configurazione con il nome della CA
- Assegnazione al gruppo utenti corretto
- Indirizzi di posta elettronica validi per gli utenti nel gruppo

Per altre informazioni, vedere [Configurare e usare i certificati PKCS con Intune](../protect/certficates-pfx-configure.md).

### <a name="denied-by-policy-module"></a>Negato dal modulo criteri

Se i dispositivi ricevono il certificato radice trusted ma non ricevono il certificato PFX e il log di NDES Connector contiene la stringa **The submission failed: Denied by Policy Module** (Invio non riuscito: negato dal modulo criteri), come illustrato nell'esempio seguente:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Causa: autorizzazioni dell'account computer per il modello di certificato

Questo problema si verifica quando l'account computer del server che ospita Connettore di certificati di Intune non ha le autorizzazioni necessarie per il modello di certificato.

**Risoluzione**:

1. Accedere all'autorità di certificazione globale (enterprise) con un account che abbia privilegi amministrativi.
2. Aprire la console **Autorità di certificazione**, fare clic con il pulsante destro del mouse su **Modelli di certificato e selezionare Gestisci**.
3. Individuare il modello di certificato e aprire la finestra di dialogo **Proprietà** del modello.
4. Selezionare la scheda **Sicurezza** e aggiungere l'account computer relativo al server in cui è installato Connettore di certificati di Microsoft Intune. Concedere all'account le autorizzazioni **Lettura** e **Registrazione**.
5. Selezionare **Applica** > **OK** per salvare il modello di certificato e quindi chiudere la console **Modelli di certificato**.
6. Nella console **Autorità di certificazione** fare clic con il pulsante destro del mouse su **Modelli di certificato** > **Nuovo** > **Modello di certificato da rilasciare**.
7. Selezionare il modello modificato e quindi fare clic su **OK**.

Per altre informazioni, vedere [Configurare i modelli di certificato nella CA](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca).

### <a name="certificate-profile-stuck-as-pending"></a>Profilo certificato bloccato come In sospeso

Nell'interfaccia di amministrazione di Microsoft Endpoint Manager non è possibile distribuire i profili certificato PKCS con lo stato **In sospeso**. Nel file di log di NDES Connector non sono presenti errori evidenti.
Poiché la causa di questo problema non viene identificata chiaramente nei log, considerare tutte le cause seguenti.

#### <a name="cause-1---unprocessed-request-files"></a>Causa: 1 file di richiesta non elaborati

Esaminare i file di richiesta per individuare eventuali errori che indichino il motivo per cui non è stato possibile elaborarli.

1. Nel computer che ospita NDES Connector passare a **%programfiles%\Microsoft Intune\PfxRequest** tramite Esplora file.
2. Esaminare i file nelle cartelle **Errore** ed **Elaborazione** usando l'editor di testo preferito.

   > [!div class="mx-imgBorder"]
   > ![Esaminare la cartella PfxRequest](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. In questi file cercare le voci che indicano errori o suggeriscono problemi. Tramite uno strumento di ricerca basato sul Web, cercare i messaggi di errore per individuare gli indizi relativi ai motivi per cui la richiesta non è stata elaborata e le soluzioni a tali problemi.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Motivo 2: configurazione errata per il profilo certificato PKCS

Se nella cartella **Errore**, **Elaborazione** o **Operazione riuscita** non sono presenti file di richiesta, il motivo potrebbe essere che al profilo certificato PKCS è associato un profilo errato, ad esempio una CA subordinata, oppure viene usato un certificato radice errato.

**Risoluzione**:

1. Esaminare il profilo certificato attendibile per assicurarsi di aver distribuito il certificato radice dalla CA globale (enterprise) ai dispositivi.
2. Esaminare il profilo certificato PKCS per assicurarsi che faccia riferimento alla CA e al tipo di certificato corretti, nonché al corretto profilo certificato attendibile che distribuisce il certificato radice ai dispositivi.

Per altre informazioni, vedere [Usare i certificati per l'autenticazione in Microsoft Intune](../protect/certificates-configure.md).

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Errore -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

La distribuzione dei certificati PKCS non riesce e la console dei certificati nella CA emittente visualizza un messaggio con la stringa **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED**, come illustrato nell'esempio seguente:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Causa: configurazione non corretta di "Inserisci nella richiesta"

Questo problema si verifica se l'opzione **Inserisci nella richiesta** non è abilitata nella scheda **Nome soggetto** della finestra di dialogo **Proprietà** del modello di certificato.

> [!div class="mx-imgBorder"]
> ![Configurare le proprietà NDES](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Risoluzione**:

Modificare il modello per risolvere il problema di configurazione:

1. Accedere all'autorità di certificazione globale (enterprise) con un account che abbia privilegi amministrativi.
2. Aprire la console **Autorità di certificazione**, fare clic con il pulsante destro del mouse su **Modelli di certificato** e selezionare **Gestisci**.
3. Aprire la finestra di dialogo Proprietà del modello di certificato.
4. Nella scheda **Nome soggetto** selezionare **Fornisci nella richiesta**.
5. Selezionare **OK** per salvare il modello di certificato e quindi chiudere la console **Modelli di certificato**.
6. Nella console **Autorità di certificazione** fare clic con il pulsante destro del mouse su **Modelli** > **Nuovo** > **Modello di certificato da emettere**.
7. Selezionare il modello modificato e quindi selezionare **OK**.

## <a name="next-steps"></a>Passaggi successivi

Se è ancora necessario trovare una soluzione o per altre informazioni su Intune, pubblicare una domanda nel [forum di Microsoft Intune](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). I forum sono frequentati da molti tecnici del supporto, MVP e membri del team di sviluppo Microsoft. C'è la quindi una buona possibilità di ricevere assistenza.

Per aprire una richiesta di supporto presso il team del supporto tecnico di Microsoft Intune, vedere [Come ottenere supporto per Microsoft Intune](../fundamentals/get-support.md).
Per altre informazioni sulla distribuzione di certificati PKCS, vedere gli articoli seguenti:

- [Configurare e usare i certificati PKCS con Intune](../protect/certficates-pfx-configure.md)
- [Configurare un profilo certificato per i dispositivi in Microsoft Intune](../protect/certificates-configure.md)
- [Rimuovere i certificati SCEP e PKCS in Microsoft Intune](../protect/remove-certificates.md)
