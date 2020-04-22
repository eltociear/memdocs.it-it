---
title: Creare e applicare combinazioni per il risparmio di energia
titleSuffix: Configuration Manager
description: Creare e applicare combinazioni per il risparmio di energia in Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: aca0f3078c046bbc988a289f548ac11e26747088
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696589"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Come creare e applicare combinazioni per il risparmio di energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le funzionalità di risparmio energia in Configuration Manager consentono di applicare le combinazioni per il risparmio di energia fornite con Configuration Manager a raccolte di computer nella gerarchia oppure di creare combinazioni per il risparmio di energia personalizzate. Usare la procedura in questo argomento per applicare una combinazione per il risparmio di energia predefinita o personalizzata ai computer.  

> [!IMPORTANT]  
>  È possibile applicare le combinazioni per il risparmio di energia di Configuration Manager solo a raccolte di dispositivi.  

 Se un computer è un membro di più raccolte, ognuna con combinazioni per il risparmio di energia diverse, verranno eseguite le azioni seguenti:  

- Combinazione per il risparmio di energia: se a un computer sono applicati più valori per le impostazioni di risparmio energia, viene usato il valore meno restrittivo.  

- Ora riattivazione: se a un computer desktop vengono applicate più ore di riattivazione, viene usata l'ora più vicina alla mezzanotte.  

  Usare il report **Computer con più combinazioni per il risparmio di energia** per visualizzare tutti i computer a cui sono applicate più combinazioni di risparmio di energia. In questo modo è più facile individuare i computer con conflitti. Per altre informazioni sui report di risparmio energia, vedere [Come monitorare e pianificare il risparmio energia in Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Le impostazioni di risparmio energia configurate tramite Criteri di gruppo di Windows avranno la priorità sulle impostazioni configurate dalle funzionalità di risparmio energia di Configuration Manager.  

 Usare la procedura seguente per creare e applicare una combinazione per il risparmio di energia di Configuration Manager.  

### <a name="to-create-and-apply-a-power-plan"></a>Per creare e applicare una combinazione per il risparmio di energia  

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3. Nell'elenco **Raccolte dispositivi** fare clic sulla raccolta a cui si vogliono applicare le impostazioni di risparmio energia e quindi nel gruppo **Proprietà** della scheda **Home** fare clic su **Proprietà**.  

4. Nella scheda **Risparmio energia** della finestra di dialogo **Proprietà**<em><nome raccolta\></em> selezionare **Specifica impostazioni di risparmio energia per questa raccolta**.  

   > [!NOTE]  
   >  È anche possibile fare clic su **Sfoglia** e quindi copiare le impostazioni di risparmio energia da una raccolta selezionata alla raccolta selezionata.  

5. Nei campi **Inizio** e **Fine** specificare l'ora di inizio e di fine per le ore di punta (o lavorative).  

6. Abilitare **Ora riattivazione (computer desktop)** per specificare l'ora in cui un computer desktop verrà riattivato dalla modalità di sospensione o ibernazione per installare gli aggiornamenti pianificati o per installazioni di software.  

   > [!IMPORTANT]  
   >  Le funzionalità di risparmio energia usano l'ora di riattivazione di Windows interna per riattivare i computer dalla modalità di sospensione o ibernazione. Le impostazioni dell'ora di riattivazione non vengono applicate ai computer portatili per evitare scenari in cui la riattivazione potrebbe essere eseguita quando non sono collegati alla rete elettrica. L'ora di riattivazione è casuale e i computer verranno riattivati per un periodo di un'ora dall'ora di attivazione specificata.  

7. Se si vuole configurare una combinazione per il risparmio di energia personalizzata per le ore di punta (o lavorative), selezionare **Personalizzazione ore di punta (Configuration Manager)** nell'elenco a discesa **Piano ore di punta** e quindi fare clic su **Modifica**. Se si vuole configurare una combinazione per il risparmio di energia personalizzata per le ore non di punta (o non lavorative), selezionare **Personalizzazione fuori ore di punta (Configuration Manager)** nell'elenco a discesa **Piano fuori ore di punta** e quindi fare clic su **Modifica**.  

   > [!NOTE]  
   >  È possibile usare il report **Attività computer** per decidere le pianificazioni da usare per le ore di punta e non di punta quando si applicano combinazioni per il risparmio di energia a raccolte di computer. Per altre informazioni, vedere [How to monitor and plan for power management](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio energia ).  

    È anche possibile selezionare le combinazioni per il risparmio di energia predefinite, **Bilanciamento (Configuration Manager)** , **Prestazioni elevate (Configuration Manager)** e **Risparmio di energia (Configuration Manager)** , quindi fare clic su **Visualizza** per visualizzare le proprietà di ogni combinazione.  

   > [!NOTE]  
   >  Non è possibile modificare le combinazioni per il risparmio di energia predefinite.  

8. Nella finestra di dialogo **Proprietà**<em><Nome combinazione risparmio di energia\></em>  configurare le impostazioni seguenti:  

   -   **Nome:** specificare un nome per la combinazione per il risparmio di energia o usare il valore predefinito fornito.  

   -   **Descrizione:**  specificare una descrizione per la combinazione per il risparmio di energia o usare il valore predefinito fornito.  

   -   **Specificare le proprietà di questa combinazione per il risparmio di energia:** configurare le proprietà della combinazione per il risparmio di energia. Per disabilitare una proprietà, deselezionare la casella di controllo. Per informazioni sulle impostazioni disponibili, vedere [Available power management plan settings](#BKMK_Plans) in questo argomento.  

       > [!IMPORTANT]  
       >  Le impostazioni abilitate vengono applicate ai computer quando viene applicata la combinazione per il risparmio di energia. Se si deseleziona la casella di controllo di un'impostazione di risparmio energia, il valore nel computer client non viene modificato quando viene applicata la combinazione per il risparmio di energia. La deselezione di una casella di controllo non consente di ripristinare l'impostazione di risparmio energia sul valore precedente prima dell'applicazione di una combinazione per il risparmio di energia.  

9. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà**<em><Nome combinazione risparmio energia\></em>.  

10. Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni** <em><nome raccolta\></em> e applicare la combinazione per il risparmio di energia.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 Nella tabella seguente sono elencate le impostazioni di risparmio energia disponibili in Configuration Manager. È possibile configurare impostazioni distinte per quando il computer è alimentato da rete elettrica o alimentato a batteria. A seconda della versione di Windows in uso, alcune impostazioni potrebbero non essere configurabili.  

> [!NOTE]  
>  Le impostazioni di risparmio energia che non vengono configurate manterranno il valore corrente nei computer client.  

|Name|Descrizione|  
|----------|-----------------|  
|**Disattiva schermo dopo (minuti)**|Specifica per quanto tempo, in minuti, il computer deve essere inattivo prima che venga disattivato lo schermo. Specificare il valore **0** se non si vuole disattivare lo schermo.|  
|**Entra in sospensione dopo (minuti)**|Specifica per quanto tempo, in minuti, il computer deve essere inattivo prima che venga attivata la sospensione. Specificare il valore **0** se non si vuole attivare lo stato di sospensione per il computer.|  
|**Richiedi password alla riattivazione**|Un valore **Sì** o **No** specifica se una password è necessaria per sbloccare il computer quando si accede alla riattivazione dalla sospensione.|  
|**Azione pulsante di alimentazione**|Specifica l'azione da eseguire quando viene premuto il pulsante di alimentazione del computer. Valori possibili: **Non eseguire alcuna operazione**, **Sospendi**, **Iberna** e **Arresta**.|  
|**Pulsante di alimentazione menu Start**|Specifica l'azione che si verifica quando si preme il pulsante di alimentazione nel menu **Start** del computer. Valori possibili: **Sospendi**, **Iberna** e **Arresta**.|  
|**Azione pulsante di sospensione**|Specifica l'azione che si verifica quando si preme il pulsante **Sospendi** del computer. Valori possibili: **Non eseguire alcuna operazione**, **Sospendi**, **Iberna** e **Arresta**.|  
|**Azione chiusura coperchio**|Specifica l'azione che si verifica quando l'utente chiude il coperchio di un computer portatile. Valori possibili: **Non eseguire alcuna operazione**, **Sospendi**, **Iberna** e **Arresta**.|  
|**Disattiva disco rigido dopo (minuti)**|Specifica per quanto tempo, in minuti, il disco rigido del computer deve essere inattivo prima che venga disattivato. Specificare il valore **0** se non si vuole disattivare il disco rigido del computer.|  
|**Metti in stato di ibernazione dopo (minuti)**|Specifica per quanto tempo, in minuti, il computer deve essere inattivo prima che venga attivato lo stato di ibernazione. Specificare il valore **0** se non si vuole attivare lo stato di ibernazione per il computer.|  
|**Azione per batteria in esaurimento**|Specifica l'azione che si verifica quando la batteria del computer raggiunge il livello di notifica di batteria in esaurimento specificato. Valori possibili: **Non eseguire alcuna operazione**, **Sospendi**, **Iberna** e **Arresta**.|  
|**Azione per batteria quasi scarica**|Specifica l'azione da eseguita quando della batteria raggiunge il livello di notifica di batteria specificato. Quando è attiva l'impostazione **A batteria**, i valori possibili sono **Sospendi**, **Iberna** e **Arresta**. Quando invece è attiva **Alimentazione da rete elettrica**, i valori possibili sono **Non eseguire alcuna operazione**, **Sospendi**, **Iberna** e **Arresta**.|  
|**Consenti sospensione ibrida**|Impostando l'opzione su **Disattivato** o **Attivato** si specifica se Windows salva un file di ibernazione quando entra in stato di sospensione, che può essere usato per ripristinare lo stato del computer in caso di interruzione dell'alimentazione mentre è in stato di sospensione.<br /><br /> La sospensione ibrida è progettata per i computer desktop e, per impostazione predefinita, non è abilitata nei computer portatili. Nei computer che eseguono Windows 7 l'abilitazione della sospensione ibrida disabilita la funzionalità di ibernazione.|  
|**Consentire lo stato di standby durante la sospensione dell'azione**|Impostando l'opzione su **Disattivato** o **Attivato** si consente lo stato di standby per il computer, che consuma un po' di energia, ma permette una riattivazione più veloce del computer. Se questa impostazione è impostata su **Disattivato**, il computer può solo entrare in stato ibernazione o essere spento.|  
|**Inattività richiesta prima della sospensione (%)**|Specifica la percentuale del tempo di inattività per il tempo del processore del computer, prima che il computer possa entrare in stato di sospensione. Nei computer che eseguono Windows 7, questo valore è sempre impostato su **0**.|  
|**Abilita timer riattivazione Windows per computer desktop**|Impostando questa opzione su **Abilitato** o **Disabilitato** è possibile abilitare il timer di Windows integrato usato dalla funzionalità di risparmio energia per riattivare un computer desktop. Quando un computer desktop è riattivato mediante il timer di riattivazione Windows, rimarrà attivo per 10 minuti per impostazione predefinita per consentire l'ora del computer per installare gli aggiornamenti o per ricevere i criteri.<br /><br /> I timer di riattivazione non sono supportati nei computer portatili per evitare scenari in cui la riattivazione potrebbe essere eseguita quando non sono collegati alla rete elettrica.|  
