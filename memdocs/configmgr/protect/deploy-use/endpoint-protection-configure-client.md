---
title: Impostazioni client di Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come configurare impostazioni client personalizzate per Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709179"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurare le impostazioni client personalizzate per Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*

Questa procedura consente di configurare impostazioni client personalizzate per Endpoint Protection, distribuibili nelle raccolte di dispositivi nella gerarchia.

> [!IMPORTANT]  
>  Configurare le impostazioni client predefinite per Endpoint Protection solo se si è certi di volerle applicare a tutti i computer nella gerarchia. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Per abilitare Endpoint Protection e configurare impostazioni client personalizzate

1. Nella console di Configuration Manager fare clic su **Amministrazione**.  

2. Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.  

3. Nel gruppo **Crea** della scheda **Home** fare clic su **Crea impostazioni dispositivo client personalizzate**.  

4. Nella finestra di dialogo **Crea impostazioni dispositivo client personalizzate** specificare un nome e una descrizione per il gruppo di impostazioni e quindi selezionare **Endpoint Protection**.  

5. Configurare le impostazioni client per Endpoint Protection che si ritengono necessarie. Per un elenco completo delle impostazioni client per Endpoint Protection che è possibile configurare, vedere la sezione relativa a Endpoint Protection in [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md#endpoint-protection).  

   > [!IMPORTANT]  
   >  Prima di configurare le impostazioni client per Endpoint Protection, installare il ruolo del sistema del sito per Endpoint Protection.  

6. Fare clic su **OK** per chiudere la finestra di dialogo **Crea impostazioni dispositivo client personalizzate** . Le nuove impostazioni client vengono visualizzate nel nodo **Impostazioni client** dell'area di lavoro **Amministrazione** .  

7. Distribuire quindi le impostazioni client personalizzate in una raccolta. Selezionare le impostazioni client personalizzate da distribuire. Nel gruppo **Impostazioni client** della scheda **Home** fare clic su **Distribuisci**.  

8. Nella finestra di dialogo **Seleziona raccolta** scegliere la raccolta in cui distribuire le impostazioni client e quindi fare clic su **OK**. La nuova distribuzione viene visualizzata nella scheda **Distribuzioni** del riquadro dei dettagli.  

I client verranno configurati con queste impostazioni al successivo download dei criteri client. Per altre informazioni, vedere [Avviare il recupero criteri per un client di Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Come effettuare il provisioning del client di Endpoint Protection in un'immagine disco

Installare il client di Endpoint Protection in un computer che si intende usare come origine dell'immagine disco per la distribuzione del sistema operativo in Configuration Manager. In genere questo computer è denominato computer di riferimento. Dopo aver creato l'immagine del sistema operativo, distribuirla usando la distribuzione del sistema operativo in Configuration Manager.

> [!Important]  
> In Windows 10 e Windows Server 2016, Windows Defender è installato per impostazione predefinita. Questa procedura non è necessaria in tali versioni di Windows.  

Usare le procedure descritte di seguito per installare e configurare il client di Endpoint Protection in un computer di riferimento.


### <a name="prerequisites"></a>Prerequisiti

Nell'elenco seguente sono inclusi i prerequisiti necessari per installare il software client di Endpoint Protection in un computer di riferimento.

- È necessario accedere al pacchetto di installazione del client di Endpoint Protection, **scepinstall.exe**. Questo pacchetto si trova nella sottocartella **Client** della cartella di installazione di Configuration Manager nel server del sito.  

- Per distribuire il client di Endpoint Protection con la configurazione richiesta dell'organizzazione, creare ed esportare un criterio antimalware. Specificare quindi tale criterio quando si installa manualmente il client di Endpoint Protection. Per altre informazioni, vedere [Come creare e distribuire criteri antimalware](endpoint-antimalware-policies.md).  

  > [!NOTE]  
  >  L'esportazione di **Criteri antimalware predefiniti del client** non è consentita.  

- Se si vuole installare il client di Endpoint Protection con le definizioni più recenti, scaricarle da [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> A partire da Configuration Manager 1802, non è necessario installare l'agente di Endpoint Protection (SCEPInstall) nei dispositivi Windows 10. Se è già installato nei dispositivi Windows 10, non viene rimosso da Configuration Manager. Gli amministratori possono rimuovere l'agente di Endpoint Protection nei dispositivi Windows 10 che eseguono almeno la versione client 1802. SCEPInstall.exe potrebbe essere ancora presente in C:\Windows\ccmsetup in alcuni computer, ma non verrà scaricato nelle nuove installazioni client. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Come installare il client di Endpoint Protection nel computer di riferimento

Installare il client di Endpoint Protection in locale nel computer di riferimento dal prompt dei comandi. Per prima cosa, ottenere il file di installazione **scepinstall.exe**. Per altre informazioni, vedere [Per installare il client di Endpoint Protection dal prompt dei comandi](#bkmk_manual-install).

Se necessario, includere anche un criterio antimalware preconfigurato oppure uno esportato in precedenza. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a> Per installare il client di Endpoint Protection dal prompt dei comandi

1. Copiare **scepinstall.exe** dalla sottocartella **Client** della cartella di installazione di Configuration Manager al computer in cui si vuole installare il software client di Endpoint Protection.  

2. Aprire un prompt dei comandi come amministratore. Passare alla cartella con il programma di installazione. Eseguire quindi `scepinstall.exe`, aggiungendo le altre proprietà della riga di comando eventualmente necessarie:


   |  Proprietà   |                                  Descrizione                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Eseguire il programma di installazione in modalità invisibile all'utente                           |
   |    `/q`     |                        Estrarre i file di installazione in modalità invisibile all'utente                        |
   |    `/i`     |                           Eseguire il programma di installazione normalmente                           |
   |  `/policy`  | Specificare un file di criteri antimalware per configurare il client durante l'installazione |
   | `/sqmoptin` |     Acconsentire esplicitamente a partecipare al programma Analisi utilizzo software     |


3. Seguire le istruzioni visualizzate per completare l'installazione del client.  

4. Se è stato scaricato il pacchetto con le definizioni più recenti, copiare il pacchetto nel computer client e quindi fare doppio clic sul pacchetto delle definizioni per installarlo.  

   > [!NOTE]  
   >  Al termine dell'installazione del client di Endpoint Protection, il client esegue automaticamente un controllo degli aggiornamenti delle definizioni. Se la ricerca di aggiornamenti viene completata, non è necessario installare manualmente il pacchetto con le definizioni più recenti.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Esempio: installare il client con un criterio antimalware

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Verificare l'installazione del client di Endpoint Protection

Dopo aver installato il client di Endpoint Protection nel computer di riferimento, verificare che il client funzioni correttamente.

1.  Nel computer di riferimento aprire **System Center Endpoint Protection** nell'area di notifica di Windows.  

2.  Nella scheda **Home** della finestra di dialogo **System Center Endpoint Protection** verificare che **Protezione in tempo reale** sia impostato su **Attivato**.  

3.  Verificare che venga visualizzato **Aggiornata** per **Virus and spyware definitions** (Definizioni di virus e spyware).  

4.  Per verificare che il computer di riferimento sia pronto per la creazione dell'immagine, in **Opzioni analisi** selezionare **Completa** e quindi fare clic su **Avvia analisi**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Preparare il client di Endpoint Protection per la creazione dell'immagine

Per preparare il client di Endpoint Protection per la creazione dell'immagine, seguire questa procedura:

1. Nel computer di riferimento eseguire l'accesso come amministratore.  

2. Scaricare e installare **PsExec** da [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Eseguire il prompt dei comandi come amministratore, passare alla cartella in cui si è installato PsTools e quindi digitare il comando seguente:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Prestare attenzione quando si esegue l'editor del Registro di sistema in questo modo. PsExec.exe viene eseguito nel contesto di LocalSystem.  

4. Nell'editor del Registro di sistema eliminare le chiavi del Registro di sistema seguenti:  

   > [!IMPORTANT]  
   >  Eliminare queste chiavi del Registro di sistema come ultimo passaggio prima della creazione dell'immagine del computer di riferimento. Il client di Endpoint Protection ricrea queste chiavi quando viene avviato. Se si riavvia il computer di riferimento, eliminare di nuovo le chiavi del Registro di sistema.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

È ora possibile preparare il computer di riferimento per la creazione dell'immagine.

Quando si distribuisce un'immagine del sistema operativo contenente il client di Endpoint Protection, le informazioni vengono automaticamente segnalate al sito assegnato di Configuration Manager del dispositivo. Il client scarica e applica tutti i criteri antimalware usati.  



## <a name="see-also"></a>Vedere anche

Per altre informazioni sulla distribuzione del sistema operativo in Configuration Manager, vedere [Gestire le immagini del sistema operativo](../../osd/get-started/manage-operating-system-images.md).

