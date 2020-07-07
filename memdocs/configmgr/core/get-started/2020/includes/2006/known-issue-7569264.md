---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590534"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a> L'autenticazione di Azure AD non funziona
<!--7569264-->
L'uso di Configuration Manager del servizio token di sicurezza di Azure Active Directory (Azure AD) non funziona. Il file **CCM_STS.log** nel punto di gestione contiene una voce simile all'errore seguente: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` Include anche HRESULT 0x80131040.

Un altro sintomo sono problemi relativi a Cloud Management Gateway (CMG). Se si esegue l'analizzatore della connessione a Cloud Management Gateway, il test del canale CMG per il punto di gestione non riesce con l'errore seguente: `Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Questo problema è dovuto a una discrepanza della versione con una libreria di supporto.

Per risolvere il problema, copiare **System.IdentityModel.Tokens.JWT.dll** dalla cartella \bin\X64 della directory di installazione nel server del sito alla cartella SMS_CCM\CCM_STS\bin nel punto di gestione.
