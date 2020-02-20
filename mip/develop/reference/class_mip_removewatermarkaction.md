---
title: Classe mip::RemoveWatermarkAction
description: 'Documenta la classe MIP:: removewatermarkaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c2e6eb141d213a9ca19a345a4dac68120200abf8
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489487"
---
# <a name="class-mipremovewatermarkaction"></a>Classe mip::RemoveWatermarkAction 
Classe di azione che specifica la rimozione della filigrana dal documento.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std:: Vector\<std:: String\>& GetUIElementNames ()  |  Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.
public ActionType GetType() const  |  Ottiene il tipo di azione.
  
## <a name="members"></a>Members
  
### <a name="getuielementnames-function"></a>GetUIElementNames (funzione)
Ottiene un elenco di nomi da usare per individuare gli elementi dell'interfaccia utente che devono essere rimossi.

  
**Restituisce**: un elenco di nomi di elementi dell'interfaccia utente.
  
### <a name="gettype-function"></a>Funzione GetType
Ottiene il tipo di azione.

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.