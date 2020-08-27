---
title: Sostituzione della scheda madre di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Scenari MBR per la distribuzione di Windows Autopilot
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
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
ms.openlocfilehash: 4ae8ffdf39b7812a869d3a7ef5b5289f46f8369a
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908356"
---
# <a name="windows-autopilot-motherboard-replacement-scenario-guidance"></a>Guida allo scenario di sostituzione della scheda madre di Windows Autopilot

**Si applica a**

- Windows 10

In questo documento vengono fornite indicazioni sugli scenari di ripristino dei dispositivi di Windows Autopilot che i partner Microsoft possono utilizzare in situazioni di sostituzione della scheda madre (MBR) e altri scenari di manutenzione.

Il ripristino dei dispositivi registrati con Autopilot è complesso perché tenta di bilanciare i requisiti OEM con i requisiti di Windows Autopilot.  In particolare, l'OEM richiede una rigida univocità tra le schede madri, gli indirizzi MAC e così via, mentre Windows Autopilot richiede una rigida univocità a livello di ID hardware per ogni dispositivo per consentire la registrazione corretta.  L'ID hardware non sempre soddisfa tutti i requisiti per i componenti hardware OEM, quindi questi requisiti sono talvolta a rischio, causando problemi con alcuni scenari di ripristino.

**Sostituzione della scheda madre (MBR)**

Se è necessaria una sostituzione della scheda madre in un dispositivo Windows Autopilot, è consigliabile procedere come segue:

1. [Annullare la registrazione del dispositivo](#deregister-the-autopilot-device-from-the-autopilot-program) da Windows Autopilot
2. [Sostituire la scheda madre](#replace-the-motherboard)
3. [Acquisisci un nuovo ID dispositivo (4K HH)](#capture-a-new-autopilot-device-id-4k-hh-from-the-device)
4. [Registrare nuovamente il dispositivo](#reregister-the-repaired-device-using-the-new-device-id) con Windows Autopilot
5. [Reimpostare il dispositivo](#reset-the-device)
6. [Restituisce il dispositivo](#return-the-repaired-device-to-the-customer)

Ogni passaggio è illustrato di seguito.

## <a name="deregister-the-autopilot-device-from-the-autopilot-program"></a>Annullare la registrazione del dispositivo Autopilot dal programma Autopilot

Prima che il dispositivo arrivi alla struttura di ripristino, è necessario annullarne la registrazione da parte dell'entità che lo ha registrato. Solo l'entità che ha registrato il dispositivo può annullarne la registrazione.   Potrebbe trattarsi dell'amministratore IT del cliente, dell'OEM o del partner CSP.  Se l'amministratore IT ha registrato il dispositivo, è probabile che abbia eseguito tale operazione tramite Intune (o forse il Microsoft Store per le aziende).  In tal caso, è necessario annullare la registrazione del dispositivo da Intune (o MSfB).  Questa operazione è necessaria perché i dispositivi registrati in Intune non vengono visualizzati in MPC.  Tuttavia, se il partner OEM o CSP ha registrato il dispositivo, probabilmente lo ha fatto tramite il centro per i partner Microsoft (MPC).  In tal caso, è necessario annullare la registrazione del dispositivo da MPC, che lo rimuoverà anche dall'account Intune dell'amministratore IT del cliente.  Di seguito vengono descritti i passaggi che un amministratore IT passa per annullare la registrazione di un dispositivo da Intune e i passaggi che un OEM o CSP passa per annullare la registrazione di un dispositivo da MPC.

**Nota**: se possibile, un OEM o un CSP dovrebbe registrare i dispositivi Autopilot, anziché fare in modo che il cliente lo esegua.  In questo modo si eviteranno problemi laddove gli OEM o i CSP potrebbero non essere in grado di annullare la registrazione di un dispositivo se, ad esempio, un cliente che rilascia un dispositivo esce dall'azienda prima di annullarne la registrazione.

**Eccezione**: se un cliente concede un'autorizzazione OEM per registrare i dispositivi per loro conto tramite il processo di consenso automatico, un OEM può usare l'API per annullare la registrazione dei dispositivi che non si sono registrati, ma il cliente ha registrato i dispositivi.  Tuttavia, si tenga presente che questa operazione rimuoverà solo i dispositivi dal programma Autopilot, ma non li disconnetterà da Intune o li disconnetterà da AAD.  Il cliente deve eseguire questi passaggi, se necessario, tramite Intune.

### <a name="deregister-from-intune"></a>Annullare la registrazione da Intune

Per annullare la registrazione di un dispositivo Autopilot da Intune, un amministratore IT:

1. Accedere al proprio account di Intune
2. Passare a gruppi di > di Intune > tutti i gruppi
3. Rimuovere il dispositivo desiderato dal relativo gruppo
4. Passare a dispositivi > di Intune > tutti i dispositivi
5. Selezionare la casella di controllo accanto al dispositivo che si desidera eliminare, quindi fare clic sul pulsante Elimina nel menu in alto.
6. Passare a dispositivi > di Intune > dispositivi Azure AD
7. Selezionare la casella di controllo accanto al dispositivo che si desidera eliminare, quindi fare clic sul pulsante Elimina nel menu in alto.
8. Passare alla registrazione del dispositivo > di Intune > registrazione Windows > dispositivi
9. Selezionare la casella di controllo accanto al dispositivo di cui si vuole annullare la registrazione
10. Fare clic sull'icona del menu esteso ("...") all'estremità destra della riga contenente il dispositivo di cui si desidera annullare la registrazione per esporre un menu aggiuntivo con l'opzione "Annulla assegnazione utente".
11. Fare clic su "Annulla assegnazione utente" Se il dispositivo è stato precedentemente assegnato a un utente. in caso contrario, questa opzione sarà disabilitata e potrà essere ignorata
12. Con la periferica non assegnata ancora selezionata, fare clic sul pulsante Elimina lungo il menu in alto per rimuovere il dispositivo

**Nota**: questa procedura annulla la registrazione del dispositivo da Autopilot, ma annulla anche la registrazione del dispositivo da Intune e la disunione dal dispositivo da AAD.  Sebbene sia possibile che si verifichi la necessità di annullare solo la registrazione del dispositivo da Autopilot, esistono alcune barriere in Intune che richiedono la necessità di eseguire tutti i passaggi precedenti. si tratta comunque di una procedura consigliata se il dispositivo viene perso o diventa irreversibile, per eliminare la possibilità di dispositivi orfani esistenti nel database Autopilot, in Intune o in AAD.  Se un dispositivo entra in uno stato irreversibile, è possibile contattare l' [alias del supporto tecnico Microsoft](autopilot-support.md) appropriato per assistenza.

Il processo di annullamento della registrazione importerà circa 15 minuti.  È possibile accelerare il processo facendo clic sul pulsante "Sincronizza" e quindi "Aggiorna" la visualizzazione finché il dispositivo non è più presente.

Altre informazioni sulla deregistrazione dei dispositivi da Intune sono disponibili [qui](/intune/enrollment-autopilot#create-an-autopilot-device-group).

### <a name="deregister-from-mpc"></a>Annullare la registrazione da MPC

Per annullare la registrazione di un dispositivo Autopilot dal centro per i partner Microsoft (MPC), un CSP:

1. Accedi a MPC
2. Passare a Customer > Devices
3. Selezionare il dispositivo di cui annullare la registrazione e fare clic sul pulsante "Elimina dispositivo"

![devices](images/devices.png)

**Nota**: se si annulla la registrazione di un dispositivo da Autopilot in MPC, viene eseguita solo questa operazione. non viene anche annullata la registrazione del dispositivo da MDM (Intune), né viene disgiunto dal dispositivo da AAD.  Pertanto, se possibile, l'OEM/CSP idealmente dovrebbe collaborare con l'amministratore IT del cliente per rimuovere completamente il dispositivo in base ai passaggi di Intune descritti nella sezione precedente.

In alternativa, un partner OEM che ha integrato le API dirette OEM può annullare la registrazione di un dispositivo chiamando l'API AutopilotDeviceRegistration con i campi TenantID e TenantDomain lasciati vuoti nella chiamata di richiesta.  

Poiché la funzionalità di ripristino non avrà accesso alle credenziali di accesso dell'utente, la funzionalità di ripristino dovrà ricreare l'immagine del dispositivo come parte del processo di ripristino.  Questo significa che il cliente deve eseguire tre operazioni prima di inviare il dispositivo per il ripristino:
1. Copiare tutti i dati importanti dal dispositivo.
2. Lasciare che la funzionalità di ripristino conosca la versione di Windows da reinstallare dopo il ripristino.
3. Se applicabile, lasciare che la funzionalità di ripristino conosca la versione di Office da reinstallare dopo il ripristino.

## <a name="replace-the-motherboard"></a>Sostituire la scheda madre

I tecnici sostituiscono la scheda madre (o altro hardware) sul dispositivo rotto.  Viene inserito un DPK di sostituzione.

I processi di ripristino e sostituzione delle chiavi variano tra le strutture.  Talvolta le strutture di ripristino ricevono parti di ricambio della scheda madre dagli OEM che hanno già inserito DPKs di sostituzione, ma a volte non.  Talvolta le strutture di ripristino ricevono strumenti BIOS completamente funzionanti dagli OEM, ma a volte non.  Ciò significa che la qualità dei dati nel BIOS dopo un MBR varia.  Per assicurarsi che il dispositivo riparato sarà ancora in grado di supportare Autopilot dopo la riparazione, il nuovo BIOS (post-riparazione) dovrebbe essere in grado di raccogliere e popolare almeno le informazioni seguenti:

- DiskSerialNumber
- SmbiosSystemSerialNumber
- SmbiosSystemManufacturer
- SmbiosSystemProductName
- SmbiosUuid
- EKPub TPM
- MacAddress
- ProductKeyID
- OSType

**Nota**: per semplicità e poiché i processi variano tra le strutture di ripristino, sono stati esclusi molti dei passaggi aggiuntivi usati spesso in un MBR, ad esempio:
- Verificare che il dispositivo sia ancora funzionante
- Disabilitare BitLocker *
- Ripristinare il dati configurazione di avvio (BCD)
- Ripristinare e verificare l'operazione del driver di rete

* È possibile sospendere BitLocker anziché disabilitarlo se il tecnico è in grado di riprenderlo dopo il ripristino.

## <a name="capture-a-new-autopilot-device-id-4k-hh-from-the-device"></a>Acquisire un nuovo ID dispositivo Autopilot (4K HH) dal dispositivo

I tecnici di riparazione devono accedere al dispositivo riparato per acquisire il nuovo ID dispositivo.  Supponendo che il tecnico di riparazione non abbia accesso alle credenziali di accesso del cliente, dovrà ricreare l'immagine del dispositivo per ottenere l'accesso, in base ai passaggi seguenti:

1. Il tecnico di riparazione crea un' [unità USB di avvio di WinPE](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#create-a-bootable-windows-pe-winpe-partition).
2. Il tecnico di riparazione avvia il dispositivo in WinPE.
3. Il tecnico della riparazione [applica una nuova immagine di Windows al dispositivo](/windows-hardware/manufacture/desktop/work-with-windows-images).

    **Nota**: idealmente, la stessa versione di Windows deve essere ricreata con l'immagine nel dispositivo che era originariamente nel dispositivo, quindi è necessario un coordinamento tra la struttura di ripristino e il cliente per acquisire queste informazioni nel momento in cui il dispositivo arriva per la riparazione.  Questo potrebbe includere il cliente che invia la struttura di ripristino un'immagine personalizzata (file con estensione PPK) tramite una chiavetta USB, ad esempio.
 
4. Il tecnico di riparazione avvia il dispositivo nella nuova immagine di Windows.
5. Una volta sul desktop, il tecnico del ripristino acquisisce il nuovo ID dispositivo (4K HH) dal dispositivo usando lo strumento OA3 o lo script di PowerShell, come descritto di seguito.

Le funzionalità di ripristino con accesso allo strumento OA3 (che fa parte di ADK) possono usare lo strumento per acquisire l'hash hardware 4K (4K HH).

In alternativa, è possibile usare lo [script di PowerShell WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) per acquisire l'HH 4K attenendosi alla procedura seguente:

1. Installare lo script dal [PowerShell Gallery](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) o dalla riga di comando (l'installazione dalla riga di comando è mostrata di seguito).
2. Passare alla directory dello script ed eseguirla nel dispositivo quando il dispositivo è in modalità di controllo o sistema operativo completo. Vedere l'esempio seguente.

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

>Se viene richiesto di installare il pacchetto NuGet, scegliere **Sì**.<br>
>Se, dopo l'installazione dello script viene visualizzato un errore che Get-WindowsAutopilotInfo.ps1 non viene trovato, verificare che C:\Program Files\WindowsPowerShell\Scripts sia presente nella variabile PATH.<br>
>Se il cmdlet Install-script ha esito negativo, verificare di avere il repository di PowerShell predefinito registrato (**Get-PSRepository**) o registrare il repository predefinito con **Register-PSRepository-default-verbose**.

Lo script crea un file con estensione CSV che contiene le informazioni sul dispositivo, incluso il totale di 4K HH.  Salvare il file in modo che sia possibile accedervi in un secondo momento. La funzionalità del servizio userà questo HH 4K per registrare nuovamente il dispositivo come descritto di seguito. Assicurarsi di usare il parametro-OutputFile quando si salva il file, in modo da garantire la correttezza della formattazione del file. Non tentare di inviare manualmente l'output del comando a un file.

**Nota**: se la funzionalità di ripristino non è in grado di eseguire lo strumento OA3 o lo script di PowerShell per acquisire il nuovo formato HH 4K, i partner CSP (o OEM) dovranno eseguire questa operazione.  Senza alcune entità che acquisiscono il nuovo 4K HH, non è possibile registrare nuovamente questo dispositivo come dispositivo Autopilot.


## <a name="reregister-the-repaired-device-using-the-new-device-id"></a>Registrare nuovamente il dispositivo riparato usando il nuovo ID dispositivo

Se un OEM non è in grado di registrare nuovamente il dispositivo, la funzionalità di riparazione o il CSP deve registrare nuovamente il dispositivo usando MPC oppure è consigliabile che l'amministratore IT del cliente possa registrare nuovamente il dispositivo tramite Intune (o MSfB).  Di seguito sono illustrate entrambe le modalità di registrazione di un dispositivo.

### <a name="reregister-from-intune"></a>Eseguire nuovamente la registrazione da Intune

Per registrare nuovamente un dispositivo Autopilot da Intune, un amministratore IT:
1. Accedere a Intune.
2. Passare alla registrazione del dispositivo > registrazione Windows > dispositivi > importa.
3. Fare clic sul pulsante **Import (importa** ) per caricare un file CSV contenente l'ID del dispositivo da registrare nuovamente (l'ID del dispositivo è il valore HH di 4K acquisito dallo script di PowerShell o lo strumento OA3 descritto in precedenza in questo documento).

Il video seguente offre una panoramica di come (re) registrare i dispositivi tramite MSfB.<br>

> [!VIDEO https://www.youtube.com/embed/IpLIZU_j7Z0]

### <a name="reregister-from-mpc"></a>Eseguire nuovamente la registrazione da MPC

Per registrare nuovamente un dispositivo Autopilot da MPC, un OEM o un CSP:

1. Accedere a MPC.
2. Passare alla pagina dispositivi > del cliente e fare clic sul pulsante **Aggiungi dispositivi** per caricare il file CSV.

![device](images/device2.png)<br>
![device](images/device3.png)

Nel caso di registrazione di un dispositivo riparato tramite MPC, il file CSV caricato deve contenere il valore HH di 4K per il dispositivo e non solo PKID o Tuple (SerialNumber + OEMName + ModelName).  Se è stata utilizzata solo la PKID o la tupla, il servizio Autopilot non sarebbe in grado di trovare una corrispondenza nel database Autopilot, perché non sono mai state inviate informazioni HH di 4K per questo dispositivo "nuovo" e il caricamento avrà esito negativo, probabilmente restituendo un errore ZtdDeviceNotFound.  Quindi, anche in questo caso, caricare solo il formato 4K HH, non la tupla o PKID.

**Nota**: quando si include l'HH 4K nel file CSV, non è necessario includere anche il pkID o la tupla.  Tali colonne possono essere lasciate vuote, come illustrato di seguito:

![hash](images/hh.png)

## <a name="reset-the-device"></a>Reimpostare il dispositivo

Poiché è necessario che il dispositivo sia in modalità di controllo o sistema operativo completo per acquisire il valore HH di 4K, la funzionalità di ripristino deve ripristinare lo stato pre-configurazione dell'immagine prima di restituirla al cliente.  A questo scopo, è possibile usare la funzionalità di reimpostazione predefinita di Windows, come indicato di seguito:

Nel dispositivo passare a impostazioni > Aggiorna & sicurezza > ripristino e fare clic su introduzione.  In Reimposta questo PC selezionare Rimuovi tutto e rimuovere i file personali. Infine, fare clic su Reimposta.

![reset](images/reset.png)

Tuttavia, è probabile che la funzionalità di ripristino non possa accedere a Windows perché non dispongono delle credenziali utente per l'accesso, nel qual caso è necessario usare altri metodi per ricreare l'immagine del dispositivo, ad esempio lo [strumento di gestione e manutenzione immagini distribuzione](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#use-a-deployment-script-to-apply-your-image).

## <a name="return-the-repaired-device-to-the-customer"></a>Restituzione del dispositivo riparato al cliente

Dopo aver completato i passaggi precedenti, il dispositivo ripristinato può ora essere restituito al cliente e verrà automaticamente registrato nel programma Autopilot al primo avvio durante la configurazione guidata.

**Nota**: se la funzionalità di ripristino non ha ridefinito l'immagine del dispositivo, potrebbe inviarla nuovamente in uno stato potenzialmente danneggiato (ad esempio, non è possibile accedere al dispositivo perché è stato annullato dall'unico account utente noto), nel qual caso deve indicare all'organizzazione che è necessario correggere la registrazione e il sistema operativo.

**Importante**: un dispositivo può essere "registrato" per Autopilot prima di essere acceso, ma il dispositivo non è effettivamente "distribuito" a Autopilot (ad esempio, abilitato come dispositivo Autopilot) finché non passa attraverso la configurazione guidata, motivo per cui la reimpostazione del dispositivo su uno stato pre-configurazione è un passaggio obbligatorio.

## <a name="specific-repair-scenarios"></a>Scenari di ripristino specifici

Questa sezione descrive gli scenari di ripristino più comuni e il relativo effetto sull'abilitazione di Autopilot.

NOTE SUI RISULTATI DEI TEST:

- Gli scenari seguenti sono stati testati solo con Intune (nessun altro MDMs testato).
- Nella maggior parte degli scenari di test riportati di seguito, il dispositivo ripristinato e registrato per l'attivazione di Autopilot è stato necessario per eseguire di nuovo la configurazione guidata.
- Gli scenari di sostituzione della scheda madre spesso comportano la perdita di dati, pertanto è consigliabile ricordare ai centri di riparazione o ai clienti di eseguire il backup dei dati, se possibile, prima del ripristino.
- Nei casi in cui una funzionalità di ripristino non è in grado di scrivere informazioni sul dispositivo nel BIOS del dispositivo riparato, è necessario creare nuovi processi per abilitare correttamente Autopilot.
- Il dispositivo riparato deve avere il codice Product Key (DPK) preinserito nel BIOS prima di acquisire il nuovo 4K HH (ID dispositivo)

Nella tabella seguente:<br>
- Supportato = **Sì**: il dispositivo può essere riabilitato per Autopilot
- Supportato = **No**: non è possibile riabilitare il dispositivo per Autopilot

<table border="1">
<th>Scenario<th>Supportato<th>Raccomandazione Microsoft
<tr><td>Sostituzione della scheda madre (MBR) in generale<td>Sì<td>La linea di azione consigliata per gli scenari MBR è la seguente:

1. Viene annullata la registrazione del dispositivo Autopilot dal programma Autopilot
2. La scheda madre è Replace
3. Viene ricreata l'immagine del dispositivo (con le informazioni sul BIOS e DPK reinserito) *
4. Un nuovo ID dispositivo Autopilot (4K HH) viene acquisito dal dispositivo
5. Il dispositivo riparato viene registrato di nuovo per il programma Autopilot usando il nuovo ID dispositivo
6. Il dispositivo riparato viene reimpostato per l'avvio della configurazione guidata
7. Il dispositivo riparato viene nuovamente rispedito al cliente

* Non è necessario ricreare l'immagine del dispositivo se il tecnico di riparazione ha accesso alle credenziali di accesso del cliente.  È tecnicamente possibile eseguire una nuova abilitazione di MBR e Autopilot senza chiavi o determinate informazioni del BIOS (ad esempio, il numero di serie, il nome del modello e così via), ma questa operazione è consigliata solo a scopo di test o didattico.

<tr><td>MBR quando la scheda madre dispone di un chip TPM (abilitato) e di una sola scheda di rete di onboarding (che viene anche sostituita)<td>Sì<td>

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci Motherboard
3. Ricreare l'immagine del dispositivo (per ottenere l'accesso), a meno che non si abbia accesso alle credenziali di accesso dei clienti
4. Scrivi informazioni sul dispositivo nel BIOS
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ripristinare il dispositivo alla configurazione guidata
8. Passa attraverso la configurazione guidata di Autopilot (cliente)
9. Abilitazione di Autopilot completata

<tr><td>MBR quando la scheda madre ha un chip TPM (abilitato) e una seconda scheda di rete (o interfaccia di rete) che non viene sostituita con la scheda madre<td>No<td>Questo scenario non è consigliato, in quanto interrompe l'esperienza di Autopilot, perché l'ID dispositivo risultante non sarà stabile fino al completamento dell'attestazione TPM e anche la registrazione potrebbe restituire risultati non corretti a causa dell'ambiguità con la risoluzione degli indirizzi MAC.
<tr><td>MBR in cui la scheda NIC, il disco rigido e la WLAN rimangono invariati dopo la riparazione<td>Sì<td>

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci scheda madre (con nuovo RDPK preinserito nel BIOS)
3. Ricreare l'immagine del dispositivo (per ottenere l'accesso), a meno che non si abbia accesso alle credenziali di accesso dei clienti
4. Scrivi le informazioni sul dispositivo obsolete nel BIOS (stessa s/n, modello e così via) *
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ripristinare il dispositivo alla configurazione guidata
8. Passa attraverso la configurazione guidata di Autopilot (cliente)
9. Abilitazione di Autopilot completata

* Si noti che per questo e per gli scenari successivi la riscrittura delle informazioni sul dispositivo obsolete non include la chiave di verifica dell'autenticità TPM 2,0, perché la chiave privata associata è bloccata al dispositivo TPM

<tr><td>MBR in cui la scheda NIC rimane invariata, ma le unità disco rigido e WLAN vengono sostituite<td>Sì<td>

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci scheda madre (con nuovo RDPK preinserito nel BIOS)
3. Inserisci nuovo HDD e WLAN
4. Scrivi le informazioni sul dispositivo obsolete nel BIOS (stessa s/n, modello e così via)
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ripristinare il dispositivo alla configurazione guidata
8. Passa attraverso la configurazione guidata di Autopilot (cliente)
9. Abilitazione di Autopilot completata

<tr><td>MBR in cui la scheda NIC e la rete WLAN rimangono invariate, ma il disco rigido viene sostituito<td>Sì<td>

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci scheda madre (con nuovo RDPK preinserito nel BIOS)
3. Inserisci nuovo HDD
4. Scrivi le informazioni sul dispositivo obsolete nel BIOS (stessa s/n, modello e così via)
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ripristinare il dispositivo alla configurazione guidata
8. Passa attraverso la configurazione guidata di Autopilot (cliente)
9. Abilitazione di Autopilot completata

<tr><td>MBR in cui vengono sostituiti solo i MB (tutte le altre parti restano uguali), ma sono stati rilevati nuovi MB da un dispositivo usato in precedenza che non era stato abilitato per la funzionalità Autopilot prima.<td>Sì<td>

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci scheda madre (con nuovo RDPK preinserito nel BIOS)
3. Ricreare l'immagine del dispositivo (per ottenere l'accesso), a meno che non si abbia accesso alle credenziali di accesso dei clienti
4. Scrivi le informazioni sul dispositivo obsolete nel BIOS (stessa s/n, modello e così via)
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ripristinare il dispositivo alla configurazione guidata
8. Passa attraverso la configurazione guidata di Autopilot (cliente)
9. Abilitazione di Autopilot completata

<tr><td>MBR in cui vengono sostituiti solo i MB (tutte le altre parti restano uguali), ma sono stati rilevati nuovi MB da un dispositivo usato in precedenza che era stato abilitato per la funzionalità Autopilot prima.<td>Sì<td>

1. Annulla la registrazione del dispositivo obsoleto da cui verranno effettuati MB
2. Annullare la registrazione del dispositivo danneggiato (che si desidera ripristinare)
3. Sostituire la scheda madre in ripristino dispositivo con MB da altro dispositivo Autopilot (con nuovo RDPK preinserito nel BIOS)
4. Ricreare l'immagine del dispositivo (per ottenere l'accesso), a meno che non si abbia accesso alle credenziali di accesso dei clienti
5. Scrivi le informazioni sul dispositivo obsolete nel BIOS (stessa s/n, modello e così via)
6. Acquisisci nuovo 4K HH
7. Registrare nuovamente il dispositivo ripristinato
8. Ripristinare il dispositivo alla configurazione guidata
9. Passa attraverso la configurazione guidata di Autopilot (cliente)
10. Abilitazione di Autopilot completata

<b>Nota</b>: il dispositivo riparato può essere usato anche con successo come dispositivo normale e non automatico.

<tr><td>Informazioni sul BIOS escluse dal dispositivo MBR<td>No<td>La funzionalità di ripristino non ha lo strumento BIOS per scrivere informazioni sul dispositivo nel BIOS dopo MBR.

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci Motherboard (il BIOS non contiene informazioni sul dispositivo)
3. Ricreare l'immagine e scrivere DPK nell'immagine
4. Acquisisci nuovo 4K HH
5. Registrare nuovamente il dispositivo ripristinato
6. Crea profilo di Autopilot per il dispositivo
7. Passa attraverso la configurazione guidata di Autopilot (cliente)
8. Autopilot non riesce a riconoscere il dispositivo riparato

<tr><td>MBR in assenza di chip TPM<td>Sì<td>Sebbene non sia consigliabile abilitare i dispositivi Autopilot senza un chip TPM (consigliato per la crittografia BitLocker), è possibile abilitare un dispositivo Autopilot in modalità "utente standard" (ma non in modalità self-Deploying) che non dispone di un chip TPM.  In questo caso, è necessario:

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci Motherboard
3. Ricreare l'immagine del dispositivo (per ottenere l'accesso), a meno che non si abbia accesso alle credenziali di accesso dei clienti
4. Scrivi le informazioni sul dispositivo obsolete nel BIOS (stessa s/n, modello e così via)
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ripristinare il dispositivo alla configurazione guidata
8. Passa attraverso la configurazione guidata di Autopilot (cliente)
9. Abilitazione di Autopilot completata

<tr><td>Nuovo DPK scritto in immagine in un dispositivo Autopilot riparato con un nuovo MB<td>Sì<td>La funzione di ripristino sostituisce i MB normali sul dispositivo danneggiato.  MB non contiene DPK nel BIOS.  Repair Facility scrive DPK nell'immagine dopo MBR.  

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci Motherboard: il BIOS non contiene informazioni DPK
3. Ricreare l'immagine del dispositivo (per ottenere l'accesso), a meno che non si abbia accesso alle credenziali di accesso dei clienti
4. Scrive le informazioni sul dispositivo nel BIOS (stessa s/n, modello e così via)
5. Acquisisci nuovo 4K HH
6. Reimpostare o ricreare l'immagine del dispositivo in pre-OOBE e scrivere DPK nell'immagine
7. Registrare nuovamente il dispositivo ripristinato
8. Passare attraverso la configurazione guidata di Autopilot
9. Abilitazione di Autopilot completata

<tr><td>Nuovo codice Product Key di ripristino (RDPK)<td>Sì<td>L'uso di una scheda madre con un nuovo RDPK preiniettato produce uno scenario di ripristino di Autopilot riuscito. 

1. Annulla registrazione dispositivo danneggiato
2. Sostituisci scheda madre (con nuovo RDPK preinserito nel BIOS)
3. Ricreare l'immagine o l'immagine Rest in pre-OOBE
4. Scrivi informazioni sul dispositivo nel BIOS 
5. Acquisisci nuovo 4K HH
6. Registrare nuovamente il dispositivo ripristinato
7. Ricreare l'immagine o ripristinare l'immagine pre-OOBE
8. Passare attraverso la configurazione guidata di Autopilot
9. Abilitazione di Autopilot completata

<tr><td>Nessun codice Product Key di ripristino (RDPK) inserito<td>No<td>Questo scenario viola i criteri Microsoft e interrompe l'esperienza di Windows Autopilot.
<tr><td>Ricreare l'immagine del dispositivo Autopilot danneggiato che non è stato annullato prima del ripristino<td>Sì, ma il dispositivo verrà comunque associato all'ID tenant precedente, quindi deve essere restituito solo allo stesso cliente<td>

1. Ricreare l'immagine del dispositivo danneggiato
2. Scrivi DPK nell'immagine
3. Passare attraverso la configurazione guidata di Autopilot
4. L'abilitazione di Autopilot è stata completata (per l'ID tenant precedente)

<tr><td>Sostituzione del disco da un dispositivo non Autopilot a un dispositivo Autopilot<td>Sì<td>

1. Non annullare la registrazione del dispositivo danneggiato prima del ripristino
2. Sostituisci HDD su dispositivo danneggiato
3. Ricreare l'immagine o ripristinare l'immagine alla configurazione guidata
4. Passa attraverso la configurazione guidata di Autopilot (cliente)
5. L'abilitazione di Autopilot è stata completata (dispositivo riparato riconosciuto come se fosse precedente)

<tr><td>Sostituzione del disco da un dispositivo Autopilot a un altro dispositivo Autopilot<td>È possibile<td>Se il dispositivo da cui è stato eseguito il disco rigido è stato precedentemente annullato da Autopilot, il disco rigido può essere usato in un dispositivo di ripristino.  Tuttavia, se non è mai stata precedentemente annullata la registrazione del disco rigido da Autopilot prima di essere usato in un dispositivo riparato, il dispositivo appena riparato non avrà l'esperienza Autopilot corretta.

Supponendo che l'unità disco rigido utilizzata sia stata annullata in precedenza (prima dell'utilizzo in questa riparazione):

1. Annulla registrazione dispositivo danneggiato
2. Sostituire HDD su un dispositivo danneggiato usando un disco rigido da un altro dispositivo Autopilot annullato
3. Ricreare l'immagine o riposizionare il dispositivo ripristinato in uno stato precedente alla configurazione guidata
4. Passa attraverso la configurazione guidata di Autopilot (cliente)
5. Abilitazione di Autopilot completata

<tr><td>Sostituzione di schede di rete non Microsoft <td>No<td>Se da un dispositivo non Autopilot a un dispositivo Autopilot, da un dispositivo Autopilot a un altro dispositivo Autopilot o da un dispositivo Autopilot a un dispositivo non Autopilot, qualsiasi scenario in cui viene sostituita una scheda di rete di terze parti (non onboard) interrompe l'esperienza Autopilot e non è consigliabile.
<tr><td>Un dispositivo è stato ripristinato più di 3 volte<td>No<td>Autopilot non è supportato quando un dispositivo viene ripristinato ripetutamente, in modo che tutte le parti non sostituite vengano associate a troppe parti sostituite, il che renderebbe difficile l'identificazione univoca del dispositivo in futuro.
<tr><td>Sostituzione memoria<td>Sì<td>La sostituzione della memoria in un dispositivo danneggiato non influisce negativamente sull'esperienza di Autopilot sul dispositivo.  Non è necessaria alcuna cancellazione.  Il tecnico della riparazione deve semplicemente sostituire la memoria.
<tr><td>Sostituzione GPU<td>Sì<td>La sostituzione delle GPU in un dispositivo danneggiato non influisce negativamente sull'esperienza di Autopilot sul dispositivo.  Non è necessaria alcuna cancellazione.  Il tecnico della riparazione deve semplicemente sostituire la GPU.
</table>

>Quando si esegue lo scavenging di parti da un altro dispositivo Autopilot, si consiglia di annullare la registrazione del dispositivo scavenging da Autopilot, di eseguire lo scavenging e di non registrare mai il dispositivo scavenged (anche in questo caso) per Autopilot, perché il riutilizzo di parti in questo modo può causare la chiusura di due dispositivi attivi con lo stesso ID, senza

**Nota**: le parti seguenti possono essere sostituite senza compromettere l'abilitazione di Autopilot o richiedere passaggi di correzione aggiuntivi speciali:
- Memoria (RAM o ROM)
- Alimentatore
- Scheda video
- Lettore di schede
- Scheda audio
- Scheda di espansione
- Microfono
- Webcam
- Fan
- Sink di calore
- Batteria CMOS

Altri scenari di ripristino non ancora testati e verificati includono:
- Sostituzione daughterboard
- Sostituzione CPU
- Sostituzione Wi-Fi
- Sostituzione Ethernet

## <a name="faq"></a>Domande frequenti

| Domanda | Risposta |
| --- | --- |
| Se si dispone di uno strumento che programma le informazioni sul prodotto nel BIOS dopo l'MBR, è comunque necessario inviare un report CBR affinché il dispositivo sia in grado di supportare la funzionalità Autopilot? | No.  Non se lo strumento interno scrive le informazioni minime necessarie nel BIOS che il programma Autopilot Cerca per identificare il dispositivo, come descritto in precedenza in questo documento. |
| Cosa accade se vengono sostituiti solo alcuni componenti anziché la scheda madre completa? | Sebbene sia vero che alcune riparazioni limitate non impediscono che l'algoritmo Autopilot corrisponda correttamente al dispositivo post-riparazione con il dispositivo di pre-riparazione, è consigliabile garantire un esito positivo del 100% eseguendo i passaggi MBR precedenti anche per i dispositivi che richiedevano solo riparazioni limitate. |
| In che modo un tecnico di riparazione ottiene l'accesso a un dispositivo rotto se non ha le credenziali di accesso del cliente? | Il tecnico dovrà ricreare l'immagine del dispositivo e usare le proprie credenziali durante il processo di ripristino. |

## <a name="related-topics"></a>Argomenti correlati

[Linee guida per i dispositivi](autopilot-device-guidelines.md)<br>