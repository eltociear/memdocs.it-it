---
title: Creare i criteri di conformità dei dispositivi in Microsoft Intune - Azure | Microsoft Docs
description: Creare i criteri di conformità, panoramica dei livelli di stato e gravità, utilizzo dello stato InGracePeriod, utilizzo dell'accesso condizionale, gestione dei dispositivi senza un criterio assegnato e differenze di conformità tra il portale di Azure e il portale classico in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1431105bdba9731bda4599e310889bfbf86a2c
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252255"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Creare criteri di conformità in Microsoft Intune

I criteri di conformità dei dispositivi sono una funzionalità fondamentale quando si usa Intune per proteggere le risorse dell'organizzazione. In Intune è possibile creare regole e impostazioni che i dispositivi devono soddisfare per essere considerati conformi, ad esempio la versione minima del sistema operativo. Se il dispositivo non è conforme, è possibile bloccare l'accesso ai dati e alle risorse tramite l'[accesso condizionale](conditional-access.md).

È anche possibile eseguire azioni specifiche in caso di mancata conformità, ad esempio inviare una notifica tramite posta elettronica all'utente. Per una panoramica degli effetti dei criteri di conformità e delle modalità di utilizzo, vedere [Introduzione ai criteri di conformità dei dispositivi in Intune](device-compliance-get-started.md).

Questo articolo:

- Illustra i prerequisiti e i passaggi da eseguire per creare criteri di conformità.
- Illustra come assegnare i criteri ai gruppi di utenti e di dispositivi.
- Descrive altre funzionalità, tra cui i tag di ambito per "filtrare" i criteri e le operazioni che è possibile eseguire sui dispositivi non conformi.
- Elenca la frequenza dei cicli di aggiornamento quando i dispositivi ricevono aggiornamenti dei criteri.

## <a name="before-you-begin"></a>Prima di iniziare

Per usare criteri di conformità del dispositivo, attenersi a quanto segue:

- Uso delle sottoscrizioni seguenti:

  - Intune
  - Se si usa l'accesso condizionale è necessario Azure Active Directory (AD) Premium. La pagina [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) spiega cosa si ottiene con le diverse edizioni. Azure AD non è necessario per la conformità di Intune.

- Uso di una piattaforma supportata:

  - Amministratore dispositivo Android
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1

- Registrazione dei dispositivi in Intune (necessaria per visualizzarne lo stato di conformità)

- Registrazione dei dispositivi per un solo utente o senza un utente primario. Non sono supportati dispositivi registrati per più utenti.

## <a name="create-the-policy"></a>Creare i criteri

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Dispositivi** > **Criteri di conformità** > **Criteri** > **Crea criterio**.

3. Selezionare una **Piattaforma** per questi criteri dalle opzioni seguenti:
   - *Amministratore di dispositivi Android*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows 8.1 e versioni successive*
   - *Windows 10 e versioni successive*

    Per *Android Enterprise* è anche possibile selezionare un **Tipo di criterio**:
     - *Criteri del profilo di lavoro Android completamente gestito, dedicato e di proprietà aziendale*
     - *Criteri di conformità del profilo di lavoro Android*

    Selezionare quindi **Crea** per aprire la finestra di configurazione **Crea criterio**.

4. Nella scheda **Informazioni di base** specificare un **Nome** per identificare facilmente i criteri in un secondo momento. Ad esempio, un nome di criterio valido è **Dispositivi iOS/iPadOS jailbroken di Marco non conformi**.

   È anche possibile specificare una **Descrizione**.
  
5. Nella scheda **Impostazioni di conformità** espandere le categorie disponibili e configurare le impostazioni per i criteri.  Gli articoli seguenti descrivono le impostazioni per ogni piattaforma:
   - [Amministratore di dispositivi Android](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows 8.1 e versioni successive](compliance-policy-create-windows-8-1.md)
   - [Windows 10 e versioni successive](compliance-policy-create-windows.md)  

6. Nella scheda **Percorsi** è possibile forzare la conformità in base al percorso del dispositivo. Scegliere un percorso esistente. Se non è ancora disponibile un percorso, vedere [Usare i percorsi (isolamento di rete)](use-network-locations.md) per informazioni aggiuntive.
   > [!TIP]
   > I **Percorsi** sono disponibili solo per la piattaforma *Amministratore di dispositivi Android*.

7. Nella scheda **Azioni per la non conformità** specificare una sequenza di azioni da applicare automaticamente ai dispositivi che non soddisfano i criteri di conformità.

   È possibile aggiungere più azioni e configurare pianificazioni e dettagli aggiuntivi per alcune azioni. È ad esempio possibile modificare la pianificazione dell'azione predefinita *Contrassegna il dispositivo come non conforme* in modo che l’azione venga eseguita dopo un giorno. È poi possibile aggiungere un'azione per inviare un messaggio di posta elettronica all'utente quando il dispositivo non è conforme per comunicargli le informazioni sullo stato. È anche possibile aggiungere azioni che bloccano o ritirano i dispositivi che rimangono non conformi.

   Per informazioni sulle azioni che è possibile configurare, vedere [Aggiungere azioni per i dispositivi non conformi](actions-for-noncompliance.md), che include la procedura per creare messaggi di posta elettronica di notifica da inviare agli utenti.

   Un altro esempio prevede l'uso di Percorsi in cui si aggiunge almeno un percorso ai criteri di conformità. In questo caso l'azione predefinita per la mancata conformità viene applicata quando si seleziona almeno un percorso. Se il dispositivo non è connesso ai percorsi selezionati, viene considerato non conforme. È possibile concedere agli utenti un periodo di tolleranza, ad esempio un giorno.

8. Nella scheda **Tag di ambito** selezionare i tag per filtrare i criteri per gruppi specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Dopo aver aggiunto le impostazioni, si può anche aggiungere un tag di ambito ai criteri di conformità. 

   Per informazioni sull’uso dei tag di ambito, vedere [Usare i tag di ambito per filtrare i criteri](../fundamentals/scope-tags.md).

9. Nella scheda **Assegnazioni** assegnare i criteri ai gruppi.  

   Selezionare **+ Selezionare i gruppi da includere**, quindi assegnare i criteri a uno o più gruppi. I criteri verranno applicati a questi gruppi al salvataggio dei criteri nel passaggio successivo. 

10. Nella scheda **Rivedi e crea** esaminare le impostazioni e selezionare **Crea** per salvare i criteri di conformità.  

    Gli utenti o i dispositivi ai quali sono applicati i criteri vengono valutati per la conformità durante la sincronizzazione con Intune.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Frequenza dei cicli di aggiornamento

Intune usa diversi cicli di aggiornamento per verificare la disponibilità di aggiornamenti per i criteri di conformità. Se il dispositivo è stato registrato di recente, il controllo viene eseguito con maggiore frequenza. [Cicli di aggiornamento di criteri e profili](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) elenca i tempi di aggiornamento stimati.

Gli utenti possono aprire in qualsiasi momento l'app Portale aziendale e sincronizzare il dispositivo, per verificare in tempo reale la disponibilità di aggiornamenti dei criteri.

### <a name="assign-an-ingraceperiod-status"></a>Assegnare uno stato InGracePeriod

Lo stato InGracePeriod è un valore dei criteri di conformità. Questo valore è determinato dalla combinazione del periodo di tolleranza del dispositivo e dello stato effettivo del dispositivo per tale criterio di conformità.

In particolare, se un dispositivo presenta uno stato NonCompliant per un criterio di conformità assegnato e:

- al dispositivo non è stato assegnato alcun periodo di tolleranza, quindi il valore assegnato per il criterio di conformità è NonCompliant
- il dispositivo ha un periodo di tolleranza scaduto, quindi il valore assegnato per il criterio di conformità è NonCompliant
- il dispositivo ha un periodo di tolleranza futuro, quindi il valore assegnato per il criterio di conformità è InGracePeriod

Nella tabella seguente sono riassunte le varie situazioni:

|Stato di conformità attuale|Valore del periodo di tolleranza assegnato|Stato di conformità effettivo|
|---------|---------|---------|
|NonCompliant |Nessun periodo di tolleranza assegnato |NonCompliant |
|NonCompliant |Data trascorsa|NonCompliant|
|NonCompliant |Data futura|InGracePeriod|

Per altre informazioni sul monitoraggio dei criteri di conformità dei dispositivi, vedere [Monitorare i criteri di conformità dei dispositivi di Intune](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Assegnare uno stato dei criteri di conformità risultante

Se un dispositivo ha più criteri di conformità e il dispositivo presenta stati di conformità diversi per due o più dei criteri di conformità assegnati, verrà assegnato un unico stato di conformità risultante. Questa assegnazione si basa su un livello di gravità concettuale assegnato a ogni stato di conformità. I livelli di gravità di ogni stato di conformità sono i seguenti:

|Stato  |Gravità  |
|---------|---------|
|Sconosciuto     |1|
|NotApplicable     |2|
|Conforme|3|
|InGracePeriod|4|
|NonCompliant|5|
|Errore|6|

Quando un dispositivo ha più criteri di conformità, viene assegnato il livello di gravità massimo di tutti i criteri per quel dispositivo.

Ad esempio, un dispositivo ha tre criteri di conformità: uno con stato Sconosciuto (gravità = 1), uno con stato Conforme (gravità = 3) e uno con stato Periodo di tolleranza (gravità = 4). Lo stato Periodo di tolleranza ha il livello di gravità più alto. Tutti e tre i criteri hanno quindi lo stato di conformità Periodo di tolleranza.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i criteri](compliance-policy-monitor.md).
