---
title: Funzionalità nella Technical Preview 1604
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1604 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ef37b5f99cda8022166972cdc015a3c60d0458a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705629"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1604 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1604. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.  

 Di seguito sono riportate le nuove funzionalità disponibili con questa versione.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a> Gestire le app acquistate con Volume Purchase Program da Windows Store per le aziende  
 In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app per l'organizzazione, singolarmente o con Volume Purchase Program. Connettendo lo Store a Configuration Manager, è possibile gestire le app acquistate con Volume Purchase Program dalla console di Configuration Manager, ad esempio:  

-   È possibile sincronizzare l'elenco di app acquistate con Configuration Manager  

-   Le app sincronizzate vengono visualizzate nella console di Configuration Manager e possono essere distribuite come qualsiasi altra app  

-   È possibile tenere traccia del numero di licenze disponibili e del numero di licenze in uso nella console di Configuration Manager  

### <a name="try-it-out"></a>Verifica  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Scenario 1: Configurare la sincronizzazione di Windows Store per le aziende  

1.  In Azure Active Directory registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web". Si riceverà un ID client che sarà necessario in seguito.  

    1.  Nel nodo **Active Directory** di [https://manage.windowsazure.com](https://manage.windowsazure.com) selezionare Azure Active Directory, quindi fare clic su **Applicazioni** > **Aggiungi**.  

    2.  Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.  

    3.  Immettere un nome per l'applicazione, selezionare **Applicazione Web** e/o **API Web** e quindi fare clic sulla freccia Avanti.  

    4.  Immettere lo stesso URL per **URL accesso** e **URI ID app**.  L'URL può essere di qualsiasi tipo e non è necessario che venga risolto in un indirizzo reale. Ad esempio è possibile immettere **https://&lt;dominioutente\>/sccm**.  

    5.  Completare la procedura guidata.  

2.  In Azure Active Directory creare una chiave client per lo strumento di gestione registrato.  

    1.  Evidenziare l'applicazione appena creata e fare clic su **Configura**.  

    2.  In **Chiavi** selezionare una durata nell'elenco e fare clic su **Salva**.  Verrà creata una nuova chiave client.  Non uscire dalla pagina fino a quando non è stato completato il caricamento di Windows Store per le aziende in Configuration Manager.  

3.  In Windows Store per le aziende configurare Configuration Manager come strumento di gestione dello Store.  

    1.  Aprire [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) ed eseguire l'accesso, se richiesto.  

    2.  Accettare le condizioni per l'utilizzo, se necessario.  

    3.  In **Management Tools** fare clic su **Add a management tool**.  

    4.  In **Search for the tool by name** digitare il nome dell'applicazione creata in precedenza in AAD e quindi fare clic su **Add**.  

    5.  Fare clic su **Activate** accanto all'applicazione appena importata.  

    6.  Nella procedura guidata **Show Offline-Licensed app** fare clic su **Yes** se si vuole consentire l'acquisto di applicazioni con licenza offline.  

4.  Acquistare almeno un'app da Windows Store per le aziende.  

5.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Windows Store per le aziende**.  

6.  Nel gruppo **Crea** della scheda **Home** fare clic su **Aggiungere un account di Windows Store per le aziende**.  

7.  Aggiungere l'ID tenant, l'ID client e la chiave client da Azure Active Directory, quindi completare la procedura guidata.  

8.  Al termine verrà visualizzato l'account configurato nell'elenco degli **account di Windows Store per le aziende** nella console di Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Scenario 2: Creare e distribuire un'applicazione di Configuration Manager da un archivio di Windows per app aziendali con licenza offline  

1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.  

2.  L'elenco delle **app di Windows Store per le aziende acquistate** mostra le applicazioni che sono state sincronizzate dall'archivio. Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.  

3.  Viene creata un'applicazione di Configuration Manager contenente l'archivio di Windows per l'applicazione aziendale. È quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a> Miglioramenti della gestione di Microsoft Passport for Work  
 È ora possibile distribuire criteri di Passport for Work a dispositivi Windows 10 aggiunti a un dominio gestiti dal client di Configuration Manager.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a> Opzione per il passaggio dei client a un nuovo punto di aggiornamento software  
 Nella versione Technical Preview 1604 è possibile abilitare l'opzione per consentire ai client di Configuration Manager di passare a un nuovo punto di aggiornamento software quando si verificano problemi con il punto di aggiornamento software attivo. Per questa opzione, è necessario che siano disponibili più punti di aggiornamento software in un sito primario. Questa opzione viene abilitata in una raccolta di dispositivi e, una volta abilitata, i client della raccolta cercheranno un altro punto di aggiornamento software nell'analisi successiva quando il client non riuscirà a connettersi al punto di aggiornamento software attivo. A seconda delle impostazioni di configurazione di WSUS (Windows Server Update Services), ad esempio classificazioni degli aggiornamenti, prodotti e così via, il passaggio a un nuovo punto di aggiornamento software può generare traffico di rete aggiuntivo. È quindi consigliabile usare questa opzione solo quando è necessario.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Per abilitare l'opzione per il passaggio tra punti di aggiornamento software  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità > Panoramica > Raccolte dispositivi**.  

2.  Nel gruppo **Raccolta** della scheda **Home** fare clic su **Notifica client**e quindi su **Passare al punto di aggiornamento software successivo**.  

> [!NOTE]  
>  Questa opzione è disponibile solo per i siti con più punti di aggiornamento software.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a> Impostazioni client per gestire le impostazioni della cache del client e la peer cache del client  
 Nella Technical Preview versione 1604 vengono introdotte due nuove impostazioni client dei dispositivi che influiscono sull'uso della cache del client. Entrambe le impostazioni possono essere usate singolarmente, ma vengono configurate nella stessa finestra delle proprietà per le impostazioni client e usate un combinazione offrono supporto per la gestione della distribuzione di contenuti ai client in posizioni remote.  

-   La prima impostazione riguarda la **peer cache del client**, una soluzione Configuration Manager integrata che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale. Per poter condividere i contenuti, i client con peer cache devono essere membri dello stesso gruppo di limiti. La peer cache non sostituisce l'uso di altre soluzioni come BracnchCache, ma si affianca a esse per offrire più opzioni che estendono le soluzioni di distribuzione di contenuti tradizionali quali i punti di distribuzione.  

     Dopo aver distribuito le impostazioni client che abilitano la peer cache a una raccolta, i membri di tale raccolta possono fungere da origine di contenuto peer per altri client nel suo gruppo limite.  Il client che agisce come origine di contenuto peer invia un elenco di contenuti disponibili che ha memorizzato nella cache al suo punto di gestione. Quindi, quando il client successivo in tale gruppo limite richiede quel contenuto, l'origine peer cache viene offerta come potenziale origine di contenuto insieme a tutti i punti di distribuzione configurati per essere veloci. Il client seleziona un'origine di contenuto casuale da questo pool combinato di origini di contenuto. I client cercheranno il contenuto da un punto di distribuzione configurato per essere lento solo quando nel gruppo limite non sono presenti punti di distribuzione rapidi o origini peer cache.  

-   La seconda nuova impostazione consente di **gestire le dimensioni della cache** nei client. È possibile impostare la dimensione massima per la cache in megabyte o come percentuale dello spazio su disco del client.  Il client applica l'impostazione che viene raggiunta prima.  

Per capire come viene usata la peer cache, è possibile visualizzare il dashboard delle **origini dati client**. Nella console passare a **Monitoraggio > Stato client > Origini dati del client**. In questa posizione è possibile selezionare un periodo di tempo da applicare al dashboard. Nella visualizzazione è quindi possibile selezionare il gruppo di limiti o il pacchetto per il quale visualizzare le informazioni. Quando si esaminano le informazioni, passare il puntatore sulla superficie per vedere altri dettagli relativi ai diversi contenuti o origini dei criteri.  

 È anche possibile usare un nuovo report, **Origini dati client - Riepilogo**, per visualizzare un riepilogo delle origini dati client per ogni gruppo limite.   
**Requisiti per l'uso della peer cache:**  

-   È necessario configurare il sito con un **Account di accesso alla rete** con **Controllo completo** per la cartella della cache in ogni client. Per impostazione predefinita, si tratta di **%windir%\ccmcache**  

-   I client possono trasferire il contenuto usando la peer cache solo quando sono membri dello stesso gruppo di limiti.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Per configurare le impostazioni del client relative alla peer cache del client  

1.  Entrambe le impostazioni vengono configurate nella stessa pagina delle impostazioni del client. Nella console di Configuration Manager passare ad **Amministrazione > Impostazioni client** e aprire l'oggetto impostazioni client del dispositivo che si desidera usare. È possibile anche modificare l'oggetto Impostazioni client predefinite.  

2.  Nell'elenco delle impostazioni disponibili selezionare **Impostazioni della cache del client**.  

3.  Per gestire la dimensione della cache impostare **Configurare le dimensioni della cache del client** su **Sì**. È quindi possibile configurare la dimensione massima della cache sia in megabyte sia come percentuale dello spazio su disco dei client.  

4.  Per consentire ai client di partecipare alla peer cache del client, impostare **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti** su **Sì**. È quindi possibile configurare le porte utilizzate dai client, incluso il fatto se saranno HTTP o HTTPS.  

### <a name="try-it-out"></a>Verifica  
 Provare a completare le attività seguenti e quindi usare il collegamento per l'invio di commenti e suggerimenti nella parte superiore di questo argomento per comunicare i risultati:  

1.  Modificare le impostazioni client per specificare una nuova dimensione per la cache client e quindi confermare questa impostazione su un computer client.  

2.  Usare le impostazioni client per configurare più client per l'uso della peer cache  

3.  Distribuire contenuti nei client in modo che alcuni o tutti i client ottengano i contenuti da un altro client usando la peer cache.  È possibile verificare l'origine contenuto in uso visualizzando il nuovo dashboard.  

    > [!NOTE]  
    >  Per completare questa attività con la Technical Preview e un singolo punto di distribuzione, configurare il punto di distribuzione in modo che sia lento per il percorso di rete di tutti i client. Distribuire quindi i contenuti in un singolo client.  Dopo che il client ha ottenuto i contenuti, è possibile distribuirli in altri client che devono trovare peer locali da usare come origine contenuto prima di ricorrere al punto di distribuzione considerato lento dal percorso del client.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a> Supporto per Passport for Work come provider di archiviazione chiavi  
 Configuration Manager consente di eseguire l'integrazione con Microsoft Passport for Work, un metodo di accesso alternativo che usa Active Directory o un account Azure Active Directory per sostituire una password, una smart card o una smart card virtuale.  
Passport consente di eseguire l'accesso usando un movimento dell'utente invece di una password. Un movimento dell'utente può essere un PIN semplice, l'autenticazione biometrica come Windows Hello o un dispositivo esterno come un lettore di impronte digitali.  

-   È possibile usare Configuration Manager per controllare i movimenti che gli utenti possono usare o meno per accedere, nonché per configurare i requisiti di complessità dei PIN.  

-   È possibile archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Passport for Work.  

Quando un utente crea un PIN di Passport, Windows invia una notifica per la quale Configuration Manager è in ascolto.  Ciò consente a Configuration Manager di venire rapidamente a conoscenza di quali utenti hanno creato un PIN di Passport. Configuration Manager può quindi anche rilasciare nuovi certificati a tali utenti se Passport viene usato come provider di archiviazione chiavi in un profilo di certificato.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a> Attestazione dell'integrità del dispositivo locale  
 L'attestazione dell'integrità per i dispositivi Windows 10 può ora essere configurata per comunicare usando l'infrastruttura locale.  Gli amministratori possono specificare se la creazione di report avviene tramite risorse cloud o locali.  Se è selezionata l'opzione **locale** per la creazione dei report di attestazione dell'integrità, è possibile specificare un URI per il servizio. In questo modo i PC client senza accesso a Internet possono usare, abilitare e gestire i dispositivi usando l'attestazione dell'integrità.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Abilitare l'attestazione dell'integrità per i dispositivi locali  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Impostazioni client**e quindi impostare **Usare il servizio di attestazione dell'integrità locale** su **Sì**.  

2.  Specificare l' **URL del servizio di attestazione dell'integrità locale**e quindi fare clic su **OK**.  

Per provare, configurare il servizio di attestazione dell'integrità locale usando le impostazioni agente client.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a> Impostazione di Smart Lock per dispositivi Android  
 È stata aggiunta una nuova impostazione, **Consenti Smart Lock e altri agenti di attendibilità**, all'elemento di configurazione **Android e Samsung KNOX** che consente di controllare la funzionalità Smart Lock sui dispositivi Android compatibili. Questa funzionalità del telefono, talvolta nota anche come agenti di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile, ad esempio quando è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti finali di configurare Smart Lock.  
