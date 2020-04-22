---
title: Sicurezza e privacy per la distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni sulle procedure di sicurezza e privacy consigliate per la distribuzione del sistema operativo in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709329"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Sicurezza e privacy per la distribuzione del sistema operativo in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene informazioni sulla sicurezza e sulla privacy per funzionalità di distribuzione del sistema operativo in Configuration Manager.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a> Procedure di sicurezza consigliate per la distribuzione del sistema operativo  

Usare le seguenti procedure di sicurezza consigliate quando si distribuiscono sistemi operativi con Configuration Manager:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementare i controlli di accesso per proteggere il supporto di avvio

Quando si crea un supporto di avvio, assegnare sempre una password per proteggere il supporto. Anche con una password, vengono crittografati solo i file che contengono informazioni sensibili e tutti i file possono essere sovrascritti.  

Controllare l'accesso fisico ai supporti per evitare che un utente malintenzionato utilizzi gli attacchi crittografici per ottenere il certificato di autenticazione client.  

Per evitare che un client installi criteri contenuto o clienti manomessi, viene eseguito l'hashing del contenuto e il contenuto deve essere usato con i criteri originali. Se l'hashing del contenuto non viene eseguito correttamente o il controllo che il contenuto soddisfi i criteri ha esito negativo, il client non userà il supporto di avvio. Viene eseguito solo l'hashing del contenuto e non dei criteri, che vengono tuttavia crittografati e protetti specificando una password. In questo modo sarà più difficile per un utente malintenzionato modificare i criteri.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Usare una posizione protetta quando si crea il supporto per le immagini del sistema operativo

Se gli utenti non autorizzati hanno accesso alla posizione, possono manomettere i file creati. Possono anche usare tutto lo spazio disponibile su disco in modo da impedire la creazione del supporto.  


### <a name="protect-certificate-files"></a>Proteggere i file di certificato 

Proteggere i file di certificato con estensione pfx usando una password complessa. Se sono archiviati nella rete, proteggere il canale di rete durante l'importazione dei file in Configuration Manager

Grazie a questa configurazione, quando viene richiesta una password per importare il certificato di autenticazione client usato per il supporto di avvio, il certificato viene protetto da utenti malintenzionati.  

Utilizzare la firma SMB o IPsec tra il percorso di rete e il server del sito per impedire all'autore di un attacco di manomettere il file di certificato.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Bloccare o revocare eventuali certificati compromessi 

Se il certificato client è compromesso, bloccare il certificato da Configuration Manager e revocarlo se si tratta di un certificato PKI.  

Per distribuire un sistema operativo usando il supporto di avvio e l'avvio PXE, è necessario che il certificato di autenticazione client abbia una chiave privata. Se tale certificato è compromesso, bloccarlo nel nodo **Certificati** dell'area di lavoro **Amministrazione** , nodo **Sicurezza** .  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Proteggere il canale di comunicazione tra il server del sito e il provider SMS

Quando il provider SMS si trova in remoto rispetto al server del sito, proteggere il canale di comunicazione affinchè le immagini di avvio siano protette.

Quando le immagini di avvio vengono modificate e il provider SMS è in esecuzione in un server che non è il server del sito, le immagini di avvio sono vulnerabili agli attacchi. Proteggere il canale di rete tra questi computer utilizzando la firma SMB o IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Abilitare i punti di distribuzione per la comunicazione client PXE solo su segmenti di rete protetta.

Quando un client invia una richiesta di avvio PXE, non è assolutamente possibile garantire che la richiesta sia presa in carico da un punto di distribuzione valido che supporta PXE. Questo scenario include i rischi di protezione seguenti:  

- Un punto di distribuzione non autorizzato che risponde alle richieste PXE potrebbe fornire ai client un'immagine manomessa.  

- Un utente malintenzionato potrebbe avviare un attacco man-in-the-middle contro il protocollo TFTP usato da PXE. Questo tipo di attacco potrebbe inviare codice dannoso insieme ai file del sistema operativo. L'utente malintenzionato potrebbe anche creare un client non autorizzato per inviare richieste TFTP direttamente al punto di distribuzione.  

- Un utente malintenzionato potrebbe utilizzare un client dannoso per avviare un attacco Denial of Service contro il punto di distribuzione.  

Usare una difesa in profondità per proteggere i segmenti di rete in cui i client accedono ai punti di distribuzione che supportano PXE.  

> [!WARNING]  
>  In considerazione di tali rischi di sicurezza, non abilitare un punto di distribuzione per la comunicazione PXE quando si trova in una rete non attendibile, ad esempio una rete perimetrale.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configurare i punti di distribuzione che supportano PXE per rispondere alle richieste PXE solo su interfacce di rete specificate.  

Se si consente al punto di distribuzione di rispondere a richieste PXE su tutte le interfacce di rete, questa configurazione potrebbe esporre il servizio PXE a reti non affidabili.  


### <a name="require-a-password-to-pxe-boot"></a>Richiedere una password per l'avvio PXE

Quando si richiede una password per l'avvio PXE, si aggiunge un livello di protezione aggiuntivo al processo di avvio PXE, in modo da proteggere da client non autorizzati che si aggiungono alla gerarchia di Configuration Manager.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Limitare il contenuto in immagini del sistema operativo usate per l'avvio PXE o il multicast

Non includere applicazioni line-of-business o software che contiene dati sensibili in un'immagine che viene usata per l'avvio PXE o il multicast.  

In considerazione dei rischi di sicurezza inerenti che interessano l'avvio PXE e il multicast, ridurre i rischi se il computer non autorizzato scarica l'immagine del sistema operativo.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Limitare il contenuto installato da variabili della sequenza di attività

Non includere applicazioni line-of-business o software che contiene dati sensibili nei pacchetti delle applicazioni installate usando variabili della sequenze di attività.  

Quando si distribuisce software usando variabili della sequenze di attività, il software potrebbe essere installato in computer e utenti che non sono autorizzati a ricevere tale software.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Proteggere il canale di rete durante la migrazione dello stato utente

Durante la migrazione dello stato utente, proteggere il canale di rete tra il client e il punto di migrazione stato usando la firma SMB o IPsec.  

Dopo la connessione iniziale in HTTP, i dati della migrazione dello stato utente vengono trasferiti tramite SMB. Se non si protegge il canale di rete, un utente malintenzionato può leggere e modificare questi dati.  


### <a name="use-the-latest-version-of-usmt"></a>Usare la versione più recente di USMT

Usare la versione più recente dell'utilità di migrazione stato utente (USMT) supportata da Configuration Manager.  

La versione più recente dell'USMT fornisce miglioramenti della protezione e un controllo maggiore durante la migrazione dei dati dello stato utente.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Eliminare manualmente le cartelle dei punti di migrazione stato quando ne viene rimossa l'autorizzazione  

Quando si rimuove una cartella del punto di migrazione stato dalle proprietà del punto di migrazione stato nella console di Configuration Manager, il sito non elimina la cartella fisica. Per proteggere i dati della migrazione dello stato utente dalla divulgazione di informazioni, è necessario rimuovere manualmente la condivisione di rete ed eliminare la cartella.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Non configurare il criterio di eliminazione per eliminare immediatamente lo stato utente  

Se si configura il criterio di eliminazione nel punto di migrazione stato per rimuovere immediatamente i dati contrassegnati per l'eliminazione e un utente malintenzionato riesce a recuperare i dati dello stato utente prima che lo faccia il computer valido, il sito elimina immediatamente i dati dello stato utente. Impostare un intervallo **Elimina dopo** abbastanza ampio per verificare il ripristino corretto dei dati dello stato utente.  


### <a name="manually-delete-computer-associations"></a>Eliminare manualmente le associazioni computer 

Eliminare manualmente le associazioni computer quando il ripristino dei dati della migrazione stato utente è stato completato e verificato.

Configuration Manager non rimuove automaticamente le associazioni computer. Proteggere l'identificazione dei dati dello stato utente eliminando manualmente le associazioni computer che non sono più necessarie.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Eseguire manualmente il backup dei dati della migrazione dello stato utente nel punto di migrazione dello stato.  

Il backup di Configuration Manager non include i dati della migrazione stato utente nel backup del sito.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementare i controlli di accesso per proteggere i supporti pre-installati.  

Controllare l'accesso fisico ai supporti per evitare che un utente malintenzionato utilizzi gli attacchi crittografici per ottenere il certificato di autenticazione client e i dati sensibili.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementare i controlli di accesso per proteggere il processo di creazione dell'immagine del computer di riferimento.  

Assicurarsi che il computer di riferimento usato per acquisire le immagini del sistema operativo si trovi in un ambiente sicuro. Usare i controlli di accesso appropriati in modo che non sia possibile installare o inavvertitamente includere il software imprevisto o dannoso nell'immagine acquisita. Quando si acquisisce l'immagine, assicurarsi che il percorso di rete di destinazione sia sicuro. In questo modo si garantisce che l'immagine non potrà essere manomessa dopo essere stata acquisita.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Installare sempre gli aggiornamenti di protezione più recenti sul computer di riferimento.  

Quando il computer di riferimento dispone degli aggiornamenti di sicurezza correnti, ciò riduce la vulnerabilità dei nuovi computer quando vengono avviati per la prima volta.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementare i controlli di accesso durante la distribuzione di un sistema operativo in un computer sconosciuto

Se si deve distribuire un sistema operativo in un computer sconosciuto, implementare i controlli di accesso per impedire ai computer non autorizzati di collegarsi alla rete.  

Il provisioning di computer sconosciuti è un modo pratico per distribuire nuovi computer su richiesta, ma può anche consentire a un utente malintenzionato di diventare un client affidabile nella rete. Limitare l'accesso fisico alla rete e monitorare i client per rilevare i computer non autorizzati. 

I computer che rispondono alla distribuzione di sistemi operativi avviata da PXE potrebbero assistere alla distruzione di tutti i dati durante il processo. Tale comportamento potrebbe portare a una perdita di disponibilità di sistemi che vengono inavvertitamente riformattati.  


### <a name="enable-encryption-for-multicast-packages"></a>Abilitare la crittografia per i pacchetti multicast  

Per ogni pacchetto di distribuzione del sistema operativo, è possibile abilitare la crittografia quando Configuration Manager trasferisce il pacchetto usando il multicast. Questa configurazione consente di impedire ai computer non autorizzati di partecipare alla sessione multicast e agli utenti malintenzionati di manomettere la trasmissione.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Monitorare i punti di distribuzione non autorizzati abilitati per multicast  

Se riescono ad accedere alla rete, gli utenti malintenzionati possono configurare server multicast non autorizzati per effettuare lo spoofing della distribuzione del sistema operativo.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Quando si esportano sequenze di attività in un percorso di rete, proteggere il percorso e il canale di rete.

Limitare l'accesso alla cartella di rete.  

Utilizzare la firma SMB o IPsec tra il percorso di rete e il server del sito per impedire all'autore di un attacco di manomettere la sequenza attività esportata.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Se si esegue la sequenza di attività come account, adottare misure di sicurezza aggiuntive

Se si [esegue la sequenza di attività come account](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account), attenersi ai passaggi precauzionali seguenti:  

- Utilizzare un account con autorizzazioni minime.  

- Non usare l'account di accesso alla rete per questo account.  

- Non modificare mai l'account in amministratore di dominio.  

- Non configurare mai profili mobili per questo account. Quando viene eseguita la sequenza di attività, viene scaricato il profilo mobile per l'account, che rende il profilo vulnerabile all'accesso nel computer locale.  

- Limitare l'ambito dell'account. Ad esempio, creare una sequenza di attività diversa per ogni sequenza di attività eseguita come account. In questo modo, qualora venga compromesso un account, risulteranno compromessi solo i computer client a cui tale account può accedere. Se la riga di comando richiede accesso amministrativo nel computer, creare un account amministratore locale unicamente per l'esecuzione della sequenza di attività come account. Creare questo account locale in tutti i computer che eseguono la sequenza di attività ed eliminarlo quando non è più necessario.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Limitare e monitorare gli utenti amministrativi a cui è garantito il ruolo di sicurezza Gestione distribuzione del sistema operativo

Gli utenti amministrativi a cui è garantito il ruolo di sicurezza **Gestione distribuzione del sistema operativo** possono creare certificati autofirmati. Questi certificati possono essere usati per rappresentare un client e ottenere i criteri client da Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Usare HTTP migliorato per ridurre la necessità di un account di accesso alla rete

A partire dalla versione 1806, quando si abilita [HTTP migliorato](../../core/plan-design/hierarchy/enhanced-http.md), alcuni scenari di distribuzione del sistema operativo non richiedono un account di accesso alla rete per scaricare il contenuto da un punto di distribuzione. Per altre informazioni, vedere [Sequenze di attività e account di accesso alla rete](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Problemi di sicurezza per la distribuzione del sistema operativo  

Nonostante la distribuzione del sistema operativo possa essere un modo utile per distribuire i sistemi operativi e le configurazioni più sicure per i computer sulla rete, presenta i rischi di sicurezza seguenti:  


### <a name="information-disclosure-and-denial-of-service"></a>Divulgazione di informazioni e Denial of Service  

Se un utente malintenzionato ottiene il controllo dell'infrastruttura di Configuration Manager, potrebbe eseguire qualsiasi sequenza di attività, tra cui la formattazione dei dischi rigidi di tutti i computer client. Le sequenze attività possono essere configurate per contenere informazioni sensibili, come gli account che dispongono delle autorizzazioni per raggiungere il dominio e le chiavi di Volume Licensing.  


### <a name="impersonation-and-elevation-of-privileges"></a>Rappresentazione e aumento di privilegi  

Le sequenze di attività possono aggiungere un computer a un dominio, operazione che può fornire a un computer non autorizzato l'accesso autenticato alla rete. 

Proteggere quindi il certificato di autenticazione client usato per i supporti della sequenza di attività di avvio e per la distribuzione dell'avvio PXE. Quando si acquisisce un certificato di autenticazione client, si dà a un utente malintenzionato l'opportunità di ottenere la chiave privata nel certificato e di rappresentare quindi un client valido sulla rete. In questo scenario, il computer non autorizzato può scaricare criteri, che possono contenere dati sensibili.  

Se i client usano l'account di accesso alla rete per accedere ai dati archiviati nel punto di migrazione stato, tali client condivideranno effettivamente la stessa identità e potranno accedere ai dati di migrazione stato da un altro client che usa l'account di accesso alla rete. I dati vengono crittografati in modo che solo il client originale sia in grado di leggerli, ma i dati potrebbero essere alterati o eliminati.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>L'autenticazione client al punto di migrazione stato viene ottenuta con un token di Configuration Manager emesso dal punto di gestione.  

Configuration Manager non limita e non gestisce la quantità di dati archiviati nel punto di migrazione stato. È pertanto possibile che lo spazio su disco disponibile venga riempito da un utente malintenzionato, provocando un attacco Denial of Service.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Se si utilizzano le variabili di raccolta, gli amministratori locali saranno in grado di leggere informazioni potenzialmente riservate  

Le variabili di raccolta rappresentano un metodo flessibile per distribuire i sistemi operativi ma possono contribuire alla divulgazione di informazioni.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a> Informazioni sulla privacy per la distribuzione del sistema operativo  

Oltre a distribuire un sistema operativo in computer che ne sono privi, Configuration Manager consente anche di eseguire la migrazione di file e impostazioni utente da un computer a un altro. L'amministratore configura le informazioni da trasferire, inclusi file di dati personali, impostazioni di configurazione e cookie del browser.  

Configuration Manager archivia le informazioni in un punto di migrazione stato e le crittografa durante la trasmissione e l'archiviazione. Le informazioni archiviate possono essere recuperate solo dal nuovo computer associato alle informazioni sullo stato. Se il nuovo computer perde la chiave per il recupero delle informazioni, un amministratore di Configuration Manager che possiede il diritto **Visualizza informazioni di ripristino** negli oggetti di istanza di associazione computer può accedere alle informazioni e associarle a un nuovo computer. Dopo il ripristino delle informazioni sullo stato, per impostazione predefinita il nuovo computer elimina i dati dopo un giorno. È possibile configurare il momento in cui il punto di migrazione dello stato rimuoverà i dati contrassegnati per l'eliminazione. Configuration Manager non archivia le informazioni sulla migrazione stato nel database del sito e non le invia a Microsoft.  

Se si usano supporti di avvio per distribuire le immagini del sistema operativo, usare sempre l'opzione predefinita per proteggere con una password il supporto di avvio. La password crittografa eventuali variabili archiviate nella sequenza attività, ma eventuali informazioni non archiviate in una variabile potrebbero essere esposte alla divulgazione.  

La distribuzione del sistema operativo può usare le sequenze di attività per eseguire varie attività durante il processo di distribuzione, che include l'installazione di applicazioni e aggiornamenti software. Quando si configurano le sequenze attività, è necessario inoltre tenere presenti le implicazioni sulla privacy relative all'installazione del software.  

Per impostazione predefinita, Configuration Manager non implementa la distribuzione del sistema operativo. Per potere raccogliere informazioni sullo stato utente o creare sequenze di attività o immagini di avvio, sono necessari alcuni passaggi di configurazione.  

Prima di configurare la distribuzione del sistema operativo, considerare i requisiti sulla privacy.  



## <a name="see-also"></a>Vedere anche

[Diagnostica e dati di utilizzo](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Sicurezza e privacy per Configuration Manager](../../core/plan-design/security/security-and-privacy.md)
