---
title: Pubblicazione e schema di Active Directory
titleSuffix: Configuration Manager
description: Estendere lo schema di Active Directory per Configuration Manager per semplificare il processo di distribuzione e configurazione dei client.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701549"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Preparare Active Directory per la pubblicazione di siti

*Si applica a: Configuration Manager (Current Branch)*

Quando si estende lo schema di Active Directory per Configuration Manager, si introducono nuove strutture in Active Directory usate dai siti di Configuration Manager per pubblicare le informazioni chiave in una posizione sicura facilmente accessibile ai client.  

Quando si gestiscono client locali, è consigliabile usare Configuration Manager con uno schema di Active Directory esteso. Uno schema esteso può infatti semplificare il processo di distribuzione e configurazione dei client e consente ai client di individuare in modo efficiente le risorse, ad esempio server di contenuto e altri servizi forniti dai diversi ruoli del sistema del sito di Configuration Manager.  

-   Se non si sa quale schema esteso offra una distribuzione di Configuration Manager, vedere [Estensioni dello schema per Configuration Manager](../../../core/plan-design/network/schema-extensions.md).  

-   Se non si usa uno schema esteso, è possibile rilevare i servizi e i server del sistema del sito configurando altri metodi, ad esempio DNS e WINS. Questi metodi di individuazione de della posizione del servizio richiedono configurazioni aggiuntive e non sono il metodo preferito per l'individuazione della posizione del servizio da parte dei client. Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Se lo schema di Active Directory è stato esteso per Configuration Manager 2007 o System Center Configuration Manager 2012, non è necessario eseguire altre operazioni. Le estensioni dello schema sono invariate e risultano già applicate.  

L'estensione dello schema è un'operazione eseguita una sola volta per ogni foresta. Per estendere e quindi usare lo schema di Active Directory esteso, seguire questa procedura:  

## <a name="step-1-extend-the-schema"></a>Passaggio 1. Estendere lo schema  
Per estendere lo schema per Configuration Manager:  

-   Usare un account che sia membro del gruppo di sicurezza Schema Admins.  

-   È necessario avere eseguito l'accesso al controller di dominio master dello schema.  

-   Eseguire lo strumento **Extadsch.exe** oppure usare l'utilità della riga di comando LDIFDE con il file **ConfigMgr_ad_schema.ldf** . Lo strumento e il file si trovano entrambi nella cartella **SMSSETUP\BIN\X64** del supporto di installazione di Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opzione A: usare extadsch.exe  

1.  Eseguire **extadsch.exe** per aggiungere nuove classi e attributi allo schema di Active Directory.  

    > [!TIP]  
    >  Eseguire lo strumento da una riga di comando per visualizzare il feedback mentre è in esecuzione.  

2.  Verificare che l'estensione dello schema abbia avuto esito positivo riesaminando il file extadsch.log nella radice dell'unità di sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opzione B: usare il file LDIF  

1.  Modificare il file **ConfigMgr_ad_schema.ldf** per definire il dominio radice di Active Directory da estendere:  

    -   Sostituire tutte le istanze del testo **DC=x** nel file con il nome completo del dominio da estendere.  

    -   Se ad esempio il nome completo del dominio da estendere è widgets.microsoft.com, modificare tutte le istanze di DC=x nel file in **DC=widgets, DC=microsoft, DC=com**.  

2.  Usare l'utilità della riga di comando LDIFDE per importare il contenuto del file **ConfigMgr_ad_schema.ldf** in Active Directory Domain Services:  

    -   Ad esempio, la seguente riga di comando importa le estensioni dello schema in Active Directory Domain Services, attiva la registrazione dettagliata e crea un file di log durante il processo di importazione: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;percorso di archiviazione del file di log\>** .  

3.  Per verificare la riuscita dell'estensione dello schema, esaminare il file di log creato dalla riga di comando usata nel passaggio precedente.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Passaggio 2:  Creare il contenitore di System Management e concedere le autorizzazioni per i siti al contenitore  
 Dopo aver esteso lo schema, è necessario creare un contenitore denominato **System Management** in Active Directory Domain Services:  

-   Questo contenitore viene creato una sola volta in ogni dominio che include un sito primario o secondario che pubblicherà dati in Active Directory.  

-   Per ogni contenitore vengono concesse autorizzazioni all'account del computer di ogni server del sito primario e secondario che pubblica dati nel dominio. Ogni account deve disporre dei diritti di tipo **Controllo completo** sul contenitore con l'autorizzazione avanzata **Applica a** impostata su **Questo oggetto e tutti i discendenti**.  

#### <a name="to-add-the-container"></a>Per aggiungere il contenitore  

1.  Accedere con un account con l'autorizzazione **Crea tutti gli oggetti figlio** per il contenitore **Sistema** in Active Directory Domain Services.  

2.  Eseguire **ADSI Edit** (adsiedit.msc) e connettersi al dominio del server del sito.  

3.  Creare il contenitore:  

    -   Espandere **Dominio** &lt;nome di dominio completo del computer\>, espandere &lt;nome distinto\>, fare clic con il pulsante destro del mouse su **CN=System**, scegliere **Nuovo** e quindi scegliere **Oggetto**.  

    -   Nella finestra di dialogo **Crea oggetto** scegliere **Contenitore** e quindi scegliere **Avanti**.  

    -   Nella casella **Valore** immettere **System Management** e quindi scegliere **Avanti**.  

4.  Assegnare le autorizzazioni:  

    > [!NOTE]  
    >  Se si preferisce, è possibile usare altri strumenti come lo strumento di amministrazione Utenti e computer di Active Directory (dsa.msc) per aggiungere autorizzazioni al contenitore.  

    -   Fare clic con il pulsante destro del mouse su **CN=System Management** e scegliere **Proprietà**.  

    -   Scegliere la scheda **Sicurezza**, scegliere **Aggiungi** e quindi aggiungere l'account computer del server del sito con l'autorizzazione **Controllo completo**.  

    -   Scegliere **Avanzate**, scegliere l'account computer del server del sito e quindi scegliere **Modifica**.  

    -   Dall'elenco **Applica a** selezionare **Questo oggetto e tutti i discendenti**.  

5.  Scegliere **OK** per chiudere la console e salvare la configurazione.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Passaggio 3. Configurare i siti per la pubblicazione in Active Directory Domain Services  
 Dopo avere configurato il contenitore, avere ottenuto le autorizzazioni e avere installato un sito primario di Configuration Manager, è possibile configurare il sito per la pubblicazione di dati in Active Directory.  

 Per altre informazioni sulla pubblicazione, vedere [Pubblicare i dati del sito per Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
