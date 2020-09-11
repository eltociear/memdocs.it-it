---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644266"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Non è possibile creare o modificare alcune raccolte

<!--6197183-->
In questa versione del ramo Technical Preview non è possibile creare una nuova raccolta. Non è inoltre possibile modificare le proprietà di una raccolta di utenti esistente.

Per risolvere questo problema, usare i cmdlet di PowerShell di Configuration Manager per creare nuove raccolte e modificare le raccolte di utenti esistenti. Di seguito sono riportati alcuni dei cmdlet disponibili per la gestione delle raccolte:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)