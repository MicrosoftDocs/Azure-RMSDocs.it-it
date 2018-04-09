---
title: Classificare e proteggere file e messaggi di posta elettronica tramite Azure Information Protection
description: Istruzioni su come classificare e proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/29/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 0d5f4e081ea68f3e8c9ddcb46409370b486f6210
ms.sourcegitcommit: d1987b1abb65f3466bbbb8f8c28e30668d629e50
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2018
---
# <a name="user-guide-classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Guida dell'utente: Classificare e proteggere un file o un messaggio di posta elettronica tramite Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

> [!NOTE]
> Usare queste istruzioni per classificare e proteggere i documenti e i messaggi di posta elettronica. Se è necessario solo classificare i documenti e i messaggi di posta elettronica senza proteggerli, vedere le [istruzioni per la sola classificazione](client-classify.md). Se non si sa quali istruzioni usare, rivolgersi al proprio amministratore o al supporto tecnico.

Il modo più semplice per classificare e proteggere i documenti e i messaggi di posta elettronica è durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è anche possibile classificare e proteggere i file tramite **Esplora file**. Questo metodo supporta altri tipi di file ed è un modo pratico per classificare e proteggere più file contemporaneamente. Questo metodo supporta la protezione di documenti di Office, file PDF, file di testo e immagine e un'ampia gamma di altri file. 

Se l'etichetta applica la protezione, un documento protetto non è adatto per essere salvato in OneDrive o SharePoint. Questi percorsi non supportano le operazioni seguenti per i file protetti: Creazione condivisa, Office Online, ricerca, anteprima di documenti, anteprima di video ed eDiscovery. 

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Condividere in modo sicuro un file con utenti esterni all'organizzazione

I file protetti possono essere condivisi con altri utenti in tutta sicurezza. Ad esempio, allegare il file a un messaggio di posta elettronica.

Se si condividono regolarmente file con utenti esterni all'organizzazione, l'amministratore potrebbe avere configurato un'etichetta che imposta la protezione in modo da consentire la lettura ai destinatari desiderati. In alternativa, prima di condividere un file è possibile usare l'[app di Office](#set-custom-permissions-for-a-document) o [Esplora file](#using-file-explorer-to-classify-and-protect-files) per impostare autorizzazioni personalizzate per tale file. Se si impostano autorizzazioni personalizzate e il file è già protetto per uso interno, eseguirne prima una copia per mantenere le autorizzazioni originali. Usare quindi la copia per impostare le autorizzazioni personalizzate.  

Quando il file è protetto con le autorizzazioni personalizzate, usare il meccanismo di condivisione standard per condividerlo. Se le persone con cui si condivide il file ricevono un file protetto per la prima volta, potrebbe essere necessario fornire loro le istruzioni per visualizzarlo. A tale scopo, è possibile copiare e incollare il messaggio seguente: **Questo file è protetto con Microsoft Azure Information Protection. In caso di primo utilizzo, vedere queste [istruzioni](https://aka.ms/rms-signup).**

## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso delle app di Office per classificare e proteggere documenti e messaggi di posta elettronica

Usare la barra di Azure Information Protection o il pulsante **Proteggi** sulla barra multifunzione per selezionare una delle etichette configurate. 

L'immagine seguente mostra ad esempio che il documento non è ancora stato etichettato perché il valore di **Sensibilità** è **Non impostato** sulla barra di Azure Information Protection. Per impostare un'etichetta, ad esempio "Generale", fare clic su **Generale**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla. 

![Esempio della barra di Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se le etichette non sono visualizzate sulla barra, fare prima clic sull'icona **Modifica l'etichetta** accanto al valore corrente dell'etichetta.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore ha configurato indicazioni per la selezione di un'etichetta specifica quando vengono rilevati dati sensibili. È possibile accettare il suggerimento (l'etichetta viene applicata) o rifiutarlo (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Eccezioni per la barra di Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>La barra di Information Protection non viene visualizzata nelle app di Office?

Motivi possibili:

- Il client Azure Information Protection non è [installato](install-client-app.md).

- Il client è installato, ma l'amministratore ha configurato un'impostazione per non visualizzare la barra. In alternativa, selezionare le etichette dal pulsante **Proteggi** nella scheda **File** sulla barra multifunzione di Office. 

- Il client è in esecuzione in [modalità di sola protezione](client-protection-only-mode.md).
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>Un'etichetta che ci si aspetta di vedere non è visualizzata? 

Motivi possibili:

- Se l'amministratore ha configurato di recente una nuova etichetta, provare a chiudere tutte le istanze dell'app di Office e riaprirle. In questo modo, verrà eseguito un controllo della presenza di modifiche alle etichette.

- Se l'etichetta mancante serve per applicare la protezione, l'edizione di Office in uso potrebbe non supportare l'applicazione della protezione di Rights Management. Per verificare, fare clic su **Proteggi** > **Commenti e suggerimenti**. Controllare se nella sezione **Stato del client** è presente il messaggio **Questo client non ha la licenza per Office Professional Plus.** 

- L'etichetta potrebbe essere in un criterio con ambito che non include l'account in uso. Rivolgersi all'help desk o all'amministratore.

### <a name="set-custom-permissions-for-a-document"></a>Impostare autorizzazioni personalizzate per un documento

Se consentito dall'amministratore, è possibile specificare impostazioni di protezione personalizzate per i documenti anziché usare quelle eventualmente incluse dall'amministratore con l'etichetta selezionata. Questa opzione è specifica per i documenti e non è disponibile con Outlook.

1. Nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Autorizzazioni personalizzate**:

    ![Opzione Autorizzazioni personalizzate](../media/custom-permissions-callout.png)
    
    Se non è possibile selezionare **Autorizzazioni personalizzate**, l'amministratore non consente l'uso di questa opzione.
    
    Si noti che le autorizzazioni personalizzate specificate non vengono aggiunte ma sono usate in sostituzione delle eventuali impostazioni di protezione definite dall'amministratore per l'etichetta scelta.  

2. Nella finestra di dialogo **Microsoft Azure Information Protection** specificare quanto segue:

    - **Proteggi con autorizzazioni personalizzate**: assicurarsi che questa opzione sia selezionata in modo da poter specificare e applicare le autorizzazioni personalizzate. Deselezionare questa opzione per rimuovere le eventuali autorizzazioni personalizzate.
    
    - **Selezionare le autorizzazioni**: se si vuole proteggere il file in modo da ottenere l'accesso esclusivo, selezionare **Solo per l'utente**. In caso contrario, selezionare il livello di accesso che dovrà essere assegnato agli utenti.
    
    - **Selezionare gli utenti, i gruppi o le organizzazioni**: specificare gli utenti che devono avere le autorizzazioni selezionate per uno o più file. Digitare l'indirizzo di posta elettronica completo di uno o più utenti o di un gruppo oppure il nome di dominio di un'organizzazione per tutti gli utenti dell'organizzazione. Si noti che gli indirizzi di posta elettronica personali non sono attualmente supportati.
        
        Se si dispone della versione di anteprima corrente del client, è anche possibile usare l'icona a forma di rubrica per selezionare utenti o gruppi dalla Rubrica di Outlook.
    
    - **Scadenza dell'accesso**: selezionare questa opzione solo per i file per cui il fattore tempo è importante in modo tale che gli utenti specificati non potranno aprire il file o i file selezionati dopo una data impostata. Sarà comunque possibile aprire il file originale, ma dopo la mezzanotte (fuso orario corrente) del giorno impostato, gli utenti specificati non potranno aprire il file.

5. Fare clic su **Applica** e attendere che venga visualizzato il messaggio **Le autorizzazioni personalizzate sono state applicate**. e quindi fare clic su **Chiudi**.

### <a name="safely-sharing-by-email"></a>Condivisione sicura tramite posta elettronica

Se si vogliono condividere documenti di Office tramite posta elettronica, è possibile allegare i documenti a messaggi di posta elettronica protetti. In questo modo ogni documento viene protetto automaticamente con le stesse restrizioni applicate al messaggio corrispondente. 

È tuttavia consigliabile prima proteggere il documento e quindi allegarlo al messaggio di posta elettronica. Proteggere anche il messaggio se quest'ultimo contiene informazioni riservate. Proteggere il documento prima di allegarlo a un messaggio di posta elettronica garantisce i due vantaggi seguenti:

- Possibilità di tenere traccia e, se necessario, di revocare il documento dopo che è stato inviato.

- Possibilità di applicare al documento autorizzazioni diverse da quelle applicate al messaggio di posta elettronica.

## <a name="using-file-explorer-to-classify-and-protect-files"></a>Uso di Esplora file per classificare e proteggere file

Quando si usa Esplora file, è possibile classificare e proteggere rapidamente un singolo file, più file o una cartella. 

Quando si seleziona una cartella, tutti i file in tale cartella e tutte le relative sottocartelle vengono selezionate automaticamente per le opzioni di classificazione e protezione impostate. Tuttavia, i nuovi file che vengono creati in tale cartella o nelle sottocartelle non vengono configurati automaticamente con queste opzioni.

Quando si usa Esplora file per classificare e proteggere i file, se una o più etichette vengono visualizzate in grigio, i file selezionati non supportano la classificazione. Per questi file, è possibile selezionare un'etichetta solo se l'amministratore ha configurato l'etichetta in modo da potere applicare la protezione. In alternativa, è possibile specificare le proprie impostazioni di protezione. 

Alcuni file vengono esclusi automaticamente dalla classificazione e dalla protezione, perché la loro modifica potrebbe causare un malfunzionamento del PC. Anche se è possibile selezionare questi file, essi vengono ignorati come una cartella o un file escluso. Ciò accade, ad esempio per i file eseguibili e la cartella Windows.

La guida dell'amministratore contiene un elenco completo dei tipi di file supportati e dei file e delle cartelle che vengono automaticamente esclusi: [Tipi di file supportati dal client Azure Information Protection](client-admin-guide-file-types.md).


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Per classificare e proteggere un file mediante Esplora file

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**. Ad esempio:
    
    ![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** usare le etichette in modo analogo a un'applicazione di Office, che consente di impostare la classificazione e la protezione come definito dall'amministratore. 

    - Se non è possibile selezionare alcuna etichetta (sono tutte visualizzate in grigio): il file selezionato non supporta la classificazione, ma è possibile proteggerlo con le autorizzazioni personalizzate (passaggio 3). Ad esempio:

    ![Nessuna etichetta disponibile nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)
    
    - Se le etichette non sono visualizzate, ma nella finestra di dialogo è presente l'opzione **Protezione predefinita dell'azienda**: il client è in esecuzione in [modalità di sola protezione](client-protection-only-mode.md). Selezionare un modello per applicare la protezione configurata dall'amministratore oppure selezionare **Autorizzazioni personalizzate** per specificare le impostazioni di protezione e andare al passaggio 4.
    
    ![Nessuna etichetta nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/info-protect-dialog-labels-protection-only.png)
    
3. Se consentito dall'amministratore, è possibile specificare impostazioni di protezione personalizzate anziché usare quelle eventualmente incluse dall'amministratore con l'etichetta selezionata. A tale scopo, selezionare **Proteggi con autorizzazioni personalizzate**.
    
    Se non è possibile selezionare **Proteggi con autorizzazioni personalizzate**, l'amministratore non consente l'uso di questa opzione.
    
    Le eventuali autorizzazioni personalizzate specificate sostituiscono le impostazioni di protezione che l'amministratore potrebbe avere definito per l'etichetta scelta e non sono aggiuntive.  

4. Se si seleziona l'opzione per le autorizzazioni personalizzate, specificare le informazioni seguenti:

    - **Selezionare le autorizzazioni**: selezionare il livello di accesso da assegnare agli utenti per la protezione del file o dei file selezionati.
    
    - **Selezionare gli utenti, i gruppi o le organizzazioni**: specificare gli utenti che devono avere le autorizzazioni selezionate per uno o più file. Digitare l'indirizzo di posta elettronica completo di uno o più utenti o di un gruppo oppure il nome di dominio di un'organizzazione per tutti gli utenti dell'organizzazione. Si noti che gli indirizzi di posta elettronica personali non sono attualmente supportati.
    
    In alternativa, è possibile usare l'icona a forma di rubrica per selezionare utenti o gruppi dalla Rubrica di Outlook.
        
    - **Scadenza dell'accesso**: selezionare questa opzione solo per i file per cui il fattore tempo è importante in modo tale che gli utenti specificati non siano in grado di aprire il file o i file selezionati dopo una data specificata. Sarà comunque possibile aprire il file originale, ma dopo la mezzanotte (fuso orario corrente) del giorno impostato gli utenti specificati non saranno in grado di aprire il file.
    
    Si noti che se questa impostazione in precedenza è stata configurata usando le autorizzazioni personalizzate di un'app di Office 2010, la data di scadenza specificata non viene visualizzata in questa finestra di dialogo, ma la data viene comunque impostata. Questo è un problema di visualizzazione che riguarda solo la data di scadenza configurata in Office 2010.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Il file o i file selezionati verranno classificati e protetti in base alle selezioni specificate. In alcuni casi (quando l'aggiunta della protezione modifica l'estensione del nome di file) il file originale in Esplora file viene sostituito con un nuovo file con l'icona di blocco di Azure Information Protection. Ad esempio:

![File protetto con l'icona di blocco di Azure Information Protection](../media/Pfile.png)

Se si cambia idea sulla classificazione e la protezione o se in seguito è necessario modificare le impostazioni, è sufficiente ripetere questo processo con le nuove impostazioni.

La classificazione e la protezione specificate rimangono associate al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. Se si protegge il file, è possibile tenere traccia del modo in cui gli utenti lo usano e se necessario revocarne l'accesso. Per altre informazioni, vedere [Tenere traccia dei documenti protetti e revocarli quando si usa Azure Information Protection](client-track-revoke.md). 


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Vedere [Configurazione dei criteri di Azure Information Protection](../deploy-use/configure-policy.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
