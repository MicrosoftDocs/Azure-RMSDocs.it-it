---
title: Criteri predefiniti per Azure Information Protection
description: "Informazioni sulla configurazione dei criteri predefiniti per Azure Information Protection. Se si modificano i criteri predefiniti, è possibile fare riferimento a questi valori per ripristinare le impostazioni predefinite dei criteri."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/09/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
ms.openlocfilehash: d89acde3a2d9e4db529c429fdedf2f3ed05e2fe5
ms.sourcegitcommit: 335c854eb5c6f387a9369d4b6f1e22160517e6ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2018
---
# <a name="the-default-azure-information-protection-policy"></a>Criteri predefiniti di Azure Information Protection

>*Si applica a: Azure Information Protection*

Le informazioni seguenti sono utili per comprendere come viene configurato il criterio predefinito per Azure Information Protection.

Quando un amministratore si connette per la prima volta al servizio Azure Information Protection tramite il portale di Azure, vengono creati i criteri predefiniti del tenant. Microsoft potrebbe occasionalmente modificare i criteri predefiniti, pertanto se è già stato usato il servizio prima della modifica dei criteri predefiniti, la versione precedente dei criteri non è aggiornata perché potrebbero essere già stati configurati e distribuiti nell'ambiente di produzione.

È possibile fare riferimento ai valori seguenti per riportare i criteri alle impostazioni predefinite o aggiornare i criteri ai valori più recenti.

## <a name="current-default-policy"></a>Criteri predefiniti correnti

Questa versione dei criteri predefiniti è del 31 luglio 2017.

I criteri predefiniti vengono creati al momento dell'attivazione del servizio Azure Rights Management, come nel caso dei nuovi tenant a partire da febbraio 2018. Per altre informazioni, vedere l'annuncio del post di blog [Improvements to the protection stack in Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/08/improvements-to-the-protection-stack-in-azure-information-protection) (Miglioramenti dello stack di protezione in Azure Information Protection).

I criteri predefiniti vengono creati anche se è stato [attivato il servizio](activate-service.md) manualmente prima di creare i criteri. 

Se il servizio non è stato attivato, i criteri predefiniti non configurano la protezione per le seguenti etichette secondarie:

- **Riservato\Tutti i dipendenti**

- **Riservato\Solo i destinatari**

- **Riservatezza elevata\Tutti i dipendenti** 

- **Riservatezza elevata\Solo i destinatari** 

Quando queste etichette secondarie non vengono configurate automaticamente per la protezione, il criterio predefinito rimane identico al [criterio predefinito precedente](#default-policy-before-july-31-2017).

Quando viene applicata alle etichette secondarie per **Tutti i dipendenti**, la protezione è configurata usando i modelli predefiniti che vengono convertiti automaticamente in etichette nel portale di Azure. Per altre informazioni sui modelli, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

A partire dal 30 agosto 2017 questa versione dei criteri predefiniti include versioni in più lingue dei nomi delle etichette e delle descrizioni. 

#### <a name="more-information-about-the-recipients-only-sublabel"></a>Ulteriori informazioni sull'etichetta secondaria Solo i destinatari

Gli utenti vedono questa etichetta solo in Outlook. Non visualizzano questa etichetta in Word, Excel, PowerPoint o da Esplora File. 

Quando gli utenti selezionano questa etichetta, l'opzione Non inoltrare di Outlook viene applicata automaticamente al messaggio di posta elettronica. I destinatari specificati dagli utenti non possono inoltrare il messaggio di posta elettronica e non è possibile copiare o stampare il contenuto o salvare gli allegati.


### <a name="labels"></a>Etichette

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Dati non business, solo per uso personale.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Pubblico|Dati business appositamente preparati e approvati per l'uso pubblico.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Generale|Dati business non sono destinati a uso pubblico. Questi dati possono tuttavia essere condivisi con partner esterni, se necessario. Ad esempio, un elenco telefonico interno della società, organigrammi, standard interni e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Confidential (Riservato)|Dati aziendali riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential (Riservatezza elevata)|Dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|


### <a name="sublabels"></a>Etichette secondarie

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Confidential \ All Employees (Riservato \ Tutti i dipendenti)|Dati riservati che richiedono protezione, ma che garantiscono autorizzazioni complete a tutti i dipendenti. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: Azure (chiave cloud) [[1]](#footnote-1)|
|Confidential \ Anyone (not protected) (Riservato \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservato\Solo i destinatari|Dati riservati che richiedono protezione e che possono essere visualizzati soltanto dai destinatari.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: Configura le autorizzazioni definite dall'utente (anteprima), In Outlook applica Non inoltrare|
|Highly Confidential \ All Employees (Riservatezza elevata \ Tutti i dipendenti)|Dati particolarmente riservati che garantiscono a tutti i dipendenti autorizzazioni di visualizzazione, modifica e risposta per il relativo contenuto. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: Azure (chiave cloud) [[2]](#footnote-2)|
|Highly Confidential \ Anyone (not protected) (Riservatezza elevata \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Riservatezza elevata\Solo i destinatari|Dati altamente riservati che richiedono protezione e che possono essere visualizzati soltanto dai destinatari.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: Configura le autorizzazioni definite dall'utente (anteprima), In Outlook applica Non inoltrare|

###### <a name="footnote-1"></a>Nota 1
Le autorizzazioni di protezione corrispondono a quelle del [modello predefinito](configure-policy-templates.md#default-templates), **Riservato\Tutti i dipendenti**.

###### <a name="footnote-2"></a>Nota 2 
Le autorizzazioni di protezione corrispondono a quelle del [modello predefinito](configure-policy-templates.md#default-templates), **Riservatezza elevata\Tutti i dipendenti**.


### <a name="information-protection-bar"></a>Barra Information Protection

|Impostazione|Valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|Etichetta corrente per questo contenuto. Questa impostazione identifica il rischio per l'azienda se questo contenuto è condiviso con persone non autorizzate all'interno o all'esterno dell'organizzazione.|


### <a name="settings"></a>Impostazioni

|Impostazione|Valore|
|-------------------------------|---------------------------|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Off|
|Selezionare l'etichetta predefinita|Nessuno|
|Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione|Off|
|For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)|Off|
|Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection)|Vuoto|


## <a name="default-policy-before-july-31-2017"></a>Criteri predefiniti prima del 31 luglio 2017

Si noti che le descrizioni in questi criteri fanno riferimento ai dati che richiedono protezione e anche al rilevamento e alla revoca dei dati. I criteri non configurano tale protezione per queste etichette, per cui è necessario eseguire altri passaggi per completare questa descrizione. Ad esempio configurare l'etichetta per applicare la protezione o usare una soluzione di prevenzione della perdita dei dati (DLP). Prima di poter essere rilevato e revocato tramite il sito di rilevamento dei documenti, un documento deve essere protetto dal servizio Azure Rights Management e rilevato dalla persona che lo ha protetto. 


### <a name="labels"></a>Etichette

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Dati non business, solo per uso personale.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Pubblico|Dati business appositamente preparati e approvati per l'uso pubblico.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Generale|Dati business non sono destinati a uso pubblico. Questi dati possono tuttavia essere condivisi con partner esterni, se necessario. Ad esempio, un elenco telefonico interno della società, organigrammi, standard interni e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Confidential (Riservato)|Dati aziendali riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential (Riservatezza elevata)|Dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|


### <a name="sublabels"></a>Etichette secondarie

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Confidential \ All Employees (Riservato \ Tutti i dipendenti)|Dati riservati che richiedono protezione, ma che garantiscono autorizzazioni complete a tutti i dipendenti. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Confidential \ Anyone (not protected) (Riservato \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Confidential (Classificato come riservato) <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential \ All Employees (Riservatezza elevata \ Tutti i dipendenti)|Dati particolarmente riservati che garantiscono a tutti i dipendenti autorizzazioni di visualizzazione, modifica e risposta per il relativo contenuto. I proprietari dei dati possono tenere traccia e revocare il relativo contenuto.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Highly Confidential \ Anyone (not protected) (Riservatezza elevata \ Chiunque (senza protezione))|Dati che non richiedono protezione. Usare questa opzione con cautela e giustificazione aziendale appropriata.|**Abilitato**: on <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica)<br /><br />Classified as Highly Confidential (Classificato con riservatezza elevata)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|

### <a name="information-protection-bar"></a>Barra Information Protection

|Impostazione|Valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|Etichetta corrente per questo contenuto. Questa impostazione identifica il rischio per l'azienda se questo contenuto è condiviso con persone non autorizzate all'interno o all'esterno dell'organizzazione.|


### <a name="settings"></a>Impostazioni

|Impostazione|Valore|
|-------------------------------|---------------------------|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Off|
|Selezionare l'etichetta predefinita|Nessuno|
|Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione|Off|
|For email messages with attachments, apply a label that matches the highest classification of those attachments (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati)|Off|
|Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection)|Vuoto|

## <a name="default-policy-before-march-21-2017"></a>Criteri predefiniti prima del 21 marzo 2017

### <a name="labels"></a>Etichette

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Personal|Solo per uso personale. I dati verranno monitorati dall'organizzazione. Le informazioni personali non devono includere dati aziendali.|**Abilitato**: on <br /><br />**Colore**: verde chiaro<br /><br />**Contrassegni visivi**: off <br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Pubblico|Queste informazioni sono interne e possono essere usate da tutti gli utenti all'interno o all'esterno dell'azienda.|**Abilitato**: on <br /><br />**Colore**: verde<br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Interno|Queste informazioni includono un'ampia gamma di dati aziendali interni che possono essere usati da tutti i dipendenti e possono essere condivisi con i clienti e partner commerciali autorizzati. Esempi di informazioni interne sono i criteri aziendali e la maggior parte delle comunicazioni interne.|**Abilitato**: on <br /><br />**Colore**: blu <br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica): <br /><br />Riservatezza: Internal<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Confidential (Riservato)|Questi dati includono informazioni aziendali riservate. L'esposizione di questi dati a utenti non autorizzati potrebbe arrecare un danno all'organizzazione. Esempi di informazioni riservate sono i dati relativi ai dipendenti, progetti o contratti di singoli clienti e i dati degli account di vendita.|**Abilitato**: on <br /><br />**Colore**: arancione<br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica):<br /><br /> Riservatezza: Confidential (Riservato)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Secret (Segreto)|Questi dati includono informazioni estremamente riservate dell'azienda, che devono essere protette. L'esposizione dei dati segreti a utenti non autorizzati potrebbe arrecare un grave danno all'organizzazione. Sono informazioni segrete, ad esempio, i dati di identificazione personale, i record dei clienti, il codice sorgente e i rendiconti finanziari annunciati in anticipo.|**Abilitato**: on <br /><br />**Colore**: rosso<br /><br />**Contrassegni visivi**: piè di pagina (documenti e messaggi di posta elettronica):<br /><br /> Riservatezza: Secret (Segreto)<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|


### <a name="sublabels"></a>Etichette secondarie

|Label|Descrizione comando|Impostazioni|
|-------------------------------|---------------------------|-----------------|
|Secret (Segreto) \ All Company (Tutta la società)|Questi dati includono informazioni aziendali riservate, cui possono accedere tutti i dipendenti della società.|**Abilitato**: on <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|
|Secret (Segreto) \ My Group (Gruppo personale)|Questi dati includono informazioni aziendali riservate, cui possono accedere solo determinati gruppi di dipendenti.|**Abilitato**: on <br /><br />**Contrassegni visivi**: off<br /><br />**Condizioni**: nessuna<br /><br />**Protezione**: nessuna|

### <a name="information-protection-bar"></a>Barra Information Protection

|Impostazione|Valore|
|-------------------------------|---------------------------|
|Titolo|Sensibilità|
|Descrizione comando|La riservatezza delle informazioni è suddivisa in quattro livelli, ovvero Public (Pubblico), Internal (Interno), Confidential (Riservato) e Secret (Segreto), che consentono di identificare il rischio derivante dall'esposizione delle informazioni a utenti non autorizzati all'interno o all'esterno dell'azienda.|


### <a name="settings"></a>Impostazioni

|Impostazione|Valore|
|-------------------------------|---------------------------|
|Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta applicata automaticamente o dagli utenti|Off|
|Selezionare l'etichetta predefinita|Nessuno|
|Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione|Off|
|Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection)|Vuoto|


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]