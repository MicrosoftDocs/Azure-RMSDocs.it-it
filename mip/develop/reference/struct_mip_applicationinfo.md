---
title: 'struct MIP:: ApplicationInfo'
description: Documents Structures associati a Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6bee61bc72de35aeaefd9ef1e7639450392b70a7
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567426"
---
# <a name="struct-mipapplicationinfo"></a>struct MIP:: ApplicationInfo 
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