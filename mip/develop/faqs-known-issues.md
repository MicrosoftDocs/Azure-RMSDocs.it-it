---
title: Domande frequenti e problemi noti - Microsoft Information Projection SDK.
description: Domande frequenti e linee guida per la risoluzione dei problemi e degli errori di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.collection: M365-security-compliance
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: 78dc655d8244378fcc37b22030d3060fd291ef16
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175469"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Problemi noti e domande frequenti di Microsoft Information Protection (MIP) SDK

In questo articolo vengono fornite le risposte alle domande comuni e informazioni sulla risoluzione dei problemi noti e degli errori comuni.

## <a name="frequently-asked-questions"></a>Domande frequenti 

### <a name="sdk-string-handling"></a>Gestione delle stringhe SDK

**Domanda**: In che modo il SDK gestisce le stringhe e il tipo di stringa è consigliabile usare nel codice?

L'SDK è progettato per essere multipiattaforma e usa [UTF-8 (Unicode Transformation Format - 8 bit)](https://wikipedia.org/wiki/UTF-8) per la gestione delle stringhe. Le linee guida specifiche dipendono dalla piattaforma in uso:

| Piattaforma | Indicazioni |
|-|-|
| Nativa Windows | Per i client C++ dell'SDK, viene usato il tipo di libreria Standard C++ [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) per il passaggio delle stringhe da e verso le funzioni dell'API. La conversione da e verso UTF-8 viene gestita internamente da MIP SDK. Quando l'API restituisce `std::string`, è necessario aspettarsi la codifica UTF-8 e gestire di conseguenza l'eventuale conversione della stringa. In alcuni casi, viene restituita una stringa come parte di un vettore `uint8_t`(ad esempio, una licenza di pubblicazione), ma deve essere trattata come un BLOB opaco.<br><br>Per ulteriori informazioni ed esempi, vedere:<ul><li>[Funzione WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) per assistenza con la conversione di stringhe di caratteri wide a più byte, ad esempio UTF-8.<li>I file di esempio seguenti inclusi nel [download dell'SDK](setup-configure-mip.md#configure-your-client-workstation):<ul><li>Le funzioni di utilità per le stringhe di esempio `file\samples\common\string_utils.cpp`, per la conversione da e verso stringhe UTF-8 wide.<li>Un'implementazione di `wmain(int argc, wchar_t *argv[])` in `file\samples\file\main.cpp`, che usa le funzioni di conversione stringa precedenti.</li></ul></ul>|
| .NET | Per i client .NET dell'SDK, tutte le stringhe usano la codifica predefinita UTF-16 e non è necessaria alcuna conversione speciale. La conversione da e verso UTF-16 viene gestita internamente da MIP SDK. |
| Altre piattaforme | Tutte le altre piattaforme supportate da MIP SDK includono il supporto nativo per UTF-8. |

## <a name="issues-and-errors-reference"></a>Informazioni di riferimento per problemi ed errori

### <a name="error-file-format-not-supported"></a>Errore: "Formato di file non supportato"  

**Domanda**: Il motivo per cui ottenere il seguente errore durante il tentativo di protezione o assegnare un'etichetta di un file con estensione PDF?

> Formato di file non supportato

Questa eccezione risultante dal tentativo di proteggere o assegnare un'etichetta di un file PDF che è stato firmato digitalmente o protetto da password. Per altre informazioni sulla protezione e l'assegnazione di etichette a file PDF, vedere [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nuovo supporto della crittografia PDF con Microsoft Azure Information Protection).

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Errore: "Non è stato possibile analizzare il criterio di conformità acquisito"  

**Domanda**: Perché viene visualizzato l'errore seguente dopo aver scaricato Microsoft Information Protection SDK e provare a usare il file di esempio per elencare tutte le etichette?

> È accaduto qualcosa non valida: Impossibile analizzare il criterio di conformità acquisito. Non è riuscita con: Tag [classe mip::CompliancePolicyParserException] non trovato: criteri, il tipo di nodo: 15, nome: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

Ciò indica che non eseguita la migrazione le etichette di Azure Information Protection per l'assegnazione di etichette esperienza unificata. Vedere [Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365](/azure/information-protection/configure-policy-migrate-labels) per eseguire la migrazione delle etichette e quindi creare criteri per le etichette nel Centro sicurezza e conformità di Office 365. 

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>Errore: "System.ComponentModel.Win32Exception: LoadLibrary non riuscito"

**Domanda**: Il motivo per cui ottenere l'errore seguente quando si usa il Wrapper .NET di MIP SDK?

> System.ComponentModel.Win32Exception: LoadLibrary non è riuscita per: [sdk_wrapper_dotnet.dll] quando si chiama MIP. Initialize ().

L'applicazione non è installato il runtime richiesto o non è stato compilato come versione. Visualizzare [assicurarsi che l'app ha il runtime richiesto](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) per altre informazioni. 

### <a name="error-proxyautherror-exception"></a>Errore: "Eccezione ProxyAuthError"

**Domanda**: Il motivo per cui ottenere l'errore seguente quando si usa il SDK di MIP?

> "ProxyAuthenticatonError: Autenticazione proxy non è supportato"

Microsoft Information Protection SDK non supporta l'uso dei proxy autenticato. Per correggere questo messaggio, gli amministratori di proxy devono impostare gli endpoint del servizio Microsoft Information Protection per ignorare il proxy. Un elenco di tali endpoint sono disponibili all'indirizzo il [intervalli di indirizzi IP e Office 365 URL](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges) pagina. Microsoft Information Protection SDK richiede che `*.protection.outlook.com` (riga 9) e gli endpoint del servizio Azure Information Protection (riga 73) ignorare l'autenticazione proxy.
