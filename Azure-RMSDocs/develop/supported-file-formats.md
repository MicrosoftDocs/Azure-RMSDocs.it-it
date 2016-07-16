---
title: Formati di file supportati | Azure RMS
description: La versione corrente dell'API file supporta la protezione nativa per i file di MS Office e PDF e la protezione PFile per tutti gli altri formati di file.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b5fbbf637a34371a676a6cba169cc0268ce5e541
ms.openlocfilehash: 58efe60d6066f2e9761aea8d66d83711e68ab642


---

# Formati di file supportati

L'API file supporta i formati nativi e PFile.

## Formati di file supportati

La versione corrente dell'API file supporta la protezione nativa per i file di Microsoft Office e Portable Document Files (PDF) e la protezione PFile per tutti gli altri formati di file. Ai file PDF è possibile applicare anche la protezione PFile.

-   **Protezione nativa**. Nella protezione nativa, il file è crittografato in un formato di file AD RMS su cui su basa il tipo MIME (estensione di file). I file protetti in modo nativo tramite l'API file sono coerenti con il formato previsto dalle applicazioni abilitate per AD RMS che usano la protezione nativa, ad esempio Office 2013, Office 2010 e il lettore PDF FoxIt. La protezione nativa è supportata solo in file di Office, file PDF e numerosi altri tipi di file. Per altre informazioni sui tipi di file in cui è supportata la protezione nativa, vedere l'articolo relativo alla [configurazione dell'API file](file-api-configuration.md).
-   **Protezione PFile**. Nella protezione PFile, i file vengono crittografati usando il formato AD RMS Protected File (PFile). Il file è crittografato in un file con estensione pfile. La protezione PFile è supportata da tutti i formati di file ad eccezione dei file di Office.

Gli amministratori possono impostare le chiavi del Registro di sistema per configurare se e come i file devono essere protetti in base all'estensione di file. Per altre informazioni su come configurare la protezione del file quando si usa l'API file, vedere l'articolo relativo alla [configurazione dell'API file](file-api-configuration.md).

## Argomenti correlati

* [Note per gli sviluppatori](developer-notes.md)
* [Configurazione dell'API file](file-api-configuration.md)
 

 



<!--HONumber=Jun16_HO4-->


