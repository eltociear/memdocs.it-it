---
title: Configurare Endpoint Protection in un client autonomo
titleSuffix: Configuration Manager
description: Informazioni su come configurare Endpoint Protection in un client autonomo.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758313"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Configurare Endpoint Protection in un client autonomo

*Si applica a: Configuration Manager (Current Branch)*

È possibile che l'organizzazione abbia un certo un numero di client autonomi che non è possibile gestire o proteggere con Microsoft Endpoint Configuration Manager. Senza la protezione degli endpoint, questi client autonomi sono vulnerabili a potenziali attacchi malware. Per proteggere tali client autonomi, è possibile configurarli manualmente con Endpoint Protection, come descritto in questo argomento.

Per configurare Endpoint Protection in un client autonomo manualmente:

- [Creare criteri antimalware per il client autonomo](#create-an-antimalware-policy-for-the-standalone-client)
- [Trasferire il pacchetto di installazione del client Endpoint Protection nel client autonomo](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Installare Endpoint Protection nel client autonomo](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Prerequisiti

Di seguito sono riportati i prerequisiti per la configurazione di Endpoint Protection in un client autonomo:

- È necessario accedere al pacchetto di installazione del client di Endpoint Protection, **scepinstall.exe**. Questo pacchetto è disponibile nella cartella **C:\Programmi\Microsoft Configuration Manager\Client**. 
- Verificare che sia installato l'[aggiornamento della piattaforma antimalware di gennaio 2017 per i client Endpoint Protection](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie). 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Creare criteri antimalware per il client autonomo

In questo passaggio si creano criteri antimalware personalizzati nella console di Configuration Manager e quindi li si trasferisce nel client autonomo.

Quando si creano i criteri antimalware, è necessario configurare l'origine degli aggiornamenti delle definizioni per mantenere aggiornate le definizioni dei criteri nel client autonomo. È possibile configurare [Microsoft Update](endpoint-definitions-microsoft-updates.md) e [Microsoft Malware Protection Center](endpoint-definitions-protection-center.md) come origine degli aggiornamenti delle definizioni, se il client autonomo è connesso a Internet. In alternativa, selezionare [condivisione di rete](endpoint-definitions-network.md) come origine di distribuzione delle definizioni e aggiornarla periodicamente con il pacchetto di aggiornamento delle definizioni più recente. 

Per creare criteri antimalware per il client autonomo:

1. Nella console di **Configuration Manager** fare clic su **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection**e quindi fare clic su **Criteri antimalware**.
3. Nel **Home** nella scheda il **Crea** di gruppo, fare clic su **Crea criterio Antimalware**.
4. Nel **Generale** sezione del **Crea criterio Antimalware** finestra di dialogo immettere un nome e una descrizione per il criterio.
5. Nel **Crea criterio Antimalware** finestra di dialogo, configurare le impostazioni necessarie per il criterio antimalware, quindi fare clic su **OK**. Per un elenco di impostazioni configurabili, vedere [Elenco di impostazioni di criteri antimalware](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > Per l'impostazione **Aggiornamenti delle definizioni** selezionare **Aggiornamenti distribuiti da Microsoft Update** e **Aggiornamenti distribuiti da Microsoft Malware Protection Center** se il client autonomo è connesso a Internet.  
    > In alternativa, selezionare **Aggiornamenti dalle condivisioni file UNC** per distribuire le definizioni dei criteri tramite la condivisione di rete. Aggiungere quindi uno o più percorsi UNC al percorso dei file degli aggiornamenti delle definizioni in una condivisione di rete.

6. Esportare i criteri appena creati come XML:
    1. Nell'elenco **Criteri antimalware** fare clic con il pulsante destro del mouse sui criteri.
    1. Selezionare **Esporta**.
    1. Salvare i criteri in un file XML, ad esempio **standalone.xml**.
7. Trasferire il nuovo file XML dei criteri antimalware nel client autonomo di destinazione in cui si vuole configurare Endpoint Protection.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Trasferire il pacchetto di installazione del client Endpoint Protection nel client autonomo

In questo passaggio si copia il pacchetto di installazione del client Endpoint Protection (**scepinstall.exe**) dal server di Configuration Manager e lo si trasferisce nel client autonomo.

1. Accedere al server di Configuration Manager.
2. Passare alla cartella **Client** della cartella di installazione di Configuration Manager (**C:\Programmi\Microsoft Configuration Manager\Client**).
3. Copiare **scepinstall.exe**.
4. Trasferire **scepinstall.exe** nel client autonomo di destinazione in cui si vuole installare il software del client Endpoint Protection.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Installare Endpoint Protection nel client autonomo
In questo passaggio vengono eseguiti il pacchetto del programma di installazione (**scepinstall.exe**) e i criteri antimalware (entrambi trasferiti in precedenza dal server di Configuration Manager) dal prompt dei comandi nel client autonomo.

Per installare Endpoint Protection nel client autonomo:

1. Nel client autonomo aprire un prompt dei comandi come amministratore.
2. Passare alla cartella in cui è stato salvato il file del programma di installazione **scepinstall.exe**.
3. Immettere il comando seguente per eseguire **scepinstall.exe** con i criteri antimalware:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Sostituire `full path` con il percorso in cui è stato salvato il file XML dei criteri antimalware e `policy file` con il nome del file dei criteri antimalware.
 
    Il programma di installazione viene estratto e viene avviata l'installazione guidata.

4. Seguire le istruzioni visualizzate per completare l'installazione del client.

    Nell'ultima schermata dell'installazione guidata l'opzione per eseguire l'analisi del computer per individuare potenziali minacce dopo aver ricevuto gli aggiornamenti più recenti è selezionata per impostazione predefinita. È possibile deselezionare la casella di controllo per ignorare l'analisi.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Modificare le impostazioni dei criteri antimalware in un client Endpoint Protection autonomo

Per modificare o aggiornare i criteri antimalware nel client Endpoint Protection autonomo: 

1. [Creare criteri antimalware per il client autonomo](#create-an-antimalware-policy-for-the-standalone-client).
2. Eseguire il comando seguente nel client autonomo:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Sostituire `full path` con il percorso in cui è stato salvato il nuovo file XML dei criteri antimalware e `policy file` con il nome del file dei criteri antimalware.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare Endpoint Protection per gestire la sicurezza e i malware nei computer client di Configuration Manager, vedere [Configurare Endpoint Protection](endpoint-protection-configure.md).