---
title: classe mip::ClassificationRequest
description: Documenta la classe mip::classificationrequest di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 81e9a7276b78817f3d2f409cc403992284d23ceb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259151"
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
