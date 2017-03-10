---
title: Procedura&#58; Usare i diritti predefiniti | Azure RMS
description: Descrive i diritti predefiniti forniti da RMS SDK 4.2 e le restrizioni di utilizzo che un&quot;app deve applicare rispettando tali restrizioni.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: True
experiment_id: priyamo-TableVsFlatList-20160805
ms.openlocfilehash: 1cd9ae9b9051f4ee5e5890ef3f1f0a17958c4b59
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-to-use-built-in-rights"></a>Procedura: Usare i diritti predefiniti

Questo argomento descrive i diritti predefiniti forniti da Microsoft Rights Management SDK 4.2 e le restrizioni di utilizzo che un'app deve applicare rispettando tali restrizioni. Il codice seguente illustra i diritti predefiniti, i diritti comuni, i diritti di modifica del documento e i diritti sui messaggi di posta elettronica con la descrizione e il valore derivante dal sistema operativo.

**Nota**: per i dettagli sull'SDK di Linux, vedere file di origine *rights.h*.

## <a name="common-rights"></a>Diritti comuni

**Tutti**: una raccolta di tutti i diritti comuni.
- Android: [CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS e OS x: [MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx) (proprietario utente e visualizzazione per implementare **Tutti**)
- Windows Store e Windows Phone: [CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux: [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

** Proprietario**: il diritto di proprietario concede il controllo completo sul contenuto protetto.
- Android: [<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS e OS X: [MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store e Windows Phone: [CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux: [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Visualizza**: il diritto di visualizzare il contenuto protetto. In genere, quando viene concesso, l'applicazione consente all'utente di aprire e visualizzare il contenuto protetto. Tuttavia, per modificare, estrarre, inoltrare o salvare il contenuto sono necessari altri diritti.

- Android: [CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS e OS X: [MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store e Windows Phone: [CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux: [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>Diritti di modifica del documento
**Tutti**: una raccolta che contiene tutti i diritti di modifica del documento.
- Android: [EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [CommonRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux: [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Commento**: il diritto per creare commenti sul documento.
- Android: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux: [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Modifica**: il diritto di modificare il contenuto protetto e salvarlo nell stesso formato protetti. In genere, quando viene concesso, l'applicazione consente all'utente di modificare il contenuto protetto e quindi salvarlo nello stesso file.
- Android: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux: [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Esporta**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato diverso protetto da AD RMS. In genere, quando viene concesso, l'applicazione consente all'utente di salvare il contenuto protetto in altri formati protetti da AD RMS; ad esempio, se l'applicazione contiene una funzionalità *Salva con nome*.

- Android: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux: [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Estrai**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. In genere, quando viene concesso, l'applicazione consente all'utente di copiare e incollare le informazioni dal contenuto protetto. Se l'app contiene una funzionalità <em>Salva con nome</em>, l'applicazione potrebbe anche consentire all'utente di salvare il contenuto protetto in formati non protetti e in altri formati protetti. Questo diritto ha lo stesso valore del diritto Estrai per i messaggi di posta elettronica.

- Android: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux: [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Stampa**: il diritto di stampare il contenuto protetto. In genere, quando viene concesso, l'applicazione consente all'utente di stampare il contenuto protetto. Questo diritto ha lo stesso valore del diritto Stampa per i messaggi di posta elettronica.

- Android: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS e OS X: [MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store e Windows Phone: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux: [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>Diritti sui messaggi di posta elettronica

**Tutti**: una raccolta che contiene tutti i diritti sui messaggi di posta elettronica.
- Android: [EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux: [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Estrai**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di copiare e incollare le informazioni di un messaggio protetto. Se l'app contiene una funzionalità <em>Salva con nome</em>, l'applicazione potrebbe anche consentire al destinatario di salvare il contenuto protetto in formati non protetti e in altri formati protetti. Questo diritto ha lo stesso valore del diritto Estrai dei documenti modificabili.

- Android: [EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux: [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Inoltra**: il diritto di inoltrare un messaggio protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di inoltrare un messaggio protetto.
- Android: [<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux: [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Stampa**: il diritto di stampare il contenuto protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di stampare un messaggio protetto. Questo diritto ha lo stesso valore del diritto Stampa dei documenti modificabili.

- Android: [EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux: [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Rispondi**: in genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di rispondere a un messaggio protetto e includere una copia del messaggio originale.

- Android: [EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux: [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Rispondi a tutti**: in genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di rispondere a tutti i destinatari di un messaggio protetto e includere una copia del messaggio originale.

- Android: [EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS e OS X: [MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store e Windows Phone: [EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux: [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]