---
title: Configurare l'infrastruttura di certificazione
titleSuffix: Configuration Manager
description: Informazioni sulla configurazione della registrazione dei certificati in Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 590c6fd336ec19949b5f5b99b25b3104524a52d6
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210112"
---
# <a name="configure-certificate-infrastructure"></a>Configurare l'infrastruttura di certificazione

*Si applica a: Configuration Manager (Current Branch)*

Informazioni sulla configurazione dell'infrastruttura di certificazione in Configuration Manager. Prima di iniziare, verificare gli eventuali prerequisiti riportati in [Prerequisiti per i profili certificato](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Usare questi passaggi per configurare l'infrastruttura per i certificati SCEP o PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Passaggio 1: installare e configurare il servizio Registrazione dispositivi di rete e le dipendenze (solo per certificati SCEP)

 È necessario installare e configurare il servizio del ruolo Servizio di registrazione dispositivi di rete per Servizi certificati Active Directory (AD CS), modificare le autorizzazioni di sicurezza nei modelli del certificato, distribuire un certificato di autenticazione client PKI (Public Key Infrastructure) e modificare il registro per aumentare il limite della dimensione predefinita di IIS (Internet Information Services). Se necessario, occorre configurare anche l'autorità di certificazione (CA) emittente per consentire un periodo di validità personalizzato.  

> [!IMPORTANT]  
>  Prima di configurare Configuration Manager per usare il servizio Registrazione dispositivi di rete, verificare l'installazione e la configurazione del servizio stesso. Se queste dipendenze non funzionano correttamente, sarà difficile risolvere problemi di registrazione dei certificati usando Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Per installare e configurare il servizio Registrazione dispositivi di rete e le dipendenze  

1. Su un server che esegue Windows Server 2012 R2, installare e configurare il ruolo servizio Registrazione dispositivi di rete per il ruolo del server Servizi certificati Active Directory. Per altre informazioni, vedere [Linee guida per il Servizio Registrazione dispositivi di rete](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).

2. Controllare e, se necessario, modificare le autorizzazioni di sicurezza per i modelli di certificato usati dal servizio Registrazione dispositivi di rete:  

   -   Per l'account che esegue la console di Configuration Manager: autorizzazione **Lettura**.  

        Questa autorizzazione è richiesta in modo che durante l'esecuzione di Creazione guidata profilo di certificato è possibile selezionare il modello di certificato che si desidera usare quando si crea profilo delle impostazioni SCEP. La selezione di un modello di certificato implica che alcune impostazioni nella procedura guidata vengano popolate automaticamente. Questo semplifica la configurazione ed evita la selezione di impostazioni che non sono compatibili con i modelli di certificato usati dal servizio Registrazione dispositivi di rete.  

   -   Per l'account del servizio SCEP usato dal pool di applicazioni del servizio Registrazione dispositivi di rete: autorizzazioni **Lettura** e **Registrazione**.  

        Questo non è un requisito specifico di Configuration Manager ma è parte della configurazione del servizio Registrazione dispositivi di rete. Per altre informazioni, vedere [Linee guida per il Servizio Registrazione dispositivi di rete](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).  

   > [!TIP]  
   >  Per identificare i modelli di certificato usati dal servizio Registrazione dispositivi di rete, visualizzare la seguente chiave del Registro di sistema sul server che esegue il servizio Registrazione dispositivi di rete: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Queste sono le autorizzazioni di sicurezza predefinite appropriate per la maggior parte degli ambienti. Tuttavia, è possibile usare una configurazione di protezione alternativa. Per altre informazioni, vedere l'articolo sulla [pianificazione delle autorizzazioni dei modelli di certificato per i profili certificato](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Distribuire a questo server un certificato PKI che supporta l'autenticazione client. Un certificato adatto potrebbe essere già disponibile sul computer in uso oppure potrebbe essere necessario o preferibile distribuire un certificato in modo specifico per questo scopo. Per altre informazioni sui requisiti richiesti per questo certificato, fare riferimento alle informazioni per i server su cui è in esecuzione il modulo criteri di Configuration Manager con il servizio ruolo del servizio Registrazione dispositivi di rete nella sezione **Certificati PKI per i server** dell'argomento [Requisiti dei certificati PKI per Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

   > [!TIP]
   >  Per consentire la distribuzione di questo certificato, è possibile usare le istruzioni relative a [Distribuzione del certificato client per punti di distribuzione](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012), perché i requisiti del certificato sono gli stessi con un'unica eccezione:  
   > 
   > - Non selezionare la casella di controllo **Rendi la chiave privata esportabile** nella scheda **Gestione richiesta** delle proprietà dei modelli di certificato.  
   > 
   >   Non è necessario esportare questo certificato con la chiave privata perché sarà possibile accedere all'archivio del computer locale e selezionarlo quando si configura il modulo criteri di Configuration Manager.  

4. Individuare il certificato principale a cui è collegato il certificato di autenticazione client. Quindi esportare questo certificato CA radice in un file di certificato (.cer). Salvare questo file in un percorso protetto a cui sarà possibile accedere in modo sicuro quando si installa e si configura il server di sistema del sito per il punto di registrazione certificati.  

5. Sullo stesso server usare l'editor del Registro di sistema per incrementare il limite dimensione URL predefinito IIS impostando i seguenti valori DWORD delle chiavi del Registro di sistema in HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

   - Impostare la chiave **MaxFieldLength** su **65534**.  

   - Impostare la chiave **MaxRequestBytes** su **16777216**.  

     Per altre informazioni, vedere l'articolo del supporto tecnico Microsoft[820129: Impostazioni del Registro di sistema Http.sys per Windows](https://support.microsoft.com/help/820129).

6. Sullo stesso server, in Gestione Internet Information Services (IIS), modificare le impostazioni del filtro richieste per l'applicazione /certsrv/mscep, quindi riavviare il server. Nella finestra di dialogo **Modifica impostazioni di filtro richieste** , verificare che le impostazioni **Limiti richiesta** corrispondano alle seguenti:  

   - **Lunghezza contenuto massima consentita (byte)** : **30000000**  

   - **Lunghezza massima URL (byte)** : **65534**  

   - **Lunghezza massima stringa di query in (byte)** : **65534**  

     Per altre informazioni su queste impostazioni e sulla loro configurazione, vedere [Limiti richiesta di IIS](https://docs.microsoft.com/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Per poter richiedere un certificato il cui periodo di validità è inferiore a quello del modello di certificato in uso: Questa configurazione è disabilitata per impostazione predefinita da una CA globale (enterprise). Per abilitare questa opzione in una CA globale (enterprise), usare lo strumento della riga di comando Certutil, quindi arrestare e riavviare il servizio certificati usando i seguenti comandi:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Per altre informazioni, vedere [Strumenti e impostazioni di Servizi certificati](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\)).

8. Verificare che il servizio Registrazione dispositivi di rete sia in funzione usando il collegamento seguente come esempio: `https://server.contoso.com/certsrv/mscep/mscep.dll`. Verrà visualizzata la pagina Web incorporata del servizio Registrazione dispositivi di rete. Questa pagina Web illustra il servizio e spiega che i dispositivi di rete usano l'URL per inviare richieste di certificati.  

   Ora che il servizio Registrazione dispositivi di rete e le dipendenze sono configurate, è possibile installare e configurare il punto di registrazione certificati.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Passaggio 2: installare e configurare il punto di registrazione certificati.

È necessario installare e configurare almeno un punto di registrazione certificati nella gerarchia di Configuration Manager ed è possibile installare questo ruolo del sistema del sito nel sito dell'amministrazione centrale oppure in un sito primario.  

> [!IMPORTANT]  
>  Prima di installare il punto di registrazione certificati, fare riferimento alla sezione dei **requisiti del sistema del sito** nell'argomento relativo alle [configurazioni supportate per Configuration Manager](../../core/plan-design/configs/supported-configurations.md) per i requisiti del sistema operativo e le dipendenze per il punto di registrazione certificati.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Per installare e configurare il punto di registrazione certificati  

1. Nella console di Configuration Manager fare clic su **Amministrazione**.  

2. Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, fare clic su **Server e ruoli del sistema del sito**, quindi selezionare il server che si desidera usare per il punto di registrazione certificati.  

3. Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**.  

4. Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.  

5. Nella pagina **Proxy** fare clic su **Avanti**. Il punto di registrazione certificati non usa le impostazioni del proxy Internet.  

6. Nella pagina **Selezione ruolo del sistema** selezionare **Punto di registrazione certificati** dall'elenco dei ruoli disponibili, quindi fare clic su **Avanti**. 

7. Nella pagina **Modalità di registrazione del certificato** specificare quali richieste devono essere elaborate dal punto di registrazione certificati selezionando **Elabora le richieste di certificati SCEP** o **Elabora le richieste di certificati PFX**. Un punto di registrazione certificati non può elaborare entrambi i tipi di richieste, ma è possibile creare più punti di registrazione se si usano entrambi i tipi di certificato.

   Se si elaborano certificati PFX, è necessario scegliere una CA, Microsoft o Entrust.

8. La pagina **Impostazioni del punto di registrazione certificati** varia a seconda del tipo di certificato:
   - Se si è selezionata l'opzione **Elabora le richieste di certificati SCEP**, configurare quanto segue:
     -   **Nome sito Web**, **Numero porta HTTPS** e **Nome dell'applicazione virtuale** per il punto di registrazione certificati. In questi campi vengono inseriti automaticamente i valori predefiniti. 
     -   **URL per il servizio di registrazione dispositivi di rete e il certificato CA radice**: fare clic su **Aggiungi** e nella finestra di dialogo **Aggiungi URL e certificato CA radice** specificare quanto segue:
         - **URL per il servizio di registrazione dispositivi di rete**: Specificare l'URL nel formato seguente: https:// *<FQDN_server>* /certsrv/mscep/mscep.dll. Ad esempio, se il nome FQDN del server che esegue il servizio Registrazione dispositivi di rete è server1.contoso.com, digitare `https://server1.contoso.com/certsrv/mscep/mscep.dll`.
         - **Certificato CA radice**: Individuare e selezionare il file del certificato (CER) creato e salvato nel **passaggio 1: Installare e configurare il servizio Registrazione dispositivi di rete e le dipendenze**. Questo certificato CA radice consente al punto di registrazione certificati di convalidare il certificato di autenticazione client che verrà usato dal modulo criteri di Configuration Manager.  

   - Se l'opzione **Elabora le richieste di certificati PFX** è selezionata, configurare i dettagli e le credenziali di connessione per la CA selezionata.

     - Per usare Microsoft come CA, fare clic su **Aggiungi** e quindi nella finestra di dialogo **Aggiungi un'autorità di certificazione e un account** specificare quanto segue:
         - **Nome del server dell'autorità di certificazione**: immettere il nome del server dell'autorità di certificazione.
         - **Account dell'autorità di certificazione**: fare clic su **Imposta** per selezionare o creare l'account che dispone delle autorizzazioni per eseguire la registrazione a modelli nell'autorità di certificazione.
         - **Account connessione al punto di registrazione certificati**: selezionare o creare l'account che connette il punto di registrazione certificati al database di Configuration Manager. In alternativa, è possibile usare l'account locale del computer che ospita il punto di registrazione certificati.
         - **Account di pubblicazione di certificati di Active Directory**: selezionare un account o creare un nuovo account che verrà usato per pubblicare i certificati agli oggetti utente in Active Directory.

         - Nella finestra di dialogo **URL per il servizio di registrazione dispositivi di rete e il certificato CA radice** specificare quanto segue e quindi fare clic su **OK**:  

     - Per usare Entrust come CA, specificare:

       - L'**URL del servizio Web MDM**
       - Il nome utente e la password per l'URL.

         Se per definire l'URL del servizio Web Entrust si usa l'API MDM, assicurarsi di usare almeno la versione 9 dell'API, come illustrato nell'esempio seguente:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Le versioni precedenti dell'API non supportano Entrust.

9. Fare clic su **Avanti** e completare la procedura guidata.  

10. Attendere qualche minuto per consentire il completamento dell'installazione, quindi verificare che il punto di registrazione certificati sia installato correttamente usando uno dei seguenti metodi:  

    -   Nell'area di lavoro **Monitoraggio** espandere **Stato del sistema**, fare clic su **Stato componente**e cercare i messaggi di stato dal componente **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   Nel server del sistema del sito usare il file *<Percorso di installazione di ConfigMgr\>* \Logs\crpsetup.log e il file *<Percorso di installazione di ConfigMgr\>* Logs\crpmsi.log. Una corretta installazione restituirà un codice di uscita pari a 0.  

    -   Usando un browser verificare che sia possibile connettersi all'URL del punto di registrazione certificati. Ad esempio, `https://server1.contoso.com/CMCertificateRegistration` Accertarsi che venga visualizzata una pagina di **Errore server** per il nome dell'applicazione con una descrizione HTTP 404.  

11. Individuare il file del certificato esportato per la CA radice che il punto di registrazione certificati ha creato automaticamente nella seguente cartella del computer del server del sito primario: *<Percorso di installazione di ConfigMgr\>* \inboxes\certmgr.box. Salvare questo file in un percorso protetto a cui sarà possibile accedere in modo sicuro quando si installerà il modulo criteri di Configuration Manager nel server che esegue il servizio Registrazione dispositivi di rete.  

    > [!TIP]  
    >  Questo certificato non è immediatamente disponibile in questa cartella. Potrebbe essere necessario attendere (ad esempio, mezz'ora) prima che Configuration Manager copi il file in questo percorso.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Passaggio 3: Installare il modulo criteri di Configuration Manager (solo per certificati SCEP).

È necessario installare e configurare il modulo criteri di Configuration Manager in ogni server specificato nel **passaggio 2: Installare e configurare il punto di registrazione certificati** come **URL per il servizio Registrazione dispositivi di rete** nelle proprietà del punto di registrazione certificati.  

##### <a name="to-install-the-policy-module"></a>Per installare il modulo criteri  

1. Nel server che esegue il servizio Registrazione dispositivi di rete accedere come amministratore di dominio e copiare i seguenti file dalla cartella <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 nei supporti di installazione di Configuration Manager in una cartella temporanea:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Inoltre, se si dispone di una cartella LanguagePack sul supporto di installazione, copiare questa cartella e il relativo contenuto.  

2. Dalla cartella temporanea, eseguire PolicyModuleSetup.exe per avviare l'Installazione guidata del modulo criteri di Configuration Manager.  

3. Nella pagina iniziale della configurazione guidata, fare clic su **Avanti**, accettare le condizioni di licenza, quindi fare clic su **Avanti**.  

4. Nella pagina **Cartella di installazione** accettare la cartella di installazione predefinita per il modulo criteri o specificare una cartella alternativa, quindi fare clic su **Avanti**.  

5. Nella pagina **Punto di registrazione certificati** , specificare l'URL del punto di registrazione certificati usando l'FQDN del server del sistema del sito e il nome dell'applicazione virtuale specificato nelle proprietà del punto di registrazione certificati. Il nome dell'applicazione virtuale predefinito è CMCertificateRegistration. Ad esempio, se il nome FQDN del server del sistema del sito è server1.contoso.com e si è usato il nome dell'applicazione virtuale predefinito, specificare `https://server1.contoso.com/CMCertificateRegistration`.

6. Accettare la porta predefinita **443** o specificare un numero di porta alternativo usato dal punto di registrazione certificati, quindi fare clic su **Avanti**.  

7. Nella pagina **Certificato client per il modulo criteri** individuare e specificare il certificato di autenticazione client distribuito nel **Passaggio 1: Installare e configurare il servizio Registrazione dispositivi di rete e le dipendenze** e quindi fare clic su **Avanti**.  

8. Nella pagina **Certificato punto di registrazione certificati** fare clic su **Sfoglia** per selezionare il file del certificato esportato per la CA radice individuata e salvata alla fine del **Passaggio 2: Installare e configurare il punto di registrazione certificati**.  

   > [!NOTE]  
   >  Se non è stato salvato in precedenza, il file di certificato si trova in <Percorso di installazione di ConfigMgr\>\inboxes\certmgr.box nel computer del server del sito.  

9. Fare clic su **Avanti** e completare la procedura guidata.  

   Per disinstallare il modulo criteri di Configuration Manager, usare **Programmi e funzionalità** nel Pannello di controllo. 

 
Ora che sono stati completati i passaggi di configurazione, si è pronti a distribuire i certificati a utenti e dispositivi creando e distribuendo profili certificato. Per altre informazioni su come creare profili certificato, vedere [Come creare profili certificato in Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  
