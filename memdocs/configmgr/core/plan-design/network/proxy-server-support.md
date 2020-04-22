---
title: Supporto dei server proxy
titleSuffix: Configuration Manager
description: Informazioni sull'utilizzo dei server proxy nei server del sistema del sito di Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5581214dd786bdefd29d0e4d2626de536ad26ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701479"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Supporto dei server proxy in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con alcuni server del sistema del sito di Configuration Manager è richiesta la connessione a Internet. Se l'ambiente richiede traffico Internet per usare un server proxy, configurare questi ruoli del sistema del sito per l'uso del proxy.  

- Un computer che ospita un server del sistema del sito supporta una sola configurazione del server proxy. Tutti i ruoli del sistema del sito in tale computer condividono la stessa configurazione proxy. Se sono necessari server proxy separati per diversi ruoli o istanze di un ruolo, inserire i ruoli in server del sistema del sito separati.  

- Quando si configurano nuove impostazioni del server proxy per un server del sistema del sito che ha già una configurazione del server proxy, la configurazione originale viene sovrascritta.  

- Per impostazione predefinita, le connessioni al proxy usano l'account di **sistema** del computer che ospita il ruolo del sistema del sito.  

- Se l'account computer non può eseguire l'autenticazione, il server del sistema del sito può archiviare le credenziali utente per la connessione al server proxy. Tali credenziali costituiscono l'**account del server proxy del sistema del sito**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Ruoli del sistema del sito che usano un proxy

I ruoli del sistema del sito seguenti si connettono a Internet e, se necessario, possono usare un server proxy:  

### <a name="asset-intelligence-synchronization-point"></a>Punto di sincronizzazione di Asset Intelligence

Questo ruolo del sistema del sito si connette a Microsoft e usa una configurazione del server proxy nel computer che ospita il punto di sincronizzazione di Asset Intelligence.  

### <a name="cloud-distribution-point"></a>Punto di distribuzione cloud

Il ruolo Punto di distribuzione cloud viene eseguito in Microsoft Azure. Non si deve configurare questo ruolo del sistema del sito per usare un proxy. Impostare la configurazione proxy nel server del sito primario che gestisce il punto di distribuzione cloud.  

Per questa configurazione, il server del sito primario:  

- Deve riuscire a connettersi a Microsoft Azure per la configurazione, il monitoraggio e la distribuzione del contenuto al punto di distribuzione cloud.  

- Per impostazione predefinita, usa l'account di **sistema** del computer per effettuare la connessione. Se necessario, può anche usare l'account del server proxy del sistema del sito.  

- Usa le API del Web browser di Windows.  

### <a name="distribution-point"></a>Punto di distribuzione

<!-- 5856396 -->

A partire dalla versione 2002, se si abilita un punto di distribuzione di Configuration Manager per Microsoft Connected Cache, può comunicare tramite un server proxy non autenticato per l'accesso a Internet. Per altre informazioni, vedere [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

### <a name="exchange-server-connector"></a>Connettore Exchange Server

Questo ruolo del sistema del sito si connette a un'istanza di Exchange Server. Usa una configurazione del server proxy nel computer che ospita il connettore Exchange Server.  

### <a name="service-connection-point"></a>punto di connessione del servizio

Questo ruolo del sistema del sito si connette al servizio cloud di Configuration Manager per scaricare gli aggiornamenti di versione per Configuration Manager. Usa un server proxy configurato nel computer che ospita il punto di connessione del servizio.  

### <a name="software-update-point"></a>Punto di aggiornamento software

Questo ruolo del sistema del sito usa il proxy quando si connette a Microsoft Update per scaricare le patch e sincronizzare le informazioni sugli aggiornamenti. Come per ogni altro ruolo del sistema del sito, configurare prima di tutto le impostazioni proxy del sistema del sito. Configurare quindi le opzioni seguenti specifiche per il punto di aggiornamento software:  

- **Usa un server proxy durante la sincronizzazione degli aggiornamenti software**  

- **Usare un server proxy quando si scaricano contenuti tramite le regole di distribuzione automatica**  

    > [!NOTE]
    > Anche se disponibile, questa impostazione non viene usata dai punti di aggiornamento software nei siti secondari.  

Queste impostazioni si trovano nella scheda **Impostazioni proxy e account** delle proprietà del punto di aggiornamento software.  

> [!NOTE]
> Per impostazione predefinita, quando vengono eseguite le regole di distribuzione automatica, viene usato l'account di **sistema** del sito del server in cui è stata creata una regola di distribuzione automatica per connettersi a Internet e scaricare gli aggiornamenti software. In alternativa, configurare e usare l'account del server proxy del sistema del sito. 
>
> Quando questo account non può accedere a Internet, non è possibile scaricare gli aggiornamenti software. Nel file **ruleengine.log** viene registrata la voce seguente:  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a> Altre funzionalità che usano il proxy per un server del sistema del sito

*(Funzionalità introdotta nella versione 2002)*

A partire da Configuration Manager versione 2002, le funzionalità seguenti usano il proxy del sistema del sito che ospita il ruolo di [punto di connessione del servizio](#service-connection-point): <!--5913817-->

- [Individuazione degli utenti di Azure Active Directory (Azure AD)](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Individuazione dei gruppi di utenti di Azure AD](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Sincronizzazione dei risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>Configurare il proxy per un server del sistema del sito  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e quindi selezionare il nodo **Server e ruoli del sistema del sito**.  

2. Selezionare il server del sistema del sito che si vuole modificare. Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sul ruolo **Sistema del sito** e scegliere **Proprietà**.  

3. In Proprietà sistema del sito passare alla scheda **Proxy**. Configurare le impostazioni proxy seguenti:  

    - **Utilizza un server proxy per sincronizzare le informazioni provenienti da Internet**: selezionare questa opzione per abilitare il server del sistema del sito per l'uso di un server proxy.  

    - **Nome del server proxy**: specificare il nome host o il nome di dominio completo del server proxy nell'ambiente.  

    - **Porta**: specificare la porta di rete da usare per comunicare con il server proxy. Per impostazione predefinita, viene usata la porta **80**.  

    - **Utilizzare le credenziali per connettersi al server proxy**: diversi server proxy richiedono l'autenticazione dell'utente. Per impostazione predefinita, il server del sistema del sito usa il relativo account computer per la connessione al server proxy. Se necessario, abilitare questa opzione. Fare clic su **Imposta** e quindi scegliere **Account esistente** o specificare un valore in **Nuovo account**. Tali credenziali costituiscono l'**account del server proxy del sistema del sito**.  Per altre informazioni, vedere [Account usati in Configuration Manager](../hierarchy/accounts.md).  

4. Scegliere **OK** per salvare la nuova configurazione del server proxy.  
