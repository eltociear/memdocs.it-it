---
title: Definizioni malware di Endpoint Protection da WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Informazioni su come configurare Windows Server Update Services per l'approvazione automatica degli aggiornamenti delle definizioni.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126030"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Abilitare le definizioni malware di Endpoint Protection da scaricare da WSUS per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Se si usa WSUS per mantenere aggiornate le definizioni antimalware, è possibile configurarlo per l'approvazione automatica degli aggiornamenti delle definizioni. Anche se l'uso degli aggiornamenti software di Configuration Manager è il metodo consigliato per mantenere aggiornate le definizioni, è anche possibile configurare WSUS come metodo per consentire agli utenti di aggiornare manualmente le definizioni. Usare le procedure seguenti per configurare WSUS come origine degli aggiornamenti delle definizioni.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Sincronizzare gli aggiornamenti delle definizioni per Configuration Manager

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e quindi selezionare **Siti**.

1. Selezionare il sito contenente il punto di aggiornamento software. Nel gruppo **Impostazioni** della barra multifunzione selezionare **Configura componenti del sito** e quindi selezionare **Punto di aggiornamento software**.

1. Nella finestra **Proprietà del componente del punto di aggiornamento software** passare alla scheda **Classificazioni**. Selezionare **Aggiornamenti delle definizioni**.

1. Per specificare i **prodotti** aggiornati con WSUS, passare alla scheda **Prodotti**.

    - Per Windows 10 e versioni successive: In Microsoft > Windows selezionare **Windows Defender**.

    - Per Windows 8.1 e versioni precedenti: In Microsoft > Forefront selezionare **System Center Endpoint Protection**.

1. Selezionare **OK** per chiudere la finestra **Proprietà del componente del punto di aggiornamento software**.

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Sincronizzare gli aggiornamenti delle definizioni per WSUS autonomo

Usare la procedura seguente per configurare gli aggiornamenti di Endpoint Protection se il server WSUS non è integrato nell'ambiente di Configuration Manager.

1. Nella console di amministrazione di WSUS espandere **Computer**, selezionare **Opzioni** e quindi selezionare **Prodotti e classificazioni**.

1. Per specificare i **prodotti** aggiornati con WSUS, passare alla scheda **Prodotti**.

    - Per Windows 10 e versioni successive: In Microsoft > Windows selezionare **Windows Defender**.

    - Per Windows 8.1 e versioni precedenti: In Microsoft > Forefront selezionare **System Center Endpoint Protection**.

1. Passare alla scheda **Classificazioni**. Selezionare **Aggiornamenti delle definizioni** e **Aggiornamenti**.

## <a name="approve-definition-updates"></a>Approvare gli aggiornamenti delle definizioni

Gli aggiornamenti delle definizioni di Endpoint Protection devono essere approvati e scaricati nel server WSUS per poter essere offerti ai client che richiedono l'elenco degli aggiornamenti disponibili. I client si connettono al server WSUS per verificare la disponibilità di aggiornamenti applicabili e quindi richiedono gli aggiornamenti delle definizioni approvati più recenti.

### <a name="approve-definitions-and-updates-in-wsus"></a>Approvare definizioni e aggiornamenti in WSUS

1. Nella console di amministrazione di WSUS selezionare **Aggiornamenti**. Selezionare quindi **Tutti gli aggiornamenti** o la classificazione degli aggiornamenti da approvare.

1. Nell'elenco degli aggiornamenti fare clic con il pulsante destro del mouse su uno o più aggiornamenti da approvare per l'installazione e quindi scegliere **Approva**.

1. Nella finestra **Approva aggiornamenti** selezionare il gruppo di computer per i quali si vogliono approvare gli aggiornamenti e quindi selezionare **Approvato per l'installazione**.

### <a name="configure-an-automatic-approval-rule"></a>Configurare una regola di approvazione automatica

È anche possibile impostare una regola di approvazione automatica per gli aggiornamenti delle definizioni e gli aggiornamenti di Endpoint Protection. In questo modo WSUS verrà configurato per approvare automaticamente gli aggiornamenti delle definizioni di Endpoint Protection scaricati da WSUS.

1. Nella console di amministrazione di WSUS selezionare **Opzioni** e quindi selezionare **Approvazioni automatiche**.

1. Nella scheda **Regole di aggiornamento** selezionare **Nuova regola**.

1. Nella finestra **Aggiungi regola**, in **Passaggio 1: selezionare le proprietà**, selezionare l'opzione: **Se l'aggiornamento è in una classificazione specifica**.

    1. In **Passaggio 2: modificare le proprietà** selezionare **qualsiasi classificazione**.

    1. Deselezionare tutte le opzioni ad eccezione di **Aggiornamenti delle definizioni** e quindi selezionare **OK**.

1. Nella finestra **Aggiungi regola**, in **Passaggio 1: selezionare le proprietà**, selezionare l'opzione: **Se l'aggiornamento è in un prodotto specifico**.

    1. In **Passaggio 2: modificare le proprietà** fare clic su **qualsiasi prodotto**.

    1. Deselezionare tutte le opzioni ad eccezione di **System Center Endpoint Protection** per Windows 8.1 e versioni precedenti o **Windows Defender** per Windows 10 e versioni successive. Selezionare **OK**.

1. In **Passaggio 3: specificare un nome** immettere un nome per la regola e quindi selezionare **OK**.

1. Nella finestra di dialogo **Approvazioni automatiche** selezionare la regola appena creata e quindi selezionare **Esegui regola**.

> [!NOTE]
> Per ottimizzare le prestazioni nei computer client e server WSUS, rifiutare gli aggiornamenti delle definizioni obsolete. A questo scopo, è possibile configurare l'approvazione automatica per le revisioni e il rifiuto automatico degli aggiornamenti scaduti. Per altre informazioni, vedere l'[articolo del supporto tecnico Microsoft 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Creare e distribuire criteri antimalware](endpoint-antimalware-policies.md)
