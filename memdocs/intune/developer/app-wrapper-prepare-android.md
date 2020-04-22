---
title: Eseguire il wrapping delle app Android con lo strumento di wrapping delle app di Intune
description: Informazioni su come eseguire il wrapping delle app Android senza modificarne il codice. Preparare le app in modo da applicare i criteri di gestione delle app mobili.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e9c349c8-51ae-4d73-b74a-6173728a520b
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7fd1a1567096f804b56c5f141fccfc825f4a02e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79360314"
---
# <a name="prepare-android-apps-for-app-protection-policies-with-the-intune-app-wrapping-tool"></a>Preparare le app Android per i criteri di protezione delle app con lo strumento di wrapping delle app di Intune

Usare lo strumento di wrapping delle app di Microsoft Intune per Android per modificare il comportamento delle app Android interne, limitandone le funzionalità senza modificare il codice.

Lo strumento è un'applicazione della riga di comando di Windows che viene eseguito in PowerShell e crea un wrapper intorno all'app Android. Dopo aver eseguito il wrapping dell'app, è possibile modificarne le funzionalità configurando i [criteri di gestione delle app mobili](../apps/app-protection-policies.md) in Intune.

Prima di eseguire lo strumento, vedere [Considerazioni sulla sicurezza per l'esecuzione dello strumento di wrapping delle app](#security-considerations-for-running-the-app-wrapping-tool). Per scaricare lo strumento, visitare la pagina dello [strumento di wrapping delle app di Microsoft Intune per Android](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android) in GitHub.

## <a name="fulfill-the-prerequisites-for-using-the-app-wrapping-tool"></a>Soddisfare i prerequisiti per l'uso dello strumento di wrapping delle app

- È necessario eseguire lo strumento di wrapping delle app in un computer Windows che esegue Windows 7 o versioni successive.

- L'app di input deve essere un pacchetto di applicazione Android valido con estensione apk e:

  - Non può essere crittografata.
  - Non può essere stata sottoposta a wrapping in precedenza con lo strumento di wrapping delle app di Intune.
  - Deve essere scritta per Android 4.0 o versione successiva.

- L'app deve essere sviluppata da o per l'azienda. Non è possibile usare questo strumento su app scaricate da Google Play Store.

- Per eseguire lo strumento di wrapping delle app, è necessario installare la versione più recente di [Java Runtime Environment](https://java.com/download/) e quindi assicurarsi che la variabile del percorso Java sia stata impostata su C:\ProgramData\Oracle\Java\javapath nelle variabili di ambiente Windows. Per altre informazioni vedere la [documentazione Java](https://java.com/download/help/).

    > [!NOTE]
    > In alcuni casi, la versione a 32 bit di Java può causare problemi di memoria. È consigliabile installare la versione a 64 bit.

- Android richiede che tutti i pacchetti dell'app (con estensione apk) siano firmati. Per informazioni sul **riutilizzo** di certificati esistenti e linee guida generali per la firma dei certificati, vedere [Riutilizzo dei certificati di protezione ed esecuzione del wrapping delle app](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps). L'eseguibile Java keytool.exe consente di generare le **nuove** credenziali necessarie per firmare l'app di output di cui è stato eseguito il wrapping. Qualsiasi password impostata deve essere sicura, ma prenderne nota perché saranno necessarie per eseguire lo strumento di wrapping delle app.

    > [!NOTE]
    > Lo strumento di wrapping delle app di Intune non supporta gli schemi di firma v2 e v3 (in arrivo) di Google per la firma delle app. Dopo avere eseguito il wrapping del file con estensione apk usando lo strumento di wrapping delle app di Intune, si consiglia di usare [lo strumento Apksigner fornito di Google]( https://developer.android.com/studio/command-line/apksigner). Ciò garantisce che una volta installata nei dispositivi degli utenti finali, l'app possa essere avviata correttamente secondo gli standard Android. 

- (Facoltativo) In alcuni casi un'app può raggiungere il limite di dimensioni DEX (Dalvik Executable) a causa delle classi MAM SDK di Intune aggiunte durante il wrapping. I file DEX fanno parte della compilazione di un'app per Android. App Wrapping Tool di Intune gestisce automaticamente l'overflow dei file DEX durante il wrapping per le app con un livello API minimo pari a 21 o superiore (per la versione [ 1.0.2501.1](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android/releases)). Per le app con un livello API minimo < 21, la procedura consigliata è di aumentare tale livello usando il flag `-UseMinAPILevelForNativeMultiDex` del wrapper. Per i clienti che non sono in grado di aumentare il livello API minimo dell'app, sono disponibili le soluzioni alternative seguenti per l'overflow dei file DEX. In alcune organizzazioni potrebbe essere necessario collaborare con gli utenti che compilano l'app, ad esempio il team di compilazione dell'app:

  - Usare Proguard per eliminare i riferimenti a classi non usati dal file DEX principale dell'app.
  - Per i clienti che usano la versione 3.1.0 o una versione successiva del plug-in Android Gradle, disabilitare [D8 dexer](https://android-developers.googleblog.com/2018/04/android-studio-switching-to-d8-dexer.html).  

## <a name="install-the-app-wrapping-tool"></a>Installare lo strumento di wrapping delle app

1. Dal [repository GitHub](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android) scaricare il file di installazione InstallAWT.exe dello strumento di wrapping delle app di Intune per Android in un computer Windows. Aprire il file di installazione.

2. Accettare il contratto di licenza e quindi finire l'installazione.

Prendere nota della cartella in cui è installato lo strumento. Il percorso predefinito è: C:\Programmi (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool.

## <a name="run-the-app-wrapping-tool"></a>Eseguire lo strumento di wrapping delle app

1. Nel computer di Windows in cui è stato installato lo strumento di wrapping delle app, aprire una finestra di PowerShell.

2. Dalla cartella in cui è installato lo strumento, importare il modulo di PowerShell dello strumento di wrapping delle app:

   ```PowerShell
   Import-Module .\IntuneAppWrappingTool.psm1
   ```

3. Eseguire lo strumento usando il comando **invoke-AppWrappingTool** che ha la sintassi seguente:

   ```PowerShell
   Invoke-AppWrappingTool [-InputPath] <String> [-OutputPath] <String> -KeyStorePath <String> -KeyStorePassword <SecureString>
   -KeyAlias <String> -KeyPassword <SecureString> [-SigAlg <String>] [<CommonParameters>]
   ```

   La tabella che segue descrive le proprietà del comando **invoke-AppWrappingTool**:

|Proprietà|Informazioni|Esempio|
|-------------|--------------------|---------|
|**-InputPath**&lt;Stringa&gt;|Percorso dell'app Android di origine (.apk).| |
 |**-OutputPath**&lt;Stringa&gt;|Percorso dell'app Android di output. Se il percorso della directory è uguale a quello per InputPath, il pacchetto non riuscirà.| |
|**-KeyStorePath**&lt;Stringa&gt;|Percorso del file dell'archivio chiavi che contiene la coppia di chiavi pubblica/privata per la firma.|Per impostazione predefinita i file dell'archivio chiavi vengono archiviati in "C:\Programmi (x86)\Java\jreX.X.X_XX\bin". |
|**-KeyStorePassword**&lt;SecureString&gt;|Password usata per decrittografare il file keystore. Android richiede che tutti i pacchetti di applicazioni (con estensione apk) siano firmati. Usare keytool Java per generare KeyStorePassword. Altre informazioni sulla classe KeyStore Java sono disponibili [qui](https://docs.oracle.com/javase/7/docs/api/java/security/KeyStore.html).| |
|**-KeyAlias**&lt;Stringa&gt;|Nome della chiave da usare per la firma.| |
|**-KeyPassword**&lt;SecureString&gt;|Password usata per decrittografare la chiave privata da usare per la firma.| |
|**-SigAlg**&lt;SecureString&gt;| (Facoltativo) Nome dell'algoritmo di firma da usare per la firma. L'algoritmo deve essere compatibile con la chiave privata.|Esempi: SHA256withRSA, SHA1withRSA|
|**-UseMinAPILevelForNativeMultiDex**| (Facoltativo) Usare questo flag per aumentare il livello API minimo dell'app Android di origine a 21. Questo flag richiederà una conferma perché limiterà chi potrà installare l'app. Gli utenti possono ignorare la finestra di dialogo di conferma aggiungendo il parametro "-Confirm:$false" al comando di PowerShell. Il flag deve essere usato dai clienti nelle app con livello API minimo < 21 che non riescono a eseguire correttamente il wrapping a causa di errori di overflow DEX. | |
| **&lt;Parametri comuni&gt;** | (Facoltativo) Il comando supporta parametri PowerShell comuni, come verbose e debug. |


- Per un elenco di parametri comuni, vedere il [Microsoft Script Center](https://technet.microsoft.com/library/hh847884.aspx).

- Per visualizzare informazioni dettagliate sull'uso dello strumento, immettere il seguente comando:

    ```PowerShell
    Help Invoke-AppWrappingTool
    ```

**Esempio:**

Importare il modulo PowerShell.

```PowerShell
Import-Module "C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool\IntuneAppWrappingTool.psm1"
```

Eseguire lo strumento di wrapping delle app sull'app nativa HelloWorld.apk.

```PowerShell
invoke-AppWrappingTool -InputPath .\app\HelloWorld.apk -OutputPath .\app_wrapped\HelloWorld_wrapped.apk -KeyStorePath "C:\Program Files (x86)\Java\jre1.8.0_91\bin\mykeystorefile" -keyAlias mykeyalias -SigAlg SHA1withRSA -Verbose
```

Verranno quindi richiesti i valori di **KeyStorePassword** e **KeyPassword**. Immettere le credenziali usate per creare il file keystore.

L'applicazione sottoposta a wrapping e un file di log vengono generati e salvati nel percorso di output specificato.

## <a name="how-often-should-i-rewrap-my-android-application-with-the-intune-app-wrapping-tool"></a>Con quale frequenza è necessario eseguire nuovamente il wrapping dell'applicazione Android con lo strumento per la disposizione testo per app di Microsoft Intune?
Gli scenari principali in cui è necessario eseguire nuovamente il wrapping delle applicazioni sono i seguenti:
* L'applicazione ha rilasciato una nuova versione. La versione precedente dell'app è stata sottoposta a wrapping e caricata nella console di Intune.
* Lo strumento per la disposizione testo per app di Microsoft Intune per Android ha rilasciato una nuova versione che consente di eseguire le principali correzioni di bug o che dispone di nuove e specifiche funzionalità con criteri di protezione per applicazioni Intune. Ciò avviene ogni 6-8 settimane tramite il repository GitHub per lo [strumento per la disposizione testo per app di Microsoft Intune per Android](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android).

Alcune procedure consigliate per eseguire nuovamente il wrapping comprendono: 
* Conservazione dei certificati di protezione utilizzati durante il processo di compilazione, vedere [Riutilizzo dei certificati di protezione ed esecuzione del wrapping delle app](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps)

## <a name="reusing-signing-certificates-and-wrapping-apps"></a>Riutilizzo dei certificati di protezione ed esecuzione del wrapping delle app
Android richiede che tutte le app siano firmate da un certificato valido per essere installate nei dispositivi Android.

Le app sottoposte a wrapping possono essere firmate nell'ambito di un processo di wrapping o *successivamente* tramite gli strumenti di firma esistenti. Le informazioni sulla firma presenti nell'app prima del wrapping vengono eliminate. Se possibile, nell'esecuzione del wrapping è consigliabile usare le informazioni sulla firma già usate durante il processo di compilazione. In alcune organizzazioni potrebbe essere necessario collaborare con gli utenti in possesso delle informazioni sull'archivio chiavi, ad esempio il team di compilazione dell'app. 

Se non è possibile usare il certificato di firma precedente o se l'app non è stata distribuita in precedenza, è possibile creare un nuovo certificato di firma seguendo le istruzioni descritte nella [Guida per gli sviluppatori Android](https://developer.android.com/studio/publish/app-signing.html#signing-manually).

Se l'app è stata distribuita in precedenza con un certificato di firma diverso, non è possibile caricarla in Intune dopo l'aggiornamento. Gli scenari di aggiornamento dell'app vengono interrotti nel caso in cui l'app sia stata firmata con un certificato diverso da quello con cui è stata compilata. Di conseguenza, è necessario mantenere i nuovi certificati di firma per gli aggiornamenti delle app. 

## <a name="security-considerations-for-running-the-app-wrapping-tool"></a>Considerazioni sulla sicurezza per l'esecuzione dello strumento di wrapping delle app
Per evitare potenziali attacchi di spoofing, divulgazione di informazioni e l'elevazione dei privilegi:

- Assicurarsi che l'applicazione line-of-business (LOB) di input, l'applicazione di output e Java KeyStore siano nello stesso computer Windows in cui è in esecuzione lo strumento di wrapping delle app.

- Importare l'applicazione di output in Intune, nello stesso computer in cui è in esecuzione lo strumento. Per altre informazioni sullo strumento keytool Java, vedere [keytool](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/keytool.html).

- Se l'applicazione di output e lo strumento si trovano in un percorso UNC (Universal Naming Convention) e non si eseguono lo strumento e il file di input nello stesso computer, configurare l'ambiente per la protezione con [IPSec (Internet Protocol Security)](https://wikipedia.org/wiki/IPsec) o la [firma SMB (Server Message Block)](https://support.microsoft.com/kb/887429).

- Assicurarsi che l'applicazione provenga da una fonte attendibile.

- Proteggere la directory di output che contiene l'applicazione di cui è stato eseguito il wrapping. È possibile utilizzare una directory a livello di utente per l'output.

## <a name="see-also"></a>Vedere anche
- [Stabilire come preparare le app per la gestione delle applicazioni mobili con Microsoft Intune](../developer/apps-prepare-mobile-application-management.md)

- [Guida a Microsoft Intune App SDK per sviluppatori di Android](../developer/app-sdk-android.md)
