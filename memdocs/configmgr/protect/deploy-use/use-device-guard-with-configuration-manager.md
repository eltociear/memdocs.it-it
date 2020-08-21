---
title: Come gestire Controllo di applicazioni di Windows Defender
titleSuffix: Configuration Manager
description: Informazioni su come usare Configuration Manager per gestire Controllo di applicazioni di Windows Defender.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0dcd519a7703b5de94f779dc5dbe48aa0d34a3bc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700464"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Gestione di Controllo di applicazioni di Windows Defender con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

## <a name="introduction"></a>Introduzione
Controllo di applicazioni di Windows Defender è progettato per proteggere i PC da malware e altro software non attendibile. Impedisce l'esecuzione di codice dannoso, garantendo che solo il codice approvato e conosciuto possa essere eseguito.

Controllo di applicazioni di Windows Defender è un livello di protezione basato su software che applica un elenco esplicito di programmi software che possono essere eseguiti in un PC. Autonomamente, Controllo di applicazioni non ha alcun prerequisito hardware o firmware. I criteri di Controllo di applicazioni distribuiti con Configuration Manager abilitano un criterio nei PC inclusi in raccolte di destinazione che soddisfano i requisiti minimi relativi a SKU e versione di Windows descritti in questo articolo. Facoltativamente, è possibile abilitare la protezione basata su hypervisor di Controllo di applicazioni distribuiti con Configuration Manager usando Criteri di gruppo su hardware idoneo.

Per altre informazioni su Controllo di applicazioni di Windows Defender, vedere la [Guida alla distribuzione di Controllo di applicazioni di Windows Defender](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

   > [!NOTE]
   > - A partire da Windows 10, versione 1709, i criteri di integrità del codice configurabili sono noti come Controllo di applicazioni di Windows Defender.
   > - A partire da Configuration Manager versione 1710, i criteri di Device Guard sono stati rinominati in criteri di Controllo di applicazioni di Windows Defender.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Uso di Controllo di applicazioni di Windows Defender con Configuration Manager

È possibile usare Configuration Manager per distribuire criteri di Controllo di applicazioni di Windows Defender. Questi criteri consentono di configurare la modalità in cui eseguire Controllo di applicazioni di Windows Defender nei PC di una raccolta. 

È possibile configurare una delle modalità seguenti:

1. **Imposizione abilitata**: è possibile eseguire solo file eseguibili attendibili.
2. **Solo controllo**: è possibile eseguire tutti i file eseguibili, ma quelli non attendibili vengono registrati nel Registro eventi del client locale.

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1702 come [funzionalità in versione non definitiva](../../core/servers/manage/pre-release-features.md). A partire dalla versione 1906, questa funzionalità non è più in versione non definitiva.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Che cosa viene eseguito quando si distribuisce un criterio di controllo delle applicazioni di Windows Defender?

Controllo di applicazioni di Windows Defender consente di controllare rigorosamente cosa può essere eseguito sui PC gestiti dall'utente. Questa funzione può essere utile per i PC nei reparti ad alta sicurezza, in cui è fondamentale che impedire l'esecuzione di software indesiderato.

Quando si distribuisce un criterio, in genere, è possibile eseguire i file eseguibili seguenti:

- Componenti del sistema operativo Windows
- Driver di Hardware Dev Center (con firme Windows Hardware Quality Labs)
- App di Windows Store
- Client di Configuration Manager 
- Tutto il software distribuito tramite Configuration Manager e installato nei PC dopo l'elaborazione del criterio di controllo delle applicazioni di Windows Defender. 
- Aggiornamenti ai componenti di Windows da:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager
    - Facoltativamente, il software considerato attendibile in base a quanto determinato da Microsoft Intelligent Security Graph. Intelligent Security Graph include Windows Defender SmartScreen e altri servizi Microsoft. Perché il software possa essere considerato attendibile, il dispositivo deve eseguire Windows Defender SmartScreen e Windows 10 versione 1709 o successiva.

>[!IMPORTANT]
>Questi elementi non includono software *non* incorporato in Windows che venga aggiornato automaticamente da Internet o da aggiornamenti software di terze parti e che sia stato installato usando uno qualsiasi dei meccanismi di aggiornamento indicati in precedenza o da Internet. Possono essere eseguite solo modifiche software distribuite tramite il client di Configuration Manager.

## <a name="before-you-start"></a>Prima di iniziare

Prima di configurare o distribuire criteri di controllo delle applicazioni di Windows Defender, leggere le informazioni seguenti:

- La gestione di Controllo di applicazioni di Windows Defender è una funzionalità di versione non definitiva per Configuration Manager ed è soggetta a modifiche.
- Per usare Controllo di applicazioni di Windows Defender con Configuration Manager, i PC gestiti devono eseguire Windows 10 Enterprise versione 1703 o successiva.
- Dopo che il criterio è stato elaborato correttamente in un computer client, Configuration Manager viene configurato come programma di installazione gestito in tale client. Il software distribuito tramite quest'ultimo, dopo l'elaborazione del criterio, viene automaticamente considerato attendibile. Il software installato da Configuration Manager prima dell'elaborazione del criterio di Controllo di applicazioni di Windows Defender non è considerato automaticamente attendibile.
- In base alla pianificazione, configurabile durante la distribuzione, la valutazione della conformità predefinita per i criteri di Controllo di applicazioni avviene ogni giorno. Se si rilevano problemi nell'elaborazione dei criteri, può essere utile configurare una pianificazione di valutazione di conformità più breve, ad esempio ogni ora. Questa pianificazione determina la frequenza con cui i client riprovano a elaborare un criterio di Controllo di applicazioni di Windows Defender in caso di errore.
- Indipendentemente dalla modalità di applicazione selezionata, quando si distribuisce un criterio di controllo delle applicazioni di Windows Defender, i PC client non possono eseguire applicazioni HTML con estensione hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Come creare criteri di controllo delle applicazioni di Windows Defender
1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection** e quindi fare clic su **Controllo delle applicazioni di Windows Defender**.
3. Nella scheda **Home**, nel gruppo **Crea** fare clic su **Crea un criterio di controllo delle applicazioni**.
4. Nella pagina **Generale** della **Create Application Control policy Wizard** (Creazione guidata criteri di Controllo di applicazioni) specificare le informazioni seguenti:
    - **Nome**: immettere un nome univoco per il criterio di controllo delle applicazioni di Windows Defender. 
    - **Descrizione**: facoltativamente, immettere una descrizione per il criterio che consenta di identificarlo nella console di Configuration Manager.
    - **Imponi un riavvio dei dispositivi in modo che questo criterio possa essere applicato per tutti i processi**: dopo l'elaborazione del criterio in un PC client, viene pianificato un riavvio nel client in base a quanto specificato in **Impostazioni client** per **Riavvio del computer**.
        - I dispositivi che eseguono Windows 10 versione 1703 o precedente verranno sempre riavviati automaticamente.
        - A partire da Windows 10 versione 1709, il nuovo criterio di Controllo di applicazioni verrà applicato alle applicazioni attualmente in esecuzione nel dispositivo solo dopo il riavvio. Le applicazioni avviate dopo l'applicazione del criterio rispetteranno tuttavia il nuovo criterio di Controllo di applicazioni. 
    - **Modalità di imposizione**: scegliere uno dei metodi di imposizione di Controllo di applicazioni di Windows Defender seguenti sul PC client.
        - **Imposizione abilitata**: è possibile eseguire solo file eseguibili attendibili.
        - **Solo controllo**: è possibile eseguire tutti i file eseguibili, ma quelli non attendibili vengono registrati nel Registro eventi del client locale.
5. Nella scheda **Inclusioni** della procedura guidata **Crea un criterio di controllo delle applicazioni** scegliere se si vuole **autorizzare il software ritenuto attendibile da Intelligent Security Graph**.
6. Fare clic su **Aggiungi** per aggiungere il trust per file o cartelle specifiche sui PC. Nella finestra di dialogo **Aggiungi file o cartella attendibile** è possibile specificare un percorso di file o cartella locale da considerare attendibile. È anche possibile specificare un percorso di file o cartella su un dispositivo remoto a cui si è autorizzati a connettersi. Se si configura il trust per cartelle o file specifici in un criterio di Controllo di applicazioni di Windows Defender, è possibile:
    - Risolvere i problemi relativi ai comportamenti del programma di installazione gestito
    - Rendere attendibili le app line-of-business che non possono essere distribuite con Configuration Manager
    - Rendere attendibili le app incluse in un'immagine di distribuzione del sistema operativo. 
8. Fare clic su **Avanti** per completare la procedura guidata.

>[!IMPORTANT]
>L'inclusione di file o cartelle attendibili è supportata solo nei PC client che eseguono la versione 1706 o versioni successive del client di Configuration Manager. Se si aggiungono regole di inclusione in un criterio di controllo delle applicazioni di Windows Defender e il criterio viene quindi distribuito in un PC client che esegue una versione precedente del client di Configuration Manager, il criterio non verrà applicato. Per risolvere il problema, aggiornare questi client precedenti. I criteri che non comprendono regole di inclusione possono comunque essere applicati alle versioni precedenti del client di Configuration Manager.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Come distribuire criteri di controllo delle applicazioni di Windows Defender
1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection** e quindi fare clic su **Controllo delle applicazioni di Windows Defender**.
3. Nell'elenco dei profili selezionare il profilo da distribuire e fare clic su **Distribuisci un criterio di controllo delle applicazioni** nel gruppo **Distribuzione** della scheda **Home**.
4. Nella finestra di dialogo **Distribuisci un criterio di controllo delle applicazioni** selezionare la raccolta in cui si vuole distribuire il criterio, quindi configurare una pianificazione per la valutazione del criterio da parte dei client. Selezionare infine se i client possono valutare i criteri al di fuori delle finestre di manutenzione configurate.
5. Al termine, fare clic su **OK** per distribuire il criterio. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Come monitorare i criteri di controllo delle applicazioni di Windows Defender

Usare le informazioni contenute nell'argomento [Monitorare le impostazioni di conformità](../../compliance/deploy-use/monitor-compliance-settings.md) per controllare che il criterio distribuito sia stato applicato correttamente a tutti i PC.

Per monitorare l'elaborazione di un criterio di controllo delle applicazioni di Windows Defender, usare il file di log seguente nei PC client:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Per verificare che il software specifico sia bloccato o controllato, vedere i registri eventi seguenti del client locale:

1. Per il blocco e controllo di file eseguibili, usare **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **Integrità del codice** > **Operativo**.
2. Per il blocco e il controllo di Windows Installer e dei file di script, usare **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Informazioni sulla sicurezza e la privacy per Controllo di applicazioni di Windows Defender

- In questa versione non definitiva non distribuire criteri di controllo delle applicazioni di Windows Defender con la modalità di applicazione **Solo controllo** in un ambiente di produzione. Questa modalità consente di testare la funzionalità solo in un ambiente di prova.
- I dispositivi in cui è stato distribuito un criterio in modalità **Solo controllo** o **Imposizione abilitata**, ma che non sono ancora stati riavviati per rendere effettivo il criterio sono vulnerabili nei confronti di eventuale software non attendibile installato.
In questo caso, l'esecuzione del software potrebbe ancora essere consentita anche se il dispositivo si riavvia o riceve un criterio in modalità **Imposizione abilitata**.
- Per assicurarsi che il criterio di controllo delle applicazioni di Windows Defender sia valido, preparare il dispositivo in un ambiente lab. Distribuire quindi il criterio con **Imposizione abilitata** e infine riavviare il dispositivo prima di consegnarlo a un utente finale.
- Non distribuire un criterio in modalità **Imposizione abilitata** per poi distribuire in un secondo momento un criterio in modalità **Solo controllo** nello stesso dispositivo. Questa configurazione potrebbe consentire l'esecuzione di software non attendibile.
- Quando si usa Configuration Manager per abilitare Controllo di applicazioni di Windows Defender sui PC client, il sistema non impedisce agli utenti con diritti di amministratore locale di eludere i criteri di Controllo di applicazioni o di eseguire in altro modo software non attendibile. 
- L'unico modo per impedire agli utenti con diritti di amministratore locale di disabilitare Controllo di applicazioni consiste nel distribuire un criterio binario firmato, operazione possibile con Criteri di gruppo, ma non attualmente supportata in Configuration Manager.
- La configurazione di Configuration Manager come programma di installazione gestito nei PC client usa criteri di AppLocker. AppLocker è usato solo per identificare i programmi di installazione gestiti e qualsiasi imposizione avviene con Controllo delle applicazioni di Windows Defender. 

## <a name="next-steps"></a>Passaggi successivi

 [Gestire i criteri antimalware e le impostazioni del firewall](endpoint-antimalware-firewall.md)