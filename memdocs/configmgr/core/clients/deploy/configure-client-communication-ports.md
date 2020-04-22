---
title: Configurare le porte di comunicazione client
titleSuffix: Configuration Manager
description: Impostare le porte di comunicazione client in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693559"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Come configurare le porte di comunicazione client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile modificare i numeri di porta richiesti usati dai client di Configuration Manager per comunicare con i sistemi del sito che usano HTTP e HTTPS per le comunicazioni. Anche se è più probabile che HTTP o HTTPS sia già stato configurato per i firewall, la notifica client che utilizza HTTP o HTTPS richiede una memoria e un utilizzo di CPU maggiori nel computer del punto di gestione rispetto all'utilizzo di un numero di porta personalizzato. È possibile specificare anche il numero di porta del sito da usare se si riattivano i client con i pacchetti di riattivazione tradizionali.  

 Quando si specificano le porte di richiesta HTTP e HTTPS, è possibile specificare un numero di porta predefinito e un numero di porta alternativo. I client tentano automaticamente di utilizzare la porta alternativa se la comunicazione con la porta predefinita non riesce. È possibile specificare le impostazioni per la comunicazione dati HTTP e HTTPS.  

 Il valore predefinito per le porte di richiesta client è **80** per il traffico HTTP e **443** per il traffico HTTPS. Modificare tali valori solo se non si desidera utilizzare i valori predefiniti. Uno scenario tipico per l'utilizzo di porte personalizzate è quando si utilizza un sito Web personalizzato in IIS anziché il sito Web predefinito. Se si modificano i numeri di porta predefiniti per il sito Web predefinito in IIS e tale sito è utilizzato anche da altre applicazioni, l'esecuzione di queste applicazioni non sarà possibile.  

> [!IMPORTANT]
>  Non modificare i numeri di porta in Configuration Manager senza conoscere le conseguenze. Esempi:  
> 
> - Se si modificano i numeri di porta per i servizi di richiesta client come una configurazione sito e i client esistenti non vengono riconfigurati per l'utilizzo dei nuovi numeri di porta, tali client diventeranno non gestiti.  
>   -   Prima di configurare un numero di porta non predefinito, assicurarsi che i firewall e tutti i dispositivi di rete coinvolti siano in grado di supportare questa configurazione e riconfigurarli come necessario. Se i client verranno gestiti in Internet e il numero di porta HTTPS predefinito 443 verrà modificato, i router e i firewall in Internet potrebbero bloccare questa comunicazione.  

 Per assicurasi che i client non assumano lo stato non gestito dopo aver modificato i numeri di porta di richiesta, è necessario che i client vengano configurati per l'utilizzo di nuovi numeri di porta di richiesta. Quando si modificano le porte di richiesta in un sito primario, tutti i siti secondari collegati ereditano automaticamente la stessa configurazione della porta. Utilizzare la procedura in questo argomento per configurare le porte di richiesta nel sito primario.  

> [!NOTE]  
>  Per informazioni su come configurare le porte di richiesta per i client nei computer che eseguono Linux e UNIX, vedere [Configurare le porte richieste per il client per Linux e UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Quando il sito di Configuration Manager viene pubblicato in Servizi di dominio Active Directory, i client nuovi ed esistenti che possono accedere a queste informazioni verranno configurati automaticamente con le impostazioni della porta del sito e non sarà necessario eseguire ulteriori operazioni. I client che non possono accedere a queste informazioni pubblicate in Servizi di dominio Active Directory includono i client del gruppo di lavoro, i client provenienti da un'altra foresta di Active Directory, i client configurati solo per Internet e i client attualmente in Internet. Se si modificano i numeri di porta predefiniti dopo che questi client sono stati installati, reinstallarli e installare eventuali nuovi client utilizzando uno dei metodi seguenti:  

- Reinstallare i client utilizzando l'Installazione push client guidata. L'installazione push client configura automaticamente i client con la configurazione della porta del sito corrente. Per altre informazioni su come usare Installazione guidata push client, vedere [Come installare i client di Configuration Manager usando push client](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

- Reinstallare i client utilizzando le proprietà di installazione CCMSetup.exe e client.msi di CCMHTTPPORT e CCMHTTPSPORT. Per altre informazioni su queste proprietà della riga di comando, vedere [Informazioni sulle proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

- Reinstallare i client utilizzando un metodo che ricerchi le proprietà di installazione client di Configuration Manager in Servizi di dominio Active Directory. Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  Per riconfigurare i numeri di porta per i client esistenti, è inoltre possibile utilizzare lo script PORTSWITCH.VBS fornito con il supporto di installazione nella cartella SMSSETUP\Tools\PortConfiguration.  

> [!IMPORTANT]  
>  Per i client nuovi ed esistenti attualmente in Internet, è necessario configurare i numeri di porta non predefiniti utilizzando le proprietà CCMSetup.exe e client.msi di CCMHTTPPORT e CCMHTTPSPORT.  

 Dopo aver modificato le porte di richiesta nel sito, i nuovi client installati utilizzando il metodo di installazione push client a livello di sito verranno configurati automaticamente con i numeri di porta correnti per il sito.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Per configurare i numeri di porta di comunicazione client per un sito  

1. Nella console di Configuration Manager fare clic su **Amministrazione**.  

2. Nell'area di lavoro **Amministrazione** espandere **Configurazione sito**, quindi fare clic su **Siti**e selezionare il sito primario da configurare.  

3. Nella scheda **Home** fare clic su **Proprietà**, quindi sulla scheda **Porte** .  

4. Selezionare gli elementi necessari e fare clic sull'icona Proprietà per visualizzare la finestra di dialogo **Dettagli porta** .  

5. Nella finestra di dialogo **Dettagli porta** specificare il numero di porta e la descrizione dell'elemento e quindi fare clic su **OK**.  

6. Selezionare **Utilizza sito Web personalizzato** se si utilizzerà il nome sito Web personalizzato **SMSWeb** per i sistemi del sito che eseguono IIS.  

7. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà per il sito.  

   Ripetere questa procedura per tutti i siti primari nella gerarchia.
