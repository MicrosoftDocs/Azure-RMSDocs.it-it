---
title: Classe ClassificationRequest
description: 'Documenta la classe classificationrequest:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 0d4b8d3ed5e12698c0044975516b017d1c9376b0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763534"
---
# <a name="class-classificationrequest"></a>Classe ClassificationRequest 
Classe che contiene la richiesta di una chiamata di classificazione sullo stato di esecuzione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String GetClassificationId () const  |  Ottiene l'ID dei criteri di classificazione.
public std:: String GetRulePackageId () const  |  Ottenere l'ID del pacchetto di regole.
  
## <a name="members"></a>Members
  
### <a name="getclassificationid-function"></a>GetClassificationId (funzione)
Ottiene l'ID dei criteri di classificazione.

  
**Restituisce**: ID dei criteri di classificazione.
  
### <a name="getrulepackageid-function"></a>GetRulePackageId (funzione)
Ottenere l'ID del pacchetto di regole.

  
**Restituisce**: ID del pacchetto di regole. le classificazioni predefinite verranno impostate su un GUID vuoto.