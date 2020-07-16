---
title: Ripubblicazione in MIP SDK
description: Questo articolo consente di comprendere lo scenario di utilizzo del gestore protezione per gli scenari di ripubblicazione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 499e4881175920fdf3127856fa9056b10ae22b79
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2020
ms.locfileid: "86405209"
---
# <a name="republishing-c"></a>Ripubblicazione (C++)

## <a name="overview"></a>Panoramica

Questa panoramica è incentrata sulla ripubblicazione in MIP SDK è uno scenario specifico rilevato quando un'applicazione deve consentire a un utente di modificare il file, ma desidera mantenere le informazioni di [licenza di pubblicazione](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/licenses-and-certificates-and-how-ad-rms-protects-and-consumes/ba-p/247309) originali su proprietario, diritti, chiave simmetrica e così via.

Il modello può avere un aspetto simile al seguente:

- Un utente apre un documento protetto per la modifica.
- L'utente deve essere autorizzato a modificare il file solo se gli è stato concesso il diritto appropriato.
- L'utente modifica e quindi Salva il documento.

Lo pseudocodice SDK MIP per completare questa attività può avere un aspetto simile al seguente:

- Creare un oggetto `mip::FileHandler` che punti al file di destinazione.
- Archiviare l'oggetto `mip::ProtectionHandler` esposto dal `mip::FileHandler` `GetProtection()` metodo di.
- Verificare che l'utente disponga dei diritti di **modifica** chiamando il `AccessCheck()` metodo.
- Usare `mip::FileHandler` `GetDecryptedTemporaryFileAsync()` o `GetDecryptedTemporaryStreamAsync()` per ottenere un output decrittografato temporaneo.
- Modificare il contenuto del flusso o del file temporaneo e salvarlo.
- Creare una nuova `mip::FileHandler` istanza di che punta al file temporaneo e usare il `SetProtection()` metodo, specificando l'oggetto archiviato `mip::ProtectionHandler` come parametro.
- Eseguire il commit della modifica.

Utilizzando il `mip::ProtectionHandler` dal file originale, il proprietario, l'ID contenuto, la chiave simmetrica e così via verranno mantenuti nel documento modificato. Questo scenario di ripubblicazione richiede che l'applicazione mantenga un riferimento all'originale `mip::ProtectionHandler` .

## <a name="implementation"></a>Implementazione

Come illustrato in precedenza, la `mip::FileHandler` classe espone metodi per la lettura, la scrittura e la rimozione di etichette e informazioni di protezione. Per l'elenco completo delle operazioni supportate, vedere le informazioni di [riferimento sulle API](./reference/class_mip_filehandler.md#summary).

In questo scenario vengono utilizzati i metodi seguenti `mip::FileHandler` :

- `GetProtection()`
- `CommitAsync()`
- `GetDecryptedTemporaryFileAsync()`
- `SetProtection()`

Lo scenario usa inoltre `mip::ProtectionHandler` , che espone le funzioni per la crittografia e la decrittografia di flussi e buffer protetti, l'esecuzione di controlli di accesso, la concessione della licenza di pubblicazione e il recupero degli attributi dalle informazioni protette. Il `AccessCheck()` metodo verrà usato per verificare che l'utente disponga dei diritti necessari per la modifica del file.

Per completare correttamente questo scenario di riprotezione, rivedere le guide introduttive in ' passaggi successivi ' e assicurarsi che l'applicazione venga compilata e possa elencare correttamente le etichette.

## <a name="create-a-protection-handler-from-the-file-and-decrypt-the-file"></a>Creare un gestore protezione dal file e decrittografare il file

`mip::ProtectionHandler`espone le funzioni per la crittografia e la decrittografia di flussi e buffer protetti, l'esecuzione di controlli di accesso, la concessione della licenza di pubblicazione e il recupero degli attributi dalle informazioni protette. `mip::ProtectionHandler`gli oggetti vengono costruiti fornendo una licenza di pubblicazione ProtectionDescriptor o serializzata. Per questo caso d'uso, la licenza di pubblicazione verrà usata in modo implicito quando si esegue la decrittografia di contenuto già protetto o quando si protegge il contenuto in cui è già stata costruita la licenza.

`mip::FileHandler`espone un metodo denominato `GetProtection()` che recupera `mip::ProtectionHandler` dal file associato a `mip::FileHandler` . Una volta `mip::ProtectionHandler` recuperato, l'oggetto può essere usato per convalidare i livelli di accesso dell'utente per il file, decrittografare il file e crittografare successivamente il file dopo che è stato modificato.

`mip::ProtectionHandler``AccessCheck()`viene usato per verificare che l'utente disponga di un diritto specifico per il file e restituisce una risposta booleana, a seconda del risultato. Per verificare, ad esempio, che l'utente disponga dei diritti per la modifica, chiamare il metodo passando il valore "EDIT". Se il risultato è *true*, consentire all'utente di modificare il file. Una volta verificato il diritto di **modifica** , `mip::FileHandler` utilizzare `GetDecryptedTemporaryFileAsync()` per recuperare il file temporaneo decrittografato.

Per ulteriori informazioni sui diversi diritti utente, consultare [i diritti utente per Azure Information Protection](/azure/information-protection/configure-usage-rights).

 > [!IMPORTANT]
 > I controlli di accesso e l'imposizione sono esclusivamente allo sviluppatore di applicazioni. Un utente con diritti di visualizzazione è in grado di decrittografare le informazioni protette. Spetta all'applicazione convalidare il set di diritti concessi all'utente e applicare tali diritti tramite controlli di protezione delle informazioni, ad esempio impedendo la copia, la modifica o l'acquisizione di schermate. L'impossibilità di implementare correttamente i controlli di protezione può comportare l'esposizione di informazioni riservate.

## <a name="save-and-publish-the-edited-file-by-applying-protection"></a>Salvare e pubblicare il file modificato applicando la protezione

Dopo la decrittografia del file, il file può essere modificato. Al termine dell'operazione di modifica, è possibile eseguire il commit delle modifiche. Creare un `IFileHandler` oggetto utilizzando il file temporaneo sopra riportato per gestire il file di cui è stato eseguito il commit. Il file temporaneo può quindi essere protetto utilizzando l' `IProtectionHandler` oggetto recuperato dal file originale.

## <a name="next-steps"></a>Passaggi successivi

- [Esaminare la Guida introduttiva di ripubblicazione per C++](quick-file-republishing-cpp.md)
- [Esaminare la Guida introduttiva di ripubblicazione per C #](quick-file-republishing-csharp.md)