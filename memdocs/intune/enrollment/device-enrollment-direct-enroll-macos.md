---
title: Usare la registrazione diretta per i dispositivi macOS
titleSuffix: Microsoft Intune
description: Informazioni su come registrare i dispositivi macOS usando la registrazione diretta.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819968"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>Usare la registrazione diretta per i dispositivi macOS

Intune supporta la registrazione di dispositivi macOS usando la registrazione diretta per i dispositivi aziendali. La registrazione diretta non cancella il dispositivo. Il dispositivo viene registrato tramite le impostazioni macOS. Questo metodo supporta solo i dispositivi **senza affinità utente**.

## <a name="prerequisites"></a>Prerequisiti

- Accesso fisico ai dispositivi macOS
- [Imposta autorità MDM](../fundamentals/mdm-authority-set.md)
- [Un certificato push MDM Apple](apple-mdm-push-certificate-get.md)
 - Diritti di amministratore per i dispositivi macOS da registrare

## <a name="create-an-apple-configurator-profile-for-devices"></a>Creare un profilo di Apple Configurator per i dispositivi

Un profilo di registrazione dispositivi consente di definire le impostazioni applicate durante la registrazione. Queste impostazioni vengono applicate una sola volta. Seguire questi passaggi per creare un profilo di registrazione per registrare i dispositivi macOS con la registrazione diretta.

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Registra i dispositivi** > **Registrazione Apple** > **Apple Configurator**.

2. Scegliere **Profili** > **Crea**.

3. In **Crea un profilo di registrazione** digitare un **nome** e una **descrizione** per il profilo per scopi amministrativi. Questi dettagli non vengono visualizzati agli utenti. È possibile usare questo campo Nome per creare un gruppo dinamico in Azure Active Directory. Usare il nome del profilo per definire il parametro enrollmentProfileName per assegnare i dispositivi con questo profilo di registrazione. Altre informazioni sui gruppi dinamici di Azure Active Directory.

4. Per **Affinità utente** scegliere **Registra senza affinità utente** - Scegliere questa opzione per i dispositivi non associati a un singolo utente. Usare questa opzione per i dispositivi che eseguono attività senza accedere ai dati utente locali. Le app che richiedono l'associazione utente, inclusa l'app Portale aziendale usata per installare le app line-of-business, non funzioneranno. Obbligatorio per la registrazione diretta.

     > [!NOTE]
     > L'opzione **Registra con affinità utente** non è supportata in macOS quando si usa la registrazione diretta. Per i dispositivi che richiedono l'affinità utente, usare la registrazione automatica dei dispositivi.

6. Scegliere **Crea** per salvare il profilo.

## <a name="direct-enrollment"></a>Registrazione diretta
Dato che la registrazione diretta supporta solo la registrazione senza affinità utente, non è possibile usare il portale aziendale per installare le applicazioni disponibili.

### <a name="export-the-profile-and-install-on-macos-devices"></a>Esportare il profilo e installarlo nei dispositivi macOS

1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) scegliere **Dispositivi** > **Registra i dispositivi** > **Registrazione Apple** > **Apple Configurator** > **Profili** > scegliere il profilo da esportare > **Esporta il profilo**.
2. In **Registrazione diretta** scegliere **Scarica profilo** e salvare il file. 

     > [!NOTE]
     > Un profilo di registrazione scaricato è valido per due settimane dopo il download. È possibile scaricare tutti i profili di registrazione usando questo collegamento in base alle esigenze. Il download di un nuovo profilo non invalida il precedente, ma non estende neanche l'ora di scadenza del file scaricato in precedenza.
         
3. Trasferire il file in un computer macOS per installarlo direttamente.
4. Fare doppio clic sul file con estensione **mobileconfig** salvato per aprirlo in Profili.
5. Quando viene richiesto di installare il profilo di gestione, selezionare **Installa**.
6. Confermare al prompt successivo che si vuole installare il profilo di gestione selezionando **Installa**.
7. Immettere le credenziali per un account amministratore nel dispositivo macOS e fare clic su **OK**.
8. Il dispositivo macOS è ora registrato in Intune e gestito. Verrà avviato il download dei profili assegnati.

## <a name="next-steps"></a>Passaggi successivi

Dopo la registrazione dei dispositivi macOS è possibile iniziare a [gestirli](../remote-actions/device-management.md).