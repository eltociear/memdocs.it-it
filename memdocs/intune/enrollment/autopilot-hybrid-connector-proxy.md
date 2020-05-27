---
title: Configurare le impostazioni proxy per il connettore di Intune per Active Directory
description: Viene illustrato come configurare il connettore di Intune per Active Directory per l'uso dei server proxy locali esistenti.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: b26bf4910e6745a60634a2b313a37beeb33192d3
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986907"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Usare i server proxy locali esistenti

Questo articolo illustra come configurare il connettore di Intune per Active Directory per l'uso dei server proxy in uscita. L'articolo è destinato ai clienti con ambienti di rete in cui sono presenti proxy.

Per impostazione predefinita, il connettore di Intune per Active Directory tenta di individuare automaticamente un server proxy nella rete usando il protocollo WPAD (Web Proxy Auto-Discovery). Se questo è stato configurato nella rete, è possibile che non siano necessarie altre operazioni di configurazione.  Se sono necessarie modifiche, le sezioni seguenti descrivono come eseguire l'override delle impostazioni predefinite, sfruttando [le funzionalità di .NET Framework standard per la configurazione delle impostazioni proxy](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  In tale documentazione sono descritte opzioni aggiuntive.

Per altre informazioni sul funzionamento dei connettori, vedere [Informazioni sui connettori di Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors).

## <a name="completely-bypass-outbound-proxies"></a>Ignorare completamente i proxy in uscita

È possibile configurare il connettore in modo che ignori il proxy locale, per garantire che usi la connettività diretta ai servizi di Azure. Se consentito dai criteri di rete, questo approccio è consigliato, perché implica una configurazione in meno da gestire.

Per disabilitare l'uso del proxy in uscita per il connettore, modificare il file C:\Programmi\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config e aggiungere l'indirizzo e la porta del proxy nella sezione indicata nell'esempio di codice seguente:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Per assicurarsi che anche il servizio Connector Updater ignori il proxy, apportare una modifica simile al file C:\Programmi\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Assicurarsi di creare copie dei file originali nel caso sia necessario ripristinare i file config predefiniti.

Dopo che i file di configurazione sono stati modificati, è necessario riavviare il servizio connettore di Intune. 

1. Aprire **services.msc**.
2. Individuare e selezionare **Servizio Connettore ODJ di Intune**.
3. Selezionare **Riavvia**.

![Screenshot del riavvio del servizio](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Indicazione di un server proxy alternativo

Se è necessario usare un server proxy diverso (ad esempio, un server proxy che ignora l'autenticazione) con il connettore di Intune per Active Directory, è possibile specificarlo in un modo simile. A tale scopo, modificare il file C:\Programmi\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config e aggiungere l'indirizzo e la porta del proxy nella sezione indicata nell'esempio di codice seguente:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Per assicurarsi che anche il servizio Connector Updater ignori il proxy, apportare una modifica simile al file C:\Programmi\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Assicurarsi di creare copie dei file originali nel caso sia necessario ripristinare i file config predefiniti.

Dopo che i file di configurazione sono stati modificati, è necessario riavviare il servizio connettore di Intune. 

1. Aprire **services.msc**.
2. Individuare e selezionare **Servizio Connettore ODJ di Intune**.
3. Selezionare **Riavvia**.

![Screenshot del riavvio del servizio](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Passaggi successivi

[Gestire i dispositivi](../remote-actions/device-management.md)
