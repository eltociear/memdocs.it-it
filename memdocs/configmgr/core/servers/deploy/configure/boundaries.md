---
title: Definire limiti
titleSuffix: Configuration Manager
description: Di seguito viene spiegato come definire i percorsi di rete nella intranet che possono contenere i dispositivi da gestire.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700062"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definire percorsi di rete come limiti di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I limiti di Configuration Manager sono costituiti dai percorsi di rete in cui sono contenuti i dispositivi da gestire. È possibile creare diversi tipi di limiti, ad esempio un sito di Active Directory o un indirizzo IP di rete. Quando il client di Configuration Manager identifica un percorso di rete simile, il dispositivo è parte del limite.

Configuration Manager supporta i tipi di limiti seguenti:

- Subnet IP
- Sito di Active Directory
- Prefisso IPv6
- Intervallo indirizzi IP
- VPN (a partire dalla versione 2006)

È possibile creare manualmente i singoli limiti o usare [Individuazione foresta Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest). Questo metodo di individuazione rileva e crea automaticamente i limiti per le subnet IP e i siti di Active Directory. Quando l'individuazione foresta Active Directory individua una supernet per un sito di Active Directory, Configuration Manager converte la supernet in un limite Intervallo di indirizzi IP.

Se un dispositivo non è presente nel limite previsto, è possibile che non sia stato definito il percorso di rete come limite. Quando il percorso di rete di un dispositivo è in dubbio, usare i comandi di Windows seguenti sul dispositivo per confermare:

- Indirizzo IP: `ipconfig`
- Sito di Active Directory: `nltest /dsgetsite`
- VPN: `ipconfig /all`

## <a name="boundary-types"></a>Tipi di limiti

### <a name="ip-subnet"></a>Subnet IP

Il tipo di limite della subnet IP richiede un **ID subnet**. Ad esempio: `169.254.0.0`. Se si specificano i valori di **Rete** (gateway predefinito) e **Subnet mask**, Configuration Manager calcola automaticamente l'**ID subnet**. Quando si salva il limite, Configuration Manager salva solo il valore di ID subnet.

> [!NOTE]
> Configuration Manager non supporta l'immissione diretta di una supernet come limite. È possibile, invece, usare il tipo di limite Intervallo di indirizzi IP.

### <a name="active-directory-site"></a>Sito di Active Directory

Per il tipo di limite **Sito di Active Directory**, specificare il nome del sito. È possibile digitare il nome o esplorare la foresta locale del server del sito.

Quando si specifica un sito di Active Directory per un limite, il limite include ogni subnet IP appartenente a tale sito di Active Directory. Se la configurazione del sito Active Directory viene modificata in Active Directory, verranno modificati anche i percorsi di rete inclusi in questo limite.  

I limiti del sito di Active Directory non sono applicabili ai dispositivi Azure Active Directory (Azure AD) puri, detti anche dispositivi aggiunti a un dominio cloud. Se effettuano il roaming locale e si creano solo i limiti del tipo Sito di Active Directory, questi dispositivi non rientrano in un limite.

> [!TIP]
> Usare il comando di Windows seguente per visualizzare il sito di Active Directory corrente di un dispositivo: `nltest /dsgetsite`.
>
> Per determinare se un client è aggiunto a un dominio cloud, usare il comando di Windows seguente: `dsregcmd /status`. Per altre informazioni, vedere [comando dsregcmd - stato del dispositivo](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### <a name="ipv6-prefix"></a>Prefisso IPv6

Per il tipo di limite **Prefisso IPv6**, è necessario specificare un **Prefisso**. Ad esempio: `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>Intervallo indirizzi IP

Per il tipo di limite **Intervallo indirizzi IP**, specificare **Indirizzo IP iniziale** e **Indirizzo IP finale** per l'intervallo. L'intervallo può includere parte di una subnet IP o più subnet IP. Usare un tipo di limite Intervallo di indirizzi IP per supportare una supernet.

È anche possibile usare questo tipo per definire un limite per un singolo indirizzo IP. Impostare gli indirizzi IP iniziale e finale con lo stesso valore. Questa configurazione può essere utile per i dispositivi o gli ambienti di test univoci.

### <a name="vpn"></a>Connessione

<!--7020519-->

A partire dalla versione 2006, per semplificare la gestione dei client remoti, creare un tipo di limite per le VPN. Quando un client invia una richiesta di posizione, include informazioni aggiuntive sulla propria configurazione di rete. In base a queste informazioni, il server determina se il client si trova su una VPN. Affinché Configuration Manager associ il client nel limite, è necessario connettere il dispositivo alla VPN.

È possibile configurare un limite VPN in diversi modi:

- **Rilevamento automatico della VPN**: Configuration Manager rileva qualsiasi soluzione VPN che usa il protocollo PPTP (Point-to-Point Tunneling Protocol). Se la VPN non viene rilevata, usare una delle altre opzioni. Il valore di limite nell'elenco della console sarà `Auto:On`.

- **Nome della connessione**: specificare il nome della connessione VPN nel dispositivo. Si tratta del nome della scheda di rete in Windows per la connessione VPN. Configuration Manager trova la corrispondenza dei primi 250 caratteri della stringa, ma non supporta caratteri jolly o stringhe parziali. Il valore limite nell'elenco della console sarà `Name:<name>`, dove `<name>` è il nome della connessione specificato.

  Ad esempio, si esegue il comando `ipconfig` nel dispositivo e una delle sezioni inizia con: `PPP adapter ContosoVPN:`. Usare la stringa `ContosoVPN` come **Nome connessione**. Viene visualizzata nell'elenco come `Name:CONTOSOVPN`.

- **Descrizione della connessione**: specificare la descrizione della connessione VPN. Configuration Manager trova la corrispondenza dei primi 243 caratteri della stringa, ma non supporta caratteri jolly o stringhe parziali. Il valore limite nell'elenco della console sarà `Description:<description>`, dove `<description>` è la descrizione della connessione specificata.

  Ad esempio, si esegue il comando `ipconfig /all` nel dispositivo e una delle connessioni include la riga seguente: `Description . . . . . . . . . . . : ContosoMainVPN`. Usare la stringa `ContosoMainVPN` come **Descrizione connessione**. Viene visualizzata nell'elenco come `Description:CONTOSOMAINVPN`.

> [!IMPORTANT]
> Per sfruttare i vantaggi di questa funzionalità, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Quando si aggiornano il sito e la console, la nuova funzionalità viene visualizzata nella console di Configuration Manager. Lo scenario completo non funzionerà fin quando anche la versione del client sarà la più recente.
>
> Per usare questo limite per le VPN durante la distribuzione di un sistema operativo, assicurarsi di aggiornare anche l'immagine di avvio per includere i binari del client più recenti.

## <a name="create-a-boundary"></a>Creare un limite

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Limiti**.

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea limite**.

1. Nella scheda **Generale** della finestra **Crea limite** specificare le informazioni seguenti:

    - **Descrizione**: identificare il limite tramite un nome descrittivo o un riferimento.

        > [!NOTE]
        > Configuration Manager denomina automaticamente il limite in base al tipo e all'ambito. Non è possibile modificare il nome.

    - **Tipo**: selezionare il tipo di limite da creare. Specificare quindi le informazioni aggiuntive necessarie per il tipo. Per altre informazioni, vedere [Tipi di limiti](#boundary-types).

1. Passare alla scheda **Gruppi limite**. Se si dispone già di gruppi di limiti nel sito, è possibile aggiungere immediatamente questo nuovo limite a uno o più gruppi.

1. Selezionare **OK** per salvare il nuovo limite.

## <a name="configure-a-boundary"></a>Configurare un limite

> [!TIP]
> Quando si crea un limite, Configuration Manager assegna automaticamente un nome basato sul tipo e sull'ambito del limite. Non è possibile modificare questo nome. Per identificare più facilmente il limite nella console di Configuration Manager, specificare una descrizione.

1. Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Limiti**.

1. Selezionare il limite da modificare. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.

1. Nella finestra **Proprietà** del limite, nella scheda **Generale**, configurare le impostazioni seguenti:

    - Modificare la **descrizione**
    - Modificare il **tipo** di limite
    - Modificare l'ambito di un limite cambiando i percorsi di rete. Per un limite del sito Active Directory è possibile ad esempio specificare un nuovo nome del sito Active Directory.

1. Per visualizzare i sistemi del sito associati a questo limite, passare alla scheda **Sistemi del sito**. Non è possibile modificare questa configurazione dalle proprietà di un limite.

    > [!TIP]
    > Per elencare un server come sistema del sito per un limite, associarlo come server di sistema del sito per almeno un gruppo di limiti che include questo limite. Applicare questa configurazione nella scheda **Riferimenti** di un gruppo di limiti. Per altre informazioni, vedere [Configurare l'assegnazione sito e selezionare i server del sistema del sito](boundary-group-procedures.md#bkmk_references).

1. Per modificare l'appartenenza al gruppo di limiti per questo limite, selezionare la scheda **Gruppi di limiti**:

    - Per aggiungere questo limite a uno o più gruppi di limiti, selezionare **Aggiungi**. Selezionare uno o più gruppi di limiti e quindi fare clic su **OK**.

    - Per rimuovere questo limite da un gruppo di limiti, scegliere il gruppo di limiti e quindi selezionare **Rimuovi**.

1. Per chiudere le proprietà del limite e salvare la configurazione, selezionare **OK**.

## <a name="next-steps"></a>Passaggi successivi

Ogni limite può essere usato da tutti i siti compresi nella gerarchia. Dopo aver creato un limite, aggiungere il limite a uno o più [gruppi di limiti](boundary-groups.md).