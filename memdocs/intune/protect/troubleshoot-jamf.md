---
title: Risoluzione dei problemi relativi all'integrazione di Jamf Pro con Microsoft Intune
titleSuffix: Microsoft Intune
description: Suggerimenti per la risoluzione di alcuni dei problemi più comuni durante l'integrazione di dispositivi Jamf Pro per Mac con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 335841a8642429e36c277673fd8a238d486366c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350616"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Risolvere i problemi di integrazione di Jamf Pro con Microsoft Intune

Questo articolo aiuta gli amministratori di Intune a comprendere e risolvere i problemi relativi all'integrazione di Jamf Pro per macOS con Intune.

> [!TIP]  
> Gran parte delle informazioni presenti in questo articolo erano originariamente contenute in [Risolvere i problemi durante l'integrazione di Jamf con Microsoft Intune](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) sul sito support.microsoft.com.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare la risoluzione dei problemi, raccogliere alcune informazioni di base per chiarire il problema e ridurre il tempo necessario per la ricerca di una soluzione. Ad esempio, quando si verifica un problema relativo all'integrazione di Jamf con Intune, verificare sempre che siano stati soddisfatti tutti i prerequisiti. Prima di iniziare la risoluzione dei problemi, esaminare le considerazioni seguenti:

- Esaminare i prerequisiti riportati in [Integrare Jamf Pro con Intune](conditional-access-integrate-jamf.md#prerequisites).
- Tutti gli utenti devono disporre di licenze per Microsoft Intune e Microsoft AAD Premium P1 
- È necessario disporre di un account utente con autorizzazioni di integrazione per Microsoft Intune nella console di Jamf Pro.
- È necessario disporre di un account utente con autorizzazioni di amministratore globale in Azure.


Quando si esamina l'integrazione di Jamf Pro con Intune, tenere presenti le informazioni seguenti: 
- Qual è il messaggio di errore esatto?
- Dove viene visualizzato il messaggio di errore?
- Quando è iniziato il problema?  L'integrazione di Jamf Pro con Intune ha mai funzionato?
- Quanti utenti sono interessati? Sono interessati tutti gli utenti o solo alcuni?
- Quanti dispositivi sono interessati? Sono interessati tutti i dispositivi o solo alcuni?
 

## <a name="common-problems"></a>Problemi comuni 

Le informazioni seguenti possono essere utili per identificare e risolvere i problemi comuni per i dispositivi dopo aver configurato l'integrazione di Intune e Jamf Pro.  

| Problema   | Altre informazioni                  |
|-----------------|--------------------------|
| **I dispositivi vengono contrassegnati come senza risposta in Jamf Pro**  | [I dispositivi non riescono a eseguire la sincronizzazione con Jamf Pro o con Azure AD](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Nei dispositivi Mac viene richiesto l'accesso tramite il portachiavi all'apertura di un'app**  | [Agli utenti viene richiesto di immettere la password per consentire la registrazione delle app con Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **La registrazione dei dispositivi non riesce**  | Le cause potrebbero essere le seguenti: <br> **-** [***Causa 1***: le autorizzazioni per l'app Jamf Pro in Azure non sono corrette](#cause-1) <br> **-** [***Causa 2***: si è verificato un problema relativo a *Jamf Native macOS Connector* in Azure AD](#cause-2) <br> **-** [***Causa 3***: l'utente non dispone di una licenza valida per Intune o Jamf](#cause-3) <br> **-** [***Causa 4***: l'utente non ha usato Jamf Self Service per avviare l'app Portale aziendale](#cause-4) <br> **-** [***Causa 5***: l'integrazione di Intune è disattivata](#cause-5) <br> **-** [***Causa 6***: il dispositivo è stato registrato in precedenza in Intune o l'utente ha tentato di registrare più volte il dispositivo](#cause-6) <br> **-** [***Causa 7***: JamfAAD richiede l'accesso a una "chiave di Microsoft Workplace Join" dal portachiavi degli utenti](#cause-7) |
|  **Il dispositivo Mac risulta conforme in Intune ma non conforme in Azure** | [Problemi di registrazione del dispositivo](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Vengono visualizzate voci duplicate nella console di Intune per i dispositivi Mac registrati tramite Jamf** | [Più registrazioni per lo stesso dispositivo](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **I criteri di conformità non sono in grado di valutare il dispositivo** | [Il criterio è destinato a gruppi di dispositivi](#compliance-policy-fails-to-evaluate-the-device) |
| **Impossibile recuperare il token di accesso per l'API Microsoft Graph** | Le cause potrebbero essere le seguenti: <br> -[Autorizzazioni per l'app Jamf Pro in Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Licenza scaduta per Jamf o Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Porte non aperte](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>I dispositivi vengono contrassegnati come senza risposta in Jamf Pro  

**Causa**: Di seguito sono riportate le cause più comuni per cui i dispositivi vengono contrassegnati come *senza riposta* da JAMF Pro:

- Il dispositivo non riesce a eseguire la sincronizzazione con Jamf Pro.  
  Jamf Pro prevede che i dispositivi eseguano la sincronizzazione ogni 15 minuti. I dispositivi vengono contrassegnati come senza risposta da Jamf se non riescono a eseguire la sincronizzazione per un periodo di 24 ore.  

- Il dispositivo non riesce a eseguire la sincronizzazione con Azure AD.  
  Con la corretta registrazione in Azure AD, i dispositivi macOS ricevono un token di Azure:
  - Questo token viene aggiornato ogni 12 ore.   
  - Quando l'aggiornamento del token non riesce per più di 24 ore, Jamf Pro contrassegna il dispositivo come senza risposta.  
  - Se il token di Azure scade, agli utenti viene richiesto di accedere ad Azure per ottenere un nuovo token. Un token di aggiornamento per l'accesso ad Azure viene generato ogni sette giorni.

**Risoluzione**  
Dopo che un dispositivo è stato contrassegnato come *senza risposta* da Jamf Pro, l'utente registrato del dispositivo deve eseguire l'accesso per correggere tale stato. Deve essere l'utente che ha aggiunto l'account alla rete aziendale perché ha l'identità di Intune nel portachiavi di accesso.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Nei dispositivi Mac viene richiesto l'accesso tramite il portachiavi all'apertura di un'app  

Dopo aver configurato l'integrazione di Intune e Jamf Pro e aver distribuito i criteri di accesso condizionale, gli utenti dei dispositivi gestiti con Jamf Pro riceveranno una password all'apertura di applicazioni Microsoft Office 365 come Teams, Outlook e altre app che richiedono l'autenticazione di Azure AD. 

Ad esempio, quando si apre Microsoft Teams viene visualizzato un messaggio di richiesta simile a quello nell'esempio seguente:

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**Causa**: Queste richieste vengono generate da Jamf Pro per ogni app applicabile che richiede la registrazione in Azure AD. 

**Risoluzione**   
Quando richiesto, l'utente deve specificare la password del dispositivo per accedere ad Azure AD. Le opzioni includono:
- **Nega**: non eseguire l'accesso e non usare l'app.
- **Consenti**: consentire l'accesso una volta. Alla successiva apertura dell'app, verrà nuovamente richiesto di eseguire l'accesso.
- **Consenti sempre**: le credenziali di accesso vengono memorizzate nella cache per l'applicazione. Alla successiva apertura dell'app, non verrà richiesto di eseguire l'accesso.  

Se si seleziona *Consenti sempre* per un'app, solo tale app viene approvata per l'accesso futuro. Le altre app richiedono l'autenticazione finché non vengono anch'esse impostate come *Consenti sempre*. Le credenziali memorizzate nella cache per un'app non possono essere usate da un'altra app.  

### <a name="devices-fail-to-register"></a>La registrazione dei dispositivi non riesce  

Se i dispositivi Mac non riescono a eseguire la registrazione, le cause possono essere diverse.  

#### <a name="cause-1"></a>Causa 1  

**L'applicazione aziendale Jamf Pro in Azure ha un'autorizzazione errata o ha più di un'autorizzazione**  

  Quando si crea l'app in Azure, è necessario rimuovere tutte le autorizzazioni predefinite dell'API e quindi assegnare a Intune un'unica autorizzazione *update_device_attributes*. 

  **Risoluzione**  
  Esaminare e, se necessario, correggere le autorizzazioni per l'app Jamf creata in Azure AD. Vedere la procedura per [creare un'applicazione per Jamf in Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### <a name="cause-2"></a>Causa 2  

**L'app**Jamf Native macOS Connector** non è stata creata nel tenant di Azure AD o il consenso per il connettore è stato firmato da un account che non dispone dei diritti di amministratore globale**  

  **Risoluzione**  
  Vedere la sezione *Configuring macOS Intune Integration* (Configurazione dell'integrazione di macOS con Intune) in [Integrating with Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) (Integrazione con Microsoft Intune) sul sito docs.jamf.com. 

#### <a name="cause-3"></a>Causa 3

**L'utente non dispone di una licenza valida per Intune o Jamf**  

  La mancanza di una licenza valida può causare l'errore seguente, che indica che la licenza Jamf è scaduta:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Risoluzione**
  - Licenza Jamf: per ottenere una nuova licenza per Jamf, contattare Jamf per assistenza.  
  - Licenza di Intune: assegnare all'utente una licenza valida o contattare Microsoft o il proprio partner per informazioni su come ottenere una licenza corrente.

#### <a name="cause-4"></a>Causa 4  

**L'utente non ha usato *Jamf Self Service* per avviare l'app Portale aziendale**

Per la corretta registrazione di un dispositivo con Intune tramite Jamf, l'utente deve usare Jamf Self Service per aprire Portale aziendale Intune. Se l'utente apre manualmente Portale aziendale, il dispositivo esegue la registrazione senza la connessione a Jamf.  

Per determinare il servizio usato dal dispositivo per la registrazione, esaminare l'app Portale aziendale sul dispositivo. Se il dispositivo è registrato tramite Jamf, si riceverà una notifica che richiede di aprire l'app Self Service per apportare modifiche.

Nell'app Portale aziendale, l'utente potrebbe visualizzare **`Not registered`** e nei log di Portale aziendale potrebbe apparire una voce simile a quella nell'esempio seguente:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Risoluzione**  
Per modificare l'origine di registrazione da Intune a Jamf:
1. [Annullare la registrazione del dispositivo macOS da Intune](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos). Per evitare ulteriori complicazioni per i dispositivi che non vengono rimossi completamente da Intune, vedere [*Causa 6*](#cause-6) in questo elenco di cause.  

2. Nel dispositivo usare Jamf Self Service per aprire l'app Portale aziendale e quindi registrare il dispositivo in Intune. Per questa attività è necessario avere [usato Jamf per distribuire l'app Portale aziendale per macOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) e avere [creato un criterio in Jamf Pro che registra il dispositivo degli utenti con Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. All'apertura del portale, nella prima schermata visualizzata viene richiesto di eseguire l'accesso. Usare l'account aziendale o dell'istituto di istruzione  

4. Il portale aziendale verifica le informazioni sull'account e visualizza gli stati relativi a Registrazione del dispositivo e Conformità del dispositivo. Triangoli gialli evidenziano le azioni da eseguire per proteggere il dispositivo macOS per l'istituto di istruzione o il lavoro. Fare clic su Inizia per iniziare la registrazione.  

5. Se richiesto, digitare le informazioni di accesso del computer.  
     
Potrebbero occorrere alcuni minuti per registrare il dispositivo per la gestione. Durante l'attesa è possibile eseguire altre operazioni sul computer. Al termine della configurazione dell'accesso aziendale viene visualizzato un messaggio relativo al completamento dell'operazione.

#### <a name="cause-5"></a>Causa 5  

**L'integrazione di Intune è disattivata**

Se l'integrazione di Intune è disattivata, gli utenti visualizzano una finestra popup nel Portale aziendale con il messaggio seguente quando tentano di registrare un dispositivo:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

Quando l'integrazione è disattivata, il server Jamf Pro invia un impulso ai server Intune per indicare che l'integrazione è disabilitata. 

**Risoluzione**  
Abilitare nuovamente l'integrazione di Intune in Jamf Pro. Vedere [Configurare l'integrazione di Microsoft Intune in Jamf Pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a><a name="cause-6"></a>Causa 6  

**Il dispositivo è stato registrato in precedenza in Intune o l'utente ha tentato di registrare più volte il dispositivo**

Se si annulla la registrazione di un dispositivo da Jamf ma il dispositivo non è stato rimosso correttamente da Intune o vengono eseguiti diversi tentativi di registrazione, potrebbero essere visualizzate più istanze dello stesso dispositivo nel portale. Questo impedisce la registrazione di Jamf.

**Risoluzione**  
1. Nel dispositivo Mac avviare **Terminale**.
2. Eseguire **sudo JAMF removemdmprofile**.
3. Eseguire **sudo JAMF removeFramework**.
4. Nel server Jamf Pro eliminare il record di inventario del computer.
5. Eliminare il dispositivo da AzureAD.
6. Se presenti, eliminare i file seguenti nel dispositivo:
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Chiave di trasporto della sessione Microsoft (chiavi pubbliche E private)
   - Chiave di Microsoft Workplace Join (chiavi pubbliche E private)
7. Rimuovere dal portachiavi sul dispositivo qualsiasi elemento che faccia riferimento a *Microsoft*, *Intune* o *Portale aziendale*, inclusi i certificati DeviceLogin.microsoft.com. Rimuovere i riferimenti a *JAMF*, ad eccezione della chiave pubblica e privata di Jamf. 
   > [!IMPORTANT]  
   > Rimuovendo la chiave pubblica e privata, la registrazione del dispositivo verrà interrotta.

8. Eliminare le voci seguenti:  
   - Tipo: Password applicazione; Account: com.microsoft.workplacejoin.thumbprint
   - Tipo: Password applicazione; Account: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Tipo: Certificato; Emesso da: MS-Organization-Access
   - Tipo: Preferenza di identità; Nome (URL STS ADFS, se presente): https://adfs\<DNSName>.com/adfs/ls
   - Tipo: Preferenza di identità; Nome: https://enterpriseregistration.windows.net
   - Tipo: Preferenza di identità; Nome: https://enterpriseregistration.windows.net/  
9. Riavviare il dispositivo Mac.
10. Disinstallare Portale aziendale dal dispositivo.
11. Passare a portal.manage.microsoft.com ed eliminare tutte le istanze del dispositivo Mac. Attendere almeno 30 minuti prima di procedere al passaggio successivo.
12. Registrare nuovamente il dispositivo in Jamf Pro.
13. Riaprire Self Service e avviare i criteri di registrazione.


#### <a name="cause-7"></a>Causa 7  

**JamfAAD richiede l'accesso a una "chiave di Microsoft Workplace Join" dal portachiavi degli utenti**

Durante la registrazione, l'utente di un dispositivo macOS riceve la richiesta seguente per consentire l'accesso di JamfAAD a una chiave nel portachiavi: 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the “login” keychain password
```

**Risoluzione**  
Per registrare correttamente il dispositivo con Azure AD, Jamf richiede all'utente di specificare la password dell'account e selezionare **Consenti**.

Questa richiesta è simile alla richiesta riportata nella sezione [Nei dispositivi Mac viene richiesto l'accesso tramite il portachiavi all'apertura di un'app](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app), più indietro in questo articolo.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Il dispositivo Mac risulta conforme in Intune ma non conforme in Azure  

**Causa**: le condizioni seguenti possono causare la visualizzazione di un dispositivo come conforme in Intune, ma come non conforme in Azure:  
- Il dispositivo non è registrato correttamente.  
- Il dispositivo è stato registrato più volte senza la necessaria pulizia.

**Risoluzione**  
Per risolvere questo problema, seguire la risoluzione per la [*causa 6*](#cause-6) nella sezione *La registrazione dei dispositivi non riesce*, più indietro in questo articolo. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Vengono visualizzate voci duplicate nella console di Intune per i dispositivi Mac registrati tramite Jamf  
 
**Causa**: un dispositivo è registrato più volte in Intune (in genere perché è stato registrato nuovamente dopo essere stato rimosso da Intune).  

Quando un dispositivo viene rimosso dall'integrazione di Intune e Jamf Pro, è possibile che vengano mantenuti alcuni dati che possono causare la creazione di voci duplicate durante le registrazioni successive.  

**Risoluzione**  
Per risolvere questo problema, seguire la risoluzione per la [*causa 6*](#cause-6) nella sezione *La registrazione dei dispositivi non riesce*, più indietro in questo articolo. 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>I criteri di conformità non sono in grado di valutare il dispositivo  

**Causa**: L'integrazione di Jamf con Intune non supporta i criteri di conformità che fanno riferimento a gruppi di dispositivi. 

**Risoluzione**  
Modificare i criteri di conformità per i dispositivi macOS da assegnare ai gruppi di utenti. 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Impossibile recuperare il token di accesso per l'API Microsoft Graph

Viene visualizzato l'errore seguente:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

La causa di questo errore può essere una delle seguenti: 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Si è verificato un problema di autorizzazioni con l'applicazione Jamf Pro in Azure

Durante la registrazione dell'app Jamf Pro in Azure, si è verificata una delle condizioni seguenti:  
- L'app ha ricevuto più di un'autorizzazione.
- L'opzione **Concedi consenso amministratore per *\<azienda>*** non è stata selezionata.  

**Risoluzione**  
Vedere la risoluzione relativa alla causa 1 nella sezione [La registrazione dei dispositivi non riesce](#devices-fail-to-register), più indietro in questo articolo.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Una licenza necessaria per l'integrazione di Jamf e Intune è scaduta

**Risoluzione**: Vedere la risoluzione relativa alla causa 3 nella sezione [La registrazione dei dispositivi non riesce](#devices-fail-to-register). 

#### <a name="the-required-ports-arent-open-on-your-network"></a>Le porte richieste non sono aperte nella rete

**Risoluzione**: Esaminare le informazioni relative alle porte di rete in [Prerequisiti](conditional-access-integrate-jamf.md#prerequisites) per l'integrazione di Jamf Pro con Intune.


## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sull'[integrazione di Jamf Pro con Intune](conditional-access-integrate-jamf.md)