---
title: Criterio predefinito di Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 977cbf2f45cab75aaca9c2a16dd1564c2af2fe4a


---

# Criterio predefinito di Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Le informazioni seguenti sono utili per comprendere come viene configurato il criterio predefinito per Azure Information Protection. Se si modifica il criterio predefinito, è possibile fare riferimento a questi valori per ripristinare le impostazioni predefinite del proprio criterio.

## Barra Information Protection

Titolo: **Sensitivity** (Riservatezza)

Descrizione comando: **la riservatezza delle informazioni è suddivisa in quattro livelli, ovvero Public (Pubblico), Internal (Interno), Confidential (Riservato) e Secret (Segreto), che consentono di identificare il rischio derivante dall'esposizione delle informazioni a utenti non autorizzati all'interno o all'esterno dell'azienda.**


## Etichette

Sono disponibili 5 etichette predefinite che hanno le impostazioni seguenti:

### **Personal**

Descrizione comando: **solo per uso personale. I dati verranno monitorati dall'organizzazione. Le informazioni personali non devono includere dati aziendali.**

Colore: verde chiaro

Contrassegni visivi: nessuno

Condizioni: nessuna

Protezione: no

----


### **Pubblico**

Descrizione comando: **queste informazioni sono interne e possono essere usate da tutti gli utenti all'interno o all'esterno dell'azienda.**

Colore: verde

Contrassegni visivi: nessuno

Condizioni: nessuna

Protezione: no

----

### **Interno**

Descrizione comando: **queste informazioni includono un'ampia gamma di dati aziendali interni che possono essere usati da tutti i dipendenti e possono essere condivisi con i clienti e partner commerciali autorizzati. Esempi di informazioni interne sono i criteri aziendali e la maggior parte delle comunicazioni interne.**

Colore: blu

Contrassegni visivi: piè di pagina (documenti e messaggi di posta elettronica)

Condizioni: nessuna

Protezione: no

----

### **Confidential (Riservato)**

Descrizione comando: **questi dati includono informazioni aziendali riservate. L'esposizione di questi dati a utenti non autorizzati potrebbe arrecare un danno all'organizzazione. Esempi di informazioni riservate sono i dati relativi ai dipendenti, progetti o contratti di singoli clienti e i dati degli account di vendita.**

Colore: arancione

Contrassegni visivi: piè di pagina (documenti e messaggi di posta elettronica)

Condizioni: nessuna

Protezione: no

----

### **Secret (Segreto)**

Descrizione comando: **questi dati includono informazioni estremamente riservate dell'azienda, che devono essere protette. L'esposizione dei dati segreti a utenti non autorizzati potrebbe arrecare un grave danno all'organizzazione. Sono informazioni segrete, ad esempio, i dati di identificazione personale, i record dei clienti, il codice sorgente e i rendiconti finanziari annunciati in anticipo.**

Colori: rosso

Contrassegni visivi: piè di pagina (documenti e messaggi di posta elettronica)

Condizioni: nessuna

Protezione: no

----


## Etichette secondarie

Sono disponibili 2 etichette secondarie predefinite che hanno le impostazioni seguenti:

### Secret (Segreto) > **All Company** (Tutta la società)

Descrizione comando: **questi dati includono informazioni aziendali riservate, cui possono accedere tutti i dipendenti della società.**

Contrassegni visivi: nessuno

Condizioni: nessuna

Protezione: no

----

### Secret (Segreto) > **My Group** (Gruppo personale)

Descrizione comando: **questi dati includono informazioni aziendali riservate, cui possono accedere solo determinati gruppi di dipendenti.**

Contrassegni visivi: nessuno

Condizioni: nessuna

Protezione: no

## Impostazioni globali

**All documents and emails must have a label (applied automatically or by users)** (Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta, applicata automaticamente o dagli utenti): No

**Select the default label** (Selezionare l'etichetta predefinita): Nessuna

**Users must provide justification when lowering the sensitivity level** (Gli utenti devono giustificare l'abbassamento del livello di riservatezza), ad esempio da Confidential (Riservato) a Public (Pubblico): No

## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy). 



<!--HONumber=Jul16_HO5-->


