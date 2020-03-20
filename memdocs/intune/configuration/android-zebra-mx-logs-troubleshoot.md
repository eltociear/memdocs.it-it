---
title: Usare i log StageNow nei dispositivi Android Zebra in Microsoft Intune - Azure | Microsoft Docs
description: Informazioni sui problemi comuni e relative soluzioni quando si usa StageNow nei dispositivi Android con Microsoft Intune. Viene anche illustrato come ottenere i log e sono riportati esempi di come leggere i log per informazioni su operazioni riuscite o errori.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8c7c60b4d9d1831aaabb9886345865234ce6351
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364617"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Risolvere e individuare i potenziali problemi relativi ai dispositivi Android Zebra in Microsoft Intune



In Microsoft Intune è possibile usare [Zebra Mobility Extensions (MX) per gestire i dispositivi Android Zebra](android-zebra-mx-overview.md). Quando si usano i dispositivi Zebra, è possibile creare i profili in StageNow per gestire le impostazioni e caricarle in Intune. Intune usa l'app StageNow per applicare le impostazioni nei dispositivi. L'app StageNow crea anche un file di log dettagliato nel dispositivo usato per la risoluzione dei problemi.

Questa funzionalità si applica a:

- Android

Ad esempio, è possibile creare un profilo in StageNow per configurare un dispositivo. Quando si crea il profilo StageNow, l'ultimo passaggio genera un file per il test del profilo. Questo file viene utilizzato con l'app StageNow nel dispositivo.

In un altro esempio, è possibile creare un profilo in StageNow e testarlo. In Intune si aggiunge il profilo StageNow, quindi lo si assegna ai dispositivi Zebra. Quando si controlla lo stato del profilo assegnato, il profilo mostra informazioni di stato di alto livello.

In entrambi i casi, è possibile ottenere altri dettagli dal file di log StageNow, che viene salvato nel dispositivo ogni volta che viene applicato un profilo StageNow.

Alcuni problemi non sono correlati al contenuto del profilo StageNow e non vengono rispecchiati nei log.

Questo articolo illustra come leggere i log di StageNow ed elenca alcuni altri problemi potenziali con i dispositivi Zebra che potrebbero non essere indicati nei log.

Per altre informazioni su questa funzionalità, vedere [Usare e gestire i dispositivi Zebra con Zebra Mobility Extensions](android-zebra-mx-overview.md).

## <a name="get-the-logs"></a>Ottenere i log

### <a name="use-the-stagenow-app-on-the-device"></a>Usare l'app StageNow nel dispositivo
Quando si esegue il test di un profilo direttamente usando StageNow nel computer, invece di usare [Intune per distribuire il profilo](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow), l'app StageNow nel dispositivo salva i log dal test. Per ottenere il file di log, usare l'opzione **More (...)** (Altro) nell'app StageNow del dispositivo.

### <a name="get-logs-using-android-debug-bridge"></a>Ottenere i log con Android Debug Bridge
Per ottenere i log dopo che il profilo è già stato distribuito con Intune, connettere il dispositivo a un computer con [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) (viene aperto il sito Web di Android).

Nel dispositivo i log vengono salvati in `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>Ottenere i log tramite posta elettronica
Per ottenere i log dopo che il profilo è già stato distribuito con Intune, gli utenti finali possono inviare i log con un messaggio di posta elettronica usando un'app di posta elettronica nel dispositivo. Nel dispositivo Zebra aprire l'app Portale aziendale e [inviare i log](https://docs.microsoft.com/user-help/send-logs-to-your-it-admin-by-email-android). L'uso della funzionalità di invio dei log crea anche un ID di evento imprevisto PowerLift, a cui è possibile fare riferimento se si contatta il supporto tecnico Microsoft.

## <a name="read-the-logs"></a>Leggere i log

Quando si esaminano i log, è presente un errore ogni volta che compare il tag `<characteristic-error>`. I dettagli dell'errore vengono scritti nella proprietà `desc` del tag `<parm-error>`.

## <a name="error-types"></a>Tipi di errore

I dispositivi Zebra includono diversi livelli di segnalazione degli errori:

- Il CSP non è supportato nel dispositivo. Ad esempio, il dispositivo non è un dispositivo cellulare e non ha un gestore di rete cellulare.
- La versione di MX o OSX non corrisponde. Ogni CSP ha una versione. Per una matrice di supporto completa, vedere la [documentazione di Zebra](http://techdocs.zebra.com/mx/) (viene aperto il sito Web di Zebra).
- Il dispositivo segnala un altro problema o errore.

## <a name="examples"></a>Esempi

Si supponga, ad esempio, che sia presente il profilo di input seguente:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

Nel log, il codice XML è identico all'input. Questo output corrispondente indica che il profilo è stato applicato correttamente al dispositivo senza errori:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

In un altro esempio, l'input è il seguente:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

Il log mostra un errore, in quanto contiene un tag `<characteristic-error>`. In questo scenario, il profilo ha tentato di installare un pacchetto Android (APK) che non esiste nel percorso specificato:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Altri potenziali problemi con i dispositivi Zebra

Questa sezione elenca altri possibili problemi che possono verificarsi quando si usano dispositivi Zebra con l'amministratore del dispositivo. Questi problemi non vengono segnalati nei log di StageNow.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView non aggiornato

Quando i dispositivi meno recenti effettuano l'accesso con l'app Portale aziendale, gli utenti potrebbero visualizzare un messaggio che indica che il componente WebView di sistema non è aggiornato e deve essere aggiornato. Se nel dispositivo è installato Google Play, connetterlo a Internet e verificare la disponibilità di aggiornamenti. Se il dispositivo non ha Google Play installato, ottenere la versione aggiornata del componente e applicarla ai dispositivi. In alternativa, eseguire l'aggiornamento al sistema operativo più recente del dispositivo rilasciato da Zebra.

### <a name="management-actions-take-a-long-time"></a>Le azioni di gestione richiedono molto tempo

Se i servizi Google Play non sono disponibili, il completamento di alcune attività potrebbe richiedere fino a 8 ore. In [Limitazioni dell'app Portale aziendale di Intune per Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (viene aperto un altro sito Web Microsoft) sono disponibili informazioni utili.

### <a name="device-spoofing-suspected-shows-in-intune"></a>In Intune viene visualizzato il messaggio "Sospetto spoofing del dispositivo"

Questo errore indica che Intune sospetta che un dispositivo Android non Zebra stia segnalando il modello e il produttore come dispositivo Zebra.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>La versione dell'app Portale aziendale è precedente alla versione minima richiesta

Intune può aggiornare la versione minima richiesta dell'app Portale aziendale. Se Google Play non è installato nel dispositivo, l'app Portale aziendale non viene aggiornata automaticamente. Se la versione minima richiesta è più recente della versione installata, l'app Portale aziendale smette di funzionare. Eseguire l'aggiornamento all'app Portale aziendale più recente usando il [sideload nei dispositivi Zebra](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Passaggi successivi

[Aree discussione di Zebra](https://developer.zebra.com/community/home/discussions) (viene aperto il sito Web di Zebra)

[Usare e gestire dispositivi Zebra con Mobility Extensions di Zebra in Intune](android-zebra-mx-overview.md)
