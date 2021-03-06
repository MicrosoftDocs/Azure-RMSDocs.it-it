---
title: Criteri predefiniti per Azure Information Protection - AIP
description: Informazioni sulla configurazione dei criteri predefiniti per Azure Information Protection. Se si modificano i criteri predefiniti, è possibile fare riferimento a questi valori per ripristinare le impostazioni predefinite dei criteri.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 7a8715e62a0b3690fd923aeb2c4662eb0732cc91
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806686"
---
# <a name="the-default-azure-information-protection-policy"></a>Criteri predefiniti di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Le informazioni seguenti sono utili per comprendere come viene configurato il criterio predefinito per Azure Information Protection.

Quando un amministratore si connette per la prima volta al servizio Azure Information Protection tramite il portale di Azure, vengono creati i criteri predefiniti di Azure Information Protection per il tenant. Microsoft potrebbe occasionalmente modificare i criteri predefiniti, pertanto se è già stato usato il servizio prima della modifica dei criteri predefiniti, la versione precedente dei criteri di Azure Information Protection non è aggiornata perché potrebbero essere già stati configurati e distribuiti nell'ambiente di produzione.

È possibile fare riferimento ai valori seguenti per riportare i criteri di Azure Information Protection alle impostazioni predefinite o aggiornare i criteri di Azure Information Protection ai valori più recenti.

> [!IMPORTANT]
> A partire dall'aprile 2019, le etichette predefinite non vengono create automaticamente per i nuovi clienti. Per questi tenant viene effettuato automaticamente il provisioning della piattaforma di etichettatura unificata, quindi non è necessario eseguire la migrazione delle etichette dopo averle configurate nel portale di Azure.
> 
> Se per questi tenant non sono già state create etichette di riservatezza nel Centro sicurezza e conformità di Office 365, nel Centro sicurezza Microsoft 365 o nel Centro conformità Microsoft 365, è possibile creare le etichette predefinite dai criteri predefiniti correnti per Azure Information Protection. A tale scopo, selezionare **genera etichette predefinite** dal riquadro **etichette** e aggiungere le etichette ai criteri globali. Se non viene visualizzata l'opzione per generare etichette predefinite, potrebbe essere necessario attivare prima l'etichetta unificata dal riquadro **Gestisci**  >  **etichetta unificata** . Per istruzioni dettagliate, vedere [Guida introduttiva: Introduzione ad Azure Information Protection nel portale di Azure](quickstart-viewpolicy.md).


## <a name="current-default-policy"></a>Criteri predefiniti correnti

Questa versione dei criteri predefiniti di Azure Information Protection è del 31 luglio 2017.

I criteri predefiniti di Azure Information Protection vengono creati al momento dell'attivazione del servizio Azure Rights Management, come nel caso dei nuovi tenant a partire da febbraio 2018. Per altre informazioni, vedere l'annuncio del post di blog [Improvements to the protection stack in Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/08/improvements-to-the-protection-stack-in-azure-information-protection) (Miglioramenti dello stack di protezione in Azure Information Protection).

I criteri predefiniti di Azure Information Protection vengono creati anche se è stato [attivato il servizio](activate-service.md) manualmente prima di creare i criteri di Azure Information Protection. 

Se il servizio non è stato attivato, i criteri predefiniti di Azure Information Protection non configurano la protezione per le etichette secondarie seguenti:

- **Riservato \ Tutti i dipendenti**

- **Riservato\Solo i destinatari**

- **Riservatezza elevata \ Tutti i dipendenti** 

- **Riservatezza elevata\Solo i destinatari** 

Quando queste etichette secondarie non vengono configurate automaticamente per la protezione, i criteri predefiniti di Azure Information Protection rimangono identici ai [criteri predefiniti precedenti](#default-policy-before-july-31-2017).

Quando viene applicata alle etichette secondarie per **Tutti i dipendenti**, la protezione è configurata usando i modelli predefiniti che vengono convertiti automaticamente in etichette nel portale di Azure. Per altre informazioni sui modelli, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

A partire dal 30 agosto 2017, questa versione dei criteri predefiniti di Azure Information Protection include versioni in più lingue dei nomi delle etichette e delle descrizioni. 

#### <a name="more-information-about-the-recipients-only-sublabel"></a>Ulteriori informazioni sull'etichetta secondaria Solo i destinatari

Gli utenti vedono questa etichetta solo in Outlook. Non visualizzano questa etichetta in Word, Excel, PowerPoint o da Esplora File. 

Quando gli utenti selezionano questa etichetta, l'opzione Non inoltrare di Outlook viene applicata automaticamente al messaggio di posta elettronica. I destinatari specificati dagli utenti non possono inoltrare il messaggio di posta elettronica e non è possibile copiare o stampare il contenuto o salvare gli allegati.


### <a name="labels"></a>Etichette

|Etichetta|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Dati non business, solo per uso personale.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Pubblico|Dati business appositamente preparati e approvati per l'uso pubblico.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Generale|Dati business non sono destinati a uso pubblico. Questi dati possono tuttavia essere condivisi con partner esterni, se necessario. Ad esempio, un elenco telefonico interno della società, organigrammi, standard interni e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservato|Dati aziendali riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential (Riservatezza elevata)|Dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|


### <a name="sublabels"></a>Etichette secondarie

|Etichetta|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Confidential \ All Employees (Riservato \ Tutti i dipendenti)|Dati riservati che richiedono protezione, ma che garantiscono autorizzazioni complete a tutti i dipendenti. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: Azure (chiave cloud) [[1]](#footnote-1)|
|Confidential \ Anyone (not protected) (Riservato \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservato\Solo i destinatari|Dati riservati che richiedono protezione e che possono essere visualizzati soltanto dai destinatari.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: impostare le autorizzazioni definite dall'utente (anteprima [[3]](#footnote-3)), in Outlook applica non inoltrare|
|Highly Confidential \ All Employees (Riservatezza elevata \ Tutti i dipendenti)|Dati particolarmente riservati che garantiscono a tutti i dipendenti autorizzazioni di visualizzazione, modifica e risposta per il relativo contenuto. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: Azure (chiave cloud) [[2]](#footnote-2)|
|Highly Confidential \ Anyone (not protected) (Riservatezza elevata \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservatezza elevata\Solo i destinatari|Dati altamente riservati che richiedono protezione e che possono essere visualizzati soltanto dai destinatari.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: impostare le autorizzazioni definite dall'utente (anteprima [[3]](#footnote-3)), in Outlook applica non inoltrare|

###### <a name="footnote-1"></a>Nota 1
Le autorizzazioni di protezione corrispondono a quelle del [modello predefinito](configure-policy-templates.md#default-templates), **Riservato\Tutti i dipendenti**.

###### <a name="footnote-2"></a>Nota 2 
Le autorizzazioni di protezione corrispondono a quelle del [modello predefinito](configure-policy-templates.md#default-templates), **Riservatezza elevata\Tutti i dipendenti**.

###### <a name="footnote-3"></a>Nota a piè di pagina 3
Questa funzionalità è attualmente disponibile in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.

### <a name="information-protection-bar"></a>Barra Information Protection

|Impostazione|valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|Etichetta corrente per questo contenuto. Questa impostazione identifica il rischio per l'azienda se questo contenuto è condiviso con persone non autorizzate all'interno o all'esterno dell'organizzazione.|


### <a name="settings"></a>Impostazioni

Alcune impostazioni sono state aggiunte dopo il 31 luglio 2017.

|Impostazione|valore|
|-------------------------------|---------------------------|
|Selezionare l'etichetta predefinita|nessuno|
|Invia i dati di controllo alle analisi di Azure Information Protection|Disattivato|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Disattivato|
|Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione|Disattivato|
|For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)|Disattivato|
|Visualizza la barra di Information Protection nelle app Office|Disattivato|
|Aggiungi il pulsante Non inoltrare alla barra multifunzione di Outlook|Disattivato|
|Rendi disponibile agli utenti l'opzione per le autorizzazioni personalizzate|Disattivato|
|Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection)|Vuoto|

## <a name="default-policy-before-july-31-2017"></a>Criteri predefiniti prima del 31 luglio 2017

Si noti che le descrizioni in questi criteri fanno riferimento ai dati che richiedono protezione e anche al rilevamento e alla revoca dei dati. I criteri non configurano tale protezione per queste etichette, per cui è necessario eseguire altri passaggi per completare questa descrizione. Ad esempio configurare l'etichetta per applicare la protezione o usare una soluzione di prevenzione della perdita dei dati (DLP). Prima di poter essere rilevato e revocato tramite il sito di rilevamento dei documenti, un documento deve essere protetto dal servizio Azure Rights Management e rilevato dalla persona che lo ha protetto. 


### <a name="labels"></a>Etichette

|Etichetta|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Dati non business, solo per uso personale.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Pubblico|Dati business appositamente preparati e approvati per l'uso pubblico.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Generale|Dati business non sono destinati a uso pubblico. Questi dati possono tuttavia essere condivisi con partner esterni, se necessario. Ad esempio, un elenco telefonico interno della società, organigrammi, standard interni e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservato|Dati aziendali riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential (Riservatezza elevata)|Dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|


### <a name="sublabels"></a>Etichette secondarie

|Etichetta|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Confidential \ All Employees (Riservato \ Tutti i dipendenti)|Dati riservati che richiedono protezione, ma che garantiscono autorizzazioni complete a tutti i dipendenti. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Confidential \ Anyone (not protected) (Riservato \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential \ All Employees (Riservatezza elevata \ Tutti i dipendenti)|Dati particolarmente riservati che garantiscono a tutti i dipendenti autorizzazioni di visualizzazione, modifica e risposta per il relativo contenuto. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential \ Anyone (not protected) (Riservatezza elevata \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|

### <a name="information-protection-bar"></a>Barra Information Protection

|Impostazione|valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|Etichetta corrente per questo contenuto. Questa impostazione identifica il rischio per l'azienda se questo contenuto è condiviso con persone non autorizzate all'interno o all'esterno dell'organizzazione.|


### <a name="settings"></a>Impostazioni

|Impostazione|valore|
|-------------------------------|---------------------------|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Disattivato|
|Selezionare l'etichetta predefinita|nessuno|
|Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione|Disattivato|
|For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)|Disattivato|
|Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection)|Vuoto|

## <a name="default-policy-before-march-21-2017"></a>Criteri predefiniti prima del 21 marzo 2017

### <a name="labels"></a>Etichette

|Etichetta|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Solo per uso personale. I dati verranno monitorati dall'organizzazione. Le informazioni personali non devono includere dati aziendali.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Pubblico|Queste informazioni sono interne e possono essere usate da tutti gli utenti all'interno o all'esterno dell'azienda.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Interno|Queste informazioni includono un'ampia gamma di dati aziendali interni che possono essere usati da tutti i dipendenti e possono essere condivisi con i clienti e partner commerciali autorizzati. Esempi di informazioni interne sono i criteri aziendali e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica): <br /><br />Riservatezza: Internal<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservato|Questi dati includono informazioni aziendali riservate. L'esposizione di questi dati a utenti non autorizzati potrebbe arrecare un danno all'organizzazione. Esempi di informazioni riservate sono i dati relativi ai dipendenti, progetti o contratti di singoli clienti e i dati degli account di vendita.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica):<br /><br /> Riservatezza: Confidential (Riservato)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Segreto|Questi dati includono informazioni estremamente riservate dell'azienda, che devono essere protette. L'esposizione dei dati segreti a utenti non autorizzati potrebbe arrecare un grave danno all'organizzazione. Sono informazioni segrete, ad esempio, i dati di identificazione personale, i record dei clienti, il codice sorgente e i rendiconti finanziari annunciati in anticipo.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica):<br /><br /> Riservatezza: Secret (Segreto)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|


### <a name="sublabels"></a>Etichette secondarie

|Etichetta|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Secret (Segreto) \ All Company (Tutta la società)|Questi dati includono informazioni aziendali riservate, cui possono accedere tutti i dipendenti della società.|**Abilitato**: on <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Secret (Segreto) \ My Group (Gruppo personale)|Questi dati includono informazioni aziendali riservate, cui possono accedere solo determinati gruppi di dipendenti.|**Abilitato**: on <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|

### <a name="information-protection-bar"></a>Barra Information Protection

|Impostazione|valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|La riservatezza delle informazioni è suddivisa in quattro livelli, ovvero Public (Pubblico), Internal (Interno), Confidential (Riservato) e Secret (Segreto), che consentono di identificare il rischio derivante dall'esposizione delle informazioni a utenti non autorizzati all'interno o all'esterno dell'azienda.|


### <a name="settings"></a>Impostazioni

|Impostazione|valore|
|-------------------------------|---------------------------|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Disattivato|
|Selezionare l'etichetta predefinita|nessuno|
|Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione|Disattivato|
|Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection)|Vuoto|


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).