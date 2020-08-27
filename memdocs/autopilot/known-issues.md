---
title: Problemi noti di Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informazioni sui problemi noti che possono verificarsi durante la distribuzione di Windows Autopilot.
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
ms.openlocfilehash: 4ad59d2891a94147a81450ee3c7157281b24d3df
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908009"
---
# <a name="windows-autopilot---known-issues"></a>Windows Autopilot-problemi noti

**Si applica a**

- Windows 10

<table>
<th>Problema<th>Ulteriori informazioni

<tr><td>Le app bloccanti specificate in un profilo di stato di registrazione di destinazione dell'utente vengono ignorate durante l'ESP del dispositivo.</td>
<td>I servizi responsabili della determinazione dell'elenco di app che devono essere bloccate durante l'ESP del dispositivo non sono in grado di determinare il profilo ESP corretto contenente l'elenco delle app perché non conoscono l'identità dell'utente. Per risolvere il problema, abilitare il profilo ESP predefinito (destinato a tutti gli utenti e i dispositivi) e collocare l'elenco di app bloccanti. In futuro sarà possibile indirizzare il profilo ESP ai gruppi di dispositivi per evitare questo problema.</tr>

<tr><td>Il nome utente appare come appartiene a un'altra organizzazione. Provare ad accedere di nuovo o ricominciare con un account diverso.</td>
 <td>Verificare che tutte le informazioni siano corrette all'HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot. Per ulteriori informazioni, vedere <a href="troubleshooting.md#windows-10-version-1709-and-above">risoluzione dei problemi di Windows Autopilot</a>.</td></tr>

<tr><td>Le distribuzioni di Azure AD ibrido basate sugli utenti di Windows Autopilot non concedono i diritti di amministratore anche se specificati nel profilo di Windows Autopilot.</td>
<td>Questo problema si verifica quando nel dispositivo è presente un altro utente che dispone già dei diritti di amministratore. Ad esempio, uno script o un criterio di PowerShell può creare un account locale aggiuntivo che è un membro del gruppo Administrators. Per assicurarsi che funzioni correttamente, non creare un account aggiuntivo fino al completamento del processo di Windows Autopilot.</tr>

<tr><td>Il provisioning dei dispositivi di Windows Autopilot può avere esito negativo con errori di attestazione TPM o timeout ESP nei dispositivi in cui il clock in tempo reale è disattivato per un periodo di tempo significativo (ad esempio, diversi minuti o più).</td>
<td>Per risolvere il problema: <ol><li>Avviare il dispositivo all'avvio dell'esperienza predefinita (OOBE).
<li>Stabilire una connessione di rete (cablata o wireless).
<li>Eseguire il comando <b>w32tm sull'/Resync/Force</b> per sincronizzare l'ora con il server di ora predefinito (Time.Windows.com).</ol>
</tr>

<tr><td>Windows Autopilot per i dispositivi esistenti non funziona per Windows 10, versione 1903 o 1909; vengono visualizzate le schermate disabilitate nel profilo di Windows Autopilot, ad esempio la schermata del contratto di licenza di Windows 10.
<br>&nbsp;<br>
Questo problema si verifica perché Windows 10, versione 1903 e 1909, Elimina il AutopilotConfigurationFile.jssu file.
<td>Per risolvere il problema: <ol><li>Modificare la sequenza di attività Configuration Manager e disabilitare il passaggio <b>prepara Windows per l'acquisizione</b> .
<li>Aggiungere un nuovo passaggio <b>Esegui riga di comando</b> che esegue <b>c:\windows\system32\sysprep\sysprep.exe/OOBE/reboot</b>.</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">Altre informazioni</a></tr>
 
<tr><td>L'attestazione TPM ha esito negativo in Windows 10 1903 perché manca l'estensione AKI nel certificato EK. (È stata aggiunta una convalida aggiuntiva in Windows 10 1903 per verificare che i certificati TPM EK dispongano degli attributi appropriati in base alle specifiche TCG, che non sono stati individuati, in modo che la convalida venga rimossa).
<td>Scaricare e installare l' <a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">aggiornamento di KB4517211</a>.
<tr><td>I problemi noti seguenti vengono risolti installando il 30 agosto 2019 aggiornamento KB4512941 (build del sistema operativo 18362,329):

- La funzionalità Windows Autopilot for existing devices non disattiva correttamente la pagina "Activities" durante la configurazione guidata. A causa di questo problema, la pagina aggiuntiva verrà visualizzata durante la configurazione guidata.
- Lo stato di attestazione TPM non è cancellato da Sysprep/generalize, causando un errore di attestazione TPM durante il flusso di configurazione successiva. Questo non è un problema particolarmente comune, ma è possibile eseguirlo durante i test se si esegue Sysprep/generalize e quindi si riavvia o si rigenera l'immagine del dispositivo per tornare indietro tramite un guanto bianco o uno scenario di distribuzione automatica.
- L'attestazione TPM potrebbe non riuscire se il dispositivo ha un certificato AIK valido, ma nessun certificato EK. (questo problema è correlato all'elemento precedente).
- Se l'attestazione TPM ha esito negativo durante il processo del guanto bianco di Windows Autopilot, la pagina di destinazione risulta bloccata. Fondamentalmente, la pagina di destinazione del guanto bianco, in cui si fa clic su "provisioning" per avviare il processo di guanto bianco, non segnala correttamente gli errori.
- L'attestazione TPM ha esito negativo in un nuovo TPMs Infineon (versione firmware > 7,69). (Prima di questa correzione è stato accettato solo un elenco specifico di versioni del firmware).
- I modelli di denominazione dei dispositivi possono troncare il nome del computer a 14 caratteri anziché 15.
- I criteri di accesso assegnati generano un riavvio, che può interferire con la configurazione di dispositivi a chiosco singolo per app.
<td>Scaricare e installare l' <a href="https://support.microsoft.com/help/4512941">aggiornamento di KB4512941</a>. <br><br>Vedere la sezione: <b>come ottenere questo aggiornamento</b> per informazioni sui canali di rilascio specifici che è possibile usare per ottenere l'aggiornamento.
<tr><td>I problemi noti seguenti vengono risolti installando il 26 luglio 2019 aggiornamento KB4505903 (build del sistema operativo 18362,267):

- Il guanto bianco di Windows Autopilot non funziona per un sistema operativo non in lingua inglese e viene visualizzata una schermata rossa con la dicitura "success".
- Windows Autopilot segnala un errore AUTOPILOTUPDATE durante la configurazione guidata dopo Sysprep, reset o altre varianti. Questo problema si verifica in genere se si reimposta il sistema operativo o si usa un'immagine preparata con Sysprep personalizzata.
- La crittografia BitLocker non è configurata correttamente. Ad esempio, BitLocker non ha ricevuto una notifica prevista dopo che i criteri sono stati applicati per iniziare la crittografia.
- Non è possibile installare le app UWP dalla Microsoft Store, causando errori durante Windows Autopilot. Se si distribuisce Portale aziendale come app bloccante durante Windows Autopilot ESP, probabilmente si è notato questo errore.
- A un utente non vengono concessi diritti di amministratore nello scenario di join basato sull'utente di Windows Autopilot Azure AD ibrido. Si tratta di un altro problema del sistema operativo non in lingua inglese.
<td>Scaricare e installare l' <a href="https://support.microsoft.com/help/4505903">aggiornamento di KB4505903</a>. <br><br>Vedere la sezione: <b>come ottenere questo aggiornamento</b> per informazioni sui canali di rilascio specifici che è possibile usare per ottenere l'aggiornamento.
<tr><td>La modalità di <a href="self-deploying.md">distribuzione automatica</a> di Windows Autopilot ha esito negativo e restituisce un codice di errore:
<td><table>
<tr><td>0x800705B4<td>Si tratta di un errore generale che indica un timeout. Una cause comune di questo errore nella modalità di distribuzione automatica è che il dispositivo non è compatibile con TPM 2,0 (ad esempio, una macchina virtuale). I dispositivi che non sono compatibili con TPM 2,0 non possono essere usati con la modalità di distribuzione automatica.
<tr><td>0x801c03ea<td>Questo errore indica che l'attestazione TPM non è riuscita, causando un errore di join Azure Active Directory con un token del dispositivo.
<tr><td>0xc1036501<td>Il dispositivo non può eseguire una registrazione MDM automatica perché sono presenti più configurazioni MDM in Azure AD. Vedere <a href="https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/">nella modalità di distribuzione automatica di Windows Autopilot</a>.
</table>
<tr><td>Il guanto bianco fornisce una schermata rossa e il registro eventi di <b>registrazione/amministrazione del dispositivo Microsoft-Windows-User</b> Visualizza il <b>codice di errore HRESULT 0x801C03F3</b><td>Questo problema può verificarsi se Azure AD non riesce a trovare un oggetto dispositivo Azure AD per il dispositivo che si sta provando a distribuire. Questo problema si verificherà se si elimina manualmente l'oggetto. Per risolvere il problema, rimuovere il dispositivo da Azure AD, Intune e Autopilot, quindi registrarlo di nuovo con Autopilot, che ricreerà l'oggetto dispositivo Azure AD.<br> 
<br>Per ottenere i log di risoluzione dei problemi, usare: <b> AutopilotMdmdiagnosticstool.exe area; c:\autopilot.cabCAB TPM </b>
<tr><td>Il guanto bianco fornisce una schermata rossa<td>Il guanto bianco non è supportato in una macchina virtuale.
<tr><td>Errore durante l'importazione dei dispositivi Windows Autopilot da un file CSV<td>Assicurarsi che il file CSV non sia stato modificato in Microsoft Excel o in un editor diverso da blocco note. Alcuni di questi editor possono presentare caratteri aggiuntivi che fanno sì che il formato del file non sia valido. 
<tr><td>Windows Autopilot per i dispositivi esistenti non segue l'esperienza di configurazione guidata Autopilot.<td>Verificare che il file di profilo JSON sia salvato in formato <b>ANSI/ASCII</b> , non Unicode o UTF-8.
<tr><td>Si è verificato <b>un errore</b> quando viene visualizzata la pagina durante la configurazione guidata.<td>È probabile che il client non riesca ad accedere a tutti gli URL relativi a Azure AD/MSA necessari. Per ulteriori informazioni, vedere [requisiti di rete](networking-requirements.md).
<tr><td>L'uso di un pacchetto di provisioning in combinazione con Windows Autopilot può causare problemi, soprattutto se il PPKG contiene informazioni su join, registrazione o nome dispositivo.<td>Non è consigliabile usare PPKGs insieme a Windows Autopilot.
</table>

## <a name="related-topics"></a>Argomenti correlati

[Diagnosticare gli errori MDM in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Risoluzione dei problemi di Windows Autopilot](troubleshooting.md)