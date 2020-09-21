---
title: Preparare un'app Win32 da caricare in Microsoft Intune
titleSuffix: ''
description: Informazioni su come preparare un'app Win32 da caricare in Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94626b6cc7e9586ff6b9230206c3e57e6b01b86f
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083798"
---
# <a name="prepare-win32-app-content-for-upload"></a>Preparare il contenuto delle app Win32 per il caricamento

Prima di poter aggiungere un'app Win32 a Microsoft Intune, è necessario preparare l'app usando lo [Strumento di preparazione di contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730).

## <a name="prerequisites"></a>Prerequisiti

Per usare la gestione delle app Win32, assicurarsi che siano soddisfatti i criteri seguenti:

- Usare Windows 10 versione 1607 o successive (edizioni Enterprise, Pro ed Education).
- I dispositivi devono essere stati aggiunti ad Azure Active Directory (Azure AD) e registrati automaticamente. L'estensione di gestione di Intune supporta i dispositivi aggiunti ad Azure AD, aggiunti al dominio ibrido e registrati con Criteri di gruppo. 
  > [!NOTE]
  > Per lo scenario di registrazione con Criteri di gruppo, l'utente usa l'account utente locale per aggiungere ad Azure AD il proprio dispositivo Windows 10. L'utente deve accedere al dispositivo usando il proprio account utente Azure AD e registrarsi in Intune. Intune installerà l'estensione di gestione di Intune nel dispositivo se c'è uno script di PowerShell o un'app Win32 destinato all'utente o al dispositivo.
- Le applicazioni Windows possono avere dimensioni massime di 8 GB.

## <a name="convert-the-win32-app-content"></a>Convertire il contenuto dell'app Win32

Usare lo [Strumento di preparazione di contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) per eseguire l'analisi preliminare delle app di Windows classiche (Win32). Lo strumento converte i file di installazione delle applicazioni nel formato *intunewin*. Lo strumento rileva anche alcuni attributi richiesti da Intune per determinare lo stato di installazione delle applicazioni. Dopo aver usato questo strumento nella cartella di installazione delle app, sarà possibile creare un'app Win32 nella console di Intune.

> [!IMPORTANT]
> Lo [strumento Microsoft di preparazione dei contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) comprime tutti i file e le sottocartelle quando crea il file con estensione *intunewin*. Assicurarsi di mantenere lo strumento Microsoft di preparazione dei contenuti Win32 separato da file e cartelle del programma di installazione, in modo da non includere lo strumento o altri file o cartelle non necessari nel file con estensione *intunewin*.

È possibile scaricare lo [Strumento di preparazione di contenuti Win32](https://go.microsoft.com/fwlink/?linkid=2065730) da GitHub come file ZIP. Il file compresso contiene una cartella denominata *Microsoft-Win32-Content-Prep-Tool-master*. La cartella contiene lo strumento di preparazione, la licenza, un file leggimi e le note sulla versione. 

### <a name="process-flow-to-create-a-intunewin-file"></a>Flusso del processo per la creazione di un file con estensione intunewin

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="running-the-microsoft-win32-content-prep-tool"></a>Esecuzione dello Strumento di preparazione di contenuti Win32

Se si esegue `IntuneWinAppUtil.exe` dalla finestra di comando senza parametri, lo strumento guiderà l'utente nell'immissione dei parametri necessari. In alternativa, è possibile aggiungere i parametri al comando facendo riferimento ai seguenti parametri della riga di comando disponibili.

### <a name="available-command-line-parameters"></a>Parametri della riga di comando disponibili 

|    **Parametro della riga di comando**    |    **Descrizione**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Help    |
|    `-c <setup_folder>`     |    Cartella per tutti i file di installazione. Tutti i file in questa cartella verranno compressi in un file con estensione *intunewin*.    |
|    `-s <setup_file>`     |    File di installazione (ad esempio, *setup.exe* o *setup.msi*).    |
|    `-o <output_folder>`     |    Cartella di output per il file con estensione *intunewin* generato.    |
|    `-q`       |    Modalità non interattiva.    |

### <a name="example-commands"></a>Comandi di esempio

|    **Comando di esempio**    |    **Descrizione**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    Questo comando mostrerà le informazioni di utilizzo per lo strumento.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Questo comando genererà il file con estensione  *intunewin* dalla cartella di origine e dal file di installazione specificati. Per il file di installazione MSI, questo strumento recupererà le informazioni necessarie per Intune. Se viene specificato `-q`, il comando verrà eseguito in modalità non interattiva. Se il file di output esiste già, verrà sovrascritto. Se la cartella di output non esiste, verrà creata automaticamente.    |

Durante la generazione di un file con estensione *intunewin*, inserire gli eventuali file a cui è necessario fare riferimento in una sottocartella della cartella di installazione. Usare quindi un percorso relativo per fare riferimento al file specifico necessario. Ad esempio:

**Cartella di origine dell'installazione:** *c:\testapp\v1.0*<br>
**File di licenza:** *c:\testapp\v1.0\licenses\license.txt*

Fare riferimento al file *license.txt* usando il percorso relativo *licenses\license.txt*.

## <a name="next-steps"></a>Passaggi successivi

- [Aggiungere app Win32 a Microsoft Intune](apps-win32-add.md)
