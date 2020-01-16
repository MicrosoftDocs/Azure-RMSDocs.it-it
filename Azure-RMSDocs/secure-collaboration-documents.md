---
title: Configurazione della collaborazione per i documenti protetti con Azure Information Protection
description: Flusso di lavoro end-to-end per collaborare a documenti protetti da Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4895c429-959f-47c7-9007-b8f032f6df6f
ms.subservice: aiplabels
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 90c49b8222e379094ee5f5d00c5bd37c7dd0377d
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "75960891"
---
# <a name="configuring-secure-document-collaboration-by-using-azure-information-protection"></a>Configurazione della collaborazione per i documenti protetti con Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Quando si usa Azure Information Protection, è possibile proteggere i documenti senza sacrificare la collaborazione per gli utenti autorizzati. La maggior parte dei documenti creati da un utente e quindi condivisi con altri per la visualizzazione e la modifica è costituita da documenti di Office Word, Excel e PowerPoint. Questi documenti supportano la protezione nativa, ovvero oltre alle funzionalità di protezione di autorizzazione e crittografia, supportano anche l'autorizzazione limitata per un controllo più granulare. 

Queste autorizzazioni sono denominate anche diritti di utilizzo e includono autorizzazioni come visualizzazione, modifica e stampa. È possibile definire singoli diritti di utilizzo quando un documento è protetto oppure è possibile definire un gruppo di diritti di utilizzo, denominato livello di autorizzazione. I livelli di autorizzazione semplificano la selezione dei diritti di utilizzo usati in genere insieme, ad esempio i diritti Revisore e Coautore. Per ulteriori informazioni sui diritti di utilizzo e sui livelli di autorizzazione, vedere [Configuring Usage Rights for Azure Information Protection](configure-usage-rights.md).

Quando si configurano queste autorizzazioni, è possibile specificare gli utenti cui sono destinate:

- **Per gli utenti nella stessa organizzazione o in una organizzazione diversa che usa Azure Active Directory**: è possibile specificare account utente Azure AD, gruppi Azure AD o tutti gli utenti nell'organizzazione. 

- **Per gli utenti che non hanno un account Azure Active Directory**: specificare un indirizzo di posta elettronica che verrà usato con un account Microsoft. Questo account può esistere già oppure gli utenti possono crearlo quando aprono il documento protetto. 
    
    Per aprire documenti con un account Microsoft, gli utenti devono usare app di Office 365 (A portata di clic). Le altre edizioni e versioni di Office non supportano ancora l'apertura di documenti protetti di Office con un account Microsoft.

- **Per gli utenti autenticati**: questa opzione è adatta quando non è necessario controllare chi accede al documento protetto, purché l'utente possa essere autenticato. L'autenticazione può essere eseguita da Azure AD, usando un account Microsoft, o anche da un provider di servizi di social networking federato o una passcode monouso quando il contenuto viene protetto dalle nuove funzionalità di Office 365 Message Encryption. 

Un amministratore può configurare un'etichetta di Azure Information Protection per applicare le autorizzazioni e gli utenti autorizzati. Questa configurazione semplifica notevolmente per gli utenti e altri amministratori l'applicazione delle corrette impostazioni di protezione, perché possono applicare semplicemente l'etichetta senza dover specificare alcun dettaglio. Le sezioni seguenti forniscono un esempio di procedura dettagliata per proteggere un documento che supporta la collaborazione sicura con utenti interni ed esterni.


## <a name="example-configuration-for-a-label-to-apply-protection-to-support-internal-and-external-collaboration"></a>Configurazione di esempio per un'etichetta per l'applicazione della protezione in modo da supportare la collaborazione interna ed esterna


Questo esempio descrive in modo dettagliato la configurazione di un'etichetta esistente per applicare la protezione in modo che gli utenti dell'organizzazione possano collaborare a documenti con tutti gli utenti di un'altra organizzazione che usa Office 365 o Azure AD, con un gruppo di un'organizzazione diversa che usa Office 365 o Azure AD e con un utente che non ha un account in Azure AD e che usa invece il proprio indirizzo di posta elettronica Gmail.

Poiché lo scenario limita l'accesso a specifici utenti, non include l'impostazione per tutti gli utenti autenticati. Per un esempio di configurazione di un'etichetta con questa impostazione, vedere [Esempio 5: Etichetta che crittografa il contenuto, ma non limita chi può accedervi](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it).  

1. Selezionare l'etichetta già inclusa nei criteri globali o in criteri con ambito. Nel riquadro **Protezione** verificare che sia selezionata l'opzione **Azure (chiave cloud)** .
    
2. Verificare che sia selezionata l'opzione **Configura le autorizzazioni** e fare clic su **Aggiungi autorizzazioni**.

3. Nel riquadro **Aggiungi autorizzazioni**: 
    
   - Per il gruppo interno: selezionare **Cerca nella directory** per selezionare il gruppo, che deve essere abilitato per la posta elettronica.
    
   - Per tutti gli utenti nella prima organizzazione esterna: selezionare **Immettere i dettagli** e digitare il nome di un dominio nel tenant dell'organizzazione. Ad esempio, fabrikam.com.
    
   - Per il gruppo nella seconda organizzazione esterna: sempre nella scheda **Immettere i dettagli**, digitare l'indirizzo di posta elettronica del gruppo nel tenant dell'organizzazione. Ad esempio, sales@contoso.com
    
   - Per l'utente che non ha un account Azure AD: sempre nella scheda **Immettere i dettagli**, digitare l'indirizzo di posta elettronica dell'utente. Ad esempio, bengi.turan@gmail.com 

4. Per concedere le stesse autorizzazioni a tutti questi utenti: per **Scegliere le autorizzazioni dai valori preimpostati** selezionare **Comproprietario**, **Coautore**, **Revisore** o **Personalizzate** per selezionare le autorizzazioni che si vuole concedere.
    
    Ad esempio, le autorizzazioni configurate possono essere simili alle seguenti:
        
    ![Configurazione delle autorizzazioni per la collaborazione sicura](./media/collaboration-permissions.png)

5. Fare clic su **OK** nel riquadro **Aggiungi autorizzazioni**.

6. Nel riquadro **protezione** fare clic su **OK**.

7. Nel riquadro **Etichetta** selezionare **Salva**. 

## <a name="applying-the-label-that-supports-secure-collaboration"></a>Applicazione dell'etichetta che supporta la collaborazione sicura

Dopo aver configurato l'etichetta, questa può essere applicata ai documenti in diversi modi, tra cui i seguenti:

|Metodi diversi per l'applicazione dell'etichetta|Altre informazioni|
|---------------|----------|
|Un utente seleziona manualmente l'etichetta quando il documento viene creato nell'applicazione di Office.|Gli utenti selezionano l'etichetta tramite il pulsante **Proteggi** sulla barra multifunzione di Office oppure sulla barra di Azure Information Protection.|
|Agli utenti viene richiesto di selezionare un'etichetta quando viene salvato un nuovo documento.|È stata configurata l'[impostazione di criteri](configure-policy-settings.md) di Azure Information Protection denominata **All documents and emails must have a label** (Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta).|
|Un utente condivide il documento tramite posta elettronica e seleziona manualmente l'etichetta in Outlook.|Gli utenti selezionano l'etichetta tramite il pulsante **Proteggi** sulla barra multifunzione di Office o sulla barra di Azure Information Protection e il documento allegato viene automaticamente protetto con le stesse impostazioni.|
|Un amministratore applica l'etichetta al documento usando PowerShell.|Usare il cmdlet [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) per applicare l'etichetta a un documento specifico o a tutti i documenti in una cartella.|
|L'etichetta è stata configurata anche per applicare la classificazione automatica, che può ora essere applicata tramite lo scanner di Azure Information Protection o PowerShell.|Vedere [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md).|

Per completare questa procedura dettagliata, applicare manualmente l'etichetta quando si crea il documento nell'applicazione di Office: 

1. In un computer client, se l'applicazione di Office è già aperta, chiuderla e riaprirla per ottenere le ultime modifiche dei criteri che includono la nuova etichetta configurata. 

2. Applicare l'etichetta a un documento e quindi salvare il documento.

Condividere il documento protetto allegandolo a un messaggio di posta elettronica e inviarlo alle persone che sono state autorizzate a modificarlo.

## <a name="opening-and-editing-the-protected-document"></a>Apertura e modifica del documento protetto

Quando gli utenti autorizzati aprono il documento per la modifica, il documento viene aperto con un banner informativo che indica che le autorizzazioni sono limitate. Ad esempio:

![Banner informativo di esempio sulle autorizzazioni di Azure Information Protection](./media/example-restricted-access-banner.png)

Se gli utenti selezionano il pulsante **Visualizza autorizzazioni**, potranno visualizzare le informazioni loro assegnate. Nell'esempio seguente l'utente può visualizzare e modificare il documento:

![Finestra di dialogo di esempio delle autorizzazioni di Azure Information Protection](./media/example-permisisons-popup.png)

Nota: se il documento viene aperto da utenti esterni che usano anche Azure Information Protection, l'applicazione Office non visualizza l'etichetta di classificazione per il documento, anche se rimangono i contrassegni visivi dall'etichetta. Gli utenti esterni possono invece applicare la propria etichetta in linea con la tassonomia di classificazione dell'organizzazione. Se questi utenti esterni inviano quindi nuovamente il documento modificato all'utente, Office visualizza l'etichetta di classificazione originale quando si riapre il documento.

Prima dell'apertura del documento protetto, viene avviato uno dei flussi di autenticazione seguenti:

- Gli utenti che hanno un account Azure AD usano le proprie credenziali per essere autenticati da Azure AD e quindi il documento viene aperto. 

- Gli utenti che non hanno un account Azure AD e non hanno effettuato l'accesso a Office con un account che ha le autorizzazioni necessarie per aprire il documento visualizzeranno la pagina **Account**. 
    
   Nella pagina **Account** selezionare **Aggiungi account**:
   
    ![Aggiunta di un account Microsoft per aprire il documento protetto](./media/add-account-msa.png)

   Nella pagina **Accedi** selezionare **Creane uno** e seguire le indicazioni per creare un nuovo account Microsoft con l'indirizzo di posta elettronica usato per concedere le autorizzazioni:
    
    ![Creazione di un account Microsoft per aprire il documento protetto](./media/create-account-msa.png)
    
    Quando viene creato il nuovo account Microsoft, l'account locale passa a questo nuovo account Microsoft e l'utente può quindi aprire il documento.


### <a name="supported-scenarios-for-opening-protected-documents"></a>Scenari supportati per l'apertura di documenti protetti

La tabella seguente offre un riepilogo dei diversi metodi di autenticazione supportati per la visualizzazione e la modifica di documenti protetti.

Anche gli scenari seguenti supportano la visualizzazione di documenti:

- Il visualizzatore Azure Information Protection per Windows e per iOS e Android può aprire file tramite un account Microsoft. 

- Un browser può aprire gli allegati protetti quando vengono usati i provider di servizi di social networking e le passcode monouso per l'autenticazione con Exchange Online e le nuove funzionalità di Office 365 Message Encryption. 

|Piattaforme per la visualizzazione e la modifica di documenti: <br />Word, Excel, PowerPoint|Metodo di autenticazione:<br />Azure AD|Metodo di autenticazione:<br />Account Microsoft|
|---------------|----------|-----------|-----------|
|Windows|Sì [[1]](#footnote-1)|Sì [[2]](#footnote-2)|
|iOS|Sì [[1]](#footnote-1)|No|
|Android|Sì [[1]](#footnote-1)|No|
|MacOS|Sì [[1]](#footnote-1)|No|

###### <a name="footnote-1"></a>Nota 1
Supporta account utente, gruppi abilitati per la posta elettronica e tutti i membri. Gli account utente e i gruppi abilitati per la posta elettronica possono includere account guest. Da tutti i membri sono esclusi gli account guest.

###### <a name="footnote-2"></a>Nota 2
Attualmente supportato solo da app di Office 365 (A portata di clic).




## <a name="next-steps"></a>Passaggi successivi

Vedere altre [configurazioni di esempio](configure-policy-protection.md#example-configurations) per informazioni sulle etichette per l'applicazione della protezione per alcuni scenari comuni. Questo articolo contiene altre informazioni sulle impostazioni di protezione.

Per maggiori informazioni sulle altre opzioni e impostazioni che è possibile configurare per l'etichetta, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md). 

L'etichetta configurata in questo articolo crea anche un modello di protezione dallo stesso nome. Se sono presenti applicazioni e servizi che si integrano con modelli di protezione di Azure Information Protection, possono applicare questo modello. Ad esempio, le soluzioni DLP e le regole di flusso di posta. Outlook sul Web visualizza automaticamente i modelli di protezione dai criteri globali di Azure Information Protection. 




