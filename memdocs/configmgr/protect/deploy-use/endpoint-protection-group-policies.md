---
title: Gestire Endpoint Protection tramite Criteri di gruppo
titleSuffix: Configuration Manager
description: Informazioni su come gestire Endpoint Protection tramite Criteri di gruppo.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c43ca9e1007c62835015a8c26a478af7da34ebb
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819993"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>Usare le impostazioni di Criteri di gruppo per gestire Endpoint Protection nelle versioni precedenti di Windows

**Si applica a:**

- [Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center Endpoint Protection nei dispositivi di livello inferiore seguenti:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

È possibile che sia disponibile un certo numero di dispositivi Windows di livello inferiore o legacy abilitati con Endpoint Protection, ma non inclusi nella gerarchia di Configuration Manager. Ad esempio, dispositivi in una rete perimetrale o dispositivi integrati in seguito a fusioni e acquisizioni. 

È possibile gestire Endpoint Protection in tali dispositivi usando le impostazioni di Criteri di gruppo descritte di seguito:

- [Copiare le definizioni dei criteri di Endpoint Protection](#copy-endpoint-protection-policy-definitions)
- Caricare le definizioni dei criteri di Endpoint Protection in una delle posizioni seguenti:
    - [Archivio centrale in un controller di dominio (scelta consigliata)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Dispositivo locale](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Per informazioni su come usare le impostazioni di Criteri di gruppo per gestire Microsoft Defender Antivirus in Windows 10, Windows Server 2019 e Windows Server 2016, vedere [Usare le impostazioni di Criteri di gruppo per configurare e gestire Microsoft Defender Antivirus](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## <a name="copy-endpoint-protection-policy-definitions"></a>Copiare le definizioni dei criteri di Endpoint Protection

In un dispositivo Windows di livello inferiore gestito da Endpoint Protection, copiare i file di definizione dei criteri di Endpoint Protection.

1. Passare a **C:\Programmi\Microsoft Security Client\Admx**. 

2. Comprimere i file seguenti in un file ZIP, ad esempio **SCEP_admx.zip**:
    - **EndPointProtection.adml**
    - **EndPointProtection.admx**
3. Copiare il file ZIP in una cartella temporanea. Ad esempio, **C:\temp_SCEP_GPO_admx**.
4. Estrai il file. 

> [!NOTE]
> Le chiavi del Registro di sistema per configurare le impostazioni dei criteri di Endpoint Protection si trovano in **Hkey_Local_Machine\Software\Policies\Microsoft\Microsoft Antimalware**.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Caricare le impostazioni di Criteri di gruppo di Endpoint Protection in un archivio centrale in un controller di dominio

Se si usa un [archivio centrale per i modelli amministrativi di Criteri di gruppo](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), seguire questa procedura per caricare e configurare le impostazione dei criteri di Endpoint Protection. Questo è il metodo consigliato.

1. Passare alla cartella in cui sono stati estratti i file di definizione dei criteri di Endpoint Protection.
2. Copiare i file con estensione admx e adml nella cartella **PolicyDefinitions** del controller di dominio:
    1. Copiare **EndPointProtection.admx** in **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions**. 
    2. Copiare **EndPointProtection.adml** in **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions\\it-IT**.  

    Ad esempio:
    
    - Copiare **EndPointProtection.admx** in **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Copiare **EndPointProtection.adml** in **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\it-IT**.
    
    dove **DC** è il nome del controller di dominio e **contoso.com** è il dominio.

3. Aprire la [Console Gestione Criteri di gruppo](https://docs.microsoft.com/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) e creare un nuovo oggetto Criteri di gruppo (GPO) nel dominio, ad esempio **Endpoint Protection**.
4. Fare clic con il pulsante destro del mouse sull'oggetto Criteri di gruppo per Endpoint Protection e quindi scegliere **Modifica**.
5. Nella Editor Gestione Criteri di gruppo passare a **Configurazione computer** > **Criteri**  > **Modelli amministrativi: Definizioni criteri** > **Componenti di Windows** > **Endpoint Protection**.

   Verrà visualizzato l'elenco dei Criteri di gruppo di Endpoint Protection.

6. Espandere la sezione che contiene l'impostazione da configurare, fare doppio clic sull'impostazione per aprirla e apportare le modifiche di configurazione.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Caricare le impostazioni di Criteri di gruppo di Endpoint Protection nel dispositivo locale

Anziché usare l'archivio centrale per il caricamento delle definizioni dei criteri di Endpoint Protection, è possibile archiviarle localmente nel dispositivo.

1. Passare alla cartella in cui sono stati estratti i file di definizione dei criteri di Endpoint Protection.
2. Copiare i file con estensione admx e adml nella cartella PolicyDefinitions locale.
    1. Copiare **EndPointProtection.admx** in **%SystemRoot%/PolicyDefinitions**. 
    2. Copiare **EndPointProtection.adml** in **%SystemRoot%/PolicyDefinitions/it-IT**.
    
    Ad esempio:

    - Copiare **EndPointProtection.admx** in **C:\Windows\PolicyDefinitions**.
    - Copiare **EndPointProtection.adml** in **C:\Windows\PolicyDefinitions\it-IT**.
    
3. Aprire l'Editor Criteri di gruppo locali.
4. Passare a **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Endpoint Protection**.

    Verrà visualizzato l'elenco dei Criteri di gruppo di Endpoint Protection.

5. Espandere la sezione che contiene l'impostazione da configurare, fare doppio clic sull'impostazione per aprirla e apportare le modifiche di configurazione.

## <a name="next-steps"></a>Passaggi successivi
- Per una panoramica di Endpoint Protection, vedere [Endpoint Protection](endpoint-protection.md).
- Per informazioni sulla configurazione manuale di Endpoint Protection in un client autonomo, vedere [Configurare Endpoint Protection in un client autonomo](endpoint-protection-configure-standalone-client.md).
