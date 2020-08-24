---
title: Aggiungere manualmente l'app Portale aziendale di Windows 10
titleSuffix: Microsoft Intune
description: Informazioni su come il personale dell'azienda può aggiungere manualmente l'app Portale aziendale di Windows 10 nei propri PC da Microsoft Store.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: bfe1a2d3-f611-4dbb-adef-c0dff4d7b810
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c41f22e2aa60803067b9015f2ae3a84db43ff894
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179537"
---
# <a name="add-the-windows-10-company-portal-app-by-using-microsoft-intune"></a>Aggiungere l'app Portale aziendale di Windows 10 usando Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Per gestire dispositivi e installare app, gli utenti possono installare l'app Portale aziendale da Microsoft Store. Se per le specifiche esigenze aziendali è richiesta l'assegnazione dell'app Portale aziendale, è comunque possibile assegnare l'app Portale aziendale di Windows 10 direttamente da Intune, anche se Intune non è integrato con Microsoft Store per le aziende.

 > [!IMPORTANT]
 > Se si scarica l'app Portale aziendale, per l'opzione descritta in questo articolo è necessario che gli aggiornamenti manuali siano assegnati ogni volta che viene rilasciato un aggiornamento dell'app. Per distribuire l'app Portale aziendale per i dispositivi Windows 10 con provisioning tramite Autopilot, vedere [Aggiungere dispositivi Autopilot all'app Portale aziendale di Windows 10](store-apps-company-portal-autopilot.md).

## <a name="configure-settings-to-show-offline-apps"></a>Configurare le impostazioni per visualizzare le app offline
1. Accedere a [Microsoft Store per le aziende](https://www.microsoft.com/business-store) con l'account amministratore.
2. Selezionare la scheda **Manage** (Gestisci) nella parte superiore della finestra.
3. Nel riquadro di sinistra selezionare **Impostazioni**.
4. Impostare **Show offline apps** (Mostra app offline) in **Shopping experience** (Esperienza di acquisto) su **On** (Attivo).  
    Saranno visualizzate le app con licenza offline.

## <a name="download-the-offline-company-portal-app"></a>Scaricare l'app Portale aziendale offline
1. Cercare e selezionare l'app **Portale aziendale**.
2. Impostare il **Tipo di licenza** su **Offline**.
3. Selezionare **Scarica l'app** per acquisire e aggiungere l'app Portale aziendale offline all'inventario.
4. Selezionare **Gestisci** nella pagina dell'app **Portale aziendale**.
5. Selezionare **Windows 10 all devices** (Windows 10 (tutti i dispositivi)) come **Piattaforma**, quindi scegliere un valore appropriato per **Versione minima**, **Architettura** e **Download app metadata**. 
6. Fare clic su **Download** in **Dettagli pacchetto** per salvare il file nel computer locale.

    ![Sono selezionati dispositivi Windows 10 la cui architettura corrisponde a X86](./media/app-sideload-windows/Win10CP-all-devices.png)

7. Scaricare tutti i pacchetti in "Framework richiesti" selezionando **Download**.  

    Questa azione deve essere completata per le architetture x86, x64 e ARM:<br> 
    *Quando si seleziona 1507 come versione minima del sistema operativo, sono 9 i pacchetti framework richiesti, i pacchetti sono 12 quando si seleziona la versione 1511, sono invece 15 quando si seleziona la versione 1607.*

8. Nel portale di Azure in Microsoft Intune caricare l'app Portale aziendale come nuova app. Aggiungere l'applicazione selezionando App line-of-business come **Tipo di app** nel riquadro **Seleziona il tipo di app**. Selezionare quindi il file del pacchetto dell'app con estensione AppxBundle.

9. In **Selezionare i file delle app relativi alle dipendenze** selezionare tutte le dipendenze scaricate nel passaggio 7 usando MAIUSC+clic e verificare che la colonna **Aggiunti** visualizzi **Sì** per le architetture necessarie.

     > [!NOTE]
     > Se le dipendenze non vengono aggiunte, è possibile che l'app non venga installata nei tipi di dispositivo specificati.

10. Fare clic su **Ok**, immettere eventuali **Informazioni sull'app** e fare clic su **Aggiungi**.

11. Assegnare l'app Portale aziendale come app obbligatoria al set di utenti o al gruppo di dispositivi selezionato.  

Per altre informazioni su come Intune gestisce le dipendenze per le app universali, vedere [Deploying an appxbundle with dependencies via Microsoft Intune MDM](https://blogs.technet.microsoft.com/configmgrdogs/2016/11/30/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm/) (Distribuzione di un appxbundle con dipendenze tramite MDM di Microsoft Intune).  

## <a name="frequently-asked-questions"></a>Domande frequenti 
### <a name="how-do-i-update-the-company-portal-app-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>Come si aggiorna l'app Portale aziendale nei dispositivi degli utenti se hanno già installato le app precedenti dallo Store?
Se gli utenti hanno già installato le app Portale aziendale di Windows 8.1 da Microsoft Store, queste dovrebbero essere aggiornate automaticamente all'ultima versione senza alcun intervento da parte dell'amministratore o degli utenti. Se l'aggiornamento non viene eseguito, chiedere agli utenti di controllare se hanno abilitato gli aggiornamenti automatici per le app dello Store nei dispositivi.   

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Come aggiornare l'app Portale aziendale di Windows 8.1 trasferita localmente all'app Portale aziendale di Windows 10?
Il percorso di migrazione consigliato consiste nell'eliminare l'assegnazione dell'app Portale aziendale di Windows 8.1 impostando l'azione di assegnazione su **Disinstalla**. Dopo aver selezionato questa impostazione, è possibile assegnare l'app Portale aziendale di Windows 10 usando una delle opzioni descritte in precedenza.  

Se è necessario trasferire localmente l'app e si è assegnata l'app Portale aziendale di Windows 8.1 senza firmarla con il certificato Symantec, completare l'aggiornamento seguendo i passaggi riportati nella sezione precedente di questo articolo.

Se è necessario trasferire localmente l'app e si è firmata e assegnata l'app Portale aziendale di Windows 8.1 con il certificato di firma codice Symantec, seguire la procedura descritta nella prossima sezione.

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>Come si aggiorna l'app Portale aziendale di Windows 8.1 firmata e trasferita localmente all'app Portale aziendale di Windows 10?
Il percorso di migrazione consigliato consiste nell'eliminare l'assegnazione esistente dell'app Portale aziendale di Windows 8.1 impostando l'azione di assegnazione su **Disinstalla**. Dopo aver selezionato questa impostazione, è possibile assegnare l'app Portale aziendale di Windows 10 normalmente.  

In caso contrario, è necessario aggiornare e firmare l'app Portale aziendale di Windows 10 per assicurarsi che il percorso di aggiornamento venga rispettato.  

Se l'app Portale aziendale di Windows 10 viene firmata e assegnata in questo modo, sarà necessario ripetere questa procedura per ogni nuovo aggiornamento dell'app disponibile nello Store. L'app non viene aggiornata automaticamente in caso di aggiornamento dello Store.  

Ecco come firmare e assegnare l'app in questo modo:

1. Scaricare lo [script di firma di Microsoft Intune per l'app Portale aziendale di Windows 10](https://aka.ms/win10cpscript).  
    Per l'esecuzione di questo script è necessario che sia installato Windows 10 SDK nel computer host. [Scaricare Windows SDK per Windows 10](https://go.microsoft.com/fwlink/?LinkId=619296).
2. Scaricare l'app Portale aziendale di Windows 10 da Microsoft Store per le aziende, come descritto in precedenza.  
3. Per firmare l'app Portale aziendale di Windows 10, eseguire lo script con i parametri di input riportati nel dettaglio nell'intestazione, come descritto nella tabella seguente.  
    Non è necessario passare le dipendenze allo script. Le dipendenze sono necessarie solo quando l'app viene caricata nella console di amministrazione di Intune.

| Parametro |  Descrizione  |
|---|---|
| InputWin10AppxBundle  |  Percorso del file appxbundle di origine. |
| OutputWin10AppxBundle | Percorso di output per il file appxbundle firmato. 
| Win81Appx  | Percorso del file (con estensione appx) dell'app Portale aziendale per Windows 8.1. |
| PfxFilePath  |  Percorso del file (con estensione pfx) del certificato di firma codice di Symantec Enterprise Mobile.  |
| PfxPassword  | Password del certificato di firma codice di Symantec Enterprise Mobile. |
| PublisherId | ID editore dell'azienda. Se assente, viene usato il campo Subject del certificato di firma codice mobile aziendale Symantec. |
| SdkPath | Percorso della cartella radice di Windows 10 SDK. Questo argomento è facoltativo e l'impostazione predefinita è ${env:ProgramFiles(x86)}\Windows Kits\10.  |

Al termine dell'esecuzione, lo script genera la versione firmata dell'app Portale aziendale di Windows 10. È quindi possibile assegnare la versione firmata dell'app come app line-of-business (LOB) tramite Intune, in modo da aggiornare le versioni attualmente assegnate alla nuova app.  

## <a name="next-steps"></a>Passaggi successivi

- [Assegnare app ai gruppi](apps-deploy.md)

