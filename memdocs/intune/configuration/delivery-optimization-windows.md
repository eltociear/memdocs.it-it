---
title: Impostazioni relative all'Ottimizzazione recapito per Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Configurare l'uso dell'Ottimizzazione recapito nei dispositivi Windows 10 gestiti con Intune. In Intune, creare un profilo di configurazione del dispositivo per installare gli aggiornamenti da Internet. Vedere anche come sostituire gli anelli di aggiornamento esistenti con un profilo di Ottimizzazione recapito.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: e42d7f303d3d79e2683845b50c7d3dceb11f1686
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820443"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Impostazioni di Ottimizzazione recapito in Microsoft Intune

Con Intune, usare le impostazioni di Ottimizzazione recapito per i dispositivi Windows 10 per ridurre il consumo di larghezza di banda quando tali dispositivi scaricano aggiornamenti e applicazioni. Configurare Ottimizzazione recapito come parte dei profili di configurazione dei dispositivi.  

Questo articolo descrive come configurare le impostazioni di Ottimizzazione recapito come parte di un profilo di configurazione del dispositivo. Dopo aver creato un profilo, lo si assegna o distribuisce ai dispositivi Windows 10.

Per visualizzare un elenco delle impostazioni di Ottimizzazione recapito supportate da Intune, vedere [Impostazioni di Ottimizzazione recapito per Intune](delivery-optimization-settings.md).  

Per informazioni sull'ottimizzazione recapito in Windows 10, vedere [Ottimizzazione recapito per gli aggiornamenti](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) nella documentazione di Windows.  

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.

3. Immettere le proprietà seguenti:

   - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
   - **Profilo**: selezionare **Ottimizzazione recapito**.

4. Selezionare **Crea**.

5. In **Informazioni di base** immettere le proprietà seguenti:

   - **Nome**: immettere un nome descrittivo per il nuovo profilo.
   - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. Nella pagina **Impostazioni di configurazione** definire il modo in cui si vogliono scaricare gli aggiornamenti e le app. Per informazioni sulle impostazioni disponibili, vedere [Impostazioni di Ottimizzazione recapito per Intune](delivery-optimization-settings.md).

   Dopo aver configurato le impostazioni, selezionare **Avanti**.

8. Nella pagina **Ambito (tag)** selezionare **Selezionare i tag di ambito** per aprire il riquadro *Seleziona tag* per assegnare tag di ambito al profilo.
  
   Selezionare **Avanti** per continuare.

9. Nella pagina **Assegnazioni** selezionare i gruppi che riceveranno questo profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](../configuration/device-profile-assign.md).

   Selezionare **Avanti**.

10. Nella pagina **Regole di applicabilità** usare le opzioni **Regola**, **Proprietà** e **Valore** per definire il modo in cui il profilo viene applicato all'interno dei gruppi assegnati.

11. Al termine, nella pagina **Rivedi e crea** scegliere **Crea**. Il profilo viene creato e visualizzato nell'elenco.

Alla successiva sincronizzazione di ogni dispositivo viene applicato il criterio.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Rimuovere Ottimizzazione recapito dagli anelli di aggiornamento di Windows 10

Ottimizzazione recapito è una funzionalità precedentemente configurata come parte degli anelli di aggiornamento software. A partire da febbraio 2019, le impostazioni di Ottimizzazione recapito sono configurate come parte di un profilo di configurazione del dispositivo di Ottimizzazione del recapito, che include impostazioni aggiuntive con effetti più ampi del recapito degli aggiornamenti software ai dispositivi. Se non è già stato fatto, rimuovere l'impostazione di Ottimizzazione recapito dagli anelli di aggiornamento impostandola su *Non configurata* e quindi usare un profilo di Ottimizzazione recapito per gestire la gamma più ampia di opzioni disponibili.

1. Creare un profilo di configurazione del dispositivo di Ottimizzazione recapito:

    1. Nell'interfaccia di amministrazione di Microsoft Endpoint Manager selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
    2. Immettere le proprietà seguenti:

        - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
        - **Profilo**: selezionare **Ottimizzazione recapito**.

    3. Selezionare **Crea**.
    4. In **Informazioni di base** immettere le proprietà seguenti:

        - **Nome**: immettere un nome descrittivo per il nuovo profilo.
        - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

    5. Selezionare **Avanti**.
    6. In **Impostazioni di configurazione** > **Modalità di download**, scegliere la stessa modalità usata dall'anello di aggiornamento software esistente, *a meno che* non si voglia cambiare le impostazioni applicate ai dispositivi. Le opzioni disponibili sono:

        - **Non configurato**
        - **Solo HTTP, senza peering**
        - **HTTP misto con peering nella stessa NAT**
        - **HTTP misto con peering in un gruppo privato**
        - **HTTP misto con peering Internet**
        - **Modalità di download semplice senza peering**
        - **Modalità Bypass**

    7. Configurare [le impostazioni aggiuntive](delivery-optimization-settings.md) che si vogliono gestire e continuare a creare il profilo.

        In **Assegnazioni**, assegnare questo nuovo profilo agli stessi dispositivi e utenti dell'anello di aggiornamento software esistente. Per altre informazioni, vedere [Assegnare il profilo](device-profile-assign.md).

2. Annullare la configurazione dell'anello di aggiornamento software esistente:

    1. Nell'interfaccia di amministrazione di Microsoft Endpoint Manager passare ad **Aggiornamenti software** > Anelli di aggiornamento di Windows 10.
    2. Selezionare l'anello di aggiornamento nell'elenco.
    3. Nelle impostazioni specificare **Non configurata** per **Modalità di download con Ottimizzazione recapito**.
    4. **OK** > **Salva** per salvare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver [assegnato il profilo](device-profile-assign.md), [monitorarne lo stato](device-profile-monitor.md).

Visualizzare le [Impostazioni di Ottimizzazione recapito](delivery-optimization-settings.md) per Intune.
