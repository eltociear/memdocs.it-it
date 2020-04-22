---
title: Creare query
titleSuffix: Configuration Manager
description: Questo argomento illustra come creare e importare query in Configuration Manager. Include query di esempio e suggerimenti.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05b77fa181da67858c30f48fc8045c20384953ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703449"
---
# <a name="create-queries-in-configuration-manager"></a>Creare query in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo descrive come creare e importare query in Configuration Manager.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a> Creare una query  
 Usare questa procedura per creare una query in Configuration Manager.  

1.  Nella console di Configuration Manager selezionare **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** selezionare **Query**. Nella scheda **Home** selezionare **Crea query** nel gruppo **Crea**.  

3.  Nella scheda **Generale** della **Creazione guidata query**specificare un nome univoco e un commento facoltativo per la query.  

4.  Per importare una query esistente da usare come modello per la nuova query, selezionare **Importa istruzione query**. Nella finestra di dialogo **Sfoglia query**, selezionare una query da importare e quindi selezionare **OK**.  

5.  Nell'elenco **Tipo oggetto** selezionare il tipo di oggetto che si vuole che la query restituisca. Nella tabella seguente vengono descritti alcuni esempi dei tipi di oggetto che è possibile cercare:  

    |Tipo di oggetto|Descrizione|  
    |-----------------|-----------------|  
    |**Risorsa di sistema**|Usare questo tipo di oggetto per cercare attributi di sistema standard, ad esempio il nome NetBIOS di un dispositivo, la versione del client, l'indirizzo IP del client e informazioni su Active Directory Domain Services.|  
    |**Risorsa utente**|Usare questo tipo di oggetto per cercare informazioni utente standard, ad esempio i nomi utente, i nomi di gruppi di utenti e i nomi dei gruppi di sicurezza.|  
    |**Distribuzione**|Usare questo tipo di oggetto per cercare gli attributi standard di una distribuzione, ad esempio il nome della distribuzione, la pianificazione e la raccolta in cui è stata distribuita.|  

6.  Selezionare **Modifica istruzione query** per aprire la finestra di dialogo &lt;Nome query\> **Proprietà istruzione**.  

7.  Nella scheda **Generale** della finestra di dialogo &lt;Nome query\> **Proprietà istruzione** specificare gli attributi restituiti dalla query e la relativa modalità di visualizzazione. Selezionare l'icona **Nuovo** per aggiungere un nuovo attributo. È anche possibile selezionare **Mostra linguaggio query** per immettere o modificare la query direttamente in WMI Query Language (WQL). Per esempi di query WMI, vedere la sezione [Query WQL di esempio](#BKMK_Example) in questo articolo.  

    > [!TIP]  
    > È possibile usare la documentazione di riferimento seguente per costruire le query WQL:  
    >   
    > -   [WQL (SQL per WMI)](https://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Clausola WHERE](https://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operatori WQL](https://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Nella scheda **Criteri** della finestra di dialogo **Proprietà istruzione** &lt;nome query\> specificare i criteri usati per definire i risultati della query. Ad esempio, è possibile restituire solo le risorse con un codice di sito **XYZ**. È possibile configurare più criteri per una query.  

    > [!IMPORTANT]  
    > Se si crea una query che non contiene alcun criterio, verranno restituiti tutti i dispositivi presenti nella raccolta **Tutti i sistemi** .  

9. Nella scheda **Join** della finestra di dialogo &lt;Nome query\> **Proprietà istruzione** è possibile combinare i dati di due attributi diversi nei risultati della query. Anche se Configuration Manager crea automaticamente join di query quando vengono selezionati attributi diversi per il risultato della query, nella scheda **Join** sono disponibili ulteriori opzioni avanzate. Configuration Manager supporta queste classi di attributo:  

    |Tipo di join|Descrizione|  
    |---------------|-----------------|  
    |Inner|Visualizza solo i risultati corrispondenti. Sempre usato per i join creati automaticamente.|  
    |Sinistra|Consente di visualizzare tutti i risultati per l'attributo di base e solo i risultati corrispondenti per l'attributo di join.|  
    |Destra|Visualizza tutti i risultati per l'attributo di join e solo i risultati corrispondenti per l'attributo di base.|  
    |Completo|Visualizza tutti i risultati sia per l'attributo di base che per l'attributo di join.|  

     Per altre informazioni su come usare le operazioni di join, vedere la documentazione di SQL Server.  

10. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà istruzione** &lt;nome query\>.  

11. Nella scheda **Generale** della **Creazione guidata query** specificare se i risultati della query non sono limitati ai membri di una raccolta, sono limitati ai membri di una raccolta specificata oppure se viene richiesta una raccolta ogni volta che viene eseguita la query.  

12. Completare la procedura guidata per creare la query. La nuova query viene visualizzata nel nodo **Query** nell'area di lavoro **Monitoraggio**.  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a> Importare una query  
 Usare questa procedura per importare una query in Configuration Manager. Per informazioni su come esportare le query, vedere [Come gestire le query](../../../core/servers/manage/manage-queries.md).  

1.  Nella console di Configuration Manager selezionare **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** selezionare **Query**. Nella scheda **Home**, nel gruppo **Crea**, selezionare **Importa oggetti**.  

3.  Nella pagina **Nome file MOF** dell'**Importazione guidata oggetti** selezionare **Sfoglia** per selezionare il file MOF (Managed Object Format) contenente la query da importare.  

4.  Esaminare le informazioni relative alla query da importare e quindi completare la procedura guidata. La nuova query viene visualizzata nel nodo **Query** nell'area di lavoro **Monitoraggio**.  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Questa sezione contiene query WQL di esempio che è possibile usare nella gerarchia o modificare per altri scopi. Per usare queste query, selezionare **Mostra linguaggio query** nella finestra di dialogo **Proprietà istruzione query**. Copiare e incollare la query nel campo **Istruzione query**.  

> [!TIP]  
> Usare il carattere jolly `%` per indicare qualsiasi stringa di caratteri. Ad esempio, `%Visio%` restituisce Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-10"></a>Computer che eseguono Windows 10

Usare la query seguente per restituire il nome NetBIOS e la versione del sistema operativo di tutti i computer che eseguono Windows 7.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computer con uno specifico pacchetto software installato  

Usare la query seguente per restituire il nome NetBIOS e il nome del pacchetto software di tutti i computer in cui è installato un pacchetto software specifico. Questo esempio restituisce tutti i computer con una versione di Microsoft Visio installata. Sostituire `Microsoft%Visio%` con il pacchetto software da cercare.  

> [!TIP]  
> Questa query cerca il pacchetto software usando i nomi visualizzati nell'elenco di programmi nel Pannello di controllo di Windows.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computer inclusi in una specifica unità organizzativa di Active Directory Domain Services

Usare la query seguente per restituire il nome NetBIOS e il nome dell'unità organizzativa di tutti i computer in un'unità organizzativa specificata. Sostituire il testo `OU Name` con il nome dell'unità organizzativa da cercare.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computer con un nome NetBIOS specifico

Usare la query seguente per restituire il nome NetBIOS di tutti i computer il cui nome inizia con una stringa specifica di caratteri. In questo esempio la query restituisce tutti i computer con un nome NetBIOS che inizia con `ABC`.  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Dispositivi di un tipo specifico

I tipi di dispositivo vengono archiviati nel database di Configuration Manager con la classe di risorse **sms_r_system** e il nome di attributo **AgentEdition**. Usare questa query per recuperare solo i dispositivi che corrispondono all'edizione dell'agente del tipo di dispositivo specificato:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Usare uno di questi valori per &lt;ID dispositivo\>:  

|Tipo di dispositivo|Valore di AgentEdition|  
|-----------------|---------------------------|  
|Computer desktop o portatile Windows|0|  
|Dispositivo Windows basato su ARM (che esegue Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Computer Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Intel System On Chip (SOC)|12|  
|Server UNIX e Linux|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> I valori non elencati in questa tabella sono associati a dispositivi che non sono più supportati.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Ad esempio, se si vuole restituire solo i computer Mac, usare questa query:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Passaggi successivi

[Come gestire le query](manage-queries.md)
