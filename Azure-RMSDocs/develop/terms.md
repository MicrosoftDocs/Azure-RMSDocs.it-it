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
ms.openlocfilehash: a053eb0d117165b02e6dfda3246d416127a9be85
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
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