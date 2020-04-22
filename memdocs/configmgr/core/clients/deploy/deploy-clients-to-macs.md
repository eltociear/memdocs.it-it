---
title: Distribuire i client Mac
titleSuffix: Configuration Manager
description: Informazioni su come distribuire i client nei computer Mac in Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694029"
---
# <a name="how-to-deploy-clients-to-macs"></a>Come distribuire i client in computer Mac

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo descrive come distribuire e gestire il client di Configuration Manager nei computer Mac. Per informazioni sulle configurazioni necessarie prima di distribuire i client nei computer Mac, vedere [Preparare la distribuzione del software client in computer Mac](prepare-to-deploy-mac-clients.md).

Quando si installa un nuovo client per i computer Mac, può essere necessario installare anche gli aggiornamenti di Configuration Manager per riflettere le nuove informazioni client nella console di Configuration Manager.

In queste procedure sono disponibili due opzioni per l'installazione dei certificati client. Altre informazioni sui certificati client per computer Mac sono disponibili in [Preparare la distribuzione del software client in computer Mac](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Usare la registrazione di Configuration Manager tramite lo [strumento CMEnroll](#bkmk_enroll). Il processo di registrazione non supporta il rinnovo automatico dei certificati. Registrare nuovamente il computer Mac prima che scada il certificato installato.    

- [Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Per distribuire il client in dispositivi che eseguono macOS Sierra, configurare correttamente il **Nome oggetto** del certificato del punto di gestione. Ad esempio, usare il nome di dominio completo del server del punto di gestione.



## <a name="configure-client-settings"></a>Configurare le impostazioni client  

Usare le [impostazioni client predefinite](about-client-settings.md) per configurare la registrazione per i computer Mac. Non è possibile usare impostazioni client personalizzate. Per richiedere e installare il certificato, il client di Configuration Manager per Mac richiede le impostazioni client predefinite.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Selezionare il nodo **Impostazioni client** e quindi selezionare **Impostazioni client predefinite**.  

2. Nella scheda **Home** della barra multifunzione scegliere **Proprietà** nel gruppo **Proprietà**.  

3. Selezionare la sezione **Registrazione** e quindi configurare le impostazioni seguenti:  

    1. **Consenti agli utenti di registrare i dispositivi mobili e i computer Mac**: **Sì**  

    2. **Profilo di registrazione:** scegliere **Imposta profilo**.  

4. Nella finestra di dialogo **Profilo di registrazione del dispositivo mobile** scegliere **Crea**.  

5. Nella finestra di dialogo **Crea profilo di registrazione** inserire un nome per questo profilo di registrazione, quindi configurare il **Codice sito di gestione**. Selezionare il sito primario di Configuration Manager che contiene i punti di gestione per questi computer Mac.  

    > [!NOTE]  
    >  Se è impossibile selezionare il sito, verificare che almeno un punto di gestione nel sito sia configurato per supportare i dispositivi mobili.  

6. Scegliere **Aggiungi**.  

7. Nella finestra **Aggiungi autorità di certificazione per dispositivi mobili** selezionare il server dell'autorità di certificazione che emette i certificati per i computer Mac.  

8. Nella finestra di dialogo **Crea profilo di registrazione** selezionare il modello di certificato del computer Mac creato in precedenza.  

9. Selezionare **OK** per chiudere la finestra di dialogo **Profilo di registrazione** e quindi la finestra di dialogo **Impostazioni client predefinite**.  

    > [!TIP]  
    > Se si vuole modificare l'intervallo dei criteri client, usare l'impostazione **Intervallo di polling dei criteri client** nel gruppo di impostazioni client **Criteri client** .  

La volta successiva che i dispositivi scaricano criteri client, Configuration Manager applica queste impostazioni per tutti gli utenti. Per avviare il recupero dei criteri per un singolo client, vedere [Avviare il recupero criteri per un client di Configuration Manager](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Oltre alle impostazioni client di registrazione, verificare di aver configurato le seguenti impostazioni del dispositivo client:  

- **Inventario hardware**: abilitare e configurare questa funzionalità per raccogliere l'inventario hardware dai computer client Mac e Windows. Per altre informazioni, vedere [Come estendere l'inventario hardware](../manage/inventory/extend-hardware-inventory.md).  

- **Impostazioni di conformità**: abilitare e configurare questa funzionalità per valutare e correggere le impostazioni nei computer client Mac e Windows. Per altre informazioni, vedere [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità).  

Per altre informazioni, vedere [Come configurare le impostazioni client](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a> Scaricare il client per macOS

1. Scaricare il pacchetto file del client macOS [Microsoft Endpoint Configuration Manager - macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850). Salvare **ConfigmgrMacClient.msi** in un computer che esegue Windows. Questo file non è incluso nel supporto di installazione di Configuration Manager.  

2. Eseguire il programma di installazione nel computer Windows. Estrarre il pacchetto del client Mac, **Macclient.dmg**, in una cartella sul disco locale. Il percorso predefinito è `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. Copiare il file **Macclient.dmg** in una cartella nel computer Mac.  

4. Nel computer Mac eseguire **Macclient.dmg** per estrarre i file in una cartella sul disco locale.  

5. Nella cartella verificare che siano presenti i file seguenti: 

    - **Ccmsetup**: installa il client di Configuration Manager nei computer Mac usando **CMClient.pkg**  

    - **CMDiagnostics**: raccoglie informazioni di diagnostica correlate al client di Configuration Manager nei computer Mac  

    - **CMUninstall**: disinstalla il client dai computer Mac  

    - **CMAppUtil**: converte i pacchetti di applicazioni Apple in un formato che si possa distribuire come applicazione di Configuration Manager  

    - **CMEnroll**: richiede e installa il certificato client per un computer Mac per poter quindi installare il client di Configuration Manager  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a> Registrare il client Mac  

Registrare singoli client con la [registrazione guidata computer Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Per automatizzare la registrazione per molti client, usare lo [strumento CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrare il client con la registrazione guidata computer Mac  

1. Al termine dell'installazione del client viene avviata la registrazione guidata computer. Per avviare manualmente la procedura guidata, selezionare **Registra** nella pagina delle preferenze di **Configuration Manager**.  

2. Nella seconda pagina della procedura guidata specificare le informazioni seguenti:  

   - **Nome utente**: Il nome utente può essere nei seguenti formati:  

     - `domain\name`. ad esempio `contoso\mnorth`  

     - `user@domain`. ad esempio `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Quando si usa un indirizzo e-mail per popolare il campo **Nome utente** Configuration Manager popola automaticamente il campo **Nome server**. Usa il nome predefinito del server del punto proxy di registrazione e il nome di dominio dell'indirizzo e-mail. Se questi nomi non corrispondono al nome del server del punto proxy di registrazione, correggere il **nome del server** durante la registrazione.  

       Il nome utente e la relativa password devono corrispondere a un account utente Active Directory con autorizzazioni di **lettura** e **registrazione** nel modello di certificato del client Mac.  

   - **Nome server**: il nome del server del punto proxy di registrazione.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automazione di client e certificati con CMEnroll  

Usare questa procedura per automatizzare l'installazione del client e la richiesta e la registrazione dei certificati client con lo strumento CMEnroll. Per eseguire lo strumento, è necessario avere un account utente di Active Directory.

1. Nel computer Mac passare alla cartella in cui è stato estratto il contenuto del file **Macclient.dmg**.  

2. Immettere il comando seguente: `sudo ./ccmsetup`  

3. Attendere fino a visualizzare il messaggio **Installazione completata** . Benché il programma di installazione visualizzi un messaggio di riavvio necessario immediato, non riavviare e andare al passaggio successivo.  

4. Dalla cartella **Strumenti** nel computer Mac digitare il comando seguente: `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Dopo l'installazione del client, viene avviata la procedura guidata di registrazione del computer Mac per semplificarne la registrazione. Per altre informazioni, vedere [Registrare il client usando la registrazione guidata computer Mac](#bkmk_enroll).  

     Esempio: Se il server del punto proxy di registrazione è denominato **server02.contoso.com** e sono state concesse le autorizzazioni **contoso\mnorth** per il modello di certificato client Mac, digitare il comando seguente: `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Se il nome utente include uno dei caratteri seguenti, la registrazione non riesce: `<>"+=,`. Usare un certificato fuori banda con un nome utente che non includa tali caratteri.  
    >  
    > Per un'esperienza utente più semplice, creare uno script per la procedura di installazione. Gli utenti dovranno specificare solo il nome utente e la password.  

5. Digitare la password per l'account utente di Active Directory. Quando si immette questo comando vengono richieste due password. La prima password consente all'account utente con privilegi avanzati di eseguire il comando. La seconda richiesta è relativa all'account utente di Active Directory. L'aspetto delle due richieste è identico, quindi accertarsi di specificarli nella sequenza corretta.  

6. Attendere fino a visualizzare il messaggio **Registrazione completata** .  

7. Per limitare il certificato registrato in Configuration Manager, sul computer Mac, aprire una finestra terminale e apportare le modifiche seguenti:  

    1. Immettere il comando `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. Nella finestra **Accesso Portachiavi** scegliere **Sistema** nella sezione **Portachiavi**. Nella sezione **Categoria** scegliere **Certificati**.  

    3. Espandere le chiavi per visualizzare i certificati client. Trovare il certificato con chiave privata installato in precedenza e aprire la chiave.  

    4. Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    5. Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    6. Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

8. Riavviare il computer Mac.  

Per verificare che l'installazione client sia avvenuta correttamente, aprire l'elemento **Configuration Manager** in **Preferenze di Sistema** nel computer Mac. Aggiornare e visualizzare inoltre la raccolta **Tutti i sistemi** nella console di Configuration Manager. Verificare che il computer Mac sia visualizzato in questa raccolta come client gestito.  

> [!TIP]  
> Per consentire la risoluzione dei problemi del client Mac, usare lo strumento **CMDiagnostics** incluso nel pacchetto del client Mac. Lo strumento consente di raccogliere le seguenti informazioni di diagnostica:  
>   
> - Un elenco dei processi in esecuzione  
> - La versione del sistema operativo Mac OS X  
> - Le segnalazioni di arresto anomalo del Mac OS X relative al client di Configuration Manager incluse **CCM\*.crash** e **System Preference.crash**.  
> - Il file della distinta base (BOM) e dell'elenco delle proprietà (.plist) creato dall'installazione client di Configuration Manager.  
> - Il contenuto della cartella **/Library/Application Support/Microsoft/CCM/Logs**.  
>   
> Le informazioni raccolte da CmDiagnostics vengono aggiunte a un file con estensione zip che viene salvato sul desktop del computer e denominato `cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a> Gestire i certificati esterni a Configuration Manager

È possibile usare una richiesta di certificato e un metodo di installazione indipendenti da Configuration Manager. Usare lo stesso processo generale, ma includere i seguenti passaggi aggiuntivi: 

- Quando si installa il client di Configuration Manager, usare le opzioni della riga di comando **MP** e **SubjectName**. Immettere il comando seguente: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. Il nome dell'oggetto certificato distingue tra maiuscole e minuscole, quindi digitarlo esattamente come appare nei dettagli del certificato.  

     Esempio: Il valore FQDN Internet del punto di gestione è **server03.contoso.com**. Il certificato client Mac ha il valore FQDN **mac12.contoso.com** come nome comune nel soggetto del certificato. Usare il comando seguente: `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Se si hanno più certificati contenenti lo stesso valore soggetto, specificare il numero di serie del certificato da usare per il client di Configuration Manager. Usare il comando seguente: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     ad esempio `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Rinnovare il certificato del client Mac  

Questa procedura rimuove il SMSID. Il client di Configuration Manager per Mac richiede un nuovo ID per usare un certificato nuovo o rinnovato.  

> [!IMPORTANT]  
> Dopo aver sostituito l'SMSID del client, quando si elimina la risorsa usata in precedenza nella console di Configuration Manager, si eliminano anche eventuali cronologie client archiviate, ad esempio, la cronologia dell'inventario hardware per il client.  


1. Creare e popolare una raccolta di dispositivi per i computer Mac che devono rinnovare i certificati dei computer.  

2. Nell'area di lavoro **Asset e conformità** , avviare la **Creazione guidata dell'elemento di configurazione**.  

3. Nella pagina **Generale** della procedura guidata specificare le informazioni seguenti:  

    - **Nome**: **Rimuovere SMSID per Mac**  

    - **Tipo**: **Mac OS X**  

4. Nella pagina **Piattaforme supportate**, selezionare tutte le versioni di Mac OS X.  

5. Nella pagina **Impostazioni** selezionare **Nuova**. Nella finestra **Crea impostazione** specificare le informazioni seguenti:  

    - **Nome**: **Rimuovere SMSID per Mac**  

    - **Tipo di impostazione**: **Script**  

    - **Tipo di dati**: **Stringa**  

6. Nella finestra **Crea impostazione** selezionare **Aggiungi script** per **Script di individuazione**. Questa azione consente di specificare uno script per individuare i computer Mac configurati con un SMSID.  

7. Nella finestra **Modifica script di individuazione** immettere il seguente script della shell:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Scegliere **OK** per chiudere la finestra **Modifica script di individuazione**.  

9. Nella finestra **Crea impostazione** scegliere **Aggiungi script** per **Script di monitoraggio e aggiornamento (facoltativo)** . Questa azione consente di specificare uno script per rimuovere eventuali SMSID rilevati sui computer Mac.  

10. Nella finestra **Crea script di monitoraggio e aggiornamento** immettere il seguente script della shell:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Scegliere **OK** per chiudere la finestra **Crea script di monitoraggio e aggiornamento**.  

12. Nella pagina **Regole di conformità** scegliere **Nuova**. Quindi specificare le informazioni seguenti nella finestra **Crea regola**:  

    - **Nome**: **Rimuovere SMSID per Mac**  

    - **Impostazione selezionata**: scegliere **Sfoglia**, quindi selezionare lo script di individuazione specificato in precedenza.  

    - Nel campo **i seguenti valori**: immettere **Il dominio/coppia predefinita di (com.microsoft.ccmclient, SMSID) non esiste**.  

    - Abilitare l'opzione **Eseguire lo script di monitoraggio e aggiornamento specificato quando l'impostazione non è conforme**.  

13. Completare la procedura guidata.  

14. Creare una linea di base di configurazione che contiene questo elemento di configurazione. Distribuire la linea di base nella raccolta di destinazione.  

     Per altre informazioni, vedere [Come creare linee di base di configurazione](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Dopo aver installato un nuovo certificato nei computer Mac con l'SMSID rimosso, eseguire il comando seguente per configurare il client per l'uso del nuovo certificato:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Vedere anche

[Preparare la distribuzione dei client nei computer Mac](prepare-to-deploy-mac-clients.md)

[Gestire i client Mac](../manage/maintain-mac-clients.md)
