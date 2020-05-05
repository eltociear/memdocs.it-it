---
title: Creare profili certificato PFX
titleSuffix: Configuration Manager
description: Informazioni su come usare i file PFX in Configuration Manager per generare certificati specifici dell'utente che supportano lo scambio di dati crittografati.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724575"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Creare profili certificato PFX usando un'autorità di certificazione

*Si applica a: Configuration Manager (Current Branch)*

Informazioni su come creare un profilo certificato che usa un'autorità di certificazione per le credenziali. In questo articolo vengono evidenziate informazioni specifiche sui profili certificato PFX (Personal Information Exchange). Per altre informazioni su come creare e configurare questi profili, vedere [profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager consente di creare un profilo certificato PFX usando le credenziali emesse da un'autorità di certificazione. È possibile scegliere Microsoft o Entrust come autorità di certificazione. Quando vengono distribuiti nei dispositivi utente, i file PFX generano certificati specifici dell'utente per supportare lo scambio di dati crittografati.

Per importare le credenziali del certificato da file di certificato esistenti, vedere [Import PFX certificate](import-pfx-certificate-profiles.md)Profiles.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare a creare un profilo certificato, verificare che i prerequisiti necessari siano pronti. Per ulteriori informazioni, vedere [prerequisiti per i profili certificato](../../protect/plan-design/prerequisites-for-certificate-profiles.md). Per i profili certificato PFX, ad esempio, è necessario un ruolo del sistema del sito del [punto di registrazione certificati](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) .

## <a name="create-a-profile"></a>Creare un profilo  

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** , espandere **impostazioni di conformità**, **accesso risorse aziendali**e quindi selezionare **profili certificato**.

1. Nella scheda **Home** della barra multifunzione selezionare **Crea profilo certificato** nel gruppo **Crea**.

1. Nella pagina **generale** della **creazione guidata profilo certificato**specificare le seguenti informazioni:  

    - **Nome**: immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

    - **Descrizione**: fornire una descrizione che fornisce una panoramica del profilo certificato che consente di identificarlo nella console di Configuration Manager. È possibile usare un massimo di 256 caratteri.  

1. Selezionare **scambio informazioni personali-impostazioni #12 PKCS (PFX)-crea**. Questa opzione richiede un certificato per conto di un utente da un'autorità di certificazione locale connessa (CA). Scegliere l'autorità di certificazione: **Microsoft** o **Entrust Datacard**.

    > [!NOTE]
    > L'opzione di **importazione** ottiene le informazioni da un certificato esistente per creare un profilo certificato. Per altre informazioni, vedere [Importare profili certificato PFX](import-pfx-certificate-profiles.md).

1. Nella pagina **piattaforme supportate** selezionare le versioni del sistema operativo supportate da questo profilo certificato. Per altre informazioni sulle versioni del sistema operativo supportate per la versione di Configuration Manager, vedere [versioni del sistema operativo supportate per client e dispositivi](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. Nella pagina **autorità di certificazione** scegliere il punto di registrazione certificati (CRP) per elaborare i certificati PFX:

    1. **Sito primario**: scegliere il server che contiene il ruolo CRP per la CA.
    1. **Autorità di certificazione**: selezionare la CA pertinente.

    Per altre informazioni, vedere [Infrastruttura di certificazione](../../protect/deploy-use/certificate-infrastructure.md).

Le impostazioni nella pagina **certificato PFX** variano a seconda della CA selezionata nella pagina **generale** :

- [CA Microsoft](#bkmk_microsoft)
- [CA Entrust Datacard](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Configurare le impostazioni del **certificato PFX** per la CA Microsoft

1. Per il **nome del modello di certificato**, scegliere il modello di certificato.

1. Per usare il profilo certificato per la firma S/MIME o la crittografia, abilitare l' **utilizzo del certificato**.

    Quando si abilita questa opzione, vengono consegnati tutti i certificati PFX associati all'utente di destinazione a tutti i dispositivi. Se non si abilita questa opzione, ogni dispositivo riceve un certificato univoco.  

1. Impostare **Formato nome soggetto** su **Nome comune** o su **Nome distinto completo**. Se non si è certi di quale usare, contattare l'amministratore della CA.

1. Per il **nome alternativo del soggetto**, abilitare l' **indirizzo di posta elettronica** e il **nome dell'entità utente (UPN)** in base alla propria autorità di certificazione.

1. **Soglia di rinnovo**: determina quando i certificati vengono rinnovati automaticamente, in base alla percentuale di tempo rimanente prima della scadenza.

1. Impostare **Periodo di validità del certificato** sulla durata del certificato.

1. Quando il punto di registrazione certificati specifica Active Directory credenziali, abilitare **Active Directory la pubblicazione**.

1. Se è stata selezionata una o più piattaforme supportate da Windows 10:

    1. Impostare l' **archivio certificati di Windows** su **utente**. (L'opzione del **computer locale** non distribuisce i certificati, non sceglierla).

    1. Selezionare uno dei provider di **archiviazione chiavi (KSP)** seguenti:

        - **Installa in TPM (Trusted Platform Module) se presente**  
        - **Installa in Trusted Platform Module (TPM) in caso di errore**
        - **Installa in Windows Hello for business in caso di errore**
        - **Installa nel provider di archiviazione chiavi software**

1. Completare la procedura guidata.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Configurare le impostazioni del **certificato PFX** per Entrust Datacard CA

1. Per la **configurazione dell'ID digitale**, scegliere il profilo di configurazione. L'amministratore di Entrust crea le opzioni di configurazione dell'ID digitale.

1. Per usare il profilo certificato per la firma S/MIME o la crittografia, abilitare l' **utilizzo del certificato**.

    Quando si abilita questa opzione, vengono consegnati tutti i certificati PFX associati all'utente di destinazione a tutti i dispositivi. Se non si abilita questa opzione, ogni dispositivo riceve un certificato univoco.  

1. Per eseguire il mapping tra i token del **formato del nome soggetto** di Entrust e i campi Configuration Manager, selezionare **formato**.

    La finestra di dialogo **Certificate Name Formatting** (Formattazione del nome del certificato) elenca le variabili di configurazione dell'ID digitale di Entrust. Per ogni variabile Entrust, scegliere i campi Configuration Manager appropriati.

1. Per mappare i token del **nome alternativo del soggetto** di Entrust alle variabili LDAP supportate, selezionare **formato**.

    La finestra di dialogo **Certificate Name Formatting** (Formattazione del nome del certificato) elenca le variabili di configurazione dell'ID digitale di Entrust. Per ogni variabile Entrust, scegliere la variabile LDAP appropriata.

1. **Soglia di rinnovo**: determina quando i certificati vengono rinnovati automaticamente, in base alla percentuale di tempo rimanente prima della scadenza.

1. Impostare **Periodo di validità del certificato** sulla durata del certificato.

1. Quando il punto di registrazione certificati specifica Active Directory credenziali, abilitare **Active Directory la pubblicazione**.

1. Se è stata selezionata una o più piattaforme supportate da Windows 10:

    1. Impostare l' **archivio certificati di Windows** su **utente**. (L'opzione del **computer locale** non distribuisce i certificati, non sceglierla).

    1. Selezionare uno dei provider di **archiviazione chiavi (KSP)** seguenti:

        - **Installa in TPM (Trusted Platform Module) se presente**  
        - **Installa in Trusted Platform Module (TPM) in caso di errore**
        - **Installa in Windows Hello for business in caso di errore**
        - **Installa nel provider di archiviazione chiavi software**

1. Completare la procedura guidata.

## <a name="deploy-the-profile"></a>Distribuire il profilo

Dopo aver creato un profilo certificato, è ora disponibile nel nodo **profili certificato** . Per altre informazioni su come distribuirlo, vedere [distribuire i profili di accesso alle risorse](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Vedere anche

[Crea un nuovo profilo certificato](../../protect/deploy-use/create-certificate-profiles.md)

[Importare profili certificato PFX](import-pfx-certificate-profiles.md)

[Distribuire profili certificato, Wi-Fi, VPN e di posta elettronica](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
