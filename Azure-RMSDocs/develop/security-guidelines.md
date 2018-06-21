---
title: Procedure ottimali di sicurezza | Microsoft Information Protection
description: È preferibile creare le applicazioni abilitate per RMS usando le procedure consigliate di Azure Information Protection.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.technology: techgroup-identity
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 6c3669c1ada24afcf3b9ec48ea5bb9c38939b47e
ms.sourcegitcommit: 8e622a93ff8d07a180e3be6e8b14748354e640bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2018
ms.locfileid: "30258776"
---
# <a name="security-best-practices-for-azure-information-protection"></a>Procedure ottimali di sicurezza per Azure Information Protection

L'SDK (Software Development Kit) di Azure Information Protection (AIP) rappresenta un solido sistema per la pubblicazione e l'utilizzo di informazioni protette di ogni tipo. Per rendere un sistema AIP il più sicuro possibile, tutte le applicazioni abilitate per AIP devono essere create usando le procedure consigliate di AIP. Tutte le applicazioni abilitate per AIP condividono la responsabilità di aiutare a mantenere la sicurezza di questo ecosistema. Identificare i rischi per la sicurezza e fornire soluzioni correttive per tali rischi introdotti durante lo sviluppo delle applicazioni aiuta a ridurre al minimo la possibilità di un'implementazione del software meno sicura.

Le procedure consigliate per l'implementazione delle applicazioni con l'SDK di Azure Information Protection includono le seguenti categorie di suggerimenti:
- [Modelli di minacce e strategie di riduzione del rischio](https://msdn.microsoft.com/library/aa362751.aspx)
- [Attacchi alla sicurezza](https://msdn.microsoft.com/library/aa362736.aspx)

Queste informazioni integrano il contratto che deve essere firmato per ottenere i certificati digitali necessari a implementare applicazioni usando l'SDK AIP.

## <a name="subjects-not-covered-in-these-topics"></a>Temi non trattati in questi argomenti
Questi argomenti descrivono brevemente i seguenti problemi, che sono significativi quando si prova a creare contemporaneamente un ambiente di sviluppo e un'applicazione protetta:
- **Gestione dei processi di sviluppo software**: include informazioni sulla gestione della configurazione, la protezione del codice sorgente, la riduzione degli accessi al codice sottoposto a debug e l'assegnazione di priorità ai bug. Per alcuni dei clienti, avere un processo di sviluppo software più sicuro è di fondamentale importanza. Alcuni clienti prevedono anche un processo di sviluppo.
- **Errori di codifica comuni**: include informazioni su come evitare i sovraccarichi del buffer. Si consiglia di leggere la versione più recente di Writing Secure Code di Michael Howard e David LeBlanc (Microsoft Press, 2002) per esaminare queste minacce generiche e le relative strategie risolutive.
- **Ingegneria sociale**: include informazioni sulle misure di sicurezza procedurali e strutturali che aiutano a proteggere contro lo sfruttamento di codice da parte degli sviluppatori o di altri utenti all'interno dell'organizzazione del produttore.
- **Sicurezza fisica**: include informazioni sul blocco dell'accesso alla base di codice e ai certificati di firma.
- **Implementazione o distribuzione del software preliminare**: include informazioni sulla distribuzione del software beta.
- **Gestione della rete**: include informazioni sui sistemi di rilevamento delle intrusioni nelle reti fisiche.

## <a name="threat-models-and-mitigations"></a>Modelli di minacce e strategie di riduzione del rischio
I proprietari di informazioni digitali devono saper valutare gli ambienti in cui verranno decrittografate le proprie risorse. Una dichiarazione di standard minimi di sicurezza può fornire ai proprietari di informazioni un framework con cui comprendere e valutare il livello di sicurezza delle applicazioni a cui affidano le loro informazioni.

Alcuni settori, ad esempio enti pubblici e assistenza sanitaria, prevedono processi e standard di certificazione e accreditamento che potrebbero essere applicati al proprio prodotto. Rispettare queste indicazioni minime di sicurezza non sostituisce le esigenze di accreditamento univoche dei clienti. Tuttavia, lo scopo degli standard di sicurezza è aiutare a prepararsi per le esigenze dei clienti attuali e futuri e l'applicazione trarrà vantaggio da qualsiasi investimento eseguito all'inizio del ciclo di sviluppo. Si tratta di indicazioni, non di un programma di certificazione formale offerto da Microsoft.

Esistono diverse categorie principali di vulnerabilità in un sistema Rights Management Services, ad esempio:
- **Fuga di dati**: le informazioni vengono visualizzate in posizioni non autorizzate.
- **Danneggiamento**: il software o i dati vengono modificati in modo non autorizzato.
- **Negazione**: una risorsa di elaborazione non è disponibile per l'uso.

Questi argomenti riguardano principalmente i problemi di fuga di dati. L'integrità di un sistema API dipende dalla capacità, nel corso del tempo, di proteggere le informazioni, consentendo l'accesso solo alle entità designate. Questi argomenti accennano anche ai problemi di danneggiamento. I problemi di negazione non sono invece trattati.

Microsoft non testa o esamina i risultati dei test relativi al rispetto degli standard minimi; spetta al partner assicurarsi che siano soddisfatti gli standard minimi. Microsoft offre due livelli aggiuntivi di consigli per ridurre le minacce più comuni. In generale, si tratta di suggerimenti supplementari; ad esempio rispettare le indicazioni preferite presuppone che siano stati soddisfatti gli standard minimi, ove possibile, se non diversamente specificato.

|Livello standard|    Descrizione|
|---|---|
|Standard minimo|  Un'applicazione che gestisce le informazioni protette da AIP deve essere determinata in modo da rispettare lo standard minimo prima che l'applicazione possa essere firmata con il certificato di produzione ricevuto da Microsoft. I partner in genere usano il certificato di gerarchia di produzione solo al momento del rilascio della versione finale del software, quando i test interni hanno già verificato che l'applicazione soddisfa tale standard minimo. Soddisfare lo standard minimo non costituisce, né può essere interpretato come, una garanzia di sicurezza da parte di Microsoft. Microsoft non testa o esamina i risultati dei test relativi al rispetto degli standard minimi; spetta al partner assicurarsi che siano soddisfatti gli standard minimi.|
|Standard consigliato|  Le linee guida consigliate tracciano un percorso alla migliorata sicurezza delle applicazioni e forniscono un'indicazione di come AIP potrebbe evolvere con l'implementazione di altri criteri di sicurezza. I fornitori potrebbero tentare di differenziare le proprie applicazioni creandole in base a questo livello più elevato di sicurezza.|
|Standard preferito|    Questa è la categoria più elevata di sicurezza attualmente definita. I fornitori che sviluppano applicazioni commercializzate come estremamente sicure devono puntare a questo standard. Le applicazioni che rispettano questo standard possono risultare meno vulnerabili agli attacchi.|




## <a name="malicious-software"></a>Software dannoso
Microsoft ha definito gli standard minimi obbligatori che l'applicazione deve soddisfare per proteggere il contenuto da software dannoso.

### <a name="importing-malicious-software-by-using-address-tables"></a>Importazione di software dannoso con le tabelle degli indirizzi
AIP non supporta la modifica del codice in fase di esecuzione o la modifica della tabella di indirizzi di importazione (IAT). Viene creata una tabella di indirizzi di importazione per ogni DLL caricata nello spazio di processo. Specifica gli indirizzi di tutte le funzioni che l'applicazione importa. Un attacco comune consiste nel modificare le voci della tabella IAT all'interno di un'applicazione, ad esempio in modo da puntare a software dannoso. AIP arresta l'applicazione quando rileva questo tipo di attacco.

### <a name="minimum-standard"></a>Standard minimo
- Non è possibile modificare la tabella di indirizzi di importazione nel processo applicativo durante l'esecuzione. L'applicazione specifica molte delle funzioni chiamate in fase di esecuzione usando le tabelle degli indirizzi e queste non possono essere modificate durante o dopo la fase di esecuzione. Tra le altre cose, ciò significa che non è possibile eseguire la profilatura del codice in un'applicazione firmata con il certificato di produzione.
- Non è possibile chiamare la funzione **DebugBreak** all'interno di qualsiasi DLL specificata nel manifesto.
- Non è possibile chiamare **LoadLibrary** con il flag **DONT_RESOLVE_DLL_REFERENCES** impostato. Questo flag indica al caricatore di ignorare l'associazione ai moduli importati, modificando di conseguenza la tabella IAT.
- Non è possibile modificare il caricamento ritardato apportando modifiche in fase di esecuzione o successive all'opzione /DELAYLOAD del linker.
- Non è possibile modificare il caricamento ritardato fornendo la propria versione della funzione Delayimp.lib dell'helper.
- Non è possibile scaricare i moduli a caricamento ritardato da moduli autenticati in presenza dell'ambiente AIP.
- Non è possibile usare l'opzione **/DELAY:UNLOAD** del linker per abilitare lo scaricamento dei moduli ritardati.


## <a name="incorrectly-interpreting-license-rights"></a>Errata interpretazione dei diritti di licenza

Se l'applicazione non interpreta né applica correttamente i diritti espressi nella licenza di pubblicazione di AIP, le informazioni potrebbero essere rese disponibili in modi non previsti dal proprietario. Un esempio è un'applicazione che consente a un utente di salvare informazioni non crittografate in nuovi supporti quando la licenza di pubblicazione conferisce unicamente il diritto di visualizzarle.

Il sistema AIP organizza i diritti in pochi raggruppamenti. Per altre informazioni, vedere [Configurazione dei diritti di utilizzo per Azure Rights Management](../deploy-use/configure-usage-rights.md).

### <a name="azure-information-protection"></a>Azure Information Protection  
L'API consente a un utente di decrittografare o no le informazioni, che non hanno alcuna protezione inerente. Se un utente ha il diritto di decrittografare le informazioni, l'API lo permette e l'applicazione è responsabile della gestione o della protezione delle informazioni dopo che sono state messe al sicuro. Un'applicazione è responsabile della gestione del suo ambiente e della sua interfaccia al fine di impedire l'uso non autorizzato delle informazioni; ad esempio, la disattivazione dei pulsanti **Stampa** e **Copia** se una licenza concede solo il diritto di RIPRODUZIONE. Il gruppo di test dovrebbe verificare che l'applicazione agisca correttamente su tutti i diritti di licenza che riconosce.

### <a name="minimum-standard"></a>Standard minimo
- L'implementazione del cliente dei diritti di XrML v.1.2 dovrebbe essere coerente con le definizioni di questi diritti, come descritto nelle specifiche XrML, che sono disponibili nel sito Web di XrML (http://www.xrml.org)). Per tutte le entità che hanno un interesse per l'applicazione è necessario definire tutti i diritti che sono specifici di quest'ultima.
- Il gruppo e il processo di test dovrebbero verificare che l'applicazione venga eseguita correttamente rispetto ai diritti che supporta e che non agisca sui diritti non supportati.
- Se si sta creando un'applicazione di pubblicazione, è necessario rendere disponibili informazioni che spieghino quali diritti intrinseci sono supportati dall'applicazione di pubblicazione e quali non lo sono e in che modo occorre interpretarli. In aggiunta, l'interfaccia utente dovrebbe chiarire all'utente finale quali sono le implicazioni di ogni diritto concesso o negato a una singola informazione.

- Eventuali diritti che vengono ricavati per inclusione nei nuovi diritti implementati da un'applicazione devono essere mappati alla nuova terminologia. Ad esempio, un nuovo diritto denominato GESTIONE potrebbe includere come diritti separati STAMPA, COPIA e MODIFICA.
Standard consigliato    Attualmente nessuno.
Standard preferito    Attualmente nessuno.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]