---
title: Riattivazione dei client
titleSuffix: Configuration Manager
description: Pianificare la riattivazione dei client in Configuration Manager con la riattivazione LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693769"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Pianificare la riattivazione dei client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 Configuration Manager supporta i pacchetti di riattivazione tradizionale per riattivare i computer in modalità sospensione quando si vuole installare software richiesto, come aggiornamenti software e applicazioni.

> [!NOTE]
> Questo articolo descrive il funzionamento di una versione precedente della riattivazione LAN. Questa funzionalità è ancora presente in Configuration Manager versione 1810, che include anche una versione più recente della funzionalità di riattivazione LAN. Le due versioni possono essere abilitate contemporaneamente, come avviene effettivamente in molti casi. Per altre informazioni sul funzionamento della nuova versione della riattivazione LAN a partire dalla versione 1810 e su come abilitare una o entrambe le versioni, vedere [Come configurare la riattivazione LAN in System Center Configuration Manager](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Come riattivare i client in Configuration Manager

 Configuration Manager supporta i pacchetti di riattivazione tradizionale per riattivare i computer in modalità sospensione quando si vuole installare software richiesto, come aggiornamenti software e applicazioni.  

È possibile integrare il metodo tradizionale di riattivazione pacchetti usando le impostazioni client proxy di riattivazione. Il proxy di riattivazione usa un protocollo peer-to-peer e computer selezionati per controllare se nella subnet sono attivi altri computer e per riattivarli se necessario. Quando il sito è configurato per la riattivazione LAN e i client sono configurati per il proxy di riattivazione, il processo funziona nel modo seguente:  

1. I computer in cui è installato il client di Configuration Manager e che non sono in stato di sospensione nella subnet controllano se nella subnet ci sono altri computer riattivati. Questo controllo viene eseguito inviando tra di loro un comando ping TCP/IP ogni cinque secondi.  

2. In assenza di una risposta da altri computer, questi verranno considerati in stato di sospensione. I computer riattivati diventano *computer di gestione* per la subnet.  

    Poiché è possibile che un computer non risponda per un motivo che non è collegato alla sospensione (ad esempio è spento, è stato rimosso dalla rete oppure non è più applicata l'impostazione client di riattivazione proxy), ai computer viene inviato un pacchetto di riattivazione ogni giorno alle 14.00 ora locale. I computer che non rispondono non verranno più considerati in stato di sospensione e non verranno riattivati dal proxy di riattivazione.  

    Per il supporto dei proxy di riattivazione, devono essere attivi almeno tre computer per ogni subnet. Per soddisfare questo requisito, tre computer vengono scelti in modo non deterministico come *computer tutori* della subnet. Questo stato indica che rimangono attivi, nonostante siano presenti criteri di risparmio energia configurati in modalità di sospensione o di ibernazione dopo un periodo di inattività. I computer tutori rispettano i comandi di arresto o di riavvio, ad esempio, in seguito ad attività di manutenzione. Se ciò accade, i computer tutori rimanenti riattivano un altro computer nella subnet in modo che la subnet stessa continui ad avere tre computer tutori.  

3. I computer di gestione chiedono al commutatore di rete di reindirizzare il traffico di rete dei computer in sospensione verso sé stessi.  

    Il reindirizzamento avviene mediante la trasmissione dal parte del computer di gestione di un frame Ethernet che usa l'indirizzo MAC del computer in sospensione come indirizzo di origine. In questo modo il commutatore di rete si comporta come se il computer in sospensione sia stato spostato sulla stessa porta su cui si trova il computer di gestione. Il computer di gestione invia anche pacchetti ARP per i computer in sospensione per mantenere la voce nella cache ARP. Il computer di gestione risponde anche alle richieste ARP per conto del computer in sospensione e usa l'indirizzo MAC del computer in sospensione.  

   > [!WARNING]  
   >  Durante questo processo, il mapping da indirizzo IP a indirizzo MAC per il computer in sospensione rimane lo stesso. Il proxy di riattivazione informa il commutatore di rete che una scheda di rete differente sta usando la porta registrata da un altra scheda di rete. Tuttavia, questo comportamento è noto come flap MAC ed è insolito per operazioni di rete standard. Alcuni strumenti di monitoraggio della rete cercano questo comportamento e possono presumere che qualcosa non vada. Di conseguenza, questi strumenti di monitoraggio sono in grado di generare avvisi o chiudere le porte quando si usa il proxy di riattivazione.  
   >   
   >  Non usare il proxy di riattivazione se gli strumenti e i servizi di monitoraggio di rete e servizi non consentono i flap MAC.  

4. Quando un computer di gestione visualizza una nuova richiesta di connessione TCP per un computer in sospensione e la richiesta è su una porta su cui tale computer era in ascolto prima di andare in sospensione, il computer di gestione invia un pacchetto di riattivazione, quindi smette di reindirizzare il traffico per questo computer.  

5. Il computer in sospensione riceve il pacchetto di riattivazione e viene riattivato. Il computer di invio ritenta automaticamente la connessione e questa volta, il computer viene riattivato ed è in grado di rispondere.  

   Il proxy di riattivazione presenta i prerequisiti e le limitazioni seguenti:  

> [!IMPORTANT]  
>  Se un team separato è responsabile dell'infrastruttura di rete e dei servizi di rete, inviare una notifica e includere tale team nel periodo di valutazione e verifica. Ad esempio, in una rete che usa il controllo accesso alla rete mediante 802.1 X, il proxy di attivazione non funziona e può causare l'interruzione del servizio di rete. Il proxy di riattivazione potrebbe inoltre causare la generazione di avvisi da parte di alcuni strumenti di monitoraggio della rete quando viene rilevato il traffico per la riattivazione di altri computer.  

-   Tutti i sistemi operativi Windows indicati come client supportati in [Sistemi operativi supportati per client e dispositivi](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) sono supportati per la riattivazione LAN (WOL).  

-   Non sono supportati i sistemi operativi guest in esecuzione su una macchina virtuale.  

-   I client devono essere abilitati per il proxy di riattivazione tramite le impostazioni client. Nonostante il funzionamento del proxy di riattivazione non dipenda dall'inventario hardware, i client non riportano l'installazione del servizio del proxy di riattivazione a meno che non siano abilitati per l'inventario hardware e non ne abbiano inviato almeno uno.  

-   Le schede di rete (ed eventualmente il BIOS) devono essere abilitate e configurate per i pacchetti di riattivazione. Se la scheda di rete non è configurata per i pacchetti di riattivazione oppure questa impostazione è disabilitata, Configuration Manager la configurerà e abiliterà automaticamente per un computer quando riceve l'impostazione client per abilitare il proxy di riattivazione.  

-   Se un computer dispone di più di una scheda di rete, non è possibile configurare la scheda da usare per il proxy di riattivazione; la scelta è non deterministica. La scheda selezionata viene tuttavia registrata nel file SleepAgent_<DOMAIN\>@SYSTEM_0.log.  

-   La rete deve consentire le richieste echo ICMP (almeno all'interno della subnet). Non è possibile configurare l'intervallo di cinque secondi usato per inviare i comandi ping ICMP.  

-   La comunicazione non è crittografata né autenticate e IPsec non è supportato.  

-   Non sono supportate le seguenti configurazioni di rete:  

    -   802.1X con autenticazione della porta  

    -   Reti wireless  

    -   Commutatori di rete che associano indirizzi MAC a porte specifiche  

    -   Reti solo IPv6  

    -   Durata dei lease DHCP inferiore a 24 ore  

Se si vogliono riattivare i computer per un'installazione software pianificata, è necessario configurare ogni sito primario all'uso dei pacchetti di riattivazione.  

 Per usare i pacchetti di riattivazione, è necessario distribuire le impostazioni client del proxy di riattivazione di Risparmio energia oltre alla configurazione del sito primario.  

Decidere se usare pacchetti di broadcast diretti a subnet oppure pacchetti unicast, nonché il numero di porta UDP da usare. Per impostazione predefinita, i pacchetti di riattivazione tradizionali vengono trasmessi usando la porta UDP 9 ma, per una maggior sicurezza, è possibile selezionare una porta alternativa per il sito se supportata dai router e firewall coinvolti.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Scegliere tra il broadcast unicast e con riferimento a subnet per la riattivazione LAN  
 Se si è scelto di riattivare i computer inviando pacchetti di riattivazione tradizionali, occorre decidere se trasmettere pacchetti unicast o pacchetti di broadcast con riferimento a subnet. Se si usa il proxy di riattivazione, è necessario usare pacchetti unicast. In caso contrario, usare la tabella seguente per determinare quale metodo di trasmissione scegliere.  

|Metodo di trasmissione|Vantaggio|Svantaggio|  
|-------------------------|---------------|------------------|  
|Unicast|Soluzione più sicura dei broadcast con riferimento a subnet perché il pacchetto viene inviato direttamente a un computer invece che a tutti i computer su una subnet.<br /><br /> Potrebbe non richiedere la riconfigurazione di router (potrebbe essere necessario configurare la cache ARP).<br /><br /> Consuma meno larghezza di banda di rete rispetto alle trasmissioni di broadcast con riferimento a subnet.<br /><br /> Supportato con IPv4 e IPv6.|I pacchetti di riattivazione non trovano i computer di destinazione che hanno modificato i relativi indirizzi di subnet dopo l'ultima pianificazione dell'inventario hardware.<br /><br /> I commutatori potrebbero dover essere configurati per inoltrare pacchetti UDP.<br /><br /> Alcune schede di rete potrebbero non rispondere ai pacchetti di riattivazione in tutti gli stati di sospensione quando usano unicast come metodo di trasmissione.|  
|Broadcast con riferimento a subnet|Maggiore percentuale di successo rispetto a unicast se si dispone di computer che cambiano spesso l'indirizzo IP nella stessa subnet.<br /><br /> Non è necessaria nessuna riconfigurazione del commutatore.<br /><br /> Elevata percentuale di compatibilità con schede di computer per tutti gli stati di sospensione, perché i broadcast con riferimento a subnet erano il metodo di trasmissione originale per l'invio di pacchetti di riattivazione.|Soluzione meno sicuro rispetto all'utilizzo di unicast, poiché un utente malintenzionato potrebbe inviare flussi continui di richieste echo di Internet Control Message Protocol (ICMP) da un indirizzo di origine falsificato all'indirizzo di broadcast con riferimento a subnet. Ciò provocherebbe la risposta di tutti gli host a tale indirizzo di origine. Se i router sono configurati per consentire trasmissioni con riferimento a subnet, per motivi di sicurezza è consigliabile la configurazione aggiuntiva:<br /><br /> Configurare i router per consentire solo broadcast diretti IP dal server del sito di Configuration Manager, usando un numero di porta UDP specificato.<br />Configurare Configuration Manager per l'uso del numero di porta non predefinito specificato.<br /><br /> Potrebbe essere richiesta la riconfigurazione di tutti i router coinvolti per abilitare broadcast con riferimento a subnet.<br /><br /> Usa una larghezza di banda di rete maggiore rispetto a trasmissioni unicast.<br /><br /> Supportato solo con IPv4 e non con IPv6.|  

> [!WARNING]  
>  I broadcast con riferimento a subnet comportano rischi per la sicurezza: un utente malintenzionato potrebbe inviare flussi continui di richieste echo di Internet Control Message Protocol (ICMP) da un indirizzo di origine falsificato all'indirizzo di broadcast con riferimento a subnet, determinando la risposta di tutti gli host a tale indirizzo di origine. Questo tipo di attacco Denial of Service è comunemente denominato attacco smurf e viene in genere limitato non abilitando le broadcast con riferimento a subnet.
