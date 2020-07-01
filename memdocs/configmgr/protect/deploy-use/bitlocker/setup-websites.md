---
title: Configurare i portali di BitLocker
titleSuffix: Configuration Manager
description: Installare i componenti di gestione BitLocker per il portale self-service e il sito Web di amministrazione e monitoraggio
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53fc4f694579fb8c53a4aea1054cf49dff21e1d2
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715680"
---
# <a name="set-up-bitlocker-portals"></a>Configurare i portali di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Per usare i componenti di gestione di BitLocker seguenti in Configuration Manager, è prima necessario installarli:

- Portale self-service degli utenti
- Account del sito Web di amministrazione e monitoraggio (portale supporto tecnico)

È possibile installare i portali in un server del sito o in un server di sistema del sito esistenti con ISS installato oppure usare un server Web autonomo per ospitarli.

> [!NOTE]
> Installare solo il portale self-service e il sito Web di amministrazione e monitoraggio con un database del sito primario. In una gerarchia installare questi siti Web per ogni sito primario.

Prima di iniziare, verificare i [prerequisiti](../../plan-design/bitlocker-management.md#prerequisites) per questi componenti.

## <a name="script-usage"></a>Uso degli script

Questo processo usa uno script di PowerShell, MBAMWebSiteInstaller.ps1, per installare questi componenti nel server Web. I parametri accettati sono i seguenti:

- `-SqlServerName <ServerName>` (obbligatorio): nome di dominio completo del server di database del sito primario.

- `-SqlInstanceName <InstanceName>`: il nome dell'istanza di SQL Server per il database del sito primario. Se SQL usa l'istanza predefinita, non includere questo parametro.

- `-SqlDatabaseName <DatabaseName>` (obbligatorio): nome del database del sito primario, ad esempio `CM_ABC`.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: URL del servizio Web del punto di Reporting Services del sito primario. Si tratta del valore **URL servizio Web** in **Gestione configurazione Reporting Services**.

    > [!NOTE]
    > Questo parametro consente di installare il **Report controllo del ripristino** collegato dal sito Web Amministrazione e monitoraggio. Per impostazione predefinita Configuration Manager include gli altri report di gestione di BitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Ad esempio, `contoso\BitLocker help desk users` Gruppo utenti di dominio i cui membri hanno accesso alle aree **Manage TPM** (Gestisci TPM) e **Drive Recovery** (Ripristino unità) nel sito Web di amministrazione e monitoraggio. Quando si usano queste opzioni, questo ruolo deve compilare tutti i campi, inclusi il dominio e il nome dell'account dell'utente.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Ad esempio, `contoso\BitLocker help desk admins` Gruppo utenti di dominio i cui membri hanno accesso alle aree di ripristino del sito Web di amministrazione e monitoraggio. Per consentire agli utenti di ripristinare le unità, questo ruolo deve solo immettere la chiave di ripristino.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Ad esempio, `contoso\BitLocker report users` Gruppo utenti di dominio i cui membri hanno accesso in sola lettura all'area **Report** del sito Web di amministrazione e monitoraggio.

    > [!NOTE]
    > Lo script del programma di installazione non crea i gruppi di utenti di dominio specificati nei parametri **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName** e **-MbamReportUsersGroupName**. Prima di eseguire lo script, assicurarsi di creare questi gruppi.
    >
    > Quando si specificano i parametri **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName** e **-MbamReportUsersGroupName** assicurarsi di specificare sia il nome di dominio sia il nome di gruppo. Usare il formato `"domain\user_group"`. Non escludere il nome di dominio. Se il nome di dominio o il nome di gruppo contiene spazi o caratteri speciali, racchiudere il parametro tra virgolette (`"`).

- `-SiteInstall Both`: specificare quale componente installare. Le opzioni valide includono:
  - `Both`: installare entrambi i componenti
  - `HelpDesk`: installare solo il sito Web di amministrazione e monitoraggio
  - `SSP`: installare solo il portale self-service

- `-IISWebSite`: il sito Web in cui lo script installa le applicazioni Web di MBAM. Per impostazione predefinita, usa il sito Web IIS predefinito. Creare il sito Web personalizzato prima di usare questo parametro.

- `-InstallDirectory`: il percorso in cui lo script installa i file dell'applicazione Web. Per impostazione predefinita, il percorso è `C:\inetpub`. Creare la directory personalizzata prima di usare questo parametro.

- `-Uninstall`: disinstalla i siti del portale Web help desk/self-service di Gestione di BitLocker da un server Web in cui sono stati installati in precedenza.


## <a name="run-the-script"></a>Eseguire lo script

Nel server Web di destinazione eseguire le operazioni seguenti:

> [!NOTE]
> A seconda della progettazione del sito, potrebbe essere necessario eseguire più volte lo script. Ad esempio, eseguire lo script nel punto di gestione per installare il sito Web di Amministrazione e monitoraggio. Quindi eseguirlo di nuovo in un server Web autonomo per installare il portale self-service.

1. Copiare i file seguenti da `SMSSETUP\BIN\X64` nella cartella di installazione Configuration Manager del server del sito a una cartella locale nel server di destinazione:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Eseguire PowerShell come amministratore e quindi eseguire lo script in modo simile alla riga di comando seguente:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Ad esempio:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > Questa riga di comando di esempio usa tutti i parametri possibili per illustrarne l'uso. Adattare l'uso ai requisiti dell'ambiente.

Una volta eseguita l'installazione, accedere ai portali tramite gli URL seguenti:

- Portale self-service: `https://webserver.contoso.com/SelfService`
- Sito Web di amministrazione e monitoraggio: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> L'uso di HTTPS è consigliato ma non obbligatorio. Per altre informazioni, vedere [Come configurare SSL in IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="verify"></a>Verifica

Per eseguire monitoraggio e risoluzione dei problemi usare i registri seguenti:

- Registri eventi di Windows in **Microsoft-Windows-MBAM-Web**. Per altre informazioni, vedere [Informazioni sui registri eventi di BitLocker](../../tech-ref/bitlocker/about-event-logs.md) e [Registri eventi del server](../../tech-ref/bitlocker/server-event-logs.md).

- I log di analisi per ogni componente si trovano nei percorsi predefiniti seguenti:

  - Portale self-service: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Sito Web di amministrazione e monitoraggio: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Per altre informazioni sulla risoluzione dei problemi, vedere [Risolvere i problemi relativi a BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Passaggi successivi

[Personalizzare il portale self-service](customize-self-service-portal.md)

Per altre informazioni sull'uso dei componenti installati, vedere gli articoli seguenti:

- [Sito Web di amministrazione e monitoraggio BitLocker](helpdesk-portal.md)
- [Portale self-service di BitLocker](self-service-portal.md)
