---
title: Codice XML di configurazione del plug-in
titleSuffix: Configuration Manager
description: Informazioni tecniche relative agli elementi XML del plug-in Package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ced1cc1347167451d4efb789b40746ff849710ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689079"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Informazioni tecniche sul codice XML di configurazione del plug-in Package Conversion Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357861-->

Questo articolo descrive gli elementi XML del file di configurazione di Configuration Manager (Microsoft.ConfigurationManagement.exe.config) che controllano il funzionamento del plug-in Package Conversion Manager. Per altre informazioni su come usare il plug-in, vedere [Come usare il plug-in Package Conversion Manager](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>Elementi di configurazione XML

La tabella seguente descrive gli elementi XML nel file di configurazione di Configuration Manager correlati al plug-in Package Conversion Manager.

|Elemento  |Tipo  |Descrizione  |
|---------|---------|---------|
|**PcmPlugIn**|Stringa|Nome dello script o del file eseguibile da usare come plug-in Package Conversion Manager.|
|**PcmPlugInTimeoutMilliseconds**|Intero|Quantità massima di tempo, espressa in millisecondi, di attesa affinché lo script o il file eseguibile del plug-in Package Conversion Manager completi l'elaborazione di un pacchetto.|
|**PcmPluginExitCode**|Intero|Il codice di uscita previsto dal processo di plug-in. Questo valore indica esito positivo. Tutti gli altri codici sono considerati un errore.|
|**ForceRequirementsExtraction**|Boolean|Consente alla conversione automatica di usare i requisiti di raccolta associati a un pacchetto. Questo elemento deve essere impostato su True solo quando si usa un plug-in Package Conversion Manager progettato per prendere decisioni sui requisiti da usare.|



## <a name="sample-configuration-xml"></a>File XML di configurazione di esempio

Questa sezione fornisce un esempio degli elementi XML di configurazione di Package Conversion Manager nel file di configurazione di Configuration Manager, **Microsoft.ConfigurationManagement.exe.config**. Per impostazione predefinita, questo file si trova nel percorso seguente:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

Nell'esempio gli elementi correlati a Package Conversion Manager sono all'interno dell'elemento seguente: `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

