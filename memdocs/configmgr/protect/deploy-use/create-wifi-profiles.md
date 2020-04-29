---
title: Come creare profili Wi-Fi
titleSuffix: Configuration Manager
description: Informazioni su come usare i profili Wi-Fi in Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690229"
---
# <a name="create-wi-fi-profiles"></a>Creare profili Wi-Fi

*Si applica a: Configuration Manager (Current Branch)*

Usare i profili Wi-Fi in Configuration Manager per distribuire impostazioni di rete wireless agli utenti della propria organizzazione. Distribuendo queste impostazioni si semplifica la procedura di connessione alla rete Wi-Fi per gli utenti.  

Si supponga ad esempio di avere una rete Wi-Fi per cui si vuole abilitare la connessione da parte di tutti i portatili Windows. Creare un profilo Wi-Fi contenente le impostazioni necessarie per connettersi alla rete wireless. Distribuire quindi il profilo a tutti gli utenti della gerarchia che hanno portatili Windows. Gli utenti di questi dispositivi visualizzeranno così la rete nell'elenco delle reti wireless e potranno stabilire facilmente la connessione.  

È possibile configurare i profili Wi-Fi per le versioni di sistema operativo seguenti:

- Windows 8.1 a 32 bit o 64 bit

- Windows RT 8.1

- Windows 10 o Windows 10 Mobile

È anche possibile usare Configuration Manager per distribuire le impostazioni di rete wireless ai dispositivi mobili usando la gestione di dispositivi mobili (MDM) locale. Per informazioni più generali, vedere [Informazioni sulla gestione di dispositivi mobili locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Quando si crea un profilo Wi-Fi, è possibile includere una vasta gamma di impostazioni di protezione. Queste impostazioni includono certificati per la convalida del server e l'autenticazione del client di cui è stato eseguito il push usando profili certificato di Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Creare un profilo Wi-Fi

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità**, espandere **Accesso risorse aziendali** e selezionare il nodo **Profili Wi-Fi**.

1. Nel gruppo **Crea** della scheda **Home** scegliere **Crea profilo Wi-Fi**.

1. Nella pagina **Generale** della Creazione guidata profilo Wi-Fi, specificare le seguenti informazioni:

    - **Nome**: immettere un nome univoco per identificare il profilo nella console.

    - **Descrizione**: facoltativamente, aggiungere una descrizione per specificare altre informazioni sul profilo Wi-Fi.

    - **Importa un elemento del profilo Wi-Fi esistente da un file**: selezionare questa opzione per usare le impostazioni di un altro profilo Wi-Fi. Quando si seleziona questa opzione, il resto della procedura guidata include semplicemente due pagine: **Importa profilo Wi-Fi** e **Piattaforme supportate**.

        > [!IMPORTANT]
        > Assicurarsi che il profilo Wi-Fi importato contenga codice XML valido per un profilo Wi-Fi. Quando si importa il file, Configuration Manager non convalida il profilo.

    - **Gravità della non conformità per i report**: scegliere uno dei livelli di gravità seguenti segnalati dal dispositivo se il profilo Wi-Fi viene valutato come non conforme. Se, ad esempio, l'installazione del profilo ha esito negativo, significa che non è conforme.

        - **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.

        - **Informazioni**

        - **Avviso**

        - **Errore critico**

        - **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. I dispositivi registrano inoltre lo stato non conforme come un evento Windows nel log eventi dell'applicazione.

1. Nella pagina **Profilo Wi-Fi** della procedura guidata specificare le informazioni seguenti:

    - **Nome rete**: specificare il nome che i dispositivi visualizzeranno come nome della rete.

        > [!IMPORTANT]
        > Configuration Manager non supporta l'uso dei caratteri apostrofo (`'`) o virgola (`,`) nel nome della rete.

    - **SSID**: specificare l'ID della rete wireless, con distinzione tra maiuscole e minuscole.

    - **Connetti automaticamente quando la rete si trova nel campo del computer**
    - **Cerca altre reti wireless durante la connessione a questa rete**
    - **Connetti quando la rete non sta trasmettendo il nome (SSID)**

1. Nella pagina **Configurazione protezione** specificare le informazioni seguenti:

    > [!IMPORTANT]
    > Se si sta creando un profilo Wi-Fi per la [gestione di dispositivi mobili (MDM) locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md), la versione Current Branch di Configuration Manager supporta solo le configurazioni di sicurezza Wi-Fi seguenti:  
    >
    > - Tipi di sicurezza: **WPA2 Enterprise** o **WPA2 Personal**  
    > - Tipi di crittografia: **AES** o **TKIP**  
    > - Tipi EAP: **Smart Card o altro certificato** o **PEAP**  

    - **Tipo di sicurezza**: selezionare il protocollo di sicurezza usato dalla rete wireless oppure scegliere **Nessuna autenticazione (aperta)** se la rete non è protetta.

    - **Crittografia**: se il tipo di sicurezza lo supporta, impostare il metodo di crittografia per la rete wireless.

    - **Tipo EAP**: selezionare il protocollo di autenticazione per il metodo di crittografia scelto.

        > [!NOTE]
        > Solo per i dispositivi Windows Phone: i tipi EAP **LEAP** ed **EAP-FAST** non sono supportati.

        Selezionare **Configura** per specificare le proprietà per il tipo EAP selezionato. Questa opzione non è disponibile per alcuni tipi EAP selezionati.

        > [!IMPORTANT]
        > La finestra di configurazione del tipo EAP è una finestra di Windows. Assicurarsi di eseguire la console di Configuration Manager in un computer che supporta il tipo EAP selezionato.

    - **Memorizza le credenziali utente a ogni accesso**: selezionare questa opzione per archiviare le credenziali utente in modo che gli utenti non debbano immettere le credenziali di rete wireless ogni volta che accedono a Windows.

1. Nella pagina **Impostazioni avanzate** della procedura guidata specificare impostazioni aggiuntive per il profilo Wi-Fi. Le impostazioni avanzate possono non essere disponibili, o variare, in base alle opzioni selezionate nella pagina **Configurazione protezione** della procedura guidata. Ad esempio, la modalità di autenticazione o le opzioni per l'accesso Single Sign-On.

1. Nella pagina **Impostazioni proxy**, se la rete wireless usa un server proxy, selezionare l'opzione **Configura impostazioni proxy per questo profilo Wi-Fi**. Fornire quindi le informazioni di configurazione per il proxy.

1. Nella pagina **Piattaforme supportate** selezionare le versioni del sistema operativo in cui è applicabile questo profilo Wi-Fi.

1. Completare la procedura guidata.

## <a name="next-step"></a>Passaggio successivo

> [!div class="nextstepaction"]
> [Come distribuire profili Wi-Fi](deploy-wifi-vpn-email-cert-profiles.md)
