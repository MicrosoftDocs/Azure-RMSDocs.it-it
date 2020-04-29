---
title: Classe AddWatermarkAction
description: 'Documenta la classe addwatermarkaction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: fe2cc80e5abb225a5e83c1b10c1c5f9f99401628
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763750"
---
# <a name="class-addwatermarkaction"></a>Classe AddWatermarkAction 
Classe di azione che specifica l'aggiunta di una filigrana.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento filigrana.
public WatermarkLayout GetLayout() const  |  API usata per ottenere il layout della filigrana.
public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nella filigrana.
public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.
public int GetFontSize() const  |  Ottiene le dimensioni del carattere usate per visualizzare la filigrana.
public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare la filigrana.
  
## <a name="members"></a>Members
  
### <a name="getuielementname-function"></a>Funzione getuielementname
API usata per contrassegnare l'elemento filigrana.

  
**Restituisce**: nome da usare per l'elemento dell'interfaccia utente che contiene la filigrana. Lo stesso nome verrà restituito in RemoveWatermarkingAction nel caso in cui la filigrana debba essere rimossa.
  
### <a name="getlayout-function"></a>Funzione GetLayout
API usata per ottenere il layout della filigrana.

  
**Restituisce**: WatermarkLayout Layout della filigrana nel formato di un'enumerazione HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext-function"></a>Funzione gettext
Ottiene il testo destinato a essere inserito nella filigrana.

  
**Restituisce**: testo dell'intestazione contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.

  
**Restituisce**: nome del carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>Funzione GetFontSize
Ottiene le dimensioni del carattere usate per visualizzare la filigrana.

  
**Restituisce**: dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare la filigrana.

  
**Restituisce**: colore del carattere in formato stringa (ad esempio "#000000").