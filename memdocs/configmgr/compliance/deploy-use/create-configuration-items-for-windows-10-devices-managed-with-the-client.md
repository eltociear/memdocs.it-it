---
title: Creare elementi di configurazione per Windows 10
titleSuffix: Configuration Manager
description: Per gestire le impostazioni dei computer Windows 10 gestiti dal client di Configuration Manager, usare l'elemento di configurazione di Windows 10.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692539"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Creare elementi di configurazione per dispositivi Windows 10

Usare l'elemento di configurazione **Windows 10** in Configuration Manager per gestire le impostazioni dei computer che eseguono Windows 10 gestiti dal client di Configuration Manager.  
  
> [!IMPORTANT]  
>  Se in questa versione è stata creata un'impostazione **Password** come parte di un elemento di configurazione del tipo **Windows 10** (per un dispositivo gestito con il client di Configuration Manager), tenere presente il seguente problema. Se l'impostazione non esiste già o non è stata configurata nel dispositivo Windows 10, viene erroneamente valutata come conforme.  
>   
>  Come soluzione alternativa, quando si crea un'impostazione per questi dispositivi assicurarsi che sia selezionata l'opzione **Monitora e aggiorna impostazioni non conformi** nelle pagine delle impostazioni della Creazione guidata dell'elemento di configurazione. Inoltre, quando si distribuisce una linea di base di configurazione contenente un elemento di configurazione di Windows 10 con impostazioni di password al suo interno, selezionare **Monitora e aggiorna le regole non conformi, se supportato**. Effettuare questa selezione nella finestra di dialogo Distribuisci linee di base di configurazione. L'uso di questa soluzione alternativa consente di monitorare l'impostazione e di correggerla se risulta non conforme. Dopo la correzione, l'impostazione viene correttamente segnalata come **Conforme**, a meno che non venga rilevato un problema, nel qual caso verrà segnalata come **Errore**.  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Per creare un elemento di configurazione Windows 10  
  
1. Nella console di Configuration Manager selezionare **Asset e conformità**.  
  
2. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e quindi selezionare **Elementi di configurazione**.  
  
3. Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea elemento di configurazione**.  
  
4. Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione** specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  
  
5. In **Specificare il tipo di elemento di configurazione da creare**selezionare **Windows 10**.  
  
6. Se si creano e assegnano categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager, selezionare **Categorie**.  
  
7. Nella pagina **Piattaforme supportate** della procedura guidata selezionare le piattaforme Windows 10 specifiche che valuteranno l'elemento di configurazione.  
  
8. Nella pagina **Impostazioni dispositivo** della creazione guidata selezionare il gruppo di impostazioni da configurare. Per dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione di Windows 10](#BKMK_Ref) in questo articolo. Selezionare quindi **Avanti**.  
  
   > [!TIP]  
   >  Se l'impostazione da modificare non è inclusa nell'elenco, selezionare la casella di controllo **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  
  
9. In ogni pagina di impostazioni configurare le impostazioni necessarie e specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  
  
10. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità da segnalare quando viene trovato un elemento di configurazione non conforme:  
  
    -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  
  
    -   **Informazioni**: I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  
  
    -   **Avviso**: I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  
  
    -   **Errore critico**: I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  
  
    -   **Errore critico con evento**: I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  
  
11. Nella pagina **Applicabilità piattaforma** della creazione guidata, verificare le eventuali impostazioni non compatibili con le piattaforme supportate selezionate in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  
  
    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  
  
12. Completare la procedura guidata.  
  
    È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Password  
  
|Impostazione|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|Lunghezza minima della password.|  
|**Scadenza password in giorni**|Numero di giorni prima che sia necessario modificare la password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password precedenti.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati da un dispositivo**|Cancella il dispositivo se l'accesso non riesce per il numero di volte indicato.|  
|**Tempo di inattività prima del blocco del dispositivo**|Specifica quanti minuti il dispositivo deve restare inattivo prima che venga bloccato automaticamente.|  
|**Complessità password**|Scegliere se è possibile specificare un PIN, ad esempio "1234", o se è necessario fornire una password complessa.|
|**Numero di set di caratteri complessi richiesti nella password**|Se è stata scelta una password **complessa**, usare questa impostazione per configurare il numero di set di caratteri complessi necessari. Per ottenere una password complessa, l'impostazione deve essere impostata almeno su **3**, ovvero sono necessari lettere e numeri. Selezionare **4** per imporre una password che richiede anche caratteri speciali, ad esempio **(% $** .<br>(solo Windows 10)  |
  
###  <a name="device"></a>Dispositivo  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Bluetooth**|Consente l'uso della funzionalità Bluetooth nel dispositivo.|  
  
### <a name="cloud"></a>Cloud  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Sincronizzazione impostazioni**|Consente la sincronizzazione delle impostazioni tra i dispositivi.|  
|**Sincronizzazione credenziali**|Consente la sincronizzazione delle credenziali tra i dispositivi.|  
|**Sincronizzazione delle impostazioni con connessione a consumo**|Consente la sincronizzazione delle impostazioni quando la connessione a Internet è a consumo.|  
  
### <a name="roaming"></a>Roaming  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Roaming dati**|Consente il roaming tra reti per l'accesso ai dati.|  
  
### <a name="encryption"></a>Crittografia  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file nel dispositivo.|  
  
### <a name="system-security"></a>Protezione del sistema  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Controllo dell'account utente**|Configura la modalità di funzionamento del controllo account utente di Windows nel dispositivo.<br />Ad esempio, è possibile disabilitare questa funzione o impostare il livello in corrispondenza del quale l'utente riceve una notifica.|  
|**Firewall di rete**|Attiva o disattiva Windows Firewall.|  
|**SmartScreen**|Attiva o disattiva Windows SmartScreen.|  
|**Protezione da virus**|Richiede che sia installato e configurato software antivirus.|  
|**Le firme per la protezione da virus sono aggiornate**|Richiede che i file di firma per il software antivirus nel dispositivo siano aggiornati.|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

Con l'aumento dei dispositivi personali nell'organizzazione, aumenta anche il rischio di perdita accidentale dei dati attraverso le app e i servizi, ad esempio posta elettronica, social media e cloud pubblico. Si trovano al di fuori del controllo dell'organizzazione. Ad esempio, quando un dipendente:

- Invia le immagini di progettazione più recenti dal proprio account di posta elettronica personale.
- Copia e incolla le informazioni sul prodotto in un tweet.
- Salva un report sulle vendite in corso nella relativa archiviazione nel cloud pubblico.

Windows Information Protection (WIP), in precedenza noto come protezione dei dati aziendali, offre protezione da questa potenziale perdita di dati senza interferire con l'esperienza del dipendente. WIP consente anche di proteggere le app e i dati aziendali da perdite di dati accidentali su dispositivi di proprietà dell'azienda e dispositivi personali che i dipendenti portano al lavoro. WIP non richiede modifiche dell'ambiente o di altre app.

Gli elementi di configurazione di Windows Information Protection in Configuration Manager gestiscono quanto segue:

- Elenco delle app protette da WIP
- Percorsi di rete aziendali
- Livello di protezione
- Impostazioni di crittografia
  
Per informazioni sulle modalità di configurazione di WIP con Configuration Manager, vedere:

- [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Creare e distribuire un criterio di Windows Information Protection (WIP) con Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Limitazioni nell'uso di Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Vedere anche  
[Elementi di configurazione per dispositivi gestiti con il client di Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)
