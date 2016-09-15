---
title: Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection | Azure Rights Management
description: "Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata."
manager: mbaldwin
ms.date: 08/29/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
translationtype: Human Translation
ms.sourcegitcommit: 87069b73e5f8959955b9967070bd3bcb5e7dc196
ms.openlocfilehash: 357b012bd8679d7e24bfe3ae40c3160e4b69c01f


---

# Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata: 

- La classificazione automatica si applica a Word, Excel e PowerPoint quando i file vengono salvati e si applica a Outlook quando i messaggi di posta elettronica vengono inviati. Non è possibile usare la classificazione automatica per i file che sono stati etichettati manualmente in precedenza.
 
- La classificazione consigliata si applica a Word, Excel e PowerPoint quando i file vengono salvati.

Quando si configurano le condizioni, è possibile usare schemi predefiniti, come numeri di carta di credito o codici fiscali. In alternativa, è possibile definire una stringa o un modello personalizzato come condizione per la classificazione automatica. Queste condizioni si applicano al corpo del testo nei documenti e nei messaggi di posta elettronica, alle intestazioni e ai piè di pagina. Per altre informazioni sulle condizioni, vedere la sezione [Informazioni dalle condizioni predefinite](#information-about-the-built-in-conditions).

Come vengono valutate più condizioni quando si applicano a più etichette:

1. Le etichette sono ordinate per la valutazione, in base alla relativa posizione specificata nel criterio: l'etichetta posizionata per prima occupa la posizione più bassa (minore riservatezza) e l'etichetta posizionata per ultima occupa la posizione più alta (massima riservatezza).

2. Viene applicata l'etichetta per la massima riservatezza.
 
3. Viene applicata l'ultima etichetta secondaria.

> [!TIP]
>Per ottenere la migliore esperienza utente e garantire la continuità aziendale, è consigliabile iniziare con la classificazione consigliata dall'utente anziché quella automatica. Con questa configurazione, gli utenti hanno la possibilità di accettare l'azione di etichettatura o protezione o di ignorare questi suggerimenti se non sono adatti al messaggio di posta elettronica o documento in questione.

Ecco un esempio di richiesta quando si configura una condizione per l'applicazione di un'etichetta come azione consigliata, con un suggerimento di criterio personalizzato:

![Rilevamento e indicazione di Azure Information Protection](../media/info-protect-recommend-callouts.png)

In questo esempio l'utente può fare clic su **Change now** (Cambia adesso) per applicare l'etichetta consigliata oppure ignorare il suggerimento chiudendo la barra.

## Per configurare la classificazione consigliata o automatica per un'etichetta

1. Se non è già stato fatto, accedere al [portale di Azure](https://portal.azure.com) e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, nel menu hub fare clic su **Esplora** e iniziare a digitare **Information** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** selezionare l'etichetta da configurare per la classificazione automatica o suggerita.

3. Nel pannello **Etichetta**, nella sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**, fare clic su **Aggiungi una nuova condizione**.

4. Nel pannello **Condition** (Condizione) selezionare **Built-in** (Predefinita) se si vuole usare una condizione predefinita oppure **Custom** (Personalizzata) se si vuole specificare una condizione personalizzata, quindi fare clic su **Save** (Salva):

    - Per **Built-in** (Predefinita), selezionare una delle condizioni disponibili nell'elenco, quindi selezionare il numero minimo di occorrenze e specificare se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        Per altre informazioni sulle regole di rilevamento per queste condizioni e alcuni esempi, vedere la sezione [Informazioni sulle condizioni predefinite](#information-about-the-built-in-conditions).

    - Per **Custom** (Personalizzata), specificare un nome e una frase di cui cercare la corrispondenza, esclusi i punti interrogativi e i caratteri speciali. Quindi specificare se usare un'espressione regolare per la corrispondenza, se la distinzione tra maiuscole e minuscole è rilevante, il numero minimo di occorrenze e se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
    **Esempio sulle opzioni relative alle occorrenze**: si seleziona l'opzione predefinita del codice fiscale e si imposta il numero minimo di occorrenze su 2 e in un documento compare due volte lo stesso codice fiscale. Se si imposta **Conta solo le occorrenze con valori univoci** su **Sì**, la condizione non è soddisfatta. Se invece si imposta questa opzione su **No**, la condizione è soddisfatta.

5. Nel pannello **Etichetta** configurare le opzioni seguenti e quindi fare clic su **Salva**:

    - Scegliere la classificazione automatica o consigliata: per **Select how this label is applied: automatically or recommended to user** (Selezionare come applicare l'etichetta: automaticamente o consigliata all'utente) selezionare **Automatic** (Automatica) o **Recommended** (Consigliata).

    - Specificare il testo per la richiesta utente o il suggerimento di criteri: mantenere il testo predefinito o specificare una stringa personalizzata.

6. Per mettere le modifiche a disposizione degli utenti, nel pannello **Azure Information Protection** fare clic su **Publish** (Pubblica).

## Informazioni sulle condizioni predefinite

Durante il periodo di anteprima è possibile selezionare le condizioni seguenti:

- [Codice SWIFT](#swift-code )

- [Numero di carta di credito](#credit-card-number )

- [ABA Routing Number (Codice ABA)](#aba-routing-number )

- [USA Social Security Number (SSN) (Numero di previdenza sociale USA - SSN)](#usa-social-security-number-ssn)

- [International Banking Account Number (IBAN)](#international-banking-account-number-iban)


### Codice SWIFT

Viene trovata la corrispondenza con questo tipo di informazioni quando il contenuto include quanto segue:  

1. Una delle frasi seguenti: **swift**, **swiftnumber**, **swiftroutingnumber** 

2. Un codice Swift, in un modello formattato:  

    a. 4 lettere (codice della banca)  

    b. 2 lettere (codice del paese)  

    c. 2 lettere o cifre (codice località)  

    d. 3 lettere o cifre facoltative (codice filiale)  


Esempi per il test:

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### Numero di carta di credito

Viene trovata la corrispondenza con questo tipo di informazioni quando il contenuto include quanto segue:  

- Un numero di carta di credito valido, in un modello formattato o non formattato, che supera il [controllo di Luhn](https://wikipedia.org/wiki/Luhn_algorithm). Le informazioni di questo tipo rilevano le carte dei principali circuiti a livello mondiale, tra cui Visa, MasterCard, Discover Card, American Express e Diner.

    - **Formattato**:
    
        - 16 numeri: (nnnn-nnnn-nnnn-nnnn)  
        
    - **Non formattato**:
    
        - (nnnnnnnnnnnnnnnn)  


Esempi per il test:

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### ABA Routing Number (Codice ABA)

Viene trovata la corrispondenza con questo tipo di informazioni quando il contenuto include quanto segue:  

1. Almeno una delle frasi seguenti: **aba**, **rtn**, **routing number** 

2. Un codice ABA, che include 9 cifre in un modello formattato o non formattato: 

    - **Formattato**: 
        
        a. Quattro cifre che iniziano con 0, 1, 2, 3, 6, 7 o 8 
        
        b. Trattino 
        
        c. Quattro cifre 
        
        d. Trattino 
        
        e. Una cifra 
        
        Esempio: 3456-9876-1 ABA 
        
    - **Non formattato**: 
        
        9 cifre consecutive che iniziano con 0, 1, 2, 3, 6, 7 o 8 
        
        Esempio: 345698761 RTN 
 

Esempi per il test:

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### USA Social Security Number (SSN) (Numero di previdenza sociale USA - SSN)

Viene trovata la corrispondenza con questo tipo di informazioni quando il contenuto include quanto segue:  

1. Almeno una delle frasi seguenti: **ssn**, **social security**, **ssid**, **ss#** 

2. Un numero di previdenza sociale: 9 cifre, che possono essere in un modello formattato o non formattato:

    - **Formattato**: 
    
        - Nove cifre nel formato seguente: nnn-nn-nnnn OPPURE nnn nn nnnn 
        
    - **Non formattato**: 
    
        - Nove cifre nel formato seguente: nnnnnnnnn 


Esempi per il test:

- **SSN 123-45-6789**

- **SS# 123456789** 


----

### International Banking Account Number (IBAN)

Viene trovata la corrispondenza con questo tipo di informazioni quando il contenuto include quanto segue:  

1. La frase seguente: **IBAN** 

2. Un codice IBAN: inizia con un codice paese (due lettere), seguito da cifre di verifica (due cifre), quindi dal numero BBAN (fino a un massimo di 30 cifre).


Esempi per il test:

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organization-s-policy).  






<!--HONumber=Aug16_HO5-->


