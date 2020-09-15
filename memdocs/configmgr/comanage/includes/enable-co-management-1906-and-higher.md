---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: b0c25174873e00cf23dacd2c77208775f1fb1ced
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644126"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

Quando si abilita la co-gestione, è possibile usare il cloud pubblico di Azure, il Cloud Azure US Government o Microsoft Azure Cina (21Vianet) (aggiunto nella versione 2006). Per abilitare la co-gestione a partire da Configuration Manager versione 1906, seguire le istruzioni riportate di seguito:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**. Fare clic su **Configura la co-gestione** nella barra multifunzione per aprire la **procedura guidata di configurazione della co-gestione**.

1. Nella pagina**Onboarding del tenant** della procedura guidata, configurare l'**ambiente Azure** da usare. Scegliere uno degli ambienti seguenti:

   - Cloud pubblico di Azure
   - Cloud Azure US Government<!--4075452-->
   - Cloud Azure Cina (aggiunto nella versione 2006)<!--7133238-->
      - Aggiornare il client Configuration Manager alla versione più recente sui propri dispositivi prima di eseguire l'onboarding in Cloud Azure Cina. <!--7630213--> 

   Quando si seleziona Cloud Azure Cina o Cloud Azure US Government, l'opzione di **caricamento nell'interfaccia di amministrazione di Microsoft Endpoint Manager** del [tenant attach](../../tenant-attach/device-sync-actions.md) è disabilitata.

1. Selezionare **Accedi**. Accedere come amministratore globale di Azure AD e quindi scegliere **Avanti**. È sufficiente accedere una sola volta per poter eseguire questa procedura guidata. Le credenziali non vengono archiviate o riusate altrove.

1. Nella pagina **Enablement** (Abilitazione) scegliere le impostazioni seguenti:

   - **Automatic enrollment into Intune** (Registrazione automatica in Intune): abilita la registrazione automatica dei client in Intune per i client di Configuration Manager esistenti. Questa opzione consente di abilitare la co-gestione su un subset di client per iniziare a testarla e implementarla mediante un approccio per fasi. Se viene annullata la registrazione di un dispositivo dall'utente, alla successiva valutazione del criterio verrà eseguita di nuovo la registrazione. <!--3330596-->

      - **Pilota**: vengono registrati automaticamente in Intune solo i client di Configuration Manager che sono membri della raccolta **Registrazione automatica di Intune**.
      - **Tutti**: abilita la registrazione automatica per tutti i client Windows 10 versione 1709 o successiva.

   - **Registrazione automatica di Intune**: questa raccolta deve contenere tutti i client di cui si vuole eseguire l'onboarding nella co-gestione. Si tratta essenzialmente di un soprainsieme di tutte le altre raccolte di gestione temporanea.

   ![Specificare la raccolta di registrazione automatica di Intune ](../media/3555750-co-management-onboarding-enablement.png)
      
      La registrazione automatica non è immediata per tutti i client. Questo comportamento consente una migliore scalabilità della registrazione per gli ambienti di grandi dimensioni. Configuration Manager sceglie in modo casuale la registrazione in base al numero di client. Se l'ambiente include 100.000 client, ad esempio, quando si abilita questa impostazione, la registrazione viene eseguita in più giorni.<!--1358003-->

      > [!Note]  
      > A partire dalla versione 1906:
      >
      > - Un nuovo dispositivo co-gestito viene ora registrato automaticamente nel servizio Microsoft Intune in base al token di *dispositivo* di Azure Active Directory (Azure AD). Non è necessario attendere che un utente esegua l'accesso al dispositivo per avviare la registrazione automatica. Questa modifica consente di ridurre il numero di dispositivi con lo stato di registrazione *Accesso utente in sospeso*.<!-- 4454491 --> Per supportare questo comportamento, è necessario che il dispositivo esegua Windows 10 versione 1803 o successiva. Per altre informazioni, vedere [Stato di registrazione della co-gestione](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Se sono già presenti dispositivi già registrati nella co-gestione, i nuovi dispositivi vengono ora registrati non appena soddisfano i [prerequisiti](../overview.md#prerequisites).<!--4321130-->

1. Per i dispositivi basati su Internet già registrati in Intune, copiare e salvare la riga di comando nella pagina **Enablement** (Abilitazione). Questa riga di comando verrà usata per installare il client di Configuration Manager come app in Intune per i dispositivi basati su Internet. Se non si salva la riga di comando a questo punto, sarà possibile esaminare la co-gestione in qualsiasi momento per ottenere la riga di comando.

1. Nella pagina **Carichi di lavoro** per ogni carico di lavoro scegliere il gruppo di dispositivi da spostare per la gestione con Intune. Per altre informazioni, vedere [Carichi di lavoro](../workloads.md). Se si vuole solo abilitare la co-gestione, non è necessario trasferire i carichi di lavoro in questo momento. È possibile trasferirli in seguito. Per altre informazioni, vedere [Come trasferire i carichi di lavoro](../how-to-switch-workloads.md).  

    - **Intune pilota**: trasferisce il carico di lavoro associato solo per i dispositivi nelle raccolte pilota che verranno specificati nella pagina **Gestione temporanea**. Ogni carico di lavoro può avere una raccolta pilota diversa.
    - **Intune** - Sposta il carico di lavoro associato per tutti i dispositivi Windows 10 co-gestiti.  

    > [!Important]
    > Prima di trasferire eventuali carichi di lavoro, assicurarsi di configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.  

1. Nella pagina**Gestione temporanea** specificare la raccolta pilota per ogni carico di lavoro impostato su **Intune pilota**.

   ![Configurazione guidata della co-gestione, pagina Gestione temporanea, specifica di raccolte pilota](../media/3555750-co-management-onboarding-staging.png)

1. Per abilitare la co-gestione, completare la procedura guidata.
