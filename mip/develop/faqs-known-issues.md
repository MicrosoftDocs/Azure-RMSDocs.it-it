---
title: Domande frequenti e problemi noti - Microsoft Information Projection SDK.
description: Domande frequenti e linee guida per la risoluzione dei problemi noti di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 10/19/2018
ms.author: bryanla
ms.openlocfilehash: cb3bdd6f2d9328a57156580f3d345d25983fccad
ms.sourcegitcommit: cc65c3851d4b8169a1a62c83afaf0f75402f7631
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/20/2018
ms.locfileid: "49476429"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-known-issues"></a>Problemi noti e domande frequenti di Microsoft Information Protection (MIP) SDK

## <a name="frequently-asked-questions-faqs"></a>Domande frequenti

### <a name="question-which-platforms-are-supported-by-the-mip-sdk"></a>Domanda: quali piattaforme sono supportate da MIP SDK?

MIP SDK è supportato nelle piattaforme seguenti:

[!INCLUDE [MIP SDK platform support](../include/mip-sdk-platform-support.md)]

### <a name="question-how-does-the-sdk-handle-strings-and-what-string-type-should-i-be-using-in-my-code"></a>Domanda: come vengono gestite le stringhe nell'SDK e quale tipo di stringa si deve usare nel codice?

L'SDK è progettato per essere multipiattaforma e usa [UTF-8 (Unicode Transformation Format - 8 bit)](https://wikipedia.org/wiki/UTF-8) per la gestione delle stringhe. Le linee guida specifiche dipendono dalla piattaforma in uso:

| Piattaforma | Indicazioni |
|-|-|
| Nativa Windows | Per i client C++ dell'SDK, viene usato il tipo di libreria Standard C++ [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) per il passaggio delle stringhe da e verso le funzioni dell'API. La conversione da e verso UTF-8 viene gestita internamente da MIP SDK. Quando l'API restituisce `std::string`, è necessario aspettarsi la codifica UTF-8 e gestire di conseguenza l'eventuale conversione della stringa. In alcuni casi, viene restituita una stringa come parte di un vettore `uint8_t`(ad esempio, una licenza di pubblicazione), ma deve essere trattata come un BLOB opaco.<br><br>Per ulteriori informazioni ed esempi, vedere:<ul><li>[Funzione WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) per assistenza con la conversione di stringhe di caratteri wide a più byte, ad esempio UTF-8.<li>I file di esempio seguenti inclusi nel [download dell'SDK](setup-configure-mip.md#configure-your-client-workstation):<ul><li>Le funzioni di utilità per le stringhe di esempio `file\samples\common\string_utils.cpp`, per la conversione da e verso stringhe UTF-8 wide.<li>Un'implementazione di `wmain(int argc, wchar_t *argv[])` in `file\samples\file\main.cpp`, che usa le funzioni di conversione stringa precedenti.</li></ul></ul>|
| .NET | Per i client .NET dell'SDK, tutte le stringhe usano la codifica predefinita UTF-16 e non è necessaria alcuna conversione speciale. La conversione da e verso UTF-16 viene gestita internamente da MIP SDK. |
| Altre piattaforme | Tutte le altre piattaforme supportate da MIP SDK includono il supporto nativo per UTF-8. |

## <a name="known-issues"></a>Problemi noti

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Errore: "Impossibile analizzare i criteri di conformità acquisiti"  

È stato scaricato MIP SDK e sono state eseguite le applicazioni di esempio. Si usa il file di esempio per provare a elencare tutte le etichette, ma viene visualizzato l'errore seguente:

| Errore | Soluzione |
|-|-|
|*Something bad happened: Failed to parse the acquired Compliance Policy (Si è verificato un errore. Impossibile analizzare i criteri di conformità acquisiti). Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]*| Questo errore indica che non è stata eseguita la migrazione delle etichette da Azure Information Protection all'esperienza di etichettatura unificata. Vedere [Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365](/azure/information-protection/configure-policy-migrate-labels) per eseguire la migrazione delle etichette e quindi creare criteri per le etichette nel Centro sicurezza e conformità di Office 365. Al termine, l'esempio verrà eseguito correttamente.|
