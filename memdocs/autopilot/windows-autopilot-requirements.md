---
title: Requisiti di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sul software, sulla rete, sulle licenze e sui requisiti di configurazione per la distribuzione di Windows Autopilot.
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
ms.openlocfilehash: bf0b6d1f074de85793f025f9578892a126bbce3d
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076078"
---
# <a name="windows-autopilot-requirements"></a>Requisiti di Windows Autopilot

**Si applica a: Windows 10**

Windows Autopilot dipende da funzionalità specifiche disponibili nei servizi Windows 10, Azure Active Directory e MDM, ad esempio Microsoft Intune.  Per usare Windows Autopilot e sfruttare queste funzionalità, è necessario soddisfare alcuni requisiti.

**Nota**: per un elenco degli OEM che attualmente supportano Windows Autopilot, vedere la sezione produttori di dispositivi partecipanti di [Windows Autopilot](https://aka.ms/windowsAutopilot).

## <a name="software-requirements"></a>Requisiti software

- È necessaria una [versione supportata](/windows/release-information/) del canale semestrale di Windows 10. È supportato anche il canale di manutenzione a lungo termine di Windows 10 Enterprise 2019 (LTSC).
- Sono supportate le edizioni seguenti:
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education
  - Windows 10 Enterprise 2019 LTSC (non supporta la modalità di distribuzione automatica)

>[!NOTE]
>Le procedure per la distribuzione di Windows Autopilot possono fare riferimento a prodotti e versioni specifici. L'inclusione di questi prodotti in questo contenuto non implica un'estensione del supporto per una versione che esula dal ciclo di vita del supporto. Windows Autopilot non supporta prodotti che esulano dal ciclo di vita del supporto. Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).

## <a name="networking-requirements"></a>Requisiti di rete

Windows Autopilot dipende da un'ampia gamma di servizi basati su Internet. Per il corretto funzionamento di Autopilot è necessario fornire l'accesso a questi servizi. Nel caso più semplice, l'abilitazione delle funzionalità appropriate può essere eseguita garantendo quanto segue:

- Verificare la risoluzione dei nomi DNS per i nomi DNS Internet
- Consentire l'accesso a tutti gli host tramite la porta 80 (HTTP), 443 (HTTPS) e 123 (UDP/NTP)

Negli ambienti con accesso a Internet più restrittivo o per quelli che richiedono l'autenticazione prima di poter ottenere l'accesso a Internet, potrebbe essere necessaria una configurazione aggiuntiva per consentire l'accesso ai servizi necessari. 

> [!NOTE]
> La smart card e l'autenticazione basata su certificato non sono supportate durante la configurazione guidata. Per altre informazioni, vedere [Smart Card e autenticazione basata su certificati](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

Per ulteriori informazioni su ciascuno di questi servizi e sui requisiti specifici, esaminare i dettagli seguenti:

<table><th>Servizio<th>Informazioni
<tr><td><b>Servizio di distribuzione di Windows Autopilot<b><td>Dopo la connessione di rete, ogni dispositivo Windows 10 contatterà il servizio di distribuzione di Windows Autopilot.  Con Windows 10 versione 1903 e successive, vengono usati gli URL seguenti: https://ztd.dds.microsoft.com https://cs.dds.microsoft.com . <br>

<tr><td><b>Attivazione di Windows<b><td>Windows Autopilot richiede anche servizi di attivazione Windows. Vedere <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">attivazione o convalida di Windows non riuscita con codice di errore 0x8004FE33</a> per informazioni dettagliate sugli URL che devono essere accessibili per i servizi di attivazione.<br>

<tr><td><b>Azure Active Directory<b><td>Le credenziali utente vengono convalidate da Azure Active Directory e il dispositivo può anche essere aggiunto al Azure Active Directory. Per ulteriori informazioni, vedere l' <a href="/office365/enterprise/office-365-ip-web-service">indirizzo IP di Office 365 e il servizio Web URL</a> .
<tr><td><b>Intune<b><td>Una volta autenticato, Azure Active Directory attiverà la registrazione del dispositivo nel servizio MDM di Intune. Per informazioni dettagliate sui requisiti di comunicazione di rete: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">requisiti di configurazione di rete di Intune e larghezza di banda</a>, vedere il collegamento seguente.
<tr><td><b>Windows Update<b><td>Durante il processo OOBE, così come dopo che il sistema operativo Windows 10 è stato completamente configurato, viene sfruttato il servizio Windows Update per recuperare gli aggiornamenti necessari. Se si verificano problemi di connessione a Windows Update, vedere <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">come risolvere i problemi di connessione relativi Windows Update o Microsoft Update</a>.<br>

Se Windows Update è inaccessibile, il processo Autopilot continuerà, ma gli aggiornamenti critici non saranno disponibili.

<tr><td><b>Ottimizzazione recapito<b><td>Quando si scaricano gli aggiornamenti di Windows, Microsoft Store app e gli aggiornamenti delle app, gli aggiornamenti di Office e le app Win32 di Intune, il servizio di <a href="/windows/deployment/update/waas-delivery-optimization">Ottimizzazione recapito</a> viene contattato per abilitare la condivisione peer-to-peer del contenuto, in modo che solo alcuni dispositivi debbano scaricarlo da Internet.<br>

Se il servizio di ottimizzazione recapito è inaccessibile, il processo Autopilot continuerà comunque con i download dell'ottimizzazione del recapito dal cloud (senza peer-to-peer).

<tr><td><b>Sincronizzazione NTP (Network Time Protocol)<b><td>Quando un dispositivo Windows viene avviato, viene parlato con un server di tempo di rete per assicurarsi che l'ora del dispositivo sia accurata. Verificare che la porta UDP 123 per time.windows.com sia accessibile.
<tr><td><b>DNS (Domain Name Services)<b><td>Per risolvere i nomi DNS per tutti i servizi, il dispositivo comunica con un server DNS, in genere fornito tramite DHCP.Questo server DNS deve essere in grado di risolvere i nomi Internet.
<tr><td><b>Dati di diagnostica<b><td>A partire da Windows 10, 1903, la raccolta dei dati di diagnostica verrà abilitata per impostazione predefinita. Per disabilitare Windows Analytics e le funzionalità di diagnostica correlate, vedere <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">gestire il livello di dati di diagnostica aziendali</a>.<br>

Se non è possibile inviare dati di diagnostica, il processo Autopilot continuerà, ma i servizi che dipendono dai dati di diagnostica, ad esempio Windows Analytics, non funzioneranno.
<tr><td><b>Indicatore stato connettività di rete<b><td>Windows deve essere in grado di indicare che il dispositivo è in grado di accedere a Internet. Per ulteriori informazioni, vedere <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">indicatore di stato della connessione di rete (NCSI)</a>.

<code>www.msftconnecttest.com</code> deve essere risolvibile tramite DNS e accessibile tramite HTTP.
<tr><td><b>Windows Notification Services (WNS)<b><td>Questo servizio viene usato per consentire a Windows di ricevere notifiche da app e servizi. Per ulteriori informazioni, vedere <a href="/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a> .<br>

Se i servizi WNS non sono disponibili, il processo Autopilot continuerà senza notifiche.
<tr><td><b>Microsoft Store, Microsoft Store per le aziende<b><td>È possibile effettuare il push delle app nel Microsoft Store al dispositivo, attivato tramite Intune (MDM).Gli aggiornamenti delle app e le app aggiuntive possono essere necessari anche quando l'utente accede per la prima volta. Per ulteriori informazioni, vedere <a href="/microsoft-store/prerequisites-microsoft-store-for-business">prerequisiti per Microsoft Store for Business and Education</a> (include anche Azure ad e Windows Notification Services).<br>

Se il Microsoft Store non è accessibile, il processo Autopilot continuerà senza Microsoft Store app.

<tr><td><b>Microsoft 365<b><td>Come parte della configurazione del dispositivo Intune, potrebbe essere necessaria l'installazione delle app Microsoft 365 per Enterprise. Per altre informazioni, vedere <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">URL e intervalli di indirizzi IP per office 365</a> (include tutti i servizi Office, i nomi DNS, gli indirizzi IP, include Azure ad e altri servizi che potrebbero sovrapporsi a quelli elencati in precedenza).
<tr><td><b>Elenchi di revoche di certificati (CRL)<b><td>Alcuni di questi servizi dovranno inoltre controllare gli elenchi di revoche di certificati (CRL) per i certificati utilizzati nei servizi.Un elenco completo di queste attività è documentato in <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">URL e intervalli di indirizzi IP di office 365</a> e <a href="https://aka.ms/o365chains">catene di certificati di Office 365</a>.
<tr><td><b>Join AAD ibrido<b><td>Il dispositivo può essere aggiunto ad AAD ibrido. Il computer deve trovarsi nella rete aziendale per far funzionare il join di AAD ibrido. Vedere i dettagli in <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">modalità basata sull'utente di Windows Autopilot</a>
<tr><td><b>Modalità di distribuzione automatica Autopilot e guanto bianco di Autopilot<b><td>I dispositivi TPM del firmware, che vengono forniti solo da Intel, AMD o Qualcomm, non includono tutti i certificati necessari in fase di avvio e devono essere in grado di recuperarli dal produttore al primo utilizzo. I dispositivi con chip TPM discreti (inclusi i dispositivi di qualsiasi altro produttore) sono dotati di questi certificati preinstallati. Per altri dettagli, vedere <a href="/windows/security/information-protection/tpm/tpm-recommendations">suggerimenti sui TPM</a> . Verificare che questi URL siano accessibili per ogni provider TPM del firmware, in modo che i certificati possano essere richiesti correttamente: 

  <br>Intel- https://www.intel.com/  <br>Qualcomm- https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1  <br>AMD https://ftpm.amd.com/pki/aia

</table>

## <a name="licensing-requirements"></a>Requisiti di licenza

Windows Autopilot dipende da funzionalità specifiche disponibili in Windows 10 e Azure Active Directory. Richiede anche un servizio MDM, ad esempio Microsoft Intune. Queste funzionalità possono essere ottenute tramite varie edizioni e programmi di sottoscrizione:

Per fornire Azure Active Directory necessarie (registrazione MDM automatica e funzionalità di personalizzazione dell'azienda) e funzionalità MDM, è necessario eseguire una delle operazioni seguenti:
- [Sottoscrizione di Microsoft 365 Business Premium](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 sottoscrizione F1 o F3](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Sottoscrizione di Microsoft 365 Academic a1, a3 o a5](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise sottoscrizione E3 o E5](https://www.microsoft.com/microsoft-365/enterprise), che include tutte le funzionalità di Windows 10, Office 365 e em + S (Azure ad e Intune).
- [Enterprise Mobility + Security sottoscrizione E3 o E5](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), che include tutte le funzionalità Azure ad e Intune necessarie.
- [Intune per Education sottoscrizione](/intune-education/what-is-intune-for-education), che include tutte le funzionalità Azure ad e Intune necessarie.
- [Azure Active Directory Premium P1 o P2](https://azure.microsoft.com/services/active-directory/) e la [sottoscrizione Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) (o un servizio MDM alternativo).

> [!NOTE]
> Anche quando si usano Microsoft 365 sottoscrizioni, è comunque necessario [assegnare le licenze di Intune agli utenti](/intune/fundamentals/licenses-assign).

Inoltre, è consigliabile anche quanto segue (ma non obbligatorio):
- [Microsoft 365 app per Enterprise](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), che possono essere distribuite facilmente tramite Intune (o altri servizi MDM).
- [Attivazione della sottoscrizione di Windows](/windows/deployment/windows-10-enterprise-subscription-activation), per eseguire automaticamente il passaggio dei dispositivi da Windows 10 Pro a Windows 10 Enterprise.

## <a name="configuration-requirements"></a>Requisiti di configurazione

Prima di poter usare Windows Autopilot, è necessario eseguire alcune attività di configurazione per supportare gli scenari comuni di Autopilot.  

- Configurare Azure Active Directory la registrazione automatica.  Per Microsoft Intune, vedere [abilitare la registrazione automatica di Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment) per informazioni dettagliate.  Se si usa un servizio MDM diverso, contattare il fornitore per gli URL specifici o per la configurazione necessaria per tali servizi.
- Configurare Azure Active Directory personalizzazione personalizzata.  Per visualizzare una pagina di accesso specifica dell'organizzazione durante il processo di Autopilot, è necessario configurare Azure Active Directory con le immagini e il testo da visualizzare.  Per informazioni dettagliate, vedere [Guida introduttiva: aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso in Azure ad](/azure/active-directory/fundamentals/customize-branding) .  Si noti che il "logo quadrato" e il testo della pagina di accesso sono gli elementi chiave per Autopilot, nonché il nome del tenant Azure Active Directory (configurato separatamente nelle proprietà del tenant Azure AD).
- Abilitare l' [attivazione della sottoscrizione di Windows](/windows/deployment/windows-10-enterprise-subscription-activation) , se necessario, per passare automaticamente da Windows 10 Pro a Windows 10 Enterprise.

Scenari specifici avranno quindi requisiti aggiuntivi.  In genere, esistono due attività specifiche:

- Registrazione di dispositivi.  I dispositivi devono essere aggiunti a Windows Autopilot per supportare la maggior parte degli scenari di Windows Autopilot.  Per altri dettagli, vedere [aggiunta di dispositivi a Windows Autopilot](add-devices.md) .
- Configurazione del profilo.  Una volta aggiunti i dispositivi a Windows Autopilot, è necessario applicare un profilo di impostazioni a ogni dispositivo.  Per informazioni dettagliate, vedere [configurare i profili di Autopilot](profiles.md) .  Si noti che Microsoft Intune possibile automatizzare l'assegnazione del profilo; Per ulteriori informazioni, vedere [creare un gruppo di dispositivi Autopilot](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) e [assegnare un profilo di distribuzione Autopilot a un gruppo di dispositivi](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group) .

Per ulteriori informazioni, vedere [scenari di Windows Autopilot](windows-Autopilot-scenarios.md) .

Per una procedura dettagliata relativa ad alcuni di questi e passaggi correlati, vedere questo video:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


Non sono previsti requisiti hardware aggiuntivi per l'utilizzo di Windows 10 Autopilot, oltre ai [requisiti per l'esecuzione di Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

## <a name="related-topics"></a>Argomenti correlati

[Panoramica di Windows Autopilot](windows-Autopilot.md)
