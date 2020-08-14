---
title: Abilitare Windows Defender | Microsoft Docs
description: Informazioni su come abilitare Windows Defender per accedere alle risorse aziendali.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110699"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Abilitare Windows Defender per accedere alle risorse aziendali

Le organizzazioni vogliono garantire che i dispositivi che accedono alle risorse siano protetti, quindi potrebbero richiedere l'uso di [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx). Windows Defender è un software antivirus incluso in Windows che può aiutare a proteggere il dispositivo da virus e altri malware e minacce. 

Questo articolo descrive come aggiornare le impostazioni del dispositivo per soddisfare i requisiti antivirus dell'organizzazione e risolvere i problemi di accesso. 

## <a name="turn-on-windows-defender"></a>Abilitare Windows Defender
Seguire questa procedura per attivare Windows Defender nel dispositivo. 

1. Selezionare il menu **Start**.
2. Nella barra di ricerca digitare **criteri di gruppo**. Selezionare quindi **Modifica Criteri di gruppo** tra i risultati elencati. Verrà aperto l'Editor Criteri di gruppo locali.
4. Selezionare **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Windows Defender Antivirus**. 
5. Scorrere fino alla fine dell'elenco e selezionare **Disabilita Windows Defender Antivirus**.  
6. Selezionare **Disabilitato** o **Non configurato**. Potrebbe risultare non intuitivo selezionare queste opzioni perché i nomi indicano che è in corso la disattivazione di Windows Defender. Queste opzioni assicurano in realtà che venga attivato. 
7. Selezionare **Applica** > **OK**.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Attivare la protezione in tempo reale e fornita dal cloud

Seguire questa procedura per attivare la protezione in tempo reale e fornita dal cloud. Insieme, queste funzionalità antivirus proteggono da spyware e possono fornire correzioni per i problemi relativi al malware tramite il cloud. 

1. Selezionare il menu **Start**.
2. Nella barra di ricerca digitare **sicurezza di Windows**. Selezionare il risultato corrispondente. 
3. Selezionare **Protezione da virus e minacce**.
4. In **Impostazioni di Protezione da virus e minacce** selezionare **Gestisci impostazioni**.
5. Selezionare ogni commutatore in **Protezione in tempo reale** e **Protezione fornita dal cloud** per attivare queste opzioni. 

Se queste opzioni non sono visualizzate sullo schermo, potrebbero essere nascoste. Seguire questa procedura per renderle visibili.  

1. Selezionare il menu **Start**.  
2. Nella barra di ricerca digitare **criteri di gruppo**. Selezionare quindi **Modifica Criteri di gruppo** tra i risultati elencati. Verrà aperto l'Editor Criteri di gruppo locali.
3. Selezionare **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Sicurezza di Windows** > **Protezione da virus e minacce**.
4. Selezionare **Nascondi l'area Protezione da virus e minacce**.
5. Selezionare **Disabilitato** > **Applica** > **OK**.  

## <a name="update-your-antivirus-definitions"></a>Aggiornare le definizioni di antivirus
Seguire questa procedura per aggiornare le definizioni di antivirus.  
1. Selezionare il menu **Start**.
2. Nella barra di ricerca digitare **sicurezza di Windows**. Selezionare il risultato corrispondente. 
3. Selezionare **Protezione da virus e minacce**.
4. In **Virus & threat protection updates** (Aggiornamenti di protezione da virus e minacce) selezionare **Verifica disponibilità di aggiornamenti**. Se questa opzione non è visualizzata sullo schermo, completare il primo set di passaggi in [Attivare la protezione in tempo reale](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection). Controllare di nuovo se sono disponibili aggiornamenti. 

## <a name="next-steps"></a>Passaggi successivi  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).
