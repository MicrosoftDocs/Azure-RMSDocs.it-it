---
title: Terminologia di Azure Information Protection per sviluppatori | Documentazione Microsoft
description: Una raccolta di definizioni di termini specifici di Rights Management Services per gli sviluppatori.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 1cf0080c899bc3095ff036f651c1f31f63b70ffe
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071379"
---
# <a name="terms"></a>Termini

Una raccolta di definizioni di termini specifici di Azure Information Protection per gli sviluppatori.

**Algoritmo deprecato**  
Un'impostazione modale che implementa uno schema di protezione del contenuto precedente che fa riferimento alla modalità di crittografia ECB (Electronic Codebook). In questo SDK, l'impostazione consente di generare licenze compatibili con la libreria MSDRM usata da [AD Rights Management Services SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Questa impostazione può causare la protezione del contenuto da parte dell'applicazione in un modo non conforme allo standard dei clienti per la protezione del contenuto.

Questa impostazione impedisce all'applicazione di beneficiare dei miglioramenti di crittografia apportati a Microsoft Rights Management SDK 3.0 o versioni successive.

**Formato di file protetto da Microsoft**

Noto anche come formato PFile, è il formato di file predefinito per AD RMS e rappresenta lo standard tra le applicazioni abilitate per RMS.

Il formato PFile è trasparente allo sviluppatore dell'applicazione in quanto è incorporato nella progettazione di Microsoft Rights Management SDK 4.2.

