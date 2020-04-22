---
title: Personalizzare Support Center
titleSuffix: Configuration Manager
description: Personalizzare il file di configurazione di Support Center.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1436f40dc989202725d7b83d551d318b970f9b5d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707439"
---
# <a name="customize-support-center"></a>Personalizzare Support Center

*Si applica a: Configuration Manager (Current Branch)*

[Support Center](support-center.md) è uno strumento che include un file di configurazione personalizzabile. Per impostazione predefinita, durante l'installazione di Support Center, questo file si trova nel percorso seguente: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. Il file di configurazione modifica il comportamento del programma:

- [Personalizzare la raccolta dati](#bkmk_datacoll): è possibile modificare i set di chiavi del Registro di sistema e gli spazi dei nomi WMI che vengono inclusi durante la raccolta dati  

- [Personalizzare i gruppi di file di log](#bkmk_loggroups): è possibile definire nuovi gruppi di file di log usando espressioni regolari. È anche possibile aggiungere altri file di log ai gruppi.  

- [Raccolta di file di log aggiuntivi tramite i caratteri jolly](#bkmk_wildcards): è possibile usare le ricerche con caratteri jolly per raccogliere file di log aggiuntivi  

Per apportare queste modifiche è necessario disporre di autorizzazioni di amministratore nel client in cui è installato Support Center. Per eseguire questi tipi di personalizzazione, usare un editor di testo o un editor XML, ad esempio Notepad o Visual Studio.

> [!Important]  
> Il file di configurazione di Support Center è un file in formato XML. È essenziale per il funzionamento di Support Center. La modifica di questo file è consigliata solo agli utenti che hanno familiarità con XML e le espressioni regolari.  

Prima di personalizzare il file di configurazione di Support Center, salvare una copia di backup del file originale. In questo modo sarà possibile ripristinare le funzionalità originali di Support Center se si commettono errori durante la modifica del file. Se non si crea una copia di backup e Support Center non funziona correttamente dopo aver modificato il file di configurazione, reinstallare Support Center. È anche possibile copiare un file di configurazione da un'altra installazione di Support Center.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a> Personalizzare la raccolta dati

Per personalizzare la raccolta dati nel client, modificare il file di configurazione di Support Center usando gli elementi XML contenuti nell'elemento `<dataCollectorSettings>`.


### <a name="wmi-data-collection"></a>Raccolta dati WMI

L'elemento `<CcmWmiDataCollector>` contiene un elemento `<collectionScopes>`. Usare questo elemento per modificare gli spazi dei nomi WMI da cui Support Center raccoglie i dati. Include anche un elemento `<ignoreScopes>`. Usare questo elemento per filtrare la raccolta dati da parti degli spazi dei nomi definiti nell'elemento `<collectionScopes>`.  
    
#### <a name="example"></a>Esempio
Il file di configurazione raccoglie i dati dallo spazio dei nomi `root\ccm`. Include questo percorso in `<add/>` in un elemento `<collectionScopes>`. 

Ignora anche tutto quello che è incluso nei percorsi `\cimodels`, `\invagt`,  `\events` e `\policy` per questo spazio dei nomi. Include questi percorsi negli elementi `<add/>` contenuti in `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Raccolta dati del Registro di sistema

L'elemento `<RegistryDataCollector>` contiene un elemento `<registryKeys>`. Usare questo elemento per modificare le chiavi e le sottochiavi del Registro di sistema che Support Center raccoglie nel percorso `HKEY_LOCAL_MACHINE`. Support Center non supporta la raccolta dati del Registro di sistema da altri percorsi del Registro di sistema radice.

#### <a name="example"></a>Esempio
Per raccogliere le chiavi del Registro di sistema per i programmi classici installati nel dispositivo, aggiungere l'elemento `<add/>` seguente nell'elemento `<registryKeys>`: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a> Personalizzare i gruppi di file di log

Per personalizzare i file di log che Support Center raccoglie e la rispettiva visualizzazione nell'elenco **Log groups** (Gruppi di log), usare gli elementi contenuti nell'elemento `<logGroups>`. Quando si avvia Support Center, lo strumento analizza questa sezione del file di configurazione. Poi crea un gruppo nell'elenco **Log groups** (Gruppi di log) per ogni valore dell'attributo chiave trovato negli elementi `<add/>` contenuti nell'elemento `<logGroups>`.

- **Component log group** (Gruppo di log componente): l'elemento `<componentLogGroup>` usa un attributo chiave per definire il nome del gruppo di log visualizzato nell'elenco. Usa anche un valore dell'attributo che contiene un'espressione regolare (regex). Usa questa espressione regolare per raccogliere un set di file di log correlati.  

- **Static log group:** (Gruppo di log statico) l'elemento `<staticLogGroup>` usa un attributo chiave per definire il nome del gruppo di log visualizzato nell'elenco. Usa anche un valore dell'attributo che definisce il nome di un file di log.  

Se lo stesso valore dell'attributo chiave viene usato in un elemento `<add/>` sia nell'elemento `<componentLogGroup>` che nell'elemento `<staticLogGroup>`, Support Center crea un singolo gruppo. Questo gruppo include i file di log definiti da entrambi gli elementi che usano la stessa chiave.

#### <a name="example"></a>Esempio
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a> Raccolta di file di log aggiuntivi tramite i caratteri jolly

Per raccogliere file di log aggiuntivi, usare i caratteri jolly nel percorso di file o nel nome file. Questi caratteri jolly includono variabili di ambiente a livello di sistema, ad esempio `%WINDIR%`, ma escludono le variabili di ambiente con ambito di utente, ad esempio `%USERPROFILE%`. Per raccogliere file di log aggiuntivi con questa ricerca di file di log non ricorsiva, usare un elemento `<add/>` nell'elemento `<additionalLogFiles>`. 

Questi esempi illustrano come Support Center usa questa funzionalità nel file di configurazione predefinito.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Esempio 1: raccogliere tutti i file di log di Windows Update nella directory di Windows
L'elemento seguente raccoglie tutti i file denominati `WindowsUpdate.log`, contenuti nella directory di Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Esempio 2: raccogliere tutti i file di log nella directory dei log di Windows
L'elemento seguente raccoglie tutti i file che terminano con `.log`, contenuti nella directory Registri di Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Esempio XML completo
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
