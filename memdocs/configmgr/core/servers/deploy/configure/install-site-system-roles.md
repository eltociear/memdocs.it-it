---
title: Installare i ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Aggiungere ruoli del sistema del sito a un server del sistema del sito esistente o nuovo nel sito.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 30b57de75e637aa083070832783647b8ad35b4a7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700532"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Installare ruoli del sistema del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Nella console di Configuration Manager sono disponibili due metodi per installare i ruoli del sistema del sito:

- **Aggiungi ruoli del sistema del sito**: aggiungere ruoli del sistema del sito a un server del sistema del sito esistente nel sito.

- **Crea server di sistema sito**: specificare un nuovo server come server del sistema del sito e quindi installare uno o più ruoli. Questo metodo è uguale ad **Aggiungi ruoli del sistema del sito**, ad eccezione della prima pagina. Specificare prima di tutto il nome del server e il sito in cui si vuole installarlo.

> [!TIP]
> Quando si installa un ruolo in un computer remoto, Configuration Manager aggiunge l'account computer del computer remoto a un gruppo locale nel server del sito.
>
> Quando si installa il sito in un controller di dominio, il gruppo nel server del sito è un gruppo di dominio anziché locale. In questo caso, il ruolo del sistema del sito remoto non funziona immediatamente. È necessario riavviare il server del sistema del sito oppure aggiornare il ticket Kerberos per l'account computer del server remoto. Per altre informazioni, vedere [Account usati](../../../plan-design/hierarchy/accounts.md).

Prima di installare il ruolo del sistema del sito, Configuration Manager controlla il computer di destinazione per verificare che soddisfi i prerequisiti per i ruoli selezionati.

Per impostazione predefinita, quando Configuration Manager installa un ruolo del sistema del sito, i file vengono installati nella prima unità disco NTFS disponibile con la maggiore quantità di spazio su disco disponibile. Per evitare l'installazione di Configuration Manager in unità specifiche, prima di installare il server del sistema del sito, creare un file vuoto denominato **no_sms_on_drive.sms** nella radice dell'unità.

Per installare i ruoli, Configuration Manager usa l'**account di installazione del sistema del sito**. L'account viene specificato quando si installa il ruolo. Per impostazione predefinita, questo account è l'account di sistema locale del computer del server del sito. È possibile specificare un account utente di dominio come account di installazione del sistema del sito. Per altre informazioni, vedere [Account -Account di installazione del sistema del sito](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Installare i ruoli in un server del sistema del sito esistente

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**. Selezionare il server del sistema del sito esistente in cui si vogliono installare nuovi ruoli del sistema del sito.

1. Nella scheda **Home** della barra multifunzione nel gruppo **Server** selezionare **Aggiungi ruoli del sistema del sito**.

1. Nella pagina **Generale** esaminare le impostazioni.

    > [!TIP]
    >  Per accedere al ruolo del sistema del sito da Internet, assicurarsi di specificare un nome di dominio completo (FQDN) Internet.

1. Nella pagina **Proxy**, se i ruoli in questo server richiedono un proxy Internet, specificare poi le impostazioni per un server proxy. Per altre informazioni, vedere [Supporto dei server proxy](../../../plan-design/network/proxy-server-support.md).

1. Nella pagina **Selezione ruolo del sistema** selezionare i ruoli del sistema del sito da aggiungere.

1. Completare la procedura guidata. È possibile che vengano visualizzate pagine aggiuntive per ruoli specifici. Per altre informazioni, vedere [Opzioni di configurazione per i ruoli del sistema del sito](configuration-options-for-site-system-roles.md).

> [!TIP]
> Il cmdlet di Windows PowerShell **New-CMSiteSystemServer** esegue la stessa funzione di questa procedura. Per altre informazioni, vedere [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Installare i ruoli in un nuovo server del sistema del sito

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**.

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea server di sistema sito**.

1. Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito.

    > [!TIP]
    > Per accedere al nuovo ruolo del sistema del sito da Internet, assicurarsi di specificare un FQDN Internet.

1. Nella pagina **Proxy**, se i ruoli in questo server richiedono un proxy Internet, specificare poi le impostazioni per un server proxy. Per altre informazioni, vedere [Supporto dei server proxy](../../../plan-design/network/proxy-server-support.md).

1. Nella pagina **Selezione ruolo del sistema** selezionare i ruoli del sistema del sito da aggiungere.

1. Completare la procedura guidata. È possibile che vengano visualizzate pagine aggiuntive per ruoli specifici. Per altre informazioni, vedere [Opzioni di configurazione per i ruoli del sistema del sito](configuration-options-for-site-system-roles.md).

> [!TIP]
> Il cmdlet di Windows PowerShell **New-CMSiteSystemServer** esegue la stessa funzione di questa procedura. Per altre informazioni, vedere [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="next-steps"></a>Passaggi successivi

- [Opzioni di configurazione per i ruoli del sistema del sito](configuration-options-for-site-system-roles.md)

- [Rimuovere il ruolo](../install/uninstall-sites-and-hierarchies.md#bkmk_role)