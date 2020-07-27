---
title: Strumento di migrazione delle regole del firewall per la sicurezza degli endpoint per Microsoft Intune - Azure | Microsoft Docs
description: Informazioni su come usare lo strumento di migrazione delle regole del firewall per la sicurezza degli endpoint per Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465002"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Panoramica dello strumento di migrazione delle regole del firewall per la sicurezza degli endpoint

Molte organizzazioni stanno valutando la possibilità di spostare la configurazione della sicurezza in Microsoft Endpoint Manager per poter usare le funzionalità di gestione moderna basata sul cloud.

La sicurezza degli endpoint in Endpoint Manager offre un'esperienza di gestione completa per la configurazione di Windows Firewall e la gestione granulare delle regole del firewall.

In molte organizzazioni vengono già usati Criteri di gruppo per gestire le regole di Windows Firewall. Il passaggio alla gestione moderna può essere complicato, dato che la creazione manuale di centinaia di regole del firewall può risultare noiosa.

Per aiutare i clienti a trasformare la configurazione delle regole del firewall in criteri di sicurezza degli endpoint in Endpoint Manager, è stato sviluppato lo **strumento di migrazione delle regole del firewall per la sicurezza degli endpoint**.

I clienti possono eseguire lo **strumento di migrazione delle regole del firewall per la sicurezza degli endpoint** in un client Windows 10 di riferimento/preconfigurato e creare automaticamente i criteri delle regole del firewall per la sicurezza degli endpoint in Endpoint Manager. Dopo averle create, gli amministratori possono assegnare queste regole a gruppi di Azure AD per configurare i client MDM e co-gestiti.

Scaricare lo [strumento di migrazione delle regole del firewall per la sicurezza degli endpoint](https://aka.ms/EndpointSecurityFWRuleMigrationTool):<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Utilizzo dello strumento

Lo strumento viene eseguito in un computer di riferimento ed esegue la migrazione della configurazione delle regole di Windows Firewall corrente. Eseguendo lo strumento verranno esportate tutte le regole del firewall abilitate presenti nel dispositivo e verranno creati automaticamente nuovi criteri di Intune con le regole raccolte.

1. Accedere al computer di riferimento con privilegi di amministratore locale.
2. Scaricare e decomprimere il file `Export-FirewallRules.zip`. <br>
   Il file zip contiene il file di script `Export-FirewallRules.ps1`. 
3. Eseguire lo script `Export-FirewallRules.ps1` nel computer. <br>
   Lo script scaricherà tutti i prerequisiti necessari per l'esecuzione. Quando richiesto, specificare le credenziali di amministratore di Intune appropriate. Per altre informazioni sulle autorizzazioni necessarie, vedere [Autorizzazioni richieste](#required-permissions).
4. Specificare un nome di criterio quando richiesto. <br>
   Questo criterio sarà visibile in [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) nel riquadro **Sicurezza degli endpoint** > **Firewall**. 

    > [!IMPORTANT]
    > Il nome del criterio deve essere univoco per il tenant.

    Se vengono rilevate più di 150 regole del firewall, verranno creati più criteri.

    > [!NOTE]
    > Per impostazione predefinita verrà eseguita la migrazione solo delle regole del firewall abilitate e verranno incluse solo le regole create dall'oggetto Criteri di gruppo. Sono disponibili opzioni per modificare questi valori predefiniti. Per altre informazioni, vedere [Opzioni](#switches).
    >
    > A seconda del numero di regole del firewall trovate, l'esecuzione dello strumento potrebbe richiedere del tempo.

5. Al termine, lo strumento restituirà il conteggio delle regole del firewall di cui non è possibile eseguire la migrazione automaticamente. Per altre informazioni, vedere [Configurazione non supportata](#unsupported-configuration).

## <a name="switches"></a>Opzioni

Per modificare la funzionalità predefinita dello strumento, è possibile usare le opzioni (parametri) seguenti.

- `IncludeLocalRules` -Se si usa questa opzione verranno incluse nell'esportazione tutte le regole di Windows Firewall create localmente/predefinite. Si noti che l'abilitazione di questa opzione può causare l'inclusione di numerose regole. 
- `IncludedDisabledRules` -Se si usa questa opzione verranno incluse nell'esportazione tutte le regole di Windows Firewall abilitate e disabilitate. Si noti che l'abilitazione di questa opzione può causare l'inclusione di numerose regole.

## <a name="unsupported-configuration"></a>Configurazione non supportata

Le impostazioni basate sul Registro di sistema seguenti non sono supportate a causa della mancanza del supporto MDM in Windows. Queste impostazioni non sono comuni. Tuttavia, se necessario, è possibile registrare questa esigenza tramite i canali di supporto standard.

|     Campo dell'oggetto Criteri di gruppo    |     Motivo    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     Identificatore di interfaccia (LUID) non gestibile    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     Attraversamento NAT in ingresso correlato non esposto tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     Loose source mapping non esposto tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     Controllo delle versioni del sistema operativo non esposto tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     Mapping solo locale non esposto tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     Impostazione ridondante non esposta tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     Incrocio dei profili consentito non esposto tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     SID proprietario utente locale non applicabile in MDM    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     Corrispondenza del traffico con la parola chiave della tupla attendibile non esposta tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     Corrispondenza del traffico con la parola chiave della tupla attendibile non esposta tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     Corrispondenza del traffico con la parola chiave della tupla attendibile non esposta tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     Corrispondenza del traffico con la parola chiave della tupla attendibile non esposta tramite Criteri di gruppo o MDM Windows    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |
|      TYPE-VALUE =/"SecurityRealmId =" STR-VAL    |     Impostazione correlata a IPSec non supportata da MDM Windows    |

## <a name="unsupported-setting-values"></a>Valori delle impostazioni non supportati
I valori delle impostazioni seguenti non sono supportati per la migrazione:

**Porte**
- `PlayToDiscovery` non è supportato come intervallo di porte locale o remoto.

**Intervalli di indirizzi**
- `LocalSubnet6` non è supportato come intervallo di indirizzi locale o remoto. 
- `LocalSubnet4` non è supportato come intervallo di indirizzi locale o remoto.
- `PlatToDevice` non è supportato come intervallo di indirizzi locale o remoto.

Dopo aver eseguito lo strumento verrà generato un report con le regole di cui non è stata completata la migrazione. È possibile visualizzare una qualsiasi di queste regole nel file `RulesError.csv` disponibile in `C:\<folder needed>`. 

## <a name="required-permissions"></a>Autorizzazioni richieste
Gli utenti con il ruolo Endpoint Security Manager, Amministratore del servizio Intune o Amministratore globale possono eseguire la migrazione delle regole di Windows Firewall a criteri di sicurezza degli endpoint. In alternativa, è possibile usare un ruolo personalizzato in cui le autorizzazioni per la baseline di sicurezza includono i diritti **Eliminazione**, **Lettura**, **Assegnazione**, **Creazione** e **Aggiornamento**. Per altre informazioni, vedere [Concedere le autorizzazioni di amministratore a Intune](../fundamentals/users-add.md#grant-admin-permissions).

## <a name="next-steps"></a>Passaggi successivi

- Assegnare le regole a gruppi di Azure AD per configurare i client MDM e con co-gestione. Per altre informazioni, vedere [Aggiungere gruppi per organizzare utenti e dispositivi](../fundamentals/groups-add.md).
