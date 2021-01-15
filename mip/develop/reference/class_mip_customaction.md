---
title: Classe CustomAction
description: 'Documenta la classe CustomAction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d1fb231d76ba2b5f076d42bbeeff95618c7386f3
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211703"
---
# <a name="class-customaction"></a>Classe CustomAction 
CustomAction è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Ottiene il nome dell'azione.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetProperties () const  |  Ottiene l'elenco di coppie valore-chiave delle proprietà.
  
## <a name="members"></a>Membri
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'azione.

  
**Restituisce**: il nome dell'azione, se esistente. In caso contrario restituisce una stringa vuota.
  
### <a name="getproperties-function"></a>GetProperties (funzione)
Ottiene l'elenco di coppie valore-chiave delle proprietà.

  
**Restituisce**: elenco di coppie chiave-valore.