---
title: Autenticazione basata su token per CMG
titleSuffix: Configuration Manager
description: Registrare un client nella rete interna per un token univoco o creare un token di registrazione in blocco per i dispositivi basati su Internet.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae92fa2f8e3ee3270de4777fd889bc5fc16a6de4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694139"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticazione basata su token per Cloud Management Gateway

*Si applica a: Configuration Manager (Current Branch)*

<!--5686290-->

Cloud Management Gateway (CMG) supporta molti tipi di client, ma anche con [HTTP avanzato](../../plan-design/hierarchy/enhanced-http.md), questi client richiedono un [certificato di autenticazione client](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Può essere complicato gestire il provisioning di questo requisito del certificato nei client basati su Internet che non si connettono spesso alla rete interna, non possono essere aggiunti ad Azure Active Directory (Azure AD) e non hanno un metodo per installare un certificato emesso da PKI.

A partire dalla versione 2002, Configuration Manager estende il supporto dei dispositivi con i metodi seguenti:

- Registrazione nella rete interna per un token univoco

- Creare un token di registrazione in blocco per i dispositivi basati su Internet

Per sfruttare i vantaggi di questa funzionalità, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Lo scenario completo non funzionerà fin quando anche la versione del client sarà la più recente. Se necessario, assicurarsi di [promuovere la nuova versione del client al livello di produzione](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

Questo token viene gestito dal client di Configuration Manager insieme al punto di gestione, quindi non esiste alcuna dipendenza dalla versione del sistema operativo. Questa funzionalità è disponibile per qualsiasi [versione del sistema operativo client supportata](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Questi metodi supportano solo scenari di gestione incentrati sul dispositivo.
>
> Microsoft consiglia di aggiungere i dispositivi ad Azure AD. I dispositivi basati su Internet possono usare Azure AD per l'autenticazione con Configuration Manager. Sono inoltre supportati scenari di dispositivi e utenti in cui il dispositivo è connesso a Internet o è connesso alla rete interna. Per altre informazioni, vedere [Installare e registrare il client usando l'identità di Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>Registrare nella rete interna

Questo metodo richiede che il client si registri prima nel punto di gestione nella rete interna. La registrazione del client si verifica in genere subito dopo l'installazione. Il punto di gestione fornisce al client un token univoco che conferma che sta usando un certificato autofirmato. Quando il client esegue il roaming su Internet, per comunicare con CMG associa il certificato autofirmato al token emesso dal punto di gestione. Il client rinnova il token una volta al mese ed è valido per 90 giorni.

Il sito abilita questo comportamento per impostazione predefinita.

## <a name="create-a-bulk-registration-token"></a>Creare un token di registrazione in blocco

Se non è possibile installare e registrare i client nella rete interna, creare un token di registrazione in blocco. Usare questo token quando il client viene installato in un dispositivo basato su Internet e viene registrato tramite CMG. Il token di registrazione in blocco ha un periodo di validità breve e non viene archiviato nel client o nel sito. Consente al client di generare un token univoco, che in combinazione con il certificato autofirmato ne consente l'autenticazione per CMG.

1. Accedere al server del sito di livello superiore nella gerarchia con privilegi di amministratore locale.

1. Aprire un prompt dei comandi come amministratore.

1. Eseguire lo strumento dalla cartella `\bin\X64` della directory di installazione di Configuration Manager nel server del sito: `BulkRegistrationTokenTool.exe`. Creare un nuovo token con il parametro `/new`. Ad esempio, `BulkRegistrationTokenTool.exe /new` Per altre informazioni, vedere [Utilizzo dello strumento per la creazione di token di registrazione in blocco](#bulk-registration-token-tool-usage).

1. Copiare il token e salvarlo in una posizione sicura.

1. Installare il client Configuration Manager in un dispositivo basato su Internet. Includere il parametro di installazione client: [ **/regtoken**](about-client-installation-properties.md#regtoken). La riga di comando di esempio seguente include le altre proprietà e i parametri di installazione necessari:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Per altre informazioni su questa riga di comando, vedere [Installare e registrare il client usando l'identità di Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Questo processo è simile, ma non usa le proprietà di Azure AD.

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

Usare con il parametro `/new` per specificare il periodo di validità del token. Specificare un valore intero in minuti. Il valore predefinito è 4.320 (tre giorni).

Esempio: `BulkRegistrationTokenTool.exe /lifetime:4320`

## <a name="see-also"></a>Vedere anche

- [Pianificare il gateway di gestione cloud](../manage/cmg/plan-cloud-management-gateway.md)

- [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](deploy-clients-cmg-azure.md)
