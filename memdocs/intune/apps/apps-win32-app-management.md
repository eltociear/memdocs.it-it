---
title: Gestione delle app Win32 in Microsoft Intune
titleSuffix: ''
description: Informazioni su come gestire le app Win32 con Microsoft Intune. Questo argomento offre una panoramica delle funzionalità di distribuzione e gestione delle app Win32 di Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: db28653207d7bf4341d614aeecb769dcc145caaa
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083931"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Gestione delle app Win32 in Microsoft Intune

Microsoft Intune offre funzionalità di gestione delle app Win32. Anche se per i clienti connessi al cloud è possibile usare Microsoft Endpoint Configuration Manager per la gestione delle app Win32, i clienti che usano solo Intune avranno maggiori funzionalità di gestione per le app line-of-business Win32. Questo argomento offre una panoramica delle funzionalità di gestione delle app Win32 di Intune e le relative informazioni.

> [!NOTE]
> Questa funzionalità di gestione delle app supporta l'architettura del sistema operativo sia a 32 bit che a 64 bit per le applicazioni di Windows.

> [!IMPORTANT]
> Quando si distribuiscono app Win32, è consigliabile usare esclusivamente l'approccio con l'[estensione di gestione di Intune](../apps/intune-management-extension.md), in particolare quando si usa un programma di installazione di app Win32 a più file. Se vengono installate sia app Win32 sia app line-of-business durante la registrazione di Autopilot, l'installazione delle app potrebbe non riuscire. L'estensione di gestione di Intune viene installata automaticamente quando uno script di PowerShell o un'app Win32 viene assegnata all'utente o al dispositivo.

## <a name="prerequisites"></a>Prerequisiti

Per usare la gestione delle app Win32, assicurarsi che siano soddisfatti i criteri seguenti:

- Usare Windows 10 versione 1607 o successive (edizioni Enterprise, Pro ed Education).
- I dispositivi devono essere stati aggiunti ad Azure Active Directory (Azure AD) e registrati automaticamente. L'estensione di gestione di Intune supporta i dispositivi aggiunti ad Azure AD, aggiunti al dominio ibrido e registrati con Criteri di gruppo. 
  > [!NOTE]
  > Per lo scenario di registrazione con Criteri di gruppo, l'utente usa l'account utente locale per aggiungere ad Azure AD il proprio dispositivo Windows 10. L'utente deve accedere al dispositivo usando il proprio account utente Azure AD e registrarsi in Intune. Intune installerà l'estensione di gestione di Intune nel dispositivo se c'è uno script di PowerShell o un'app Win32 destinato all'utente o al dispositivo.
- Le applicazioni Windows possono avere dimensioni massime di 8 GB.

## <a name="prepare-the-win32-app-content-for-upload"></a>Preparare il contenuto delle app Win32 per il caricamento

Prima di poter aggiungere un'app Win32 a Microsoft Intune, è necessario preparare l'app usando lo Strumento di preparazione di contenuti Win32. Lo Strumento di preparazione di contenuti Win32 esegue l'analisi preliminare delle app di Windows classiche (Win32). Lo strumento converte i file di installazione delle applicazioni nel formato *intunewin*. Per altre informazioni e procedure, vedere [Preparare il contenuto dell'app Win32 per il caricamento](apps-win32-prepare.md). 

## <a name="add-assign-and-monitor-a-win32-app"></a>Aggiungere, assegnare e monitorare un'app Win32

Dopo aver [preparato un'app Win32 per il caricamento in Intune](apps-win32-prepare.md) usando lo Strumento di preparazione di contenuti Win32, è possibile aggiungere l'app a Intune. Per altre informazioni e procedure, vedere [Aggiungere, assegnare e monitorare un'app Win32 in Microsoft Intune](apps-win32-add.md).

## <a name="delivery-optimization"></a>Ottimizzazione recapito

I client Windows 10 1709 e versioni successive scaricheranno il contenuto dell'app Win32 di Intune usando un componente di Ottimizzazione recapito nel client Windows 10. Ottimizzazione recapito offre funzionalità peer-to-peer attivate per impostazione predefinita. 

È possibile configurare l'agente di Ottimizzazione recapito per scaricare il contenuto dell'app Win32 in background o in primo piano in base all'assegnazione. È possibile configurare Ottimizzazione recapito con Criteri di gruppo e la configurazione dei dispositivi di Intune. Per altre informazioni, vedere [Ottimizzazione recapito per Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> È anche possibile installare un server Microsoft Connected Cache nei punti di distribuzione di Configuration Manager per memorizzare nella cache il contenuto dell'app Win32 di Intune. Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Installare le app obbligatorie e disponibili nei dispositivi

L'utente riceverà le notifiche di Windows per le installazioni delle app obbligatorie e disponibili. L'immagine seguente illustra un esempio di notifica in cui l'installazione dell'app non risulta completa fino al riavvio del dispositivo. 

![Screenshot delle notifiche di Windows per l'installazione di un'app.](./media/apps-win32-app-management/apps-win32-app-08.png)    

Nell'immagine seguente l'utente riceve una notifica indicante che sono in corso modifiche all'app nel dispositivo.

![Screenshot di invio della notifica relativa alle modifiche in corso per l'app.](./media/apps-win32-app-management/apps-win32-app-09.png)    

L'app Portale aziendale visualizza anche i messaggi aggiuntivi sullo stato dell'installazione dell'app per gli utenti. Alle funzionalità di dipendenza Win32 vengono applicate le condizioni seguenti:
- Installazione dell'app non riuscita. Le dipendenze definite dall'amministratore non sono state soddisfatte.
- L'app è stata installata correttamente, ma è necessario un riavvio.
- È in corso l'installazione dell'app, ma è necessario un riavvio per continuare.

## <a name="set-win32-app-availability-and-notifications"></a>Impostare la disponibilità e le notifiche delle app Win32
È possibile configurare l'ora di inizio e l'ora di scadenza per un'app Win32. All'ora di inizio, l'estensione di gestione di Intune avvia il download del contenuto dell'app e lo memorizza nella cache. L'app viene installata all'ora di scadenza. 

Per le app disponibili, l'ora di inizio determina quando l'app sarà visibile nel Portale aziendale e il contenuto verrà scaricato quando l'utente richiede l'app dal Portale aziendale. È anche possibile abilitare un periodo di tolleranza per il riavvio. 

> [!IMPORTANT]
> L'impostazione **Periodo di tolleranza per il riavvio** nella sezione **Assegnazione** è disponibile solo quando **Comportamento riavvio dispositivo** della sezione **Programma** è impostato su una delle opzioni seguenti:
> - **Determinare il comportamento in base ai codici restituiti**
> - **Intune forzerà il riavvio obbligatorio del dispositivo**

Impostare la disponibilità dell'app in base a una data e un'ora per un'app obbligatoria seguendo questa procedura:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **App** > **Tutte le app**.
3. Nell'elenco **App Windows (Win32)** selezionare un'app. 
4. Nel riquadro dell'app selezionare **Proprietà** > **Modifica** accanto alla sezione **Assegnazioni**. In seguito selezionare **Aggiungi gruppo** sotto il tipo di assegnazione **Richiesto**. 
   
   Si noti che la disponibilità dell'app può essere impostata in base al tipo di assegnazione. Il **Tipo di assegnazione** può essere **Richiesto**, **Disponibile per i dispositivi registrati** o **Disinstalla**.
5. Selezionare un gruppo nel riquadro **Seleziona gruppo** per specificare a quale gruppo di utenti verrà assegnata l'app. 

    > [!NOTE]
    > **Tipo di assegnazione** include le opzioni seguenti:<br>
    > - **Richiesto**: È possibile scegliere **Rendi questa app obbligatoria per tutti gli utenti** e/o **Rendi questa app obbligatoria in tutti i dispositivi**.<br>
    > - **Disponibile per i dispositivi registrati**: È possibile scegliere **Rendi questa app disponibile per tutti gli utenti con dispositivi registrati**.<br>
    > - **Uninstall** (Disinstalla): È possibile scegliere **Disinstalla questa app per tutti gli utenti** e/o **Disinstalla questa app per tutti i dispositivi**.

6. Per modificare le opzioni di **Notifiche per l'utente finale**, selezionare **Mostra tutte le notifiche di tipo avviso popup**.
7. Nel riquadro **Modifica assegnazione** impostare **Notifiche per l'utente finale** su **Mostra tutte le notifiche di tipo avviso popup**. Si noti che è possibile impostare **Notifiche per l'utente finale** su **Mostra tutte le notifiche di tipo avviso popup**, **Mostra le notifiche di tipo avviso popup per i riavvii dei computer** o **Nascondi tutte le notifiche di tipo avviso popup**.
8. Impostare **Disponibilità dell'app** su **Data o ora specifiche** e selezionare la data e l'ora. La data e l'ora specificano quando l'app viene scaricata nel dispositivo degli utenti. 
9. Impostare **Scadenza dell'installazione app** su **Data o ora specifiche** e selezionare la data e l'ora. La data e l'ora specificano quando l'app viene installata nel dispositivo degli utenti. Quando viene effettuata più di un'assegnazione per lo stesso utente o dispositivo, viene selezionata l'ora di scadenza dell'installazione dell'app in base alla prima ora possibile.

10. Selezionare **Attivato** accanto a **Periodo di tolleranza per il riavvio**. Il periodo di tolleranza per il riavvio viene avviato subito dopo il termine dell'installazione dell'app nel dispositivo. Quando è disabilitato, il dispositivo può essere riavviato senza preavviso. 

    È possibile personalizzare le opzioni seguenti:
    
    - **Periodo di tolleranza per il riavvio del dispositivo (minuti)** : Il valore predefinito è 1.440 minuti (24 ore). Il valore massimo è di 2 settimane.
    - **Selezionare quando visualizzare la finestra di dialogo per il conto alla rovescia prima del riavvio (minuti)** : Il valore predefinito è 15 minuti.
    - **Consenti all'utente di posporre la notifica di riavvio**: È possibile scegliere **Sì** o **No**.
        - **Selezionare la durata della posposizione (minuti)** : Il valore predefinito è 240 minuti (4 ore). Il valore della posposizione non può essere maggiore del periodo di tolleranza per il riavvio.

11. Selezionare **Verifica e salva**.

## <a name="notifications-for-win32-apps"></a>Notifiche per app Win32 
Se necessario, è possibile eliminare la visualizzazione delle notifiche utente per ogni assegnazione di app. In Intune selezionare **App** > **Tutte le app** > *selezionare l'app*  > **Assegnazioni** > **Includi gruppi**. 

> [!NOTE]
> Le app Win32 installate dall'estensione di gestione di Intune non verranno disinstallate nei dispositivi di cui è stata annullata la registrazione. Gli amministratori possono usare l'esclusione di assegnazione per non consentire l'installazione di app Win32 in dispositivi BYOD.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sull'aggiunta di app a Intune, vedere [Aggiungere app in Microsoft Intune](apps-add.md).
