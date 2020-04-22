---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692099"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Non è possibile creare o modificare alcune raccolte

<!--6197183-->
In questa versione del ramo Technical Preview non è possibile creare una nuova raccolta. Non è inoltre possibile modificare le proprietà di una raccolta di utenti esistente.

Per risolvere questo problema, usare i cmdlet di PowerShell di Configuration Manager per creare nuove raccolte e modificare le raccolte di utenti esistenti. Di seguito sono riportati alcuni dei cmdlet disponibili per la gestione delle raccolte:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
