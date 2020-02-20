---
title: Classe mip::CustomAction
description: 'Documenta la classe MIP:: CustomAction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 9dfbd444684f68b954dd577c9ccdd208f55f9a89
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490196"
---
# <a name="class-mipcustomaction"></a>Classe mip::CustomAction 
CustomAction è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Ottiene il nome dell'azione.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetProperties () const  |  Ottiene l'elenco di coppie valore-chiave delle proprietà.
  
## <a name="members"></a>Members
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'azione.

  
**Restituisce**: il nome dell'azione, se esistente. In caso contrario restituisce una stringa vuota.
  
### <a name="getproperties-function"></a>GetProperties (funzione)
Ottiene l'elenco di coppie valore-chiave delle proprietà.

  
**Restituisce**: elenco di coppie chiave-valore.