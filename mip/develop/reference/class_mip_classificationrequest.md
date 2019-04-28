---
title: classe mip::ClassificationRequest
description: Documenta la classe mip::classificationrequest di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3fddd870b6aebb9f5209fc43160c32d87b1d7129
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184757"
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