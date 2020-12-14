---
title: Azure Information Protection (AIP) assegnazione di etichette, classificazione e protezione
description: Informazioni su come Azure Information Protection (AIP) può assegnare etichette a documenti e messaggi di posta elettronica per classificare e proteggere i dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 71f07f5ffb9167ab61653cef10c610968ff74786
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384197"
---
# <a name="azure-information-protection-aip-labeling-classification-and-protection"></a>Azure Information Protection (AIP) assegnazione di etichette, classificazione e protezione

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Pertinente per**: [Azure Information Protection Unified Labeling client e il client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Azure Information Protection è una soluzione basata sul cloud che consente alle organizzazioni di classificare e proteggere documenti e messaggi di posta elettronica mediante l'applicazione di etichette. 

Ad esempio, l'amministratore potrebbe configurare un'etichetta con regole che rilevano dati sensibili, ad esempio le informazioni della carta di credito. In questo caso, qualsiasi utente che salva le informazioni della carta di credito in un file di Word potrebbe visualizzare una descrizione comando nella parte superiore del documento con la raccomandazione di applicare l'etichetta configurata per questo scenario.

Le etichette possono sia [classificare](#how-labels-apply-classification-with-aip) che, facoltativamente, [proteggere](#how-aip-protects-your-data) il documento consentendo di:

- **Tenere traccia e controllare** la modalità di utilizzo del contenuto
- **Analizzare i flussi di dati** per ottenere informazioni approfondite sull'azienda **- Rilevare comportamenti rischiosi** e adottare misure correttive
- **Tenere traccia dell'accesso ai documenti** ed evitare perdite di dati o uso improprio
- E altro ancora...

## <a name="how-labels-apply-classification-with-aip"></a>Classificazione tramite le etichette con AIP

L'assegnazione di etichette ai contenuti con AIP include:

- **Classificazione**, che può essere rilevata indipendentemente dalla posizione in cui sono archiviati i dati o da cui vengono condivisi.
- **Contrassegni visivi**, ad esempio intestazioni, piè di pagina o filigrane.
- **Metadati**, aggiunti a file e intestazioni di posta elettronica in testo non crittografato. I metadati come testo non crittografato consentono ad altri servizi di identificare la classificazione e adottare le misure appropriate.

Nell'immagine seguente, ad esempio, l'assegnazione di etichette ha classificato un messaggio di posta elettronica come *generale*:

:::image type="content" source="media/example-email-footerv2.png" alt-text="Piè di pagina e intestazioni del messaggio di posta elettronica di esempio che mostrano la classificazione di Azure Information Protection":::

In questo esempio, l'etichetta:

- **Aggiunta di un piè di pagina di *Sensitivity: generale* al messaggio di posta elettronica**. Il piè di pagina è un indicatore visivo che segnala a tutti i destinatari che il messaggio è previsto per dati aziendali generici che non devono essere inviati fuori dall'organizzazione.
- **Metadati incorporati nelle intestazioni del messaggio di posta elettronica**. I dati dell'intestazione consentono ai servizi di posta elettronica di ispezionare l'etichetta e, in teoria, di creare una voce di controllo o impedirne l'invio all'esterno dell'organizzazione.

Le etichette possono essere applicate automaticamente dagli amministratori usando regole e condizioni, manualmente dagli utenti o usando una combinazione in cui gli amministratori definiscono le raccomandazioni visualizzate agli utenti.

## <a name="how-aip-protects-your-data"></a>Protezione dei dati con AIP

Azure Information Protection usa il [*servizio Azure Rights Management* (Azure RMS)](what-is-azure-rms.md) per proteggere i dati. 

Azure RMS è integrato con altri servizi e applicazioni cloud Microsoft, ad esempio Office 365 e Azure Active Directory, e può essere usato anche con soluzioni di protezione delle informazioni e delle applicazioni personalizzate o di terze parti. Azure RMS funziona con soluzioni sia locali che cloud.

Azure RMS usa crittografia, identità e criteri di autorizzazione. Analogamente alle etichette AIP, la protezione applicata con Azure RMS rimane con i documenti e i messaggi di posta elettronica, indipendentemente dalla posizione del documento o del messaggio di posta elettronica, assicurando di mantenere il controllo del contenuto anche quando viene condiviso con altri utenti.

Le impostazioni di protezione possono essere:

- **Parte della configurazione dell'etichetta**, per consentire agli utenti di classificare e proteggere i documenti e i messaggi di posta elettronica semplicemente applicando un'etichetta. 
- **Usati autonomamente** dalle applicazioni e dai servizi che supportano la protezione senza etichettare. 

    Per le applicazioni e i servizi che supportano solo la protezione, le impostazioni di protezione vengono usate come [modelli di Rights Management](#rights-management-templates).

È possibile, ad esempio, configurare un report o un foglio di calcolo di previsione delle vendite in modo che sia accessibile solo per gli utenti dell'organizzazione. In questo caso, è necessario applicare le impostazioni di protezione per controllare se il documento può essere modificato, limitarlo alla sola lettura o impedire che venga stampato.

I messaggi di posta elettronica possono avere impostazioni di protezione simili per impedirne l'inoltro o l'uso dell'opzione Rispondi a tutti.

### <a name="rights-management-templates"></a>Modelli di Rights Management

Non appena viene attivato il servizio Azure Rights Management, sono disponibili due modelli di Rights Management predefiniti che limitano l'accesso ai dati agli utenti all'interno dell'organizzazione. Usare immediatamente questi modelli o configurare le proprie impostazioni di protezione per applicare controlli più restrittivi in nuovi modelli.

I modelli di Rights Management possono essere usati con qualsiasi applicazione o servizio che supporta Azure Rights Management.

L'immagine seguente mostra un esempio dall'interfaccia di amministrazione di Exchange, in cui è possibile configurare le regole del flusso di posta elettronica di Exchange Online per l'uso dei modelli di RMS:

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="Esempio di selezione di modelli per Exchange Online":::

> [!NOTE]
> La creazione di un'etichetta AIP che include le impostazioni di protezione crea anche un modello di Rights Management corrispondente che può essere usato separatamente dall'etichetta. 
>  

Per altre informazioni, vedere [Informazioni su Microsoft Azure Rights Management](what-is-azure-rms.md).

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>AIP e integrazione dell'utente finale per documenti e messaggi di posta elettronica

Il client AIP installa la barra di Information Protection per le applicazioni di Office e consente agli utenti finali di integrare AIP nei documenti e nei messaggi di posta elettronica.

Ad esempio, in Excel:

![Esempio di barra di Azure Information Protection in Excel](./media/excelproplus-infoprotect-bar.png)

Sebbene le etichette possano essere applicate automaticamente ai documenti e ai messaggi di posta elettronica, per evitare dubbi agli utenti o per conformarsi ai criteri di un'organizzazione, la barra di Information Protection consente agli utenti finali di selezionare le etichette e applicare la classificazione autonomamente.

Inoltre, il client AIP consente agli utenti di classificare e proteggere altri tipi di file o più file contemporaneamente, usando il menu di scelta rapida da Esplora file di Windows. Ad esempio:

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection":::

L'opzione di menu **Classifica e proteggi** funziona in modo analogo alla barra di Information Protection nelle applicazioni di Office, consentendo agli utenti di selezionare un'etichetta o impostare autorizzazioni personalizzate.

> [!TIP]
> Gli utenti esperti o gli amministratori potrebbero trovare più comodi i comandi di PowerShell per gestire e impostare la classificazione e la protezione per più file. I [comandi di PowerShell pertinenti](https://docs.microsoft.com/powershell/module/azureinformationprotection) sono inclusi nel client e possono anche essere installati separatamente.

Gli utenti e gli amministratori possono usare siti di rilevamento dei documenti per monitorare i documenti protetti, controllare chi vi accede e quando. Se sospettano un uso improprio, possono anche revocare l'accesso ai documenti. Ad esempio:

![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Integrazione aggiuntiva per la posta elettronica

L'uso di AIP con Exchange Online offre l'ulteriore vantaggio di poter inviare messaggi di posta elettronica protetti a tutti gli utenti, con la certezza che possano leggerli in qualsiasi dispositivo.

Ad esempio, potrebbe essere necessario inviare informazioni riservate agli indirizzi di posta elettronica personali che usano un account **Gmail**, **Hotmail** o **Microsoft** o a utenti che non hanno un account in Office 365 o Azure AD. Questi messaggi di posta elettronica deve essere crittografati sia nella posizione di archiviazione che in transito e devono essere letti solo dai destinatari originali.

Questo scenario richiede le [funzionalità di Crittografia messaggi di Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Se i destinatari non sono in grado di aprire il messaggio di posta elettronica protetto nel client di posta elettronica predefinito, possono usare un unico codice per leggere le informazioni riservate in un browser.

Ad esempio, un utente di Gmail potrebbe visualizzare la richiesta seguente in un messaggio di posta elettronica ricevuto:

:::image type="content" source="media/ome-message.png" alt-text="Esperienza per i destinatari Gmail per Crittografia messaggi di Office 365 e Azure Information Protection":::

Per l'utente che invia il messaggio di posta elettronica, le azioni necessarie sono le stesse per l'invio di un messaggio di posta elettronica protetto a un utente nella propria organizzazione. Ad esempio, selezionare il pulsante **Non inoltrare** che il client AIP può aggiungere alla barra multifunzione di Outlook. 

In alternativa, la funzionalità **non inoltrare** può essere integrata in un'etichetta che gli utenti possono selezionare per applicare la classificazione e la protezione al messaggio di posta elettronica. Ad esempio:

![Selezione di un'etichetta configurata per Non inoltrare](./media/recipients-only-label2.png)

Gli amministratori possono anche fornire automaticamente protezione per gli utenti configurando regole del flusso di posta che applicano la protezione dei diritti.

Vengono protetti automaticamente anche tutti i documenti di Office allegati a questi messaggi di posta elettronica.

## <a name="scanning-for-existing-content-to-classify-and-protect"></a>Ricerca del contenuto esistente da classificare e proteggere

Idealmente, i documenti e i messaggi di posta elettronica vengono etichettati al momento della creazione. È tuttavia probabile che esistano già molti documenti negli archivi locali o nel cloud e che si vogliano classificare e proteggere anche questi documenti.

Per classificare e proteggere il contenuto esistente, usare uno dei metodi seguenti:

- **Archiviazione locale**: usare lo [scanner di Azure Information Protection](deploy-aip-scanner.md) per individuare, classificare e proteggere i documenti nelle condivisioni di rete e in siti e raccolte di Microsoft SharePoint Server.

    Lo scanner viene eseguito come servizio in Windows Server e usa le stesse regole dei criteri per rilevare le informazioni riservate e applicare etichette specifiche ai documenti. 

    In alternativa, usare lo scanner per applicare un'etichetta predefinita a tutti i documenti in un archivio dati senza esaminare il contenuto dei file. Usare lo scanner in modalità solo report, per individuare informazioni sensibili che potrebbero non essere note.

- **Archiviazione dei dati nel cloud**: usare [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/azip-integration) per applicare le etichette ai documenti in Box, SharePoint e OneDrive. Per un'esercitazione, vedere [Applicare automaticamente etichette di classificazione di Azure Information Protection](https://docs.microsoft.com/cloud-app-security/use-case-information-protection) 


## <a name="next-steps"></a>Passaggi successivi

Configurare e visualizzare Azure Information Protection per se stessi con la Guida introduttiva e le esercitazioni:

- [Avvio rapido: Distribuire il client di etichettatura unificata](quickstart-deploy-client.md)
- [Esercitazione: Installazione dello scanner di etichettatura unificata di Azure Information Protection (AIP)](tutorial-install-scanner.md)
- [Esercitazione: Ricerca del contenuto sensibile con lo scanner di Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Esercitazione: Prevenzione dell'oversharing in Outlook con Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)

Se invece si è pronti a distribuire il servizio nella propria organizzazione, vedere le [guide con le procedure](how-to-guides.md).
