---
title: 'Classe MIP:: ClassificationRequest'
description: 'Documenta la classe MIP:: classificationrequest di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 27c6e01eea2dae3735ce5cc3e5cd618b6223d2eb
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489028"
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