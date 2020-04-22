---
title: Strumento di reimpostazione dell'aggiornamento
titleSuffix: Configuration Manager
description: Usare lo strumento di reimpostazione dell'aggiornamento per gli aggiornamenti nella console per Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704329"
---
# <a name="update-reset-tool"></a>Strumento di reimpostazione dell'aggiornamento

*Si applica a: Configuration Manager (Current Branch)*  


A partire dalla versione 1706, i siti primari e i siti di amministrazione centrale di Configuration Manager includono lo strumento di reimpostazione dell'aggiornamento di Configuration Manager, **CMUpdateReset.exe**. Usare lo strumento per correggere gli errori quando gli aggiornamenti nella console presentano problemi durante il download o la replica. Lo strumento si trova nella cartella ***\cd.latest\SMSSETUP\TOOLS*** del server del sito.

È possibile usare questo strumento con qualsiasi versione di Current Branch supportata.

Usare questo strumento quando un [aggiornamento nella console](install-in-console-updates.md) non è ancora installato e si trova in uno stato di errore. Uno stato di errore indica che il download dell'aggiornamento è in corso, ma è bloccato o sta richiedendo troppo tempo. Per "troppo tempo" si intende più ore di quanto previsto in base alle precedenti esperienze con aggiornamenti di dimensioni simili. Può anche trattarsi di un errore nella replica dell'aggiornamento nei siti primari figlio.  

Lo strumento viene eseguito nell'aggiornamento specificato. Per impostazione predefinita, lo strumento non elimina gli aggiornamenti scaricati o installati correttamente.  

### <a name="prerequisites"></a>Prerequisiti
L'account usato per eseguire lo strumento richiede le autorizzazioni seguenti:
- **Lettura** e **Scrittura** per il database del sito di amministrazione centrale e per ogni sito primario della gerarchia. Per impostare queste autorizzazioni, è possibile aggiungere l'account utente come membro dei [ruoli predefiniti del database](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** e **db_datareader** nel database di Configuration Manager di ogni sito. Lo strumento non interagisce con i siti secondari.
- **Amministratore locale** nel sito di livello superiore della gerarchia.
- **Amministratore locale** nel computer che ospita il punto di connessione del servizio.

È necessario il GUID dell'aggiornamento da reimpostare. Per ottenere il GUID:
  1.   Nella console passare ad **Amministrazione** > **Aggiornamenti e manutenzione**.
  2.   Nel riquadro informazioni fare clic con il pulsante destro del mouse sull'intestazione di una delle colonne, ad esempio **Stato**, quindi selezionare **GUID pacchetto** per aggiungere tale colonna alle informazioni.
  3.   La colonna visualizza ora il GUID dell'aggiornamento.

> [!TIP]  
> Per copiare il GUID, selezionare la riga del pacchetto di aggiornamento da ripristinare e quindi copiarla premendo CTRL+C. Copiando la selezione in un editor di testo, è possibile copiare solo il GUID per usarlo come parametro della riga di comando quando si esegue lo strumento.

### <a name="run-the-tool"></a>Eseguire lo strumento    
Lo strumento deve essere eseguito nel sito di livello superiore della gerarchia.

Quando si esegue lo strumento, usare i parametri della riga di comando per specificare:
- L'istanza di SQL Server nel sito di livello superiore della gerarchia.
- Il nome del database del sito nel sito di livello superiore.
- Il GUID dell'aggiornamento da reimpostare.

In base allo stato dell'aggiornamento, lo strumento identifica i server aggiuntivi a cui deve accedere.   

Se il pacchetto di aggiornamento è nella fase *successiva al download*, lo strumento non esegue la pulizia del pacchetto. In alternativa, è possibile forzare la rimozione di un aggiornamento scaricato correttamente usando il parametro per l'eliminazione forzata. I parametri della riga di comando vengono descritti più avanti in questo argomento.

Dopo l'esecuzione dello strumento:
- Se un pacchetto è stato eliminato, riavviare il servizio SMS_Executive nel sito di livello superiore. Verificare la disponibilità di aggiornamenti per poter scaricare nuovamente il pacchetto.
- Se un pacchetto non è stato eliminato, non è necessario intraprendere alcuna azione. L'aggiornamento reinizializza e quindi riavvia la replica o l'installazione.

**Parametri della riga di comando:**  


|                        Parametro                         |                                                       Descrizione                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN dell'istanza di SQL Server del sito di livello superiore>** | *Richiesto* <br> Specificare il nome di dominio completo dell'istanza di SQL Server che ospita il database del sito per il sito di livello superiore della gerarchia. |
|                **-D &lt;Nome database>**                 |                          *Richiesto* <br> Specificare il nome del database nel sito di livello superiore.                          |
|                 **-P &lt;GUID pacchetto>**                 |                        *Richiesto* <br> Specificare il GUID dell'aggiornamento da reimpostare.                        |
|           **-I &lt;Nome istanza SQL Server>**           |                    *Facoltativo* <br> Identifica l'istanza di SQL Server che ospita il database del sito.                     |
|                       **-FDELETE**                       |                       *Facoltativo* <br> Forza l'eliminazione di un aggiornamento scaricato correttamente.                        |

**Esempi:**  
In uno scenario tipico, si vuole reimpostare un aggiornamento che presenta problemi di download. L'FQDN di SQL Server è *server1.fabrikam.com*, il database del sito è *CM_XYZ* e il GUID del pacchetto è *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Eseguire: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

In uno scenario più complesso, si vuole forzare l'eliminazione del pacchetto di aggiornamento che crea problemi. L'FQDN di SQL Server è *server1.fabrikam.com*, il database del sito è *CM_XYZ* e il GUID del pacchetto è *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Eseguire: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
