---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1709 per Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3cefbbb9824266fd5fa057a7625332e85ec0ab32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705119"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1709 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1709. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemi noti di questa versione Technical Preview:**
- **L'aggiornamento alla versione 1709 di Technical Preview ha esito negativo se il server del sito è in modalità passiva**. Quando si eseguono le versioni 1706, 1707 o 1708 di Technical Preview ed è presente un [server del sito primario in modalità passiva](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima di poter aggiornare il sito alla versione 1709 di Technical Preview. Sarà possibile reinstallare il server del sito in modalità passiva quando nel sito sarà in esecuzione la versione 1709.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Esperienza del profilo VPN migliorata nella console di Configuration Manager
<!-- 1313282 -->
In questa versione sono state aggiornate la procedura guidata di creazione del profilo VPN e le pagine delle proprietà per visualizzare le impostazioni appropriate per la piattaforma selezionata. In particolare:

- Ogni piattaforma ha un proprio flusso di lavoro, vale a dire che i nuovi profili VPN contengono solo l'impostazione supportata dalla piattaforma.
- Le pagine **Piattaforme supportate** vengono ora visualizzate dopo la pagina **Generale**.  È ora possibile scegliere la piattaforma prima di impostare i valori delle proprietà.
- Quando la piattaforma è impostata su **Android**, **Android for Work** o **Windows Phone 8.1**, la pagina **Piattaforme supportate** non è necessaria e non viene visualizzata.
- Il flusso di lavoro basato su client di Configuration Manager è stato combinato con i flussi di lavoro di Windows 10 basato su client dei dispositivi mobili ibridi (MDM), visto che supportano le stesse impostazioni.
- Ogni flusso di lavoro di piattaforma include solo le impostazioni appropriate per il flusso di lavoro.  Ad esempio, il flusso di lavoro Android contiene le impostazioni appropriate per Android; le impostazioni appropriate per iOS e Windows 10 Mobile non vengono più visualizzate nel flusso di lavoro Android.
- Per i dispositivi Windows 8.1, le impostazioni gestite da Configuration Manager sono contrassegnate in modo chiaro.
- La pagina VPN automatico è obsoleta ed è stata rimossa.

Queste modifiche vengono applicate ai nuovi profili VPN.  

Per ridurre al minimo i rischi relativi alla compatibilità, i profili VPN esistenti non vengono modificati.  Quando viene modificato un profilo esistente, le impostazioni vengono visualizzate come quando è stato creato il profilo.  

### <a name="try-it-out"></a>Verifica

Creare un nuovo profilo VPN usando il processo consueto. Si noti che la prima pagina di opzioni della procedura guidata di creazione del profilo VPN è stata modificata.

1. Passare a **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Accesso risorse aziendali** > **Profilo VPN** e quindi scegliere **Crea profilo VPN**.
2. Immettere un nome nella pagina **Generale** e scegliere una delle opzioni seguenti in **Specificare il tipo di profilo VPN da creare**:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS e macOS  
    - Android  
    - Android for Work  

3. Se si sceglie **Windows 8.1**, sono disponibili anche le opzioni **Create new profile** (Crea nuovo profilo) o **Importa da file**.
4. Completare la procedura guidata per la creazione del profilo.

Quando si selezionano piattaforme diverse, si noti che vengono visualizzate solo le impostazioni rilevanti per la piattaforma selezionata.

## <a name="co-management-for-windows-10-devices"></a>Co-gestione per dispositivi Windows 10    
<!-- 1350871 -->
Molti clienti vogliono gestire i dispositivi Windows 10 nello stesso modo in cui gestiscono i dispositivi mobili usando una soluzione semplice, a costi contenuti e basata su cloud. Tuttavia, la transizione dalla gestione tradizionale a una gestione moderna può essere complessa. A partire da Windows 10, versione 1607 (nota anche come Aggiornamento dell'anniversario) è possibile aggiungere un dispositivo Windows 10 ad Active Directory (AD) locale e ad Azure AD basata sul cloud AD allo stesso tempo (Azure AD ibrida). La co-gestione sfrutta questo miglioramento e consente di gestire i dispositivi Windows 10 contemporaneamente usando sia Configuration Manager che Intune. È una soluzione che costituisce un ponte tra la gestione tradizionale e quella moderna e che consente di eseguire la transizione mediante un approccio per fasi. 

### <a name="prerequisites"></a>Prerequisiti
Prima di poter abilitare la co-gestione, è necessario soddisfare i prerequisiti seguenti. Esistono prerequisiti generali e prerequisiti diversi per client di Configuration Manager esistenti e per dispositivi non client.

### <a name="known-issues"></a>Problemi noti
Dopo aver creato criteri di co-gestione, non è possibile modificarli. Per modificare i criteri, eliminarli e ricrearli con le impostazioni necessarie. 

#### <a name="general-prerequisites"></a>Prerequisiti generali
Di seguito sono elencati i prerequisiti generali per abilitare la co-gestione:  

- Technical Preview per Configuration Manager versione 1709
- Azure AD 
- Licenza di EMS o Intune per tutti gli utenti
- Sottoscrizione a Intune &#40; Autorità MDM impostata su **Intune**&#41;

   > [!Note]  
   > Se si ha un ambiente MDM ibrido, ovvero Intune integrato con Configuration Manager, non è possibile abilitare la co-gestione.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Prerequisiti aggiuntivi per client di Configuration Manager esistenti
- Windows 10, versione 1709 (Fall Creators Update) e versioni successive
- Dispositivo ibrido aggiunto ad Active Directory e Azure AD

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Prerequisiti aggiuntivi per i nuovi dispositivi Windows 10
- Windows 10, versione 1709 (Fall Creators Update) e versioni successive
- [Cloud Management Gateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) in Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Carichi di lavoro che è possibile passare a Intune
Dopo aver abilitato la co-gestione, Configuration Manager continua a gestire tutti i carichi di lavoro. Quando si è pronti, impostare Intune perché inizi a gestire i carichi di lavoro disponibili. In questa versione Intune può gestire i carichi di lavoro seguenti.   

#### <a name="compliance-policies"></a>Criteri di conformità
I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. È anche possibile usare tali criteri per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale.

#### <a name="windows-update-for-business-policies"></a>Criteri di Windows Update per le aziende
I criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende. Per altre informazioni, vedere [Configurare i criteri di rinvio di Windows Update per le aziende](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Azioni remote disponibili in Intune in Azure per dispositivi co-gestiti
Quando un dispositivo Windows 10 è abilitato per la co-gestione, sono disponibili le azioni remote seguenti da Intune in Azure:  
- [Ripristino impostazioni predefinite](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Cancellazione selettiva](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminazione di dispositivi](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Riavvio di dispositivi](https://docs.microsoft.com/intune/device-restart)
- [Installazione da zero](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Preparare Intune per la co-gestione
Prima di passare i carichi di lavoro da Configuration Manager a Intune, creare i profili e i criteri necessari in Intune per assicurarsi che i dispositivi continuino a essere protetti.
È possibile creare oggetti in Intune in base agli oggetti presenti in Configuration Manager. In alternativa, se la strategia corrente si basa sulla gestione legacy o tradizionale, rivedere i criteri e i profili necessari per la gestione moderna. Usare le risorse seguenti per creare criteri e profili.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Criteri di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Profili di configurazione del dispositivo](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Panoramica dell'architettura per la co-gestione
Il diagramma seguente offre una panoramica dell'architettura della co-gestione e illustra come questa si inserisce nelle infrastrutture di Configuration Manager e Intune esistenti.

![Diagramma architettura co-gestione](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Scenari per abilitare la co-gestione  
È possibile abilitare la co-gestione sia per i dispositivi Windows 10 registrati in Microsoft Intune sia per i client esistenti di Configuration Manager in Windows 10. In entrambi gli scenari i dispositivi Windows 10 vengono gestiti congiuntamente da Configuration Manager e da Intune, nonché aggiunti ad Active Directory e Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Dispositivi registrati in Intune  
Quando i dispositivi Windows 10 sono registrati in Intune, è possibile installare il client di Configuration Manager nei dispositivi, mediante un argomento della riga di comando specifico, per preparare i client alla co-gestione. In seguito è possibile abilitare la co-gestione dalla console di Configuration Manager per avviare lo spostamento di carichi di lavoro specifici in Intune per alcuni dispositivi Windows 10.  

Per i dispositivi Windows 10 non ancora registrati in Intune, è possibile usare la registrazione automatica in Azure per registrare i dispositivi. Per i nuovi dispositivi Windows 10, è possibile usare Windows AutoPilot per avviare la configurazione guidata che include la registrazione automatica dei dispositivi in Intune.  

#### <a name="configuration-manager-clients"></a>Client di Configuration Manager
Quando si hanno dispositivi Windows 10 che sono client di Configuration Manager, è possibile registrare tali dispositivi e abilitare la co-gestione dalla console di Configuration Manager. Configuration Manager attiva la registrazione automatica in Intune in base alle informazioni del tenant di Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Preparare i dispositivi Windows 10 per la co-gestione
È possibile abilitare la co-gestione nei dispositivi Windows 10 aggiunti ad Active Directory e Azure AD e registrati in Intune e che siano client di Configuration Manager. Per i nuovi dispositivi Windows 10 e per i dispositivi già registrati in Intune, installare il client di Configuration Manager prima di attivare la co-gestione. Per i dispositivi Windows 10 che sono già client di Configuration Manager, è possibile registrare i dispositivi con Intune e abilitare la co-gestione dalla console di Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Riga di comando per installare il client di Configuration Manager
Creare un'app in Intune per i dispositivi Windows 10 che non sono già client di Configuration Manager. Quando si crea l'app nelle sezioni successive, usare la riga di comando seguente:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL dell'endpoint autorizzazione reciproca di Cloud Management Gateway*&#62;/ CCMHOSTNAME=&#60;*URL dell'endpoint autorizzazione reciproca di Cloud Management Gateway*&#62; SMSSiteCode=&#60;*Codice sito*&#62; SMSMP=https:&#47;/&#60;*FQDN del punto di gestione*&#62; AADTENANTID=&#60;*ID tenant AAD*&#62; AADTENANTNAME=&#60;*Nome tenant*&#62; AADCLIENTAPPID=&#60;*AppID del server per l'integrazione di AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ID risorsa*&#62;"

Ad esempio, se sono stati restituiti i valori seguenti:

- **URL dell'endpoint di autenticazione reciproca di Cloud Management Gateway**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Usare il valore **MutualAuthPath** nella visualizzazione di SQL **vProxy_Roles** per il valore dell'**URL dell'endpoint di autenticazione reciproca di Cloud Management Gateway**.

- **FQDN del punto di gestione** : sccmmp.corp.contoso.com    
- **Codice sito**: PS1    
- **ID tenant di Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome del tenant di Azure AD**: contoso    
- **ID app client Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI ID risorsa AAD**: ConfigMgrServer    

  > [!Note]    
  > Usare il valore **IdentifierUri** trovato nella visualizzazione SQL **vSMS_AAD_Application_Ex** per il valore **URI ID risorsa AAD**.

A tale scopo, usare la riga di comando seguente:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
>È possibile trovare i parametri della riga di comando per il sito tramite la procedura seguente:     
> 1. Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).  
> 2. Nella scheda Home nel gruppo di gestione scegliere **Configura la co-gestione** per aprire il caricamento guidato della co-gestione.    
> 3. Nella pagina della sottoscrizione fare clic su **Accedi**, accedere al tenant di Intune e fare clic su **Avanti**.    
> 4. Nella pagina di attivazione fare clic su **Copia** nella sezione **Devices enrolled in Intune** (Dispositivi registrati in Intune) per copiare la riga di comando negli Appunti e quindi salvare la riga di comando da usare nella procedura per creare l'app.  
> 5. Per uscire dalla procedura guidata, fare clic su **Annulla**.

#### <a name="new-windows-10-devices"></a>Nuovi dispositivi Windows 10
Per i nuovi dispositivi Windows 10, è possibile usare il servizio AutoPilot per la configurazione guidata, che include l'aggiunta del dispositivo ad AD e Azure AD, nonché la registrazione del dispositivo in Intune. In seguito, creare un'app in Intune per distribuire il client di Configuration Manager.  
1. Abilitare AutoPilot per i nuovi dispositivi Windows 10. Per informazioni dettagliate, vedere [Panoramica di Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configurare la registrazione automatica in Azure AD perché registri automaticamente i dispositivi in Intune. Per informazioni dettagliate, vedere  [Registrazione di dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).
3. Creare un'app in Intune con il pacchetto client di Configuration Manager e distribuire l'app ai dispositivi Windows 10 per i quali si vuole abilitare la co-gestione. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet usando Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivi Windows 10 non registrati in Intune o che non hanno il client di Configuration Manager
Per i dispositivi Windows 10 che non sono registrati in Intune o non hanno il client di Configuration Manager, è possibile usare la registrazione automatica in modo che vengano registrati in Intune. In seguito, creare un'app in Intune per distribuire il client di Configuration Manager.
1. Configurare la registrazione automatica in Azure AD perché registri automaticamente i dispositivi in Intune. Per informazioni dettagliate, vedere  [Registrazione di dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).  
2. Creare un'app in Intune con il pacchetto client di Configuration Manager e distribuire l'app ai dispositivi Windows 10 per i quali si vuole abilitare la co-gestione. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet usando Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivi Windows 10 registrati in Intune
Per i dispositivi Windows 10 che sono già registrati in Intune, creare un'app in Intune per distribuire il client di Configuration Manager. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet usando Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Passare i carichi di lavoro di Configuration Manager a Intune
Nella sezione precedente i dispositivi Windows 10 sono stati preparati per la co-gestione. I dispositivi sono stati aggiunti ad AD e Azure AD, sono stati registrati in Intune e hanno il client di Configuration Manager. È probabile che vi siano ancora dispositivi Windows 10 aggiunti ad AD e che hanno il client di Configuration Manager, ma che non sono stati aggiunti ad Azure AD o registrati in Intune. Di seguito sono riportati i passaggi per abilitare la co-gestione, preparare il resto dei dispositivi Windows 10, ovvero quelli che hanno il client di Configuration Manager ma che non sono registrati in Intune, e avviare il passaggio di specifici carichi di lavoro di Configuration Manager a Intune.

1. Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).    
2. Nella scheda Home nel gruppo di gestione scegliere **Configura la co-gestione** per aprire il caricamento guidato della co-gestione.    
3. Nella pagina della sottoscrizione fare clic su **Accedi**, accedere al tenant di Intune e fare clic su **Avanti**.   
4. Nella pagina della gestione temporanea configurare le impostazioni seguenti e fare clic su **Avanti**:
    - **Gruppo pilota**: il gruppo pilota contiene una o più raccolte selezionate. Usare il gruppo come parte dell'implementazione a fasi della co-gestione. È possibile iniziare con una raccolta di test di piccole dimensioni e quindi aggiungere più raccolte al gruppo pilota durante l'implementazione della co-gestione per più utenti e dispositivi. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento dalle proprietà della co-gestione.
    - **Production**: quando si seleziona questa impostazione, tutti i dispositivi Windows 10 supportati vengono abilitati per la co-gestione. Configurare **Exclusion group** (Gruppo di esclusione) con una o più raccolte. I dispositivi che sono membri di una raccolta nel gruppo vengono esclusi dalla co-gestione. 
5. Nella pagina di attivazione scegliere **Pilota** o **Tutti**, a seconda delle impostazioni configurate nella pagina della gestione temporanea, per abilitare la registrazione automatica in Intune e fare clic su **Avanti**. Quando si sceglie **Pilota**, vengono registrati automaticamente in Intune solo i client di Configuration Manager che sono membri del gruppo pilota. Ciò consente di abilitare la co-gestione inizialmente su un subset di client per testarla e implementarla mediante un approccio per fasi. 
6. Nella pagina dei carichi di lavoro scegliere se passare i carichi di lavoro di Configuration Manager a Intune e fare clic su **Avanti**. Usare i dispositivi di scorrimento per selezionare se passare il carico di lavoro per il gruppo di pilota o per tutti i client Windows 10, a seconda delle impostazioni configurate nella pagina della gestione temporanea. 
7. Per abilitare la co-gestione, completare la procedura guidata.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Vedere anche
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md). 
