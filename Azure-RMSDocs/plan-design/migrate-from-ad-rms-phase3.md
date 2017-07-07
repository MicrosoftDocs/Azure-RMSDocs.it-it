---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 3'
description: Fase 3 della migrazione da AD RMS ad Azure Information Protection, che illustra il passaggio 7 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 27dc3de51c72d0142ac3dbdbd97c02c0241e902d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 della migrazione: configurazione lato client

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Usare le informazioni seguenti per la fase 3 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano il passaggio 7 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

Se non è possibile migrare tutti i client in una sola volta, eseguire queste procedure per batch di client. Per ogni utente che ha un computer Windows per cui si vuole eseguire la migrazione in batch, aggiungere l'utente al gruppo **AIPMigrated** creato in precedenza.

## <a name="step-7-reconfigure-clients-to-use-azure-information-protection"></a>Passaggio 7. Riconfigurare i client per l'uso di Azure Information Protection

Questo passaggio usa script di migrazione per riconfigurare i client AD RMS. Gli script reimpostano la configurazione nei computer Windows in modo che usino il servizio Azure Rights Management anziché AD RMS: 

**CleanUpRMS.cmd**:

- Elimina il contenuto di tutte le cartelle e le chiavi del Registro di sistema usate dal client AD RMS per archiviare la configurazione. Queste informazioni includono il percorso del cluster AD RMS del client.

**MigrateClient.cmd**:

- Configura il client per inizializzare l'ambiente utente (bootstrap) per il servizio di Azure Rights Management.

-  Configura il client per connettersi al servizio Azure Rights Management per ottenere licenze d'uso per il contenuto protetto dal cluster AD RMS. 


### <a name="client-reconfiguration-by-using-registry-edits"></a>Riconfigurazione di client tramite modifiche del Registro di sistema

1. Ritornare agli script di migrazione **CleanUpRMS.cmd** e **MigrateClient.cmd** estratti in precedenza.

2.  Seguire le istruzioni in **MigrateClient.cmd** per modificare lo script in modo che contenga l'URL del servizio Azure Rights Management del tenant, e anche i nomi dell'URL di gestione licenze Extranet del cluster AD RMS e dell'URL di gestione licenze intranet.

    > [!IMPORTANT]
    > Come in precedenza, prestare attenzione a non introdurre spazi aggiuntivi prima o dopo gli indirizzi.
    > 
    > Inoltre, se i server AD RMS usano certificati del server SSL/TLS, controllare se i valori URL di gestione licenze includono il numero di porta **443** nella stringa. Ad esempio: https:// rms.treyresearch.net:443/_wmcs/licensing. Queste informazioni sono disponibili nella console di Active Directory Rights Management Services quando si fa clic sul nome del cluster e si visualizzano le informazioni **Dettagli cluster**. Se il numero di porta 443 è presente nell'URL, includere questo valore quando si modifica lo script. Ad esempio, https://rms.treyresearch.net:**443**. 

    Se è necessario recuperare l'URL del servizio Azure Rights Management per *&lt;URL tenant&gt;*, vedere nelle sezioni precedenti l'argomento [Per identificare l'URL del servizio Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3.  Eseguire **CleanUpRMS.cmd** e quindi **MigrateClient.cmd** nei computer client usati dai membri del gruppo **AIPMigrated**. Ad esempio, creare un oggetto Criteri di gruppo che esegue questi script e lo assegna a questo gruppo di utenti.


## <a name="next-steps"></a>Passaggi successivi
Per continuare la migrazione, passare a [Fase 4: configurazione di servizi di supporto](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]