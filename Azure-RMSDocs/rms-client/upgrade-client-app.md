---
title: "Attività eseguite in precedenza con l&quot;applicazione RMS sharing"
description: Istruzioni per utenti che hanno eseguito l&quot;aggiornamento dall&quot;applicazione RMS sharing al client Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: edc17f17d9668ed9c3dbaabab2b5000359fa410d
ms.openlocfilehash: 678f444d487f020c2806aef4479696f19b6263e6


---

# <a name="tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>Attività eseguite in precedenza con l'applicazione RMS sharing

Di recente è stato eseguito l'aggiornamento dall'applicazione di condivisione Microsoft Rights Management (nota anche come "app RMS sharing") al client Azure Information Protection? 

Usare le informazioni seguenti per muovere i primi passi rapidamente.

|App RMS sharing|Come eseguire questa operazione con il client Azure Information Protection
|-----------|--------------------|
|Proteggere un file in un dispositivo <br /><br />Operazione chiamata anche "protezione sul posto"|Per le app di Office che visualizzano la barra di Azure Information Protection: selezionare un'etichetta che applica la protezione necessaria.<br /><br />Per altri file e se il client Azure Information Protection è in [modalità di sola protezione](client-protection-only-mode.md): usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Selezionare quindi un'etichetta che applica la protezione necessaria oppure specificare autorizzazioni personalizzate. <br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Proteggere un file che si condivide tramite posta elettronica <br /><br />Operazione chiamata anche "condivisione di file protetti"|Condivisione a livello interno: applicare un'etichetta con la protezione necessaria per il documento o il messaggio di posta elettronica oppure selezionare l'opzione di Outlook **Non inoltrare**. <br /><br /> Condivisione a livello esterno: usando una copia del file, usare Esplora file per proteggere il file con autorizzazioni personalizzate. Condividere quindi il file usando il meccanismo di condivisione standard, come un allegato a un messaggio di posta elettronica o un invito a un documento di SharePoint Online. Valutare se includere il collegamento https://aka.ms/rms-signup come istruzioni per il primo utilizzo. <br /><br />Per altre informazioni sulla condivisione a livello esterno, vedere la sezione [Condividere in modo sicuro un file con utenti esterni all'organizzazione](client-classify-protect.md#safely-share-a-file-with-people-outside-your-organization) della guida per l'utente.
|Modificare le autorizzazioni per i file protetti <br /><br />Operazione chiamata anche "riprotezione"|Per le app di Office che visualizzano la barra di Azure Information Protection: selezionare un'etichetta che applica la protezione necessaria.<br /><br />Per altri file e se il client Azure Information Protection è in [modalità di sola protezione](client-protection-only-mode.md): usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Selezionare quindi un'etichetta che applica la protezione necessaria oppure specificare autorizzazioni personalizzate.<br /><br />Per altre informazioni, vedere [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md).
|Tenere traccia dei documenti e revocarli|Per le app di Office: aprire il documento e quindi scheda **Home** > gruppo **Protezione** > **Proteggi** > **Rileva e revoca**<br /><br />In Esplora file: fare clic con il pulsante destro del mouse su un file o una cartella > **Classifica e proteggi**. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rileva e revoca**. <br /><br />Per altre informazioni, vedere [Tenere traccia dei documenti e revocarli](client-track-revoke.md).
|Visualizzare e utilizzare i file che sono stati protetti|Il visualizzatore Azure Information Protection può aprire file protetti per permettere di leggerli o di stamparli e salvarli se si hanno le autorizzazioni necessarie per eseguire queste operazioni. Questo visualizzatore viene automaticamente installato con il client oppure può essere installato separatamente.<br /><br />Per altre informazioni, vedere [Aprire file protetti](client-view-use-files.md).
|Rimuovere la protezione da uno o più file|Usare l'opzione di menu **Classifica e proteggi** di Esplora file per aprire la finestra di dialogo **Classifica e proteggi - Azure Information Protection**. <br /><br />Quindi, per un singolo file, deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. Per più file o una cartella, fare clic su **Rimuovi le autorizzazioni personalizzate**.<br /><br />Per altre informazioni, vedere [Rimuovere etichette di classificazione e protezione da file e messaggi di posta elettronica](client-remove-label-protection.md).|

## <a name="cant-find-the-option-youre-looking-for"></a>Se non è possibile trovare l'opzione desiderata

Per trovare un'opzione specifica dell'applicazione RMS sharing, controllare la tabella seguente.

|Opzione nell'app RMS sharing|Informazioni
|-----------|--------------------|
|**Condividi file protetto**|Questa opzione non è più disponibile sulla barra multifunzione di Office. Invece di condividere il file direttamente dall'applicazione di Office, usare l'opzione di menu di scelta rapida **Classifica e proteggi** di Esplora file per proteggere una copia del documento con autorizzazioni personalizzate e quindi condividere il file usando il client di posta elettronica o il percorso di condivisione preferito. Valutare se includere il collegamento https://aka.ms/rms-signup come istruzioni per il primo utilizzo. <br /><br />Per altre informazioni sulla condivisione a livello esterno, vedere la sezione [Condividere in modo sicuro un file con utenti esterni all'organizzazione](#safely-share-a-file-with-people-outside-your-organization) della guida per l'utente.
|**Invia messaggio se qualcuno prova ad aprire i documenti**|Usare il sito di rilevamento dei documenti per configurare l'impostazione di notifica tramite posta elettronica preferita: individuare il documento protetto che è stato condiviso > **Impostazioni** > **Notifiche tramite posta elettronica**
|**Consenti di revocare immediatamente l'accesso ai documenti**|Questa opzione non è più disponibile. Configurare modelli che non permettono l'accesso offline. Valutare inoltre se è necessario ridurre il periodo di validità della licenza con l'utente finale per il tenant, eseguendo [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime).







[!INCLUDE[Commenting house rules](../includes/houserules.md)]  



<!--HONumber=Feb17_HO2-->

