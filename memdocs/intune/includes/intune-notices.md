---
title: includere il file
description: Includere file
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438720"
---
Questi avvisi forniscono importanti informazioni utili per prepararsi per le modifiche e le funzionalità di Intune future.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Fine del supporto per Windows 10 Mobile in Microsoft Intune<!--3544938-->
Il supporto Mainstream Microsoft per Windows 10 Mobile è terminato nel dicembre 2019. Come indicato nella presente informativa sul supporto, gli utenti di Windows 10 Mobile non saranno più idonei a ricevere nuovi aggiornamenti della sicurezza, hotfix non di sicurezza, opzioni di supporto tecnico gratuite o aggiornamenti del contenuto tecnico online da Microsoft. A seconda del supporto del sistema operativo per dispositivi mobili, Microsoft Intune terminerà il supporto del Portale aziendale per l'app Windows 10 Mobile e del sistema operativo Windows 10 Mobile l'11 maggio 2020.

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?
Se nell'organizzazione sono distribuiti dispositivi Windows 10 Mobile, da ora all'11 maggio 2020 è possibile registrare nuovi dispositivi, aggiungere o rimuovere criteri e app o aggiornare le impostazioni di gestione. Dopo l'11 maggio, le nuove registrazioni verranno interrotte e infine verrà rimossa la gestione di Windows 10 Mobile dall'interfaccia utente di Intune. I dispositivi non verificheranno più il servizio Intune e i dati dei dispositivi e dei criteri verranno eliminati.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica
È possibile controllare i report di Intune per vedere quali dispositivi o utenti potrebbero essere interessati. Passare a **Dispositivi** > **Tutti i dispositivi** e filtrare in base al sistema operativo. È possibile aggiungere altre colonne per facilitare l'identificazione degli utenti dell'organizzazione che hanno dispositivi che eseguono Windows 10 Mobile. Richiedere agli utenti finali di aggiornare i dispositivi o di interrompere l'uso dei dispositivi per l'accesso aziendale.


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>È stata aggiornata l'informativa di supporto per l'app per dispositivi mobili 'Adobe Acrobat Reader per Intune'<!--5746776-->
Nel documento MC188653 della fine di agosto è stato comunicato che l'app per dispositivi mobili Adobe Acrobat Reader per Intune stava avvicinandosi alla scadenza dell'1 dicembre 2019 e che Adobe prevedeva di includere il supporto dei criteri di protezione delle app di Intune all'interno dell'app Acrobat Reader principale. Da allora, abbiamo ricevuto il feedback dei clienti che richiedeva più tempo per continuare a consentire agli amministratori IT di impostare l'app come destinazione e agli utenti finali di iniziare a usare Adobe Acrobat Reader per Intune. Considerato l'utilizzo elevato di Adobe Acrobat Reader per Intune nei dispositivi degli utenti finali e la sua importanza negli scenari aziendali, vogliamo assicurarci che qualsiasi esperienza soddisfi le esigenze di protezione delle app dell'organizzazione. 

Sebbene sia ancora consigliabile impostare come destinazione l'app per dispositivi mobili Acrobat Reader generale nei criteri poiché l'app per dispositivi mobili Acrobat Reader supporta i criteri di protezione delle app e include l'SDK Intune integrato, l'app Adobe Acrobat Reader per Intune continuerà a essere supportata fino al 31 marzo 2020. 

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?
Si riceve questo messaggio poiché risulta che uno o più criteri dell'organizzazione includono come destinazione l'applicazione Adobe Acrobat Reader per Intune e/o si potrebbe aver ricevuto la comunicazione EOL precedente. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica
Informare gli utenti finali e il supporto tecnico di questa modifica. È possibile usare la [funzionalità delle informazioni sul supporto del Portale aziendale](../apps/company-portal-app.md#support-information) per stabilire un canale per le domande correlate a Intune.

#### <a name="additional-information"></a>Informazioni aggiuntive
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>Azione: Usare Microsoft Edge per l'esperienza protetta del browser di Intune<!--5728447-->
Come descritto nel corso dell'ultimo anno, Microsoft Edge per dispositivi mobili supporta la stessa gamma di funzionalità di gestione supportata da Managed Browser, ma garantisce un'esperienza utente molto migliore. Per lasciare spazio alle esperienze consolidate offerte da Microsoft Edge, Intune Managed Browser verrà ritirato. A partire dal 27 gennaio 2020 Intune non supporterà più Intune Managed Browser.  

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica? 
A partire dal 1 febbraio 2020 Intune Managed Browser non sarà più disponibile in Google Play Store o nell'App Store iOS. Dopo tale data sarà ancora possibile indirizzare i nuovi criteri di protezione delle app a Intune Managed Browser, ma i nuovi utenti non potranno più scaricare l'app Intune Managed Browser. Inoltre in iOS le nuove clip Web che vengono distribuite a dispositivi registrati in MDM verranno aperte in Microsoft Edge anziché in Intune Managed Browser.  

Il 31 marzo 2020 Intune Managed Browser verrà rimosso dalla console di Azure. Di conseguenza non sarà più possibile creare nuovi criteri per Intune Managed Browser. I criteri di Intune Managed Browser già implementati non subiranno variazioni. Intune Managed Browser verrà visualizzato nella console come applicazione line-of-business senza icone e i criteri esistenti continueranno ad apparire come associati all'app. Verrà anche rimossa l'opzione per reindirizzare il contenuto Web a Intune Managed Browser nel contesto della sezione Protezione dei dati dei criteri di protezione delle app.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica 
Per garantire una transizione ottimale da Intune Managed Browser a Microsoft Edge è consigliabile adottare le seguenti misure con il necessario anticipo: 

1. Impostare Microsoft Edge per iOS e Android come destinazione per i criteri di protezione delle app (detti anche MAM) e le impostazioni di configurazione delle app. Per riusare i criteri di Intune Managed Browser per Microsoft Edge, impostare anche Microsoft Edge come destinazione dei criteri esistenti.  
2. Verificare che per tutte le app dell'ambiente protette tramite MAM il criterio di protezione "Limita il trasferimento di contenuto Web con altre app" sia impostato su "Browser gestiti da criteri". 
3. Verificare che per tutte le app protette tramite MAM l'impostazione di configurazione dell'app gestita "com.microsoft.intune.useEdge" sia impostata su True. A partire dal mese prossimo con la versione 1911 sarà possibile completare i passaggi 2 e 3 configurando semplicemente "Limita il trasferimento di contenuto Web con altre app" in modo che "Microsoft Edge" sia selezionato nella sezione Protezione dei dati dei criteri di protezione delle app. 

Il supporto delle clip Web in iOS e Android sarà disponibile a breve. Dopo il rilascio del supporto, sarà necessario reimpostare la destinazione delle clip Web preesistenti, per garantire che vengano aperte in Microsoft Edge anziché in Managed Browser. 

#### <a name="additional-information"></a>Informazioni aggiuntive
Per altre informazioni vedere la documentazione relativa all'[uso di Microsoft Edge con i criteri di protezione delle app](../apps/manage-microsoft-edge.md) o visualizzare il [post del blog sul supporto](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269).

### <a name="end-of-support-for-legacy-pc-management"></a>Termine del supporto per la gestione dei PC legacy

La gestione dei PC legacy non sarà più supportata a partire dal 15 ottobre 2020. Aggiornare i dispositivi a Windows 10 e registrarli nuovamente come dispositivi MDM perché continuino a essere gestiti da Intune.

[Altre informazioni](https://go.microsoft.com/fwlink/?linkid=2107122)


