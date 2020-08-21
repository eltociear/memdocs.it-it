---
title: Aggiornare i dispositivi Windows a una versione diversa
titleSuffix: Configuration Manager
description: Usare Configuration Manager per aggiornare automaticamente i dispositivi Windows 10 a una diversa edizione di Windows.
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 920f3c9aabcdec1242a6f5e5fc8e6b65c5cc0b53
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694611"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Aggiornare i dispositivi Windows a una nuova edizione con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I **criteri di aggiornamento edizione** consentono di aggiornare automaticamente i dispositivi Windows 10 a un'edizione diversa.

Sono supportati i percorsi di aggiornamento seguenti:

- Da Windows 10 Pro a Windows 10 Enterprise
- Da Windows 10 Home a Windows 10 Education
- Da Windows 10 Mobile a Windows 10 Mobile Enterprise

I dispositivi devono eseguire il software client di Configuration Manager. I dispositivi gestiti da [MDM locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) non sono supportati.

## <a name="before-you-start"></a>Prima di iniziare

Prima di iniziare l'aggiornamento dei dispositivi alla versione più recente, esaminare i prerequisiti seguenti:  

- Per le edizioni Desktop di Windows 10: un codice Product Key valido per la nuova versione di Windows in tutti i dispositivi a cui sono destinati i criteri. Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server. <!--496871-->  

- Per Windows 10 Mobile: un file di licenza XML del Centro servizi per contratti multilicenza (VLSC). Questo file contiene le informazioni sulle licenze per la nuova versione di Windows in tutti i dispositivi a cui sono destinati i criteri. Scaricare il file ISO per **Windows 10 Mobile Enterprise**, che include il codice di licenza XML.<!-- SCCMDocs#2033 -->

- Per gestire questo tipo di criteri, è necessario essere nel ruolo di sicurezza **Amministratore completo** di Configuration Manager.

## <a name="configure-the-policy"></a>Configurare i criteri  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare il nodo **Aggiornamento edizione di Windows 10**.  

2. Nella scheda **Home** della barra multifunzione selezionare **Crea criterio di aggiornamento edizione** nel gruppo **Crea**.  

3. Selezionare **Crea criterio**.  

4. Nella pagina **Generale** della **Creazione guidata criteri aggiornamento edizione**specificare le informazioni seguenti:  

    - **Nome** - Immettere un nome per i criteri di aggiornamento edizione  

    - **Descrizione** (facoltativo) - Facoltativamente, immettere una descrizione per il criterio che consenta di identificarlo nella console di Configuration Manager  

    - **SKU per aggiornare il dispositivo a** - Nell'elenco a discesa selezionare l'edizione di destinazione di Windows 10 Desktop o Windows 10 Mobile  

    - **Informazioni sulla licenza** - Selezionare una delle opzioni seguenti:  

        - **Codice Product Key** -Immettere un codice Product Key valido per l'edizione Windows 10 Desktop di destinazione  

            > [!NOTE]  
            > Dopo aver creato criteri che contengono un codice Product Key, non è possibile modificare il codice Product Key in un secondo momento. Configuration Manager nasconde il codice per motivi di sicurezza. Per modificare il codice Product Key, immettere nuovamente l'intero codice.  

        - **File di licenza** - Selezionare **Sfoglia** per scegliere un file di licenza valido in formato XML. Configuration Manager usa questo file di licenza per aggiornare i dispositivi Windows 10 Mobile.  

5. Completare la procedura guidata.  

## <a name="deploy-the-policy"></a>Distribuire il criterio  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare il nodo **Aggiornamento edizione di Windows 10**.  

2. Selezionare i criteri di aggiornamento dell'edizione di Windows 10 da distribuire. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci** nel gruppo **Distribuzione**.  

3. Scegliere la raccolta di dispositivi in cui si vuole distribuire il criterio.

4. Selezionare la pianificazione in base alla quale il client valuta i criteri.

5. Completare la procedura guidata.

## <a name="next-steps"></a>Passaggi successivi

Monitorare la distribuzione dal nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Se vengono visualizzati errori che indicano che la distribuzione non è riuscita, ad esempio:

- **Non applicabile per questo dispositivo**
- **Conversione tipo di dati non riuscita**

Questi errori non indicano che la distribuzione non è riuscita. Verificare nel dispositivo di destinazione che l'aggiornamento sia stato eseguito correttamente.

Dopo che il client ha valutato i criteri di destinazione, l'aggiornamento verrà applicato entro due ore. [Alcune versioni di Windows](/windows/deployment/upgrade/windows-10-edition-upgrades) possono richiedere un riavvio in quel momento. Assicurarsi di informare tutti gli utenti interessati dalla distribuzione dei criteri o pianificare la distribuzione dei criteri in ore non lavorative.

Se viene visualizzato l'errore seguente in **DcmWmiProvider.log** nel client, verificare di usare il codice corretto per lo scenario di attivazione. Per altre informazioni, vedere la sezione [Prima di iniziare](#before-you-start). Se si usa un servizio di gestione delle chiavi (KMS) per l'attivazione, assicurarsi di usare un [codice di installazione client KMS](/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Vedere anche

- [Pianificare l'attivazione dei contratti multilicenza](/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Aggiornamento edizione di Windows 10](/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Aggiornare le edizioni Windows 10 o disattivare la modalità S nei dispositivi con Microsoft Intune](/intune/edition-upgrade-configure-windows-10)