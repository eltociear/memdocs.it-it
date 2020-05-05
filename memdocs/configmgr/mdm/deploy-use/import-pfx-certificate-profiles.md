---
title: Importare profili certificato PFX
titleSuffix: Configuration Manager
description: Informazioni su come usare i file PFX in Configuration Manager per generare certificati specifici dell'utente che supportano lo scambio di dati crittografati.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f72dcba7e7f1e3af0bf168ca83deb958094879a
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724595"
---
# <a name="import-pfx-certificate-profiles"></a>Importare profili certificato PFX

*Si applica a: Configuration Manager (Current Branch)*

Informazioni su come creare un profilo certificato importando le credenziali da certificati esterni. In questo articolo vengono evidenziate informazioni specifiche sui profili certificato PFX (Personal Information Exchange). Per altre informazioni su come creare e configurare questi profili, vedere [profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager supporta diversi tipi di archivi certificati per diversi dispositivi e versioni del sistema operativo. Ad esempio, Windows 10 e Windows 10 Mobile. Per altre informazioni, vedere [prerequisiti per i profili certificato](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Usare Configuration Manager per importare le credenziali del certificato e quindi eseguire il provisioning dei file PFX nei dispositivi. È possibile usare questi file per generare certificati specifici dell'utente per supportare lo scambio di dati crittografati.

> [!TIP]  
> Per una procedura dettagliata di questo processo, vedere il post di Blog su [come creare e distribuire profili certificato pfx in Configuration Manager](https://blogs.technet.microsoft.com/karanrustagi/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager/).  

## <a name="create-a-profile"></a>Creare un profilo

1. Nella console di Configuration Manager passare all'area di lavoro **asset e conformità** , espandere **impostazioni di conformità**, **accesso risorse aziendali**e quindi selezionare **profili certificato**.

1. Nella scheda **Home** della barra multifunzione selezionare **Crea profilo certificato** nel gruppo **Crea**.

1. Nella pagina **generale** della **creazione guidata profilo certificato**specificare le seguenti informazioni:  

    - **Nome**: immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

    - **Descrizione**: fornire una descrizione che fornisce una panoramica del profilo certificato che consente di identificarlo nella console di Configuration Manager. È possibile usare un massimo di 256 caratteri.  

1. Selezionare **scambio di informazioni personali-impostazioni di PKCS #12 (PFX)-importa**. Questa opzione Importa le informazioni da un certificato esistente per creare un profilo certificato.

    > [!NOTE]
    > L'opzione **Crea** richiede un certificato per conto di un utente da un'autorità di certificazione locale connessa (CA). Questo processo distribuisce il certificato ai client come file PFX in modo sicuro. Per altre informazioni, vedere [creare profili certificato PFX usando un'autorità di certificazione](create-pfx-certificate-profiles.md).

1. Nella pagina **certificato PFX** della **creazione guidata profilo certificato**specificare il provider di archiviazione chiavi (KSP) del dispositivo:

    - **Installa in TPM (Trusted Platform Module) se presente**  
    - **Installa in Trusted Platform Module (TPM) in caso di errore**
    - **Installa in Windows Hello for business in caso di errore**
    - **Installa nel provider di archiviazione chiavi software**

1. Nella pagina **piattaforme supportate** scegliere le piattaforme per dispositivi supportate.

1. Completare la procedura guidata.

## <a name="deploy-the-profile"></a>Distribuire il profilo

Dopo aver creato ed eseguito il provisioning di un profilo certificato, è ora disponibile nel nodo **profili certificato** . Per altre informazioni su come distribuirlo, vedere [distribuire i profili di accesso alle risorse](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Assegnare gli utenti primari

Assegnare gli utenti di destinazione come utenti primari nei dispositivi Windows 10 in cui è necessario installare i certificati PFX. Per altre informazioni, vedere [affinità utente dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Eseguire il provisioning di uno script di creazione PFX

Per importare un certificato PFX, usare i cmdlet di PowerShell seguenti Configuration Manager per eseguire il provisioning di uno script di creazione PFX:

- [Get-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Import-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Script di esempio

Per eseguire il provisioning di un file PFX in un profilo certificato per un utente, aprire PowerShell in un computer con la console di Configuration Manager. Modificare le variabili con i valori dell'ambiente.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Vedere anche

[Crea un nuovo profilo certificato](../../protect/deploy-use/create-certificate-profiles.md)

[Creare profili certificato PFX usando un'autorità di certificazione](create-pfx-certificate-profiles.md)

[Distribuire profili certificato, Wi-Fi, VPN e di posta elettronica](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
