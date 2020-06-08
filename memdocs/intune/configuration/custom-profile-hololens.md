---
title: Usare il Controllo applicazioni di Windows Defender nei dispositivi HoloLens 2 in Microsoft Intune - Azure | Microsoft Docs
description: Configurare il CSP di Controllo applicazioni di Windows Defender (WDAC) per consentire o bloccare l'apertura delle app nei dispositivi HoloLens 2 in Microsoft Intune. Usare PowerShell e un profilo di configurazione personalizzato.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990135"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Usare WDAC e Windows PowerShell per consentire o bloccare le app nei dispositivi HoloLens 2 con Microsoft Intune

I dispositivi Microsoft HoloLens 2 supportano il [CSP di Controllo applicazioni di Windows Defender (WDAC)](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp), che sostituisce il [CSP di AppLocker](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).

Usando Windows PowerShell e Microsoft Intune, è possibile usare il CSP di WDAC per consentire o bloccare l'apertura di app specifiche nei dispositivi Microsoft HoloLens 2. Ad esempio, è possibile consentire o impedire l'apertura dell'app Cortana nei dispositivi HoloLens 2 dell'organizzazione.

Questa funzionalità si applica a:

- Dispositivi HoloLens 2 che eseguono Windows Holographic for Business

Il CSP di WDAC è basato sulla [funzionalità Controllo applicazioni di Windows Defender (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). È anche possibile [usare più criteri di WDAC](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

Questo articolo illustra come:

1. Usare Windows PowerShell per creare criteri di WDAC.
2. Usare Windows PowerShell per convertire le regole del criterio di WDAC in XML, aggiornare il file XML e convertirlo in un file binario.
3. In Microsoft Intune creare un [profilo di configurazione del dispositivo personalizzato](custom-settings-windows-holographic.md), aggiungere il file binario con il criterio di WDAC e applicare il criterio ai dispositivi HoloLens 2.

In Intune è necessario creare un profilo di configurazione personalizzato per usare il CSP di Controllo applicazioni di Windows Defender (WDAC). 

Usare la procedura descritta in questo articolo come modello per consentire o negare l'apertura di app specifiche nei dispositivi HoloLens 2.

## <a name="prerequisites"></a>Prerequisiti

- Acquisire familiarità con Windows PowerShell.
- Accedere a Intune come membro di:

  - ruoli di Intune **Gestione criteri e profili** o **Amministratore dei ruoli di Intune**

    OPPURE

  - ruoli di Azure AD **Amministratore globale** o **Amministratore del servizio Intune**

  [Controllo degli accessi in base al ruolo (RBAC) con Microsoft Intune](../fundamentals/role-based-access-control.md) contiene altre informazioni.

- Creare un gruppo di utenti o un gruppo di dispositivi con i dispositivi HoloLens 2. Per altre informazioni, vedere [Gruppi di utenti e gruppi di dispositivi](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Esempio

Questo esempio usa Windows PowerShell per creare un criterio di Controllo applicazioni di Windows Defender (WDAC). Il criterio impedisce l'apertura di app specifiche. Usare Intune per distribuire il criterio ai dispositivi HoloLens 2.

1. Nel computer desktop aprire l'app **Windows PowerShell**.
2. Ottenere informazioni sul pacchetto dell'applicazione installato nel computer desktop:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Immettere ad esempio:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Successivamente, verificare che il pacchetto abbia gli attributi dell'applicazione:

    ```powershell
    $package1
    ```

    Verranno visualizzati attributi simili ai dettagli delle app seguenti:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Creare un criterio WDAC e aggiungere il pacchetto dell'app alla regola di NEGAZIONE:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Ripetere i passaggi 2 e 3 per tutte le altre applicazioni che si desidera NEGARE:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Immettere ad esempio:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Convertire il criterio WDAC in **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Per includere tutte le versioni di un'app, in newPolicy.xml, assicurarsi che `PackageVersion="65535.65535.65535.65535"` sia nel nodo Nega:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Per `PackageFamilyNameRules`, è possibile usare le versioni seguenti:

    - **Consenti**: immettere `PackageVersion, 0.0.0.0`, che significa "Consentire questa versione e versioni successive".
    - **Nega**: immettere `PackageVersion, 65535.65535.65535.65535`, che significa "Negare questa versione e versioni successive".

6. Unire **newPolicy.xml** con il criterio predefinito presente sul computer desktop. Questo passaggio crea **mergedPolicy.xml**. Ad esempio, consentire l'esecuzione dei driver firmati Windows e WHQL e delle app firmate Microsoft Store:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Disabilitare la regola della **Modalità di controllo** in **mergedPolicy.xml**. Quando si esegue l'unione, la Modalità di controllo viene attivata automaticamente:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Abilitare la regola **Invalidare EA dopo il riavvio** in **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Per altre informazioni su queste regole, vedere [Comprendere le regole dei criteri di WDAC e le regole dei file](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Convertire **mergedPolicy.xml** in formato binario. Questo passaggio crea **compiledPolicy.bin**. Si aggiungerà questo file binario **compiledPolicy.bin** a Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Creare il profilo di configurazione del dispositivo personalizzato in Intune:

    1. Nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) creare un profilo di configurazione del dispositivo personalizzato di Windows 10.

        Per i passaggi specifici, vedere [Creare un profilo personalizzato usando OMA-URI in Intune](custom-settings-configure.md).

    2. Quando si crea il profilo, immettere le impostazioni seguenti:

      - **OMA-URI**: immettere `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. Sostituire `<PolicyGUID>` con il nodo PolicyTypeID nel file **mergedPolicy.xml** creato nel passaggio 6.

        Usando l'esempio, immettere `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`.

        Il GUID di criterio **deve corrispondere** al nodo PolicyTypeID nel file **mergedPolicy.xml** (creato nel passaggio 6).

      - **Tipo di dati**: impostare su **file Base64**. Il file viene convertito automaticamente da bin a Base64.
      - **File di certificato**: Caricare il file binario **compiledPolicy.bin** (creato nel passaggio 9).

      Al termine, le impostazioni saranno simili alle seguenti:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Aggiungere un OMA-URI personalizzato per configurare il CSP di Controllo applicazioni in Microsoft Intune.":::

11. Quando il profilo viene [assegnato](device-profile-assign.md) al gruppo HoloLens 2, verificare lo stato del profilo. Dopo che il profilo è stato applicato correttamente, riavviare i dispositivi HoloLens 2.

## <a name="next-steps"></a>Passaggi successivi

[Assegnare il profilo](device-profile-assign.md) e [monitorarne lo stato](device-profile-monitor.md).

[Altre informazioni sui profili personalizzati in Intune](custom-settings-configure.md).
