---
title: Impostazioni di Windows Hello for Business
titleSuffix: Configuration Manager
description: Informazioni su come integrare Windows Hello for Business con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706219"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Impostazioni di Windows Hello for Business in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1245704-->
Configuration Manager si integra con Windows Hello for Business. Questa funzionalità in precedenza era nota come Microsoft Passport for Work. Windows Hello for Business è un metodo di accesso alternativo per i dispositivi Windows 10. Usa Active Directory o un account di Azure Active Directory (Azure AD) per sostituire una password, una smart card o una smart card virtuale. Hello for Business consente di eseguire l'accesso usando un *movimento dell'utente* anziché una password. Il movimento dell'utente può essere un semplice PIN, un'autenticazione biometrica o un dispositivo come un lettore di impronte digitali.

> [!Important]  
> A partire dalla versione 1910 l'autenticazione basata su certificato con le impostazioni di Windows Hello for Business in Configuration Manager non è supportata. Per altre informazioni, vedere [Funzionalità deprecate](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). L'autenticazione basata su chiave è ancora valida.
>
> La distribuzione di Active Directory Federation Services Registration Authority (ADFS RA) è più semplice, offre un'esperienza utente migliore e consente un'esperienza di registrazione certificati più deterministica. Usare ADFS RA per l'autenticazione basata su certificato con Windows Hello for Business.
>
> Per i dispositivi con co-gestione può essere utile trasferire il carico di lavoro [**Criteri di accesso alle risorse**](../../comanage/workloads.md#resource-access-policies) a Intune. Quindi usare i criteri Intune per gestire i certificati corrispondenti. Per altre informazioni, vedere [Come trasferire i carichi di lavoro](../../comanage/how-to-switch-workloads.md).

Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

Configuration Manager si integra con Windows Hello for Business nei modi seguenti:  

- Stabilire quali movimenti gli utenti possono e non possono usare per accedere.  

- Archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Windows Hello for Business. Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  

- Creare e distribuire un profilo di Windows Hello per controllarne le impostazioni su dispositivi appartenenti a un dominio Windows 10 che eseguono il client di Configuration Manager. A partire dalla versione 1910 non è possibile usare l'autenticazione basata su certificati. Quando si usa l'autenticazione basata su chiavi non è necessario distribuire un profilo certificato.

## <a name="configure-a-profile"></a>Configurare un profilo  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **Impostazioni di conformità**, espandere **Accesso alle risorse aziendali** e selezionare il nodo **Profili Windows Hello for business**.

1. Nella barra multifunzione selezionare **Creare profilo Windows Hello for Business** per avviare la creazione guidata profilo.

1. Nella pagina **Generale** specificare un nome e una descrizione facoltativa per il profilo.

1. Nella pagina **Piattaforme supportate** selezionare le versioni del sistema operativo a cui deve essere applicato il profilo.

1. Nella pagina **Impostazioni** configurare le impostazioni seguenti:

    - **Configurare Windows Hello for Business**: Specificare se il profilo abilita, disabilita o non configura Hello for Business.

    - **Usa un modulo TPM (Trusted Platform Module)** : Un TPM (Trusted Platform Module) fornisce un livello aggiuntivo di sicurezza dei dati. Scegliere uno dei valori seguenti:  

      - **Richiesto**: Solo i dispositivi con un modulo TPM accessibile possono eseguire il provisioning di Windows Hello for Business.  

      - **Preferito**: I dispositivi provano a usare prima un modulo TPM. Se non è disponibile, possono usare la crittografia software.

    - **Metodo di autenticazione**: Impostare questa opzione su **Non configurato** o **Basato su chiavi**.

        > [!NOTE]
        > A partire dalla versione 1910 l'autenticazione basata su certificato con le impostazioni di Windows Hello for Business in Configuration Manager non è supportata.

    - **Configurare la lunghezza minima del PIN**: Se si vuole richiedere una lunghezza minima per il PIN dell'utente, abilitare questa opzione e specificare un valore. Se l'opzione è abilitata, il valore predefinito è `4`.

    - **Configurare la lunghezza massima del PIN**: Se si vuole richiedere una lunghezza massima per il PIN dell'utente, abilitare questa opzione e specificare un valore. Se l'opzione è abilitata, il valore predefinito è `127`.

    - **Richiedi scadenza PIN (giorni)** : Specifica il numero di giorni prima che l'utente debba modificare il PIN del dispositivo.

    - **Impedisci riutilizzo dei PIN precedenti**: Non consentire agli utenti di usare PIN già usati in precedenza.

    - **Richiedi lettere maiuscole nel PIN**: specifica se gli utenti devono includere lettere maiuscole nel PIN di Windows Hello for Business. Scegliere tra:  

      - **Consentito**: gli utenti possono usare caratteri maiuscoli nel PIN, ma non è obbligatorio.

      - **Richiesto**: gli utenti devono includere almeno un carattere maiuscolo nel PIN.  

      - **Non consentito**: gli utenti non possono usare caratteri maiuscoli nel PIN.  

    - **Richiedi lettere minuscole nel PIN**: specifica se gli utenti devono includere lettere minuscole nel PIN di Windows Hello for Business. Scegliere tra:  

      - **Consentito**: gli utenti possono usare caratteri minuscoli nel PIN, ma non è obbligatorio.

      - **Richiesto**: gli utenti devono includere almeno un carattere minuscolo nel PIN.  

      - **Non consentito**: gli utenti possono usare caratteri minuscoli nel PIN.  

    - **Configurare i caratteri speciali**: Specifica l'uso di caratteri speciali nel PIN. Scegliere tra:  

        > [!NOTE]
        > I caratteri speciali includono il set seguente:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Consentito**: gli utenti possono usare caratteri speciali nel PIN, ma non è obbligatorio.  

      - **Richiesto**: gli utenti devono includere almeno un carattere speciale nel PIN.  

      - **Non consentito**: gli utenti non possono usare caratteri speciali nel PIN. Questo comportamento si verifica anche se l'opzione **non è configurata**.  

    - **Configurare l'uso delle cifre nel PIN**: Specifica l'uso dei numeri nel PIN. Scegliere tra:

      - **Consentito**: Gli utenti possono usare numeri nel PIN, ma non è obbligatorio.  

      - **Richiesto**: Gli utenti devono includere almeno un numero nel PIN.  

      - **Non consentito**: Gli utenti non possono usare numeri nel PIN.

    - **Abilita movimenti biometrici**: Usare l'autenticazione biometrica, ad esempio l'impronta digitale o il riconoscimento facciale. Queste modalità sono alternative all'uso di un PIN per Windows Hello for Business. Gli utenti devono comunque configurare un PIN in caso di errore dell'autenticazione biometrica.  

      Se impostato su **Sì**, Windows Hello for Business consente l'autenticazione biometrica. Se impostato su **No**, Windows Hello for Business impedisce l'autenticazione biometrica per tutti i tipi di account.  

    - **Usare l'anti-spoofing avanzato**: Configura la funzionalità avanzata di anti-spoofing nei dispositivi che la supportano. Se impostato su **Sì**, Windows richiede a tutti gli utenti di usare la funzionalità di anti-spoofing per le caratteristiche del viso, se supportata.  

    - **Usare l'accesso tramite telefono**: Configura l'autenticazione a due fattori con un telefono cellulare.

1. Completare la procedura guidata.

Lo screenshot seguente è un esempio di impostazioni del profilo di Windows Hello for business:  

![Creazione guidata dei criteri di Windows Hello for Business, con l'elenco delle impostazioni disponibili](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Configurare le autorizzazioni

1. Se l'utente è un amministratore di dominio o ha credenziali equivalenti, può accedere a una workstation amministrativa sicura con la seguente funzionalità facoltativa installata: Strumenti di amministrazione remota del server: Active Directory Domain Services e strumenti Lightweight Directory Services.

1. Aprire la console **Utenti e computer di Active Directory**.

1. Selezionare il dominio, passare al menu **Azione** e selezionare **Proprietà**.

1. Passare alla scheda **Protezione** e selezionare **Avanzata**.

    > [!TIP]
    > Se la scheda **Protezione** non viene visualizzata, chiudere la finestra delle proprietà. Accedere al menu **Visualizza** e selezionare **Caratteristiche avanzate**.

1. Selezionare **Aggiungi**.

1. Scegliere **Selezionare un'entità** e immettere `Key Admins`.

1. Dall'elenco **Si applica a** scegliere **Oggetti Utente discendenti**.

1. Selezionare **Cancella tutto** nella parte inferiore della pagina.

1. Nella sezione **Proprietà** selezionare **Leggi msDS-KeyCredentialLink**.

1. Selezionare **OK** per salvare le modifiche e chiudere tutte le finestre.

## <a name="next-steps"></a>Passaggi successivi

[Profili certificato](introduction-to-certificate-profiles.md)
