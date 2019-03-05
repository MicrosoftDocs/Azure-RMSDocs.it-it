---
title: classe mip::ClassificationRequest
description: Documenta la classe mip::classificationrequest di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 61846ef3b8273169e9cf38eaa173eac3ba18dae6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330520"
---
# <a name="class-mipclassificationrequest"></a>classe mip::ClassificationRequest 
Classe che contiene la richiesta di una chiamata di classificazione dello stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: String GetClassificationId() const  |  Ottiene l'ID dei criteri di classificazione.
Public std:: String GetRulePackageId() const  |  Ottenere l'ID del pacchetto di regola.
  
## <a name="members"></a>Membri
  
### <a name="getclassificationid-function"></a>GetClassificationId (funzione)
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getrulepackageid-function"></a>GetRulePackageId (funzione)
Ottenere l'ID del pacchetto di regola.

  
**Restituisce**: ID del pacchetto di regola. le classificazioni predefinite verranno impostate su un guid vuoto.
