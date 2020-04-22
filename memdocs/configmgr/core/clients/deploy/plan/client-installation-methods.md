---
title: Metodo di installazione client
titleSuffix: Configuration Manager
description: Informazioni sui metodi di installazione del client di Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693839"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Metodi di installazione client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare diversi metodi per installare il software client di Configuration Manager. È possibile usare un metodo o una combinazione di metodi. In questo articolo viene descritto ogni metodo, in modo da acquisire quello che risulta più adatto per l'organizzazione.  

## <a name="client-push-installation"></a>Installazione push client  

**Piattaforma client supportata**: Windows  

#### <a name="advantages"></a>Vantaggi  

-   Può essere utilizzato per installare il client in un singolo computer, una raccolta di computer o nei risultati di una query.  

-   Può essere utilizzato per installare automaticamente il client in tutti i computer individuati.  

-   Utilizza automaticamente le proprietà di installazione del client definite nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .  

#### <a name="disadvantages"></a>Svantaggi  

-   Può causare traffico di rete elevato quando si esegue il push in raccolte di grandi dimensioni.  

-   Può essere usato solo nei computer individuati da Configuration Manager.  

-   Non può essere usato per installare client in un gruppo di lavoro.  

-   È necessario specificare un account di installazione push client che dispone di diritti amministrativi sul computer client previsto.  

-   Windows Firewall deve essere configurato con eccezioni nei computer client.   

-   Non è possibile annullare l'installazione push client. Configuration Manager tenta di installare il client in tutte le risorse individuate. In caso di errore, ritenta l'esecuzione per un periodo fino a sette giorni.  

Per altre informazioni , vedere [Come installare i client con l'installazione push client](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Installazione basata sul punto di aggiornamento software  

**Piattaforma client supportata**: Windows  

#### <a name="advantages"></a>Vantaggi  

-   Può utilizzare l'infrastruttura di aggiornamenti software esistente per gestire il software client.  

-   Se Windows Server Update Services (WSUS) e le impostazioni di Criteri di gruppo sono configurati correttamente in Active Directory Domain Services, WSUS può installare automaticamente il software client nei nuovi computer.  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   I computer possono leggere le proprietà di installazione client che sono state pubblicate in Servizi di dominio Active Directory.  

-   Se il client viene rimosso, questo metodo lo reinstalla.  

-   Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

#### <a name="disadvantages"></a>Svantaggi  

-   Richiede un'infrastruttura per gli aggiornamenti software che sia funzionante come prerequisito.  

-   Deve usare lo stesso server per l'installazione del client e gli aggiornamenti software. Il server deve risiedere in un sito primario.  

-   Per installare nuovi client, è necessario configurare un oggetto Criteri di gruppo in Active Directory Domain Services con la porta e il punto di aggiornamento software attivo del software.  

-   Se lo schema di Active Directory non viene esteso per Configuration Manager, è necessario usare le impostazioni di Criteri di gruppo per eseguire il provisioning dei computer con le proprietà di installazione client.  

Per altre informazioni, vedere [Come installare i client con l'installazione basata sull'aggiornamento software](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Installazione con Criteri di gruppo  

**Piattaforma client supportata**: Windows  

#### <a name="advantages"></a>Vantaggi  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Può essere utilizzato per le nuove installazioni di client o per gli aggiornamenti.  

-   I computer possono leggere le proprietà di installazione client che sono state pubblicate in Servizi di dominio Active Directory.  

-   Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

#### <a name="disadvantages"></a>Svantaggi  

-   L'installazione di molti client può causare traffico di rete elevato.  

-   Se lo schema di Active Directory non viene esteso per Configuration Manager, è necessario usare le impostazioni di Criteri di gruppo per aggiungere le proprietà di installazione del client ai computer presenti nel sito.  

Per altre informazioni, vedere [Come installare i client con Criteri di gruppo](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Installazione tramite script di accesso  

**Piattaforma client supportata**: Windows  

#### <a name="advantages"></a>Vantaggi  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

#### <a name="disadvantages"></a>Svantaggi  

-   L'installazione di molti client in un periodo di tempo breve può causare un traffico di rete elevato.  

-   Se gli utenti non si collegano alla rete di frequente, l'installazione in tutti i computer client può richiedere molto tempo.  

Per altre informazioni , vedere [Come installare i client con gli script di accesso](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Installazione manuale  

**Piattaforma client supportata**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vantaggi  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Può essere utile a scopo di test.  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

#### <a name="disadvantages"></a>Svantaggi  

-   Non prevede automazione, pertanto risulta dispendioso in termini di tempo.  

Per altre informazioni su come installare manualmente il client in ogni piattaforma, vedere gli articoli seguenti:  

-   [Come distribuire i client nei computer Windows](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Come distribuire i client nei server UNIX e Linux](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Come distribuire i client in computer Mac](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Installazione MDM di Microsoft Intune

**Piattaforme client supportate**: Windows 10

#### <a name="advantages"></a>Vantaggi  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

-   Può usare l'autenticazione moderna con Azure Active Directory.  

-   Può installare e assegnare i computer in Internet.  

-   Può realizzare l'automatizzazione con Windows AutoPilot e Microsoft Intune per la co-gestione.  

#### <a name="disadvantages"></a>Svantaggi  

-   Richiede tecnologie aggiuntive al di fuori di Configuration Manager.  

-   Richiede che il dispositivo abbia accesso a Internet, anche se non è basato su Internet.  

Per altre informazioni, vedere gli articoli seguenti:  

-   [Come installare i client nei dispositivi Windows gestiti da MDM di Intune](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](../deploy-clients-cmg-azure.md)  

