---
title: Sincronizzare manualmente il dispositivo Windows | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820681"
---
# <a name="sync-your-windows-device-manually"></a>Sincronizzare il dispositivo Windows manualmente

Quando la velocità di installazione di un'app non è quella prevista, avviare una sincronizzazione manuale del dispositivo. Le sincronizzazioni manuali forzano la connessione del dispositivo a Intune per trovare gli aggiornamenti e le comunicazioni più recenti. La velocità di installazione può aumentare dopo avere completato la sincronizzazione del dispositivo.

Intune supporta la sincronizzazione manuale dall'app Portale aziendale, dalla barra delle applicazioni o dal menu Start del desktop e dall'app Impostazioni del dispositivo. La funzionalità dell'app Portale aziendale è supportata nei dispositivi Windows 10 che eseguono Creators Update (1703) o versione successiva. 

Tutti i dispositivi Windows possono essere sincronizzati dall'app Impostazioni del dispositivo, inclusi:

* [Windows 10 Desktop](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Eseguire la sincronizzazione diretta dall'app Portale aziendale per Windows
Completare questi passaggi per sincronizzare manualmente qualsiasi dispositivo Windows 10 che esegue l'aggiornamento Creators Update (versione 1709) o versione successiva.

1. Aprire l'app Portale aziendale nel dispositivo.

2. Selezionare **Impostazioni** > **Sincronizza**.

    ![Screenshot della home page dell'app Portale aziendale, con Impostazioni evidenziato](./media/RS1_homePage_settings_04.png)  
    
    ![Screenshot della pagina Impostazioni dell'app Portale aziendale, con il pulsante Sincronizza evidenziato](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Eseguire la sincronizzazione dalla barra delle applicazioni o dal menu Start del dispositivo   

È anche possibile accedere al controllo della sincronizzazione all'esterno dell'app, dal desktop del dispositivo. È utile se l'app è stata aggiunta direttamente alla barra delle applicazioni o al menu Start e si vuole eseguire rapidamente la sincronizzazione.  

1. Trovare l'icona dell'app Portale aziendale nel menu Start o nella barra delle applicazioni.  
2. Fare clic con il pulsante destro del mouse sull'icona dell'app per visualizzare il menu (detto anche jump list).  

    ![Screenshot della barra delle applicazioni di Windows nel desktop di un dispositivo. L'icona dell'app Portale aziendale è stata selezionata e visualizza un menu con le opzioni "Aggiungi alla barra delle applicazioni", "Chiudi finestra" e "Sincronizza il dispositivo".](./media/sync-device-from-start-menu-1807.png)  

3. Scegliere **Sincronizza il dispositivo**. Viene aperta la pagina **Impostazioni** dell'app Portale aziendale e inizia la sincronizzazione.  

## <a name="sync-from-settings-app"></a>Eseguire la sincronizzazione dall'app Impostazioni 
Completare questi passaggi per sincronizzare manualmente i dispositivi Microsoft HoloLens e Windows 10 desktop dall'app Impostazioni.  

### <a name="windows-10-desktop"></a>Windows 10 Desktop
1. Nel dispositivo selezionare **Start** > **Impostazioni**.

2. Selezionare **Account**.

    ![Scelta di Account nella pagina Impostazioni](./media/win10pc-sync-2-settings-accounts.png)  

3. Esistono più versioni di Windows 10 per desktop. Confrontare la schermata con gli screenshot seguenti per determinare quale procedura seguire. 

    * Se nella schermata è visualizzato **Accedi all'azienda o all'istituto di istruzione**, vedere la procedura illustrata in [Accesso all'azienda o all'istituto di istruzione](#access-work-or-school-steps).

    ![Opzione Accedi all'azienda o all'istituto di istruzione nell'app Impostazioni](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Se nella schermata è visualizzato **Accesso società**, vedere la procedura illustrata in [Accesso società](#work-access-steps).  

    ![Scelta di Accesso società come tipo di account](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Queste istruzioni si applicano ai dispositivi HoloLens che eseguono l'Aggiornamento dell'anniversario di Windows 10 (noto anche come RS1).  

1. Aprire l'app Impostazioni del dispositivo.  

2. Selezionare **Account** > **Accesso società**.  

    ![Screenshot dell'app Impostazioni di HoloLens, con il collegamento Account evidenziato](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Selezionare l'account connesso > **Sincronizza**.  

    ![Screenshot dell'app Impostazioni di HoloLens, con il pulsante Sincronizza evidenziato](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>Procedura di accesso all'azienda o all'istituto di istruzione  

1. Selezionare **Accesso aziendale o dell'istituto di istruzione**.

    ![Screenshot che illustra l'opzione Accedi all'azienda o all'istituto di istruzione](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Selezionare l'account con l'icona a forma di valigetta. Se questo account non è visualizzato, è possibile che la società abbia configurato diversamente le impostazioni. Selezionare invece l'account con il logo Microsoft.

     ![Scegliere il nome dell'account accanto a Sincronia file o al logo Microsoft](./media/win10pc-rs1-sync-info-button.png)

3. Selezionare **Informazioni**. 

4. Selezionare **Sincronizza**. 

#### <a name="work-access-steps"></a>Procedura di accesso società

1. Selezionare **Accesso società**.

    ![Scelta di Accesso società come tipo di account](./media/win10pc-sync-3-work-access.png)

2. In **Registrati per la gestione dispositivi** selezionare il nome della società.

    ![Scelta del nome della società per la gestione dei dispositivi](./media/win10pc-sync-4-tap-com-name.png)

3. Selezionare **Sincronizza**. Il pulsante rimane disabilitato finché non viene completata la sincronizzazione.

    ![Scelta del pulsante Sincronizza](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>Passaggi successivi  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
