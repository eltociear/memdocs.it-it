---
title: Gruppi di limiti per le versioni 1511, 1602 e 1606
titleSuffix: Configuration Manager
description: Usare gruppi di limiti con Configuration Manager versioni 1511, 1602 e 1606.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704839"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Gruppi di limiti per Configuration Manager versioni 1511, 1602 e 1606

*Si applica a: Configuration Manager (Current Branch)*
<!-- This topic drops from TOC with the release of version 1706 -->

Le informazioni contenute in questo argomento si riferiscono specificamente all'uso di gruppi di limiti con le versioni 1511, 1602 e 1606 di Configuration Manager.
Se si usa la versione 1610 o successiva, vedere [Configurare gruppi di limiti](boundary-groups.md) per informazioni sull'uso di gruppi di limiti riprogettati.  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Gruppi di limiti  
 I gruppi di limiti vengono creati per raggruppare logicamente i percorsi di rete correlati (limiti) e semplificare la gestione dell'infrastruttura. Prima di usare un gruppo di limiti è necessario assegnare i limiti ai gruppi di limiti. I client usano la configurazione del gruppo di limiti per:  

-   Assegnazione automatica al sito  

-   Percorso contenuto  

-   Punti di gestione preferiti

    Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dall'interno della configurazione del gruppo di limiti. Vedere la procedura *Per abilitare l'uso dei punti di gestione preferiti* più avanti in questo argomento.  

Quando si configurano i gruppi di limiti, uno o più limiti vengono aggiunti al gruppo. È quindi possibile configurare altre impostazioni per l'uso da parte dei client che si trovano in tali limiti.  

#### <a name="to-create-a-boundary-group"></a>Per creare un gruppo di limiti  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea gruppo limite**.  

3.  Nella finestra di dialogo **Crea gruppo limite** scegliere la scheda **Generale** e quindi specificare **Nome** per il gruppo di limiti.  

4.  Scegliere **OK** per salvare il nuovo gruppo di limiti.  

#### <a name="to-set-up-a-boundary-group"></a>Per configurare un gruppo di limiti  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Scegliere il gruppo di limiti da modificare.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** del gruppo di limiti scegliere la scheda **Generale** per modificare i limiti appartenenti a questo gruppo:  

    -   Per aggiungere limiti, scegliere **Aggiungi**, selezionare la casella di controllo per uno o più limiti e quindi scegliere **OK**.  

    -   Per rimuovere limiti, selezionarne uno e scegliere **Rimuovi**.  

5.  Scegliere la scheda **Riferimenti** per modificare l'assegnazione al sito e la configurazione del server del sistema del sito associata:  

    -   Per consentire ai client di usare questo gruppo di limiti per l'assegnazione al sito, selezionare la casella di controllo **Utilizza questo gruppo limite per l'assegnazione sito** e quindi selezionare un sito dalla casella a discesa **Sito assegnato**.  

    -   Per configurare quali server del sistema del sito disponibili sono associati a questo gruppo di limiti:  

    1.  Scegliere **Aggiungi** e quindi selezionare la casella di controllo per uno o più server. I server vengono aggiunti come server del sistema del sito associati per questo gruppo di limiti. Sono disponibili solo i server su cui è installato il ruolo del sistema del sito supportato.  

        > [!NOTE]  
        >  È possibile selezionare qualsiasi combinazione dei sistemi del sito disponibili da qualsiasi sito della gerarchia. I sistemi del sito selezionati vengono elencati nella scheda **Sistemi del sito** nelle proprietà di ogni limite appartenente a questo gruppo di limiti.  

    2.  Per rimuovere un server da questo gruppo di limiti, selezionare il server e quindi scegliere **Rimuovi**.  

        > [!NOTE]  
        >  Per non usare più questo gruppo di limiti per l'associazione dei sistemi del sito, è necessario rimuovere tutti i server elencati come server del sistema del sito associati.  

    3.  Per modificare la velocità di connessione di rete per un server del sistema del sito per questo gruppo di limiti, selezionare il server e quindi scegliere **Modifica connessione**.  

         Per impostazione predefinita, la velocità di connessione per ogni sistema del sito è impostata su **Veloce**, ma è possibile modificarla in **Lenta**. La velocità di connessione di rete e la configurazione di una distribuzione determinano se un client può scaricare il contenuto dal server.  

6.  Scegliere **OK** per chiudere le proprietà del gruppo di limiti e salvare la configurazione.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Per associare un server di distribuzione del contenuto o un punto di gestione a un gruppo di limiti  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Scegliere il gruppo di limiti da modificare.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti scegliere la scheda **Riferimenti**.  

5.  In **Seleziona server del sistema del sito** scegliere **Aggiungi**, selezionare la casella di controllo per i server del sistema del sito da associare a questo gruppo di limiti e quindi scegliere **OK**.  

6.  Scegliere **OK** per chiudere la finestra di dialogo e salvare la configurazione del gruppo di limiti.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Per abilitare l'uso dei punti di gestione preferiti  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** > **Siti** e quindi nella scheda **Home** scegliere **Impostazioni gerarchia**.  

2.  Nella scheda **Generale** di **Impostazioni gerarchia** scegliere **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**.  

3.  Scegliere **OK** per chiudere le finestra di dialogo e salvare la configurazione.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Per configurare un sito di fallback per l'assegnazione automatica al sito  

1. Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** >  **Siti**.  

2. Nella scheda **Home** del gruppo **Siti** scegliere **Impostazioni gerarchia**.  

3. Nella scheda **Generale** selezionare la casella di controllo **Utilizza sito di fallback** e quindi scegliere un sito dall'elenco a discesa **Sito di fallback**.  

4. Scegliere **OK** per salvare la configurazione.  

   Le sezioni seguenti forniscono dettagli aggiuntivi sulle configurazioni del gruppo di limiti.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informazioni sull'assegnazione al sito  
 È possibile configurare ogni gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica al sito verrà aggiunto al sito assegnato di un gruppo di limiti che si trova nel percorso di rete corrente del client.  

-   Dopo l'assegnazione a un sito, il client non cambia la propria assegnazione in caso di modifica del percorso di rete. Se ad esempio il client si sposta in un nuovo percorso di rete rappresentato da un limite incluso in un gruppo con un'assegnazione sito diversa, il sito assegnato di tale client rimane invariato.  

-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, le informazioni sulla rete per la risorsa individuata vengono valutate in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  

-   Quando un limite è membro di più gruppi con diversi siti assegnati, i client selezionano uno dei siti in modo casuale.  

-   Le modifiche a un sito assegnato del gruppo di limiti si applicano solo alle nuove azioni di assegnazione sito. I client assegnati in precedenza a un sito non valutano nuovamente l'assegnazione in base alle modifiche apportate alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione di client a un sito, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Come assegnare i client a un sito](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informazioni sul percorso del contenuto  
 È possibile configurare ogni gruppo di limiti con uno o più punti di distribuzione e punti di migrazione stato e associare questi stessi punti a più gruppi di limiti.  

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione. Configuration Manager invia al client un elenco dei punti di distribuzione associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

-   **Durante la distribuzione del sistema operativo** i client richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato. Configuration Manager invia al client un elenco dei punti di migrazione dello stato associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o del contenuto.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informazioni sui punti di gestione preferiti  
 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

-   Il client prova a usare un punto di gestione preferito dal sito assegnato prima di usare un punto di gestione dal sito assegnato che non è configurato come preferito.  

-   Per usare questa opzione è necessario abilitarla per la gerarchia e configurare i gruppi di limiti nei singoli siti primari in modo da includere i punti di gestione che devono essere associati ai limiti del gruppo.  

-   Se sono configurati punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, i punti di gestione preferiti vengono inseriti all'inizio dell'elenco dei punti di gestione assegnati, che include tutti i punti di gestione del sito assegnato del client.  

> [!NOTE]  
>  Quando un client si sposta, come nel caso di un computer portatile spostato in una postazione remota con un nuovo percorso di rete, può usare un punto di gestione (o un punto di gestione proxy) dal sito locale nella nuova posizione prima di provare a usare un punto di gestione dal sito assegnato (che include i punti di gestione preferiti).  Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informazioni sui limiti sovrapposti  
 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto:  

-   **Quando un client richiede un contenuto** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno il contenuto.  

-   **Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o del contenuto.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Informazioni sulla velocità di connessione di rete  
 È possibile impostare la velocità di connessione di rete per ogni server del sistema del sito in un gruppo di limiti. Questa impostazione si applica ai client che si connettono a un sistema del sito basato sulla configurazione di questo gruppo di limiti. Lo stesso server del sistema del sito può avere una velocità di connessione impostata nei diversi gruppi di limiti.  

 Per impostazione predefinita, la velocità di connessione di rete è **Veloce**, ma è possibile modificarla in **Lenta**. La velocità di connessione di rete e la configurazione della distribuzione verificano se un client incluso in un gruppo di limiti associato può scaricare contenuto da un punto di distribuzione.  

 Per altre informazioni sul modo in cui la configurazione della velocità di connessione di rete influisce sulla modalità di recupero del contenuto da parte dei client, vedere [Scenari del percorso di origine del contenuto](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
