---
title: Problemi noti-Azure Information Protection
description: Eseguire ricerche ed esaminare i problemi noti e le limitazioni per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/02/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cec682216c07f93b36d189f3c385dc935b2f887d
ms.sourcegitcommit: 6d10435c67434bdbbdd51b4a3535d0efaf8307da
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86869659"
---
# <a name="known-issues---azure-information-protection"></a>Problemi noti-Azure Information Protection

Usare gli elenchi e le tabelle seguenti per trovare informazioni dettagliate sui problemi noti e sulle limitazioni relative alle funzionalità di Azure Information Protection.

> [!NOTE]
> Questo articolo si riferisce a problemi noti nei client di etichette classici e unificati. Non si è certi della differenza tra questi client? Vedere le [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).

<!--removed from this page
## HYOK known issues

HYOK has the following known issues:

- [Supported Microsoft Office versions](#supported-microsoft-office-versions)
- [Email recommendations for Office 365 and other online services](#email-recommendations-for-office-365-and-other-online-services)

### Supported Microsoft Office versions

HYOK for the Azure Information Protection classic client does not support versions of Office earlier than Office 2013.

### Email recommendations for Office 365 and other online services

We recommend that you do not use HYOK protection for emails in Office 365 and other online services.

Office 365 and other online services are not be able to decrypt HYOK-protected documents and emails. This limitation includes HYOK-protected documents and emails that have been protected with the Rights Management connector, and prevents these services from inspecting the content and taking action on them.

This loss of functionality for HYOK-protected email includes malware scanners, data loss prevention (DLP) solutions, mail routing rules, journaling, eDiscovery, archiving solutions, and Exchange ActiveSync.

Additionally, users may not understand why some devices cannot open their HYOK-protected emails, resulting in more calls to your help desk.
-->

## <a name="client-support-for-container-files-such-as-zip-files"></a>Supporto client per file contenitore, ad esempio file con estensione zip

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione. È possibile tuttavia rimuovere la protezione per tutti i file contenuti nei file contenitore supportati usando il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

Per altre informazioni, vedere [Guida dell'amministratore: tipi di file supportati dal client Azure Information Protection](rms-client/client-admin-guide-file-types.md).

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Supporto di PowerShell per il client di Azure Information Protection

La versione corrente del modulo **AzureInformationProtection** di PowerShell installato con il client di Azure Information Protection presenta i seguenti problemi noti:

- **Cartelle personali di Outlook (* file. pst *) * *. La protezione nativa dei file *. pst* non è supportata con il modulo **AzureInformationProtection** .

- **Messaggi di posta elettronica protetti di Outlook (file con *estensione rpmsg* )**. La rimozione della protezione dei messaggi di posta elettronica protetti di Outlook è supportata dal modulo **AzureInformationProtection** solo se si trovano all'interno di una cartella personale di Outlook (file con *estensione pst* ).

    La rimozione della protezione dei messaggi di posta elettronica all'esterno di un file con *estensione pst* non è supportata.

Per altre informazioni, vedere [Guida dell'amministratore: uso di PowerShell con il client Azure Information Protection](rms-client/client-admin-guide-powershell.md).

<!-- removed from this page
## Protection-only mode known issues

The following known issues apply for [Protection-only mode for the Azure Information Protection client](rms-client/client-protection-only-mode.md):

- In Office apps, the Azure Information Protection bar is not shown. When you click **Protect** > **Show Bar**, this menu option is unavailable.

- When you use the **Classify and protect - Azure Information Protection** dialog box with the File Explorer, labels for classification are not shown. Instead, you have an option select a Rights Management (RMS) template.
-->

## <a name="aip-known-issues-in-office-applications"></a>Problemi noti di AIP nelle applicazioni di Office

|Funzionalità  |Problemi noti  |
|---------|---------|
|Più versioni di Office    | I client Azure Information Protection, incluse le etichette classiche e unificate, non supportano più versioni di Office nello stesso computer o scambiano gli account utente in Office.       |
|Supporto di IRM in Office 2016 | L'impostazione del registro di sistema [DRMEncryptProperty](https://docs.microsoft.com/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) , che controlla la crittografia dei metadati in in Office 2016, non è supportata per le etichette Azure Information Protection.|
|Contrassegni di contenuto in Word    | Azure Information Protection i [Contrassegni](configure-policy-markings.md) di contenuto possono essere nascosti nei piè di pagina di Microsoft Word, quando il piè di pagina contiene anche una tabella. Per ulteriori informazioni, vedere [quando vengono applicati i contrassegni visivi](configure-policy-markings.md#when-visual-markings-are-applied). |
|Contrassegni di contenuto nei messaggi di posta elettronica | Il contrassegno di contenuto dinamico, ad esempio l'aggiunta di intestazioni/piè di pagina con macro ai messaggi di posta elettronica, è supportato solo per Outlook quando si usa il client Azure Information Protection. </br></br>Il contrassegno di contenuto dinamico non è supportato nell'applicazione Outlook nativa o in Outlook online. |
|File allegati ai messaggi di posta elettronica |A causa di una limitazione negli aggiornamenti recenti di Windows, quando [Microsoft Outlook è protetto da Azure Rights Management](office-apps-services-support.md), i file allegati ai messaggi di posta elettronica possono essere bloccati dopo l'apertura del file. |
|Unione posta    |  La funzionalità di Unione di Office [mail](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) non è supportata con alcuna funzionalità Azure Information Protection.       |
| | |

<!-- removing b/c this is relevant for classic only. for UL, labels are configured in m365. so this is basically irrelevant for us.
## Known issues in labeling

Depending on your policy rule size limit, configuring more than 200 users or user groups for each label may cause unexpected errors. 
-->

## <a name="known-issues-in-policies"></a>Problemi noti dei criteri

I criteri di pubblicazione possono richiedere fino a 24 ore.

## <a name="known-issues-in-the-aip-client"></a>Problemi noti nel client AIP

- **Dimensioni massime dei file. I file** di oltre 2 GB sono supportati per la protezione, ma non per la decrittografia.

- **Visualizzatore AIP.** Il Visualizzatore AIP Visualizza le immagini in modalità verticale e alcune immagini di visualizzazione orizzontale possono sembrare estesi.

    Ad esempio, un'immagine originale viene visualizzata sotto a sinistra, con una versione con estensione verticale nel Visualizzatore AIP a destra. 
    
    :::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="Immagine estesa nel visualizzatore client":::
    
    Per altre informazioni, vedere:

    - [**Client classico**: visualizzare i file protetti con il Visualizzatore Azure Information Protection](rms-client/client-view-use-files.md)
    - [**Client con etichetta unificata**: visualizzare i file protetti con il Visualizzatore Azure Information Protection](rms-client/clientv2-view-use-files.md)


## <a name="more-information"></a>Ulteriori informazioni

Gli articoli aggiuntivi seguenti possono essere utili per rispondere alle domande sui problemi noti in Azure Information Protection:

- [Domande frequenti su Azure Information Protection](faqs.md)
- [Domande frequenti sulla protezione dati in Azure Information Protection](faqs-rms.md)
- [Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection](faqs-infoprotect.md)
- [Domande frequenti sull'app di Microsoft Azure Information Protection per iOS e Android](rms-client/mobile-app-faq.md)

