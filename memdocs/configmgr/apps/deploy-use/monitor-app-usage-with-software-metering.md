---
title: Monitorare l'utilizzo delle app con la misurazione del software
titleSuffix: Configuration Manager
description: Informazioni sulle operazioni disponibili per la misurazione del software in Configuration Manager.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689249"
---
# <a name="software-metering-in-configuration-manager"></a>Misurazione del software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni di riferimento per tutte le operazioni eseguibili quando si usa la misurazione del software di Configuration Manager.

> [!IMPORTANT]
>  Il controllo del software viene usato per monitorare le app desktop in PC Windows con un nome di file che termina con **.exe**. La misurazione del software non consente di monitorare app di Windows moderne, come quelle usate da Windows 8.

##  <a name="prerequisites-for-software-metering"></a>Prerequisiti per il controllo del software
Il controllo del software non ha dipendenze esterne, ma solo dipendenze all'interno del prodotto.

|Dipendenza|Altre informazioni|
|----------------|----------------------|
|Impostazioni client per il controllo del software|Per usare il controllo del software, l'impostazione client **Abilitare controllo software nei client** deve essere abilitata e distribuita nei computer. È possibile distribuire le impostazioni di controllo del software a tutti i computer nella gerarchia oppure distribuire impostazioni personalizzate a gruppi di computer. Vedere **Configurare il controllo del software** in questo argomento.|
|Punto di Reporting Services.|Prima di poter visualizzare i report di controllo del software, è necessario configurare un punto di Reporting Services. Per altre informazioni, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Configurare il controllo del software
 Questa procedura consente di configurare le impostazioni client predefinite per il controllo del software e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e distribuirla in una raccolta contenente i computer in cui si vuole usare il controllo del software. Per altre informazioni su come creare le impostazioni personalizzate del dispositivo, vedere [Configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).

1. Nella console di Configuration Manager fare clic su **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.

2. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.

3. Nella finestra di dialogo **Impostazioni predefinite** fare clic su **Controllo del software**.

4. Nell'elenco **Impostazioni dispositivo** configurare le impostazioni seguenti:

   -   **Abilitare controllo software nei client**: selezionare **True** per abilitare la misurazione del software.

   -   **Pianifica raccolta dati**: configurare la frequenza con cui verranno raccolti i dati dalla misurazione del software nei computer client. Usare il valore predefinito **7 giorni** oppure fare clic su **Pianifica** per configurare una pianificazione personalizzata.

5. Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni dispositivo** .

   I computer client vengono configurati con queste impostazioni al successivo download dei criteri client. Per iniziare il recupero dei criteri per un singolo client, vedere [Gestire i client](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a>Creare regole di controllo software
 Usare la Creazione guidata regola controllo software per creare una nuova regola di controllo software per il sito di Configuration Manager.

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Controllo software**.

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea regola di controllo software**.

4.  Nella pagina **Generale** della Creazione guidata regola controllo software specificare le informazioni seguenti:

    -   **Nome** - Nome della regola di controllo software. Deve essere univoco e descrittivo.

        > [!NOTE]
        >  Le regole di controllo software possono avere lo stesso nome se il nome di file contenuto nelle regole è diverso.

    -   **Nome file** - Nome del file di programma da controllare. È possibile fare clic su **Sfoglia** per visualizzare la finestra di dialogo **Apri** in cui è possibile selezionare il file di programma da usare.

        > [!NOTE]
        >  Se si digita il nome del file eseguibile nella casella **Nome file** , non vengono effettuati controlli per determinare se il file esiste già o se contiene le informazioni di intestazione necessarie. Quando possibile, fare clic su **Sfoglia** e selezionare il file eseguibile da controllare.
        >
        >  I caratteri jolly non sono consentiti nel nome di file.
        >
        >  Questa casella è facoltativa se si specifica un valore per **Nome file originale** .

    -   **Nome file originale** - Nome del file eseguibile da controllare. Questo nome corrisponde alle informazioni nell'intestazione del file, e non al nome del file stesso, quindi può essere utile nei casi in cui il file eseguibile è stato rinominato ma si vuole controllarlo in base al nome originale.

        > [!NOTE]
        >  I caratteri jolly non sono consentiti nel nome di file originale.
        >
        >  Questa casella è facoltativa se si specifica un valore per **Nome file** .

    -   **Versione** - Versione del file eseguibile da controllare. È possibile usare il carattere jolly (&#42;) per rappresentare qualsiasi stringa di caratteri o il carattere jolly (? ) per rappresentare qualsiasi carattere singolo. Per controllare tutte le versioni di un file eseguibile, usare il valore predefinito (&#42;).

    -   **Lingua** - Lingua del file eseguibile da controllare. Il valore predefinito corrisponde alle impostazioni locali correnti del sistema operativo in uso. Se si seleziona un file eseguibile da controllare facendo clic sul pulsante **Sfoglia** , questa casella viene compilata automaticamente se sono presenti informazioni sulla lingua nell'intestazione del file. Per controllare tutte le versioni localizzate di un file, selezionare **Qualsiasi** nell'elenco a discesa.

    -   **Descrizione** - Descrizione facoltativa della regola di controllo software.

    -   **Applica questa regola di controllo software ai client seguenti** - Selezionare se si desidera applicare la regola di controllo software a tutti i client nella gerarchia o ai client assegnati al sito specificato nell'elenco **Sito** .

5.  Per continuare, fare clic su **Avanti**.

6.  Verificare e confermare le impostazioni, quindi completare la procedura guidata per creare la regola di controllo software. La nuova regola di controllo software viene visualizzata nel nodo **Controllo del software** dell'area di lavoro **Asset e conformità** .

##  <a name="configure-automatic-software-metering-rules"></a>Configurare regole di controllo software automatiche
 È possibile configurare il controllo del software in Configuration Manager per generare automaticamente regole di controllo software disabilitate dai dati di inventario di utilizzo recenti disponibili nel database del sito. È possibile configurare questi dati di inventario in modo che le regole di controllo software vengano create solo per le applicazioni usate in una percentuale specificata di computer. È anche possibile specificare il numero massimo di regole di controllo software generate automaticamente consentite nel sito.

> [!NOTE]
>  Per impostazione predefinita, le regole di controllo software create automaticamente sono disabilitate. Prima di poter iniziare a raccogliere dati di utilizzo con queste regole, è necessario abilitarle.

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Controllo software** e quindi nella scheda **Home** fare clic su **Proprietà di controllo software** nel gruppo **Impostazioni**.

3.  Nella finestra di dialogo **Proprietà di controllo software** configurare le impostazioni seguenti:

    -   **Conservazione dati (in giorni)** - Specifica la quantità di tempo per cui vengono conservati nel database del sito i dati generati dalle regole di controllo software. Il valore predefinito è **90** giorni.

    -   Abilitare l'opzione **v**.

    -   **Specificare la percentuale di computer nella gerarchia che deve utilizzare un programma prima che venga creata automaticamente una regola di controllo software** - Il valore predefinito è **10** %.

    -   **Specificare il numero di regole di controllo software che deve essere superato nella gerarchia prima che venga disabilitata la creazione automatica delle regole** - Il valore predefinito è **100** regole.

4.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà di controllo software** .

##  <a name="manage-software-metering-rules"></a>Gestire le regole di controllo software
 Nell'area di lavoro **Asset e conformità** selezionare **Controllo del software**, selezionare la regola di controllo software da gestire e quindi selezionare un'attività di gestione.

 Per altre informazioni sulle attività di gestione che potrebbero richiedere alcune informazioni prima della relativa selezione, usare la seguente tabella.

|Attività di gestione|Dettagli|
|---------------------|-------------|
|**Abilita**<br /><br /> **Disabilita**|Abilita o disabilita una regola di controllo software. Questa impostazione viene scaricata nei computer client in base all'intervallo specificato in **Intervallo di polling dei criteri client** nella sezione **Criteri client** delle impostazioni del client (per impostazione predefinita, ogni 60 minuti).<br /><br /> Vedere [Configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).|

##  <a name="monitor-software-metering"></a>Monitorare il controllo del software
 Il controllo del software in Configuration Manager include vari report incorporati che consentono di monitorare le informazioni sulle operazioni di controllo del software. Tali report dispongono della categoria report di **Controllo del software**.

 Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Introduzione ai report](../../core/servers/manage/introduction-to-reporting.md).

 È anche possibile creare query e raccolte in base ai dati archiviati nel database di Configuration Manager dal controllo del software.

 Per altre informazioni sulle raccolte in Configuration Manager, vedere [Introduzione alle raccolte](../../core/clients/manage/collections/introduction-to-collections.md).

 Per altre informazioni sulle query in Configuration Manager, vedere [Introduzione alle query](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Sicurezza e privacy per il controllo del software

### <a name="security-issues-for-software-metering"></a>Problemi di sicurezza per il controllo del software
 Un utente malintenzionato potrebbe inviare informazioni di controllo del software non valide a Configuration Manager e tali informazioni verranno accettate dal punto di gestione anche quando l'impostazione del client di controllo del software è disabilitata. Ciò potrebbe comportare la replica di un numero elevato di regole di controllo in tutta la gerarchia, causando un attacco Denial of Service nella rete e nei server del sito di Configuration Manager.

 Poiché un utente malintenzionato può creare dati di controllo del software non validi, non considerare autorevoli le informazioni di controllo del software.

 Il controllo del software è abilitato per impostazione predefinita come impostazione client.

###  <a name="privacy-information-for-software-metering"></a>Informazioni sulla privacy per il controllo del software
 Il controllo software esegue il monitoraggio dell'utilizzo delle applicazioni nei computer client. Il controllo del software è abilitato per impostazione predefinita. È necessario configurare le applicazioni da controllare. Le informazioni di controllo del software sono archiviate nel database di Configuration Manager. Le informazioni vengono crittografate durante il trasferimento a un punto di gestione, ma non vengono archiviate in forma crittografata nel database di Configuration Manager.

 Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione **Elimina dati di controllo software obsoleti** (ogni 5 giorni) ed **Elimina dati di riepilogo di controllo software obsoleti** (ogni 270 giorni). È possibile configurare l'intervallo di eliminazione. Le informazioni relative al controllo non vengono inviate a Microsoft.

 Prima di configurare il controllo del software, considerare i requisiti sulla privacy.

## <a name="example-scenario-for-using-software-metering"></a>Scenario di esempio per l'uso della misurazione del software
 In questa sezione si creerà un regola di misurazione del software che consente di risolvere i dubbi sui requisiti aziendali seguenti:

- Determinare il numero di copie di una particolare app presenti nell'azienda

- Individuare le eventuali copie non utilizzate di un'app

- Determinare quali utenti usano regolarmente una particolare app

  Woodgrove Bank ha distribuito Microsoft Office 2010 come famiglia standard di prodotti di produttività per l'ufficio. Per supportare un'applicazione legacy, tuttavia, alcuni computer devono continuare a eseguire Microsoft Office Word 2003. Il reparto IT vuole ridurre i costi di licenza e supporto rimuovendo le copie di Word 2003, se l'applicazione legacy non viene più usata. Anche l'help desk vuole identificare gli utenti che usano l'applicazione legacy.

  Il responsabile dei sistemi IT di Woodgrove Bank usa la misurazione del software in Configuration Manager per raggiungere questi obiettivi aziendali. L'amministratore esegue le azioni seguenti:

- Verifica i prerequisiti per la misurazione del software e conferma che il punto di Reporting Services sia installato e funzionante.
- Configura le impostazioni client predefinite per la misurazione del software:<br>L'amministratore abilita la misurazione del software e usa la pianificazione di raccolta dati predefinita, una volta ogni sette giorni.<br>L'amministratore configura l'inventario software in modo da eseguire l'inventario dei file con estensione exe, configurando l'impostazione dell'agente client inventario software **Tipi di file da includere nell'inventario**.<br>L'amministratore aggiunge una nuova regola di misurazione del software, denominata **woodgrove.exe**, per monitorare l'applicazione legacy.
- Aspetta sette giorni, dopo di che i computer client iniziano a inviare report sui dati di utilizzo per il file eseguibile **woodgrove.exe**.
- L'amministratore usa il report di Configuration Manager **Installare la base per tutti i programmi di controllo software** per visualizzare i computer in cui è caricata l'applicazione **woodgrove.exe**.
- Dopo sei mesi, l'amministratore esegue il report **Computer che hanno installato un programma di controllo ma non hanno eseguito il programma da una data specificata**, specificando la regola di misurazione del software e una data di sei mesi nel passato. Questo report identifica 120 computer che non hanno eseguito il programma negli ultimi sei mesi.
- L'amministratore effettua ulteriori controlli per verificare che l'applicazione legacy non sia necessaria nei computer identificati. L'amministratore disinstalla quindi l'applicazione legacy e la copia di Word 2003 da questi computer.<br>L'amministratore esegue il report **Utenti che hanno eseguito un programma di controllo software specifico** per fornire all'help desk un elenco di utenti che continuano a usare l'applicazione legacy.
- L'amministratore continua a controllare i report di misurazione del software ogni settimana e, se necessario, esegue azioni correttive.

  Come risultato di questa linea di azione, i costi di licenza e di supporto IT si riducono, grazie alla rimozione delle applicazioni non più necessarie. Inoltre, ora l'help desk ha a disposizione l'elenco degli utenti che eseguono l'applicazione legacy di cui aveva bisogno.
