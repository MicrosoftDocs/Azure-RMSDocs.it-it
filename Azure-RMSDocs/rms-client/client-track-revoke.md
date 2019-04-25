---
title: Tenere traccia di documenti e revocarli - Azure Information Protection
description: Dopo aver protetto i documenti, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l'accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 95a70375f65e461cff2f69d28598d2a72aeaec10
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "62773520"
---
# <a name="user-guide-track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Manuale dell'utente: Tenere traccia dei documenti e revocarli quando si usa Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dopo avere protetto i documenti con Azure Information Protection, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l'accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli. A tale scopo usare il **sito di rilevamento dei documenti**. È possibile accedere al sito da computer Windows, Mac e anche da tablet e telefoni.

Quando si accede a questo sito, eseguire l'accesso per effettuare il rilevamento dei documenti. Se l'organizzazione ha una [sottoscrizione che supporta il rilevamento e la revoca dei documenti](https://www.microsoft.com/cloud-platform/azure-information-protection-features) ed è presente di una licenza per tale sottoscrizione, è possibile sapere chi ha tentato di aprire i file protetti e se il tentativo ha avuto esito positivo (ovvero se è stata eseguita correttamente l'autenticazione) o meno. È anche possibile verificare ogni tentativo di accesso al documento e la posizione dell'utente in quel momento. Tuttavia, in rari casi, la posizione segnalata potrebbe non essere accurata, ad esempio quando un utente che apre un documento protetto usa una connessione VPN o il computer dispone di un indirizzo IPv6.

Azioni che è possibile eseguire nel sito di rilevamento dei documenti:

- Se è necessario interrompere la condivisione di un documento: 
    
    - Fare clic su **Revoca l'accesso**. Rilevare il periodo di tempo per il quale documento continua a essere disponibile. Decidere se comunicare con un messaggio personalizzato che si revoca l'accesso al documento, in precedenza condiviso. Quando si revoca un documento condiviso il documento non viene eliminato, ma gli utenti autorizzati non possono più aprirlo:
        
        ![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](../media/tracking-site-revoke-access-icon.png)
        
- Per esportare in Excel, 
    
    - Fare clic su **Esporta in CSV**, in modo da poter modificare i dati e creare visualizzazioni e grafici personalizzati:
         
        ![Icona Esporta in CSV nel sito di rilevamento dei documenti](../media/tracking-site-export-icon.png)
         
- Per configurare notifiche di posta elettronica, 
     
    - Fare clic su **Impostazioni** e indicare se e in che modo ricevere una notifica di posta elettronica quando un utente accede al documento:
        
        ![Configurare notifiche tramite posta elettronica nel sito di rilevamento dei documenti](../media/tracking-site-settings-email.png)

- Per rilevare e revocare i documenti condivisi per conto di altri utenti:
    
    - Gli amministratori di Azure Information Protection possono fare clic sull'icona di amministrazione per rilevare e revocare documenti protetti per gli utenti, se tali utenti hanno registrato i rispettivi documenti nel sito di rilevamento dei documenti. Solo gli amministratori possono visualizzare questa icona:
        
        ![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)
        
        Se si è un amministratore globale e l'icona non è visibile, significa che non sono stati ancora condivisi documenti. In questo caso, usare l'URL seguente per accedere al sito di rilevamento dei documenti: https://portal.azurerms.com/#/admin

A meno che non sia un amministratore, l'utente può rilevare e revocare solo i documenti che ha protetto. Non è possibile rilevare i messaggi di posta elettronica protetti usando il sito di rilevamento dei documenti.

> [!NOTE] 
> Se l'amministratore ha configurato controlli sulla privacy per il sito di rilevamento dei documenti, può non essere possibile vedere quando gli utenti dell'organizzazione accedono a un documento rilevato. Un amministratore può escludere tutti gli utenti o solo alcuni utenti. Tuttavia, è sempre possibile revocare l'accesso ai documenti rilevati.

Per rilevare un documento protetto, è necessario usare il computer Windows per registrarlo con il sito di rilevamento dei documenti. A questo scopo, usare Esplora file o le app di Office.

Se si dispone della versione di disponibilità generale corrente del client Azure Information Protection, è anche possibile registrare il documento protetto con PowerShell quando si usa la *EnableTracking* parametro con il [ Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet.

## <a name="using-office-to-track-or-revoke-the-document"></a>Uso di Office per tenere traccia del documento e revocarlo

Per le applicazioni di Office, Word, Excel e PowerPoint: 

1. Aprire il documento protetto di cui tenere traccia o da revocare.

2. Nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Rileva e revoca**:

    ![Opzione Rileva utilizzo](../media/track-usage-callout.png)
    
    Se non è possibile visualizzare queste opzioni nelle applicazioni di Office, la causa probabile è una delle seguenti:
    
    - Il client Azure Information Protection non è installato nel computer in uso.
    
    - È necessario riavviare le applicazioni Office.
    
    - Per completare il processo di installazione è necessario riavviare il computer.
    
Per altre informazioni su come installare il client di Azure Information Protection, vedere [Scaricare e installare il client di Azure Information Protection](install-client-app.md).

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>Uso di Esplora File per tenere traccia del documento o revocarlo

1. Fare clic con il pulsante destro del mouse sul file protetto e scegliere **Classifica e proteggi**.

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rileva e revoca**.

    ![Icona Rileva e revoca nella finestra di dialogo Classifica e proteggi - Azure Information Protection](../media/track-and-revoke.png)


### <a name="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered"></a>Uso di un Web browser per rilevare e revocare i documenti registrati

Dopo aver registrato i documenti protetti tramite le app di Office o Esplora file, è possibile tenere traccia di questi documenti e revocarli usando un Web browser supportato:

- Tramite il PC Windows, il computer Mac o il dispositivo mobile, visitare il [sito di rilevamento dei documenti](https://go.microsoft.com/fwlink/?LinkId=529562).

    **Browser supportati**: È consigliabile usare almeno di Internet Explorer versione 10, ma è possibile usare uno qualsiasi dei browser seguenti per usare il sito di rilevamento dei documenti:

    - Internet Explorer: Almeno la versione 10

    - Internet Explorer 9 con almeno MS12-037: Aggiornamento cumulativo della sicurezza per Internet Explorer: 12 giugno 2012

    - Mozilla Firefox: Almeno versione 12

    - Apple Safari 5: Almeno la versione 5

    - Google Chrome: Almeno versione 18


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Vedere [Configurazione e uso del rilevamento dei documenti per Azure Information Protection](client-admin-guide-document-tracking.md) nella [Guida dell'amministratore](client-admin-guide.md).
