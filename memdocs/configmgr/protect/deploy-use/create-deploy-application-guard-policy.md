---
title: Gestire i criteri di Application Guard
titleSuffix: Configuration Manager
description: Informazioni su come creare e distribuire criteri di Microsoft Defender Application Guard
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3fb7559f624afdb16ef228c61331387c163fbd54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697110"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Creare e distribuire criteri di Microsoft Defender Application Guard

*Si applica a: Configuration Manager (Current Branch)*
<!-- 1351960 -->  
È possibile creare e distribuire criteri di [Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview) usando Configuration Manager Endpoint Protection. Questi criteri consentono di proteggere gli utenti aprendo i siti Web non attendibili in un contenitore isolato protetto non accessibile da altre parti del sistema operativo.

## <a name="prerequisites"></a>Prerequisiti

Per creare e distribuire criteri di Microsoft Defender Application Guard, è necessario usare la versione Windows 10 Fall Creators Update (1709). I dispositivi Windows 10 in cui verranno distribuiti i criteri devono essere configurati con [criteri di isolamento di rete](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings). Per altre informazioni, vedere [Panoramica di Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Creare un criterio e individuare le impostazioni disponibili

1. Nella console di Configuration Manager scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando l'[articolo](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard) come riferimento, è possibile selezionare e configurare le impostazioni disponibili. Configuration Manager consente di configurare determinate impostazioni dei criteri:
   - [Impostazioni per l'interazione degli host](#bkmk_HIS)
   - [Comportamento dell'applicazione](#bkmk_ABS)
   - [Gestione file](#bkmk_FM)
5. Nella pagina **Definizione di rete** specificare l'identità aziendale e definire il limite di rete aziendale.

    > [!NOTE]
    > I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. È possibile creare due tipi diversi di elenchi di isolamento di rete e quindi distribuirli nel client:
    >
    >  - uno da Windows Information Protection
    >  - uno da Microsoft Defender Application Guard
    >
    > Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo. Per altre informazioni, vedere la [documentazione di Windows Information Protection](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Al termine, completare la procedura guidata e distribuire i criteri in uno o più dispositivi Windows 10 1709.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> Impostazioni per l'interazione degli host

Configura le interazioni tra i dispositivi host e il contenitore Application Guard. Prima di Configuration Manager versione 1802, le impostazioni relative al comportamento delle applicazioni e all'interazione degli host si trovavano nella scheda **Impostazioni**.

- **Appunti**: in Impostazioni prima di Configuration Manager 1802
  - Tipo di contenuto consentito
    - Testo
    - Immagini
- **Stampa:**
  - Abilitazione della stampa in XPS
  - Abilitazione della stampa in PDF
  - Abilitazione della stampa nelle stampanti locali
  - Abilitazione della stampa nelle stampanti di rete
- **Grafica:** (a partire da Configuration Manager versione 1802)
  - Accesso all'unità di elaborazione grafica virtuale
- **File:** (a partire da Configuration Manager versione 1802)
  - Salvataggio dei file scaricati nell'host

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> Impostazioni relative al comportamento delle applicazioni

Consentono di configurare il comportamento delle applicazioni all'interno della sessione di Application Guard. Prima di Configuration Manager versione 1802, le impostazioni relative al comportamento delle applicazioni e all'interazione degli host si trovavano nella scheda **Impostazioni**.

- **Contenuto:**
  - I siti aziendali possono caricare contenuti non aziendali, ad esempio plug-in di terze parti.
- **Altro:**
  - Conserva i dati del browser generati dall'utente
  - Controlla gli eventi di sicurezza nella sessione Application Guard isolata

### <a name="file-management"></a><a name="bkmk_FM"></a> Gestione file
<!--3555858-->
A partire dalla versione 1906 di Configuration Manager, un'impostazione dei criteri consente agli utenti di considerare attendibili i file che si aprono normalmente in Application Guard. Al termine dell'esecuzione, i file vengono aperti nel dispositivo host anziché in Application Guard. Per altre informazioni sui criteri di Application Guard, vedere [Configurare le impostazioni dei criteri di Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard).

- **Consenti agli utenti di ritenere attendibili i file aperti in Windows Defender Application Guard**: consente all'utente di contrassegnare i file come attendibili. Quando un file è attendibile, viene aperto nell'host anziché in Application Guard. Si applica ai client Windows 10 versione 1809 o successive.
  - **Non consentito:** non consente agli utenti di contrassegnare i file come attendibili (impostazione predefinita).
  - **File checked by antivirus:** (File controllati da antivirus) consente agli utenti di contrassegnare i file come attendibili dopo il controllo dell'antivirus.
  - **Tutti i file:** consente agli utenti di contrassegnare qualsiasi file come attendibile.

Quando si abilita la gestione dei file, è possibile che vengano visualizzati errori registrati nel log DCMReporting.log del client. Gli errori riportati di seguito in genere non hanno effetto sulle funzionalità: <!--4619457-->

- Nei dispositivi compatibili:
  - FileTrustCriteria_condition not found (Impossibile trovare FileTrustCriteria_condition)
- Nei dispositivi non compatibili:
  - FileTrustCriteria_condition not found (Impossibile trovare FileTrustCriteria_condition)
  - FileTrustCriteria_condition could not be located in the map (Impossibile trovare FileTrustCriteria_condition nella mappa)
  - FileTrustCriteria_condition not found in digest (Impossibile trovare FileTrustCriteria_condition nel digest)

Per modificare le impostazioni di Application Guard, espandere **Endpoint Protection** nell'area di lavoro **Asset e conformità** e quindi fare clic sul nodo **Windows Defender Application Guard**. Fare clic con il pulsante destro del mouse sui criteri da modificare e quindi selezionare **Proprietà**.

## <a name="known-issues"></a>Problemi noti

I dispositivi che eseguono Windows 10, versione 2004 mostreranno errori nella creazione di report di conformità per i criteri di attendibilità file di Microsoft Defender Application Guard. Questo problema si verifica perché alcune sottoclassi sono state rimosse dalla classe WMI `MDM_WindowsDefenderApplicationGuard_Settings01` in Windows 10, versione 2004. Tutte le altre impostazioni di Microsoft Defender Application Guard verranno comunque applicate. Solo i criteri di attendibilità file non verranno applicati correttamente. Non sono attualmente disponibili soluzioni alternative per ignorare l'errore. <!--7099444,5946790-->

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Microsoft Defender Application Guard, vedere
 - [Panoramica di Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).
- [Domande frequenti su Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard).