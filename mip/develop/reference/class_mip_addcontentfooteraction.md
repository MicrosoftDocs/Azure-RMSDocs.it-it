---
title: Classe mip::AddContentFooterAction
description: 'Documenta la classe MIP:: addcontentfooteraction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 48b558c423c8cefa37333b1c5133dda31d70433d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884585"
---
# <a name="class-mipaddcontentfooteraction"></a>Classe mip::AddContentFooterAction 
Classe di azione che specifica l'aggiunta di un piè di pagina contenuto al documento.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento piè di pagina contenuto.
public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nel piè di pagina contenuto.
public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare il piè di pagina contenuto.
public int GetFontSize() const  |  Ottiene le dimensioni del carattere usato per visualizzare il piè di pagina contenuto.
public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare il piè di pagina contenuto.
public ContentMarkAlignment GetAlignment() const  |  Ottiene l'allineamento del piè di pagina.
public int GetMargin() const  |  Ottiene il margine del piè di pagina a partire dal basso.
  
## <a name="members"></a>Members
  
### <a name="getuielementname-function"></a>Funzione getuielementname
API usata per contrassegnare l'elemento piè di pagina contenuto.

  
**Restituisce**: Nome da utilizzare per l'elemento dell'interfaccia utente che include il piè di pagina contenuto. Lo stesso nome verrà restituito in [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) nel caso in cui il piè di pagina contenuto debba essere rimosso.
  
### <a name="gettext-function"></a>Funzione gettext
Ottiene il testo destinato a essere inserito nel piè di pagina contenuto.

  
**Restituisce**: Testo del piè di pagina contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: Nome del tipo di carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>Funzione GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: Colore del carattere sotto forma di stringa, ad esempio "#000000".
  
### <a name="getalignment-function"></a>Funzione getAlignment
Ottiene l'allineamento del piè di pagina.

  
**Restituisce**: Enumeratore ContentMarkAlignment: A SINISTRA | A DESTRA | CENTER. 
  
**Vedere anche**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>Funzione GetMargin
Ottiene il margine del piè di pagina a partire dal basso.

  
**Restituisce**: I margini dalla parte inferiore del documento, ad esempio 10 mm.