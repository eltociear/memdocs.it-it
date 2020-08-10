---
title: Installare il certificato mancante richiesto
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 162a5c2ff02a762578fb6f52b60b6ff404862329
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546709"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>Installare il certificato mancante richiesto dall'organizzazione  

Se il dispositivo non è registrato in Intune e manca un certificato specifico necessario, non sarà possibile accedere all'app Portale aziendale. Quando si tenta di accedere, verrà visualizzato il messaggio seguente:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Si può provare a scaricare il certificato necessario e registrare il dispositivo in due modi. 

- Abilitare l'accesso al browser nell'app Portale aziendale.
- Identificare il certificato mancante in un PC della società o dell'istituto di istruzione. Eseguire quindi una ricerca in Internet per scaricare il certificato mancante. 

Prima di tutto, completare i passaggi per abilitare l'accesso al browser. Successivamente, se non è ancora possibile registrare il dispositivo, seguire la procedura per trovare il certificato in Internet. 

## <a name="enable-browser-access"></a>Abilitare l'accesso al browser
Completare questi passaggi per abilitare l'accesso al browser. Dopo aver abilitato l'accesso, l'app Portale aziendale installerà il certificato appropriato e continuerà la registrazione.    

1. Nell'app Portale aziendale selezionare il menu nell'angolo a destra.  
2. Selezionare **Impostazioni**.  
3. Accanto ad **Abilita l'accesso al browser** selezionare **Abilita**.  
4. Nella schermata relativa all'amministratore del dispositivo selezionare **ATTIVA**. 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>Identificare e scaricare il certificato mancante tramite la ricerca sul Web
Completare questi passaggi per identificare e installare manualmente il certificato nel dispositivo.  

1. In un PC aprire Internet Explorer. Se non si ha un PC da usare per questo scopo, contattare il supporto tecnico dell'azienda. Per le informazioni di contatto del supporto tecnico dell'azienda, vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).

2. Passare al [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980) ed eseguire l'accesso con le credenziali della società o dell'istituto di istruzione.

3. All'estrema destra della barra degli indirizzi del browser, fare clic sul simbolo simile a un lucchetto, come illustrato di seguito.

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    Se non viene visualizzato il simbolo di un lucchetto, interrompere la procedura e contattare il supporto tecnico dell'azienda. Il lucchetto indica che l'accesso viene eseguito in modalità sicura. Se quindi non si visualizza tale simbolo, è consigliabile non procedere.

4. Fare clic su **Visualizza certificati**.

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. Scegliere la scheda **Percorso certificazione** e identificare il certificato che è necessario ottenere da Internet. Il nome del certificato necessario si trova nello stesso percorso di quello evidenziato nella schermata di esempio precedente.

6. Con un motore di ricerca come Bing o Google, cercare il nome del certificato mancante identificato nella sezione precedente. Il certificato può avere varie "estensioni", ad esempio "crt" o "pem" e così via.

7. Scaricare il certificato radice dal sito Web.

8. Dopo aver scaricato il certificato, trascinare verso il basso dalla parte superiore del dispositivo per aprire le notifiche e quindi toccare il nome del certificato nell'elenco delle notifiche.

4. Nella finestra di dialogo **Name the Certificate** (Denominare il certificato) illustrata nella schermata seguente, accettare il nome predefinito.

5. Verificare che l'uso delle **credenziali** sia impostato su **VPN e app**, quindi fare clic su **OK**.

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. Chiudere l'app Portale aziendale.

7. Aprire nuovamente l'app Portale aziendale. Accedere all'app Portale aziendale. Per assistenza, contattare il supporto tecnico dell'azienda.

Se viene visualizzato di nuovo il messaggio "Certificato mancante" illustrato in precedenza ed è già stata eseguita la relativa procedura, è probabile che sia necessario installare un altro certificato con l'assistenza del supporto tecnico dell'azienda. Per indicazioni sull'uso delle informazioni di contatto disponibili nel [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980), contattare il supporto tecnico dell'azienda.

## <a name="next-steps"></a>Passaggi successivi  

Serve ancora assistenza? Contattare l'amministratore IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  
