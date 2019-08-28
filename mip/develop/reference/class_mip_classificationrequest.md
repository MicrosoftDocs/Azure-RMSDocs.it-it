---
title: 'Classe MIP:: ClassificationRequest'
description: 'Documenta la classe MIP:: classificationrequest di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 39fde4fa5fb0fe6f91545c9cffa36ed976a4b8b1
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055330"
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