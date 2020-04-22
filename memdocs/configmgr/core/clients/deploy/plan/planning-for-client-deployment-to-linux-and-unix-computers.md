---
title: Pianificazione della distribuzione del client per computer Linux e UNIX
titleSuffix: Configuration Manager
description: Pianificare la distribuzione del client in computer Linux e UNIX in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693729"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Pianificazione della distribuzione del client in computer Linux e UNIX in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

> [!Important]  
> A partire dalla versione 1902, Configuration Manager non supporta i client Linux o UNIX. 
> 
> Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.

È possibile installare il client di Configuration Manager nei computer che eseguono Linux o UNIX. Questo client è progettato per i server che funzionano come computer di un gruppo di lavoro e il client non supporta l'interazione con gli utenti connessi. Dopo aver installato il software client e dopo che il client ha stabilito la comunicazione con il sito di Configuration Manager, gestire il client usando la console e i report di Configuration Manager.  

> [!NOTE]
>  Il client di Configuration Manager per computer Linux e UNIX non supporta le funzionalità di gestione seguenti:  
> 
> - Installazione push client  
>   -   Distribuzione del sistema operativo  
>   -   Distribuzione di applicazioni; in alternativa, distribuire il software usando pacchetti e programmi.  
>   -   Inventario software  
>   -   Aggiornamenti software  
>   -   Impostazioni di conformità  
>   -   Controllo remoto  
>   -   Risparmio energia  
>   -   Controllo e correzione client dello stato client  
>   -   Gestione client basata su Internet  

 Per informazioni sulle distribuzioni Linux e UNIX supportate e sull'hardware necessario per supportare il client per Linux e UNIX, vedere [Hardware consigliato per Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Usare le informazioni contenute in questo articolo per pianificare la distribuzione del client di Configuration Manager per Linux e UNIX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a> Prerequisiti per la distribuzione del client ai server Linux e UNIX  
 Utilizzare le informazioni seguenti per determinare i prerequisiti, di che è necessario disporre correttamente in grado installare il client per Linux e UNIX.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a> Dipendenze esterne a Configuration Manager:  
 Nella tabella seguente vengono descritti i sistemi UNIX e Linux e le dipendenze dei pacchetti necessari.  

 **Red Hat Enterprise Linux Server versione 5.1 (Tikanga)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Librerie standard C|2.5-12|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8b-8.3.el5|  
|PAM|Moduli di autenticazione plug-in|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server versione 6**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Librerie standard C|2.12-1.7|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Moduli di autenticazione plug-in|1.1.1-4|  

 **Red Hat Enterprise Linux Server versione 7**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Librerie standard C|2.17|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|1.0.1|  
|PAM|Moduli di autenticazione plug-in|1.1.1-4|  

 **Solaris 10 SPARC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Patch richiesta del sistema operativo|Problemi di memoria PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|SUNopenssl-librararies (Usr)<br /><br /> Sun fornisce le librerie OpenSSL per Solaris 10 SPARC, che vengono aggregate al sistema operativo.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Moduli di autenticazione plug-in<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Patch richiesta del sistema operativo|Problemi di memoria PAM|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10, REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Shared Libs) (i386)|11.10.0, REV=2005.01.21.16.34|  
|SUNWcslr|Core Solaris Libraries (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|SUNWopenssl-libraries; OpenSSL Libraries (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Moduli di autenticazione plug-in<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0, REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Libreria condivisa standard C|2.4-31.30|  
|OpenSSL|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8a-18.15|  
|PAM|Moduli di autenticazione plug-in|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Libreria condivisa standard C|2.9-13.2|  
|PAM|Moduli di autenticazione plug-in|pam-1.0.2-20.1|  

 **Universal Linux (pacchetto Debian) Debian, Ubuntu Server**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|libc6|Libreria condivisa standard C|2.3.6|  
|OpenSSL|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8 o 1.0|  
|PAM|Moduli di autenticazione plug-in|0.79-3|  

 **Universal Linux (pacchetto RPM) CentOS, Oracle Linux**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|glibc|Libreria condivisa standard C|2.5-12|  
|Openssl|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8 o 1.0|  
|PAM|Moduli di autenticazione plug-in|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Versione sistema operativo|Versione del sistema operativo|AIX 6.1: qualsiasi Technology Level e Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|Librerie OpenSSL; Secure Network Communications Protocol|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|Versione sistema operativo|Versione del sistema operativo|AIX 7.1: qualsiasi Technology Level e Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|Librerie OpenSSL; Secure Network Communications Protocol||  


 **HP-UX 11i v3 IA64**  

|Pacchetto necessario|Descrizione|Versione minima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Librerie di sviluppo specifico IA|B.11.31|  
|SysMgmtMin|Strumenti minimi di distribuzione software|B.11.31.0709|  
|SysMgmtMin.openssl|Librerie OpenSSL; Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Moduli di autenticazione plug-in|PAM fa parte dei componenti principali del sistema operativo di HP-UX. Non ci sono altre dipendenze.|  

 **Dipendenze di Configuration Manager:** la tabella seguente elenca i ruoli di sistema del sito che supportano client Linux e UNIX. Per altre informazioni su questi ruoli del sistema del sito, vedere [Determinare i ruoli del sistema del sito per i client di Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistema del sito di Configuration Manager|Altre informazioni|  
|---------------------------------------|----------------------|  
|Punto di gestione|Anche se non è necessario un punto di gestione per installare un client di Configuration Manager per Linux e UNIX, è invece necessario un punto di gestione per trasferire informazioni tra i computer client e i server di Configuration Manager. Senza un punto di gestione, non è possibile gestire i computer client.|  
|Punto di distribuzione|Il punto di distribuzione non è necessario per installare un client di Configuration Manager per Linux e UNIX. Tuttavia, il ruolo del sistema del sito è necessario se si distribuisce software per server Linux e UNIX.<br /><br /> Poiché il client di Configuration Manager per Linux e UNIX non supporta le comunicazioni che usano SMB, i punti di distribuzione usati con il client devono supportare la comunicazione HTTP o HTTPS.|  
|Punto di stato di fallback|Il punto di stato di fallback non è necessario per installare un client di Configuration Manager per Linux e UNIX. Il punto di stato di fallback consente tuttavia ai computer nel sito di Configuration Manager di inviare messaggi di stato quando non possono comunicare con un punto di gestione. Client può inoltre inviare lo stato dell'installazione per il punto di stato di fallback.|  

 **Requisiti firewall**: verificare che i firewall non blocchino le comunicazioni tra le porte specificate come porte di richiesta client. Il client per Linux e UNIX comunica direttamente con i punti di gestione, i punti di distribuzione e i punti di stato di fallback.  

 Per informazioni sulle comunicazioni client e sulle porte di richiesta, vedere  [Configurare il Client per Linux e UNIX individuare i punti di gestione](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a> Pianificazione delle comunicazioni attraverso trust tra foreste per server Linux e UNIX  
 I server Linux e UNIX gestiti con Configuration Manager funzionano come client di un gruppo di lavoro e richiedono configurazioni simili ai client basati su Windows che si trovano in un gruppo di lavoro. Per informazioni sulle comunicazioni provenienti da computer che si trovano in gruppi di lavoro, vedere [Comunicazioni tra foreste Active Directory](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a> Posizione del servizio dal client per Linux e UNIX  
 L'attività di individuazione di un server di sistema del sito che offre servizi ai client viene considerato come percorso del servizio. A differenza di un client basato su Windows, il client per Linux e UNIX non usa Active Directory per la posizione del servizio. Il client di Configuration Manager per Linux e UNIX non supporta inoltre una proprietà client che specifica il suffisso di dominio di un punto di gestione. Al contrario, il client conosciuti da server del sistema del sito aggiuntivi che forniscono servizi ai client da un punto di gestione noti che viene assegnato quando si installa il software client.  

 Per altre informazioni, vedere [Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a> Pianificazione di sicurezza e certificati per server Linux e UNIX  
 Per comunicazioni autenticate e protette con i siti di Configuration Manager, il client di Configuration Manager per Linux e UNIX usa lo stesso modello per la comunicazione del client di Configuration Manager per Windows.  

 Quando si installa il client Linux e UNIX, è possibile assegnare il client di un certificato PKI che consente di usare HTTPS per comunicare con i siti di Configuration Manager. Se non si assegna un certificato PKI, il client crea un certificato autofirmato e comunica solo tramite HTTP.  

 I client a cui viene fornito un certificato PKI durante l'installazione usano HTTPS per comunicare con i punti di gestione. Se un client non riesce a rilevare un punto di gestione che supporta HTTPS, tornerà a usare HTTP con il certificato PKI fornito.  

 Quando un client Linux o UNIX usa un certificato PKI, non è necessaria l'approvazione. Se un client usa un certificato autofirmato, verificare le impostazioni di gerarchia per l'approvazione client nella console di Configuration Manager. Se non è il metodo di approvazione client **approvare automaticamente tutti i computer (scelta non consigliati)** , è necessario approvare manualmente il client.  

 Per altre informazioni sull'approvazione manuale del client, vedere [Gestire i client dal nodo Dispositivi](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Per informazioni su come usare i certificati in Configuration Manager, vedere [Requisiti dei certificati PKI](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a> Informazioni sui certificati per l'uso da server Linux e UNIX  
 Il client di Configuration Manager per Linux e UNIX usa un certificato autofirmato o un certificato x. 509 PKI come i client basati su Windows. Non ci sono modifiche ai requisiti di infrastruttura a chiave pubblica (PKI) per i sistemi del sito di Configuration Manager quando si gestiscono client Linux e UNIX.  

 I certificati usati per i client Linux e UNIX che comunicano con i sistemi del sito di Configuration Manager devono essere in formato Public Key Certificate Standard (PKCS #12) e la password deve essere nota, in modo che sia possibile specificarla al client quando si specifica il certificato PKI.  

 Il client di Configuration Manager per Linux e UNIX supporta un singolo certificato PKI e non supporta certificati multipli. I criteri di selezione del certificato da configurare per un sito di Configuration Manager non sono quindi validi.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a> Configurazione dei certificati per server Linux e UNIX  
 Per configurare un client di Configuration Manager per i server Linux e UNIX per usare le comunicazioni HTTPS, è necessario configurare il client per usare un certificato PKI quando si installa il client. Non è possibile effettuare il provisioning di un certificato prima dell'installazione del software client.  

 Quando si installa un client che usa un certificato PKI, si usa il parametro della riga di comando `-UsePKICert` per specificare il percorso e il nome di un file PKCS#12 che contiene il certificato PKI. È inoltre necessario usare il parametro della riga di comando `-certpw` per specificare la password per il certificato.  

 Se non si specifica `-UsePKICert`, il client genera un certificato autofirmato e cerca di comunicare con i server di sistema del sito solo tramite HTTP.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a> Versioni che non supportano SHA-256  
 I sistemi operativi Linux e UNIX seguenti supportati come client per Configuration Manager sono stati rilasciati con le versioni di OpenSSL che non supportano SHA-256:  

-   Solaris versione 10 (SPARC/x86)  


 Per gestire questi sistemi operativi con Configuration Manager, è necessario installare il client di Configuration Manager per Linux e UNIX con un'opzione della riga di comando che indichi al client di ignorare la convalida di SHA-256. I client di Configuration Manager eseguiti in queste versioni del sistema operativo operano in una modalità meno sicura rispetto ai client che supportano SHA-256. Questa modalità meno sicura dell'operazione presenta il seguente comportamento:  

-   I client non convalidano la firma del server del sito associata ai criteri richiesti da un punto di gestione.  

-   I client non convalidano l'hash per i pacchetti scaricati da un punto di distribuzione.  

> [!IMPORTANT]  
>  L'opzione `ignoreSHA256validation` consente di eseguire il client per computer Linux e UNIX in una modalità meno sicura. Questo deve essere utilizzato su piattaforme precedenti che non include il supporto per SHA-256. È un override di sicurezza e non è consigliato da Microsoft, ma è supportato l'utilizzo in un ambiente sicuro e attendibile datacenter.  

 Quando si installa il client di Configuration Manager per Linux e UNIX, lo script di installazione verifica la versione del sistema operativo. Per impostazione predefinita, se la versione del sistema operativo viene identificata come rilasciata senza una versione di OpenSSL che supporta SHA-256, l'installazione del client di Configuration Manager non riesce.  

 Per installare il client di Configuration Manager nei sistemi operativi Linux e UNIX che non sono stati rilasciati con una versione di OpenSSL che supporta SHA-256, è necessario usare l'opzione della riga di comando di installazione `ignoreSHA256validation`. Quando si usa questa opzione della riga di comando in un sistema operativo Linux o UNIX applicabile, il client di Configuration Manager ignora la convalida di SHA-256 e dopo l'installazione, il client non userà SHA-256 per firmare i dati inviati ai sistemi del sito tramite HTTP. Per informazioni sulla configurazione dei client Linux e UNIX per usare i certificati, vedere [Pianificazione di sicurezza e certificati per server Linux e UNIX](#BKMK_SecurityforLnU). Per altre informazioni sulle richieste di SHA-256, vedere [Configurare la firma e la crittografia](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  L'opzione della riga di comando `ignoreSHA256validation` viene ignorata nei computer che eseguono una versione di Linux e UNIX rilasciata con versioni di OpenSSL che supportano SHA-256.  
