---
title: Assegnazione di etichette e protezione-Microsoft Information Protection SDK
description: Operazioni di Microsoft Information Protection Software Development Kit.
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 2e18b9ae65a4915807fdcb8fc37dd18396270fee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865011"
---
# <a name="labeling-and-pre-existing-protection-in-microsoft-information-protection-sdk"></a>Assegnazione di etichette e protezione preesistente in Microsoft Information Protection SDK

Microsoft Information Protection supporta l'assegnazione di etichette e i servizi di classificazione. Gli utenti e le applicazioni possono applicare quanto segue ai file supportati:

- Classificazione solo tramite l'applicazione di un'etichetta

- Classificazione e protezione tramite l'applicazione di un'etichetta

- Solo protezione

Questo articolo illustra il modo in cui l'SDK gestisce il tentativo di applicazione di un'etichetta a un file con protezione preesistente. Quando il documento dispone di protezione preesistente tramite l'applicazione di un'etichetta o in caso contrario, SDK gestisce l'applicazione di una nuova etichetta negli scenari indicati di seguito.

## <a name="label-based-protection-when-label-metadata-has-been-stripped"></a>Protezione basata su etichette quando i metadati dell'etichetta sono stati rimossi

Se per un file è stata applicata un'etichetta e l'etichetta applica la protezione, l'SDK deve essere in grado di risolvere tale protezione file con l'etichetta specifica. Se un utente che dispone di autorizzazioni di "modifica" sul file, rimuove i metadati dell'etichetta in modo accidentale o dannoso, la protezione rimane ancora. Quando l'SDK successivo interagisce con il file, esamina i dati di protezione, risolve tale modello di protezione nell'etichetta originale e riapplica l'etichetta. Si tratta di un meccanismo di sicurezza integrato nell'SDK per la protezione delle informazioni, nel caso in cui i metadati dell'etichetta vengano manomessi.

## <a name="custom-protection-and-label-applications"></a>Applicazioni per la protezione e l'etichetta personalizzate

Se per il file è stata applicata una qualche forma di protezione, tramite un modello RMS e un utente tenta di applicare un'etichetta al file, l'SDK deve prima essere in grado di risolvere la protezione originale in un'etichetta. Non essendo in grado di eseguire questa operazione, l'SDK non sarà in grado di valutare se il nuovo livello di sensibilità della protezione è più restrittivo o permissivo rispetto alla sensibilità originale per la protezione e, di conseguenza, l'SDK non applicherà la nuova etichetta al file.

## <a name="user-defined-permissions"></a>Autorizzazioni definite dall'utente

Se a un file è applicata un'etichetta e l'etichetta applica la protezione definita dall'utente, la protezione viene applicata al file, ma non esiste alcun modo per l'SDK per risolvere lo stesso in un modello RMS. In questo caso, quando un utente tenta di applicare una nuova etichetta al file, SDK considera l'azione simile alla precedente e non applica la nuova etichetta al file.
