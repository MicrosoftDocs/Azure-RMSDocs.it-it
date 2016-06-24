---
# required metadata

title: Proteggere gli allegati della posta elettronica aziendale
description:
keywords:
author: karthikaraman
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: a1e630c1-7190-4ba9-b71d-ed9c2e93a6cc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteggere la posta elettronica e gli allegati dalla fuga di dati
La sezione [Protezione dei messaggi di posta elettronica e dei documenti aziendali](protect-corporate-email-documents.md) ha illustrato come assicurarsi che solo i dispositivi conformi possano accedere alla posta elettronica aziendale. Tuttavia, proteggere l'accesso non garantisce anche la protezione del contenuto dei messaggi di posta elettronica e dei relativi allegati. Il contenuto può essere copiato, spostato e salvato in un percorso diverso o condiviso con un altro utente. EMS risolve questo problema usando i criteri di gestione delle applicazioni mobili (MAM).

Le app gestite sono app conformi ai requisiti di sicurezza dell'azienda che vengono distribuite dall'amministratore IT. Con queste app il reparto IT ha il controllo diretto sulla distribuzione, la gestione continuativa come inventario o aggiornamenti e sulla cancellazione selettiva delle app e dei relativi dati associati. Con un set di criteri di gestione delle applicazioni mobili (MAM), Intune consente anche di modificare la funzionalità delle app e di limitare la condivisione dei dati:

-   Bloccare le funzionalità di copia e incolla o impedire il trasferimento dei dati da un'app gestita a un'app senza criteri MAM.

-   Impedire il backup nello spazio di archiviazione cloud personale, impedendo funzionalità come Salva con nome e così via.

-   Proteggere l'accesso alle app richiedendo PIN/passcode o credenziali aziendali in un'app protetta da MAM.

-   Configurare l'applicazione in modo da aprire tutti i collegamenti Web all'interno di Intune Managed Browser.

-   Cancellare in modo selettivo solo i dati associati all'app gestita. Quando un dispositivo viene perso, rubato o non viene più gestito dal reparto IT, una cancellazione selettiva può rimuovere tutti i dati aziendali dalle app, lasciando solo i dati personali delle app. Processo noto come multi-identità.

Con [Azure Rights Management Services](https://technet.microsoft.com/en-us/library/jj585026.aspx)è possibile estendere la protezione della posta elettronica nei modi seguenti:

-   È possibile crittografare i messaggi di posta elettronica in modo che solo gli utenti appropriati possano leggere o visualizzare il contenuto sia all'interno dell'azienda che all'esterno.

-   Gli utenti possono proteggere i messaggi di posta elettronica e il destinatario può leggere e usare messaggi di posta elettronica protetti ricevuti.

-   Un amministratore può impostare le regole per:

    -   Applicare automaticamente le regole a un gruppo specificato di destinatari o creare modelli per reparti specifici.

    -   Rilevare e applicare automaticamente le regole ai messaggi di posta elettronica con contenuto riservato. La regola può essere basata sul mittente, sul destinatario, sull'oggetto del messaggio o sul contenuto.

    -   Rilevare il contenuto riservato e avvertire il mittente di applicare le regole di protezione prima di inviare il messaggio di posta elettronica.

## Componenti delle app gestite

-   **Microsoft Intune** consente di configurare i criteri, associare i criteri all'app o usare lo strumento di wrapping delle app per consentire a un'app interna di usare i criteri di gestione delle applicazioni mobili.

-   **Portale aziendale** è un'app che viene eseguita in modo nativo in ogni dispositivo o è basata su browser. Il reparto IT distribuisce le app gestite a utenti o dispositivi e gli utenti finali possono installare l'app dal portale. I criteri associati alle app vengono estesi al dispositivo con le app.

![Grafico che mostra la modalità di gestione dei criteri per le app gestite tramite il portale aziendale e Microsoft Intune](./media/ProtectEmail/CADataSheet-Diagram-Apps.png)

## Esperienza dell'amministratore IT:
L'amministratore IT crea i criteri di gestione delle applicazioni mobili, associa i criteri all'app e distribuisce l'app a utenti o dispositivi. Quando l'app gestita viene installata nel dispositivo, le restrizioni dell'app diventano effettive. La creazione e la distribuzione delle app gestite non implicano altre attività se non minime:

-   Sono disponibili delle app esistenti che includono già l'App SDK che consente di applicare le restrizioni all'app. Tali app non richiedono altre attività di elaborazione ma solo di aggiungere un collegamento che punta a un App Store come iTunes o Google Play. Leggere [questo](https://technet.microsoft.com/en-us/library/dn708489.aspx) articolo per vedere l'elenco di app gestite.

-   Se si vogliono gestire le app create internamente, è possibile riassemblare le app con lo strumento di wrapping delle app di Microsoft Intune. Lo strumento riassembla l'app consentendo di applicare le restrizioni all'app.

## Esperienza dell'utente finale:
Gli utenti finali possono installare le app gestite e usarle per svolgere il proprio lavoro. Potranno solo spostare o condividere i dati tra le app gestite. Qualsiasi tentativo di spostare i dati all'esterno dell'ecosistema di app gestite verrà bloccato.

## Come proseguire
Dopo avere acquisito le informazioni sulla [protezione dei documenti e dei messaggi di posta elettronica aziendali](protect-corporate-email-documents.md) e degli allegati, leggere le informazioni su come [implementare una soluzione per la protezione della posta elettronica aziendale](implement-solution.md).


<!--HONumber=Apr16_HO4-->


