---
title: Funzionalità nella Technical Preview 1609
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1609 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: e7e803dd1cbacbbd65a5f2968e217656b088d281
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705449"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1609 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*



Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager, versione 1609. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    

**Problemi noti di questa versione Technical Preview:**  
*  Durante l'aggiornamento a Configuration Manager 1609 Technical Preview, verranno eliminati i criteri di aggiornamento dell'edizione eventualmente distribuiti. Per continuare a usare questi criteri, è necessario ricrearli e distribuirli.


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="improvements-to-endpoint-protection"></a>Miglioramenti a Endpoint Protection
Miglioramento delle impostazioni dei criteri antimalware di Endpoint Protection: è ora possibile specificare il livello a cui il servizio di protezione di Endpoint Protection Cloud bloccherà i file sospetti. Una nuova impostazione consente agli amministratori di specificare i computer "a rischio", in base a elevate quantità di malware rilevate.

## <a name="increased-number-of-enrolled-devices"></a>Aumento del numero di dispositivi registrati
Gli amministratori possono ora concedere agli utenti di registrare fino a 15 dispositivi nella gestione dei dispositivi mobili ibridi con Intune. In precedenza, il limite vigeva un limite di 5 dispositivi per utente.

## <a name="additional-apple-dep-settings"></a>Impostazioni aggiuntive per il DEP di Apple

Gli amministratori possono ora configurare le seguenti impostazioni del Programma di registrazione dispositivi di Apple nel profilo DEP di dispositivi iOS e Mac:
- **Touch ID**
- **Zoom**
- **Siri**

Se l'opzione è abilitata, l'assistente configurazione di Apple richiede questo servizio durante l'attivazione del dispositivo.

## <a name="integration-with-upgrade-analytics"></a>Integrazione con Upgrade Analytics

Upgrade Analytics consente di valutare e analizzare la leggibilità e la compatibilità dei dispositivi con Windows 10, per consentire aggiornamenti più semplici. L'integrazione di Upgrade Analytics con Configuration Manager consente di accedere ai dati di compatibilità dell'aggiornamento nella console di amministrazione di Configuration Manager e quindi, dall'elenco dei dispositivi, ai dispositivi da aggiornare o correggere.

Per altre informazioni su Upgrade Analytics, vedere in [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Introduzione a Upgrade Analytics).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Tipi di connessione nativa per i profili ibridi VPN di Windows 10

Quando si usa Configuration Manager con Intune, è possibile creare profili VPN di Windows 10 con tipi di connessione Microsoft Automatico, IKEv2, PPTP e L2TP nella console di Configuration Manager senza usare URI OMA.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Miglioramenti apportati a Integrazione di Windows Store per le aziende con Configuration Manager

In questa versione [Integrazione di Windows Store per le aziende](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) è stata aggiornata con le nuove funzionalità seguenti:

**Aggiornamento:** nella versione Technical Preview corrente la funzionalità di sincronizzazione immediata non è funzionale.

- In precedenza, era possibile distribuire solo app gratuite da Windows Store per le aziende. Configuration Manager ora supporta anche la distribuzione di app con licenza online a pagamento (solo per dispositivi registrati con Intune).
- Ora è possibile avviare una sincronizzazione immediata tra Windows Store per le aziende e Configuration Manager.
- È ora possibile modificare la chiave privata del client ottenuta da Azure Active Directory.

### <a name="try-it-out"></a>Verifica

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Acquisto e sincronizzare di un'app con licenza online a pagamento

1. Acquistare almeno un'app con licenza online a pagamento da Windows Store per le aziende.
2. Nell'area di lavoro **Amministrazione** della console di Configuration Manager fare clic su **Servizi cloud** > **Aggiornamenti e manutenzione** > **Windows Store per le aziende**.
3. Nella scheda **Home** nel **Gruppo di sincronizzazione** fare clic su **Sincronizza ora**.
4. Immediatamente dopo, l'app acquistata viene visualizzata nel nodo **Informazioni di licenza per le app dello Store** dell'area di lavoro **Gestione applicazioni**.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Creare e distribuire un'applicazione di Configuration Manager dai dati di un'app sincronizzata

La procedura per creare e distribuire un'applicazione di Configuration Manager da un'app dello Store a pagamento è identica a quella usata per la creazione di un'applicazione da un'applicazione gratuita. Vedere la sezione **Creare e distribuire un'applicazione di Configuration Manager da un'app di Windows Store per le aziende** in [Gestire le app Windows Store per le aziende con Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modificare la chiave privata del client da Azure Active Directory

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager fare clic su **Servizi cloud** > **Aggiornamenti e manutenzione** > **Windows Store per le aziende**.
2. Selezionare l'aqccount Windows Store per le aziende e fare clic su **Proprietà**.
3. Nella finestra di dialogo **Windows Store for Business Account Properties** (Proprietà account Windows Store per le aziende) immettere una nuova chiave nel campo **Chiave privata del client** e quindi fare clic su **Verifica**. Al termine della verifica, fare clic su **Applica**, quindi chiudere la finestra di dialogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Nuove impostazioni di conformità per gli elementi di configurazione

Sono state aggiunte molte nuove impostazioni che è possibile usare negli elementi di configurazione relativi a diverse piattaforme di dispositivi.
Si tratta di impostazioni che in precedenza esistevano nella configurazione autonoma di Microsoft Intune, rese ora disponibili per Intune con Configuration Manager.
Per assistenza con queste impostazioni, aprire [Gestire impostazioni e funzionalità nei dispositivi con i criteri di Microsoft Intune](/mem/intune/configuration/device-profiles) e selezionare il sottoargomento relativo alle impostazioni per la piattaforma desiderata.


### <a name="new-settings-for-android-devices"></a>Nuove impostazioni per i dispositivi Android

#### <a name="password-settings"></a>Impostazioni della password

- **Ricorda cronologia password**
- **Consenti sblocco delle impronte digitali**

#### <a name="security-settings"></a>Impostazioni di sicurezza

- **Richiedi crittografia sulle schede di memoria**
- **Consenti acquisizione schermo**
- **Consenti invio dati di diagnostica**

#### <a name="browser-settings"></a>Impostazioni del browser

- **Consenti browser Web**
- **Consenti riempimento automatico**
- **Consenti blocco popup**
- **Consenti cookie**
- **Consenti scripting**

#### <a name="app-settings"></a>Impostazioni delle app

- **Consenti archivio Google Play**

#### <a name="device-capability-settings"></a>Impostazioni relative alle funzionalità dei dispositivi

- **Consenti archivi rimovibili**
- **Consenti tethering Wi-Fi**
- **Consenti georilevazione**
- **Consenti NFC**
- **Consenti Bluetooth**
- **Consenti roaming vocale**
- **Consenti dati in roaming**
- **Consenti messaggi SMS/MMS**
- **Consenti assistente vocale**
- **Consenti composizione vocale**
- **Consenti copia e incolla**


### <a name="new-settings-for-ios-devices"></a>Nuove impostazioni per i dispositivi iOS

#### <a name="password-settings"></a>Impostazioni della password

- **Numero di caratteri complessi richiesti nella password**
- **Consenti password semplici**
- **Minuti di inattività prima che venga richiesta la password**
- **Ricorda cronologia password**

### <a name="new-settings-for-mac-os-x-devices"></a>Nuove impostazioni per i dispositivi Mac OS X

#### <a name="password-settings"></a>Impostazioni della password

- **Numero di caratteri complessi richiesti nella password**
- **Consenti password semplici**
- **Ricorda cronologia password**
- **Minuti di inattività prima dell'attivazione dello screen saver**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nuove impostazioni per i dispositivi Windows 10 Desktop e mobili

#### <a name="password-settings"></a>Impostazioni della password

- **Numero minimo di set di caratteri**
- **Ricorda cronologia password**
- **Richiedi una password quando il dispositivo torna attivo dopo uno stato di inattività**

#### <a name="security-settings"></a>Impostazioni di sicurezza

- **Richiedi crittografia sui dispositivi mobili**
- **Consenti l'annullamento della registrazione manuale**

#### <a name="device-capability-settings"></a>Impostazioni relative alle funzionalità dei dispositivi

- **Consenti VPN su rete cellulare**
- **Consenti roaming VPN su rete cellulare**
- **Consenti ripristino del telefono**
- **Consenti connessione USB**
- **Consenti Cortana**
- **Consenti notifiche del Centro operativo**

### <a name="new-settings-for-windows-10-team-devices"></a>Nuove impostazioni per i dispositivi Windows 10 Team

#### <a name="device-settings"></a>Impostazioni del dispositivo

- **Abilita Azure Operational Insights**
- **Abilita proiezione wireless Miracast**
- **Scegli le informazioni sulla riunione visualizzate nella schermata iniziale**
- **URL dell'immagine di sfondo per la schermata di blocco**


### <a name="new-settings-for-windows-81-devices"></a>Nuove impostazioni per i dispositivi Windows 8.1

#### <a name="applicability-settings"></a>Impostazioni di applicabilità

- **Applica tutte le configurazioni a Windows 10**

#### <a name="password-settings"></a>Impostazioni della password

- **Tipo di password richiesto**
- **Numero minimo di set di caratteri**
- **Lunghezza minima password**
- **Numero di errori di accesso ripetuti consentiti prima della cancellazione del dispositivo**
- **Minuti di inattività prima dello spegnimento dello schermo**
- **Scadenza password (giorni)**
- **Ricorda cronologia password**
- **Impedisci riutilizzo delle password precedenti**
- **Consenti password grafica e PIN**

#### <a name="browser-settings"></a>Impostazioni del browser

- **Consenti rilevamento automatico della rete Intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Nuove impostazioni per i dispositivi Windows Phone 8.1

#### <a name="applicability-settings"></a>Impostazioni di applicabilità

- **Applica tutte le configurazioni a Windows 10**

#### <a name="password-settings"></a>Impostazioni della password

- **Numero minimo di set di caratteri**
- **Consenti password semplici**
- **Ricorda cronologia password**

#### <a name="device-capability-settings"></a>Impostazioni relative alle funzionalità dei dispositivi

- **Consenti connessione automatica agli hotspot Wi-Fi gratuiti**


## <a name="improvements-for-boundary-groups"></a>Miglioramenti ai gruppi limite
Questa versione di anteprima introduce importanti modifiche ai gruppi limite e al relativo funzionamento con i punti di distribuzione. Queste modifiche consentiranno di semplificare la progettazione dell'infrastruttura del contenuto, offrendo maggiore controllo su come e quando i client eseguono il fallback per la ricerca di punti di distribuzione aggiuntivi come i percorsi di origine del contenuto. Sono inclusi i punti di distribuzione in locale e su cloud.

Questi miglioramenti sostituiscono i concetti e i comportamenti correnti, come la configurazione dei punti di distribuzione rapida o lenta, con un nuovo modello più facile da configurare e mantenere. Tali modifiche rappresentano anche un presupposto per le modifiche future che miglioreranno altri ruoli del sistema del sito associati ai gruppi limite.  

Durante l'aggiornamento a 1609, si verifica la conversione delle configurazioni dell gruppi limite corrente per adattarlo al nuovo modello, in modo che queste modifiche non disturbino le configurazioni di distribuzione del contenuto. Vedere [Update existing boundary groups to the new model](capabilities-in-technical-preview-1609.md#bkmk_update) (Aggiornare i gruppi limite esistenti al nuovo modello).

Le sezioni seguenti illustrano le modifiche introdotte con questa versione di anteprima, il funzionamento del nuovo modello e le aspettative per l'aggiornamento di un sito che dispone già di gruppi limite configurati.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Modifiche all'interfaccia utente e al comportamento per gruppi limite e percorsi del contenuto
Di seguito sono riportate le modifiche principali ai gruppi limite e alle modalità di ricerca del contenuto da parte dei client. Molti di queste modifiche e concetti funzionano in combinazione.
- **Rimozione delle configurazioni per i punti lenti o veloci:** I singoli punti di distribuzione non vengono più configurati come punti di distribuzione lenti o veloci.  Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente. Grazie a questa modifica, la scheda **Riferimenti** delle proprietà del gruppo limite non supporta la configurazione Veloce o Lento.
- **Nuovo gruppo di limiti predefinito in ogni sito:**  Ogni sito primario ha un nuovo gruppo di limiti predefinito denominato ***Default-Site-Boundary-Group\<codicesito>***.  Quando un client non è presente in un percorso di rete che viene assegnato a un gruppo limite, il client usa i sistemi del sito associati al gruppo predefinito del sito assegnato. Considerare l'uso di questo gruppo limite come sostituzione del concetto di percorso del contenuto di fallback.    
  -  Rimozione dell'opzione **'Consenti percorso origine di fallback per il contenuto'** : la configurazione di un punto di distribuzione da usare per il fallback non avviene più in modo esplicito e le opzioni per impostare questa proprietà vengono rimosse dall'interfaccia utente.

  Il risultato dell'impostazione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) in un tipo di distribuzione per le applicazioni cambia. Questa impostazione su un tipo di distribuzione consente ora al client di usare il gruppo limite del sito predefinito come percorso di origine del contenuto.

  -  **Relazioni tra gruppi di limiti:** ogni gruppo di limiti può essere collegato a uno o più gruppi di limiti aggiuntivi. Questi collegamenti costituiscono le relazioni configurate sulla nuova scheda delle proprietà del gruppo limite, denominata **Relationships** (Relazioni):
  -   Ogni gruppo limite associato direttamente a un client viene chiamato gruppo limite **corrente**.  
  -   Qualsiasi gruppo di limiti che un client può usare grazie all'associazione tra il gruppo di limiti *corrente* e un altro gruppo viene chiamato gruppo di limiti **adiacente**.
  -  Nella scheda **Relationships** (Relazioni) è possibile aggiungere gruppi limite da usare come gruppo limite *adiacente*. È anche possibile configurare una quantità di minuti che stabiliste il momento in cui il client che non riesce a trovare il contenuto da un punto di distribuzione nel gruppo *corrente* avvierà la ricerca dei percorsi del contenuto nei gruppi limite *adiacenti*.

      Quando si aggiunge o si modifica una configurazione del gruppo limite, è possibile bloccare il fallback su tale gruppo limite dal gruppo corrente che si sta configurando.

  Per usare la nuova configurazione, definire le associazioni esplicite (collegamenti) da un gruppo limite a un altro e configurare tutti i punti di distribuzione nel gruppo associato con la stessa durata in minuti. Il tempo configurato determina quando il momento in cui un client che non riesce a trovare l'origine di un contenuto del relativo gruppo limite *corrente* può iniziare a cercare le origini del contenuto nel gruppo limite adiacente.

  Oltre ai gruppi limite configurati in modo esplicito, ogni gruppo limite dispone di un collegamento implicito al gruppo limite del sito predefinito. Questo collegamento si attiva dopo 120 minuti, momento in cui il gruppo limite del sito predefinito diventa un gruppo limite adiacente che consente ai client di usare i punti di distribuzione associati a tale gruppo limite come percorsi di origine del contenuto.

  Questo comportamento sostituisce ciò che in precedenza veniva definito "fallback per il contenuto".  È possibile eseguire l'override di questo comportamento predefinito di 120 minuti, associando in modo esplicito il gruppo limite del sito predefinito a un gruppo *corrente* e impostando un momento specifico, indicato in minuti, o il blocco completo del fallback per impedirne l'uso.


- **I client provano a ottenere il contenuto da ogni punto di distribuzione per un massimo di 2 minuti:** quando un client cerca un percorso di origine del contenuto, prova ad accedere a ogni punto di distribuzione per 2 minuti prima di passare a un altro punto di distribuzione. Si tratta di una modifica rispetto alle versioni precedenti in cui i client tentavano di connettersi a un punto di distribuzione per un massimo di 2 ore.

  - Il primo punto di distribuzione che un client tenta di usare viene selezionato casualmente dal pool di punti di distribuzione disponibili nel gruppo, o gruppi, di limiti *corrente* del client.

  - Dopo due minuti, se il client non ha trovato il contenuto, passa a un nuovo punto di distribuzione e tenta di ottenere il contenuto da questo server. Questo processo viene ripetuto ogni due minuti fino a quando il client trova il contenuto o raggiunge l'ultimo server del pool.

  - Se un client non trova un percorso di origine del contenuto valido nel proprio pool *corrente* prima dell'intervallo di fallback verso un gruppo limite *adiacente*, il client aggiunge quindi i punti di distribuzione dal gruppo *adiacente* alla fine dell'elenco corrente e quindi cerca nel gruppo espanso di percorsi di origine che include i punti di distribuzione da entrambi i gruppi limite.

      > [!TIP]  
      > Quando si crea un collegamento esplicito tra il gruppo limite corrente e il gruppo limite del sito predefinito e si definisce un intervallo di fallback inferiore al tempo di fallback per il collegamento a un gruppo limite adiacente, i client iniziano la ricerca dei percorsi di origine dal gruppo limite del sito predefinito prima di includere il gruppo adiacente.

  - Quando il client non riesce a ottenere il contenuto dall'ultimo server nel pool, avvia nuovamente il processo.


### <a name="how-the-new-model-works"></a>Come funziona il nuovo modello
Quando si configurano i gruppi limite, associare i limiti (percorsi di rete) e i ruoli del sistema del sito, ad esempio i punti di distribuzione, al gruppo limite. Questa operazione agevola il collegamento dei client ai server del sistema del sito, come i punti di distribuzione che si trovano vicino ai client nella rete.   
- È possibile assegnare lo stesso limite a più gruppi limite.
- I server del sistema del sito, ad esempio i punti di distribuzione, possono essere associati a più gruppi limite, rendendoli disponibili per una vasta gamma di percorsi di rete.
- Se un punto di distribuzione non è associato a un gruppo limite, i client non saranno in grado di usare tale punto di distribuzione come percorso di origine del contenuto.

A partire da questa Technical Preview, è possibile definire le relazioni del gruppo limite per configurare il comportamento di fallback per i percorsi di origine del contenuto. Questo nuovo comportamento viene configurato nella nuova scheda **Relationships** (Relazioni) delle proprietà del gruppo limite e sostituisce la configurazione veloce o lenta dei sistemi del sito, nonché la configurazione di un gruppo limite per consentire il percorso di origine di fallback per il contenuto.

Nella scheda Relationshps (Relazioni) aggiungere altri gruppi limite per configurare una relazione con questi gruppi. Ogni relazione è un collegamento unidirezionale dal gruppo limite **corrente** al gruppo limite che si aggiunge, chiamato gruppo **adiacente**. Per ogni collegamento creato, è possibile configurare i punti di distribuzione con un tempo di fallback definito in minuti. Questo tempo viene usato per determinare dopo quanto tempo client del gruppo limite *corrente* può fare uso dei punti di distribuzione del gruppo limite *adiacente* se non riesce a trovare un percorso di origine del contenuto valido nel gruppo limite corrente.

Se un client non riesce a trovare il contenuto e inizia la ricerca dei percorsi nei gruppi di limiti adiacenti, il pool di punti di distribuzione disponibili aumenta in modo controllato per quel client.  

- Un gruppo limite può avere più di una relazione. Ciò consente di configurare il fallback su diversi gruppi adiacenti a diversi intervalli di tempo.
- I client eseguiranno il fallback a un gruppo limite solo se è direttamente adiacente al gruppo limite corrente.
- Se un client fa parte di più gruppi di limiti, il gruppo di limiti corrente è definito come un'unione di tutti i gruppi di limiti del client.  Il client può quindi eseguire il fallback a un gruppo adiacente di uno di questi gruppi limite originali.

Oltre ai collegamenti definiti dall'utente, esiste un collegamento implicito che viene creato automaticamente tra i gruppi limite creato dall'utente e il gruppo limite predefinito, creato automaticamente per ogni sito. Questo collegamento automatico:
- Viene usato dai client che non si trovano su un limite associato a un gruppo limite nella gerarchia che usa automaticamente il gruppo limite predefinito dal proprio sito assegnato per identificare i percorsi di origine del contenuto validi.   
-  Si tratta di un'opzione di fallback predefinita dal gruppo limite corrente al gruppo limite predefinito dei siti, usato dopo 120 minuti.

**Esempio di uso del nuovo modello:** Creare tre gruppi limite che non condividono limiti o server del sistema del sito:
- Gruppo BG_A con punti di distribuzione DP_A1 e DP_A2 associati al gruppo
- Gruppo BG_B con punti di distribuzione DP_B1 e DP_B2 associati al gruppo
- Gruppo BG_C con punti di distribuzione DP_C1 e DP_C2 associati al gruppo

Aggiungere i percorsi di rete dei client come limiti solo al gruppo limite BG_A e configurare le relazioni tra tale gruppo limite e gli altri due gruppi limite:
- Configurare i punti di distribuzione per il primo gruppo *adiacente* (BG_B) da usare dopo 10 minuti. Questo gruppo contiene i punti di distribuzione DP_B1 e DP_B2. Entrambi sono ben connessi ai percorsi limite dei primi gruppi.
- Configurare il secondo gruppo *adiacente* (BG_C) da usare dopo 20 minuti. Questo gruppo contiene i punti di distribuzione DP_C1 e DP_C2. Entrambi si trovano a un WAN rispetto agli altri due gruppi limite.
- Aggiungere anche un punto di distribuzione aggiuntivo che si trova nel server del sito al gruppo limite del sito predefinito di siti. Si tratta della posizione di origine di contenuto meno preferita, ma si trova a livello centrale per tutti i gruppi limite.

  Esempio di gruppi limite e tempi di fallback:

  ![BG_Fallack](media/BG_Fallback.png)


Con questa configurazione:
- Il client inizia la ricerca del contenuto dai punti di distribuzione nel relativo gruppo limite *corrente* (BG_A), cercando in ogni punto di distribuzione per due minuti prima di passare al successivo punto di distribuzione del gruppo limite. Il pool di client dei percorsi di origine del contenuto validi include DP_A1 e DP_A2.
- Se il client non riesce a trovare il contenuto nel proprio gruppo limite *corrente* dopo 10 minuti di ricerca, aggiunge i punti di distribuzione dal gruppo limite BG_B alla ricerca. Continua quindi a eseguire la ricerca del contenuto da un punto di distribuzione nel proprio pool combinato di punti di distribuzione che include ora i gruppi limite BG_A sia BG_B. Il client continuerà a contattare ogni punto di distribuzione per due minuti prima di passare al successivo punto di distribuzione del pool. Il pool di client dei percorsi di origine del contenuto validi include DP_A1, DP_A2, DP_B1 e DP_B2.
- Dopo altri 10 minuti (totale di 20 minuti), se il client non ha ancora rilevato un punto di distribuzione con contenuto, espande il proprio pool di punti di distribuzione disponibili per includere i punti del secondo gruppo *adiacente*, il gruppo limite BG_C. Il client ora dispone di 6 punti di distribuzione per la ricerca (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua la modifica a un nuovo punto di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.
- Se il client non ha rilevato il contenuto dopo un totale di 120 minuti, esegue il fallback per includere il *gruppo limite del sito predefinito* nella ricerca. Il pool di punti di distribuzione include ora tutti i punti di distribuzione dei tre gruppi limite configurati e il punto di distribuzione finale situato nel computer server del sito.  Il client continua quindi la ricerca del contenuto, modificando i punti di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.

Configurando i vari gruppi adiacenti perché siano disponibili in momenti diversi, è possibile controllare quando i punti di distribuzione specifici vengono aggiunti come percorso di origine del contenuto e quando o se il client esegue il fallback al gruppo limite del sito predefinito come rete di protezione per il contenuto non disponibile in altre posizioni.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Aggiornare i gruppi limite esistenti al nuovo modello
Quando si installa la versione 1609 e si aggiorna il sito, le configurazioni seguenti vengono eseguite in automatico. Tali configurazioni sono utili per verificare che il comportamento di fallback corrente rimanga disponibile finché non si configurano i nuovi gruppi limite e le relazioni.  
- Vengono aggiunti punti di distribuzione non protetti di un sito al gruppo limite *Default-Site-Boundary-Group\<CodiceSito>* di tale sito.
- Viene creata una copia di ogni gruppo limite esistente che include un server del sito configurato con una connessione lenta. Il nome del nuovo gruppo è ***\<nome originale del gruppo limite >-Slow-Tmp***:  
  -   I sistemi del sito che dispongono di una connessione veloce rimangono nel gruppo limite originale.
  -   Viene aggiunta una copia dei sistemi del sito con connessione lenta alla copia del gruppo limite. I sistemi del sito originale configurati con connessione lenta rimangono nel gruppo limite originale per la compatibilità con le versioni precedenti, ma non vengono usati da questo gruppo limite.
  -   Questa copia del gruppo limite non dispone di limiti associati. Tuttavia, viene creato un collegamento fallback tra il gruppo originale e la nuova copia del gruppo limite che presenta l'ora di fallback impostata su zero.

  La tabella seguente identifica il nuovo comportamento di fallback previsto dalla combinazione di impostazioni di distribuzione originali e di configurazioni di punti di distribuzione:

Configurazione della distribuzione originale per "Non eseguire il programma" in una rete lenta  |Configurazione del punto di distribuzione originale per "Allow client to use a fallback source location for content" (Consenti al client di usare un percorso di origine di fallback per il contenuto)  |Nuovo comportamento di fallback  
---------|---------|---------
Selezionato     |  Selezionato    |  **Nessun fallback**: usare solo i punti di distribuzione nel gruppo limite corrente       
Selezionato     |  Non selezionato|  **Nessun fallback**: usare solo i punti di distribuzione nel gruppo limite corrente       
Non selezionato |  Non selezionato|  **Fallback verso adiacente**: usare i punti di distribuzione nel gruppo limite corrente e quindi aggiungere i punti di distribuzione del gruppo limite adiacente. A meno che non sia configurato un collegamento esplicito al gruppo limite del sito predefinito, i client non eseguono il fallback su questo gruppo.    
Non selezionato | Selezionato |   **Fallback normale**: usare i punti di distribuzione nel gruppo limite corrente, quindi quelli del gruppo adiacente e dal gruppo limite del sito predefinito

 Tutte le altre configurazioni di distribuzione seguiranno il **Fallback normale**.  



## <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365  
Configuration Manager 1609 Technical Preview introduce un nuovo dashboard. Per visualizzare il dashboard, nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management** (Gestione Client di Office 365).
>[!NOTE]
>Nell'area di lavoro **Novità** della console di Configuration Manager, il nuovo dashboard viene erroneamente chiamato **Office 365 Servicing dashboard** (Dashboard per la manutenzione di Office 365).

Nel dashboard vengono visualizzati i grafici per:

- Numero di client di Office 365
- Versioni dei client di Office 365
- Lingue dei client di Office 365
- Canali dei client di Office 365     
Per altre informazioni, vedere [Panoramica dei canali di aggiornamento per Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Regole di distribuzione automatica con il client di Office 365 selezionato nel set dei prodotti disponibili.

Sul dashboard è possibile eseguire le azioni seguenti:
- Nella parte superiore del dashboard, usare l'impostazione a discesa **Raccolta** per filtrare i dati del dashboard in base ai membri di una raccolta specifica.
- Sul lato superiore destro del dashboard, fare clic su **Office 365 Installer** (Programma di installazione di Office 365) per avviare l'installazione guidata di Office 365 Client e distribuire le applicazioni di Office 365 sui client. Per informazioni dettagliate, vedere [Distribuire le app di Office 365 sui client](#deploy-office-365-apps-to-clients).
- Sul lato centrale a destra del dashboard, fare clic su **Create an ADR** (Crea un ADR) per aprire la creazione guidata delle regole di distribuzione automatica e creare una nuova regola di distribuzione automatica (ADR). Per creare un ADR per le applicazioni di Office 365, selezionare **Office 365 Client** (Client Office 365) quando si sceglie il prodotto. Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](../../sum/deploy-use/automatically-deploy-software-updates.md).
- Sul lato inferiore destro del dashboard, fare clic su **Create Client Agent Settings** (Crea impostazioni agente client) per aprire le impostazioni dell'agente client. Per altre informazioni, vedere [About client settings](../clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client).



Per altre informazioni sugli aggiornamenti di Office 365 ProPlus, vedere [Manage Office 365 ProPlus updates with Configuration Manager](../../sum/deploy-use/manage-office-365-proplus-updates.md) (Gestire gli aggiornamenti di Office 365 ProPlus con Configuration Manager).

## <a name="deploy-office-365-apps-to-clients"></a>Distribuire le app di Office 365 sui client
In questa versione, nel dashboard di gestione del client di Office 365, è possibile avviare l'installazione di Office 365 che consente di configurare le impostazioni di installazione di Office 365, scaricare file dalle reti di distribuzione del contenuto (CDN) e distribuire i file come applicazione in Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Limitazioni della distribuzione di Office 365
- Si potrebbero anche presentare problemi quando si tenta di importare le impostazioni client esistenti (XML) durante l'installazione guidata dell'app Office 365. È possibile configurare manualmente le impostazioni del client senza riscontrare problemi.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Per distribuire le app di Office 365 sui client
1. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management** (Gestione Client di Office 365).
2. Fare clic su **Office 365 Installer** (Programma di installazione di Office 365) nel riquadro in alto a destro. Si apre l'installazione guidata dei client di Office 365.
3. Nella pagina **Impostazioni applicazione** specificare il nome e la descrizione per l'app, immettere il percorso di download per i file e quindi fare clic su **Avanti**. Si noti che è necessario specificare il percorso nel formato &#92;&#92;*server*&#92;*share*.
4. Nella pagina **Import Client Settings** (Importa impostazioni client) scegliere se importare le impostazioni del client di Office 365 da un file di configurazione XML esistente o se specificare manualmente le impostazioni, quindi fare clic su **Avanti**.
Se già si dispone di un file di configurazione, immettere il percorso del file e andare al passaggio 7. Si noti che è necessario specificare il percorso nel formato &#92;&#92;*server*&#92;*share*&#92;*nomedelfile*.XML.

    > [!IMPORTANT]
    >In questa Tecnical Preview, si potrebbero anche presentare problemi quando si tenta di importare le impostazioni client esistenti (XML).

5. Nella pagina **Client Products** (Prodotti client) selezionare la suite Office 365 in uso, selezionare le applicazioni da includere, selezionare eventuali prodotti aggiuntivi di Office da includere e quindi fare clic su **Avanti**.
6. Nella pagina **Impostazioni client** scegliere le impostazioni da includere e fare clic su **Avanti**.
7. Nella pagina **Distribuzione** scegliere se distribuire l'applicazione, quindi fare clic su pagina **Avanti**.
Se si sceglie di non distribuire il pacchetto nella procedura guidata, andare al passaggio 9.
8. Configurare il resto delle pagine della procedura guidata come si farebbe per la distribuzione di un'applicazione comune. Per altre informazioni, vedere [Create and deploy an application](../../apps/get-started/create-and-deploy-an-application.md) (Creare e distribuire un'applicazione).
9. Completare la procedura guidata.
10. È possibile distribuire o modificare l'applicazione esattamente come si farebbe con qualsiasi altra applicazione in Configuration Manager da **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Applicazioni**.

>[!NOTE]
>Dopo la distribuzione delle applicazioni di Office 365, è possibile creare regole di distribuzione automatica per le applicazioni. Per creare un ADR per le applicazioni di Office 365, fare clic su **Create an ADR** (Crea un ADR) e selezionare **Office 365 Client** (Client Office 365) quando si sceglie il prodotto. Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>Miglioramenti della conversione da BIOS a UEFI
È ora possibile personalizzare una sequenza di attività di distribuzione del sistema operativo con una nuova variabile, TSUEFIDrive, in modo che il passaggio di riavvio del computer prepari una partizione FAT32 sul disco rigido per la transizione a UEFI. La procedura seguente fornisce un esempio sulle modalità di creazione dei passaggi della sequenza di attività per preparare il disco rigido alla conversione da BIOS a UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Per preparare la partizione FAT32 alla conversione a UEFI:
In una sequenza di attività esistente per installare un sistema operativo si aggiungerà un nuovo gruppo usando la procedura di conversione da BIOS a UEFI.

1. Creare un nuovo gruppo di sequenze di attività dopo aver eseguito la proceduta per acquisire file e impostazioni e prima della procedura di installazione del sistema operativo. Ad esempio, creare un gruppo dopo il gruppo **Acquisisci file e impostazioni** denominato **BIOS-to-UEFI** (Da BIOS a UEFI).
2. Nella scheda **Opzioni** del nuovo gruppo aggiungere una nuova variabile della sequenza di attività come condizione in cui **_SMSTSBootUEFI** sia **diverso** da **true**. Questa operazione blocca l'esecuzione dei passaggi nel gruppo quando il computer è già in modalità UEFI.
![Gruppo BIOS to UEFI](media/BIOS-to-UEFI-group.png)
3. Nel nuovo gruppo aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.  
4. Nella scheda **Opzioni** aggiungere una variabile della sequenza attività come condizione in cui **_SMSTSInWinPE sia uguale a false** Questa operazione blocca l'esecuzione di questo passaggio se il computer è già in Windows PE.

    ![Passaggio Riavvia il computer](media/Restart-in-Windows-PE.png)
5. Aggiungere un passaggio per avviare lo strumento OEM che convertirà il firmware da BIOS a UEFI. Si tratta in genere di un passaggio della sequenza di attività **Esegui riga di comando** con una riga di comando per avviare lo strumento OEM.
5. Aggiungere il passaggio della sequenza attività Formato e disco partizione che partiziona e formatta il disco rigido. Nel passaggio, eseguire le operazioni seguenti:
    1. Creare la partizione FAT32 che verrà convertita in UEFI prima di installare il sistema operativo. Scegliere **GPT** per **Tipo disco**.
    ![Passaggio Formato e disco partizione](media/Format-and-partition-disk.png)
    2. Accedere alle proprietà della partizione FAT32. Immettere **TSUEFIDrive** nel campo **Variabile**. Quando la sequenza di attività rileva questa variabile, si avvia la preparazione per la transizione di UEFI prima di riavviare il computer.
    ![Proprietà della partizione](media/Partition-properties.png)
    3. Creare una partizione NTFS che il motore della sequenza di attività usa per il salvataggio dello stato e per archiviare i file di log.
6. Aggiungere il passaggio della sequenza di attività **Riavvia il computer**. In **Specificare cosa eseguire dopo il riavvio:** selezionare **The boot image assigned to this task sequence is selected** (L'immagine di avvio assegnata a questa sequenza di attività è selezionata) per avviare il computer in Windows PE.  




## <a name="intune-compliance-charts"></a>Grafici di conformità di Intune
In questa versione, è possibile ottenere una panoramica sulla conformità generale dei dispositivi e sui motivi principali della non conformità tramite nuovi grafici offerti **nell'area di lavoro di monitoraggio** della console di Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Per visualizzare i grafici di conformità di Intune
1. Nel riquadro di spostamento della console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Impostazioni di conformità**.
2. Viene visualizzato il grafico **Overall Device Compliance** (Conformità generale del dispositivo).
3. Fare clic sul nodo **Criteri di conformità** per visualizzare i grafici **Overall Device Compliance** (Conformità generale del dispositivo) e **Top Non-Compliance Reasons** (Motivi principali della non conformità).

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitazioni dei grafici di conformità di Intune in 1609 TP
- Attualmente, il drill-down per il grafico **Overall Device Compliance** (Conformità generale del dispositivo) genera un errore.
- Il grafico **Top Non-Compliance Reasons** (Motivi principali della non conformità) elenca il nome del criterio e non i singoli motivi di non conformità. È possibile scegliere i criteri per il drill-down e visualizzare i dispositivi non conformi a tale criterio.

### <a name="try-it-out"></a>Procedura
Completare le sezioni seguenti in ordine:

#### <a name="check-overall-compliance-chart"></a>Controllare il grafico sulla conformità generale.
1. Aggiungere a due criteri di conformità iOS in Configuration Manager. Un criterio deve avere un set di impostazioni per i dispositivi (ad esempio, impostare la lunghezza del PIN su 6). L'altro criterio deve avere un altro set di impostazioni (ad esempio, la complessità del PIN). Le impostazioni dei criteri non devono sovrapporsi o essere in conflitto.
2. Distribuire i due criteri in un set di utenti.
3. Registrare due dispositivi iOS in Intune usando lo stesso account utente e un account che abbia ricevuto i criteri nel passaggio precedente. I dispositivi non devono soddisfare i criteri di conformità.
4. In Configuration Manager, controllare il grafico **Overall Device Compliance** (Conformità generale del dispositivo). Entrambi i dispositivi devono essere contrassegnati come non conformi.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Controllare il grafico Top Non-Compliance Reasons (Motivi principali della non conformità).
5. Controllare il grafico **Top Non-Compliance Reasons (Motivi principali della non conformità)** . Questo grafico elenca i 5 motivi principali della non conformità ma, se sono state configurate solo due impostazioni di conformità nei criteri, vengono visualizzati solo i primi 2 motivi.
6. Fare clic su una delle sezioni nel grafico. Entrambi i dispositivi dovrebbero essere visualizzati nella visualizzazione filtrata in **Asset e conformità** > **Panoramica** > **Dispositivo**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Rendere i dispositivi conformi e controllare i grafici.
7. Rendere uno dei dispositivi conformi a uno dei criteri. Controllare nuovamente il grafico **Overall Device Compliance** (Conformità generale del dispositivo). Il grafico deve visualizzare un dispositivo conforme e un dispositivo non conforme.
8. Rendere l'altro dispositivo conforme agli stessi criteri. In questo modo si avrà un dispositivo conforme ai due criteri e un dispositivo conforme a uno solo dei criteri.
9. Controllare il grafico **Top Non-Compliance Reasons (Motivi principali della non conformità)** . Dovrebbe essere elencato un solo motivo di non conformità.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Vedere anche
[Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md)
