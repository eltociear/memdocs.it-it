---
title: Configurare criteri di accesso condizionale basato su app con Intune
titleSuffix: Microsoft Intune
description: Informazioni su come configurare criteri di accesso condizionale basato su app con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fadd5817ccd4e591fe92c11cb30041296ac85d61
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696464"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Configurare criteri di accesso condizionale basato su app con Intune

Configurare criteri di accesso condizionale basato su app per le app incluse nell'elenco di app approvate. L'elenco di app approvate include le applicazioni testate da Microsoft.

Per poter usare i criteri di accesso condizionale basato su app è necessario che i [criteri di protezione delle app di Intune](../apps/app-protection-policies.md) siano applicati alle app in uso.

> [!IMPORTANT]
> Questo articolo illustra in dettaglio i passaggi per aggiungere un criterio di accesso condizionale semplice basato su app. È possibile usare la stessa procedura per altre app cloud. Per altre informazioni, vedere [Pianificare la distribuzione dell'accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/plan-conditional-access).

## <a name="create-app-based-conditional-access-policies"></a>Creare criteri di accesso condizionale basato su app

L'accesso condizionale è una tecnologia di Azure Active Directory (Azure AD). Il nodo di accesso condizionale accessibile da *Intune* è lo stesso nodo a cui si accede da *Azure AD*. Poiché il nodo è lo stesso, non è necessario spostarsi fra Intune e Azure AD per configurare i criteri.

Per poter creare criteri di accesso condizionale dall'interfaccia di amministrazione di Microsoft Endpoint Manager, è necessario avere una licenza Azure AD Premium.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Per creare criteri di accesso condizionale basato su app

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selezionare **Endpoint Security** > **Accesso condizionale** > **Nuovi criteri**.

3. Immettere un **Nome** per i criteri e quindi in *Assegnazioni* selezionare **Utenti e gruppi**. Usare l'opzione Includi o Escludi per aggiungere i gruppi per il criterio e selezionare **Fatto**.

4. Selezionare **Applicazioni cloud o azioni** e scegliere le app da proteggere. Ad esempio, scegliere **Selezionare le app** e selezionare **Office 365 (anteprima)** .

   Selezionare **Fatto** per salvare le modifiche.

5. Selezionare **Condizioni** > **App client** per applicare il criterio alle app e ai browser. Ad esempio, selezionare **Sì** e quindi abilitare **Browser** e **App per dispositivi mobili e client desktop**.

   Selezionare **Fatto** per salvare le modifiche.

6. In *Controlli di accesso* selezionare **Concedi** per applicare l'accesso condizionale basato sulla conformità del dispositivo. Ad esempio, selezionare **Concedi accesso** > **Richiedi app client approvata** e **Richiedi criteri di protezione delle app (anteprima)** quindi selezionare **Richiedi uno dei controlli selezionati**

   Scegliere **OK** per salvare le modifiche.

7. In **Attiva criterio** selezionare **Attivato**, e quindi selezionare **Crea** per salvare le modifiche.





## <a name="next-steps"></a>Passaggi successivi
[Bloccare le app che non usano l'autenticazione moderna](app-modern-authentication-block.md)

## <a name="see-also"></a>Vedere anche

[Proteggere i dati delle app con i criteri di protezione delle app](../apps/app-protection-policies.md)
[Accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
