---
title: Configurare la registrazione per MDM locale
titleSuffix: Configuration Manager
description: Concedere agli utenti le autorizzazioni per registrare i propri dispositivi per la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724685"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>Configurare la registrazione dei dispositivi per MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il passaggio finale per configurare la gestione di dispositivi mobili (MDM) locale è consentire agli utenti di registrare i propri dispositivi. Usare Configuration Manager impostazioni client per concedere agli utenti l'autorizzazione per registrare i dispositivi in MDM locale.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> Creare un profilo di registrazione

Per eseguire il push delle impostazioni necessarie per consentire agli utenti di registrare i dispositivi mobili, aggiungere un nuovo profilo di registrazione alle impostazioni client predefinite. Questo profilo viene quindi applicato a tutti gli utenti nel sito Configuration Manager.

> [!NOTE]
> Questo processo usa le **Impostazioni client predefinite**, che verranno applicate automaticamente a tutti i dispositivi e gli utenti. In alternativa, è possibile creare impostazioni client personalizzate e quindi distribuirle in raccolte di propria scelta. Questo metodo alternativo richiede almeno due impostazioni client personalizzate, una per le impostazioni del *dispositivo* e una per le impostazioni *utente* . Per altre informazioni, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Impostazioni client** . Aprire **Impostazioni client predefinite** e selezionare il gruppo di **registrazioni** .

1. In Impostazioni dispositivo specificare l' **intervallo di polling per i dispositivi moderni (minuti)**. Per impostazione predefinita, questo intervallo è di 60 minuti.

1. In impostazioni utente abilitare l'opzione per **consentire agli utenti di registrare i dispositivi moderni**.

1. Per il **profilo di registrazione del dispositivo moderno**selezionare **Imposta profilo**. Nella finestra profilo di registrazione selezionare **Crea**.

1. Nella finestra Crea profilo di registrazione specificare le informazioni seguenti:

    - **Nome** univoco e descrittivo per il profilo di registrazione.

    - **Descrizione** facoltativa per fornire informazioni aggiuntive sul profilo.

    - Scegliere il **codice del sito di gestione** che contiene il punto di gestione periferiche. Selezionare **OK** per salvare e chiudere.

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>Configurare impostazioni client aggiuntive

Sono disponibili altre impostazioni client per configurare i dispositivi dopo la registrazione. Per informazioni generali, vedere [How to configure client Settings](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager supporta le seguenti impostazioni client per MDM locale:

- **Criteri client**: queste impostazioni specificano la frequenza di download dei criteri client nel dispositivo. È anche possibile abilitare le impostazioni per i criteri utente. Per ulteriori informazioni, vedere [About Client Settings-client Policy](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Distribuzione software**: impostare l'intervallo per la valutazione delle distribuzioni software. Per ulteriori informazioni, vedere [About Client Settings-Software Deployment](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > Per MDM locale, le impostazioni di distribuzione software possono essere usate solo come impostazioni client predefinite.

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>Individua utenti

Per consentire agli utenti di ricevere le impostazioni client con il profilo di registrazione per MDM locale, il sito individua il proprio account utente in Active Directory. Per assicurarsi che il profilo di registrazione venga ottenuto da tutti gli utenti che ne hanno bisogno, eseguire l'individuazione degli utenti di Active Directory. Per ulteriori informazioni, vedere [Active Directory individuazione utente](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>Installare il certificato radice attendibile

I dispositivi aggiunti a un dominio ottengono il certificato radice attendibile per la comunicazione attendibile con i server che ospitano i ruoli del sistema del sito. Active Directory Servizi certificati distribuisce automaticamente il certificato radice attendibile. Per i computer e i dispositivi mobili non appartenenti a un dominio è necessario che questo certificato sia installato con altri mezzi per consentire la registrazione.

> [!NOTE]
> Se i certificati del server Web vengono rilasciati da un'autorità di certificazione pubblica, la maggior parte dei dispositivi sono già considerati attendibili. Se la progettazione include l'uso di una di queste CA pubbliche, non è necessario eseguire questo passaggio.

Dopo aver [esportato il certificato radice attendibile](set-up-certificates-on-premises-mdm.md#bkmk_exportCert), è necessario installarlo nei dispositivi che dovranno registrarsi. Ad esempio, i dispositivi che non sono stati aggiunti al dominio e non possono ottenerli automaticamente da Active Directory. Il processo che si utilizza dipende dai fattori seguenti:

- Tipi di dispositivi specifici e funzionalità tecniche
- Versione sistema operativo
- Requisiti aziendali, di sicurezza e dell'esperienza utente

L'elenco seguente include alcuni metodi di esempio per la distribuzione e l'installazione del certificato radice attendibile nei dispositivi:

- Condivisione file

- Allegato di posta elettronica

- Scheda di memoria

- Dispositivo con tethering

- Archiviazione cloud (ad esempio OneDrive)

- Connessione NFC (Near Field Communication)

- Scanner di codice a barre

- Pacchetto di provisioning della Configurazione guidata

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>Installare manualmente il certificato radice attendibile in Windows

1. Nel dispositivo da registrare, passare a Esplora file al file del certificato radice attendibile (con estensione CER) e **aprirlo** .

1. Nella finestra certificato selezionare **Installa certificato**.

1. Nell'importazione guidata certificati selezionare **computer locale**e quindi fare clic su **Avanti** per continuare come amministratore.

1. Nella pagina archivio certificati selezionare **colloca tutti i certificati nel seguente archivio**e quindi selezionare **Sfoglia**.

1. Nella finestra Seleziona archivio certificati selezionare autorità di **certificazione radice attendibili**e quindi fare clic su **OK**.

1. Completamento e procedura guidata.

## <a name="next-step"></a>Passaggio successivo

> [!div class="nextstepaction"]
> [Registra i dispositivi](../deploy-use/enroll-devices-on-premises-mdm.md)
