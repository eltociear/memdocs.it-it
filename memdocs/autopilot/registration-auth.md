---
title: Consenso del cliente di Windows Autopilot
description: Informazioni sul modo in cui un partner del provider di servizi cloud (CSP) o un OEM può ottenere l'autorizzazione del cliente per registrare i dispositivi di Windows Autopilot per conto dell'utente.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: db2dc86b4f7cb514f3ceca4d37bf387db31c13f4
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568555"
---
# <a name="windows-autopilot-customer-consent"></a>Consenso del cliente di Windows Autopilot

**Si applica a: Windows 10**

Questo articolo descrive come un partner del provider di servizi cloud (CSP) (Direct fattura, provider indiretto o rivenditore indiretto) o un OEM può ottenere l'autorizzazione del cliente per registrare i dispositivi di Windows Autopilot per conto del cliente.

## <a name="csp-authorization"></a>Autorizzazione CSP

I partner CSP possono ottenere l'autorizzazione del cliente per registrare i dispositivi di Windows Autopilot per conto dell'utente in base alle restrizioni seguenti:

<table>
<tr><td>CSP diretto<td>Ottiene l'autorizzazione diretta dal cliente per la registrazione dei dispositivi.
<tr><td>Provider CSP indiretto<td>Ottiene l'autorizzazione implicita per la registrazione dei dispositivi tramite la relazione con il cliente del partner del rivenditore CSP. I provider CSP indiretti registrano i dispositivi tramite il centro per i partner Microsoft.
<tr><td>Rivenditore CSP indiretto<td>Ottiene l'autorizzazione diretta dal cliente per la registrazione dei dispositivi. Allo stesso tempo, il partner provider CSP indiretto ottiene anche l'autorizzazione, il che significa che il provider indiretto o il rivenditore indiretto può registrare i dispositivi per il cliente. Tuttavia, il rivenditore CSP indiretto deve registrare i dispositivi tramite l'interfaccia utente di MPC (caricamento manuale del file CSV). Il provider CSP indiretto può registrare i dispositivi usando le API MPC.
</table>

### <a name="steps"></a>Passaggi

Affinché un CSP registri i dispositivi di Windows Autopilot per un cliente, il cliente deve prima concedere l'autorizzazione del partner CSP usando il processo seguente:

1. CSP invia il collegamento al cliente che richiede autorizzazione/consenso per registrare/gestire i dispositivi per loro conto. A tale scopo, procedere nel seguente modo:
    1. CSP accede al centro per i partner Microsoft.
    2. Fare clic su **Dashboard** nel menu in alto.
    3. Fare clic su **Customer** nel menu laterale.
    4. Fare clic sul collegamento **Richiedi una relazione Reseller** :

        ![Richiedere una relazione del rivenditore](images/csp1.png)
 
    5. Selezionare la casella di controllo che indica se si desiderano i diritti amministrativi delegati:
 
        ![Diritti delegati](images/csp2.png)

        > [!NOTE]
        > A seconda del partner, potrebbero richiedere autorizzazioni di amministratore delegato (DAP) per la richiesta del consenso. Se possibile, è preferibile usare il processo di DAP-Free più recente (illustrato in questo documento). In caso contrario, è possibile rimuovere facilmente lo stato del DAP dall'interfaccia di amministrazione di Microsoft o dal portale di amministrazione di Microsoft 365: https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    6. Inviare il modello precedente al cliente tramite posta elettronica.

2. Il cliente con privilegi di amministratore globale di Microsoft Admin Center fa clic sul collegamento nel messaggio di posta elettronica. Il collegamento passa alla seguente Microsoft 365 pagina dell'interfaccia di amministrazione:

    ![Screencap di accettazione del contratto e autorizzazione della pagina partner-diritti amministrativi delegati](images/csp3a.png)

    L'immagine precedente è quella che verrà visualizzata dal cliente se hanno richiesto diritti amministrativi delegati (DAP). La pagina indica i ruoli di amministratore richiesti. Se il cliente non ha richiesto diritti amministrativi delegati, viene visualizzata la pagina seguente:

    ![Screencap della pagina Accept Agreement and autorizz partner](images/csp3b.png) 

    > [!NOTE]
    > Un utente senza privilegi di amministratore globale che fa clic sul collegamento visualizzerà un messaggio simile al seguente:

    ![Screencap della pagina di autorizzazione](images/csp4.png)

3. Customer seleziona la casella di controllo **Sì** , seguito dal pulsante **Accept** . L'autorizzazione viene eseguita immediatamente.
4. Per verificare che la richiesta di autorizzazione sia completa, il CSP può controllare l'elenco dei **clienti** nell'account MPC. Se il cliente è presente nell'elenco, la richiesta è stata completata. Ad esempio:

    ![Clienti](images/csp5.png)

## <a name="oem-authorization"></a>Autorizzazione OEM

Ogni OEM dispone di un collegamento univoco da fornire ai rispettivi clienti, che l'OEM può richiedere da Microsoft tramite msoemops@microsoft.com .

1. Il collegamento dei messaggi di posta elettronica OEM al cliente.
2. I privilegi di amministratore globale del cliente con Microsoft Store for business (MSfB) fanno clic sul collegamento nel messaggio di posta elettronica, che li porta direttamente alla pagina MSfB seguente:

    ![Screencap della pagina di invito di Accept partner](images/csp6.png)

    > [!NOTE]
    > Un utente senza privilegi di amministratore globale che fa clic sul collegamento visualizzerà un messaggio simile al seguente:

    ![Screencap della pagina richiesta di autorizzazione MSfB](images/csp7.png)

3. Customer seleziona la casella di controllo **Sì** , seguito dal pulsante **Accept (Accetto** ). L'autorizzazione viene eseguita immediatamente.

    > [!NOTE]
    > Al termine di questo processo, non è possibile che un amministratore rimuova un OEM. Per rimuovere un OEM o revocarne le autorizzazioni, inviare una richiesta a msoemops@microsoft.com

4. L'OEM può usare l'API per la convalida dei dati di invio del dispositivo per verificare che il consenso sia stato completato. Questa API è illustrata nella versione più recente del white paper sulle API, p. 14ff [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) . **Nota**: questo collegamento è accessibile solo ai partner di dispositivi Microsoft. Come illustrato in questo articolo, è consigliabile che i partner OEM eseguano il controllo dell'API per confermare che hanno ricevuto il consenso del cliente prima di provare a registrare i dispositivi. Questo controllo consente di evitare errori durante il processo di registrazione.

    > [!NOTE]
    > Durante il processo di registrazione dell'autorizzazione OEM, all'OEM non vengono concesse autorizzazioni di amministratore delegato.

## <a name="summary"></a>Riepilogo

In questa fase del processo, Microsoft non è più necessario. lo scambio di consenso avviene direttamente tra l'OEM e il cliente. E tutto avviene immediatamente, con la stessa rapidità con cui si fa clic sui pulsanti.
