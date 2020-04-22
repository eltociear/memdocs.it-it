---
title: Ottenere una chiave di ripristino per un dispositivo macOS dal sito Web Portale aziendale Intune
description: Visualizzare la chiave di ripristino per un dispositivo macOS registrato e gestito.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5a15f3a05f96333eba19cf69c5778e6c8bd04f59
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "79336758"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>Ottenere una chiave di ripristino per un dispositivo macOS

Usare il sito Web Portale aziendale per ottenere una chiave di ripristino per un dispositivo macOS bloccato. Se si dimentica la password del dispositivo, è possibile accedere a Portale aziendale da un altro dispositivo per recuperare la chiave.  

## <a name="get-recovery-key-from-company-portal-website"></a>Ottenere la chiave di ripristino dal sito Web Portale aziendale

Questa opzione è disponibile per i dispositivi che sono stati crittografati dall'organizzazione tramite FileVault. Non è disponibile per i dispositivi che sono stati crittografati personalmente dall'utente.

1. In qualsiasi dispositivo accedere al [sito Web Portale aziendale](https://portal.manage.microsoft.com) e selezionare il pulsante **Menu** > **Dispositivi**.  
2. Selezionare il dispositivo macOS crittografato.  
3. Selezionare **Ottieni la chiave di ripristino**.  

    ![Screenshot del sito Web Portale aziendale, con la sezione Ottieni la chiave di ripristino evidenziata.](./media/1907-recovery2-cpweb-intune.PNG)  

4. Verrà visualizzata la chiave di ripristino.

    ![Screenshot del sito Web Portale aziendale che mostra la chiave di ripristino.](./media/1907-recovery-cpweb-intune.PNG)  

    Per motivi di sicurezza, la chiave scomparirà dopo cinque minuti. Per visualizzarla di nuovo, selezionare **Ottieni la chiave di ripristino**.

Se non viene trovata alcuna chiave ma il dispositivo è crittografato correttamente, contattare il personale di supporto dell'organizzazione. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>Ottenere la chiave di ripristino dall'app Portale aziendale per iOS

È possibile recuperare la propria chiave di ripristino personale (chiave di FileVault) usando l'app Portale aziendale per iOS. Il dispositivo con la chiave di ripristino personale deve essere registrato in Intune e crittografato con FileVault in Intune. Questa opzione non è disponibile per i dispositivi che sono stati crittografati personalmente dall'utente. 

Usando l'app Portale aziendale, è possibile aprire la visualizzazione Web di Safari e recuperare la chiave di ripristino personale. 

1. Aprire Portale aziendale.
2. Fare clic su **Ottieni la chiave di ripristino**.

    ![Screenshot dell'app Portale aziendale per iOS che mostra la chiave di ripristino](./media/get-recovery-key-cpweb-02.png)  

Il sito Web Portale aziendale viene aperto nella visualizzazione Web di Safari e viene visualizzata la chiave. 

## <a name="it-pro-support"></a>Supporto per professionisti IT

Se si è un responsabile del supporto IT e si vuole configurare e gestire la crittografia FileVault per i dispositivi macOS, vedere [Usare la crittografia dei dispositivi con Intune](/intune/protect/encrypt-devices).

## <a name="next-steps"></a>Passaggi successivi

Scopri le altre operazioni che puoi eseguire dal sito Web Portale aziendale. Per l'elenco delle azioni, vedere [Uso del sito Web del portale aziendale](using-the-intune-company-portal-website.md).  

Serve ancora assistenza? Contattare il responsabile del supporto IT. Per informazioni sul contatto vedere il [sito Web del portale aziendale](https://go.microsoft.com/fwlink/?linkid=2010980).  
