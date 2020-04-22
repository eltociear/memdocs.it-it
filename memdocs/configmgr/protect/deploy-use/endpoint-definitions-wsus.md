---
title: Definizioni malware di Endpoint Protection da WSUS
titleSuffix: Configuration Manager
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Informazioni su come configurare Windows Server Update Services per l'approvazione automatica degli aggiornamenti delle definizioni.
manager: dougeby
ms.openlocfilehash: 301a3f318e836f2501a25ae65ebb61173b8e6231
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697209"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Abilitare le definizioni malware di Endpoint Protection da scaricare da Windows Server Update Services (WSUS) per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 Se si usa WSUS per mantenere aggiornate le definizioni antimalware, è possibile configurarlo per l'approvazione automatica degli aggiornamenti delle definizioni. Anche se l'uso degli aggiornamenti software di Configuration Manager è il metodo consigliato per mantenere aggiornate le definizioni, è anche possibile configurare WSUS come metodo per consentire agli utenti di avviare manualmente l'aggiornamento delle definizioni. Usare le procedure seguenti per configurare WSUS come origine degli aggiornamenti delle definizioni.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>Per sincronizzare gli aggiornamenti delle definizioni di Endpoint Protection in Configuration Manager

1. Nella console di Configuration Manager fare clic su **Amministrazione**.

2. Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.

3. Selezionare il sito contenente il punto di aggiornamento software. Nel gruppo **Impostazioni** fare clic su **Configura componenti del sito**e quindi su **Punto di aggiornamento software**.

4. Nella scheda **Classificazioni** della finestra di dialogo **Proprietà del componente del punto di aggiornamento software** selezionare la casella di controllo **Aggiornamenti delle definizioni** .

5. Specificare i **Prodotti** aggiornati con WSUS:

   -   Per Windows 8.1 e versioni precedenti, nella scheda **Prodotti** della finestra di dialogo **Proprietà del componente del punto di aggiornamento software** selezionare la casella di controllo **Forefront Endpoint Protection 2010** .

   -   Per Windows 10 e versioni successive, nella scheda **Prodotti** della finestra di dialogo **Proprietà del componente del punto di aggiornamento software** selezionare la casella di controllo **Windows Defender**.

6. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà del componente del punto di aggiornamento software** .

   Seguire la procedura seguente per configurare gli aggiornamenti di Endpoint Protection se il server WSUS non è integrato nell'ambiente di Configuration Manager.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>Per sincronizzare gli aggiornamenti delle definizioni di Endpoint Protection in un'istanza autonoma di WSUS

1.  Nella console di amministrazione di WSUS espandere **Computer**, fare clic su **Opzioni**e quindi fare clic su **Prodotti e classificazioni**.

2.  Specificare i **Prodotti** aggiornati con WSUS:

    -   Per Windows 8.1 e versioni precedenti, nella scheda **Prodotti** della finestra di dialogo **Proprietà del componente del punto di aggiornamento software** selezionare la casella di controllo **Forefront Endpoint Protection 2010** .

    -   Per Windows 10 e versioni successive, nella scheda **Prodotti** della finestra di dialogo **Proprietà del componente del punto di aggiornamento software** selezionare la casella di controllo **Windows Defender**.

3.  Nella scheda **Classificazioni** della finestra di dialogo **Prodotti e classificazioni** selezionare le caselle di controllo **Aggiornamenti delle definizioni** e **Aggiornamenti** .

## <a name="approving-definition-updates"></a>Approvazione degli aggiornamenti delle definizioni
 Gli aggiornamenti delle definizioni di Endpoint Protection devono essere approvati e scaricati nel server WSUS per poter essere offerti ai client che richiedono l'elenco degli aggiornamenti disponibili. I client si connettono al server WSUS per verificare la disponibilità di aggiornamenti applicabili e quindi richiedono gli aggiornamenti delle definizioni approvati più recenti.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>Per approvare definizioni e aggiornamenti in WSUS

1. Nella console di amministrazione di WSUS fare clic su **Aggiornamenti**e quindi su **Tutti gli aggiornamenti** o sulla classificazione degli aggiornamenti da approvare.

2. Nell'elenco degli aggiornamenti fare clic con il pulsante destro del mouse su uno o più aggiornamenti da approvare per l'installazione e quindi scegliere **Approva**.

3. Nella finestra di dialogo **Approva aggiornamenti** selezionare il gruppo di computer per i quali approvare gli aggiornamenti e quindi fare clic su **Approvato per l'installazione**.

   Oltre all'approvazione manuale, è anche possibile impostare una regola di approvazione automatica degli aggiornamenti delle definizioni e degli aggiornamenti di Endpoint Protection. In questo modo, WSUS verrà configurato per approvare automaticamente gli aggiornamenti delle definizioni di Endpoint Protection scaricati da WSUS.

### <a name="to-configure-an-automatic-approval-rule"></a>Per configurare una regola di approvazione automatica

1.  Nella console di amministrazione di WSUS fare clic su **Opzioni**e quindi su **Approvazioni automatiche**.

2.  Nella scheda **Regole di aggiornamento** fare clic su **Nuova regola**.

3.  Nella finestra di dialogo **Aggiungi regola** in **Passaggio 1: Selezionare le proprietà** selezionare la casella di controllo **Se l'aggiornamento è in una classificazione specifica**.

4.  In **Passaggio 2: Modificare le proprietà** fare clic su **qualsiasi classificazione**.

5.  Deselezionare tutte le caselle di controllo ad eccezione di **Aggiornamenti delle definizioni**e quindi fare clic su **OK**.

6.  Nella finestra di dialogo **Aggiungi regola** in **Passaggio 1: Selezionare le proprietà** selezionare la casella di controllo **Se l'aggiornamento è in un prodotto specifico**.

7.  In **Passaggio 2: Modificare le proprietà** fare clic su **qualsiasi prodotto**.

8.  Deselezionare tutte le caselle di controllo ad eccezione di **Forefront Endpoint Protection** per Windows 8.1 e versioni precedenti o **Windows Defender** per Windows 10 e versioni successive e quindi fare clic su **OK**.

9. In **Passaggio 3: Specificare un nome** immettere un nome per la regola e quindi fare clic su **OK**.

10. Nella finestra di dialogo **Approvazioni automatiche** selezionare la casella di controllo per la regola appena creata e quindi fare clic su **Esegui regola**.

> [!NOTE]
>  Per ottimizzare le prestazioni nei computer client e server WSUS, rifiutare gli aggiornamenti delle definizioni obsolete. A questo scopo, è possibile configurare l'approvazione automatica per le revisioni e il rifiuto automatico degli aggiornamenti scaduti. Per altre informazioni, vedere l' [articolo 938947 della Microsoft Knowledge Base](https://go.microsoft.com/fwlink/p/?LinkId=204078).
> 
> [!div class="button"]
> [Passaggio successivo >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Indietro >](endpoint-configure-alerts.md)
