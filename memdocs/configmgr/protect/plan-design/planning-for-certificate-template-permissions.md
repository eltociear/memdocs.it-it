---
title: Pianificazione delle autorizzazioni per i modelli di certificato
titleSuffix: Configuration Manager
description: Informazioni sulla pianificazione delle autorizzazioni necessarie per configurare i modelli di certificato usati da Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 075d371a334f26a788c656fe85ec01ae2338eb26
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074827"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Pianificazione per autorizzazioni modello di certificato per profili certificato in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


Le informazioni seguenti illustrano come pianificare la modalità di configurazione delle autorizzazioni per i modelli di certificato usati da Configuration Manager quando vengono distribuiti i profili certificato.  

## <a name="default-security-permissions-and-considerations"></a>Autorizzazioni di sicurezza predefinite e considerazioni  
 Le autorizzazioni di sicurezza predefinite necessarie per i modelli di certificato che vengono usate da Configuration Manager per richiedere certificati per utenti e dispositivi sono le seguenti:  

- Lettura e registrazione per l'account utilizzato dal pool di applicazioni del servizio Registrazione dispositivi di rete  

- Lettura per l'account che esegue la console di Configuration Manager  

  Per altre informazioni su queste autorizzazioni di sicurezza, vedere [Configurazione dell'infrastruttura di certificazione](../deploy-use/certificate-infrastructure.md).  

  Se si utilizza questa configurazione predefinita, gli utenti e i dispositivi non possono richiedere direttamente i certificati dai modelli di certificato e tutte le richieste devono essere avviate dal servizio Registrazione dispositivi di rete. È una limitazione importante perché questi modelli di certificato devono essere configurati con **Inserisci nella richiesta** per il soggetto del certificato, il che significa che c'è un rischio di rappresentazione se un utente non autorizzato o un dispositivo danneggiato richiede un certificato. Nella configurazione predefinita, il servizio Registrazione dispositivi di rete deve avviare una richiesta di questo tipo. Rimane tuttavia il rischio di rappresentazione se il servizio che esegue il servizio Registrazione dispositivi di rete viene danneggiato. Per evitare questo rischio, seguire tutte le procedure di protezione consigliate per il servizio Registrazione dispositivi di rete e il computer che esegue questo ruolo dei servizi.  

  Se le autorizzazioni di protezione predefinite non soddisfano i requisiti aziendali, è disponibile un'altra opzione per configurare le autorizzazioni di protezione nei modelli di certificato: Si possono aggiungere autorizzazioni di lettura e registrazione per utenti e computer.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Aggiunta di autorizzazioni Lettura e Registrazione per utenti e computer  
 L'aggiunta di autorizzazioni di lettura e registrazione potrebbe essere appropriata se un team separato gestisce il team dell'infrastruttura dell'autorità di certificazione (CA) e tale team separato vuole che Configuration Manager verifichi che gli utenti dispongano di un account Active Directory Domain Services valido prima di inviare loro un profilo certificato per richiedere un certificato utente. Per questa configurazione è necessario specificare uno o più gruppi di protezione che contengono gli utenti e quindi concedere loro le autorizzazioni Lettura e Registrazione nei modelli di certificato. In questo scenario, l'amministratore CA gestisce il controllo di protezione.  

 Nello stesso modo è possibile specificare uno o più gruppi di protezione che contengono gli utenti e concedono loro le autorizzazioni Lettura e Registrazione nei modelli di certificato. Se si distribuisce un profilo certificato del computer a un computer appartenente a un dominio, all'account di quel computer devono essere concesse le autorizzazioni Lettura e Registrazione. Queste autorizzazioni non sono necessarie se il computer non appartiene a un dominio, ad esempio se è un computer del gruppo di lavoro o un dispositivo mobile personale.  

 Sebbene questa configurazione utilizzi un controllo di protezione aggiuntivo, non è raccomandata come procedura consigliata. Il motivo è che gli utenti o proprietari specificati dei dispositivi potrebbero richiedere i certificati indipendentemente da Configuration Manager e specificare valori per l'oggetto del certificato che potrebbero essere usati per rappresentare un altro utente o dispositivo.  

 Inoltre, se si specificano account che non è possibile autenticare al momento della richiesta del certificato, per impostazione predefinita, non sarà possibile richiedere il certificato. Ad esempio, non sarà possibile richiedere il certificato se il server su cui è in esecuzione il servizio Registrazione dispositivi di rete è in una foresta Active Directory considerata non attendibile dalla foresta che contiene il server di sistema del sito del punto di registrazione certificati. È possibile configurare il punto di registrazione del certificato per continuare se un account non può essere autenticato perché non ottiene risposta da un controller di dominio. Non si tratta tuttavia di una procedura di protezione consigliata.  

 Se il punto di registrazione certificati è configurato per controllare le autorizzazioni dell'account e un controller di dominio è disponibile e rifiuta la richiesta di autenticazione (ad esempio, l'account è bloccato o è stato eliminato), la richiesta di registrazione del certificato avrà esito negativo.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Verificare le autorizzazioni Lettura e Registrazione per gli utenti e i computer appartenenti a un dominio  

1.  Nel server del sistema del sito che ospita il punto di registrazione certificati, creare la seguente chiave del Registro di sistema DWORD per avere un valore di 0:  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Se un account non può essere autenticato perché non si riceve alcuna risposta da un controller di dominio e si desidera ignorare la verifica delle autorizzazioni:  

    -   Nel server del sistema del sito che ospita il punto di registrazione certificati, creare la seguente chiave del Registro di sistema DWORD per avere un valore di 1:  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Nella CA emittente aggiungere uno o più gruppi di protezione per concedere agli account utente o dispositivo le autorizzazioni Lettura e Registrazione nella scheda **Protezione** delle proprietà del modello di certificato.  
