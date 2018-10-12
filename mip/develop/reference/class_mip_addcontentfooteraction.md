---
title: Classe mip AddContentFooterAction
description: Riferimento per la classe mip AddContentFooterAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 73f641d965c3cf0236919557128af2ed07705672
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445836"
---
# <a name="class-mipaddcontentfooteraction"></a>Classe mip::AddContentFooterAction 
Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento piè di pagina contenuto.
 public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nel piè di pagina contenuto.
 public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare il piè di pagina contenuto.
 public int GetFontSize() const  |  Ottiene le dimensioni del carattere usato per visualizzare il piè di pagina contenuto.
 public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare il piè di pagina contenuto.
 public ContentMarkAlignment GetAlignment() const  |  Ottiene l'allineamento del piè di pagina.
 public int GetMargin() const  |  Ottiene il margine del piè di pagina a partire dal basso.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementname"></a>GetUIElementName
API usata per contrassegnare l'elemento piè di pagina contenuto.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene il piè di pagina contenuto. Lo stesso nome verrà restituito in [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) nel caso in cui il piè di pagina contenuto debba essere rimosso.
  
### <a name="gettext"></a>GetText
Ottiene il testo destinato a essere inserito nel piè di pagina contenuto.

  
**Restituisce**: testo del piè di pagina contenuto.
  
### <a name="getfontname"></a>GetFontName
Ottiene il nome del tipo di carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: nome del carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize"></a>GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: dimensioni del carattere come numero intero.
  
### <a name="getfontcolor"></a>GetFontColor
Ottiene il colore del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: colore del carattere in formato stringa (ad esempio "#000000").
  
### <a name="getalignment"></a>GetAlignment
Ottiene l'allineamento del piè di pagina.

  
**Restituisce**: enumeratore ContentMarkAlignment: LEFT|RIGHT|CENTER. 
  
**Vedere anche**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Ottiene il margine del piè di pagina a partire dal basso.

  
**Restituisce**: margini dalla parte inferiore del documento (ad esempio 10 mm).
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.