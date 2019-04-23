---
title: Classe mip::AddContentFooterAction
description: 'Classe MIP:: addcontentfooteraction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 625406d1b2207e4b1f74c77c6813ee3d852f0d37
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173499"
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
  
### <a name="getuielementname-function"></a>GetUIElementName (funzione)
API usata per contrassegnare l'elemento piè di pagina contenuto.

  
**Restituisce**: Il nome deve essere utilizzato per l'elemento dell'interfaccia utente che contiene il piè di pagina contenuto. Lo stesso nome verrà restituito in [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) nel caso in cui il piè di pagina contenuto debba essere rimosso.
  
### <a name="gettext-function"></a>GetText (funzione)
Ottiene il testo destinato a essere inserito nel piè di pagina contenuto.

  
**Restituisce**: Testo piè di pagina contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: Nome del tipo di carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>GetFontSize (funzione)
Ottiene le dimensioni del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare il piè di pagina contenuto.

  
**Restituisce**: Colore del carattere come stringa (ad esempio, "#000000").
  
### <a name="getalignment-function"></a>GetAlignment (funzione)
Ottiene l'allineamento del piè di pagina.

  
**Restituisce**: Enumeratore ContentMarkAlignment: LEFT | RIGHT | CENTRO. 
  
**Vedere anche**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment)
  
### <a name="getmargin-function"></a>GetMargin (funzione)
Ottiene il margine del piè di pagina a partire dal basso.

  
**Restituisce**: I margini dalla parte inferiore del documento (ad esempio 10 mm).

### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.