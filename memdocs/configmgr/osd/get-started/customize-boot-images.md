---
title: 'Personalizzare le immagini di avvio '
titleSuffix: Configuration Manager
description: Informazioni su diversi modi di usare Configuration Manager o lo strumento da riga di comando Gestione e manutenzione immagini distribuzione (DISM) per personalizzare un'immagine d'avvio.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e486ddd8652529000c6ec02266f677e45669111
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708999"
---
# <a name="customize-boot-images-with-configuration-manager"></a>Personalizzare le immagini d'avvio con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Ogni versione di Configuration Manager supporta una versione specifica di Windows Assessment and Deployment Kit (Windows ADK). È possibile aggiornare o personalizzare le immagini d'avvio dalla console di Configuration Manager quando sono basate su una versione di Windows PE dalla versione supportata di Windows ADK. Per altre immagini di avvio, è necessario personalizzarle usando un altro metodo, come ad esempio usando lo strumento della riga di comando Deployment Image Servicing and Management (DISM) che fa parte di Windows AIK e Windows ADK.  

 Di seguito sono riportate la versione supportata di Windows ADK, la versione Windows PE su cui si basa l'immagine d'avvio che può essere personalizzata dalla console di Configuration Manager e le versioni Windows PE su cui è basata l'immagine d'avvio che è possibile personalizzare usando DISM e aggiungere a Configuration Manager.  

- **Versione di Windows ADK**  

   Windows ADK per Windows 10  

- **Versioni di Windows PE per le immagini d'avvio personalizzabili dalla console di Configuration Manager**  

   Windows PE 10  

- **Versioni di Windows PE supportate per le immagini d'avvio non personalizzabili dalla console di Configuration Manager**  

   Windows PE 3.1<sup>1</sup> e Windows PE 5  

   <sup>1</sup> È possibile aggiungere un'immagine d'avvio a Configuration Manager solo se è basata su Windows PE 3.1. Installare il supplemento Windows AIK per Windows 7 SP1 per aggiornare Windows AIK per Windows 7 (basato su Windows PE 3) con il supplemento Windows AIK per Windows 7 SP1 (basato su Windows PE 3.1). È possibile scaricare il supplemento Windows AIK per Windows 7 SP1 dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

   Ad esempio, se si ha Configuration Manager, è possibile personalizzare le immagini d'avvio da Windows ADK per Windows 10 (basato su Windows PE 10) dalla console di Configuration Manager. Tuttavia, anche se le immagini di avvio basate su Windows PE 5 sono supportate, è necessario personalizzarle da un computer diverso e usare la versione di Gestione e manutenzione immagini distribuzione installata con Windows AIK per Windows 8. È quindi possibile aggiungere l'immagine d'avvio alla console di Configuration Manager.  

  Le procedure in questo argomento illustrano come aggiungere i componenti facoltativi richiesti da Configuration Manager all'immagine di avvio usando i seguenti pacchetti Windows PE:  

- **WinPE-WMI**: aggiunge il supporto di Strumentazione gestione Windows (WMI).  

- **WinPE-Scripting**: aggiunge il supporto di Windows Script Host (WSH).  

- **WinPE-WDS-Tools**: installa gli strumenti dei Servizi di distribuzione Windows.  

  È possibile aggiungere altri pacchetti Windows PE. Le seguenti risorse forniscono più informazioni sui componenti facoltativi che è possibile aggiungere all'immagine di avvio.  

- Per Windows PE 5, vedere [WinPE: aggiungere pacchetti (informazioni di riferimento sui componenti facoltativi)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

- Per Windows PE 3.1, vedere l'argomento [Aggiungi un pacchetto a un'immagine Windows PE](https://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) nella libreria della documentazione TechNet per Windows 7.  

> [!NOTE]
>All'avvio di WinPE da un'immagine di avvio personalizzata che include strumenti aggiunti dall'utente, è possibile aprire un prompt dei comandi da WinPE e digitare il nome del file dello strumento per eseguirlo. La posizione di questi strumenti viene aggiunta automaticamente alla variabile di percorso. Il prompt dei comandi può essere aggiunto solo se l'impostazione **Abilita supporto comandi (solo test)** è selezionata nella scheda **Personalizzazione** nella finestra delle proprietà dell'immagine di avvio.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Personalizzare un'immagine d'avvio che usa Windows PE 5  
 Per personalizzare un'immagine d'avvio che usa Windows PE 5 è necessario installare Windows ADK e usare lo strumento da riga di comando Gestione e manutenzione immagini distribuzione per montare l'immagine d'avvio, aggiungere componenti e driver facoltativi e salvare le modifiche nell'immagine d'avvio. Usare la seguente procedura per personalizzare l'immagine di avvio.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Per personalizzare un'immagine d'avvio che usa Windows PE 5  

1. Installare Windows ADK in un computer che non ha un'altra versione di Windows AIK o Windows ADK né componenti di Configuration Manager installati.  

2. Scaricare Windows ADK per Windows 8.1 dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=39982).  

3. Copiare l'immagine d'avvio (wimpe.wim) dalla cartella di installazione di Windows ADK (ad esempio, <*Percorso installazione*>\Windows Kits\\<*versione*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 or amd64*>\\<*locale*>) in una cartella di destinazione nel computer da cui si personalizzerà l'immagine d'avvio. Questa procedura usa C:\WinPEWAIK come nome della cartella di destinazione.  

4. Usare DISM per montare l'immagine di avvio in una cartella locale di Windows PE. Ad esempio, digitare la seguente riga di comando:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Dove C:\WinPEWAIK è la cartella che contiene l'immagine di avvio e C:\WinPEMount è la cartella montata.  

   > [!NOTE]
   >  Per altre informazioni su DISM, vedere l'argomento [DISM - Guida tecnica Gestione e manutenzione immagini distribuzione](https://technet.microsoft.com/library/hh824821.aspx) nella libreria della documentazione TechNet per Windows 8.1 e Windows 8.

5. Dopo avere montato l'immagine di avvio, usare DISM per aggiungere componenti facoltativi all'immagine di avvio. In Windows PE 5 i componenti facoltativi a 64 bit si trovano in <*Percorso di installazione*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

   > [!NOTE]
   >  Questa procedura usa il percorso seguente per i componenti facoltativi: C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Ambiente preinstallazione di Windows\amd64\WinPE_OCs. Il percorso da usare potrebbe essere diverso a seconda della versione e delle opzioni di installazione scelte per Windows ADK.  

    Digitare quanto segue per installare i componenti facoltativi:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Ambiente preinstallazione di Windows\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-SecureStartup_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Ambiente preinstallazione di Windows\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WMI_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Ambiente preinstallazione di Windows\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-Scripting** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Ambiente preinstallazione di Windows\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WDS-Tools_** *<locale\>* **.cab"**  

    Dove C:\WinPEMount è la cartella montata e impostazioni locali sono le impostazioni locali per i componenti. Ad esempio, per l'impostazione locale **en-us** , digitare:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  Per altre informazioni sui componenti facoltativi che è possibile aggiungere all'immagine di avvio, vedere l'argomento [Guida componenti facoltativi Windows PE](https://technet.microsoft.com/library/hh824926.aspx) nella libreria della documentazione TechNet per Windows 8.1 e Windows 8.  

6. Usare DISM per aggiungere specifici driver all'immagine di avvio, se necessario. Digitare quanto segue per aggiungere driver all'immagine di avvio:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *path to driver .inf file* **>**  

    Dove C:\WinPEMount è la cartella montata.  

7. Digitare quanto segue per smontare il file dell'immagine di avvio e salvare le modifiche.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Dove C:\WinPEMount è la cartella montata.  

8. Aggiungere l'immagine di avvio aggiornata a Configuration Manager per renderla disponibile per l'uso nelle sequenze di attività. Usare i seguenti passaggi per importare l'immagine di avvio aggiornata:  

   1. Nella console di Configuration Manager fare clic su **Raccolta software**.  

   2. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

   3. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi immagine di avvio** per avviare l'Aggiunta guidata immagine d'avvio.  

   4. Nella pagina **Origine dati** specificare le seguenti opzioni e quindi fare clic su **Avanti**.  

      - Nella casella **Percorso** , specificare il percorso all'immagine di avvio aggiornata. Il percorso specificato deve essere un percorso di rete valido in formato UNC. Ad esempio:  **\\\\<** <em>nomeserver</em> **>\\<** <em>condivisione WinPEWAIK</em> **>\winpe.wim**.  

      - Selezionare l'immagine di avvio dall'elenco a discesa **Immagine di avvio** . Se il file WIM contiene più immagini di avvio, viene elencata ogni immagine.  

   5. Nella pagina **Generale** specificare le seguenti opzioni e quindi fare clic su **Avanti**.  

      -   Nella casella **Nome** specificare un nome univoco per l'immagine di avvio.  

      -   Nella casella **Versione** specificare un numero di versione per l'immagine di avvio.  

      -   Nella casella **Commento** specificare una breve descrizione di come viene usata l'immagine di avvio.  

   6. Completare la procedura guidata.  

9. È possibile attivare una shell dei comandi nell'immagine di avvio per eseguire il debug e la risoluzione dei problemi in Windows PE. Usare i seguenti passaggi per attivare la shell dei comandi.  

   1. Nella console di Configuration Manager fare clic su **Raccolta software**.  

   2. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

   3. Individuare la nuova immagine di avvio nell'elenco e identificare l'ID del pacchetto per l'immagine. È possibile trovare l'ID del pacchetto nella colonna **ID immagine** per l'immagine di avvio.  

   4. Da un prompt dei comandi, digitare **wbemtest** per aprire il Tester di Strumentazione gestione Windows.  

   5. Digitare **\\\\<** <em>Computer provider SMS</em> **>\root\sms\site_<** <em>codicesito</em> **>** in **Spazio dei nomi** e quindi fare clic su **Connetti**.  

   6. Fare clic su **Apri istanza**, digitare **sms_bootimagepackage.packageID="<IDpacchetto\>"** e quindi fare clic su **OK**. Per packageID, immettere il valore identificato nel passaggio 3.  

   7. Fare clic su **Aggiorna oggetto**e quindi fare clic su **EnableLabShell** nel riquadro **Proprietà** .  

   8. Fare clic su **Modifica proprietà**, impostare il valore su **TRUE**e fare clic su **Salva proprietà**.  

   9. Fare clic su **Salva oggetto**e quindi chiudere il tester di Strumentazione gestione Windows.  

10. È necessario distribuire l'immagine di avvio ai punti di distribuzione, ai gruppi di punti di distribuzione o alle raccolte associate ai gruppi di punti di distribuzione prima di poter usare l'immagine di avvio in una sequenza di attività. Usare i seguenti passaggi per distribuire l'immagine di avvio.  

    1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

    2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

    3.  Fare clic sull'immagine di avvio identificata nel passaggio 3.  

    4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Aggiorna punti di distribuzione**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Personalizzare un'immagine di avvio che usa Windows PE 3.1  
 Per personalizzare un'immagine di avvio che usa WinPE 3.1, è necessario installare Windows AIK, installare il supplemento Windows AIK per Windows 7 SP1 e usare lo strumento della riga di comando DISM per montare l'immagine di avvio, aggiungere componenti e driver facoltativi e salvare le modifiche all'immagine di avvio. Usare la seguente procedura per personalizzare l'immagine di avvio.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Personalizzare un'immagine di avvio che usa Windows PE 3.1  

1. Installare Windows AIK in un computer che non ha un'altra versione di Windows AIK o Windows ADK né componenti di Configuration Manager installati. Scaricare Windows AIK dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=5753).  

2. Installare Windows AIK Supplement per Windows 7 con SP1 nel computer dal passaggio 1. Scaricare Windows AIK per Windows 7 SP1 dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

3. Copiare l'immagine di avvio (wimpe.wim) dalla cartella di installazione Windows AIK (ad esempio *PercorsoInstallazione*>\Windows AIK\Tools\PETools\amd64\\) in una cartella nel computer da cui si personalizzerà l'immagine di avvio. Questa procedura usa C:\WinPEWAIK come nome della cartella.  

4. Usare DISM per montare l'immagine di avvio in una cartella locale di Windows PE. Ad esempio, digitare la seguente riga di comando:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Dove C:\WinPEWAIK è la cartella che contiene l'immagine di avvio e C:\WinPEMount è la cartella montata.  

   > [!NOTE]
   >  Per altre informazioni su DISM, vedere l'argomento [Documentazione tecnica su Gestione e manutenzione immagini](https://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) nella libreria della documentazione TechNet per Windows 7.  

5. Dopo avere montato l'immagine di avvio, usare DISM per aggiungere componenti facoltativi all'immagine di avvio. In Windows PE 3.1, ad esempio, i componenti facoltativi si trovano in <*PercorsoInstallazione*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

   > [!NOTE]
   >  Questa procedura usa il percorso seguente per i componenti facoltativi: C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Il percorso da usare potrebbe essere diverso a seconda delle opzioni di installazione e della versione scelte per Windows AIK.  

    Digitare quanto segue per installare i componenti facoltativi:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wmi_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-scripting_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wds-tools_** *<locale\>* **.cab"**  

    Dove C:\WinPEMount è la cartella montata e impostazioni locali sono le impostazioni locali per i componenti. Ad esempio, per l'impostazione locale **en-us** , digitare:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Programmi\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  Per altre informazioni sui diversi pacchetti che è possibile aggiungere all'immagine di avvio, vedere l'argomento [Aggiungere un pacchetto a un'immagine di Windows PE](https://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) nella libreria della documentazione TechNet per Windows 7.  

6. Usare DISM per aggiungere specifici driver all'immagine di avvio, se necessario. Se necessario, digitare quanto segue per aggiungere driver all'immagine di avvio:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *path to driver .inf file* **>**  

    Dove C:\WinPEMount è la cartella montata.  

7. Digitare quanto segue per smontare il file dell'immagine di avvio e salvare le modifiche.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Dove C:\WinPEMount è la cartella montata.  

8. Aggiungere l'immagine di avvio aggiornata a Configuration Manager per renderla disponibile per l'uso nelle sequenze di attività. Usare i seguenti passaggi per importare l'immagine di avvio aggiornata:  

   1. Nella console di Configuration Manager fare clic su **Raccolta software**.  

   2. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

   3. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi immagine di avvio** per avviare l'Aggiunta guidata immagine d'avvio.  

   4. Nella pagina **Origine dati** specificare le seguenti opzioni e quindi fare clic su **Avanti**.  

      - Nella casella **Percorso** , specificare il percorso all'immagine di avvio aggiornata. Il percorso specificato deve essere un percorso di rete valido in formato UNC. Ad esempio:  **\\\\<** <em>nomeserver</em> **>\\<** <em>condivisione WinPEWAIK</em> **>\winpe.wim**.  

      - Selezionare l'immagine di avvio dall'elenco a discesa **Immagine di avvio** . Se il file WIM contiene più immagini di avvio, viene elencata ogni immagine.  

   5. Nella pagina **Generale** specificare le seguenti opzioni e quindi fare clic su **Avanti**.  

      -   Nella casella **Nome** specificare un nome univoco per l'immagine di avvio.  

      -   Nella casella **Versione** specificare un numero di versione per l'immagine di avvio.  

      -   Nella casella **Commento** specificare una breve descrizione di come viene usata l'immagine di avvio.  

   6. Completare la procedura guidata.  

9. È possibile attivare una shell dei comandi nell'immagine di avvio per eseguire il debug e la risoluzione dei problemi in Windows PE. Usare i seguenti passaggi per attivare la shell dei comandi.  

   1. Nella console di Configuration Manager fare clic su **Raccolta software**.  

   2. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

   3. Individuare la nuova immagine di avvio nell'elenco e identificare l'ID del pacchetto per l'immagine. È possibile trovare l'ID del pacchetto nella colonna **ID immagine** per l'immagine di avvio.  

   4. Da un prompt dei comandi, digitare **wbemtest** per aprire il Tester di Strumentazione gestione Windows.  

   5. Digitare **\\\\<** <em>Computer provider SMS</em> **>\root\sms\site_<** <em>codicesito</em> **>** in **Spazio dei nomi** e quindi fare clic su **Connetti**.  

   6. Fare clic su **Apri istanza**, digitare **sms_bootimagepackage.packageID="<IDpacchetto\>"** e quindi fare clic su **OK**. Per packageID, immettere il valore identificato nel passaggio 3.  

   7. Fare clic su **Aggiorna oggetto**e quindi fare clic su **EnableLabShell** nel riquadro **Proprietà** .  

   8. Fare clic su **Modifica proprietà**, impostare il valore su **TRUE**e fare clic su **Salva proprietà**.  

   9. Fare clic su **Salva oggetto**e quindi chiudere il tester di Strumentazione gestione Windows.  

10. È necessario distribuire l'immagine di avvio ai punti di distribuzione, ai gruppi di punti di distribuzione o alle raccolte associate ai gruppi di punti di distribuzione prima di poter usare l'immagine di avvio in una sequenza di attività. Usare i seguenti passaggi per distribuire l'immagine di avvio.  

    1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

    2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

    3.  Fare clic sull'immagine di avvio identificata nel passaggio 3.  

    4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Aggiorna punti di distribuzione**.  
