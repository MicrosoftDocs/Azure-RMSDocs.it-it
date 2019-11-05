---
title: Classe mip::CustomAction
description: 'Documenta la classe MIP:: CustomAction di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 450ae0e455f74c6cb9b1f6b0b6d8aded9b30b2bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558899"
---
# <a name="class-mipcustomaction"></a>Classe mip::CustomAction 
CustomAction è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Ottiene il nome dell'azione.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetProperties () const  |  Ottiene l'elenco di coppie valore-chiave delle proprietà.
  
## <a name="members"></a>Membri
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'azione.

  
**Restituisce**: il nome dell'azione, se esistente. In caso contrario restituisce una stringa vuota.
  
### <a name="getproperties-function"></a>GetProperties (funzione)
Ottiene l'elenco di coppie valore-chiave delle proprietà.

  
**Restituisce**: elenco di coppie chiave-valore.