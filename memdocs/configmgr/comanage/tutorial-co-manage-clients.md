---
title: Esercitazione&#58; Abilitare la co-gestione per i client esistenti
titleSuffix: Configuration Manager
description: Configurare la co-gestione con Microsoft Intune quando si gestiscono già dispositivi Windows 10 con Configuration Manager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc05ae5a9be6c437fab60f8c4c5a45d61e8c3e65
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694883"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistenti

Con la co-gestione è possibile mantenere i processi consolidati per l'uso di Configuration Manager per la gestione dei PC nell'organizzazione. Allo stesso tempo, è possibile investire nel cloud usando Intune per sicurezza e provisioning moderno.  

In questa esercitazione si configura la co-gestione per i dispositivi Windows 10 che sono già registrati in Configuration Manager. Questa esercitazione inizia con il presupposto che Configuration Manager sia già in uso per la gestione dei dispositivi Windows 10.

Usare questa esercitazione in questi casi:  

- È presente un'istanza locale di Active Directory che è possibile connettere ad Azure Active Directory (Azure AD) in una configurazione di Azure AD ibrido.

  Se non è possibile distribuire un'istanza di Azure Active Directory (AD) ibrido che unisce Active Directory locale con Azure AD, è consigliabile seguire l'esercitazione complementare [Abilitare la co-gestione per nuovi dispositivi Windows 10 basati su Internet](tutorial-co-manage-new-devices.md).
- Sono presenti client di Configuration Manager che si vuole collegare al cloud.

**In questa esercitazione verrà descritto come:**  
> [!div class="checklist"]
> * Esaminare i prerequisiti per Azure e per l'ambiente locale
> * Configurare Azure AD ibrido  
> * Configurare agenti client di Configuration Manager per la registrazione con Azure AD  
> * Configurare Intune per la registrazione automatica dei dispositivi  
> * Abilitare la co-gestione in Configuration Manager  

## <a name="prerequisites"></a>Prerequisiti  

### <a name="azure-services-and-environment"></a>Ambiente e servizi di Azure

- Sottoscrizione di Azure ([versione di valutazione gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Sottoscrizione di Microsoft Intune
  > [!TIP]  
  > Una sottoscrizione di Enterprise Mobility + Security (EMS) include sia Azure Active Directory Premium sia Microsoft Intune. Sottoscrizione di EMS ([versione di valutazione gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Se le configurazioni non sono già presenti nell'ambiente, in questa esercitazione verranno eseguite le operazioni seguenti:

- Configurare [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-select-installation) tra l'istanza di Active Directory locale e il tenant di Azure Active Directory (AD).

> [!TIP]
> Non è più necessario acquistare e assegnare singole licenze di Intune o EMS ai propri utenti. Per altre informazioni, vedere [Domande frequenti su prodotto e licenze](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Infrastruttura locale

- Una [versione supportata](../core/servers/manage/updates.md#supported-versions) della console di Configuration Manager Current Branch
- È necessario impostare l'autorità di gestione di dispositivi mobili (MDM) su Intune.  

### <a name="permissions"></a>Autorizzazioni

In questa esercitazione usare le autorizzazioni seguenti per completare le attività:

- Un account che sia un *amministratore di dominio* nell'infrastruttura locale  
- Un account che sia un *amministratore completo* per *tutti* gli ambiti in Configuration Manager
- Un account che sia *amministratore globale* in Azure Active Directory (Azure AD)
   - Assicurarsi di aver assegnato una licenza di Intune all'account usato per accedere al tenant. In caso contrario, l'accesso avrà esito negativo con il messaggio di errore "Utente non riconosciuto". <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>Configurare Azure AD ibrido

Quando si configura un'istanza di Azure AD ibrido, si sta effettivamente configurando l'integrazione di un'istanza di Active Directory locale con Azure AD usando Azure AD Connect e Active Directory Federation Services (ADFS). Grazie a questa configurazione, i lavoratori potranno accedere facilmente ai sistemi esterni usando le credenziali di Active Directory locali.

> [!IMPORTANT]  
> Questa esercitazione illustra in modo dettagliato un processo essenziale per configurare Azure AD ibrido per un dominio gestito. È consigliabile avere familiarità con il processo e non fare affidamento solo su questa esercitazione come guida per comprendere e distribuire Azure AD ibrido.
>
> Per altre informazioni su Azure AD ibrido, vedere gli articoli seguenti nella documentazione di Azure Active Directory:
>
> - [Pianificare l'implementazione dell'aggiunta ad Azure AD](/azure/active-directory/devices/azureadjoin-plan)
> - [Pianificare l'implementazione dell'aggiunta ad Azure AD ibrido](/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Controllare l'aggiunta dei dispositivi ad Azure AD ibrido](/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Configurare l'aggiunta ad Azure AD ibrido per i domini federati](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Configurare Azure AD Connect

Azure AD ibrido richiede la configurazione di Azure AD Connect per mantenere sincronizzati gli account computer nell'istanza locale di Active Directory (AD) e l'oggetto dispositivo in Azure AD.

A partire dalla versione 1.1.819.0, Azure AD Connect offre una procedura guidata per configurare l'aggiunta ad Azure AD ibrido. L'uso della procedura guidata semplifica il processo di configurazione.  

Per configurare Azure AD Connect, sono necessarie le credenziali di amministratore globale per Azure AD.  

> [!TIP]  
> La procedura seguente non deve essere considerata obbligatoria per la configurazione di Azure AD Connect, ma viene illustrata per semplificare la configurazione della co-gestione tra Intune e Configuration Manager. Per contenuto autorevole su questa procedura e sulle procedure correlate per la configurazione di Azure AD, vedere [Configurare l'aggiunta ad Azure AD ibrido per i domini gestiti](/azure/active-directory/devices/hybrid-azuread-join-managed-domains) nella documentazione di Azure AD.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurare l'aggiunta ad Azure AD ibrido con Azure AD Connect

1. Ottenere e installare la [versione più recente di Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 o versione successiva).  
2. Avviare Azure AD Connect e quindi selezionare **Configura**.
3. Nella pagina **Attività aggiuntive** selezionare **Configura le opzioni del dispositivo** e quindi **Avanti**.
4. Nella pagina **Panoramica** selezionare **Avanti**.
5. Nella pagina **Connessione ad Azure AD** immettere le credenziali di un amministratore globale per Azure AD.
6. Nella pagina **Opzioni dispositivo** selezionare **Configura l'aggiunta ad Azure AD ibrido** e quindi **Avanti**.
7. Nella pagina **Sistemi operativi del dispositivo** selezionare i sistemi operativi usati dai dispositivi nell'ambiente Active Directory e quindi selezionare **Avanti**.  

   È possibile selezionare l'opzione per supportare i dispositivi Windows di livello inferiore aggiunti al dominio, ma tenere presente che la co-gestione dei dispositivi è supportata solo per Windows 10.
8. Nella pagina **Punto di connessione del servizio** per ogni foresta locale per la quale si vuole che Azure AD Connect configuri il punto di connessione del servizio, eseguire questa procedura e quindi selezionare **Avanti**:  
   1. Selezionare la foresta.  
   2. Selezionare il servizio di autenticazione.  Se si ha un dominio federato, selezionare il server AD FS, a meno che l'organizzazione non abbia esclusivamente client Windows 10 e sia stata configurata la sincronizzazione di computer/dispositivi o che l'organizzazione non usi [Seamless SSO](/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Fare clic su **Aggiungi** per immettere le credenziali di amministratore aziendale.  
9. Se si ha un dominio gestito, ignorare questo passaggio.  

   Nella pagina **Configurazione della federazione** immettere le credenziali dell'amministratore AD FS e quindi selezionare **Avanti**.
10. Nella pagina **Pronto per la configurazione** selezionare **Configura**.
11. Nella pagina **La configurazione è stata completata** selezionare **Esci**.

Se si verificano problemi con il completamento dell'aggiunta ad Azure AD ibrido per i dispositivi Windows aggiunti al dominio, vedere [Risolvere i problemi dei dispositivi Windows correnti aggiunti ad Azure AD ibrido](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Configurare le impostazioni client per fare in modo che i client eseguano la registrazione con Azure AD

Usare le impostazioni client per configurare i client di Configuration Manager per la registrazione automatica con Azure AD.  

1. Aprire **Console di Configuration Manager** > **Amministrazione** > **Panoramica** > **Impostazioni client** e quindi modificare i valori in **Impostazioni client predefinite**.  

2. Selezionare **Servizi cloud**.  

3. Nella pagina **Impostazioni predefinite** impostare **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory** su = **Sì**.  

4. Selezionare **OK** per salvare la configurazione.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurare la registrazione automatica dei dispositivi in Intune

Verrà ora configurata la registrazione automatica dei dispositivi con Intune. Con la registrazione automatica, i dispositivi gestiti con Configuration Manager vengono registrati automaticamente con Intune.

La registrazione automatica consente inoltre agli utenti di registrare i propri dispositivi Windows 10 in Intune. I dispositivi vengono registrati quando un utente aggiunge il proprio account aziendale nel dispositivo personale o quando un dispositivo aziendale viene aggiunto ad Azure Active Directory.  

1. Accedere al [portale di Azure](https://portal.azure.com/) e selezionare **Azure Active Directory** > **Servizi Mobility (MDM e MAM)**  > **Microsoft Intune**.  

2. Configurare **Ambito utente MDM**. Specificare una delle opzioni seguenti per configurare quali dispositivi degli utenti sono gestiti da Microsoft Intune e accettare le impostazioni predefinite per i valori di URL.  

   - **In parte**: in **Gruppi** selezionare i gruppi che possono registrare automaticamente i propri dispositivi Windows 10  

   - **Tutti**: tutti gli utenti possono registrare automaticamente i dispositivi Windows 10

   - **Nessuno**: disabilitare la registrazione automatica MDM in Azure.

   > [!IMPORTANT]  
   > Se per un gruppo sono abilitati sia **Ambito utente MAM** che la registrazione automatica di Gestione di dispositivi mobili (**Ambito utente MDM**) solo MAM è abilitato. Per gli utenti in tale gruppo viene aggiunto solo il servizio Gestione di applicazioni mobili (MAM, Mobile Application Management) quando aggiungono alla rete aziendale il proprio dispositivo personale. I dispositivi non vengono registrati automaticamente in MDM.  

3. Selezionare **Salva** per completare la configurazione della registrazione automatica.  

4. Tornare a **Servizi Mobility (MDM e MAM)** e quindi selezionare **Microsoft Intune Enrollment** (Registrazione di Microsoft Intune).  

    > [!NOTE]
    > È possibile che in alcuni tenant queste opzioni non siano disponibili per la configurazione.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** definisce la modalità di configurazione dell'app MDM per Azure AD. **Registrazione di Microsoft Intune** è un'app specifica di Azure AD che viene creata quando si applicano i criteri di autenticazione a più fattori per la registrazione in iOS e Android. Per altre informazioni, vedere [Richiedere l'autenticazione a più fattori per le registrazioni di dispositivi Intune](/intune/enrollment/multi-factor-authentication).

5. Per l'ambito utente MDM selezionare **Tutti** e quindi fare clic su **Salva**.  

## <a name="enable-co-management-in-configuration-manager"></a>Abilitare la co-gestione in Configuration Manager

Dopo aver completato la configurazione di Azure AD ibrido e le configurazioni dei client di Configuration Manager, è possibile abilitare la co-gestione dei dispositivi Windows 10.  

> [!TIP]
> - Quando si abilita la co-gestione, si assegna una raccolta come *gruppo pilota*. Si tratta di un gruppo che contiene un numero ridotto di client per testare le configurazioni di co-gestione. È consigliabile creare una raccolta appropriata prima di avviare la procedura. È quindi possibile selezionare la raccolta senza chiudere la procedura a questo scopo.
> - A partire da Configuration Manager versione 1906, potrebbero essere necessarie più raccolte poiché è possibile assegnare un *gruppo pilota* diverso per ogni carico di lavoro.

### <a name="enable-co-management-starting-in-version-1906"></a>Abilitare la co-gestione a partire dalla versione 1906

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Abilitare la co-gestione nella versione 1902 e nelle versioni precedenti

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Passaggi successivi

- Esaminare lo stato dei dispositivi co-gestiti con il [dashboard di co-gestione](how-to-monitor.md)
- Iniziare a ottenere [valore immediato](quickstarts.md#immediate-value) dalla co-gestione
- Usare l'[accesso condizionale](quickstart-conditional-access.md) e le regole di conformità di Intune per gestire l'accesso utente alle risorse aziendali