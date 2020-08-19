---
title: Requisiti di rete di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sui requisiti di rete per la distribuzione di Windows Autopilot.
keywords: MDM, installazione, Windows, Windows 10, OOBE, gestione, distribuzione, Autopilot, ZTD, zero-touch, partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 18031ff51e8086d29f706110946adeacb63d908e
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88590905"
---
# <a name="windows-autopilot-networking-requirements"></a>Requisiti di rete di Windows Autopilot

**Si applica a: Windows 10**

Windows Autopilot dipende da un'ampia gamma di servizi basati su Internet. Per il corretto funzionamento di Autopilot è necessario fornire l'accesso a questi servizi. Nel caso più semplice, l'abilitazione della funzionalità appropriata può essere eseguita garantendo le condizioni seguenti:

- Verificare la risoluzione dei nomi DNS (Domain Name Services) per i nomi DNS Internet
- Consentire l'accesso a tutti gli host tramite la porta 80 (HTTP), 443 (HTTPS) e 123 (UDP/NTP)

Potrebbe essere necessaria una configurazione aggiuntiva per concedere l'accesso ai servizi richiesti in ambienti che:
- hanno accesso a Internet più restrittivo.
- richiedere l'autenticazione prima di poter ottenere l'accesso a Internet. 

> [!NOTE]
> La smart card e l'autenticazione basata su certificato non sono supportate durante la configurazione guidata. Per altre informazioni, vedere [Smart Card e autenticazione basata su certificati](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

Per ulteriori informazioni su ciascuno di questi servizi e sui requisiti specifici, esaminare i dettagli seguenti:

<table><th>Servizio<th>Informazioni
<tr><td><b>Servizio di distribuzione di Windows Autopilot<b><td>Dopo la connessione di rete, ogni dispositivo Windows 10 contatterà il servizio di distribuzione di Windows Autopilot. Con Windows 10 versione 1903 e successive, vengono usati gli URL seguenti: https://ztd.dds.microsoft.com https://cs.dds.microsoft.com . <br>

<tr><td><b>Attivazione di Windows<b><td>Windows Autopilot richiede i servizi di attivazione Windows. Per informazioni dettagliate sugli URL che devono essere accessibili per i servizi di attivazione, vedere l' <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">attivazione di Windows o la convalida non riesce con codice di errore 0x8004FE33</a>.<br>

<tr><td><b>Azure Active Directory<b><td>Le credenziali utente vengono convalidate da Azure Active Directory e il dispositivo può anche essere aggiunto al Azure Active Directory. Per altre informazioni, vedere <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">indirizzo IP di Office 365 e servizio Web URL</a>.
<tr><td><b>Intune<b><td>Una volta autenticato, Azure Active Directory attiverà la registrazione del dispositivo nel servizio di gestione di dispositivi mobili (MDM) di Intune. Per informazioni dettagliate sui requisiti di comunicazione di rete: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">requisiti di configurazione di rete di Intune e larghezza di banda</a>, vedere il collegamento seguente.
<tr><td><b>Windows Update<b><td>Durante il processo OOBE e dopo la configurazione del sistema operativo Windows 10, il servizio Windows Update recupera gli aggiornamenti necessari. Se si verificano problemi di connessione a Windows Update, vedere <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">come risolvere i problemi di connessione relativi Windows Update o Microsoft Update</a>.<br>

Se Windows Update è inaccessibile, il processo Autopilot continuerà, ma gli aggiornamenti critici non saranno disponibili.

<tr><td><b>Ottimizzazione recapito<b><td>Autopilot Contatta il servizio di <a href="https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization">Ottimizzazione recapito</a> durante il download delle app e degli aggiornamenti. Questo contatto stabilisce la condivisione peer-to-peer del contenuto, in modo che solo pochi dispositivi debbano scaricarlo da Internet.
- Aggiornamenti - di Windows Microsoft Store app e aggiornamenti delle app di - Office aggiornamenti di Intune app - Win32<br>

Se il servizio di ottimizzazione recapito è inaccessibile, il processo Autopilot continuerà comunque con i download dell'ottimizzazione del recapito dal cloud (senza peer-to-peer).

<tr><td><b>Sincronizzazione NTP (Network Time Protocol)<b><td>Quando un dispositivo Windows viene avviato, viene parlato con un server di tempo di rete per assicurarsi che l'ora del dispositivo sia corretta. Verificare che la porta UDP 123 per time.windows.com sia accessibile.
<tr><td><b>DNS (Domain Name Services)<b><td>Per risolvere i nomi DNS per tutti i servizi, il dispositivo comunica con un server DNS, in genere fornito tramite DHCP. Questo server DNS deve essere in grado di risolvere i nomi Internet.
<tr><td><b>Dati di diagnostica<b><td>A partire da Windows 10, 1903, la raccolta dei dati di diagnostica verrà abilitata per impostazione predefinita. Per disabilitare Windows Analytics e le funzionalità di diagnostica correlate, vedere <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">gestire il livello di dati di diagnostica aziendali</a>.<br>

Se non è possibile inviare i dati di diagnostica, il processo Autopilot continua comunque. Tuttavia, i servizi che dipendono dai dati di diagnostica, ad esempio Windows Analytics, non funzioneranno.
<tr><td><b>Indicatore stato connettività di rete<b><td>Windows deve essere in grado di indicare che il dispositivo può accedere a Internet. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">indicatore di stato della connessione di rete (NCSI)</a>.

<code>www.msftconnecttest.com</code> deve essere risolvibile tramite DNS e accessibile tramite HTTP.
<tr><td><b>Windows Notification Services (WNS)<b><td>Questo servizio viene usato per consentire a Windows di ricevere notifiche da app e servizi. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a>.<br>

Se i servizi WNS non sono disponibili, il processo Autopilot continuerà senza notifiche.
<tr><td><b>Microsoft Store, Microsoft Store per le aziende<b><td>È possibile effettuare il push delle app nel Microsoft Store al dispositivo, attivato tramite Intune (MDM).Gli aggiornamenti delle app e le app aggiuntive possono essere necessari anche quando l'utente accede per la prima volta. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business">prerequisiti per Microsoft Store for Business and Education</a> (include anche Azure ad e Windows Notification Services).<br>

Se il Microsoft Store non è accessibile, il processo Autopilot continuerà senza Microsoft Store app.

<tr><td><b>Office 365<b><td>Come parte della configurazione del dispositivo Intune, potrebbe essere necessaria l'installazione delle app Microsoft 365 per Enterprise. Per altre informazioni, vedere <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">URL e intervalli di indirizzi IP per Office 365</a>. Questo articolo include tutti i servizi Office, i nomi DNS e gli indirizzi IP. Include anche Azure AD e altri servizi che potrebbero sovrapporsi ai servizi elencati in precedenza.
<tr><td><b>Elenchi di revoche di certificati (CRL)<b><td>Alcuni di questi servizi dovranno inoltre controllare gli elenchi di revoche di certificati (CRL) per i certificati utilizzati nei servizi.Per un elenco completo, vedere <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">URL e intervalli di indirizzi IP di office 365</a> e <a href="https://aka.ms/o365chains">catene di certificati di Office 365</a>.
<tr><td><b>Aggiunta ad Azure AD ibrido<b><td>Il dispositivo può essere ibrido Azure AD Unito. Il computer deve trovarsi nella rete aziendale affinché Hybrid Azure AD join funzioni. Vedere i dettagli in <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">modalità basata sull'utente di Windows Autopilot</a>
<tr><td><b>Modalità di distribuzione automatica Autopilot e guanto bianco di Autopilot<b><td>I dispositivi TPM del firmware, che vengono forniti solo da Intel, AMD o Qualcomm, non includono tutti i certificati necessari in fase di avvio e devono essere in grado di recuperarli dal produttore al primo utilizzo. I dispositivi con chip TPM discreti (inclusi i dispositivi di qualsiasi altro produttore) sono dotati di questi certificati preinstallati. Per altre informazioni, vedere <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">raccomandazioni per TPM</a>. Per ogni provider TPM del firmware, assicurarsi che questi URL siano accessibili in modo che i certificati possano essere richiesti correttamente:

 <br>Intel <code>https://ekop.intel.com/ekcertservice</code>
 <br>Qualcomm <code>https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1</code>
 <br>AMD <code>https://ftpm.amd.com/pki/aia</code>

</table>

**Passaggi successivi**

[Requisiti per le licenze di Windows Autopilot](licensing-requirements.md)

