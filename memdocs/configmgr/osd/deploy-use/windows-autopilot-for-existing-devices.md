---
title: Windows Autopilot per dispositivi esistenti
titleSuffix: Configuration Manager
description: Usare una sequenza di attività di Configuration Manager per ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per la modalità definita dall'utente di Windows Autopilot
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709019"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot per dispositivi esistenti
<!--3607717, fka 1358333-->

*Si applica a: Configuration Manager (Current Branch)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) offre alle organizzazioni un modo per distribuire dispositivi Windows 10 aggiornati e intatti direttamente all'utente finale e per definire il flusso di provisioning eseguito dall'utente per ottenere un dispositivo Windows 10 sicuro e produttivo. Il dispositivo viene registrato nel servizio Windows Autopilot, in modo da poter assegnare il profilo di Windows Autopilot necessario. Questo profilo consente di definire l'esperienza di Configurazione guidata per il dispositivo. 

[Windows Autopilot per i dispositivi esistenti](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) è disponibile con Windows 10 versione 1809 o successiva. Questa funzionalità consente di ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per la [modalità definita dall'utente di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando una singola sequenza di attività nativa di Configuration Manager. 



## <a name="prerequisites"></a>Prerequisiti

- Acquistare i supporti di installazione per Windows 10 versione 1809 o successive. Creare quindi un'immagine del sistema operativo di Configuration Manager. Per altre informazioni, vedere [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md).

- In Microsoft Intune, creare i profili per Windows Autopilot. Per altre informazioni, vedere [Registrare dispositivi Windows in Intune con Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Un dispositivo che non sia già registrato con il servizio Windows Autopilot. Se il dispositivo è già registrato, il profilo assegnato ha la precedenza. Il profilo Autopilot per dispositivi esistenti si applica solo nel caso di un timeout del profilo online.



## <a name="create-the-configuration-file"></a>Creare il file di configurazione

1. In un dispositivo Windows con connettività Internet, aprire una finestra di comando di PowerShell amministrativa ed eseguire i comandi seguenti:  

    1. Installare i moduli necessari e accettare le richieste per continuare  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Accedere a Intune con le credenziali di amministratore  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Recuperare tutti i profili di Windows Autopilot associati al tenant di Intune  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Creare un file di configurazione per ogni profilo. I file vengono denominati in base al nome visualizzato del profilo e salvati sul desktop dell'utente corrente.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Il file di configurazione può contenere solo un profilo. Ogni profilo deve essere all'interno di parentesi graffe `{}`.  

2. Salvare uno dei profili in un file con codifica ANSI denominato **AutopilotConfigurationFile.json**. Salvarlo in una posizione adatta come origine pacchetto di Configuration Manager.  

    > [!Tip]  
    > Se si usa il cmdlet di PowerShell **Out-File** per reindirizzare l'output JSON in un file, viene usata la codifica Unicode per impostazione predefinita. Questo cmdlet può anche troncare righe lunghe. Usare il cmdlet **Set-Content** con il parametro `-Encoding ASCII` per impostare la codifica del testo appropriata.   
    > 
    > Il Blocco note di Windows usa la codifica ANSI per impostazione predefinita.  

3. Creare un pacchetto di Configuration Manager che contiene questo file. Non richiede un programma. Per altre informazioni, vedere [Creare un pacchetto](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > Windows richiede che il file sia denominato **AutopilotConfigurationFile.json**. Per usare più di un profilo Autopilot, creare pacchetti di Configuration Manager separati.  



## <a name="create-the-task-sequence"></a>Creare la sequenza di attività

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Sequenze di attività**. Selezionare **Crea sequenza di attività** nella barra multifunzione.  

2. Nella pagina **Crea nuova sequenza di attività** selezionare la nuova opzione **Distribuisci Windows Autopilot per dispositivi esistenti**.  

3. Nella pagina **Informazioni sequenza attività** specificare un nome, aggiungere facoltativamente una descrizione e selezionare un'immagine di avvio. Per altre informazioni sulle versioni di immagini di avvio supportate, vedere [Supporto per Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. Nella pagina **Installa Windows** selezionare il **pacchetto dell'immagine** di Windows 10. Configurare quindi le impostazioni seguenti:  

    - **Indice immagine**: Selezionare Enterprise, Education o Professional, in base ai requisiti dall'organizzazione  

    - Abilitare l'opzione **Creare partizioni e formattare il computer di destinazione prima di installare il sistema operativo**  

    - **Configura sequenza di attività da utilizzare con BitLocker**: se si abilita questa opzione, la sequenza di attività include i passaggi necessari per abilitare Bitlocker  

    - **Codice Product Key**: se è necessario specificare un codice Product Key per l'attivazione di Windows, immetterlo qui  

    - Selezionare una delle opzioni seguenti per configurare l'account amministratore locale in Windows 10:  
        - **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate (consigliato)**
        - **Attiva l'account e specifica la password dell'amministratore locale**

5. Nella pagina **Configura rete** selezionare l'opzione **Aggiunta a un gruppo di lavoro**. Questa sequenza di attività usa Utilità preparazione sistema di Windows (sysprep). Se il dispositivo è aggiunto a un dominio, sysprep genera un errore.  

6. Nella pagina **Installa Configuration Manager** aggiungere eventuali proprietà di installazione necessarie per l'ambiente.  

    > [!Tip]  
    > Queste informazioni sono necessarie per la sequenza di attività solo se sono richiesti i componenti client di Configuration Manager durante la sequenza di attività prima dell'esecuzione di sysprep. Ad esempio, per installare aggiornamenti software o applicazioni. Se non si devono eseguire azioni di questo tipo, il client non è necessario. Viene disinstallato prima che la sequenza di attività esegua sysprep.  

7. Nella pagina **Includi aggiornamenti** è selezionata per impostazione predefinita l'opzione **Non installare alcun aggiornamento software**.  

    > [!Tip]  
    > Usare la funzionalità di manutenzione delle immagini offline per mantenere aggiornata l'immagine con gli ultimi aggiornamenti di qualità di Windows 10. Per altre informazioni, vedere [Applicare aggiornamenti software a un'immagine del sistema operativo](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).  

8. Nella pagina **Installa applicazioni** è possibile selezionare le applicazioni da installare durante la sequenza di attività. Tuttavia, Microsoft consiglia di adottare l'approccio per l'immagine di firma con questo scenario. Dopo il provisioning del dispositivo con Autopilot, applicare tutte le applicazioni e le configurazioni dalla co-gestione di Microsoft Intune o Configuration Manager. Questo processo offre un'esperienza coerente agli utenti che ricevono i nuovi dispositivi e a quelli che usano Windows Autopilot per i dispositivi esistenti.  

8. Nella pagina **Preparazione sistema** selezionare il pacchetto che include il file di configurazione di Autopilot. Per impostazione predefinita, la sequenza di attività riavvia il computer dopo l'esecuzione di Sysprep di Windows. È anche possibile selezionare l'opzione **Shutdown computer after this task sequence completes** (Arresta il computer dopo il completamento di questa sequenza di attività). Questa opzione consente di preparare un dispositivo e quindi di fornirlo a un utente per un'esperienza coerente di Autopilot.  

9. Completare la procedura guidata.  

Se si modifica la sequenza di attività, la procedura è simile a quella per la sequenza di attività predefinita per applicare un'immagine del sistema operativo esistente. Questa sequenza di attività include i passaggi aggiuntivi seguenti:  

- **Applica la configurazione di Windows Autopilot**: questo passaggio applica il file di configurazione di Autopilot dal pacchetto specificato. Non è un nuovo tipo di passaggio, ma un passaggio **Esegui riga di comando** per copiare il file.  

- **Prepara Windows per l'acquisizione**: questo passaggio esegue Windows Sysprep e include l'impostazione **Arresta il computer dopo l'esecuzione di questa azione**. Per altre informazioni, vedere [Prepara Windows per l'acquisizione](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

Il risultato della sequenza di attività Windows Autopilot per i dispositivi esistenti è l'aggiunta di un dispositivo ad Azure Active Directory (Azure AD). 

> [!NOTE]  
> Con Windows 10 versione 1903 e versione 1909, Autopilot presenta un problema noto per cui Sysprep elimina il file **AutopilotConfigurationFile.json**. Se si usa questo metodo per distribuire Windows 10 versione 1903 o 1909, modificare questa sequenza di attività e apportare le modifiche seguenti:
>
> 1. Disabilitare il passaggio **Prepara Windows per l'acquisizione**.
> 2. Subito dopo il passaggio **Prepara Windows per l'acquisizione** disabilitato, aggiungere un nuovo passaggio **Esegui riga di comando**. Configurarlo per l'esecuzione della riga di comando seguente: `c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Per altre informazioni, vedere [Problemi noti di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Usare la funzionalità di [spostamento delle cartelle note](https://docs.microsoft.com/onedrive/redirect-known-folders) di OneDrive for Business per assicurarsi che venga eseguito un backup dei dati dell'utente prima dell'aggiornamento di Windows 10.



## <a name="next-steps"></a>Passaggi successivi

Usare la co-gestione per migliorare le funzionalità di gestione dei dispositivi Windows 10. Il secondo percorso per la co-gestione è tramite il provisioning moderno con Windows Autopilot. Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sulla co-gestione](../../comanage/overview.md)
- [Percorsi per la co-gestione](../../comanage/quickstart-paths.md)
- [Windows Autopilot con co-gestione](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Vedere anche

- [Registrare dispositivi Windows in Intune con Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot)
