---
title: Connettori di certificati C per Microsoft Intune - Azure | Microsoft Docs
description: Informazioni sui connettori di certificati per certificati e profili di certificato SCEP (Simple Certificate Enrollment Protocol) o PKCS (Public Key Cryptography Standards) con Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428895"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Connettori di certificati per Microsoft Intune

Per supportare l'uso di certificati per l'autenticazione e la firma e la crittografia dei messaggi di posta elettronica tramite S/MIME, Intune richiede l'uso di un connettore di certificati. Un connettore di certificati è un componente software installato in un server locale. Il connettore consente ai dispositivi gestiti dal cloud di effettuare il provisioning dei certificati dall'infrastruttura locale, come un'autorità di certificazione emittente.

Questo articolo descrive i connettori disponibili, il relativo ciclo di vita, i prerequisiti per l'uso e come mantenerli aggiornati.  

## <a name="available-connectors"></a>Connettori disponibili

Sono disponibili due connettori di certificati per Intune. Ognuno ha usi e requisiti specifici.

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>Connettore di certificati PFX per Microsoft Intune

Il **connettore di certificati PFX** supporta la distribuzione di certificati per richieste di certificati PCKS #12 e gestisce le richieste per i file PFX importati in Intune per la crittografia della posta elettronica S/MIME per un utente specifico.

> [!TIP]
> Prima dell'aggiornamento di agosto per questo connettore, le richieste di certificati PKCS #12 venivano gestite dal *connettore di certificati Intune*. Con l'aggiornamento di agosto, la funzionalità per tutte le richieste di certificati PKCS è stata consolidata nel *connettore di certificati PFX*, che supporta l'aggiornamento automatico del connettore alle nuove versioni e richiede l'uso di .NET Framework versione 4.7.2.
>
> Le funzionalità del connettore Microsoft Intune non sono deprecate ed è possibile continuare a usarle con i profili di certificato PKCS. Tuttavia, se non si usa SCEP o se non occorre usare il servizio Registrazione dispositivi di rete per altri motivi, è possibile passare al connettore di certificati PFX e rimuovere il servizio Registrazione dispositivi di rete dai server. 

**Il connettore di certificati PFX**:

- Supporta più istanze di questo connettore per ogni tenant di Intune. Ogni istanza del connettore deve essere installata in un server Windows e avere accesso alla chiave privata usata per crittografare le password dei file PFX caricati.
- Può essere installato nello stesso server in cui è ospitata un'istanza del *connettore Microsoft Intune*.
- Supporta [aggiornamenti automatici](#automatic-update) alle nuove versioni. Per installare automaticamente nuove versioni, il computer che ospita il connettore deve contattare **autoupdate.msappproxy.net** sulla porta **443**. Se l'aggiornamento automatico del connettore non riesce, è possibile aggiornare manualmente il connettore.
- Supporta la revoca dei certificati (è richiesta la versione del connettore **6.2008.60.607** o versione successiva)
- Ha gli stessi requisiti di rete dei [dispositivi gestiti](../fundamentals/intune-endpoints.md#access-for-managed-devices)

  Per altre informazioni, vedere [Endpoint di rete per Microsoft Intune](../fundamentals/intune-endpoints.md) e [Requisiti di configurazione di rete di Intune e larghezza di banda](../fundamentals/network-bandwidth-use.md).

**Il server Windows in cui viene installato il connettore**:

- Deve eseguire Windows Server 2012 R2 o versione successiva.
- Esegue NET Framework 4.7.2.  

**Per installare il connettore di certificati PFX**:

Per istruzioni sull'installazione di questo connettore, vedere [Scaricare, installare e configurare il connettore di certificati PFX](certficates-pfx-configure.md).

### <a name="microsoft-intune-connector"></a>Connettore Microsoft Intune

Il **connettore Microsoft Intune** viene a volta indicato come *Connettore di certificati di Microsoft Intune*. Questo connettore supporta la distribuzione di certificati quando si usa *SCEP* (Simple Certificate Enrollment Protocol) ed è disponibile un'autorità di certificazione (CA) per Servizi certificati Active Directory. Questo tipo di CA è nota anche come *CA Microsoft*.

Quando si usa SCEP con una CA Microsoft, è necessario configurare anche il **servizio Registrazione dispositivi di rete** (NDES). Per questo motivo, questo connettore è spesso indicato come *connettore di certificati NDES*.

Se si usa un'[autorità di certificazione di terze parti](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), non è necessario usare questo connettore e il servizio Registrazione dispositivi di rete non è richiesto.

**Il connettore Microsoft Intune**:

- Viene installato in un server Windows, che può ospitare anche un'istanza del *connettore di certificati PFX*.
- Sono supportate fino a 100 istanze di questo connettore per ogni tenant, con ogni istanza in un server Windows separato. Quando si usano più connettori:
  - Tutte le istanze del *connettore Microsoft Intune* nell'ambiente in uso devono essere della stessa versione.
  - L'infrastruttura supporta la ridondanza e il bilanciamento del carico perché qualsiasi istanza del connettore disponibile può elaborare le richieste di certificati.
- Richiede un [aggiornamento manuale](#manual-update) per installare la nuova versione del connettore. Per l'aggiornamento manuale è necessario disinstallare il connettore corrente e quindi installare la nuova versione del connettore. Non dovrebbero essere necessarie altre azioni.
- Supporta la modalità *FIPS* (Federal Information Processing Standard). La modalità FIPS non è obbligatoria. Quando lo standard FIPS è abilitato, è possibile emettere e revocare i certificati.
- Ha gli stessi requisiti di rete dei [dispositivi gestiti](../fundamentals/intune-endpoints.md#access-for-managed-devices).

  Per altre informazioni, vedere [Endpoint di rete per Microsoft Intune](../fundamentals/intune-endpoints.md) e [Requisiti di configurazione di rete di Intune e larghezza di banda](../fundamentals/network-bandwidth-use.md).

**Il server Windows in cui viene installato il connettore**:

- Deve eseguire Windows Server 2012 R2 o versione successiva.
- Esegue NET Framework 4.5. Quando questo connettore viene installato nello stesso server del *connettore di certificati PFX*, è necessario usare .NET Framework 4.7.2, richiesto per il connettore PFX.
- Non può essere lo stesso server in cui è ospitata l'autorità di certificazione (CA) emittente.
- Se usato per SCEP con una CA Microsoft, è richiesto l'accesso a un server che esegue il servizio Registrazione dispositivi di rete. Il servizio Registrazione dispositivi di rete viene eseguito in un server Windows e può essere eseguito nello stesso server di questo connettore.

**Quando è richiesto il servizio Registrazione dispositivi di rete**:

- La configurazione della sicurezza avanzata di Internet Explorer [deve essere disabilitata nel server che ospita il servizio Registrazione dispositivi di rete](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) e nel server che ospita il *connettore Microsoft Intune*.
- Il connettore richiede configurazioni aggiuntive per comunicare con il servizio Registrazione dispositivi di rete. Informazioni sulle procedure per l'installazione e la configurazione del servizio Registrazione dispositivi di rete sono disponibili insieme alle procedure per l'installazione del *connettore Microsoft Intune*.

  Per altre informazioni, vedere [Linee guida per il servizio Registrazione dispositivi di rete](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

**Per installare il connettore Microsoft Intune**:

Per istruzioni sull'installazione di questo connettore, vedere [Configurare l'infrastruttura per il supporto di SCEP con Intune](certificates-scep-configure.md).

## <a name="connector-lifecycle"></a>Ciclo di vita dei connettori

Periodicamente, vengono rilasciate versioni aggiornate dei connettori di certificato. Gli annunci per le nuove versioni dei connettori vengono visualizzati nell'articolo (Novità](../fundamentals/whats-new.md) per Intune e nella sezione [Novità dei connettori](#whats-new-for-connectors) verso la fine di questo articolo.

Quando viene rilasciata una nuova versione, il supporto per la versione precedente viene deprecato con un periodo di tolleranza limitato per continuare a usarla. Una volta scaduto il periodo di tolleranza, il supporto per la versione deprecata termina e può smettere di funzionare in qualsiasi momento. Il periodo di tolleranza è di sei mesi.

Pianificare l'aggiornamento di un connettore alla versione più recente non appena praticabile. Ogni connettore ha un percorso di aggiornamento diverso:

- **Connettore di certificati PFX per Microsoft Intune** - Supporta gli aggiornamenti automatici.
- **Connettore Microsoft Intune** - Richiede l'aggiornamento manuale.

### <a name="automatic-update"></a>Aggiornamento automatico

Se supportato dal tipo di connettore e dall'ambiente, Intune può aggiornare automaticamente il connettore alla versione più recente subito dopo il rilascio di tale versione del connettore.  

Per eseguire l'aggiornamento automaticamente, il server che ospita il connettore deve accedere al **servizio di aggiornamento Azure**:

- Porta: **443**
- Endpoint: **autoupdate.msappproxy.net**

Quando i firewall, l'infrastruttura o le configurazioni di rete limitano l'accesso per l'aggiornamento automatico, risolvere i problemi che rappresentano un impedimento o aggiornare manualmente il connettore alla nuova versione.

### <a name="manual-update"></a>Aggiornamento manuale

Il processo di aggiornamento manuale di un connettore di certificati è uguale a quello per la reinstallazione di un connettore.

È possibile aggiornare manualmente un connettore di certificati anche quando supporta gli aggiornamenti automatici. Ad esempio, è possibile aggiornare manualmente il connettore quando la configurazione di rete impedisce un aggiornamento automatico.  

### <a name="to-reinstall-a-certificate-connector"></a>Per reinstallare un connettore di certificati

1. Nel server Windows che ospita il connettore usare **App e funzionalità di Windows** per disinstallare il connettore.

2. Per installare la nuova versione, usare la procedura per installare una nuova versione del connettore. Assicurarsi di verificare la presenza di eventuali prerequisiti nuovi o aggiornati quando si installa una versione più recente di un connettore:
   - SCEP: [Configurare l'infrastruttura per il supporto di SCEP con Intune](certificates-scep-configure.md)
   - PKCS: [Scaricare, installare e configurare il connettore di certificati PFX per Microsoft Intune](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>Stato e versione del connettore

Nell'interfaccia di amministrazione di Microsoft Endpoint Manager è possibile selezionare un connettore di certificati per visualizzare informazioni sullo stato e controllarne la versione:

1. Accedere all'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Passare ad **Amministrazione del tenant** > **Connettori e token** > **Connettori di certificati**.

3. Selezionare un connettore per visualizzarne lo stato.

Quando si visualizza lo stato del connettore:

- I connettori deprecati verranno visualizzati con un **avviso**. Dopo il periodo di tolleranza di sei mesi l'avviso diventa un errore.
- Per i connettori con periodo di tolleranza scaduto viene visualizzato un errore. Questi connettori non sono più supportati e possono smettere di funzionare in qualsiasi momento.

## <a name="whats-new-for-connectors"></a>Novità dei connettori

Periodicamente vengono rilasciati aggiornamenti per i due connettori di certificati. Quando un connettore viene aggiornato, le modifiche vengono illustrate qui.

### <a name="pfx-certificate-connector-release-history"></a>Cronologia delle versioni del connettore di certificati PFX

Il *connettore di certificati PFX per Microsoft Intune* [supporta gli aggiornamenti automatici](#automatic-update).

#### <a name="august-26-2020"></a>26 agosto 2020

**Versione 6.2008.60.607** - Modifiche in questa versione:

- È richiesto .NET Framework versione 4.7.2
- Sostituzione dell'uso del *connettore Microsoft Intune* per i profili di certificato PKCS. Il *connettore di certificati PFX* è ora l'unico connettore necessario per usare certificati PCKS #12 o certificati PFX importati.
- Aggiunta del supporto per l'uso di profili di certificato PKCS con tutte le piattaforme supportate ad eccezione di Windows 8.1.
- Aggiunta del supporto per la revoca dei certificati per Outlook S/MIME.

#### <a name="november-18-2019"></a>18 novembre 2019

**Versione: 6.1911.11.602** - Modifiche in questa versione:

- Aggiunta del supporto di S/MIME per l'importazione PFX.  

#### <a name="may-17-2019"></a>17 maggio 2019

**Versione 6.1905.0.404** - Modifiche in questa versione:

- È stato risolto un problema a causa del quale i certificati PFX esistenti continuano a essere rielaborati e di conseguenza il connettore smette di elaborare le nuove richieste. 

#### <a name="may-6-2019"></a>6 maggio 2019

**Versione 6.1905.0.402** - Modifiche in questa versione:

- L'intervallo di polling per il connettore è stato ridotto da 5 minuti a 30 secondi.

#### <a name="april-2-2019"></a>2 aprile 2019

**Versione 6.1904.0.401** - Modifiche in questa versione:

- Questo connettore supporta ora l'aggiornamento automatico.
- È stato risolto un problema a causa del quale può verificarsi un errore di registrazione in Intune dopo avere eseguito l'accesso al connettore con un account amministratore globale.

### <a name="microsoft-intune-connector-release-history"></a>Cronologia delle versioni di Connettore Microsoft Intune

#### <a name="april-2-2019"></a>2 aprile 2019

**Versione 6.1904.1.0** - Modifiche in questa versione:  

- È stato risolto un problema a causa del quale può verificarsi un errore di registrazione in Intune dopo avere eseguito l'accesso al connettore con un account amministratore globale.
- Include correzioni relative all'affidabilità della revoca dei certificati.
- Include correzioni relative alle prestazioni per aumentare la velocità di elaborazione delle richieste di certificati PKCS.

## <a name="next-steps"></a>Passaggi successivi

Creare profili di certificato SCEP, PKCS o PKCS importati per ogni piattaforma che si vuole usare. Per continuare, vedere gli articoli seguenti:

- [Configurare l'infrastruttura per supportare i certificati SCEP con Intune](certificates-scep-configure.md)  
- [Configurare e gestire i certificati PKCS con Intune](certficates-pfx-configure.md)  
- [Creare un profilo di certificato PKCS importato](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
