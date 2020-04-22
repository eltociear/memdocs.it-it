---
title: Privacy e sicurezza per il controllo remoto
titleSuffix: Configuration Manager
description: Informazioni sulla sicurezza e la privacy per il controllo remoto in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696399"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Sicurezza e privacy per il controllo remoto in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo argomento contiene informazioni relative alla sicurezza e alla privacy per il controllo remoto in Configuration Manager.  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Procedure di sicurezza consigliate per il controllo remoto  
 Utilizzare le seguenti procedure ottimali di protezione per gestire i computer client utilizzando il controllo remoto.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Al momento di connettersi a un computer remoto, non continuare la procedura se viene usata l'autenticazione NTLM anziché l'autenticazione Kerberos.|Se Configuration Manager rileva che la sessione di controllo remoto viene autenticata con NTLM anziché Kerberos, un prompt segnala che non è possibile verificare l'identità del computer remoto. Non continuare la sessione di controllo remoto. NTLM è un protocollo di autenticazione più debole rispetto a Kerberos ed è vulnerabile agli attacchi di riproduzione e rappresentazione.|  
|Non abilitare la condivisione degli Appunti nel visualizzatore controllo remoto.|Gli Appunti supportano oggetti quali file eseguibili e testo. L'utente potrebbe quindi usarli nel computer host durante la sessione di controllo remoto per eseguire un programma nel computer di origine.|  
|Quando si amministra un computer in remoto, non immettere password di account con privilegi.|Eventuale software in grado di osservare l'input da tastiera potrebbe infatti acquisire le password. Questa violazione potrebbe avvenire anche tramite l'esecuzione nel computer client di un programma diverso da quello presupposto dall'utente del controllo remoto. Se sono richiesti account e password, l'utente finale deve immetterli.|  
|Durante una sessione di controllo remoto bloccare la tastiera e il mouse.|Se Configuration Manager rileva che la connessione di controllo remoto è terminata, blocca automaticamente la tastiera e il mouse per impedire a un utente di assumere il controllo della sessione di controllo remoto aperta. Tale rilevamento, però, potrebbe non essere immediato e comunque non si verifica se il servizio di controllo remoto è stato arrestato.<br /><br /> Selezionare l'azione **Blocca tastiera e mouse remoti** nella finestra **Controllo remoto di Configuration Manager** .|  
|Non consentire agli utenti di configurare le impostazioni di controllo remoto in Software Center.|Non abilitare l'impostazione client **Gli utenti possono modificare le impostazioni di criteri o notifiche in Software Center** per evitare che gli utenti vengano controllati. Se un utente la cambia, questa impostazione può consentire di visualizzare in modalità remota un altro utente nello stesso computer. <br /><br />**Questa impostazione si riferisce al computer e non all'utente connesso**.|  
|Abilitare il profilo di Windows Firewall **Dominio** .|Abilitare l'impostazione client **Abilitare controllo remoto nei client Profili delle eccezioni firewall** e quindi selezionare il profilo di Windows Firewall **Dominio** per i computer della Intranet.|  
|Se ci si disconnette durante una sessione di controllo remoto e si riaccede con un account utente diverso, assicurarsi di eseguire la disconnessione prima di disconnettere la sessione di controllo remoto.|In questo scenario, se non si esegue la disconnessione, la sessione rimane aperta.|  
|Non concedere diritti di amministratore locale agli utenti.|Se si concedono diritti di amministratore locale agli utenti, questi ultimi potrebbero assumere il controllo della sessione di controllo remoto o compromettere le credenziali dell'amministratore.|  
|Per configurare le impostazioni di Assistenza remota, usare Criteri di gruppo o Configuration Manager, ma non entrambi.|È possibile usare Configuration Manager e Criteri di gruppo per apportare modifiche di configurazione alle impostazioni di Assistenza remota. Con l'aggiornamento di Criteri di gruppo nel client, per impostazione predefinita la procedura viene ottimizzata con la modifica dei soli criteri modificati nel server. Configuration Manager modifica le impostazioni nei criteri di sicurezza locali, che potrebbero essere sovrascritti solo se viene forzato l'aggiornamento di Criteri di gruppo.<br /><br /> Se si impostano i criteri in entrambe le posizioni si potrebbero ottenere risultati incoerenti. Per configurare le impostazioni di Assistenza remota, scegliere uno di questi metodi.|  
|Abilitare l'impostazione client **Richiedere all'utente l'autorizzazione di controllo remoto**.|Anche se esistono metodi alternativi a questa impostazione per richiedere all'utente di confermare una sessione remota, abilitare questa impostazione per ridurre la possibilità che gli utenti vengano controllati mentre eseguono attività riservate.<br /><br /> Inoltre, invitare gli utenti a verificare il nome dell'account visualizzato durante la sessione di controllo remoto e a disconnettere la sessione se si sospetta che l'account non sia autorizzato.|  
|Limitare l'elenco dei visualizzatori autorizzati.|Per usare il controllo remoto non sono necessari diritti di amministratore locale.|  

### <a name="security-issues-for-remote-control"></a>Problemi di sicurezza per il controllo remoto  
 La gestione dei computer client tramite controllo remoto presenta i problemi di sicurezza seguenti:  

-   Non considerare affidabili i messaggi di controllo di controllo remoto.  

     Se si avvia una sessione di controllo remoto e quindi si accede con credenziali alternative, i messaggi di controllo vengono inviati dall'account originale e non dall'account che usa le credenziali alternative.  

     Non vengono inviati messaggi di controllo se anziché installare la console di Configuration Manager si copiano i file binari per il controllo remoto e quindi si esegue il controllo remoto dal prompt dei comandi.  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per il controllo remoto  
 Il controllo remoto consente di visualizzare le sessioni attive nei computer client di Configuration Manager e, potenzialmente, tutte le informazioni archiviate in tali computer. Per impostazione predefinita, il controllo remoto non è abilitato.  

 È possibile configurare il controllo remoto in modo da visualizzare in modo evidente un messaggio di preavviso e ottenere il consenso dall'utente prima di iniziare una sessione, ma è anche possibile monitorare gli utenti senza la loro autorizzazione e senza che ne siano consapevoli. È possibile configurare il livello di accesso di sola visualizzazione, in modo che non sia possibile eseguire modifiche durante il controllo remoto, o di controllo completo. Nella sessione di controllo remoto viene visualizzato l'account dell'amministratore connesso, per consentire agli utenti di identificare chi si connette al loro computer.  

 Per impostazione predefinita, Configuration Manager concede l'autorizzazione di controllo remoto al gruppo Administrators locale.  

 Prima di configurare il controllo remoto, prendere in considerazione i requisiti in vigore relativi alla privacy.  
