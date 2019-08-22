---
title: Classe mip::CustomAction
description: 'Documenta la classe MIP:: CustomAction di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: e71adc9c791f71b73c9386955d6b9606f2554f83
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884379"
---
# <a name="class-mipcustomaction"></a>Classe mip::CustomAction 
[CustomAction](class_mip_customaction.md) è una classe di azione generica che acquisisce tutte le sottoproprietà dell'azione sotto forma di contenitore delle proprietà. Il chiamante ha la responsabilità di comprendere il significato dell'azione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Ottiene il nome dell'azione.
public const std::\<vector std::p\<aria std:: String, std::\>String\>& GetProperties () const  |  Ottiene l'elenco di coppie valore-chiave delle proprietà.
  
## <a name="members"></a>Members
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'azione.

  
**Restituisce**: Nome dell'azione se ne esiste una stringa vuota.
  
### <a name="getproperties-function"></a>GetProperties (funzione)
Ottiene l'elenco di coppie valore-chiave delle proprietà.

  
**Restituisce**: Elenco di coppie chiave-valore.