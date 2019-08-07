---
title: Procedura&#58; Usare i diritti predefiniti | Azure RMS
description: Descrive i diritti predefiniti specificati da RMS SDK 4.2 e le restrizioni di utilizzo che un'app deve applicare e rispettare.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 83dbafe17b5ef68735b404fdc819f485d8008c7f
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68791242"
---
# <a name="how-to-use-built-in-rights"></a>Come fare per: Usare i diritti predefiniti

Questo argomento descrive i diritti predefiniti specificati da Microsoft Rights Management SDK 4.2 e le restrizioni di utilizzo che un'app deve applicare e rispettare. Il codice seguente illustra i diritti predefiniti, i diritti comuni, i diritti di modifica del documento e i diritti sui messaggi di posta elettronica con la descrizione e il valore derivante dal sistema operativo.

**Nota**: per i dettagli sull'SDK di Linux, vedere file di origine *rights.h*.

## <a name="common-rights"></a>Diritti comuni

**Tutti**: una raccolta di tutti i diritti comuni.
- Android: [CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS e OS X: [MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx) - proprietario utente e visualizzazione per implementare **Tutti**
- Windows Store e Windows Phone: [CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux: [CommonRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Proprietario**: il diritto di proprietario concede il controllo completo sul contenuto protetto.
- Android: [<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS e OS X: [MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store e Windows Phone: [CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux: [CommonRights::Owner](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Visualizza**: il diritto di visualizzare il contenuto protetto. In genere, quando viene concesso, l'applicazione consente all'utente di aprire e visualizzare il contenuto protetto. Tuttavia, per modificare, estrarre, inoltrare o salvare il contenuto sono necessari altri diritti.

- Android: [CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS e OS X: [MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store e Windows Phone: [CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux: [CommonRights::View](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>Diritti di modifica del documento
**Tutti**: una raccolta che contiene tutti i diritti di modifica del documento.
- Android: [EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux: [EditableDocumentRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Commento**: il diritto per creare commenti sul documento.
- Android: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux: [EditableDocumentRights::Comment](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Modifica**: il diritto di modificare il contenuto protetto e salvarlo nell stesso formato protetti. In genere, quando viene concesso, l'applicazione consente all'utente di modificare il contenuto protetto e quindi salvarlo nello stesso file.
- Android: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux: [EditableDocumentRights::Edit](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Esporta**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato diverso protetto da AD RMS. In genere, quando viene concesso, l'applicazione consente all'utente di salvare il contenuto protetto in altri formati protetti da AD RMS; ad esempio, se l'applicazione contiene una funzionalità *Salva con nome*.

- Android: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux: [EditableDocumentRights::Export](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Estrai**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. In genere, quando viene concesso, l'applicazione consente all'utente di copiare e incollare le informazioni dal contenuto protetto. Se l'app contiene una funzionalità <em>Salva con nome</em>, l'applicazione potrebbe anche consentire all'utente di salvare il contenuto protetto in formati non protetti e in altri formati protetti. Questo diritto ha lo stesso valore del diritto Estrai per i messaggi di posta elettronica.

- Android: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux: [EditableDocumentRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Stampa**: il diritto di stampare il contenuto protetto. In genere, quando viene concesso, l'applicazione consente all'utente di stampare il contenuto protetto. Questo diritto ha lo stesso valore del diritto Stampa per i messaggi di posta elettronica.

- Android: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux: [EditableDocumentRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>Diritti sui messaggi di posta elettronica

**Tutti**: una raccolta che contiene tutti i diritti sui messaggi di posta elettronica.
- Android: [EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux: [EmailRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Estrai**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di copiare e incollare le informazioni di un messaggio protetto. Se l'app contiene una funzionalità <em>Salva con nome</em>, l'applicazione potrebbe anche consentire al destinatario di salvare il contenuto protetto in formati non protetti e in altri formati protetti. Questo diritto ha lo stesso valore del diritto Estrai dei documenti modificabili.

- Android: [EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux: [EmailRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Inoltra**: il diritto di inoltrare un messaggio protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di inoltrare un messaggio protetto.
- Android: [<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux: [EmailRights::Forward](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Stampa**: il diritto di stampare il contenuto protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di stampare un messaggio protetto. Questo diritto ha lo stesso valore del diritto Stampa dei documenti modificabili.

- Android: [EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux: [EmailRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Rispondi**: in genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di rispondere a un messaggio protetto e includere una copia del messaggio originale.

- Android: [EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux: [EmailRights::Reply](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Rispondi a tutti**: in genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di rispondere a tutti i destinatari di un messaggio protetto e includere una copia del messaggio originale.

- Android: [EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux: [EmailRights::ReplyAll](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)
