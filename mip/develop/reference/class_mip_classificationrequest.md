---
title: 'Classe MIP:: ClassificationRequest'
description: 'Documenta la classe MIP:: classificationrequest di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 1966123c8a0975ea42aa119883cabd47db594bc4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884482"
---
# <a name="class-mipclassificationrequest"></a>Classe MIP:: ClassificationRequest 
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