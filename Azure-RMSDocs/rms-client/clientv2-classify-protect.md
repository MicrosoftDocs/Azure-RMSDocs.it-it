---
title: Classificare e proteggere tramite il client di assegnazione di etichette unificato di Azure Information Protection per Windows
description: Istruzioni classificare e proteggere documenti e messaggi di posta elettronica quando si usa Azure Information Protection client per l'assegnazione di etichette per Windows unificata.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 0404acb6f79100a78d955a94f67ea0a0a7aaf604
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181387"
---
# <a name="user-guide-classify-and-protect-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>Manuale dell'utente: Classificare e proteggere un file o un messaggio di posta elettronica usando il client di assegnazione di etichette unificato di Azure Information Protection per Windows

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Usare queste istruzioni per classificare e proteggere i documenti e i messaggi di posta elettronica. Se è necessario solo classificare i documenti e i messaggi di posta elettronica senza proteggerli, vedere le [istruzioni per la sola classificazione](clientv2-classify.md). Se non si sa quali istruzioni usare, rivolgersi al proprio amministratore o al supporto tecnico.

Il momento migliore per classificare e proteggere i documenti e i messaggi di posta elettronica è durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è anche possibile classificare e proteggere i file tramite **Esplora file**. Questo metodo supporta altri tipi di file ed è un modo pratico per classificare e proteggere più file contemporaneamente. Questo metodo supporta la protezione di documenti di Office, file PDF, file di testo e immagine e un'ampia gamma di altri file. 

Se l'etichetta applica la protezione, un documento protetto non è adatto per essere salvato in OneDrive o SharePoint. Questi percorsi non supportano quanto segue per i file protetti: creazione condivisa, Office Online, ricerca, anteprima di documenti e video ed eDiscovery.

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Condividere in modo sicuro un file con utenti esterni all'organizzazione

I file protetti possono essere condivisi con altri utenti in tutta sicurezza. Ad esempio, è possibile allegare un documento protetto a un messaggio di posta elettronica.

Prima di condividere file con utenti esterni all'organizzazione, rivolgersi all'help desk o all'amministratore per informazioni su come proteggere i file per gli utenti esterni.

Se, ad esempio, l'organizzazione comunica regolarmente con utenti di un'altra organizzazione, l'amministratore potrebbe avere configurato etichette che impostano la protezione, in modo da consentire a questi utenti la lettura e l'uso dei documenti protetti. Selezionare quindi le etichette per classificare e proteggere i documenti da condividere.

In alternativa, se gli utenti esterni [gli account di business-to-business (B2B)](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) creato per essi, è possibile usare [Esplora File per impostare le autorizzazioni personalizzate](#using-file-explorer-to-classify-and-protect-files) per un documento prima di condividerlo. Se si impostano autorizzazioni personalizzate e il documento è già protetto per l'uso interno, eseguirne prima una copia per mantenere le autorizzazioni originali. Usare quindi la copia per impostare le autorizzazioni personalizzate.


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso delle app di Office per classificare e proteggere documenti e messaggi di posta elettronica

Dal **Home** scheda, seleziona la **sensibilità** nella barra multifunzione e quindi selezionare una delle etichette che è stato configurato per l'utente. Ad esempio:

![Esempio di pulsante di sensibilità](../media/sensitivity-not-set-callout.png)

Oppure, se si è scelto **Mostra barra** dal **sensibilità** pulsante, è possibile selezionare un'etichetta dalla barra di Azure Information Protection. Ad esempio: 

![Esempio della barra di Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Per impostare un'etichetta, ad esempio "**Confidential** \ **tutti i dipendenti**", selezionare **Confidential** e quindi **tutti i dipendenti**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla. Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se è stato visualizzato la barra Azure Information Protection e le etichette non vengono visualizzate sulla barra per poter selezionare, fare clic il **modifica l'etichetta** sull'icona accanto al valore di etichetta corrente.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore configurato etichette impostato automaticamente quando viene rilevate le informazioni riservate.

- L'amministratore ha configurato consigliato etichette quando viene rilevate le informazioni riservate e viene richiesto di accettare il suggerimento (e viene applicata l'etichetta), o rifiutarlo (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-sensitivity-button"></a>Eccezioni per il pulsante di sensibilità

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Il pulsante tra maiuscole e minuscole nelle app di Office non è visualizzato?

- Il client di assegnazione di etichette unificato di Azure Information Protection non si dispone [installato](install-unifiedlabelingclient-app.md).

- Se non viene visualizzata una **sensibilità** nella barra multifunzione, ma viene visualizzato un **Proteggi** pulsante invece con le etichette, aver installato il client Azure Information Protection e non di Azure Information Protection client unificato di assegnazione di etichette. [Altre informazioni](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>Un'etichetta che ci si aspetta di vedere non è visualizzata? 

Motivi possibili:

- Se l'amministratore ha configurato di recente una nuova etichetta, provare a chiudere tutte le istanze dell'app di Office e riaprirle. In questo modo, verrà eseguito un controllo della presenza di modifiche alle etichette.

- Se l'etichetta mancante serve per applicare la protezione, l'edizione di Office in uso potrebbe non supportare l'applicazione della protezione di Rights Management. Per verificare, fare clic su **Proteggi** > **Commenti e suggerimenti**. Controllare se nella sezione **Stato del client** è presente il messaggio **Questo client non ha la licenza per Office Professional Plus.** 
    
    Office Professional Plus non è necessario se sono disponibili app di Office 365 da Office 365 Business o Microsoft 365 Business quando all'utente viene assegnata una licenza per Azure Rights Management (nota anche come Azure Information Protection per Office 365).

- L'etichetta potrebbe essere in un criterio con ambito che non include l'account in uso. Rivolgersi all'help desk o all'amministratore.


### <a name="safely-sharing-by-email"></a>Condivisione sicura tramite posta elettronica

Se si vogliono condividere documenti di Office tramite posta elettronica, è possibile allegare i documenti a messaggi di posta elettronica protetti. In questo modo ogni documento viene protetto automaticamente con le stesse restrizioni applicate al messaggio corrispondente. 

Tuttavia, è possibile proteggere il documento prima di tutto e quindi allegarlo al messaggio di posta elettronica. Proteggere anche il messaggio se quest'ultimo contiene informazioni riservate. Un vantaggio di proteggere il documento prima di allegarlo al messaggio di posta elettronica:

- Possibilità di applicare al documento autorizzazioni diverse da quelle applicate al messaggio di posta elettronica.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Uso di Esplora file per classificare e proteggere file

Quando si usa Esplora file, è possibile classificare e proteggere rapidamente un singolo file, più file o una cartella. 

Quando si seleziona una cartella, tutti i file in tale cartella e tutte le relative sottocartelle vengono selezionate automaticamente per le opzioni di classificazione e protezione impostate. Tuttavia, i nuovi file che vengono creati in tale cartella o nelle sottocartelle non vengono configurati automaticamente con queste opzioni.

Quando si usa Esplora file per classificare e proteggere i file, se una o più etichette vengono visualizzate in grigio, i file selezionati non supportano la classificazione. Per questi file, è possibile selezionare un'etichetta solo se l'amministratore ha configurato l'etichetta in modo da potere applicare la protezione. In alternativa, è possibile specificare le proprie impostazioni di protezione. 

Alcuni file vengono esclusi automaticamente dalla classificazione e dalla protezione, perché la loro modifica potrebbe causare un malfunzionamento del PC. Anche se è possibile selezionare questi file, essi vengono ignorati come una cartella o un file escluso. Ciò accade, ad esempio per i file eseguibili e la cartella Windows.

La guida dell'amministratore contiene un elenco completo dei tipi di file supportati e dei file e delle cartelle che vengono automaticamente esclusi: [Tipi di file supportati dal client Azure Information Protection unified imprevisto delle etichette](clientv2-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Per classificare e proteggere un file mediante Esplora file

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**. Ad esempio: 
    
    ![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** usare le etichette in modo analogo a un'applicazione di Office, che consente di impostare la classificazione e la protezione come definito dall'amministratore. 

   - Se nessuna delle etichette può essere selezionata (sono visualizzate in grigio): il file selezionato non supporta la classificazione, ma è possibile proteggerlo con le autorizzazioni personalizzate (passaggio 3). Ad esempio:

     ![Nessuna etichetta disponibile nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. È possibile specificare le impostazioni di protezione anziché utilizzare le impostazioni di protezione che l'amministratore potrebbe avere incluso con l'etichetta selezionata. A tale scopo, selezionare **Proteggi con autorizzazioni personalizzate**.
    
    Le eventuali autorizzazioni personalizzate specificate sostituiscono le impostazioni di protezione che l'amministratore potrebbe avere definito per l'etichetta scelta e non sono aggiuntive.  

4. Se si seleziona l'opzione per le autorizzazioni personalizzate, specificare le informazioni seguenti:

   - **Selezionare le autorizzazioni**: selezionare il livello di accesso da assegnare agli utenti per la protezione del file o dei file selezionati.
    
   - **Selezionare gli utenti, i gruppi o le organizzazioni**: specificare gli utenti che devono avere le autorizzazioni selezionate per il file o i file. Digitare l'indirizzo di posta elettronica completo di uno o più utenti o di un gruppo oppure il nome di dominio di un'organizzazione per tutti gli utenti dell'organizzazione. 
    
     In alternativa, è possibile usare l'icona a forma di rubrica per selezionare utenti o gruppi dalla Rubrica di Outlook.
        
    - **Scadenza dell'accesso**: Selezionare questa opzione solo per i tempi sono importanti in modo che gli utenti specificati non è possibile aprire il file o i file selezionati dopo una data è impostata. Sarà comunque possibile aprire il file originale, ma dopo la mezzanotte (fuso orario corrente) del giorno impostato, gli utenti specificati non potranno aprire il file.
    
     Si noti che se questa impostazione in precedenza è stata configurata usando le autorizzazioni personalizzate di un'app di Office 2010, la data di scadenza specificata non viene visualizzata in questa finestra di dialogo, ma la data viene comunque impostata. Questo è un problema di visualizzazione che riguarda solo la data di scadenza configurata in Office 2010.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Il file o i file selezionati verranno classificati e protetti in base alle selezioni specificate. In alcuni casi (quando l'aggiunta della protezione modifica l'estensione del nome di file) il file originale in Esplora file viene sostituito con un nuovo file con l'icona di blocco di Azure Information Protection. Ad esempio: 

![File protetto con l'icona di blocco di Azure Information Protection](../media/Pfile.png)

Se si cambia idea sulla classificazione e la protezione o se in seguito è necessario modificare le impostazioni, è sufficiente ripetere questo processo con le nuove impostazioni.

La classificazione e la protezione specificate rimangono associate al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. 

## <a name="other-instructions"></a>Altre istruzioni
Guidano per altre istruzioni sulle procedure da parte dell'utente per client di assegnazione di etichette unificata di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    

Visualizzare [Panoramica di etichette di riservatezza](/Office365/SecurityCompliance/sensitivity-labels).
