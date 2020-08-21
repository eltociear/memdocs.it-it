---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704154"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Non è possibile creare o modificare alcune raccolte

<!--6197183-->
In questa versione del ramo Technical Preview non è possibile creare una nuova raccolta. Non è inoltre possibile modificare le proprietà di una raccolta di utenti esistente.

Per risolvere questo problema, usare i cmdlet di PowerShell di Configuration Manager per creare nuove raccolte e modificare le raccolte di utenti esistenti. Di seguito sono riportati alcuni dei cmdlet disponibili per la gestione delle raccolte:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)