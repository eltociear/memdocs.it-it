---
title: Visualizzare i dati di diagnostica
titleSuffix: Configuration Manager
description: È possibile visualizzare i dati di diagnostica e di utilizzo per verificare che la gerarchia di Configuration Manager non contenga informazioni riservate.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a11b5779eca41ed25a8e53e555f91b596452e51b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128570"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Come visualizzare i dati di diagnostica e utilizzo per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile visualizzare i dati di diagnostica e di utilizzo dalla gerarchia di Configuration Manager per verificare che non siano incluse informazioni sensibili o personali. Il sito riepiloga e archivia i dati di diagnostica nella tabella **TEL_TelemetryResults** del database del sito. Formatta i dati in modo che siano utilizzabili ed efficienti a livello di codice.

Le informazioni in questo articolo sono pensate come presentazione dei dati esatti inviati a Microsoft e non sono destinate all'uso per altri scopi, ad esempio l'analisi dei dati.  

## <a name="view-data-in-database"></a>Visualizzare i dati nel database

Usare il comando SQL seguente per visualizzare il contenuto di questa tabella e i dati esatti inviati:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Esportare i dati

Quando il punto di connessione del servizio è in modalità offline, usare lo strumento di connessione del servizio per esportare i dati correnti in un file con valori delimitati da virgole (CSV). Eseguire lo strumento di connessione del servizio per il punto di connessione del servizio con il parametro **-Export**.

Per altre informazioni, vedere [Usare lo strumento di connessione del servizio](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a> Hash unidirezionali

Alcuni dati sono costituiti da stringhe di caratteri alfanumerici casuali. Configuration Manager usa l'algoritmo SHA-256 per creare hash unidirezionali. Questo processo assicura che Microsoft non raccolga dati potenzialmente sensibili. I dati con hash possono comunque essere usati a scopo di correlazione e confronto.

Ad esempio, anziché raccogliere i nomi delle tabelle nel database del sito, viene acquisito l'hash unidirezionale per ogni nome di tabella. Questo comportamento assicura che eventuali nomi di tabella personalizzati non siano visibili. Microsoft esegue quindi lo stesso processo di hash unidirezionale dei nomi predefiniti delle tabelle SQL. Il confronto dei risultati delle due query determina la deviazione dello schema del database rispetto all'impostazione predefinita del prodotto. Queste informazioni possono poi essere usate per migliorare gli aggiornamenti che richiedono modifiche allo schema di SQL.  

Quando si visualizzano i dati non elaborati, viene visualizzato un valore con hash comune in ogni riga di dati. Questo hash è l'ID della gerarchia. Viene usato per correlare i dati alla stessa gerarchia senza identificare il cliente o l'origine.

### <a name="how-the-one-way-hash-works"></a>Come funziona l'hash unidirezionale

1. Ottenere l'ID gerarchia eseguendo la query SQL seguente in SQL Management Studio sul database di Configuration Manager:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Usare lo script di Windows PowerShell seguente per eseguire l'hash unidirezionale dell'ID gerarchia.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Confrontare l'output dello script con il GUID nei dati non elaborati. Questo processo mostra come vengono oscurati i dati.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Livelli dei dati di diagnostica e utilizzo](levels-overview.md)
