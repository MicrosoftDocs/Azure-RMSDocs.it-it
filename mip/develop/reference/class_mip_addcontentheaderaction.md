---
title: Classe mip::AddContentHeaderAction
description: 'Documenta la classe MIP:: addcontentheaderaction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: e9de81595ead9a629c3266962a08f1b13fdb9675
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885928"
---
# <a name="class-mipaddcontentheaderaction"></a>Classe mip::AddContentHeaderAction 
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

  
**Restituisce**: Nome che deve essere utilizzato per l'elemento dell'interfaccia utente che include l'intestazione del contenuto. Lo stesso nome verrà restituito in [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) nel caso in cui l'intestazione contenuto debba essere rimossa.
  
### <a name="gettext-function"></a>Funzione gettext
Ottiene il testo destinato a essere inserito nell'intestazione contenuto.

  
**Restituisce**: Testo dell'intestazione del contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: Nome del tipo di carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>Funzione GetFontSize
Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: Colore del carattere sotto forma di stringa, ad esempio #000000 ".
  
### <a name="getalignment-function"></a>Funzione getAlignment
Ottiene l'allineamento dell'intestazione.

  
**Restituisce**: Enumeratore ContentMarkAlignment: A SINISTRA | A DESTRA | CENTER. 
  
**Vedere anche**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>Funzione GetMargin
Ottiene il margine dell'intestazione a partire dal basso.

  
**Restituisce**: I margini dalla parte inferiore del documento, ad esempio 10 mm.