---
title: Classe AddContentHeaderAction
description: 'Documenta la classe addcontentheaderaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 090bf4e1ad70238d6023a914fba4786a97a25a0d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567326"
---
# <a name="class-addcontentheaderaction"></a>Classe AddContentHeaderAction 
Classe di azione che specifica l'aggiunta di un'intestazione contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento di intestazione contenuto.
public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nell'intestazione contenuto.
public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.
public int GetFontSize() const  |  Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.
public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare l'intestazione contenuto.
public ContentMarkAlignment GetAlignment() const  |  Ottiene l'allineamento dell'intestazione.
public int GetMargin() const  |  Ottiene il margine dell'intestazione a partire dal basso.
  
## <a name="members"></a>Members
  
### <a name="getuielementname-function"></a>Funzione getuielementname
API usata per contrassegnare l'elemento di intestazione contenuto.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene l'intestazione contenuto. Lo stesso nome verrà restituito in RemoveContentHeaderAction nel caso in cui l'intestazione contenuto debba essere rimossa.
  
### <a name="gettext-function"></a>Funzione gettext
Ottiene il testo destinato a essere inserito nell'intestazione contenuto.

  
**Restituisce**: testo dell'intestazione contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: nome del carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>Funzione GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce** il colore del carattere sotto forma di stringa, ad esempio #000000 ".
  
### <a name="getalignment-function"></a>Funzione getAlignment
Ottiene l'allineamento dell'intestazione.

  
**Restituisce**: l'enumeratore CONTENTMARKALIGNMENT: Left | A destra | Center. 
  
**Vedere anche**: ContentMarkAlignment
  
### <a name="getmargin-function"></a>Funzione GetMargin
Ottiene il margine dell'intestazione a partire dal basso.

  
**Restituisce**: margini dalla parte inferiore del documento (ad esempio 10 mm).