---
title: classe mip::ClassificationRequest
description: Documenta la classe mip::classificationrequest di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a7350961af4c2e5d63211840382ee7a0b701f1c4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652031"
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