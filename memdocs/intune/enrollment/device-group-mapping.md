---
title: Raggruppare i dispositivi in categorie in Intune
titleSuffix: Microsoft Intune
description: Informazioni sul raggruppamento dei dispositivi in categorie per una gestione più semplice.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7b668c37-40b9-4c69-8334-5d8344e78c24
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b10d56e9eb915273d5be9a5b14ca4528a64a2057
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327112"
---
# <a name="categorize-devices-into-groups"></a>Raggruppare i dispositivi in categorie

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Per semplificare la gestione dei dispositivi, è possibile usare le categorie di dispositivi di Microsoft Intune per aggiungere automaticamente i dispositivi a gruppi basati su categorie definite dall'utente.

Le categorie dei dispositivi usano il flusso di lavoro seguente:
1. Creare categorie che gli utenti possano scegliere quando registrano i dispositivi.
2. Quando gli utenti registrano un dispositivo iOS/iPadOS e Android, devono scegliere una categoria nell'elenco delle categorie configurate. Per assegnare una categoria a un dispositivo Windows, gli utenti devono utilizzare il sito Web Portale aziendale.
3. È quindi possibile distribuire app e criteri a tali gruppi.

È possibile creare qualsiasi categoria di dispositivi desiderata. Ad esempio:
- Dispositivo POS
- Dispositivo di prova
- Vendite
- Contabilità
- Manager

## <a name="how-to-configure-device-categories"></a>Come configurare le categorie di dispositivi

### <a name="step-1-create-device-categories-on-the-intune-blade-of-the-azure-portal"></a>Passaggio 1: creare categorie di dispositivi nel pannello Intune del portale di Azure
1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere **Dispositivi** > **Categorie di dispositivi**.
2. Nella pagina **Categorie di dispositivi** scegliere **Crea** per aggiungere una nuova categoria.
3. Nel pannello **Crea categoria di dispositivi** immettere un **Nome** per la nuova categoria e una **Descrizione** facoltativa.
4. Al termine, selezionare **Crea**. È possibile visualizzare la nuova categoria nell'elenco delle categorie.

Il nome della categoria di dispositivi verrà usato per la creazione dei gruppi di sicurezza di Azure Active Directory (Azure AD) nel passaggio 2.

### <a name="step-2-create-azure-active-directory-security-groups"></a>Passaggio 2: creare i gruppi di sicurezza di Azure Active Directory
In questo passaggio verranno creati gruppi dinamici nel portale di Azure, basati sulla categoria di dispositivi e sul nome della categoria di dispositivi.

Per continuare, vedere [Uso degli attributi per creare regole avanzate](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/#using-attributes-to-create-rules-for-device-objects) nella documentazione di Azure Active Directory.

Usare le informazioni in questa sezione per creare un gruppo di dispositivi con una regola avanzata usando l'attributo **deviceCategory**. Ad esempio (**device.deviceCategory - eq** "*nome della categoria di dispositivi ottenuto dal portale di Azure*".

Dopo aver configurato i gruppi di dispositivi, e dopo che gli utenti hanno registrato i loro dispositivi, viene visualizzato un elenco delle categorie configurate. Dopo che gli utenti hanno scelto una categoria e completato la registrazione, il loro dispositivo viene aggiunto al gruppo di sicurezza di Active Directory corrispondente alla categoria selezionata.

### <a name="view-the-categories-of-devices-that-you-manage"></a>Visualizzare le categorie di dispositivi gestiti

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e scegliere **Dispositivi** > **Tutti i dispositivi**.

2. Nell'elenco dei dispositivi esaminare la colonna **Categoria del dispositivo**.

Se la colonna **Categoria del dispositivo** non è visualizzata, selezionare **Colonne** > **Categoria** > **Applica**.

### <a name="change-the-category-of-a-device"></a>Cambiare la categoria di un dispositivo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), scegliere **Dispositivi** > **Tutti i dispositivi** > scegliere il dispositivo desiderato > **Proprietà**.
2. Nel pannello successivo è possibile modificare la **categoria del dispositivo** selezionato in uno dei nomi di categoria configurati in precedenza.

## <a name="after-you-configure-device-groups"></a>Dopo la configurazione dei gruppi di dispositivi

Quando gli utenti registrano il dispositivo iOS/iPadOS e Android, devono scegliere una categoria nell'elenco delle categorie configurate. Dopo che hanno scelto una categoria e completato la registrazione, il loro dispositivo viene aggiunto al gruppo di dispositivi di Intune o al gruppo di sicurezza di Active Directory corrispondente alla categoria selezionata.

Gli utenti in Windows devono usare il sito Web Portale aziendale per selezionare una categoria.

Indipendentemente dalla piattaforma, gli utenti possono sempre passare a portal.manage.microsoft.com dopo la registrazione del dispositivo. Richiedere all'utente di accedere al sito Web Portale aziendale e passare a **Dispositivi personali**. L'utente potrà scegliere un dispositivo registrato elencato nella pagina e quindi selezionare una categoria.

Dopo la scelta della categoria, il dispositivo viene automaticamente aggiunto al gruppo corrispondente creato. Se un dispositivo è già registrato prima che vengano configurate le categorie, l'utente visualizza una notifica sul dispositivo nel sito Web Portale aziendale. Viene così comunicato all'utente che la volta successiva che eseguirà l'accesso all'app Portale aziendale in iOS/iPadOS o Android dovrà selezionare una categoria.

## <a name="further-information"></a>Altre informazioni
- È possibile modificare una categoria di dispositivo nel portale di Azure, ma è necessario aggiornare manualmente i gruppi di sicurezza di Azure AD che fanno riferimento a questa categoria.

- Se si elimina una categoria, per i dispositivi a essa assegnati viene visualizzato il nome di categoria **Non assegnati**.
