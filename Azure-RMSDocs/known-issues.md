---
title: Problemi noti - Azure Information Protection
description: Eseguire ricerche ed esaminare i problemi noti e le limitazioni per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/08/2021
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 87ed3e51e063baa864d0e58f391777aa9b4426ee
ms.sourcegitcommit: 34b029c05998681ff4af845cc51ee13cf3f2b58b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2021
ms.locfileid: "99817823"
---
# <a name="known-issues---azure-information-protection"></a>Problemi noti - Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Usare gli elenchi e le tabelle seguenti per trovare informazioni dettagliate sui problemi noti e sulle limitazioni relative alle funzionalità di Azure Information Protection.

## <a name="client-support-for-container-files-such-as-zip-files"></a>Supporto client per file contenitore, ad esempio file con estensione zip

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione. È possibile tuttavia rimuovere la protezione per tutti i file contenuti nei file contenitore supportati usando il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

Per altre informazioni, vedere [Guida dell'amministratore: tipi di file supportati dal client Azure Information Protection](rms-client/client-admin-guide-file-types.md).

## <a name="known-issues-for-aip-and-exploit-protection"></a>Problemi noti per la protezione da AIP e exploit

Il client Azure Information Protection non è supportato nei computer in cui è installato .NET 2 o 3, in cui è abilitata la [protezione dagli exploit](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) e le app di Office si comportano in modo imprevisto.

In questi casi, è consigliabile aggiornare la versione di .NET. Per ulteriori informazioni, vedere [Microsoft .NET Framework requirements](rms-client/reqs-ul-client.md#microsoft-net-framework-requirements).

Se è necessario lasciare .NET versione 2 o 3, assicurarsi di disabilitare la protezione dagli exploit prima di installare AIP. 

Per disabilitare la protezione dagli exploit tramite PowerShell, eseguire le operazioni seguenti:

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Supporto di PowerShell per il client di Azure Information Protection

La versione corrente del modulo **AzureInformationProtection** di PowerShell installato con il client di Azure Information Protection presenta i seguenti problemi noti:

- **Cartelle personali di Outlook (* file. pst *) * *. La protezione nativa dei file *. pst* non è supportata con il modulo **AzureInformationProtection** .

- **Messaggi di posta elettronica protetti di Outlook (file con *estensione rpmsg* )**. La rimozione della protezione dei messaggi di posta elettronica protetti di Outlook è supportata dal modulo **AzureInformationProtection** solo se si trovano all'interno di una cartella personale di Outlook (file con *estensione pst* ).

    La rimozione della protezione dei messaggi di posta elettronica all'esterno di un file con *estensione pst* non è supportata.

Per altre informazioni, vedere [Guida dell'amministratore: uso di PowerShell con il client Azure Information Protection](rms-client/client-admin-guide-powershell.md).

## <a name="aip-known-issues-in-office-applications"></a>Problemi noti di AIP nelle applicazioni di Office

|Funzionalità  |Problemi noti  |
|---------|---------|
|**Più versioni di Office**    | I client di Azure Information Protection, incluse le etichettature classica e unificata, non supportano più versioni di Office nello stesso computer o lo scambio degli account utente in Office.       |
|**Più visualizzazioni** |Se si usano più visualizzazioni e si apre un'applicazione di Office: <br><br>-È possibile che si verifichino problemi di prestazioni nelle app di Office.<br>-La barra di Azure Information Protection può sembrare mobile al centro della schermata di Office, in una o in entrambe le visualizzazioni <br><br>Per garantire prestazioni coerenti e che la barra rimanga nella posizione corretta, aprire la finestra di dialogo **Opzioni** per l'applicazione di Office e in **generale** Selezionare **Ottimizza per compatibilità** anziché **Ottimizza per l'aspetto migliore**.    |
|**Supporto di IRM in Office 2016**| L'impostazione del registro di sistema [DRMEncryptProperty](/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) , che controlla la crittografia dei metadati in Office 2016, non è supportata per le etichette Azure Information Protection.|
|**Accesso al modello a oggetti di Outlook** | -L'impostazione del registro di sistema [PromptOOMAddressBookAccess](/outlook/troubleshoot/security/information-about-email-security-settings#configure-a-prompt-when-a-program-accesses-an-address-book-by-using-the-outlook-object-model) , che controlla i prompt che vengono visualizzati quando si accede alle rubriche tramite il modello a oggetti di Outlook, non è supportata con le etichette Azure Information Protection. <br><br>-L'impostazione del registro di sistema [PromptOOMAddressInformationAccess](/outlook/troubleshoot/security/information-about-email-security-settings#configure-a-prompt-when-a-program-reads-address-information-by-using-the-outlook-object-model) , che controlla le richieste visualizzate quando un programma legge le informazioni sull'indirizzo, non è supportata per le etichette Azure Information Protection.|
|**Contrassegni di contenuto in Word**    | I [contrassegni di contenuto](configure-policy-markings.md) AIP nelle intestazioni o nei piè di pagina di Microsoft Word possono essere spostati o posizionati in modo errato oppure possono essere nascosti completamente, quando la stessa intestazione o il piè di pagina contiene anche una tabella.<br><br>Per ulteriori informazioni, vedere [quando vengono applicati i contrassegni visivi](configure-policy-markings.md#when-visual-markings-are-applied). |
|**File allegati ai messaggi di posta elettronica** |A causa di una limitazione negli aggiornamenti recenti di Windows, quando [Microsoft Outlook è protetto da Azure Rights Management](office-apps-services-support.md), i file allegati ai messaggi di posta elettronica possono essere bloccati dopo l'apertura del file. |
|**Unione posta**    |  La funzionalità di [stampa unione](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) di Office non è supportata con alcuna funzionalità di Azure Information Protection.       |
| **Messaggi di posta elettronica S/MIME** | L'apertura di messaggi di posta elettronica S/MIME nel riquadro di lettura di Outlook può causare problemi di prestazioni. <br><br>Per evitare problemi di prestazioni con i messaggi di posta elettronica S/MIME, abilitare la proprietà avanzata [**OutlookSkipSmimeOnReadingPaneEnabled**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) . <br><br>**Nota**: l'abilitazione di questa proprietà impedisce la visualizzazione della barra di AIP o della classificazione dei messaggi di posta elettronica nel riquadro di lettura di Outlook. |
|**Opzione Invia a Esplora file** |Se si sceglie di fare clic con il pulsante destro del mouse su un file in Esplora file e selezionare **Invia a > destinatario della posta**, il messaggio di Outlook visualizzato con il file allegato potrebbe non visualizzare la barra degli strumenti di AIP. <br><br>In tal caso, è necessario usare le opzioni della barra degli strumenti di AIP, avviare la posta elettronica da Outlook, quindi individuare e alleghiare il file che si vuole inviare.|
| | |

## <a name="known-issues-in-policies"></a>Problemi noti dei criteri

I criteri di pubblicazione possono richiedere fino a 24 ore.

## <a name="maximum-file-sizes"></a>Dimensioni massime file

I file di oltre 2 GB sono supportati per la protezione, ma non per la decrittografia.

## <a name="known-issues-for-the-aip-viewer"></a>Problemi noti per il Visualizzatore AIP

Il Visualizzatore AIP Visualizza le immagini in modalità verticale e alcune immagini di visualizzazione orizzontale possono sembrare estesi.

Ad esempio, un'immagine originale viene visualizzata sotto a sinistra, con una versione con estensione verticale nel Visualizzatore AIP a destra. 
    
:::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="Immagine estesa nel visualizzatore client":::
    
Per altre informazioni, vedere:

- [**Client classico**: visualizzare i file protetti con il Visualizzatore Azure Information Protection](rms-client/client-view-use-files.md)
- [**Client con etichetta unificata**: visualizzare i file protetti con il Visualizzatore Azure Information Protection](rms-client/clientv2-view-use-files.md)

## <a name="known-issues-for-track-and-revoke-features-public-preview"></a>Problemi noti per le funzionalità di rilevamento e revoca (anteprima pubblica)

Il rilevamento e la revoca dell'accesso ai documenti mediante il client Unified Labeling presenta i seguenti problemi noti:

- [Documenti protetti da password](#password-protected-documents)
- [Più allegati in un messaggio di posta elettronica protetto](#multiple-attachments-in-a-protected-email)
- [Documenti a cui si accede tramite SharePoint o OneDrive](#documents-accessed-via-sharepoint-or-onedrive)

Per ulteriori informazioni, vedere la [Guida dell'amministratore](rms-client/track-and-revoke-admin.md) e le procedure per la [Guida dell'utente](rms-client/revoke-access-user.md) .

#### <a name="password-protected-documents"></a>Documenti protetti da password

I documenti protetti da password non sono supportati dalle funzionalità di rilevamento e revoca.
#### <a name="multiple-attachments-in-a-protected-email"></a>Più allegati in un messaggio di posta elettronica protetto

Se si collegano più documenti a un messaggio di posta elettronica e quindi si proteggono i messaggi di posta elettronica e li si invia, ogni allegato otterrà lo stesso valore ContentID. 

Il valore di ContentID verrà restituito solo con il primo file aperto. Se si cerca gli altri allegati, il valore ContentID richiesto per ottenere i dati di rilevamento non viene restituito.      

Inoltre, la revoca dell'accesso per uno degli allegati revoca anche l'accesso per gli altri allegati nello stesso indirizzo di posta elettronica protetto.

#### <a name="documents-accessed-via-sharepoint-or-onedrive"></a>Documenti a cui si accede tramite SharePoint o OneDrive
    
- I documenti protetti caricati in SharePoint o OneDrive perdono il valore **ContentID** e non è possibile rilevare o revocare l'accesso.

- Se un utente Scarica il file da SharePoint o OneDrive e lo accede dal computer locale, al documento viene applicato un nuovo **ContentID** quando viene aperto localmente. 
    
    Se si usa il valore **ContentID** originale per tenere traccia dei dati, non sarà incluso alcun accesso eseguito per il file scaricato dall'utente. Inoltre, la revoca dell'accesso in base al valore **ContentID** originale non revoca l'accesso per nessuno dei file scaricati.

    In questi casi, gli amministratori potrebbero essere in grado di individuare i file scaricati usando PowerShell per trovare i nuovi valori **ContentID** per rilevare o revocare l'accesso.

### <a name="known-issues-for-the-aip-client-and-onedrive"></a>Problemi noti per il client AIP e OneDrive

Se sono presenti documenti archiviati in OneDrive con un'etichetta di riservatezza applicata e un amministratore modifica l'etichetta nel criterio di etichettatura per aggiungere la protezione, la protezione appena applicata non viene applicata automaticamente al documento con etichetta. 

In questi casi, rietichettare manualmente il documento per applicare la protezione in base alle esigenze.
## <a name="aip-and-legacy-windows-and-office-versions"></a>AIP e versioni legacy di Windows e Office

- [**Windows 7 Extended supported è terminato il 14 gennaio 2020**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet). 

    Si consiglia vivamente di eseguire l'aggiornamento a una versione più recente di Windows 10. 

    Tuttavia, se sono presenti aggiornamenti della sicurezza estesi e un contratto di supporto, è disponibile il supporto per AIP per continuare a mantenere i sistemi Windows 7 protetti.

    Per ulteriori informazioni, consultare il contatto del supporto tecnico.

- [**Il supporto esteso per Office 2010 è terminato il 13 ottobre 2020**](https://support.microsoft.com/lifecycle/search?alpha=office%202010). 

    Questo supporto non verrà esteso e l'unità di servizio non verrà offerta per Office 2010. 

    Si consiglia vivamente di eseguire l'aggiornamento a una versione più recente di Office 365. 
    
    Per ulteriori informazioni, consultare il contatto del supporto tecnico.

## <a name="aip-based-conditional-access-policies"></a>Criteri di accesso condizionale basati su AIP

Per visualizzare il contenuto, gli utenti esterni che ricevono contenuti protetti da [criteri di accesso condizionale](/azure/active-directory/conditional-access/concept-conditional-access-policy-common) devono disporre di un account utente guest di collaborazione B2B (business to business) Azure Active Directory (Azure ad).

Sebbene sia possibile invitare gli utenti esterni ad attivare un account utente Guest, consentendo loro di eseguire l'autenticazione e superare i requisiti di accesso condizionale, potrebbe essere difficile assicurarsi che ciò avvenga per tutti gli utenti esterni necessari.

È consigliabile abilitare i criteri di accesso condizionale basati su AIP solo per gli utenti interni.

**Abilitare i criteri di accesso condizionale per AIP solo per gli utenti interni**:

1.  Nel portale di Azure passare al pannello **accesso condizionale** e selezionare i criteri di accesso condizionale che si desidera modificare. 
2.  In **assegnazioni** selezionare **utenti e gruppi** e quindi selezionare **tutti gli utenti**. Assicurarsi che l'opzione **tutti gli utenti guest ed External** *non* sia selezionata.
3.  Salvare le modifiche. 
 
È anche possibile disabilitare completamente la CA entro Azure Information Protection se la funzionalità non è necessaria per l'organizzazione, al fine di evitare questo potenziale problema. 

Per ulteriori informazioni, vedere la [documentazione sull'accesso condizionale](/azure/active-directory/conditional-access/concept-conditional-access-users-groups).

## <a name="more-information"></a>Ulteriori informazioni

Gli articoli aggiuntivi seguenti possono essere utili per rispondere alle domande sui problemi noti in Azure Information Protection:

- [Domande frequenti su Azure Information Protection](faqs.md)
- [Domande frequenti sulla protezione dati in Azure Information Protection](faqs-rms.md)
- [Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection](faqs-infoprotect.md)
- [Domande frequenti sull'app di Microsoft Azure Information Protection per iOS e Android](rms-client/mobile-app-faq.md)