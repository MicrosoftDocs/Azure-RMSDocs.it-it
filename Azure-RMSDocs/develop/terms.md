---
title: Terminologia di Azure Information Protection per sviluppatori | Documentazione Microsoft
description: Una raccolta di definizioni di termini specifici di Rights Management Services per gli sviluppatori.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9c0977c57ea8e85b6750fe1f5a063059ee343db9
ms.openlocfilehash: 4ecf686d8e7e26909c8bda4a2d0df7fc61f413bb
ms.lasthandoff: 01/24/2017


---

# <a name="terms"></a>Termini

Una raccolta di definizioni di termini specifici di Azure Information Protection per gli sviluppatori.

**Algoritmo deprecato**  
Un'impostazione modale che implementa uno schema di protezione del contenuto precedente che fa riferimento alla modalità di crittografia ECB (Electronic Codebook). In questo SDK, l'impostazione consente di generare licenze compatibili con la libreria MSDRM usata da [AD Rights Management Services SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Questa impostazione può causare la protezione del contenuto da parte dell'applicazione in un modo non conforme allo standard dei clienti per la protezione del contenuto.

Questa impostazione impedisce all'applicazione di beneficiare di eventuali miglioramenti della crittografia apportati a Microsoft Rights Management SDK 3.0 o versione successiva.

**Formato di file protetto da Microsoft**

Noto anche come formato PFile, è il formato di file predefinito per AD RMS e rappresenta lo standard tra le applicazioni abilitate per RMS.

Il formato PFile è trasparente allo sviluppatore dell'applicazione in quanto è incorporato nella progettazione di Microsoft Rights Management SDK 4.2.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
