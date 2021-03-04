---
title: "Concetti: i concetti di base in MIP SDK, ovvero le autorizzazioni definite dall'utente."
description: Questo articolo consente di comprendere il concetto di Core SDK, denominato autorizzazioni definite dall'utente.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/02/2021
ms.author: tommos
ms.openlocfilehash: 47939a37616173c456d1588e95e36f8a978ed32d
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844184"
---
# <a name="microsoft-information-protection-sdk---user-defined-permissions"></a>Microsoft Information Protection SDK-autorizzazioni definite dall'utente

Microsoft Information Protection SDK supporta due tipi principali di autorizzazioni basate su etichetta, ovvero basate su modelli e definite dall'utente.

- **Autorizzazioni basate su modelli:** Questi diritti sono definiti dall'amministratore delle etichette in Security and Compliance Center. Queste etichette sono gestite centralmente e le modifiche apportate alla configurazione avranno un effetto sugli utenti che dispongono già di copie dei file. Se, ad esempio, l'amministratore rimuove un utente dall'elenco di utenti autorizzati, l'utente non potrà più accedere ai dati protetti alla successiva esecuzione del tentativo di recupero di una licenza.

- **Autorizzazioni definite dall'utente**: questi diritti vengono definiti **al momento dell'etichettatura** da parte dell'utente finale o dell'applicazione. Le autorizzazioni vengono passate all'SDK MIP sotto forma di una raccolta di mapping da utente a ruolo o da utenti a diritti. Questi diritti vengono scritti nella licenza di pubblicazione per il documento protetto e, a differenza delle autorizzazioni basate su modelli, non possono essere gestiti o modificati centralmente dopo la condivisione senza l'accesso diretto e la modifica del documento.

## <a name="users-rights-and-roles"></a>Utenti, diritti e ruoli

Poiché si prevede che i diritti verranno definiti dall'utente al momento dell'assegnazione di etichette, l'applicazione deve fornire un'interfaccia per consentire all'utente o al servizio di fornire input sugli indirizzi di posta elettronica e i diritti o i ruoli che l'utente avrà. Questa configurazione viene eseguita passando una raccolta di `UserRoles` `UserRights` oggetti o che definiscono in modo specifico chi deve avere il livello di accesso ai documenti.

```csharp
// Create a List<string> of the first set of permissions. 
List<string> users = new List<string>()
{
    "alice@contoso.com",
    "bob@contoso.com"
};

// Create a List<string> of the Rights the above users should have. 
List<string> rights = new List<string>()
{
    Rights.View,
    Rights.Edit                
};

// Create a UserRights object containing the defined users and rights.
UserRights userRights = new UserRights(users, rights);

// Add them to a new List<UserRights>
List<UserRights> userRightsList = new List<UserRights>()
{
    userRights
};
```

Il risultato è che si avrà una `List<UserRights>` raccolta che specifica che Alice e Bob hanno la visualizzazione e la modifica del file protetto. Per aggiungere altri utenti con un *diverso* set di autorizzazioni, è necessario ripetere il processo per creare un secondo `UserRights` oggetto, passando i nuovi utenti e autorizzazioni, quindi aggiungere alla raccolta chiamando `List<UserRights>` `userRightsList.Add(userRights2)` .

Questo modello è valido anche per `UserRoles` e può essere implementato semplicemente sostituendo **i diritti con i** **ruoli** e creando una `List<UserRoles>` raccolta.

### <a name="apply-protection"></a>Applicare la protezione

Per ottenere l'impostazione della protezione è possibile creare un `ProtectionDescriptor` `List<UserRights>` oggetto dall' `List<UserRoles>` oggetto o, quindi passarlo a `FileHandler.SetProtection()` . Infine, eseguire il commit della modifica apportata al file per scrivere un nuovo file. 

### <a name="when-to-apply-protection-to-files"></a>Quando applicare la protezione ai file

Quando si imposta un'etichetta tramite `FileHandler.SetLabel()` MIP SDK, è sufficiente eseguire un'azione e applicare qualsiasi protezione. Quando l'etichetta è configurata per le autorizzazioni definite dall'utente (UDP), l'applicazione non è in grado di stabilire in anticipo che l'etichetta è un'etichetta UDP. L'SDK MIP mette in superficie queste informazioni generando un'eccezione del tipo `Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException` . Il `FileHandler` codice deve rilevare questa eccezione, quindi attivare l'interfaccia utente o del servizio per definire le autorizzazioni personalizzate. Al termine, sarà possibile impostare la protezione. Nell'esempio seguente viene illustrato il modello end-to-end, ma si presuppone che sia già stata implementata una funzione per la compilazione dell' `List<UserRights>` oggetto.

```csharp
try
{
    // Attempt to set the label. If it's a UDP label, this will throw. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());
}

catch (Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException)
{
    // Assumes you've create a function that returns the List<UserRights> as previously detailed. 
    List<UserRights> userRightsList = GetUserRights();

    // Create a ProtectionDescriptor using the set of UserRights.
    ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(userRightsList);
    
    // Apply protection to the file using the new ProtectionDescriptor. 
    handler.SetProtection(protectionDescriptor, new ProtectionSettings());

    // Set the label. This will now succeed as protection has been defined. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());

    // Commit the change. 
    var result = Task.Run(async () => await handler.CommitAsync("myFileOutput.xlsx")).Result;
}
```

## <a name="custom-protection"></a>Protezione personalizzata

Questo processo può essere utilizzato anche per impostare solo la protezione impostando la protezione e ignorando il `SetLabel()` passaggio. Se l'applicazione non deve applicare un'etichetta, il gestore di eccezioni non è necessario e la protezione può essere impostata seguendo il `ProtectionDescriptor`  ->  `SetProtection()`  ->  `CommitAsync()` modello.

## <a name="next-steps"></a>Passaggi successivi

- [Esaminare la configurazione della crittografia delle etichette nella documentazione di Microsoft 365.](/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide#understand-how-the-encryption-works)