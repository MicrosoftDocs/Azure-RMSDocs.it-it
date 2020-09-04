---
title: Problemi noti-Azure Information Protection
description: Eseguire ricerche ed esaminare i problemi noti e le limitazioni per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9a6d2ae357490b57b71b52e33ffef9827ecdceac
ms.sourcegitcommit: 9600ae255e7ccc8eeb49c50727a26e4666415fe2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2020
ms.locfileid: "89447039"
---
# <a name="known-issues---azure-information-protection"></a>Problemi noti-Azure Information Protection

Usare gli elenchi e le tabelle seguenti per trovare informazioni dettagliate sui problemi noti e sulle limitazioni relative alle funzionalità di Azure Information Protection.

> [!NOTE]
> Questo articolo si riferisce a problemi noti nei client di etichette classici e unificati. Non si è certi della differenza tra questi client? Vedere le [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).

## <a name="client-support-for-container-files-such-as-zip-files"></a>Supporto client per file contenitore, ad esempio file con estensione zip

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione. È possibile tuttavia rimuovere la protezione per tutti i file contenuti nei file contenitore supportati usando il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

Per altre informazioni, vedere [Guida dell'amministratore: tipi di file supportati dal client Azure Information Protection](rms-client/client-admin-guide-file-types.md).

## <a name="known-issues-for-installing-the-aip-client"></a>Problemi noti per l'installazione del client AIP

Il client Azure Information Protection non è supportato nei computer in cui è abilitata la [protezione dagli exploit](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) .

Assicurarsi di disabilitare la protezione dagli exploit prima di installare AIP. 

Per disabilitare la protezione dagli exploit tramite PowerShell, eseguire le operazioni seguenti:

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

Per ulteriori informazioni, vedere [Azure Information Protection requirements](requirements.md).

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Supporto di PowerShell per il client di Azure Information Protection

La versione corrente del modulo **AzureInformationProtection** di PowerShell installato con il client di Azure Information Protection presenta i seguenti problemi noti:

- **Cartelle personali di Outlook (* file. pst *) * *. La protezione nativa dei file *. pst* non è supportata con il modulo **AzureInformationProtection** .

- **Messaggi di posta elettronica protetti di Outlook (file con *estensione rpmsg* )**. La rimozione della protezione dei messaggi di posta elettronica protetti di Outlook è supportata dal modulo **AzureInformationProtection** solo se si trovano all'interno di una cartella personale di Outlook (file con *estensione pst* ).

    La rimozione della protezione dei messaggi di posta elettronica all'esterno di un file con *estensione pst* non è supportata.

Per altre informazioni, vedere [Guida dell'amministratore: uso di PowerShell con il client Azure Information Protection](rms-client/client-admin-guide-powershell.md).

## <a name="aip-known-issues-in-office-applications"></a>Problemi noti di AIP nelle applicazioni di Office

|Feature  |Problemi noti  |
|---------|---------|
|**Più versioni di Office**    | I client Azure Information Protection, incluse le etichette classiche e unificate, non supportano più versioni di Office nello stesso computer o scambiano gli account utente in Office.       |
|**Più visualizzazioni** |Se si usano più visualizzazioni e si apre un'applicazione di Office: </br></br>-È possibile che si verifichino problemi di prestazioni nelle app di Office.</br>-La barra di Azure Information Protection può sembrare mobile al centro della schermata di Office, in una o in entrambe le visualizzazioni </br></br>Per garantire prestazioni coerenti e che la barra rimanga nella posizione corretta, aprire la finestra di dialogo **Opzioni** per l'applicazione di Office e in **generale** Selezionare **Ottimizza per compatibilità** anziché **Ottimizza per l'aspetto migliore.**    |
|**Supporto di IRM in Office 2016**| L'impostazione del registro di sistema [DRMEncryptProperty](https://docs.microsoft.com/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) , che controlla la crittografia dei metadati in Office 2016, non è supportata per le etichette Azure Information Protection.|
|**Contrassegni di contenuto in Word**    | Azure Information Protection i [Contrassegni](configure-policy-markings.md) di contenuto possono essere nascosti nei piè di pagina di Microsoft Word, quando il piè di pagina contiene anche una tabella. Per ulteriori informazioni, vedere [quando vengono applicati i contrassegni visivi](configure-policy-markings.md#when-visual-markings-are-applied). |
|**File allegati ai messaggi di posta elettronica** |A causa di una limitazione negli aggiornamenti recenti di Windows, quando [Microsoft Outlook è protetto da Azure Rights Management](office-apps-services-support.md), i file allegati ai messaggi di posta elettronica possono essere bloccati dopo l'apertura del file. |
|**Unione posta**    |  La funzionalità di Unione di Office [mail](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) non è supportata con alcuna funzionalità Azure Information Protection.       |
| **Messaggi di posta elettronica S/MIME** | L'apertura di messaggi di posta elettronica S/MIME nel riquadro di lettura di Outlook può causare problemi di prestazioni. </br></br>Per evitare problemi di prestazioni con i messaggi di posta elettronica S/MIME, abilitare la proprietà avanzata [**OutlookSkipSmimeOnReadingPaneProperty**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) . </br></br>**Nota:** L'abilitazione di questa proprietà impedisce la visualizzazione della barra di AIP o della classificazione dei messaggi di posta elettronica nel riquadro di lettura di Outlook. |
| | |

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

## <a name="aip-for-windows-and-office-versions-in-extended-support"></a>AIP per versioni di Windows e Office nel supporto esteso

- [**Windows 7 Extended supported è terminato il 14 gennaio 2020**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet). 

    Si consiglia vivamente di eseguire l'aggiornamento a una versione più recente di Windows 10. Tuttavia, se sono presenti aggiornamenti della sicurezza estesi e un contratto di supporto, è disponibile il supporto per AIP per continuare a mantenere i sistemi Windows 7 protetti.

    Per ulteriori informazioni, consultare il contatto del supporto tecnico.

- [**Office 2010 è attualmente in supporto esteso**](https://support.microsoft.com/lifecycle/search?alpha=office%202010). 

    Il supporto terminerà il 13 ottobre 2020 e non verrà esteso. Inoltre, l'unità di gestione delle attività non verrà offerta per Office 2010 e si consiglia vivamente di eseguire l'aggiornamento a una versione più recente di Office 365. 
    
    Per i clienti che eseguono attualmente Office 2010 nel supporto esteso, il supporto per AIP è disponibile fino al 13 ottobre 2020. 

    Per ulteriori informazioni, consultare il contatto del supporto tecnico.


## <a name="more-information"></a>Altre informazioni

Gli articoli aggiuntivi seguenti possono essere utili per rispondere alle domande sui problemi noti in Azure Information Protection:

- [Domande frequenti su Azure Information Protection](faqs.md)
- [Domande frequenti sulla protezione dati in Azure Information Protection](faqs-rms.md)
- [Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection](faqs-infoprotect.md)
- [Domande frequenti sull'app di Microsoft Azure Information Protection per iOS e Android](rms-client/mobile-app-faq.md)

