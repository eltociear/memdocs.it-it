---
title: Usare certificati PFX importati in Microsoft Intune - Azure | Microsoft Docs
description: Usare i certificati PKCS (Public Key Cryptography Standards) importati con Microsoft Intune. Importare i certificati, configurare i modelli di certificato, installare il connettore per certificati PFX importati di Intune e creare un profilo del certificato PKCS importato.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/29/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda; rimarram
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 630d270202f1064c9e80e7cb87df3929138ee54a
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048107"
---
# <a name="configure-and-use-imported-pkcs-certificates-with-intune"></a>Configurare e usare i certificati PKCS importati con Intune

Microsoft Intune supporta l'uso di certificati PKCS importati, comunemente usati per la crittografia S/MIME con profili di posta elettronica. Determinati profili di posta elettronica in Intune supportano un'opzione che consente di abilitare S/MIME, dove è possibile definire un certificato di firma S/MIME e un certificato di crittografia S/MIME.

La crittografia S/MIME è complessa perché la posta elettronica è crittografata con un certificato specifico:

- È necessario avere la chiave privata del certificato che ha crittografato il messaggio di posta elettronica nel dispositivo in cui si sta leggendo il messaggio, in modo che possa essere decrittografato.
- Prima della scadenza di un certificato in un dispositivo, è necessario importare un nuovo certificato in modo che il dispositivo possa continuare a decrittografare i nuovi messaggi di posta elettronica. Il rinnovo di questi certificati non è supportato.
- I certificati di crittografia vengono rinnovati regolarmente, pertanto è consigliabile mantenere il vecchio certificato nei dispositivi per garantire che la posta elettronica precedente possa continuare a essere decrittografata.  

Dal momento che si deve usare lo stesso certificato nei vari dispositivi, non è possibile usare i profili dei certificati [SCEP](certificates-scep-configure.md) o [PKCS](certficates-pfx-configure.md) per questo scopo, poiché i meccanismi di recapito di tali certificati inviano certificati univoci per dispositivo.

Per altre informazioni sull'uso di s/MIME con Intune, vedere [Usare s/MIME per crittografare la posta elettronica](certificates-s-mime-encryption-sign.md).

## <a name="supported-platforms"></a>Piattaforme supportate

Intune supporta l'importazione di certificati PFX per le piattaforme seguenti:

- Android - Amministratore di dispositivi
- Android Enterprise - Completamente gestito
- Android Enterprise - Profilo di lavoro
- Android Enterprise - Proprietà aziendale con profilo di lavoro
- iOS/iPadOS
- macOS
- Windows 10

## <a name="requirements"></a>Requisiti

Per usare i certificati PKCS importati con Intune, è necessaria l'infrastruttura seguente:

- **Connettore di certificati PFX per Microsoft Intune**:

  Ogni tenant di Intune supporta più istanze di questo connettore. Verificare che ogni connettore abbia accesso alla chiave privata usata per crittografare le password dei file PFX caricati.
  È possibile installare questo connettore nello stesso server di un'istanza del connettore di certificati di Microsoft Intune.

  Questo connettore gestisce le richieste per i file PFX importati in Intune per la crittografia S/MIME della posta elettronica per un utente specifico.

  Questo connettore consente l'aggiornamento automatico quando diventano disponibili nuove versioni. Per usare la funzionalità di aggiornamento, è necessario verificare che i firewall siano aperti per consentire al connettore di contattare **autoupdate.msappproxy.net** sulla porta **443**.

  Per altre informazioni, vedere [Endpoint di rete per Microsoft Intune](../fundamentals/intune-endpoints.md) e [Requisiti di configurazione di rete di Intune e larghezza di banda](../fundamentals/network-bandwidth-use.md).

- **Windows Server**:

  Usare Windows Server per ospitare il connettore di certificati PFX per Microsoft Intune.  Il connettore viene usato per elaborare le richieste per i certificati importati in Intune.
  
  Il connettore richiede l'accesso alle stesse porte descritte in dettaglio per i dispositivi gestiti, come indicato nel [contenuto per l'endpoint del dispositivo](https://docs.microsoft.com/intune/fundamentals/intune-endpoints#access-for-managed-devices).

  Intune supporta l'installazione del *connettore di certificati di Microsoft Intune* nello stesso server del *connettore di certificati PFX per Microsoft Intune*.

  Per supportare il connettore, il server deve eseguire .NET 4.6 Framework o versione successiva. Se .NET 4.6 Framework non è installato quando si avvia l'installazione del connettore, il programma di installazione del connettore lo installerà automaticamente.

- **Visual Studio 2015 o versione successiva** (facoltativo):

  Si usa Visual Studio per compilare il modulo PowerShell helper con i cmdlet per l'importazione dei certificati PFX in Microsoft Intune. Per ottenere i cmdlet helper di PowerShell, vedere [PFXImport PowerShell Project](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell) su GitHub.

## <a name="how-it-works"></a>Come funziona

Quando si usa Intune per distribuire un **certificato PFX importato** a un utente, in aggiunta al dispositivo sono disponibili due componenti:

- **Servizio Intune**: Archivia i certificati PFX in uno stato crittografato e gestisce la distribuzione del certificato al dispositivo dell'utente.  Le password che proteggono le chiavi private dei certificati vengono crittografate prima di essere caricate usando un modulo di protezione hardware o la crittografia di Windows, verificando che Intune non possa accedere alla chiave privata in qualsiasi momento.

- **Connettore di certificati PFX per Microsoft Intune**: Quando un dispositivo richiede un certificato PFX importato in Intune, la password crittografata, il certificato e la chiave pubblica del dispositivo vengono inviati al connettore.  Il connettore decrittografa la password usando la chiave privata locale e quindi crittografa di nuovo la password (e tutti i profili plist se si usa iOS) con la chiave del dispositivo prima di inviare di nuovo il certificato a Intune.  Intune recapita quindi il certificato al dispositivo e il dispositivo è in grado di decrittografarlo con la chiave privata del dispositivo e di installare il certificato.

## <a name="download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune"></a>Scaricare, installare e configurare il connettore di certificati PFX per Microsoft Intune

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Amministrazione del tenant** > **Connettori e token** > **Connettori di certificati** > **Aggiungi**.

   ![Download del connettore di certificati PFX per Microsoft Intune](./media/certificates-imported-pfx-configure/download-imported-pfxconnector.png)

3. Seguire le indicazioni per scaricare il *connettore di certificati PFX per Microsoft Intune* in un percorso accessibile dal server in cui si intende installare il connettore.

4. Al termine del download, accedere al server ed eseguire il programma di installazione (PfxCertificateConnectorBootstrapper.exe).  
   - Quando si accetta il percorso di installazione predefinito, il connettore viene installato in `Program Files\Microsoft Intune\PFXCertificateConnector`.
   - Il servizio Connector viene eseguito con l'account di sistema locale. Se è necessario un proxy per l'accesso a Internet, verificare che l'account del servizio locale possa accedere alle impostazioni del proxy nel server.

5. Dopo l'installazione, il connettore di certificati PFX per Microsoft Intune consente di aprire la scheda **Registrazione**. Per abilitare la connessione a Intune, selezionare **Accedi** e specificare un account con autorizzazioni di amministratore globale o di amministratore di Intune.

   > [!WARNING]
   > Per impostazione predefinita, in Windows Server la **Configurazione sicurezza avanzata IE** è impostata su **On** e questo può causare problemi di accesso a Office 365.

6. Chiudere la finestra.

7. Nell'interfaccia di amministrazione di Microsoft Endpoint Manager tornare a **Amministrazione del tenant** > **Connettori e token** > **Connettori di certificati**. Dopo alcuni istanti, viene visualizzato un segno di spunta verde e lo stato della connessione si aggiorna. Il server del connettore ora può comunicare con Intune.

## <a name="import-pfx-certificates-to-intune"></a>Importare certificati PFX in Intune

Usare [Microsoft Graph](https://docs.microsoft.com/graph) per importare i certificati PFX degli utenti in Intune. L'helper [PFXImport PowerShell Project su GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell) offre i cmdlet che consentono di semplificare le operazioni.

Se si preferisce usare una soluzione personalizzata con Graph, usare il [tipo di risorsa userPFXCertificate](https://docs.microsoft.com/graph/api/resources/intune-raimportcerts-userpfxcertificate?view=graph-rest-beta).

### <a name="build-pfximport-powershell-project-cmdlets"></a>Creare i cmdlet "PFXImport PowerShell Project"

Per usare i cmdlet PowerShell, compilare il progetto autonomamente con Visual Studio. Il processo è semplice e, benché possa essere eseguito sul server, è consigliabile eseguirlo nella workstation.  

1. Passare alla radice del repository [Intune-Resource-Access](https://github.com/microsoft/Intune-Resource-Access) su GitHub e quindi scaricare o clonare il repository con Git nel computer.

   ![Pulsante di download di GitHub](./media/certificates-imported-pfx-configure/github-download.png)

2. Passare a `.\Intune-Resource-Access-develop\src\PFXImportPowershell\` e aprire il progetto con Visual Studio usando il file **PFXImportPS.sln**.

3. In alto modificare **Debug** in **Versione**.

4. Passare a **Compila** e selezionare **Compila PFXImportPS**. Tra poco la conferma di **Visualizzazione completata** sarà visualizzata in basso a sinistra di Visual Studio.

   ![Opzione Compila di Visual Studio](./media/certificates-imported-pfx-configure/vs-build-release.png)

5. Il processo di compilazione crea una nuova cartella con il modulo PowerShell in `.\Intune-Resource-Access-develop\src\PFXImportPowershell\PFXImportPS\bin\Release`.

   La cartella **Release** verrà usata per i passaggi successivi.

### <a name="create-the-encryption-public-key"></a>Creare la chiave pubblica di crittografia

Importare i certificati PFX e le relative chiavi private in Intune. La password che protegge la chiave privata è crittografata con una chiave pubblica archiviata in locale. È possibile usare la crittografia di Windows, un modulo di sicurezza hardware o un altro tipo di crittografia per generare e archiviare le coppie di chiavi pubblica/privata.  A seconda del tipo di crittografia usata, la coppia di chiavi pubblica/privata può essere esportata in formato di file per il backup.

Il modulo di PowerShell offre i metodi che consentono di creare una chiave usando la crittografia di Windows. È anche possibile usare altri strumenti per creare una chiave.  

#### <a name="to-create-the-encryption-key-using-windows-cryptography"></a>Per creare la chiave di crittografia usando la crittografia di Windows

1. Copiare la cartella *Release* creata da Visual Studio nel server in cui è stato installato il **connettore di certificati PFX per Microsoft Intune**. La cartella contiene il modulo di PowerShell.

2. Nel server aprire *PowerShell* come amministratore e quindi passare alla cartella *Release* che contiene il modulo di PowerShell.

3. Per importare il modulo, eseguire `Import-Module .\IntunePfxImport.psd1`.

4. Quindi, eseguire `Add-IntuneKspKey -ProviderName "Microsoft Software Key Storage Provider" -KeyName "PFXEncryptionKey"`

   > [!TIP]
   > Il provider da usare deve essere selezionato di nuovo quando si importano i certificati PFX. È possibile usare il **provider di archiviazione chiavi per software Microsoft**, sebbene sia supportato l'uso di un provider diverso. Anche il nome della chiave è solo un esempio ed è possibile usare un nome di chiave diverso a scelta.

   Se si intende importare il certificato dalla workstation, è possibile esportare la chiave in un file con il comando seguente: `Export-IntunePublicKey -ProviderName "<ProviderName>" -KeyName "<KeyName>" -FilePath "<File path\Filename.PFX>"`

   La chiave privata deve essere importata nel server che ospita il connettore di certificati PFX per Microsoft Intune in modo che i certificati PFX importati possano essere elaborati correttamente.

#### <a name="to-use-a-hardware-security-module-hsm"></a>Per usare un modulo di protezione hardware

È possibile usare un modulo di protezione hardware per generare e archiviare la coppia di chiavi pubblica/privata. Per altre informazioni, vedere la documentazione del fornitore del modulo di protezione hardware.

### <a name="import-pfx-certificates"></a>Importare i certificati PFX

Il processo seguente usa i cmdlet PowerShell come esempio di importazione dei certificati PFX. È possibile scegliere opzioni diverse a seconda dei requisiti.

Le opzioni includono:

- Scopo designato (raggruppa i certificati in base a un tag):
  - non assegnato
  - smimeEncryption
  - smimeSigning

- Schema spaziatura interna:
  - oaepSha256
  - oaepSha384
  - oaepSha512

Selezionare il provider di archiviazione chiavi che corrisponde al provider usato per creare la chiave.

#### <a name="to-import-the-pfx-certificate"></a>Per importare il certificato PFX  

1. Esportare i certificati da un'autorità di certificazione (CA) seguendo la documentazione del provider.  Per i servizi certificati Microsoft Active Directory è possibile usare questo [script di esempio](https://gallery.technet.microsoft.com/Export-CMPfxCertificatesFro-d55f687b).

2. Nel server aprire *PowerShell* come amministratore e quindi passare alla cartella *Release* che contiene il modulo di PowerShell.

3. Per importare il modulo, eseguire `Import-Module .\IntunePfxImport.psd1`

4. Per eseguire l'autenticazione a Graph di Intune, eseguire `Set-IntuneAuthenticationToken  -AdminUserName "<Admin-UPN>"`

   > [!NOTE]
   > Quando viene eseguita l'autenticazione per Graph, è necessario specificare le autorizzazioni per l'ID app. Se è la prima volta che si usa questa utilità, è necessario un *amministratore globale*. I cmdlet PowerShell usano lo stesso ID app usato con gli [esempi di PowerShell per Intune](https://github.com/microsoftgraph/powershell-intune-samples).

5. Convertire la password per ogni file PFX che si sta importando in una stringa sicura eseguendo `$SecureFilePassword = ConvertTo-SecureString -String "<PFXPassword>" -AsPlainText -Force`.

6. Per creare un oggetto **UserPFXCertificate**, eseguire `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>"`

   ad esempio `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "C:\temp\userA.pfx" $SecureFilePassword "userA@contoso.com" "Microsoft Software Key Storage Provider" "PFXEncryptionKey" "smimeEncryption"`

   > [!NOTE]
   > Quando si importa il certificato da un sistema diverso dal server in cui è installato il connettore, usare il comando seguente che include il percorso del file di chiave: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>" "<PaddingScheme>" "<File path to public key file>"`
   >
   > Il *VPN* non è supportato come IntendedPurpose. 


7. Importare l'oggetto **UserPFXCertificate** in Intune eseguendo `Import-IntuneUserPfxCertificate -CertificateList $userPFXObject`

8. Per verificare che il certificato è stato importato, eseguire `Get-IntuneUserPfxCertificate -UserList "<UserUPN>"`

9.  Come procedura consigliata per pulire la cache dei token di AAD senza attendere che scada da sola, eseguire `Remove-IntuneAuthenticationToken`

Per altre informazioni sugli altri comandi disponibili, vedere il file Leggimi in [PFXImport PowerShell Project su GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="create-a-pkcs-imported-certificate-profile"></a>Creare un profilo certificato PKCS importato

Dopo aver importato i certificati in Intune, creare un profilo **certificato PKCS importato** e assegnarlo ai gruppi di Azure Active Directory.

> [!NOTE]
> Dopo la creazione di un profilo certificato PKCS importato, i valori **Scopo designato** e **Provider di archiviazione chiavi** (KSP) nel profilo sono di sola lettura e non possono essere modificati. Se è necessario un valore diverso per una di queste impostazioni, creare e distribuire un nuovo profilo. 

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare e passare a **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le proprietà seguenti:
   - **Piattaforma**: scegliere la piattaforma dei dispositivi.
   - **Profilo**: Selezionare **Certificato PKCS importato**

4. Selezionare **Crea**.

5. In **Informazioni di base** immettere le proprietà seguenti:
   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo efficace, ad esempio, è *Profilo certificato importato PKCS per l'intera azienda*.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** immettere le proprietà seguenti:

   - **Scopo designato**: Specificare lo scopo designato dei certificati importati per questo profilo. Gli amministratori possono importare certificati con scopi designati diversi, ad esempio firma S/MIME o crittografia S/MIME. Lo scopo designato selezionato nel profilo certificato corrisponde al profilo certificato con i certificati importati corretti. Lo scopo designato è un tag usato per raggruppare i certificati importati e non garantisce che i certificati importati con tale tag soddisfino lo scopo designato.  

   <!-- Not in new UI:
   - **Certificate validity period**: Unless the validity period was changed in the certificate template, this option defaults to one year.
   -->
   - **Provider di archiviazione chiavi (KSP)** : per Windows, selezionare la posizione in cui archiviare le chiavi nel dispositivo.

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

   Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

    Selezionare **Avanti**.

11. (*Solo per Windows 10*) In **Regole di applicabilità** specificare regole di applicabilità per perfezionare l'assegnazione di questo profilo. È possibile scegliere di assegnare o non assegnare il profilo in base all'edizione del sistema operativo o alla versione di un dispositivo.

    Per altre informazioni, vedere [Regole di applicabilità](../configuration/device-profile-create.md#applicability-rules) in *Creare un profilo di dispositivo in Microsoft Intune*.

    Selezionare **Avanti**.

12. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona Crea, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="support-for-third-party-partners"></a>Supporto per partner di terze parti

I partner seguenti forniscono metodi o strumenti supportati che è possibile usare per importare i certificati PFX in Intune.

### <a name="digicert"></a>DigiCert

Se si usa il servizio DigiCert PKI Platform, è possibile usare lo **strumento di importazione dei certificati S/MIME di Intune** di DigiCert per importare i certificati PFX in Intune. Se si usa questo strumento, non è più necessario seguire le istruzioni descritte in dettaglio nella sezione [Per importare certificati PFX in Intune](#import-pfx-certificates-to-intune) più indietro in questo articolo.

Per altre informazioni sullo strumento di importazione di DigiCert, inclusa la procedura per ottenere lo strumento, vedere https://knowledge.digicert.com/tutorials/microsoft-intune.html nella Knowledge Base di DigiCert.

### <a name="keytalk"></a>KeyTalk

Se si usa il servizio KeyTalk, è possibile configurare il servizio per importare certificati PFX in Intune. Dopo aver completato l'integrazione, non è più necessario seguire le istruzioni descritte in dettaglio nella sezione [Importare certificati PFX in Intune](#import-pfx-certificates-to-intune) più indietro in questo articolo.

Per altre informazioni sull'integrazione di KeyTalk con Intune, vedere https://keytalk.com/support nella Knowledge Base di KeyTalk.

## <a name="next-steps"></a>Passaggi successivi

Il profilo è stato creato, ma non è ancora operativo. [Assegnare](../configuration/device-profile-assign.md) il nuovo profilo del dispositivo.
