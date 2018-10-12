---
title: Classe mip AddContentHeaderAction
description: Riferimento per la classe mip AddContentHeaderAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: bc60fe32005a0c6bc8088ab7687a3f711ae7a99a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445649"
---
# <a name="class-mipaddcontentheaderaction"></a>Classe mip::AddContentHeaderAction 
Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento di intestazione contenuto.
 public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nell'intestazione contenuto.
 public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.
 public int GetFontSize() const  |  Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.
 public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare l'intestazione contenuto.
 public ContentMarkAlignment GetAlignment() const  |  Ottiene l'allineamento dell'intestazione.
 public int GetMargin() const  |  Ottiene il margine dell'intestazione a partire dal basso.
 public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementname"></a>GetUIElementName
API usata per contrassegnare l'elemento di intestazione contenuto.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene l'intestazione contenuto. Lo stesso nome verrà restituito in [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) nel caso in cui l'intestazione contenuto debba essere rimossa.
  
### <a name="gettext"></a>GetText
Ottiene il testo destinato a essere inserito nell'intestazione contenuto.

  
**Restituisce**: testo dell'intestazione contenuto.
  
### <a name="getfontname"></a>GetFontName
Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: nome del carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize"></a>GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: dimensioni del carattere come numero intero.
  
### <a name="getfontcolor"></a>GetFontColor
Ottiene il colore del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: colore del carattere in formato stringa (ad esempio "#000000").
  
### <a name="getalignment"></a>GetAlignment
Ottiene l'allineamento dell'intestazione.

  
**Restituisce**: enumeratore ContentMarkAlignment: LEFT|RIGHT|CENTER. 
  
**Vedere anche**: ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
Ottiene il margine dell'intestazione a partire dal basso.

  
**Restituisce**: margini dalla parte inferiore del documento (ad esempio 10 mm).
  
### <a name="actiontype"></a>ActionType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.