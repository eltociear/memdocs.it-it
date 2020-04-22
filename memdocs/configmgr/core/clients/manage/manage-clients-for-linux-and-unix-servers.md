---
title: Gestire i client Linux e UNIX
titleSuffix: Configuration Manager
description: Gestire i client in server Linux e UNIX in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690049"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Come gestire i client per i server Linux e UNIX in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

Quando si gestiscono server Linux e UNIX con Configuration Manager, è possibile configurare raccolte, finestre di manutenzione e impostazioni client per semplificare la gestione dei server. Inoltre, anche se il client di Configuration Manager per Linux e UNIX non ha un'interfaccia utente, è possibile forzare manualmente il polling dei criteri client.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Raccolte di server Linux e UNIX  
 Usare le raccolte per gestire i gruppi di server Linux e UNIX in modo analogo all'uso delle raccolte per gestire altri tipi di client. Le raccolte possono essere raccolte di appartenenza diretta o raccolte basate su query. Le raccolte basate su query identificano i sistemi operativi client, le configurazioni hardware o altri dettagli relativi ai client archiviati nel database del sito. Ad esempio, è possibile usare le raccolte che includono server Linux e UNIX per gestire le impostazioni seguenti:  

- Impostazioni client  

- Distribuzioni software  

- Imposizione delle finestre di manutenzione  

  Prima di poter identificare un client Linux o UNIX mediante il relativo sistema operativo o la relativa distribuzione, è necessario raccogliere l'[inventario hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) dal client.  

  Le impostazioni client predefinite per l'inventario hardware includono le informazioni sul sistema operativo di un computer client. È possibile usare la proprietà **Didascalia** della classe **Sistema operativo** per identificare il sistema operativo di un server Linux o UNIX.  

  È possibile visualizzare i dettagli relativi ai computer che eseguono il client di Configuration Manager per Linux e UNIX nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità** della console di Configuration Manager. Nell'area di lavoro **Asset e conformità** della console di Configuration Manager è possibile visualizzare il nome del sistema operativo di ogni computer nella colonna **Sistema operativo**.  

  Per impostazione predefinita i server Linux e UNIX sono membri della raccolta **Tutti i sistemi** . È consigliabile creare raccolte personalizzate che includono solo i server Linux e UNIX o un loro subset. Le raccolte personalizzate consentono di gestire operazioni quali la distribuzione del software o l'assegnazione di impostazioni client ai gruppi di computer applicabili, in modo da poter misurare con precisione l'esito di una distribuzione.   

  Quando si crea una raccolta personalizzata per server Linux e UNIX, includere le query relative alle regole di appartenenza contenenti l'attributo Didascalia per l'attributo Sistema operativo. Per informazioni sulla creazione delle raccolte, vedere [Come creare le raccolte](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Finestre di manutenzione per server Linux e UNIX  
 Il client di Configuration Manager per i server Linux e UNIX supporta l'uso di [finestre di manutenzione](../../../core/clients/manage/collections/use-maintenance-windows.md). Questo supporto è lo stesso dei client basati su Windows.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Impostazioni client per server Linux e UNIX  
 È possibile [configurare le impostazioni client](../../../core/clients/deploy/configure-client-settings.md) che si applicano a server Linux e UNIX in modo analogo alla configurazione delle impostazioni per gli altri client.  

 Per impostazione predefinita l'opzione **Impostazioni agente client predefinite** si applica a server Linux e UNIX. È anche possibile creare impostazioni client personalizzate e distribuirle alle raccolte di client specifici.  

 Non sono presenti impostazioni client aggiuntive che si applicano solo ai client Linux e UNIX. Ci sono tuttavia impostazioni client predefinite che non si applicano ai client Linux e UNIX. Il client per Linux e UNIX applica le impostazioni solo per le funzionalità supportate.  

 Ad esempio, un'impostazione del dispositivo client personalizzata che abilita e configura le impostazioni di controllo remoto viene ignorata dai server Linux e UNIX, perché il client per Linux e UNIX non supporta il controllo remoto.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Criteri del computer per server Linux e UNIX  
 Il client per i server Linux e UNIX esegue periodicamente il polling dei criteri del computer nel relativo sito per recuperare informazioni sulle configurazioni richieste e per controllare le distribuzioni.  

 È anche possibile imporre il client a un server Linux o UNIX per eseguire il polling immediato dei criteri del computer. A tale scopo, usare le credenziali **root** nel server per eseguire il comando seguente: **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 I dettagli relativi al polling dei criteri del computer vengono inseriti nel file di log del client condiviso **scxcm.log**.  

> [!NOTE]  
>  Il client di Configuration Manager per Linux e UNIX non richiede né elabora mai i criteri utente.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> Come gestire i certificati sul client per Linux e UNIX  
 Dopo aver installato il client per Linux e UNIX, è possibile usare lo strumento **certutil** per aggiornare il client con un nuovo certificato PKI e per importare un nuovo elenco di revoche di certificati (CRL). Quando si installa il client per Linux e UNIX, questo strumento viene inserito in `/opt/microsoft/configmgr/bin/certutil`. 

 Per gestire i certificati, in ogni client eseguire lo strumento certutil con una delle opzioni seguenti:  

|Opzione|Altre informazioni|  
|------------|----------------------|  
|`importPFX`|Usare questa opzione per specificare un certificato per sostituire il certificato attualmente usato da un client.<br /><br /> Quando si usa `-importPFX`, è necessario usare anche il parametro della riga di comando `-password` per specificare la password associata al file PKCS#12.<br /><br /> Usare `-rootcerts` per specificare eventuali requisiti aggiuntivi relativi al certificato radice.<br /><br /> Esempio: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Usare questa opzione per aggiornare il certificato di firma del server del sito che si trova nel server di gestione.<br /><br /> Esempio: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Usare questa opzione per aggiornare l'elenco di revoche di certificati sul client con uno o più percorsi di file CRL.<br /><br /> Esempio: `certutil -importcrl <comma separated CRL file paths>`|  
