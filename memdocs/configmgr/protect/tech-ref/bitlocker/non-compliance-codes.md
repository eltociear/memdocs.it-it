---
title: Codici di non conformità
titleSuffix: Configuration Manager
description: Riferimento tecnico per i codici possibili di un client Configuration Manager non conforme ai criteri di BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2cb6c17802319b0d559474fa8ff208346c2811e0
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127934"
---
# <a name="non-compliance-codes"></a>Codici di non conformità

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

WMI sul client fornisce i codici di non conformità seguenti. Inoltre descrive i motivi per cui un determinato dispositivo viene segnalato come non conforme.

Sono disponibili diversi metodi per visualizzare WMI. Ad esempio, usare il seguente comando di PowerShell:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Se il dispositivo è conforme, questo comando non restituisce alcun valore.
>
> È anche possibile controllare l'attributo `Compliant` di questa classe, che è `1` se il dispositivo è conforme.

|Codice di non conformità|Motivo della mancata conformità|
|--- |--- |
|0|Livello di codifica diverso da AES 256.|
|1|I criteri di BitLocker richiedono che questo volume sia crittografato, mentre non lo è.|
|2|I criteri di BitLocker richiedono che questo volume *non* sia crittografato, mentre lo è.|
|3|I criteri di BitLocker richiedono che questo volume usi una protezione TPM, che non è presente.|
|4|I criteri di BitLocker richiedono che questo volume usi una protezione TPM+PIN, che non è presente.|
|5|I criteri di BitLocker non consentono ai computer privi di TPM di creare report conformi.|
|6|Il volume ha una protezione TPM, ma TPM non è visibile.|
|7|I criteri di BitLocker richiedono che questo volume usi una protezione con password, che non è presente.|
|8|I criteri di BitLocker richiedono che questo volume *non* usi una protezione con password, che è invece presente.|
|9|I criteri di BitLocker richiedono che questo volume usi una protezione con sblocco automatico, che non è presente.|
|10|I criteri di BitLocker richiedono che questo volume *non* usi una protezione con sblocco automatico, che è invece presente.|
|11|BitLocker rileva un conflitto di criteri che impedisce la segnalazione del volume come conforme.|
|12|È necessario un volume di sistema per crittografare il volume del sistema operativo, che non è presente.|
|13|La protezione viene sospesa per il volume.|
|14|La protezione con sblocco automatico non è sicura a meno che il volume del sistema operativo non sia crittografato.|
|15|Il criterio richiede un livello di crittografia minimo pari a XTS-AES-128 bit, il livello di crittografia effettivo è meno sicuro.|
|16|Il criterio richiede un livello di crittografia minimo pari a XTS-AES-256 bit, il livello di crittografia effettivo è meno sicuro.|
