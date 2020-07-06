---
title: Creare profili certificato in Microsoft Intune - Azure | Microsoft Docs
description: Informazioni sull'uso di certificati e profili di certificato SCEP (Simple Certificate Enrollment Protocol) e PKCS (Public Key Cryptography Standards) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5de1268b8b04c98ac7a9cfa96d42349fc0f8890
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383207"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Usare i certificati per l'autenticazione in Microsoft Intune

Usare i certificati con Intune per autenticare gli utenti in applicazioni e risorse aziendali tramite profili VPN, Wi-Fi o di posta elettronica. Quando si usano i certificati per autenticare queste connessioni, gli utenti finali non dovranno immettere nomi utente e password e l'accesso risulta così semplificato. I certificati vengono usati anche per la firma e la crittografia della posta elettronica tramite S/MIME.

## <a name="intune-supported-certificates-and-usage"></a>Certificati supportati da Intune e utilizzo

| Tipo              | Autenticazione | Firma S/MIME | Crittografia S/MIME  |
|--|--|--|--|
| Certificato importato PKCS (Public Key Cryptography Standards) |  | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png)|
| PKCS#12 (o PFX)    | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) |  |
| Simple Certificate Enrollment Protocol (SCEP)  | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | |

Per distribuire questi certificati, verranno creati e assegnati profili di certificato ai dispositivi.

Ogni singolo profilo di certificato creato supporta un'unica piattaforma. Se, ad esempio, si usano certificati PKCS, si creerà un profilo di certificato PKCS per Android e un profilo di certificato PKCS separato per iOS/iPadOS. Se per queste due piattaforme si usano anche certificati SCEP, si creerà un profilo di certificato SCEP per Android e un altro per iOS/iPadOS.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Considerazioni generali se si usa un'autorità di certificazione Microsoft

Quando si usa un'autorità di certificazione (CA) Microsoft:

- Per usare i profili certificato SCEP, è necessario [configurare un server del servizio Registrazione dispositivi di rete (NDES)](certificates-scep-configure.md#set-up-ndes) per l'uso con Intune.
- Per usare i seguenti tipi di profilo certificato, è necessario [installare il connettore di certificati di Microsoft Intune](certificates-scep-configure.md#install-the-intune-certificate-connector):
  - Profilo di certificazione SCEP
  - Profilo di certificato PKCS

- Per usare i certificati PKCS importati:
  - [Installare il connettore di certificati PFX per Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Esportare i certificati dall'autorità di certificazione e quindi importarli in Microsoft Intune. Vedere [il progetto PowerShell PFXImport](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Distribuire i certificati usando i meccanismi seguenti:
  - [Profili certificato attendibili](certificates-configure.md#create-trusted-certificate-profiles) per distribuire il certificato CA radice attendibile dalla CA radice o intermedia (emittente) ai dispositivi
  - Profili certificato SCEP
  - Profilo di certificato PKCS
  - Profili certificato PKCS importati

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Considerazioni generali se si usa un'autorità di certificazione di terze parti

Quando si usa un'autorità di certificazione (CA) di terze parti (non Microsoft):

- Per usare i profili certificato SCEP:
  - Configurare l'integrazione con una CA di terze parti da [uno dei partner supportati](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners). La configurazione prevede che vengano seguite le istruzioni della CA di terze parti per completare l'integrazione della propria autorità di certificazione con Intune.
  - [Creare un'applicazione in Azure AD](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) che deleghi i diritti a Intune per eseguire la convalida della richiesta di verifica del certificato SCEP.

- Per i certificati PKCS importati è necessario [installare il connettore di certificati PFX per Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).

- Distribuire i certificati usando i meccanismi seguenti:
  - [Profili certificato attendibili](certificates-configure.md#create-trusted-certificate-profiles) per distribuire il certificato CA radice attendibile dalla CA radice o intermedia (emittente) ai dispositivi
  - Profili certificato SCEP
  - Profili certificato PKCS *(supportati solo con la [piattaforma PKI DigiCert](certificates-digicert-configure.md))*
  - Profili certificato PKCS importati

## <a name="supported-platforms-and-certificate-profiles"></a>Piattaforme e profili di certificato supportati

| Piattaforma              | Profilo di certificato attendibile | Profilo di certificato PKCS | Profilo di certificato SCEP | Profilo di certificato PKCS importato  |
|--|--|--|--|---|
| Amministratore dispositivo Android | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png)|  ![Supportato](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> - Dispositivi completamente gestiti (proprietario del dispositivo)   | ![Supportato](./media/certificates-configure/green-check.png) |   | ![Supportato](./media/certificates-configure/green-check.png) |   |
| Android Enterprise <br> - Dedicato (proprietario del dispositivo)   | ![Supportato](./media/certificates-configure/green-check.png)  |   | ![Supportato](./media/certificates-configure/green-check.png)  |   |
| Android Enterprise <br> - Profilo di lavoro    | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) |
| macOS                 | ![Supportato](./media/certificates-configure/green-check.png) |  ![Supportato](./media/certificates-configure/green-check.png) |![Supportato](./media/certificates-configure/green-check.png)|![Supportato](./media/certificates-configure/green-check.png)|
| Windows Phone 8.1     |![Supportato](./media/certificates-configure/green-check.png)  |  | ![Supportato](./media/certificates-configure/green-check.png)| ![Supportato](./media/certificates-configure/green-check.png) |
| Windows 8.1 e versioni successive |![Supportato](./media/certificates-configure/green-check.png)  |  |![Supportato](./media/certificates-configure/green-check.png) |   |
| Windows 10 e versioni successive  | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) | ![Supportato](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Esportare il certificato CA radice attendibile

Per usare i certificati PKCS, SCEP e PKCS importato, i dispositivi devono considerare attendibile l'autorità di certificazione radice. Per stabilire la relazione di trust, esportare il certificato della CA radice attendibile, nonché eventuali certificati di autorità di certificazione intermedia o emittente, come certificato pubblico (file CER). È possibile ottenere questi certificati dalla CA emittente o da qualsiasi dispositivo che considera attendibile la CA emittente.

Per esportare il certificato, fare riferimento alla documentazione relativa all'autorità di certificazione. Sarà necessario esportare il certificato pubblico come file con estensione cer.  Non esportare la chiave privata (file con estensione pfx).

Il file con estensione cer verrà usato quando si [creano profili di certificato attendibili](#create-trusted-certificate-profiles) per distribuire il certificato nei dispositivi.

## <a name="create-trusted-certificate-profiles"></a>Creare profili di certificati attendibili

Creare e distribuire un profilo di certificato attendibile prima di creare un profilo di certificato SCEP o PKCS oppure un profilo di certificato PKCS importato. La distribuzione di un profilo certificato attendibile agli stessi gruppi che ricevono gli altri tipi di profilo certificato garantisce che ogni dispositivo sia in grado di riconoscere la legittimità dell'autorità di certificazione. Sono inclusi i profili come quelli per VPN, Wi-Fi e posta elettronica.

I profili di certificato SCEP fanno riferimento direttamente a un profilo di certificato attendibile. I profili di certificato PKCS non fanno riferimento direttamente al profilo di certificato attendibile, ma fanno riferimento direttamente al server che ospita la CA. I profili di certificato PKCS importati non fanno riferimento direttamente al profilo di certificato attendibile, ma possono usarlo nel dispositivo. La distribuzione di un profilo di certificato attendibile nei dispositivi garantisce che venga stabilita questa relazione di trust. Quando un dispositivo non considera attendibile la CA radice, i criteri del profilo di certificato SCEP o PKCS avranno esito negativo.

Creare un profilo di certificato attendibile separato per ogni piattaforma del dispositivo che si vuole supportare, così come si farà per i profili di certificato SCEP, PKCS e PKCS importati.

> [!IMPORTANT]
> I profili radice attendibili creati per la piattaforma *Windows 10 e versioni successive*, vengono visualizzati nell'interfaccia di amministrazione di Microsoft Endpoint Manager come profili per la piattaforma *Windows 8.1 e versioni successive*. 
>
> Si tratta di un problema noto della presentazione della piattaforma per i profili certificato attendibili. Il profilo visualizza la piattaforma Windows 8.1 e versioni successive, mentre funziona con Windows 10 e versioni successive.

### <a name="to-create-a-trusted-certificate-profile"></a>Per creare un profilo certificato attendibile

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare e passare a **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

   ![Passare a Intune e creare un nuovo profilo per un certificato attendibile](./media/certificates-configure/certificates-configure-profile-new.png)

3. Immettere le proprietà seguenti:
   - **Piattaforma**: Scegliere la piattaforma dei dispositivi che riceveranno questo profilo.
   - **Profilo**: selezionare **Certificato attendibile**
  
4. Selezionare **Crea**.

5. In **Informazioni di base** immettere le proprietà seguenti:
   - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo efficace, ad esempio, è *Profilo certificato attendibile per l'intera azienda*.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** specificare il file con estensione cer per il certificato CA radice attendibile esportato in precedenza. 

   Solo per i dispositivi Windows 8.1 e Windows 10, selezionare l'**Archivio di destinazione** per il certificato attendibile da:

   - **Archivio certificati computer - Radice**
   - **Archivio certificati computer - Intermedio**
   - **Archivio certificati utente - Intermedio**

   ![Creare un profilo e caricare un certificato attendibile](./media/certificates-configure/certificates-configure-profile-fill.png)

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

   Selezionare **Avanti**.

10. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

    Selezionare **Avanti**.

11. (*Solo per Windows 10*) In **Regole di applicabilità** specificare regole di applicabilità per perfezionare l'assegnazione di questo profilo. È possibile scegliere di assegnare o non assegnare il profilo in base all'edizione del sistema operativo o alla versione di un dispositivo.

  Per altre informazioni, vedere [Regole di applicabilità](../configuration/device-profile-create.md#applicability-rules) in *Creare un profilo di dispositivo in Microsoft Intune*.

12. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona Crea, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

## <a name="additional-resources"></a>Risorse aggiuntive

- [Assegnare i profili di dispositivo](../configuration/device-profile-assign.md)  
- [Usare S/MIME per firmare e crittografare la posta elettronica](certificates-s-mime-encryption-sign.md)  
- [Usare l'autorità di certificazione di terze parti](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Passaggi successivi

Creare profili di certificato SCEP, PKCS o PKCS importati per ogni piattaforma che si vuole usare. Per continuare, vedere gli articoli seguenti:

- [Configurare l'infrastruttura per supportare i certificati SCEP con Intune](certificates-scep-configure.md)  
- [Configurare e gestire i certificati PKCS con Intune](certficates-pfx-configure.md)  
- [Creare un profilo di certificato PKCS importato](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
