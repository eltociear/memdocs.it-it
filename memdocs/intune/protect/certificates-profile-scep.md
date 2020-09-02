---
title: Usare i profili di certificato SCEP con Microsoft Intune - Azure | Microsoft Docs
description: Creare e assegnare profili di certificato SCEP (Simple Certificate Enrollment Protocol) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5126f2e5cc145e864fb4f56e472dba7a5179540f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915586"
---
# <a name="create-and-assign-scep-certificate-profiles-in-intune"></a>Creare e assegnare profili di certificato SCEP in Intune

Dopo aver [configurato l'infrastruttura](certificates-scep-configure.md) per supportare i certificati SCEP (Simple Certificate Enrollment Protocol), è possibile creare e quindi assegnare profili di certificato SCEP a utenti e dispositivi in Intune.

> [!IMPORTANT]
> Per usare un profilo di certificato SCEP, i dispositivi devono considerare attendibile l'autorità di certificazione (CA) radice attendibile. Per stabilire l'attendibilità della CA radice è consigliabile distribuire un [profilo certificato attendibile](../protect/certificates-configure.md#create-trusted-certificate-profiles) allo stesso gruppo che riceve il profilo certificato SCEP. I profili certificato attendibile eseguono il provisioning del certificato CA radice attendibile.

## <a name="create-a-scep-certificate-profile"></a>Creare un profilo certificato SCEP

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare e passare a **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le proprietà seguenti:
   - **Piattaforma**: scegliere la piattaforma dei dispositivi.
   - **Profilo**: Selezionare **Certificato SCEP**

     Per la piattaforma **Android Enterprise**, *Tipo di profilo* è diviso in due categorie: *Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale* e *Solo profilo di lavoro*. Assicurarsi di selezionare il profilo di certificato SCEP corretto per i dispositivi gestiti.  

     I profili certificato SCEP per il profilo *Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale* presentano le limitazioni seguenti:

      1. In Monitoraggio la generazione di report per i certificati non è disponibile per i profili di certificato SCEP del proprietario del dispositivo.

      2. Non è possibile usare Intune per revocare i certificati di cui è stato effettuato il provisioning tramite profili certificato SCEP per i proprietari del dispositivo. È possibile gestire la revoca tramite un processo esterno o direttamente con l'autorità di certificazione.

      3. Per i dispositivi Android Enterprise dedicati, i profili certificato SCEP sono supportati solo per la configurazione di reti Wi-Fi, per reti VPN e per l'autenticazione. I profili certificato SCEP per i dispositivi Android Enterprise dedicati non sono supportati per l'autenticazione di app.

4. Selezionare **Crea**.

5. In **Informazioni di base** immettere le proprietà seguenti:
   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo efficace, ad esempio, è *Profilo SCEP per l'intera azienda*.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** completare le configurazioni seguenti:

   - **Tipo di certificato**:

     *(Si applica a:  Android, Android Enterprise, iOS/iPadOS, macOS, Windows 8.1 e versioni successive, Windows 10 e versioni successive.)*

     Selezionare un tipo a seconda del modo in cui verrà usato il profilo di certificato:

     - **Utente**: i certificati di tipo *Utente* possono contenere attributi sia relativi agli utenti che ai dispositivi nel soggetto e nel nome alternativo del soggetto del certificato.  
     - **Dispositivo**:  I certificati di tipo *Dispositivo* possono contenere solo attributi relativi ai dispositivi nel soggetto e nel nome alternativo del soggetto del certificato.

       Usare il tipo **Dispositivo** per scenari quali i dispositivi senza utente, ad esempio i chioschi multimediali, o per i dispositivi Windows. Nei dispositivi Windows il certificato viene inserito nell'archivio certificati Computer locale.

     > [!NOTE]
     > In macOS i certificati di cui si effettua il provisioning con SCEP vengono sempre inseriti nel keychain di sistema (archivio di sistema) del dispositivo.
 
   - **Formato nome soggetto**:

     selezionare come Intune crea automaticamente il nome del soggetto nella richiesta di certificato. Le opzioni per il formato del nome soggetto dipendono dal tipo di certificato selezionato, ovvero **Utente** o **Dispositivo**.

     > [!NOTE]
     > L'uso di SCEP per ottenere certificati presenta un [problema noto](#avoid-certificate-signing-requests-with-escaped-special-characters) quando il nome del soggetto nella richiesta di firma del certificato risultante include uno dei caratteri seguenti come carattere di escape (preceduto da una barra rovesciata \\):
     > - \+
     > - ;
     > - ,
     > - =

     - **Tipo di certificato utente**

       Le opzioni di formato per *Formato nome soggetto* includono:

       - **Non configurato**
       - **Nome comune**
       - **Nome comune incluso l'indirizzo di posta elettronica**
       - **Nome comune come indirizzo di posta elettronica**
       - **IMEI (International Mobile Equipment Identity)**
       - **Numero di serie**
       - **Personalizzato**: quando si seleziona questa opzione, viene visualizzata anche una casella di testo **Personalizzato**. Usare questo campo per immettere un formato di nome soggetto personalizzato, incluse le variabili. Il formato personalizzato supporta due variabili: **CN (Nome comune)** ed **E (Posta elettronica)** . **CN (Nome comune)** può essere impostata su una delle variabili seguenti:

         - **CN={{UserName}}** : Nome utente, ad esempio janedoe.
         - **CN={{UserPrincipalName}}** : Nome dell'entità utente (UPN) dell'utente, ad esempio janedoe@contoso.com.\*
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
         
         \* Per i profili Android di tipo Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale, l'impostazione **CN={{UserPrincipalName}}** non funzionerà. I profili Android di tipo Profilo di lavoro completamente gestito, dedicato e di proprietà aziendale possono essere usati per i dispositivi senza utente, quindi questo profilo non potrà ottenere il nome dell'entità utente dell'utente. Se questa opzione è realmente necessaria per i dispositivi con utenti, è possibile usare una soluzione alternativa come la seguente: **CN={{UserName}}\@contoso.com** specifica il nome utente e il dominio aggiunti manualmente, ad esempio janedoe@contoso.com

      - **Tipo di certificato dispositivo**

        Le opzioni di formato per il formato del nome soggetto includono le variabili seguenti:

        - **{{AAD_Device_ID}}** o **{{AzureADDeviceId}}** : è possibile usare una delle due variabili per identificare un dispositivo in base all'ID Azure AD.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
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

   - **Nome alternativo soggetto**: specificare in che modo Intune crea automaticamente il nome alternativo del soggetto nella richiesta di certificato. Le opzioni per il nome alternativo del soggetto dipendono dal tipo di certificato selezionato, ovvero **Utente** o **Dispositivo**.

      - **Tipo di certificato utente**

        Selezionare uno degli attributi disponibili:

        - **Indirizzo di posta elettronica**
        - **Nome dell'entità utente (UPN)**

        Ad esempio, i certificati di tipo Utente possono includere il nome dell'entità utente (UPN) nel nome alternativo del soggetto. Se un certificato client viene usato per eseguire l'autenticazione in un server dei criteri di rete, impostare il nome alternativo del soggetto sul nome dell'entità utente.

      - **Tipo di certificato dispositivo**

        Usare l'elenco a discesa **Attributo** e selezionare un attributo, assegnare un **Valore** e selezionare **Aggiungi** per aggiungerlo al profilo di certificato. È possibile aggiungere più valori selezionando attributi aggiuntivi.

        Gli attributi disponibili includono:

        - **Indirizzo di posta elettronica**
        - **Nome dell'entità utente (UPN)**
        - **DNS**

        Con il tipo di certificato *Dispositivo*, per il valore è possibile usare le variabili del certificato del dispositivo seguenti:

        - **{{AAD_Device_ID}}** o **{{AzureADDeviceId}}** : è possibile usare una delle due variabili per identificare un dispositivo in base all'ID Azure AD.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}**
        - **{{MEID}}**

        Per specificare un valore per un attributo, includere il nome della variabile tra parentesi graffe, seguito dal testo per la variabile. Ad esempio, è possibile aggiungere il valore per l'attributo DNS **{{AzureADDeviceId}}.dominio.com** dove *.dominio.com* è il testo. Per un utente denominato *Utente1*, un indirizzo di posta elettronica potrebbe comparire come {{FullyQualifiedDomainName}}User1@Contoso.com.

        > [!IMPORTANT]
        > - Quando si usa una variabile di un certificato del dispositivo, racchiuderla tra parentesi graffe { }.
        > - Non usare parentesi graffe **{ }** , simboli di barra verticale **|** e punti e virgola **;** nel testo che segue la variabile.
        > - Le proprietà del dispositivo usate nel *soggetto* o nel *nome alternativo del soggetto* di un certificato del dispositivo, ad esempio **IMEI**, **SerialNumber** e **FullyQualifiedDomainName**, sono proprietà soggette a spoofing da parte di un utente con accesso al dispositivo.
        > - Un dispositivo deve supportare tutte le variabili specificate in un profilo di certificato, affinché tale profilo possa essere installato nel dispositivo.  Ad esempio, se si usa **{{IMEI}}** nel nome alternativo del soggetto di un profilo SCEP e il profilo viene assegnato a un dispositivo che non ha un numero IMEI, l'installazione del profilo non riesce.

   - **Periodo di validità del certificato**:

     È possibile immettere un valore inferiore, ma non superiore, al periodo di validità presente nel modello di certificato. Se il modello di certificato è stato configurato per [supportare un valore personalizzato che è possibile impostare dalla console di Intune](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template), usare questa impostazione per specificare la quantità di tempo rimanente prima della scadenza del certificato.

     Se ad esempio il periodo di validità del certificato nel modello di certificato è di due anni, è possibile immettere un valore di un anno ma non un valore di cinque anni. Inoltre, il valore deve essere inferiore rispetto al periodo di validità rimanente del certificato della CA emittente.

   - **Provider di archiviazione chiavi (KSP)** :

     *(Si applica a:  Windows 8.1 e versioni successive e Windows 10 e versioni successive)*

     Specificare dove viene archiviata la chiave per il certificato. Scegliere uno dei valori seguenti:

     - **Registra nel provider di archiviazione chiavi Trusted Platform Module (TPM) se presente, altrimenti nel provider di archiviazione chiavi software**
     - **Registra nel provider di archiviazione chiavi Trusted Platform Module (TPM) oppure genera errore**
     - **Registra in Passport oppure genera errore (Windows 10 e versioni successive)**
     - **Registra nel provider di archiviazione chiavi software**

   - **Utilizzo chiavi**:

     selezionare le opzioni di utilizzo delle chiavi per il certificato:

     - **Firma digitale**: consentire lo scambio di chiavi solo se viene usata una firma digitale per proteggere la chiave.
     - **Crittografia chiave**: consentire lo scambio di chiavi solo quando la chiave è crittografata.

   - **Dimensioni chiave (bit)** :

     selezionare il numero di bit contenuti nella chiave.

   - **Algoritmo hash**:

     *(Si applica ad Android, Android Enterprise, Windows 8.1 e versioni successive e Windows 10 e versioni successive)*

     selezionare uno dei tipi di algoritmo hash disponibili da usare con questo certificato. Selezionare il livello di sicurezza più avanzato supportato dai dispositivi che verranno connessi.

   - **Certificato radice**:

     Selezionare il *profilo certificato attendibile* configurato in precedenza e assegnato a utenti e dispositivi applicabili per questo profilo di certificato SCEP. Il profilo di certificato attendibile viene usato per eseguire il provisioning di utenti e dispositivi con il certificato CA radice attendibile. Per informazioni sul profilo di certificato attendibile, vedere [Esportare il certificato CA radice attendibile](certificates-configure.md#export-the-trusted-root-ca-certificate) e [Creare profili di certificato attendibili](certificates-configure.md#create-trusted-certificate-profiles) in *Usare i certificati per l'autenticazione in Intune*. Se sono disponibili un'autorità di certificazione radice e un'autorità di certificazione emittente, selezionare il profilo del certificato radice trusted che convalida l'autorità di certificazione emittente.
     > [!NOTE]
     > Nei dispositivi iOS/iPadOS, se sono disponibili un'autorità di certificazione radice e un'autorità di certificazione emittente, selezionare il profilo del certificato radice trusted che convalida l'autorità di certificazione radice. 

   - **Utilizzo chiavi avanzato**:

     aggiungere valori per lo scopo designato del certificato. Nella maggior parte dei casi il certificato richiede l'*autenticazione client* in modo che l'utente o il dispositivo possa eseguire l'autenticazione in un server. È possibile aggiungere altri utilizzi di chiavi in base alle esigenze.

   - **Soglia di rinnovo (%)** :

     immettere la percentuale di durata residua del certificato prima che il dispositivo richieda il rinnovo del certificato. Se si immette 20, ad esempio, il rinnovo del certificato verrà tentato quando il certificato risulta scaduto all'80% e verranno eseguiti ulteriori tentativi fino al completamento del rinnovo. Il rinnovo genera un nuovo certificato, che comporta una nuova coppia di chiavi pubblica/privata.

   - **URL server SCEP**:

     specificare uno o più URL per i server del servizio Registrazione dispositivi di rete che emettono certificati tramite SCEP. Ad esempio, `https://ndes.contoso.com/certsrv/mscep/mscep.dll`.

     Se necessario, è possibile aggiungere altri URL SCEP per il bilanciamento del carico. I dispositivi effettuano tre chiamate separate al server NDES: per ottenere le funzionalità dei server, per ottenere una chiave pubblica e quindi per inviare una richiesta di firma. Quando si usano più URL, è possibile che a causa del bilanciamento del carico venga usato un URL diverso per le chiamate successive a un server NDES. Se un server diverso viene contattato per una chiamata successiva durante la stessa richiesta, la richiesta avrà esito negativo.

     Il comportamento per la gestione dell'URL del server NDES è specifico per ogni piattaforma del dispositivo:

     - **Android**: il dispositivo usa in modo casuale l'elenco degli URL ricevuti nel criterio SCEP, quindi elabora l'elenco fino a quando non viene trovato un server NDES accessibile. Il dispositivo continua quindi a usare lo stesso URL e il medesimo server nell'intero processo. Se il dispositivo non è in grado di accedere ad alcun server NDES, il processo ha esito negativo.
     - **iOS/iPadOS**: Intune genera in modo casuale gli URL e fornisce un singolo URL a un dispositivo. Se il dispositivo non riesce ad accedere al server NDES, la richiesta SCEP ha esito negativo.
     - **Windows**: l'elenco di URL NDES viene creato in modo causale e quindi passato al dispositivo Windows, che quindi tenta gli URL nell'ordine ricevuto, fino a quando non ne viene individuato uno disponibile. Se il dispositivo non è in grado di accedere ad alcun server NDES, il processo ha esito negativo.

     Se un dispositivo non riesce a raggiungere lo stesso server NDES correttamente durante una delle tre chiamate al server NDES, la richiesta SCEP ha esito negativo. Questo potrebbe verificarsi, ad esempio, quando una soluzione di bilanciamento del carico fornisce un URL diverso per la seconda o terza chiamata al server NDES o fornisce un server NDES effettivo diverso in base a un URL virtualizzato per NDES. Dopo una richiesta non riuscita, un dispositivo prova a eseguire di nuovo il processo al successivo ciclo del criterio, a partire dall'elenco casuale di URL NDES (o un URL singolo per iOS/iPadOS).  

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

   Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

    Selezionare **Avanti**.

11. (*Solo per Windows 10*) In **Regole di applicabilità** specificare regole di applicabilità per perfezionare l'assegnazione di questo profilo. È possibile scegliere di assegnare o non assegnare il profilo in base all'edizione del sistema operativo o alla versione di un dispositivo.

   Per altre informazioni, vedere [Regole di applicabilità](../configuration/device-profile-create.md#applicability-rules) in *Creare un profilo di dispositivo in Microsoft Intune*.

12. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona Crea, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

### <a name="avoid-certificate-signing-requests-with-escaped-special-characters"></a>Evitare le richieste di firma del certificato con caratteri speciali di escape

Esiste un problema noto per le richieste di certificati SCEP e PKCS che includono un nome soggetto con uno o più dei caratteri speciali seguenti come carattere di escape. I nomi soggetto che includono uno dei caratteri speciali come carattere di escape generano un CSR con un nome soggetto errato. Un nome soggetto errato causa l'esito negativo della convalida della richiesta di verifica SCEP di Intune e la mancata emissione del certificato.

I caratteri speciali sono:
- \+
- ,
- ;
- =

Quando il nome del soggetto include uno dei caratteri speciali, usare una delle opzioni seguenti per ovviare a questa limitazione:

- Racchiudere tra virgolette il valore CN contenente il carattere speciale.  
- Rimuovere il carattere speciale dal valore CN.

**Ad esempio**, si supponga di avere un nome soggetto visualizzato come *Test user (TestCompany, LLC)* .  Una richiesta di firma del certificato che includa un CN con la virgola tra *TestCompany* e *LLC* presenta un problema.  È possibile evitare il problema racchiudendo l'intero CN tra virgolette oppure rimuovendo la virgola tra *TestCompany* e *LLC*:

- **Aggiungere le virgolette**: *CN="Test User (TestCompany, LLC)",OU=UserAccounts,DC=corp,DC=contoso,DC=com*
- **Rimuovere la virgola**: *CN=Test User (TestCompany LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

 I tentativi di escape della virgola tramite l'uso di una barra rovesciata, tuttavia, non riusciranno con un errore nei log CRP:
 
- **Escape della virgola**: *CN=Test User (TestCompany\\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

L'errore è simile al seguente:

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## <a name="assign-the-certificate-profile"></a>Assegnare il profilo certificato

La procedura per assegnare i profili di certificato SCEP è uguale a quella per la [distribuzione dei profili di dispositivo](../configuration/device-profile-assign.md) per altri scopi.

Per usare un profilo certificato SCEP, un dispositivo deve avere ricevuto anche il profilo certificato attendibile che ne esegue il provisioning insieme al certificato CA radice attendibile. Si consiglia di distribuire il profilo certificato radice attendibile e il profilo certificato SCEP agli stessi gruppi.

Tenere presente quanto segue prima di continuare:

- Quando si assegnano profili di certificato SCEP a gruppi, il file del certificato CA radice attendibile (specificato nel *profilo di certificato attendibile*) viene installato nel dispositivo. Il dispositivo usa il profilo di certificato SCEP per creare una richiesta di certificato per tale certificato CA radice attendibile.

- Il profilo di certificato SCEP viene installato solo nei dispositivi che eseguono la piattaforma specificata al momento della creazione del profilo di certificato.

- È possibile assegnare profili certificato alle raccolte di utenti o di dispositivi.

- Per pubblicare rapidamente un certificato in un dispositivo dopo la registrazione del dispositivo, assegnare il profilo certificato a un gruppo di utenti invece che a un gruppo di dispositivi. Se si assegna il profilo certificato a un gruppo di dispositivi, è necessario eseguire una registrazione completa dei dispositivi prima che questi ricevano i criteri.

- Se si usa la co-gestione per Intune e Configuration Manager, in Configuration Manager [impostare il dispositivo di scorrimento del carico di lavoro](/configmgr/comanage/how-to-switch-workloads) per Criteri di accesso alle risorse su **Intune** o **Intune pilota**. Questa impostazione consente ai client Windows 10 di avviare il processo di richiesta del certificato.

> [!NOTE]
> - Nei dispositivi iOS/iPadOS, quando un profilo certificato SCEP o un profilo certificato PKCS viene associato a un profilo aggiuntivo, ad esempio un profilo Wi-Fi o VPN, il dispositivo riceve un certificato per ognuno di questi profili aggiuntivi. Ne risulta che il dispositivo iOS/iPadOS riceve più certificati dalla richiesta di certificato SCEP o PKCS. 
> 
>   I certificati recapitati da SCEP sono univoci. I certificati recapitati da PKCS sono gli stessi, ma vengono visualizzati in modo diverso poiché ogni istanza del profilo è rappresentata da una riga separata nel profilo di gestione.
> - In iOS 13 e macOS 10.15, è necessario tenere presenti alcuni [requisiti di sicurezza aggiuntivi documentati da Apple](https://support.apple.com/HT210176).  


## <a name="next-steps"></a>Passaggi successivi

[Assegnare profili](../configuration/device-profile-assign.md)

[Risolvere i problemi di distribuzione dei profili certificato SCEP](../protect/troubleshoot-scep-certificate-profiles.md)