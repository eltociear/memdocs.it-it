---
title: Come registrare in blocco i dispositivi
titleSuffix: Configuration Manager
description: Registrare in blocco i dispositivi in modo automatico con la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 474d59ec22d1edaf8e662298e90555e6772d302b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698797"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Come registrare in blocco i dispositivi con MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La registrazione in blocco in Configuration Manager gestione di dispositivi mobili (MDM) locale è un metodo automatico per registrare i dispositivi. L'altro metodo è la registrazione utente, che richiede agli utenti di immettere le credenziali per registrare il dispositivo. La registrazione in blocco usa un pacchetto di registrazione per autenticare il dispositivo durante la registrazione. Il pacchetto è un file con estensione ppkg, che può contenere anche profili certificato e Wi-Fi per supportare la registrazione.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Creare un profilo del certificato

Includere un profilo certificato per installare automaticamente un certificato radice attendibile nel dispositivo. Questo certificato radice è necessario per la comunicazione attendibile tra i dispositivi e i ruoli del sistema del sito necessari per MDM locale.

Quando si prepara il sito per MDM locale, viene esportato il certificato radice attendibile. Usare questo certificato nel profilo del certificato del pacchetto di registrazione. Per ulteriori informazioni su come ottenere il certificato radice attendibile, vedere [esportare il certificato radice attendibile](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Usare il certificato esportato per creare un profilo certificato. Per ulteriori informazioni, vedere [How to Create Certificate Profiles](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Creare un profilo Wi-Fi

Un altro componente del pacchetto di registrazione in blocco è un profilo Wi-Fi. Questo profilo può verificare che il dispositivo disponga della connettività di rete per supportare la registrazione.

Per ulteriori informazioni su come creare un profilo Wi-Fi in Configuration Manager, vedere [How to create Wi-Fi Profiles](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Limitazioni del profilo Wi-Fi

Quando si crea un profilo Wi-Fi per la registrazione in blocco MDM locale, esaminare le limitazioni seguenti.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Configurazioni di sicurezza Wi-Fi per MDM locale

Current Branch of Configuration Manager supporta solo le configurazioni di sicurezza Wi-Fi seguenti per MDM locale:

- Tipi di sicurezza: **WPA2 Enterprise** o **WPA2 Personal**

- Tipi di crittografia: **AES** o **TKIP**

- Tipi EAP: **Smart Card o altro certificato** o **PEAP**

#### <a name="proxy-server"></a>Server proxy

Sebbene Configuration Manager disponga di un'impostazione per le informazioni sul server proxy nel profilo Wi-Fi, il proxy non viene configurato quando il dispositivo viene registrato. Se è necessario configurare un server proxy nei dispositivi registrati in blocco:

- Distribuire le impostazioni usando gli elementi di configurazione dopo la registrazione dei dispositivi.

- Creare un secondo pacchetto usando la finestra di progettazione di Windows Image and Configuration (ICD), quindi distribuirlo insieme al pacchetto di registrazione in blocco.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Creare un profilo di registrazione

Il profilo di registrazione consente di specificare le impostazioni necessarie per la registrazione del dispositivo. Queste impostazioni includono un [profilo certificato](#bkmk_createCert) e un [profilo Wi-Fi](#CreateWifi).

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** , espandere **tutti i dispositivi di proprietà dell'azienda**, espandere **Windows**e selezionare il nodo **profili di registrazione** .

1. Sulla barra multifunzione selezionare **Crea profilo di registrazione**.

1. Nella pagina **generale** della creazione guidata profilo di registrazione specificare le seguenti informazioni:

    - **Nome**: nome univoco per identificare il profilo

    - **Descrizione**: campo facoltativo per descrivere ulteriormente il profilo

    - **Autorità di gestione**: selezionare solo **in locale**

1. Nella pagina **assegnazione sito** selezionare il codice del **sito di gestione** con un punto di gestione periferiche.

1. Nella pagina **Seleziona punto proxy di registrazione** selezionare **solo Intranet**e quindi selezionare uno o più punti proxy di registrazione. Il dispositivo utilizzerà questi server per avviare il processo di registrazione.

1. Nella pagina **Seleziona certificato radice trusted** selezionare il profilo certificato contenente il certificato radice attendibile.

1. Nella pagina **profili Wi-Fi** selezionare il profilo Wi-Fi che contiene le impostazioni di rete necessarie per la connessione dei dispositivi.

    > [!TIP]
    > Se non si usa un profilo Wi-Fi per il pacchetto di registrazione, ignorare questo passaggio.

1. Completare la procedura guidata.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a> Creare un pacchetto di registrazione

Il pacchetto di registrazione (ppkg) è il file usato per registrare in blocco i dispositivi per MDM locale. Creare questo file con Configuration Manager. Sebbene sia possibile creare tipi simili di pacchetti con Windows ICD, solo i pacchetti creati in Configuration Manager possono essere usati per registrare i dispositivi per MDM locale. Un pacchetto creato con Windows ICD può fornire solo il nome dell'entità utente (UPN) necessario per la registrazione, ma non può avviare il processo di registrazione effettivo.

Il processo per creare il pacchetto di registrazione richiede Windows Assessment and Deployment Kit (ADK) per Windows 10. Nel computer che esegue la console di Configuration Manager installare la versione più recente di Windows ADK. Selezionare la funzionalità **progettazione immagini e configurazione (ICD)** ed eventuali dipendenze. Questa versione non deve corrispondere alla versione usata per la distribuzione del sistema operativo da parte del Configuration Manager sito. Per altre informazioni, vedere [scaricare Windows ADK per Windows 10](/windows-hardware/get-started/adk-install).

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** , espandere **tutti i dispositivi di proprietà dell'azienda**, espandere **Windows**e selezionare il nodo **profili di registrazione** .

1. Selezionare un profilo di registrazione esistente. Sulla barra multifunzione selezionare **Esporta**.

1. Nella finestra Esporta il pacchetto di registrazione specificare le informazioni seguenti:

    - **Periodo di validità (giorni)**: per impostazione predefinita, Configuration Manager imposta la scadenza del pacchetto di registrazione tra due settimane (14 giorni). Non è possibile usare il pacchetto per la registrazione del dispositivo dopo la scadenza del periodo di validità. Immettere un numero intero compreso tra 1 e 30.

    - **File del pacchetto**: specificare il percorso e il nome di un file locale o di rete per il file con estensione ppkg.

    - **Crittografa pacchetto**: abilitare questa opzione per proteggere la password del pacchetto. Dopo aver esportato il pacchetto, Configuration Manager Visualizza la password generata. Copiare e salvare la password in un luogo sicuro. Non è possibile usare il pacchetto di registrazione esportato senza la password.

        > [!IMPORTANT]
        > Configuration Manager non salva la password e non è possibile personalizzarla o modificarla. Una volta chiusa la finestra in cui viene visualizzata la password, non è possibile recuperare la password.

1. Selezionare **Export** (Esporta). Configuration Manager usa Windows ADK per creare il pacchetto di registrazione.

Configuration Manager tiene traccia dei pacchetti di registrazione validi. Nella console espandere il nodo **profilo di registrazione** e selezionare **pacchetti esportati**.

> [!TIP]
> Se si rimuove un pacchetto di registrazione dalla console di Configuration Manager, non è possibile usarlo per registrare i dispositivi. Usare questo metodo per gestire i pacchetti di registrazione che non si desidera vengano usati da altri utenti per la registrazione in blocco.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a> Registrare in blocco un dispositivo

È possibile usare un pacchetto per registrare i dispositivi prima o dopo il processo di configurazione guidata del dispositivo. Il pacchetto di registrazione può anche essere incluso come parte di un pacchetto di provisioning OEM (Original Equipment Manufacturer).

Per usare il pacchetto per la registrazione in blocco, è necessario distribuirlo fisicamente al dispositivo. Sono disponibili diversi metodi a seconda delle esigenze, ad esempio:

- Copia dalla file system

- Connetti a un messaggio di posta elettronica

- Copia attraverso una connessione NFC (Near Field Communication)

- Copia da una scheda di memoria

- Effettuare la scansione di un codice a barre

- Copia da un dispositivo con tethering

- Includi in un pacchetto di provisioning OEM

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Registrare un dispositivo con un pacchetto di registrazione in blocco

1. In un dispositivo aprire il file con estensione ppkg. Eseguire come amministratore, se necessario.

1. Windows chiede se il pacchetto provenga da una fonte attendibile, selezionare **Sì**.

Viene avviato il processo di registrazione.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a> Verificare la registrazione

### <a name="verify-bulk-enrollment-on-the-device"></a>Verificare la registrazione in blocco sul dispositivo

1. Nel dispositivo aprire **Impostazioni**.

1. Selezionare **account**e selezionare **Accedi all'ufficio o all'Istituto di istruzione**. Quando la registrazione ha esito positivo, viene visualizzato un account in **companyapps.**.

1. Selezionare l'account e quindi selezionare **Sincronizza**. Questa azione avvia la gestione con Configuration Manager.

### <a name="verify-enrollment-in-the-console"></a>Verificare la registrazione nella console di

Usare la console di Configuration Manager per verificare che i dispositivi siano registrati correttamente. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare **Dispositivi**. Sfogliare o cercare il dispositivo registrato nell'elenco dei dispositivi.