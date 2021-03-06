---
title: Domande frequenti per Microsoft Endpoint Configuration Manager
titleSuffix: Configuration Manager
description: Domande frequenti su Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0b59ffa73bb2c7524f2eed29326f238d856adef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699314"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Domande frequenti per Microsoft Endpoint Configuration Manager

*Si applica a: Configuration Manager (Current Branch, Technical Preview Branch)*

A partire dalla versione 1910, Configuration Manager è incluso in Microsoft Endpoint Manager. Questo articolo include le risposte alla domande frequenti su questo strumento.

## <a name="summary"></a>Riepilogo

Per iniziare, guardare questo video di due minuti di Brad Anderson, vicepresidente di Microsoft, per Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>Domande frequenti

### <a name="what-is-microsoft-endpoint-manager"></a>Che cosè Microsoft Endpoint Manager?

Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft riunisce Configuration Manager e Intune con una gestione delle licenze semplificata. L'investimento esistente in Configuration Manager continua a essere valido e consente al contempo di sfruttare i vantaggi offerti dalla potenza del cloud Microsoft.

Le soluzioni di gestione Microsoft seguenti fanno ora parte del marchio **Microsoft Endpoint Manager**:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Altre funzionalità della [console di amministrazione della gestione dei dispositivi](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Per altre informazioni, vedere i post seguenti di Brad Anderson, vicepresidente di Microsoft, per Microsoft 365:

- [Post di blog sull'annuncio](https://aka.ms/cmannounce)
- [Documento sulla visione](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Che cosa cambia in Configuration Manager con l'introduzione di Microsoft Endpoint Manager?

Nella versione 1910, a parte il nuovo nome, Configuration Manager funziona allo stesso modo.

In particolare, i nomi delle cartelle del menu Start sono state cambiate per i componenti comuni, ad esempio [Console di Configuration Manager](../servers/manage/admin-console.md#bkmk_open) e [Software Center](software-center.md#bkmk_open).

### <a name="how-do-we-refer-to-the-product-now"></a>Qual è il nome usato ora per fare riferimento al prodotto?

- Quando si fa riferimento all'intera soluzione che include tutti i componenti: **Microsoft Endpoint Manager**

- Quando si fa riferimento al componente locale:
  - La prima volta, usare il nome completo del marchio: **Microsoft Endpoint Configuration Manager**
  - Per un uso generale: **Configuration Manager**
  - Per un uso vincolato allo spazio: **ConfigMgr**, solo in istanze in cui il nome usato in generale è troppo lungo

### <a name="are-there-any-licensing-changes"></a>Sono state apportate modifiche alle licenze?

Sì. Come annunciato in occasione di Microsoft Ignite 2019, se si dispone di una licenza per Configuration Manager, si può usufruire anche di una licenza per Intune per la [co-gestione](../../comanage/overview.md) dei PC Windows. Per altre informazioni, vedere [Domande frequenti su prodotto e licenze](product-and-licensing-faq.md#bkmk_mem).

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>Perché in alcuni casi compare ancora "System Center Configuration Manager"?

L'applicazione globale di modifiche a prodotti, servizi e materiali di supporto, come la documentazione, richiede tempo.

Alcuni componenti fondamentali possono anche non cambiare mai. Il principale servizio Windows nei server del sito è ancora **SMS_Executive**. Il repository GitHub che supporta questa documentazione continuerà a essere **SCCMDocs**.

## <a name="next-steps"></a>Passaggi successivi

Leggere l'articolo [Novità delle versioni incrementali di Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)