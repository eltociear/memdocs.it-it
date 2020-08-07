---
title: Domande frequenti su Windows Autopilot
ms.reviewer: This topic provides OEMs, partners, administrators, and end users with answers to some frequently asked questions about deploying Windows 10 with Windows Autopilot.
manager: laurawi
description: Informazioni di supporto per Windows Autopilot
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 060f2188be0c4674a7770e36c4bfdf26def669f4
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757414"
---
# <a name="windows-autopilot-faq"></a>Domande frequenti su Windows Autopilot

**Si applica a: Windows 10**

Questo articolo fornisce agli OEM, ai partner, agli amministratori e agli utenti finali le risposte ad alcune domande frequenti sulla distribuzione di Windows 10 con Windows Autopilot. 

Alla fine viene fornito un [Glossario](#glossary) delle abbreviazioni usate in questo articolo.


## <a name="microsoft-partner-center"></a>Microsoft Partner Center

| Domanda | Risposta |
| --- | --- |
| Nel centro per i partner è necessario fornire l'ID tenant con ogni caricamento di file del dispositivo? È necessario consentire ai clienti aziendali di accedere ai propri dispositivi in Microsoft Store for business (MSfB)?     | No. Fornire l'ID tenant è una singola voce nel centro per i partner che può essere riutilizzata con caricamenti di dispositivi futuri. |
| In che modo il cliente o il tenant sa che i loro dispositivi sono pronti per essere richiesti in MSfB?    |  Al termine del caricamento del file del dispositivo nel centro per i partner, il tenant può visualizzare i dispositivi disponibili per la configurazione di Windows Autopilot in MSfB. L'OEM deve consigliare al tenant di accedere a MSfB. È in corso lo sviluppo della notifica di autonotifica da MSfB al tenant.  |
| In che modo un cliente autorizza un partner OEM o canale a registrare i dispositivi Autopilot per conto dell'utente?   |  Prima che un partner OEM o canale possa registrare un dispositivo per l'autopilot per conto di un cliente, il cliente deve prima concedere il consenso.  Il processo di consenso inizia con l'OEM o il partner del canale che invia un collegamento al cliente che indirizza il cliente a una pagina di consenso in MSfB.  Per ulteriori informazioni, vedere la pagina relativa alla [registrazione](registration-auth.md).  |
|  Sono presenti restrizioni se un cliente aziendale ha registrato dispositivi in MSfB e in un secondo momento desidera che i dispositivi siano gestiti da un provider di soluzioni cloud (CSP) tramite il centro per i partner? | I dispositivi dovranno essere eliminati in MSfB dal cliente aziendale prima che il CSP possa caricarli e gestirli nel centro per i partner. | 
| Windows Autopilot supporta la rimozione dell'opzione per abilitare un account amministratore locale?    |  Windows Autopilot non supporta la rimozione dell'account amministratore locale. Tuttavia, non supporta la limitazione dell'utente che esegue l'aggiunta al dominio di Azure Active Directory (Azure AD) in OOBE a un account standard (rispetto a un account amministratore per impostazione predefinita).|
| Come è possibile testare il file CSV di Windows Autopilot nel centro per i partner?    |  Solo i partner CSP possono accedere al portale del centro per i partner. Se si è un CSP, è possibile creare un account utente dell'agente di vendita con accesso ai dispositivi per il test del file. Questa operazione può essere eseguita oggi nel centro per i partner. <br><br>Per altre informazioni, vedere [creare account utente e impostare le autorizzazioni](https://msdn.microsoft.com/partner-center/create-user-accounts-and-set-permissions). |
|  È necessario diventare un CSP per partecipare a Windows Autopilot? | I principali OEM del volume non lo fanno, perché possono usare l'API diretta OEM.  Tutti gli altri utenti che scelgono di usare MPC per registrare i dispositivi devono diventare CSP per poter accedere a MPC.  |
| I diversi livelli CSP hanno tutte le stesse funzionalità quando si tratta di Windows Autopilot?   |  Per gli scopi di Windows Autopilot sono disponibili tre diversi tipi di CSP, ognuno con diversi livelli di autorità e accesso: <br><br>1. <b>Direct CSP</b>: Ottiene l'autorizzazione diretta dal cliente per la registrazione dei dispositivi. <br><br>2. <b>provider CSP indiretto</b>: Ottiene l'autorizzazione implicita per la registrazione dei dispositivi tramite la relazione tra il partner del rivenditore CSP e il cliente.  I provider CSP indiretti registrano i dispositivi tramite il centro per i partner Microsoft. <br><br>3. <b>rivenditore CSP indiretto</b>: Ottiene l'autorizzazione diretta dal cliente per la registrazione dei dispositivi.  Allo stesso tempo, il partner provider CSP indiretto ottiene anche l'autorizzazione, il che significa che il provider indiretto o il rivenditore indiretto può registrare i dispositivi per il cliente.  Tuttavia, il rivenditore CSP indiretto deve registrare i dispositivi tramite l'interfaccia utente di MPC (caricando manualmente il file CSV), mentre il provider CSP indiretto ha la possibilità di registrare i dispositivi usando le API MPC. |


## <a name="manufacturing"></a>Produzione

| Domanda | Risposta |
| --- | --- |
| Quali modifiche devono essere apportate nell'immagine del sistema operativo Factory per le impostazioni di configurazione del cliente?     |Per abilitare la distribuzione di Windows Autopilot, non sono necessarie modifiche nel piano Factory.  |
| Quale versione dello strumento OA3 soddisfa i requisiti di distribuzione di Windows Autopilot?     | Windows Autopilot può funzionare con qualsiasi versione dello strumento OA3. È consigliabile usare una versione supportata del canale semestrale di Windows 10 per generare l'hash hardware 4K.    |
|  Al momento dell'inserimento di un ordine, i clienti devono essere in stato indipendentemente dal fatto che lo desiderino con o senza le opzioni di Windows Autopilot?   | Sì, se desiderano Windows Autopilot, vorranno una versione supportata del canale semestrale di Windows 10. Inoltre, dovranno ricevere il file CSV o avere completato il caricamento del file (ovvero la registrazione) per loro conto.    |
|  L'OEM ha la necessità di gestire o raccogliere file di imaging personalizzati dai clienti ed eseguire qualsiasi caricamento di immagini in Microsoft?   | Gli OEM semplicemente inviano il CBRs come di consueto a Microsoft. Non viene inviata alcuna immagine a Microsoft per abilitare Windows Autopilot.  Windows Autopilot Personalizza solo la configurazione guidata e consente le configurazioni dei criteri (ad esempio, Disabilita l'account amministratore).  |
|  Ci sono effetti dei clienti sull'aggiornamento da Windows 8 a Windows 10?    | I dispositivi devono eseguire una versione supportata del canale semestrale di Windows 10 per registrare la distribuzione di Windows Autopilot. In caso contrario, non ci sono effetti.    |
| Verranno apportate modifiche al codice CBR esistente con hash hardware 4K?    | No.  |
| Quali nuove informazioni devono essere inviate dall'OEM a Microsoft?    | Niente, a meno che l'OEM non opti per la registrazione del dispositivo per conto del cliente, nel qual caso carica l'ID del dispositivo usando un file CSV nel centro per i partner Microsoft oppure usa l'API diretta OEM.  |
| Un contratto o una modifica per un OEM può partecipare alla distribuzione di Windows Autopilot?    | No.  |

## <a name="csv-schema"></a>Schema CSV

| Domanda | Risposta |
| --- | --- |
|  È possibile utilizzare una virgola nel file CSV? | No.   |
| Quali messaggi di errore possono essere visualizzati da un utente nel centro per i partner o MSfB quando si carica un file?    | Vedere la sezione in Microsoft Store for business di questa guida.  |
| È previsto un limite per il numero di dispositivi che possono essere elencati nel file CSV?    | Sì, il file CSV può contenere solo dispositivi 1.000 da applicare a un unico profilo. Se è necessario applicare più di 1.000 dispositivi a un profilo, i dispositivi devono essere caricati tramite più file CSV.    |
| Microsoft offre consigli su come un OEM deve fornire il file CSV ai clienti?    |  Si consiglia di crittografare il file CSV durante l'invio al cliente aziendale per la registrazione automatica dei dispositivi Windows Autopilot (tramite MPC, MSfB o Intune).   |


## <a name="hardware-hash"></a>Hash hardware

| Domanda | Risposta |
| --- | --- |
| È necessario che ogni hash hardware inviato dall'OEM includa l'UUID SMBIOS (identificatore univoco universale), l'indirizzo MAC (Media Access Control) e il numero di serie del disco univoco (se si usa lo strumento Windows 10 OEM Activation 3,0)?    | Sì. Poiché Windows Autopilot è basato sulla possibilità di identificare in modo univoco i dispositivi che applicano la configurazione cloud, è fondamentale inviare hash hardware che soddisfino il requisito descritto.   |
| Qual è il motivo per cui sono necessari l'UUID SMBIOS, l'indirizzo MAC e il numero di serie del disco nei dettagli dell'hash hardware?    | Per la creazione dell'hash hardware, questi sono i campi necessari per identificare un dispositivo, in quanto le parti del dispositivo vengono aggiunte o rimosse. Poiché non è presente un identificatore univoco per i dispositivi Windows, questa è la logica migliore per identificare un dispositivo.    |
| Qual è la differenza tra hash hardware OA3, hash hardware 4K e hash hardware di Windows Autopilot?    | No.  Si tratta di nomi diversi per la stessa cosa.  L'output dello strumento OA3 è denominato hash OA3, che è di dimensioni 4K, che è utilizzabile per lo scenario di distribuzione di Windows Autopilot. Nota: quando si usa una versione precedente non supportata di Windows OA3Tool, si ottiene un hash di dimensioni diverso, che non può essere usato per la distribuzione di Windows Autopilot.  |
|  Qual è il pensiero della sostituzione e del ripristino delle parti per la scheda di interfaccia di rete (Network Interface Controller) e il disco? L'hash hardware diventa non valido?   |  Sì.  Se si sostituiscono parti, è necessario raccogliere il nuovo hash hardware, sebbene dipenda da ciò che viene sostituito e dalle caratteristiche delle parti. Se ad esempio si sostituisce il TPM o la scheda madre, si tratta di un nuovo dispositivo ed è necessario avere un nuovo hash hardware. Se si sostituisce una scheda di rete, probabilmente non è un nuovo dispositivo e il dispositivo funzionerà con l'hash hardware precedente.  Tuttavia, come procedura consigliata, è necessario presupporre che l'hash hardware precedente non sia valido e ottenga un nuovo hash hardware dopo le modifiche apportate all'hardware. Questa operazione è consigliata in qualsiasi momento in cui si sostituisce parti. |

## <a name="motherboard-replacement"></a>Sostituzione della motherboard

| Domanda | Risposta |
| --- | --- |
| In che modo Autopilot gestisce gli scenari di sostituzione della scheda madre?  |  La sostituzione della scheda madre è esclusa per l'ambito di Autopilot. Tutti i dispositivi riparati o serviti in modo da modificare la capacità di identificare il dispositivo per Windows Autopilot devono eseguire il normale processo OOBE e selezionare manualmente le impostazioni corrette o applicare un'immagine personalizzata, come nel caso attuale.  <br><br>Per riutilizzare lo stesso dispositivo per Windows Autopilot dopo una sostituzione della scheda madre, è necessario annullare la registrazione del dispositivo da Autopilot, la scheda madre sostituita, una nuova raccolta 4K HH e quindi ripetere la registrazione usando il nuovo hash hardware 4K (o l'ID dispositivo). <br><br>**Nota**: un OEM non sarà in grado di usare l'API diretta OEM per registrare di nuovo il dispositivo, perché l'API diretta OEM accetta solo una tupla o PKID.  In questo caso, l'OEM dovrà inviare le nuove informazioni sull'hash hardware 4K usando un file CSV al cliente e consentire al cliente di registrare nuovamente il dispositivo usando MSfB o Intune.|

## <a name="smbios"></a>SMBIOS

| Domanda | Risposta |
| --- | --- |
| Un requisito specifico per l'UUID di SMBIOS?    | Deve essere univoco come specificato nei requisiti hardware di Windows 10.    |
| Qual è il requisito della tabella SMBIOS per soddisfare le esigenze dell'hash hardware di Windows Autopilot?    | Deve soddisfare tutti i requisiti hardware di Windows 10.  Ulteriori dettagli sono disponibili [qui](https://msdn.microsoft.com/library/jj128256(v=vs.85).aspx).    |
| Se il SMBIOS supporta UUID e il numero di serie, è sufficiente che lo strumento OA3 generi l'hash hardware?    | No.  Come minimo, i campi SMBIOS seguenti devono essere popolati con valori univoci: ProductKeyID SmbiosSystemManufacturer SmbiosSystemProductName SmbiosSystemSerialNumber SmbiosSkuNumber SmbiosSystemFamily MacAddress SmbiosUuid DiskSerialNumber TPM EkPub |

## <a name="technical-interface"></a>Interfaccia tecnica

| Domanda | Risposta |
| --- | --- |
|  Qual è l'interfaccia per ottenere l'indirizzo MAC e il numero di serie del disco? In che modo lo strumento OA ottiene il MAC e il disco seriale #?   | Il numero di serie del disco è stato trovato da IOCTL_STORAGE_QUERY_PROPERTY con StorageDeviceProperty/PropertyStandardQuery.   L'indirizzo MAC di rete è IOCTL_NDIS_QUERY_GLOBAL_STATS da OID_802_3_PERMANENT_ADDRESS.  Tuttavia, il metodo per l'esecuzione di questa operazione varia a seconda dello scenario.  |
| Completamento del chiarimento: se nel sistema sono presenti 2-3 Mac, in che modo lo strumento OA sceglie quali indirizzi MAC e numero di serie del disco si trovano nel sistema perché sono presenti più istanze di ognuna? Se una piattaforma dispone di LAN e WLAN, quale MAC viene scelto?     |  In breve, vengono utilizzati tutti i valori disponibili.  In dettaglio, è possibile che siano presenti regole di utilizzo specifiche. Il numero di serie del disco di sistema è più importante degli altri dischi disponibili. Le interfacce di rete rimovibili non devono essere usate se rilevate quando sono rimovibili. LAN rispetto a WLAN non è rilevante, perché verranno usati entrambi.  |

## <a name="the-end-user-experience"></a>Esperienza dell'utente finale

|Domanda|Risposta|
|----|-----|
|Ricerca per categorie noto che ho ricevuto Autopilot?|È possibile indicare che è stato ricevuto Windows Autopilot (come nel dispositivo è stata ricevuta una configurazione ma non è ancora stato applicato) quando si ignora la pagina di selezione (come illustrato di seguito) e viene immediatamente visualizzata una pagina di accesso generica o personalizzata.|
|Windows Autopilot non funziona, cosa devo fare adesso?| Domande e azioni per semplificare la risoluzione dei problemi: una schermata non viene ignorata?   Un utente si trova come amministratore se configurato per non? Tenere presente che gli amministratori di Azure AD saranno amministratori locali indipendentemente dal fatto che Windows Autopilot sia configurato per disabilitare le informazioni della raccolta amministrativa locale: eseguire licensingdiag.exe e inviare il file CAB (CAB) generato a AutopilotHelp@microsoft.com . Se possibile, raccogliere un ETL da Windows Performance Recorder (WPR). Spesso in questi casi, gli utenti non eseguono l'accesso al tenant di Azure AD appropriato o creano account utente locali.  Per un elenco completo delle opzioni di supporto, vedere [supporto di Windows Autopilot](autopilot-support.md). |
| Se un amministratore apporta modifiche a un profilo esistente, le modifiche avranno effetto sui dispositivi a cui è stato assegnato il profilo che sono già stati distribuiti? |No. I profili di Windows Autopilot non sono residenti nel dispositivo. Vengono scaricate durante la configurazione guidata, vengono applicate le impostazioni definite al momento. Il profilo viene quindi rimosso sul dispositivo. Se viene ricreata l'immagine del dispositivo o viene reimpostata, le nuove impostazioni del profilo diverranno effettive alla successiva esecuzione del dispositivo tramite la configurazione guidata.|
|Qual è l'esperienza se un dispositivo non è registrato o se un amministratore IT non configura Windows Autopilot prima che un utente finale tenti di eseguire la distribuzione automatica? |Se il dispositivo non è registrato, non riceverà l'esperienza di Windows Autopilot e l'utente finale passerà attraverso la configurazione guidata normale. Le configurazioni di Windows Autopilot non verranno applicate finché l'utente non eseguirà di nuovo la configurazione guidata, dopo la registrazione. Se un dispositivo viene avviato prima della creazione di un profilo MDM, il dispositivo passerà attraverso l'esperienza di configurazione guidata standard.  L'amministratore IT dovrà quindi registrare manualmente il dispositivo nella MDM, dopo il quale la volta successiva che il dispositivo verrà reimpostato, passerà attraverso l'esperienza di configurazione guidata di Windows Autopilot.|
|Perché non è stata ricevuta una schermata di accesso personalizzata durante Autopilot? |La personalizzazione del tenant deve essere configurata in portal.azure.com per ricevere un'esperienza di accesso personalizzata.|
|Cosa accade se un dispositivo viene registrato con Azure AD ma non è stato assegnato un profilo di Windows Autopilot?                                |Il normale Azure AD OOBE si verificherà perché al dispositivo non è stato assegnato alcun profilo di Windows Autopilot.|
|Come si raccolgono I log su AUTOPILOT?|Il modo migliore per raccogliere i log sulle prestazioni di Windows Autopilot consiste nel raccogliere una traccia WPR durante la configurazione guidata. Il file XML (estensione WPRP) per questa traccia può essere fornito su richiesta.|

## <a name="mdm"></a>MDM

| Domanda | Risposta |
| --- | --- |
| È necessario usare Intune per la MDM?  |  No, qualsiasi MDM funzionerà con Autopilot, ma altre probabilmente non avranno la stessa suite completa di funzionalità di Windows Autopilot di Intune.  Potrai ottenere la migliore esperienza da Intune. |
| Intune può supportare preinstallazioni di app Win32?  | Sì.  A partire dall'aggiornamento di ottobre di Windows 10 (versione 1809), Intune supporta le app Win32 usando i wrapper MSI (e msix).  |
| Informazioni sulla co-gestione  | La co-gestione è quando si usa una combinazione di uno strumento MDM cloud (Intune) e uno strumento di configurazione locale come Microsoft endpoint Configuration Manager. È sufficiente usare il Configuration Manager se Intune non è in grado di supportare ciò che si vuole fare con il profilo.  Se si sceglie di eseguire la co-gestione usando Intune + Configuration Manager, è necessario includere un agente Configuration Manager nel profilo di Intune. Quando viene effettuato il push del profilo al dispositivo, il dispositivo visualizzerà l'agente Configuration Manager e passerà al Configuration Manager per eseguire il pull delle impostazioni del profilo aggiuntive. |
| È necessario usare Microsoft endpoint Configuration Manager per Windows Autopilot  |  No.  La co-gestione (descritta sopra) è facoltativa. |


## <a name="features"></a>Funzionalità

| Domanda | Risposta |
| --- | --- |
| Modalità di distribuzione automatica  | Una nuova versione di Windows Autopilot in cui l'utente accende solo il dispositivo e nient'altro.  È utile per gli scenari in cui non è necessario un account utente standard, ad esempio dispositivi condivisi o dispositivi KIOSK.  |
| Join Azure Active Directory ibrido  |  Consente ai dispositivi Windows Autopilot di connettersi a un controller di dominio Active Directory locale (oltre a essere Azure AD Uniti). |
| Ripristino di Windows Autopilot  | Rimuove le app e le impostazioni utente da un dispositivo, ma mantiene Azure AD aggiunta a un dominio e la registrazione MDM.  Utile quando si trasferisce un dispositivo da un utente a un altro.  |
| Personalizzazione  | Aggiunge quanto segue all'esperienza OOBE: è possibile creare un messaggio di benvenuto personalizzato. Un hint nome utente può essere aggiunto. il testo della pagina di accesso può essere personalizzato. Il logo della società può essere incluso |
| [Autopilot per dispositivi esistenti](existing-devices.md)  |  Offre un percorso di aggiornamento a Windows Autopilot per tutti i dispositivi basati su Windows 7 e Windows 8 esistenti. |



## <a name="general"></a>Generale

|Domanda|Risposta
|------------------|-----------------|
|Se si cancella il computer e si riavvia, riceverò comunque Windows Autopilot?|Sì, se il dispositivo è ancora registrato per Windows Autopilot ed esegue una versione supportata del canale semestrale di Windows 10, riceverà l'esperienza di Windows Autopilot.|
|È possibile raccogliere l'impronta digitale del dispositivo nei computer esistenti?|Sì, se nel dispositivo è in esecuzione una versione supportata del canale semestrale di Windows 10, è possibile raccogliere le impronte digitali del dispositivo per la registrazione. Non ci sono piani per backporting la funzionalità alle versioni legacy e non è possibile raccoglierli nei dispositivi che eseguono versioni non supportate di Windows.|
|Windows Autopilot è supportato in altri SKU, ad esempio Surface Hub, HoloLens e Windows Mobile.|No, Windows Autopilot non è supportato in altri SKU.|
|Windows Autopilot funziona dopo la reinstallazione di MBR o immagini?|Sì.|
| I computer in cui è stata ricreata l'immagine possono passare attraverso Autopilot? Cosa significa un messaggio di errore che indica che l'utente non è autorizzato a eseguire la registrazione? Codice di errore 801c0003. |Sono previsti limiti per il numero di dispositivi che possono essere registrati da un determinato utente Azure AD Azure AD, nonché il numero di dispositivi supportati per utente in Intune.  (Sono configurabili ma non infinite).  Questa operazione viene eseguita spesso se si riutilizzano i dispositivi o anche se si ripristinano gli snapshot precedenti della macchina virtuale.|
|Cosa accade se un dispositivo viene registrato in un agente malintenzionato?                                                   |Per impostazione predefinita, Windows Autopilot non applica un profilo finché l'utente non accede con il tenant corrispondente per il profilo configurato usando il processo di accesso Azure AD. Il risultato è illustrato di seguito.  Se badguys.com registra un dispositivo di proprietà di contoso.com, nel peggiore dei casi l'utente verrà indirizzato per l'accesso a badguys.com. Quando l'utente immette la posta elettronica o la password, le informazioni di accesso vengono reindirizzate tramite Azure AD alla corretta autenticazione Azure AD e all'utente viene richiesto di accedere a contoso.com. Poiché contoso.com non corrisponde a badguys.com come tenant, il profilo di Windows Autopilot non verrà applicato e verrà eseguita la normale Azure AD OOBE.|
|Dove vengono archiviati i dati di Windows Autopilot?                                                            |I dati di Windows Autopilot vengono archiviati nel Stati Uniti (US), non in un cloud sovrano, anche quando il tenant di Azure AD è registrato in un cloud sovrano. Questa operazione è applicabile a tutti i dati di Windows Autopilot, indipendentemente dal portale sfruttato per la distribuzione di Autopilot.|
|Perché i dati di Windows Autopilot vengono archiviati negli Stati Uniti e non in un cloud sovrano?|Non si tratta di dati del cliente archiviati, ma i dati aziendali che consentono a Microsoft di fornire un servizio, pertanto è accettabile che i dati risiedano negli Stati Uniti. I clienti possono interrompere la sottoscrizione al servizio in qualsiasi momento e, in questo caso, i dati aziendali vengono rimossi da Microsoft.|
|Quanti modi sono disponibili per registrare un dispositivo per Windows Autopilot|Sono disponibili sei modi per registrare un dispositivo, a seconda dell'utente che esegue la registrazione: <br><br>1. API diretta OEM (disponibile solo per TVOs) <br>2. MPC con l'API MPC (deve essere un CSP) <br>3. MPC con caricamento manuale del file CSV nell'interfaccia utente (deve essere un CSP) <br>4. MSfB con il caricamento di file CSV <br>5. Intune che usa il caricamento di file CSV <br>6. Microsoft 365 Business portale con il caricamento di file CSV|
|Quanti modi sono disponibili per creare un profilo di Windows Autopilot?|Esistono quattro modi per creare e assegnare un profilo di Windows Autopilot: <br><br>1. tramite MPC (deve essere un CSP) <br>da 2 a MSfB <br>3. tramite Intune (o un altro MDM) <br>4. portale di Microsoft 365 Business <br><br>Microsoft consiglia di creare e assegnare profili tramite Intune.  |
| Quali sono le cause più comuni degli errori di registrazione? |1. le voci hash hardware errate o mancanti possono causare tentativi di registrazione difettosi <br>2. caratteri speciali nascosti nei file CSV.  <br><br>Per evitare questo problema, dopo aver creato il file CSV aprirlo nel blocco note per cercare i caratteri nascosti o gli spazi finali o altri danneggiamenti.|
|  Autopilot è supportato nei dispositivi Internet? |  Autopilot non è supportato nei dispositivi Core di Internet delle cose e non è attualmente disponibile alcun piano per aggiungere questo supporto. Autopilot è supportato sui dispositivi SAC di Windows 10. Autopilot è supportato in Windows 10 Enterprise LTSC 2019 e versioni successive. non è supportata nelle versioni precedenti di LTSC.|
|  Autopilot è supportato in tutte le aree/paesi? |  Autopilot supporta solo i clienti che usano Azure globale. Azure globale non include le tre entità elencate di seguito:<br>-Azure Germania <br>-Azure Cina 21Vianet<br>-Azure per enti pubblici<br>Quindi, se un cliente è configurato in Azure globale, non sono previste restrizioni relative all'area. Se, ad esempio, contoso USA Azure globale ma i dipendenti lavorano in Cina, i dipendenti di Contoso che lavorano in Cina potranno usare Autopilot per distribuire i dispositivi. Se contoso USA Azure Cina 21Vianet, i dipendenti di Contoso non saranno in grado di usare Autopilot.|

## <a name="glossary"></a>Glossario

| Termine | Significato |
| --- | --- |
| CSV  | Valori delimitati da virgole (tipo di file simile a foglio di calcolo di Excel)  |
| MPC  | Microsoft Partner Center   |
| MDM  | Gestione dei dispositivi mobili   |
| OEM  | Produttore attrezzature originale   |
| CSP  |  Provider di soluzioni cloud  |
| MSfB  | Microsoft Store per le aziende   |
| Azure AD  | Azure Active Directory   |
| HH 4K  |  hash hardware 4K |
| CBR  | Report compilazione computer  |
| EC  |  Commercio aziendale  |
| DDS  | Servizio directory dispositivo    |
| OOBE  | Esperienza predefinita   |
| UUID  | Identificatore univoco universale   |