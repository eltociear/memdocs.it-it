---
title: Privacy dei dati di Desktop Analytics
titleSuffix: Configuration Manager
description: Desktop Analytics si impegna a proteggere la privacy dei dati dei clienti
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd970dc1517a6fcc197b2bf39a141871b4999a02
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268420"
---
# <a name="desktop-analytics-data-privacy"></a>Privacy dei dati di Desktop Analytics

Desktop Analytics si impegna a fondo per proteggere la privacy dei dati dei clienti, concentrandosi sui principi seguenti:

- **Trasparenza:** gli eventi di diagnostica di Windows sono documentati in modo completo. Esaminarli insieme ai team di sicurezza e conformità dell'azienda. Il visualizzatore dati di diagnostica di Windows consente di visualizzare i dati di diagnostica inviati da un determinato dispositivo. Per altre informazioni, vedere [Panoramica del visualizzatore dati di diagnostica](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Controllo:** è possibile controllare il livello dei dati di diagnostica da condividere con Microsoft. Windows 10 versione 1709 aggiunge nuovi criteri per limitare i dati di diagnostica avanzati al minimo richiesto da Desktop Analytics.  

- **Sicurezza:** Microsoft protegge i dati con sicurezza e crittografia avanzate.  

- **Attendibilità:** Desktop Analytics supporta l'[informativa sulla privacy](https://privacy.microsoft.com/privacystatement) di Microsoft e le [condizioni del servizio online](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  

Per altre informazioni, vedere [Servizi di Windows in cui Microsoft è il responsabile del trattamento secondo il GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Flusso di dati

La figura seguente illustra il flusso dei dati di diagnostica da singoli dispositivi tramite il servizio dati di diagnostica, l'archiviazione temporanea e l'area di lavoro Log Analytics:

![Diagramma che illustra il flusso dei dati di diagnostica dai dispositivi](media/da-data-flow.png)

1. Accedere al portale di Azure ed eseguire l'onboarding a Desktop Analytics. Creare l'app Azure AD per connettersi con Configuration Manager. Quando si configura Desktop Analytics, creare un'area di lavoro di Azure Log Analytics nel percorso scelto.  

2. Connettere Configuration Manager e registrare i dispositivi  

    1. Configurare il servizio cloud Desktop Analytics in Configuration Manager con i dettagli dell'app Azure AD.  

    2. Entro 15 minuti Configuration Manager sincronizza i dati seguenti con Desktop Analytics usando l'ID tenant. Questo processo viene ripetuto ogni ora.

      - Informazioni sulle raccolte di dispositivi necessarie per [creare piani di distribuzione](create-deployment-plans.md). Queste informazioni includono l'ID della raccolta, l'ID della gerarchia, il nome della raccolta e il numero di dispositivi. 
      - Informazioni necessarie per [registrare i dispositivi](enroll-devices.md). Queste informazioni includono l'ID della raccolta, l'identificatore univoco SMS, la versione build del sistema operativo, il nome del dispositivo e il numero di serie.
      - Informazioni dal dashboard [Monitorare l'integrità della connessione](monitor-connection-health.md). Queste informazioni includono il numero di dispositivi per stato di integrità e le proprietà dei dispositivi.
      - Informazioni sui piani di distribuzione, che includono l'ID della raccolta, l'ID di distribuzione, il tipo di distribuzione pilota o di produzione e il numero di dispositivi per decisione di aggiornamento.

    3. Configuration Manager imposta l'ID commerciale, il livello dei dati di diagnostica e altre impostazioni per i dispositivi nella raccolta di destinazione. Questa configurazione specifica i dispositivi da visualizzare nell'area di lavoro di Desktop Analytics.  

    4. Gli aggiornamenti della compatibilità vengono distribuiti a tutti i dispositivi di destinazione.  

3. I dispositivi inviano i dati di diagnostica al servizio di gestione dati di diagnostica di Microsoft per Windows. Questo servizio è ospitato negli Stati Uniti.  

4. Ogni giorno, Microsoft crea uno snapshot delle informazioni dettagliate incentrate sull'IT. Questo snapshot combina i dati di diagnostica di Windows con l'input per i dispositivi registrati. Questo processo avviene nell'archiviazione temporanea, che viene usata solo da Desktop Analytics. L'archiviazione temporanea è ospitata nei data center di Microsoft negli Stati Uniti. Tutti i dati vengono inviati tramite un canale crittografato SSL (HTTPS). Gli snapshot vengono separati in base all'ID commerciale.  

5. Vengono quindi copiati nell'area di lavoro di Azure Log Analytics. Questo trasferimento dei dati avviene tramite HTTPS tramite il protocollo di inserimento del webhook, che è una funzionalità di Log Analytics. Desktop Analytics non ha autorizzazioni di lettura o scrittura per lo spazio di archiviazione di Log Analytics. Desktop Analytics chiama l'API webhook con un URI di firma di accesso condiviso (SAS). Log Analytics ottiene quindi i dati dalle tabelle di archiviazione tramite HTTPS.

6. Desktop Analytics archivia l'input dell'utente nello spazio di archiviazione di Log Analytics. Queste configurazioni includono i piani di distribuzione e le decisioni sulle risorse per l'aggiornamento e l'importanza.  

## <a name="other-resources"></a>Altre risorse

Per le domande frequenti sulla alla privacy per Desktop Analytics, vedere [Domande frequenti sulla privacy](faq.md#privacy).

Per altre informazioni sugli aspetti correlati alla privacy, vedere gli articoli seguenti:

- [Windows 10 e GDPR: informazioni per amministratori IT e decision maker](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Eventi e campi dei dati di diagnostica per i responsabili valutazione di Windows 7, Windows 8 e Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Campi ed eventi di diagnostica Windows livello base per Windows 10, versione 1809](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Campi ed eventi di dati di diagnostica avanzati di Windows 10, versione 1709 usati da Desktop Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Panoramica del visualizzatore dati di diagnostica](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Condizioni di licenza e documentazione](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Sicurezza dei dati di Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Sicurezza e privacy nei data center di Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Fidati del tuo cloud](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro protezione](https://www.microsoft.com/trustcenter)  

- [Privacy Shield](https://www.privacyshield.gov/)  

Separatamente da Desktop Analytics, Configuration Manager invia dati di diagnostica e di utilizzo a Microsoft. Microsoft usa questi dati per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future di Configuration Manager. Per altre informazioni, vedere [Dati di diagnostica e di utilizzo per Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
