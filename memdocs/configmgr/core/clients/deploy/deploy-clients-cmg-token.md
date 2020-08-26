---
title: Autenticazione basata su token per CMG
titleSuffix: Configuration Manager
description: Registrare un client nella rete interna per un token univoco o creare un token di registrazione in blocco per i dispositivi basati su Internet.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 55997c9185a221d105aa8ad40bbb14021463d07b
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512700"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticazione basata su token per Cloud Management Gateway

*Si applica a: Configuration Manager (Current Branch)*

<!--5686290-->

Cloud Management Gateway (CMG) supporta molti tipi di client, ma anche con [HTTP avanzato](../../plan-design/hierarchy/enhanced-http.md), questi client richiedono un [certificato di autenticazione client](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Può essere complicato gestire il provisioning di questo requisito del certificato nei client basati su Internet che non si connettono spesso alla rete interna, non possono essere aggiunti ad Azure Active Directory (Azure AD) e non hanno un metodo per installare un certificato emesso da PKI.

Per risolvere questi problemi, a partire dalla versione 2002 Configuration Manager estende il supporto dei dispositivi inviando i propri token di autenticazione. Per sfruttare i vantaggi di questa funzionalità, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Lo scenario completo non funzionerà fin quando anche la versione del client sarà la più recente. Se necessario, assicurarsi di [promuovere la nuova versione del client al livello di produzione](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

 I client si registrano inizialmente per ricevere questi token con uno dei due metodi seguenti:

- Rete interna

- Registrazione in blocco

Questo token viene gestito dal client di Configuration Manager insieme al punto di gestione, quindi non esiste alcuna dipendenza dalla versione del sistema operativo. Questa funzionalità è disponibile per qualsiasi [versione del sistema operativo client supportata](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Questi metodi supportano solo scenari di gestione incentrati sul dispositivo.
>
> Microsoft consiglia di aggiungere i dispositivi ad Azure AD. I dispositivi basati su Internet possono usare Azure AD per l'autenticazione con Configuration Manager. Sono inoltre supportati scenari di dispositivi e utenti in cui il dispositivo è connesso a Internet o è connesso alla rete interna. Per altre informazioni, vedere [Installare e registrare il client usando l'identità di Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="internal-network-registration"></a>Registrazione tramite rete interna

Questo metodo richiede che il client si registri prima nel punto di gestione nella rete interna. La registrazione del client si verifica in genere subito dopo l'installazione. Il punto di gestione fornisce al client un token univoco che conferma che sta usando un certificato autofirmato. Quando il client esegue il roaming su Internet, per comunicare con CMG associa il certificato autofirmato al token emesso dal punto di gestione.

Il sito abilita questo comportamento per impostazione predefinita.

## <a name="bulk-registration-token"></a>Token di registrazione in blocco

Se non è possibile installare e registrare i client nella rete interna, creare un token di registrazione in blocco. Usare questo token quando il client viene installato in un dispositivo basato su Internet e viene registrato tramite CMG. Il token di registrazione in blocco ha un periodo di validità breve e non viene archiviato nel client o nel sito. Consente al client di generare un token univoco, che in combinazione con il certificato autofirmato ne consente l'autenticazione per CMG.

> [!NOTE]
> Non confondere i token di registrazione in blocco con quelli inviati da Configuration Manager ai singoli dispositivi. Il token di registrazione in blocco consente al client di installare e comunicare inizialmente con il sito. Questa comunicazione iniziale è sufficientemente lunga da consentire al sito di inviare al client uno specifico token di autenticazione univoco. Il client usa quindi il proprio token di autenticazione per tutte le comunicazioni con il sito mentre è connesso a Internet. A parte la registrazione iniziale, il client non usa né archivia il token di registrazione in blocco.

Per creare un token di registrazione in blocco da usare durante l'installazione del client nei dispositivi basati su Internet, completare le azioni seguenti:

1. Accedere al server del sito di livello superiore nella gerarchia con privilegi di amministratore locale.

1. Aprire un prompt dei comandi come amministratore.

1. Eseguire lo strumento dalla cartella `\bin\X64` della directory di installazione di Configuration Manager nel server del sito: `BulkRegistrationTokenTool.exe`. Creare un nuovo token con il parametro `/new`. Ad esempio, `BulkRegistrationTokenTool.exe /new` Per altre informazioni, vedere [Utilizzo dello strumento per la creazione di token di registrazione in blocco](#bulk-registration-token-tool-usage).

1. Copiare il token e salvarlo in una posizione sicura.

1. Installare il client Configuration Manager in un dispositivo basato su Internet. Includere il parametro di installazione client: [ **/regtoken**](about-client-installation-properties.md#regtoken). La riga di comando di esempio seguente include le altre proprietà e i parametri di installazione necessari:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Per altre informazioni su questa riga di comando, vedere [Installare e registrare il client usando l'identità di Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Questo processo è simile, ma non usa le proprietà di Azure AD.

Per verificare, cercare nel file di log seguente una voce simile:<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

Per risolvere i problemi di installazione, esaminare `%WinDir%\ccmsetup\logs\ccmsetup.log` nel client. Dopo l'installazione, esaminare `%WinDir%\ccm\logs\ClientIDManagerStartup.log`.

Esaminare i log seguenti nel server:

- [Log CMG](../../plan-design/hierarchy/log-files.md#cloud-management-gateway)
- Punto di gestione
  - CCM_STS.log
  - MP_RegistrationManager.log
  - ClientAuth.log

### <a name="known-issues"></a>Problemi noti

Non è possibile creare un token di registrazione in blocco in un sito con un server del sito in modalità passiva.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Utilizzo dello strumento per la creazione di token di registrazione in blocco

Eseguire lo strumento `BulkRegistrationTokenTool.exe` nella cartella `\bin\X64` della directory di installazione di Configuration Manager nel server del sito. Accedere al server del sito ed eseguirlo come amministratore. Sono supportati i parametri della riga di comando seguenti:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Visualizza queste informazioni sull'utilizzo.

Esempio: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

Creare un nuovo token di registrazione in blocco.

Esempio: `BulkRegistrationTokenTool.exe /new`

Questo strumento fornisce le informazioni seguenti:
  
- GUID usato dal sito per tenere traccia dei token emessi
- Periodo di validità del token, che per impostazione predefinita è di tre giorni.
- Token di registrazione in blocco.

Il token non viene archiviato nel client o nel sito. Assicurarsi di copiare il token dal prompt dei comandi e archiviarlo in una posizione sicura.

#### <a name="lifetime"></a>/lifetime

Usare con il parametro `/new` per specificare il periodo di validità del token. Specificare un valore intero in minuti. Il valore predefinito è 4.320 (tre giorni). Il valore massimo è 10.080 (sette giorni).

Esempio: `BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>Gestione di token di registrazione in blocco

È possibile visualizzare i token di registrazione in blocco creati in precedenza e la loro durata nella console di Configuration Manager e bloccarne l'utilizzo, se necessario. Il database del sito, tuttavia, non archivia i token di registrazione in blocco.

### <a name="review-a-bulk-registration-token"></a>Rivedere un token di registrazione in blocco

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**.

2. Espandere **Sicurezza** e selezionare il nodo **Certificati**. La console elenca tutti i certificati correlati al sito e i token di registrazione in blocco nel riquadro dei dettagli.

3. Selezionare il token di registrazione in blocco da rivedere.

È possibile applicare un filtro o eseguire l'ordinamento in base alla colonna **Tipo**. Identificare token di registrazione in blocco specifici in base al GUID. Quando si crea un token di registrazione in blocco, lo strumento visualizza il GUID.

### <a name="block-a-bulk-registration-token"></a>Bloccare un token di registrazione in blocco

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**.

2. Espandere **Sicurezza**, selezionare il nodo **Certificati** e selezionare il token di registrazione in blocco da bloccare.

3. Nella scheda **Home** della barra multifunzione o nel menu di scelta rapida selezionare **Blocca**. Per sbloccare i token di registrazione in blocco precedentemente bloccati, selezionare l'azione **Sblocca**.

## <a name="token-renewal"></a>Rinnovo del token

Una volta al mese il client rinnova il proprio token univoco inviato da Configuration Manager, che è valido per 90 giorni. Non è necessario che un client si connetta alla rete interna per rinnovare il token. Purché il token sia ancora valido, la connessione al sito con CMG è sufficiente. Se il token non viene rinnovato entro 90 giorni, il client deve connettersi direttamente a un punto di gestione in una rete interna per riceverne uno nuovo.

Non è possibile rinnovare un token di registrazione in blocco. Dopo la scadenza di un token di registrazione in blocco, generarne uno nuovo per la registrazione dei dispositivi basati su Internet tramite CMG.

## <a name="see-also"></a>Vedere anche

- [Pianificare il gateway di gestione cloud](../manage/cmg/plan-cloud-management-gateway.md)

- [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](deploy-clients-cmg-azure.md)
