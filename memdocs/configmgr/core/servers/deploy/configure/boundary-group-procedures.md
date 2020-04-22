---
title: Procedure per i gruppi di limiti
titleSuffix: Configuration Manager
description: Configurare i gruppi di limiti per organizzare logicamente i percorsi di rete correlati chiamati limiti.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697389"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Come configurare gruppi di limiti per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo include procedure su come configurare i gruppi di limiti. Prima di iniziare, assicurarsi di aver compreso i concetti relativi ai gruppi di limiti. Per altre informazioni, vedere [Gruppi di limiti](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a> Creare un gruppo di limiti  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Gruppi limite**.  

2.  Nella scheda **Home** selezionare **Crea gruppo limite** nel gruppo **Crea**.  

3.  Nella finestra di dialogo **Crea gruppo limite**, nella scheda **Generale**, specificare un valore in **Nome** per il gruppo di limiti. Facoltativamente, compilare il campo **Descrizione**.  

4.  Selezionare **OK** per salvare il nuovo gruppo di limiti o passare alla sezione successiva per configurare il gruppo di limiti.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a> Configurare un gruppo di limiti  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Gruppi limite**.  

2.  Selezionare il gruppo di limiti da modificare e quindi selezionare **Proprietà** sulla barra multifunzione. Verrà aperta la finestra delle proprietà del gruppo di limiti.  

Configurare le seguenti impostazioni:  
- [Aggiungere o rimuovere limiti](#bkmk_add)  
- [Configurare l'assegnazione sito e selezionare i server del sistema del sito](#bkmk_references)  
- [Configurare il comportamento di fallback](#bkmk_bg-fallback)  
- [Configurare le opzioni del gruppo di limiti](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a> Aggiungere o rimuovere limiti

Nella finestra di dialogo delle proprietà del gruppo di limiti usare la scheda **Generale** per modificare i limiti che fanno parte del gruppo:  

- Per aggiungere limiti, selezionare **Aggiungi**. Nella finestra Aggiungi limiti selezionare la casella di controllo per uno o più limiti e quindi selezionare **OK**.  

- Per rimuovere i limiti, selezionare il limite nell'elenco e quindi selezionare **Rimuovi**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a> Configurare l'assegnazione sito e selezionare i server del sistema del sito

Per modificare l'assegnazione sito e la configurazione del server del sistema del sito associata, passare alla scheda **Riferimenti** nella finestra delle proprietà del gruppo di limiti.  

- Per abilitare questo gruppo di limiti per l'uso da parte dei client per l'assegnazione sito, selezionare **Utilizza questo gruppo limite per l'assegnazione sito**. Selezionare quindi un sito dall'elenco a discesa **Sito assegnato**. Per altre informazioni, vedere [Assegnazione sito](boundary-groups.md#site-assignment).  

- Per associare i server del sistema del sito disponibili al gruppo di limiti, selezionare **Aggiungi**. Nella finestra Aggiungi sistemi del sito sono elencati solo i server con ruoli del sistema del sito supportati. Selezionare la casella di controllo per uno o più server e quindi fare clic su **OK**. I server vengono aggiunti come server del sistema del sito associati per il gruppo di limiti.  

    > [!NOTE]  
    >  È possibile selezionare qualsiasi combinazione dei sistemi del sito disponibili da qualsiasi sito della gerarchia. I sistemi del sito selezionati sono elencati nella scheda **Sistemi del sito** nelle proprietà di ogni limite appartenente al gruppo di limiti.  

- Per rimuovere un server dal gruppo di limiti, selezionare il server e quindi selezionare **Rimuovi**.  

    > [!NOTE]  
    >  Per interrompere l'uso di questo gruppo di limiti per i sistemi del sito in fase di associazione, rimuovere tutti i server elencati come server del sistema del sito associati.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a> Configurare il comportamento di fallback

Per configurare il comportamento di fallback, passare alla scheda **Relazioni** nella finestra delle proprietà del gruppo di limiti.  

- Per creare una relazione con un altro gruppo di limiti:  

  - Selezionare **Aggiungi**. Nella finestra Gruppi di limiti di fallback selezionare il gruppo di limiti da configurare.  

  - Impostare il tempo di fallback per i ruoli del sistema del sito seguenti:  
    - Punto di distribuzione  
    - Punto di aggiornamento software  
    - Punto di gestione  

      > [!Note]  
      > Ad esempio, aprire la finestra delle proprietà per il gruppo di limiti di una succursale. Nella finestra Gruppi di limiti di fallback selezionare il gruppo di limiti della sede centrale. Impostare il tempo di fallback per i punti di distribuzione su `20`. Quando si salva questa configurazione, i client nel gruppo di limiti della succursale inizieranno a cercare il contenuto nei punti di distribuzione nel gruppo di limiti della sede centrale dopo 20 minuti.  

  - Per impedire il fallback a un gruppo di limiti specifico, selezionare il gruppo di limiti e quindi selezionare **Non eseguire mai il fallback** per il tipo di ruolo del sistema del sito. Questa operazione può includere il *gruppo di limiti del sito predefinito*.  

- Per modificare la configurazione di una relazione esistente, selezionare il gruppo di limiti nell'elenco e quindi selezionare **Cambia**. Questa operazione apre la finestra Gruppi di limiti di fallback solo per il gruppo di limiti specifico.  
 
- Per rimuovere una relazione, selezionare il gruppo di limiti nell'elenco e quindi selezionare **Rimuovi**.  

Per altre informazioni, vedere [Fallback](boundary-groups.md#fallback). 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a> Configurare le opzioni del gruppo di limiti
<!--1356193-->
A partire dalla versione 1806, per configurare opzioni aggiuntive per i client in questo gruppo di limiti, passare alla scheda **Opzioni**. Per altre informazioni, vedere [Opzioni del gruppo di limiti per download peer](boundary-groups.md#bkmk_bgoptions).

- **Consenti i download peer in questo gruppo di limiti**: Questa opzione è attivata per impostazione predefinita. Il punto di gestione fornisce ai client un elenco di posizioni del contenuto che include le origini peer.  

    - **Durante i download peer, usa solo i peer entro la stessa subnet**: Questa impostazione dipende da quella precedente. Se si abilita questa opzione, il punto di gestione include nell'elenco delle posizioni del contenuto solo le origini peer incluse nella stessa subnet del client.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a> Configurare un sito di fallback per l'assegnazione sito automatica  

Se i client non si trovano in un gruppo di limiti con un sito assegnato, assegnarli al sito durante l'installazione.

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2.  Nella scheda **Home** della barra multifunzione selezionare **Impostazioni gerarchia** nel gruppo **Siti**.  

3.  Nella scheda **Generale** selezionare la casella di controllo **Utilizza sito di fallback**. Selezionare quindi un sito nell'elenco a discesa **Sito di fallback**.  

4.  Selezionare **OK** per salvare la configurazione.  

Per altre informazioni, vedere [Assegnazione sito](boundary-groups.md#site-assignment).


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a> Abilitare l'uso dei punti di gestione preferiti  

Per altre informazioni, vedere [Punti di gestione preferiti](boundary-groups.md#bkmk_preferred).

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Nella scheda **Home** della barra multifunzione selezionare **Impostazioni gerarchia** nel gruppo **Siti**.  

3. Nella scheda **Generale** selezionare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**.  

4. Selezionare **OK** per salvare la configurazione.  

