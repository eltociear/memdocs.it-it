---
title: Distribuzione di Windows Autopilot per i dispositivi esistenti
description: La distribuzione desktop moderna con Windows Autopilot consente di distribuire facilmente la versione più recente di Windows 10 nei dispositivi esistenti.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.technology: windows
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 685466a9760fa8aa688e76b10e1f44b7ac9eb37e
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643562"
---
# <a name="windows-autopilot-deployment-for-existing-devices"></a>Distribuzione di Windows Autopilot per i dispositivi esistenti

**Si applica a: Windows 10**

La distribuzione desktop moderna con Windows Autopilot consente di distribuire facilmente la versione più recente di Windows 10 nei dispositivi esistenti. Le app necessarie per il lavoro possono essere installate automaticamente. Il profilo di lavoro è sincronizzato, quindi è possibile riprendere subito a lavorare.

In questo argomento viene descritto come convertire i computer Windows 7 o Windows 8.1 aggiunti a un dominio in dispositivi Windows 10 aggiunti a Azure Active Directory o Active Directory (Aggiunta ad Azure AD ibrido) utilizzando Windows Autopilot.

>[!NOTE]
>Windows Autopilot per i dispositivi esistenti supporta solo profili Azure Active Directory e Azure AD ibrido basati su utenti. I profili di distribuzione automatica non sono supportati.

## <a name="prerequisites"></a>Prerequisiti

- Una versione attualmente supportata di Microsoft endpoint Configuration Manager Branch Current Branch o Technical Preview. 
- [Windows ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) 1803 o versione successiva
    - Per ulteriori informazioni sul supporto Configuration Manager, vedere [supporto per Windows 10 ADK](/configmgr/core/plan-design/configs/support-for-windows-10#windows-10-adk).
- Licenze Microsoft Intune assegnate
- Azure Active Directory Premium
- Windows 10 versione 1809 o successiva importata in Configuration Manager come immagine del sistema operativo
  - **Importante**: vedere i [problemi noti](known-issues.md) se si usa Windows 10 1903 con il modello di sequenza di attività del **dispositivo esistente di Windows Autopilot esistente** Configuration Manager. Attualmente, uno dei passaggi in questa sequenza di attività deve essere modificato per funzionare correttamente con Windows 10, versione 1903.

## <a name="procedures"></a>Procedure

### <a name="configure-the-enrollment-status-page-optional"></a>Configurare la pagina relativa allo stato della registrazione (facoltativo)

Se lo si desidera, è possibile configurare una [pagina relativa allo stato della registrazione](enrollment-status.md) per Autopilot con Intune.

Per abilitare e configurare la pagina di registrazione e stato:

1. Aprire [Intune nel portale di Azure](https://aka.ms/intuneportal).
2. Accedere a **Intune > la registrazione del dispositivo > la registrazione di Windows** e [configurare una pagina relativa allo stato della registrazione](/intune/windows-enrollment-status). 
3. Accedere **Azure Active Directory > Mobility (MDM e MAM) > Microsoft Intune** e [configurare la registrazione MDM automatica](/configmgr/mdm/deploy-use/enroll-hybrid-windows#enable-windows-10-automatic-enrollment) e configurare l'ambito utente MDM per alcuni o tutti gli utenti. 

Vedere gli esempi seguenti.

![pagina relativa allo stato della registrazione](images/esp-config.png)<br><br>
![mdm](images/mdm-config.png)

### <a name="create-the-json-file"></a>Creare il file JSON 

>[!TIP]
>Per eseguire i comandi seguenti in un computer che esegue Windows Server 2012/2012 R2 o Windows 7/8.1, è necessario prima scaricare e installare [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616).

1. In un PC o un server Windows connesso a Internet aprire una finestra di comando di Windows PowerShell con privilegi elevati
2. Immettere le righe seguenti per installare i moduli necessari

    #### <a name="install-required-modules"></a>Installare i moduli necessari

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module WindowsAutopilotIntune -Force
    Install-Module Microsoft.Graph.Intune -Force
    ```
   
3. Immettere le righe seguenti e fornire le credenziali amministrative di Intune:
   - Assicurarsi che l'account utente specificato disponga di diritti amministrativi sufficienti.

     ```powershell
     Connect-MSGraph
     ```
     L'utente e la password per l'account verranno richiesti usando un modulo di Azure AD standard. Digitare il nome utente e la password e quindi fare clic su **Accedi**. 
     <br>Vedere l'esempio seguente:

     ![Autenticazione di Azure AD](images/pwd.png)

     Se è la prima volta che si usano le API Graph di Intune, verrà richiesto di abilitare Microsoft Intune autorizzazioni di lettura e scrittura di PowerShell. Per abilitare le autorizzazioni seguenti:
   - Selezionare il **consenso per conto dell'organizzazione**
   - Fare clic su **Accetto**

4. Recuperare e visualizzare quindi tutti i profili di Autopilot disponibili nel tenant di Intune specificato in formato JSON:

    #### <a name="retrieve-profiles-in-autopilot-for-existing-devices-json-format"></a>Recuperare i profili in Autopilot per i dispositivi esistenti formato JSON

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

    Vedere l'output di esempio seguente: (usare la barra di scorrimento orizzontale nella parte inferiore per visualizzare le righe lunghe)
    <pre style="overflow-y: visible">
    PS C:\> Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    {
        "CloudAssignedTenantId": "1537de22-988c-4e93-b8a5-83890f34a69b",
        "CloudAssignedForcedEnrollment": 1,
        "Version": 2049,
        "Comment_File": "Profile Autopilot Profile",
        "CloudAssignedAadServerData": "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"ForcedEnrollment\":1,\"CloudAssignedTenantDomain\":\"M365x373186.onmicrosoft.com\"}}",
        "CloudAssignedTenantDomain": "M365x373186.onmicrosoft.com",
        "CloudAssignedDomainJoinMethod": 0,
        "CloudAssignedOobeConfig": 28,
        "ZtdCorrelationId": "7F9E6025-1E13-45F3-BF82-A3E8C5B59EAC"
    }</pre>

    Ogni profilo è incapsulato tra parentesi graffe **{}**. Nell'esempio precedente viene visualizzato un solo profilo.

    Per una descrizione delle proprietà usate nel file JSON, vedere la tabella seguente.


   |                          Proprietà                          |                                                                                                                                                                        Descrizione                                                                                                                                                                         |
   |------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                 Versione (numero, facoltativo)                 | Numero di versione che identifica il formato del file JSON. Per Windows 10 1809, la versione specificata deve essere 2049.                                                                                                                  |
   |           CloudAssignedTenantId (Guid, obbligatorio)           | ID del tenant Azure Active Directory da usare. Questa proprietà è il GUID del tenant e si trova nelle proprietà del tenant. Il valore non deve includere le parentesi graffe.                                                                                       |
   |        CloudAssignedTenantDomain (stringa, obbligatorio)        | Nome del tenant Azure Active Directory da usare, ad esempio: tenant.onmicrosoft.com.                                                                                                                                  |
   |         CloudAssignedOobeConfig (numero, obbligatorio)         | Questa proprietà è una bitmap che mostra quali impostazioni di Autopilot sono state configurate. I valori includono: SkipCortanaOptIn = 1, OobeUserNotLocalAdmin = 2, SkipExpressSettings = 4, SkipOemRegistration = 8, SkipEula = 16                                                                           |
   |      CloudAssignedDomainJoinMethod (numero, obbligatorio)      |                                                                                                                                    Questa proprietà specifica se il dispositivo deve partecipare Azure Active Directory o Active Directory (Aggiunta ad Azure AD ibrido). I valori includono: Active AD join = 0, Aggiunta ad Azure AD ibrido = 1                                                        |
   |      CloudAssignedForcedEnrollment (numero, obbligatorio)      |                                                                                                                         Specifica che il dispositivo deve richiedere Azure AD la registrazione di join e MDM. <br>0 = non necessario, 1 = obbligatorio.                                                                                                                         |
   |             ZtdCorrelationId (Guid, obbligatorio)              | Un GUID univoco (senza parentesi graffe) che verrà fornito a Intune come parte del processo di registrazione. ZtdCorrelationId verrà incluso nel messaggio di registrazione come "OfflineAutoPilotEnrollmentCorrelator". Questo attributo sarà presente solo se la registrazione viene eseguita in un dispositivo registrato con il provisioning con zero touch tramite registrazione offline. |
   | CloudAssignedAadServerData (stringa JSON codificata, obbligatoria) |                                                  Stringa JSON incorporata utilizzata per la personalizzazione. Richiede la personalizzazione di Azure AD Corp abilitata. <br> Valore di esempio: "CloudAssignedAadServerData": "{ \" ZeroTouchConfig \" : { \" CloudAssignedTenantUpn \" : \" \" , \" CloudAssignedTenantDomain \" : \" tenant.onmicrosoft.com \" }}"                                                   |
   |         CloudAssignedDeviceName (stringa, facoltativo)         | Nome assegnato automaticamente al computer. Segue la convenzione del modello di denominazione configurata nel profilo Autopilot di Intune. In alternativa, è possibile specificare un nome esplicito da usare. |


5. Il profilo di Autopilot deve essere salvato come file JSON in formato ASCII o ANSI. Per impostazione predefinita, Windows PowerShell è formato Unicode. Quindi, se si reindirizza l'output dei comandi in un file, specificare anche il formato del file. Ad esempio, per salvare il file in formato ASCII usando Windows PowerShell, è possibile creare una directory (ad esempio: c:\Autopilot) e salvare il profilo come illustrato di seguito: (usare la barra di scorrimento orizzontale nella parte inferiore se necessario per visualizzare l'intera stringa di comando)

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON | Out-File c:\Autopilot\AutopilotConfigurationFile.json -Encoding ASCII
    ```
    **Importante**: il nome del file deve essere denominato **AutopilotConfigurationFile.json** e deve essere codificato come ASCII/ANSI. 

    Se si preferisce, è possibile salvare il profilo in un file di testo e modificarlo nel blocco note. Nel blocco note, quando si sceglie **Salva con nome** , è necessario selezionare Salva come tipo: **tutti i file** e scegliere ANSI dall'elenco a discesa accanto a **codifica**. Vedere l'esempio seguente.

    ![Blocco note JSON](images/notepad.png)

    Dopo aver salvato il file, spostare il file in un percorso appropriato come un endpoint Microsoft Configuration Manager origine del pacchetto.

    >[!IMPORTANT]
    >È possibile usare più file di profilo JSON, ognuno dei quali deve essere denominato **AutopilotConfigurationFile.json** affinché la configurazione guidata segua l'esperienza di Autopilot. Anche il file deve essere codificato come ANSI. <br><br>**Se si salva il file con codifica Unicode o UTF-8 o lo si salva con un nome file diverso, la configurazione guidata di Windows 10 non seguirà l'esperienza di Autopilot**.<br>


### <a name="create-a-package-containing-the-json-file"></a>Creare un pacchetto contenente il file JSON

1. In Configuration Manager passare a **\SOFTWARE Library\Overview\Application Management\Packages**
2. Sulla barra multifunzione fare clic su **Crea pacchetto**
3. Nella **creazione guidata pacchetto e programma** immettere i dettagli del **pacchetto** e del **tipo di programma** seguenti:<br>
    - <u>Nome</u>: **Autopilot for existing devices config**
    - Selezionare **questo pacchetto contiene i file di origine**.
    - <u>Cartella di origine</u>: fare clic su **Sfoglia** e specificare un percorso UNC contenente il AutopilotConfigurationFile.jssu file. 
    - Fare clic su **OK** e quindi su **Avanti**.
    - <u>Tipo di programma</u>: **non creare un programma**
4. Fare clic due volte su **Avanti** e quindi su **Chiudi**.

**Nota**: se si modificano le impostazioni del profilo di Autopilot guidato dall'utente in Intune in un secondo momento, è necessario aggiornare anche il file JSON e ridistribuire il pacchetto di Configuration Manager associato.

### <a name="create-a-target-collection"></a>Creare una raccolta di destinazione

>[!NOTE]
>È anche possibile scegliere di riutilizzare una raccolta esistente

1. Passare a **raccolte \Assets e Compliance\Overview\Device**
2. Sulla barra multifunzione fare clic su **Crea** e quindi su **Crea raccolta dispositivi**
3. Nella **creazione guidata raccolta dispositivi** immettere i dettagli **generali** seguenti:
   - <u>Nome</u>: **Autopilot per la raccolta di dispositivi esistenti**
   - Commento: (facoltativo)
   - <u>Raccolta di limitazione</u>: fare clic su **Sfoglia** e selezionare **tutti i sistemi**

     >[!NOTE]
     >Facoltativamente, è possibile scegliere di usare una raccolta alternativa per la raccolta di limitazione. Il dispositivo da aggiornare deve eseguire l'agente ConfigMgr nella raccolta selezionata.

4. Fare clic su **Avanti**, quindi immettere le seguenti informazioni sulle **regole di appartenenza** :
   - Fare clic su **Aggiungi regola** e specificare una regola di raccolta diretta o basata su query per aggiungere i dispositivi Windows 7 di test di destinazione alla nuova raccolta.
   - Se, ad esempio, il nome host del computer da cancellare e ricaricare è PC-01 e si desidera utilizzare il nome come attributo:
      1. Fare clic su **Aggiungi regola > > regola diretta (si apre la procedura guidata) > avanti**.
      2. Immettere **PC-01** accanto a **valore**.
      3. Fare clic su **Next**  >  **PC-01** (in **Resources**). Vedere gli esempi seguenti.

         ![Finestra di dialogo Individua risorse-finestra di dialogo ](images/pc-01a.png)
          ![ Seleziona risorse](images/pc-01b.png)

5. Continuare la creazione della raccolta dispositivi con le impostazioni predefinite:
    - USA aggiornamenti incrementali per questa raccolta: non selezionato
    - Pianifica un aggiornamento completo in questa raccolta: predefinita
    - Fare clic due volte su **Avanti** e quindi su **Chiudi** .

### <a name="create-an-autopilot-for-existing-devices-task-sequence"></a>Creare una sequenza di attività di Autopilot per dispositivi esistenti

>[!TIP]
>Per la procedura successiva è necessaria un'immagine di avvio per Windows 10 1803 o versione successiva. Esaminare le immagini d'avvio disponibili nel Configuration Manager Conole in **software Library\Overview\Operating Systems\Boot immagini** e verificare che la **versione del sistema operativo** sia 10.0.17134.1 (Windows 10 versione 1803) o successiva.

1. Nella console di Configuration Manager passare a **\SOFTWARE Library\Overview\Operating Systems\Task sequences**
2. Sulla barra multifunzione Home fare clic su **Crea sequenza di attività**
3. Selezionare **installa un pacchetto immagine esistente** , quindi fare clic su **Avanti** .
4. Nella creazione guidata della sequenza di attività immettere i dettagli seguenti:
   - <u>Nome sequenza di attività</u>: **Autopilot per i dispositivi esistenti**
   - <u>Immagine d'avvio</u>: fare clic su **Sfoglia** e selezionare un'immagine di avvio di Windows 10 (1803 o versione successiva)
   - Fare clic su **Avanti**  >  **Sfoglia** > selezionare un **pacchetto di immagini** Windows 10 e un **Indice immagine**, versione 1803 o successiva.
   - Selezionare la **partizione e formattare il computer di destinazione prima di installare la** casella di controllo sistema operativo.
   - Selezionare o deselezionare **la casella di controllo Configura sequenza attività per l'utilizzo con BitLocker** . Questo indirizzo è facoltativo.
   - <u>Codice Product Key</u> e <u>modalità di gestione licenze server</u>: facoltativamente, immettere un codice Product Key e la modalità di gestione licenze server.
   - <u>Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme di supporto (scelta consigliata)</u>: facoltativo.
   - <u>Abilitare l'account e specificare la password dell'amministratore locale</u>: facoltativa.
   - Fare clic su **Avanti**, quindi nella pagina Configura rete scegliere **partecipa a un gruppo** di lavoro e specificare un nome, ad esempio gruppo di lavoro, accanto a **gruppo**di lavoro.

     > [!IMPORTANT]
     > La sequenza di attività Autopilot for existing devices eseguirà l'azione **prepara Windows per l'acquisizione** che usa l'utilità preparazione sistema (Sysprep). Questa azione avrà esito negativo se il computer di destinazione è aggiunto a un dominio.
     
     >[!IMPORTANT]
     > L'utilità preparazione sistema (Sysprep) viene eseguita con il parametro/generalize che, in Windows 10 versioni 1903 e 1909, eliminerà il file del profilo di Autopilot e il computer verrà avviato in fase di configurazione guidata anziché in fase di Autopilot. Per risolvere questo problema, vedere la pagina relativa ai [problemi noti di Windows Autopilot](known-issues.md).

5. Fare clic su **Avanti**, quindi fare di nuovo clic su **Avanti** per accettare le impostazioni predefinite nella pagina installa Configuration Manager.
6. Nella pagina migrazione stato immettere i dettagli seguenti:
   - Deselezionare la casella di controllo **Acquisisci impostazioni utente e file** .
   - Deselezionare la casella di controllo **Acquisisci impostazioni di rete** .
   - Deselezionare la casella di controllo **Acquisisci impostazioni di Microsoft Windows** .
   - Fare clic su **Avanti**.

     >[!NOTE]
     >Poiché la sequenza di attività Autopilot for existing devices viene completata in Windows PE, la migrazione dei dati di utilità di migrazione stato utente (USMT) non è supportata perché non è possibile ripristinare lo stato utente nel nuovo sistema operativo. Il Toolkit di migrazione stato utente (USMT), inoltre, non supporta i dispositivi aggiunti a Azure AD.

7. Nella pagina Includi aggiornamenti scegliere una delle tre opzioni disponibili. Questa selezione è facoltativa.
8. Nella pagina Installa applicazioni è possibile aggiungere facoltativamente applicazioni.
9. Fare clic su **Avanti**, confermare le impostazioni, fare clic su **Avanti**, quindi fare clic su **Chiudi**.
10. Fare clic con il pulsante destro del mouse sulla sequenza di attività Autopilot for existing devices e scegliere **modifica**.
11. Nell'editor della sequenza di attività, nel gruppo **Installa sistema operativo** , fare clic sull'azione **Applica impostazioni Windows** .
12. Fare clic su **Aggiungi** e quindi su **nuovo gruppo**.
13. Modificare il **nome** del gruppo da **nuovo gruppo** a **Autopilot per la configurazione dei dispositivi esistente**.
14. Fare clic su **Aggiungi**, scegliere **generale**, quindi fare clic su **Esegui riga di comando**.
15. Verificare che il passaggio **Esegui riga di comando** sia annidato sotto il gruppo **di configurazione Autopilot for existing devices** .
16. Modificare il **nome** in **applica Autopilot per il file di configurazione dei dispositivi esistenti**, incollare il codice seguente nella casella di testo della **riga di comando** > **applica**:
    ```
    cmd.exe /c xcopy AutopilotConfigurationFile.json %OSDTargetSystemDrive%\windows\provisioning\Autopilot\ /c
    ```
    - **AutopilotConfigurationFile.js** deve corrispondere al nome del file JSON presente nel pacchetto Autopilot for existing devices creato in precedenza.

17. Nel passaggio **Apply Autopilot for existing devices config file** selezionare il **pacchetto**  >  **Browse**.
18. Selezionare il pacchetto **di configurazione Autopilot for existing devices creato in** precedenza e fare clic su **OK**. Un esempio viene visualizzato alla fine di questa sezione.
19. Nel gruppo **Imposta sistema operativo** fare clic sull'attività **imposta Windows e Configuration Manager** .
20. Fare clic su **Aggiungi** e quindi su **nuovo gruppo**.
21. Modificare il **nome** da **nuovo gruppo** per **preparare il dispositivo per Autopilot**
22. Verificare che il gruppo **preparare il dispositivo per Autopilot** sia l'ultimo passaggio della sequenza di attività. Se necessario, utilizzare il pulsante **Sposta giù** .
23. Con il gruppo **prepara dispositivo per Autopilot** selezionato, fare clic su **Aggiungi**, scegliere **Immagini** e quindi fare clic su **prepara client ConfigMgr per l'acquisizione**.
24. Aggiungere un secondo passaggio facendo clic su **Aggiungi**, puntando a **Immagini**e facendo clic su **prepara Windows per l'acquisizione**. In questo passaggio usare le impostazioni seguenti:
    - <u>Compila automaticamente l'elenco di driver di archiviazione di massa</u>: **non selezionato**
    - <u>Non reimpostare il flag di attivazione</u>: **non selezionato**
    - <u>Arrestare il computer dopo l'esecuzione di questa azione</u>: **facoltativo**

    ![Sequenza di attività Autopilot](images/ap-ts-1.png)

25. Fare clic su **OK** per chiudere l'editor della sequenza di attività.

> [!NOTE]
> In Windows 10 1903 e 1909, il **AutopilotConfigurationFile.jsin** viene eliminato dal passaggio **prepara Windows per l'acquisizione** . Per ulteriori informazioni e per una soluzione alternativa, vedere la pagina relativa ai [problemi noti di Windows Autopilot](known-issues.md).

### <a name="deploy-content-to-distribution-points"></a>Distribuire il contenuto nei punti di distribuzione

Assicurarsi quindi che tutto il contenuto necessario per la sequenza di attività venga distribuito nei punti di distribuzione.

1. Fare clic con il pulsante destro del mouse sulla sequenza attività **Autopilot for existing devices** e scegliere **Distribuisci contenuto**.
2. Fare clic su **Avanti**, **controllare il contenuto da distribuire**e quindi fare clic su **Avanti**.
3. Nella pagina specificare la distribuzione del contenuto fare clic su **Aggiungi** per specificare un **punto di distribuzione** o un gruppo di **punti di distribuzione**.
4. Nella procedura guidata Aggiungi punti di distribuzione o Aggiungi gruppi di punti di distribuzione specificare le destinazioni di contenuto che consentono alla sequenza di attività di recuperare il file JSON.
5. Al termine della specifica della distribuzione del contenuto, fare clic su **Avanti** due volte e quindi su **Chiudi**.

### <a name="deploy-the-os-with-autopilot-task-sequence"></a>Distribuire il sistema operativo con la sequenza di attività Autopilot

1. Fare clic con il pulsante destro del mouse sulla sequenza attività **Autopilot for existing devices** e quindi scegliere **Distribuisci**.
2. Nella distribuzione guidata del software immettere i dettagli seguenti **delle impostazioni** **generali** e di distribuzione:
    - <u>Sequenza di attività</u>: **Autopilot per i dispositivi esistenti**.
    - <u>Raccolta</u>: fare clic su **Sfoglia** e quindi selezionare **Autopilot per la raccolta di dispositivi esistente** (o un'altra raccolta desiderata).
    - Fare clic su **Avanti** per specificare **le impostazioni di distribuzione**.
    - <u>Azione</u>: **Install**.
    - <u>Scopo</u>: **disponibile**. Facoltativamente, è possibile selezionare **obbligatorio** anziché **disponibile**. Questa impostazione non è consigliata durante il test perché le configurazioni accidentali possono avere un impatto negativo.
    - <u>Rendere disponibile per gli elementi seguenti</u>: **solo Configuration Manager client**. Nota: scegliere l'opzione qui pertinente per il contesto del test. Se per il client di destinazione non è installato l'agente Configuration Manager o Windows, è necessario selezionare un'opzione che includa PXE o supporti di avvio.
    - Fare clic su **Avanti** per specificare i dettagli della **pianificazione** .
    - <u>Pianifica quando questa distribuzione diventerà disponibile</u>: facoltativo
    - <u>Pianifica al</u>termine della distribuzione: facoltativo
    - Fare clic su **Avanti** per specificare i dettagli **dell'esperienza utente** .
    - <u>Mostra stato sequenza di attività</u>: selezionato.
    - <u>Installazione software</u>: non selezionata.
    - <u>Riavvio del sistema (se necessario per completare l'installazione)</u>: non selezionato.
    - <u>Commit modificato alla scadenza o durante una finestra di manutenzione (riavvio necessario)</u>: facoltativo.
    - <u>Consenti l'esecuzione della sequenza di attività per il client su Internet</u>: facoltativo
    - Fare clic su **Avanti** per specificare i dettagli degli **avvisi** .
    - <u>Creare un avviso di distribuzione quando la soglia è superiore a quella riportata di seguito</u>: facoltativa.
    - Fare clic su **Avanti** per specificare i dettagli dei **punti di distribuzione** .
    - <u>Opzioni di distribuzione</u>: **scaricare il contenuto localmente quando necessario per la sequenza di attività in esecuzione**.
    - <u>Quando non è disponibile alcun punto di distribuzione locale, usare un punto di distribuzione remoto</u>: facoltativo.
    - <u>Consenti ai client di usare i punti di distribuzione dal gruppo di limiti del sito predefinito</u>: facoltativo.
    - Fare clic su **Avanti**, confermare le impostazioni, fare clic su **Avanti**, quindi fare clic su **Chiudi**.

### <a name="complete-the-client-installation-process"></a>Completare il processo di installazione client

1. Nel computer client Windows 7 o Windows 8.1 di destinazione scegliere Avvia > digitare **Software Center** > premere INVIO.

2. Nella raccolta software selezionare **Autopilot per i dispositivi esistenti** e fare clic su **Installa**. Vedere l'esempio seguente:

    ![Finestra di ](images/sc.png) dialogo di conferma della pagina per i dispositivi esistenti di Autopilot ![](images/sc1.png)

La sequenza di attività:
1. Scarica contenuto
2. Riavviare il dispositivo
3. Formattare le unità
4. Installare Windows 10
5. Prepararsi per Autopilot

Al termine della sequenza di attività, il dispositivo avvierà la configurazione guidata e fornirà un'esperienza di Autopilot.

![Refresh-1 Refresh ](images/up-1.png)
 ![ -2 ](images/up-2.png)
 ![ Refresh-3](images/up-3.png)

>[!NOTE]
>Se l'aggiunta di dispositivi a Active Directory (Aggiunta ad Azure AD ibrido), è necessario creare un profilo di configurazione del dispositivo di aggiunta al dominio destinato a "tutti i dispositivi" (poiché non è presente un Azure Active Directory oggetto dispositivo per il computer per la destinazione basata su gruppi). Per altre informazioni, vedere [modalità guidata dall'utente per l'aggiunta di Azure Active Directory ibride](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join).

### <a name="register-the-device-for-windows-autopilot"></a>Registrare il dispositivo per Windows Autopilot

I dispositivi di cui è stato effettuato il provisioning con Autopilot ricevono solo l'esperienza di configurazione guidata guidato automatico per il primo avvio. Dopo l'aggiornamento a Windows 10, assicurarsi di registrare il dispositivo in modo che disponga dell'esperienza Autopilot quando il computer viene reimpostato. È possibile abilitare la registrazione automatica per un gruppo assegnato usando l'impostazione **Converti tutti i dispositivi di destinazione in Autopilot** . Per altre informazioni, vedere [Creare un profilo di distribuzione Autopilot](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

Vedere anche [aggiunta di dispositivi a Windows Autopilot](add-devices.md).

## <a name="speeding-up-the-deployment-process"></a>Velocizzare il processo di distribuzione

Per rimuovere circa 20 minuti dal processo di distribuzione, vedere il Blog di Michael Niehaus con le istruzioni per [velocizzare Windows Autopilot per i dispositivi esistenti](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices).
