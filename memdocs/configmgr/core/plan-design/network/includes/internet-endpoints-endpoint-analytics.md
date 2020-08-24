---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126462"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Endpoint necessari per i dispositivi gestiti da Configuration Manager

I dispositivi gestiti da Configuration Manager inviano i dati a Intune tramite il connettore sul ruolo Configuration Manager e non hanno bisogno di accedere direttamente al cloud pubblico Microsoft.

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://graph.windows.net` | Usato per recuperare automaticamente le impostazioni quando si connette la gerarchia ad Analisi degli endpoint per il ruolo del server di Configuration Manager. Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare la raccolta di dispositivi e i dispositivi con Analisi degli endpoint solo per il ruolo del server di Configuration Manager. Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="endpoints-required-for-intune-managed-devices"></a>Endpoint necessari per i dispositivi gestiti da Intune

Per registrare i dispositivi per Analisi degli endpoint, è necessario inviare i dati funzionali richiesti al cloud pubblico Microsoft. Per raccogliere i dati dai dispositivi gestiti da Intune, l'analisi degli endpoint usa le esperienze utente connesse a Windows 10 e Windows Server e i componenti di telemetria (DiagTrack). Assicurarsi che il servizio **Esperienze utente connesse e telemetria** nel dispositivo sia in esecuzione.

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Usato dai dispositivi gestiti da Intune per inviare i [dati funzionali richiesti](../../../../../analytics/data-collection.md#bkmk_datacollection) all'endpoint di raccolta dati di Intune. |
