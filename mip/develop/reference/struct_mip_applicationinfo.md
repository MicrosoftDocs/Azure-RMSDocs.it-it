---
title: struct ApplicationInfo
description: Documents Structures associati a Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4971d7cf0891308733dafd0dc64d58c02343f1e4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566552"
---
# <a name="struct-applicationinfo"></a>struct ApplicationInfo 
Struct che include informazioni specifiche dell'applicazione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
public std::string applicationName  |  Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
public std::string applicationVersion  |  Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')
  
## <a name="members"></a>Members
  
### <a name="applicationid-struct-member"></a>membro struct applicationId
Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).
  
### <a name="applicationname-struct-member"></a>membro struct di ApplicationName
Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')
  
### <a name="applicationversion-struct-member"></a>membro struct applicationVersion
Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')