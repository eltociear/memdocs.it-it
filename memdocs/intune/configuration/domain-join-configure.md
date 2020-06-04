---
title: Impostazioni del profilo di aggiunta al dominio per Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Creare un profilo di configurazione del dispositivo per l'aggiunta a un dominio per i dispositivi aggiunti ad Azure AD ibridi. Usare questo profilo per distribuire informazioni sul dominio Active Directory locale ai dispositivi di cui viene effettuato il provisioning con Windows Autopilot e Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 211722a02183d3b86525468f907d4093331d9de6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988421"
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

    - **Piattaforma**: selezionare **Windows 10 e versioni successive**.
    - **Profilo**: selezionare **Aggiunta a un dominio (anteprima)** .

4. Selezionare **Crea**.
5. In **Informazioni di base** immettere le proprietà seguenti:

    - **Nome**: immettere un nome descrittivo per il criterio. Assegnare ai criteri nomi che possano essere identificati facilmente in un secondo momento. Ad esempio, un nome di criterio valido è **Windows 10: Profilo di aggiunta al dominio che include informazioni sul dominio locale per registrare dispositivi aggiunti ad AD ibridi con Windows Autopilot**.
    - **Descrizione**: immettere una descrizione del criterio. Questa impostazione è facoltativa ma consigliata.

6. Selezionare **Avanti**.
7. In **Impostazioni di configurazione** immettere le proprietà seguenti:

    - **Prefisso nome computer**: immettere un prefisso per il nome del dispositivo. I nomi dei computer hanno una lunghezza di 15 caratteri. Dopo il prefisso, i 15 caratteri rimanenti vengono generati in modo casuale.
    - **Nome di dominio**: immettere il nome di dominio completo (FQDN) a cui aggiungere i dispositivi. Immettere ad esempio `americas.corp.contoso.com.`
    - **Unità organizzativa** (facoltativo): immettere il percorso completo ([nome distinto](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) per l'unità organizzativa (OU) in cui devono essere creati gli account computer. Immettere ad esempio `"CN=Users,DC=Contoso,DC=com"`. Se non si immette un valore, viene usato un contenitore di oggetti computer noto.

      Per ulteriori informazioni e consigli su questa impostazione, vedere [Distribuire dispositivi aggiunti ad Azure AD ibridi](../enrollment/windows-autopilot-hybrid.md).

8. Selezionare **Avanti**.

9. In **Tag ambito** (facoltativo) assegnare un tag per filtrare il profilo a gruppi IT specifici, ad esempio `US-NC IT Team` o `JohnGlenn_ITDepartment`. Per altre informazioni sui tag di ambito, vedere [Usare il controllo degli accessi in base al ruolo (RBAC) e i tag di ambito per l'infrastruttura IT distribuita](../fundamentals/scope-tags.md).

    Selezionare **Avanti**.

10. In **Assegnazioni** selezionare gli utenti o il gruppo utente che riceveranno il profilo. Per altre informazioni sull'assegnazione di profili, vedere [Assegnare profili utente e dispositivo](device-profile-assign.md).

    Selezionare **Avanti**.

11. In **Rivedi e crea** rivedere le impostazioni. Quando si seleziona **Crea**, le modifiche vengono salvate e il profilo viene assegnato. Il criterio viene visualizzato anche nell'elenco dei profili.

Si è ora pronti per [distribuire dispositivi aggiunti ad Azure AD ibridi usando Intune e Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo l'[assegnazione](device-profile-assign.md) del profilo, [monitorarne lo stato](device-profile-monitor.md).

[Distribuire dispositivi aggiunti ad Azure AD ibridi usando Intune e Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
