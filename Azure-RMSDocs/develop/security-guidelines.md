---
title: Procedure di sicurezza consigliate per Information Protection
description: È preferibile creare le applicazioni abilitate per RMS usando le procedure consigliate di Information Protection.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 12/13/2018
ms.topic: conceptual
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: c3a342dfa6be9640504bac4b44ef910534b1497d
ms.sourcegitcommit: c9a0d81c18ea79a2520baa4b3777b06a72f87f60
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53382453"
---
# <a name="security-best-practices-for-information-protection"></a>Procedure di sicurezza consigliate per Information Protection

L'SDK (Software Development Kit) di Information Protection offre un solido sistema per la pubblicazione e l'uso di informazioni protette di ogni tipo. Per rendere un sistema il più sicuro possibile, tutte le applicazioni abilitate per Information Protection devono essere create usando le procedure consigliate. Tutte le applicazioni condividono la responsabilità di aiutare a mantenere la sicurezza di questo ecosistema. Identificare i rischi per la sicurezza e fornire soluzioni correttive per tali rischi introdotti durante lo sviluppo delle applicazioni aiuta a ridurre al minimo la possibilità di un'implementazione del software meno sicura.

Queste informazioni integrano il contratto che deve essere firmato per ottenere i certificati digitali per le applicazioni usando gli SDK.

## <a name="subjects-not-covered"></a>Argomenti non trattati

Anche se gli argomenti seguenti offrono considerazioni importanti per la creazione di un ambiente di sviluppo e di applicazioni protette, esulano dall'ambito di questo articolo:

- **Gestione dei processi di sviluppo software**: gestione della configurazione, protezione del codice sorgente, riduzione degli accessi al codice sottoposto a debug e assegnazione di priorità ai bug. Per alcuni clienti avere un processo di sviluppo software più sicuro è di fondamentale importanza. Alcuni clienti prevedono anche un processo di sviluppo.
- **Errori di codifica comuni**: informazioni su come evitare i sovraccarichi del buffer. Si consiglia di leggere la versione più recente di Writing Secure Code di Michael Howard e David LeBlanc (Microsoft Press, 2002) per esaminare queste minacce generiche e le relative strategie risolutive.
- **Ingegneria sociale**: include informazioni sulle misure di sicurezza procedurali e strutturali che aiutano a proteggere il codice dallo sfruttamento da parte degli sviluppatori o di altri utenti all'interno dell'organizzazione del produttore.
- **Sicurezza fisica**: include informazioni sul blocco dell'accesso alla base di codice e ai certificati di firma.
- **Implementazione o distribuzione del software preliminare**: include informazioni sulla distribuzione del software beta.
- **Gestione della rete**: include informazioni sui sistemi di rilevamento delle intrusioni nelle reti fisiche.

## <a name="threat-models-and-mitigations"></a>Modelli di minacce e strategie di mitigazione dei rischi

I proprietari di informazioni digitali devono saper valutare gli ambienti in cui verranno decrittografate le proprie risorse. Una dichiarazione di standard minimi di sicurezza offre ai proprietari di informazioni un framework con cui comprendere e valutare il livello di sicurezza delle applicazioni.

Alcuni settori, ad esempio enti pubblici e assistenza sanitaria, prevedono processi e standard di certificazione e accreditamento che potrebbero essere applicati al proprio prodotto. Rispettare queste indicazioni minime di sicurezza non sostituisce le esigenze di accreditamento univoche dei clienti. Tuttavia, lo scopo degli standard di sicurezza è aiutare a prepararsi per le esigenze dei clienti attuali e futuri e l'applicazione trarrà vantaggio da qualsiasi investimento eseguito all'inizio del ciclo di sviluppo. Le indicazioni sono elementi consigliati e non costituiscono un programma di certificazione formale di Microsoft.

Esistono diverse categorie principali di vulnerabilità in un sistema Rights Management Services, ad esempio:

- **Fuga di dati**: le informazioni vengono visualizzate in posizioni non autorizzate.
- **Danneggiamento**: il software o i dati vengono modificati in modo non autorizzato.
- **Negazione**: una risorsa di elaborazione non è disponibile per l'uso.

Questi argomenti riguardano principalmente i problemi di fuga di dati. L'integrità di un sistema API dipende dalla capacità, nel corso del tempo, di proteggere le informazioni, consentendo l'accesso solo alle entità designate. Questi argomenti accennano anche ai problemi di danneggiamento. I problemi di negazione non sono trattati.

Microsoft non esegue test né analisi dei risultati dei test per verificare la conformità allo standard minimo. È responsabilità del partner verificare che siano soddisfatti gli standard minimi. Microsoft offre due livelli aggiuntivi di consigli per ridurre le minacce più comuni. In generale, si tratta di suggerimenti supplementari. Ad esempio, rispettare le indicazioni preferite presuppone che siano stati soddisfatti gli standard minimi, ove possibile, se non diversamente specificato.

|Livello standard|Descrizione|
|---|---|
|Standard minimo| Un'applicazione che gestisce le informazioni protette deve rispettare lo standard minimo per poter essere firmata con il certificato di produzione ricevuto da Microsoft. I partner in genere usano il certificato di gerarchia di produzione al momento del rilascio della versione finale del software. I test interni di un partner vengono usati per verificare se l'applicazione soddisfa lo standard minimo. Soddisfare lo standard minimo non costituisce, né può essere interpretato come, una garanzia di sicurezza da parte di Microsoft. Microsoft non esegue test né analisi dei risultati dei test per verificare la conformità allo standard minimo. È responsabilità del partner verificare che siano soddisfatti i requisiti minimi.|
|Standard consigliato| Le linee guida consigliate consentono di ottimizzare la sicurezza delle applicazioni e offrono un'indicazione di come l'SDK potrebbe evolvere con l'implementazione di altri criteri di sicurezza. I fornitori possono differenziare le proprie applicazioni creandole in base a questo livello più elevato di sicurezza.|
|Standard preferito| Questo standard è la categoria più elevata di sicurezza attualmente definita. I fornitori che sviluppano applicazioni commercializzate come estremamente sicure devono puntare a questo standard. Le applicazioni che rispettano questo standard possono risultare meno vulnerabili agli attacchi.|

## <a name="malicious-software"></a>Software dannoso

Microsoft ha definito gli standard minimi obbligatori che l'applicazione deve soddisfare per proteggere il contenuto da software dannoso.

### <a name="importing-malicious-software-by-using-address-tables"></a>Importazione di software dannoso con le tabelle degli indirizzi

Information Protection SDK non supporta la modifica del codice in fase di esecuzione o la modifica della tabella di indirizzi di importazione (IAT). Viene creata una tabella di indirizzi di importazione per ogni DLL caricata nello spazio di processo. Specifica gli indirizzi di tutte le funzioni che l'applicazione importa. Un attacco comune consiste nel modificare le voci della tabella IAT all'interno di un'applicazione, ad esempio in modo da puntare a software dannoso. L'SDK arresta l'applicazione quando rileva questo tipo di attacco.

### <a name="minimum-standard"></a>Standard minimo

- Non è possibile modificare la tabella di indirizzi di importazione nel processo applicativo durante l'esecuzione. L'applicazione specifica molte delle funzioni chiamate in fase di esecuzione usando le tabelle degli indirizzi. Le tabelle non possono essere modificate durante o dopo la fase di esecuzione. Tra le altre cose, questa restrizione implica che non è possibile eseguire la profilatura del codice in un'applicazione firmata con il certificato di produzione.
- Non è possibile chiamare la funzione **DebugBreak** all'interno di qualsiasi DLL specificata nel manifesto.
- Non è possibile chiamare **LoadLibrary** con il flag **DONT_RESOLVE_DLL_REFERENCES** impostato. Questo flag indica al caricatore di ignorare l'associazione ai moduli importati, modificando di conseguenza la tabella IAT.
- Non è possibile modificare il caricamento ritardato apportando modifiche durante o dopo la fase di esecuzione all'opzione /DELAYLOAD del linker.
- Non è possibile modificare il caricamento ritardato specificando la propria versione della funzione Delayimp.lib dell'helper.
- Non è possibile scaricare i moduli a caricamento ritardato da moduli autenticati in presenza dell'ambiente Information Protection SDK.
- Non è possibile usare l'opzione **`/DELAY:UNLOAD`** del linker per abilitare lo scaricamento dei moduli ritardati.

## <a name="incorrectly-interpreting-license-rights"></a>Errata interpretazione dei diritti di licenza

Se l'applicazione non interpreta né applica correttamente i diritti espressi nella licenza di pubblicazione dell'SDK, è possibile che le informazioni vengano rese disponibili in modi non previsti dal proprietario. Questo si verifica, ad esempio, se un'applicazione consente a un utente di salvare informazioni non crittografate in nuovi supporti quando la licenza di pubblicazione conferisce unicamente il diritto di visualizzarle.

### <a name="azure-information-protection-aip"></a>Azure Information Protection (AIP)

Il sistema di protezione delle informazioni consente di organizzare i diritti in pochi raggruppamenti. Per altre informazioni, vedere [Configurazione dei diritti di utilizzo per Azure Rights Management](../configure-usage-rights.md).

AIP consente a un utente di decrittografare o meno le informazioni. Le informazioni non hanno una protezione intrinseca. Se un utente ha il diritto di decrittografare le informazioni, l'API lo consente. L'applicazione è responsabile della gestione o della protezione delle informazioni dopo che sono state messe al sicuro. Un'applicazione è responsabile della gestione del proprio ambiente e dell'interfaccia per impedire l'uso non autorizzato delle informazioni. Ad esempio, nel caso in cui vengano disattivati i pulsanti **Stampa** e **Copia** e una licenza conceda solo il diritto di visualizzazione. Il gruppo di test dovrebbe verificare che l'applicazione agisca correttamente su tutti i diritti di licenza che riconosce.

### <a name="minimum-standard"></a>Standard minimo

- L'implementazione del cliente dei diritti di XrML v.1.2 dovrebbe essere coerente con le definizioni di questi diritti, come descritto nelle specifiche XrML, che sono disponibili nel sito Web di XrML (http://www.xrml.org)). Per tutte le entità che hanno un interesse per l'applicazione è necessario definire tutti i diritti che sono specifici di quest'ultima.
- Il gruppo e il processo di test devono verificare che l'applicazione venga eseguita correttamente rispetto ai diritti che supporta e che **non** agisca in base a diritti non supportati.
- Se si sta creando un'applicazione di pubblicazione, è necessario rendere disponibili informazioni che spiegano i diritti intrinseci in uso, tra cui quelli che sono e non sono supportati dall'applicazione di pubblicazione, e come devono essere interpretati questi diritti. In aggiunta, l'interfaccia utente dovrebbe chiarire all'utente finale quali sono le implicazioni di ogni diritto concesso o negato a una singola informazione.
- Eventuali diritti che vengono ricavati per inclusione nei nuovi diritti implementati da un'applicazione devono essere mappati alla nuova terminologia. Ad esempio, un nuovo diritto denominato GESTIONE potrebbe includere come diritti separati STAMPA, COPIA e MODIFICA.

### <a name="recommended-standard"></a>Standard consigliato

Nessuna in questo momento.

### <a name="preferred-standard"></a>Standard preferito

Nessuna in questo momento.

## <a name="next-steps"></a>Passaggi successivi

Le procedure consigliate per l'implementazione di applicazioni con AIP SDK includono gli articoli seguenti:

- [Modelli di minacce e strategie di riduzione del rischio](https://msdn.microsoft.com/library/aa362751.aspx)
- [Attacchi alla sicurezza](https://msdn.microsoft.com/library/aa362736.aspx)
