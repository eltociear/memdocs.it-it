---
title: Risolvere i problemi relativi a BitLocker
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi relativi alla gestione di BitLocker in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0158738f77a0070835bec2385dd85c42dfd763fd
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127815"
---
# <a name="troubleshoot-bitlocker"></a>Risolvere i problemi relativi a BitLocker

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni contenute in questo articolo per risolvere i problemi relativi alla gestione di BitLocker in Configuration Manager.

## <a name="server-error-in-self-service"></a>Errore del server in self-service

Quando si tenta di aprire il portale self-service (`https://webserver.contoso.com/SelfService`) per la prima volta, viene visualizzato il messaggio di errore seguente:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Per risolvere questo problema, assicurarsi di aver installato il [prerequisito](../../plan-design/bitlocker-management.md#prerequisites) per **Microsoft ASP.NET MVC 4.0** nel server Web.

## <a name="see-also"></a>Vedere anche

Per altre informazioni sull'uso dei registri eventi di BitLocker, vedere [Registri eventi di BitLocker](about-event-logs.md).

Per un elenco degli errori noti e delle possibili cause per le voci del registro eventi, vedere gli articoli seguenti:

- [Registri eventi del client](client-event-logs.md)
- [Registri eventi del server](server-event-logs.md)

Per comprendere il motivo per cui i client risultano non conformi ai criteri di gestione di BitLocker, vedere [Codici di non conformità](non-compliance-codes.md).
