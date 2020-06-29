---
title: Quali sono le informazioni visibili per l'azienda quando si registra il dispositivo?
description: Informazioni visibili e non visibili per il personale IT sul dispositivo gestito.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: 740d9b68a0101e04e6bf690d09ecce7eaff4509e
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107310"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Quali sono le informazioni visibili per l'organizzazione quando si registra il dispositivo?

L'organizzazione non può vedere le informazioni personali di un utente che registra un dispositivo con Microsoft Intune. Quando si registra un dispositivo, si concede all'organizzazione l'autorizzazione per visualizzare determinati tipi di informazioni nel dispositivo, ad esempio il modello di dispositivo e il numero di serie. L'organizzazione usa queste informazioni per la protezione dei dati aziendali nel dispositivo.

**Informazioni che l'organizzazione non può mai visualizzare:**

- Cronologia delle chiamate e delle esplorazioni Web
- Posta elettronica e messaggi di testo
- Contatti
- Calendario
- Password
- Immagini, incluse quelle nell'app Foto o nel rullino della fotocamera
- File

**Informazioni che l'organizzazione può sempre visualizzare:**

- Modello del dispositivo, ad esempio Google Pixel
- Produttore del dispositivo, ad esempio Microsoft
- Sistema operativo e versione, ad esempio iOS 12.0.1
- Inventario delle app e nomi delle app, ad esempio Microsoft Word. nei dispositivi personali l'organizzazione può visualizzare solo l'inventario delle app gestite. Nei dispositivi di proprietà dell'azienda l'organizzazione può visualizzare l'inventario di tutte le app.
- Proprietario del dispositivo
- Nome del dispositivo
- Numero di serie del dispositivo
- IMEI

 > [!NOTE]
 > Per i dispositivi Android Enterprise completamente gestiti e dedicati, non sarà possibile visualizzare l'inventario di tutte le app.
 
 > [!NOTE]
 > Un'app è considerata **app gestita** quando viene installata in uno dei modi seguenti:
 > 1. Un utente può installarla dall'app Portale aziendale dopo che è stata pubblicata come **disponibile** da un amministratore di Intune.
 > 2. L'app viene pubblicata come **obbligatoria** da un amministratore di Intune ed è installata nel dispositivo. 
 >
 > Se si è un amministratore IT o un utente del supporto tecnico dell'organizzazione e si vogliono ottenere altre informazioni sulla gestione delle app in Intune, vedere [Informazioni sulle funzionalità delle app non gestite, delle app gestite e delle app MAM](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164).
    
**Informazioni che l'organizzazione potrebbe visualizzare:**

- Numero di telefono: per i dispositivi di proprietà dell'azienda, può essere visualizzato il numero di telefono completo. Per i dispositivi di proprietà personale, l'organizzazione può visualizzare solo le ultime quattro cifre del numero di telefono. È possibile visualizzare il tipo di proprietà di un singolo dispositivo nella pagina **Dettagli dispositivo** corrispondente.
- Spazio di archiviazione del dispositivo: se non è possibile installare un'app necessaria, l'organizzazione può esaminare lo spazio di archiviazione del dispositivo per determinare se lo spazio non è sufficiente.  
- Percorso: Per i dispositivi di proprietà dell'azienda, l'organizzazione può vedere la posizione di un dispositivo perso. Per i dispositivi di proprietà personale, l'organizzazione non può mai visualizzare la posizione del dispositivo, a meno che non stia tentando di trovare un dispositivo iOS con supervisione smarrito. Consultare la [documentazione di Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) per altre informazioni sui dispositivi supervisionati.  
- Dettagli dell'inventario delle app: se la propria organizzazione usa Mobile Threat Defense, può visualizzare dettagli aggiuntivi sulle app presenti nel dispositivo iOS. Altre informazioni su [Mobile Threat Defense](set-up-mobile-threat-defense.md). In caso contrario, per i dispositivi di proprietà personale l'organizzazione può visualizzare solo l'inventario delle app gestite. Nei dispositivi di proprietà dell'azienda l'organizzazione può visualizzare l'inventario di tutte le app.
- Informazioni sulla rete: per il supporto tecnico dell'organizzazione possono essere disponibili alcune informazioni sulle connessioni di rete per dispositivi Android. Se l'organizzazione esigesse, ad esempio, che i dispositivi rimangano all'interno di un determinato edificio, il dispositivo potrebbe identificare la rete a cui è connesso. 
