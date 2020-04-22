---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690399"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**. Fare clic su **Configura la co-gestione** nella barra multifunzione per aprire la **procedura guidata di configurazione della co-gestione**.

2. Nella pagina **Sottoscrizione** della procedura guidata fare clic su **Accedi**. Accedere al tenant di Intune e quindi selezionare **Avanti**.  

3. Nella pagina **Abilitazione** scegliere l'impostazione **Registrazione automatica in Intune**: **Pilota** o **Tutti**. Se viene annullata la registrazione di un dispositivo dall'utente, alla successiva valutazione del criterio verrà eseguita di nuovo la registrazione. <!--3330596--> 

    Questa azione abilita la registrazione automatica dei client in Intune per i client di Configuration Manager esistenti. Quando si sceglie **Pilota**, vengono registrati automaticamente in Intune solo i client di Configuration Manager che sono membri della raccolta pilota. Questa opzione consente di abilitare la co-gestione su un subset di client per iniziare a testarla e implementarla mediante un approccio per fasi. 

    > [!Note]  
    > A partire dalla versione 1806, la registrazione automatica non è immediata per tutti i client. Questo comportamento consente una migliore scalabilità della registrazione per gli ambienti di grandi dimensioni. Configuration Manager sceglie in modo casuale la registrazione in base al numero di client. Se l'ambiente include 100.000 client, ad esempio, quando si abilita questa impostazione, la registrazione viene eseguita in più giorni.<!--1358003-->  

4. Per i dispositivi basati su Internet già registrati in Intune, copiare e salvare la riga di comando nella pagina **Enablement** (Abilitazione). È possibile usare questa riga di comando per installare il client di Configuration Manager come app in Intune. Se non si salva la riga di comando a questo punto, sarà possibile esaminare la co-gestione in qualsiasi momento per ottenere la riga di comando.

5. Nella pagina **Carichi di lavoro** per ogni carico di lavoro scegliere il gruppo di dispositivi da spostare per la gestione con Intune. Per altre informazioni, vedere [Carichi di lavoro](../workloads.md).  

    Se si vuole solo abilitare la co-gestione, non è necessario trasferire i carichi di lavoro in questo momento. È possibile trasferirli in seguito. Per altre informazioni, vedere [Come trasferire i carichi di lavoro](../how-to-switch-workloads.md).  

    L'impostazione **Intune pilota** trasferisce il carico di lavoro associato solo per i dispositivi nella raccolta pilota. L'impostazione **Intune** trasferisce il carico di lavoro associato per tutti i dispositivi Windows 10 co-gestiti.  

    > [!Important]
    > Prima di trasferire eventuali carichi di lavoro, assicurarsi di configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.  

6. Nella pagina **Gestione temporanea** configurare le impostazioni seguenti:  

    - **Pilota**: il gruppo pilota contiene una o più raccolte selezionate. Usare il gruppo come parte dell'implementazione a fasi della co-gestione. Iniziare con una raccolta di test di piccole dimensioni e quindi aggiungere più raccolte al gruppo pilota durante l'implementazione della co-gestione per più utenti e dispositivi. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento.  

    - **Produzione**: configurare il **gruppo di esclusione** con una o più raccolte. I dispositivi che sono membri di una raccolta nel gruppo vengono esclusi dalla co-gestione.  

7. Per abilitare la co-gestione, completare la procedura guidata.  
