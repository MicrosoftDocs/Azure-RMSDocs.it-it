---
title: Configurazioni personalizzate per il client di assegnazione di etichette unificata di Azure Information Protection
description: Informazioni sulla personalizzazione del client di assegnazione di etichette unificato di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c565c025b6ae3001984141a691ed37a057203f38
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181090"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guida dell'amministratore: Configurazioni personalizzate per il client di assegnazione di etichette unificata di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni seguenti per le configurazioni avanzate che potrebbe essere necessario per scenari specifici o un sottoinsieme di utenti per gestire il client di assegnazione di etichette unificato di Azure Information Protection.

Queste impostazioni richiedono la modifica del Registro di sistema.  

## <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, gli utenti non sarebbero in genere necessario eseguire l'accesso come utente diverso quando usano Azure Information Protection unified client imprevisto delle etichette. Per un amministratore, tuttavia, può essere necessario accedere con le credenziali di un altro utente durante una fase di testing. 

È possibile verificare a quale account è stato eseguito l'accesso usando la finestra di dialogo **Microsoft Azure Information Protection**: Aprire un'applicazione di Office e, nella **Home** scheda, seleziona il **sensibilità** e quindi selezionare **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

Assicurarsi di controllare anche il nome di dominio dell'account di accesso che viene visualizzato. Può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo dell'uso di un account non corretto impossibilità di scaricare le etichette, o non possono visualizzare le etichette o un comportamento previsto.

Per accedere come utente diverso:

1. Passare a **%localappdata%\Microsoft\MSIP** ed eliminare il file **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non è possibile visualizzare un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare al **Microsoft Azure Information Protection** finestra di dialogo e selezionare **Accedi** dal aggiornata **lo stato del Client** sezione.

Inoltre:

- Se il client di assegnazione di etichette unificato di Azure Information Protection viene ancora eseguito l'accesso con l'account precedente dopo aver completato questi passaggi, eliminare tutti i cookie di Internet Explorer e quindi ripetere i passaggi 1 e 2.

- Se si usa la funzione Single Sign-On, è necessario uscire da Windows e accedere con un account utente diverso dopo aver eliminato il file del token. Il client di assegnazione di etichette unificato di Azure Information Protection quindi esegue automaticamente l'autenticazione usando l'accesso dell'account utente.

- Questa soluzione è supportata per l'accesso come utente diverso dallo stesso tenant. Non è supportata per l'accesso come utente diverso da un diverso tenant. Per testare Azure Information Protection con più tenant, usare computer diversi.

- È possibile usare la **Reimposta le impostazioni** opzione **Guida e commenti** per disconnettersi ed eliminare le impostazioni e le etichette scaricate di Office 365 Centro sicurezza e conformità, il Il Centro sicurezza di Microsoft 365 o il centro di conformità di Microsoft 365.


## <a name="change-the-local-logging-level"></a>Modificare il livello di registrazione locale

Per impostazione predefinita, Azure Information Protection unified imprevisto delle etichette client scrive file di log client per il **%localappdata%\Microsoft\MSIP** cartella. Questi file sono destinati al supporto tecnico Microsoft per la risoluzione dei problemi.
 
Per modificare il livello di registrazione per questi file, individuare il nome di valore seguente del Registro di sistema e impostare il valore per il livello di registrazione necessario:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

Impostare il livello di registrazione su uno dei valori seguenti:

- **Off**: nessuna registrazione locale.

- **Errore**: solo errori.

- **Info**: registrazione minima che non include ID evento.

- **Debug**: Informazioni complete.

- **Traccia**: Registrazione dettagliata (impostazione predefinita per i client).

Questa impostazione del Registro di sistema non modifica le informazioni che viene inviate ad Azure Information Protection per [reporting centralizzato](../reports-aip.md).


## <a name="next-steps"></a>Passaggi successivi
Ora che è stato personalizzato il client di assegnazione di etichette unificato di Azure Information Protection, vedere le risorse seguenti per informazioni aggiuntive che potrebbe essere necessario supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)
