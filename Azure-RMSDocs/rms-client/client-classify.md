---
title: Classificazione-Azure Information Protection client classico
description: Istruzioni su come classificare i documenti e i messaggi di posta elettronica quando si usa il client di Azure Information Protection classico per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/09/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d65c7690-fab7-4823-845c-8c73903e9c79
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 9d2930b7cc5ed01ecb97a59247f0082900d1a606
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164165"
---
# <a name="user-guide-classify-a-file-or-email-with-the-azure-information-protection-classic-client"></a>Guida dell'utente: classificare un file o un messaggio di posta elettronica con il client classico Azure Information Protection

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere la guida per l' [utente del client Unified Labeling](clientv2-classify.md). *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

> [!TIP]
> Usare queste istruzioni per classificare senza proteggere i documenti e i messaggi di posta elettronica. Se è necessario proteggere i documenti e i messaggi di posta elettronica, vedere le [istruzioni per classificare e proteggere](client-classify-protect.md). Se non si sa quali istruzioni usare, rivolgersi al proprio amministratore o al supporto tecnico.

È più semplice classificare i documenti e i messaggi di posta elettronica durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è anche possibile classificare i file usando **Esplora file**. Questo metodo supporta altri tipi di file ed è un modo pratico per classificare più file contemporaneamente. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Uso delle app di Office per classificare documenti e messaggi di posta elettronica

Usare la barra di Azure Information Protection e selezionare una delle etichette configurate. 

L'immagine seguente mostra ad esempio che il documento non è ancora stato etichettato perché il valore di **Sensibilità** è **Non impostato**. Per impostare un'etichetta, ad esempio "Generale", fare clic su **Generale**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla. 

![Esempio della barra di Azure Information Protection](../media/info-protect-bar-not-set-callout.png)

Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se le etichette non sono visualizzate sulla barra, fare prima clic sull'icona **Modifica l'etichetta** accanto al valore corrente dell'etichetta.

> [!TIP]
> È inoltre possibile selezionare le etichette dal pulsante **Proteggi** nella scheda **File**.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore ha configurato indicazioni per la selezione di un'etichetta specifica quando vengono rilevati dati sensibili. È possibile accettare il suggerimento (l'etichetta viene applicata) o rifiutarlo (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Eccezioni per la barra di Azure Information Protection 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>La barra di Information Protection non viene visualizzata nelle app di Office?

- È possibile che il client Azure Information Protection non sia [installato](install-client-app.md).

- Il client è installato, ma l'amministratore ha configurato un'impostazione per non visualizzare la barra. In alternativa, selezionare le etichette dal pulsante **Proteggi** nella scheda **File** sulla barra multifunzione di Office. 

##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>Sulla barra non è visualizzata un'etichetta che ci si aspetterebbe di vedere? 

- Se l'amministratore ha configurato di recente una nuova etichetta, provare a chiudere tutte le istanze dell'app di Office e riaprirle. In questo modo, verrà eseguito un controllo della presenza di modifiche alle etichette.

- L'etichetta potrebbe essere in un criterio con ambito che non include l'account in uso. Rivolgersi all'help desk o all'amministratore.


## <a name="using-file-explorer-to-classify-files"></a>Uso di Esplora file per classificare i file

Quando si usa Esplora file, è possibile classificare rapidamente un singolo file, più file o una cartella. 

Quando si seleziona una cartella, tutti i file nella cartella e tutte le relative sottocartelle vengono selezionate automaticamente per la classificazione impostata. Tuttavia, i nuovi file creati nella cartella o nelle sottocartelle non vengono classificati automaticamente.

Quando si usa Esplora file per classificare i file, se una o più etichette vengono visualizzate in grigio, i file selezionati non supportano la classificazione senza protezione.

La guida dell'amministratore include l'elenco completo dei tipi di file che supportano la classificazione senza protezione: [Tipi di file supportati solo per la classificazione](client-admin-guide-file-types.md#file-types-supported-for-classification-only).

### <a name="to-classify-a-file-by-using-file-explorer"></a>Per classificare un file mediante Esplora file

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**. Ad esempio:
    
    ![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** usare le etichette in modo analogo a un'applicazione di Office che consente di impostare la classificazione definita dall'amministratore. 
    
    Se non è possibile selezionare alcuna etichetta (sono tutte visualizzate in grigio) significa che il file selezionato non supporta la classificazione. Ad esempio:
    
    ![Nessuna etichetta disponibile nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/info-protect-dialog-labels-dimmed.png)

3. Se è stato selezionato un file non supporta la classificazione, fare clic su **Chiudi**. Non è possibile classificare il file senza proteggerlo.
    
    Se è stata selezionata un'etichetta, fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Se si vuole cambiare selezionare un'altra etichetta, ripetere la procedura e scegliere un'etichetta diversa.

La classificazione specificata rimane associata al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. 
## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Vedere [Configurazione dei criteri di Azure Information Protection](../configure-policy.md).

