---
title: Classificare e proteggere tramite Azure Information Protection
description: Istruzioni su come classificare e proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 3db62d81976267155764abf7e45598628259710d
ms.lasthandoff: 02/24/2017


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Classificare e proteggere un file o un messaggio di posta elettronica tramite Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Il modo più semplice per classificare e proteggere i documenti e i messaggi di posta elettronica è durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è possibile classificare e proteggere i file tramite **Esplora file**, che supporta altri tipi di file e consente di classificare e proteggere più file contemporaneamente. Questo metodo supporta la protezione di documenti di Office, file PDF, file di testo e immagine e un'ampia gamma di altri file. 

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>Condividere in modo sicuro un file con utenti esterni all'organizzazione

I file protetti possono essere condivisi con altri utenti in tutta sicurezza. È ad esempio possibile allegare il file a un messaggio di posta elettronica o inviare un invito dal sito di SharePoint.

Se si condividono regolarmente file con utenti esterni all'organizzazione, l'amministratore potrebbe avere configurato un'etichetta che imposta la protezione in modo da consentire la lettura ai destinatari desiderati. In alternativa, è possibile usare [Esplora file per impostare autorizzazioni personalizzate](#using-file-explorer-to-classify-and-protect-files) per un file prima di condividerlo. 

Se si impostano autorizzazioni personalizzate e il file è già protetto per uso interno, effettuare prima una copia. Usare la copia per impostare le autorizzazioni personalizzate.  

Quando il file è protetto con le autorizzazioni personalizzate, usare il meccanismo di condivisione standard per condividerlo. Se le persone con cui si condivide il file ricevono un file protetto per la prima volta, potrebbe essere necessario fornire loro le istruzioni per visualizzarlo. A tale scopo, è possibile copiare e incollare il messaggio seguente: **Questo file è protetto con Microsoft Azure Information Protection. In caso di primo utilizzo, vedere queste [istruzioni](https://aka.ms/rms-signup).**


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Uso delle app di Office per classificare e proteggere documenti e messaggi di posta elettronica

Usare la barra di Azure Information Protection e selezionare una delle etichette configurate. 

L'immagine seguente mostra ad esempio che il documento non è ancora stato etichettato perché il valore di **Sensibilità** è **Non impostato**. Per impostare un'etichetta, ad esempio "Interno", fare clic su **Interno**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla.

![Esempio della barra di Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se le etichette non sono visualizzate sulla barra, fare prima clic sull'icona **Modifica l'etichetta** accanto al valore corrente dell'etichetta.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore ha configurato indicazioni per la selezione di un'etichetta specifica quando vengono rilevati dati sensibili. È possibile accettare il suggerimento (l'etichetta viene applicata) o rifiutarlo (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Eccezioni per la barra di Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>La barra di Information Protection non viene visualizzata nelle app di Office?

- Il client Azure Information Protection potrebbe non essere [installato](install-client-app.md) oppure potrebbe essere in esecuzione in [modalità di sola protezione](client-protection-only-mode.md).
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>Sulla barra non è visualizzata un'etichetta che ci si aspetterebbe di vedere? 

- Se l'amministratore ha configurato di recente una nuova etichetta, provare a chiudere tutte le istanze dell'app di Office e riaprirle. In questo modo, verrà eseguito un controllo della presenza di modifiche alle etichette.

- Se l'etichetta mancante serve per applicare la protezione, l'edizione di Office in uso potrebbe non supportare l'applicazione della protezione di Rights Management. Per verificare, fare clic su **Proteggi** > **Guida e commenti** e controllare se nella sezione **Stato del client** è presente il messaggio **Questo client non ha la licenza per Office Professional Plus**. 

- L'etichetta potrebbe essere in un criterio con ambito che non include l'account in uso. Rivolgersi all'help desk o all'amministratore.

### <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Tasti di scelta rapida per la barra di Azure Information Protection

Per accedere alla barra di Azure Information Protection tramite i tasti di scelta rapida, usare la combinazione di tasti seguente:

- Premere **CTRL** + **MAIUSC** + **~** 

Usare quindi TAB per passare tra le etichette e altri controlli sulla barra (le icone **Nascondi le etichette** e **Elimina l'etichetta**) e INVIO per selezionarle.

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
    
3. Per specificare impostazioni di protezione personalizzate invece di usare quelle eventualmente incluse dall'amministratore con l'etichetta selezionata, selezionare **Proteggi con autorizzazioni personalizzate**.
    
    Le eventuali autorizzazioni personalizzate specificate sostituiscono le impostazioni di protezione che l'amministratore potrebbe avere definito per l'etichetta scelta e non sono aggiuntive.  

4. Se si seleziona l'opzione per le autorizzazioni personalizzate, specificare le informazioni seguenti:

    - **Selezionare le autorizzazioni**: selezionare il livello di accesso da assegnare agli utenti per la protezione del file o dei file selezionati.
    
    - **Selezionare gli utenti**: specificare gli utenti che devono avere le autorizzazioni selezionate per il file o i file. Per gli utenti e i gruppi all'interno dell'organizzazione è possibile usare la Rubrica per cercarli e selezionarli. Per gli utenti di un'altra organizzazione è necessario specificare l'indirizzo di posta elettronica completo. Assicurarsi di usare un indirizzo di posta elettronica aziendale perché gli indirizzi di posta elettronica personali non sono attualmente supportati.
        
    - **Scadenza dell'accesso**: selezionare questa opzione solo per i file per cui il fattore tempo è importante in modo tale che gli utenti specificati non potranno aprire il file o i file selezionati dopo una data specificata. Sarà comunque possibile aprire il file originale, ma dopo la mezzanotte (fuso orario corrente) del giorno selezionato, gli utenti specificati non potranno aprire il file.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Il file o i file selezionati verranno classificati e protetti in base alle selezioni specificate. In alcuni casi (quando l'aggiunta della protezione modifica l'estensione del nome di file) il file originale in Esplora file viene sostituito con un nuovo file con l'icona di blocco di Azure Information Protection. Ad esempio:

![File protetto con l'icona di blocco di Azure Information Protection](../media/Pfile.png)

Se si cambia idea sulla classificazione e la protezione o se in seguito è necessario modificare le impostazioni, è sufficiente ripetere questo processo con le nuove impostazioni.

La classificazione e la protezione specificate rimangono associate al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. Se si protegge il file, è possibile tenere traccia del modo in cui gli utenti lo usano e se necessario revocarne l'accesso. Per altre informazioni, vedere [Tenere traccia dei documenti protetti e revocarli quando si usa Azure Information Protection](client-track-revoke.md). 


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

