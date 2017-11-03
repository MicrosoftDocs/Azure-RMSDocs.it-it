---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 3'
description: Fase 3 della migrazione da AD RMS ad Azure Information Protection, che illustra il passaggio 7 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ca2c8156489b55911ee340fd52f85e68b5280915
ms.sourcegitcommit: 3952fc01c6182c143df7f0d2e748594e49bf1da8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/01/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 della migrazione: configurazione lato client

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Usare le informazioni seguenti per la fase 3 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano il passaggio 7 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Passaggio 7. Riconfigurare i computer Windows per usare Azure Information Protection

Usare due script di migrazione per riconfigurare i client AD RMS in computer Windows:

- Migrate-Client.cmd

- Migrate-User.cmd

Lo script di configurazione client (Migrate-Client.cmd) configura le impostazioni a livello di computer nel Registro di sistema. Deve pertanto essere eseguito in un contesto di protezione che consenta di apportare modifiche di questo genere. È quindi solitamente necessario seguire questi metodi:

- Usare Criteri di gruppo per eseguire lo script come script di avvio del computer.

- Usare Criteri di gruppo Installazione software per assegnare lo script al computer.

- Usare una soluzione di distribuzione software per distribuire lo script nei computer. Usare ad esempio i [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in System Center Configuration Manager. In **Modalità esecuzione** nelle proprietà del pacchetto e del programma specificare che lo script viene eseguito con autorizzazioni amministrative nel dispositivo. 

- Se l'utente dispone di privilegi di amministratore locale, usare uno script di accesso.

Lo script di configurazione utente (Migrate-User.cmd) configura le impostazioni a livello utente e pulisce l'archivio licenze client. È quindi necessario eseguire questo script nel contesto dell'utente effettivo. Ad esempio:

- Usare uno script di accesso.

- Usare Criteri di gruppo Installazione software per pubblicare lo script che l'utente deve eseguire.

- Usare una soluzione di distribuzione software per distribuire lo script agli utenti. Usare ad esempio i [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in System Center Configuration Manager. In **Modalità esecuzione** nelle proprietà del pacchetto e del programma specificare che lo script viene eseguito con le autorizzazioni dell'utente. 

- Chiedere all'utente di eseguire lo script dopo aver eseguito l'accesso al computer.

I due script includono un numero di versione e non vengono rieseguiti fino a quando il numero di versione viene modificato. Ciò significa che è possibile lasciare gli script presenti fino a quando la migrazione non è stata completata. Se invece gli script vengono modificati e si vuole che i computer e gli utenti li rieseguano nei computer Windows, aggiornare la riga seguente nei due script incrementando il valore:

    SET Version=20170427

Lo script di configurazione utente è progettato per essere eseguito dopo lo script di configurazione client e usa il numero di versione specificato in questo controllo. Si interrompe se lo script di configurazione client con lo stesso numero di versione non è stato eseguito. Con questo controllo si verifica che i due script siano eseguiti nella sequenza corretta. 

Se non è possibile migrare tutti i client di Windows in una sola volta, eseguire le procedure seguenti per batch di client. Per ogni utente che ha un computer Windows per cui si vuole eseguire la migrazione in batch, aggiungere l'utente al gruppo **AIPMigrated** creato in precedenza.

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>Riconfigurazione di client di Windows tramite modifiche del Registro di sistema

1. Tornare agli script di migrazione **Migrate-Client.cmd** e **Migrate-User.cmd** che sono stati precedentemente estratti durante il download di questi script nella [fase di preparazione](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2.  Seguire le istruzioni in **Migrate-Client.cmd** per modificare lo script in modo che contenga l'URL del servizio Azure Rights Management del tenant e i nomi server dell'URL di gestione licenze Extranet del cluster AD RMS e dell'URL di gestione licenze Intranet. A questo punto incrementare la versione dello script, come spiegato in precedenza. Per tener traccia delle versioni degli script, è consigliabile usare la data corrente nel formato seguente: AAAAMMGG

    > [!IMPORTANT]
    > Come in precedenza, prestare attenzione a non introdurre spazi aggiuntivi prima o dopo gli indirizzi.
    > 
    > Inoltre, se i server AD RMS usano certificati del server SSL/TLS, controllare se i valori URL di gestione licenze includono il numero di porta **443** nella stringa. Ad esempio: https:// rms.treyresearch.net:443/_wmcs/licensing. Queste informazioni sono disponibili nella console di Active Directory Rights Management Services quando si fa clic sul nome del cluster e si visualizzano le informazioni **Dettagli cluster**. Se il numero di porta 443 è presente nell'URL, includere questo valore quando si modifica lo script. Ad esempio, https://rms.treyresearch.net:**443**. 

    Se è necessario recuperare l'URL del servizio Azure Rights Management per *&lt;URL tenant&gt;*, vedere nelle sezioni precedenti l'argomento [Per identificare l'URL del servizio Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. Seguendo le istruzioni all'inizio di questo passaggio, configurare i metodi di distribuzione script per eseguire **Migrate-Client.cmd** e **Migrate-User.cmd** nei computer client Windows che vengono usati dai membri del gruppo AIPMigrated. 

## <a name="next-steps"></a>Passaggi successivi
Per continuare la migrazione, passare a [Fase 4: configurazione di servizi di supporto](migrate-from-ad-rms-phase4.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]