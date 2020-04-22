---
title: Panoramica dei certificati CNG
titleSuffix: Configuration Manager
description: Informazioni sul supporto dei certificati Cryptography Next Generation (CNG) per i clienti e i server Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4574b7ae97e8200da248a0b798677eacadb6229f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703079"
---
# <a name="cng-certificates-overview"></a>Panoramica dei certificati CNG
<!-- 1356191 --> 

Configuration Manager offre supporto limitato per la crittografia, ovvero solo per certificati CNG. I client di Configuration Manager possono usare certificati di autenticazione client con chiave privata nel provider di archiviazione chiavi (KSP) CNG. Con il supporto per i provider di archiviazione chiavi, i client di Configuration Manager supportano chiavi private basate sull'hardware, ad esempio TPM KSP per i certificati di autenticazione client PKI.

## <a name="supported-scenarios"></a>Scenari supportati
È possibile usare i modelli di certificato dell'[API di crittografia CNG (Cryptography Next Generation)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) per gli scenari seguenti:

- Registrazione e comunicazione dei client con un punto di gestione HTTPS   
- Distribuzione di software e applicazioni con un punto di distribuzione HTTPS   
- Distribuzione del sistema operativo  
- Client messaging SDK (con l'aggiornamento più recente) e proxy ISV   
- Configurazione di Cloud Management Gateway  

A partire dalla versione 1802, usare i certificati CNG per i seguenti ruoli del server abilitati per HTTPS: <!-- 1357314 -->   
- Punto di gestione
- Punto di distribuzione
- Punto di aggiornamento software
- Punto di migrazione stato     

A partire dalla versione 1806, usare i certificati CNG per i ruoli del server seguenti abilitati per HTTPS:

- Punto di registrazione certificati, incluso il server del servizio Registrazione dispositivi di rete con il modulo di criteri di Configuration Manager <!--1357314-->

> [!NOTE]
> CNG è compatibile con le versioni precedenti di Crypto API (CAPI). I certificati CAPI continuano a essere supportati anche quando nel client è abilitato il supporto per CNG.

## <a name="unsupported-scenarios"></a>Scenari non supportati

Attualmente non sono supportati gli scenari seguenti:

- I ruoli del server seguenti non sono operativi se installati in modalità HTTPS con un certificato CNG associato al sito Web in Internet Information Services (IIS): 
    - Servizio Web del Catalogo applicazioni
    - Sito Web del Catalogo applicazioni
    - Punto di registrazione  
    - Punto proxy di registrazione  

- Software Center non visualizza come disponibili le applicazioni e i pacchetti distribuiti in raccolte di utenti o di gruppi di utenti.

- Uso di certificati CNG per creare un punto di distribuzione cloud.

- Se il modulo criteri NDES usa un certificato CNG per l'autenticazione client, la comunicazione con il punto di registrazione certificati non riesce. 
    - Questa funzionalità è supportata a partire da Configuration Manager versione 1806.

- Se si specifica un certificato CNG durante la creazione dei supporti della sequenza di attività, la procedura guidata non riesce a creare supporti di avvio.
    - Questa funzionalità è supportata a partire da Configuration Manager versione 1806.

## <a name="to-use-cng-certificates"></a>Per usare certificati CNG

Per usare i certificati CNG, l'autorità di certificazione (CA) deve fornire i modelli di certificato CNG per i computer di destinazione. I dettagli dei modelli variano in base allo scenario. Le proprietà seguenti, tuttavia, sono obbligatorie:

- Scheda **Compatibilità**

    - L'**autorità di certificazione** deve essere Windows Server 2008 o versione successiva. È consigliabile usare Windows Server 2012.

    - Il **destinatario del certificato** deve essere Windows Vista/Windows Server 2008 o versione successiva. È consigliabile usare Windows 8/Windows Server 2012.

- Scheda **Crittografia**

    - **Categoria provider** deve corrispondere a **Provider di archiviazione chiavi**. (obbligatorio).
    - L'opzione **Le richieste devono utilizzare uno dei provider seguenti** deve essere impostata sul **provider di archiviazione chiavi per software Microsoft**. 

> [!NOTE]
> I requisiti per l'ambiente o l'organizzazione possono essere diversi. Contattare l'esperto di PKI. L'aspetto importante da considerare è che un modello di certificato deve usare un provider di archiviazione chiavi per trarre vantaggio da CNG.

Per ottenere risultati ottimali, è consigliabile creare il nome soggetto da informazioni di Active Directory. Usare il nome DNS per **Formato del nome soggetto** e includere il nome DNS nel nome soggetto alternativo. In caso contrario, è necessario fornire queste informazioni durante la registrazione del dispositivo nel profilo del certificato.
