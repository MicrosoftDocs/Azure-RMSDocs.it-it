---
title: Classe mip::AddContentHeaderAction
description: 'Classe MIP:: addcontentheaderaction di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 367626955ba1652b20b372efd309d15304e5336f
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184859"
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
  
### <a name="getuielementname-function"></a>GetUIElementName (funzione)
API usata per contrassegnare l'elemento di intestazione contenuto.

  
**Restituisce**: Il nome deve essere utilizzato per l'elemento dell'interfaccia utente che contiene l'intestazione contenuto. Lo stesso nome verrà restituito in [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) nel caso in cui l'intestazione contenuto debba essere rimossa.
  
### <a name="gettext-function"></a>GetText (funzione)
Ottiene il testo destinato a essere inserito nell'intestazione contenuto.

  
**Restituisce**: Testo dell'intestazione contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: Nome del tipo di carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>GetFontSize (funzione)
Ottiene le dimensioni del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare l'intestazione contenuto.

  
**Restituisce**: Colore del carattere sotto forma di stringa (ad esempio, #000000 ").
  
### <a name="getalignment-function"></a>GetAlignment (funzione)
Ottiene l'allineamento dell'intestazione.

  
**Restituisce**: Enumeratore ContentMarkAlignment: LEFT | RIGHT | CENTRO. 
  
**Vedere anche**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment)
  
### <a name="getmargin-function"></a>GetMargin (funzione)
Ottiene il margine dell'intestazione a partire dal basso.

  
**Restituisce**: I margini dalla parte inferiore del documento (ad esempio 10 mm).

### <a name="gettype-function"></a>Funzione GetType
Specifica il tipo di [Action](class_mip_action.md).

  
**Restituisce**: ActionType Tipo di azione derivata in cui è possibile eseguire il cast di questa classe di base.