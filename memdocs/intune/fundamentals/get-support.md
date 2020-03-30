---
title: Come ottenere supporto per Microsoft Intune
titleSuffix: Microsoft Intune
description: Ottenere supporto online e per telefono per Microsoft Intune a pagamento e per le sottoscrizioni di prova.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7fc95d17-098e-4da5-8a09-a96476569dd9
ms.reviewer: crisk
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf732907b9123dfe8cbd72970556ecfbb5380733
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086040"
---
# <a name="how-to-get-support-for-microsoft-intune"></a>Come ottenere supporto per Microsoft Intune

Microsoft offre supporto globale tecnico e per la prevendita, la fatturazione e le sottoscrizioni di Microsoft Intune. Il supporto è disponibile sia online che telefonicamente per le sottoscrizioni a pagamento e di valutazione. Il supporto tecnico online è disponibile in lingua inglese e giapponese. Il supporto telefonico e il supporto online per la fatturazione sono disponibili anche in altre lingue.

L'amministratore di Intune può usare l'opzione **Guida e supporto tecnico** per inviare un ticket di supporto online per Intune dal portale di Azure. Per creare e gestire una richiesta di assistenza, l'account deve avere un ruolo di Azure Active Directory (Azure AD) che includa l'*azione* **microsoft.office365.supportTickets**. Per informazioni sui ruoli e le autorizzazioni di Azure AD necessari per creare un ticket di supporto, vedere [Autorizzazioni del ruolo di amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal).

>[!IMPORTANT]
> Per il supporto tecnico dei prodotti di terze parti usati con Intune, come ad esempio Saaswedo, Cisco o Lookout, contattare prima il fornitore del prodotto. Prima di aprire una richiesta di supporto per Intune, verificare che l'altro prodotto sia stato configurato correttamente.
>
> Per informazioni sulla risoluzione dei problemi relativi a Microsoft Intune, vedere la [sezione Risoluzione dei problemi](help-desk-operators.md) della documentazione di Intune.

## <a name="help-and-support-experience"></a>Esperienza di Guida e supporto tecnico

L’esperienza di Guida e supporto tecnico per Intune è disponibile nell'[interfaccia di amministrazione di Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e in tutti i pannelli o tutte le pagine di Intune nel portale di Azure.

L'esperienza *Guida e supporto tecnico* è simile a quella offerta dall'[interfaccia di amministrazione di Microsoft 365](https://admin.microsoft.com/) e sostituisce l'opzione *Guida e supporto* precedente che rimane disponibile per altri servizi in Azure.

> [!TIP]
> A partire dal 18 novembre 2019, viene implementata nei tenant un'esperienza nella console aggiornata e semplificata per accedere a Guida e supporto tecnico. Se questo tipo di esperienza non è ancora disponibile per il proprio tenant, lo sarà presto.

### <a name="options-to-access-help-and-support"></a>Opzioni per accedere a Guida e supporto tecnico

Quando si usa un tenant appena creato per Intune, è possibile che *Guida e supporto tecnico* non si apra e un messaggio indichi che:

- *si è verificato un problema sconosciuto. In questo caso è necessario aggiornare la pagina e, se il problema persiste, creare un caso nell'[interfaccia di amministrazione di M365](https://admin.microsoft.com) facendo riferimento all'ID sessione specificato.*

I dettagli dell'errore includono un *ID sessione*, i dettagli dell'*estensione* e altro ancora.

Questo problema si verifica quando l'account del nuovo tenant non è stato autenticato nell'**interfaccia di amministrazione di M365** all'indirizzo https://admin.microsoft.com o nel **portale di Office 365** all'indirizzo https://portal.office.com. Per risolvere il problema, selezionare il collegamento all'*interfaccia di amministrazione di M365* nel messaggio o visitare https://portal.office.com e accedere. Dopo l'autenticazione in uno dei siti, *Guida e supporto tecnico* per Intune diventa accessibile.

**Accedere a Guida e supporto tecnico**:

- **Nel portale di Azure**

  - Selezionare **Guida e supporto** in qualsiasi pannello o pagina di Intune.

  > [!NOTE]  
  > Se l'istanza di Intune è ospitata nel cloud privato per enti pubblici, noto anche come cloud sovrano, ad esempio Azure per enti pubblici, vedere [Supporto di Intune per il cloud privato per enti pubblici](#intune-support-for-private-cloud-for-government) più avanti in questo articolo. L'esperienza *Guida e supporto tecnico* di Intune sarà disponibile nel cloud privato per enti pubblici non prima del prossimo anno.

- **Nell'interfaccia di amministrazione di Microsoft Endpoint Manager**

  - Da qualsiasi nodo dell'interfaccia di amministrazione di Microsoft Endpoint Manager selezionare l'icona **?** nell'angolo superiore destro del portale e quindi usare l'elenco a discesa per selezionare il tipo di gestione per il quale si vuole ottenere assistenza. L'interfaccia di amministrazione di Microsoft Endpoint Manager supporta i tipi di gestione seguenti ed è necessario selezionare quello per il quale si vuole ottenere assistenza, come ad esempio Intune:

    - Configuration Manager (include Desktop Analytics)
    - Intune
    - Co-gestione  

    > [!div class="mx-imgBorder"]
    > ![Selezionare il tipo di gestione](./media/get-support/select-management-type.png)

    Dopo aver selezionato un tipo di gestione, si apre la pagina *Guida e supporto tecnico* in cui è possibile specificare i dettagli per [trovare le soluzioni](#find-solutions) per un problema specifico. I dettagli vengono filtrati in base al tipo di gestione selezionato.

     Se non è stato selezionato il tipo di gestione corretto **(1)** , fare clic su *Selezionare un tipo di gestione* **(2)** per tornare all'elenco a discesa di selezione del tipo di gestione:

    > [!div class="mx-imgBorder"]
    > ![Confermare il tipo di gestione](./media/get-support/confirm-management-selection.png)

  - Se si apre Guida e supporto tecnico da **Risoluzione dei problemi e supporto tecnico** > **Guida e supporto tecnico**, il tipo di gestione selezionato non verrà visualizzato di seguito a *Guida e supporto tecnico*.

  - Se si esegue il drill-down in qualsiasi altro nodo, ad esempio *Dispositivi*, *App* o *Utenti* e quindi si seleziona *Guida e supporto tecnico*, non sarà possibile selezionare un tipo di gestione e il tipo non verrà visualizzato di seguito a *Guida e supporto tecnico*. In questo caso si presuppone che il tipo di gestione sia *Intune*. Se non si vuole che il contesto sia Intune, usare l'opzione **?** in modo che sia possibile selezionare un tipo di gestione diverso.

### <a name="the-support-experience"></a>Esperienza di supporto tecnico

  Quando si accede a Guida e supporto tecnico, il portale visualizza la finestra **Serve aiuto?** :

  ![Visualizzare la finestra Serve aiuto?](./media/get-support/need-help.png)

  Nell'angolo in alto a sinistra sono disponibili tre icone che è possibile selezionare per aprire riquadri diversi della finestra *Serve aiuto?* . Il riquadro visualizzato viene identificato dalla sottolineatura.

  I clienti che dispongono di un contratto di supporto **Premier** o **Unified** hanno a disposizione [opzioni aggiuntive](#premier-and-unified-support-customers) per il supporto e visualizzano un banner in *Serve aiuto?* simile all'immagine seguente: ![Banner Premier](./media/get-support/premier-banner.png)

  *Serve aiuto?* aprirà il riquadro *Cerca soluzioni*. Se invece il caso di supporto è attivo, la finestra aprirà il riquadro *Richieste di servizio* in cui è possibile visualizzare i dettagli relativi ai casi di supporto attivi e chiusi.

#### <a name="find-solutions"></a>Cercare le soluzioni

![Selezionare il riquadro Cerca soluzioni](./media/get-support/find-solutions.png)

Nel riquadro *Cerca soluzioni* specificare alcuni dettagli relativi a un problema nella casella di testo specificata. In base al testo specificato sul problema, il riquadro viene popolato con informazioni dettagliate potenzialmente corrispondenti. Si otterranno anche collegamenti ad articoli consigliati che potrebbero essere utili per risolvere il problema.

In caso di corrispondenza alta sulla base dei dettagli specificati, i suggerimenti per la risoluzione del problema possono essere visualizzati direttamente nella finestra *Serve aiuto?* .

È ad esempio possibile immettere **Errori di sincronizzazione password**. I risultati includono linee guida per la risoluzione dei problemi direttamente nel riquadro e collegamenti ad articoli consigliati della raccolta di documentazione.

![Visualizzare informazioni dettagliate per la risoluzione del problema](./media/get-support/troubleshooting-insights.png)

#### <a name="contact-support"></a>Rivolgersi al Supporto Tecnico

![Selezionare il riquadro Contattare il supporto](./media/get-support/contact-support.png)

Dal riquadro *Contattare il supporto* è possibile inviare una richiesta di assistenza. Questo riquadro è disponibile dopo aver immesso alcune parole chiave di base nel riquadro *Cerca soluzioni*.

Quando si richiede assistenza, immettere una descrizione del problema con tutti i dettagli necessari.  Dopo aver confermato il telefono e la posta elettronica di contatto, selezionare il metodo di contatto preferito. Nella finestra viene visualizzato un tempo di risposta per ogni metodo di contatto, che consente di sapere indicativamente quando si verrà contattati. Prima di inviare la richiesta, allegare file, ad esempio log o schermate per aggiungere informazioni dettagliate sul problema.

![Modulo per contattare il supporto tecnico](./media/get-support/contact-support-form.png)

Dopo aver compilato le informazioni necessarie, selezionare **Contattami** per inviare la richiesta.

#### <a name="service-requests"></a>Richieste di servizio

![Selezionare il riquadro Richieste di servizio](./media/get-support/service-requests.png)

Il riquadro *Richieste di servizio* visualizza la cronologia del caso. I casi attivi vengono visualizzati nella parte superiore dell'elenco, inclusi i casi chiusi disponibili anche per la revisione.

![Visualizzare l'elenco delle richieste di servizio](./media/get-support/service-requests-pane.png)

Se si dispone di un numero di caso di supporto attivo, è possibile immetterlo qui per passare al relativo problema oppure è possibile selezionare una qualsiasi richiesta dall'elenco delle richieste attive e chiuse per visualizzare altre informazioni corrispondenti.

Dopo aver visualizzato i dettagli relativi a una richiesta, selezionare la freccia sinistra visualizzata nella parte superiore della finestra delle richieste di servizio, appena sopra le tre icone del riquadro *Serve aiuto?* . La freccia indietro apre nuovamente l'elenco delle richieste di assistenza aperte.

#### <a name="premier-and-unified-support-customers"></a>Clienti con contratto di supporto Premier e Unified

I clienti che dispongono di un contratto di supporto **Premier** o **Unified** possono specificare una gravità per il problema e pianificare la richiamata di supporto per un'ora e un giorno specifici. Queste opzioni sono disponibili quando si apre o si invia un nuovo problema e quando si modifica un caso di supporto attivo.

**Gravità**: le opzioni per specificare la gravità di un problema dipendono dal contratto di supporto:

- *Premier*: gravità di tipo A, B o C
- *Unified*: critico o non critico

Se si seleziona un problema di gravità **A** o **Critico**, l'utente può solo scegliere a un caso di supporto telefonico, che offre l'opzione più rapida per ottenere supporto.

**Pianificazione callback** è possibile richiedere di essere richiamati a un'ora e giorno specifici.

## <a name="azure-help--support-experience"></a>Esperienza di Guida e supporto tecnico di Azure

Non è più possibile usare l'esperienza *Guida e supporto* di Azure per ottenere assistenza per Intune, a meno che la sottoscrizione non faccia parte di un cloud privato per enti pubblici.
Se l'istanza di Intune non è eseguita in un cloud privato per enti pubblici, l'esplorazione di *Guida e supporto* di Azure determina il reindirizzamento dell'utente all'esperienza *Guida e supporto tecnico* di Intune per creare e gestire le richieste di assistenza:

Quando si usa **Guida e supporto** nel riquadro di spostamento a sinistra oppure l'opzione **?** per aprire il riquadro *Guida e supporto* e selezionare **Guida e supporto**, si aprirà la pagina *Guida e supporto* di Azure.

Selezionare **+ Nuova richiesta di supporto** in questa pagina per aprire la scheda *Informazioni di base* della pagina *Guida e supporto - Nuova richiesta di supporto*.

![Guida e supporto](./media/get-support/help-plus-support.png)

In questa pagina:

- Per *Tipo di problema*, specificare **Tecnico**.
- Per *Servizio*, specificare **Microsoft Intune**.

  Verrà visualizzato un collegamento che reindirizza l'utente alla [pagina Guida e supporto tecnico di Intune](https://aka.ms/intunehelpsupport).
  
  ![Nuova richiesta di supporto](./media/get-support/new-request.png)

## <a name="intune-support-for-private-cloud-for-government"></a>Supporto di Intune per il cloud privato per enti pubblici

Per le sottoscrizioni di Intune ospitate nel cloud privato per enti pubblici, noto anche come cloud sovrano, ad esempio Azure per enti pubblici, la nuova esperienza Guida e supporto tecnico di Intune non è ancora disponibile.  Per ottenere supporto per Intune usare le informazioni indicate di seguito.

### <a name="create-an-online-support-ticket"></a>Creare un ticket di supporto online

>[!IMPORTANT]
> Durante la transizione di *Guida e supporto tecnico* a un nuovo sistema che non è ancora disponibile per il cloud privato per enti pubblici, quando viene creata una richiesta di assistenza, il portale identifica un caso di supporto che usa un codice identificativo di 15 cifre. Alla creazione del caso a 15 cifre, viene creato un caso speculare che sarà usato dal supporto tecnico Microsoft. Questo caso speculare viene creato in un nuovo sistema di supporto, usa un ID a 8 cifre e viene usato dai servizi di supporto tecnico per tenere traccia di tutte le attività e le comunicazioni relative alla richiesta di assistenza. Subito dopo la creazione del caso a 15 cifre, si riceverà un messaggio di posta elettronica che identifica il codice a 8 cifre del caso di supporto speculare usato dai servizi di supporto tecnico.
>
> Il personale del supporto lavora e comunica dal caso di supporto a 8 cifre e usa esclusivamente questo caso di supporto per registrare le comunicazioni e monitorare lo stato della richiesta di assistenza. Gli aggiornamenti tramite posta elettronica verranno pertanto inviati all'utente dal caso di supporto a 8 cifre che funge da riepilogo delle attività svolte. Nessun dettaglio viene registrato nella richiesta di assistenza a 15 cifre. Al termine dell'intervento di supporto, quando il caso a 8 cifre viene chiuso, lo stato viene riportato nel caso di supporto a 15 cifre che è possibile visualizzare dall'interno del portale di Azure.  Per il caso di supporto a 15 cifre non ci saranno altri aggiornamenti o modifiche di stato.
>
> Al termine della transizione degli strumenti di supporto, più avanti nel corso dell'anno, l'esperienza di supporto che Intune ospitava nel cloud per enti pubblici sarà simile all'esperienza *Guida e supporto tecnico* predefinita attualmente disponibile per le sottoscrizioni di Intune ospitate nel cloud pubblico.

1. Accedere al portale di Azure (<https://portal.azure.us>) con le credenziali di amministratore di Intune, scegliere l'icona **?** nell'angolo superiore destro del portale e scegliere **Guida e supporto** per visualizzare la pagina [Guida e supporto](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) di Azure.

   ![Immagine del collegamento a forma di punto interrogativo con il collegamento Guida e supporto evidenziato](./media/get-support/azure-get-support.png)

2. Nella pagina **Guida e supporto** di Azure selezionare **Nuova richiesta di supporto**.

   ![Immagine del collegamento Nuova richiesta di supporto evidenziato nella pagina Guida e supporto](./media/get-support/azure-support-ticket-link.png)

3. Nella scheda **Informazioni di base**, per la maggior parte dei problemi di supporto tecnico di Intune, scegliere le opzioni seguenti:
   - **Tipo di problema**: **Tecnico**
   - **Sottoscrizione**: <*nome della sottoscrizione*>
   - **Servizio**: **Microsoft Intune**
   - **Tipo di problema**: scegliere il tipo di problema dal menu a discesa.
   - **Sottotipo del problema**: scegliere il sottotipo del problema dal menu a discesa.
   - **Oggetto**: descrivere brevemente il problema per il quale serve assistenza.

   ![Immagine della scheda relativa alle informazioni di base nella pagina Guida e supporto - Nuova richiesta di supporto](./media/get-support/help-new-support-case-basics.png)

   Scegliere **Avanti: Soluzioni** per continuare.
4. Nella scheda **Soluzioni** esaminare le procedure consigliate che possono essere utili per risolvere il problema senza inviare un ticket. Se dopo aver esaminato le procedure si vuole comunque creare una richiesta di supporto, fare clic su **Avanti: Dettagli**.

   ![Immagine della scheda relativa alle soluzioni nella pagina Guida e supporto - Nuova richiesta di supporto](./media/get-support/help-new-support-case-solutions.png)
5. Nella scheda **Dettagli** immettere i dettagli per il problema, il metodo di supporto, le informazioni di contatto e quindi fare clic su **Avanti: Rivedi e crea**.

   ![Immagine della scheda relativa ai dettagli nella pagina Guida e supporto - Nuova richiesta di supporto](./media/get-support/help-new-support-case-details.png)
6. Rivedere le informazioni, verificare che siano corrette e quindi scegliere **Crea** per inviare la richiesta di supporto.

   ![Immagine della scheda Rivedi e crea nella pagina Guida e supporto - Nuova richiesta di supporto](./media/get-support/help-new-support-case-create.png)

>[!IMPORTANT]
>Per domande su fatturazione o abbonamento, è possibile aprire un caso per ottenere assistenza tramite l'[Interfaccia di amministrazione di Microsoft 365](https://admin.microsoft.com/Support/SupportEntry.aspx).

### <a name="view-support-requests"></a>Visualizzare le richieste di supporto  

È possibile visualizzare le richieste di supporto dal portale di Azure. Sono tuttavia disponibili informazioni limitate.  Per visualizzare le richieste di assistenza:

1. Accedere a Azure (<https://portal.azure.com>) con le credenziali di amministratore di Intune, scegliere l'icona **?** nell'angolo superiore destro del portale e scegliere **Guida e supporto** per visualizzare la pagina [Guida e supporto](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) di Azure.

2. Nella pagina **Guida e supporto tecnico** è possibile visualizzare l'elenco **Richieste di supporto recenti**.

   > [!IMPORTANT]  
   > I clienti del cloud privato per enti pubblici possono visualizzare solo il codice a 15 cifre del caso di supporto e lo stato della richiesta di assistenza. Tutte le comunicazioni e le registrazioni di attività o avvisi relative al caso vengono inviate tramite posta elettronica e hanno come riferimento il codice a 8 cifre del caso di supporto creato come caso di supporto speculare di quello aperto dalla console di Intune.

## <a name="additional-resources"></a>Risorse aggiuntive  

- [Supporto per la fatturazione e la sottoscrizione](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)
- [Volume licensing](https://go.microsoft.com/fwlink/p/?LinkID=282015)
- [Risoluzione dei problemi relativi a Intune](help-desk-operators.md)
