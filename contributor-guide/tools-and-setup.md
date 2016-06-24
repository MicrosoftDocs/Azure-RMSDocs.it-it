<properties pageTitle="Installare e configurare gli strumenti di creazione in GitHub" description="Strumenti e passaggi di configurazione per la creazione di contenuto EMS in GitHub." services="contributor-guide" documentationCenter="" authors="v-jocgar" manager="robmazz" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="02/25/2016" ms.author="v-jocgar" />

# Installare e configurare gli strumenti di creazione in GitHub
Attività:
- [ ] #21 È necessario testare l'intera procedura con un account non Microsoft e un computer. 

Seguire i passaggi descritti in questo articolo per configurare gli strumenti per collaborare alla documentazione tecnica EMS. 

- Se non si ha familiarità con Git, è possibile rivedere parte della terminologia Git in [https://help.github.com/articles/github-glossary](https://help.github.com/articles/github-glossary).
- È anche consigliabile vedere questa serie di video relativi a [Git e Github Foundations](https://www.youtube.com/playlist?list=PLg7s6cbtAD15G8lNyoaYDuKZSKyJrgwB-). Si tratta di video brevi e di facile comprensione.  

## Istruzioni dettagliate

- [Creare un account GitHub e impostare il profilo](#create-a-github-account-and-set-up-your-profile)
- [Autorizzazioni in GitHub](#permissions-in-github)
- [Installare GIT per Windows](#install-git-for-windows)
- [Abilitare l'autenticazione a due fattori](#enable-two-factor-authentication)
- [Creare un token di accesso personale](#create-a-personal-access-token)
- [Installare un editor markdown](#install-a-markdown-editor)
- [Configurare Atom](#configure-atom)
- [Creare un ramo dal repository](#create-a-branch-from-the-repository)
- [Impostare la connessione al repository remoto e configurare le credenziali](#set-remote-repository-connection-and-configure-credentials)
- [Configurare il nome utente e la posta elettronica in locale](#configure-your-user-name-and-email-locally)
- [Passaggi successivi](#next-steps)

## Creare un account GitHub e impostare il profilo

Per collaborare al contenuto tecnico EMS, è necessario un account [GitHub](http://www.github.com).

- **Profile picture**: immagine dell'utente (obbligatorio)
- **Name**: nome e cognome (obbligatorio)
- **Email**: indirizzo di posta elettronica (obbligatorio)
- **Company**: società (obbligatorio)
- **Location**: specificare la posizione (obbligatorio)

Il profilo dovrebbe essere simile al seguente:

 ![Esempio di profilo GitHub](./media/githubprofile.png)

## Autorizzazioni in GitHub

Chiunque disponga di un account GitHub può collaborare al contenuto tecnico EMS tramite l'archivio pubblico disponibile in [http://www.github.com/microsoft/emdocs](http://www.github.com/microsoft/emdocs). Non sono necessarie autorizzazioni speciali.

## Installare GIT per Windows

Installare **GIT per Windows** da [http://git-scm.com/download/win](http://git-scm.com/download/win). Questo download installa il sistema di controllo di versione Git e Git Bash, l'applicazione della riga di comando da usare per interagire con il repository Git locale.

**Nota**
Questo programma non corrisponde a "Github per Windows". "Github for Windows" è uno strumento basato su GUI che consente anche di leggere argomenti su se stessi. [https://windows.github.com/](https://windows.github.com/)) 

Durante l'installazione è possibile selezionare la modalità di interazione con il repository Github. È consigliabile usare solo Git solo da Git Bash. 
 ![Esempio di profilo GitHub](./media/gitbashinstall.png)

## Abilitare l'autenticazione a due fattori

Se si usa il repository dei contenuti privati, è necessario abilitare l'autenticazione a due fattori (2FA) nell'account GitHub. A tale scopo, seguire le istruzioni dell'argomento della Guida di GitHub seguente:

- [Informazioni sull'autenticazione a due fattori](https://help.github.com/articles/about-two-factor-authentication/)

## Creare un token di accesso personale
Il token di accesso personale esegue l'autenticazione dell'utente e del computer in uso in GitHub.
1. In GitHub fare clic su se stessi, quindi fare clic su Settings.
2. Nella scheda Personal Access Token fare clic su Generate new token.
3. Specificare una descrizione per il token. 
4. Impostare l'ambito. Per un accesso completo al repository e all'utente si selezionano le caselle di controllo delle autorizzazioni.
5. Fare clic su Generate token.
6. Copiare il token visualizzato e incollarlo in una posizione sicura, ad esempio un messaggio di posta elettronica o un documento di Word. È necessario che il token esegua il pull e il push in GitHub.

## Installare un editor markdown

Il contenuto viene creato usando la semplice notazione "markdown" nei file anziché la complessa notazione "markup" (HTML, XML e così via). Per questo motivo è necessario installare un editor markdown. Viene usato il markdown specifico per Github. 

- **Atom**: la maggior parte dei collaboratori usa l'editor markdown di Atom per GitHub: [http://atom.io](http://atom.io). Non richiede una licenza per l'uso professionale e include il controllo ortografico. 
- **Blocco note**: è possibile usare Blocco note per un'opzione molto leggera.
- **Prose**: si tratta di un editor markdown leggero, elegante, online e open source che offre un'anteprima. Visitare [http://prose.io](http://prose.io) e autorizzare Prose nel repository.
- **[Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx)** - il programma Microsoft per questo contesto.
- **MarkdownPad 2**: [MarkdownPad 2](http://markdownpad.com/) è disponibile gratuitamente. Tuttavia, se si acquista una licenza, è possibile usare la funzione di rendering markdown per GitHub nell'anteprima dinamica.  

## Configurare l'editor markdown di Atom

Se si usa Atom, è necessario configurare alcune opzioni.

- Per impostazione predefinita, Atom usa 2 spazi per le tabulazioni, mentre markdown prevede 4 spazi. Se si usa il valore predefinito di due spazi, l'articolo verrà visualizzato correttamente nell'anteprima locale, ma non quando viene importato in docs.microsoft.com. Per questo motivo, configurare Atom per l'uso di 4 spazi. L'impostazione si trova in File->Settings->Editor Settings->Tab Length. 
- In questa sezione è anche possibile abilitare il ritorno a capo che ha la stessa funzione del ritorno a capo automatico del testo di Blocco note. 
- Per attivare l'anteprima markdown, fare clic su Packages->Markdown Preview->Toggle Preview. È possibile usare Ctrl+MAIUSC+M per attivare o disattivare la visualizzazione HTML in anteprima. 

## Creare un ramo dal repository

Creare un ramo dal repository in GitHub. 

1. Aprire Git Bash. 
2. Al prompt dei comandi immettere il comando seguente. 

        git clone https://[your GitHub user name]:[token]@github.com/microsoft/emdocs.git

Il comando crea una directory `emdocs` nel computer.  Se si usa il percorso predefinito, sarà `c:\users\<your Windows user name>\emdocs`. Ad esempio, questo comando clone sarebbe simile al seguente:

        git clone https://smithj:b428654321d613773d423ef2f173ddf4a312345@github.com/microsoft/emdocs.git  

## Impostare la connessione al repository remoto e configurare le credenziali

Configurare Git in modo che vengano usati per impostazione predefinita il proprio ID GitHub e il token di accesso personale senza dover digitare o incollare manualmente il token di accesso per ogni azione `push` o `pull`. 

Eseguire il comando seguente in Git Bash:

        cd emdocs
        git remote –v 
        git remote remove origin
        git remote add origin http://<githubID>:<token>@github.com/microsoft/emdocs
        git remote -v

L'operazione richiede in genere alcuni minuti. Al termine, non è necessario immettere nuovamente le credenziali. Sarà necessario ripetere il processo solo per configurare gli strumenti in un altro computer.

## Configurare il nome utente e la posta elettronica in locale

Per assicurarsi di essere visualizzato correttamente come collaboratore, è necessario configurare il proprio nome utente e la posta elettronica in locale in Git.

1. Avviare Git Bash e passare in emdocs
   ````
   cd emdocs
   ````
2. Configurare il proprio nome utente in modo che corrisponda al nome impostato nel profilo di GitHub:

    ````
    git config --global user.name "John Doe"
    ````
3. Configurare la posta elettronica in modo che corrisponda alla posta elettronica principale definita nel profilo di GitHub:

    ````
    git config --global user.email "alias@example.com"
    ````
4. Digitare `git config -l` e rivedere le impostazioni locali per verificare che il nome utente e la posta elettronica nella configurazione siano corretti.

## Passaggi successivi

- Leggere e seguire le istruzioni nella pagina relativa all'[Utilizzo di Git](./work-with-git.md) per iniziare a scrivere.


## Torna alla pagina iniziale

- [Articolo di panoramica](./../README.md)
- [Indice degli articoli del materiale sussidiario](./contributor-guide-index.md)


<!--Anchors-->
[Create a GitHub account and set up your profile]: #create-a-github-account-and-set-up-your-profile
[Permissions in GitHub]: #permissions-in-github
[Install Git for Windows]: #install-git-for-windows
[Enable two-factor authentication]: #enable-two-factor-authentication
[Create a personal access token]: #create-a-personal-access-token
[Install a markdown editor]: #install-a-markdown-editor
[Configure Atom]:#configure-atom
[Create a branch from the repository]: #create-a-branch-from-the-repository
[Set remote repository connection and configure credentials]: #set-remote-repository-connection-and-configure-credentials
[Configure your user name and email locally]: #configure-your-user-name-and-email-locally
[Next steps]: #next-steps

<!--HONumber=Mar16_HO1-->


