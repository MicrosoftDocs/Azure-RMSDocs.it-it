---
title: Attività eseguite in precedenza con l'applicazione RMS sharing - AIP
description: Istruzioni per utenti che hanno eseguito l'aggiornamento dall'applicazione RMS sharing al client Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: d8a9c0e81b7b5bedb1b8f41dc129f4370c827acf
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048596"
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Guida dell'utente: Attività eseguite in precedenza con l'applicazione RMS sharing

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Di recente è stato eseguito l'aggiornamento dall'applicazione di condivisione Microsoft Rights Management (nota anche come "app RMS sharing") al client Azure Information Protection? 

Usare le informazioni seguenti per muovere i primi passi rapidamente.

|App RMS sharing|Come eseguire questa operazione con il client Azure Information Protection
|-----------|--------------------|
|Proteggere un file in un dispositivo <br /><br />Operazione chiamata anche "protezione sul posto"|Per le app di Office: selezionare un'etichetta che applica la protezione necessaria oppure impostare autorizzazioni personalizzate.<br /><br />Per altri file: usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Selezionare quindi un'etichetta che applica la protezione necessaria oppure specificare autorizzazioni personalizzate. <br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Proteggere un file condiviso tramite posta elettronica <br /><br />Operazione chiamata anche "condivisione di file protetti"|Se si usa Outlook applicare un'etichetta con la protezione necessaria per il messaggio di posta elettronica oppure selezionare l'opzione di Outlook **Non inoltrare**. Gli allegati non protetti che hanno un [tipo di file supportato](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) vengono automaticamente protetti.<br /><br />Nota: per tenere traccia di un documento protetto inviato via posta elettronica, prima proteggerlo e poi allegarlo al messaggio di posta elettronica.<br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Modificare le autorizzazioni per i file protetti <br /><br />Operazione chiamata anche "riprotezione"|Per le app di Office che visualizzano la barra di Azure Information Protection: selezionare un'etichetta che applica la protezione necessaria.<br /><br />Per altri file e se il client Azure Information Protection è in [modalità di sola protezione](client-protection-only-mode.md): usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Selezionare quindi un'etichetta che applica la protezione necessaria oppure specificare autorizzazioni personalizzate.<br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Tenere traccia dei documenti e revocarli|Per Word, Excel e PowerPoint: aprire il documento e quindi scheda **Home** > gruppo **Protezione** > **Proteggi** > **Rileva e revoca**<br /><br />In Esplora file: fare clic con il pulsante destro del mouse su un file o una cartella > **Classifica e proteggi**. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rileva e revoca**. <br /><br />Quando si usa PowerShell per il client Azure Information Protection: usare il parametro *EnableTracking* con il cmdlet [set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) per registrare il documento con etichetta per il rilevamento.<br /><br />Per altre informazioni, vedere [Tenere traccia dei documenti e revocarli](client-track-revoke.md).
|Visualizzare e usare file protetti|È necessario che Office sia installato per usare i documenti di Office protetti. Il visualizzatore Azure Information Protection è in grado di aprire molti altri file protetti per consentirne la lettura, nonché la stampa e il salvataggio se si è autorizzati a eseguire queste operazioni. Questo visualizzatore viene automaticamente installato con il client oppure può essere installato separatamente.<br /><br />Per altre informazioni, vedere [Aprire file protetti](client-view-use-files.md).
|Rimuovere la protezione da uno o più file|Usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. <br /><br />Quindi, per un singolo file, deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. Per più file o una cartella, fare clic su **Rimuovi le autorizzazioni personalizzate**.<br /><br />Per altre informazioni, vedere [Rimuovere etichette di classificazione e protezione da file e messaggi di posta elettronica](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>Se non è possibile trovare l'opzione desiderata

Per trovare un'opzione specifica dell'applicazione RMS sharing, controllare la tabella seguente.

|Opzione nell'app RMS sharing|Informazioni
|-----------|--------------------|
|**Condividi file protetto**|Questa opzione non è più disponibile sulla barra multifunzione di Office. Invece di condividere il file direttamente dall'applicazione di Office, usare l'opzione di menu di scelta rapida **Classifica e proteggi** di Esplora file per proteggere una copia del documento con autorizzazioni personalizzate e quindi condividere il file usando il client di posta elettronica o il percorso di condivisione preferito. <br /><br /> È anche possibile allegare un documento di Office non protetto a un messaggio di posta elettronica protetto e il documento viene automaticamente protetto con le stesse restrizioni. Tuttavia, non è possibile monitorare e revocare il documento.
|**Invia messaggio se qualcuno prova ad aprire i documenti**|Usare il sito di rilevamento dei documenti per configurare l'impostazione preferita per le notifiche di posta elettronica: individuare il documento protetto condiviso > **le impostazioni delle**  >  **notifiche di posta elettronica**
|**Consenti di revocare immediatamente l'accesso a questi documenti**|Questa opzione non è più disponibile. Usare le impostazioni di protezione definite dall'amministratore che non consentono l'accesso offline. Inoltre, un amministratore può ridurre il periodo di validità della licenza d'uso per il tenant, eseguendo [set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime).
|**Rileva utilizzo** in Outlook|Non è più possibile accedere al sito di rilevamento dei documenti da Outlook. Usare invece l'opzione **Rileva e revoca** da Word, PowerPoint, Excel o Esplora file oppure andare direttamente al [sito di rilevamento dei documenti](https://go.microsoft.com/fwlink/?LinkId=529562) usando un browser.

## <a name="next-steps"></a>Passaggi successivi
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Vedere la [Guida dell'amministratore del client Azure Information Protection](client-admin-guide.md).

  
