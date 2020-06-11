---
title: Co-gestire i dispositivi basati su Internet
titleSuffix: Configuration Manager
description: Informazioni su come preparare i dispositivi Windows 10 basati su Internet per la co-gestione.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 66e6156466d0432aaa8b3b162263f8207bdc9d78
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455107"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Come preparare i dispositivi basati su Internet per la co-gestione

Questo articolo è incentrato sul secondo percorso relativo alla co-gestione, per i nuovi dispositivi basati su Internet. Questo scenario si verifica quando nuovi dispositivi Windows 10 vengono aggiunti ad Azure AD e automaticamente registrati in Intune. Per raggiungere uno stato di co-gestione, è necessario installare il client di Configuration Manager.  

## <a name="windows-autopilot"></a>Windows Autopilot

Per i nuovi dispositivi Windows 10 è possibile usare il servizio Autopilot per definire la Configurazione guidata. Questo processo include l'aggiunta del dispositivo ad Azure AD e la registrazione del dispositivo in Intune.  

Per altre informazioni, vedere [Panoramica di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Per configurare i dispositivi per la registrazione automatica in Intune quando vengono aggiunti ad Azure AD, vedere [Configurare la registrazione dei dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Raccogliere informazioni da Configuration Manager

Usare Configuration Manager per raccogliere e segnalare le informazioni sul dispositivo richieste da Intune. Queste informazioni includono il numero di serie del dispositivo, l'identificatore del prodotto Windows e un ID hardware. Vengono usate per registrare il dispositivo in Intune per il supporto di Windows Autopilot.

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere il nodo **Report**, espandere **Report** e selezionare il nodo **Hardware - Generale**.  

2. Eseguire il report **Informazioni sui dispositivi di Windows Autopilot** e visualizzare i risultati.  

3. Nel visualizzatore report selezionare l'icona **Esporta** e scegliere l'opzione **CSV (delimitato da virgole)** .  

4. Dopo aver salvato il file, caricare i dati in Intune.  

Per altre informazioni, vedere [Aggiungere dispositivi in Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Autopilot per dispositivi esistenti
<!--1358333-->

[Windows Autopilot per i dispositivi esistenti](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) è disponibile in Windows 10 versione 1809 o successive. Questa funzionalità consente di ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per la [modalità definita dall'utente di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando una singola sequenza di attività nativa di Configuration Manager.

Per altre informazioni, vedere la [sequenza di attività Windows Autopilot per dispositivi esistenti](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Installare il client di Configuration Manager

Per i dispositivi basati su Internet nel secondo percorso, è necessario creare un'app in Intune. Distribuire quest'app nei dispositivi Windows 10 che non sono ancora client di Configuration Manager.

> [!NOTE]
> Prima di assegnare questa app ai dispositivi Intune, assicurarsi che i dispositivi considerino attendibile il certificato di autenticazione server di Cloud Management Gateway. Per altre informazioni, vedere [Certificato radice trusted del gateway di gestione cloud per i client](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Se un dispositivo non considera attendibile il certificato di autenticazione server di Cloud Management Gateway verrà indicato l'errore WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA nel file ccmsetup.log nel client.

### <a name="get-the-command-line-from-configuration-manager"></a>Recuperare la riga di comando da Configuration Manager

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  

2. Selezionare l'oggetto co-gestione e quindi scegliere **Proprietà** nella barra multifunzione.  

3. Nella scheda **Abilitazione** copiare la riga di comando. Incollarla nel Blocco note e salvarla per il processo successivo.  

La riga di comando seguente è un esempio: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Decidere quali proprietà della riga di comando sono necessarie per l'ambiente:  

- Le seguenti proprietà della riga di comando sono richieste in tutti gli scenari:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- Le seguenti proprietà sono richieste quando si usa Azure AD per l'autenticazione client anziché i certificati di autenticazione client basati su infrastruttura a chiave pubblica:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Se il client effettua il roaming alla rete Intranet, usare la proprietà seguente:
  - SMSMP  

- Se si usa il proprio certificato PKI e l'elenco di revoche di certificati non è pubblicato in Internet, il parametro seguente è obbligatorio:  
  - /noCRLCheck  

    Per altre informazioni, vedere [Pianificazione degli elenchi di revoche di certificati](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- A partire dalla versione 2002, usare la proprietà seguente per avviare una sequenza di attività immediatamente dopo la registrazione del client:
  - PROVISIONTS

    Per altri dettagli, vedere [Informazioni sulle proprietà di installazione client - PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

Il sito pubblica le informazioni aggiuntive di Azure AD in Cloud Management Gateway (CMG). Un client aggiunto ad Azure AD ottiene queste informazioni da CMG durante il processo ccmsetup, usando lo stesso tenant a cui viene aggiunto. Questo comportamento semplifica ulteriormente la registrazione dei dispositivi per la co-gestione in un ambiente con più di un tenant di Azure AD. Le uniche due proprietà di ccmsetup richieste sono **CCMHOSTNAME** e **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Se si distribuisce già il client di Configuration Manager da Intune, aggiornare l'app di Intune con una nuova riga di comando e un nuovo file MSI. <!-- SCCMDocs-pr issue 3084 -->

L'esempio seguente include tutte queste proprietà:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Creare l'app in Intune

1. Passare all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://endpoint.microsoft.com) e quindi espandere il riquadro di spostamento a sinistra.  

2. Selezionare **App** > **Tutte le app** > **Aggiungi**.  

3. In **Altro** selezionare **App line-of-business**.  

4. Caricare il file del pacchetto dell'app **ccmsetup.msi**. Questo file è disponibile nella cartella seguente nel server del sito di Configuration Manager: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Quando si aggiorna il sito, assicurarsi di aggiornare anche l'app in Intune.  

5. Dopo aver aggiornato l'app, configurare le informazioni sull'app con la riga di comando copiata da Configuration Manager.  

> [!IMPORTANT]
> Se si personalizza questa riga di comando, assicurarsi che la lunghezza non superi i 1024 caratteri. Se la lunghezza della riga di comando supera i 1024 caratteri, l'installazione del client non va a buon fine.
