---
title: Registrare un Mac in Portale aziendale Intune | Microsoft Docs
description: Informazioni su come registrare un Mac in Intune con l'app Portale aziendale.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/18/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: fe405b66892ec7777d8d1572b2fb6ab6ce1aaa91
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85094219"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Registrare il dispositivo macOS con l'app Portale aziendale  

Registrare un dispositivo macOS nell'app Portale aziendale Intune per ottenere accesso protetto alla posta elettronica aziendale o dell'istituto di istruzione, ai file e alle app.

Le organizzazioni in genere richiedono la registrazione del dispositivo prima di concedere l'accesso ai dati proprietari. Dopo la registrazione, il dispositivo diventa *gestito*. L'organizzazione può assegnare criteri e app al dispositivo tramite un provider di gestione di dispositivi mobili (MDM), ad esempio Intune. Per ottenere accesso continuato alle informazioni aziendali o dell'istituto di istruzione tramite il dispositivo, è necessario configurare il dispositivo in modo corrispondente alle impostazioni dei criteri dell'organizzazione.  

Questo articolo descrive come usare l'app Portale aziendale per macOS per configurare e gestire il dispositivo in modo da soddisfare i requisiti dell'organizzazione.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Aspettative relative all'app Portale aziendale

Durante la configurazione iniziale, l'app Portale aziendale richiede di eseguire l'accesso e l'autenticazione nell'organizzazione. Portale aziendale segnala quindi le eventuali impostazioni del dispositivo che è necessario configurare per soddisfare i requisiti dell'organizzazione. Ad esempio, le organizzazioni spesso definiscono il numero di caratteri minimo o massimo che la password deve soddisfare.    

Dopo la registrazione del dispositivo, Portale aziendale assicurerà sempre che il dispositivo sia protetto in base ai requisiti dell'organizzazione. Ad esempio se si installa un'app da un'origine non attendibile, Portale aziendale segnalerà il problema e potrebbe limitare l'accesso alle risorse dell'organizzazione. I criteri di protezione delle app come questo sono comuni. Per ottenere nuovamente l'accesso, sarà probabilmente necessario disinstallare l'app. 

Se dopo la registrazione l'organizzazione applica un nuovo requisito di sicurezza, ad esempio l'autenticazione a più fattori, l'app Portale aziendale invierà una notifica. L'utente potrà quindi modificare le impostazioni per continuare a lavorare dal proprio dispositivo.  

Per altre informazioni sulla registrazione, vedere [Che cosa avviene quando si installa l'app Portale aziendale e si registra il dispositivo?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## <a name="get-your-macos-device-managed"></a>Configurare il dispositivo macOS come gestito  
Usare la procedura seguente per registrare il dispositivo macOS nell'organizzazione. Il dispositivo deve eseguire macOS 10.12 o versioni successive.   

> [!NOTE]
> Durante questo processo, potrebbe essere richiesto di consentire a Portale aziendale di usare informazioni riservate archiviate nel portachiavi. Queste richieste fanno parte della sicurezza di Apple. Quando viene richiesto, digitare la password del portachiavi di accesso e selezionare **Consenti sempre**. Se si preme **INVIO** o **restituire** sulla tastiera, verrà invece selezionato **Consenti**, che può comportare la visualizzazione di richieste aggiuntive.  

### <a name="install-company-portal-app"></a>Installare l'app Portale aziendale  
1. Passare a [Registra Mac](https://go.microsoft.com/fwlink/?linkid=853070).  
2. Verrà scaricato il file con estensione pkg del programma di installazione di Portale aziendale. Aprire il programma di installazione e seguire la procedura. 
3. Accettare il contratto di licenza software. 
4. Immettere la password del dispositivo o l'impronta digitale registrata per installare il software.  
5. Aprire Portale aziendale. 

> [!IMPORTANT]
> Potrebbe essere aperto Microsoft AutoUpdate per aggiornare il software Microsoft. Dopo aver installato tutti gli aggiornamenti, aprire l'app Portale aziendale. Per un'esperienza di installazione ottimale, installare le versioni più recenti di Microsoft AutoUpdate e Portale aziendale.  


### <a name="enroll-your-mac"></a>Registrare il Mac  


1. Accedere al Portale aziendale con l'account aziendale o dell'istituto di istruzione.  
2. All'apertura dell'app, selezionare **Inizia**.  
3. Esaminare le [informazioni che l'organizzazione può visualizzare o meno](what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) nel dispositivo registrato. Selezionare quindi **Continua**.
4. Nella schermata **Installa il profilo di gestione** selezionare **Scarica il profilo**.  

    ![Screenshot di esempio della schermata Installare il profilo di gestione di Portale aziendale, con la richiesta della password evidenziata.](./media/install-management-profile-macos-2006.png)   

5. Verranno aperte le preferenze di sistema del dispositivo.  
    a. Selezionare **Installa** e quindi selezionare di nuovo **Installa**.  
    b. Se viene richiesto, immettere la password del dispositivo.   
6. Una volta installato, il profilo verrà visualizzato nell'elenco dei profili in **Profilo di gestione**.
    ![Screenshot di esempio della schermata Profilo di gestione in Preferenze di Sistema, con il pulsante "Approva" evidenziato.](./media/management-profile-approve-macos-2006.png)   
7. Tornare a Portale aziendale.    
8. L'organizzazione potrebbe richiedere all'utente di aggiornare le impostazioni del dispositivo. Al termine dell'aggiornamento delle impostazioni, selezionare **Riprova**.  

    ![Screenshot di esempio della schermata Aggiorna impostazioni del dispositivo di Portale aziendale, con il pulsante Riprova evidenziato.](./media/update-settings-mac-2006.png)  
9. Al termine dell'installazione, selezionare **Fine**.  


 ## <a name="troubleshooting-and-feedback"></a>Risoluzione dei problemi e feedback   

Se si verificano problemi durante la registrazione, passare a **?**  > **Invia report di diagnostica** per segnalare il problema agli sviluppatori dell'app Microsoft. Queste informazioni vengono usate per contribuire al miglioramento dell'app. Queste informazioni verranno usate anche per risolvere il problema se il personale del supporto IT richiede assistenza agli sviluppatori.  

Dopo aver segnalato il problema a Microsoft, è possibile inviare i relativi dettagli al personale del supporto IT. Selezionare **Dettagli della posta elettronica**. Digitare una descrizione del problema che si è verificato nel corpo del messaggio di posta elettronica. Per trovare l'indirizzo di posta elettronica del personale di supporto, passare all'app Portale aziendale > **Contatto**. Oppure vedere il [sito Web Portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  
 

Inoltre, il team di Portale aziendale di Microsoft Intune è interessato a conoscere l'opinione degli utenti. Passare a **?**  > **Invia commenti e suggerimenti** per condividere suggerimenti e idee.  

## <a name="unverified-profiles"></a>Profili non verificati  
Quando si visualizzano i profili di gestione di dispositivi mobili (MDM) installati in **Preferenze di sistema** > **Profili**, alcuni profili vengono visualizzati con lo stato non verificato. Purché il profilo di gestione presenti uno stato verificato, non sarà necessario preoccuparsene.  

È il profilo di gestione a definire la connessione al canale MDM. Purché il profilo di gestione sia verificato, tutti gli altri profili distribuiti nel computer tramite tale canale ereditano le caratteristiche di sicurezza del profilo di gestione.  

## <a name="updating-the-company-portal-app"></a>Aggiornamento dell'app Portale aziendale

L'aggiornamento dell'app Portale aziendale viene eseguito come quello di qualsiasi altra app di Office, tramite Microsoft AutoUpdate per macOS. Vedere altre informazioni sull'[aggiornamento di app Microsoft per macOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## <a name="next-steps"></a>Passaggi successivi  
Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  


