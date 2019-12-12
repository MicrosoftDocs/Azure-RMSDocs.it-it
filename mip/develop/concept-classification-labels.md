---
title: Concetti - Etichette di classificazione
description: Questo articolo aiuterà a comprendere come vengono usate le etichette per la classificazione dei dati.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e1101bd505a35e02fdeeed032d5dec61364bfb8d
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "60175243"
---
# <a name="microsoft-information-protection-sdk---classification-label-concepts"></a>Microsoft Information Protection SDK - Concetti relativi alle etichette di classificazione

Come parte di una strategia di protezione dei dati completa, le organizzazioni devono implementare un sistema di classificazione dei dati che definisce i livelli di riservatezza dei dati all'interno dell'organizzazione e quindi mappare gli attributi dei documenti a tali classificazioni.

Gli attributi correlati alla classificazione in genere comportano **rischi** per l'organizzazione, se tali dati o documenti vanno perduti o diventano visibili per soggetti non autorizzati. Nel noto sistema di classificazione adottato dall'amministrazione pubblica statunitense esistono tre livelli di classificazione. Ogni livello ha una definizione che descrive quando deve essere applicata tale classificazione:

* **Top Secret (Segretissimo)** : si applica alle informazioni, la cui divulgazione non autorizzata è ragionevolmente prevedibile causi danni estremamente gravi alla sicurezza nazionale che l'autorità di classificazione originale sia in grado di identificare o descrivere.
* **Secret (Segreto)** : si applica alle informazioni, la cui divulgazione non autorizzata è ragionevolmente prevedibile causi seri danni alla sicurezza nazionale che l'autorità di classificazione originale sia in grado di identificare o descrivere.
* **Confidential (Riservato)** : si applica alle informazioni, la cui divulgazione non autorizzata è ragionevolmente prevedibile causi danni alla sicurezza nazionale che l'autorità di classificazione originale sia in grado di identificare o descrivere.
* **Non classificato**: non è effettivamente una classificazione, ma piuttosto l'assenza di una delle tre classificazioni precedenti.

In un'applicazione del settore privato o commerciale, si potrebbe definire un elenco simile a quello predefinito nel servizio Azure Information Protection con valori monetari collegati.

* **Riservatissimo**: si applica alle informazioni, la cui divulgazione non autorizzata è ragionevolmente prevedibile causi danni maggiori di 1 milione di dollari USA.
* **Riservato**: si applica alle informazioni, la cui divulgazione non autorizzata è ragionevolmente prevedibile causi danni maggiori di 100.000 dollari USA.
* **Generale**: si applica alle informazioni, la cui divulgazione non autorizzata è ragionevolmente prevedibile causi danni misurabili di minore entità.
* **Pubblico**: si applica alle informazioni destinate alla divulgazione esterna al pubblico. 
* **Non aziendale**: si applica alle informazioni non correlate alle attività dell'azienda, direttamente o indirettamente.

Ogni classificazione descrive il rischio per l'azienda in caso di divulgazione non autorizzata delle informazioni corrispondenti. Dopo aver individuato queste classificazione e condizioni, occorre identificare gli attributi di identificazione che consentono ai proprietari dei dati di comprendere le classificazioni da applicare.

## <a name="labeling"></a>Etichettatura

L'atto di associare una classificazione dei dati a un set di informazioni è detto **etichettatura**. Dato che MIP SDK si occupa dell'applicazione di **etichette** di classificazione ai documenti, non si parlerà di classificazioni, ma piuttosto di etichette. Un utente o processo ha già **classificato** i dati in base alla conoscenza delle informazioni: MIP SDK eseguirà quindi l'**etichettatura** delle informazioni.

## <a name="labels-in-the-mip-sdk"></a>Etichette in MIP SDK

Le etichette sono un componente fondamentale di MIP SDK. Le etichette sono l'elemento cruciale per assegnare tag, proteggere e contrassegnare il contenuto di tutti i documenti a cui viene applicato l'SDK. L'SDK consente di:

* Applicare etichette ai documenti
* Leggere le etichette esistenti nei documenti
* Modificare un'etichetta esistente con giustificazione obbligatoria se richiesto dai criteri
* Rimuovere un'etichetta da un documento

L'etichetta applicherà la protezione e contrassegnerà il contenuto in base all'etichetta di configurazione definita dagli amministratori nel Centro sicurezza e conformità. 

## <a name="miplabel-vs-mipcontentlabel"></a>mip::Label o mip::ContentLabel

Esistono due tipi di etichette in MIP SDK. `Label` e `ContentLabel`.

* Label: un'etichetta che può essere applicata da un utente o processo, in base a quanto definito nei criteri dell'organizzazione.
* ContentLabel: un'etichetta che esiste già per documenti o informazioni. Può essere letta, aggiornata o rimossa. 

In altre parole, `ContentLabel` è un'etichetta `Label` applicata a un'informazione.

## <a name="metadata"></a>Metadati

L'SDK supporta anche l'aggiunta di metadati aggiuntivi ai documenti sotto forma di coppie chiave/valore. Se l'organizzazione usa sottoclassificazioni o tag che descrivono le informazioni in modo più specifico, è possibile usare l'SDK per applicare i metadati.

## <a name="next-steps"></a>Passaggi successivi

Per altri dettagli sul sistema di classificazione dell'amministrazione pubblica statunitense, vedere https://www.gpo.gov/fdsys/pkg/FR-2010-01-05/html/E9-31418.htm.
