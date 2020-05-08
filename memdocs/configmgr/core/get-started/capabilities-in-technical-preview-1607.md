---
title: Funzionalità nella Technical Preview 1607
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1607 per Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 73aac9e1bfb7b902a7db28ba4be00a2a02277324
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905688"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1607 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1607. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview per Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>Miglioramenti ai criteri di aggiornamento edizione di Windows 10

In questa versione sono stati apportati ai criteri i miglioramenti seguenti:

* È ora possibile usare i criteri di aggiornamento edizione con PC Windows 10 che eseguono il client di Configuration Manager, oltre che con PC Windows 10 registrati con Microsoft Intune.
* È possibile eseguire l'aggiornamento da Windows 10 Professional a una qualsiasi delle piattaforme nella procedura guidata compatibili con l'hardware in uso.

[Altre informazioni sui criteri di aggiornamento edizione di Windows 10](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>Verifica

1. Per creare i criteri di aggiornamento edizione, usare le informazioni contenute nell'[argomento sui criteri di aggiornamento edizione esistenti](../../compliance/deploy-use/upgrade-windows-version.md).
2. Distribuire i criteri a un PC Windows 10 che esegue il client di Configuration Manager.
Quando i criteri raggiungono un PC Windows specificato, il PC verrà riavviato entro due ore per applicare l'aggiornamento. Non è attualmente possibile interrompere il riavvio. Informare tutti gli utenti interessati dalla distribuzione dei criteri o pianificare la distribuzione dei criteri in ore non lavorative.

### <a name="known-issue-with-this-release"></a>Problemi noti per questa versione
Nelle impostazioni del client di Configuration Manager è possibile visualizzare le impostazioni relative ad **Aggiornamento edizione**. In questa versione tali impostazioni non sono funzionali. Usare le istruzioni fornite in precedenza per aggiornare Windows 10 a una versione più recente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Personalizzazione delle finestre di dialogo di Software Center

In Configuration Manager versione 1602 è stata introdotta la personalizzazione per Software Center. In Technical Preview versione 1607 la personalizzazione viene ora estesa a tutte le finestre di dialogo associate e alle notifiche della barra delle applicazioni in modo da offrire agli utenti di Software Center un'esperienza più uniforme.

### <a name="try-it-out"></a>Verifica

In Software Center la personalizzazione viene applicata secondo le regole seguenti:

1. Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni non è installato, Software Center visualizzerà il nome dell'organizzazione specificato nell'impostazione **Nome organizzazione visualizzato in Software Center** del client **Agente computer**. Per istruzioni, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).

2. Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni è installato, Software Center visualizzerà il nome dell'organizzazione e il colore specificati nelle proprietà del ruolo del server del sito punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Configuration options for Application Catalog website point](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website) (Opzioni di configurazione per il punto per siti Web del Catalogo applicazioni).

3. Se una sottoscrizione di Microsoft Intune è configurata e connessa all'ambiente Configuration Manager, Software Center visualizzerà il nome dell'organizzazione, il colore e il logo aziendale specificati nelle proprietà della sottoscrizione di Intune.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Usare la stessa scheda di rete per più distribuzioni avviate da PXE
In Technical Preview versione 1607, se si usa una scheda ethernet per creare un'immagine di più dispositivi (ad esempio una scheda ethernet USB usata su più dispositivi), è possibile abilitare una nuova impostazione che consente di immettere gli identificatori hardware per le schede ethernet. Configuration Manager ignora gli identificatori hardware nell'elenco quando si esegue un'installazione di PXE e per la registrazione del client.

Per altre informazioni su questo problema, vedere il [blog del team di supporto di Configuration Manager OSD](https://techcommunity.microsoft.com/t5/configuration-manager-archive/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in/ba-p/273721).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Abilitare la funzionalità per gestire gli identificatori hardware duplicati  
1. Nella console di Configuration Manager andare su **Amministrazione** > **Panoramica** > **Servizi cloud** > **Aggiornamenti e manutenzione** > **Funzionalità**.
2. Nel riquadro informazioni selezionare **Gestione degli identificatori hardware duplicati**.
3. Nel gruppo **Funzionalità** della scheda **Home** fare clic su **Attiva**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Aggiungere identificatori hardware che Configuration Manager deve ignorare  
1. Nella console di Configuration Manager andare su **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Nella scheda **Home** , del gruppo **Siti** , fare clic su **Impostazioni gerarchia**.
3. Andare alla scheda **Approvazione client e record in conflitto**.
4. Per aggiungere nuovi identificatori hardware, fare clic su **Aggiungi** nella sezione **Identificatori hardware duplicati**.
