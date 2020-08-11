---
title: Aggiunta di dispositivi
ms.reviewer: ''
manager: laurawi
description: Come aggiungere dispositivi a Windows Autopilot
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: fc892a4372aa7d72f294ddf93f811d641ca961b5
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051425"
---
# <a name="adding-devices-to-windows-autopilot"></a>Aggiunta di dispositivi a Windows Autopilot

**Si applica a**

- Windows 10

Prima di distribuire un dispositivo usando Windows Autopilot, il dispositivo deve essere registrato con il servizio di distribuzione di Windows Autopilot. Idealmente, questa operazione verrebbe eseguita dall'OEM, dal rivenditore o dal server di distribuzione da cui sono stati acquistati i dispositivi, ma questa operazione può essere eseguita anche dall'organizzazione raccogliendo l'identità hardware e caricando manualmente tale identità.

## <a name="oem-registration"></a>Registrazione OEM

Quando si acquistano dispositivi direttamente da un OEM, l'OEM può registrare automaticamente i dispositivi con il servizio di distribuzione di Windows Autopilot.  Per l'elenco degli OEM che attualmente lo supportano, vedere la sezione "produttori di dispositivi partecipanti e rivenditori" della pagina delle [informazioni di Windows Autopilot](https://aka.ms/windowsautopilot).

Prima che un OEM possa registrare i dispositivi per conto di un'organizzazione, l'organizzazione deve concedere l'autorizzazione OEM a tale scopo.  Questo processo viene avviato dall'OEM, con approvazione concessa da un Azure AD amministratore globale dell'organizzazione.  Vedere la sezione "consenso del cliente" della [pagina di consenso del cliente](registration-auth.md#oem-authorization).

> [!Note]
> Mentre gli hash hardware vengono generati come parte del processo di produzione dei dispositivi OEM, questi non devono essere forniti direttamente ai clienti o ai partner CSP.  Al contrario, l'OEM deve registrare i dispositivi per conto del cliente.  Nei casi in cui i dispositivi vengono registrati da partner CSP, gli OEM possono fornire a tali partner informazioni PKID per supportare il processo di registrazione del dispositivo.

## <a name="reseller-distributor-or-partner-registration"></a>Rivenditore, distributore o registrazione partner

I clienti possono acquistare dispositivi da rivenditori, distributori o altri partner.  Fino a quando questi rivenditori, distributori e partner fanno parte del [programma Cloud Solution Partner (CSP)](https://partner.microsoft.com/cloud-solution-provider), possono anche registrare i dispositivi per conto del cliente.  

Come per gli OEM, ai partner CSP deve essere concessa l'autorizzazione per registrare i dispositivi per conto di un'organizzazione.  Segue il processo descritto nella pagina di [consenso del cliente](registration-auth.md#csp-authorization).  Il partner CSP avvia una richiesta di stabilire una relazione con l'organizzazione, con l'approvazione concessa da un amministratore globale dell'organizzazione.  Una volta approvata, i partner CSP aggiungono dispositivi tramite il centro per i [partner](https://partner.microsoft.com/pcv/dashboard/overview), direttamente tramite il sito Web o tramite API disponibili che consentono di automatizzare le stesse attività.

Windows Autopilot non richiede autorizzazioni di amministratore delegato quando stabilisce la relazione tra il partner CSP e l'organizzazione.  Nell'ambito del processo di approvazione eseguito dall'amministratore globale, l'amministratore globale può scegliere di deselezionare la casella di controllo "Includi autorizzazioni amministrative delegate".

> [!Note]
> Mentre i rivenditori, i distributori o i partner possono avviare ogni nuovo dispositivo Windows per ottenere l'hash hardware (per fornire loro i clienti o la registrazione diretta dal partner), questa operazione non è consigliata.  Al contrario, questi partner devono registrare i dispositivi usando le informazioni PKID ottenute dal pacchetto di dispositivi (codice a barre) o ottenute elettronicamente dall'OEM o dal partner upstream (ad esempio, Distributor).

## <a name="automatic-registration-of-existing-devices"></a>Registrazione automatica dei dispositivi esistenti

Se un dispositivo esistente sta già eseguendo una versione supportata del canale semestrale di Windows 10 e registrato in un servizio MDM quale Intune, il servizio MDM può chiedere al dispositivo l'ID hardware (noto anche come hash hardware).  Al termine, può registrare automaticamente il dispositivo con Windows Autopilot.

Per istruzioni su come eseguire questa operazione con Microsoft Intune, vedere la pagina relativa alla [creazione di un profilo di distribuzione Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) che descrive l'impostazione "Converti tutti i dispositivi di destinazione in Autopilot". 

Si noti inoltre che quando si utilizza lo scenario [Windows Autopilot for existing devices](existing-devices.md) , non è necessario pre-registrare i dispositivi con Windows Autopilot.  Viene invece utilizzato un file di configurazione (AutopilotConfigurationFile.js) contenente tutte le impostazioni del profilo di Windows Autopilot; il dispositivo può essere registrato con Windows Autopilot dopo il fatto che usa la stessa impostazione "Converti tutti i dispositivi di destinazione in Autopilot".

## <a name="manual-registration"></a>Registrazione manuale

Per eseguire la registrazione manuale di un dispositivo, è prima necessario acquisire il relativo ID hardware (noto anche come hash hardware).  Al termine del processo, l'ID hardware risultante può essere caricato nel servizio Windows Autopilot.  Poiché questo processo richiede l'avvio del dispositivo in Windows 10 per ottenere l'ID hardware, questo è destinato principalmente a scenari di test e valutazione.

> [!Note]
> I clienti possono registrare i dispositivi solo con un hash hardware.  Altri metodi (PKID, Tuple) sono disponibili tramite OEM o partner CSP, come descritto nelle sezioni precedenti.

## <a name="device-identification"></a>Identificazione del dispositivo

Per definire un dispositivo per il servizio di distribuzione di Windows Autopilot, è necessario acquisire e caricare nel servizio un ID hardware univoco per il dispositivo. Sebbene questo passaggio sia idealmente eseguito dal fornitore di hardware (OEM, rivenditore o distributore), associando automaticamente il dispositivo a un'organizzazione, è anche possibile eseguire questa operazione tramite un processo di raccolta che raccoglie il dispositivo dall'interno di un'installazione di Windows 10 in esecuzione.

L'ID hardware, noto anche come hash hardware, contiene diversi dettagli sul dispositivo, inclusi il produttore, il modello, il numero di serie del dispositivo, il numero di serie del disco rigido e molti altri attributi che possono essere usati per identificare in modo univoco il dispositivo.

Si noti che l'hash hardware contiene anche i dettagli relativi al momento in cui è stato generato, quindi verrà modificato ogni volta che viene generato. Quando il servizio di distribuzione di Windows Autopilot tenta di trovare la corrispondenza con un dispositivo, considera le modifiche simili, oltre a modifiche più sostanziali, ad esempio un nuovo disco rigido, ed è ancora in grado di trovare una corrispondenza corretta. Tuttavia, le modifiche sostanziali apportate all'hardware, ad esempio la sostituzione di una scheda madre, non corrispondono, quindi è necessario generare e caricare un nuovo hash.

### <a name="collecting-the-hardware-id-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Raccolta dell'ID hardware dai dispositivi esistenti utilizzando Microsoft endpoint Configuration Manager

Microsoft endpoint Configuration Manager raccoglie automaticamente gli hash hardware per i dispositivi Windows 10 esistenti. Per ulteriori informazioni, vedere [raccogliere informazioni da Configuration Manager per Windows Autopilot](https://docs.microsoft.com/configmgr/comanage/how-to-prepare-win10#windows-autopilot). È possibile estrarre le informazioni hash da Configuration Manager in un file CSV.

> [!Note]
> Prima di caricare il file CSV in Intune, assicurarsi che la prima riga contenga il numero di serie del dispositivo, l'ID prodotto Windows, l'hash hardware, il tag di gruppo e l'utente assegnato. Se sono presenti informazioni di intestazione nella parte superiore del file CSV, eliminare le informazioni di intestazione. Vedere i dettagli in [registrare i dispositivi Windows in Intune](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot).

### <a name="collecting-the-hardware-id-from-existing-devices-using-powershell"></a>Raccolta dell'ID hardware dai dispositivi esistenti tramite PowerShell

L'ID hardware o l'hash hardware per un dispositivo esistente è disponibile tramite Strumentazione gestione Windows (WMI), purché il dispositivo esegua una versione supportata del canale semestrale di Windows 10. Per raccogliere queste informazioni, nonché il numero di serie del dispositivo (utile per visualizzare immediatamente il computer a cui appartiene), uno script di PowerShell denominato [Get-WindowsAutoPilotInfo.ps1 è stato pubblicato nel sito Web di PowerShell Gallery](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo).

Per usare questo script, è possibile scaricarlo dalla PowerShell Gallery ed eseguirlo in ogni computer oppure è possibile installarlo direttamente dalla PowerShell Gallery. Per installarlo direttamente e acquisire l'hash hardware dal computer locale, usare i comandi seguenti da un prompt di Windows PowerShell con privilegi elevati:

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

I comandi possono essere eseguiti anche in modalità remota, purché siano disponibili le autorizzazioni WMI e WMI sia accessibile tramite il Windows Firewall nel computer remoto. Per ulteriori informazioni sull'esecuzione dello script, vedere la guida dello script [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) (tramite "Get-Help Get-WindowsAutoPilotInfo.ps1").

>[!IMPORTANT]
>Non connettere i dispositivi a Internet prima di acquisire l'ID hardware e creare un profilo di dispositivo Autopilot. Ciò include la raccolta dell'ID hardware, il caricamento di. CSV in MSfB o Intune, assegnazione del profilo e conferma dell'assegnazione del profilo. La connessione del dispositivo a Internet prima del completamento di questo processo comporterà il download del dispositivo di un profilo vuoto archiviato nel dispositivo fino a quando non viene rimosso in modo esplicito. In Windows 10 versione 1809 è possibile cancellare il profilo memorizzato nella cache riavviando la configurazione guidata. Nelle versioni precedenti, l'unico modo per cancellare il profilo archiviato consiste nel reinstallare il sistema operativo, ricreare l'immagine del PC oppure eseguire **sysprep/generalize/oobe**. <br>
>Dopo che Intune ha segnalato il profilo pronto per l'uso, solo il dispositivo deve essere connesso a Internet.

>[!NOTE]
>Se OOBE viene riavviato troppe volte, può accedere a una modalità di ripristino e non eseguire la configurazione di Autopilot. È possibile identificare questo scenario se OOBE Visualizza più opzioni di configurazione nella stessa pagina, tra cui la lingua, l'area e il layout di tastiera. Il file OOBE normale Visualizza ognuno di questi in una pagina separata. La chiave di valore seguente tiene traccia del numero di tentativi di configurazione guidata: <br>
>**HKCU\SOFTWARE \\ Microsoft \\ Windows \\ CurrentVersion \\ UserOOBE** <br>
>Per assicurarsi che la configurazione guidata non sia stata riavviata troppe volte, è possibile impostare questo valore su 1.

## <a name="registering-devices"></a>Registrazione dei dispositivi

<img src="./images/image2.png" width="511" height="249" alt="process" />


Quando gli ID hardware sono stati acquisiti da dispositivi esistenti, possono essere caricati con diversi mezzi. Vedere la documentazione dettagliata per ogni meccanismo disponibile.

-   [Microsoft Intune](enrollment-autopilot.md).  Questo è il meccanismo preferito per tutti i clienti.
    - L'interfaccia di amministrazione di Microsoft Endpoint Manager viene usata per la registrazione dei dispositivi in Intune.
-   [Centro](https://msdn.microsoft.com/partner-center/autopilot)per i partner.  Viene usato dai partner CSP per registrare i dispositivi per conto dei clienti.
-   [Microsoft 365 Business & amministratore di Office 365](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa).  Questa operazione viene in genere usata da piccole e medie imprese (PMI) che gestiscono i propri dispositivi usando Microsoft 365 Business.
-   [Microsoft Store per le aziende](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles).  È possibile che si stia già usando MSfB per gestire le app e le impostazioni.

Di seguito è riportato un riepilogo delle funzionalità di ogni piattaforma.<br>
<br>
<table>
<tr>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Piattaforma/portale</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Registrare i dispositivi?</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Crea/Assegna profilo</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">DeviceID accettabile</font></td>
</tr>

<tr>
<td>API diretta OEM</td>
<td>Sì-1000 alla volta Max</td>
<td>NO</td>
<td>Tupla o PKID</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/partner-center/autopilot">Centro per i partner</a></td>
<td>Sì-1000 alla volta Max</td>
<td>Sì<b><sup>34</sup></b></td>
<td>Tupla o PKID o 4K HH</td>
</tr>

<tr>
<td><a href="enrollment-autopilot.md">Intune</a></td>
<td>Sì-500 alla volta Max<b><sup>1</sup></b></td> 
<td>Sì<b><sup>12</sup></b></td> 
<td>HH 4K</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">Microsoft Store per le aziende</a></td>
<td>Sì-1000 alla volta Max</td>
<td>Sì<b><sup>4</sup></b></td>
<td>HH 4K</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business</a></td>
<td>Sì-1000 alla volta Max</td>
<td>Sì<b><sup>3</sup></b></td>
<td>HH 4K</td>
</tr>

</table>

><b><sup>1</sup></b> Piattaforma consigliata da Microsoft per l'uso<br>
><b><sup>2</sup></b> Licenza di Intune obbligatoria<br>
><b><sup>3</sup></b> Le funzionalità sono limitate<br>
><b><sup>4</sup></b> L'assegnazione del profilo dispositivo verrà ritirata da MSfB e dal centro per i partner nei prossimi mesi<br>


Per ulteriori informazioni sugli ID dispositivo, vedere anche gli argomenti seguenti:
- [Identificazione del dispositivo](#device-identification)
- [Linee guida sui dispositivi di Windows Autopilot](autopilot-device-guidelines.md)
- [Aggiungere dispositivi a un account cliente](https://docs.microsoft.com/partner-center/autopilot)


## <a name="summary"></a>Riepilogo

Quando si distribuiscono nuovi dispositivi con Windows Autopilot, è necessario eseguire i passaggi seguenti:

1.  [Registrare i dispositivi](#registering-devices). Idealmente, questo passaggio viene eseguito dall'OEM, dal rivenditore o dal distributore dal quale sono stati acquistati i dispositivi, ma questa operazione può essere eseguita anche dall'organizzazione raccogliendo l'identità hardware e caricando manualmente l'identità.
2.  [Configurare i profili di dispositivo](profiles.md), specificando la modalità di distribuzione del dispositivo e l'esperienza utente da presentare.
3.  Avviare il dispositivo. Quando il dispositivo è connesso a una rete con accesso a Internet, contatterà il servizio di distribuzione di Windows Autopilot per verificare se il dispositivo è registrato e, in tal caso, scaricherà le impostazioni del profilo, ad esempio la [pagina relativa allo stato della registrazione](enrollment-status.md), che consente di personalizzare l'esperienza dell'utente finale.

## <a name="other-configuration-settings"></a>Altre impostazioni di configurazione

- [Impostazioni di crittografia di BitLocker](bitlocker.md): è possibile configurare le impostazioni di crittografia di BitLocker da applicare prima dell'avvio della crittografia automatica.