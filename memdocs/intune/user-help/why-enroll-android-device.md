---
title: Perché registrare il dispositivo Android
description: Informazioni sul motivo per cui è importante registrare il dispositivo in Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d22f5aea-7be4-419b-b51b-a522ca037b69
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 9be7d656769f3f937e873792df6eceb65beafdc2
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881391"
---
# <a name="why-enroll-your-android-device"></a>Perché registrare il dispositivo Android  

Datori di lavoro e istituti di istruzione vogliono assicurarsi che i propri utenti si servano di un dispositivo sicuro e attendibile per accedere alle risorse interne. Le app Portale aziendale e Microsoft Intune mantengono il dispositivo Android e i dati protetti durante l'accesso a queste risorse. Garantiscono l'accesso sicuro alle risorse ovunque ci si trovi e indipendentemente dal dispositivo usato. 

Se l'organizzazione richiede l'installazione e la registrazione in una di queste app, è necessario eseguire questa operazione prima di poter accedere alle risorse aziendali dal dispositivo. Questo articolo descrive lo scopo e i vantaggi della registrazione dei dispositivi in queste app.  

## <a name="gets-your-device-managed"></a>Attiva la gestione del dispositivo  
 Portale aziendale e l'app Microsoft Intune registrano il dispositivo in Intune.  Intune è un provider di gestione dei dispositivi mobili che consente all'organizzazione di gestire app e dispositivi mobili tramite criteri di sicurezza e di dispositivo. 

Le app guidano l'utente in ogni passaggio della registrazione e configurano le impostazioni del dispositivo in modo che corrispondano ai criteri dell'organizzazione. Segnalano inoltre eventuali problemi o impostazioni da correggere prima di poter ottenere l'accesso aziendale.  

Esempi di criteri che l'organizzazione potrebbe richiedere:  
* Configurazione di una password o di un PIN
* Limitare l'accesso dopo un determinato numero di tentativi di accesso
* Garantire che il dispositivo non sia jailbroken o rooted
* Installazione delle app necessarie per il lavoro  

## <a name="gives-you-access-to-work-and-school-apps-work-files-and-email"></a>Consente di accedere alle app aziendali e dell'istituto di istruzione, ai file di lavoro e alla posta elettronica  
Durante la registrazione, Portale aziendale e l'app Microsoft Intune richiedono di connettersi al proprio account aziendale o dell'istituto di istruzione.  Dopo aver eseguito l'autenticazione e dopo aver configurato le impostazioni del dispositivo in modo che corrispondano ai criteri dell'organizzazione, si otterrà l'accesso all'account di posta elettronica, alla rete, ai file e alle app dell'organizzazione.  

Le organizzazioni a volte richiedono di installare app di lavoro o di sicurezza, ad esempio Microsoft Office o Mobile Threat Defense. Se queste app sono necessarie o disponibili per l'utente, è possibile trovarle in Portale aziendale o nell'app Microsoft Intune.

## <a name="lets-you-remotely-reset-a-lost-or-stolen-device-if-device-supports-it"></a>Consente di ripristinare in remoto un dispositivo smarrito o rubato (se il dispositivo supporta la procedura)
Se un dispositivo viene smarrito o rubato, è possibile accedere al sito Web o all'app Portale aziendale da un altro dispositivo e ripristinare le impostazioni di fabbrica sul telefono. Questa funzionalità è utile se il dispositivo smarrito contiene dati di lavoro proprietari che non devono essere resi disponibili ad altri. Poiché il dispositivo è registrato nel servizio di gestione, il supporto tecnico dell'azienda o l'amministratore IT può reimpostarlo.  

La funzionalità di reimpostazione non è disponibile nell'app Microsoft Intune.  

## <a name="notifies-you-of-policy-updates-and-requirements"></a>Avvisa della presenza di aggiornamenti dei criteri e dei requisiti
L'app Portale aziendale o Microsoft Intune esegue automaticamente un controllo, ovvero si sincronizza con Intune, ogni otto ore. Se si usa Portale aziendale e si vuole eseguire un controllo più frequente, il supporto tecnico aziendale o l'utente può avviare una sincronizzazione manuale. Durante l'operazione di controllo, l'app:  

* Scarica tutti gli aggiornamenti dei criteri o dell'app resi disponibili dal supporto tecnico dell'azienda.  
* Invia gli aggiornamenti dell'inventario hardware. Questi aggiornamenti non contengono informazioni personali.  
* Invia gli aggiornamenti dell'inventario delle app aziendali. Questi aggiornamenti non contengono informazioni personali.  

Quando il dispositivo non è sincronizzato o non soddisfa più i requisiti, il suo stato risulta *Non conforme*. L'accesso alle risorse di lavoro o dell'istituto di istruzione potrebbe essere sospeso in attesa che il dispositivo soddisfi di nuovo i requisiti. L'app Portale aziendale informa l'utente di questi problemi e dei passaggi da eseguire per correggerli.  


## <a name="permits-company-support-access-to-your-device"></a>Consente di accedere al supporto aziendale per il dispositivo
Quando si registra il dispositivo, al supporto tecnico dell'azienda o all'amministratore IT viene concesso l'accesso al dispositivo per motivi limitati e importanti. Gli utenti possono:  

* Ripristinare le impostazioni predefinite del produttore del dispositivo. Come indicato in precedenza, l'utente può reimpostare personalmente il dispositivo. Tuttavia, se l'utente non riesce ad accedere immediatamente all'app Portale aziendale, l'azienda può reimpostare il dispositivo per conto dell'utente.  

* Rimuovere tutti i dati correlati alla società. L'organizzazione può rimuovere i dati aziendali dal dispositivo se l'utente lascia l'azienda o se il dispositivo diventa non gestito. I dati personali e le impostazioni dell'utente non vengono rimossi e rimangono nel dispositivo.  

* Impostare i requisiti per il dispositivo, ad esempio richiedere una password o un PIN. In questo caso, tramite le notifiche dell'app si verrà informati che il dispositivo non è conforme. Il supporto tecnico aziendale può anche limitare il numero di volte che è possibile immettere una password non corretta nel dispositivo. Troppi tentativi di immettere una password errata potrebbero comportare il blocco del dispositivo.  

* Richiedere di accettare i termini e le condizioni.  

* Disabilitare la fotocamera. Lo scopo di questo criterio è evitare che informazioni proprietarie vengano fotografate, nonché rimuovere elementi di distrazione negli istituti di istruzione. Le scuole potrebbero disabilitare le fotocamere digitali nei dispositivi in aula affinché gli studenti non possano condividere i contenuti delle verifiche.  

* Imporre la crittografia di tutti i dati del dispositivo. Se il dispositivo viene smarrito o rubato, questo criterio consente di proteggere i dati al suo interno. Permette inoltre di proteggere i dati che vengono condivisi tra i dispositivi e le app. 

## <a name="next-steps"></a>Passaggi successivi  

Serve assistenza? Contattare il supporto tecnico aziendale (accedere al [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) per informazioni sul contatto) oppure scrivere al <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble installing the Company Portal app on my Android device&body=Describe the issue you're experiencing here.">team Microsoft Android</a>.
