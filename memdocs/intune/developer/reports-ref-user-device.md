---
title: Associazione utente-dispositivo nel data warehouse di Intune
titleSuffix: Microsoft Intune
description: L'entità UserDeviceAssociation contiene le associazioni utente-dispositivo presenti nell'organizzazione.
keywords: Data warehouse di Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6127b365a04ad48a9cbaa98bdef821c4d1334181
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339891"
---
# <a name="reference-for-user-device-association-entity"></a>Riferimento per l'entità dell'associazione utente-dispositivo

L'entità **userDeviceAssociation** contiene le associazioni utente-dispositivo presenti nell'organizzazione.

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Nome        |                                           Descrizione                                            |        Esempio         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Identificatore univoco dell'utente nel data warehouse (chiave sostitutiva).               |          123           |
|     deviceKey      |                      Identificatore univoco del dispositivo nel data warehouse.                      |          123           |
| createdDateTimeUTC |           Data e ora della creazione dell'associazione utente-dispositivo. Viene usato il formato UTC.           | 23/11/2016 12.00.00 |
|     isDeleted      | Indica che l'utente ha annullato la registrazione del dispositivo e che l'associazione non è più aggiornata. |       True/False       |
|  endedDateTimeUTC  |              Data e ora in formato UTC in cui IsDeleted è stato impostato su <strong>True</strong>.               | 23/06/2017 12.00.00 |

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sul [data warehouse di Intune](reports-nav-create-intune-reports.md).
