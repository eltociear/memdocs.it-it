---
title: User - Data warehouse di Intune
titleSuffix: Microsoft Intune
description: Argomento di riferimento per la categoria User delle raccolte di entità nell'API data warehouse di Intune.
keywords: Data warehouse di Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: C29A6EEA-72B7-427E-9601-E05B408F3BB0
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c8cab6eb85e8b3f68b7c2cf7ab2cd998e619e51
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165108"
---
# <a name="reference-for-user-entity"></a>Informazioni di riferimento per l'entità User

La categoria **Users** contiene l'entità **user** che definisce le proprietà utente nel modello di dati.

## <a name="users"></a>user

L'entità **user** elenca tutti gli utenti di Azure Active Directory (Azure AD) con licenze assegnate nell'organizzazione.

La raccolta di entità **user** contiene i dati utente. In questi record sono inclusi gli stati utente registrati nel periodo di raccolta dei dati, anche se l'utente è stato rimosso. Nel corso dell'ultimo mese, ad esempio, è possibile che un utente sia stato aggiunto e rimosso da Intune. Se anche l'utente non è presente al momento del report, l'utente e lo stato sono comunque presenti nei dati del mese precedente. In questo caso, è possibile creare un report che mostri la durata della presenza storica dell'utente nei dati.

|          Proprietà          |                                                                                                           Descrizione                                                                                                          |                Esempio               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Identificatore univoco dell'utente nel data warehouse - chiave surrogata.                                                                                                                                                         | 123                                  |
| userId                     | Identificatore univoco dell'utente, simile a UserKey, ma è una chiave naturale.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| userEmail                  | Indirizzo di posta elettronica dell'utente.                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | UPN dell'utente.                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Nome visualizzato dell'utente.                                                                                                                                                                                                      | Luca                                 |
| intuneLicensed             | Specifica se l'utente ha una licenza per Intune.                                                                                                                                                                              | True/False                           |
| isDeleted                  | Indica se tutte le licenze dell'utente sono scadute e se l'utente è stato pertanto rimosso da Intune. Per un singolo record, questo flag non cambia. Per un nuovo stato utente viene creato invece un nuovo record. | True/False                           |
| RowLastModifiedDateTimeUTC | Data e ora in formato UTC dell'ultima modifica del record nel data warehouse                                                                                                                                                 | 23/11/2016 0:00                      |


## <a name="next-steps"></a>Passaggi successivi
- È possibile usare la raccolta di entità **Current User** per limitare i dati agli utenti attualmente attivi. Per altre informazioni, vedere [Informazioni di riferimento per l'entità Current User](reports-ref-data-model.md).
- Per altre informazioni su come il data warehouse controlla la durata di un utente in Intune, vedere [Rappresentazione della durata degli utenti nel data warehouse di Intune](reports-ref-user-timeline.md).
