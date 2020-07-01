---
title: Configurare le impostazioni di Microsoft Edge
titleSuffix: Configuration Manager
description: Configurare le impostazioni per la versione legacy del Web browser Microsoft Edge nei client Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 898d5240046655ca3d13037f74c92e730ab1993e
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506143"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Configurare le impostazioni della versione legacy di Microsoft Edge in Configuration Manager

> [!IMPORTANT]
> Se si usa Microsoft Edge versione 77 o successiva e si sta provando ad aprire il riquadro Impostazioni, immettere `edge://settings/profiles` nella barra degli indirizzi del browser invece che in Cerca. Per altre informazioni, vedere [Scopri Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> Questo articolo consente ai professionisti IT di gestire le impostazioni della versione legacy di Microsoft Edge con Microsoft Endpoint Configuration Manager.

*Si applica a: Configuration Manager (Current Branch)*

<!-- 1357310 -->
I clienti che usano la [versione legacy del Web browser Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/) in client Windows 10 possono creare criteri di conformità di Configuration Manager per configurare le impostazioni del browser.

Questi criteri si applicano solo ai client in Windows 10, versione 1703 o successiva e alla versione legacy di Microsoft Edge 45 e versioni precedenti. <!--511552-->

Per altre informazioni sulla gestione di Microsoft Edge 77 o versione successiva con Configuration Manager, vedere [Distribuire Microsoft Edge versione 77 e successive](../../apps/deploy-use/deploy-edge.md). Per altre informazioni sulla configurazione dei criteri per Microsoft Edge 77 o versione successiva, vedere [Microsoft Edge - Criteri](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies).

## <a name="policy-settings"></a>Impostazioni dei criteri

Questo criterio include attualmente le impostazioni seguenti:

- **Imposta il browser Microsoft Edge come predefinito**: configura l'impostazione dell'app predefinita di Windows 10 per il Web browser su Microsoft Edge.

- **Consenti l'elenco a discesa della barra degli indirizzi**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser AllowAddressBarDropdown](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).

- **Consenti la sincronizzazione dei Preferiti tra browser Microsoft**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser SyncFavoritesBetweenIEAndMicrosoftEdge](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).

- **Consenti la cancellazione dei dati di esplorazione all'uscita**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser ClearBrowsingDataOnExit](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).

- **Consenti le intestazioni Do Not Track**: per altre informazioni, vedere [Criterio del browser AllowDoNotTrack](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).

- **Consenti riempimento automatico**: per altre informazioni, vedere [Criterio del browser AllowAutofill](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).

- **Consenti cookie**: per altre informazioni, vedere [Criterio del browser AllowCookies](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).

- **Consenti blocco popup**: per altre informazioni, vedere [Criterio del browser AllowPopups](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).

- **Consenti suggerimenti di ricerca nella barra degli indirizzi**: per altre informazioni, vedere [Criterio del browser AllowSearchSuggestionsinAddressBar](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).

- **Consenti l'invio di traffico Intranet a Internet Explorer**: per altre informazioni, vedere [Criterio del browser SendIntranetTraffictoInternetExplorer](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).

- **Consenti strumento per la gestione delle password**: per altre informazioni, vedere [Criterio del browser AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).

- **Consenti gli Strumenti di sviluppo**: per altre informazioni, vedere [Criterio del browser AllowDeveloperTools](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).

- **Consenti le estensioni**: per altre informazioni, vedere [Criterio del browser AllowExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

> [!TIP]
> Per altre informazioni sull'uso di criteri di gruppo per configurare queste e altre impostazioni, vedere [Criteri di gruppo della versione legacy di Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Configurare le impostazioni di Windows Defender SmartScreen per la versione legacy di Microsoft Edge
<!--1353701-->
Questi criteri prevedono tre impostazioni aggiuntive per [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). I criteri ora includono le seguenti impostazioni aggiuntive nella pagina **Impostazioni di SmartScreen**:

- **Consenti SmartScreen**: specifica se Windows Defender SmartScreen è consentito. Per altre informazioni, vedere il [criterio di browser AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Gli utenti possono eseguire l'override del prompt di SmartScreen per i siti**: specifica se gli utenti possono eseguire l'override degli avvisi del filtro Windows Defender SmartScreen su siti Web potenzialmente dannosi. Per altre informazioni, vedere il [criterio di browser PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).

- **Gli utenti possono eseguire l'override del prompt di SmartScreen per i file**: specifica se gli utenti possono eseguire l'override degli avvisi del filtro Windows Defender SmartScreen sul download di file non verificati. Per altre informazioni, vedere il [criterio di browser PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).

## <a name="create-the-browser-profile"></a>Creare il profilo del browser

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **Impostazioni di conformità** e selezionare il nodo **Profili del browser Microsoft Edge**. Selezionare **Crea un profilo di Microsoft Edge** sulla barra multifunzione.

2. Specificare un **Nome** per il criterio e una descrizione facoltativa nel campo **Descrizione**, quindi selezionare **Avanti**.

3. Nella pagina **Impostazioni generali** modificare il valore delle impostazioni da includere nel criterio selezionando **Configurato**. Per continuare la procedura guidata, configurare l'impostazione su **Imposta il browser Microsoft Edge come predefinito**.

4. Configurare le impostazioni della pagina **Impostazioni di SmartScreen**.

5. Nella pagina **Piattaforme supportate** selezionare le architetture e le versioni del sistema operativo a cui si applica il criterio.

6. Completare la procedura guidata.

## <a name="deploy-the-policy"></a>Distribuire il criterio

1. Selezionare il criterio e nella barra multifunzione selezionare **Distribuisci**.

2. Fare clic su **Sfoglia** per selezionare la raccolta utenti o dispositivi nella quale si vuole distribuire il criterio.

3. Se necessario selezionare le opzioni aggiuntive:

    1. Generare avvisi quando il criterio non è conforme.

    2. Impostare la pianificazione in base alla quale il client valuta la conformità del dispositivo al criterio.

4. Selezionare **OK** per creare la distribuzione.

## <a name="next-steps"></a>Passaggi successivi

Come avviene con qualsiasi criterio delle impostazioni di conformità, il client monitora e aggiorna le impostazioni sulla pianificazione specificata. [Monitorare e creare report sulla conformità dei dispositivi](monitor-compliance-settings.md) nella console di Configuration Manager.
