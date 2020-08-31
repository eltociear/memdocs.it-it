---
title: Partner per la conformità dei dispositivi in Microsoft Intune - Azure | Microsoft Docs
description: Usare un partner per la conformità dei dispositivi di terze parti come origine dei dati di conformità per i dispositivi gestiti con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643704"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Supportare partner per la conformità dei dispositivi di terze parti in Intune

Microsoft Intune può aggiungere ad Azure Active Directory (Azure AD) dati sullo stato di conformità per i dispositivi gestiti con uno o più partner per la conformità dei dispositivi di terze parti. Con questa configurazione, i dati di conformità di tali dispositivi possono essere usati con i criteri di accesso condizionale.

Per impostazione predefinita, Intune è configurato come autorità di gestione di dispositivi mobili (MDM) per i dispositivi. Quando si aggiunge ad Azure AD e Intune un partner per la conformità, si configura tale partner come origine dell'autorità di gestione di dispositivi mobili (MDM) per i dispositivi assegnati a tale partner tramite un gruppo di utenti di Azure AD.

Per abilitare l'uso dei dati dei partner per la conformità dei dispositivi, completare le attività seguenti:

1. **Configurare Intune per l'interazione con il partner per la conformità dei dispositivi** e quindi configurare gruppi di utenti i cui dispositivi vengono gestiti da tale partner per la conformità.

2. **Configurare il partner per la conformità per l'invio di dati a Intune**.

3. **Registrare i dispositivi iOS o Android con tale partner per la conformità dei dispositivi**.

Una volta completate queste attività, il partner per la conformità dei dispositivi invia i dettagli sullo stato dei dispositivi a Intune. Intune aggiunge quindi queste informazioni ad Azure AD. Se ad esempio un dispositivo ha lo stato non conforme, lo stato viene aggiunto al record del dispositivo in Azure AD.

Lo stato di conformità viene quindi valutato dai criteri di accesso condizionale, come avviene per i dati sullo stato di conformità per i dispositivi gestiti da Intune.  Per impostazione predefinita, Intune è un partner per la conformità registrato per iOS e Android. Quando si aggiungono altri partner, è possibile impostare l'ordine di priorità per garantire che il partner corretto gestisca il dispositivo in base alle esigenze aziendali.

## <a name="supported-device-compliance-partners"></a>Partner per la conformità dei dispositivi supportati

In anteprima pubblica:

- VMware Workspace ONE UEM (in precedenza AirWatch)

## <a name="prerequisites"></a>Prerequisiti

- Sottoscrizione a Microsoft Intune e accesso all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

- Sottoscrizione al partner per la conformità dei dispositivi.

- Per le piattaforme per dispositivi supportate e i prerequisiti aggiuntivi, vedere la documentazione del partner per la conformità.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Configurare Intune per l'interazione con un partner per la conformità dei dispositivi

Abilitare il supporto per un partner di conformità del dispositivo per usare i dati sullo stato di conformità di tale partner con i criteri di accesso condizionale.

### <a name="add-a-compliance-partner-to-intune"></a>Aggiungere a Intune un partner per la conformità

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Passare a **Amministrazione del tenant** > **Connettori e token** > **Gestione della conformità dei partner** > **Aggiungi un partner per la conformità**.

   > [!div class="mx-imgBorder"]
   > ![Aggiungere un partner per la conformità dei dispositivi](./media/device-compliance-partners/add-compliance-partner.png)

3. Nella pagina **Informazioni di base** espandere l'elenco a discesa **Partner per la conformità** e selezionare il partner da aggiungere.

   - Per usare VMware Workspace ONE come partner di conformità per le piattaforme iOS o Android, selezionare **VMware Workspace ONE mobile compliance**.

   Successivamente selezionare l'elenco a discesa **Piattaforma** e selezionare la piattaforma. macOS non è supportato in questa anteprima.

   È previsto un limite di un solo partner per piattaforma, anche se ad Azure AD sono stati aggiunti più partner per la conformità.

4. In **Assegnazioni** selezionare i gruppi utenti i cui dispositivi saranno gestiti da questo partner. Con questa assegnazione, si modificherà l'autorità MDM in modo che i dispositivi applicabili usino questo partner. Agli utenti con dispositivi gestiti dal partner è necessario assegnare anche una licenza per Intune.

5. Nella pagina **Rivedi e crea** rivedere le selezioni e quindi selezionare **Crea** per completare questa configurazione.

La configurazione viene ora visualizzata nella pagina Gestione della conformità dei partner.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Modificare la configurazione per un partner per la conformità

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Passare ad **Amministrazione del tenant** > **Connettori e token** > **Gestione della conformità dei partner** e quindi selezionare la configurazione del partner che si vuole modificare. Le configurazioni sono ordinate in base al tipo di piattaforma.

3. Nella pagina **Panoramica** della configurazione del partner selezionare **Proprietà** per aprire la pagina Proprietà in cui è possibile modificare le assegnazioni.

4. Nella pagina **Proprietà** selezionare **Modifica** per aprire la visualizzazione Assegnazioni in cui è possibile modificare i gruppi che useranno questa configurazione.

5. Selezionare **Verifica e salva** e quindi **Salva** per salvare le modifiche.

6. *Questo passaggio si applica solo quando si usa VMware Workspace ONE*:

   Nella console di Workspace ONE UEM è necessario sincronizzare manualmente le modifiche salvate nell'interfaccia di amministrazione di Microsoft Endpoint Manager. Finché le modifiche non vengono sincronizzate manualmente, Workspace ONE UEM non è in grado di riconoscere le modifiche di configurazione e gli utenti dei nuovi gruppi assegnati non segnalano correttamente la conformità.

   Per eseguire manualmente la sincronizzazione dai servizi di Azure:
   1. Accedere alla console di VMware Workspace ONE UEM.
   2. Passare a **Settings** > **System** > **Enterprise Integration** > **Directory Services** (Impostazioni > Sistema > Integrazione aziendale > Servizi di directory).
   3. Per *Sync Azure Services* (Sincronizza servizi di Azure), fare clic su **SYNC** (Sincronizza).

      Tutte le modifiche apportate dopo la configurazione iniziale o l'ultima sincronizzazione manuale vengono sincronizzate con UEM dai servizi di Azure.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Configurare il partner per la conformità per l'interazione con Intune

Per consentire a un partner per la conformità dei dispositivi di interagire con Intune, è necessario completare le configurazioni specifiche di tale partner. Per informazioni su questa attività, vedere la documentazione relativa al partner applicabile:

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Registrare i dispositivi iOS o Android con tale partner per la conformità dei dispositivi

Per informazioni su come registrare i dispositivi con tale partner, vedere la documentazione relativa ai partner per la conformità dei dispositivi. Dopo che i dispositivi sono stati registrati e hanno inviato i dati di conformità al partner, tali dati di conformità vengono inoltrati a Intune e aggiunti ad Azure AD.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Monitorare i dispositivi gestiti da partner per la conformità dei dispositivi di terze parti

Dopo aver configurato i partner per la conformità dei dispositivi di terze parti e aver registrato i dispositivi con questi partner, i partner inviano i dettagli di conformità a Intune. Dopo che Intune ha ricevuto i dati, è possibile visualizzare i dettagli sui dispositivi nel portale di Azure.

Accedere al portale di Azure e passare a **Azure AD** > **Dispositivi** > [**Tutti i dispositivi**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## <a name="next-steps"></a>Passaggi successivi

Consultare la documentazione del partner di terze parti per creare criteri di conformità per i dispositivi.

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
