---
title: 'Scenario di esempio: distribuire client Windows Embedded'
titleSuffix: Configuration Manager
description: Descrizione di uno scenario di esempio per la distribuzione e la gestione dei client di Configuration Manager in dispositivi con Windows Embedded.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693869"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Scenario di esempio per la distribuzione e la gestione dei client di Configuration Manager in dispositivi con Windows Embedded

*Si applica a: Configuration Manager (Current Branch)*

Questo scenario illustra come è possibile gestire i dispositivi con Windows Embedded abilitati per i filtri di scrittura con System Center Configuration Manager. Se i dispositivi integrati non supportano i filtri di scrittura, funzionano come client standard di Configuration Manager e queste procedure non sono applicabili.  

Coho Vineyard & Winery sta per aprire un centro visite e deve installare dei chioschi multimediali con Windows Embedded per eseguire delle presentazioni interattive. L'edificio del nuovo centro visite non si trova vicino al reparto IT, per cui i chioschi devono essere gestiti in remoto. Oltre al software per eseguire le presentazioni, questi dispositivi dovranno eseguire un software di protezione antimalware aggiornato, in conformità con le politiche di sicurezza dell'azienda. I chioschi devono essere in funzione 7 giorni alla settimana senza tempi di inattività durante l'orario di apertura del centro visite.  

 Coho usa già Configuration Manager per gestire i dispositivi nella rete. Configuration Manager è configurato per eseguire Endpoint Protection e per installare gli aggiornamenti di software e applicazioni. Tuttavia, poiché il team IT non ha mai gestito dispositivi con Windows Embedded in precedenza, l'amministratore di Configuration Manager esegue un progetto pilota per gestire due chioschi multimediali che si trovano nella sala d'attesa della reception.   

 Per gestire questi dispositivi Windows Embedded, abilitati per i filtri di scrittura, l'amministratore di Configuration Manager esegue i passaggi seguenti per installare il client di Configuration Manager, proteggere il client usando Endpoint Protection e installare il software per la presentazione interattiva.  

1. L'amministratore di Configuration Manager legge in che modo i dispositivi Windows Embedded usano i filtri di scrittura e come Configuration Manager può semplificare questa operazione disabilitando e riabilitando automaticamente i filtri di scrittura per salvare in modo permanente un'installazione software.  

    Per altre informazioni, vedere [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Prima di installare il client di Configuration Manager, l'amministratore crea una nuova raccolta dispositivi basata su query per i dispositivi Windows Embedded. Poiché la società usa formati di denominazione standard per identificare i computer, l'amministratore può identificare i dispositivi Windows Embedded con le prime sei lettere del nome computer: **WEMDVC**. Per creare la raccolta, l'amministratore usa la query WQL seguente: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

    Questa raccolta consente all'amministratore di gestire i dispositivi Windows Embedded con opzioni di configurazione diverse di altri dispositivi. L'amministratore userà questa raccolta per controllare i riavvii, distribuire Endpoint Protection con impostazioni client e distribuire l'applicazione per le presentazioni interattive.  

    Vedere [Come creare le raccolte](../../../core/clients/manage/collections/create-collections.md).  

3. L'amministratore configura una finestra di manutenzione per la raccolta, per assicurarsi che i riavvii eventualmente richiesti per l'installazione dell'applicazione per le presentazioni e per eventuali aggiornamenti non si verifichino durante gli orari di apertura del centro visite. Gli orari di apertura saranno dalle 9:00 alle 18:00, da lunedì a domenica. L'amministratore configura l'attivazione della finestra di manutenzione ogni giorno, dalle 18:30 alle 06:00.  

4. Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. L'amministratore configura quindi un'impostazione personalizzata per il client dei dispositivi che consente di installare il client di Endpoint Protection selezionando **Sì** per le impostazioni che seguono e quindi distribuisce l'impostazione client personalizzata nella raccolta dispositivi Windows Embedded:  

   - **Installare il client Endpoint Protection nei computer client**  

   - **Per i dispositivi con Windows Embedded con filtri di scrittura, confermare l'installazione del client di Endpoint Protection (richiesto riavvio)**  

   - **Consentire l'installazione del client di Endpoint Protection e i riavvii al di fuori delle finestre di manutenzione**  

     Quando viene installato il client di Configuration Manager, queste impostazioni installano il client di Endpoint Protection, garantendo cosi che sarà salvato in modo permanente nel sistema operativo come parte dell'installazione e non solo scritto sull'overlay. I criteri di sicurezza della società richiedono che il software antimalware sia sempre installato e l'amministratore non vuole rischiare che i chioschi multimediali rimangano senza protezione anche solo per un breve periodo di tempo quando si riavviano.  

   > [!NOTE]  
   >  I riavvii richiesti per installare il client di Endpoint Protection avvengono solo una volta, che avviene durante l'installazione dei dispositivi e prima che il centro visite sia operativo. Diversamente dalla distribuzione periodica degli aggiornamenti di definizioni per applicazioni o software, il client di Endpoint Protection sarà installato nuovamente nello stesso dispositivo quando l'azienda eseguirà l'aggiornamento alla nuova versione di Configuration Manager.  

    Per altre informazioni, vedere [Configurazione di Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. Dopo aver definito le impostazioni di configurazione per il client, l'amministratore prepara l'installazione dei client di Configuration Manager. Prima di installare i client, l'amministratore deve disabilitare manualmente il filtro di scrittura nei dispositivi Windows Embedded. Legge quindi la documentazione OEM che accompagna i chioschi multimediali e segue le istruzioni per disabilitare i filtri di scrittura.  

    L'amministratore rinomina ogni dispositivo in modo che usi il formato di denominazione standard della società e quindi installa il client manualmente eseguendo CCMSetup da un'unità mappata che contiene i file di origine del client tramite il comando seguente: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    Questo comando installa il client, assegna il client al punto di gestione che ha l'intranet FQDN di **mpserver.cohovineyardandwinery.com**e assegna il client al sito primario denominato **CO1**.  

    L'amministratore sa che l'installazione dei client e l'invio dello stato di questi al sito richiede sempre un certo tempo. Attende quindi prima di verificare che i client siano stati installati correttamente, che siano stati assegnati al sito e che compaiano come client nella raccolta creata per i dispositivi Windows Embedded.  

    Per maggiore sicurezza, l'amministratore controlla le proprietà di Configuration Manager nel Pannello di controllo dei dispositivi e le confronta con quelle dei computer Windows standard gestiti dal sito. Ad esempio, nella scheda **Componenti** , l' **Agente di inventario hardware** visualizza **Abilitato**e nella scheda **Azioni** , sono disponibili 11 azioni che includono **Ciclo di valutazione distribuzione applicazione** e **Ciclo di recupero dati di rilevamento**.  

    Con la certezza che i client sono stati installati e assegnati e che ricevono i criteri client dal punto di gestione, l'amministratore abilita manualmente i filtri di scrittura seguendo le istruzioni dell'OEM.  

    Per altre informazioni, vedere:  

   -   [Come distribuire i client nei computer Windows](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Come assegnare i client a un sito](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Il client di Configuration Manager è ora configurato nei dispositivi Windows Embedded e l'amministratore verifica di poterli gestire nello stesso modo in cui gestisce i client Windows standard. Dalla console di Configuration Manager può, ad esempio, gestire i client in remoto tramite il controllo remoto, avviare criteri client e visualizzare le proprietà dei client e l'inventario hardware.  

    Questi dispositivi fanno parte di un dominio di Active Directory. L'amministratore non deve quindi approvarli manualmente come client attendibili e ne conferma l'approvazione dalla console di Configuration Manager.  

    Per altre informazioni, vedere [Come gestire i client](../../../core/clients/manage/manage-clients.md).  

8. Per installare il software per le presentazioni interattive, l'amministratore esegue la **Distribuzione guidata del software** e configura un'applicazione richiesta. Nella sezione **Gestione filtri di scrittura per dispositivi con Windows Embedded** della pagina **Esperienza utente** della procedura guidata accetta l'opzione predefinita **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** .  

    L'amministratore mantiene questa opzione predefinita per i filtri di scrittura per assicurarsi che l'applicazione permanga dopo un riavvio e sia quindi sempre disponibile per i visitatori che usano i chioschi multimediali. La finestra di manutenzione quotidiana fornisce un periodo di tempo sicuro durante si possono effettuare i riavvii per l'installazione ed eventuali aggiornamenti.  

    L'amministratore distribuisce l'applicazione nella raccolta dispositivi Windows Embedded.  

    Per altre informazioni, vedere [Come distribuire applicazioni in Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Per configurare gli aggiornamenti delle definizioni per Endpoint Protection, l'amministratore usa gli aggiornamenti software ed esegue la Creazione guidata delle regole di distribuzione automatica. Seleziona il modello **Aggiornamenti della definizione** per il popolamento preliminare della procedura guidata con le impostazioni appropriate per Endpoint Protection.  

     Queste impostazioni includono i seguenti elementi nella pagina **Esperienza utente** della procedura guidata:  

   - **Comportamento scadenza**: la casella di controllo **Installazione software** non è selezionata.  

   - **Gestione filtri di scrittura per dispositivi con Windows Embedded**: la casella di controllo **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** non è selezionata.  

     L'amministratore mantiene queste impostazioni predefinite. Insieme, queste due opzioni con questa configurazione consentono l'installazione di tutte le definizioni di aggiornamento software per Endpoint Protection nella sovrapposizione durante il giorno e nessuna attesa per l'installazione e l'invio durante la finestra di manutenzione. Questa configurazione soddisfa al meglio i criteri di sicurezza dell'azienda per i computer con protezione antimalware aggiornata.  

     > [!NOTE]  
     >  A differenza delle installazioni software per applicazioni, le definizioni di aggiornamento software per Endpoint Protection possono verificarsi molto spesso, anche più volte al giorno. Sono spesso file di piccole dimensioni. Per questi tipi di distribuzione relativi alla sicurezza, può essere spesso utile installare sempre nella sovrapposizione piuttosto che aspettare fino alla finestra di manutenzione. Il client di Configuration Manager reinstallerà rapidamente gli aggiornamenti delle definizioni software se il dispositivo si riavvia, perché questa azione avvia un controllo di valutazione e non aspetta fino alla valutazione pianificata successiva.  

     L'amministratore seleziona la raccolta dispositivi Windows Embedded per la regola di distribuzione automatica.  

     Per ulteriori informazioni, vedere  
               Passaggio 3: Configurare gli aggiornamenti software di Configuration Manager per inviare gli aggiornamenti delle definizioni ai computer client in [Configurazione di Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. L'amministratore decide di configurare un'attività di manutenzione che esegue periodicamente il commit di tutte le modifiche alla sovrimpressione. Questa attività serve per supportare le definizioni di aggiornamento software e per ridurre il numero di aggiornamenti che si sono accumulati e che devono essere installati di nuovo ogni volta che il dispositivo si riavvia. Nella sua esperienza, in questo modo i programmi antimalware funzionano in modo più efficiente.  

    > [!NOTE]  
    >  Queste definizioni di aggiornamento software verrebbero automaticamente inviate al'immagine se i dispositivi con Windows Embedded eseguissero un'altra attività di gestione che supportasse l'invio delle modifiche. Ad esempio, anche l'installazione di una nuova versione del software per le presentazioni interattivi invierebbe le modifiche per le definizioni di aggiornamento software. In alternativa, anche l'installazione degli aggiornamenti software standard in ogni mese di installazione durante la finestra di manutenzione potrebbe inviare le modifiche per le definizioni di aggiornamento software. Tuttavia, in questo scenario in cui non vengono eseguiti gli aggiornamenti software standard e il software per le presentazioni interattive probabilmente non viene aggiornato molto spesso, potrebbe passare dei mesi prima che gli aggiornamenti delle definizioni software vengano inviati automaticamente all'immagine.  

     L'amministratore crea prima una sequenza di attività personalizzata che non ha altre impostazioni che il nome. Esegue la Creazione guidata della sequenza di attività:  

    1. Nella pagina **Crea una nuova sequenza attività** l'amministratore seleziona **Crea una nuova sequenza attività personalizzata** e quindi fa clic su **Avanti**.  

    2. Nella pagina **Informazioni sequenza di attività** l'amministratore immette **Maintenance task to commit changes on embedded devices** (Attività di manutenzione per il commit delle modifiche a dispositivi Windows Embedded) come nome della sequenza di attività e quindi fa clic su **Avanti**.  

    3. Nella pagina **Riepilogo** l'amministratore seleziona **Avanti** e completa la procedura guidata.  

       Distribuisce quindi la sequenza di attività personalizzata nella raccolta dispositivi Windows Embedded e configura la pianificazione per l'esecuzione ogni mese. Nell'ambito delle impostazioni di distribuzione, seleziona la casella di controllo **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** per rendere permanenti le modifiche dopo un riavvio. Per configurare questa distribuzione, l'amministratore seleziona la sequenza di attività personalizzata che ha appena creato e quindi nel gruppo **Distribuzione** della scheda **Home** fa clic su **Distribuisci** per avviare la Distribuzione guidata del software:  

    4. Nella pagina **Generale** l'amministratore seleziona la raccolta dispositivi Windows Embedded e quindi fa clic su **Avanti**.  

    5. Nella pagina **Impostazioni distribuzione** seleziona come **Scopo** l'opzione **Richiesto** e quindi fa clic su **Avanti**.  

    6. Nella pagina **Pianificazione** fa clic su **Nuovo** per indicare una pianificazione settimanale durante la finestra di manutenzione e quindi fa clic su **Avanti**.  

    7. L'amministratore completa la procedura guidata senza altre modifiche.  

       Per ulteriori informazioni, vedere  
                 [Gestire le sequenze di attività per automatizzare le attività](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Per l'esecuzione automatica dei chioschi multimediali, l'amministratore scrive uno script per configurare i dispositivi con le impostazioni seguenti:  

    - Accedere automaticamente, utilizzando un account guest senza password.  

    - Eseguire automaticamente il software per la presentazione interattiva all'avvio.  

      L'amministratore usa pacchetti e programmi per distribuire questo script nella raccolta dispositivi Windows Embedded. Quando esegue la Distribuzione guidata del software, l'amministratore seleziona di nuovo la casella di controllo **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** per rendere permanenti le modifiche dopo un riavvio.  

      Per altre informazioni, vedere [Packages and programs](../../../apps/deploy-use/packages-and-programs.md) (Pacchetti e programmi).  

12. Il mattino seguente, l'amministratore controlla i dispositivi Windows Embedded. Verifica quanto segue:  

    - Il chiosco viene automaticamente connesso utilizzando l'account guest.  

    - Il software di presentazione interattiva è in esecuzione.  

    - Il client Endpoint Protection è installato e dispone delle definizioni di aggiornamento software più recenti.  

    - Il dispositivo è stato riavviato durante la finestra di manutenzione.  

      Per altre informazioni, vedere:  

    - [Come monitorare Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Monitorare le applicazioni con Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. L'amministratore esegue il monitoraggio dei chioschi multimediali e ne segnala la corretta gestione al manager. Di conseguenza, vengono ordinati 20 chioschi per il centro visite.  

     Per evitare di dover installare manualmente il client di Configuration Manager, che richiede la disabilitazione manuale e quindi la riabilitazione dei filtri di scrittura, l'amministratore verifica che l'ordine includa un'immagine personalizzata già comprensiva dell'installazione e dell'assegnazione del sito del client di Configuration Manager. Inoltre, i dispositivi vengono denominati in base al formato dei nomi aziendali.  

     I chioschi vengono consegnati al centro visitate una settimana prima dell'apertura. Durante questo periodo, i chioschi vengono connessi alla rete, tutta la relativa gestione dei dispositivi è automatica e non sono necessari amministratori locali. L'amministratore verifica che i chioschi funzionino come richiesto:  

    -   I client nei chioschi completano l'assegnazione del sito e scaricano la chiave radice attendibile da Servizi di dominio Active Directory.  

    -   I client nei chioschi vengono automaticamente aggiunti alla raccolta di dispositivi Windows Embedded e vengono configurati con la finestra di manutenzione.  

    -   Il client Endpoint Protection è installato e dispone delle definizioni di aggiornamento software più recenti per la protezione antimalware.  

    -   Il software di presentazione interattiva è installato e viene eseguito automaticamente, pronto per i visitatori.  

14. Al termine dell'installazione iniziale eventuali riavvii che potrebbero essere necessari per gli aggiornamenti si verificano solo quando il centro visite è chiuso.  
