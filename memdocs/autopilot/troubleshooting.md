---
title: Risoluzione dei problemi di Windows Autopilot
description: Informazioni su come gestire i problemi man mano che si verificano durante il processo di distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: c89731edddd94da99e114cf98c10547c096ebb53
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252014"
---
# <a name="troubleshooting-windows-autopilot"></a>Risoluzione dei problemi di Windows Autopilot

**Si applica a: Windows 10**

Windows Autopilot è progettato per semplificare tutte le parti del ciclo di vita dei dispositivi Windows, ma è sempre possibile che si verifichino problemi. Esaminare le informazioni seguenti per assistenza per la risoluzione dei problemi.

## <a name="troubleshooting-process"></a>Processo di risoluzione dei problemi

Che si tratti di eseguire distribuzioni di dispositivi basati su utenti o autodeploying, il processo di risoluzione dei problemi è lo stesso. È utile per comprendere il flusso di un dispositivo specifico:

1. Viene stabilita una connessione di rete. La connessione può essere una connessione wireless (Wi-Fi) o cablata (Ethernet).
2. Il profilo di Windows Autopilot è stato scaricato. Quando si usa una connessione cablata o si stabilisce manualmente una connessione wireless, il profilo Scarica dal servizio di distribuzione Autopilot non appena viene stabilita la connessione di rete.
3. Si verifica l'autenticazione utente. Quando si esegue una distribuzione guidata dall'utente, l'utente immette le credenziali Azure Active Directory, che verranno convalidate.
4. Si verifica Azure Active Directory join. Per le distribuzioni basate sull'utente, il dispositivo verrà aggiunto al Azure AD usando le credenziali utente specificate. Per gli scenari di distribuzione automatica, il dispositivo verrà aggiunto senza specificare le credenziali utente.
5. Si verifica la registrazione automatica di MDM. Nell'ambito del processo di Azure AD join, il dispositivo si registrerà nel servizio MDM configurato in Azure AD (ad esempio, Microsoft Intune).
6. Vengono applicate le impostazioni. Se la [pagina relativa allo stato della registrazione](enrollment-status.md) è configurata, la maggior parte delle impostazioni verrà applicata mentre viene visualizzata la pagina relativa allo stato della registrazione. Se non è configurato o disponibile, le impostazioni verranno applicate dopo l'accesso dell'utente.

Per la risoluzione dei problemi, le attività principali da eseguire sono:

- Configurazione: ha Azure Active Directory e Microsoft Intune (o un servizio MDM equivalente) è stato configurato come specificato nei [requisiti di configurazione di Windows Autopilot](configuration-requirements.md)?
- Connettività di rete: il dispositivo può accedere ai servizi descritti nei [requisiti di rete di Windows Autopilot](networking-requirements.md)?
- Comportamento predefinito della configurazione guidata automatico: erano visualizzate solo le schermate di esperienza predefinite previste? La pagina delle credenziali Azure AD è stata personalizzata con i dettagli specifici dell'organizzazione, come previsto?
- Problemi di Azure AD join: il dispositivo è in grado di partecipare Azure Active Directory?
- Problemi di registrazione di MDM: è stato possibile registrare il dispositivo in Microsoft Intune (o un servizio MDM equivalente)?

## <a name="troubleshooting-autopilot-device-import"></a>Risoluzione dei problemi relativi all'importazione di dispositivi Autopilot

### <a name="clicking-import-after-selecting-csv-does-nothing-400-error-appears-in-network-trace-with-error-body-cannot-convert-the-literal-devicehash-to-the-expected-type-edmbinary"></a>Se si fa clic su Importa dopo aver selezionato CSV, non viene visualizzato alcun errore ' 400' nella traccia di rete con corpo errore **"Impossibile convertire il valore letterale ' [DEVICEHASH]' nel tipo previsto ' EDM. Binary '"**

Questo errore indica che l'hash del dispositivo non è formattato correttamente. Questo errore può essere causato da qualsiasi elemento che danneggia l'hash raccolto. Una possibilità è che l'hash stesso (anche se valido) non venga decodificato.

L'hash del dispositivo è Base64. A livello di dispositivo, viene codificato come base64 non riempita, ma Autopilot prevede l'aggiunta di Base64. In genere, il payload non richiede la spaziatura interna e il processo funziona. In alcuni casi, tuttavia, il payload non è allineato in modo corretto e la spaziatura interna è necessaria. In questo caso, si ottiene l'errore visualizzato in precedenza. Il decodificatore Base64 di PowerShell prevede anche la codifica Base64, quindi è possibile usare questo decodificatore per verificare che l'hash venga riempito correttamente.

I caratteri "A" alla fine dell'hash sono in effetti dati vuoti. Ogni carattere in Base64 è a 6 bit, un valore in Base64 è 6 bit uguale a 0. L'eliminazione o l'aggiunta di **un oggetto**alla fine non comporta la modifica dei dati di payload effettivi.

Per risolvere questo problema, è necessario modificare l'hash, quindi testare il nuovo valore fino a quando PowerShell non riesce a decodificare l'hash. Il risultato è prevalentemente illeggibile. Stiamo semplicemente cercando di non generare l'errore "lunghezza non valida per una stringa o una matrice di caratteri base-64". 

Per testare la codifica Base64, è possibile usare il comando PowerShell seguente:
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

Quindi, ad esempio (non si tratta di un hash del dispositivo, ma è non allineato a Base64, quindi è adatto per il test):
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

Ora per le regole di riempimento. Il carattere di riempimento è "=". Il carattere di riempimento può essere solo alla fine dell'hash e può essere costituito solo da un massimo di due caratteri di riempimento. Ecco la logica di base.

- La decodifica dell'hash ha esito negativo?
 - Sì: sono gli ultimi due caratteri "="?
   - Sì: sostituire sia "=" con un singolo carattere "A", quindi riprovare
   - No: aggiungere un altro carattere "=" alla fine, quindi riprovare
 - No: hash valido

Eseguendo il loop della logica precedente nell'hash di esempio precedente, si ottengono le permutazioni seguenti:
- Q29udG9zbwAAA
- Q29udG9zbwAAA =
- Q29udG9zbwAAA = =
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA =
- **Q29udG9zbwAAAA = =** (questo ha un riempimento valido)

Sostituire l'hash raccolto con questo nuovo hash imbottito, quindi provare a eseguire di nuovo l'importazione.

## <a name="troubleshooting-autopilot-oobe-issues"></a>Risoluzione dei problemi relativi alla configurazione guidata di Autopilot

Quando la configurazione guidata include un comportamento imprevisto di Autopilot, è utile controllare se il dispositivo ha ricevuto un profilo di Autopilot. In tal caso, controllare le impostazioni contenute nel profilo. A seconda della versione di Windows 10, sono disponibili diversi meccanismi a tale scopo.

### <a name="windows-10-version-1803-and-above"></a>Windows 10 versione 1803 e successive

Windows 10 versione 1803 e successive aggiunge voci del registro eventi. È possibile usare le voci og per visualizzare i dettagli relativi alle impostazioni del profilo di Autopilot e al flusso della configurazione guidata. Queste voci possono essere visualizzate usando Visualizzatore eventi. Esaminare le informazioni in **registri applicazioni e servizi-> Microsoft-> Windows-> provisioning-Diagnostics-provider-> Autopilot** per le versioni precedenti alla 1903. Per la versione 1903 e successive, vedere **registri applicazioni e servizi-> Microsoft-> Windows-> ModernDeployment-Diagnostics-provider-> Autopilot**. È possibile registrare gli eventi seguenti, a seconda dello scenario e della configurazione del profilo:

| ID evento | Type | Descrizione |
|----------|------|-------------| 
| 100 | Avviso | "Criterio Autopilot [nome] non trovato". Questo errore è in genere un problema temporaneo, mentre il dispositivo è in attesa del download di un profilo di Autopilot. |
| 101 | Info | "AutopilotGetPolicyDwordByName succeeded: Nome criterio = [nome impostazione]; valore criterio = [valore]. " Questo messaggio Mostra il recupero e l'elaborazione delle impostazioni OOBE numeriche di Autopilot. |
| 103 | Info | "AutopilotGetPolicyStringByName succeeded: nome del criterio = [nome]; valore = [valore]. " Questo messaggio Mostra il recupero e l'elaborazione di stringhe di impostazioni OOBE come il nome del tenant Azure AD. |
| 109 | Info | "AutopilotGetOobeSettingsOverride succeeded: impostazione OOBE [nome impostazione]; stato = [stato]. " Questo messaggio Mostra le impostazioni della configurazione guidata per il recupero e l'elaborazione di Autopilot. |
| 111 | Info | "AutopilotRetrieveSettings riuscito". Questo messaggio indica che le impostazioni archiviate nel profilo di Autopilot che controllano il comportamento della configurazione guidata sono state recuperate correttamente. |
| 153 | Info | "AutopilotManager ha segnalato che lo stato è stato modificato da [stato originale] a [nuovo stato]". In genere, questo messaggio deve indicare "ProfileState_Unknown" a "ProfileState_Available". Questo caso indica che un profilo è stato disponibile e scaricato per il dispositivo. Il dispositivo è quindi pronto per la distribuzione tramite Autopilot. |
| 160 | Info | "AutopilotRetrieveSettings inizio acquisizione". Questo messaggio indica che Autopilot è pronto per il download delle impostazioni del profilo di Autopilot necessarie. |
| 161 | Info | "AutopilotManager recupero delle impostazioni è riuscito." Il profilo di Autopilot è stato scaricato. |
| 163 | Info | "Il download determinato da AutopilotManager non è necessario e il dispositivo è già stato sottoposto a provisioning. Pulire o ripristinare il dispositivo per modificare questo ". Questo messaggio indica che un profilo di Autopilot è residente nel dispositivo. in genere verrà rimosso solo dal processo **/generalize di Sysprep** . |
| 164 | Info | "AutopilotManager determinato Internet è disponibile per il tentativo di download dei criteri". |
| 171 | Errore | "AutopilotManager non è riuscito a impostare l'identità TPM confermata. HRESULT = [codice errore]. " Questo messaggio indica un problema che esegue l'attestazione TPM, necessario per completare il processo di modalità di distribuzione automatica. | 
| 172 | Errore | "AutopilotManager non è riuscito a impostare il profilo di Autopilot come disponibile. HRESULT = [codice errore]. " Questo errore è in genere correlato all'ID evento 171. |

Oltre alle voci del registro eventi, il registro di sistema e le opzioni di traccia ETW seguenti funzionano con Windows 10 versione 1803 e successive.

### <a name="windows-10-version-1709-and-above"></a>Windows 10 versione 1709 e successive

Le impostazioni del profilo di Autopilot ricevute dal servizio di distribuzione Autopilot vengono archiviate nel registro di sistema del dispositivo. Queste informazioni sono reperibili in **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**. Le voci del registro di sistema disponibili includono:

| Valore | Descrizione |
|-------|-------------|
| AadTenantId | GUID del tenant Azure AD cui l'utente ha effettuato l'accesso. L'utente riceve un errore se questa voce non corrisponde al tenant usato per registrare il dispositivo. |
| CloudAssignedTenantDomain | Il tenant Azure AD il dispositivo è stato registrato con, ad esempio, "contosomn.onmicrosoft.com". Se il dispositivo non è registrato con Autopilot, questo valore sarà vuoto. |
| CloudAssignedTenantId | GUID del tenant di Azure AD con cui è registrato il dispositivo. Il GUID corrisponde al dominio del tenant dal valore del registro di sistema CloudAssignedTenantDomain. Se il dispositivo non è registrato con Autopilot, questo valore sarà vuoto.|
| IsAutopilotDisabled | Se impostato su 1, questo valore del registro di sistema indica che il dispositivo non è registrato con Autopilot. Questo stato può anche indicare che non è stato possibile scaricare il profilo di Autopilot a causa di problemi di connettività di rete o di firewall o di timeout della rete. |
| TenantMatched | Questa voce è impostata su 1 se l'ID tenant dell'utente corrisponde all'ID tenant con cui è stato registrato il dispositivo. Se il valore del registro di sistema è 0, all'utente viene visualizzato un errore e viene forzata la riparte. |
| CloudAssignedOobeConfig | Bitmap che mostra quali impostazioni di Autopilot sono state configurate. I valori includono: SkipCortanaOptIn = 1, OobeUserNotLocalAdmin = 2, SkipExpressSettings = 4, SkipOemRegistration = 8, SkipEula = 16 |

### <a name="windows-10-semi-annual-channel-supported-versions"></a>Versioni supportate del canale semestrale di Windows 10

Nei dispositivi che eseguono una [versione supportata](https://docs.microsoft.com/windows/release-information/) del canale semestrale di Windows 10, è possibile usare la traccia ETW per ottenere informazioni dettagliate da Autopilot e dai componenti correlati. È possibile visualizzare i file di traccia ETW utilizzando Windows Performance Analyzer o strumenti simili. Per ulteriori informazioni, vedere [il Blog sulla risoluzione dei problemi avanzata](https://blogs.technet.microsoft.com/mniehaus/2017/12/13/troubleshooting-windows-autopilot-level-300400/).

## <a name="troubleshooting-azure-ad-join-issues"></a>Risoluzione dei problemi di Azure AD join

Il problema più comune per l'aggiunta di un dispositivo a Azure AD è relativo alle autorizzazioni di Azure AD. Assicurarsi che [sia attiva la configurazione corretta](configuration-requirements.md) per consentire agli utenti di aggiungere dispositivi ai Azure ad. È possibile che si verifichino errori anche se l'utente supera il numero di dispositivi a cui è consentito partecipare. Questo limite è configurato in Azure AD.

Un dispositivo Azure AD viene creato al momento dell'importazione. È importante che l'oggetto non venga eliminato. L'oggetto funge da ancoraggio di Autopilot in Azure AD per l'appartenenza al gruppo e la destinazione (incluso il profilo). L'eliminazione può causare errori di join. Se questo oggetto viene eliminato, è possibile risolvere il problema eliminando e reimportando questo hash di Autopilot, in modo che sia possibile ricreare l'oggetto associato.

Il codice di errore 801C0003 viene in genere segnalato in una pagina di errore intitolata "si è verificato un problema". Questo errore indica che il join Azure AD non è riuscito.

## <a name="troubleshooting-intune-enrollment-issues"></a>Risoluzione dei problemi di registrazione di Intune

Vedere [questo articolo della Knowledge base](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) per assistenza per i problemi di registrazione di Intune. I problemi comuni possono includere "
- licenze non corrette o mancanti assegnate all'utente.
- troppi dispositivi registrati per l'utente.

Il codice di errore 80180018 viene in genere segnalato in una pagina di errore intitolata "si è verificato un problema". Questo errore indica che la registrazione MDM non è riuscita.

Se la reimpostazione di Autopilot non riesce immediatamente con l'errore si è verificata una **difficoltà. Accedere con un account amministratore per vedere perché e reimpostare manualmente**. per ulteriori informazioni, vedere [risolvere i problemi di reimpostazione di Autopilot](https://docs.microsoft.com/education/windows/autopilot-reset#troubleshoot-autopilot-reset) .

## <a name="profile-download"></a>Download del profilo

Quando si avvia un dispositivo Windows 10 connesso a Internet, si tenterà di connettersi al servizio Autopilot e di scaricare un profilo di Autopilot. Nota: è importante che in questa fase sia presente un profilo, in modo che un profilo vuoto non venga memorizzato nella cache localmente nel computer. Per rimuovere il profilo locale attualmente memorizzato nella cache in Windows 10 versione 1803 e precedenti, è necessario rigeneralizzare il sistema operativo con **sysprep/generalize/oobe**, reinstallare il sistema operativo o ricreare l'immagine del PC. In Windows 10 versione 1809 e successive è possibile recuperare un nuovo profilo riavviando il computer.

Quando un profilo viene scaricato dipende dalla versione di Windows 10 in esecuzione nel PC. Vedere la tabella seguente.

| Versione di Windows 10 | Comportamento di download del profilo |
| --- | --- |
| 1709 | Il profilo viene scaricato dopo la pagina di connessione alla rete OOBE. Questa pagina non viene visualizzata quando si usa una connessione cablata. In questo caso, il profilo viene scaricato prima della schermata EULA. |
| 1803 | Il profilo viene scaricato il prima possibile. Se cablato, viene scaricato all'avvio della configurazione guidata. Se è wireless, viene scaricato dopo la pagina connessione di rete. |
| 1809 | Il profilo viene scaricato il prima possibile (uguale a 1803) e di nuovo dopo ogni riavvio. |

Se è necessario riavviare un computer durante la configurazione guidata:
- Premere MAIUSC + F10 per aprire un prompt dei comandi.
- Immettere **Shutdown/r/t 0** per riavviare immediatamente oppure arrestare **/s/t 0** per arrestarlo immediatamente.

Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

## <a name="related-topics"></a>Argomenti correlati

[Windows Autopilot-problemi noti](known-issues.md)<br>
[Diagnosticare gli errori MDM in Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
