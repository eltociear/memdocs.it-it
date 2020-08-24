---
title: Notifiche della console di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sulle applicazioni dalla console di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129546"
---
# <a name="configuration-manager-console-notifications"></a>Notifiche della console di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--3556016, fka 1318035-->
A partire da Configuration Manager versione 1902, la console di Configuration Manager visualizza una notifica per gli specifici eventi che si verificano. È possibile configurare alcune delle notifiche degli eventi per i siti di Configuration Manager.

- Notifiche degli eventi non configurabili:
   - Quando è disponibile un aggiornamento per Configuration Manager
   - Quando nell'ambiente si verificano eventi di manutenzione e relativi al ciclo di vita
- Notifiche degli eventi configurabili:
   - [Modifiche all'integrità del sito non critiche](#bkmk_noncrit)
   - [Messaggi da Microsoft](#bkmk_msft) (a partire dalla versione 2006)

Queste notifiche sono visualizzate in una barra nella parte superiore della finestra della console sotto la barra multifunzione. Sostituiscono l'esperienza precedente che avvisava della disponibilità di aggiornamenti di Configuration Manager. Queste notifiche nella console visualizzano comunque informazioni critiche, ma non interferiscono con l'interazione tra utente e console. Le notifiche critiche non possono essere ignorate. Tutte le notifiche della console sono visualizzate in una nuova area di notifica della barra del titolo.

![Barra delle notifiche e flag nella console](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a>Configurare un sito per la visualizzazione delle notifiche non critiche

È possibile configurare ogni sito per la visualizzazione delle notifiche non critiche nelle proprietà del sito.

1. Nell'area di lavoro **Amministrazione** espandere **Configurazione sito** e quindi selezionare il nodo **Siti**.
1. Selezionare il sito che si vuole configurare per le notifiche non critiche.
1. Nella barra multifunzione selezionare **Proprietà**.
1. Nella scheda **Avvisi** selezionare l'opzione **Abilita le notifiche della console per modifiche non critiche all'integrità del sito**.
   - Se si abilita questa impostazione, tutti gli utenti vedranno le notifiche di livello critico, gli avvisi e le informazioni. Questa opzione è attivata per impostazione predefinita.  
   - Se si disabilita questa impostazione, gli utenti della console vedranno solo le notifiche di livello critico.  

La maggior parte delle notifiche della console sono relative alla sessione. La console valuta le query quando vengono avviate dall'utente. Per visualizzare le modifiche nelle notifiche, riavviare la console. Se un utente chiude una notifica critica, questa verrà inviata nuovamente al riavvio della console, purché sia ancora applicabile.

Le notifiche seguenti vengono rivalutate ogni cinque minuti:

- Il sito si trova in modalità di manutenzione  
- Il sito si trova in modalità di ripristino  
- Il sito si trova in modalità di aggiornamento  

Le notifiche seguono le autorizzazioni dell'amministrazione basata sui ruoli. Ad esempio, se un utente non dispone delle autorizzazioni per visualizzare gli aggiornamenti di Configuration Manager, l'utente non vedrà tali notifiche.

Alcune notifiche sono associate a un'azione. Ad esempio, se la versione della console non corrisponde alla versione del sito, selezionare **Install the new console version** (Installare la nuova versione della console). Questa azione avvia il programma di installazione della console.

A partire dalla versione 2006, se si configurano i servizi di Azure per il cloud-attach del sito, verranno visualizzate le notifiche contenenti un'azione per [rinnovare la chiave privata](../deploy/configure/azure-services-wizard.md#bkmk_renew).<!--6386392--> Il sito valuta lo stato di questo avviso una volta ogni ora:

- Una o più chiavi private dell'app Azure AD sono prossime alla scadenza
- Una o più chiavi private dell'app Azure AD sono scadute

Le notifiche seguenti sono applicabili in prevalenza al ramo Technical Preview:  

- La versione di valutazione ha una scadenza entro 30 giorni (Avviso): la data di scadenza della versione di valutazione è entro 30 giorni dalla data corrente  
- La versione di valutazione è scaduta (Errore critico): la data corrente è oltre la data di scadenza della versione di valutazione  
- Mancata corrispondenza con la versione della console (Errore critico): la versione della console non corrisponde alla versione del sito  
- Aggiornamento del sito disponibile (Avviso): è disponibile un nuovo pacchetto di aggiornamento  

Per altre informazioni e istruzioni per la risoluzione dei problemi, vedere il file **SmsAdminUI.log** nel computer della console. Per impostazione predefinita, questo file si trova nel percorso seguente: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a>Configurare un sito per ricevere messaggi da Microsoft
 <!--3953121-->

A partire dalla versione 2006, è possibile scegliere di ricevere notifiche da Microsoft nella console di Configuration Manager. Queste notifiche consentono di ricevere informazioni sulle funzionalità nuove o aggiornate, sulle modifiche apportate a Configuration Manager e ai servizi collegati e sui problemi che richiedono azioni di correzione.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Configurare le impostazioni per la notifica dei messaggi Microsoft

1. Passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.
1. Fare clic con il pulsante destro del mouse su un sito e selezionare **Proprietà**.
1. Nella scheda **Avvisi** abilitare le notifiche selezionando **Receive messages from Microsoft** (Ricevi messaggi da Microsoft). Se non si vuole ricevere una delle notifiche seguenti, è possibile deselezionarla:  
   - **Impedisci/Correggi**: problemi noti che interessano l'organizzazione e potrebbero richiedere l'intervento dell'utente.
   - **Pianifica per la modifica**: modifiche a Configuration Manager che potrebbero richiedere l'intervento dell'utente.
   - **Rimani aggiornato**: segnalazione di funzionalità nuove o aggiornate disponibili.

     [ ![Notifiche dalle opzioni Microsoft nelle proprietà del sito](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Passaggi successivi

- [Usare la console](admin-console.md)
- [Suggerimenti sulla console](admin-console-tips.md)
- [Funzionalità di accesso facilitato](../../understand/accessibility-features.md)
