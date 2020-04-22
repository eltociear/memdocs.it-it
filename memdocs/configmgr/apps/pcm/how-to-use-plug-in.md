---
title: Come usare il plug-in di conversione
titleSuffix: Configuration Manager
description: Usare il plug-in Package Conversion Manager per personalizzare i processi di analisi e conversione.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688959"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Come usare il plug-in Package Conversion Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357861-->

Il plug-in Package Conversion Manager consente di personalizzare i processi di analisi e conversione. Per usare il plug-in Package Conversion Manager, scrivere un file di script o eseguibile che effettua operazioni personalizzate. Modificare quindi il file di configurazione, Microsoft.ConfigurationManagement.exe.config, per chiamare il file di script o eseguibile. I linguaggi più comuni usati per scrivere lo script sono VBScript o PowerShell.

Il plug-in Package Conversion Manager viene eseguito una volta per ogni pacchetto. Se si analizzano o si convertono più pacchetti contemporaneamente, il plug-in Package Conversion Manager viene eseguito più volte.

> [!NOTE]  
> Per altre informazioni sugli elementi di Package Conversion Manager nel file di configurazione di Configuration Manager, vedere [Informazioni tecniche sul codice XML di configurazione del plug-in Package Conversion Manager](plugin-config-xml.md).



## <a name="default-process"></a>Processo predefinito

Per impostazione predefinita, Package Conversion Manager esegue le operazioni seguenti:

1.  Lettura di un pacchetto di Configuration Manager.  

2.  Creazione di un'applicazione dal pacchetto e aggiunta di attributi predefiniti.  

3.  Analisi dell'applicazione e determinazione dello stato di conformità del pacchetto.  

4.  Scegliere una delle operazioni seguenti, a seconda dell'operazione di Package Conversion Manager:  

    - **Analizza**: viene visualizzato lo stato di conformità del pacchetto nella console di Configuration Manager.  

    - **Converti**: l'applicazione viene scritta nel database di Configuration Manager.  


## <a name="plug-in-based-process"></a>Processo basato sul plug-in 

Quando si usa il plug-in, Package Conversion Manager esegue le operazioni seguenti:

1.  Lettura di un pacchetto di Configuration Manager.  

2.  Creazione di un'applicazione dal pacchetto e aggiunta di attributi predefiniti.  

3.  Conversione dell'applicazione in formato XML. Salvataggio del file su disco.  

4.  Esecuzione dello script del plug-in per modificare il codice XML dell'applicazione. Per altre informazioni, vedere [Informazioni tecniche sul codice XML di configurazione del plug-in Package Conversion Manager](plugin-config-xml.md).  

5.  Conversione del codice XML dell'applicazione in un'applicazione di Configuration Manager.  

6.  Analisi dell'applicazione e determinazione dello stato di conformità del pacchetto.  

7.  Scegliere una delle operazioni seguenti, a seconda dell'operazione di Package Conversion Manager:  

    - **Analizza**: viene visualizzato lo stato di conformità del pacchetto nella console di Configuration Manager.  

    - **Converti**: l'applicazione viene scritta nel database di Configuration Manager.  



## <a name="see-also"></a>Vedere anche

[Informazioni tecniche sul codice XML di configurazione del plug-in Package Conversion Manager](plugin-config-xml.md)
