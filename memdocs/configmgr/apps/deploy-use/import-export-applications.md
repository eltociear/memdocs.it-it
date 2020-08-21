---
title: Importare ed esportare le applicazioni
titleSuffix: Configuration Manager
description: Informazioni su come importare ed esportare le applicazioni in Configuration Manager per la condivisione tra gerarchie diverse.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3db127deb353f30566a1f03cbc6ac0eef666cb37
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695257"
---
# <a name="import-and-export-applications"></a>Importare ed esportare le applicazioni

*Si applica a: Configuration Manager (Current Branch)*

Usare Configuration Manager per importare ed esportare applicazioni tra due gerarchie. Ad esempio è possibile copiare un'applicazione da un ambiente di test a un ambiente di produzione.

## <a name="export"></a>Export

1. Nella console di Configuration Manager selezionare il nodo **Applicazioni**. Nel gruppo Crea della barra multifunzione scegliere **Esporta applicazione**.
1. Nella schermata **Generale** immettere il percorso di un nuovo file con estensione zip nel quale eseguire l'esportazione. Facoltativamente specificare se esportare *dipendenze, relazioni di sostituzione, condizioni e ambienti virtuali*, nonché *contenuto per le applicazioni selezionate e le dipendenze*.  Immettere eventuali commenti dell'amministratore e quindi selezionare **Avanti**.
1. Verificare che l'applicazione e tutte le dipendenze siano elencate nella pagina **Oggetti correlati** e selezionare **Avanti**.
1. Nella pagina Riepilogo selezionare **Avanti**.
1. Dopo il completamento del processo viene creato il file con estensione zip ed è possibile chiudere la procedura guidata.

> [!IMPORTANT]
> Se si vuole copiare questa applicazione in un altro ambiente, copiare sia il file con estensione zip sia la cartella associata. Il file con estensione zip deve essere presente nella stessa directory in cui si trova la cartella creata.

## <a name="import"></a>Importa

> [!NOTE]
> È possibile importare applicazioni solo da percorsi UNC, non è possibile importarle direttamente dal disco locale.

1. Nella console di Configuration Manager selezionare il nodo **Applicazioni**. Nel gruppo Crea della barra multifunzione scegliere **Importa applicazione**.
1. Scegliere il file con estensione zip che si vuole importare e quindi selezionare **Avanti**.
1. La finestra Contenuto file visualizza cosa accade quando si importa l'applicazione. Selezionare **Avanti**.
1. Esaminare la schermata di riepilogo e selezionare **Avanti**.
1. Chiudere la procedura guidata. L'applicazione è ora disponibile nel sito.

## <a name="see-also"></a>Vedere anche
 
Automatizzare l'importazione e l' esportazione di applicazioni tramite PowerShell.

* [Import-CMApplication](/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](/powershell/module/configurationmanager/export-cmapplication)