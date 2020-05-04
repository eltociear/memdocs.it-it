---
title: Usare i modelli per dispositivi Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Usare i modelli amministrativi di Microsoft Intune ed Endpoint Manager per creare gruppi di impostazioni per dispositivi Windows 10. Usare queste impostazioni in un profilo di configurazione del dispositivo per controllare le applicazioni di Office, Microsoft Edge, proteggere le funzionalità di Internet Explorer, controllare l'accesso a OneDrive, usare le funzionalità di desktop remoto, abilitare la riproduzione automatica, impostare le opzioni di risparmio energia, usare la stampa HTTP, usare opzioni di accesso utente diverse e controllare le dimensioni del log eventi.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f609ec62259deffb220c8ee935d0f10a98ae77b5
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254895"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Usare i modelli di Windows 10 per configurare le impostazioni di Criteri di gruppo in Microsoft Intune

Per gestire i dispositivi di un'organizzazione, può essere utile creare un gruppo di impostazioni da applicare a gruppi di dispositivi diversi. Supponiamo ad esempio di avere vari gruppi di dispositivi. A GruppoA si vuole assegnare un set di impostazioni specifico. A GruppoB si vuole assegnare un set di impostazioni diverso. Si vuole anche disporre di una visualizzazione semplice delle impostazioni che è possibile configurare.

Per completare questa attività, è possibile usare **Modelli amministrativi** in Microsoft Intune. I modelli amministrativi includono centinaia di impostazioni che controllano le funzionalità in Microsoft Edge versione 77 e successive, Internet Explorer, applicazioni Microsoft Office, Desktop remoto, OneDrive, password e PIN e altro ancora. Queste impostazioni consentono agli amministratori di gruppi di gestire i Criteri di gruppo tramite il cloud.

Questa funzionalità si applica a:

- Windows 10 e versioni successive

Le impostazioni di Windows sono simili alle impostazioni di Criteri di gruppo (GPO) in Active Directory (AD). Queste impostazioni sono incluse in Windows e sono [impostazioni supportate da ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) che usano XML. Le impostazioni di Office e Microsoft Edge vengono inserite in ADMX e usano le impostazioni di ADMX nei [file dei modelli amministrativi di Office](https://www.microsoft.com/download/details.aspx?id=49030) e nei [file dei modelli amministrativi di Microsoft Edge](https://www.microsoftedgeinsider.com/enterprise). I modelli di Intune sono completamente basati sul cloud. Offrono un modo semplice e immediato di configurare le impostazioni e trovare quelle che interessano.

La funzionalità **Modelli amministrativi** è incorporata in Intune e non richiede alcuna personalizzazione, incluso l'uso di OMA-URI. Usare queste impostazioni dei modelli nella propria soluzione di gestione di dispositivi mobili (MDM) per gestire i dispositivi Windows 10 da una posizione centralizzata.

Questo articolo illustra i passaggi da eseguire per creare un modello per dispositivi Windows 10 e mostra come filtrare tutte le impostazioni disponibili in Intune. Con la creazione del modello viene creato un profilo di configurazione del dispositivo. È quindi possibile assegnare o distribuire questo profilo ai dispositivi Windows 10 dell'organizzazione.

## <a name="before-you-begin"></a>Prima di iniziare

- Alcune di queste impostazioni sono disponibili a partire da Windows 10 versione 1709 (RS2/build 15063). Alcune impostazioni non sono incluse in tutte le edizioni di Windows. Per un'esperienza ottimale, è consigliabile usare Windows 10 Enterprise versione 1903 (19H1/build 18362) e versioni successive.

- Le impostazioni di Windows usano i [provider di servizi di configurazione (CSP) dei criteri di Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). I provider CSP funzionano in diverse edizioni di Windows, ad esempio Home, Professional, Enterprise e così via. Per verificare se un provider CSP funziona in un'edizione specifica, vedere i [provider di servizi di configurazione (CSP) di criteri di Windows](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Creare il modello

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
    - **Profilo**: selezionare **Modelli amministrativi**.

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il profilo. Assegnare ai profili nomi che possano essere identificati facilmente in un secondo momento. Un nome di profilo valido è ad esempio **Modello amministrativo: modello amministrativo Windows 10 che configura le impostazioni XYZ in Microsoft Edge**.
    - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.

7. In **Impostazioni di configurazione** configurare le impostazioni che si applicano al dispositivo (**Configurazione computer**) e le impostazioni che si applicano agli utenti **(Configurazione utente**):

    > [!div class="mx-imgBorder"]
    > ![Applicare le impostazioni del modello ADMX a utenti e dispositivi in Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Quando si seleziona **Configurazione computer**, vengono visualizzate le categorie di impostazioni. È possibile selezionare qualsiasi categoria per visualizzare le impostazioni disponibili.

    Selezionare ad esempio **Configurazione computer** > **Componenti di Windows** > **Internet Explorer** per visualizzare tutte le impostazioni del dispositivo che si applicano a Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Vedere tutte le impostazioni del dispositivo che si applicano a Internet Explorer in Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. È anche possibile selezionare **Tutte le impostazioni** per visualizzare tutte le impostazioni del dispositivo. Scorrere verso il basso e usare le frecce per andare avanti e indietro per visualizzare altre impostazioni:

    > [!div class="mx-imgBorder"]
    > ![Esempio di un elenco di impostazioni con le frecce avanti e indietro](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Selezionare un'impostazione qualsiasi, Ad esempio, filtrare in base a **Office** e selezionare **Attivazione esplorazione con restrizioni**. Viene visualizzata una descrizione dettagliata dell'impostazione. Scegliere **Abilitata**, **Disabilitata** oppure lasciare l'opzione **Non configurata** (impostazione predefinita). La descrizione dettagliata spiega anche cosa accade quando si sceglie **Abilitata**, **Disabilitata** o **Non configurata**.

    > [!TIP]
    > Le impostazioni di Windows in Intune sono correlate al percorso dei Criteri di gruppo locali visualizzato in Editor Criteri di gruppo locali (`gpedit`)

11. Selezionare **OK** per salvare le modifiche.

    Continuare a scorrere l'elenco delle impostazioni e configurare quelle che si vogliono implementare nell'ambiente. Ecco alcuni esempi:

    - Usare l'impostazione **Impostazioni notifiche macro VBA** per gestire le macro VBA in diverse applicazioni Microsoft Office, tra cui Word ed Excel.
    - Usare l'impostazione **Consenti download dei file** per consentire o impedire i download da Internet Explorer.
    - Usare **Richiedi password alla riattivazione del computer (alimentazione da rete elettrica)** per richiedere agli utenti una password quando il dispositivo torna attivo dopo uno stato di inattività.
    - Usare l'impostazione **Scarica controlli ActiveX non firmati** per impedire agli utenti di scaricare controlli ActiveX non firmati da Internet Explorer.
    - Usare l'impostazione **Disattiva Ripristino configurazione di sistema** per consentire o impedire agli utenti di eseguire un ripristino del sistema sul dispositivo.
    - Usare l'impostazione **Allow importing of favorites** (Consenti importazione Preferiti) per consentire o impedire agli utenti di importare i Preferiti da un altro browser in Microsoft Edge.
    - E molte altre...

12. Selezionare **Avanti**.
13. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](..//fundamentals/scope-tags.md).

    Selezionare **Avanti**.

14. In **Assegnazioni** selezionare l'utente o i gruppi che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Se il profilo è assegnato a gruppi di utenti, le impostazioni ADMX configurate si applicano a tutti i dispositivi che l'utente registra e a cui accede. Se il profilo è assegnato a gruppi di dispositivi, le impostazioni ADMX configurate si applicano a qualsiasi utente che accede al dispositivo. Questa assegnazione si verifica se l'impostazione ADMX è una configurazione computer (`HKEY_LOCAL_MACHINE`) o una configurazione utente (`HKEY_CURRENT_USER`). Con alcune impostazioni, un'impostazione del computer assegnata a un utente può anche influire sull'esperienza di altri utenti su tale dispositivo.
    
    Per altre informazioni, vedere [Gruppi di utenti e gruppi di dispositivi](device-profile-assign.md#user-groups-vs-device-groups).

    Selezionare **Avanti**.

15. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

Alla successiva verifica degli aggiornamenti della configurazione da parte del dispositivo, le impostazioni configurate verranno applicate.

## <a name="find-some-settings"></a>Trovare alcune impostazioni

In questi modelli sono disponibili centinaia di impostazioni. Per trovare più facilmente determinate impostazioni, usare le funzionalità predefinite:

- Nel modello selezionare la colonna **Impostazioni**, **Stato**, **Tipo di impostazione** o **Percorso** per ordinare l'elenco. Ad esempio, selezionare la colonna **Percorso** e usare la freccia avanti per visualizzare le impostazioni nel percorso `Microsoft Excel`:

- Usare la **casella di ricerca** del modello per trovare impostazioni specifiche. È possibile eseguire la ricerca in base all'impostazione o al percorso. Ad esempio, cercare `copy`. Vengono visualizzate tutte le impostazioni che contengono `copy`:

  > [!div class="mx-imgBorder"]
  > ![Ricerca di copy per visualizzare tutte le impostazioni del dispositivo nei modelli amministrativi in Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  In un altro esempio cercare `microsoft word`. Vengono visualizzate le impostazioni che è possibile configurare per l'applicazione Microsoft Word. Cercare `explorer` per visualizzare le impostazioni di Internet Explorer che è possibile aggiungere al modello.

## <a name="next-steps"></a>Passaggi successivi

Il modello è stato creato, ma non è ancora operativo. A questo punto [Assegnare il modello, detto anche profilo](device-profile-assign.md), e [monitorarne lo stato](device-profile-monitor.md).

Aggiornare [Office 365 usando i modelli amministrativi](administrative-templates-update-office.md).

[Esercitazione: Usare il cloud per configurare criteri di gruppo nei dispositivi Windows 10 con modelli ADMX e Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
