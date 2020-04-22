---
title: Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale
titleSuffix: Configuration Manager
description: Usare distribuzioni con supporti pre-installati per ridurre il traffico di rete durante la distribuzione di un sistema operativo in un computer di cui non è stato effettuato il provisioning completo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707289"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le distribuzioni con supporti pre-installati in Configuration Manager consentono di distribuire un sistema operativo in un computer di cui non è stato effettuato il provisioning completo. Il supporto preinstallato è un file WIM (Windows Imaging Format) che può essere installato in un computer bare metal dal produttore (OEM) o in un centro di gestione temporanea aziendale non connesso all'ambiente di Configuration Manager. Successivamente, nell'ambiente di Configuration Manager il computer viene avviato usando l'immagine d'avvio fornita dal supporto, viene eseguito un controllo hash nel supporto pre-installato per verificare che sia valido e quindi il computer si connette al punto di gestione del sito per le sequenze di attività disponibili che completano il processo di download.


Questo metodo di distribuzione può ridurre il traffico di rete perché l'immagine di avvio e l'immagine del sistema operativo sono già nel computer di destinazione. È possibile specificare applicazioni, pacchetti e pacchetti driver da includere nel supporto pre-installato. Dopo l'installazione del sistema operativo nel computer, vengono innanzitutto ricercati nella cache della sequenza di attività applicazioni, pacchetti o pacchetti di driver. Se il contenuto non viene trovato o è stato modificato, viene scaricato da un punto di distribuzione configurato nei supporti preinstallati e quindi installato.  

 È possibile usare i supporti pre-installati negli scenari di distribuzione del sistema operativo seguenti:  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)  

  Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi usare le sezioni seguenti per preparare e creare il supporto pre-installato.  

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione  
 Quando si usa un supporto pre-installato per avviare il processo di distribuzione del sistema operativo, è necessario configurare la distribuzione per rendere disponibile il sistema operativo per il supporto. È possibile eseguire questa configurazione nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione.  Per l'impostazione **Rendi disponibile per** , configurare uno degli elementi seguenti:  

-   **Client di Configuration Manager, supporti e PXE**  

-   **Solo supporti e PXE**  

-   **Solo supporti e PXE (nascosto)**  

## <a name="create-the-prestaged-media"></a>Creare supporti pre-installati  
 Creare il file del supporto pre-installato da inviare all'OEM o al rivenditore locale. Per altre informazioni, vedere [Creare supporti pre-installati con Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Inviare il file del supporto pre-installato all'OEM o al rivenditore locale  
 Inviare i supporti all'OEM o al rivenditore locale per pre-installare i computer. Il file del supporto pre-installato viene applicato a un disco rigido formattato nel computer.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Avviare il computer per installare il sistema operativo  
 Il file del supporto pre-installato viene applicato ai computer. Quando il computer viene avviato per la prima volta, viene avviato il processo di installazione del sistema operativo.  
