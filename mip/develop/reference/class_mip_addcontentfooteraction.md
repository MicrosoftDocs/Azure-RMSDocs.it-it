---
title: Classe AddContentFooterAction
description: 'Documenta la classe addcontentfooteraction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 1ecebda7a6df2fcba2bca531b7cc6e28eefdde99
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212485"
---
# <a name="class-addcontentfooteraction"></a>Classe AddContentFooterAction 
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
  
## <a name="members"></a>Membri
  
### <a name="getuielementname-function"></a>Funzione getuielementname
API usata per contrassegnare l'elemento piè di pagina contenuto.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene il piè di pagina contenuto. Lo stesso nome verrà restituito in RemoveContentFooterAction nel caso in cui il piè di pagina contenuto debba essere rimosso.
  
### <a name="gettext-function"></a>Funzione gettext
Ottiene il testo destinato a essere inserito nel piè di pagina contenuto.

  
**Restituisce**: testo del piè di pagina contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: nome del carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>Funzione GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: colore del carattere in formato stringa (ad esempio "#000000").
  
### <a name="getalignment-function"></a>Funzione getAlignment
Ottiene l'allineamento del piè di pagina.

  
**Restituisce**: l'enumeratore CONTENTMARKALIGNMENT: Left | A destra | Center. 
  
**Vedere anche**: ContentMarkAlignment
  
### <a name="getmargin-function"></a>Funzione GetMargin
Ottiene il margine del piè di pagina a partire dal basso.

  
**Restituisce**: margini dalla parte inferiore del documento (ad esempio 10 mm).