---
title: Usare certificati con chiave pubblica e privata in Microsoft Intune - Azure | Microsoft Docs
description: Usare i certificati PKCS (Public Key Cryptography Standards) con Microsoft Intune, usare i certificati radice e i modelli di certificato, installare il Connettore Microsoft Intune (servizio Registrazione dispositivi di rete) e usare i profili di configurazione dei dispositivi per un certificato PKCS.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1024681ed42c192983ffde23777de72c40622c65
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423722"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>Configurare e usare i certificati PKCS con Intune

Intune supporta l'uso di certificati con coppia di chiavi pubblica e privata (PKCS). Questo articolo fornisce informazioni utili per configurare l'infrastruttura necessaria, ad esempio i connettori di certificati locali, esportare un certificato PKCS e quindi aggiungere il certificato a un profilo di configurazione del dispositivo in Intune.

Microsoft Intune include impostazioni predefinite per utilizzare i certificati PKCS per l’accesso e l’autenticazione delle risorse dell’organizzazione. I certificati consentono di autenticare e proteggere l'accesso alle risorse aziendali, ad esempio una rete VPN o Wi-Fi. Queste impostazioni vengono distribuite nei dispositivi usando i profili di configurazione dei dispositivi in Intune.

Per informazioni sull'uso di certificati PKCS importati, vedere [Certificati PFX importati](certificates-imported-pfx-configure.md).


## <a name="requirements"></a>Requisiti

Per usare i certificati PKCS con Intune, è necessaria l'infrastruttura seguente:

- **Dominio di Active Directory**:  
  tutti i server elencati in questa sezione devono essere aggiunti al dominio di Active Directory.

  Per altre informazioni sull'installazione e sulla configurazione di Active Directory Domain Services, vedere [Pianificazione e progettazione di Active Directory Domain Services](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning).

- **Autorità di certificazione**:  
   Un'autorità di certificazione globale (enterprise).

  Per altre informazioni sull'installazione e sulla configurazione di Servizi certificati Active Directory (AD CS), vedere [Active Directory Certificate Services Step-by-Step Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10)) (Guida dettagliata di Servizi certificati Active Directory).

  > [!WARNING]  
  > Intune richiede l'esecuzione di Servizi certificati Active Directory con un'autorità di certificazione globale (enterprise), non con un'autorità di certificazione autonoma (Standalone).

- **Un client**:  
  Per la connessione alla CA globale (enterprise).

- **Certificato radice**:  
  Una copia del certificato radice esportato dall'autorità di certificazione globale (enterprise).

- **Connettore di certificati PFX per Microsoft Intune**:

  Per informazioni sul connettore di certificati PFX, inclusi i prerequisiti e le versioni di rilascio, vedere [Connettori di certificati](certificate-connectors.md).

  > [!IMPORTANT]
  > A partire dal rilascio del connettore di certificati PFX versione 6.2008.60.607, il connettore Microsoft Intune non è più necessario per i profili di certificato PKCS. 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>Esportare il certificato radice dall'autorità di certificazione globale (enterprise)

Per l'autenticazione di un dispositivo con una VPN, una rete Wi-Fi o altre risorse, un dispositivo richiede un certificato della CA radice o intermedio. La procedura seguente illustra come ottenere il certificato richiesto dall'autorità di certificazione globale (enterprise).

**Usare una riga di comando**:  

1. Accedere al server dell'autorità di certificazione radice con l'account amministratore.

2. Passare a **Start** > **Esegui** e quindi immettere **Cmd** per aprire il prompt dei comandi.

3. Specificare **certutil -ca.cert ca_name.cer** per esportare il certificato radice come file denominato *ca_name.cer*.

## <a name="configure-certificate-templates-on-the-ca"></a>Configurare i modelli di certificato nella CA

1. Accedere all'autorità di certificazione globale (enterprise) con un account che abbia privilegi amministrativi.
2. Aprire la console **Autorità di certificazione**, fare clic con il pulsante destro del mouse su **Modelli di certificato** e selezionare **Gestisci**.
3. Trovare il modello di certificato **Utente**, fare clic con il pulsante destro del mouse su di esso e scegliere **Duplica modello** per aprire **Proprietà nuovo modello**.

    > [!NOTE]
    > Per scenari di firma e crittografia S/MIME della posta elettronica, molti amministratori usano certificati separati per la firma e la crittografia. Se si usa Servizi certificati Microsoft Active Directory, è possibile usare il modello **Solo firma di Exchange** per i certificati di firma S/MIME per la posta elettronica e il modello **Utente di Exchange** per i certificati di crittografia S/MIME.  Se si usa un'autorità di certificazione di terze parti è consigliabile rivedere il le istruzioni di tale autorità per la configurazione dei modelli di firma e crittografia.

4. Nella scheda **Compatibilità**:

    - Impostare **Autorità di certificazione** su **Windows Server 2008 R2**
    - Impostare **Destinatario certificato** su **Windows 7 / Server 2008 R2**

5. Nella scheda **Generale** impostare **Nome visualizzato modello** su un valore significativo.

    > [!WARNING]
    > Per impostazione predefinita, il parametro **Nome modello** corrisponde al valore **Nome visualizzato modello** *senza spazi*. Annotare il nome del modello, sarà necessario in un secondo momento.

6. In **Gestione richiesta** selezionare **Rendi la chiave privata esportabile**.

    > [!NOTE]
    > Diversamente da SCEP, con PKCS la chiave privata del certificato viene generata nel server in cui è installato il connettore e non nel dispositivo. È necessario che il modello di certificato consenta l'esportazione della chiave privata, in modo che il connettore di certificati sia in grado di esportare il certificato PFX e di inviarlo al dispositivo. 
    >
    > Tuttavia, si noti che i certificati vengono installati nel dispositivo stesso con la chiave privata contrassegnata come non esportabile.

7. In **Crittografia** verificare che il campo **Dimensioni minime chiave** sia impostato su 2048.
8. In **Nome soggetto** scegliere **Inserisci nella richiesta**.
9. In **Estensioni** verificare che nell'area **Criteri di applicazione** siano presenti Crittografia file system, Posta elettronica sicura e Autenticazione client.

    > [!IMPORTANT]
    > Per i modelli di certificato iOS/iPadOS, accedere alla scheda **Estensioni**, aggiornare **Utilizzo chiavi** e verificare che l'opzione **Firma come prova dell'origine** non sia selezionata.

10. In **Sicurezza** aggiungere l'account computer per il server in cui si installa il connettore Microsoft Intune. Assegnare all'account le autorizzazioni **Lettura** e **Registrazione**.
11. Selezionare **Applica** > **OK** per salvare il modello di certificato. Chiudere la **console Modelli di certificato**.
12. Nella console **Autorità di certificazione** fare clic con il pulsante destro del mouse su **Modelli di certificato** > **Nuovo** > **Modello di certificato da rilasciare**. Scegliere il modello creato nei passaggi precedenti. Selezionare **OK**.
13. Per consentire al server di gestire i certificati per gli utenti e i dispositivi registrati, eseguire i passaggi seguenti:

    1. Fare clic con il pulsante destro del mouse sull'autorità di certificazione e scegliere **Proprietà**.
    2. Nella scheda della sicurezza aggiungere l'account computer del server in cui si eseguono i connettori (il **connettore Microsoft Intune** e il **connettore di certificati PFX per Microsoft Intune**). 
    3. Assegnare all'account le autorizzazioni **Rilascio e gestione certificati** e **Richiesta certificati**.

14. Disconnettersi dall'autorità di certificazione globale (enterprise).

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>Scaricare, installare e configurare il connettore di certificati PFX

Prima di iniziare, [verificare i requisiti per il connettore](certificate-connectors.md) e assicurarsi che l'ambiente e il server Windows in uso siano pronti per supportare il connettore.

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Amministrazione del tenant** > **Connettori e token** > **Connettori di certificati** >  **+Aggiungi**.

3. Fare clic su *Scaricare il software del connettore del certificato* per il connettere per PKCS #12 e salvare il file in un percorso a cui è possibile accedere dal server in cui si installerà il connettore.

   ![Download del connettore Microsoft Intune](./media/certficates-pfx-configure/download-connector.png)

4. Al termine del download, accedere al server ed eseguire il programma di installazione (PfxCertificateConnectorBootstrapper.exe).  
   - Quando si accetta il percorso di installazione predefinito, il connettore viene installato in `Program Files\Microsoft Intune\PFXCertificateConnector`.
   - Il servizio Connector viene eseguito con l'account di sistema locale. Se è necessario un proxy per l'accesso a Internet, verificare che l'account del servizio locale possa accedere alle impostazioni del proxy nel server.

5. Dopo l'installazione, il connettore di certificati PFX per Microsoft Intune consente di aprire la scheda **Registrazione**. Per abilitare la connessione a Intune, selezionare **Accedi** e specificare un account con autorizzazioni di amministratore globale o di amministratore di Intune.

   > [!WARNING]
   > Per impostazione predefinita, in Windows Server la **Configurazione sicurezza avanzata IE** è impostata su **On** e questo può causare problemi di accesso a Office 365.

6. Chiudere la finestra.

7. Nell'interfaccia di amministrazione di Microsoft Endpoint Manager tornare a **Amministrazione del tenant** > **Connettori e token** > **Connettori di certificati**. Dopo alcuni istanti, viene visualizzato un segno di spunta verde e lo stato della connessione si aggiorna. Il server del connettore ora può comunicare con Intune.

## <a name="create-a-trusted-certificate-profile"></a>Creare un profilo certificato attendibile

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare e passare a **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le proprietà seguenti:
   - **Piattaforma**: Scegliere la piattaforma dei dispositivi che riceveranno questo profilo.
   - **Profilo**: selezionare **Certificato attendibile**
  
4. Selezionare **Crea**.

5. In **Informazioni di base** immettere le proprietà seguenti:
   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo efficace, ad esempio, è *Profilo certificato attendibile per l'intera azienda*.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** specificare il file con estensione cer del certificato CA radice esportato in precedenza.

   > [!NOTE]
   > In base alla piattaforma selezionata nel **passaggio 3**, si può avere la possibilità di scegliere l'**archivio di destinazione** per il certificato.

   ![Creare un profilo e caricare un certificato attendibile](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

   Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Pianificare la distribuzione del profilo certificato negli stessi gruppi che ricevono il profilo certificato PKCS. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

    Selezionare **Avanti**.

11. (*Solo per Windows 10*) In **Regole di applicabilità** specificare regole di applicabilità per perfezionare l'assegnazione di questo profilo. È possibile scegliere di assegnare o non assegnare il profilo in base all'edizione del sistema operativo o alla versione di un dispositivo.

  Per altre informazioni, vedere [Regole di applicabilità](../configuration/device-profile-create.md#applicability-rules) in *Creare un profilo di dispositivo in Microsoft Intune*.

12. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona Crea, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="create-a-pkcs-certificate-profile"></a>Creare un profilo certificato PKCS

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare e passare a **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le proprietà seguenti:
   - **Piattaforma**: scegliere la piattaforma dei dispositivi. Le opzioni disponibili sono:
     - Amministratore dispositivo Android
     - Android Enterprise > Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale
     - Android Enterprise > Solo profilo di lavoro
     - iOS/iPadOS
     - macOS
     - Windows 10 e versioni successive
   - **Profilo**: Selezionare **Certificato PKCS**

   > [!NOTE]
   > Nei dispositivi con un profilo Android Enterprise, i certificati installati usando un profilo di certificato PKCS non sono visibili nel dispositivo. Per verificare la corretta distribuzione del certificato, controllare lo stato del profilo nella console di Intune.
4. Selezionare **Crea**.

5. In **Informazioni di base** immettere le proprietà seguenti:
   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo efficace, ad esempio, è *Profilo PKCS per l'intera azienda*.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** le impostazioni configurabili variano in base alla piattaforma scelta. Selezionare la piattaforma per le impostazioni dettagliate:-Amministratore di dispositivi Android -Android Enterprise -iOS/iPadOS -Windows 10
   
   |Impostazione     | Piattaforma     | Dettagli   |
   |------------|------------|------------|
   |**Soglia di rinnovo (%)**        |<ul><li>All         |il valore consigliato è 20%  | 
   |**Periodo di validità del certificato**  |<ul><li>All         |se il modello di certificato non è stato cambiato, questa opzione può essere impostata su un anno. |
   |**Provider di archiviazione chiavi (KSP)**   |<ul><li>Windows 10  |per Windows, selezionare la posizione in cui archiviare le chiavi nel dispositivo. |
   |**Autorità di certificazione**      |<ul><li>All         |visualizza il nome di dominio completo (FQDN, Fully Qualified Domain Name) interno dell'autorità di certificazione globale (enterprise).  |
   |**Nome dell'autorità di certificazione** |<ul><li>All         |specifica il nome dell'autorità di certificazione globale (enterprise), ad esempio "Contoso Certification Authority" (Autorità di certificazione Contoso). |
   |**Nome modello di certificato**    |<ul><li>All         |Elenca il nome del modello di certificato. |
   |**Tipo di certificato**             |<ul><li>Android Enterprise (*Profilo di lavoro*)</li><li>iOS</li><li>macOS</li><li>Windows 10 e versioni successive|Selezionare un tipo: <ul><li> i certificati di tipo **Utente** possono contenere attributi sia relativi agli utenti che ai dispositivi nel soggetto e nel nome alternativo del soggetto del certificato. </il><li>I certificati di tipo **Dispositivo** possono contenere solo attributi relativi ai dispositivi nel soggetto e nel nome alternativo del soggetto del certificato. Usare il tipo Dispositivo per scenari quali i dispositivi senza utente, ad esempio i chioschi multimediali o altri dispositivi condivisi.  <br><br> Questa selezione influisce sul formato del nome soggetto. |
   |**Formato nome soggetto**          |<ul><li>All         |Per informazioni dettagliate su come configurare il formato del nome soggetto, vedere [Formato del nome soggetto](#subject-name-format) più avanti in questo articolo.  <br><br> Per la maggior parte delle piattaforme usare l'opzione **Nome comune**, se non diversamente richiesto. <br><br>Per le piattaforme seguenti, il formato del nome soggetto è determinato dal tipo di certificato: <ul><li>Android Enterprise (*Profilo di lavoro*)</li><li>iOS</li><li>macOS</li><li>Windows 10 e versioni successive</li></ul>  <p>  |
   |**Nome alternativo soggetto**     |<ul><li>All         |Per *Attributo* selezionare **Nome dell'entità utente (UPN)** se non diversamente richiesto, configurare un *Valore* corrispondente e quindi fare clic su **Aggiungi**. <br><br>Per altre informazioni, vedere [Formato del nome soggetto](#subject-name-format) più avanti in questo articolo.|
   |**Utilizzo chiavi avanzato**           |<ul><li> Amministratore dispositivo Android </li><li>Android Enterprise (*Proprietario del dispositivo*, *Profilo di lavoro*) </li><li>Windows 10 |I certificati richiedono in genere l'*Autenticazione Client* in modo che l'utente o il dispositivo possa eseguire l'autenticazione a un server. |
   |**Consenti a tutte le app l'accesso alla chiave privata** |<ul><li>macOS  |Impostare su **Abilita** per concedere alle app configurate per l'accesso al dispositivo Mac associato la chiave privata dei certificati PKCS. <br><br> Per altre informazioni su questa impostazione, vedere *AllowAllAppsAccess* nella sezione Certificate Payload (Payload del certificato) del documento [Configuration Profile Reference](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) (Informazioni di riferimento sui profili di configurazione) nella documentazione per sviluppatori Apple. |
   |**Certificato radice**             |<ul><li>Amministratore dispositivo Android </li><li>Android Enterprise (*Proprietario del dispositivo*, *Profilo di lavoro*) |Selezionare un profilo del certificato CA radice assegnato in precedenza. |

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

   Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Pianificare la distribuzione del profilo del certificato negli stessi gruppi che ricevono il profilo del certificato PKCS. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona Crea, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.


### <a name="subject-name-format"></a>Formato del nome soggetto

Quando si crea un profilo di certificato PKCS per le piattaforme seguenti, le opzioni per il formato del nome soggetto dipendono dal tipo di certificato selezionato, **Utente** o **Dispositivo**.  

Piattaforme:

- Android Enterprise (*Profilo di lavoro*)
- iOS
- macOS
- Windows 10 e versioni successive

> [!NOTE]
> L'uso di PKCS per ottenere certificati presenta un problema noto ([lo stesso problema rilevato per SCEP](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters)) quando il nome del soggetto nella richiesta di firma del certificato risultante include uno dei caratteri seguenti come carattere di escape (preceduto da una barra rovesciata \\):
> - \+
> - ;
> - ,
> - =

- **Tipo di certificato utente**  
  Le opzioni di formato per *Formato nome soggetto* includono due variabili: **CN (Nome comune)** ed **E (Posta elettronica)** . **CN (Nome comune)** può essere impostata su una delle variabili seguenti:

  - **CN={{UserName}}** : nome dell'entità utente (UPN) dell'utente, ad esempio janedoe@contoso.com.
  - **CN={{AAD_Device_ID}}** : ID assegnato quando si registra un dispositivo in Azure Active Directory (AD). Questo ID è in genere usato per l'autenticazione con Azure AD.
  - **CN={{SERIALNUMBER}}** : numero di serie (SN) univoco usato in genere dal produttore per identificare un dispositivo.
  - **CN={{IMEINumber}}** : numero IMEI (International Mobile Equipment Identity) univoco usato per identificare un telefono cellulare.
  - **CN={{OnPrem_Distinguished_Name}}** : sequenza di nomi distinti relativi separati da virgola, ad esempio *CN=Giorgia Fanucci,OU=UserAccounts,DC=corp,DC=contoso,DC=com*.

    Per usare la variabile *{{OnPrem_Distinguished_Name}}* , assicurarsi di sincronizzare l'attributo utente *onpremisesdistinguishedname* usando [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) con Azure AD.

  - **CN={{onPremisesSamAccountName}}** : gli amministratori possono sincronizzare l'attributo samAccountName da Active Directory ad Azure AD usando Azure AD Connect in un attributo denominato *onPremisesSamAccountName*. Intune può sostituire tale variabile come parte di una richiesta di emissione di certificati nel soggetto di un certificato. L'attributo samAccountName è il nome di accesso utente usato per supportare i client e i server da una versione precedente di Windows (precedente a Windows 2000). Il formato del nome di accesso dell'utente è: *NomeDomino\utenteTest* o solo *utenteTest*.

    Per usare la variabile *{{onPremisesSamAccountName}}* , assicurarsi di sincronizzare l'attributo utente *onPremisesSamAccountName* usando [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) con Azure AD.

  Usando una combinazione di una o più variabili e stringhe statiche, è possibile creare un formato di nome soggetto personalizzato, ad esempio:  
  - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**
  
  Questo esempio include un formato di nome soggetto che usa le variabili CN ed E, oltre a stringhe per i valori di unità organizzativa (OU), organizzazione (O), località (L), stato (S) e paese (C). L'argomento [Funzione CertStrToName](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea) visualizza questa funzione e le relative stringhe supportate.

- **Tipo di certificato dispositivo**  
  Le opzioni di formato per il formato del nome soggetto includono le variabili seguenti: 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEI}}**
  - **{{DeviceName}}**
  - **{{FullyQualifiedDomainName}}** *(applicabile solo per i dispositivi Windows e aggiunti a un dominio)*
  - **{{MEID}}**

  È possibile specificare queste variabili, seguite dal testo per la variabile, nella casella di testo. Ad esempio, il nome comune per un dispositivo denominato *Dispositivo1* può essere aggiunto come **CN={{DeviceName}}Dispositivo1**.

  > [!IMPORTANT]  
  > - Quando si specifica una variabile, racchiudere il nome della variabile tra parentesi graffe { }, come illustrato nell'esempio, per evitare un errore.  
  > - Le proprietà del dispositivo usate nel *soggetto* o nel *nome alternativo del soggetto* di un certificato del dispositivo, ad esempio **IMEI**, **SerialNumber** e **FullyQualifiedDomainName**, sono proprietà soggette a spoofing da parte di un utente con accesso al dispositivo.
  > - Un dispositivo deve supportare tutte le variabili specificate in un profilo di certificato, affinché tale profilo possa essere installato nel dispositivo.  Ad esempio, se si usa **{{IMEI}}** nel nome del soggetto di un profilo SCEP e il profilo viene assegnato a un dispositivo che non ha un numero IMEI, l'installazione del profilo non riesce.

## <a name="next-steps"></a>Passaggi successivi

[Usare SCEP per i certificati ](certificates-scep-configure.md) o [Rilasciare certificati PKCS da un servizio Web di gestione PKI Symantec](certificates-digicert-configure.md).

[Risolvere i problemi relativi ai profili di certificato PKCS](../protect/troubleshoot-pkcs-certificate-profiles.md)
