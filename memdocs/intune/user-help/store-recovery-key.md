---
title: Archiviare una chiave di ripristino in Intune tramite il sito Web Portale aziendale
description: Caricare e archiviare la chiave di ripristino del dispositivo dal sito Web Portale aziendale.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f0a674753ff23fca509bd21e6b52101104a6803f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910792"
---
# <a name="store-your-personal-filevault-key"></a>Archiviare la chiave di FileVault personale 

Archiviare una chiave di FileVault per il dispositivo macOS crittografato personalmente. Oltre a soddisfare i requisiti di crittografia, l'archiviazione della chiave in Intune consente di: 

* Recuperare o ruotare rapidamente la chiave da qualsiasi dispositivo in modo semplice e rapido. 
* Chiedere assistenza al personale di supporto se è necessario recuperare o ruotare la chiave e non è possibile accedere alle app o al sito Web per eseguire autonomamente questa operazione.


## <a name="retrieve-or-rotate-the-key"></a>Recuperare o ruotare la chiave

Se si rimane bloccati fuori dal dispositivo, è possibile recuperare la chiave dalle posizioni seguenti:
   
- sito Web del portale aziendale
- App Portale aziendale per iOS/iPadOS 
- App Portale aziendale per Android
- App Intune
 
 Il personale di supporto IT con accesso come amministratore a Intune può ruotare la chiave di ripristino personale se il dispositivo viene bloccato. Questi utenti possono anche visualizzare le chiavi, ma solo quelle che appartengono ai dispositivi di proprietà aziendale. Il personale di supporto IT non può visualizzare le chiavi di ripristino che appartengono a dispositivi personali.   


## <a name="do-i-need-to-store-my-key"></a>È necessario archiviare la chiave?  
Un addetto al supporto IT darà indicazioni se è necessario caricare una chiave di ripristino personale. Si potrebbe ricevere una notifica a questo scopo dalle app Portale aziendale per iOS/iPadOS o Android, se questo è il modo usato comunemente dal reparto IT dell'organizzazione per comunicare con gli utenti. 

È consigliabile caricare una chiave di ripristino solo se si rientra in una delle categorie seguenti:
* L'utente ha crittografato il dispositivo prima di registrarlo nell'organizzazione. 
* L'utente ha crittografato manualmente il dispositivo tramite le preferenze di sistema macOS.   

A seconda dei criteri dell'organizzazione, è possibile che l'accesso alle risorse aziendali nel dispositivo venga bloccato fino a quando non si carica la chiave.  

## <a name="upload-personal-recovery-key"></a>Caricare la chiave di ripristino personale 
Seguire questa procedura per salvare la chiave di FileVault personale per il dispositivo Mac crittografato.  


1. Passare al [sito Web Portale aziendale](https://portal.manage.microsoft.com) e accedere con l'account aziendale o dell'istituto di istruzione. 
2. Selezionare il dispositivo crittografato.
3. Selezionare **Store recovery key** (Archivia chiave di ripristino).  
4. Immettere la chiave di FileVault alfanumerica a 24 caratteri.  
5. Immettere di nuovo la chiave. Selezionare **Salva**.
6. Portale aziendale tenterà di verificare, ruotare e salvare la chiave di ripristino personale. Non è necessaria alcuna azione aggiuntiva dopo aver salvato la chiave. Se si esce dal sito Web prima di completare il caricamento, sarà possibile visualizzarne lo stato nella pagina dei dettagli del dispositivo al successivo accesso.  

Per altre informazioni sui messaggi che possono essere visualizzati durante questo processo, vedere [Messaggi del Portale aziendale](store-recovery-key.md#company-portal-messages).  

## <a name="company-portal-messages"></a>Messaggi del portale aziendale

|Messaggio  |Significato  |
|---------|---------|
|Le chiavi devono corrispondere. Controllare le chiavi e riprovare.     | Questo messaggio viene visualizzato sotto la casella **Conferma chiave di ripristino** per indicare che le chiavi non corrispondono. Digitare nuovamente le chiavi in entrambi i campi, quindi riprovare a salvarle.        |
|Non è stato possibile aggiornare la chiave di ripristino del dispositivo.| Viene visualizzato come notifica di tipo avviso popup nella parte superiore dello schermo per indicare che Portale aziendale non è riuscito a archiviare una chiave di ripristino. Per altri dettagli, selezionare il dispositivo crittografato. Leggere quindi il messaggio nella parte superiore della pagina per i passaggi successivi. |
|Non è stato possibile caricare la chiave di ripristino. Verificare di aver immesso la chiave corretta e riprovare. Se il problema persiste, provare a ruotare manualmente la chiave. Toccare per altre informazioni.     | Viene visualizzato nella pagina dei dettagli del dispositivo e potrebbe avere due significati: In primo luogo, Portale aziendale non è riuscito a ruotare e salvare la chiave perché la chiave immessa non è corretta. Verificare di disporre della chiave corretta e riprovare. La seconda possibilità è che il dispositivo non sia stato sincronizzato con l'organizzazione per un po' di tempo. Per sincronizzare gli aggiornamenti più recenti dall'organizzazione, selezionare il dispositivo > **Stato** > **Verifica l'accesso**. Riprovare quindi ad archiviare la chiave di ripristino. Infine, se il problema persiste, potrebbe significare che l'organizzazione non ha abilitato FileVault. Contattare il personale di supporto IT e segnalare che il dispositivo è stato sincronizzato, ma non è ancora possibile archiviare la chiave di FileVault.         |
|La chiave di ripristino è stata aggiornata. Se il dispositivo risulta bloccato ed è necessario recuperare la chiave di ripristino, accedere al Portale aziendale e selezionare **Ottieni la chiave di ripristino**.    | Viene visualizzato nella pagina dei dettagli del dispositivo. La chiave salvata è stata ruotata correttamente e la nuova chiave di ripristino personale è archiviata.    |



## <a name="it-pro-support"></a>Supporto per professionisti IT

Se si è un responsabile del supporto IT e si vuole configurare e gestire la crittografia FileVault per i dispositivi Mac nell'organizzazione, vedere [Usare la crittografia del disco FileVault per macOS con Intune](../protect/encrypt-devices-filevault.md).  

## <a name="next-steps"></a>Passaggi successivi

È sempre possibile recuperare la chiave dal sito Web Portale aziendale, dall'app di Intune e dalle app Portale aziendale per iOS e Android e usarla per accedere al dispositivo Mac. Per informazioni su come recuperare la chiave di ripristino, vedere [Ottenere la chiave di ripristino](get-recovery-key-cpweb.md).

Scoprire le altre operazioni che è possibile eseguire nel sito Web Portale aziendale. Per un elenco delle azioni, vedere [Uso del sito Web Portale aziendale Intune](using-the-intune-company-portal-website.md).  

Serve ancora assistenza? Contattare il responsabile del supporto IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).