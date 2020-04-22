---
title: Gestire i client Mac
titleSuffix: Configuration Manager
description: Attività di manutenzione per i client Mac di Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690059"
---
# <a name="maintain-mac-clients"></a>Gestire i client Mac
*Si applica a: Configuration Manager (Current Branch)*

Di seguito sono illustrate le procedure per disinstallare i client Mac e rinnovarne i certificati.

##  <a name="uninstalling-the-mac-client"></a>Disinstallazione del client Mac  

1.  In un computer Mac aprire una finestra terminale e spostarsi nella cartella che contiene il file **macclient.dmg**.  

2.  Spostarsi nella cartella Strumenti e immettere la seguente riga di comando:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  La proprietà **-c** indica alla disinstallazione del client di rimuovere anche i registri di arresto anomalo e i file di registro del client. È consigliabile usare questa opzione per evitare confusione nel caso in cui il client sia poi reinstallato.  

3.  Se necessario, rimuovere manualmente il certificato di autenticazione client usato da Configuration Manager o revocarlo. CMUnistall non rimuove né revoca questo certificato.  

##  <a name="renewing-the-mac-client-certificate"></a>Rinnovo del certificato del client Mac  
 Per rinnovare il certificato del client Mac, usare uno dei seguenti metodi:  

-   [Rinnovo guidato del certificato](#renew-certificate-wizard)  

-   [Rinnovo manuale del certificato](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Rinnovo guidato del certificato  

1. Configurare i valori seguenti come *stringhe* nel file ccmclient.plist che specifica quando aprire il Rinnovo guidato del certificato:  

   - **RenewalPeriod1**: specifica, in secondi, il primo periodo di rinnovo in cui gli utenti possono rinnovare il certificato. Il valore predefinito è 3888000 secondi (45 giorni). Non configurare un valore inferiore a 300, poiché il periodo sarà ripristinato sul valore predefinito. 

   - **RenewalPeriod2**: specifica, in secondi, il secondo periodo di rinnovo in cui gli utenti possono rinnovare il certificato. Il valore predefinito è 259200 secondi (3 giorni). Se il valore viene configurato, è superiore o uguale a 300 secondi ed è inferiore o uguale a **RenewalPeriod1**, il valore sarà usato. Se **RenewalPeriod1** è maggiore di 3 giorni, verrà usato un valore di 3 giorni per **RenewalPeriod2**.  Se **RenewalPeriod1** è minore di 3 giorni, **RenewalPeriod2** viene impostato sullo stesso valore di **RenewalPeriod1**.  

   - **RenewalReminderInterval1**: specifica, in secondi, la frequenza con la quale la procedura guidata di rinnovo certificato verrà presentata agli utenti durante il primo periodo di rinnovo. Il valore predefinito è 86.400 secondi (1 giorno). Se **RenewalReminderInterval1** è superiore a 300 secondi e inferiore al valore configurato per **RenewalPeriod1**, verrà usato il valore configurato. In caso contrario, verrà usato il valore predefinito di 1 giorno.  

   - **RenewalReminderInterval2**: specifica, in secondi, la frequenza con la quale la procedura guidata di rinnovo del certificato verrà presentata agli utenti durante il secondo periodo di rinnovo. Il valore predefinito è 28.800 secondi (8 ore). Se **RenewalReminderInterval2** è superiore a 300 secondi, inferiore o uguale a **RenewalReminderInterval1** e inferiore o uguale a **RenewalPeriod2**, verrà usato il valore configurato. In caso contrario, verrà usato un valore di 8 ore.  

     **Esempio:** se vengono mantenuti i valori predefiniti, 45 giorni prima della scadenza del certificato la procedura guidata si aprirà ogni 24 ore.  Entro 3 giorni del certificato in scadenza, la procedura guidata si aprirà ogni 8 ore.  

     **Esempio:** usare la riga di comando seguente o uno script per impostare il primo periodo di rinnovo su 20 giorni.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Quando si apre il Rinnovo guidato del certificato, i campi **Nome utente** e **Nome server** vengono solitamente prepopolati e l'utente deve soltanto immettere una password per rinnovare il certificato.  

   > [!NOTE]  
   >  Se la procedura guidata non si apre oppure se questa viene chiusa in modo accidentale, fare clic su **Rinnova** dalla pagina delle preferenze **Configuration Manager** per aprire la procedura guidata.  

###  <a name="renew-certificate-manually"></a>Rinnovo manuale del certificato  
 Il periodo di validità tipico per il certificato client Mac è 1 anno. Configuration Manager non rinnova automaticamente il certificato utente richiesto durante la registrazione, perciò è necessario usare la procedura seguente per rinnovare il certificato manualmente.  

> [!IMPORTANT]  
>  Se il certificato scade, è necessario disinstallare, reinstallare e quindi registrare nuovamente il client Mac.  

 Questa procedura rimuove l'SMSID, necessario per richiedere un nuovo certificato per lo stesso computer Mac. Quando si rimuove e sostituisce l'SMSID del client, tutte le cronologie client archiviate, come l'inventario, vengono eliminate dopo aver eliminato il client dalla console di Configuration Manager.  

1.  Creare e popolare una raccolta di dispositivi per i computer Mac che devono rinnovare i certificati utente.  

    > [!WARNING]  
    >  Configuration Manager non monitora il periodo di validità del certificato che registra per i computer Mac. È necessario monitorarlo indipendentemente da Configuration Manager per identificare i computer Mac da aggiungere a questa raccolta.  

2.  Nell'area di lavoro **Asset e conformità** , avviare la **Creazione guidata dell'elemento di configurazione**.  

3.  Nella pagina **Generale** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo:Mac OS X**  

4.  Nella pagina **Piattaforme supportate**, assicurarsi che siano selezionate tutte le versioni di Mac OS X.  

5.  Nella pagina **Impostazioni** scegliere **Nuovo**. Nella finestra di dialogo **Crea impostazione** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo di impostazione:Script**  

    -   **Tipo di dati: stringa**  

6.  Nella finestra di dialogo **Crea impostazione**, per **Script di individuazione** scegliere **Aggiungi script** per specificare uno script che individui i computer Mac con un SMSID configurato.  

7.  Nella finestra di dialogo **Modifica script di individuazione** , immettere il seguente script della shell:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Modifica script di individuazione** .  

9. Nella finestra di dialogo **Crea impostazione**, per **Script di monitoraggio e aggiornamento (facoltativo)** scegliere **Aggiungi script** per specificare uno script che rimuova l'SMSID quando viene rilevato in computer Mac.  

10. Nella finestra di dialogo **Crea script di monitoraggio e aggiornamento** , immettere il seguente script della shell:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Fare clic su **OK** per chiudere la finestra di dialogo **Crea script di monitoraggio e aggiornamento**.  

12. Nella pagina **Regole di conformità** della procedura guidata fare clic su **Nuovo**, quindi nella finestra di dialogo **Crea regola** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Impostazione selezionata:** scegliere **Sfoglia**, quindi selezionare lo script di individuazione specificato in precedenza.  

    -   Nel campo **i seguenti valori** immettere **Il dominio/coppia predefinita di (com.microsoft.ccmclient, SMSID) non esiste**.  

    -   Abilitare l'opzione **Eseguire lo script di monitoraggio e aggiornamento specificato quando l'impostazione non è conforme**.  

13. Completare la Creazione guidata dell'elemento di configurazione.  

14. Creare una linea di base di configurazione che contenga l'elemento di configurazione appena creato e distribuirlo nella raccolta di dispositivi creata nel passaggio 1.  

     Per altre informazioni su come creare e distribuire le linee di base di configurazione, vedere [Come creare linee di base di configurazione](../../../compliance/deploy-use/create-configuration-baselines.md) e [Come distribuire linee di base di configurazione](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Nei computer Mac con l'SMSID rimosso, eseguire il comando seguente per installare un nuovo certificato:  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Se richiesto, fornire la password per l'account utente con privilegi avanzati per eseguire il comando, quindi la password per l'account utente di Active Directory.  

16. Per limitare il certificato registrato in Configuration Manager, sul computer Mac, aprire una finestra terminale e apportare le modifiche seguenti:  

    a.  Immettere il comando `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`

    b.  Nella finestra di dialogo **Keychain Access** (Accesso portachiavi) scegliere **System** (Sistema) nella sezione **Keychains** (Portachiavi) e quindi **Keys** (Chiavi) nella sezione **Category** (Categoria).  

    c.  Espandere le chiavi per visualizzare i certificati client. Dopo aver identificato il certificato con una chiave privata appena installata, fare doppio clic sulla chiave.  

    d.  Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    e.  Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    f.  Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

17. Riavviare il computer Mac.  

