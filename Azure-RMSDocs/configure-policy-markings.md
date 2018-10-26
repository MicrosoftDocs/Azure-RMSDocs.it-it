---
title: Configurare i contrassegni visivi per un'etichetta di Azure Information Protection
description: Quando si assegna un'etichetta a un documento o a un messaggio di posta elettronica, è possibile selezionare diverse opzioni per rendere facilmente visibile la classificazione scelta. Questi contrassegni visivi sono un'intestazione, un piè di pagina e una filigrana.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/16/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: dbc63a0ddca9e7583693219103268048b524121c
ms.sourcegitcommit: 6a732226a3c97fc06fcf815fbbb24a2e2faae209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358976"
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Come configurare un'etichetta per i contrassegni visivi per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Quando si assegna un'etichetta a un documento o a un messaggio di posta elettronica, è possibile selezionare diverse opzioni per rendere facilmente visibile la classificazione scelta. Questi contrassegni visivi sono un'intestazione, un piè di pagina e una filigrana.

Altre informazioni su questi contrassegni visivi:

- Intestazioni e piè di pagina si applicano a Word, Excel, PowerPoint e Outlook.

- Le filigrane si applicano a Word, Excel e PowerPoint:

    - Excel: le filigrane sono visibili solo nelle modalità Layout di pagina e Anteprima di stampa, oltre che sulla stampa.
    
    - PowerPoint: le filigrane vengono applicate alla diapositiva master, come immagine di sfondo. Nella scheda **Visualizza**, **Schema diapositiva**, assicurarsi che la casella di controllo **Nascondi grafica di sfondo** non sia selezionata.
    
    - Sono supportate più righe di testo.

- Lunghezze massime delle stringhe:
    
    - La lunghezza massima della stringa che è possibile immettere per le intestazioni e i piè di pagina è 1024 caratteri. Excel ha tuttavia un limite totale di 255 caratteri per le intestazioni e i piè di pagina. Quando si immette una stringa lunga per le intestazioni e i piè di pagina, in Excel questo testo può essere troncato a 255 caratteri o meno.
    
    - La lunghezza massima della stringa delle filigrane che è possibile immettere è di 255 caratteri.

- È possibile specificare una stringa di testo o usare [variabili](#using-variables-in-the-text-string) per creare dinamicamente la stringa di testo quando viene applicata l'intestazione, il piè di pagina o la filigrana.

- Word, PowerPoint e Outlook, supportano i contrassegni visivi in colori diversi. I contrassegni visivi configurati a colori vengono sempre visualizzati in nero in Excel.

- I contrassegni visivi supportano una sola lingua.

## <a name="when-visual-markings-are-applied"></a>Quando vengono applicati i contrassegni visivi

Per i messaggi di posta elettronica, i contrassegni visivi vengono applicati quando il messaggio viene inviato da Outlook.

Per i documenti, i contrassegni visivi vengono applicati come segue:

- In un'app di Office, i contrassegni visivi da un'etichetta vengono applicati insieme a quest'ultima. Vengono inoltre applicati quando un documento con etichetta viene aperto e quindi salvato per la prima volta.  

- Quando a un documento viene applicata un'etichetta usando Esplora file, PowerShell o lo scanner di Azure Information Protection, i contrassegni visivi non vengono applicati subito, ma vengono applicati dal client di Azure Information Protection quando tale documento viene aperto in un'app di Office e salvato per la prima volta.
    
    L'eccezione è l'uso del [salvataggio automatico](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5) con Office 2016 per i file salvati in SharePoint Online, OneDrive o OneDrive for Business: quando il salvataggio automatico è attivato, i contrassegni visivi non vengono applicati, a meno che non si configuri l'[impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) per attivare la classificazione per l'esecuzione continua in background. 

## <a name="to-configure-visual-markings-for-a-label"></a>Per configurare i contrassegni visivi per un'etichetta

Seguire le istruzioni seguenti per configurare i contrassegni visivi per un'etichetta.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Classificazioni** > **Etichette**: nel pannello **Azure Information Protection - Etichette** selezionare l'etichetta che contiene i contrassegni visivi da aggiungere o modificare.

3. Nel pannello **Etichetta**, nella sezione **Configurare il contrassegno visivo (ad esempio intestazione o piè di pagina)**, configurare le impostazioni per i contrassegni visivi desiderati e quindi fare clic su **Salva**:
    
    - Per configurare un'intestazione: per **I documenti con questa etichetta includono un'intestazione** selezionare **Sì** se si vuole usare un'intestazione, altrimenti **No**. Se si seleziona **Sì** specificare il testo, le dimensioni, il [carattere](#setting-the-font-name), il [colore](#setting-the-font-color) e l'allineamento per l'intestazione.
    
    - Per configurare un piè di pagina: per **I documenti con questa etichetta includono un piè di pagina** selezionare **Sì** se si vuole usare un piè di pagina, altrimenti **No**. Se si seleziona **Sì** specificare il testo, le dimensioni, il [carattere](#setting-the-font-name), il [colore](#setting-the-font-color) e l'allineamento per il piè di pagina.
    
    - Per configurare una filigrana: per **Documents with this label have a watermark** (I documenti con questa etichetta hanno una filigrana) selezionare **Sì** se si vuole usare una filigrana, altrimenti **No**. Se si seleziona **Sì** specificare il testo, le dimensioni, il [carattere](#setting-the-font-name), il [colore](#setting-the-font-color) e l'allineamento per la filigrana.
    
Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.


## <a name="using-variables-in-the-text-string"></a>Uso di variabili nella stringa di testo

Nella stringa di testo è possibile usare le variabili seguenti per l'intestazione, il piè di pagina o la filigrana:

- `${Item.Label}` per l'etichetta selezionata. Ad esempio: interno

- `${Item.Name}` per l'oggetto del messaggio di posta elettronica o il nome di file. Ad esempio: JulySales.docx

- `${Item.Location}` per il percorso e il nome di file dei documenti e l'oggetto per i messaggi di posta elettronica. Ad esempio: \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` per il proprietario del documento o del messaggio di posta elettronica, in base al nome utente connesso a Windows. Ad esempio: rsimone

- `${User.PrincipalName}` per il proprietario del documento o del messaggio di posta elettronica, in base all'indirizzo di posta elettronica connesso al client di Azure Information Protection (UPN). ad esempio rsimone@vanarsdelltd.com

- `${Event.DateTime}` per la data e l'ora in cui è stata impostata l'etichetta selezionata. Ad esempio: 16/8/2016 13:30

Esempio: se si specifica la stringa `Document: ${item.name}  Classification: ${item.label}` per il piè di pagina dell'etichetta **General**, il testo del piè di pagina applicato a un documento denominato project.docx sarà **Document: project.docx  Classification: General** (Documento: project.docx Classificazione: Generale).

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>Impostazione di contrassegni visivi diversi per Word, Excel, PowerPoint e Outlook

Per impostazione predefinita, i contrassegni visivi specificati vengono applicati a Word, Excel, PowerPoint e Outlook. Tuttavia, è possibile specificare i contrassegni visivi per tipo di applicazione di Office quando si usa un'istruzione con variabile "If.App" nella stringa di testo e identificare il tipo di applicazione usando i valori **Word**, **Excel**, **PowerPoint**, o **Outlook**. È anche possibile abbreviare questi valori, operazione necessaria se si desidera specificarne più di uno nella stessa istruzione If.App.

Usare la sintassi seguente:

    ${If.App.<application type>}<your visual markings text> ${If.End}

La distinzione in questa istruzione supporta la distinzione tra maiuscole e minuscole.

Esempi:

- **Impostare il testo dell'intestazione solo per i documenti di Word:**
    
    `${If.App.Word}This Word document is sensitive ${If.End}`
    
    Solo nelle intestazioni dei documenti di Word, l'etichetta applica il testo dell'intestazione "Questo documento di Word è sensibile". Non viene applicato alcun testo dell'intestazione ad altre applicazioni di Office.

- **Impostare il testo a piè di pagina per Word, Excel e Outlook e testo a piè di pagina diverso per PowerPoint:**
    
    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`
    
    In Word, Excel e Outlook, l'etichetta applica il testo a piè di pagina "Questo contenuto è riservato". In PowerPoint,l'etichetta applica il testo a piè di pagina "Questa presentazione è riservata".

- **Impostare il testo della filigrana specifico per Word e PowerPoint e quindi il testo della filigrana per Word, Excel e PowerPoint:**
    
    `${If.App.WP}This content is ${If.End}Confidential`
    
    In Word e Power Point l'etichetta applica il testo della filigrana "Questo contenuto è riservato". In Excel, l'etichetta applica il testo della filigrana "Riservato". In Outlook, l'etichetta non ha alcun testo della filigrana perché le filigrane come contrassegni visivi non sono supportate per Outlook.

### <a name="setting-the-font-name"></a>Impostazione del nome del tipo di carattere

Il tipo di carattere predefinito per le intestazioni, i piè di pagina e il testo della filigrana è Calibri. Se si specifica il nome di un tipo di carattere alternativo, verificare che sia disponibile nei dispositivi client che applicheranno i contrassegni visivi. 

Se il tipo di carattere specificato non è disponibile, il client torna a usare il tipo di carattere Calibri.

### <a name="setting-the-font-color"></a>Impostazione del colore del carattere

È possibile scegliere un colore nell'elenco dei colori disponibile o specificare un colore personalizzato immettendo un codice tripletta esadecimale per i componenti rosso, verde e blu (RGB) del colore. Ad esempio, **#DAA520**. 

Se sono necessarie informazioni di riferimento per questi codici, un punto di partenza utile può essere [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx) (Colori per nome) nella documentazione MSDN. È anche possibile trovare i codici in molte applicazioni per la modifica di immagini. Ad esempio quando in Microsoft Paint si sceglie un colore personalizzato in una tavolozza vengono visualizzati automaticamente i valori RGB corrispondenti ed è possibile copiarli.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

