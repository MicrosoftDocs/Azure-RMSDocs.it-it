---
title: Come configurare un&quot;etichetta per i contrassegni visivi | Azure Information Protection
description: "Quando si assegna un&quot;etichetta a un documento o a un messaggio di posta elettronica, è possibile selezionare diverse opzioni per rendere facilmente visibile la classificazione scelta. Questi contrassegni visivi sono un&quot;intestazione, un piè di pagina e una filigrana."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: d5b3f3fc473661022a4f17b6587d58a252d07d1a
ms.openlocfilehash: eca90185e6225d3f55f979f66f8225d661fe59cd


---

# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Come configurare un'etichetta per i contrassegni visivi per Azure Information Protection

>*Si applica a: Azure Information Protection*

Quando si assegna un'etichetta a un documento o a un messaggio di posta elettronica, è possibile selezionare diverse opzioni per rendere facilmente visibile la classificazione scelta. Questi contrassegni visivi sono un'intestazione, un piè di pagina e una filigrana:

I contrassegni visivi vengono applicati ai documenti di Word, Excel e PowerPoint quando viene applicata l'etichetta e quando viene salvato il documento. Per i messaggi di posta elettronica, i contrassegni visivi vengono applicati all'invio del messaggio.

Altre informazioni su questi contrassegni visivi:

- Intestazioni e piè di pagina si applicano a Word, Excel, PowerPoint e Outlook.

- Le filigrane si applicano a Word, Excel e PowerPoint:

    - Excel: le filigrane sono visibili solo nelle modalità Layout di pagina e Anteprima di stampa, oltre che sulla stampa.

    - PowerPoint: le filigrane vengono applicate alla diapositiva master, come immagine di sfondo.

- È possibile specificare una stringa di testo o usare [variabili](#using-variables-in-the-text-string) per creare dinamicamente la stringa di testo quando viene applicata l'intestazione, il piè di pagina o la filigrana. 

Seguire le istruzioni seguenti per configurare i contrassegni visivi per un'etichetta.

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** selezionare l'etichetta da configurare per i contrassegni visivi.

3. Nel pannello **Etichetta**, nella sezione **Configurare il contrassegno visivo (ad esempio intestazione o piè di pagina)**, configurare le impostazioni per i contrassegni visivi desiderati e quindi fare clic su **Salva**:

    - Per configurare un'intestazione: per **I documenti con questa etichetta includono un'intestazione** selezionare **Sì** se si vuole usare un'intestazione, altrimenti **No**. Se si seleziona **Sì**, specificare il testo, le dimensioni, il colore e l'allineamento per l'intestazione.
    
    - Per configurare un piè di pagina: per **I documenti con questa etichetta includono un piè di pagina** selezionare **Sì** se si vuole usare un piè di pagina, altrimenti **No**. Se si seleziona **Sì**, specificare il testo, le dimensioni, il colore e l'allineamento per il piè di pagina.
    
    - Per configurare una filigrana: per **Documents with this label have a watermark** (I documenti con questa etichetta hanno una filigrana) selezionare **Sì** se si vuole usare una filigrana, altrimenti **No**. Se si seleziona **Sì**, specificare il testo, le dimensioni, il colore e il layout per la filigrana. 

4. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## <a name="using-variables-in-the-text-string"></a>Uso di variabili nella stringa di testo

Nella stringa di testo è possibile usare le variabili seguenti per l'intestazione, il piè di pagina o la filigrana:

- `${Item.Label}` per l'etichetta selezionata. Ad esempio: interno

- `${Item.Name}` per l'oggetto del messaggio di posta elettronica o il nome di file. Ad esempio: JulySales.docx

- `${Item.Location}` per il percorso e il nome di file dei documenti e l'oggetto per i messaggi di posta elettronica. Ad esempio: \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` per il proprietario del documento o del messaggio di posta elettronica, in base al nome utente connesso a Windows. Ad esempio: rsimone

- `${User.PrincipalName}` per il proprietario del documento o del messaggio di posta elettronica, in base all'indirizzo di posta elettronica connesso al client di Azure Information Protection (UPN). ad esempio rsimone@vanarsdelltd.com

- `${Event.DateTime}` per la data e l'ora in cui è stata impostata l'etichetta selezionata. Ad esempio: 16/8/2016 13:30
    
Esempio: se si specifica la stringa `Document: ${item.name}  Classification: ${item.label}` per il piè di pagina dell'etichetta Secret (Segreto), il testo del piè di pagina applicato a un documento denominato project.docx sarà **Documento: project.docx Classificazione: Secret (Segreto)**.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  





<!--HONumber=Nov16_HO1-->


