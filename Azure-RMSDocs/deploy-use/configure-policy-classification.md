---
title: Configurare le condizioni per un'etichetta di Azure Information Protection
description: "Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: ef84f3ceb8f732dd475b4db8eae489e715d4b7da
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection

>*Si applica a: Azure Information Protection*

Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata: 

- La classificazione automatica si applica a Word, Excel e PowerPoint quando i file vengono salvati e si applica a Outlook quando i messaggi di posta elettronica vengono inviati. Non è possibile usare la classificazione automatica per i file che sono stati etichettati manualmente in precedenza.
 
- La classificazione consigliata si applica a Word, Excel e PowerPoint quando i file vengono salvati.

Quando si configurano le condizioni è possibile usare schemi predefiniti, come **Numero della carta di credito** o **USA Social Security Number (SSN)** (Social Security Number - USA). In alternativa, è possibile definire una stringa o un modello personalizzato come condizione per la classificazione automatica. Queste condizioni si applicano al corpo del testo nei documenti e nei messaggi di posta elettronica, alle intestazioni e ai piè di pagina. Per altre informazioni sulle condizioni, vedere la sezione [Dettagli sui tipi di informazioni](#details-about-the-information-types).

Come vengono valutate più condizioni quando si applicano a più etichette:

1. Le etichette sono ordinate per la valutazione, in base alla relativa posizione specificata nel criterio: l'etichetta posizionata per prima occupa la posizione più bassa (minore riservatezza) e l'etichetta posizionata per ultima occupa la posizione più alta (massima riservatezza).

2. Viene applicata l'etichetta per la massima riservatezza.
 
3. Viene applicata l'ultima etichetta secondaria.

> [!TIP]
>Per ottenere la migliore esperienza utente e garantire la continuità aziendale, è consigliabile iniziare con la classificazione consigliata dall'utente anziché quella automatica. Con questa configurazione, gli utenti possono accettare l'azione di etichettatura o protezione o ignorare questi suggerimenti se non sono adatti al messaggio di posta elettronica o documento in questione.

Ecco un esempio di richiesta quando si configura una condizione per l'applicazione di un'etichetta come azione consigliata, con un suggerimento di criterio personalizzato:

![Rilevamento e indicazione di Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

In questo esempio l'utente può fare clic su **Change now** (Cambia adesso) per applicare l'etichetta consigliata oppure ignorare il suggerimento selezionando **Dismiss** (Ignora).

## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Per configurare la classificazione consigliata o automatica per un'etichetta

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza. Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se l'etichetta da configurare viene applicata a tutti gli utenti, restare nel pannello **Azure Information Protection - Criteri globali**.
    
    Se l'etichetta da configurare si trova in un [criterio con ambito](configure-policy-scope.md) in modo da essere applicata solo agli utenti selezionati, nel menu **CRITERI** selezionare **Criteri con ambito**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

3. Nel pannello **Azure Information Protection - Criteri globali** o nel pannello **Criteri:\<nome>** selezionare l'etichetta da configurare. 

4. Nel pannello **Etichetta**, nella sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**, fare clic su **Aggiungi una nuova condizione**.

5. Nel pannello **Condizione** selezionare **Tipi di informazioni** se si vuole usare una condizione predefinita oppure **Personalizzata** se si vuole specificare una condizione personalizzata, quindi fare clic su **Salva**:
    - Per **Tipi di informazioni** selezionare una delle condizioni disponibili nell'elenco, quindi selezionare il numero minimo di occorrenze e specificare se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        Per disporre dell'elenco completo di condizioni è necessario usare la versione di anteprima corrente del client Azure Information Protection. Se si usa la versione di disponibilità generale corrente del client sono supportate solo le cinque condizioni seguenti: **Codice SWIFT**, **Numero della carta di credito**, **ABA Routing Number** (Codice ABA), **USA Social Security Number (SSN)** (Numero di previdenza sociale USA - SSN) e **International Banking Account Number (IBAN)**. [Altre informazioni](#details-about-the-information-types)
    
    - Per **Custom** (Personalizzata), specificare un nome e una frase di cui cercare la corrispondenza, esclusi i punti interrogativi e i caratteri speciali. Quindi specificare se usare un'espressione regolare per la corrispondenza, se la distinzione tra maiuscole e minuscole è rilevante, il numero minimo di occorrenze e se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        Se si dispone della versione di anteprima corrente del client Azure Information Protection, le espressioni regolari usano i criteri delle espressione regolari di Office 365. Per altre informazioni, vedere [Definizione di corrispondenze basate su espressioni regolari](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2) nella documentazione di Office. 
        
    **Esempio sulle opzioni relative alle occorrenze**: si seleziona l'opzione predefinita del codice fiscale e si imposta il numero minimo di occorrenze su 2 e in un documento compare due volte lo stesso codice fiscale. Se si imposta **Conta solo le occorrenze con valori univoci** su **Sì**, la condizione non è soddisfatta. Se invece si imposta questa opzione su **No**, la condizione è soddisfatta.

6. Nel pannello **Etichetta** configurare le opzioni seguenti e quindi fare clic su **Salva**:
    
    - Scegliere la classificazione automatica o consigliata: per **Select how this label is applied: automatically or recommended to user** (Selezionare come applicare l'etichetta: automaticamente o consigliata all'utente) selezionare **Automatic** (Automatica) o **Recommended** (Consigliata).
    
    - Specificare il testo per la richiesta utente o il suggerimento di criteri: mantenere il testo predefinito o specificare una stringa personalizzata.

7. Per mettere le modifiche a disposizione degli utenti, nel pannello iniziale di **Azure Information Protection** fare clic su **Publish** (Pubblica).

## <a name="details-about-the-information-types"></a>Dettagli sui tipi di informazioni

Se si dispone della versione di anteprima corrente del client Azure Information Protection è supportato l'elenco completo dei tipi di informazioni, nonché l'uso dei tipi di informazioni riservate e del rilevamento di modelli della prevenzione perdita dei dati (DLP) di Office 365. È possibile scegliere tra vari tipi di informazioni riservate comuni. Alcuni tipi sono specifici per determinate aree. Per altre informazioni, vedere [Elementi cercati dai tipi di informazioni riservate](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b) nella documentazione di Office. Quando Azure Information Protection valuta questi tipi di informazioni non usa l'impostazione del livello di attendibilità DLP di Office, ma ricerca corrispondenze in base al livello di attendibilità più basso.  

Se si dispone della versione di disponibilità generale corrente del client sono supportati solo i seguenti tipi di informazioni:

- [Codice SWIFT](#swift-code )

- [Numero di carta di credito](#credit-card-number )

- [ABA Routing Number (Codice ABA)](#aba-routing-number )

- [USA Social Security Number (SSN) (Numero di previdenza sociale USA - SSN)](#usa-social-security-number-ssn)

- [International Banking Account Number (IBAN)](#international-banking-account-number-iban)

Vedere le sezioni seguenti per altre informazioni su ciascun tipo di informazioni nella versione di disponibilità generale corrente del client.

### <a name="swift-code"></a>Codice SWIFT

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


### <a name="credit-card-number"></a>Numero di carta di credito

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

### <a name="aba-routing-number"></a>ABA Routing Number (Codice ABA)

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

### <a name="usa-social-security-number-ssn"></a>USA Social Security Number (SSN) (Numero di previdenza sociale USA - SSN)

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

### <a name="international-banking-account-number-iban"></a>International Banking Account Number (IBAN)

Viene trovata la corrispondenza con questo tipo di informazioni quando il contenuto include quanto segue:  

1. La frase seguente: **IBAN** 

2. Un codice IBAN: inizia con un codice paese (due lettere), seguito da cifre di verifica (due cifre), quindi dal numero BBAN (fino a un massimo di 30 cifre).


Esempi per il test:

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


