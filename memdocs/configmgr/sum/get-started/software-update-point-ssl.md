---
title: "Esercitazione: Configurare un punto di aggiornamento software per l'uso di TLS/SSL con un certificato PKI"
titleSuffix: Configuration Manager
description: "Esercitazione: Configurare i server Windows Server Update Services (WSUS) e i punti di aggiornamento software per l'uso di TLS/SSL con un certificato PKI."
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: e8359077ac363d2d732b2ffa6712c9b938a2c709
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718932"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>Esercitazione: Configurare un punto di aggiornamento software per l'uso di TLS/SSL con un certificato PKI

*Si applica a: Configuration Manager (Current Branch)*

La configurazione dei server Windows Server Update Services (WSUS) e dei punti di aggiornamento software (SUP, software update point) corrispondenti per l'uso di TLS/SSL può limitare la capacità di utenti malintenzionati di attaccare un client in remoto ed elevare i privilegi. Per garantire l'applicazione dei protocolli di sicurezza ottimali, è consigliabile usare il protocollo TLS/SSL per proteggere l'infrastruttura di aggiornamento software. Questo articolo illustra i passaggi necessari per configurare ogni server WSUS e il punto di aggiornamento software per l'uso di HTTPS. Per altre informazioni sulla protezione di WSUS, vedere l'articolo [Proteggere WSUS con il protocollo Secure Sockets Layer](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) nella documentazione di WSUS.

In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Ottenere un certificato PKI, se necessario
> * Associare il certificato al sito Web Amministrazione di Windows Server Update Services
> * Configurare i servizi Web WSUS in modo che richiedano SSL
> * Configurare l'applicazione WSUS per l'uso di SSL
> * Verificare che la connessione alla console WSUS sia abilitata all'uso di SSL
> * Configurare il punto di aggiornamento software in modo che richieda la comunicazione SSL al server WSUS
> * Verificare la funzionalità con Configuration Manager

## <a name="considerations-and-limitations"></a>Considerazioni e limitazioni

WSUS usa TLS/SSL per l'autenticazione dei computer client e dei server WSUS downstream con il server WSUS upstream. WSUS usa TLS/SSL anche per crittografare i metadati degli aggiornamenti. WSUS non usa TLS/SSL per i file di contenuto di un aggiornamento. I file di contenuto sono firmati e l'hash del file è incluso nei metadati dell'aggiornamento. Prima che i file vengano scaricati e installati dal client, vengono verificati sia la firma digitale sia l'hash. Se il controllo ha esito negativo, l'aggiornamento non viene installato.

Quando si usa TLS/SSL per la protezione di una distribuzione di WSUS, tenere presenti le limitazioni seguenti:

- L'uso di TLS/SSL aumenta il carico di lavoro del server. È probabile che la crittografia di tutti i metadati inviati attraverso la rete provochi una lieve riduzione delle prestazioni.
- Se si usa WSUS con un database SQL Server remoto, la connessione tra il server WSUS e il server di database non è protetta da TLS/SSL. Se la connessione al database deve essere protetta, prendere in considerazione i consigli seguenti:
   - Spostare il database WSUS nel server WSUS.
   - Spostare il server di database remoto e il server WSUS in una rete privata.
   - Distribuire Internet Protocol Security (IPsec) per proteggere il traffico di rete.

Quando si configurano i server WSUS e i relativi punti di aggiornamento software per l'uso di TLS/SSL, può risultare utile applicare gradualmente anche le modifiche alle gerarchie di Configuration Manager di grandi dimensioni. Se si sceglie di applicare gradualmente queste modifiche, iniziare dalla parte inferiore della gerarchia e procedere verso l'alto, terminando con il sito di amministrazione centrale.

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione illustra il metodo più comune per ottenere un certificato da usare con Internet Information Services (IIS). Indipendentemente dal metodo usato dall'organizzazione, assicurarsi che il certificato soddisfi i [requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md) per un punto di aggiornamento software di Configuration Manager. Come per qualsiasi certificato, l'autorità di certificazione deve essere considerata attendibile dai dispositivi che comunicano con il server WSUS.

- Server WSUS con il ruolo punto di aggiornamento software installato
- Prima di abilitare TLS/SSL, verificare di aver seguito le [procedure consigliate](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits) per disabilitare il riciclo e configurare i limiti di memoria per WSUS.
- Una delle due opzioni seguenti:
   - Un certificato PKI appropriato già presente nell'archivio certificati **Personale** del server WSUS.
   - La possibilità di richiedere e ottenere un certificato PKI appropriato per il server WSUS presso l'autorità di certificazione (CA) radice dell'organizzazione.
      - Per impostazione predefinita, la maggior parte dei modelli di certificato che includono il modello di certificato WebServer viene rilasciata solo ad amministratori di dominio. Se l'utente connesso non è un amministratore di dominio, l'account dell'utente dovrà avere l'autorizzazione **Registrazione** per il modello di certificato.

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> Ottenere il certificato dall'autorità di certificazione, se necessario

Se si ha già un certificato appropriato nell'archivio certificati **Personale** del server WSUS, ignorare questa sezione e iniziare con la sezione [Associare il certificato](#bkmk_bind). Per inviare una richiesta di certificato all'autorità di certificazione interna e installare un nuovo certificato, seguire le istruzioni riportate in questa sezione.
 
1. Nel server WSUS aprire un prompt dei comandi amministrativo ed eseguire `certlm.msc`. Per la gestione dei certificati per il computer locale, l'account utente deve essere di tipo amministratore locale.

   Viene visualizzato lo strumento Gestione certificati per il dispositivo locale.

1. Espandere **Personale**, quindi fare clic con il pulsante destro del mouse su **Certificati**.
1. Selezionare **Tutte le attività** e quindi **Richiedi nuovo certificato**.
1. Scegliere **Avanti** per avviare la registrazione del certificato.
1. Scegliere il tipo di certificato da registrare. Lo scopo del certificato è **Autenticazione server** e il modello di certificato Microsoft da usare è **Server Web** o un modello personalizzato in cui **Autenticazione server** è specificata come **Utilizzo chiavi avanzato**. È possibile che vengano richieste ulteriori informazioni per registrare il certificato. In genere è necessario specificare almeno le informazioni seguenti:
   - **Nome comune:** disponibile nella scheda **Oggetto**. Impostare come valore il nome di dominio completo del server WSUS.
   - **Nome descrittivo:** disponibile nella scheda **Generale**. Impostare il valore su un nome descrittivo per facilitare l'identificazione del certificato in un secondo momento.
:::image type="content" source="media/certificate-properties.png" alt-text="Finestra Proprietà certificato che consente di specificare altre informazioni per la registrazione":::
1. Selezionare **Registra** e quindi **Fine** per completare la registrazione.
1. Aprire il certificato se si vuole visualizzarne i dettagli, ad esempio l'identificazione personale del certificato.

> [!TIP]
> Se il server WSUS è connesso a Internet, il certificato deve includere il nome di dominio completo esterno in Oggetto o in Nome alternativo del soggetto (SAN).

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> Associare il certificato al sito di amministrazione di WSUS

Quando il certificato è presente nell'archivio certificati personale del server WSUS, associarlo al sito di amministrazione di WSUS in IIS.

1. Nel server WSUS aprire Gestione Internet Information Services (IIS).
1. Passare a **Siti** > **Amministrazione di Windows Server Update Services**.
1. Selezionare **Binding** dal menu Azione oppure facendo clic con il pulsante destro del mouse sul sito.
1. Nella finestra **Binding sito** selezionare la riga corrispondente a **https** e quindi selezionare **Modifica**.
   - Non rimuovere il binding al sito HTTP. WSUS usa HTTP per i file di contenuti dell'aggiornamento.
1. Nell'opzione **Certificato SSL** scegliere il certificato da associare al sito di amministrazione di WSUS. Il nome descrittivo del certificato viene visualizzato nel menu a discesa. Se non è stato specificato un nome descrittivo, viene visualizzato il campo `IssuedTo` del certificato. Se non si è sicuri del certificato da usare, selezionare **Visualizza** e verificare che l'identificazione personale corrisponda a quella ottenuta.  
   :::image type="content" source="media/edit-site-binding.png" alt-text="Finestra Modifica binding sito con selezione del certificato SSL":::
1. Al termine selezionare **OK** e quindi **Chiudi** per uscire dai binding del sito. Per i passaggi successivi è consigliabile aprire Gestione IIS (Internet Information Services).



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> Configurare i servizi Web WSUS in modo che richiedano SSL

1. In Gestione IIS nel server WSUS passare a **Siti** > **Amministrazione di Windows Server Update Services**.
1. Espandere il sito Amministrazione di Windows Server Update Services in modo da visualizzare l'elenco dei servizi Web e delle directory virtuali per WSUS.
1. Per ognuno dei servizi Web WSUS seguenti:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Apportare le modifiche seguenti:

      1. Selezionare **Impostazioni SSL**.
      1. Selezionare l'opzione **Richiedi SSL**.
      1. Verificare che l'opzione **Certificati client** sia impostata su **Ignora**.
      1. Selezionare **Applica**.

Non configurare le impostazioni SSL sul sito principale di Amministrazione di Windows Server Update Services, perché alcune funzioni, ad esempio i contenuti, devono usare HTTP.

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> Configurare l'applicazione WSUS per l'uso di SSL

Quando i servizi Web sono impostati in modo da richiedere SSL, l'applicazione WSUS deve ricevere una notifica per eseguire alcune operazioni di configurazione aggiuntive per il supporto della modifica.

1. Aprire un prompt dei comandi di amministratore nel server WSUS. L'account utente che esegue questo comando deve essere membro del gruppo WSUS Administrators o del gruppo di amministratori locale.
1. Passare alla cartella degli strumenti di WSUS:  
   `cd "c:\Program Files\Update Services\Tools"`
1. Configurare WSUS per l'uso di SSL con il comando seguente:

    `WsusUtil.exe configuressl server.contoso.com`
   
   Dove *server.contoso.com* è il nome di dominio completo del server WSUS.
1. WsusUtil restituisce l'URL del server WSUS con il numero di porta specificato alla fine. La porta è 8531 (impostazione predefinita) o 443. Verificare che l'URL restituito sia quello previsto. In caso di errori di digitazione è possibile eseguire di nuovo il comando.

   :::image type="content" source="media/wsusutil.png" alt-text="Comando wsusutil configuressl che restituisce l'URL HTTPS per WSUS":::

> [!TIP] 
> Se il server WSUS è con connessione Internet, specificare il nome di dominio completo esterno quando si esegue `WsusUtil.exe configuressl`.

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> Verificare che la console WSUS sia in grado di connettersi tramite SSL

La console di WSUS usa il servizio Web ApiRemoting30 per la connessione. Il punto di aggiornamento software di Configuration Manager usa lo stesso servizio Web per indirizzare WSUS all'esecuzione di determinate azioni, ad esempio:

- Avvio di una sincronizzazione degli aggiornamenti software
- Impostazione del server upstream appropriato per WSUS, che dipende dalla posizione in cui si trova il sito SUP nella gerarchia di Configuration Manager
- Aggiunta o rimozione di prodotti e classificazioni per la sincronizzazione dal server WSUS di livello superiore della gerarchia.
- Rimozione degli aggiornamenti scaduti

Aprire la console di WSUS per verificare che sia possibile usare una connessione SSL al servizio Web ApiRemoting30 del server WSUS. In un secondo momento verranno testati alcuni altri servizi Web.

1. Aprire la console WSUS e selezionare **Azione** > **Connetti al server**.
1. Nell'opzione **Nome server** immettere il nome di dominio completo del server WSUS.
1. Scegliere il **Numero di porta** restituito nell'URL da WSUSutil.
1. L'opzione **Utilizza SSL (Secure Sockets Layer) per la connessione al server** viene abilitata automaticamente quando si sceglie 8531 (impostazione predefinita) o 443.
       :::image type="content" source="media/connect-wsus-console.png" alt-text="Connettersi alla console WSUS tramite la porta HTTPS":::
1. Se il server del sito Configuration Manager è remoto rispetto al punto di aggiornamento software, avviare la console WSUS dal server del sito e verificare che la console sia in grado di connettersi tramite SSL.
   - Se la console WSUS remota non riesce a connettersi, è probabile che sia presente un problema con l'attendibilità del certificato, la risoluzione dei nomi o la porta bloccata.

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> Configurare il punto di aggiornamento software in modo che richieda la comunicazione SSL al server WSUS

Dopo aver configurato WSUS per l'uso di TLS/SSL, è necessario aggiornare anche il punto di aggiornamento software Configuration Manager corrispondente in modo che richieda SSL. Quando si esegue questa modifica, Configuration Manager:

- Verifica di essere in grado di configurare il server WSUS per il punto di aggiornamento software
- Richiede ai client di usare la porta SSL quando devono eseguire l'analisi su questo server WSUS.

Per configurare il punto di aggiornamento software in modo che richieda la comunicazione SSL con il server WSUS, seguire questa procedura: 

1. Aprire la console di Configuration Manager e connettersi al sito di amministrazione centrale o al server del sito primario per il punto di aggiornamento software che è necessario modificare.
1. Passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito**.
1. Selezionare il server del sistema del sito in cui è installato WSUS, quindi selezionare il ruolo del sistema del sito del punto di aggiornamento software.
1. Nella barra multifunzione scegliere **Proprietà**.
1. Abilitare l'opzione **Richiedi comunicazione SSL a server WSUS**.

   :::image type="content" source="media/sup-properties.png" alt-text="Proprietà SUP che visualizzano l'opzione Richiedi comunicazione SSL a server WSUS":::
1. Nel file [**WCM.log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) del sito, quando si applica la modifica vengono visualizzate le voci seguenti:

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

Gli esempi di file di log sono stati modificati in modo da rimuovere le informazioni non necessarie per questo scenario.  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> Verificare la funzionalità con Configuration Manager

### <a name="verify-the-site-server-can-sync-updates"></a>Verificare che il server del sito sia in grado di sincronizzare gli aggiornamenti

1. Connettere la console di Configuration Manager al sito principale.
1. Passare a **Raccolta software** > **Panoramica** > **Aggiornamenti software** > **Tutti gli aggiornamenti software**.
1. Nella barra multifunzione selezionare **Sincronizza aggiornamenti software**.
1. Selezionare **Sì** nella notifica che chiede se si vuole avviare una sincronizzazione nell'intero sito per gli aggiornamenti software.
   - Poiché la configurazione di WSUS è cambiata, viene eseguita una sincronizzazione completa degli aggiornamenti software anziché una sincronizzazione delta.
1. Aprire **wsyncmgr.log** per il sito. Se si sta monitorando un sito figlio, attendere fino a quando il sito padre completa la sincronizzazione. Verificare che il server venga sincronizzato correttamente, esaminando il log per visualizzare voci simili alle seguenti:

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>Verificare che un client sia in grado di rilevare la disponibilità di aggiornamenti

Quando si modifica il punto di aggiornamento software in modo che richieda SSL, i client Configuration Manager ricevono l'URL di WSUS aggiornato quando viene creata una richiesta di percorso per un punto di aggiornamento software. Eseguendo il test di un client è possibile:
-  Determinare se il client considera attendibile il certificato del server WSUS. 
- Determinare se SimpleAuthWebService e ClientWebService per WSUS sono funzionanti.
-  Determinare se la directory virtuale del contenuto WSUS è funzionante, se il client ha ricevuto un contratto di licenza durante l'analisi

1. Identificare un client che esegue l'analisi sul punto di aggiornamento software modificato recentemente per l'uso di TLS/SSL. Usare [Esegui script](../..//apps/deploy-use/create-deploy-scripts.md) con lo script di PowerShell seguente per facilitare l'identificazione di un client:

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. Eseguire un ciclo di analisi degli aggiornamenti software nel client di test. È possibile forzare un'analisi con il seguente script di PowerShell:

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. Esaminare il file **ScanAgent.log** del client per verificare che il messaggio che richiede l'analisi sul punto di aggiornamento software sia stato ricevuto.

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. Esaminare **LocationServices.log** per verificare che il client veda l'URL WSUS corretto.
**LocationServices.log**
   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. Esaminare **WUAHandler.log** per verificare che il client sia in grado di eseguire l'analisi.

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>Passaggi successivi

[Distribuire gli aggiornamenti software](../deploy-use/deploy-software-updates.md)