---
title: Messaggi di stato
titleSuffix: Configuration Manager
description: Descrizioni dei messaggi di stato nelle versioni supportate di Configuration Manager.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704589"
---
# <a name="state-messages-in-configuration-manager"></a>Messaggi di stato in Configuration Manager 

*Si applica a: Configuration Manager (Current Branch)*

I messaggi di stato contengono informazioni sintetiche sulle condizioni nel client di Configuration Manager. Il sistema di messaggistica di stato viene usato da componenti specifici di Configuration Manager, ad esempio aggiornamenti software e impostazioni di configurazione.

I client di Configuration Manager inviano messaggi di stato ai sistemi del sito del punto di stato di fallback o del punto di gestione per segnalare lo stato corrente delle operazioni. È possibile creare report per visualizzare i messaggi di stato inviati dai client di Configuration Manager.

Ogni funzionalità di Configuration Manager che usa i messaggi di stato viene identificata in base al tipo di argomento del messaggio di stato. I tipi di argomento del messaggio di stato elencati in questo articolo possono essere usati per definire la funzionalità di Configuration Manager a cui è correlato un messaggio di stato.

> [!NOTE]  
> Il valore zero (0) per un ID del messaggio di stato indica in genere che il tipo di argomento è in uno stato sconosciuto.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 | Stato di conformità sconosciuto|
| 1 | Conforme | 
| 2 | Non conformi | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0  | Stato dell'applicazione sconosciuto |
| 1  | Installazione degli aggiornamenti        | 
| 2  | In attesa del riavvio          | 
| 3  | In attesa del completamento di un'altra installazione         | 
| 4  | Installazione dell'aggiornamento completata(2)          | 
| 5  | Riavvio del sistema in sospeso         | 
| 6  | Impossibile installare gli aggiornamenti         | 
| 7  | Download degli aggiornamenti in corso   | 
| 8  | Aggiornamenti scaricati    | 
| 9  | Impossibile scaricare gli aggiornamenti     | 
| 10 | In attesa della finestra di manutenzione prima dell'installazione         | 
| 11 | In attesa di orchestrazione         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|      
| 0 | Stato della valutazione sconosciuto|                 
| 1 |Valutazione attivata      |
| 2 |Valutazione riuscita      |
| 3 |Valutazione non riuscita      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 | Stato del rilevamento sconosciuto|
| 1 | Non richiesto   |
| 2 | Non rilevato    |
| 3 | Rilevato   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 | Stato di conformità sconosciuto|
| 1 |Conforme     |
| 2 |Non conformi     |
| 3 |Rilevato conflitto    |
| 4 |Errore      |
| 5 |Sconosciuto     |
| 6 |Conformità parziale   |
| 7 |Conformità non configurata    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0  | Stato dell'applicazione sconosciuto|
| 1  |Applicazione avviata          |
| 2  |Applicazione in attesa del contenuto         |
| 3  | In attesa del completamento di un'altra installazione        |
| 4  |In attesa della finestra di manutenzione prima dell'installazione         |
| 5  |Riavvio richiesto prima dell'installazione         |
| 6  |Errore generale        |
| 7  |Installazione in sospeso         |
| 8  |Installazione dell'aggiornamento          |
| 9  |Riavvio del sistema in sospeso        |
| 10 |Installazione dell'aggiornamento completata         |
| 11 |Impossibile installare l'aggiornamento        |
| 12 |Download dell'aggiornamento in corso        |
| 13 | Aggiornamento scaricato        |
| 14 |Impossibile scaricare l'aggiornamento        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|0 |Stato del rilevamento sconosciuto|
| 1 | Aggiornamento non richiesto  |
| 2 | Aggiornamento richiesto   |
| 3 | Aggiornamento installato  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 |Stato dell'analisi sconosciuto|
| 1 | Analisi in attesa di contenuto   |
| 2 | Analisi in corso    |
| 3 | Analisi completata    |
| 4 | Nuovo tentativo di analisi in sospeso   |
| 5 | Analisi non riuscita   |
| 6 | Analisi completata con errori |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Nessun ID stato.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Nessun ID stato.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Nessun ID stato.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 100 |Distribuzione di client avviata      |       
| 101 |In attesa del download       |       
| 102 |Distribuzione pianificata       |       
| 103 | In attesa della finestra prima della distribuzione |
| 104 |Distribuzione ignorata       |       
| 301 |Errore di distribuzione client sconosciuto |       
| 302 |Non è stato possibile creare il servizio ccmsetup  |       
| 303 |Non è stato possibile eliminare il servizio ccmsetup |       
| 304 |Impossibile eseguire l'installazione sul sistema operativo integrato con il filtro di scrittura basato su file abilitato sull'unità di sistema |       
| 305 |La modalità di protezione nativa non è valida in Windows 2000  |       
| 306 |Non è stato possibile avviare il processo di download di ccmsetup  |       
| 307 |Riga di comando di ccmsetup non valida |       
| 308 |Non è stato possibile scaricare il file tramite WINHTTP all'indirizzo |       
| 309 |Non è stato possibile scaricare i file tramite BITS all'indirizzo |       
| 310 |Non è stato possibile installare la versione BITS |       
| 311 |Impossibile verificare se il file di prerequisiti è firmato MS  |       
| 312 |Non è stato possibile copiare il file perché il disco è pieno |       
| 313 |Installazione di Client.msi non riuscita con errore MSI |       
| 314 |Non è stato possibile caricare il file manifesto ccmsetup.xml |       
| 315 |Non è stato possibile ottenere il certificato client  |       
| 316 |Il file di prerequisiti non è firmato da MS |       
| 317 |Per completare l'installazione, è necessario riavviare il computer  |       
| 318 |Impossibile installare il client su MP. Le versioni client e MP non corrispondono |       
| 319 |Sistema operativo o Service Pack non supportato  |       
| 320 |La distribuzione non è supportata       |       
| 321 |BITS mancante        |       
| 322 |Cartella di origine non disponibile       |       
| 323 |Appv non supportato              |       
| 324 |Versione del sito non corretta              |       
| 325 |Mancata corrispondenza hash dei prerequisiti       |       
| 326 |Annullamento della registrazione di MDM non riuscito      |       
| 327 |Rilevata registrazione MDM      |       
| 328 |Rilevato Intune       |       
| 329 |Rete a consumo non consentita      |       
| 400 |Distribuzione client completata |  
| 401 |Distribuzione client riuscita. Richiesto riavvio.     |       
| 402 |Distribuzione riuscita. Il riavvio ha avuto esito positivo.     |
| 500 |Assegnazione client avviata|
| 601 |Errore di assegnazione client sconosciuto|
| 602 |Il codice del sito seguente non è valido|
| 603 |L'assegnazione al Management Pack non è riuscita|
| 604 |Non è stato possibile individuare il punto di gestione predefinito|
| 605 |Non è stato possibile scaricare il certificato di firma del sito|
| 606 |Non è stato possibile individuare automaticamente il codice del sito|
| 607 |Assegnazione del sito non riuscita. La versione del client è superiore alla versione del sito.|
| 608 |Non è stato possibile ottenere la versione del sito da Active Directory e SLP|
| 609 |Non è stato possibile ottenere la versione client|
| 700 |Assegnazione client completata|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Nessun ID stato.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 100 | Stato registrazione   |
| 101 | Registrazione pianificata   |
| 102 | Registrazione annullata   |
| 105 | Registrazione avviata   |
| 106 | Registrazione riuscita ma senza provisioning
| 107 | Registrazione riuscita e provisioning eseguito
| 108 | Registrazione - nessun utente attivo   |
| 110 | Registrazione non riuscita   |


## <a name="820--state_topictype_client_wufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 | Stato client Windows Update per le aziende| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 | Spazio su disco   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Nessun ID stato.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Nessun ID stato.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Nessun ID stato.

## <a name="1000--state_topictype_client_framework_comm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 | Comunicazione del client con il punto di gestione riuscita |
| 2 | Impossibile per il client comunicare con il punto di gestione |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Recupero da parte del client di un certificato dall'archivio certificati locale riuscito    |
| 2 |Impossibile per il client recuperare un certificato dall'archivio certificati locale |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Nessun ID stato.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Nessun ID stato.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Nessun ID stato.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Nessun ID stato.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Nessun ID stato.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Nessun ID stato.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Nessun ID stato.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Nessun ID stato.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Nessun ID stato.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Nessun ID stato.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Nessun ID stato.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Nessun ID stato.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Nessun ID stato.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Nessun ID stato.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Client non pronto per la modalità nativa  |
| 2 |Client pronto per la modalità nativa     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 | Operazione completata|
| 2 | Operazione non riuscita |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Nessun ID stato.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Nessun ID stato.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Nessun ID stato.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Nessun ID stato. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Affinità utente impostata       |
| 2 |Affinità utente rimossa       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Nessun ID stato.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Nessun ID stato.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1000  |Esito positivo dell'elemento di configurazione           |
| 1001 |Esito positivo dell'elemento di configurazione - già installato         |
| 1002 |Esito positivo dell'elemento di configurazione - stato preliminare          |
| 1003 |Esito positivo stato rapido elemento di configurazione          |
| 2000 |Elemento di configurazione in corso           |
| 2001 |Elemento di configurazione in corso - in attesa del contenuto         |
| 2002 |Elemento di configurazione in corso - installazione          |
| 2003 |Elemento di configurazione in corso - in attesa del riavvio         |
| 2004 |Elemento di configurazione in corso - in attesa della finestra di manutenzione        |
| 2005 |Elemento di configurazione in corso - in attesa della pianificazione         |
| 2006 |Elemento di configurazione in corso - download di contenuto dipendente     |
| 2007 |Elemento di configurazione in corso - installazione delle dipendenze        |
| 2008 |Elemento di configurazione in corso - riavvio in sospeso         |
| 2009 |Elemento di configurazione in corso - contenuto scaricato         |
| 2010 |Elemento di configurazione in corso - aggiornamento in sospeso         |
| 2011 |Elemento di configurazione in corso - in attesa della riconnessione dell'utente        |
| 2012 |Elemento di configurazione in corso - in attesa della disconnessione dell'utente         |
| 2013 |Elemento di configurazione in corso - in attesa dell'accesso dell'utente         |
| 2014 |Elemento di configurazione in corso - in attesa dell'installazione         |
| 2015 |Elemento di configurazione in corso - in attesa di ripetizione dei tentativi         |
| 2016 |Elemento di configurazione in corso - in attesa di presmode         |
| 2017 |Elemento di configurazione in corso - in attesa dell'orchestrazione        |
| 2018 |Elemento di configurazione in corso - in attesa della rete         |
| 2019 |Elemento di configurazione in corso - aggiornamento VE in sospeso         |
| 2020 |Elemento di configurazione in corso -aggiornamento VE in corso         |
| 3000 |Requisiti dell'elemento di configurazione non soddisfatti           |
| 3001 |Requisiti dell'elemento di configurazione non soddisfatti - host non applicabile        |
| 4000 |Elemento di configurazione sconosciuto           |
| 5000 |Errore dell'elemento di configurazione            |
| 5001 |Errore dell'elemento di configurazione durante la valutazione          |
| 5002 |Errore dell'elemento di configurazione durante l'installazione          |
| 5003 |Errore dell'elemento di configurazione durante il recupero del contenuto         |
| 5004 |Errore dell'elemento di configurazione durante l'installazione delle dipendenze         |
| 5005 |Errore dell'elemento di configurazione durante il recupero delle dipendenze del contenuto        |
| 5006 |Errore dell'elemento di configurazione - conflitto delle regole          |
| 5007 |Errore dell'elemento di configurazione - in attesa di un nuovo tentativo          |
| 5008 |Errore dell'elemento di configurazione - disinstallazione della sostituzione        |
| 5009 |Errore dell'elemento di configurazione - download sostituito         |
| 5010 |Errore dell'elemento di configurazione - aggiornamento VE          |
| 5011 |Errore dell'elemento di configurazione - installazione della licenza         |
| 5012 |Errore dell'elemento di configurazione durante il recupero di tutte le app attendibili       |
| 5013 |Errore dell'elemento di configurazione - nessuna licenza disponibile         |
| 5014 |Errore dell'elemento di configurazione - sistema operativo non supportato          |
| 6000 |Esito positivo dell'avvio dell'elemento di configurazione            |
| 6010 |Errore di avvio dell'elemento di configurazione            |
| 6020 |Avvio dell'elemento di configurazione sconosciuto|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Nessun ID stato.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Nessun ID stato.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Nessun ID stato.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Nessun ID stato.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Nessun ID stato.

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Nessun ID stato.

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Nessun ID stato.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Nessun ID stato.

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Endpoint Protection non gestito   |
| 2 |Endpoint Protection in attesa di installazione  |
| 3 |Endpoint Protection gestito   |
| 4 |Installazione di Endpoint Protection non riuscita  |
| 5 |Riavvio in sospeso di Endpoint Protection  |
| 6 |Endpoint Protection non supportato   |
| 7 |Endpoint Protection co-gestito   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 |Stato applicazione criteri di Endpoint Protection sconosciuto    |
| 1 |Applicazione criteri di Endpoint Protection riuscita    |
| 2 |Applicazione criteri di Endpoint Protection non riuscita    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 0 |  Sconosciuto    |
| 1 |  Attivo    |
| 2 |  Inattivo    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 | Proxy di riattivazione non installato    |
| 2 | Proxy di riattivazione in attesa dell'installazione   |
| 3 | Proxy di riattivazione installato    |
| 4 | Installazione del proxy di riattivazione non riuscita   |
| 5 | Proxy di riattivazione in attesa del riavvio   |
| 6 | Proxy di riattivazione non è supportato in questo sistema operativo  |
| 7 | Rifiuto esplicito server proxy di riattivazione   |
| 8 | Disinstallazione di proxy di riattivazione non riuscita   |
| 9 | Runtime di proxy di riattivazione non supportato   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Nessun ID stato.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Nessun ID stato.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Nessun ID stato.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|0 | Set di canale del servizio notifica push di Windows|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Nessun ID stato.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Nessun ID stato.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Nessun ID stato.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Nessun ID stato.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Nessun ID stato.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Nessun ID stato.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Nessun ID stato.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Nessun ID stato.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Nessun ID stato.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Nessun ID stato.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Nessun ID stato.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Nessun ID stato.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Richiesta di verifica rilasciata         |
| 2 |Rilascio richiesta di verifica non riuscito        |
| 3 |La creazione della richiesta non è riuscita        |
| 4 |Invio della richiesta non riuscito        |
| 5 |Convalida della richiesta di verifica riuscita       |
| 6 |Convalida della richiesta di verifica non riuscita       |
| 7 |Rilascio non riuscito         |
| 8 |Rilascio in sospeso         |
| 9 |Rilasciato          |
| 10 |Elaborazione della risposta non riuscita       |
| 11 |Risposta in sospeso         |
| 12 |Registrazione riuscita         |
| 13 |Registrazione non richiesta         |
| 14 |Revocato          |
| 15 |Rimosso dalla raccolta        |
| 16 |Rinnovo verificato         |
| 17 |Installazione non riuscita        |
| 18 |Installato         |
| 19 |Eliminazione non riuscita         |
| 20 |Eliminato         |
| 21 |Rinnovo richiesto        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Richiesta di verifica rilasciata         |
| 2 |Rilascio richiesta di verifica non riuscito        |
| 3 |La creazione della richiesta non è riuscita        |
| 4 |Invio della richiesta non riuscito        |
| 5 |Convalida della richiesta di verifica riuscita       |
| 6 |Convalida della richiesta di verifica non riuscita       |
| 7 |Rilascio non riuscito         |
| 8 |Rilascio in sospeso         |
| 9 |Rilasciato          |
| 10 |Elaborazione della risposta non riuscita       |
| 11 |Risposta in sospeso         |
| 12 |Registrazione riuscita         |
| 13 |Registrazione non richiesta         |
| 14 |Revocato          |
| 15 |Rimosso dalla raccolta        |
| 16 |Rinnovo verificato         |
| 17 |Installazione non riuscita        |
| 18 |Installato         |
| 19 |Eliminazione non riuscita         |
| 20 |Eliminato         |
| 21 |Rinnovo richiesto        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 | Configurazione del pin di stato riuscita       |
| 2 | Configurazione del pin di stato non riuscita       |
| 3 | Configurazione del pin di stato non supportata      |
| 4 | Configurazione del pin di stato in corso      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Nessun ID stato.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Nessun ID stato.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Nessun ID stato.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Nessun ID stato.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Nessun ID stato.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Nessun ID stato.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Richiesta di verifica rilasciata    |
| 2 |Rilascio richiesta di verifica non riuscito   |
| 3 |La creazione della richiesta non è riuscita   |
| 4 |Invio della richiesta non riuscito   |
| 5 |Convalida della richiesta di verifica riuscita  |
| 6 |Convalida della richiesta di verifica non riuscita  |
| 7 |Rilascio non riuscito    |
| 8 |Rilascio in sospeso    |
| 9 |Rilasciato     |
| 10 |Elaborazione della risposta non riuscita  |
| 11 |Risposta in sospeso    |
| 12 |Registrazione riuscita    |
| 13 |Registrazione non richiesta    |
| 14 |Revocato     |
| 15 |Rimosso dalla raccolta   |
| 16 |Rinnovo verificato    |
| 17 |Installazione non riuscita   |
| 18 |Installato    |
| 19 |Eliminazione non riuscita    |
| 20 |Eliminato    |
| 21 |Rinnovo richiesto   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
|| 1 | Conformità corretta    |
| 2 | Errore di conformità nel Management Pack   |
| 3 | Errore di conformità nel client   |
| 4 | Errore di conformità in Intune   |
| 5 | Errore di conformità in AAD   |
| 6 | Co-gestione conformità Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Origine di peer cache aggiunta       |
| 2 |Origine di peer cache rimossa      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Origine di peer cache disattivata       |
| 2 |Origine di peer cache attiva       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Caricamento dati aggregati scaricati       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Caricamento dati rifiuto origine peer     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Nessun ID stato.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Nessun ID stato.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Nessun ID stato.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Nessun ID stato.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID del messaggio di stato     |  Descrizione del messaggio di stato |
|:-------------|:------|
| 1 |Attestazione dell'integrità supportata      |
| 2 |Attestazione dell'integrità non supportata      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Nessun ID stato.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Nessun ID stato.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Nessun ID stato.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Nessun ID stato.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Nessun ID stato.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Nessun ID stato.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Nessun ID stato.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Nessun ID stato.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Nessun ID stato.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Nessun ID stato.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Nessun ID stato.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Nessun ID stato.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Nessun ID stato.

## <a name="next-steps"></a>Passaggi successivi

- [Descrizione della messaggistica di stato in Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [White paper sulla gestione degli aggiornamenti software per Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
