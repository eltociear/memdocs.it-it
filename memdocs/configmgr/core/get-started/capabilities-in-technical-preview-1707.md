---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1707 per Configuration Manager.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705139"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Funzionalità della versione Technical Preview 1707 per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo presenta le funzionalità disponibili nella Technical Preview per Configuration Manager versione 1707. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire commenti e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Problemi noti di questa versione Technical Preview:**
- **L'aggiornamento alla versione Technical Preview 1707 ha esito negativo se il server del sito è in modalità passiva**. Quando si esegue la versione Technical Preview 1706 ed è presente un [server del sito primario in modalità passiva](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima di poter aggiornare il sito Technical Preview alla versione 1707. Sarà possibile reinstallare il server del sito in modalità passiva quando nel sito è in esecuzione la versione 1707.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.



**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Supporto della peer cache del client per i file di installazione rapida per Windows 10 e Office 365
<!-- 1352486 -->
A partire da questa versione, la peer cache supporta la distribuzione dei file di installazione rapida del contenuto per Windows 10 e dei file di aggiornamento per Office 365. Non sono richieste configurazioni aggiuntive.

## <a name="surface-device-dashboard"></a>Dashboard del dispositivo Surface
<!--1355788-->
Il dashboard del dispositivo Surface visualizza informazioni sui dispositivi Surface rilevati nell'ambiente in uso. Nella console passare a **Monitoraggio** > **Surface Devices** (Dispositivi Surface). È possibile visualizzare le seguenti informazioni:
- percentuale di dispositivi Surface
- percentuale di modelli Surface
- prime cinque versioni del sistema operativo

Fare clic su una sezione del grafico dei **modelli Surface** per un elenco completo dei dispositivi.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurare e distribuire i criteri di Windows Defender Application Guard
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) è una nuova funzionalità di Windows che consente di proteggere gli utenti con l'apertura di siti Web non attendibili in un contenitore protetto isolato non è accessibile da altre parti del sistema operativo. In questa versione Technical Preview, è stato aggiunto il supporto per configurare questa funzionalità usando le impostazioni di conformità di Configuration Manager configurate dall'utente e quindi distribuite in una raccolta. Questa funzionalità verrà rilasciata in anteprima per la versione a 64 bit di Windows 10 Fall Creators Update (nome in codice: RS3). Per provare ora questa funzionalità è necessario usare una versione di anteprima dell'aggiornamento.

### <a name="before-you-start"></a>Prima di iniziare

Per creare e distribuire i criteri di Windows Defender Application Guard, configurare i dispositivi Windows 10 in cui vengono distribuiti i criteri con un criterio di isolamento rete. Per informazioni dettagliate, vedere [questo post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Questa funzionalità funziona solo con le build correnti di Windows 10 Insider. Per provarla, i client devono eseguire una build recente di Windows 10 Insider.

### <a name="try-it-out"></a>Verifica

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Per creare un criterio e per individuare le impostazioni disponibili:

1. Nella console di Configuration Manager scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando il post di blog come riferimento, è possibile selezionare e configurare le impostazioni disponibili per provare la funzionalità.
5. In questa versione è stata aggiunta alla procedura guidata la nuova pagina **Definizione di rete**. Usare questa pagina per specificare l'identità aziendale e definire il limite di rete aziendale.<br>I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. In questa versione è possibile creare due tipi diversi di elenchi di isolamento rete, uno da Windows Information Protection e uno da Windows Defender Application Guard, e distribuirli al client. Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo.
Altre informazioni su come specificare le definizioni di rete sono disponibili nella [documentazione di Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Al termine, completare la procedura guidata e distribuire il criterio in uno o più dispositivi Windows 10.

### <a name="further-reading"></a>Letture di approfondimento
Per altre informazioni su Windows Defender Application Guard, vedere [questo post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Per altre informazioni sulla modalità autonoma di Windows Defender Application Guard vedere [questo post di blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Aggiungere i parametri quando si distribuiscono gli script di PowerShell da Configuration Manager

<!-- 1236459 --->

Nell'ultima versione Technical Preview è stata introdotta una nuova funzionalità che consente di [creare ed eseguire script di PowerShell dalla console di Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
La funzionalità è stata espansa in questa versione Technical Preview. Configuration Manager ora legge lo script di PowerShell e visualizza tutti i parametri nella procedura guidata Crea script. È possibile specificare nella procedura guidata un valore per il parametro che verrà usato durante l'esecuzione dello script. In alternativa, è possibile omettere il parametro. In questo caso è necessario specificare un valore per il parametro quando si esegue lo script.
In questa versione Technical Preview è necessario specificare gli eventuali parametri richiesti dagli script. Nelle versioni future la definizione dei parametri degli script diventerà facoltativa.

### <a name="try-it-out"></a>Verifica

1. Seguire le istruzioni per [creare ed eseguire script di PowerShell dalla console di Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. Nella nuova pagina **Parametri script** della **procedura guidata Crea script** scegliere un parametro e quindi fare clic su **Modifica**.
3. Specificare un valore di parametro per il parametro selezionato e quindi fare clic su **OK**.
4. Completare la procedura guidata.

Quando viene eseguito lo script, verranno usati i valori dei parametri configurati.
