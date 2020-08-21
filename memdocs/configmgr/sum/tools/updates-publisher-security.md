---
title: Certificati e sicurezza
titleSuffix: Configuration Manager
description: Gestire certificati e sicurezza per System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc8e31245212136cd67f6f8cac062723c2cabefb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696005"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Gestire certificati e sicurezza per Updates Publisher

*Si applica a: Configuration Manager (Current Branch)*

Le procedure seguenti consentono di configurare l'archivio certificati nel server di aggiornamento, configurare un certificato autofirmato nel computer client e configurare Criteri di gruppo per consentire all'agente di Windows Update installato nei computer di analizzare gli aggiornamenti pubblicati.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configurare l'archivio certificati nel server di aggiornamento
 Updates Publisher usa un certificato digitale per firmare gli aggiornamenti nei cataloghi che pubblica. Affinché un catalogo possa essere pubblicato nel server di aggiornamento, è necessario che il certificato si trovi nell'archivio certificati del server di aggiornamento e nell'archivio certificati del computer con Updates Publisher, se tale computer è remoto rispetto al server di aggiornamento.

La procedura seguente è uno dei diversi metodi possibili per aggiungere il certificato all'archivio certificati nel server di aggiornamento.

### <a name="to-configure-the-certificate-store"></a>Per configurare l'archivio certificati
1.  In un computer con accesso sia al computer con Updates Publisher che al server di aggiornamento fare clic su **Avvia** e quindi su **Esegui**, digitare **MMC** nella casella di testo e quindi fare clic su **OK** per aprire Microsoft Management Console (MMC).

2.  Fare clic su **File** e quindi su **Aggiungi/Rimuovi snap-in**, **Aggiungi**, **Certificati**, **Aggiungi**, selezionare **Account del computer** e quindi fare clic su **Avanti**.

3.  Selezionare **Another computer** (Altro computer), digitare il nome del server di aggiornamento o fare clic su **Sfoglia** per trovare il server di aggiornamento, fare clic su **Fine**, **Chiudi** e quindi fare clic su **OK**.

4.  Espandere **Certificati (*nome server di aggiornamento*)** , espandere **WSUS** e quindi fare clic su **Certificati**.

5.  Nel riquadro dei risultati fare clic sul certificato desiderato, fare clic su **All Tasks** (Tutte le attività) e quindi fare clic su **Esporta**.

6.  Nell'Esportazione guidata certificati usare le impostazioni predefinite per creare un file di esportazione con il nome e il percorso specificati nella procedura guidata. Per procedere al passaggio successivo, è necessario che il file sia disponibile nel server di aggiornamento.

7.  Fare clic con il pulsante destro del mouse su **Autori attendibili** scegliere **All Tasks** (Tutte le attività) e quindi fare clic su **Importa**. Completare l'Esportazione guidata certificati usando il file esportato al Passaggio 6.

8.  Se viene usato un certificato autofirmato, ad esempio **Autori WSUS autofirmato**, fare clic con il pulsante destro del mouse su **Autorità di certificazione radice attendibili**, su **All Tasks** (Tutte le attività) e quindi fare clic su **Importa**. Completare l'Esportazione guidata certificati usando il file esportato al Passaggio 6.

9.  Fare clic con il pulsante destro del mouse su **Certificati (*nome server di aggiornamento*)** , fare clic su **Connetti a un altro computer**, immettere il nome del computer per Updates Publisher e quindi fare clic su **OK**.

10. Se Updates Publisher è remoto rispetto al server di aggiornamento, ripetere i passaggi da 7 a 9 per importare il certificato nell'archivio certificati nel computer di Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configurare un certificato autofirmato nei computer client
Nei computer client, l'agente di Windows Update (WUA) esegue la scansione degli aggiornamenti dal catalogo. Se l'agente non è in grado di individuare il certificato digitale nell'archivio Autori attendibili nel computer locale, questo processo avrà esito negativo. Se per la pubblicazione del catalogo degli aggiornamenti è stato usato un certificato autofirmato, ad esempio **Autori WSUS autofirmato**, tale certificato deve trovarsi anche nell'archivio certificati dell'autorità di certificazione radice attendibile nel computer locale, in modo che l'agente ne possa verificare la validità.

È possibile usare uno dei diversi metodi di configurazione dei certificati sui computer client, ad esempio Criteri di gruppo e l'**Importazione guidata certificati** oppure lo strumento Certutil e la distribuzione del software.

Di seguito è riportato un esempio di come configurare il certificato di firma nei computer client.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Per configurare un certificato autofirmato nei computer client
1. In un computer con accesso al server di aggiornamento fare clic su **Avvia** e quindi su **Esegui**, digitare **MMC** nella casella di testo e quindi fare clic su **OK** per aprire Microsoft Management Console (MMC).

2. Fare clic su **File**, **Aggiungi/Rimuovi snap-in**, **Aggiungi**, **Certificati**, **Aggiungi**, selezionare **Account del computer** e quindi fare clic su **Avanti**.

3. Selezionare **Another computer** (Altro computer), digitare il nome del server di aggiornamento o fare clic su **Sfoglia** per trovare il server di aggiornamento, fare clic su **Fine**, **Chiudi** e quindi fare clic su **OK**.

4. Espandere **Certificati (*nome server di aggiornamento*)** , espandere **WSUS** e quindi fare clic su **Certificati**.

5. Fare clic con il pulsante destro del mouse nel riquadro dei risultati, fare clic su **All Tasks** (Tutte le attività) e quindi fare clic su **Esporta**. Completare l'**Esportazione guidata certificati** usando le impostazioni predefinite per creare un certificato di esportazione con il nome e il percorso specificati nella procedura guidata.

6. Usare uno dei metodi seguenti per aggiungere il certificato usato per firmare il catalogo di aggiornamenti in ogni computer client che userà l'agente di Windows Update per l'analisi degli aggiornamenti nel catalogo. Aggiungere il certificato al computer client seguendo questa procedura:

   -   Per i certificati autofirmati: aggiungere il certificato agli archivi certificati **Autorità di certificazione radice disponibile nell'elenco locale** e **Autori attendibili**.

   -   Per i certificati emessi dall'autorità di certificazione: aggiungere il certificato all'archivio certificati **Autori attendibili**.

   > [!NOTE]
   > L'agente di Windows Update verifica se l'impostazione di Criteri di gruppo **Allow signed content from intranet Microsoft update service location** (Consenti contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet) è abilitata nel computer locale. È necessario abilitare questa impostazione dei criteri per l'agente di Windows Update affinché venga eseguita la scansione degli aggiornamenti che sono stati creati e pubblicati con Updates Publisher. Per altre informazioni sull'abilitazione di questa impostazione di Criteri di gruppo, vedere [Come configurare Criteri di gruppo sui computer client](/previous-versions/bb530967(v=technet.10)).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Configurazione di Criteri di gruppo per consentire all'agente di Windows Update installato nei computer di analizzare gli aggiornamenti pubblicati
Prima che l'agente di Windows Update installato nei computer analizzi gli aggiornamenti creati e pubblicati con Updates Publisher, è necessario abilitare un'impostazione dei criteri per consentire contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet. Quando l'impostazione dei criteri viene abilitata, l'agente di Windows Update accetterà gli aggiornamenti ricevuti tramite un percorso Intranet se tali aggiornamenti sono firmati nell'archivio certificati **Autori attendibili** nel computer locale. Sono disponibili diversi metodi per configurare Criteri di gruppo nei computer dell'ambiente in uso.

Per i computer che non si trovano nel dominio, è possibile configurare una chiave del Registro di sistema che consenta contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet.

Le procedure seguenti illustrano i passaggi di base che possono essere usati per configurare Criteri di gruppo per i computer del dominio e un valore di chiave del Registro di sistema nei computer che non sono presenti nel dominio.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Per configurare Criteri di gruppo per consentire all'agente di Windows Update di analizzare gli aggiornamenti pubblicati
1.  Aprire lo snap-in Editor oggetti Criteri di gruppo in Microsoft Management Console (MMC) con credenziali dotate dei diritti di sicurezza appropriati per la configurazione di Criteri di gruppo.

2.  Fare clic su **Sfoglia** e selezionare il dominio, l'unità organizzativa o gli oggetti Criteri di gruppo collegati al sito in cui il criterio configurato verrà propagato ai computer specificati. Fare clic su **OK**, **Fine**, **Chiudi** e quindi fare clic su **OK**.

3.  Nell'albero della console espandere l'impostazione di Criteri di gruppi selezionata, espandere **Configurazione computer**, **Administrative Templates** (Modelli amministrativi), **Windows Components** (Componenti di Windows) e quindi fare clic su **Windows Update**.

4.  Nel riquadro dei risultati, fare clic con il pulsante destro del mouse su **Allow signed content from intranet Microsoft update service location** (Consenti contenuto firmato dal percorso del servizio di aggiornamento Microsoft nella rete Intranet), fare clic su **Proprietà**, **Abilitato** e quindi fare clic su **OK**.