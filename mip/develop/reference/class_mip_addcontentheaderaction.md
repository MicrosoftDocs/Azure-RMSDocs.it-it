---
title: Classe mip::AddContentHeaderAction
description: 'Documenta la classe MIP:: addcontentheaderaction di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 40e9b648799008bcc75b48ae9379f7a3010bd7bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559059"
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
  
## <a name="members"></a>Membri
  
### <a name="getuielementname-function"></a>Funzione getuielementname
API usata per contrassegnare l'elemento di intestazione contenuto.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene l'intestazione contenuto. Lo stesso nome verrà restituito in RemoveContentHeaderAction nel caso in cui l'intestazione del contenuto debba essere rimossa.
  
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

  
**Restituisce**: colore del carattere in formato stringa (ad esempio "#000000").
  
### <a name="getalignment-function"></a>Funzione getAlignment
Ottiene l'allineamento dell'intestazione.

  
**Restituisce**: enumeratore ContentMarkAlignment: LEFT|RIGHT|CENTER. 
  
**Vedere anche**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>Funzione GetMargin
Ottiene il margine dell'intestazione a partire dal basso.

  
**Restituisce**: margini dalla parte inferiore del documento (ad esempio 10 mm).