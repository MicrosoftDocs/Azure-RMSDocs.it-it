---
title: Domande frequenti e problemi noti - Microsoft Information Projection SDK.
description: Domande frequenti e linee guida per la risoluzione dei problemi e degli errori di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: 974995056b14d714dbda7e00df4255cbd54302e1
ms.sourcegitcommit: 44b874f32cbd1e0552ba8a1f8c9496344ecf8adc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83630402"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Problemi noti e domande frequenti di Microsoft Information Protection (MIP) SDK

In questo articolo vengono fornite le risposte alle domande comuni e informazioni sulla risoluzione dei problemi noti e degli errori comuni.

## <a name="frequently-asked-questions"></a>Domande frequenti 

### <a name="sdk-string-handling"></a>Gestione delle stringhe SDK

**Domanda**: in che modo l'SDK gestisce le stringhe e il tipo di stringa da usare nel codice?

L'SDK è progettato per essere multipiattaforma e usa [UTF-8 (Unicode Transformation Format - 8 bit)](https://wikipedia.org/wiki/UTF-8) per la gestione delle stringhe. Le linee guida specifiche dipendono dalla piattaforma in uso:

| Piattaforma | Materiale sussidiario |
|-|-|
| Nativa Windows | Per i client SDK C++, il tipo di libreria standard C++ [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) viene usato per passare stringhe da e verso le funzioni API. La conversione da e verso UTF-8 viene gestita internamente da MIP SDK. Quando l'API restituisce `std::string`, è necessario aspettarsi la codifica UTF-8 e gestire di conseguenza l'eventuale conversione della stringa. In alcuni casi, viene restituita una stringa come parte di un vettore `uint8_t`(ad esempio, una licenza di pubblicazione), ma deve essere trattata come un BLOB opaco.<br><br>Per ulteriori informazioni ed esempi, vedere:<ul><li>[Funzione WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) per assistenza con la conversione di stringhe di caratteri wide a più byte, ad esempio UTF-8.<li>I file di esempio seguenti inclusi nel [download dell'SDK](setup-configure-mip.md#configure-your-client-workstation):<ul><li>Le funzioni di utilità per le stringhe di esempio `file\samples\common\string_utils.cpp`, per la conversione da e verso stringhe UTF-8 wide.<li>Un'implementazione di `wmain(int argc, wchar_t *argv[])` in `file\samples\file\main.cpp`, che usa le funzioni di conversione stringa precedenti.</li></ul></ul>|
| .NET | Per i client .NET dell'SDK, tutte le stringhe usano la codifica predefinita UTF-16 e non è necessaria alcuna conversione speciale. La conversione da e verso UTF-16 viene gestita internamente da MIP SDK. |
| Altre piattaforme | Tutte le altre piattaforme supportate da MIP SDK includono il supporto nativo per UTF-8. |

## <a name="issues-and-errors-reference"></a>Informazioni di riferimento per problemi ed errori

### <a name="error-file-format-not-supported"></a>Errore: "Formato di file non supportato"  

**Domanda**: perché si verifica l'errore seguente quando si tenta di proteggere o etichettare un file PDF?

> Formato di file non supportato

Questa eccezione deriva dal tentativo di proteggere o etichettare un file PDF con firma digitale o protetto da password. Per altre informazioni sulla protezione e l'assegnazione di etichette a file PDF, vedere [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nuovo supporto della crittografia PDF con Microsoft Azure Information Protection).

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Errore: "Impossibile analizzare i criteri di conformità acquisiti"  

**Domanda**: perché viene riportato l'errore seguente dopo il download dell'SDK MIP e viene effettuato un tentativo di usare l'esempio di file per elencare tutte le etichette?

> Something bad happened: Failed to parse the acquired Compliance Policy (Si è verificato un errore. Impossibile analizzare i criteri di conformità acquisiti). Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

Ciò indica che non è stata eseguita la migrazione delle etichette da Azure Information Protection all'esperienza unificata di assegnazione di etichette. Vedere [Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365](/azure/information-protection/configure-policy-migrate-labels) per eseguire la migrazione delle etichette e quindi creare criteri per le etichette nel Centro sicurezza e conformità di Office 365. 

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>Errore: "System. ComponentModel. Win32exception: LoadLibrary failed"

**Domanda**: perché si verifica l'errore seguente quando si usa il wrapper .NET di MIP SDK?

> System. ComponentModel. Win32exception: LoadLibrary non riuscito per: [sdk_wrapper_dotnet. dll] quando si chiama MIP. Inizializzare ().

L'applicazione non dispone del runtime necessario o non è stata compilata come versione. Per ulteriori informazioni, vedere [verificare che l'applicazione disponga del runtime necessario](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) . 

### <a name="error-proxyautherror-exception"></a>Errore: "eccezione ProxyAuthError"

**Domanda**: perché si verifica l'errore seguente quando si usa l'SDK MIP?

> "ProxyAuthenticatonError: autenticazione proxy non supportata"

Il MIP SDK non supporta l'uso di proxy autenticati. Per correggere questo messaggio, gli amministratori del proxy devono impostare gli endpoint di servizio di Microsoft Information Protection per ignorare il proxy. Un elenco di tali endpoint è disponibile nella pagina [URL e intervalli di indirizzi IP di Office 365](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges) . Per MIP SDK è necessario che `*.protection.outlook.com` (riga 9) e gli endpoint servizio Azure Information Protection (riga 73) ignorino l'autenticazione proxy.

### <a name="issues-in-net-core"></a>Problemi in .NET Core

**Domanda**: il pacchetto NuGet funziona in .NET Core? 

Il pacchetto NuGet verrà installato in un progetto .NET Core, ma non verrà eseguito. Stiamo lavorando per correggere questa operazione per Windows, ma non abbiamo una sequenza temporale per supportare altre piattaforme. 