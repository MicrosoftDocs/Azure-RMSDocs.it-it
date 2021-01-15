---
title: Domande frequenti e problemi noti - Microsoft Information Projection SDK.
description: Domande frequenti e linee guida per la risoluzione dei problemi e degli errori di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: da1e3f26ca4c2a0326b6ae8dfee7a13a1855044a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212604"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Problemi noti e domande frequenti di Microsoft Information Protection (MIP) SDK

In questo articolo vengono fornite le risposte alle domande comuni e informazioni sulla risoluzione dei problemi noti e degli errori comuni.

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="metadata-storage-changes"></a>Modifiche all'archiviazione dei metadati

Recentemente è stato [annunciato](https://aka.ms/mipsdkmetadata) che è stata apportata una modifica al percorso di archiviazione dei metadati etichetta per i file di Office (Word, Excel, PowerPoint) per supportare le nuove funzionalità di Office 365, SharePoint Online e altri servizi.

#### <a name="metadata-faq"></a>Domande frequenti sui metadati

**Domanda**: quando saranno rese disponibili le prime funzionalità che richiedono la nuova posizione di archiviazione?

- Si prevede che le prime funzionalità saranno disponibili nel secondo trimestre dell'anno di calendario 2021. I clienti possono acconsentire esplicitamente alle anteprime private o pubbliche in precedenza.  

**Domanda**: sono interessati altri formati, ad esempio il formato PDF?

- No, solo i file di Office, in particolare i file Word, Excel e PowerPoint.

**Domanda**: esiste una versione specifica di MIP SDK richiesta?

- MIP SDK 1,7 e versioni successive sono completamente compatibili.

**Domanda**: esiste una versione specifica del client di Office che sarà obbligatoria o userà questo archivio?

- Quando vengono annunciate le funzionalità, il client di Office verrà aggiornato per sfruttare la nuova posizione di archiviazione. I nuovi percorsi di archiviazione non verranno usati finché le funzionalità non vengono abilitate dagli amministratori tenant.

**Domanda**: i metadati esistenti archiviati come proprietà personalizzate in *custom.xml* essere mantenuti aggiornati?

- No. La prima volta che il documento viene salvato dopo l'abilitazione del nuovo percorso di archiviazione, i metadati dell'etichetta verranno spostati nella nuova posizione. I metadati scritti tramite [`LabelingOptions.ExtendedProperties`](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.file.labelingoptions.extendedproperties?view=mipsdk-dotnet-1.7#Microsoft_InformationProtection_File_LabelingOptions_ExtendedProperties) rimarranno in *custom.xml*.

**Domanda**: è possibile leggere i metadati delle etichette senza l'SDK MIP? 

- Sì, ma è necessario implementare il proprio codice per analizzare il file ed estrarre le informazioni.

**Domanda**: attualmente è facile "leggere" l'etichetta estraendo le stringhe di coppie chiave/valore dal file. La lettura sarà ancora possibile in questo modo? 

- Sì, i metadati sono ancora disponibili nel file XML di Office per la lettura. Tuttavia, si noti che l'applicazione deve comprendere se il nuovo set di funzionalità è abilitato per sapere quale sezione è autorevole (custom.xml e labelinfo.xml). Esaminare [MS-OFFCRYPTO: LabelInfo anziché le proprietà personalizzate del documento | Microsoft Docs.](https://docs.microsoft.com/openspecs/office_file_formats/ms-offcrypto/13939de6-c833-44ab-b213-e0088bf02341) per informazioni dettagliate sull'implementazione.
  
**Domanda**: come è possibile individuare se le nuove funzionalità sono abilitate? 

- Queste informazioni vengono condivise in modo da raggiungere le date di rilascio delle funzionalità. 

**Domanda**: come verrà eseguita la migrazione delle etichette?

- La logica seguente viene usata per determinare quale sezione viene letta e usata per leggere o scrivere i dati delle etichette.

| Azione                                                                                                | Funzionalità non abilitata                                                                    | Funzionalità abilitata                                              |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Lettura                                                                                                  | Etichetta in custom.xml (non protetto) o doc SummaryInfo (Protected).                      | Se nell'labelinfo.xml è presente un'etichetta, l'etichetta è valida.<br> Se non è presente alcuna etichetta in labelinfo.xml, l'etichetta in custom.xml o doc SummaryInfo è l'etichetta valida. |
| Scrittura                                                                                                 | Tutte le nuove etichette vengono scritte in custom.xml (non protetto) o SummaryInfo di documenti (protetto). | Tutte le nuove etichette vengono scritte in labelinfo.xml.                 |


<br>
<br>

### <a name="file-parsing"></a>Analisi dei file

**Domanda**: è possibile scrivere nello stesso file che sto attualmente leggendo con il file SDK?

L'SDK MIP non supporta la lettura e la scrittura simultanee dello stesso file. Tutti i file con etichetta comporteranno una *copia* del file di input con le azioni etichetta applicate. L'applicazione deve sostituire l'originale con il file con etichetta.

### <a name="sdk-string-handling"></a>Gestione delle stringhe SDK

**Domanda**: in che modo l'SDK gestisce le stringhe e il tipo di stringa da usare nel codice?

L'SDK è progettato per essere multipiattaforma e usa [UTF-8 (Unicode Transformation Format - 8 bit)](https://wikipedia.org/wiki/UTF-8) per la gestione delle stringhe. Le linee guida specifiche dipendono dalla piattaforma in uso:

| Piattaforma        | Indicazioni                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nativa Windows  | Per i client SDK C++, il tipo di libreria standard C++ [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) viene usato per passare stringhe da e verso le funzioni API. La conversione da e verso UTF-8 viene gestita internamente da MIP SDK. Quando l'API restituisce `std::string`, è necessario aspettarsi la codifica UTF-8 e gestire di conseguenza l'eventuale conversione della stringa. In alcuni casi, viene restituita una stringa come parte di un vettore `uint8_t`(ad esempio, una licenza di pubblicazione), ma deve essere trattata come un BLOB opaco.<br><br>Per ulteriori informazioni ed esempi, vedere:<ul><li>[Funzione WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) per assistenza con la conversione di stringhe di caratteri wide a più byte, ad esempio UTF-8.<li>I file di esempio seguenti inclusi nel [download dell'SDK](setup-configure-mip.md#configure-your-client-workstation):<ul><li>Le funzioni di utilità per le stringhe di esempio `file\samples\common\string_utils.cpp`, per la conversione da e verso stringhe UTF-8 wide.<li>Un'implementazione di `wmain(int argc, wchar_t *argv[])` in `file\samples\file\main.cpp`, che usa le funzioni di conversione stringa precedenti.</li></ul></ul> |
| .NET            | Per i client .NET dell'SDK, tutte le stringhe usano la codifica predefinita UTF-16 e non è necessaria alcuna conversione speciale. La conversione da e verso UTF-16 viene gestita internamente da MIP SDK.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Altre piattaforme | Tutte le altre piattaforme supportate da MIP SDK includono il supporto nativo per UTF-8.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## <a name="issues-and-errors-reference"></a>Informazioni di riferimento per problemi ed errori

### <a name="error-file-format-not-supported"></a>Errore: "Formato di file non supportato"  

**Domanda**: perché si verifica l'errore seguente quando si tenta di proteggere o etichettare un file PDF?

> Formato di file non supportato

Questa eccezione deriva dal tentativo di proteggere o etichettare un file PDF con firma digitale o protetto da password. Per altre informazioni sulla protezione e l'assegnazione di etichette a file PDF, vedere [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nuovo supporto della crittografia PDF con Microsoft Azure Information Protection).

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Errore: "Impossibile analizzare i criteri di conformità acquisiti"  

**Domanda**: perché viene riportato l'errore seguente dopo il download dell'SDK MIP e viene effettuato un tentativo di usare l'esempio di file per elencare tutte le etichette?

> Something bad happened: Failed to parse the acquired Compliance Policy (Si è verificato un errore. Impossibile analizzare i criteri di conformità acquisiti). Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

Questo errore indica che non è stata eseguita la migrazione delle etichette da Azure Information Protection all'esperienza di etichettatura unificata. Vedere [Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365](/azure/information-protection/configure-policy-migrate-labels) per eseguire la migrazione delle etichette e quindi creare criteri per le etichette nel Centro sicurezza e conformità di Office 365. 

### <a name="error-nopolicyexception-label-policy-did-not-contain-data"></a>Errore: "nopolicyexception: i criteri di etichetta non contengono dati"

**Domanda**: perché si verifica l'errore seguente quando si tenta di leggere un'etichetta o un elenco di etichette tramite il MIP SDK?

> Nopolicyexception: i criteri di etichetta non contengono dati, CorrelationId = GUID, CorrelationId. Description = PolicyProfile, NoPolicyError. Category = SyncFile, NoPolicyError. Category = SyncFile

Questo errore indica che i criteri di etichetta non sono stati pubblicati in Microsoft Security and Compliance Center. Seguire [creare e configurare le etichette di riservatezza e i relativi criteri](/microsoft-365/compliance/create-sensitivity-labels) per configurare i criteri di etichettatura.

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>Errore: "System. ComponentModel. Win32exception: LoadLibrary failed"

**Domanda**: perché si verifica l'errore seguente quando si usa il wrapper .NET di MIP SDK?

> System. ComponentModel. Win32exception: LoadLibrary non riuscito per: [sdk_wrapper_dotnet.dll] quando viene chiamato MIP.Initialize ().

L'applicazione non dispone del runtime necessario o non è stata compilata come versione. Per ulteriori informazioni, vedere [verificare che l'applicazione disponga del runtime necessario](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) . 

### <a name="error-proxyautherror-exception"></a>Errore: "eccezione ProxyAuthError"

**Domanda**: perché si verifica l'errore seguente quando si usa l'SDK MIP?

> "ProxyAuthenticatonError: autenticazione proxy non supportata"

Il MIP SDK non supporta l'uso di proxy autenticati. Per correggere questo messaggio, gli amministratori del proxy devono impostare gli endpoint di servizio di Microsoft Information Protection per ignorare il proxy. Un elenco di tali endpoint è disponibile nella pagina [URL e intervalli di indirizzi IP di Office 365](/office365/enterprise/urls-and-ip-address-ranges) . Per MIP SDK è necessario che `*.protection.outlook.com` (riga 9) e gli endpoint servizio Azure Information Protection (riga 73) ignorino l'autenticazione proxy.
