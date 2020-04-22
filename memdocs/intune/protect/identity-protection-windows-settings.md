---
title: Impostazioni di Windows Hello for Business in Microsoft Intune - Azure | Microsoft Docs
description: Visualizzare un elenco di tutte le impostazioni per PIN, biometria e anti-spoofing in un profilo di protezione delle identità per usare e configurare Windows Hello for Business nei dispositivi Windows 10 in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/20/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: b4581ba6bdc8b5be41d5cf567c631ffaad40d418
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79351968"
---
# <a name="windows-10-device-settings-to-enable-windows-hello-for-business-in-intune"></a>Impostazioni dei dispositivi Windows 10 per abilitare Windows Hello for Business in Intune

Questo articolo elenca e descrive le impostazioni di Windows Hello for Business che è possibile controllare nei dispositivi Windows 10 in Intune. Come amministratore di Intune, è possibile configurare e assegnare queste impostazioni ai dispositivi Windows 10 come parte della soluzione di gestione di dispositivi mobili (MDM). 

È possibile trovare altre informazioni su queste impostazioni in [Configurare le impostazioni dei criteri per Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings), nella documentazione di Windows Hello.


Per altre informazioni sui profili di Windows Hello for Business in Intune, vedere [Configurare le impostazioni di Identity Protection in Microsoft Intune](identity-protection-configure.md).

## <a name="before-you-begin"></a>Prima di iniziare

[Creare un profilo di configurazione](identity-protection-configure.md#create-the-device-profile).

## <a name="windows-hello-for-business"></a>Windows Hello for Business
- **Configurare Windows Hello for Business**:
  - **Non configurato** - Selezionare questa impostazione se non si vuole usare Intune per controllare le impostazioni di Windows Hello for Business. Eventuali impostazioni di Windows Hello for Business presenti nei dispositivi Windows 10 non verranno modificate. Tutte le altre impostazioni nel riquadro non sono disponibili.

  - **Disabilitato** - Selezionare questa impostazione se non si vuole usare Windows Hello for Business. Tutte le altre impostazioni nella schermata risultano non disponibili.
  - **Abilitato** - Selezionare questa impostazione se si vuole configurare le impostazioni di Windows Hello for Business.  
  
  **Impostazione predefinita**: Non configurato

  Con l'opzione *Abilitato* sono disponibili le impostazioni seguenti:

  - **Lunghezza minima del PIN**  
    Specificare una lunghezza minima del PIN per i dispositivi, per proteggerne l'accesso. Le impostazioni predefinite dei dispositivi Windows prevedono sei caratteri, ma per questa impostazione possono essere accettati da quattro a 127 caratteri. 

    **Impostazione predefinita**: *Non configurato*

  - **Lunghezza massima del PIN**  
  Specificare una lunghezza massima del PIN per i dispositivi, per proteggerne l'accesso. Le impostazioni predefinite dei dispositivi Windows prevedono sei caratteri, ma per questa impostazione possono essere accettati da quattro a 127 caratteri.  

    **Impostazione predefinita**: *Non configurato*  

  - **Lettere minuscole nel PIN**  
    è possibile applicare un PIN più efficace richiedendo agli utenti finali di includere lettere minuscole. Le opzioni disponibili sono:

    - **Non consentito** - Impedisce agli utenti di usare lettere minuscole nel PIN. Questo comportamento si verifica anche se l'impostazione non è configurata.
    - **Consentito** - Consente agli utenti di usare lettere minuscole nel PIN, ma non è obbligatorio.
    - **Obbligatorio** - Gli utenti devono includere almeno una lettera minuscola nel PIN. Ad esempio, di solito si richiede almeno una lettera maiuscola e un carattere speciale.

  - **Lettere maiuscole nel PIN**  
    è possibile applicare un PIN più efficace richiedendo agli utenti finali di includere lettere maiuscole. Le opzioni disponibili sono:

    - **Non consentito** - Impedisce agli utenti di usare lettere maiuscole nel PIN. Questo comportamento si verifica anche se l'impostazione non è configurata.
    - **Consentito** - Consente agli utenti di usare caratteri speciali nel PIN, ma non è obbligatorio.
    - **Obbligatorio** - Gli utenti devono includere almeno un carattere speciale nel PIN. Ad esempio, di solito si richiede almeno una lettera maiuscola e un carattere speciale.

  - **Caratteri speciali nel PIN**  
    è possibile applicare un PIN più efficace richiedendo agli utenti finali di includere caratteri speciali. I caratteri speciali includono: `! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`  

    Le opzioni disponibili sono:
    - **Non consentito** - Impedisce agli utenti di usare caratteri speciali nel PIN. Questo comportamento si verifica anche se l'impostazione non è configurata.
    - **Consentito** - Consente agli utenti di usare caratteri speciali nel PIN, ma non è obbligatorio.
    - **Obbligatorio** - Gli utenti devono includere almeno un carattere speciale nel PIN. Ad esempio, di solito si richiede almeno una lettera maiuscola e un carattere speciale.

    **Impostazione predefinita**: Non consentito

  - **Scadenza PIN (giorni)**  
    Si consiglia di specificare un periodo di scadenza dopo il quale gli utenti finali devono modificare il PIN. Le impostazioni predefinite dei dispositivi Windows prevedono 41 giorni.

    **Impostazione predefinita**: Non configurato

  - **Ricorda cronologia PIN**  
    Limita il riutilizzo di PIN usati in precedenza. Per impostazione predefinita, nei dispositivi Windows non è possibile riusare gli ultimi cinque PIN impostati.  

    **Impostazione predefinita**: Non configurato  

  - **Abilita il recupero del PIN**   
    Consente all'utente di usare il servizio di ripristino PIN di Windows Hello for Business. 
    
    - **Abilitato** - Il segreto di ripristino del PIN viene archiviato nel dispositivo e l'utente, se necessario, può modificare il PIN.  
    - **Disabilitato** - Non viene creato né archiviato alcun segreto del ripristino.

    **Impostazione predefinita**: Non configurato

  - **Usa un modulo TPM (Trusted Platform Module)**    
    Un chip TPM (Trusted Platform Module) fornisce un livello aggiuntivo di sicurezza dei dati.  

    - **Abilitato** - Solo i dispositivi con un modulo TPM accessibile possono eseguire il provisioning di Windows Hello for Business.
    - **Non configurato** - I dispositivi provano a usare prima un modulo TPM. Se non è disponibile, possono usare la crittografia software.
    
    **Impostazione predefinita**: Non configurato

  - **Consenti autenticazione biometrica**  
     Abilita l'autenticazione biometrica, ad esempio il riconoscimento facciale o delle impronte digitali, come alternativa a un PIN di Windows Hello for Business. Gli utenti devono comunque configurare un PIN aziendale in caso di errore dell'autenticazione biometrica. Scegliere tra:

    - **Abilita** - Windows Hello for Business consente l'autenticazione biometrica.
    - **Non configurato** - Windows Hello for Business impedisce l'autenticazione biometrica (per tutti i tipi di account).

    **Impostazione predefinita**: Non configurato

  - **Usa anti-spoofing avanzato, se disponibile**  
    Consente di configurare se usare le funzionalità di anti-spoofing di Windows Hello nei dispositivi che lo supportano, ad esempio il rilevamento di una fotografia di un viso invece di un viso reale.  
    - **Abilita** - Windows richiede a tutti gli utenti di usare la funzionalità di anti-spoofing per il riconoscimento facciale, se supportata.
    - **Non configurato** - Windows rispetta le configurazioni di anti-spoofing del dispositivo.

    **Impostazione predefinita**: Non configurato

  - **Certificato per risorse locali**  

    - **Abilita** - Consente a Windows Hello for Business di usare i certificati per l'autenticazione a risorse locali.
    - **Non configurato** - Impedisce a Windows Hello for Business di usare i certificati per l'autenticazione a risorse locali. Al contrario, i dispositivi usano il comportamento predefinito di *autenticazione locale con chiave*. Per altre informazioni, vedere [Certificato utente per l'autenticazione locale](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) nella documentazione di Windows Hello.  

  **Impostazione predefinita**: Non configurato

- **Usa le chiavi di sicurezza per l'accesso**  
  Questa impostazione è disponibile per i dispositivi che eseguono Windows 10 versione 1903 o successiva. Consente di gestire il supporto per l'uso delle chiavi di sicurezza di Windows Hello per la procedura di accesso.  

  - **Abilitato** - Gli utenti possono usare una chiave di sicurezza di Windows Hello come credenziale di accesso per i PC interessati da questi criteri. 
  - **Disabilitato** - Le chiavi di sicurezza sono disabilitate e gli utenti non possono usarle per accedere ai PC.   

  **Impostazione predefinita**: Non configurato

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](../configuration/device-profile-assign.md) e [monitorarne lo stato](../configuration/device-profile-monitor.md).
