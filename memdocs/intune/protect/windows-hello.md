---
title: Integrare Windows Hello for Business in Microsoft Intune
titleSuffix: Microsoft Intune
description: Informazioni su come creare criteri per controllare l'uso di Windows Hello for Business nei dispositivi gestiti durante la registrazione del dispositivo."
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/08/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: 64a76911725e5d596a80ecc67e42f088666017de
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531894"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Integrare Windows Hello for Business in Microsoft Intune  

È possibile integrare Windows Hello for Business (in precedenza Microsoft Passport for Work) in Microsoft Intune, durante la registrazione del dispositivo.

Hello for Business è un metodo di accesso alternativo che usa Active Directory o un account Azure Active Directory per sostituire una password, una smart card o una smart card virtuale. Consente di eseguire l'accesso usando un *movimento dell'utente* invece di una password. Il movimento dell'utente può essere un PIN, un'autenticazione biometrica come Windows Hello o un dispositivo esterno come un lettore di impronte digitali.

Intune si integra con Hello for Business in due modi:

- **A livello di tenant**: È possibile creare criteri Intune in *Registrazione del dispositivo*. Questi criteri hanno come destinazione tutta l'organizzazione, ovvero agiscono a livello di tenant. Supportano la Configurazione guidata di Windows AutoPilot e vengono applicati quando un dispositivo viene registrato.
- **Gruppi discreti**: è possibile distribuire i criteri che gestiscono Windows Hello for Business nei dispositivi registrati in Intune. I tipi di criteri che possono gestire Windows Hello includono i profili di *protezione delle identità* creati in *Configurazione del dispositivo*, varie *baseline di sicurezza* e i profili di *protezione degli account* di sicurezza degli endpoint. Questi tipi di profilo sono destinati a utenti o dispositivi assegnati e vengono applicati durante la sincronizzazione.

Usare questo articolo per creare criteri di Windows Hello for Business predefiniti che abbiano come destinazione tutta l'organizzazione. Per creare un profilo di Identity Protection che viene applicato per selezionare gruppi di utenti e di dispositivi, vedere [Configure an identity protection profile](identity-protection-configure.md) (Configurare un profilo di Identity Protection).  

> [!IMPORTANT]
> Nelle versioni di Windows 10 Desktop e Mobile precedenti all'aggiornamento dell'anniversario era possibile impostare due diversi PIN da usare per l'autenticazione alle risorse:
> - Il **PIN dispositivo** che poteva essere usato per sbloccare il dispositivo e connetterlo alle risorse cloud.
> - Il **PIN di lavoro** che veniva usato per accedere alle risorse di Azure AD nei dispositivi personali dell'utente (BYOD).
> 
> Nell'aggiornamento dell'anniversario questi due PIN sono stati uniti in un unico PIN dispositivo.
> Eventuali criteri di configurazione di Intune impostati per controllare il PIN del dispositivo ed eventuali criteri di Windows Hello for Business configurati, ora impostano questo nuovo valore di PIN.
> Se entrambi i tipi di criteri sono stati impostati per controllare il PIN, i criteri di Windows Hello for Business verranno applicati ai dispositivi Windows 10 Desktop e Mobile.
> Per assicurarsi che i conflitti dei criteri vengano risolti e che i criteri dei PIN vengano applicati correttamente, aggiornare i criteri di Windows Hello for Business in modo che corrispondano alle impostazioni nei criteri di configurazione e chiedere agli utenti di sincronizzare i propri dispositivi nell'app Portale aziendale.



## <a name="create-a-windows-hello-for-business-policy"></a>Creare un criterio di Windows Hello for Business

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Passare a **Dispositivi** >  **Registrazione** > **Registra i dispositivi** > **Registrazione Windows** > **Windows Hello for Business**. Viene visualizzato il riquadro di Windows Hello for Business.

3. Selezionare una delle opzioni seguenti per **Configurare Windows Hello for Business**:

     - **Attivata**. Selezionare questa impostazione se si vuole configurare le impostazioni di Windows Hello for Business.  Quando si seleziona *Abilitato* vengono visualizzate le impostazioni aggiuntive per Windows Hello e possono essere configurate per i dispositivi.

    - **Disabilitato**. Se non si vuole abilitare Windows Hello for Business durante la registrazione del dispositivo, selezionare questa opzione. Quando l'opzione è disabilitata, gli utenti non possono eseguire il provisioning di Windows Hello for Business tranne che nei telefoni cellulari aggiunti ad Azure Active Directory in cui potrebbe essere obbligatorio eseguirlo. Con l'impostazione *Disabilitato* è comunque possibile configurare le impostazioni successive per Windows Hello for Business, anche se questo criterio non abiliterà Windows Hello for Business.

    - **Non configurato**. Selezionare questa impostazione se non si vuole usare Intune per controllare le impostazioni di Windows Hello for Business. Eventuali impostazioni di Windows Hello for Business presenti nei dispositivi Windows 10 non verranno modificate. Tutte le altre impostazioni nel riquadro non sono disponibili.

4. Se si seleziona **Abilitato** nel passaggio precedente, configurare le impostazioni obbligatorie che verranno applicate a tutti i dispositivi Windows 10 e Windows 10 Mobile registrati. Dopo aver configurato queste impostazioni selezionare **Salva**.

   - **Usa un modulo TPM (Trusted Platform Module)** :

     Un chip TPM (Trusted Platform Module) fornisce un livello aggiuntivo di sicurezza dei dati. Scegliere uno dei valori seguenti:

     - **Obbligatorio** (impostazione predefinita). Solo i dispositivi con un modulo TPM accessibile possono eseguire il provisioning di Windows Hello for Business.
     - **Preferito**. I dispositivi provano a usare prima un modulo TPM. Se non è disponibile, possono usare la crittografia software.

   - **Lunghezza minima del PIN** e **Lunghezza massima del PIN**:

     Configura i dispositivi in modo che usino i valori massimo e minimo specificati per la lunghezza del PIN per garantire l'accesso protetto. La lunghezza del PIN predefinita è 6 caratteri, ma è possibile applicare una lunghezza minima di 4 caratteri. La lunghezza massima del PIN è 127 caratteri.

   - **Lettere minuscole nel PIN**, **Lettere maiuscole nel PIN** e **Caratteri speciali nel PIN**.

     Per applicare un PIN più complesso, richiedere l'utilizzo di lettere maiuscole, lettere minuscole e caratteri speciali nel PIN. Per ognuno, selezionare una delle seguenti opzioni:

     - **Consentito**. Gli utenti possono usare il tipo di carattere specificato nel PIN, ma non è obbligatorio.

     - **Obbligatorio**. Gli utenti devono includere almeno uno dei tipi di carattere specificati nel PIN. Ad esempio, di solito si richiede almeno una lettera maiuscola e un carattere speciale.

     - **Non consentito** (impostazione predefinita). Gli utenti non devono usare questi tipi di carattere nel PIN. Se l'impostazione non è configurata, questa è l'impostazione predefinita.

       I caratteri speciali includono: **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

   - **Scadenza PIN (giorni)** :

     Si consiglia di specificare un periodo di scadenza dopo il quale gli utenti finali devono modificare il PIN. L'impostazione predefinita è 41 giorni.

   - **Ricorda cronologia PIN**:

     Limita il riutilizzo di PIN usati in precedenza. Per impostazione predefinita, non è possibile riutilizzare gli ultimi 5 PIN.

   - **Consenti autenticazione biometrica**:

     Abilita l'autenticazione biometrica, ad esempio il riconoscimento facciale o delle impronte digitali, come alternativa a un PIN di Windows Hello for Business. Gli utenti devono comunque configurare un PIN aziendale in caso di errore dell'autenticazione biometrica. Scegliere tra:

     - **Sì**. Windows Hello for Business consente l'autenticazione biometrica.
     - **No**. Windows Hello for Business impedisce l'autenticazione biometrica per tutti i tipi di account.

   - **Usa anti-spoofing avanzato, se disponibile**:

     specifica se le funzionalità di anti-spoofing di Windows Hello vengono usate nei dispositivi che le supportano. Ad esempio, il rilevamento della fotografia di un viso anziché di un viso reale.

     Se impostato su **Sì**, Windows richiede a tutti gli utenti di usare la funzionalità di anti-spoofing per le caratteristiche del viso, se supportata.

   - **Consenti l'accesso tramite telefono**:

     Se questa opzione è impostata su **Sì**, gli utenti possono usare Passport remoto come dispositivo portatile complementare per l'autenticazione del computer desktop. Il computer desktop deve essere aggiunto ad Azure Active Directory e il dispositivo complementare deve essere configurato con un PIN di Windows Hello for Business.

## <a name="windows-holographic-for-business-support"></a>Supporto di Windows Holographic for Business

Windows Holographic for Business supporta le impostazioni di Windows Hello for Business seguenti:

- Usa un modulo TPM (Trusted Platform Module)
- Lunghezza minima del PIN
- Lunghezza massima del PIN
- Lettere minuscole nel PIN
- Lettere maiuscole nel PIN
- Caratteri speciali nel PIN
- Scadenza PIN (giorni)
- Ricorda cronologia PIN

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Windows Hello for Business, vedere [la guida](https://technet.microsoft.com/library/mt589441.aspx) nella documentazione di Windows 10.
