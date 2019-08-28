---
title: Classe mip::AddWatermarkAction
description: 'Documenta la classe MIP:: addwatermarkaction di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2b6a50385e5d891b8893949a8761e7f38f591f17
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056345"
---
# <a name="class-mipaddwatermarkaction"></a>Classe mip::AddWatermarkAction 
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

  
**Restituisce**: Nome che deve essere utilizzato per l'elemento dell'interfaccia utente che include la filigrana. Lo stesso nome verrà restituito in RemoveWatermarkingAction nel caso in cui la filigrana debba essere rimossa.
  
### <a name="getlayout-function"></a>Funzione GetLayout
API usata per ottenere il layout della filigrana.

  
**Restituisce**: WatermarkLayout Layout della filigrana nel formato di un'enumerazione HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext-function"></a>Funzione gettext
Ottiene il testo destinato a essere inserito nella filigrana.

  
**Restituisce**: Testo dell'intestazione del contenuto.
  
### <a name="getfontname-function"></a>GetFontName (funzione)
Ottiene il nome del tipo di carattere usato per visualizzare la filigrana.

  
**Restituisce**: Nome del tipo di carattere. Il valore predefinito è Calibri se non ne viene impostato nessuno dai criteri.
  
### <a name="getfontsize-function"></a>Funzione GetFontSize
Ottiene le dimensioni del carattere usate per visualizzare la filigrana.

  
**Restituisce**: Dimensioni del carattere come numero intero.
  
### <a name="getfontcolor-function"></a>GetFontColor (funzione)
Ottiene il colore del carattere usato per visualizzare la filigrana.

  
**Restituisce**: Colore del carattere sotto forma di stringa, ad esempio "#000000".