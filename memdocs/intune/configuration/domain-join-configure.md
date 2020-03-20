---
title: Impostazioni del profilo di aggiunta al dominio per Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Creare un profilo di configurazione del dispositivo per l'aggiunta a un dominio per i dispositivi aggiunti ad Azure AD ibridi. Usare questo profilo per distribuire informazioni sul dominio Active Directory locale ai dispositivi di cui viene effettuato il provisioning con Windows Autopilot e Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364396"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Configurazione delle impostazioni di aggiunta al dominio per dispositivi aggiunti ad Azure AD ibridi in Microsoft Intune

Molti ambienti usano Active Directory (AD) in locale. Quando i dispositivi aggiunti a un dominio di AD vengono aggiunti anche ad Azure AD, vengono chiamati dispositivi aggiunti ad Azure AD ibridi. È possibile usare Windows Autopilot per [registrare dispositivi aggiunti ad Azure AD ibridi](../enrollment/windows-autopilot-hybrid.md) in Intune. Per eseguire la registrazione, è necessario anche un profilo di configurazione **Aggiunta a un dominio**.

Un profilo di configurazione **Aggiunta a un dominio** include informazioni sul dominio di Active Directory locale. Quando si esegue il provisioning dei dispositivi (in genere offline), questo profilo distribuisce i dettagli del dominio di AD, in modo che i dispositivi sappiano a quale dominio locale devono essere aggiunti. Se non si crea un profilo di aggiunta a un dominio, la distribuzione di questi dispositivi potrebbe non riuscire.

Questa funzionalità si applica a:

- Windows 10 e versioni successive
- Dispositivi aggiunti ad Azure AD ibridi
- Distribuzione ibrida con Autopilot + Intune

Questo articolo illustra come creare un profilo di aggiunta a un dominio per una distribuzione ibrida di Autopilot. È anche possibile visualizzare le impostazioni disponibili.

## <a name="create-the-profile"></a>Creare il profilo

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selezionare **Dispositivi** > **Profili di configurazione** > **Crea profilo**.
3. Immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **Windows 10: Profilo di aggiunta al dominio che include informazioni sul dominio locale per registrare dispositivi aggiunti ad AD ibridi con Windows Autopilot**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.
    - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
    - **Tipo di profilo**: selezionare **Aggiunta a un dominio (anteprima)** .

4. Selezionare **Impostazioni**. Immettere le proprietà seguenti:

    - **Prefisso nome computer**: immettere un prefisso per il nome del dispositivo. I nomi dei computer hanno una lunghezza di 15 caratteri. Dopo il prefisso, i 15 caratteri rimanenti vengono generati in modo casuale.
    - **Nome di dominio**: immettere il nome di dominio completo (FQDN) a cui aggiungere i dispositivi. Immettere ad esempio `americas.corp.contoso.com.`
    - **Unità organizzativa** (facoltativo): immettere il percorso completo ([nome distinto](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) per l'unità organizzativa (OU) in cui devono essere creati gli account computer. Immettere ad esempio `"CN=Users,DC=Contoso,DC=com"`. Se non si immette un valore, viene usato un contenitore di oggetti computer noto.

      Per ulteriori informazioni e consigli su questa impostazione, vedere [Distribuire dispositivi aggiunti ad Azure AD ibridi](../enrollment/windows-autopilot-hybrid.md).

5. Al termine, selezionare **OK** > **Crea** per salvare le modifiche.

Il profilo viene creato e visualizzato nell'elenco dei profili. Si è ora pronti per [distribuire dispositivi aggiunti ad Azure AD ibridi usando Intune e Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo averlo creato, il profilo è pronto per l'assegnazione. [Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

[Distribuire dispositivi aggiunti ad Azure AD ibridi usando Intune e Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
