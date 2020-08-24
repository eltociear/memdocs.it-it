---
title: Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale
titleSuffix: Configuration Manager
description: Usare distribuzioni con supporti pre-installati per ridurre il traffico di rete durante la distribuzione di un sistema operativo in un computer di cui non è stato effettuato il provisioning completo.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125441"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le distribuzioni con supporti pre-installati in Configuration Manager consentono di distribuire un sistema operativo in un computer di cui non è stato effettuato il provisioning completo. Il supporto pre-installato è un file Windows Imaging Format (WIM), che può essere installato in un computer bare metal dal produttore o che può essere usato in un centro di gestione temporanea separato dall'ambiente di produzione.

Questo metodo di distribuzione può ridurre il traffico di rete perché l'immagine d'avvio e l'immagine del sistema operativo sono già nel computer di destinazione. È possibile specificare applicazioni, pacchetti e pacchetti driver da includere nel supporto pre-installato. Dopo aver installato il sistema operativo nel computer, la sequenza di attività verifica innanzitutto la cache pre-installata per le applicazioni, i pacchetti o i pacchetti driver. Se non riesce a trovare il contenuto necessario o se è disponibile una revisione più recente online, la sequenza di attività scarica il contenuto da un punto di distribuzione.

Usare i supporti pre-installati negli scenari di distribuzione del sistema operativo seguenti:

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)

Completare i passaggi in uno di questi scenari di distribuzione del sistema operativo. Usare quindi le sezioni seguenti per preparare e creare il supporto pre-installato.

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione

Nella pagina **Impostazioni distribuzione** della distribuzione, per l'impostazione **Rendi disponibile per**, selezionare una delle opzioni seguenti:

- Client di Configuration Manager, supporti e PXE

- Solo supporti e PXE

- Solo supporti e PXE (nascosto)

## <a name="create-the-prestaged-media"></a>Creare supporti pre-installati

Creare il file del supporto pre-installato da inviare all'OEM o al rivenditore locale. Per altre informazioni, vedere [Creare supporti pre-installati con Configuration Manager](create-prestaged-media.md).

## <a name="send-the-prestaged-media-file"></a>Inviare il file dei supporti pre-installati

Inviare i supporti all'OEM o al rivenditore locale per pre-installarli nel computer. Il file di immagine viene applicato a un disco rigido formattato nel computer.

## <a name="deliver-the-computer"></a>Distribuire il computer

Quando si distribuisce il computer a un utente e lo si attiva per la prima volta:

1. Il computer si avvia con l'immagine d'avvio pre-installata.

1. Controlla un hash nel supporto pre-installato per assicurarsi che sia valido.

1. Il computer si connette al punto di gestione per le sequenze di attività disponibili per completare il processo.

## <a name="next-steps"></a>Passaggi successivi

[Esperienze utente per la distribuzione del sistema operativo](../understand/user-experience.md)
