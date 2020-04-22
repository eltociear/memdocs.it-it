---
title: Sincronizzare gli aggiornamenti di Office 365 senza una connessione Internet
titleSuffix: Configuration Manager
description: Sincronizzare gli aggiornamenti di Office 365 nel punto di aggiornamento software di livello superiore disconnesso da Internet.
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 78b97be755659fa06466dd1bb1f6920e2a7be330
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699469"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a> Sincronizzare gli aggiornamenti di Office 365 da un punto di aggiornamento software disconnesso

*Si applica a: Configuration Manager (Current Branch)*
<!--4065163-->
A partire da Configuration Manager versione 2002, è possibile usare uno strumento per importare gli aggiornamenti di Office 365 da un server WSUS connesso a Internet in un ambiente di Configuration Manager disconnesso. In passato, quando si esportavano e importavano i metadati per il software aggiornato in ambienti disconnessi, non era possibile distribuire gli aggiornamenti di Office 365. Gli aggiornamenti di Office 365 richiedono metadati aggiuntivi scaricati da un'API di Office e dalla rete CDN di Office, operazione impossibile per gli ambienti disconnessi.

## <a name="prerequisites"></a>Prerequisiti

- Un server WSUS connesso a Internet che esegue almeno Windows Server 2012.
- Il server WSUS richiede la connettività a questi due endpoint Internet:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Copiare lo strumento OfflineUpdateExporter e le relative dipendenze nel server WSUS connesso a Internet.
  - Lo strumento e le relative dipendenze si trovano nella directory **&lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter**.
- È necessario che l'utente che esegue lo strumento faccia parte del gruppo **WSUS Administrators**.
- La directory creata per archiviare i metadati e il contenuto di aggiornamento di Office deve disporre degli elenchi di controllo di accesso (ACL) appropriati per proteggere i file.
    - È anche necessario che la directory sia vuota.
- I dati spostati dal server WSUS online nell'ambiente disconnesso devono essere trasferiti in modo sicuro.

> [!IMPORTANT]
> Il contenuto verrà scaricato per tutte le lingue di Office 365. Ogni aggiornamento può avere circa 10 GB di contenuto.

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>Sincronizzare e rifiutare gli aggiornamenti di Office 365 non necessari

1. Nel server WSUS connesso a Internet aprire la console WSUS.
1. Selezionare **Opzioni**, quindi **Prodotti e classificazioni**.
1. Nella scheda **Prodotti** selezionare **Client Office 365** e selezionare **Aggiornamenti** nella scheda **Classificazioni**. [![Prodotti e classificazioni per gli aggiornamenti di Office 365 in WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Passare a **Sincronizzazioni** e selezionare **Sincronizza** per ottenere gli aggiornamenti di Office 365 in WSUS.
1. Al termine della sincronizzazione, rifiutare gli aggiornamenti di Office 365 che non devono essere distribuiti con Configuration Manager. Non è necessario approvare gli aggiornamenti di Office 365 per poterli scaricare.  
   - Il rifiuto degli aggiornamenti di Office 365 non necessari in WSUS, non ne impedisce l'esportazione durante un'esportazione WsusUtil.exe, ma impedisce allo strumento OfflineUpdateExporter di scaricarne il contenuto.
   - Lo strumento OfflineUpdateExporter scarica gli aggiornamenti di Office 365. Sarà comunque necessario approvare il download per altri prodotti, se si esportano i relativi aggiornamenti.
    - Creare una [nuova visualizzazione per gli aggiornamenti in WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) per visualizzare e rifiutare facilmente gli aggiornamenti di Office 365 non necessari in WSUS.
1. Se si stanno approvando il download e l’esportazione di altri aggiornamenti di prodotto, attendere il completamento del download del contenuto prima di eseguire l’esportazione WsusUtil.exe e copiare il contenuto della cartella WSUSContent. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso](synchronize-software-updates-disconnected.md).

## <a name="exporting-the-office-365-updates"></a>Esportazione degli aggiornamenti di Office 365

1. Copiare la cartella OfflineUpdateExporter da Configuration Manager nel server WSUS connesso a Internet.
    - Lo strumento e le relative dipendenze si trovano nella directory **&lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter**.
1. Da un prompt dei comandi nel server WSUS connesso a Internet eseguire lo strumento con l'utilizzo seguente: **OfflineUpdateExporter.exe -O -D &lt;percorso di destinazione>**

   |Parametro OfflineUpdateExporter|Descrizione|
   |---|---|
   |**-O**|  **-Office**. Specifica se il prodotto per l'esportazione degli aggiornamenti è Office 365|
   |**-D**|**-Destination**. La destinazione è un parametro obbligatorio ed è necessario specificare il percorso completo della cartella di destinazione.|

   - Lo strumento **OfflineUpdateExporter** esegue le operazioni seguenti:
      - Si connette a WSUS
      - Legge i metadati di aggiornamento di Office 365 in WSUS
      - Scarica il contenuto ed eventuali metadati aggiuntivi necessari per gli aggiornamenti di Office 365 nella cartella di destinazione

1. Al prompt dei comandi nel server WSUS connesso a Internet passare alla cartella che contiene WsusUtil.exe. Per impostazione predefinita, lo strumento si trova in %*ProgramFiles*%\Update Services\Tools. Ad esempio, se lo strumento si trova nel percorso predefinito, digitare **cd %ProgramFiles%\Update Services\Tools**.
   - Se si usa Windows Server 2012, assicurarsi che l'aggiornamento [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) sia installato nei server WSUS.
   - L’utente che esegue lo strumento WsusUtil deve essere un membro del gruppo Administrators locale nel server.

1. Digitare quanto segue per esportare i metadati degli aggiornamenti software in un file GZIP:  

    **WsusUtil.exe export**  *nomepacchetto*  *filelog*  

    Ad esempio:  

    **WsusUtil.exe export export.xml.gz export.log**

1. Copiare il file **export.xml.gz** nel server WSUS di livello superiore nella rete disconnessa.
1. Se sono stati approvati aggiornamenti per altri prodotti, copiare il contenuto della cartella WSUSContent nella cartella WSUSContent del server WSUS disconnesso di livello superiore.
1. Copiare la cartella di destinazione usata per **OfflineUpdateExporter** nel server del sito di Configuration Manager di livello superiore nella rete disconnessa.

## <a name="import-the-office-365-updates"></a>Importare gli aggiornamenti di Office 365

1. Nel server WSUS disconnesso di livello superiore importare i metadati di aggiornamento dal file **export.xml.gz** generato nel server WSUS connesso a Internet.
   
    Ad esempio:  

    **WsusUtil.exe import export.xml.gz import.log**
    
    Per impostazione predefinita, lo strumento WsusUtil.exe si trova in %*ProgramFiles*%\Update Services\Tools.

1. Al termine dell'importazione, è necessario configurare una proprietà di controllo del sito nel server del sito di Configuration Manager disconnesso di livello superiore. Questa modifica di configurazione indirizza Configuration Manager al contenuto per Office 365. Per modificare la configurazione della proprietà:
   1. Copiare lo [script di PowerShell O365OflBaseUrlConfigured](#bkmk_o365_script) nel server del sito di Configuration Manager disconnesso di livello superiore.
   1. Modificare `"D:\Office365updates\content"` nel percorso completo della directory copiata contenente il contenuto e i metadati di Office generati da OfflineUpdateExporter.
      > [!IMPORTANT]
      > Solo i percorsi locali funzionano per la proprietà O365OflBaseUrlConfigured.
   1. Salvare lo script come `O365OflBaseUrlConfigured.ps1`
   1. Da una finestra di PowerShell con privilegi elevati nel server del sito di Configuration Manager disconnesso di livello superiore eseguire `.\O365OflBaseUrlConfigured.ps1`.
   1. Riavviare il servizio **SMS_Executive** nel server del sito.
1. Nella console di **Configuration Manager** passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.
1. Fare clic con il pulsante destro del mouse sul sito di livello superiore e scegliere **Configura componenti del sito** > **Punto di aggiornamento software**.
1. Nella scheda **Classificazioni** selezionare *Aggiornamenti*. Nella scheda **Prodotti** selezionare *Client Office 365*.
1. [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md#manually-start-software-updates-synchronization) per Configuration Manager
1. Al termine della sincronizzazione, usare il normale processo per distribuire gli aggiornamenti di Office 365.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a> Configurazione proxy

- La configurazione del proxy non è incorporata in modo nativo nello strumento. Se il proxy è impostato nelle opzioni Internet del server in cui viene eseguito lo strumento, teoricamente verrà usato e dovrebbe funzionare correttamente.
   - Da un prompt dei comandi eseguire `netsh winhttp show proxy` per visualizzare il proxy configurato.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a> Modificare la proprietà O365OflBaseUrlConfigured

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Passaggi successivi

[Aggiungere aggiornamenti software a un gruppo di aggiornamento](../deploy-use/add-software-updates-to-an-update-group.md)