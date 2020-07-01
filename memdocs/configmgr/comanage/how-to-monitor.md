---
title: Monitorare la co-gestione
titleSuffix: Configuration Manager
description: Usare il dashboard di co-gestione per esaminare le informazioni sui dispositivi con co-gestione.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eab91146ec21bbee888d496012419f47bca4b599
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776974"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Come monitorare la co-gestione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver abilitato la co-gestione, monitorare i dispositivi di co-gestione usando i metodi seguenti:

- [Dashboard di co-gestione](#co-management-dashboard)  

- [Criteri di distribuzione](#deployment-policies)

- [Dati del dispositivo WMI](#wmi-device-data)

## <a name="co-management-dashboard"></a>Dashboard di co-gestione

Questo dashboard consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.<!--1356648,1358980-->

Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Co-gestione**.

![Screenshot del dashboard di co-gestione](media/co-management-dashboard.png)

### <a name="client-os-distribution"></a>Distribuzione del sistema operativo client

Specifica il numero di dispositivi client per ogni versione di sistema operativo. Gli elementi sono raggruppati nei modi seguenti:  

- Windows 7 e 8.x
- Windows 10, versioni precedenti alla 1709  
- Windows 10, versione 1709 e successive  

    > [!Tip]  
    > Windows 10, versione 1709 e successive, è un prerequisito per la co-gestione.  

Passare il mouse su una sezione del grafico per visualizzare la percentuale dei dispositivi nello specifico gruppo di sistemi operativi.

![Riquadro Distribuzione del sistema operativo client](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status"></a>Stato della co-gestione

Un grafico a imbuto che mostra il numero di dispositivi che presentano i seguenti stati del processo di registrazione:
  
- Dispositivi idonei
- Scheduled  
- La registrazione è stata avviata  
- Registrazione eseguita  

![Riquadro Stato della co-gestione (imbuto)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Stato di registrazione della co-gestione

Specifica la suddivisione degli stati dei dispositivi nelle categorie seguenti:

- Esito positivo, aggiunto ad Azure AD ibrido  
- Esito positivo, aggiunto ad Azure AD  
- Registrazione, aggiunta ad Azure AD ibrido  
- Operazione non riuscita, aggiunta ad Azure AD ibrido  
- Operazione non riuscita, aggiunta ad Azure AD  
- Accesso utente in sospeso  

    > [!NOTE]
    > A partire dalla versione 1906, per ridurre il numero di dispositivi in sospeso, un nuovo dispositivo co-gestito viene registrato automaticamente nel servizio Microsoft Intune in base al token di *dispositivo* di Azure AD. Non è necessario attendere che un utente esegua l'accesso al dispositivo per avviare la registrazione automatica. Per supportare questo comportamento, è necessario che il dispositivo esegua Windows 10 versione 1803 o successiva.
    >
    > Se il token di dispositivo non esegue l'operazione, viene eseguito il fallback al comportamento precedente con il token utente. Cercare in **ComanagementHandler.log** la voce seguente: `Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Selezionare uno stato nel riquadro per visualizzare un elenco dei dispositivi con tale stato.  

![Riquadro Stato di registrazione della co-gestione](media/co-management-dashboard/1358980-enrollment-status.png)

### <a name="workload-transition"></a>Transizione del carico di lavoro

Grafico a barre con il numero di dispositivi passati a Microsoft Intune per i carichi di lavoro disponibili.

L'elenco dei carichi di lavoro varia in base alla versione di Configuration Manager. Per altre informazioni, vedere [Carichi di lavoro che è possibile passare a Intune](workloads.md).

Passare il mouse su una sezione del grafico per visualizzare il numero di dispositivi di cui è stata eseguita la transizione per il carico di lavoro.

![Grafico a barre della transizione dei carichi di lavoro](media/co-management-dashboard/Workload-Transition.PNG)

### <a name="enrollment-errors"></a>Errori di registrazione

Questa tabella è un elenco di errori di registrazione dei dispositivi. Questi errori possono provenire dal componente MDM in Windows, dal sistema operativo Windows principale o dal client di Configuration Manager.

Esistono centinaia di possibili errori. La tabella seguente elenca gli errori più comuni.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Errore | Descrizione |
|---------|---------|
| 2147549183 (0x8000FFFF) | La registrazione MDM non è ancora stata configurata in Azure AD oppure l'URL di registrazione non è previsto.<br><br>[Abilitare la registrazione automatica di Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | La licenza dell'utente ha uno stato non valido e blocca la registrazione<br><br>[Assegnare licenze agli utenti](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Quando si tenta di eseguire automaticamente la registrazione in Intune, ma la configurazione di Azure AD non viene applicata completamente. Questo problema dovrebbe essere temporaneo e il dispositivo riproverà dopo un breve periodo. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | L'utente ha annullato l'operazione<br><br>Se la registrazione MDM richiede l'autenticazione a più fattori e l'utente non ha eseguito l'accesso con un secondo fattore supportato, Windows visualizza una notifica di tipo avviso popup con cui invita l'utente a eseguire la registrazione. Se l'utente non risponde alla notifica di tipo avviso popup, si verifica questo errore. Questo problema dovrebbe essere temporaneo e Configuration Manager eseguirà un nuovo tentativo con richiesta all'utente. Gli utenti devono usare l'autenticazione a più fattori quando accedono a Windows. È anche necessario informare gli utenti di questo possibile comportamento e invitarli a intervenire se richiesto. |
| 2149056532 (0x80180014)<br>MENROLL_E_DEVICENOTSUPPORTED | La gestione di dispositivi mobili non è supportata. Controllare le restrizioni dei dispositivi. |
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | La gestione di dispositivi mobili non è supportata. Controllare le restrizioni dei dispositivi. |
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Il server non è riuscito ad autenticare l'utente<br><br> Non è disponibile un token di Azure AD per l'utente. Assicurarsi che l'utente possa eseguire l'autenticazione in Azure AD. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | La registrazione automatica di MDM (gestione dei dispositivi mobili) è supportata solo in Windows RS3 e versioni successive.<br><br>Verificare che il dispositivo soddisfi i [requisiti minimi](overview.md#windows-10) per la co-gestione. |
| 3400073293 | Risposta dell'area di autenticazione account utente ADAL sconosciuta<br><br>Controllare la configurazione di Azure AD e assicurarsi che gli utenti riescano a eseguire l'autenticazione. |
| 3399548929 | È necessario l'accesso dell'utente<br><br>Questo problema dovrebbe essere temporaneo. Si verifica quando l'utente esegue rapidamente la disconnessione prima che avvenga l'attività di registrazione. |
| 3400073236 | Richiesta del token di sicurezza ADAL non riuscita.<br><br>Controllare la configurazione di Azure AD e assicurarsi che gli utenti riescano a eseguire l'autenticazione. |
| 2149122477 | Problema HTTP generico |
| 3400073247 | L'autenticazione Windows integrata in ADAL è supportata solo nel flusso federato<br><br>[Pianificare l'implementazione dell'aggiunta ad Azure Active Directory ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) |
| 3399942148 | Il server o il proxy non è stato trovato.<br><br>Questo problema dovrebbe essere temporaneo e verificarsi quando il client non riesce a comunicare con il cloud. Se persiste, assicurarsi che il client abbia una connessione costante ad Azure. | 
| 2149056532 | Piattaforma o versione specifica non supportata<br><br>Verificare che il dispositivo soddisfi i [requisiti minimi](overview.md#windows-10) per la co-gestione. |
| 2147943568 | Elemento non trovato<br><br>Questo problema dovrebbe essere temporaneo. Se persiste, contattare il supporto tecnico Microsoft. |
| 2192179208 | Risorse di memoria insufficienti per elaborare il comando.<br><br>Questo problema dovrebbe essere temporaneo e risolversi automaticamente al nuovo tentativo del client. |
| 3399614467 | Concessione autorizzazione ADAL non riuscita per questa asserzione<br><br>Controllare la configurazione di Azure AD e assicurarsi che gli utenti riescano a eseguire l'autenticazione. |
| 2149056517 | Errore generico del server di gestione, ad esempio errore di accesso al database<br><br>Questo problema dovrebbe essere temporaneo. Se persiste, contattare il supporto tecnico Microsoft. |
| 2149134055 | Nome Winhttp non risolto<br><br>Il client non riesce a risolvere il nome del servizio. Controllare la configurazione DNS. |
| 2149134050 | Timeout di Internet<br><br>Questo problema dovrebbe essere temporaneo e verificarsi quando il client non riesce a comunicare con il cloud. Se persiste, assicurarsi che il client abbia una connessione costante ad Azure. |

Per altre informazioni, vedere [MDM Registration Error Values](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants) (Valori degli errori di registrazione MDM).

## <a name="deployment-policies"></a>Criteri di distribuzione

vengono creati due criteri nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Un criterio è per il gruppo pilota e uno per la produzione. Questi criteri segnalano solo il numero di dispositivi in cui Configuration Manager ha applicato il criterio. Non tengono conto del numero di dispositivi registrati in Intune, che è un requisito necessario prima che i dispositivi possano essere co-gestiti.

Il criterio di produzione (CoMgmtSettingsProd) è destinato alla raccolta **Tutti i sistemi**. Prevede una condizione di applicabilità che verifica il tipo e la versione del sistema operativo. Se il sistema operativo client o server non è Windows 10, il criterio non viene applicato e non vengono eseguite azioni.

## <a name="wmi-device-data"></a>Dati del dispositivo WMI

Eseguire una query sulla classe WMI **SMS_Client_ComanagementState** nello spazio dei nomi **ROOT\SMS\site_&lt;SITECODE>** nel server del sito. È possibile creare raccolte personalizzate in Configuration Manager che consentono di determinare lo stato della distribuzione della co-gestione. Per altre informazioni sulla creazione delle raccolte personalizzate, vedere [Come creare raccolte in Configuration Manager](../core/clients/manage/collections/create-collections.md).

Nella classe WMI sono disponibili i campi seguenti:

- **MachineId**: ID dispositivo univoco per il client di Configuration Manager

- **MDMEnrolled**: specifica se il dispositivo è registrato nella soluzione MDM

- **Authority**: autorità per cui è registrato il dispositivo

- **ComgmtPolicyPresent**: specifica se nel client sono presenti criteri di co-gestione di Configuration Manager. Se il valore di **MDMEnrolled** è `0`, il dispositivo non è co-gestito, indipendentemente dalla presenza o meno di criteri di co-gestione nel client.

Un dispositivo è co-gestito quando i campi **MDMEnrolled** e **ComgmtPolicyPresent** hanno entrambi il valore `1`.
