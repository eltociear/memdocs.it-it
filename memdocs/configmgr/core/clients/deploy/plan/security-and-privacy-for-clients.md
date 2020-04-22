---
title: Sicurezza e privacy dei client
titleSuffix: Configuration Manager
description: Informazioni sulla sicurezza e sulla privacy per i client di Configuration Manager.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4922502b49ab2da9ce393fab809e4dc583fd962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694839"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Sicurezza e privacy per i client di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene informazioni sulla sicurezza e sulla privacy per i client di Configuration Manager e informazioni sui dispositivi mobili gestiti con il [connettore Exchange Server](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a> Procedure di sicurezza consigliate per i client  

Il sito di Configuration Manager accetta dati da dispositivi che eseguono il client di Configuration Manager. In questo modo espone il sito a un potenziale attacco da parte dei client. Ad esempio, i client potrebbero inviare un inventario non corretto o tentare di sovraccaricare i sistemi del sito. Distribuire il client di Configuration Manager solo ai dispositivi considerati attendibili. Inoltre, è possibile usare le seguenti procedure consigliate per proteggere il sito da dispositivi non autorizzati o compromessi:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Usare i certificati di infrastruttura a chiave pubblica (PKI) per le comunicazioni client con sistemi del sito che eseguono IIS.  

- Quale proprietà del sito, configurare **Impostazioni sistema del sito** su **Solo HTTPS**.  

- Installare i client con la proprietà CCMSetup `UsePKICert`.  

- Usare un elenco di revoche di certificati (CRL) e assicurarsi che i client e i server di comunicazione possano sempre accedervi.  

Alcuni client dispositivo mobile o basati su internet richiedono questi certificati. Microsoft consiglia tali certificati per tutte le connessioni client sulla intranet.  

Per altre informazioni sui requisiti dei certificati PKI e su come vengono usati per contribuire alla protezione di Configuration Manager, vedere [Requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Approvare automaticamente i computer client dai domini attendibili e controllare e approvare manualmente gli altri computer  

L'approvazione identifica un computer considerato attendibile per la gestione da parte di Configuration Manager quando non è possibile usare l'autenticazione PKI. Per configurare l'approvazione client, la gerarchia offre le opzioni seguenti:  

- Manuale
- Automatica per i computer nei domini attendibili
- Automatica per tutti i computer  

Il metodo più sicuro è quello che prevede l'approvazione automatica dei client membri di domini attendibili, con successivo controllo e approvazione manuale di tutti gli altri computer. Non è consigliabile approvare automaticamente tutti i client a meno che non ci si avvalga di altri controlli di accesso per impedire l'ingresso nella rete a computer non attendibili.  

Per altre informazioni sull'approvazione manuale dei computer, vedere [Gestire i client dal nodo Dispositivi](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Non affidarsi al blocco per impedire l'accesso dei client alla gerarchia di Configuration Manager  

I client bloccati vengono rifiutati dall'infrastruttura di Configuration Manager. Non potranno quindi comunicare con i sistemi del sito per scaricare criteri, caricare dati di inventario o inviare messaggi di stato.

Il blocco è concepito per gli scenari seguenti:

- Per bloccare supporti di avvio persi o danneggiati quando si distribuisce un sistema operativo ai client.
- Quando tutti i sistemi del sito accettano connessioni client HTTPS.

In quest'ultimo caso, tuttavia, è opportuno non affidarsi al blocco per proteggere la gerarchia di Configuration Manager da computer non attendibili. In questo scenario, un client bloccato potrebbe associarsi di nuovo al sito con un nuovo certificato autofirmato e un ID hardware.

La revoca dei certificati è la prima linea difesa contro certificati potenzialmente compromessi. Un elenco di revoche di certificati (CRL) è reso disponibile soltanto da un'infrastruttura PKI supportata. Il blocco dei client in Configuration Manager offre una seconda linea di difesa per la protezione della gerarchia.  

Per altre informazioni, vedere [Determinare se bloccare i client](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Usare i metodi di installazione client più sicuri e più adatti al proprio ambiente  

- Per i computer del dominio, i metodi di installazione client basati su aggiornamento software e sui Criteri di gruppo sono più sicuri dell'installazione push client.  

- Se si applicano controlli di accesso e controlli delle modifiche, usare metodi di creazione dell'immagine e installazione manuali.  

- A partire dalla versione 1806, usare l'autenticazione reciproca Kerberos con l'installazione push client.  

Di tutti i metodi di installazione client, l'installazione push client è il meno sicuro, poiché comporta numerose dipendenze, incluse le autorizzazioni amministrative locali, la condivisione Admin$ e molte eccezioni del firewall. Il numero e la tipologia di queste dipendenze aumentano la superficie di attacco.  

A partire dalla versione 1806, quando si usa il push client il sito può richiedere l'autenticazione reciproca Kerberos non consentendo il fallback a NTLM prima di stabilire la connessione. Questo miglioramento consente di proteggere la comunicazione tra il server e il client. Per altre informazioni , vedere [Come installare i client con l'installazione push client](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->  

Per altre informazioni sui diversi metodi di installazione client, vedere [Metodi di installazione client](client-installation-methods.md).  

Quando possibile, selezionare un metodo di installazione client che preveda autorizzazioni di sicurezza minime in Configuration Manager. È anche consigliabile limitare gli utenti amministratori assegnati ai ruoli di sicurezza con autorizzazioni che possono essere usate per scopi diversi dalla distribuzione client. Ad esempio, la configurazione dell'aggiornamento automatico del client richiede il ruolo di protezione **Amministratore completo**, che garantisce a un utente amministratore tutte le autorizzazioni di sicurezza.  

Per altre informazioni sulle dipendenze e sulle autorizzazioni di sicurezza necessarie per ogni metodo di installazione client, vedere "Dipendenze del metodo di installazione" in [Prerequisiti per computer client](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Se è necessario usare l'installazione push client, adottare misure aggiuntive per proteggere l'account di installazione push client  

Questo account deve essere membro del gruppo **Administrators** locale in ogni computer in cui verrà installato il client di Configuration Manager. Non aggiungere l'account di installazione push client al gruppo **Domain Admins**. Creare invece un gruppo globale e aggiungerlo al gruppo locale **Admnistrators** sui client. Creare un oggetto Criteri di gruppo per aggiungere un'impostazione di Gruppi con restrizioni per l'aggiunta dell'account di installazione push client nel gruppo locale **Administrators**.  

Per una maggiore sicurezza, creare più account di installazione push client, ognuno con accesso amministrativo a un numero limitato di computer. In questo modo, qualora venga compromesso un account, risulteranno compromessi solo i computer client a cui tale account può accedere.  

### <a name="remove-certificates-before-imaging-clients"></a>Rimuovere i certificati prima di creare l'immagine dei client  

Rimuovere sempre i certificati prima di acquisire l'immagine dei client quando questi vengono distribuiti usando le immagini del sistema operativo. I certificati includono i certificati PKI per l'autenticazione client e i certificati autofirmati. Se non vengono rimossi, i client potrebbero rappresentarsi reciprocamente. Non è possibile verificare i dati di ogni client.  

Per altre informazioni, vedere [Creare una sequenza di attività per acquisire un sistema operativo](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Verificare che i computer client di Configuration Manager ottengano una copia autorizzata dei certificati seguenti:  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Certificato della chiave radice attendibile di Configuration Manager  

Quando sono soddisfatte entrambe le condizioni seguenti, i client si basano sulla chiave radice attendibile di Configuration Manager per l'autenticazione dei punti di gestione validi:  

- Lo schema di Active Directory non è stato esteso a Configuration Manager.
- I client non usano certificati PKI quando comunicano con i punti di gestione.  

In questo scenario, i client non sono in grado di verificare in alcun modo l'attendibilità di un punto di gestione per la gerarchia, a meno che non usino la chiave radice attendibile. Senza la chiave radice attendibile, un utente malintenzionato esperto potrebbe indirizzare i client verso un punto di gestione non autorizzato.  

Quando i client non sono in grado di scaricare la chiave radice attendibile di Configuration Manager dal catalogo globale o tramite i certificati PKI, eseguire il pre-provisioning dei client con la chiave radice attendibile per verificare che non possano essere indirizzati a un punto di gestione non autorizzato. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>Certificato di firma del server del sito  

I client usano questo certificato per verificare che il server del sito abbia firmato i criteri scaricati da un punto di gestione. Questo certificato è autofirmato dal server del sito e pubblicato in Servizi di dominio Active Directory.  

Per impostazione predefinita, quando i client non sono in grado di scaricare il certificato di firma del server del sito dal catalogo globale, lo scaricano dal punto di gestione. Se quest'ultimo è esposto a una rete non attendibile come Internet, è consigliabile installare manualmente nei client i certificati di firma del server del sito. In questo modo non sarà possibile scaricare criteri client alterati da un punto di gestione compromesso.  

Per installare manualmente il certificato di firma del server del sito, usare la proprietà client.msi CCMSetup **SMSSIGNCERT**. Per altre informazioni, vedere [Proprietà di installazione client](../about-client-installation-properties.md).  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Non usare l'assegnazione automatica del sito se il client scarica la chiave radice attendibile dal primo punto di gestione con cui entra in contatto  

Per evitare il rischio che un nuovo client scarichi la chiave radice attendibile da un punto di gestione non autorizzato, usare l'assegnazione automatica del sito solo negli scenari seguenti:  

- Il client può accedere alle informazioni del sito di Configuration Manager pubblicate in Active Directory Domain Services.  

- Viene eseguito il pre-provisioning del client con la chiave radice attendibile.  

- Sono usati certificati PKI rilasciati da un'autorità di certificazione dell'organizzazione (enterprise) per stabilire un trust tra il client e il punto di gestione.  

Per altre informazioni sulla chiave radice attendibile, vedere [Pianificare la chiave radice attendibile](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Installare i computer client con l'opzione Client.msi CCMSetup SMSDIRECTORYLOOKUP=NoWINS  

Il metodo di individuazione del servizio più sicuro per il rilevamento di siti e punti di gestione da parte dei client è quello che prevede l'utilizzo di Servizi di dominio Active Directory. In alcuni ambienti, questo metodo può non essere applicabile perché, ad esempio, non è possibile estendere lo schema di Active Directory per Configuration Manager o perché i client sono in una foresta o in un gruppo di lavoro non attendibili. In alternativa, è possibile usare la pubblicazione DNS come metodo di posizione del servizio. Se entrambi i metodi non sono applicabili e se il punto di gestione non è configurato per le connessioni client HTTPS, i client possono eseguire il fallback a WINS.  

Dal momento che la pubblicazione su WINS è meno sicura rispetto agli altri metodi di pubblicazione, configurare i computer client in modo tale che eseguano il fallback usando WINS specificando **SMSDIRECTORYLOOKUP = NoWINS**. Qualora sia necessario usare WINS per la posizione del servizio, usare **SMSDIRECTORYLOOKUP=WINSSECURE**. È l'impostazione predefinita. e usa la chiave radice attendibile di Configuration Manager per convalidare il certificato autofirmato del punto di gestione.  

> [!NOTE]  
> Quando il client è configurato per **SMSDIRECTORYLOOKUP=WINSSECURE** e rileva un punto di gestione da WINS, il client controlla la sua copia della chiave radice attendibile di Configuration Manager presente in WMI.  
>
> Se la firma sul certificato del punto di gestione corrisponde alla copia del client della chiave radice attendibile, il certificato viene convalidato e il client avvia la comunicazione con il punto di gestione rilevato tramite WINS.  
>
> Se la firma sul certificato del punto di gestione non corrisponde alla copia del client della chiave radice attendibile, il certificato non viene convalidato e il client non comunicherà con il punto di gestione rilevato tramite WINS.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Assicurarsi che le dimensioni delle finestre di manutenzione siano sufficienti per la distribuzione degli aggiornamenti software critici  

Le finestre di manutenzione per le raccolte di dispositivi limitano il numero di possibili installazioni del software da parte di Configuration Manager su questi dispositivi. Se vengono configurate dimensioni insufficienti della finestra di manutenzione, il client potrebbe non essere in grado di installare aggiornamenti software critici, diventando vulnerabile ad attacchi altrimenti limitati dall'aggiornamento software.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Adottare precauzioni di sicurezza aggiuntive per ridurre la superficie di attacco su dispositivi Windows Embedded con filtri di scrittura  

Quando i filtri di scrittura vengono abilitati su dispositivi con Windows Embedded, qualsiasi modifica o installazione software viene eseguita solo sulla sovrapposizione e non permane dopo il riavvio del dispositivo. Se si usa Configuration Manager per disabilitare i filtri di scrittura, durante questo periodo il dispositivo con Windows Embedded è vulnerabile alle modifiche su tutti i volumi, comprese le cartelle condivise.  

Configuration Manager blocca il computer durante questo periodo in modo da consentire l'accesso solo agli amministratori locali. Quando possibile, adottare precauzioni di sicurezza aggiuntive per proteggere il computer, ad esempio abilitando altre restrizioni del firewall.  

Se si usano delle finestre di manutenzione per rendere permanenti le modifiche, pianificarle attentamente per ridurre al minimo il tempo di disabilitazione dei filtri di scrittura, pur garantendo un intervallo sufficiente al completamento delle installazioni software e dei riavvii.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Usare la versione del client più recente con l'installazione client basata su aggiornamento software

Se si usa l'installazione client basata su aggiornamento software e si installa una versione del client successiva sul sito, aggiornare l'aggiornamento software pubblicato per consentire ai client di ricevere la versione più recente dal punto di aggiornamento software.  

Quando si aggiorna il sito, l'aggiornamento software per la distribuzione client pubblicato nel punto di aggiornamento software non viene aggiornato automaticamente. Pubblicare nuovamente il client di Configuration Manager nel punto di aggiornamento software, quindi aggiornare il numero di versione.  

Per altre informazioni, vedere [Come installare i client con l'installazione basata sull'aggiornamento software](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Sospendere l'immissione del PIN di BitLocker soltanto per i dispositivi considerati attendibili e con accesso limitato  

Configurare l'impostazione del client **Sospendere immissione PIN di BitLocker al riavvio** su **Sempre** soltanto per i computer considerati attendibili e con accesso fisico limitato.

Quando si configura questa impostazione su **Sempre**, Configuration Manager è in grado di completare l'installazione del software. In questo modo viene garantita l'installazione di aggiornamenti software critici e il ripristino dei servizi. Se, tuttavia, un utente malintenzionato intercetta il processo di riavvio, potrebbe assumere il controllo del computer. Usare questa impostazione solo se il computer è considerato attendibile e il relativo accesso fisico è limitato. Ad esempio, questa impostazione potrebbe essere appropriata per i server in un data center.  

Per altre informazioni su questa impostazione client, vedere [Informazioni sulle impostazioni client](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>Non configurare l'impostazione Criteri di esecuzione di PowerShell su Ignora

Se si configura l'impostazione client di Configuration Manager **Criteri di esecuzione PowerShell** su **Ignora**, Windows consente l'esecuzione di script PowerShell non firmati, permettendo potenzialmente l'esecuzione di malware sui computer client. Se è necessario selezionare questa opzione, usare un'impostazione client personalizzata e assegnarla esclusivamente ai computer client che devono eseguire script PowerShell non firmati.  

Per altre informazioni su questa impostazione client, vedere [Informazioni sulle impostazioni client](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a> Procedure di sicurezza consigliate per i dispositivi mobili  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Installare il punto proxy di registrazione in una rete perimetrale e il punto di registrazione nella intranet  

Per i dispositivi mobili registrati con Configuration Manager e basati su Internet, installare il punto proxy di registrazione in una rete perimetrale e il punto di registrazione nella intranet. Questa separazione dei ruoli contribuisce a proteggere il punto di registrazione da attacchi esterni. Se il punto di registrazione viene compromesso, un utente malintenzionato potrebbe ottenere i certificati per l'autenticazione e impadronirsi delle credenziali degli utenti che registrano il proprio dispositivo mobile.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Configurare le impostazioni della password per proteggere i dispositivi mobili da accessi non autorizzati  

*Per i dispositivi mobili registrati da Configuration Manager*: usare un elemento di configurazione del dispositivo mobile per configurare la complessità delle password come PIN. Specificare almeno la lunghezza minima predefinita della password.  

*Per i dispositivi mobili su cui non è installato il client di Configuration Manager ma che sono gestiti dal connettore Exchange Server*: configurare le **Impostazioni password** per il connettore Exchange Server in modo che la complessità della password sia il PIN. Specificare almeno la lunghezza minima predefinita della password.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Consentire solo l'esecuzione di applicazioni firmate da aziende considerate attendibili  

Prevenire eventuali manomissioni delle informazioni di inventario e delle informazioni sullo stato abilitando solo l'esecuzione delle applicazioni firmate da aziende ritenute attendibili. Impedire ai dispositivi di installare file non firmati.  

*Per i dispositivi mobili registrati da Configuration Manager*: usare un elemento di configurazione del dispositivo mobile per configurare l'impostazione di protezione **Applicazioni non firmate** su **Non consentito**. Configurare l'impostazione **Installazione file non firmati** come un'origine attendibile.  

*Per i dispositivi mobili su cui non è installato il client di Configuration Manager ma che sono gestiti dal connettore Exchange Server*: configurare **Impostazioni applicazione** per il connettore Exchange Server in modo tale che **Installazione file non firmati** e **Applicazioni non firmate** siano impostate su **Non consentito**.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Bloccare i dispositivi mobili quando non sono in uso  

Evitare attacchi tramite elevazione dei privilegi bloccando il dispositivo mobile quando non è in uso.

*Per i dispositivi mobili registrati da Configuration Manager*: usare un elemento di configurazione del dispositivo mobile per configurare l'impostazione della password **Tempo di inattività in minuti prima del blocco del dispositivo mobile**.  

*Per i dispositivi mobili su cui non è installato il client di Configuration Manager ma che sono gestiti dal connettore Exchange Server*: Configurare le **Impostazioni password** per il connettore Exchange Server per impostare **Tempo di inattività in minuti prima del blocco del dispositivo mobile**.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Limitare gli utenti che possono registrare i dispositivi mobili  

Evitare l'elevazione dei privilegi limitando gli utenti autorizzati a registrare i propri dispositivi mobili. Usare un'impostazione client personalizzata anziché le impostazioni predefinite per consentire solo a utenti autorizzati di registrare i propri dispositivi mobili.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Indicazioni sull'affinità utente-dispositivo per dispositivi mobili  

Non distribuire applicazioni agli utenti che dispongono di dispositivi mobili registrati da Configuration Manager o Windows Intune negli scenari seguenti:  

- Il dispositivo mobile viene usato da più persone.  

- Il dispositivo viene registrato da un amministratore per conto di un utente.  

- Il dispositivo viene trasferito a un'altra persona senza ritiro e successiva nuova registrazione del dispositivo.  

La registrazione del dispositivo crea una relazione di affinità utente-dispositivo che consente di associare l'utente che esegue la registrazione al dispositivo mobile. Se il dispositivo mobile è usato da un altro utente, sarà possibile eseguire le applicazioni distribuite all'utente originale, determinando potenzialmente un'elevazione dei privilegi. Allo stesso modo, se un amministratore registra il dispositivo mobile per un utente, le applicazioni distribuite all'utente non saranno installate sul dispositivo, mentre potrebbero invece essere installate le applicazioni distribuite all'amministratore.  

A differenza dell'affinità utente-dispositivo per computer Windows, non è possibile definire manualmente le informazioni relative a tale affinità per i dispositivi mobili registrati da Microsoft Intune.  

Se si trasferisce la titolarità di un dispositivo mobile registrato da Intune, ritirare il dispositivo mobile da Intune per rimuovere l'affinità utente-dispositivo, quindi chiedere all'utente corrente di registrare nuovamente il dispositivo.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Verificare che gli utenti registrino i propri dispositivi mobili per Windows Intune  

La relazione di affinità utente-dispositivo viene creata durante la registrazione e consente di associare l'utente che esegue la registrazione al dispositivo mobile. Se un amministratore registra il dispositivo mobile per un utente, le applicazioni distribuite all'utente non saranno installate sul dispositivo, mentre potrebbero invece essere installate le applicazioni distribuite all'amministratore.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Proteggere la connessione tra il server del sito di Configuration Manager e il server di Exchange

Usare IPsec se Exchange Server è installato in locale. Exchange ospitato protegge automaticamente la connessione tramite SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Usare il principio dei privilegi minimi per il connettore  

Per un elenco dei cmdlet minimi richiesti dal connettore Exchange Server, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a> Procedure di sicurezza consigliate per i Mac  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Archiviare e accedere ai file di origine del client da un percorso protetto  

Configuration Manager non verifica se i file di origine client sono stati manomessi prima dell'installazione o della registrazione del client nel computer Mac. Scaricare questi file da una fonte attendibile, archiviarli e accedervi in modo sicuro.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Monitorare e tenere traccia del periodo di validità del certificato  

Per garantire la continuità aziendale, monitorare e tenere traccia del periodo di validità dei certificati usati per i computer Mac. Configuration Manager non supporta il rinnovo automatico del certificato né avvisa della scadenza prossima. In genere, il periodo di validità è 1 anno.  

Per informazioni su come rinnovare il certificato, vedere [Rinnovo del certificato del client Mac](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configurare il certificato radice trusted in modo che sia attendibile solo per il protocollo SSL  

Per facilitare la protezione contro il rischio di elevazione dei privilegi, configurare il certificato radice trusted in modo che sia attendibile per il solo protocollo SSL.

Quando si registrano i computer Mac, viene installato automaticamente un certificato utente per gestire il client di Configuration Manager, che include il certificato radice trusted nella relativa catena di certificati. Per limitare l'attendibilità del certificato radice al solo protocollo SSL, seguire questa procedura:  

1. Nei computer Mac, aprire una finestra terminale.  

2. Immettere il comando seguente: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. Nella finestra di dialogo **Accesso Portachiavi** nella sezione **Portachiavi** fare clic su **Sistema**. Nella sezione **Categoria** fare quindi clic su **Certificati**.  

4. Individuare e fare doppio clic sul certificato CA radice per il certificato del client Mac.  

5. Nella finestra di dialogo per il certificato CA radice espandere la sezione **Attendibilità** ed eseguire le modifiche seguenti:  

    1. **When using this certificate** (Quando si usa questo certificato): modificare l'impostazione predefinita **Always Trust** (Considera sempre attendibile) in **Use System Defaults** (Usa valori predefiniti di sistema).  

    2. **Secure Sockets Layer (SSL)** : modificare **no value specified** (Nessun valore specificato) in **Always Trust** (Considera sempre attendibile).  

6. Chiudere la finestra di dialogo. Quando richiesto, immettere la password dell'amministratore e quindi fare clic su **Aggiorna impostazioni**.  

Dopo aver completato questa procedura, il certificato radice sarà attendibile solo per convalidare il protocollo SSL e non per altri protocolli diversi da SSL, come Protezioni messaggi (S/MIME), Extensible Authentication (EAP) o firma codice.  

> [!NOTE]  
> È anche possibile usare questa procedura se è stato installato il certificato client indipendentemente da Configuration Manager.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemi di protezione per i client di Configuration Manager  

Non è possibile ovviare ai seguenti problemi di protezione:  

### <a name="status-messages-arent-authenticated"></a>I messaggi di stato non sono autenticati

L'autenticazione non viene eseguita sui messaggi di stato. Quando un punto di gestione accetta connessioni client HTTP, tutti i dispositivi possono inviare messaggi di stato al punto di gestione. Se il punto di gestione accetta solo connessioni client HTTPS, un dispositivo deve ottenere un certificato di autenticazione client valido, ma può anche inviare qualsiasi messaggio di stato. Un eventuale messaggio di stato non valido inviato da un client viene rimosso dal punto di gestione.  

Esistono alcuni potenziali attacchi contro questa vulnerabilità.

- Un utente malintenzionato potrebbe inviare un messaggio di stato falso per ottenere l'appartenenza a una raccolta basata su query messaggi di stato.
- Qualsiasi client può lanciare un attacco di tipo Denial of Service contro il punto di gestione, sovraccaricandolo con messaggi di stato.
- Se i messaggi di stato attivano azioni nelle regole di filtro del messaggio di stato, un utente malintenzionato potrebbe attivare una regola.
- Potrebbe inviare un messaggio di stato che renderebbe inaccurate le informazioni relative ai rapporti.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>I criteri possono essere reindirizzati ai client non di destinazione  

Gli autori di un attacco potrebbero usare diversi metodi per applicare un criterio assegnato a un client a un altro client completamente differente. Ad esempio, un utente malintenzionato su un client attendibile potrebbe inviare informazioni di individuazione o di inventario false per aggiungere il computer a una raccolta alla quale non dovrebbe appartenere. Il client riceverebbe successivamente tutte le distribuzioni in quella raccolta.

Sono previsti controlli per impedire la modifica diretta di un criterio, ma gli autori di attacchi potrebbero usare un criterio esistente per riformattare e ridistribuire un sistema operativo e inviarlo a un computer diverso, creando un attacco Denial of Service. Questi tipi di attacchi richiederebbero tempistiche precise e una profonda conoscenza dell'infrastruttura di Configuration Manager.  

### <a name="client-logs-allow-user-access"></a>I registri del client consentono l'accesso utente  

Tutti i file di log del client consentono al gruppo **Utenti** l'accesso in *Lettura* e agli utenti **interattivi** l'accesso in *Scrittura*. Se si abilita la registrazione dettagliata, gli autori di un attacco potrebbero leggere i file di log per cercare informazioni sulle vulnerabilità del sistema o sulla conformità. I processi eseguiti in un contesto utente, come l'installazione software, devono essere in grado di scrivere nei file di log con un account utente con diritti limitati. Ciò significa che un utente malintenzionato potrebbe anche scrivere nei registri con un account con diritti limitati.  

Il rischio maggiore è che l'autore dell'attacco possa rimuovere dai file di log informazioni potenzialmente utili per il controllo e il rilevamento di intrusi da parte dell'amministratore.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>È possibile usare un computer per ottenere un certificato progettato per la registrazione di dispositivi mobili  

Quando Configuration Manager elabora una richiesta di registrazione, non è in grado di verificare se la richiesta proviene da un dispositivo mobile anziché da un computer. Se la richiesta proviene da un computer, sarà possibile installare un certificato PKI che consentirà la successiva registrazione in Configuration Manager.

Per evitare un attacco tramite elevazione dei privilegi in questo scenario, consentire solo a utenti attendibili di registrare il proprio dispositivo mobile. Monitorare attentamente le attività di registrazione dei dispositivi mobili nel sito.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Un client bloccato è in grado di inviare messaggi al punto di gestione

Quando si blocca un client non ritenuto più attendibile e il client ha stabilito una connessione di rete per la notifica client, Configuration Manager non disconnette la sessione. Il client bloccato può continuare a inviare pacchetti al suo punto di gestione finché non si disconnette dalla rete. Si tratta solo di piccoli pacchetti keep-alive. Il client non può essere gestito da Configuration Manager finché è bloccato.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>L'aggiornamento automatico del client non verifica il punto di gestione

Quando si usa l'aggiornamento automatico del client, quest'ultimo può essere indirizzato a un punto di gestione per il download dei file di origine client. In questo scenario, il punto di gestione non viene verificato come un'origine attendibile.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>La prima volta che eseguono la registrazione di computer Mac, gli utenti sono esposti al rischio di attacchi di spoofing DNS  

Quando i computer Mac si connettono al punto proxy di registrazione durante la registrazione, probabilmente il computer Mac non disporrà del certificato CA radice attendibile. A questo punto, il Mac non considera attendibile il server e chiede all'utente di continuare. Se il nome di dominio completo del punto proxy di registrazione viene risolto da un server DNS non autorizzato, potrebbe indirizzare il computer Mac a un punto proxy di registrazione non autorizzato e installare i certificati da un'origine non attendibile. Per ridurre questo rischio, seguire le procedure consigliate per evitare gli attacchi di spoofing DNS nel proprio ambiente.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>La registrazione Mac non limita le richieste di certificati  

Gli utenti possono registrare di nuovo i computer Mac, ogni volta che richiedono un nuovo certificato client. Configuration Manager non verifica più richieste o non limita il numero di certificati richiesti da un singolo computer. Un utente non autorizzato potrebbe eseguire uno script che ripete la richiesta di registrazione della riga di comando causando un attacco Denial of Service alla rete o all'autorità di emissione del certificato. Per ridurre questo rischio, è necessario monitorare questo tipo di comportamenti sospetti nella CA emittente. Un computer che mostra questo tipo di comportamento deve essere immediatamente bloccato dalla gerarchia di Configuration Manager.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Una conferma di cancellazione non verifica che il dispositivo sia stato effettivamente cancellato  

Quando si avvia un'azione di cancellazione per un dispositivo mobile e Configuration Manager conferma la cancellazione, il sistema verifica che Configuration Manager abbia *inviato* il messaggio e non che il dispositivo *abbia completato* la richiesta.

Per i dispositivi mobili gestiti dal connettore Exchange Server, una conferma di cancellazione verifica che il comando sia stato ricevuto da Exchange, non dal dispositivo.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Se si usano le opzioni di conferma delle modifiche in dispositivi con Windows Embedded, gli account potrebbero essere bloccati prima del previsto  

Se il dispositivo con Windows Embedded esegue una versione del sistema operativo precedente a Windows 7 e un utente prova ad accedere mentre i filtri di scrittura sono disabilitati da Configuration Manager, il numero di tentativi di accesso errati consentiti prima del blocco dell'account viene dimezzato.

Se, ad esempio, il Criteri dominio per la **soglia di blocchi dell'account** è configurato su sei tentativi e l'utente sbaglia la password per tre volte, l'account viene bloccato, creando effettivamente una situazione di tipo Denial of Service. In questo scenario, se gli utenti devono accedere a dispositivi incorporati, è necessario allertarli circa la potenziale riduzione del valore di soglia di blocco.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a> Informazioni sulla privacy per i client di Configuration Manager  

Quando si distribuisce il client di Configuration Manager, vengono abilitate le impostazioni client che consentono di usare le funzionalità di Configuration Manager. Le impostazioni usate per la configurazione delle funzionalità possono essere applicate a tutti i client nella gerarchia di Configuration Manager, indipendentemente dal fatto che siano connessi direttamente alla rete aziendale, connessi tramite sessione remota o connessi a Internet.  

Le informazioni sui client vengono archiviate nel database di Configuration Manager nel server SQL e non vengono inviate a Microsoft. Vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina dati di individuazione obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione. 

Alcune informazioni di diagnostica e dati di utilizzo riepilogativi o aggregati vengono inviati a Microsoft. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Prima di configurare il client di Configuration Manager, esaminare i requisiti sulla privacy.  

Nell'[Informativa sulla privacy Microsoft](https://privacy.microsoft.com/privacystatement) sono disponibili altre informazioni sulla raccolta e sull'uso di dati Microsoft.

### <a name="client-status"></a>Stato del client  

Configuration Manager monitora l'attività dei client. Periodicamente valuta e corregge le eventuali problematiche di Configuration Manager e le relative dipendenze. Lo stato del client è attivato per impostazione predefinita. Usa una metrica lato server per i controlli dell'attività client e azioni lato client per i controlli automatici, la correzione e l'invio di informazioni sullo stato del client al sito. Il client esegue i controlli automatici secondo una pianificazione configurabile. Il client invia i risultati dei controlli al sito di Configuration Manager. Queste informazioni vengono crittografate durante il trasferimento.  

Le informazioni sui client vengono archiviate nel database di Configuration Manager nel server SQL e non vengono inviate a Microsoft. Le informazioni non vengono memorizzate in forma crittografata nel database del sito. Vengono conservate nel database fino alla relativa eliminazione, che avviene come specificato dal valore dell'impostazione di stato del client **Mantieni la cronologia stato del client per il numero di giorni seguente**. Il valore predefinito di tale impostazione è ogni 31 giorni.  

Prima di installare il client di Configuration Manager con il controllo dello stato del client, valutare i requisiti relativi alla privacy.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a> Informazioni sulla privacy per i dispositivi mobili gestiti con il connettore Exchange Server  

Il connettore Exchange Server rileva e gestisce i dispositivi che si connettono a Exchange Server (locale o ospitato) usando il protocollo ActiveSync. I record rilevati dal connettore Exchange Server vengono memorizzati nel database di Configuration Manager nel server SQL dell'utente. Le informazioni vengono raccolte da Exchange Server. Tali informazioni non includono informazioni aggiuntive su quanto i dispositivi mobili inviano a Exchange Server.  

Le informazioni sul dispositivo mobile non vengono inviate a Microsoft. Sono archiviate nel database di Configuration Manager nel server SQL dell'utente, dove vengono conservate fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina dati di individuazione obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione.  

Prima di installare e configurare il connettore Exchange Server, valutare i requisiti relativi alla privacy.  

Nell'[Informativa sulla privacy Microsoft](https://privacy.microsoft.com/privacystatement) sono disponibili altre informazioni sulla raccolta e sull'uso di dati Microsoft.
