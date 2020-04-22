---
title: Account usati
titleSuffix: Configuration Manager
description: Identificare e gestire i gruppi di Windows, gli account e gli oggetti SQL usati in Configuration Manager.
ms.date: 10/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0cfc9ee0fe80aa39ba49b25c392334a01169a8a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703769"
---
# <a name="accounts-used-in-configuration-manager"></a>Account usati in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni seguenti per identificare i gruppi di Windows, gli account e gli oggetti SQL usati in Configuration Manager, le relative modalità d'uso e gli eventuali requisiti.  

- [Gruppi Windows creati e usati da Configuration Manager](#bkmk_groups)  
  - [ConfigMgr_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [ConfigMgr_DViewAccess](#configmgr_dviewaccess)  
  - [Utenti di Controllo remoto di ConfigMgr](#configmgr-remote-control-users)  
  - [SMS Admins](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_&lt;codicesito\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;codicesito\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;codicesito\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_&lt;codicesito\>](#bkmk_filerepl)  

- [Account usati da Configuration Manager](#bkmk_accounts)
  - [Account di individuazione gruppo Active Directory](#active-directory-group-discovery-account)  
  - [Account individuazione sistema Active Directory](#active-directory-system-discovery-account)  
  - [Account individuazione utente Active Directory](#active-directory-user-discovery-account)  
  - [Account foresta Active Directory](#active-directory-forest-account)  
  - [Account del punto di registrazione certificati](#certificate-registration-point-account)  
  - [Account di acquisizione immagine del sistema operativo](#capture-os-image-account)  
  - [Account di installazione push client](#client-push-installation-account)  
  - [Account di connessione al punto di registrazione](#enrollment-point-connection-account)  
  - [Account di connessione a Exchange Server](#exchange-server-connection-account)  
  - [Account di connessione al punto di gestione](#management-point-connection-account)  
  - [Account di connessione multicast](#multicast-connection-account)  
  - [Account di accesso alla rete](#network-access-account)  
  - [Account di accesso ai pacchetti](#package-access-account)  
  - [Account punto di Reporting Services](#reporting-services-point-account)  
  - [Account visualizzatori autorizzati di strumenti remoti](#remote-tools-permitted-viewer-accounts)  
  - [Account di installazione sito](#site-installation-account)
  - [Account di installazione sistema del sito](#site-system-installation-account)  
  - [Account del server proxy del sistema sito](#site-system-proxy-server-account)  
  - [Account di connessione al server SMTP](#smtp-server-connection-account)  
  - [Account di connessione al punto di aggiornamento software](#software-update-point-connection-account)  
  - [Account del sito di origine](#source-site-account)  
  - [Account del database del sito di origine](#source-site-database-account)  
  - [Account di aggiunta dominio della sequenza di attività](#task-sequence-domain-join-account)  
  - [Account di connessione cartella di rete della sequenza di attività](#task-sequence-network-folder-connection-account)  
  - [Sequenza di attività eseguita come account](#task-sequence-run-as-account)  

- [Oggetti utente usati da Configuration Manager in SQL](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Ruoli del database usati da Configuration Manager in SQL](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Gruppi Windows creati e usati da Configuration Manager  

Configuration Manager crea automaticamente e, in molti casi, gestisce automaticamente i gruppi di Windows seguenti:  

> [!NOTE]  
> Quando Configuration Manager crea un gruppo in un computer appartenente a un dominio, il gruppo è un gruppo di sicurezza locale. Se il computer è un controller di dominio, il gruppo è un gruppo locale di dominio. Questo tipo di gruppo è comune a tutti i controller di dominio del dominio.  


### <a name="configmgr_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> ConfigMgr_CollectedFilesAccess

Configuration Manager usa questo gruppo per concedere l'accesso per la visualizzazione dei file raccolti dall'inventario software.  

Per altre informazioni, vedere [Introduzione all'inventario software](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato nel server del sito primario.

Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente. Eliminarlo manualmente dopo la disinstallazione del sito.

#### <a name="membership"></a>Appartenenze
Configuration Manager gestisce automaticamente l'appartenenza a gruppi. L'appartenenza comprende gli utenti amministratori a cui è concessa l'autorizzazione **Visualizza file raccolti** per l'oggetto a protezione diretta **Raccolta** da un ruolo di sicurezza assegnato.

#### <a name="permissions"></a>Autorizzazioni
Per impostazione predefinita, questo gruppo dispone dell'autorizzazione di **Lettura** per la seguente cartella nel server del sito: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configmgr_dviewaccess"></a><a name="configmgr_dviewaccess"></a>ConfigMgr_DViewAccess  

Questo gruppo è un gruppo di sicurezza locale creato da Configuration Manager nel server di database del sito o nel server di replica del database di un sito primario figlio. Il sito lo crea quando si usano le viste distribuite per la replica di database tra siti all'interno di una gerarchia. Contiene il server del sito e gli account computer di SQL Server del sito di amministrazione centrale.

Per altre informazioni, vedere [Trasferimenti di dati tra siti](data-transfers-between-sites.md).


### <a name="configmgr-remote-control-users"></a>Utenti di Controllo remoto di ConfigMgr  

Gli strumenti remoti di Configuration Manager usano questo gruppo per l'archiviazione di account e gruppi configurati nell'elenco **Visualizzatori autorizzati**. Il sito assegna questo elenco a ogni client.  

Per altre informazioni, vedere [Introduzione al controllo remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato nel client di Configuration Manager quando il client riceve un criterio che abilita gli strumenti remoti.

Questo gruppo non viene rimosso automaticamente dopo che gli strumenti remoti per un client sono stati disabilitati. Eliminarlo manualmente dopo la disabilitazione degli strumenti remoti.

#### <a name="membership"></a>Appartenenze
Per impostazione predefinita, non esistono membri per questo gruppo. Gli utenti aggiunti all'elenco **Visualizzatori autorizzati** vengono aggiunti automaticamente a questo gruppo.

Usare l'elenco **Visualizzatori autorizzati** per gestire l'appartenenza di questo gruppo anziché aggiungervi direttamente utenti o gruppi.

Oltre a essere un visualizzatore autorizzato, un utente amministratore deve avere l'autorizzazione **Controllo remoto** per l'oggetto **Raccolta**. Assegnare questa autorizzazione tramite il ruolo di sicurezza **Operatore strumenti remoti**.  

#### <a name="permissions"></a>Autorizzazioni
Per impostazione predefinita, questo gruppo non ha le autorizzazioni per accedere ad alcun percorso nel computer. Viene usato esclusivamente per contenere l'elenco **Visualizzatori autorizzati**.  


### <a name="sms-admins"></a>SMS Admins  

Questo gruppo viene usato da Configuration Manager per concedere l'accesso al provider SMS tramite WMI. L'accesso al provider SMS è necessario per visualizzare e modificare gli oggetti nella console di Configuration Manager.  

> [!NOTE]  
> La configurazione dell'amministrazione basata su ruoli di un utente amministratore determina gli oggetti che è possibile visualizzare e gestire usando la console di Configuration Manager.  

Per altre informazioni, vedere [Piano per il provider SMS](plan-for-the-sms-provider.md).

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato in ogni computer che ha un provider SMS. 

Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente. Eliminarlo manualmente dopo la disinstallazione del sito.

#### <a name="membership"></a>Appartenenze
Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, ogni utente amministratore di una gerarchia e l'account computer del server del sito appartengono al gruppo **SMS Admins** in ciascun computer del provider SMS di un sito.

#### <a name="permissions"></a>Autorizzazioni
È possibile visualizzare i diritti e le autorizzazioni del gruppo SMS Admins usando lo snap-in MMC del **Controllo WMI**. Per impostazione predefinita, al gruppo vengono concesse le autorizzazioni **Abilita account** e **Abilita remoto** nello spazio dei nomi WMI `Root\SMS`. Agli utenti autenticati, invece, vengono concesse le autorizzazioni **Esegui metodi**, **Scrittura provider** e **Abilita account**.

Quando si usa una console di Configuration Manager remota, configurare le autorizzazioni DCOM di **attivazione remota** sul computer del server di sito e nel provider SMS. Concedere questi diritti al gruppo **SMS Admins**. Questa operazione semplifica l'amministrazione perché evita di dover concedere questi diritti direttamente a utenti o gruppi. Per altre informazioni, vedere [Configurare le autorizzazioni DCOM per le console remote di Configuration Manager](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;codicesito\>  
 
I punti di gestione remoti rispetto al server del sito usano questo gruppo per connettersi database del sito. Questo gruppo consente l'accesso del punto di gestione alle cartelle della posta in arrivo nel server del sito e nel database del sito.  

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato in ogni computer che ha un provider SMS.

Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente. Eliminarlo manualmente dopo la disinstallazione del sito.

#### <a name="membership"></a>Appartenenze
Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, l'appartenenza include gli account computer dei computer remoti che dispongono di un punto di gestione per il sito.

#### <a name="permissions"></a>Autorizzazioni
Per impostazione predefinita, questo gruppo include le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella** per la seguente cartella del server del sito `C:\Program Files\Microsoft Configuration Manager\inboxes`. Questo gruppo ha anche l'autorizzazione **Scrittura** per varie sottocartelle in **posta in arrivo**, in cui il punto di gestione scrive i dati client.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;codicesito\>  
 
I computer del provider SMS remoti usano questo gruppo per connettersi al server del sito.  

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato nel server del sito.

Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente. Eliminarlo manualmente dopo la disinstallazione del sito.

#### <a name="membership"></a>Appartenenze
Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, l'appartenenza comprende l'account computer o un account utente di dominio. usato per la connessione al server del sito da ciascun provider SMS remoto.

#### <a name="permissions"></a>Autorizzazioni
Per impostazione predefinita, questo gruppo include le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella** per la seguente cartella del server del sito `C:\Program Files\Microsoft Configuration Manager\inboxes`. Questo gruppo dispone inoltre delle autorizzazioni di **Scrittura** e **Modifica** per le sottocartelle della posta in arrivo. Il provider SMS richiede l'accesso a tali cartelle.

Questo gruppo dispone inoltre delle autorizzazioni di **Lettura** per le sottocartelle nel server del sito sotto `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

Include anche le autorizzazioni seguenti per le sottocartelle sotto `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Lettura**  
- **Lettura ed esecuzione**  
- **Elenca contenuti cartella**  
- **Scrittura**  
- **Modifica**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;codicesito\>  

Il componente Gestione invio file nei computer di sistema del sito remoto di Configuration Manager usa questo gruppo per la connessione al server del sito.  

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato nel server del sito.

Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente. Eliminarlo manualmente dopo la disinstallazione del sito.

#### <a name="membership"></a>Appartenenze
Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, l'appartenenza comprende l'account computer o l'account utente di dominio. Usa questo account per connettersi al server del sito da ogni sistema del sito remoto che esegue Gestione invio file.

#### <a name="permissions"></a>Autorizzazioni
Per impostazione predefinita, questo gruppo include le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella** per la seguente cartella e le relative sottocartelle del server del sito `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

Questo gruppo dispone inoltre delle autorizzazioni di **Scrittura** e **Modifica** per la seguente cartella nel server del sito `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;codicesito\>  
Configuration Manager usa questo gruppo per abilitare la replica basata su file tra siti di una gerarchia. Per ciascun sito remoto che esegue il trasferimento diretto di file in questo sito, questo gruppo contiene account configurati come **account di replica file**.  

#### <a name="type-and-location"></a>Tipo e percorso
Questo è un gruppo di sicurezza locale creato nel server del sito.

#### <a name="membership"></a>Appartenenze
Quando si installa un nuovo sito come sito figlio di un altro sito, Configuration Manager aggiunge automaticamente l'account computer del nuovo server del sito al gruppo nel server del sito padre. Configuration Manager aggiunge anche l'account computer del sito padre al gruppo nel nuovo server del sito. Se viene specificato un altro account per i trasferimenti basati su file, aggiungere l'account al gruppo nel server del sito di destinazione.

Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente. Eliminarlo manualmente dopo la disinstallazione del sito.

#### <a name="permissions"></a>Autorizzazioni
Per impostazione predefinita, il gruppo dispone del **controllo completo** per la cartella `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Account usati da Configuration Manager  

È possibile configurare gli account seguenti per Configuration Manager.  


### <a name="active-directory-group-discovery-account"></a>Account di individuazione gruppo Active Directory  

Il sito usa l'**account individuazione gruppo Active Directory** per individuare gli oggetti seguenti nei percorsi di Servizi di dominio Active Directory specificati dall'utente:
- Gruppi di sicurezza locali, globali e universali
- L'appartenenza all'interno di questi gruppi
- L'appartenenza all'interno dei gruppi di distribuzione
  - I gruppi di distribuzione non vengono rilevati come risorse di gruppo

Questo account può essere un account computer del server del sito che esegue l'individuazione o un account utente Windows. L'account deve disporre dell'autorizzazione di accesso in **Lettura** ai percorsi di Active Directory specificati per l'individuazione.  

Per altre informazioni, vedere [Individuazione gruppo Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Account individuazione sistema Active Directory  

Il sito usa l'**account individuazione sistema Active Directory** per individuare computer nei percorsi di Servizi di dominio Active Directory specificati dall'utente.  

Questo account può essere un account computer del server del sito che esegue l'individuazione o un account utente Windows. L'account deve disporre dell'autorizzazione di accesso in **Lettura** ai percorsi di Active Directory specificati per l'individuazione.  

Per altre informazioni, vedere [Individuazione sistema Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Account individuazione utente Active Directory  
 
Il sito usa l'**account individuazione utente Active Directory** per individuare gli account utente nei percorsi di Servizi di dominio Active Directory specificati dall'utente.  

Questo account può essere un account computer del server del sito che esegue l'individuazione o un account utente Windows. L'account deve disporre dell'autorizzazione di accesso in **Lettura** ai percorsi di Active Directory specificati per l'individuazione.  

Per altre informazioni, vedere [Individuazione utente Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Account foresta Active Directory  

Il sito usa l'**account foresta Active Directory** per individuare l'infrastruttura di rete delle foreste Active Directory. Viene anche usato dai siti di amministrazione centrale e dai siti primari per pubblicare i dati del sito in Active Directory Domain Services per una foresta.  

> [!NOTE]  
> I siti secondari usano sempre l'account computer del server del sito secondario per la pubblicazione in Active Directory.  

Per l'individuazione e la pubblicazione in foreste non trusted, l'account foresta Active Directory deve essere un account globale. Se non si usa l'account computer del server del sito, è possibile selezionare solo un account globale.  

L'account deve disporre delle autorizzazioni di **Lettura** per ogni foresta Active Directory in cui di desidera individuare l'infrastruttura di rete.  

L'account deve disporre delle autorizzazioni di **Controllo completo** per il contenitore di **System Management** e per i relativi oggetti figlio in tutte le foreste Active Directory in cui si desidera pubblicare i dati del sito. Per altre informazioni, vedere [Preparare Active Directory per la pubblicazione di siti](../network/extend-the-active-directory-schema.md).  

Per altre informazioni, vedere [Individuazione foresta Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Account del punto di registrazione certificati  

Il punto di registrazione certificati usa l'**account del punto di registrazione certificati** per connettersi al database di Configuration Manager. Per impostazione predefinita usa il proprio account computer, ma al suo posto è possibile configurare un account utente. Quando il punto di registrazione certificati si trova in un dominio non attendibile del server del sito, è necessario specificare un account utente. Questo account richiede solo l'accesso in **Lettura** al database del sito perché le operazioni di scrittura vengono gestite dal sistema dei messaggio di stato.  

Per altre informazioni, vedere l'[introduzione alle raccolte](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>Account di acquisizione immagine del sistema operativo  

Quando si acquisisce un'immagine del sistema operativo, Configuration Manager usa l'**account di acquisizione immagine del sistema operativo** per accedere alla cartella in cui sono archiviate le immagini acquisite. Se si aggiunge il passaggio **Acquisisci immagine del sistema operativo** a una sequenza di attività, questo account è obbligatorio.  

L'account deve disporre delle autorizzazioni di **Lettura** e **Scrittura** nella condivisione di rete in cui sono archiviate le immagini acquisite.  

Se si cambia la password dell'account in Windows, aggiornare la sequenza di attività definendo la nuova password. Il client di Configuration Manager riceverà la nuova password durante il successivo download dei criteri client.  

Se è necessario usare questo account, creare un account utente di dominio. Concedere all'account le autorizzazioni minime necessarie per accedere alle risorse di rete richieste e usarlo per tutte le sequenze delle attività di acquisizione.  

> [!IMPORTANT]  
> Non assegnare a questo account autorizzazioni di accesso interattivo.  
>   
> Non usare l'account di accesso alla rete per questo account.  

Per altre informazioni, vedere [Creare una sequenza di attività per acquisire un sistema operativo](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Account di installazione push client  

Quando si distribuiscono i client usando il metodo di installazione push client, il sito usa l'**account di installazione push client** per connettersi ai computer e per installare il software client di Configuration Manager. Se non si specifica questo account, il server del sito prova a usare il suo account computer.  

L'account deve essere membro del gruppo **Administrators** locale nei computer client di destinazione. Questo account non necessita dei diritti di **amministratore di dominio**.  

È possibile specificare più di un account di installazione push client. Configuration Manager proverà in successione ognuno di essi fino a individuare quello giusto.  

> [!TIP]  
> Se si dispone di un ambiente Active Directory di grandi dimensioni ed è necessario modificare questo account, usare il seguente processo per coordinare in modo più efficace questo aggiornamento: 
> 1. Creare un nuovo account con un nome diverso   
> 2. Aggiungere il nuovo account all'elenco degli account di installazione push client in Configuration Manager  
> 3. Attendere un tempo sufficiente per consentire ai servizi di dominio Active Directory di replicare il nuovo account  
> 4. A questo punto, rimuovere il vecchio account da Configuration Manager e dai servizi di dominio Active Directory  

> [!IMPORTANT]  
> Non concedere a questo account il diritto di accesso locale.  

Per altre informazioni, vedere [Installazione push client](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Account di connessione al punto di registrazione  

Il punto di registrazione usa l'**account di connessione al punto di registrazione** per connettersi al database del sito di Configuration Manager. Per impostazione predefinita usa il proprio account computer, ma al suo posto è possibile configurare un account utente. Quando il punto di registrazione si trova in un dominio non attendibile dal server del sito, è necessario specificare un account utente. Questo account richiede l'accesso in **Lettura** e **Scrittura** al database del sito.  

Per altre informazioni, vedere [Installare i ruoli del sistema del sito per la gestione dei dispositivi mobili (MDM) locale](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).


### <a name="exchange-server-connection-account"></a>Account di connessione a Exchange Server  

Il server del sito usa l'**account di connessione a Exchange Server** per connettersi all'Exchange Server specificato. Usa questa connessione per l'individuazione e la gestione dei dispositivi mobili che si connettono a Exchange Server. Questo account richiede i cmdlet di Exchange PowerShell che forniscono le autorizzazioni necessarie per il computer Exchange Server. Per altre informazioni sui cmdlet, vedere [Installare e configurare Exchange Connector](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Account di connessione al punto di gestione  

Il punto di gestione usa l'**account di connessione al punto di gestione** per connettersi al database del sito di Configuration Manager. Usa questa connessione per inviare e recuperare informazioni per i client. Per impostazione predefinita, il punto di gestione usa il proprio account computer, ma al suo posto è possibile configurare un account utente. Quando il punto di gestione si trova in un dominio non attendibile dal server del sito, è necessario specificare un account utente.  

Creare l'account come account locale e con diritti limitati sul computer con Microsoft SQL Server in esecuzione.  

> [!IMPORTANT]  
> Non concedere diritti di accesso interattivo a questo account.  


### <a name="multicast-connection-account"></a>Account di connessione multicast  

I punti di distribuzione configurati per il multicast usano l'**account di connessione multicast** per leggere le informazioni dal database del sito. Per impostazione predefinita il server usa il proprio account computer, ma al suo posto è possibile configurare un account utente. Quando il database del sito si trova in una foresta non trusted, è necessario specificare un account utente. Ad esempio, se il data center dispone di una rete perimetrale in una foresta diversa dal server del sito e dal database del sito, usare questo account per leggere le informazioni multicast dal database del sito.  

Se serve questo account, crearlo come account locale e con diritti limitati sul computer che esegue Microsoft SQL Server.  

> [!IMPORTANT]  
> Non concedere diritti di accesso interattivo a questo account.  

Per altre informazioni, vedere [Usare il multicast per distribuire Windows in rete](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Account di accesso alla rete  

I computer client usano l'**account di accesso alla rete** quando non possono usare il proprio account computer locale per accedere al contenuto nei punti di distribuzione. Ciò è specialmente vero per i client e i computer di gruppi di lavoro di domini non attendibili. Questo account è anche usato durante la distribuzione del sistema operativo quando il computer che installa il sistema operativo non ha ancora un account computer nel dominio.  

> [!Important]  
> L'account di accesso alla rete non viene mai usato come contesto di protezione per eseguire programmi, installare aggiornamenti software o eseguire sequenze di attività. Viene usato solo per l'accesso alle risorse in rete.  

Un client di Configuration Manager tenta, in prima battuta, di usare il proprio account computer per scaricare il contenuto. Poiché non riesce, ritenta automaticamente con l'account di accesso alla rete.  

A partire dalla versione 1806, un gruppo di lavoro o un client associato ad Azure AD può accedere in modo sicuro al contenuto dai punti di distribuzione senza la necessità di un account di accesso alla rete. Questo comportamento comprende gli scenari di distribuzione del sistema operativo con una sequenza di attività eseguita da supporti di avvio, PXE o Software Center. Per altre informazioni, vedere [HTTP migliorato](enhanced-http.md).<!--1358228,1358278-->

> [!Note]  
> Se si abilita **HTTP avanzato** in modo che non richieda l'account di accesso alla rete, il punto di distribuzione deve eseguire Windows Server 2012 o versione successiva. <!--SCCMDocs-pr issue #2696-->
>  
> Aggiornare i client almeno alla versione 1806 prima di abilitare questa funzionalità. Se si consentono solo le connessioni **HTTP avanzato**, non sarà possibile eseguire l'autenticazione con questo metodo nei client meno recenti, che non potranno quindi scaricare il pacchetto di aggiornamento del client da un punto di distribuzione. <!--vso2841213-->   

#### <a name="permissions"></a>Autorizzazioni

Concedere a questo account le autorizzazioni minime appropriate sul contenuto che il client richiede per accedere al software. L'account deve disporre del diritto **Accedi al computer dalla rete** per il punto di distribuzione. È possibile configurare fino a 10 account di accesso alla rete per sito.  

Creare l'account in tutti i domini che forniscono l'accesso necessario alle risorse. L'account di accesso alla rete deve sempre includere un nome di dominio. La protezione pass-through non è supportata per questo account. Se si dispone di punti di distribuzione in più domini, creare l'account in un dominio attendibile.  

> [!TIP]  
> Per evitare blocchi degli account, non modificare la password di un account di accesso alla rete esistente. Creare invece un nuovo account e configurarlo in Configuration Manager. Quando è trascorso tempo sufficiente e tutti i client hanno ricevuto i dettagli del nuovo account, rimuovere il vecchio account dalle cartelle condivise in rete ed eliminare l'account.  

> [!IMPORTANT]  
> Non concedere diritti di accesso interattivo a questo account.  
>   
> Non concedere a questo account il diritto di aggiungere computer al dominio. Se è necessario aggiungere computer al dominio durante una sequenza di attività, usare l'[account di aggiunta dominio della sequenza di attività](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Configurare l'account di accesso alla rete  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Quindi selezionare il sito.  

2.  Nel gruppo **Impostazioni** della barra multifunzione selezionare **Configura componenti del sito** e quindi scegliere **Distribuzione software**.  

3.  Scegliere la scheda **Account di accesso alla rete**. Configurare uno o più account e quindi scegliere **OK**.  


### <a name="package-access-account"></a>Account di accesso al pacchetto  

Un **account di accesso ai pacchetti** consente di impostare le autorizzazioni NTFS per specificare gli utenti e i gruppi di utenti che possono accedere al contenuto del pacchetto nei punti di distribuzione. Per impostazione predefinita, Configuration Manager concede l'accesso solo agli account di accesso generici **Utenti** e **Amministratori**. È possibile controllare l'accesso per i computer client usando gruppi o account di Windows aggiuntivi. I dispositivi mobili recuperano sempre il contenuto dei pacchetti in modo anonimo, quindi non usano un account di accesso ai pacchetti.  

Per impostazione predefinita, quando Configuration Manager copia i file di contenuto in un punto di distribuzione, garantisce l'accesso di **Lettura** al gruppo **Utenti** locale e **Controllo completo** al gruppo **Amministratori** locale. Le autorizzazioni effettivamente necessarie dipendono dal pacchetto. Se si dispone di client in gruppi di lavoro o in foreste non trusted, tali client usano l'account di accesso alla rete per accedere al contenuto del pacchetto. Assicurarsi che l'account di accesso alla rete disponga delle autorizzazioni per il pacchetto usando gli account di accesso ai pacchetti definiti.  

Usare gli account in un dominio che possa accedere ai punti di distribuzione. Se si crea o si modifica l'account dopo la creazione del pacchetto, è necessario ridistribuire il pacchetto. L'aggiornamento del pacchetto non modifica le autorizzazioni NTFS sul pacchetto.  

Non è necessario aggiungere l'account di accesso alla rete come account di accesso ai pacchetti, poiché l'appartenenza al gruppo **Utenti** lo aggiunge automaticamente. La limitazione dell'account di accesso ai pacchetti al solo account di accesso alla rete non impedisce ai client di accedere al pacchetto.  

#### <a name="manage-package-access-accounts"></a>Gestire gli account di accesso ai pacchetti  

1.  Nella console di Configuration Manager scegliere **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** determinare il tipo di contenuto per cui gestire gli account di accesso e seguire i passaggi indicati:  

    - **Applicazione**: espandere **Gestione applicazioni**, scegliere **Applicazioni** e quindi selezionare l'applicazione per cui gestire gli account di accesso.  

    - **Pacchetto**: espandere **Gestione applicazioni**, scegliere **Pacchetti** e quindi selezionare il pacchetto per cui gestire gli account di accesso.  

    - **Pacchetto di distribuzione aggiornamento software**: espandere **Aggiornamenti software**, scegliere **Pacchetti di distribuzione** e quindi selezionare il pacchetto di distribuzione per cui gestire gli account di accesso.  

    - **Pacchetto driver**: espandere **Sistemi operativi**, scegliere **Pacchetti driver** e quindi selezionare il pacchetto driver per cui gestire gli account di accesso.  

    - **Immagine sistema operativo**: espandere **Sistemi operativi**, scegliere **Immagini del sistema operativo**, quindi selezionare l'immagine del sistema operativo per cui gestire gli account di accesso.  

    - **Pacchetto di aggiornamento del sistema operativo**: espandere **Sistemi operativi**, scegliere **Pacchetto di aggiornamento del sistema operativo**, quindi selezionare il pacchetto di aggiornamento del sistema operativo per cui gestire gli account di accesso.  

    - **Immagine d'avvio**: espandere **Sistemi operativi**, scegliere **Immagini d'avvio** e quindi selezionare l'immagine d'avvio per cui gestire gli account di accesso.  

3.  Fare clic con il pulsante destro del mouse sull'oggetto selezionato e quindi scegliere **Gestione account di accesso**.  

4.  Nella finestra di dialogo **Aggiungi account** , specificare il tipo di account al quale sarà garantito l'accesso al contenuto, quindi specificare i diritti di accesso associati all'account.  

    > [!NOTE]  
    > Quando si aggiunge un nome utente per l'account e Configuration Manager trova sia un account utente locale sia un account utente di dominio con tale nome, Configuration Manager imposta i diritti di accesso per l'account utente di dominio.  


### <a name="reporting-services-point-account"></a>Account punto di Reporting Services  
 
SQL Server Reporting Services usa l'**account punto di Reporting Services** per recuperare i dati per i report di Configuration Manager dal database del sito. La password e l'account utente Windows specificati vengono crittografati e archiviati nel database di SQL Server Reporting Services.  

> [!NOTE]  
> L'account specificato deve disporre delle autorizzazioni di **Accesso locale** nel computer che ospita il database SQL di Reporting Services.

> [!NOTE]  
> All'account vengono concessi automaticamente tutti i diritti necessari tramite l'aggiunta al ruolo smsschm_users del database SQL nel database ConfigMgr.

Per altre informazioni, vedere [Introduzione ai report](../../servers/manage/introduction-to-reporting.md).


### <a name="remote-tools-permitted-viewer-accounts"></a>Account visualizzatori autorizzati di strumenti remoti  

Gli account specificati come **Visualizzatori autorizzati** per il controllo remoto sono un elenco di utenti a cui è consentito usare le funzionalità di strumenti remoti nei client.  

Per altre informazioni, vedere [Introduzione al controllo remoto](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Account di installazione sito
<!--SCCMDocs issue #572-->
Usare un account utente di dominio per accedere al server in cui eseguire il programma di installazione di Configuration Manager e installare un nuovo sito.

L'account richiede le autorizzazioni seguenti:  

- **Amministratore** nei server seguenti:
    - Server del sito  
    - Ogni server che ospita il database del sito  
    - Ogni istanza del provider SMS per il sito  

- **Amministratore di sistema** nell'istanza di SQL Server che ospita il database del sito  

Installazione di Configuration Manager aggiunge automaticamente questo account al gruppo [SMS Admins](#sms-admins).

Dopo l'installazione, questo account è l'unico utente con diritti per la console di Configuration Manager. Se è necessario rimuovere questo account, assicurarsi di aggiungere prima i relativi diritti a un altro utente.

Quando si espande un sito autonomo per includere un sito di amministrazione centrale, questo account richiede diritti di amministrazione basata su ruoli **amministratore completo** oppure **amministratore infrastruttura** nel sito primario autonomo.


### <a name="site-system-installation-account"></a>Account di installazione del sistema del sito  

Il server del sito usa l'**account di installazione del sistema del sito** per installare, reinstallare, disinstallare e configurare i sistemi del sito. Se si configura il sistema del sito in modo che il server del sito avvii le connessioni a questo sistema del sito, Configuration Manager usa anche questo account per eseguire il pull dei dati dal sistema del sito dopo l'installazione del sistema del sito e di tutti i ruoli. Ogni sistema del sito può avere un account di installazione sito diverso, ma è possibile configurare un unico account di questo tipo per gestire tutti i ruoli in quel sistema del sito.  

Questo account richiede le autorizzazioni amministrative locali nei sistemi del sito di destinazione. Inoltre, questo account deve disporre del diritto **Accedi al computer dalla rete** nei criteri di sicurezza dei sistemi del sito di destinazione.  

> [!TIP]  
> Se sono presenti numerosi controller di dominio e questi account vengono usati nei domini, prima di configurare il sistema del sito, verificare Active Directory abbia replicato gli account.  
>   
> Quando si specifica un account locale in ogni sistema del sito da gestire, questa configurazione è più sicura dell'utilizzo di account di dominio. Limita i danni che possono provocare gli utenti malintenzionati se l'account è compromesso. Gli account di dominio sono comunque più semplici da gestire. Valutare i vantaggi e gli svantaggi in termini di sicurezza ed efficienza per l'amministrazione.  


### <a name="site-system-proxy-server-account"></a>Account del server proxy del sistema del sito
<!--SCCMDocs issue #648-->
I ruoli del sistema del sito seguenti usano l'**account del server proxy del sistema sito** per accedere a Internet con un server proxy o un firewall che richiede l'accesso autenticato:

- Punto di sincronizzazione di Asset Intelligence
- Connettore Exchange Server
- punto di connessione del servizio
- Punto di aggiornamento software

> [!IMPORTANT]  
> Specificare un account che disponga delle autorizzazioni minime per il server proxy o il firewall richiesti.  

Per altre informazioni, vedere [Supporto dei server proxy](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>Account di connessione al server SMTP  

Il server del sito usa l'**account di connessione al server SMTP** per inviare avvisi tramite posta elettronica quando il server SMTP richiede l'accesso autenticato.  

> [!IMPORTANT]  
> Specificare un account che disponga delle autorizzazioni minime per l'invio di e-mail.  

Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Account di connessione al punto di aggiornamento software  

Il server del sito usa l'**account di connessione al punto di aggiornamento software** per i due servizi di aggiornamento software seguenti:  

- Windows Server Update Services (WSUS), che configura impostazioni quali classificazioni, definizioni di prodotti e impostazioni upstream.  

- Gestione sincronizzazione WSUS, che richiede la sincronizzazione a un server WSUS upstream o a Microsoft Update.  

L'[account di installazione del sistema del sito](#site-system-installation-account) può installare i componenti per gli aggiornamenti software, ma non può eseguire funzioni specifiche di aggiornamenti software nel punto di aggiornamento software. Se non è possibile usare l'account del computer del server di sito per questa funzionalità perché il punto di aggiornamento software si trova in una foresta non trusted, è necessario specificare questo account oltre all'account di installazione sistema del sito.  

Questo account deve essere un amministratore locale sul computer in cui si installa WSUS. Deve anche essere membro del gruppo **WSUS Administrators** locale.  

Per altre informazioni, vedere [Pianificare gli aggiornamenti software](../../../sum/plan-design/plan-for-software-updates.md).


### <a name="source-site-account"></a>Account del sito di origine  

Il processo di migrazione usa l'**account del sito di origine** per accedere al provider SMS del sito di origine. Questo account richiede autorizzazioni di **Lettura** per gli oggetti del sito presenti nel sito di origine per raccogliere dati per i processi di migrazione.  

Se si dispone di punti di distribuzione di Configuration Manager 2007 oppure di siti secondari con i punti di distribuzione con percorso condiviso, quando si esegue l'aggiornamento di tali punti a punti di distribuzione di Configuration Manager (ramo corrente), questo account deve disporre anche delle autorizzazioni **Elimina** per la classe **Sito**. Queste autorizzazioni servono per rimuovere il punto di distribuzione dal sito di Configuration Manager 2007 durante l'aggiornamento.  

> [!NOTE]  
> L'account del sito di origine e l'[account del database del sito di origine](#source-site-database-account) vengono identificati come **Gestione migrazione** nel nodo **Account** dell'area di lavoro **Amministrazione** nella console di Configuration Manager.  

Per altre informazioni, vedere [Eseguire la migrazione dei dati da una gerarchia all'altra](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Account del database del sito di origine  

Il processo di migrazione usa l'**account del database del sito di origine** per accedere al database di SQL Server per il sito di origine. Per raccogliere dati dal database di SQL Server del sito di origine, l'account del database del sito di origine deve avere le autorizzazioni **Lettura** ed **Esegui** per il database di SQL Server del sito di origine.  

Se si usa un account computer di Configuration Manager (ramo corrente), verificare che tutte le opzioni seguenti siano vere per tale account:  
  
- È un membro del gruppo di sicurezza **Distributed COM Users** nel dominio in cui risiede il sito di Configuration Manager 2007  
- È un membro del gruppo di sicurezza **SMS Admins**  
- Ha l'autorizzazione **Lettura** per tutti gli oggetti di Configuration Manager 2007  

> [!NOTE]  
> L'account del sito di origine e l'[account del database del sito di origine](#source-site-database-account) vengono identificati come **Gestione migrazione** nel nodo **Account** dell'area di lavoro **Amministrazione** nella console di Configuration Manager.  

Per altre informazioni, vedere [Eseguire la migrazione dei dati da una gerarchia all'altra](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Account di aggiunta dominio della sequenza di attività 

Il programma di installazione di Windows utilizza l'**account di aggiunta dominio della sequenza di attività** per aggiungere un computer con un'immagine nuova a un dominio. Questo account è necessario per il passaggio [Aggiunta a dominio o gruppo di lavoro](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) della sequenza di attività con l'opzione **Aggiunta a un dominio**. Questo account può anche essere configurato con il passaggio [Applica impostazioni di rete](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings), ma non è obbligatorio.  

Questo account richiede il diritto **Aggiungi a dominio** nel dominio di destinazione.  

> [!TIP]  
> Creare un account utente di dominio con le autorizzazioni minime per aggiungerlo al dominio e usarlo per tutte le sequenze di attività.  

> [!IMPORTANT]  
> Non assegnare a questo account autorizzazioni di accesso interattivo.  
>   
> Non usare l'account di accesso alla rete per questo account.  


### <a name="task-sequence-network-folder-connection-account"></a>Account di connessione cartella di rete della sequenza di attività  

Il motore della sequenza di attività usa l'**account di connessione cartella di rete della sequenza di attività** per connettersi a una cartella condivisa in rete. Questo account è necessario per il passaggio [Connetti alla cartella di rete](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) della sequenza di attività.  

Questo account richiede autorizzazioni per accedere alla cartella condivisa specificata. Deve essere un account utente di dominio.  

> [!TIP]  
> Creare un account utente di dominio con le autorizzazioni minime per accedere alle risorse di rete richieste e usarlo per tutte le sequenze di attività.  

> [!IMPORTANT]  
> Non assegnare a questo account autorizzazioni di accesso interattivo.  
>   
> Non usare l'account di accesso alla rete per questo account.  


### <a name="task-sequence-run-as-account"></a>Sequenza di attività eseguita come account  

Il motore della sequenza di attività usa la **sequenza di attività eseguita come account** per eseguire righe di comando o script di PowerShell con credenziali diverse dall'account di sistema locale. Questo account è necessario per i passaggi [Esegui riga di comando](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) ed **Esegui script PowerShell** della sequenza di attività con l'opzione [Esegui questo passaggio come account specificato](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) selezionata.  

Configurare l'account in modo che abbia le autorizzazioni minime necessarie per eseguire la riga di comando specificata nella sequenza di attività. L'account richiede diritti di accesso interattivi. In genere richiede la possibilità di installare il software e accedere alle risorse di rete. Per l'attività Esegui script PowerShell, questo account richiede autorizzazioni di amministratore locale. 

> [!IMPORTANT]  
> Non usare l'account di accesso alla rete per questo account.  
>   
> Non impostare mai l'account come amministratore di dominio.  
>   
> Non configurare mai profili mobili per questo account. Quando viene eseguita la sequenza di attività, verrà scaricato il profilo mobile per l'account. In questo modo il profilo è vulnerabile all'accesso nel computer locale.  
>   
> Limitare l'ambito dell'account. Ad esempio, creare una sequenza di attività diversa per ogni sequenza di attività eseguita come account. In questo modo, qualora un account venga compromesso, risulteranno compromessi solo i computer client a cui tale account può accedere.  
>   
> Se la riga di comando richiede accesso amministrativo al computer, creare un account amministratore locale unicamente per questo account in tutti i computer che eseguono la sequenza di attività. Eliminare l'account quando non è più necessario.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Oggetti utente usati da Configuration Manager in SQL 
<!--SCCMDocs issue #1160-->
Configuration Manager crea automaticamente e mantiene gil oggetti utente seguenti in SQL.  Questi oggetti si trovano all'interno del database di Configuration Manager in SIcurezza/Utenti.  

> [!IMPORTANT]  
>  La modifica o la rimozione di questi oggetti può generare problemi seri in un ambiente di Configuration Manager.  È consigliabile non apportare modifiche a questi oggetti.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Questo oggetto viene usato per eseguire query nel contesto di sola lettura.  Viene usato da diverse stored procedure.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Questo oggetto viene usato per fornire le autorizzazioni per le istruzioni SQL dinamiche.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Questo oggetto viene usato per le esecuzioni di report SQL.  La stored procedure seguente viene usata con questa funzione: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Ruoli del database usati da Configuration Manager in SQL
<!--SCCMDocs issue #1160-->
Configuration Manager crea automaticamente e mantiene gli oggetti ruolo seguenti in SQL. Questi ruoli consentono di accedere a stored procedure, tabelle, viste e funzioni specifiche per eseguire le azioni richieste per ogni ruolo per recuperare o inserire dati da e nel database ConfigMgr. Questi oggetti si trovano all'interno del database di Configuration Manager in Sicurezza/Ruoli/Ruoli del database.

> [!IMPORTANT]  
> La modifica o la rimozione di questi oggetti può generare problemi seri in un ambiente di Configuration Manager.  È consigliabile non apportare modifiche a questi oggetti.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Importazione di contratti multilicenza per Asset Intelligence. ConfigMgr concede questa autorizzazione agli account utente in base all'accesso RBA per poter importare contratti multilicenza da usare con Asset Intelligence.  Questo account può essere aggiunto da un ruolo di amministratore completo o da un ruolo di Gestione asset.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Sincronizzazione aggiornamenti di Asset Intelligence. ConfigMgr concede all'account computer che ospita l'account del punto di sincronizzazione di Asset Intelligence l'accesso per ottenere i dati del proxy di Asset Intelligence e visualizzare i dati di AI in sospeso per l'upload.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Gestione fuori banda. Questo ruolo viene usato dal ruolo AMT di Configuration Manager per recuperare i dati nei dispositivi che supportano Intel AMT.

> [!NOTE]  
> Questo ruolo è deprecato nelle versioni più recenti di ConfigMgr.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Supporto per il punto di registrazione certificati per System Center Endpoint Protection (SCEP). ConfigMgr concede l'autorizzazione all'account computer del sistema del sito che supporta il punto di registrazione certificati per il supporto SCEP per la firma e il rinnovo del certificato.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

Supporto PFX per il punto di registrazione certificati. ConfigMgr concede l'autorizzazione all'account computer del sistema del sito che supporta il punto di registrazione certificati per il supporto PFX per la firma e il rinnovo.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Punto gestione periferiche. ConfigMgr concede questa autorizzazione all'account computer per un punto di gestione con l'opzione "Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione", per fornire supporto per i dispositivi registrati in MDM.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Punto di connessione del servizio. ConfigMgr concede questa autorizzazione all'account computer che ospita il punto di connessione del servizio per recuperare e fornire dati di telemetria, gestire i servizi cloud e recuperare gli aggiornamenti del servizio.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Viste distribuite. Configuration Manager concede questa autorizzazione all'account computer dei server del sito primario in CAS quando l'opzione delle viste distribuite di SQL Server viene selezionata nelle proprietà del collegamento di replica.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Data warehouse. ConfigMgr concede questa autorizzazione all'account computer che ospita il ruolo Data warehouse.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Punto di registrazione. ConfigMgr concede questa autorizzazione all'account computer che ospita il punto di registrazione per consentire la registrazione del dispositivo tramite MDM.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Consente di accedere a tutte le viste dello schema estese.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Servizio di gestione della gerarchia. ConfigMgr concede queste autorizzazioni all'account per gestire i messaggi sullo stato di failover e le transazioni di SQL Server Broker tra i siti all'interno di una gerarchia.

> [!NOTE]  
> Per impostazione predefinita, il ruolo smdbrole_WebPortal è un membro di questo ruolo.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Servizio multicast. ConfigMgr concede questa autorizzazione all'account computer del punto di distribuzione che supporta il multicast.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Punto di gestione. ConfigMgr concede questa autorizzazione all'account computer che ospita il ruolo del punto di gestione per fornire supporto per i client ConfigMgr.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Punto di gestione per Microsoft BitLocker Administration And Monitoring. ConfigMgr concede questa autorizzazione all'account computer che ospita il punto di gestione che gestisce MBAM per un ambiente.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Richiesta di applicazioni del punto di gestione. ConfigMgr concede questa autorizzazione all'account computer che ospita il punto di gestione per supportare le richieste di applicazioni in base all'utente.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

Provider SMS. Configuration Manager concede questa autorizzazione all'account computer che ospita un ruolo del provider SMS.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Server del sito. ConfigMgr concede questa autorizzazione all'account computer che ospita il sito primario o CAS.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Punto di aggiornamento software. ConfigMgr concede questa autorizzazione all'account computer che ospita il punto di aggiornamento software per l'uso di aggiornamenti di terze parti.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Punto per siti Web del Catalogo applicazioni. ConfigMgr concede questa autorizzazione all'account computer che ospita il punto per siti Web del Catalogo applicazioni per fornire la distribuzione di applicazioni in base all'utente.

### <a name="smsschm_users"></a>smsschm_users

Accesso per la creazione di report utente. ConfigMgr concede l'accesso all'account usato per l'account del punto di Reporting Services per consentire l'accesso alle viste di reporting SMS per visualizzare i dati di reporting di Configuration Manager.  I dati sono ulteriormente limitati con l'uso di RBA.
