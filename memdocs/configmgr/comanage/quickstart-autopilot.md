---
title: Windows Autopilot con la co-gestione
titleSuffix: Configuration Manager
description: Usare Windows Autopilot con la co-gestione in Configuration Manager per semplificare la configurazione di nuovi dispositivi Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91b938b5ab64616a35773406cd18b54de80b40e7
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590410"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot con la co-gestione

Avere a disposizione un nuovo dispositivo Windows 10 è divertente e utile, ma serve tempo per configurare tutte le impostazioni e le app in modo da poter essere produttivi. La co-gestione consente di risolvere questo problema di provisioning dei dispositivi con Windows Autopilot.

Autopilot offre un'esperienza semplificata sia per gli amministratori che per gli utenti nelle situazioni seguenti:
- Configurare e preconfigurare nuovi dispositivi Windows 10  
- Reimpostare, riciclare e ripristinare dispositivi esistenti  

Autopilot consente di ridurre il tempo, le risorse e la complessità associati a distribuzione, gestione e ritiro dei dispositivi. Allo stesso tempo, l'esperienza per gli utenti è priva di complicazioni e facile sin dal primo avvio.

Windows Autopilot supporta diversi scenari, ognuno dei quali può essere ottimizzato con la co-gestione:

- Gli utenti possono indirizzare le distribuzioni di nuovi dispositivi in Active Directory con l'aggiunta ad Azure AD ibrido o in Azure Active Directory (Azure AD)  

- È possibile configurare la distribuzione automatica dei nuovi dispositivi in Azure AD per i dispositivi condivisi e in modalità tutto schermo  

- Con Windows Autopilot per i dispositivi esistenti, usare Configuration Manager per eseguire la migrazione di un dispositivo esistente da Windows 7 e Active Directory a Windows 10 e Azure AD  

Nel video seguente il Senior Program Manager Danny Guillory e il Principal Program Manager Andrew McMurray trattano e illustrano Windows Autopilot con la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Vantaggi

Usando insieme la co-gestione e Autopilot ci si assicura che i nuovi dispositivi che accedono alla rete abbiano lo stesso stato di gestione. In questa configurazione, i dispositivi vengono registrati in Intune e hanno un client di Configuration Manager.  Ciò consente di usare il nuovo modello di provisioning di Windows 10 e contribuisce a eliminare la necessità di creare, gestire e aggiornare immagini personalizzate del sistema operativo. 

In tutti questi scenari, è possibile [abilitare la co-gestione](how-to-prepare-Win10.md) automaticamente da Intune. Questa automazione agevola il processo di provisioning e la gestione continuativa del dispositivo.

Con Autopilot non è necessario preoccuparsi di immagini e driver. È possibile concentrarsi sul provisioning dei dispositivi con questo processo automatizzato usando Intune e Configuration Manager tramite la co-gestione.


Ecco alcuni dei vantaggi immediati dell'uso combinato di co-gestione e Autopilot:

#### <a name="reduce-time-costs-and-complexity"></a>Ridurre tempi, costi e complessità
Windows Autopilot usa la versione ottimizzata per OEM di Windows 10 che è già preinstallata nel dispositivo. Questa configurazione consente di evitare alle organizzazioni l'impegno di dover gestire le immagini personalizzate e i driver per ogni modello di dispositivo in uso. Invece di ricreare l'immagine del dispositivo, l'installazione esistente di Windows 10 viene trasformata in base alle esigenze aziendali ed è pronta per l'uso. Vengono applicati criteri e impostazioni, installate le app e modificata l'edizione di Windows 10. Ad esempio, l'aggiornamento da Windows 10 Pro a Windows 10 Enterprise in modo da poter supportare funzionalità avanzate.

#### <a name="improve-the-user-experience"></a>Migliorare l'esperienza utente
Offrire un esperienza ottimale agli utenti si traduce in disservizi minimi e consente loro di concentrarsi sul proprio lavoro. Windows Autopilot offre un approccio semplice per consentire agli utenti di completare rapidamente la configurazione con pochi clic e le credenziali di Azure AD. Molte organizzazioni con un numero elevato di dipendenti remoti usano Windows Autopilot per fornire i nuovi dispositivi direttamente dal produttore.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Usare Autopilot e Configuration Manager per eseguire la migrazione di dispositivi Windows 7 esistenti a Windows 10
Con Windows Autopilot per i dispositivi esistenti, è possibile creare un file di configurazione e distribuirlo con una sequenza di attività di Configuration Manager. Questo processo consente di eseguire facilmente la migrazione di dispositivi esistenti da Windows 7 a Windows 10. È sufficiente usare un'immagine di Windows 10 con firma in Configuration Manager e quindi applicarla nel dispositivo Windows 7 esistente con la configurazione di Autopilot. All'avvio del dispositivo, gli utenti usano il processo di onboarding guidato dall'utente di Autopilot.

Questi sono i passaggi per Autopilot per i dispositivi esistenti:

![Panoramica del processo con Windows Autopilot per i dispositivi esistenti](media/autopilot-for-existing-devices.png)

1. Distribuire Criteri di gruppo per il reindirizzamento delle cartelle note in OneDrive
2. Generare il file di configurazione di Autopilot
3. Distribuire la sequenza di attività per eseguire l'aggiornamento a Windows 10
4. La configurazione Autopilot viene applicata al computer Windows 10 al primo avvio

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernizzazione del provisioning dei dispositivi per tutti i tipi di utenti
Con Autopilot è ora possibile usare la modalità di distribuzione automatica del sistema operativo per i dispositivi senza operatore o condivisi. Questa configurazione soddisfa le esigenze di tutti i diversi tipi di ruoli di lavoro. Inoltre, la funzione Reimpostazione di Windows Autopilot garantisce la facilità di riesecuzione del provisioning di un dispositivo per un nuovo utente. Questo processo semplifica un'attività tradizionalmente difficile, in presenza di collaboratori stagionali o interinali. 



## <a name="case-study"></a>Case study

L'impresa di logistica e trasporto merci su rotaia tedesca DB Schenker usa Autopilot per aumentare la produttività dei dipendenti e liberare i team IT dalle attività quotidiane di supporto. DB Schenker ha sostituito l'uso tradizionale delle immagini con il provisioning tramite il cloud. Ora usano l'aggiunta ad Azure AD e Intune per configurare e rendere operativi rapidamente i nuovi dispositivi. 

Da quando DB Schenker usa Windows Autopilot, i collaboratori remoti non devono più perdere tempo per raggiungere una sede in grado di offrire i servizi IT. L'hardware viene consegnato direttamente ai collaboratori dal produttore agli uffici sul campo locali. Il collaboratore connette il nuovo dispositivo a Internet e accede con le proprie credenziali di Azure AD. Il dispositivo si connette quindi alle applicazioni e ai servizi assegnati dal reparto IT di DB Schenker al singolo profilo dell'utente.

Per altre informazioni, vedere [Global logistics firm centralizes IT, unites employees with modern digital workplace](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10) (Un'impresa di logistica globale centralizza i servizi IT e offre ai dipendenti un'area di lavoro unificata digitale moderna).



## <a name="value-proposition"></a>Proposta di valore

Generare soddisfazione all'interno dell'organizzazione tramite la creazione di un'esperienza utente migliore per gli utenti. Usare Windows Autopilot per ridurre i costi. Guadagnare tempo per concentrarsi su altri progetti con valore e impatto maggiori per l'organizzazione.



## <a name="configure"></a>Configura

Per altre informazioni, vedere gli articoli seguenti:

[Usare Intune per creare i profili di Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

Sequenza di attività [Windows Autopilot per dispositivi esistenti](../osd/deploy-use/windows-autopilot-for-existing-devices.md)

