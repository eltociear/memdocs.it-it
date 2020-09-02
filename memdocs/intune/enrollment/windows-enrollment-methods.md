---
title: Metodi di registrazione di Intune per dispositivi Windows
titleSuffix: Microsoft Intune
description: Informazioni sui diversi metodi in cui è possibile registrare dispositivi Windows in Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: ''
ms.openlocfilehash: c91c0f776ee46ddebbbb7bc27895b0f8795ae975
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911591"
---
# <a name="intune-enrollment-methods-for-windows-devices"></a>Metodi di registrazione di Intune per dispositivi Windows

Per gestire i dispositivi in Intune, questi devono essere prima di tutto registrati nel servizio Intune. Sia i dispositivi personali sia quelli di proprietà aziendale possono essere registrati per la gestione di Intune. 

Esistono due metodi per registrare i dispositivi in Intune:
- Gli utenti possono registrare personalmente i propri PC Windows 
- Gli amministratori possono configurare criteri per forzare la registrazione automatica senza alcun coinvolgimento dell'utente

## <a name="user-self-enrollment-in-intune"></a>Registrazione da parte dell'utente in Intune

Gli utenti possono registrare personalmente il proprio dispositivo Windows usando uno di questi metodi:

- [Bring Your Own Device (BYOD)](../user-help/enroll-windows-10-device.md): Gli utenti registrano i propri dispositivi personali scaricando e installando l'**app Portale aziendale**. Questo processo:
  - Registra il dispositivo con Azure Active Directory per poter accedere a risorse aziendali come la posta elettronica.
  - Registra il dispositivo in Intune come dispositivo personale (BYOD).
Se un amministratore ha configurato la registrazione automatica (disponibile con sottoscrizioni di Azure AD premium), l'utente deve immettere le credenziali solo una volta. In caso contrario, l'utente dovrà eseguire la registrazione separatamente tramite la registrazione solo MDM e immettere di nuovo le credenziali.  
- **Registrazione solo MDM**: permette agli utenti di registrare un PC aggiunto a un gruppo di lavoro, ad Active Directory o ad Azure Active Directory in Intune. Gli utenti eseguono la registrazione da Impostazioni nel PC Windows esistente. Questo metodo non è consigliato, in quanto non registra il dispositivo in Azure Active Directory. Impedisce anche l'uso di funzionalità come l'accesso condizionale.
- [Aggiunta ad Azure Active Directory (Azure AD)](/azure/active-directory/user-help/user-help-join-device-on-network) - Aggiunge il dispositivo ad Azure Active Directory e permette agli utenti di accedere a Windows con le proprie credenziali di Azure AD. Se è abilitata la registrazione automatica, il dispositivo viene registrato automaticamente in Intune. Il vantaggio della registrazione automatica è che si tratta di un processo a un solo passaggio per l'utente. In caso contrario, l'utente dovrà eseguire la registrazione separatamente tramite la registrazione solo MDM e immettere di nuovo le credenziali. Gli utenti eseguono la registrazione in questo modo durante la Configurazione iniziale di Windows o da Impostazioni. Il dispositivo viene contrassegnato come dispositivo di proprietà aziendale in Intune.
- [AutoPilot](../../autopilot/enrollment-autopilot.md): automatizza l'aggiunta ad Azure AD e registra nuovi dispositivi di proprietà aziendale in Intune. Questo metodo semplifica la Configurazione guidata ed elimina la necessità di applicare le immagini personalizzate del sistema operativo nei dispositivi. Quando gli amministratori usano Intune per gestire i dispositivi AutoPilot, possono gestire criteri, profili, app e altro ancora dopo la registrazione.  Esistono quattro tipi di distribuzione Autopilot: [Modalità di distribuzione automatica](/windows/deployment/windows-autopilot/self-deploying) (per chioschi multimediali, segnaletica digitale o un dispositivo condiviso), [modalità definita dall'utente](/windows/deployment/windows-autopilot/user-driven) (per gli utenti tradizionali), [White Glove](/windows/deployment/windows-autopilot/white-glove) consente ai partner o al personale IT di eseguire il pre-provisioning di un PC Windows 10 in modo che sia completamente configurato e pronto per le attività aziendali e [Autopilot per i dispositivi esistenti](/windows/deployment/windows-autopilot/existing-devices) consente di distribuire facilmente la versione più recente di Windows 10 nei dispositivi esistenti.

## <a name="administrator-based-enrollment-in-intune"></a>Registrazione basata sull'amministratore in Intune

Gli amministratori possono configurare i metodi di registrazione seguenti, che non richiedono alcuna interazione da parte dell'utente:

- [Aggiunta ad Azure AD ibrido](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy): permette agli amministratori di configurare criteri di gruppo di Active Directory per registrare automaticamente i dispositivi aggiunti ad Azure AD ibrido.
- [Co-gestione di Configuration Manager](/configmgr/comanage/overview): permette agli amministratori di registrare i propri dispositivi esistenti gestiti con Configuration Manager in Intune per ottenere tutti i vantaggi di Intune e Configuration Manager.
- [Manager di registrazione dispositivi](device-enrollment-manager-enroll.md): account di servizio speciale. Gli account manager di registrazione dispositivi hanno autorizzazioni che permettono agli utenti di registrare e gestire più dispositivi di proprietà aziendale. Questi tipi di dispositivi sono ideali per app POS o di utilità, ad esempio, ma non sono adatti per gli utenti che devono accedere alla posta elettronica o alle risorse aziendali. Questo metodo non consente l'uso di funzionalità come l'accesso condizionale. 
- [Registrazione in blocco](windows-bulk-enroll.md): permette a un utente non autorizzato di aggiungere un numero elevato di nuovi dispositivi di proprietà aziendale ad Azure Active Directory e Intune. Creare un pacchetto di provisioning con l'app Progettazione configurazione di Windows. Usando quindi supporti USB durante la Configurazione guidata di Windows iniziale o da un PC Windows esistente, installare il pacchetto di provisioning per registrare automaticamente i dispositivi in Intune. Questo metodo non consente l'uso dell'accesso condizionale.
- La [registrazione di dispositivi Windows IoT Core](/windows/iot-core/manage-your-device/intunedeviceenrollment) viene effettuata usando il Dashboard Windows IoT Core per preparare il dispositivo e quindi usando Progettazione configurazione di Windows per creare un pacchetto di provisioning. Quindi, con un supporto di scheda SD durante l'avvio iniziale, viene installato il pacchetto di provisioning per registrare automaticamente i dispositivi in Intune.

## <a name="next-steps"></a>Passaggi successivi

[Informazioni sulle funzionalità dei metodi di registrazione di Windows](enrollment-method-capab.md)