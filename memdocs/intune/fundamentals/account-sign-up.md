---
title: Iscriversi o accedere a Microsoft Intune
description: Come iscriversi per ottenere una sottoscrizione di Microsoft Intune o eseguire l'accesso per iniziare a usare la sottoscrizione.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31cc746edce40300b5678439550ce3108270750d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988877"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Iscriversi o accedere a Microsoft Intune

Questo argomento descrive come gli amministratori iscriversi per ottenere un account Intune.

Prima di iscriversi a Intune, verificare se si ha già un account Microsoft Online Services, un contratto Enterprise o un contratto multilicenza equivalente. Un contratto multilicenza Microsoft o un'altra sottoscrizione dei servizi cloud Microsoft, ad esempio Office 365, include in genere un account aziendale o dell'istituto di istruzione.

Se si ha già un account aziendale o dell'istituto di istruzione, **eseguire l'accesso** con tale account e aggiungere Intune alla sottoscrizione. In alternativa, è possibile **iscriversi** per ottenere un nuovo account e usare Intune per l'organizzazione.

>[!WARNING]
>Non è possibile combinare un account aziendale o dell'istituto di istruzione dopo essersi iscritti per ottenere un nuovo account.

## <a name="how-to-sign-up-for-intune"></a>Come iscriversi a Intune

1. Visitare la pagina di [iscrizione a Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20).

   ![Screenshot della pagina Web di iscrizione per l'account di prova Microsoft Intune](./media/account-sign-up/account-sign-up-site.png)

2. Nella pagina Iscrizione accedere o eseguire l'iscrizione per la gestione di una nuova sottoscrizione a Intune.

## <a name="post-sign-up-considerations"></a>Considerazioni successive all'iscrizione

Dopo avere eseguito l'iscrizione per una nuova sottoscrizione, all'indirizzo di posta elettronica specificato in fase di iscrizione viene inviato un messaggio contenente le informazioni sul proprio account. Questo messaggio conferma che la sottoscrizione è attiva.

Dopo aver completato il processo di iscrizione, si viene indirizzati all'interfaccia di amministrazione di Microsoft 365, usata per aggiungere utenti e assegnare loro licenze. Se si hanno esclusivamente account basati su cloud che usano il nome di dominio onmicrosoft.com predefinito, è quindi possibile proseguire per aggiungere utenti e assegnare loro licenze. Tuttavia, se si prevede di usare il [nome di dominio personalizzato](custom-domain-name-configure.md) dell'organizzazione o di [sincronizzare le informazioni sull'account utente](users-add.md#sync-active-directory-and-add-users-to-intune) da Active Directory locale, è possibile chiudere la finestra del browser.

## <a name="sign-in-to-microsoft-intune"></a>Accedere a Microsoft Intune

Dopo l'iscrizione a Intune, è possibile usare qualsiasi dispositivo con un [browser supportato](supported-devices-browsers.md#intune-supported-web-browsers) per accedere a [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) e amministrare il servizio.

Per impostazione predefinita, l'account deve avere una delle autorizzazioni seguenti in Azure AD:

- Amministratore globale
- Amministratore del servizio Intune (noto anche come amministratore di Intune)

Per concedere l'accesso per amministrare il servizio per gli utenti con altre autorizzazioni, vedere quindi [Controllo degli accessi in base al ruolo](role-based-access-control.md)

### <a name="intune-admin-portal-url"></a>URL del portale di amministrazione di Intune

Interfaccia di amministrazione di Microsoft Endpoint Manager: https://endpoint.microsoft.com

Intune nel portale di Azure: https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade

Intune per Education: https://intuneeducation.portal.azure.com

Portale classico di Intune: https://manage.microsoft.com Il portale classico di Intune viene usato solo per gestire i dispositivi registrati con il client software per PC di Intune

### <a name="urls-for-intune-services-provided-by-office-365"></a>URL per i servizi di Intune offerti da Office 365

Microsoft 365 Business: https://portal.microsoft.com/adminportal

Gestione dispositivi mobili per Office 365: https://admin.microsoft.com/adminportal/home#/MifoDevices

## <a name="see-also"></a>Vedere anche

[Impossibile accedere a Office 365, Azure o Intune](https://support.microsoft.com/help/2412085)
