---
title: App nel Portale aziendale
titleSuffix: Configuration Manager
description: Configurando i dispositivi co-gestiti per l'uso del Portale aziendale, è possibile offrire un'esperienza utente coerente.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd49546e49d6964cfe37b0b13e1abe9175f4aa0e
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432558"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Usare l'app Portale aziendale in dispositivi con co-gestione

*Si applica a: Configuration Manager (Current Branch)*

<!--CMADO-3601237,INADO-4297660-->

A partire dalla versione 2006, il Portale aziendale è ora l'esperienza di portale delle app multipiattaforma per Microsoft Endpoint Manager. Configurando i dispositivi co-gestiti in modo da usare anche il Portale aziendale, è possibile offrire un'esperienza utente coerente su tutti i dispositivi.

Il Portale aziendale supporta le azioni seguenti:

- Avviare l'app Portale aziendale in dispositivi con co-gestione ed eseguire l'accesso Single Sign-On (SSO) ad Azure Active Directory (Azure AD).
- Visualizzare le app di Configuration Manager disponibili e installate nel Portale aziendale insieme alle app di Intune.
- Installare le app di Configuration Manager disponibili dal Portale aziendale e ricevere informazioni sullo stato dell'installazione.

:::image type="content" source="media/3601237-company-portal.png" alt-text="Portale aziendale con app di Configuration Manager" lightbox="media/3601237-company-portal.png":::

Il comportamento del Portale aziendale varia a seconda della configurazione del carico di lavoro di co-gestione:

| Carico di lavoro | Impostazione | Comportamento |
|----------|---------|----------|
| App client | **Configuration Manager** | Vengono visualizzate solo le app client di Configuration Manager |
| App client | **Intune pilota** o **Intune** | Vengono visualizzate le app di Configuration Manager e le app client di Intune |
| App A portata di clic di Office | **Configuration Manager** | Vengono visualizzate solo le app A portata di clic di Office di Configuration Manager |
| App A portata di clic di Office | **Intune pilota** o **Intune** | Vengono visualizzate solo le app A portata di clic di Office di Intune |

Per altre informazioni, vedere gli articoli seguenti:

- [Diagramma per i carichi di lavoro delle app](workloads.md#diagram-for-app-workloads)

- [Come trasferire i carichi di lavoro di Configuration Manager a Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Prerequisiti

- Configuration Manager (Current Branch) versione 2006 o successiva <sup>([Vedere Domande frequenti](#bkmk_ver-prereq))</sup>

- App Portale aziendale versione 11.0.8980.0 o successiva

- Windows 10, versione 1803 o successiva:

  - Registrazione per la [co-gestione](how-to-enable.md)

  - Accesso agli [endpoint Internet per Intune](../../intune/fundamentals/intune-endpoints.md)

- Per gli account utente che accedono a questi dispositivi sono necessarie le configurazioni seguenti:

  - Un'identità Azure AD

  - Una licenza Intune assegnata

## <a name="configure-and-deploy"></a>Configurare e distribuire

### <a name="configuration-manager-client-settings"></a>Impostazioni client di Configuration Manager

Per assicurarsi che gli utenti ricevano le notifiche solo dal Portale aziendale, configurare le impostazioni client di Configuration Manager. Nel gruppo **Software Center** delle impostazioni del dispositivo impostare **Selezionare il portale per gli utenti** su **Portale aziendale**.

Per altre informazioni sulle impostazioni client, vedere gli articoli seguenti:

- [Come configurare le impostazioni client](../core/clients/deploy/configure-client-settings.md)
- [Informazioni sulle impostazioni client](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Distribuire l'app Portale aziendale

- Gli utenti possono installare manualmente l'app Portale aziendale da [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab).

- Per richiedere l'app nei dispositivi co-gestiti, il processo di distribuzione dipende dallo stato del carico di lavoro di co-gestione delle [app client](workloads.md#client-apps):

  - Se il carico di lavoro delle app client è con Configuration Manager, [creare e distribuire un'applicazione con Configuration Manager](../apps/get-started/create-and-deploy-an-application.md). Scaricare l'app Portale aziendale offline da [Microsoft Store per le aziende](https://www.microsoft.com/business-store).

  - Se il carico di lavoro delle app client è con Intune, è possibile distribuirlo tramite Configuration Manager oppure [aggiungere l'app Portale aziendale di Windows 10 usando Microsoft Intune](../../intune/apps/store-apps-company-portal-app.md).

Per altre informazioni sulla personalizzazione del Portale aziendale, vedere [Come personalizzare le app Portale aziendale Intune](../../intune/apps/company-portal-app.md).

## <a name="use-the-company-portal"></a>Usare il Portale aziendale

1. Avviare il Portale aziendale dal menu Start. L'utente attualmente connesso viene connesso automaticamente al Portale aziendale in base alla sua identità di Azure AD.

1. Selezionare la pagina **App**. Le app di Configuration Manager verranno visualizzate nell'elenco.

1. Selezionare una delle app distribuite da Configuration Manager.

    - La scheda **Panoramica** mostra i dettagli sull'app, come dimensioni, versione e data di pubblicazione.

    - Per verificare se Configuration Manager è il servizio di gestione per questa app, passare alla scheda **Informazioni aggiuntive**.

    - Per installare l'app, selezionare **Installa**. Il Portale aziendale mostra lo stato dell'installazione e al termine verrà visualizzata una notifica.

    - Se l'app è già installata, selezionare **Disinstalla** per rimuoverla.

    - Selezionare i puntini di sospensione (`...`) per visualizzare azioni aggiuntive, ad esempio **Ripristina** e **Condividi**.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="App di Configuration Manager con i dettagli nel Portale aziendale" lightbox="media/3601237-company-portal-app-details.png":::

    - Dopo aver installato un'app Web di Configuration Manager, selezionare il menu con i puntini di sospensione e quindi scegliere **Apri nel browser** per avviarla.

    - Se l'installazione di un'applicazione di Configuration Manager non riesce con un codice di errore noto, selezionare il collegamento allo stato di errore per cercare il codice di errore.

Se si cambia l'impostazione client per il Portale aziendale, quando un utente seleziona una notifica di Configuration Manager, viene avviato il Portale aziendale. Se la notifica riguarda uno scenario non supportato dal Portale aziendale, la selezione della notifica avvia Software Center.

Per risolvere i problemi relativi all'installazione delle app di Configuration Manager, vedere la sezione **Guida e supporto tecnico** del Portale aziendale. Se si usa l'opzione **Supporto**, è possibile inviare i file di log di Configuration Manager come parte della richiesta.

## <a name="frequently-asked-questions-faq"></a>Domande frequenti

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Perché il nuovo Portale aziendale visualizza le app di Configuration Manager quando si usa Configuration Manager versione 2002?

Il Portale aziendale versione 11.0.8980.0 o successiva mostra le applicazioni distribuite tramite Configuration Manager per tutti i client con co-gestione in cui viene usato. Configuration Manager versione 2006 è il prerequisito poiché aggiunge l'impostazione client per controllare le notifiche. Se si installa il Portale aziendale in un dispositivo con co-gestione di una versione precedente o non si configura l'impostazione client, gli utenti visualizzeranno le notifiche di entrambi i portali. Questa esperienza può essere disorientante per gli utenti.

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Il Portale aziendale supporta le applicazioni distribuite come aggiornamenti software da Configuration Manager?

Sì. Se si distribuisce un'app usando la funzionalità degli aggiornamenti software, il client la considera allo stesso modo, sia che l'esperienza utente sia il Portale aziendale o Software Center.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>Gli utenti possono ripristinare, disinstallare e aggiornare le app di Configuration Manager nel Portale aziendale?

Sì. Se si configura l'app Configuration Manager per supportare queste azioni aggiuntive, il Portale aziendale supporta il ripristino, la disinstallazione e l'aggiornamento.

## <a name="known-issues"></a>Problemi noti

Le funzionalità seguenti di Software Center non sono attualmente disponibili nel Portale aziendale:

- Alcune informazioni sull'app, ad esempio se è necessario un riavvio o il tempo stimato per l'installazione

- [Gruppi di app](../apps/deploy-use/create-app-groups.md)

Altri problemi noti:

- Se la stessa app viene distribuita sia da Configuration Manager che da Intune verrà visualizzata due volte nel Portale aziendale.

- Se si esegue una ricerca nel Portale aziendale, le app di Intune vengono sempre visualizzate prima di quelle di Configuration Manager.

## <a name="next-steps"></a>Passaggi successivi

[Come trasferire i carichi di lavoro di Configuration Manager a Intune](how-to-switch-workloads.md)

[Come personalizzare l'app del Portale aziendale Intune](../../intune/apps/company-portal-app.md)
