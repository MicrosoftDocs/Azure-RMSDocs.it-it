---
title: Formati di file supportati | Azure RMS
description: La versione corrente dell'API file supporta la protezione nativa per i file di MS Office e PDF e la protezione PFile per tutti gli altri formati di file.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5dc4cc7a54e7976339ad0def3f2a1d71c8204991
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39369925"
---
# <a name="supported-file-formats"></a>Formati di file supportati

L'API file supporta i formati nativi e PFile.

## <a name="supported-file-formats"></a>Formati di file supportati

La versione corrente dell'API file supporta la protezione nativa per i file di Microsoft Office e Portable Document Files (PDF) e la protezione PFile per tutti gli altri formati di file. Ai file PDF è possibile applicare anche la protezione PFile.

-   **Protezione nativa**. Nella protezione nativa, il file è crittografato in un formato di file AD RMS su cui su basa il tipo MIME (estensione di file). I file protetti in modo nativo tramite l'API file sono coerenti con il formato previsto dalle applicazioni abilitate per AD RMS che usano la protezione nativa, ad esempio Office 2013, Office 2010 e il lettore PDF FoxIt. La protezione nativa è supportata solo in file di Office, file PDF e numerosi altri tipi di file. Per altre informazioni sui tipi di file in cui è supportata la protezione nativa, vedere l'articolo relativo alla [configurazione dell'API file](file-api-configuration.md).
-   **Protezione PFile**. Nella protezione PFile, i file vengono crittografati usando il formato AD RMS Protected File (PFile). Il file è crittografato in un file con estensione pfile. La protezione PFile è supportata da tutti i formati di file ad eccezione dei file di Office.

Gli amministratori possono impostare le chiavi del Registro di sistema per configurare se e come i file devono essere protetti in base all'estensione di file. Per altre informazioni su come configurare la protezione del file quando si usa l'API file, vedere l'articolo relativo alla [configurazione dell'API file](file-api-configuration.md).

## <a name="related-topics"></a>Argomenti correlati

* [Note per gli sviluppatori](developer-notes.md)
* [Configurazione dell'API file](file-api-configuration.md)
 