---
title: Crea supporto per sequenza di attività
titleSuffix: Configuration Manager
description: È possibile creare supporti per sequenza di attività per distribuire un sistema operativo in un computer di destinazione nell'ambiente di Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf7ce32ed9e126b5526c68b7da03cf44d9b5062d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125169"
---
# <a name="create-task-sequence-media"></a>Crea supporto per sequenza di attività

*Si applica a: Configuration Manager (Current Branch)*

Si possono usare supporti per acquisire un'immagine del sistema operativo da un computer di riferimento o per distribuire un sistema operativo in un computer di destinazione nell'ambiente di Configuration Manager. Il supporto creato può essere un set di CD/DVD o un'unità flash USB.

In genere, il supporto viene usato per distribuire sistemi operativi nei computer che non dispongono di una connessione di rete o la cui connessione di rete al sito ha larghezza di banda bassa. Tuttavia, è possibile usare i supporti per avviare una distribuzione del sistema operativo all'esterno di un sistema operativo Windows esistente. Questo metodo è utile quando non esiste un sistema operativo, il sistema operativo non funziona o si vuole ripartire il disco rigido.Questo metodo è utile quando non esiste un sistema operativo, il sistema operativo non funziona o si vuole ripartire il disco.

I supporti di distribuzione includono supporti di avvio, supporti autonomi e supporti pre-installati. Il contenuto dei supporti varia a seconda del tipo di supporto usato. Ad esempio, un supporto autonomo contiene la sequenza di attività che distribuisce il sistema operativo. Altri tipi di supporto recuperano le sequenze di attività dal punto di gestione.

> [!IMPORTANT]
> Per creare un supporto per una sequenza di attività è necessario essere un amministratore del computer in cui si esegue la console di Configuration Manager. Se non si è un amministratore, verranno richieste le credenziali di amministratore quando si avvia la Creazione guidata del supporto per la sequenza di attività.

## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> Supporto di acquisizione

Il supporto di acquisizione consente di acquisire un'immagine del sistema operativo da un computer di riferimento. Contiene l'immagine d'avvio che avvia il computer di riferimento e la sequenza di attività che acquisisce l'immagine del sistema operativo.

## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> Supporto di avvio

Un supporto di avvio contiene i componenti seguenti:

- L'immagine d'avvio
- [Comandi di preavvio](../understand/prestart-commands-for-task-sequence-media.md) facoltativi e i relativi file obbligatori
- File binari di Configuration Manager

All'avvio il computer di destinazione si connette alla rete e recupera la sequenza di attività, l'immagine del sistema operativo e tutti gli altri contenuti richiesti dalla rete. Poiché la sequenza di attività non è presente nel supporto, è possibile modificare la sequenza di attività o il contenuto senza dover ricreare il supporto.  

> [!IMPORTANT]  
> I pacchetti nei supporti di avvio non sono crittografati. Adottare le misure di sicurezza appropriate, ad esempio l'aggiunta di una password al supporto, per garantire che il contenuto del pacchetto sia protetto da utenti non autorizzati.  

A partire dalla versione 2006, il supporto di avvio può scaricare contenuto basato sul cloud. Il dispositivo necessita tuttavia di una connessione Intranet al punto di gestione. Può ottenere contenuto da un gateway di gestione cloud (CMG) o da un punto di distribuzione cloud abilitati per il contenuto.<!--6209223--> Per altre informazioni, vedere [Supporto per contenuto basato sul cloud](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> Supporto pre-installato

Il supporto pre-installato consente di applicare i supporti di avvio e un'immagine del sistema operativo in un disco rigido prima del processo di provisioning. È un file di immagine (WIM) di Windows, Il produttore può installarlo nel computer bare metal durante il processo di compilazione. In alternativa, può essere usato in un centro di gestione temporanea non connesso all'ambiente di produzione di Configuration Manager.

I supporti pre-installati contengono l'immagine d'avvio usata per avviare il computer di destinazione e l'immagine del sistema operativo applicata al computer di destinazione. È anche possibile specificare applicazioni, pacchetti e pacchetti driver da includere come parte del supporto pre-installato. La sequenza di attività che distribuisce il sistema operativo non è inclusa nel supporto. Quando si distribuisce una sequenza di attività che usa supporti pre-installati, il client cerca prima di tutto contenuto valido nella cache della sequenza di attività locale. Se il contenuto non viene trovato o è stato rivisto, il client scarica il contenuto da un punto di distribuzione o da un peer.  

Il supporto pre-installato viene applicato al disco rigido di un nuovo computer prima che il computer venga inviato all'utente finale. Quando il computer viene avviato per la prima volta dopo aver applicato i supporti pre-installati, il computer viene avviato in Windows PE. Si connette a un punto di gestione per individuare la sequenza di attività che completa il processo di distribuzione del sistema operativo.  

> [!IMPORTANT]
> I pacchetti nei supporti pre-installati non sono crittografati. Adottare le misure di sicurezza appropriate, ad esempio l'aggiunta di una password al supporto, per garantire che il contenuto del pacchetto sia protetto da utenti non autorizzati.

## <a name="standalone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Supporti autonomi

Il supporto autonomo contiene tutti gli elementi necessari per distribuire il sistema operativo. Il contenuto include anche la sequenza di attività e altri elementi necessari. Poiché tutto si trova sul supporto, lo spazio su disco richiesto è maggiore di quello di altri tipi di supporti.

## <a name="considerations-when-using-https"></a>Considerazioni sull'uso di HTTPS

Quando si configurano i punti di gestione e i punti di distribuzione per l'uso di HTTPS, creare un supporto di avvio e un supporto pre-installato in un sito primario e non nel sito di amministrazione centrale. Inoltre, tenere presente quanto segue per stabilire se sia necessario configurare il supporto come dinamico o basato su sito:  

- Per configurare il supporto come dinamico, per tutti i siti primari deve essere disponibile un'autorità di certificazione principale (CA) del sito da cui è stato creato il supporto. È possibile importare la CA radice in tutti i siti primari della gerarchia.  

- Quando i siti primari presenti nella gerarchia di Configuration Manager usano CA radice diverse è necessario usare un supporto basato su sito in ognuno di essi.  

## <a name="next-steps"></a>Passaggi successivi

- [Creare supporti di acquisizione](create-capture-media.md)

- [Creare supporti di avvio](create-bootable-media.md)

- [Creare supporti pre-installati](create-prestaged-media.md)

- [Creare supporti autonomi](create-stand-alone-media.md)
