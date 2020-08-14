---
title: Registri eventi del client
titleSuffix: Configuration Manager
description: Riferimento tecnico per le possibili voci del client BitLocker (MBAM) nel registro eventi di Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d108f56032b1ca3cf4a41a836a7e9096afe41d0d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127968"
---
# <a name="client-event-logs"></a>Registri eventi del client

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

In un client Gestione configurazione in cui si distribuisce un criterio di gestione di BitLocker, usare il Visualizzatore eventi di Windows per visualizzare i registri eventi del client BitLocker. Passare a **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **MBAM** per i registri eventi [Amministratore](#admin) e [Operativo](#operational).

## <a name="admin"></a>Amministratore

### <a name="2-volumeenactmentfailed"></a>2: VolumeEnactmentFailed

Errore durante l'applicazione dei criteri MBAM.

#### <a name="error-code--2144272219"></a>Codice di errore: -2144272219

Dettagli: Crittografia unità BitLocker supporta solo la Crittografia del solo spazio utilizzato per l'archiviazione con thin provisioning.

Questo errore si verifica se si tenta di usare BitLocker per crittografare una macchina virtuale che esegue Windows 10 versione 1803 o precedente. Le versioni precedenti di Windows 10 non supportano la crittografia del disco completo. I criteri di gestione di BitLocker applicano la crittografia del disco completo.

#### <a name="error-code--2147024774"></a>Codice di errore: -2147024774

Dettagli: L'area dati passata a una chiamata di sistema è troppo piccola.

Per risolvere il problema, riavviare il computer.

### <a name="4-transferstatusdatafailed"></a>4: TransferStatusDataFailed

Errore durante l'invio dei dati sullo stato di crittografia.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Volume di sistema mancante. Il volume di sistema è necessario per crittografare l'unità del sistema operativo.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

Hardware TPM mancante. TPM è necessario per crittografare l'unità del sistema operativo con una protezione TPM.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

Il computer è esente dalla crittografia. Stato dell'hardware del computer: Esentato

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

Il computer è esente dalla crittografia. Stato dell'hardware del computer: Sconosciuto

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Controllo esenzione hardware non riuscito.

### <a name="13-userisexempted"></a>13: UserIsExempted

L'utente è esente dalla crittografia.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

L'utente ha richiesto un'esenzione.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Controllo esenzione utente non riuscito.

### <a name="16-userpostponed"></a>16: UserPostponed

L'utente ha rimandato il processo di crittografia.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

Inizializzazione TPM non riuscita. L'utente ha rifiutato le modifiche del BIOS.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Impossibile connettersi al servizio ripristino e hardware MBAM.

#### <a name="error-code--2147024809"></a>Codice di errore: -2147024809

Dettagli: il parametro non è corretto.

Questo errore si verifica se il sito Web non è HTTPS o il client non ha un certificato PKI.

### <a name="20-policymismatch"></a>20: PolicyMismatch

I criteri di gestione di BitLocker sono in conflitto o danneggiati.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Rilevato un conflitto nei criteri di crittografia del volume del sistema operativo. Controllare i criteri di BitLocker correlati alla protezione delle unità del sistema operativo.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Rilevato un conflitto nei criteri di crittografia del volume dell'unità dati fissa. Controllare i criteri di BitLocker correlati alla protezione dell'unità dati fissa.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Errore durante la crittografia. La protezione dell'agente recupero dati è necessaria in modalità FIPS per i computer precedenti a Windows 8.1.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Impossibile reimpostare il blocco del TPM.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Impossibile recuperare il valore OwnerAuth del TPM dai servizi MBAM.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Impossibile aggiornare il percorso di ricerca DLL per il provider WMI.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Arresto dell'agente in corso. Timeout durante l'attesa dell'istanza del provider WMI di MBAM.

## <a name="operational"></a>Operativo

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

I criteri di gestione di BitLocker sono stati applicati correttamente.

### <a name="3-transferstatusdatasuccessful"></a>3: TransferStatusDataSuccessful

Dati sullo stato di crittografia inviati correttamente.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Connessione al servizio ripristino e hardware MBAM completata.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

Il valore OwnerAuth del TPM è stato depositato.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

La chiave di ripristino BitLocker per il volume è stata depositata.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

La chiave di ripristino BitLocker per il volume è stata aggiornata.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

La data di applicazione dei criteri è stata impostata per il volume.

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

La data di applicazione dei criteri è stata cancellata per il volume.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

Il blocco del TPM è stato reimpostato.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

Il valore OwnerAuth del TPM è stato recuperato correttamente dai servizi MBAM.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

L'unità rimovibile è stata montata.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

L'unità rimovibile è stata smontata.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

La mancata connessione al servizio di hardware e ripristino di MBAM ha impedito l'applicazione dei criteri di gestione di BitLocker al volume.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Lo stato del volume bloccato ha impedito l'applicazione dei criteri di gestione di BitLocker al volume.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

La mancata connessione al servizio di conformità e stato di MBAM ha impedito il trasferimento dei dati sullo stato della crittografia.

## <a name="see-also"></a>Vedere anche

Per altre informazioni sull'uso di questi registri, vedere [Registri eventi di BitLocker](about-event-logs.md).

Per altre informazioni sulla risoluzione dei problemi, vedere [Risolvere i problemi relativi a BitLocker](troubleshoot.md).
