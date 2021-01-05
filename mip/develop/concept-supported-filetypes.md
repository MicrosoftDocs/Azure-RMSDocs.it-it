---
title: Tipi di file supportati-Microsoft Information Protection SDK
description: Dettagli tecnici sui tipi di file supportati, le estensioni dei nomi di file e i livelli di protezione per gli amministratori responsabili del Software Development Kit di Microsoft Information Protection.
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/16/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: e247a31b364c40f270538d73815464491fca7647
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864856"
---
# <a name="file-types-supported-by-the-microsoft-information-protection-sdk"></a>Tipi di file supportati da Microsoft Information Protection SDK

Microsoft Information Protection SDK può applicare quanto segue ai documenti e ai messaggi di posta elettronica:

- Solo classificazione

- Classificazione e protezione

- Solo protezione

Microsoft Information Protection SDK può inoltre esaminare il contenuto di alcuni tipi di file utilizzando tipi di informazioni riservate note o espressioni regolari definite dall'utente.

Usare le informazioni seguenti per verificare quali tipi di file sono supportati da Microsoft Information Protection SDK, comprendere i diversi livelli di protezione e come modificare il livello di protezione predefinito e identificare i file esclusi automaticamente (ignorati) dalla classificazione e dalla protezione.

## <a name="file-types-supported-for-classification-only"></a>Tipi di file supportati solo per la classificazione

I tipi di file seguenti possono essere classificati anche se non sono protetti.

- **Adobe Portable Document Format**: .pdf

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft XPS**: .xps .oxps

- **Immagini**: con estensione jpg, jpe, jpeg, jif, jfif, jfi, png, tif e tiff

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

- **Microsoft Office**: i tipi di file nella tabella seguente.

    I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

    | Tipo di file Office                                                                                                                                                                                                                                               | Tipo di file Office                                                                                                                                                                                                                                 |
    | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | doc<br /><br />docm<br /><br />docx<br /><br />dot<br /><br />dotm<br /><br />dotx<br /><br />potm<br /><br />potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />ppt<br /><br />pptm<br /><br />pptx<br /><br />.vdw<br /><br />vsd | .vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />xls<br /><br />xlsb<br /><br />xlt<br /><br />xlsm<br /><br />xlsx<br /><br />xltm<br /><br />xltx |

Tipi di file aggiuntivi supportano la classificazione anche quando sono protetti. Per altre informazioni su questi file, vedere la sezione [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).

Se, ad esempio, un'etichetta **generale** applica la classificazione e non applica la protezione, è possibile applicare l'etichetta **generale** a un file denominato sales.pdf ma non è stato possibile applicare questa etichetta a un file denominato sales.txt.

Se, inoltre, un'etichetta **riservata \ tutti i dipendenti** applica la classificazione e la protezione, è possibile applicare questa etichetta a un file denominato sales.pdf e a un file denominato sales.txt. È possibile applicare solo la protezione a questi file, senza applicare la classificazione.

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

Microsoft Information Protection SDK supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

| Tipo di protezione     | Nativo                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Generico                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Descrizione            | Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).                                                                                                                                                                                                                                                                                       | Per tutte le altre applicazioni e gli altri tipi di file, la protezione generica offre un livello di protezione che include funzionalità di incapsulamento dei file, usando il tipo di file pfile, e di autenticazione per verificare se un utente è autorizzato ad aprire il file.                                                                                                                                                                                                                                                                                              |
| Protezione             | La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Vengono anche applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto al momento dell'applicazione della protezione ai file quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati). | La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione non riesce, il file non viene aperto.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Viene effettuata la registrazione di controllo dell'apertura di file e dell'accesso a questi da parte di utenti autorizzati. I diritti di utilizzo, tuttavia, non vengono applicati. |
| Livello predefinito per tipi di file | Questo è il livello di protezione predefinito per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione che segue, [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).                                                                                                                                                                              | Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio i file con estensione vsdx, rtf e così via) che non sono supportati dalla protezione nativa.                                                                                                                                                                                                                                                                                                                                                                                             |

È possibile modificare il livello di protezione predefinito applicato da Microsoft Information Protection SDK. È possibile modificare il livello predefinito da nativo a generico, da generico a nativo, e anche impedire a Microsoft Information Protection SDK di applicare la protezione.

### <a name="file-sizes-supported-for-protection"></a>Dimensioni dei file supportati per la protezione

A partire da Microsoft Information Protection SDK 1,6, le dimensioni massime del file predefinite sono di 6 GB. Se necessario, è possibile eseguire l'override di questa impostazione. Vengono comunque applicate le impostazioni predefinite minori per le piattaforme legacy di Office.


- **Per i file di Office:**

  | Applicazione di Office                                                                                                          | Dimensione massima del file supportata                                                                                                |
  | --------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
  | Word 2007 (supportato solo da AD RMS)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016                         | 32 bit: 512 MB<br /><br />64 bit: 512 MB                                                                                   |
  | Excel 2007 (supportato solo da AD RMS)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016                     | 32 bit: 2 GB<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco                                            |
  | PowerPoint 2007 (supportato solo da AD RMS)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bit: limitato solo dalla memoria e dallo spazio disponibile su disco<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco |

- **Per tutti gli altri file**:

    Per proteggere altri tipi di file e rimuovere la protezione su questi tipi di file tramite l'SDK: le dimensioni massime del file sono limitate solo dalla memoria e dallo spazio disponibile su disco.

### <a name="supported-file-types-for-classification-and-protection"></a>Tipi di file supportati per la classificazione e la protezione

La tabella seguente elenca un subset di tipi di file che supportano la protezione nativa da Microsoft Information Protection SDK e che possono anche essere classificati.

Questi tipi di file vengono identificati separatamente perché quando sono protetti in modo nativo l'estensione del nome file originale viene modificata e i file diventano di sola lettura. Si noti che se i file sono protetti in modo generico, l'estensione del nome file originale viene sempre modificata in pfile.

> [!WARNING]
> Se si dispone di firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali software e dispositivi di rete per supportare queste nuove estensioni.

| Estensione del file originale | Estensione dei file protetti |
| ---------------------------- | ----------------------------- |
| .txt                         | ptxt                         |
| xml                         | pxml                         |
| jpg                         | pjpg                         |
| jpeg                        | pjpeg                        |
| pdf                         | .ppdf [[1]](#footnote-1)      |
| png                         | ppng                         |
| tif                         | .ptif                         |
| tiff                        | ptiff                        |
| bmp                         | pbmp                         |
| gif                         | pgif                         |
| jpe                         | pjpe                         |
| jfif                        | pjfif                        |

###### <a name="footnote-1"></a>Nota 1
Con la versione più recente di Microsoft Information Protection SDK, l'estensione del nome file del documento PDF protetto rimane come. pdf.

Nella tabella seguente sono elencati i tipi di file rimanenti che supportano la protezione nativa da Microsoft Information Protection SDK e che possono anche essere classificati. Questi sono riconoscibili come tipi di file delle app di Microsoft Office. I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

Per questi file, l'estensione del nome di file rimane invariata dopo che il file è stato protetto da un servizio Rights Management.

| Tipi di file supportati da Office                                                                                                                                                                                                                  | Tipi di file supportati da Office                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| doc<br /><br />docm<br /><br />docx<br /><br />dot<br /><br />dotm<br /><br />dotx<br /><br />potm<br /><br />potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />ppt<br /><br />pptm<br /><br />pptx<br /><br />.vsdm | .vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />xla<br /><br />xlam<br /><br />xls<br /><br />xlsb<br /><br />xlt<br /><br />xlsm<br /><br />xlsx<br /><br />xltm<br /><br />xltx<br /><br />xps |

### <a name="limitations-for-container-files-such-as-zip-msg-files"></a>Limitazioni per i file contenitore, ad esempio file con estensione zip, msg

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi sono i file con estensione rar, 7z e msg, i file con estensione rpmsg e i documenti PDF che includono gli allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore. Analogamente, un file contenitore protetto può essere non protetto usando l'SDK, ma la protezione (se applicata) ai file all'interno del contenitore non verrà rimossa dall'operazione di rimozione della protezione sul file contenitore in modo ricorsivo. Gli sviluppatori di applicazioni sono responsabili della ricorsione e della rimozione della protezione di tutti i file all'interno dei contenitori.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione.
