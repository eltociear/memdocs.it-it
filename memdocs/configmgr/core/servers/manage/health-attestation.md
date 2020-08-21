---
title: Attestazione dell'integrità
titleSuffix: Configuration Manager
description: Informazioni sulla funzionalità di Attestazione dell'integrità del dispositivo visibile nella console di Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d57be201274c347e5dcd492734b2141c64d579b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700011"
---
# <a name="health-attestation-for-configuration-manager"></a>Attestazione dell'integrità per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gli amministratori possono visualizzare l'[attestazione dell'integrità del dispositivo di Windows 10](/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) nella console di Configuration Manager.  L'attestazione dell'integrità dei dispositivi consente all'amministratore di assicurare che nei computer client siano abilitate le seguenti configurazioni attendibili di BIOS, TPM e software di avvio:  

-   Antimalware ad esecuzione anticipata: l'antimalware ad esecuzione anticipata (ELAM) protegge il computer all'avvio e prima dell'inizializzazione dei driver di terze parti. [Come attivare la funzionalità ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker: Crittografia unità BitLocker di Windows è un software che consente di crittografare tutti i dati archiviati nel volume del sistema operativo Windows.  [Come attivare BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Avvio protetto: Avvio protetto è uno standard di sicurezza sviluppato dai membri del settore IT per garantire che i computer vengano avviati usando solo software considerato attendibile dal relativo produttore. [Altre informazioni su Avvio protetto](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Integrità del codice: Integrità del codice è una funzionalità che migliora la sicurezza del sistema operativo convalidando l'integrità di un driver o di un file di sistema ogni volta che viene caricato nella memoria. [Altre informazioni su Integrità del codice](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Questa funzionalità è disponibile per i PC e le risorse locali gestite da Configuration Manager e i dispositivi mobili gestiti con Microsoft Intune. Gli amministratori possono specificare se la creazione di report avviene tramite cloud o infrastruttura locale. Il monitoraggio locale dell'attestazione dell'integrità del dispositivo consente all'amministratore di controllare i PC client senza accesso a Internet.

## <a name="enable-health-attestation"></a>Abilitare l'attestazione di integrità

 **Requisiti:**  

-   Dispositivi client che eseguono Windows 10 versione 1607 o Windows Server 2016 versione 1607 con [Attestazione dell'integrità del dispositivo abilitata](/windows-server/security/device-health-attestation).
-   Dispositivi abilitati per TPM 1.2 o TPM 2.
-   Quando si usa la gestione cloud, comunicazione tra l'agente client di Configuration Manager e il punto di gestione con il servizio di attestazione dell'integrità *has.spserv.microsoft.com* (porta 443) (gestione cloud). In locale, il client deve essere in grado di comunicare con il punto di gestione abilitato per l'attestazione dell'integrità del dispositivo.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Come abilitare la comunicazione del servizio di attestazione dell'integrità nei computer client di Configuration Manager

Seguire questa procedura per abilitare il monitoraggio dell'attestazione dell'integrità per i dispositivi con connessione a Internet.

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Panoramica** > **Impostazioni client**.  Selezionare la scheda delle impostazioni di **Agente computer** .  
2.  Nella finestra di dialogo **Impostazioni predefinite** selezionare **Agente computer** e quindi scorrere fino a **Abilita le comunicazioni con il servizio di attestazione dell'integrità**  
3.  Impostare l'opzione **Abilita le comunicazioni con il servizio di attestazione dell'integrità** su **Sì**e quindi fare clic su **OK**.  
4. Definire come destinazione le raccolte di dispositivi che devono comunicare informazioni sull'integrità.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Come abilitare la comunicazione del servizio di attestazione dell'integrità locale nei computer client di Configuration Manager
Seguire questa procedura per abilitare il monitoraggio dell'attestazione dell'integrità per i dispositivi locali senza connessione a Internet.

A partire da Configuration Manager 1702, è possibile configurare l'URL del servizio locale di attestazione dell'integrità del dispositivo nel punto di gestione, in modo da supportare i dispositivi client che non hanno accesso a Internet.

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Fare clic con il pulsante destro del mouse sul sito primario o secondario con il punto di gestione che supporta i client locali dell'attestazione dell'integrità del dispositivo e scegliere **Configura componenti del sito** > **Punto di gestione**. Viene visualizzata la pagina **Proprietà del componente del punto di gestione**.
3. Nella scheda **Opzioni avanzate** selezionare **Aggiungi** e specificare un URL valido del servizio locale di attestazione dell'integrità del dispositivo. È possibile aggiungere più URL. Se vengono specificati più URL locali, i client ricevono il set completo e scelgono in modo casuale quello da usare.
4.  Nella console di Configuration Manager scegliere **Amministrazione** > **Panoramica** > **Impostazioni client**.  Selezionare la scheda delle impostazioni di **Agente computer** .  
5.  Scorrere in basso fino all'opzione **Abilita le comunicazioni con il servizio di attestazione dell'integrità** e impostarla su **Sì**.
7.  Fare clic sull'opzione **Usare il servizio di attestazione dell'integrità locale** e impostarla su **Sì**.
8. Definire come destinazione le raccolte di dispositivi che devono comunicare informazioni sull'integrità con le impostazioni dell'agente client per abilitare la creazione di report sull'attestazione dell'integrità del dispositivo.

È possibile anche usare le opzioni **Modifica** o **Rimuovi** per modificare o rimuovere gli URL del servizio di attestazione dell'integrità del dispositivo.

> [!NOTE]
> Se l'attestazione dell'integrità del dispositivo è stata usata prima dell'aggiornamento a Configuration Manager 1702, gli URL locali specificati nelle impostazioni dell'agente client vengono inseriti nelle proprietà del punti di gestione durante l'aggiornamento. I client locali continueranno a usare l'URL specificato nelle impostazioni dell'agente client fino a quando non vengono aggiornati. Passeranno quindi a uno degli URL specificati nel punto di gestione.

## <a name="monitor-device-health-attestation"></a>Monitorare l'attestazione dell'integrità del dispositivo

1.  Per visualizzare l'attestazione dell'integrità del dispositivo, nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** , fare clic sul nodo **Sicurezza** e quindi su **Attestazione dell'integrità**.  
2.  Viene visualizzato Attestazione dell'integrità dei dispositivi.  

L'attestazione dell'integrità del dispositivo di Configuration Manager visualizza quanto segue:  

-   **Stato dell'attestazione dell'integrità** : mostra la quota di dispositivi nello stato conforme, non conforme, errore e sconosciuto  
-   **Dispositivi che generano report di attestazione dell'integrità** : mostra la percentuale dei dispositivi che segnalano lo stato di attestazione dell'integrità  
-   **Dispositivi non conformi per tipo di client** : mostra la quota di dispositivi mobili e computer che non sono conformi  
-   **Impostazioni principali per l'attestazione dell'integrità mancante** : mostra il numero di dispositivi in cui manca l'impostazione per l'attestazione dell'integrità, elencati per impostazione