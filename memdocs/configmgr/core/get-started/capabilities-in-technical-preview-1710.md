---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1710 per Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3dd4c3f22a0f2c24153e6d26be2e3098511c5dc4
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905315"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1710 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1710. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemi noti di questa versione Technical Preview:**
- **Supporto per Windows 10, versione 1709 (anche noto come Fall Creators Update)** .  A partire da questa versione di Windows, il supporto include più versioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento o di un'immagine del sistema operativo, assicurarsi di selezionare un'[edizione utilizzabile da Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **L'aggiornamento a una nuova versione di anteprima ha esito negativo se il server del sito è in modalità passiva**. Se si esegue una versione di anteprima con il [server del sito primario in modalità passiva](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima di poter aggiornare il sito di anteprima alla nuova versione di anteprima. Sarà possibile reinstallare il server del sito in modalità passiva al termine dell'aggiornamento del sito.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Miglioramenti per la distribuzione di script di PowerShell da Configuration Manager
Con questa versione gli script di PowerShell distribuiti supportano ora i miglioramenti seguenti: 
- **Ambiti di protezione**.  Vengono ora usati ambiti di protezione per controllare la creazione e l'esecuzione degli script. Questo avviene tramite l'assegnazione di tag che rappresentano gruppi di utenti. Per altre informazioni sull'uso degli ambiti di protezione, vedere [Configurare l'amministrazione basata su ruoli per Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Monitoraggio in tempo reale**. Il monitoraggio dell'esecuzione di uno script avviene ora in tempo reale, durante l'esecuzione dello script.
- **Convalida dei parametri**. Ogni parametro nello script ha una finestra di dialogo **Proprietà parametri script**, in cui è possibile aggiungere la convalida per il parametro. Dopo aver aggiunto la convalida, verranno restituiti errori quando si immette un valore che non soddisfa i requisiti di convalida per il parametro.

La distribuzione di script di PowerShell è stata introdotta per la prima volta nella versione [Technical Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). Miglioramenti aggiuntivi sono stati quindi introdotti nella versione [Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) e quindi nella versione [Technical Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Verifica

Per provare la funzionalità Esegui script, vedere [Creare ed eseguire script](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitare i dati avanzati di Windows 10 al solo invio dei dati pertinenti per Integrità dispositivi di Windows Analytics
<!-- 1356148 -->

Con questa versione è ora possibile impostare il livello della raccolta dei dati di diagnostica di Windows 10 su **Avanzata (con limitazioni)** . Questa impostazione consente di ottenere informazioni utili sui dispositivi presenti nell'ambiente in uso senza che i dispositivi segnalino tutti i dati nel livello **avanzato** con Windows 10 1709 o versione successiva.

Il livello Avanzata (con limitazioni) include metriche del livello di base e un subset di dati raccolti dal livello **Avanzato** pertinenti per Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Software Center non deforma più le icone maggiori di 250x250 pixel  
<!-- 1356194 -->

Con questa versione, Software Center non distorce più le icone maggiori di 250x250 pixel. In Software Center tali icone apparivano sfocate. È ora possibile impostare icone con dimensioni massime pari a 512x512 pixel. Tali icone verranno visualizzate senza distorsione.

### <a name="try-it-out"></a>Verifica
Aggiungere un'icona per l'app in Software Center. Per provare subito, vedere [Creare applicazioni](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Controllare la conformità da Software Center per i dispositivi co-gestiti
<!-- 1356374 -->
In questa versione gli utenti possono usare Software Center per verificare la conformità dei dispositivi Windows 10 co-gestiti, anche se l'accesso condizionale viene gestito da Intune. Per i dettagli, vedere [Co-gestione per dispositivi Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Supporto per Exploit Guard
In questa versione è stato aggiunto il supporto per Windows Defender Exploit Guard. È possibile configurare e distribuire criteri di gestione per tutti i quattro componenti di Exploit Guard. Questi componenti prevedono:
-   Riduzione della superficie di attacco
-   Accesso controllato alle cartelle
-   Protezione dagli exploit
-   Protezione di rete

I dati di conformità per la distribuzione di criteri di Exploit Guard sono disponibili nella console di Configuration Manager.

Per altre informazioni su Exploit Guard, nonché sulle regole e sui componenti specifici, vedere [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) nella libreria della documentazione di Windows.

### <a name="prerequisites"></a>Prerequisiti
I dispositivi gestiti devono eseguire Windows 10 1709 Fall Creators Update o versione successiva e soddisfare i requisiti seguenti a seconda delle regole e dei componenti configurati:

|Componente di Exploit Guard |Altri prerequisiti|
|------------------------|------------------------|
| Riduzione della superficie di attacco  | Nei dispositivi deve essere abilitata la [protezione in tempo reale di Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).  |
| Accesso controllato alle cartelle  | Nei dispositivi deve essere abilitata la [protezione in tempo reale di Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).   |
| Protezione dagli exploit  | Nessuno  |
| Protezione di rete  |  Nei dispositivi deve essere abilitata la [protezione in tempo reale di Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard).  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Creare criteri di Exploit Guard  <!--1355468 -->
1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Endpoint Protection** e fare clic su **Windows Defender Exploit Guard**.
2. Nel gruppo **Crea** della scheda **Home** fare clic su **Create Exploit Policy** (Crea criterio di Exploit Guard).
3. Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.
4. Selezionare quindi i componenti di Exploit Guard da gestire con questo criterio. Per ogni componente selezionato è quindi possibile configurare altri dettagli.
   - **Riduzione della superficie di attacco:** configurare le minacce che prendono di mira rispettivamente Office e la posta elettronica e le minacce di scripting da bloccare o controllare. È anche possibile escludere da questa regola cartelle o file specifici.
   - **Accesso controllato alle cartelle:** configurare i criteri di blocco o di controllo e quindi aggiungere le app che possono ignorare questi criteri.  È anche possibile specificare cartelle aggiuntive non protette per impostazione predefinita.
   - **Protezione dagli exploit:**  specificare un file XML contenente le impostazioni per attenuare gli exploit di processi di sistema e app. È possibile esportare queste impostazioni dall'app Windows Defender Security Center in un dispositivo Windows 10.
   - **Protezione di rete:** impostare la protezione di rete in modo da bloccare o controllare l'accesso a domini sospetti.
5. Completare la procedura guidata di creazione del criterio, che potrà in seguito essere distribuito ai dispositivi.

### <a name="deploy-an-exploit-guard-policy"></a>Distribuire un criterio di Exploit Guard     
Dopo aver creato i criteri di Exploit Guard, usare la procedura guidata Deploy Exploit Guard Policy (Distribuzione criterio di Exploit Guard) per distribuirli. A tale scopo, aprire la console di Configuration Manager, passare ad **Asset e conformità** > **Endpoint Protection** e fare clic su **Deploy Exploit Guard Policy** (Distribuzione criterio di Exploit Guard).

## <a name="limited-support-for-cng-certificates"></a>Supporto limitato per i certificati CNG
<!-- 1356191 -->
A partire da questa versione è possibile usare i modelli di certificato delle [API Cryptography: CNG (Cryptography Next Generation)](https://docs.microsoft.com/windows/win32/seccng/cng-features) per gli scenari seguenti:

- Registrazione e comunicazione dei client con un punto di gestione HTTPS.   
- Distribuzione di software e applicazioni con un punto di distribuzione HTTPS.   
- Distribuzione del sistema operativo.  
- Client messaging SDK (con l'aggiornamento più recente) e proxy ISV.   
- Configurazione di Cloud Management Gateway.  

Per usare i certificati CNG, l'autorità di certificazione (CA) deve fornire i modelli di certificato CNG per i computer di destinazione.  I dettagli dei modelli variano in base allo scenario. Le proprietà seguenti, tuttavia, sono obbligatorie:

- Scheda **Compatibilità**

    - L'**autorità di certificazione** deve essere Windows Server 2008 o versione successiva. È consigliabile usare Windows Server 2012.

    - Il **destinatario del certificato** deve essere Windows Vista/Windows Server 2008 o versione successiva. È consigliabile usare Windows 8/Windows Server 2012.

- Scheda **Crittografia**

    - **Categoria provider** deve corrispondere a **Provider di archiviazione chiavi**.  Obbligatorio.

Per ottenere risultati ottimali, è consigliabile creare il nome soggetto da informazioni di Active Directory.  Usare il nome DNS per **Formato del nome soggetto** e includere il nome DNS nel nome soggetto alternativo.  In caso contrario, è necessario fornire queste informazioni quando si registra il dispositivo nel profilo certificato.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descrizioni migliorate per i riavvii in sospeso del computer   <!--1356283 -->
In [Technical Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console) è stata aggiunta la possibilità di identificare i dispositivi in attesa di riavvio dalla console di Configuration Manager.

A partire da questa Technical Preview, la console visualizza dettagli aggiuntivi con informazioni sul processo o sull'azione che richiede il riavvio del computer.

## <a name="device-guard-policy-changes----1355092---"></a>Modifiche apportate ai criteri di Device Guard <!-- 1355092 -->
Con la Technical Preview versione 1710 sono state apportate le tre modifiche seguenti relative ai criteri di Device Guard:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Criteri di Device Guard rinominati in criteri di controllo delle applicazioni di Windows Defender
I criteri di Device Guard sono stati rinominati in criteri di controllo delle applicazioni di Windows Defender. Ad esempio la **procedura guidata Crea criterio di Device Guard** è ora denominata **Create Windows Defender Application Control policy wizard** (Creazione di criteri di controllo delle applicazioni di Windows Defender).

### <a name="restart-is-not-required-to-apply-policies"></a>Per applicare i criteri non è necessario riavviare il computer
A partire dall'aggiornamento Fall Creators Update per Windows versione 1709, i dispositivi con la nuova versione di Windows non richiedono un riavvio per applicare i criteri di controllo delle applicazioni di Windows Defender.

Il riavvio è l'impostazione predefinita.

#### <a name="try-it-out"></a>Verifica  

Se si vuole disattivare il riavvio, seguire questa procedura:

1.  Aprire la procedura guidata **Create Windows Defender Application Control Policy** (Creazione di criteri di controllo delle applicazioni di Windows Defender).
2.  Nella pagina **Generale** deselezionare la casella di controllo **Imponi un riavvio dei dispositivi in modo che questo criterio possa essere applicato per tutti i processi**.
3.  Fare clic su **Avanti** fino al termine della procedura guidata.

Per le versioni precedenti di Windows viene ancora imposto un riavvio automatico.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Eseguire automaticamente software considerato attendibile da Intelligent Security Graph

Gli amministratori hanno ora la possibilità di consentire ai dispositivi bloccati l'esecuzione di software considerato attendibile con una buona reputazione secondo Microsoft Intelligent Security Graph (ISG). ISG è costituito da Windows Defender SmartScreen e da altri servizi Microsoft.

Perché il software possa essere considerato attendibile, i dispositivi devono eseguire Windows Defender SmartScreen.

#### <a name="try-it-out"></a>Verifica  

Per consentire a un dispositivo con Windows Defender SmartScreen l'esecuzione di software considerato attendibile, seguire questa procedura:

1.  Aprire la procedura guidata **Create Windows Defender Application Control Policy** (Creazione di criteri di controllo delle applicazioni di Windows Defender).
2.  Nella pagina **Inclusioni** selezionare la casella **Autorizza il software ritenuto attendibile da Intelligent Security Graph**.
3.  Nella casella **File o cartelle attendibili** aggiungere i file e le cartelle che devono essere considerati attendibili.
4.  Fare clic su **Avanti** fino al termine della procedura guidata.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configurare e distribuire i criteri di Windows Defender Application Guard <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) è una nuova funzionalità di Windows che consente di proteggere gli utenti con l'apertura di siti Web non attendibili in un contenitore protetto isolato non è accessibile da altre parti del sistema operativo. In questa versione Technical Preview, è stato aggiunto il supporto per configurare questa funzionalità usando le impostazioni di conformità di Configuration Manager configurate dall'utente e quindi distribuite in una raccolta. Questa funzionalità verrà rilasciata in anteprima per la versione a 64 bit di Windows 10 Creators Update. Per provare ora questa funzionalità è necessario usare una versione di anteprima dell'aggiornamento.

### <a name="before-you-start"></a>Prima di iniziare
Per creare e distribuire i criteri di Windows Defender Application Guard, configurare i dispositivi Windows 10 in cui vengono distribuiti i criteri con un criterio di isolamento rete. Per altre informazioni, vedere il post di blog indicato più avanti. Questa funzionalità funziona solo con le build correnti di Windows 10 Insider. Per provarla, i client devono eseguire una build recente di Windows 10 Insider.

### <a name="try-it-out"></a>Verifica

Per comprendere le nozioni di base relative a Windows Defender Application Guard, leggere [il post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Per creare un criterio e per individuare le impostazioni disponibili:
1. Nella console di **Configuration Manager** scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando il post di blog come riferimento, è possibile selezionare e configurare le impostazioni disponibili per provare la funzionalità.
5. In questa versione è stata aggiunta alla procedura guidata la nuova pagina Definizione di rete. In questa pagina specificare l'identità aziendale e definire il limite della rete aziendale.

    > [!NOTE]
    > I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. In questa versione è possibile creare due tipi diversi di elenchi di isolamento rete, uno da Windows Information Protection e uno da Windows Defender Application Guard, e distribuirli al client. Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo.

    Altre informazioni su come specificare le definizioni di rete sono disponibili nella [documentazione di Windows Information Protection] - [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Al termine, completare la procedura guidata e distribuire il criterio in uno o più dispositivi Windows 10.

### <a name="further-reading"></a>Letture di approfondimento

Per altre informazioni su Windows Defender Application Guard, vedere [questo post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Per altre informazioni sulla modalità autonoma di Windows Defender Application Guard vedere [questo post di blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per Configuration Manager](technical-preview.md).    
