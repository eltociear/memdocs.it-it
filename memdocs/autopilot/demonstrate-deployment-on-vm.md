---
title: Dimostrazione della distribuzione di Autopilot
ms.reviewer: ''
manager: laurawi
description: Istruzioni dettagliate su come configurare una macchina virtuale con una distribuzione di Windows Autopilot
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune, aggiornamento
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: autopilot
ms.openlocfilehash: 7ff25816c0398389fc23bbde4983f4bc9556d192
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757755"
---
# <a name="demonstrate-autopilot-deployment"></a>Dimostrazione della distribuzione di Autopilot

**Si applica a**

- Windows 10

Per iniziare a usare Windows Autopilot, provare con una macchina virtuale (VM) o un dispositivo fisico che verrà cancellato e quindi avere una nuova installazione di Windows 10.

In questo argomento verrà illustrato come configurare una distribuzione di Windows Autopilot per una macchina virtuale con Hyper-V.

> [!NOTE]
> Sebbene siano disponibili [più piattaforme](add-devices.md#registering-devices) per abilitare Autopilot, questo Lab usa principalmente Intune.

> Hyper-V e una macchina virtuale non sono necessari per questo Lab. È anche possibile usare un dispositivo fisico. Tuttavia, le istruzioni presuppongono che si usi una macchina virtuale. Per usare un dispositivo fisico, ignorare le istruzioni per installare Hyper-V e creare una macchina virtuale. Tutti i riferimenti a' Device ' nella Guida fanno riferimento al dispositivo client, fisico o virtuale.

Il video seguente offre una panoramica del processo:

</br>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/KYVptkpsOqs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

> Per un elenco dei termini usati in questa guida, vedere la sezione [Glossario](#glossary) .

## <a name="prerequisites"></a>Prerequisiti

Questi sono gli elementi necessari per completare il Lab:
<table><tr><td>Supporto di installazione di Windows 10</td><td>Windows 10 Professional o Enterprise (file ISO) per una versione supportata di Windows 10, ovvero un canale semestrale. Se non si dispone già di un file ISO da usare, viene fornito un collegamento per scaricare una <a href="https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise" data-raw-source="[evaluation version of Windows 10 Enterprise](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)">versione di valutazione di Windows 10 Enterprise</a>.</td></tr>
<tr><td>Accesso a Internet</td><td>Se si è protetti da un firewall, vedere i <a href="windows-autopilot-requirements.md#networking-requirements" data-raw-source="[networking requirements](windows-autopilot-requirements.md#networking-requirements)">requisiti di rete</a>dettagliati. In caso contrario, è sufficiente assicurarsi di disporre di una connessione a Internet.</td></tr>
<tr><td>Hyper-V o un dispositivo fisico che esegue Windows 10</td><td>Nella guida si presuppone che si utilizzi una macchina virtuale Hyper-V e si forniscano istruzioni per l'installazione e la configurazione di Hyper-V, se necessario. Per usare un dispositivo fisico, ignorare i passaggi per l'installazione e la configurazione di Hyper-V.</td></tr>
<tr><td>Un account Intune Premium</td><td>Questa guida descrive come ottenere un account Premium di 30 giorni di valutazione gratuito che può essere usato per completare il Lab.</td></tr></table>

## <a name="procedures"></a>Procedure

Di seguito è riportato un riepilogo delle sezioni e delle procedure nel Lab. Seguire ogni sezione nell'ordine in cui viene presentata, ignorando le sezioni che non si applicano all'utente. Le procedure facoltative sono disponibili nell'appendice.

[Verificare il supporto per Hyper-V](#verify-support-for-hyper-v)
<br>[Abilitare Hyper-V](#enable-hyper-v)
<br>[Creare una macchina virtuale demo](#create-a-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[Imposta percorso file ISO](#set-iso-file-location)
<br>&nbsp;&nbsp;&nbsp;[Determinare il nome della scheda di rete](#determine-network-adapter-name)
<br>&nbsp;&nbsp;&nbsp;  [Usare Windows PowerShell per creare la macchina virtuale demo](#use-windows-powershell-to-create-the-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[Installare Windows 10](#install-windows-10)
<br>[Acquisisci ID hardware](#capture-the-hardware-id)
<br>[Ripristinare la macchina virtuale in modalità predefinita (configurazione guidata)](#reset-the-vm-back-to-out-of-box-experience-oobe)
<br>[Verificare il livello di sottoscrizione](#verify-subscription-level)
<br>[Configurare la personalizzazione aziendale](#configure-company-branding)
<br>[Configurare Microsoft Intune la registrazione automatica](#configure-microsoft-intune-auto-enrollment)
<br>[Registrare la macchina virtuale](#register-your-vm)
<br>&nbsp;&nbsp;&nbsp;[Registrazione di Autopilot con Intune](#autopilot-registration-using-intune)
<br>&nbsp;&nbsp;&nbsp;[Registrazione di Autopilot con MSfB](#autopilot-registration-using-msfb)
<br>[Creare e assegnare un profilo di distribuzione di Windows Autopilot](#create-and-assign-a-windows-autopilot-deployment-profile)
<br>&nbsp;&nbsp;&nbsp;[Creare un profilo di distribuzione di Windows Autopilot con Intune](#create-a-windows-autopilot-deployment-profile-using-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Assegnare il profilo](#assign-the-profile)
<br>&nbsp;&nbsp;&nbsp;[Creare un profilo di distribuzione di Windows Autopilot con MSfB](#create-a-windows-autopilot-deployment-profile-using-msfb)
<br>[Vedere Windows Autopilot in azione](#see-windows-autopilot-in-action)
<br>[Rimuovere i dispositivi da Autopilot](#remove-devices-from-autopilot)
<br>&nbsp;&nbsp;&nbsp;[Elimina (Annulla registrazione) il dispositivo Autopilot](#delete-deregister-autopilot-device)
<br>[Appendice A: verificare il supporto per Hyper-V](#appendix-a-verify-support-for-hyper-v)
<br>[Appendice B: aggiunta di app al profilo](#appendix-b-adding-apps-to-your-profile)
<br>&nbsp;&nbsp;&nbsp;[Aggiungere un'app Win32](#add-a-win32-app)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Preparare l'app per Intune](#prepare-the-app-for-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Creare un'app in Intune](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Assegnare l'app al profilo di Intune](#assign-the-app-to-your-intune-profile)
<br>&nbsp;&nbsp;&nbsp;[Aggiungi Office 365](#add-office-365)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Creare un'app in Intune](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Assegnare l'app al profilo di Intune](#assign-the-app-to-your-intune-profile)
<br>[Glossario](#glossary)

## <a name="verify-support-for-hyper-v"></a>Verificare il supporto per Hyper-V

Se non si dispone già di Hyper-V, è necessario innanzitutto abilitarlo in un computer che esegue Windows 10 o Windows Server (2012 R2 o versione successiva).

> Se Hyper-V è già abilitato, passare al passaggio [creare una demo della macchina virtuale](#create-a-demo-vm) . Se si usa un dispositivo fisico anziché una macchina virtuale, passare a [installare Windows 10](#install-windows-10).

Se non si è certi che il dispositivo supporti Hyper-V o si verifichino problemi durante l'installazione di Hyper-V, vedere l' [appendice a](#appendix-a-verify-support-for-hyper-v) di seguito per informazioni dettagliate su come verificare che Hyper-v possa essere installato correttamente.

## <a name="enable-hyper-v"></a>Abilitare Hyper-V

Per abilitare Hyper-V, aprire un prompt di Windows PowerShell con privilegi elevati ed eseguire il comando seguente:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

Questo comando funziona su tutti i sistemi operativi che supportano Hyper-V, ma nei sistemi operativi Windows Server è necessario digitare un comando aggiuntivo (sotto) per aggiungere il modulo Hyper-V di Windows PowerShell e la console di gestione di Hyper-V. Il comando seguente installerà anche Hyper-V, se non è già installato. Pertanto, se si usa Windows Server, è possibile digitare il comando seguente invece di usare il comando Enable-WindowsOptionalFeature:

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools
```

Quando viene richiesto di riavviare il computer, scegliere **Sì**. Il computer potrebbe essere riavviato più di una volta.

> In alternativa, è possibile installare Hyper-V usando il pannello di controllo in Windows in **attivazione o disattivazione delle funzionalità Windows** per un sistema operativo client o usando l' **Aggiunta guidata ruoli e funzionalità** di Server Manager in un sistema operativo server, come illustrato di seguito:

   ![Funzionalità Hyper-V](images/hyper-v-feature.png)

   ![Hyper-V](images/svr_mgr2.png)

<P>Se si sceglie di installare Hyper-V con Server Manager, accettare tutte le selezioni predefinite. Assicurarsi anche di installare entrambi gli elementi in <strong>amministrazione ruoli Tools\Hyper-V strumenti di gestione</strong>.

Al termine dell'installazione, aprire la console di gestione di Hyper-V digitando **virtmgmt. msc** a un prompt dei comandi con privilegi elevati oppure digitando **Hyper-v** nella casella di ricerca del menu Start.

Per ulteriori informazioni su Hyper-V, vedere [Introduzione a Hyper-v in Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/) e [Hyper-v in Windows Server](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server).

## <a name="create-a-demo-vm"></a>Creare una macchina virtuale demo

Ora che Hyper-V è abilitato, è necessario creare una macchina virtuale che esegue Windows 10. È possibile [creare una VM e una](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine) [rete virtuale](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network) usando la console di gestione di Hyper-V, ma è più semplice usare Windows PowerShell.

Per usare Windows PowerShell, è sufficiente sapere due elementi:

1. Percorso del file ISO di Windows 10.
   - Nell'esempio si presuppone che il percorso sia **c:\iso\win10-EVAL.ISO**.
2. Nome dell'interfaccia di rete che si connette a Internet.
   - Nell'esempio viene usato un comando di Windows PowerShell per determinarlo automaticamente.

Dopo aver impostato il percorso del file ISO e aver determinato il nome dell'interfaccia di rete appropriata, è possibile installare Windows 10.

### <a name="set-iso-file-location"></a>Imposta percorso file ISO

È possibile scaricare un file ISO per una versione di valutazione della versione più recente di Windows 10 Enterprise [qui](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise).
- Quando viene richiesto di selezionare una piattaforma, scegliere **64 bit**.

Dopo aver scaricato il file, il nome sarà estremamente lungo (ad esempio: 17763.107.101029-1455. rs5_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-US. ISO).

1. In modo che sia più semplice digitare e ricordare, rinominare il file in **WIN10-EVAL. ISO**.
2. Creare una directory nel computer denominata **c:\ISO** e spostare il file **WIN10-EVAL. ISO** in questo punto, in modo che il percorso del file sia **c:\iso\win10-EVAL.ISO**.
3. Se si desidera utilizzare un nome e un percorso diversi per il file, è necessario modificare i comandi di Windows PowerShell riportati di seguito per utilizzare il nome e la directory personalizzati.

### <a name="determine-network-adapter-name"></a>Determinare il nome della scheda di rete

Il cmdlet Get-NetAdaper viene usato di seguito per individuare automaticamente la scheda di rete che probabilmente sarà quella usata per la connessione a Internet. È necessario testare prima questo comando eseguendo il comando seguente a un prompt di Windows PowerShell con privilegi elevati:

```powershell
(Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
```

L'output di questo comando deve essere il nome dell'interfaccia di rete usata per la connessione a Internet. Verificare che il nome dell'interfaccia sia corretto. Se non è il nome dell'interfaccia corretto, è necessario modificare il primo comando riportato di seguito per usare il nome dell'interfaccia di rete.

Se ad esempio il comando precedente Visualizza Ethernet ma si vuole usare ETHERNET2, il primo comando seguente sarà New-VMSwitch-Name AutopilotExternal-AllowManagementOS $true-NetAdapterName **ETHERNET2**.

### <a name="use-windows-powershell-to-create-the-demo-vm"></a>Usare Windows PowerShell per creare la macchina virtuale demo

Tutti i dati della VM verranno creati nel percorso corrente nel prompt di PowerShell. Provare a spostarsi in una nuova cartella prima di eseguire i comandi seguenti.

> [!IMPORTANT]
> **Switch della macchina virtuale**: un'opzione della macchina virtuale è il modo in cui Hyper-V connette le macchine virtuali a una rete. <br><br>Se Hyper-V è stato precedentemente abilitato e l'interfaccia di rete connessa a Internet è già associata a un'opzione di macchina virtuale, i comandi di PowerShell riportati di seguito avranno esito negativo. In questo caso, è possibile eliminare l'opzione della macchina virtuale esistente (in modo che i comandi seguenti possano crearne uno). in alternativa, è possibile riutilizzare l'opzione della VM ignorando il primo comando riportato di seguito e modificando il secondo comando per sostituire il nome dell'opzione **AutopilotExternal** con il nome dell'opzione oppure rinominando l'opzione esistente su "AutopilotExternal".<br><br>Se non è mai stato creato un comportatore esterno per la macchina virtuale, eseguire i comandi seguenti.

```powershell
New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal
Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
Start-VM -VMName WindowsAutopilot
```

Dopo aver immesso questi comandi, connettersi alla macchina virtuale appena creata e attendere che venga richiesta la pressione di un tasto e l'avvio dal DVD.  È possibile connettersi alla VM facendo doppio clic su di esso nella console di gestione di Hyper-V.

Vedere l'output di esempio riportato di seguito. In questo esempio, la VM viene creata nella directory **c:\autopilot** e viene usato il comando vmconnect.exe, disponibile solo in Windows Server. Se Hyper-V è stato installato in Windows 10, utilizzare la console di gestione di Hyper-V per connettersi alla macchina virtuale.

<pre style="overflow-y: visible">
PS C:\autopilot&gt; dir c:\iso


    Directory: C:\iso


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/12/2019   2:46 PM     4627343360 win10-eval.iso

PS C:\autopilot&gt; (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name
Ethernet
PS C:\autopilot&gt; New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name

Name              SwitchType NetAdapterInterfaceDescription
----              ---------- ------------------------------
AutopilotExternal External   Intel(R) Ethernet Connection (2) I218-LM

PS C:\autopilot&gt; New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal

Name             State CPUUsage(%) MemoryAssigned(M) Uptime   Status             Version
----             ----- ----------- ----------------- ------   ------             -------
WindowsAutopilot Off   0           0                 00:00:00 Operating normally 8.0

PS C:\autopilot&gt; Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
PS C:\autopilot&gt; Start-VM -VMName WindowsAutopilot
PS C:\autopilot&gt; vmconnect.exe localhost WindowsAutopilot
PS C:\autopilot&gt; dir

    Directory: C:\autopilot

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/12/2019   3:15 PM                VMData
d-----        3/12/2019   3:42 PM                VMs

PS C:\autopilot&gt;
</pre>

### <a name="install-windows-10"></a>Installare Windows 10

Verificare che la macchina virtuale sia stata avviata dall'installazione ISO, fare clic su **Avanti** , quindi fare clic su **Installa ora** e completare il processo di installazione di Windows. Vedere gli esempi seguenti:

   ![Installazione di Windows installazione di Windows impostazione Windows installazione di Windows installazione ](images/winsetup1.png) di Windows ![ ](images/winsetup2.png) ![ ](images/winsetup3.png) ![ ](images/winsetup4.png) ![ ](images/winsetup5.png) ![](images/winsetup6.png)

Dopo il riavvio della macchina virtuale, durante la configurazione guidata è possibile selezionare **configurazione per uso personale** o aggiunta a un **dominio** , quindi scegliere un account offline nella schermata di **accesso** .  Questo offrirà il modo più rapido per il desktop. Ad esempio:

   ![Installazione di Windows](images/winsetup7.png)

Al termine dell'installazione, accedere e verificare di essere al desktop di Windows 10, quindi creare il primo checkpoint Hyper-V. I checkpoint vengono usati per ripristinare lo stato precedente della macchina virtuale. In questo Lab verranno creati più checkpoint, che possono essere usati in un secondo momento per eseguire nuovamente il processo.

   ![Installazione di Windows](images/winsetup8.png)

Per creare il primo checkpoint, aprire un prompt di Windows PowerShell con privilegi elevati nel computer che esegue Hyper-V (non nella VM) ed eseguire le operazioni seguenti:

```powershell
Checkpoint-VM -Name WindowsAutopilot -SnapshotName "Finished Windows install"
```

Fare clic sulla macchina virtuale **WindowsAutopilot** nella console di gestione di Hyper-V e verificare che nel riquadro Checkpoint sia visualizzata l' **installazione di Windows completata** .

## <a name="capture-the-hardware-id"></a>Acquisisci ID hardware

> [!NOTE]
> In genere, l'ID dispositivo viene acquisito dall'OEM durante l'esecuzione dello strumento OA3 in ogni dispositivo della factory.  L'OEM invia quindi il valore HH di 4K creato dallo strumento OA3 a Microsoft inviando il report con un report di compilazione del computer (CBR).  Ai fini di questo Lab, si agisce come OEM (acquisendo il valore HH di 4K), ma non si userà lo strumento OA3 per acquisire la versione completa di 4K HH per vari motivi (è necessario installare lo strumento OA3, il dispositivo non può avere una versione di Windows con contratti multilicenza, è un processo più complesso rispetto all'uso di uno script PS e così via).  Al contrario, si simula l'esecuzione dello strumento OA3 eseguendo uno script di PowerShell, che acquisisce il dispositivo 4K HH esattamente come lo strumento OA3.

Per eseguire lo script PS, attenersi alla procedura seguente:

1. Aprire un prompt di Windows PowerShell con privilegi elevati ed eseguire i comandi seguenti. Questi comandi sono gli stessi indipendentemente dal fatto che si usi una macchina virtuale o un dispositivo fisico:

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

Quando viene richiesto di installare il pacchetto NuGet, scegliere **Sì**.

Vedere l'output di esempio riportato di seguito.

<pre>
PS C:\> md c:\HWID

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/14/2019  11:33 AM                HWID

PS C:\> Set-Location c:\HWID
PS C:\HWID> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
PS C:\HWID> Install-Script -Name Get-WindowsAutopilotInfo -Force

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\user1\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and
import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
PS C:\HWID> $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
PS C:\HWID> Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
PS C:\HWID> dir

    Directory: C:\HWID

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/14/2019  11:33 AM           8184 AutopilotHWID.csv

PS C:\HWID>
</pre>

Verificare che nella directory **c:\HWID** sia presente un file di **AutopilotHWID.csv** di dimensioni pari a circa 8 KB.  Questo file contiene le HH complete 4K.

> [!NOTE]
> Sebbene l'estensione CSV possa essere associata a Microsoft Excel, non è possibile visualizzare il file in modo corretto facendo doppio clic su di esso. Per analizzare correttamente i delimitatori di virgola e visualizzare il file in Excel, è necessario utilizzare i **dati**della  >  funzione**text/csv** in Excel per importare le colonne di dati appropriate. Non è necessario visualizzare il file in Excel a meno che non si sia curiosi. Il formato del file verrà convalidato quando viene importato in Autopilot. Di seguito è riportato un esempio dei dati in questo file.

![Numero di serie e hash hardware](images/hwid.png)

È necessario caricare questi dati in Intune per registrare il dispositivo per Autopilot, in modo che sia necessario trasferirlo nel computer che verrà usato per accedere al portale di Azure.  Se si usa un dispositivo fisico anziché una macchina virtuale, è possibile copiare il file in una chiavetta USB.  Se si usa una macchina virtuale, è possibile fare clic con il pulsante destro del mouse sul file AutopilotHWID.csv e copiarlo, quindi fare clic con il pulsante destro del mouse e incollare il file sul desktop (all'esterno della macchina virtuale).

Se non si riesce a copiare e incollare il file, è sufficiente visualizzare il contenuto del blocco note nella macchina virtuale e copiare il testo nel blocco note all'esterno della macchina virtuale. Per eseguire questa operazione, non usare un altro editor di testo.

> [!NOTE]
> Quando si esegue la copia e incolla in o da macchine virtuali, evitare di fare clic su altri elementi con il cursore del mouse tra il processo di copia e incolla, perché questo può svuotare o sovrascrivere gli appunti e richiedere l'avvio. Passare direttamente da copia a Incolla.

## <a name="reset-the-vm-back-to-out-of-box-experience-oobe"></a>Ripristinare la macchina virtuale in modalità predefinita (configurazione guidata)

Con l'ID hardware acquisito in un file, preparare la macchina virtuale per la distribuzione di Windows Autopilot ripristinando la configurazione guidata.

Nella macchina virtuale passare a **impostazioni > aggiorna & sicurezza > ripristino** e fare clic su **inizia** in **Reimposta il PC**.
Selezionare **Rimuovi tutto** e **rimuovere solo i file personali**. Infine, fare clic su **Reimposta**.

![Reimposta la richiesta finale del PC](images/autopilot-reset-prompt.jpg)

Il ripristino della macchina virtuale o del dispositivo può richiedere qualche minuto. Procedere al passaggio successivo (verificare il livello di sottoscrizione) durante il processo di reimpostazione.

![Reimposta l'acquisizione schermo del PC](images/autopilot-reset-progress.jpg)

## <a name="verify-subscription-level"></a>Verificare il livello di sottoscrizione

Per questo laboratorio è necessaria una sottoscrizione Premium di AAD.  È possibile stabilire se si dispone di una sottoscrizione Premium passando al pannello [configurazione della registrazione MDM](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) . Vedere l'esempio seguente:

**Azure Active Directory**  >  **Mobilità (MDM e MAM)**  >  **Microsoft Intune**

![MDM e Intune](images/mdm-intune2.png)

Se il pannello configurazione illustrato in precedenza non viene visualizzato, è probabile che non si disponga di una sottoscrizione **Premium** .  La registrazione automatica è una funzionalità disponibile solo in AAD Premium.

Per convertire l'account di valutazione di Intune in un account di valutazione Premium gratuito, passare a **Azure Active Directory**  >  **licenze**  >  **tutti i prodotti**  >  **try/Buy** e selezionare **versione di valutazione gratuita** per Azure ad Premium o EMS E5.

![Reimposta la richiesta finale del PC](images/aad-lic1.png)

## <a name="configure-company-branding"></a>Configurare la personalizzazione aziendale

Se è già stata configurata la personalizzazione dell'azienda in Azure Active Directory, è possibile ignorare questo passaggio.

> [!IMPORTANT]
> Assicurarsi di accedere con un account amministratore globale.

Passare a informazioni personalizzate distintive [dell'azienda in Azure Active Directory](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding), fare clic su **Configura** e configurare qualsiasi tipo di personalizzazione aziendale che si desidera visualizzare durante la configurazione guidata.

![Configurare la personalizzazione aziendale](images/branding.png)

Al termine, fare clic su **Salva**.

> [!NOTE]
> Per applicare le modifiche apportate alla personalizzazione dell'azienda possono essere necessari fino a 30 minuti.

## <a name="configure-microsoft-intune-auto-enrollment"></a>Configurare Microsoft Intune la registrazione automatica

Se è già stata configurata la registrazione automatica MDM in Azure Active Directory, è possibile ignorare questo passaggio.

Aprire [Mobility (MDM e MAM) in Azure Active Directory](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) e selezionare **Microsoft Intune**. Se non viene visualizzato Microsoft Intune, fare clic su **Aggiungi applicazione** e scegliere **Intune**.

Ai fini di questa demo, selezionare **tutto** nell'ambito dell' **utente MDM** e fare clic su **Salva**.

![Ambito utente MDM nel pannello Mobility](images/autopilot-aad-mdm.png)

## <a name="register-your-vm"></a>Registrare la macchina virtuale

La macchina virtuale (o dispositivo) può essere registrata tramite Intune o Microsoft Store for business (MSfB).  Entrambi i processi sono illustrati di seguito, ma <u>ne scelgono solo uno</u> ai fini di questo Lab. Si consiglia vivamente di usare Intune anziché MSfB.

### <a name="autopilot-registration-using-intune"></a>Registrazione di Autopilot con Intune

1. In Intune nel portale di Azure scegliere registrazione del **dispositivo**registrazione  >  **Windows**  >  **dispositivi**  >  **importazione**.

    ![Importazione dispositivo Intune](images/device-import.png)

    > [!NOTE]
    > Se le voci di menu come la **registrazione di Windows** non sono attive, cercare il pannello all'estrema destra nell'interfaccia utente.  Potrebbe essere necessario fornire i privilegi di configurazione di Intune in una finestra di verifica che è stata visualizzata.

2. In **Aggiungi dispositivi Windows Autopilot** nel riquadro all'estrema destra passare al file **AutopilotHWID.csv** copiato in precedenza nel computer locale.  Il file deve contenere il numero di serie e l'HH 4K della VM (o dispositivo).  È accettabile se gli altri campi (ID prodotto Windows) vengono lasciati vuoti.

    ![HWID CSV](images/hwid-csv.png)

    Si dovrebbe ricevere la conferma che il file è formattato correttamente prima di caricarlo, come illustrato in precedenza.

3. Fare clic su **Importa** e attendere il completamento del processo di importazione. Questa operazione può richiedere fino a 15 minuti.

4. Fare clic su **Sincronizza** per sincronizzare il dispositivo appena registrato. Attendere alcuni istanti prima dell'aggiornamento per verificare che la macchina virtuale o il dispositivo sia stato aggiunto. Vedere l'esempio seguente.

   ![Importa HWID](images/import-vm.png)

### <a name="autopilot-registration-using-msfb"></a>Registrazione di Autopilot con MSfB

> [!IMPORTANT]
> Se è già stata eseguita la registrazione della macchina virtuale (o del dispositivo) con Intune, ignorare questo passaggio.

Facoltativo: per una panoramica del processo, vedere il video seguente.

&nbsp;

> [!video https://www.youtube.com/embed/IpLIZU_j7Z0]

Per prima cosa, è necessario un account MSfB.  È possibile usare lo stesso creato in precedenza per Intune oppure seguire [queste istruzioni](https://docs.microsoft.com/microsoft-store/windows-store-for-business-overview) per crearne uno nuovo.

Successivamente, accedere a [Microsoft Store for business](https://businessstore.microsoft.com/en-us/store) usando il proprio account di test facendo clic su **Accedi** nell'angolo superiore destro della pagina principale.

Selezionare **Gestisci** dal menu in alto, quindi fare clic sul collegamento **programma Windows Autopilot Deployment** nella scheda **dispositivi** . Vedere l'esempio seguente:

![Microsoft Store per le aziende](images/msfb.png)

Fare clic sul collegamento **Aggiungi dispositivi** per caricare il file CSV. Verrà visualizzato un messaggio che indica che è in corso l'elaborazione della richiesta. Attendere alcuni istanti prima di aggiornare per vedere che è stato aggiunto il nuovo dispositivo.

![Dispositivi](images/msfb-device.png)

## <a name="create-and-assign-a-windows-autopilot-deployment-profile"></a>Creare e assegnare un profilo di distribuzione di Windows Autopilot

> [!IMPORTANT]
> I profili Autopilot possono essere creati e assegnati alla macchina virtuale o al dispositivo registrato tramite Intune o MSfB.  Entrambi i processi sono illustrati di seguito, ma <U>ne scelgono solo uno ai fini di questo Lab</U>:

Selezionarne uno:
- [Creare profili con Intune](#create-a-windows-autopilot-deployment-profile-using-intune)
- [Creare profili usando MSfB](#create-a-windows-autopilot-deployment-profile-using-msfb)

### <a name="create-a-windows-autopilot-deployment-profile-using-intune"></a>Creare un profilo di distribuzione di Windows Autopilot con Intune

> [!NOTE]
> Anche se il dispositivo è stato registrato in MSfB, verrà comunque visualizzato in Intune, anche se potrebbe essere necessario eseguire la **sincronizzazione** e **aggiornare** prima l'elenco dei dispositivi:

![Dispositivi](images/intune-devices.png)

> Nell'esempio precedente sono elencati sia un dispositivo fisico che una macchina virtuale. L'elenco deve includere solo uno di questi.

Per creare un profilo di Windows Autopilot, selezionare **registrazione del dispositivo**  >  profili di**Windows enrollment**  >  **distribuzione** di Windows

![Profili di distribuzione](images/deployment-profiles.png)

Fare clic su **Crea profilo**.

![Crea profilo di distribuzione](images/create-profile.png)

Nel pannello **Crea profilo** usare i valori seguenti:

| Impostazione | valore |
|---|---|
| Nome | Profilo Lab Autopilot |
| Description | vuoto |
| Convertire tutti i dispositivi di destinazione in Autopilot | No |
| Modalità di distribuzione | Basata sull'utente |
| Unisci a Azure AD | Aggiunta ad Azure AD |

Fare clic su configurazione **guidata** e configurare le impostazioni seguenti:

| Impostazione | valore |
|---|---|
| CONTRATTO DI LICENZA | Nascondi |
| impostazioni del profilo | Nascondi |
| Nascondi opzioni account modifica | Nascondi |
| Tipo di account utente | Standard |
| Applica modello nome dispositivo | No |

Vedere l'esempio seguente:

![Profilo di distribuzione](images/profile.png)

Fare clic su **OK** e quindi su **Crea**.

> Se si vuole aggiungere un'app al profilo tramite Intune, i passaggi FACOLTATIVi per farlo sono disponibili nell' [Appendice B: aggiunta di app al profilo](#appendix-b-adding-apps-to-your-profile).

#### <a name="assign-the-profile"></a>Assegnare il profilo

I profili possono essere assegnati solo ai gruppi, quindi è prima necessario creare un gruppo che contenga i dispositivi a cui applicare il profilo. In questa guida vengono fornite istruzioni semplici per l'assegnazione di un profilo. per istruzioni più dettagliate, vedere [creare un gruppo di dispositivi Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group) e [assegnare un profilo di distribuzione Autopilot a un gruppo di dispositivi](https://docs.microsoft.com/intune/enrollment-autopilot#assign-an-autopilot-deployment-profile-to-a-device-group), come lettura facoltativa.

Per creare un gruppo, aprire il portale di Azure e selezionare **Azure Active Directory**  >  **gruppi**  >  **tutti i gruppi**:

![Tutti i gruppi](images/all-groups.png)

Selezionare nuovo gruppo dal pannello gruppi per aprire l'interfaccia utente dei nuovi gruppi.  Selezionare il tipo di gruppo "sicurezza", assegnare un nome al gruppo e selezionare il tipo di appartenenza "assegnato":

Prima di fare clic su **Crea**, espandere il pannello **membri** , fare clic sul numero di serie del dispositivo (verrà visualizzato sotto **membri selezionati**) e quindi fare clic su **Seleziona** per aggiungere il dispositivo a questo gruppo.

![Nuovo gruppo](images/new-group.png)

A questo punto fare clic su **Crea** per completare la creazione del nuovo gruppo.

Fare clic su **tutti i gruppi** e fare clic su **Aggiorna** per verificare che il nuovo gruppo sia stato creato correttamente.

Con un gruppo creato che contiene il dispositivo, è ora possibile tornare indietro e assegnare il profilo a tale gruppo. Tornare alla pagina di Intune nella portale di Azure (è possibile digitare **Intune** nella barra di ricerca del banner superiore e selezionare **Intune** nei risultati).

Da Intune, selezionare **registrazione del dispositivo**  >  **Windows enrollment**  >  **profili di distribuzione** di Windows per aprire il pannello profilo.  Fare clic sul nome del profilo creato in precedenza (profilo Lab Autopilot) per aprire il pannello dei dettagli per il profilo:

![Profilo Lab](images/deployment-profiles2.png)

In **Gestisci**fare clic su **assegnazioni**, quindi, con la scheda **Includi** evidenziata, espandere il pannello **Seleziona gruppi** e fare clic su **AP Lab Group 1** (il gruppo verrà visualizzato in **membri selezionati**).

![Includi gruppo](images/include-group.png)

Fare clic su **Seleziona** e quindi su **Salva**.

![Includi gruppo](images/include-group2.png)

È anche possibile assegnare utenti specifici a un profilo, ma questo scenario non verrà analizzato nel Lab. Per informazioni più dettagliate, vedere [registrare i dispositivi Windows in Intune usando Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="create-a-windows-autopilot-deployment-profile-using-msfb"></a>Creare un profilo di distribuzione di Windows Autopilot con MSfB

Se è già stato creato e assegnato un profilo tramite Intune usando la procedura appena descritta sopra, ignorare questa sezione.

È disponibile un [video](https://www.youtube.com/watch?v=IpLIZU_j7Z0) che illustra i passaggi necessari per creare e assegnare profili in MSfB. Questi passaggi sono riepilogati anche di seguito.

Per prima cosa, accedere al [Microsoft Store for business](https://businessstore.microsoft.com/manage/dashboard) con l'account di Intune creato inizialmente per questo Lab.

Fare clic su **Gestisci** nel menu in alto, quindi fare clic su **dispositivi** nell'albero di spostamento a sinistra.

![Gestione MSfB](images/msfb-manage.png)

Fare clic sul collegamento **programma Windows Autopilot Deployment** nel riquadro **dispositivi** .

Per creare il profilo:

Selezionare il dispositivo dall'elenco dei **dispositivi** :

![Creazione di MSfB](images/msfb-create1.png)

Nel menu a discesa distribuzione di Autopilot selezionare **Crea nuovo profilo**:

![Creazione di MSfB](images/msfb-create2.png)

Assegnare un nome al profilo, scegliere le impostazioni desiderate e quindi fare clic su **Crea**:

![Creazione di MSfB](images/msfb-create3.png)

Il nuovo profilo viene aggiunto all'elenco di distribuzione di Autopilot.

Per assegnare il profilo:

Per assegnare (o riassegnare) il profilo a un dispositivo, selezionare le caselle di controllo accanto al dispositivo registrato per il Lab, quindi selezionare il profilo che si vuole assegnare dal menu a discesa **distribuzione Autopilot** come illustrato:

![Assegnazione MSfB](images/msfb-assign1.png)

Verificare che il profilo sia stato assegnato correttamente al dispositivo desiderato controllando il contenuto della colonna del **profilo** :

![Assegnazione MSfB](images/msfb-assign2.png)

> [!IMPORTANT]
> Il nuovo profilo verrà applicato solo se il dispositivo non è stato avviato ed è stato passato attraverso la configurazione guidata. Non è possibile applicare le impostazioni da un profilo diverso quando è stato applicato un altro profilo. È necessario reinstallare Windows nel dispositivo affinché il secondo profilo venga applicato al dispositivo.

## <a name="see-windows-autopilot-in-action"></a>Vedere Windows Autopilot in azione

Se la macchina virtuale viene arrestata dopo l'ultima reimpostazione, è necessario avviarla di nuovo, in modo che possa avanzare attraverso l'esperienza di configurazione guidata di Autopilot, ma non provare ad avviare di nuovo il dispositivo fino a quando lo **stato del profilo** del dispositivo in Intune non viene modificato da **non assegnato** ad **assegnazione** e infine **assegnato**:

![Stato dei dispositivi](images/device-status.png)

Assicurarsi anche di attendere almeno 30 minuti dal momento in cui è stata [configurata la personalizzazione dell'azienda](#configure-company-branding). in caso contrario, è possibile che queste modifiche non vengano visualizzate.

> [!TIP]
> Se il dispositivo viene reimpostato in precedenza dopo aver raccolto le informazioni di HH per 4K e quindi riavviato nella prima schermata di configurazione guidata, potrebbe essere necessario riavviare il dispositivo per assicurarsi che il dispositivo venga riconosciuto come dispositivo Autopilot e visualizzi l'esperienza di configurazione guidata di Autopilot in attesa.  Se non viene visualizzata l'esperienza di configurazione guidata di Autopilot, reimpostare nuovamente il dispositivo (impostazioni > Aggiorna & sicurezza > ripristino e fare clic su introduzione.  In Reimposta questo PC selezionare Rimuovi tutto e rimuovere i file personali. Fare clic su Reimposta).

- Verificare che il dispositivo disponga di una connessione Internet.
- Accendere il dispositivo
- Verificare che vengano visualizzate le schermate OOBE appropriate (con personalizzazione della società appropriata).  Verrà visualizzata la schermata di selezione dell'area, la schermata di selezione della tastiera e la seconda schermata di selezione della tastiera, che può essere ignorata.

![Pagina di accesso a OOBE](images/autopilot-oobe.jpg)

Subito dopo aver raggiunto il desktop, il dispositivo dovrebbe essere visualizzato in Intune come dispositivo Autopilot **abilitato** .  Accedere al portale di Azure di Intune e selezionare **dispositivi > tutti i dispositivi**, quindi **aggiornare** i dati per verificare che il dispositivo sia stato modificato da disabilitato ad abilitato e che il nome del dispositivo venga aggiornato.

![Dispositivo abilitato](images/enabled-device.png)

Dopo aver selezionato una lingua e un layout di tastiera, verrà visualizzata la schermata di accesso personalizzata dell'azienda. Fornire le credenziali di Azure Active Directory e l'operazione è stata eseguita.

Windows Autopilot ora assume la funzione di aggiungere automaticamente il dispositivo a Azure Active Directory e di registrarlo Microsoft Intune. Usare i checkpoint creati per eseguire nuovamente questo processo con impostazioni diverse.

## <a name="remove-devices-from-autopilot"></a>Rimuovere i dispositivi da Autopilot

Per usare il dispositivo (o macchina virtuale) per altri scopi dopo il completamento di questo Lab, sarà necessario rimuovere (annullare la registrazione) il dispositivo da Autopilot tramite Intune o MSfB e quindi reimpostarlo.  Le istruzioni per annullare la registrazione dei dispositivi sono disponibili [qui](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group) e [qui](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal) e sotto.

### <a name="delete-deregister-autopilot-device"></a>Elimina (Annulla registrazione) il dispositivo Autopilot

Prima di annullare la registrazione del dispositivo da Autopilot, è necessario eliminare o ritirare o ripristinare le impostazioni predefinite del dispositivo da Intune. Per eliminare il dispositivo da Intune (non Azure Active Directory), accedere al portale di Azure di Intune, quindi passare a **intune > dispositivi > tutti i dispositivi**.  Selezionare la casella di controllo accanto al dispositivo che si desidera eliminare, quindi fare clic sul pulsante Elimina nel menu in alto.

![Eliminare un dispositivo](images/delete-device1.png)

Quando richiesto, fare clic su **X** per completare l'operazione:

![Eliminare un dispositivo](images/delete-device2.png)

Il dispositivo verrà rimosso dalla gestione di Intune e scomparirà dai **dispositivi > intune > tutti i dispositivi**. Tuttavia, questa operazione non Annulla ancora la registrazione del dispositivo da Autopilot, quindi il dispositivo dovrebbe ancora essere visualizzato in **Intune > registrazione del dispositivo > registrazione windows > Windows Autopilot Deployment Program > dispositivi**.

![Eliminare un dispositivo](images/delete-device3.png)

I **dispositivi > di intune > elenco tutti i dispositivi** e la **registrazione del dispositivo > di Intune > registrazione Windows > programma di distribuzione di windows Autopilot >** elenco dei dispositivi significano elementi diversi e sono due archivi dati completamente distinti.  Il primo (tutti i dispositivi) è l'elenco dei dispositivi attualmente registrati in Intune.

> [!NOTE]
> Un dispositivo verrà visualizzato solo nell'elenco tutti i dispositivi dopo l'avvio.  Il secondo (programma di distribuzione di Windows Autopilot >) è l'elenco dei dispositivi attualmente registrati da tale account Intune nel programma Autopilot, che può essere registrato o meno in Intune.

Per rimuovere il dispositivo dal programma Autopilot, selezionare il dispositivo e fare clic su Elimina.

![Eliminare un dispositivo](images/delete-device4.png)

Viene visualizzato un messaggio di avviso per ricordare prima di tutto di rimuovere il dispositivo da Intune, che in precedenza era stato fatto.

![Eliminare un dispositivo](images/delete-device5.png)

A questo punto, è stata annullata la registrazione del dispositivo da Intune ed è stata anche annullata la registrazione da Autopilot.  Dopo alcuni minuti, fare clic sul pulsante **Sincronizza** , seguito dal pulsante **Aggiorna** per verificare che il dispositivo non sia più elencato nel programma Autopilot:

![Eliminare un dispositivo](images/delete-device6.png)

Una volta che il dispositivo non viene più visualizzato, è possibile riutilizzarlo per altri scopi.

Se si vuole anche rimuovere il dispositivo da AAD, passare a **Azure Active Directory > dispositivi > tutti i dispositivi**, selezionare il dispositivo e quindi fare clic sul pulsante Elimina:

![Eliminare un dispositivo](images/delete-device7.png)

## <a name="appendix-a-verify-support-for-hyper-v"></a>Appendice A: verificare il supporto per Hyper-V

A partire da Windows 8, il microprocessore del computer host deve supportare la conversione degli indirizzi di secondo livello (stecca) per installare Hyper-V. Per ulteriori informazioni, vedere [Hyper-V: elenco delle CPU che supportano le doghe per gli host](https://social.technet.microsoft.com/wiki/contents/articles/1401.hyper-v-list-of-slat-capable-cpus-for-hosts.aspx) .

Per verificare che il computer supporti la stecca, aprire un prompt dei comandi dell'amministratore, digitare **SystemInfo**, premere INVIO, scorrere verso il basso ed esaminare la sezione visualizzata nella parte inferiore dell'output, accanto a requisiti di Hyper-V. Vedere l'esempio seguente:

<pre style="overflow-y: visible">
C:>systeminfo

...
Hyper-V Requirements:      VM Monitor Mode Extensions: Yes
                           Virtualization Enabled In Firmware: Yes
                           Second Level Address Translation: Yes
                           Data Execution Prevention Available: Yes
</pre>

In questo esempio, il computer supporta le doghe e Hyper-V.

> Se uno o più requisiti vengono valutati come **No** , il computer non supporta l'installazione di Hyper-V.  Tuttavia, se solo l'impostazione di virtualizzazione è incompatibile, potrebbe essere possibile abilitare la virtualizzazione nel BIOS e modificare la **virtualizzazione abilitata nell'** impostazione del firmware da **No** a **Sì**. Il percorso di questa impostazione dipende dal produttore e dalla versione del BIOS, ma viene in genere trovato associato alle impostazioni di sicurezza del BIOS.

È anche possibile identificare il supporto di Hyper-V usando gli [strumenti](https://blogs.msdn.microsoft.com/taylorb/2008/06/19/hyper-v-will-my-computer-run-hyper-v-detecting-intel-vt-and-amd-v/) forniti dal produttore del processore, lo strumento [msinfo32](https://technet.microsoft.com/library/cc731397.aspx) oppure è possibile scaricare l'utilità [Coreinfo](https://technet.microsoft.com/sysinternals/cc835722) ed eseguirla, come illustrato nell'esempio seguente:

<pre style="overflow-y: visible">
C:>coreinfo -v

Coreinfo v3.31 - Dump information on system CPU and memory topology
Copyright (C) 2008-2014 Mark Russinovich
Sysinternals - www.sysinternals.com

Intel(R) Core(TM) i7-2600 CPU @ 3.40GHz
Intel64 Family 6 Model 42 Stepping 7, GenuineIntel
Microcode signature: 0000001B
HYPERVISOR      -       Hypervisor is present
VMX             *       Supports Intel hardware-assisted virtualization
EPT             *       Supports Intel extended page tables (SLAT)
</pre>

> [!NOTE]
> Per eseguire Hyper-V è necessario un sistema operativo a 64 bit.

## <a name="appendix-b-adding-apps-to-your-profile"></a>Appendice B: aggiunta di app al profilo

### <a name="add-a-win32-app"></a>Aggiungere un'app Win32

#### <a name="prepare-the-app-for-intune"></a>Preparare l'app per Intune

Prima di poter eseguire il pull di un'applicazione in Intune per renderla parte del profilo di AP, è necessario "assemblare" l'applicazione per la distribuzione usando lo [strumento da riga di comandoIntuneWinAppUtil.exe](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool).  Dopo aver scaricato lo strumento, raccogliere le seguenti tre informazioni per usare lo strumento:

1. Cartella di origine per l'applicazione
2. Nome del file eseguibile di installazione
3. Cartella di output per il nuovo file

Ai fini di questo laboratorio, verrà usato lo strumento Blocco note + + come app Win32.

Scaricare [qui](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available) il pacchetto MSI di Notepad + +, quindi copiare il file in un percorso noto, ad esempio C:\Notepad + + MSI.

Eseguire lo strumento IntuneWinAppUtil, fornendo risposte alle tre domande, ad esempio:

![Aggiungere l'app](images/app01.png)

Al termine dell'esecuzione dello strumento, è necessario disporre di un file con estensione intunewin nella cartella di output, che è ora possibile caricare in Intune attenendosi alla procedura seguente.

#### <a name="create-app-in-intune"></a>Creare un'app in Intune

Accedere al portale di Azure e selezionare **Intune**.

Passare a **Intune > client app > app**, quindi fare clic sul pulsante **Aggiungi** per creare un nuovo pacchetto dell'app.

![Aggiungere l'app](images/app02.png)

In **tipo di app**selezionare **app Windows (Win32)**:

![Aggiungere l'app](images/app03.png)

Nel pannello **file del pacchetto dell'app** individuare il file **NPP. 7.6.3. Installer. x64. intunewin** nella cartella di output, aprirlo e quindi fare clic su **OK**:

![Aggiungere l'app](images/app04.png)

Nel pannello **informazioni sull'app configurare** specificare un nome descrittivo, una descrizione e un server di pubblicazione, ad esempio:

![Aggiungere l'app](images/app05.png)

Nel pannello **Configurazione programma** specificare i comandi di installazione e disinstallazione:

Installazione: msiexec/i "npp.7.6.3.installer.x64.msi"/q Uninstall: msiexec/x "{F188A506-C3C6-4411-BE3A-DA5BF1EA6737}"/q

> [!NOTE]
> È probabile che non sia necessario scrivere i comandi di installazione e disinstallazione manualmente, perché lo [strumento da riga di comandoIntuneWinAppUtil.exe](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) li ha generati automaticamente durante la conversione del file con estensione msi in un file con estensione intunewin.

![Aggiungere l'app](images/app06.png)

Se si usa semplicemente un comando di installazione come "Notepad + +. exe/S", non verrà installato il blocco note + +; verrà avviata solo l'app.  Per installare effettivamente il programma, è necessario usare invece il file con estensione msi.  Notepad + + non dispone effettivamente di una versione MSI del programma, ma è stata ottenuta una versione MSI da un [provider di terze parti](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available).

Fare clic su **OK** per salvare l'input e attivare il pannello **requisiti** .

Nel pannello **configurazione requisiti** specificare l'architettura del **sistema operativo** e la **versione minima del sistema operativo**:

![Aggiungere l'app](images/app07.png)

Successivamente, configurare le **regole di rilevamento**.  A questo scopo, si selezionerà il formato manuale:

![Aggiungere l'app](images/app08.png)

Fare clic su **Aggiungi** per definire le proprietà della regola.  Per **tipo di regola**selezionare **MSI**, che importerà automaticamente il codice prodotto MSI corretto nella regola:

![Aggiungere l'app](images/app09.png)

Fare clic su **OK** due volte per salvare, mentre si torna al pannello principale **Aggiungi app** per la configurazione finale.

**Codici restituiti**: per i nostri scopi, lasciare i valori predefiniti dei codici restituiti:

![Aggiungere l'app](images/app10.png)

Fare clic su **OK** per uscire.

È possibile ignorare la configurazione del pannello finale dell' **ambito (tag)** .

Fare clic sul pulsante **Aggiungi** per completare e salvare il pacchetto dell'app.

Quando il messaggio dell'indicatore indica che l'aggiunta è stata completata.

![Aggiungere l'app](images/app11.png)

Sarà possibile trovare l'app nell'elenco di app:

![Aggiungere l'app](images/app12.png)

#### <a name="assign-the-app-to-your-intune-profile"></a>Assegnare l'app al profilo di Intune

> [!NOTE]
> I passaggi seguenti funzionano solo se in precedenza è [stato creato un gruppo in Intune a cui è stato assegnato un profilo](#assign-the-profile).  Se non è stato fatto, tornare alla parte principale del Lab e completare i passaggi prima di tornare qui.

Nel riquadro app **Client > app > di Intune** selezionare il pacchetto dell'app già creato per visualizzare il relativo pannello Proprietà.  Fare quindi clic su **assegnazioni** dal menu:

![Aggiungere l'app](images/app13.png)

Selezionare **Aggiungi gruppo** per aprire il riquadro **Aggiungi gruppo** relativo all'app.

Per questo scopo, selezionare **obbligatorio** dal menu a discesa **tipo di assegnazione** :

> **Disponibile per i dispositivi registrati** significa che gli utenti installano l'app dall'app portale aziendale o dal sito web di portale aziendale.

Selezionare **gruppi inclusi** e assegnare i gruppi creati in precedenza che useranno l'app:

![Aggiungere l'app](images/app14.png)

![Aggiungere l'app](images/app15.png)

Nel riquadro **Seleziona gruppi** fare clic sul pulsante **Seleziona** .

Nel riquadro **assegna gruppo** fare clic su **OK**.

Nel riquadro **Aggiungi gruppo** selezionare **OK**.

Nel riquadro **Assegnazioni** dell'app selezionare **Salva**.

![Aggiungere l'app](images/app16.png)

A questo punto, sono stati completati i passaggi per l'aggiunta di un'app Win32 a Intune.

Per altre informazioni sull'aggiunta di app a Intune, vedere [Intune autonomo-gestione delle app Win32](https://docs.microsoft.com/intune/apps-win32-app-management).

### <a name="add-office-365"></a>Aggiungi Office 365

#### <a name="create-app-in-intune"></a>Creare un'app in Intune

Accedere al portale di Azure e selezionare **Intune**.

Passare a **Intune > client app > app**, quindi fare clic sul pulsante **Aggiungi** per creare un nuovo pacchetto dell'app.

![Aggiungere l'app](images/app17.png)

In **tipo di app**selezionare **Office 365 Suite > Windows 10**:

![Aggiungere l'app](images/app18.png)

Nel riquadro **Configura suite di app** selezionare le app di Office che si vuole installare.  Ai fini di questo oggetto Label è stato selezionato solo Excel:

![Aggiungere l'app](images/app19.png)

Fare clic su **OK**.

Nel riquadro **informazioni della suite di app** immettere un nome di gruppo <i>univoco</i> e una descrizione appropriata.

> immettere il nome della suite di app visualizzato nel portale aziendale. Verificare che tutti i nomi di suite usati siano univoci. Se il nome di una suite viene usato due volte, solo una delle due suite viene visualizzata dagli utenti nel portale aziendale.

![Aggiungere l'app](images/app20.png)

Fare clic su **OK**.

Nel riquadro **impostazioni della suite di app** selezionare **mensile** per il **canale di aggiornamento** (qualsiasi selezione sarebbe corretta per gli scopi di questo Lab).  Selezionare anche **Sì** per **accettare automaticamente il contratto di licenza con l'utente finale dell'app**:

![Aggiungere l'app](images/app21.png)

Fare clic su **OK** e quindi su **Aggiungi**.

#### <a name="assign-the-app-to-your-intune-profile"></a>Assegnare l'app al profilo di Intune

> [!NOTE]
> I passaggi seguenti funzionano solo se in precedenza è [stato creato un gruppo in Intune a cui è stato assegnato un profilo](#assign-the-profile).  Se non è stato fatto, tornare alla parte principale del Lab e completare i passaggi prima di tornare qui.

Nel riquadro **app Client > app > di Intune** selezionare il pacchetto di Office già creato per visualizzare il relativo pannello Proprietà.  Fare quindi clic su **assegnazioni** dal menu:

![Aggiungere l'app](images/app22.png)

Selezionare **Aggiungi gruppo** per aprire il riquadro **Aggiungi gruppo** relativo all'app.

Per questo scopo, selezionare **obbligatorio** dal menu a discesa **tipo di assegnazione** :

> **Disponibile per i dispositivi registrati** significa che gli utenti installano l'app dall'app portale aziendale o dal sito web di portale aziendale.

Selezionare **gruppi inclusi** e assegnare i gruppi creati in precedenza che useranno l'app:

![Aggiungere l'app](images/app23.png)

![Aggiungere l'app](images/app24.png)

Nel riquadro **Seleziona gruppi** fare clic sul pulsante **Seleziona** .

Nel riquadro **assegna gruppo** fare clic su **OK**.

Nel riquadro **Aggiungi gruppo** selezionare **OK**.

Nel riquadro **Assegnazioni** dell'app selezionare **Salva**.

![Aggiungere l'app](images/app25.png)

A questo punto, sono stati completati i passaggi per aggiungere Office a Intune.

Per altre informazioni sull'aggiunta di app di Office a Intune, vedere [assegnare le app di office 365 ai dispositivi Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

Se sono state installate sia l'app Win32 (Notepad + +) che Office (solo Excel) in base alle istruzioni in questo Lab, la macchina virtuale li visualizzerà nell'elenco delle app, anche se potrebbero essere necessari alcuni minuti per popolare:

![Aggiungere l'app](images/app26.png)

## <a name="glossary"></a>Glossario

<table border="1">
<tr><td>OEM</td><td>Produttore attrezzature originale</td></tr>
<tr><td>CSV</td><td>Valori delimitati da virgole</td></tr>
<tr><td>MPC</td><td>Microsoft Partner Center</td></tr>
<tr><td>CSP</td><td>Provider di soluzioni cloud</td></tr>
<tr><td>MSfB</td><td>Microsoft Store per le aziende</td></tr>
<tr><td>AAD</td><td>Azure Active Directory</td></tr>
<tr><td>HH 4K</td><td>Hash hardware 4K</td></tr>
<tr><td>CBR</td><td>Report compilazione computer</td></tr>
<tr><td>EC</td><td>Enterprise Commerce (Server)</td></tr>
<tr><td>DDS</td><td>Servizio directory dispositivo</td></tr>
<tr><td>OOBE</td><td>Esperienza predefinita</td></tr>
<tr><td>VM</td><td>Macchina virtuale</td></tr>
</table>
