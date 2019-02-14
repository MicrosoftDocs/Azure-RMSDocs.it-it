---
title: Classe mip::AddWatermarkAction
description: 'Classe MIP:: addwatermarkaction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 660d2d81492895a6c18ec0b9a921b694e70fbe65
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260001"
---
# <a name="class-mipaddwatermarkaction"></a>Classe mip::AddWatermarkAction 
Classe di azione che specifica l'aggiunta di una filigrana.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API usata per contrassegnare l'elemento filigrana.
public WatermarkLayout GetLayout() const  |  API usata per ottenere il layout della filigrana.
public const std::string& GetText() const  |  Ottiene il testo destinato a essere inserito nella filigrana.
public const std::string& GetFontName() const  |  Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.
public int GetFontSize() const  |  Ottiene le dimensioni del carattere usate per visualizzare la filigrana.
public const std::string& GetFontColor() const  |  Ottiene il colore del carattere usato per visualizzare la filigrana.
public ActionType GetType() const  |  Specifica il tipo di [Action](class_mip_action.md).
  
## <a name="members"></a>Membri
  
### <a name="getuielementname-function"></a>GetUIElementName (funzione)
API usata per contrassegnare l'elemento filigrana.

  
**Restituisce**: Il nome deve essere utilizzato per l'elemento dell'interfaccia utente che contiene la filigrana. Lo stesso nome verrà restituito in RemoveWatermarkingAction nel caso in cui la filigrana debba essere rimossa.
  
### <a name="getlayout-function"></a>GetLayout (funzione)
API usata per ottenere il layout della filigrana.

  
**Restituisce**: WatermarkLayout Layout della filigrana nel formato di un'enumerazione HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext-function"></a>GetText (funzione)
Ottiene il testo destinato a essere inserito nella filigrana.

  
**Restituisce**: Testo dell'intestazione contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.

  
**Restituisce**: Nome del tipo di carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>GetFontSize (funzione)
Ottiene le dimensioni del carattere usate per visualizzare la filigrana.

  
**Restituisce**: Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare la filigrana.

  
**Restituisce**: Colore del carattere come stringa (ad esempio, "#000000").
  
### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.
