---
title: Proprietà di installazione client in Active Directory
titleSuffix: Configuration Manager
description: Pubblicare le proprietà di installazione client di Configuration Manager in Active Directory Domain Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692069"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services

*Si applica a: Configuration Manager (Current Branch)*

Quando si estende lo schema di Active Directory per Configuration Manager e il sito viene pubblicato in Active Directory Domain Services, molte proprietà di installazione client vengono pubblicate in Active Directory Domain Services. Se un computer è in grado di rilevare le proprietà di installazione del client, può usarle durante la distribuzione del client di Configuration Manager.  

 I vantaggi dell'uso di Active Directory Domain Services per pubblicare le proprietà dell'installazione del client includono:  

-   L'installazione client basata sul punto di aggiornamento software e le installazioni client di Criteri di gruppo non richiedono la configurazione dei parametri di impostazione in ogni computer.  

-   Poiché queste informazioni vengono generate automaticamente, viene eliminato il rischio di errori umani associato all'immissione manuale delle proprietà di installazione.  

> [!NOTE]  
>  Per altre informazioni su come estendere lo schema di Active Directory per Configuration Manager e come pubblicare un sito, vedere [Estensioni dello schema per Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Proprietà di installazione client pubblicate in Active Directory Domain Services  
Di seguito è riportato un elenco delle proprietà di installazione client. Per altre informazioni su ogni elemento elencato di seguito, vedere [Informazioni sui parametri e le proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

- Codice del sito di Configuration Manager.  

- Il certificato di firma del server del sito.  

- La chiave radice attendibile.  

- Le porte di comunicazione client per HTTP e HTTPS.  

- Il punto di stato di fallback. Se nel sito sono presenti più punti di stato di fallback, verrà pubblicato in Active Directory Domain Services soltanto il primo elemento installato.  

- Un'impostazione per indicare che il client deve comunicare solo tramite HTTPS.  

- Impostazioni relative ai certificati PKI:  

  -   Se si desidera utilizzare un certificato PKI del client.  

  -   Criteri per la selezione del certificato. Possono essere necessari perché il client dispone di più certificati PKI validi utilizzabili per Configuration Manager.  

  -   Un'impostazione per stabilire quale certificato utilizzare se il client dispone di più certificati validi dopo il processo di selezione del certificato.  

  -   L'elenco di autorità emittenti del certificato che contiene un elenco di certificati CA radice attendibili.  

- Le proprietà di installazione client.msi specificate nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .

L'installazione client (CCMSetup) usa le proprietà pubblicate in Active Directory Domain Services solo se non vengono specificate altre proprietà mediante uno dei metodi seguenti:  

-   Metodo di installazione manuale (descritto più avanti in questo articolo)

-   Metodo di installazione Criteri di gruppo (descritto più avanti in questo articolo)

> [!NOTE]  
>  Proprietà di installazione client usate per installare il client. Queste proprietà possono essere sovrascritte con le nuove impostazioni del sito assegnato, dopo che il client è stato installato e assegnato correttamente a un sito di Configuration Manager.  

 Usare le informazioni dettagliate nelle sezioni seguenti per determinare quali metodi di installazione client di Configuration Manager usano Active Directory Domain Services per ottenere le proprietà di installazione client.  

## <a name="client-push-installation"></a>Installazione push client  
 L'installazione push del client non usa Active Directory Domain Services per ottenere le proprietà di installazione.  

 È possibile invece specificare le proprietà di installazione client nella scheda **Proprietà di installazione** della finestra di dialogo **Proprietà installazione push client**. Queste opzioni e impostazioni del sito relative al client vengono archiviate in un file che il client legge durante l'installazione client.  

> [!NOTE]  
>  Non è necessario specificare alcuna proprietà CCMSetup per l'installazione push client né il punto di stato di fallback né la chiave radice attendibile nella scheda **Proprietà di installazione**. Queste impostazioni vengono fornite ai client automaticamente al momento dell'installazione tramite installazione push del client.
Oltre alle proprietà di Client.msi, CCMSetup supporta i parametri seguenti: /forcereboot, /skipprereq, /logon, /BITSPriority, /downloadtimeout, /forceinstall

 Se il sito viene pubblicato in Active Directory Domain Services, qualsiasi proprietà specificata nella scheda **Proprietà di installazione** viene pubblicata in Active Directory Domain Services. Queste impostazioni vengono lette dalle installazioni del client quando CCMSetup viene eseguito senza proprietà di installazione.  

## <a name="software-update-point-based-installation"></a>Installazione basata sul punto di aggiornamento software  
 Il metodo di installazione basata sul punto di aggiornamento software non supporta l'aggiunta di proprietà di installazione nella riga di comando di CCMSetup.  

 Se non è stato eseguito il provisioning delle proprietà della riga di comando nel computer client utilizzando i Criterio di gruppo, CCMSetup cerca le proprietà di installazione in Active Directory Domain Services.  

## <a name="group-policy-installation"></a>Installazione tramite Criteri di gruppo  
 Il metodo di installazione con Criteri di gruppo non supporta l'aggiunta di proprietà di installazione nella riga di comando di CCMSetup.  

 Se non è stato eseguito il provisioning delle proprietà della riga di comando nel computer client, CCMSetup cerca le proprietà di installazione in Active Directory Domain Services.  

## <a name="manual-installation"></a>Installazione manuale  
 CCMSetup cerca le proprietà di installazione in Active Directory Domain Services nelle circostanze seguenti:  

-   Nessuna proprietà della riga di comando viene specificata dopo il comando CCMSetup.exe.  

-   Non è stato eseguito il provisioning del computer con le proprietà di installazione utilizzando i Criteri di gruppo.  

## <a name="logon-script-installation"></a>Installazione tramite script di accesso  
 CCMSetup cerca le proprietà di installazione in Active Directory Domain Services nelle circostanze seguenti:  

-   Nessuna proprietà della riga di comando viene specificata dopo il comando CCMSetup.exe.  

-   Non è stato eseguito il provisioning del computer con le proprietà di installazione utilizzando i Criteri di gruppo.  

## <a name="software-distribution-installation"></a>Installazione della distribuzione software  
 CCMSetup cerca le proprietà di installazione in Active Directory Domain Services nelle circostanze seguenti:  

-   Nessuna proprietà della riga di comando viene specificata dopo il comando CCMSetup.exe.  

-   Non è stato eseguito il provisioning del computer con le proprietà di installazione utilizzando i Criteri di gruppo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Installazioni per i client che non possono accedere ad Active Directory Domain Services  
Questi computer client non sono in grado di leggere o accedere alle proprietà di installazione da Active Directory Domain Services.

 Tra questi client sono inclusi:  

-   Computer del gruppo di lavoro.  

-   Client assegnati a un sito di Configuration Manager non pubblicato in Active Directory Domain Services.  

-   Client installati quando si trovano in Internet.  
