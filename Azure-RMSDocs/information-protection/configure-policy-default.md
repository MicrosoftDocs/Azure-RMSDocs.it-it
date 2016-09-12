---
title: Criterio predefinito di Azure Information Protection | Azure Rights Management
description: "Informazioni sulla configurazione dei criteri predefiniti per Azure Information Protection. Se si modifica il criterio predefinito, è possibile fare riferimento a questi valori per ripristinare le impostazioni predefinite del proprio criterio."
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: da0145444a7d0abb6407ed2ccbb581d4dcdd10d6
ms.openlocfilehash: 44dd47bd73eabe73241ab331c5dee7e06c6c0bef


---

# Criterio predefinito di Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Le informazioni seguenti sono utili per comprendere come viene configurato il criterio predefinito per Azure Information Protection. Se si modifica il criterio predefinito, è possibile fare riferimento a questi valori per ripristinare le impostazioni predefinite del proprio criterio.

## Barra Information Protection

|Impostazioni|Valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|La riservatezza delle informazioni è suddivisa in quattro livelli, ovvero Public (Pubblico), Internal (Interno), Confidential (Riservato) e Secret (Segreto), che consentono di identificare il rischio derivante dall'esposizione delle informazioni a utenti non autorizzati all'interno o all'esterno dell'azienda.|

## Etichette

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Solo per uso personale. I dati verranno monitorati dall'organizzazione. Le informazioni personali non devono includere dati aziendali.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|
|Pubblico|Queste informazioni sono interne e possono essere usate da tutti gli utenti all'interno o all'esterno dell'azienda.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|
|Interno|Queste informazioni includono un'ampia gamma di dati aziendali interni che possono essere usati da tutti i dipendenti e possono essere condivisi con i clienti e partner commerciali autorizzati. Esempi di informazioni interne sono i criteri aziendali e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|
|Confidential (Riservato)|Questi dati includono informazioni aziendali riservate. L'esposizione di questi dati a utenti non autorizzati potrebbe arrecare un danno all'organizzazione. Esempi di informazioni riservate sono i dati relativi ai dipendenti, progetti o contratti di singoli clienti e i dati degli account di vendita.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|
|Secret (Segreto)|Questi dati includono informazioni estremamente riservate dell'azienda, che devono essere protette. L'esposizione dei dati segreti a utenti non autorizzati potrebbe arrecare un grave danno all'organizzazione. Sono informazioni segrete, ad esempio, i dati di identificazione personale, i record dei clienti, il codice sorgente e i rendiconti finanziari annunciati in anticipo.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|

## Etichette secondarie

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|*Secret* (Segreto) > All Company (Tutta la società)|Questi dati includono informazioni aziendali riservate, cui possono accedere tutti i dipendenti della società.|**Abilitato**: on <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|
|*Secret* (Segreto) > My Group (Gruppo personale)|Questi dati includono informazioni aziendali riservate, cui possono accedere solo determinati gruppi di dipendenti.|**Abilitato**: on <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: no|

## Impostazioni globali

|Impostazioni|Valore|
|-------------------------------|---------------------------|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Off|
|Selezionare l'etichetta predefinita|Nessuno|
|Users must provide justification when lowering the sensitivity level (Gli utenti devono giustificare l'abbassamento del livello di riservatezza), ad esempio da Confidential (Riservato) a Public (Pubblico)|Off|


## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy). 



<!--HONumber=Aug16_HO4-->


