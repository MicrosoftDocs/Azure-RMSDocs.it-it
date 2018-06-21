---
title: Attività eseguite in precedenza con l'applicazione RMS sharing - AIP
description: Istruzioni per utenti che hanno eseguito l'aggiornamento dall'applicazione RMS sharing al client Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 58b0ab62b260e407aa9ae6a36b4a063fe147889b
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
ms.locfileid: "30206860"
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Guida dell'utente: Attività eseguite in precedenza con l'applicazione RMS sharing

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
>Di recente è stato eseguito l'aggiornamento dall'applicazione di condivisione Microsoft Rights Management (nota anche come "app RMS sharing") al client Azure Information Protection? 

Usare le informazioni seguenti per muovere i primi passi rapidamente.

|App RMS sharing|Come eseguire questa operazione con il client Azure Information Protection
|-----------|--------------------|
|Proteggere un file in un dispositivo <br /><br />Operazione chiamata anche "protezione sul posto"|Per le app di Office: selezionare un'etichetta che applica la protezione necessaria oppure impostare autorizzazioni personalizzate.<br /><br />Per altri file: usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Selezionare quindi un'etichetta che applica la protezione necessaria oppure specificare autorizzazioni personalizzate. <br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Proteggere un file che si condivide tramite posta elettronica <br /><br />Operazione chiamata anche "condivisione di file protetti"|Se si usa Outlook applicare un'etichetta con la protezione necessaria per il messaggio di posta elettronica oppure selezionare l'opzione di Outlook **Non inoltrare**. Gli allegati non protetti che hanno un [tipo di file supportato](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) vengono automaticamente protetti.<br /><br />Nota: per tenere traccia di un documento protetto inviato via posta elettronica, prima proteggerlo e poi allegarlo al messaggio di posta elettronica.<br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Modificare le autorizzazioni per i file protetti <br /><br />Operazione chiamata anche "riprotezione"|Per le app di Office che visualizzano la barra di Azure Information Protection: selezionare un'etichetta che applica la protezione necessaria.<br /><br />Per altri file e se il client Azure Information Protection è in [modalità di sola protezione](client-protection-only-mode.md): usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Selezionare quindi un'etichetta che applica la protezione necessaria oppure specificare autorizzazioni personalizzate.<br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Tenere traccia dei documenti e revocarli|Per le app di Office: aprire il documento e quindi scheda **Home** > gruppo **Protezione** > **Proteggi** > **Rileva e revoca**<br /><br />In Esplora file: fare clic con il pulsante destro del mouse su un file o una cartella > **Classifica e proteggi**. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rileva e revoca**. <br /><br />Per altre informazioni, vedere [Tenere traccia dei documenti e revocarli](client-track-revoke.md).
|Visualizzare e utilizzare i file che sono stati protetti|È necessario che Office sia installato per usare i documenti di Office protetti. Il visualizzatore Azure Information Protection è in grado di aprire molti altri file protetti per consentirne la lettura, nonché la stampa e il salvataggio se si è autorizzati a eseguire queste operazioni. Questo visualizzatore viene automaticamente installato con il client oppure può essere installato separatamente.<br /><br />Per altre informazioni, vedere [Aprire file protetti](client-view-use-files.md).
|Rimuovere la protezione da uno o più file|Usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. <br /><br />Quindi, per un singolo file, deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. Per più file o una cartella, fare clic su **Rimuovi le autorizzazioni personalizzate**.<br /><br />Per altre informazioni, vedere [Rimuovere etichette di classificazione e protezione da file e messaggi di posta elettronica](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>Se non è possibile trovare l'opzione desiderata

Per trovare un'opzione specifica dell'applicazione RMS sharing, controllare la tabella seguente.

|Opzione nell'app RMS sharing|Informazioni
|-----------|--------------------|
|**Condividi file protetto**|Questa opzione non è più disponibile sulla barra multifunzione di Office. Invece di condividere il file direttamente dall'applicazione di Office, usare l'opzione di menu di scelta rapida **Classifica e proteggi** di Esplora file per proteggere una copia del documento con autorizzazioni personalizzate e quindi condividere il file usando il client di posta elettronica o il percorso di condivisione preferito. <br /><br /> È anche possibile allegare un documento non protetto a un messaggio di posta elettronica protetto e il documento viene automaticamente protetto con le stesse restrizioni. Tuttavia, non è possibile monitorare e revocare il documento.
|**Invia messaggio se qualcuno prova ad aprire i documenti**|Usare il sito di rilevamento dei documenti per configurare l'impostazione di notifica tramite posta elettronica preferita: individuare il documento protetto che è stato condiviso > **Impostazioni** > **Notifiche tramite posta elettronica**
|**Consenti di revocare immediatamente l'accesso ai documenti**|Questa opzione non è più disponibile. Configurare modelli che non permettono l'accesso offline. Valutare inoltre se è necessario ridurre il periodo di validità della licenza con l'utente finale per il tenant, eseguendo [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime).







[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
