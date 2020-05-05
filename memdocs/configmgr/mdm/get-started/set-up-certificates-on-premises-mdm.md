---
title: Certificati per MDM locale
titleSuffix: Configuration Manager
description: Configurare i certificati per le comunicazioni attendibili con la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724665"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Configurare i certificati per le comunicazioni attendibili con MDM locale

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager gestione di dispositivi mobili (MDM) locale richiede la configurazione dei ruoli del sistema del sito per le comunicazioni attendibili con i dispositivi gestiti. Sono necessari due tipi di certificati:

- Un **certificato del server Web** in IIS nei server che ospitano i ruoli del sistema del sito richiesti. Se un server ospita più ruoli del sistema del sito, è necessario solo un certificato per tale server. Se ogni ruolo si trova in un server separato, per ogni server è necessario un certificato separato.

- Il **certificato radice attendibile** dell'autorità di certificazione (CA) che emette i certificati del server Web. Installare questo certificato radice in tutti i dispositivi che devono connettersi ai ruoli del sistema del sito.

Per i dispositivi aggiunti a un dominio, se si usa Active Directory Servizi certificati, può installare automaticamente questi certificati in tutti i dispositivi. Per i dispositivi non aggiunti a un dominio, installare il certificato radice attendibile in altri modi.

Per i dispositivi registrati in blocco, è possibile includere il certificato nel pacchetto di registrazione. Per i dispositivi registrati dagli utenti, è necessario aggiungere il certificato tramite posta elettronica, download Web o altro metodo.

Se si usa una CA pubblica nota, ad esempio VeriSign o GoDaddy, per emettere i certificati del server, è possibile evitare di dover installare manualmente il certificato radice attendibile in ogni dispositivo. La maggior parte dei dispositivi considera attendibili in modo nativo queste autorità pubbliche. Questo metodo è un'alternativa utile per i dispositivi registrati dall'utente, invece di installare il certificato in altri modi.

> [!IMPORTANT]  
> Esistono diversi modi per configurare i certificati per le comunicazioni attendibili tra i dispositivi e i server del sistema del sito per MDM locale. Le informazioni contenute in questo articolo sono un esempio di un modo per eseguire questa operazione. Questo metodo richiede Active Directory Servizi certificati, con un'autorità di certificazione e il ruolo registrazione Web autorità di certificazione. Per ulteriori informazioni, vedere [Servizi certificati Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>Pubblicare il CRL

Per impostazione predefinita, l'autorità di certificazione Active Directory (CA) USA gli elenchi di revoche di certificati (CRL) basati su LDAP. Consente le connessioni al CRL per i dispositivi aggiunti a un dominio. Per consentire ai dispositivi non aggiunti a un dominio di considerare attendibili i certificati emessi dall'autorità di certificazione, aggiungere un CRL basato su HTTP.

1. Nel server che esegue l'autorità di certificazione per il sito, andare al menu **Start** , selezionare **strumenti di amministrazione**e scegliere **autorità di certificazione**.

1. Nella console autorità di certificazione fare clic con il pulsante destro del mouse su **CertificateAuthority**e quindi scegliere **Proprietà**.

1. In proprietà di CertificateAuthority passare alla scheda **estensioni** . Assicurarsi che **Seleziona estensione** sia impostato su punto di **distribuzione CRL (CDP)**.

1. Selezionare `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. Quindi selezionare le opzioni seguenti:

    - **Includi nei CRL. i client lo usano per trovare i percorsi Delta CRL.**

    - **Includi nell'estensione dei punti di distribuzione dei certificati emessi.**

    - **Includi nell'estensione IDP dei CRL rilasciati**

1. Passare alla scheda **uscita modulo** . Selezionare **Proprietà**, quindi selezionare **Consenti la pubblicazione di certificati nel file System**. Verrà visualizzato un avviso per riavviare Active Directory Servizi certificati.

1. Fare clic con il pulsante destro del mouse su **certificati revocati**, selezionare **tutte le attività**, quindi scegliere **pubblica**.

1. Nella finestra Publish CRL selezionare **solo Delta CRL**e quindi fare clic su **OK** per chiudere la finestra.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Creare il modello di certificato

La CA USA il modello di certificato del server Web per rilasciare i certificati per i server che ospitano i ruoli del sistema del sito. Questi server saranno endpoint SSL per le comunicazioni attendibili tra i ruoli del sistema del sito e i dispositivi registrati.

1. Creare un gruppo di sicurezza di dominio denominato **ConfigMgr MDM Servers**. Aggiungere al gruppo gli account computer dei server del sistema del sito.

1. Nella console autorità di certificazione fare clic con il pulsante destro del mouse su **modelli di certificato**e scegliere **Gestisci**. Questa azione carica la console modelli di certificato.

1. Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce che visualizza **server Web** nella colonna **nome visualizzato modello** , quindi scegliere **Duplica modello**.

1. Nella finestra **modello duplicato** selezionare **Windows 2003 Server, Enterprise edition** o **Windows 2008 Server, Enterprise Edition**, quindi fare clic su **OK**.

    > [!TIP]
    > Configuration Manager supporta i modelli di certificato server Windows 2008, noti anche come certificati V3 o Cryptography: Next Generation (CNG). Per altre informazioni, vedere [Panoramica dei certificati CNG](../../core/plan-design/network/cng-certificates-overview.md).

    Se la CA viene eseguita in Windows Server 2012 o versioni successive, in questa finestra non viene visualizzata l'opzione per la versione del modello di certificato. Dopo aver duplicato il modello, selezionare la versione nella scheda **compatibilità** delle proprietà del modello.

1. Nella finestra **Proprietà nuovo modello** , nella scheda **generale** , immettere un nome di modello. La CA USA questo nome per generare i certificati Web che verranno usati nei sistemi del sito Configuration Manager. Ad esempio, digitare **ConfigMgr MDM Web Server**.

1. Passare alla scheda **nome soggetto** e selezionare **Compila da Active Directory informazioni**. Per il formato del nome soggetto, specificare il **nome DNS**. Se si seleziona **nome entità utente (UPN)** , disabilitare l'opzione per nome soggetto alternativo.

1. Passare alla scheda **sicurezza** .

    1. Rimuovere l'autorizzazione **registrazione** dai gruppi di sicurezza **Domain Admins** ed **Enterprise Admins** .

    1. Selezionare **Aggiungi**e immettere il nome del gruppo di sicurezza. Ad esempio, **ConfigMgr MDM Servers**. Selezionare **OK** per chiudere la finestra.

    1. Selezionare l'autorizzazione **registrazione** per questo gruppo. Non rimuovere l'autorizzazione di **lettura** .

1. Selezionare **OK** per salvare le modifiche e chiudere la console modelli di certificato.

1. Nella console autorità di certificazione fare clic con il pulsante destro del mouse su **modelli di certificato**, selezionare **nuovo**, quindi scegliere **modello di certificato da emettere**.

1. Nella finestra **Abilita modelli di certificato** selezionare il nuovo modello. Ad esempio, il **server Web MDM ConfigMgr**. Fare quindi clic su **OK** per salvare e chiudere la finestra.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Richiedere il certificato

Questo processo descrive come richiedere il certificato del server Web per IIS. Eseguire questo processo per ogni server del sistema del sito che ospita uno dei ruoli per MDM locale.

1. Nel server di sistema del sito che ospita uno dei ruoli, aprire un prompt dei comandi come amministratore. Immettere `mmc` per aprire una console di gestione di Microsoft vuota.

1. Nella finestra della console passare al menu **file** e selezionare **Aggiungi/Rimuovi snap-in**.

    1. Scegliere **certificati** dall'elenco di snap-in disponibili e selezionare **Aggiungi**.

    1. Nella finestra snap-in certificati scegliere **account computer**. Selezionare **Avanti**, quindi fare clic su **fine** per gestire il computer locale.

    1. Fare clic su **OK** per uscire dalla finestra Aggiungi o Rimuovi snap-in.

1. Espandere **certificati (computer locale)** e selezionare l'archivio **personale** . Andare al menu **azione** , selezionare **tutte le attività**e scegliere **Richiedi nuovo certificato**. Questa azione comunica con Active Directory Servizi certificati per creare un nuovo certificato usando il modello creato in precedenza.

    1. Nella pagina prima di iniziare della procedura guidata di registrazione del certificato selezionare **Avanti**.

    1. Nella pagina Seleziona criteri di registrazione certificato selezionare **Active Directory criterio di registrazione**e quindi fare clic su **Avanti**.

    1. Selezionare il modello di certificato del server Web (**server Web MDM ConfigMgr**), quindi selezionare **registra**.

    1. Dopo aver richiesto il certificato, fare clic su **fine**.

Ogni server necessita di un certificato server Web univoco. Ripetere questo processo per ogni server che ospita uno dei ruoli del sistema del sito richiesti. Se un server ospita tutti i ruoli del sistema del sito, è sufficiente richiedere un certificato del server Web.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Associare il certificato

Il passaggio successivo consiste nell'associare il nuovo certificato al server Web. Seguire questa procedura per ogni server che ospita i ruoli del sistema del sito del punto di *registrazione* e del *punto proxy di registrazione* . Se un server ospita tutti i ruoli del sistema del sito, è necessario eseguire questo processo una sola volta.

> [!NOTE]
> Non è necessario eseguire questo processo per i ruoli del sistema del sito del punto di distribuzione e del punto di gestione dei dispositivi. Ricevono automaticamente il certificato richiesto durante la registrazione.

1. Nel server che ospita il punto di registrazione o il punto proxy di registrazione, andare al menu **Start** , selezionare strumenti di **Amministrazione**e quindi **Gestione IIS**.

1. Nell'elenco delle connessioni selezionare il **sito Web predefinito**, quindi selezionare **Modifica binding**.

    1. Nella finestra Binding sito selezionare **https**, quindi scegliere **modifica**.

    1. Nella finestra Modifica binding sito selezionare il certificato appena registrato per il **certificato SSL**. Selezionare **OK** per salvare, quindi fare clic su **Chiudi**.

1. Nell'elenco delle connessioni della console Gestione IIS selezionare il server Web. Nel pannello azione sul lato destro selezionare **Riavvia**. Questa azione riavvia il servizio server Web.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Esportare il certificato radice attendibile

Active Directory Servizi certificati installa automaticamente il certificato richiesto dalla CA in tutti i dispositivi aggiunti a un dominio. Per ottenere il certificato necessario per i dispositivi non aggiunti a un dominio per comunicare con i ruoli del sistema del sito, esportarlo dal certificato associato al server Web.

1. In Gestione IIS selezionare il **sito Web predefinito**. Nel pannello azione sul lato destro selezionare **Binding**.

1. Nella finestra Binding sito selezionare **https**, quindi fare clic su **modifica**.

1. Selezionare il certificato del server Web e selezionare **Visualizza**.

1. In proprietà del certificato del server Web passare alla scheda **percorso certificazione** . Selezionare la radice del percorso di certificazione e selezionare **Visualizza certificato**.

1. Nelle proprietà del certificato radice passare alla scheda **Dettagli** , quindi selezionare **copia su file**.

1. Nella pagina iniziale dell'esportazione guidata certificati selezionare **Avanti**.

1. Selezionare il **formato binario codificato der X. 509 (. CER)** come formato e selezionare **Avanti**.

1. Immettere un percorso e un nome file per identificare il certificato radice attendibile. Per nome file, fare clic su **Sfoglia**, scegliere un percorso in cui salvare il file del certificato, assegnare un nome al file e selezionare **Avanti**.

1. Verificare le impostazioni e fare clic su **fine** per esportare il certificato in un file.

A seconda della progettazione dell'autorità di certificazione, potrebbe essere necessario esportare ulteriori certificati radice della CA subordinata. Ripetere questo processo per esportare gli altri certificati nel percorso di certificazione del certificato del server Web.

## <a name="next-step"></a>Passaggio successivo

> [!div class="nextstepaction"]
> [Impostare la registrazione dei dispositivi](set-up-device-enrollment-on-premises-mdm.md)
