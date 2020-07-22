---
title: Classificazione & proteggere-Azure Information Protection client di etichetta unificata
description: Istruzioni per la classificazione e la protezione di documenti e messaggi di posta elettronica quando si usa il client di etichettatura unificato di Azure Information Protection per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/20/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 5da4eca4af78083c1b5090f6621706e91d4a1680
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927761"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-unified-labeling-client"></a>Guida dell'utente: classificare e proteggere con la Azure Information Protection Unified Labeling client

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
> **I clienti con supporto Microsoft esteso per Windows 7 e Office 2010 possono anche ottenere supporto Azure Information Protection per queste versioni. Per i dettagli completi, rivolgersi al contatto di supporto.*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> Usare queste istruzioni per classificare e proteggere i documenti e i messaggi di posta elettronica. Se è necessario solo classificare i documenti e i messaggi di posta elettronica senza proteggerli, vedere le [istruzioni per la sola classificazione](clientv2-classify.md). Se non si sa quali istruzioni usare, rivolgersi al proprio amministratore o al supporto tecnico.

Il modo più semplice per classificare e proteggere i documenti e i messaggi di posta elettronica è durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è anche possibile classificare e proteggere i file tramite **Esplora file**. Questo metodo supporta altri tipi di file ed è un modo pratico per classificare e proteggere più file contemporaneamente. Questo metodo supporta la protezione di documenti di Office, file PDF, file di testo e immagine e un'ampia gamma di altri file. 

Se l'etichetta applica la protezione a un documento, il documento protetto potrebbe non essere adatto per essere salvato in SharePoint o in OneDrive. Controllare se l'amministratore ha [abilitato le etichette di riservatezza per i file di Office in SharePoint e OneDrive](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Condividere in modo sicuro un file con utenti esterni all'organizzazione

I file protetti possono essere condivisi con altri utenti in tutta sicurezza. Ad esempio, è possibile allegare un documento protetto a un messaggio di posta elettronica.

Prima di condividere file con utenti esterni all'organizzazione, rivolgersi all'help desk o all'amministratore per informazioni su come proteggere i file per gli utenti esterni.

Se, ad esempio, l'organizzazione comunica regolarmente con utenti di un'altra organizzazione, l'amministratore potrebbe avere configurato etichette che impostano la protezione, in modo da consentire a questi utenti la lettura e l'uso dei documenti protetti. Selezionare quindi le etichette per classificare e proteggere i documenti da condividere.

In alternativa, se per gli utenti esterni sono stati creati [account business-to-business (B2B)](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b) , è possibile usare [Esplora file per impostare le autorizzazioni personalizzate](#using-file-explorer-to-classify-and-protect-files) per un documento prima di condividerlo. Se si impostano autorizzazioni personalizzate e il documento è già protetto per l'uso interno, eseguirne prima una copia per mantenere le autorizzazioni originali. Usare quindi la copia per impostare le autorizzazioni personalizzate.


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso delle app di Office per classificare e proteggere documenti e messaggi di posta elettronica

Nella scheda **Home** selezionare il pulsante **sensibilità** sulla barra multifunzione e quindi selezionare una delle etichette configurate. Ad esempio:

![Esempio di pulsante Sensitivity](../media/sensitivity-not-set-callout.png)

In alternativa, se è stata selezionata l'opzione **Mostra barra** dal pulsante **sensibilità** , è possibile selezionare un'etichetta dalla barra Azure Information Protection. Ad esempio:

![Esempio della barra di Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Per impostare un'etichetta, ad esempio "**Confidential**  \  **All Employees**", selezionare **Confidential** e quindi **All Employees**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla.

Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se è stata visualizzata la barra di Azure Information Protection e le etichette non sono visualizzate sulla barra da selezionare, fare prima clic sull'icona **Modifica etichetta** accanto al valore etichetta corrente.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore ha configurato le etichette da impostare automaticamente quando vengono rilevate informazioni riservate.

- L'amministratore ha configurato le etichette consigliate quando vengono rilevate informazioni riservate e viene richiesto di accettare la raccomandazione (e l'etichetta viene applicata) o di rifiutarla (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-sensitivity-button"></a>Eccezioni per il pulsante Sensitivity

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Non viene visualizzato il pulsante Sensitivity nelle app di Office?

- Potrebbe non essere [installato](install-unifiedlabelingclient-app.md)il client di Azure Information Protection Unified labeling.

- Se non viene visualizzato un pulsante di **riservatezza** sulla barra multifunzione, ma viene visualizzato un pulsante **Proteggi** con etichette, è necessario che sia installato il client di Azure Information Protection (versione classica) e non il Azure Information Protection client di etichetta unificata. [Altre informazioni](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>Un'etichetta che ci si aspetta di vedere non è visualizzata? 

Motivi possibili:

- Se l'amministratore ha configurato di recente una nuova etichetta, provare a chiudere tutte le istanze dell'app di Office e riaprirle. In questo modo, verrà eseguito un controllo della presenza di modifiche alle etichette.

- Se l'etichetta mancante serve per applicare la protezione, l'edizione di Office in uso potrebbe non supportare l'applicazione della protezione di Rights Management. Per verificare, fare clic su Guida **sensibile**  >  **e commenti e suggerimenti**. Controllare se nella sezione **Stato del client** è presente il messaggio **Questo client non ha la licenza per Office Professional Plus.** 
    
    Office Professional Plus non è necessario se si dispone di app di Office da [Microsoft 365 app for business](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename) quando all'utente viene assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365).

- L'etichetta potrebbe essere in un criterio con ambito che non include l'account in uso. Rivolgersi all'help desk o all'amministratore.


### <a name="safely-sharing-by-email"></a>Condivisione sicura tramite posta elettronica

Se si vogliono condividere documenti di Office tramite posta elettronica, è possibile allegare i documenti a messaggi di posta elettronica protetti. In questo modo ogni documento viene protetto automaticamente con le stesse restrizioni applicate al messaggio corrispondente. 

Tuttavia, potrebbe essere necessario proteggere prima il documento e quindi collegarlo al messaggio di posta elettronica. Proteggere anche il messaggio se quest'ultimo contiene informazioni riservate. Un vantaggio della protezione del documento prima di collegarlo a un messaggio di posta elettronica è che è possibile applicare autorizzazioni diverse al documento anziché al messaggio di posta elettronica.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Uso di Esplora file per classificare e proteggere file

Quando si usa Esplora file, è possibile classificare e proteggere rapidamente un singolo file, più file o una cartella. 

Quando si seleziona una cartella, tutti i file in tale cartella e tutte le relative sottocartelle vengono selezionate automaticamente per le opzioni di classificazione e protezione impostate. Tuttavia, i nuovi file che vengono creati in tale cartella o nelle sottocartelle non vengono configurati automaticamente con queste opzioni.

Quando si usa Esplora file per classificare e proteggere i file, se una o più etichette vengono visualizzate in grigio, i file selezionati non supportano la classificazione. Per questi file, è possibile selezionare un'etichetta solo se l'amministratore ha configurato l'etichetta in modo da potere applicare la protezione. In alternativa, è possibile specificare le proprie impostazioni di protezione. 

Alcuni file vengono esclusi automaticamente dalla classificazione e dalla protezione, perché la loro modifica potrebbe causare un malfunzionamento del PC. Anche se è possibile selezionare questi file, essi vengono ignorati come una cartella o un file escluso. Ciò accade, ad esempio per i file eseguibili e la cartella Windows.

La guida dell'amministratore contiene un elenco completo dei tipi di file supportati e dei file e delle cartelle esclusi automaticamente: [tipi di file supportati dal client di Azure Information Protection Unified Labeling](clientv2-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Per classificare e proteggere un file mediante Esplora file

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**. Ad esempio:
    
    ![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** usare le etichette in modo analogo a un'applicazione di Office, che consente di impostare la classificazione e la protezione come definito dall'amministratore. 

   - Se non è possibile selezionare alcuna etichetta (sono tutte visualizzate in grigio): il file selezionato non supporta la classificazione, ma è possibile proteggerlo con le autorizzazioni personalizzate (passaggio 3). Ad esempio:

     ![Nessuna etichetta disponibile nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. È possibile specificare le proprie impostazioni di protezione anziché usare le impostazioni di protezione che l'amministratore potrebbe avere incluso nell'etichetta selezionata. A tale scopo, selezionare **Proteggi con autorizzazioni personalizzate**.
    
    Le eventuali autorizzazioni personalizzate specificate sostituiscono le impostazioni di protezione che l'amministratore potrebbe avere definito per l'etichetta scelta e non sono aggiuntive.  

4. Se si seleziona l'opzione per le autorizzazioni personalizzate, specificare le informazioni seguenti:

   - **Selezionare le autorizzazioni**: selezionare il livello di accesso da assegnare agli utenti per la protezione del file o dei file selezionati.
    
   - **Selezionare gli utenti, i gruppi o le organizzazioni**: specificare gli utenti che devono avere le autorizzazioni selezionate per uno o più file. Digitare l'indirizzo di posta elettronica completo di uno o più utenti o di un gruppo oppure il nome di dominio di un'organizzazione per tutti gli utenti dell'organizzazione. 
    
     In alternativa, è possibile usare l'icona a forma di rubrica per selezionare utenti o gruppi dalla Rubrica di Outlook.
        
    - **Scadenza dell'accesso**: selezionare questa opzione solo per i file sensibili al tempo, in modo che gli utenti specificati non possano aprire il file o i file selezionati dopo una data impostata. Sarà comunque possibile aprire il file originale, ma dopo la mezzanotte (fuso orario corrente) del giorno impostato, gli utenti specificati non potranno aprire il file.
    
     Si noti che se questa impostazione in precedenza è stata configurata usando le autorizzazioni personalizzate di un'app di Office 2010, la data di scadenza specificata non viene visualizzata in questa finestra di dialogo, ma la data viene comunque impostata. Questo è un problema di visualizzazione che riguarda solo la data di scadenza configurata in Office 2010.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Il file o i file selezionati verranno classificati e protetti in base alle selezioni specificate. In alcuni casi (quando l'aggiunta della protezione modifica l'estensione del nome di file) il file originale in Esplora file viene sostituito con un nuovo file con l'icona di blocco di Azure Information Protection. Ad esempio:

![File protetto con l'icona di blocco di Azure Information Protection](../media/Pfile.png)

Se si cambia idea sulla classificazione e la protezione o se in seguito è necessario modificare le impostazioni, è sufficiente ripetere questo processo con le nuove impostazioni.

La classificazione e la protezione specificate rimangono associate al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. 

## <a name="other-instructions"></a>Altre istruzioni
Ulteriori istruzioni sulle procedure sono disponibili nel manuale dell'utente per Azure Information Protection client di etichetta unificata:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    

Vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels).
