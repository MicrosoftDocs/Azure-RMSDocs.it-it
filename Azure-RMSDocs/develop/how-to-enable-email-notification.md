---
title: Abilitazione della notifica tramite posta elettronica | Azure RMS
description: La notifica tramite posta elettronica consente al proprietario di un contenuto protetto di ricevere un messaggio quando qualcuno accede al contenuto.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 77e2dfe7f2afb1e70de658850f83f86e9224aea6
ms.openlocfilehash: 411c549cc865914c6e35ececad99da0a0d46c5d4


---

# Procedura: Abilitare la notifica tramite posta elettronica

La notifica tramite posta elettronica consente al proprietario di un contenuto protetto di ricevere un messaggio quando qualcuno accede al contenuto.

Per configurare la notifica tramite posta elettronica per una determinata licenza, usare [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) con il parametro di tipo di proprietà *dwPropID* come [IPC\_LI\_APP\_SPECIFIC\_DATA](https://msdn.microsoft.com/library/hh535287.aspx) e i campi dei dati dell'applicazione formattati come [IPC\_NAME\_VALUE\_LIST](https://msdn.microsoft.com/library/hh535277.aspx).

    C++

    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {"MS.Conetent.Name", 0, "FinancialReport.docx"};
    propertyValuePairs[1] = {"MS.Notify.Enabled",0 , "true"};
    propertyValuePairs[2] = {"MS.Notify.Culture",0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);


La tabella seguente contiene i campi dei dati dell'applicazione e le coppie di nome e valore delle proprietà per la notifica tramite posta elettronica di RMS.


|Nome proprietà | Tipo di dati | Valore di esempio | Note |
|--------------|-----------|---------------|-------|
|MS.Content.Name|string|"FinancialReport.docx"|Si tratta di un identificatore associato al contenuto protetto.<br><br> Per i file protetti questo valore deve corrispondere al nome del file senza alcuna informazione sul percorso.<br><br> Per altri tipi di contenuto, ad esempio un messaggio di posta elettronica, può essere l'oggetto del messaggio di posta elettronica o può essere vuoto.|
|MS.Notify.Enabled|string|“true” &#124; “false”|Se questo valore è impostato su "true", verrà inviato un messaggio di notifica al proprietario della licenza di pubblicazione quando qualcuno ne tenta l’utilizzo per ottenere una licenza con l’utente finale.|
|MS.Notify.Culture|string|“it-IT”| **Origine:** System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>Questo valore viene utilizzato per determinare la lingua localizzata del messaggio di notifica e la formattazione di data/ora e numeri da usare nel messaggio di posta elettronica.<br><br>Deve essere impostato in base alle impostazioni utente del computer in cui viene creata la licenza di pubblicazione o in base alla lingua preferita del proprietario della licenza di pubblicazione.|
|MS.Notify.TZID|string|“Ora solare Pacifico”|**Origine:** TimeZoneInfo.Local.Id - ID fuso orario di Windows.<br><br>Questo valore corrisponde all'identificatore del fuso orario del sistema operativo Microsoft Windows che descrive un particolare fuso orario e le relative caratteristiche.|
|MS.Notify.TZO|string|“-480”|Questa è la differenza del fuso orario del proprietario della licenza di pubblicazione in termini di minuti rispetto all'ora UTC.<br><br>Se si specifica un valore TZID valido, verrà utilizzata la differenza del fuso orario specificato e questo valore verrà ignorato.<br><br>Questo valore verrà molto probabilmente usato da piattaforme di pubblicazione non basate su Windows che non hanno accesso all'elenco dei valori di ID del fuso orario del sistema operativo Windows.<br><br>Se non si specifica un valore TZID, verrà usato questo valore per calcolare la differenza di orario nei messaggi di notifica e il valore TZSN (indipendentemente dal valore del fuso orario) per indicare il nome del fuso orario. Il fuso orario sarà quindi fisso e non verrà aggiornato in caso di applicazione dell’ora legale.<br><br>Ad esempio:<br><br>Se TXID è vuoto, TZ0 è impostato su "-420" e il valore TZSN è impostato su "Ora legale Pacifico", tutti i valori indicati nel messaggio di notifica verranno regolati in base all’ora legale del Pacifico e verranno visualizzati di conseguenza anche se l'ora legale non è più attualmente in vigore.<br><br>Se invece si specifica un TZID insieme a entrambi i valori TZSN e TZDN, gli orari specificati nel messaggio di notifica verranno regolati e visualizzati in base all’ora legale o solare in vigore.|
|MS.Notify.TZSN|string|“Ora solare Pacifico”|**Origine:** TimeZoneInfo.Local.StandardName - Nome del fuso orario ora solare.<br><br>Questo valore deve corrispondere al nome localizzato del fuso orario ora solare.|
|MS.Notify.TZDN|string|"Ora legale Pacifico"|**Origine:** TimeZoneInfo.Local.DaylightName - Nome del fuso orario ora legale.<br><br>Questo valore deve corrispondere al nome localizzato del fuso orario ora legale. Può essere uguale al nome del fuso orario ora solare se il fuso orario non supporta l'ora legale.|

## Argomenti correlati

- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [IPC\_LI\_APP\_SPECIFIC\_DATA](https://msdn.microsoft.com/library/hh535287.aspx)
- [IPC\_NAME\_VALUE\_LIST](https://msdn.microsoft.com/library/hh535277.aspx).
 

 



<!--HONumber=Oct16_HO4-->


