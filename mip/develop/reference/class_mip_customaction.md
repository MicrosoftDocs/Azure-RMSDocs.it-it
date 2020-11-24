---
title: Classe CustomAction
description: 'Documenta la classe CustomAction:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc67920b517f3a9f75c395b42350cec9d75b23b3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567171"
---
# <a name="class-customaction"></a>Classe CustomAction 
CustomAction è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Ottiene il nome dell'azione.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetProperties () const  |  Ottiene l'elenco di coppie valore-chiave delle proprietà.
  
## <a name="members"></a>Members
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'azione.

  
**Restituisce**: il nome dell'azione, se esistente. In caso contrario restituisce una stringa vuota.
  
### <a name="getproperties-function"></a>GetProperties (funzione)
Ottiene l'elenco di coppie valore-chiave delle proprietà.

  
**Restituisce**: elenco di coppie chiave-valore.