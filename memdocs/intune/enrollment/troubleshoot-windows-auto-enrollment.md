---
title: Risolvere i problemi di registrazione automatica di Windows 10 in Intune
titleSuffix: Microsoft Intune
description: Informazioni su come risolvere i problemi di registrazione automatica.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 968aa9b2f7127e9b7f092f36a99b491a75f0b78c
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546867"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Risolvere i problemi di registrazione automatica basata su Criteri di gruppo di Windows 10 in Intune

È possibile usare Criteri di gruppo per attivare la registrazione automatica nel sistema MDM per i dispositivi Active Directory (AD) aggiunti a un dominio. Per altre informazioni, vedere [Registrare un dispositivo Windows 10 automaticamente tramite Criteri di gruppo](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

## <a name="verify-the-configuration"></a>Verificare la configurazione

Prima di avviare il processo di risoluzione dei problemi, è consigliabile verificare che tutti gli elementi siano configurati correttamente. Se il problema non può essere risolto durante la verifica, è possibile procedere con la risoluzione dei problemi controllando alcuni file di log importanti.

- Verificare che all'utente che sta provando a registrare il dispositivo sia assegnata una licenza di Intune valida.

   ![Verificare la licenza di Intune](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Verificare che la registrazione automatica sia abilitata per tutti gli utenti che registreranno i dispositivi in Intune. Per altre informazioni, vedere [Azure AD e Microsoft Intune: Registrazione MDM automatica nel nuovo portale](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal).

   ![Verificare la registrazione automatica](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Verificare che **Ambito utente MDM** sia impostato su **Tutti** per consentire a tutti gli utenti di registrare un dispositivo in Intune.
   - Verificare che **Ambito utente MAM** sia impostato su **Nessuno**. In caso contrario, questa impostazione avrà la precedenza sull'ambito MDM e causerà problemi.
   - Verificare che **URL di individuazione MDM** sia impostato su **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** .

- Verificare che nel dispositivo sia in esecuzione Windows 10, versione 1709 o versione successiva.

- Verificare che i dispositivi siano impostati su **Aggiunto ad Azure AD ibrido**. Questa impostazione indica che i dispositivi sono aggiunti a un dominio e aggiunti ad Azure AD.

   Per verificare le impostazioni, eseguire **dsregcmd /status** dalla riga di comando. Verificare quindi i valori di stato seguenti nell'output:

   - Stato dispositivo
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - Stato SSO

     ```asciidoc
     AzureAdPrt: YES
     ```

   È possibile trovare queste informazioni nell'elenco dei dispositivi aggiunti ad Azure AD:

   ![Elenco dei dispositivi aggiunti ad Azure AD](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- Sia **Microsoft Intune** che  **Registrazione Microsoft Intune** potrebbero essere elencati in  **Servizi Mobility (MDM e MAM)**  nel pannello di Azure AD. Se sono presenti entrambi, assicurarsi di configurare le impostazioni di registrazione automatica in  **Microsoft Intune**.

- Verificare che la seguente impostazione di Criteri di gruppo sia stata distribuita correttamente in tutti i dispositivi che devono essere registrati in Intune:

   **Configurazione computer** > **Criteri** > **Modelli amministrativi** > **Componenti di Windows** > **MDM** > **Abilita la registrazione automatica MDM utilizzando le credenziali di Azure AD predefinite**

   È possibile contattare gli amministratori del dominio per verificare che l'impostazione di Criteri di gruppo sia stata distribuita correttamente.

- Verificare che il dispositivo non sia registrato in Intune usando l'agente PC classico.
- Verificare le impostazioni seguenti in Azure AD e Intune:

   **Nelle impostazioni del dispositivo Azure AD:**

   ![Impostazioni del dispositivo Azure AD](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - L'impostazione **Gli utenti possono aggiungere dispositivi ad Azure AD** è **Tutti**.
   - Il numero di dispositivi che un utente ha in Azure AD non supera la quota **Numero massimo di dispositivi per utente**.
   
   **Nelle restrizioni di registrazione in Intune:**

   - La registrazione dei dispositivi Windows è consentita.

     ![Registrazione consentita di dispositivi Windows](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Risoluzione dei problemi

Se il problema persiste, esaminare i log MDM nel dispositivo nella posizione seguente nel Visualizzatore eventi:

**Registri applicazioni e servizi** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Admin**

Cercare l'ID evento 75 (messaggio dell'evento "Auto MDM Enroll: Succeeded"). Questo evento indica che la registrazione automatica è stata completata.

L'ID evento 75 non viene registrato nelle situazioni seguenti:

- La registrazione ha esito negativo.

  Per verificare l'errore, cercare l'ID evento 76 (messaggio dell'evento: Registrazione MDM automatica: Failed (Unknown Win32 Error code: 0x8018002b) (Registrazione MDM automatica: non riuscita (codice errore Win32 sconosciuto: 0x8018002b)). Questo evento indica una registrazione automatica non riuscita.

  Per la risoluzione di questo errore, vedere [Risoluzione dei problemi di registrazione dei dispositivi Windows in Microsoft Intune](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors).

- La registrazione non è stata attivata. In questo caso, l'ID evento 75 e l'ID evento 76 non vengono registrati.
  
  Il processo di registrazione automatica viene attivato dall'attività "**Schedule created by enrollment client for automatically enrolling in MDM from AAD**" (Pianificazione creata dal client di registrazione per la registrazione automatica in MDM da AAD) disponibile in **Microsoft** > **Windows** > **EnterpriseMgmt** in Utilità di pianificazione.

  ![La registrazione non è stata attivata](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Questa attività viene creata quando l'impostazione di Criteri di gruppo **Abilita la registrazione automatica MDM utilizzando le credenziali di Azure AD predefinite** viene distribuita correttamente nel dispositivo di destinazione. L'attività è pianificata per l'esecuzione ogni 5 minuti per 1 giorno.

  Per verificare che l'attività sia stata avviata, controllare i registri eventi dell'utilità di pianificazione nella posizione seguente nel Visualizzatore eventi:

  **Registri applicazioni e servizi > Microsoft > Windows > TaskScheduler > Operativo**

  Quando l'attività viene attivata nell'utilità di pianificazione, viene registrato l'ID evento 107.

  Quando l'attività viene completata, viene registrato l'ID evento 102. L'evento viene registrato indipendentemente dal fatto che la registrazione automatica abbia esito positivo o negativo.

  > [!NOTE]
  > È possibile usare il log dell'utilità di pianificazione per verificare se la registrazione automatica è attivata. Tuttavia, non è possibile usare il log per determinare se la registrazione automatica è riuscita.

  La situazione seguente può causare il mancato avvio della pianificazione creata dal client per l'attività di registrazione automatica in MDM da AAD:

  - Il dispositivo è già registrato in un'altra soluzione MDM. In questo caso,viene registrato l'ID evento 7016 insieme al codice di errore 2149056522 nel registro eventi **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **TaskScheduler** > **Operativo**.

    Per risolvere il problema, annullare la registrazione del dispositivo da MDM.

  - Esiste un problema relativo a Criteri di gruppo. In questo caso, forzare un aggiornamento delle impostazioni di Criteri di gruppo eseguendo il comando seguente:

    **gpupdate /force**

    Se il problema persiste, eseguire ulteriori operazioni di risoluzione dei problemi in Active Directory.

## <a name="next-steps"></a>Passaggi successivi
[Risolvere i problemi di registrazione dei dispositivi Windows](troubleshoot-windows-enrollment-errors.md)