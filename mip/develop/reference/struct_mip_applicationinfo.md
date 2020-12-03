---
title: struct ApplicationInfo
description: Documenta la struttura ApplicationInfo
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d56fdcaccf67f46b2d6632ec6586e2b140717696
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535587"
---
# <a name="struct-applicationinfo"></a>struct ApplicationInfo 
Struct che include informazioni specifiche dell'applicazione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
public std::string applicationName  |  Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
public std::string applicationVersion  |  Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')
  
## <a name="members"></a>Membri
  
### <a name="applicationid-struct-member"></a>membro struct applicationId
Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
  
### <a name="applicationname-struct-member"></a>membro struct di ApplicationName
Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
  
### <a name="applicationversion-struct-member"></a>membro struct applicationVersion
Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')