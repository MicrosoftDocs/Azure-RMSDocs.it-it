---
title: Procedura&#58; Usare i diritti predefiniti | Azure RMS
description: Descrive i diritti predefiniti forniti da RMS SDK 4.2 e le restrizioni di utilizzo che un'app deve applicare rispettando tali restrizioni.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: true
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: d8fb04fd80e9a84bd7784e48b77e3aa8b045bf2d


---

# Procedura: Usare i diritti predefiniti

Questo argomento descrive i diritti predefiniti forniti da Microsoft Rights Management SDK 4.2 e le restrizioni di utilizzo che un'app deve applicare rispettando tali restrizioni. Il codice seguente illustra i diritti predefiniti, i diritti comuni, i diritti di modifica del documento e i diritti sui messaggi di posta elettronica con la descrizione e il valore derivante dal sistema operativo.

**Nota**: per i dettagli sull'SDK di Linux, vedere file di origine *rights.h*.

## Diritti comuni ##

**Tutti**: una raccolta di tutti i diritti comuni.
- Android: [CommonRights.All](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL)
- iOS e OS X: [MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store e Windows Phone: [CommonRights.All</strong>](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)
- Linux: [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

** Proprietario**: il diritto Proprietario concede il controllo completo sul contenuto protetto.
- Android: [<strong>CommonRights.Owner](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner)
- iOS e OS X: [MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store e Windows Phone: [CommonRights.Owner](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner)
- Linux: [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Visualizza**: il diritto di visualizzare il contenuto protetto. In genere, quando viene concesso, l'applicazione consente all'utente di aprire e visualizzare il contenuto protetto. Tuttavia, per modificare, estrarre, inoltrare o salvare il contenuto sono necessari altri diritti.

- Android: [CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- iOS e OS X: [MSCommonRights view](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store e Windows Phone: [CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- Linux: [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## Diritti di modifica del documento ##
**Tutti**: una raccolta che contiene tutti i diritti di modifica del documento.
- Android: [EditableDocumentRights.All](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL)
- iOS e OS X: [MSEditableDocumentRights all](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [CommonRights.All](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all)
- Linux: [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Commento**: il diritto per creare commenti sul documento.
- Android: [EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)
- iOS e OS X: [MSEditableDocumentRights comment](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)
- Linux: [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Modifica**: il diritto di modificare il contenuto protetto e salvarlo nell stesso formato protetti. In genere, quando viene concesso, l'applicazione consente all'utente di modificare il contenuto protetto e quindi salvarlo nello stesso file.
- Android: [EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit)
- iOS e OS X: [MSEditableDocumentRights edit](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit)
- Linux: [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Esporta**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato diverso protetto da AD RMS. In genere, quando viene concesso, l'applicazione consente all'utente di salvare il contenuto protetto in altri formati protetti da AD RMS; ad esempio, se l'applicazione contiene una funzionalità *Salva con nome*.

- Android: [EditableDocumentRights.Export](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export)
- iOS e OS X: [MSEditableDocumentRights exportable](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Export](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export)
- Linux: [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Estrai**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. In genere, quando viene concesso, l'applicazione consente all'utente di copiare e incollare le informazioni dal contenuto protetto. Se l'app contiene una funzionalità <em>Salva con nome</em>, l'applicazione potrebbe anche consentire all'utente di salvare il contenuto protetto in formati non protetti e in altri formati protetti. Questo diritto ha lo stesso valore del diritto Estrai per i messaggi di posta elettronica.

- Android: [EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract)
- iOS e OS X: [MSEditableDocumentRights extract](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract)
- Linux: [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Stampa**: il diritto di stampare il contenuto protetto. In genere, quando viene concesso, l'applicazione consente all'utente di stampare il contenuto protetto. Questo diritto ha lo stesso valore del diritto Stampa per i messaggi di posta elettronica.

- Android: [EditableDocumentRights.Print](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print)
- iOS e OS X: [MSEditableDocumentRights print](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Print](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print)
- Linux: [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## Diritti sui messaggi di posta elettronica ##

**Tutti**: una raccolta che contiene tutti i diritti sui messaggi di posta elettronica.
- Android: [EmailRights.All](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL)
- iOS e OS X: [MSEmailRights all](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.All](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)
- Linux: [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Estrai**: il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di copiare e incollare le informazioni di un messaggio protetto. Se l'app contiene una funzionalità <em>Salva con nome</em>, l'applicazione potrebbe anche consentire al destinatario di salvare il contenuto protetto in formati non protetti e in altri formati protetti. Questo diritto ha lo stesso valore del diritto Estrai dei documenti modificabili.

- Android: [EmailRights.Extract](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract)
- iOS e OS X: [MSEmailRights extract](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Extract</strong>](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract)
- Linux: [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Inoltra**: il diritto di inoltrare un messaggio protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di inoltrare un messaggio protetto.
- Android: [<strong>EmailRights.Forward</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward)
- iOS e OS X: [MSEmailRights forward](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Forward](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward)
- Linux: [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Stampa**: il diritto di stampare il contenuto protetto. In genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di stampare un messaggio protetto. Questo diritto ha lo stesso valore del diritto Stampa dei documenti modificabili.

- Android: [EmailRights.Print](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print)
- iOS e OS X: [MSEmailRights print](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Print](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print)
- Linux: [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Rispondi**: in genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di rispondere a un messaggio protetto e includere una copia del messaggio originale.

- Android: [EmailRights.Reply](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply)
- iOS e OS X: [MSEmailRights reply](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Reply](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply)
- Linux: [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Rispondi a tutti**: in genere, quando viene concesso, l'app consente a un destinatario di posta elettronica di rispondere a tutti i destinatari di un messaggio protetto e includere una copia del messaggio originale.

- Android: [EmailRights.ReplyAll</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll)
- iOS e OS X: [MSEmailRights replyAll](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.ReplyAll](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall)
- Linux: [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 



<!--HONumber=Sep16_HO5-->


