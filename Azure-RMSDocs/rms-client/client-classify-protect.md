---
title: Classificare e proteggere un file o un messaggio di posta elettronica tramite Azure Information Protection | Azure Information Protection
description: Istruzioni su come classificare e proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e6d4cc50259b9d9bb73a75c648f9e6915562accf
ms.openlocfilehash: e1d61fbe1d74a4a57d9a1fdf518aeb0242d0f7ad


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Classificare e proteggere un file o un messaggio di posta elettronica tramite Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

**[Questa versione del client è in anteprima e soggetta a modifiche].**

Il modo più semplice per classificare e proteggere i documenti e i messaggi di posta elettronica è durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è possibile classificare e proteggere i file tramite **Esplora file**, che supporta altri tipi di file e consente di classificare e proteggere più file contemporaneamente.

## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso delle app di Office per classificare e proteggere documenti e messaggi di posta elettronica

Usare la barra di Azure Information Protection e selezionare una delle etichette configurate. Ad esempio:

![Esempio della barra di Azure Information Protection](../media/info-protect-bar-not-set-callout.png)


## <a name="using-file-explorer-to-classify-and-protect-files"></a>Uso di Esplora file per classificare e proteggere file

Quando si usa Esplora file, è possibile classificare e proteggere rapidamente un singolo file, più file o una cartella. 

Quando si seleziona una cartella, tutti i file in tale cartella e tutte le relative sottocartelle vengono selezionate automaticamente per le opzioni di classificazione e protezione impostate. Tuttavia, i nuovi file che vengono creati in tale cartella o nelle sottocartelle non vengono configurati automaticamente con queste opzioni.

Quando si usa Esplora file per classificare e proteggere i file, si potrebbe notare che le etichette non sono sempre disponibili. Ciò si verifica quando i file selezionati non supportano la classificazione. Per questi file, è possibile selezionare un'etichetta solo se l'amministratore ha configurato l'etichetta in modo da potere applicare la protezione. In alternativa, è possibile specificare le proprie impostazioni di protezione. 

Per un elenco dei tipi di file supportati da Esplora file, vedere la sezione [Tipi di file supportati per la classificazione e la protezione](#file-types-supported-for-classification-and-protection) in questa pagina.


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Per classificare e proteggere un file mediante Esplora file

1.  In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e selezionare **Classifica e proteggi (anteprima)**. 

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** usare le etichette in modo analogo a un'applicazione di Office, che consente di impostare la classificazione e la protezione come definito dall'amministratore. Se non è possibile selezionare un'etichetta, ovvero non è disponibile, il file selezionato non supporta la classificazione ma è possibile proteggerlo.

3. Per proteggere il file, scegliere tra le impostazioni di protezione definite dall'amministratore per l'etichetta selezionata (**Automatico, in base all'etichetta di classificazione selezionata**) o specificare le proprie impostazioni (**Esegui l'override con le autorizzazioni personalizzate**).
    
    L'opzione di override non usa alcuna impostazione di protezione che l'amministratore potrebbe avere definito per l'etichetta scelta. In alternativa, è possibile specificare le proprie impostazioni di protezione. 

4. Se si seleziona l'opzione di override, specificare le opzioni seguenti:

    - **Selezionare le autorizzazioni**: selezionare il livello di accesso da assegnare agli utenti per la protezione del file o dei file selezionati.
    
    - **Selezionare gli utenti**: specificare gli utenti che devono avere le autorizzazioni selezionate per il file o i file. Per gli utenti e i gruppi all'interno dell'organizzazione è possibile usare la Rubrica per cercarli e selezionarli. Per gli utenti di un'altra organizzazione è necessario specificare l'indirizzo di posta elettronica completo. Assicurarsi di usare un indirizzo di posta elettronica aziendale perché gli indirizzi di posta elettronica personali non sono attualmente supportati.
        
    - **Scadenza dell'accesso**: selezionare questa opzione solo per i file per cui il fattore tempo è importante in modo tale che gli utenti specificati non potranno aprire il file o i file selezionati dopo una data specificata. Sarà comunque possibile aprire il file originale, ma dopo la mezzanotte (fuso orario corrente) del giorno selezionato, gli utenti specificati non potranno aprire il file.

5. Fare clic su **Applica**, quindi su **Chiudi**.

Il file o i file selezionati verranno classificati e protetti in base alle selezioni specificate. In alcuni casi (quando l'aggiunta della protezione modifica l'estensione del nome di file) il file originale in Esplora file viene sostituito con un nuovo file con l'icona di blocco di Azure Information Protection. Ad esempio:

![File protetto con l'icona di blocco di Azure Information Protection](../media/Pfile.png)

Se si cambia idea sulla classificazione e la protezione o se in seguito è necessario modificare le impostazioni, è sufficiente ripetere questo processo con le nuove impostazioni.

La classificazione e la protezione specificate rimangono associate al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. Se si protegge il file, è possibile tenere traccia del modo in cui gli utenti lo usano e se necessario revocarne l'accesso. Per altre informazioni, vedere [Tenere traccia dei documenti protetti e revocarli quando si usa Azure Information Protection](client-track-revoke.md). 

#### <a name="file-types-supported-for-classification-and-protection"></a>Tipi di file supportati per la classificazione e la protezione

Per i tipi di file seguenti è supportata solo la classificazione. Gli altri tipi di file supportano la classificazione quando vengono anche protetti.

- **Microsoft Visio**: .vsdx, .vsdm, .vssx, .vssm, .vsd, .vdw, .vst

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft Office 97, Office 2010, Office 2003**: .xls, .xlt, .doc, .dot, .ppt, .pps, .pot

- **Microsoft XPS**: .xps .oxps

- **Immagini**: .jpg, .jpe, .jpeg, .jif, .jfif, .jfi.png, .tif, .tiff

- **SolidWorks**: .sldprt, .slddrw, .sldasm

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng


La protezione con il servizio Rights Management è supportata per i tipi di file documentati nella [configurazione dell'API file](../develop/file-api-configuration.md). Questa protezione può essere applicata automaticamente quando si seleziona un'etichetta configurata dall'amministratore o è possibile specificare le proprie impostazioni di protezione usando i [livelli di autorizzazione](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 


## <a name="other-instructions"></a>Altre istruzioni
Per le istruzioni d'uso, vedere le sezioni seguenti della Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)




<!--HONumber=Dec16_HO1-->


