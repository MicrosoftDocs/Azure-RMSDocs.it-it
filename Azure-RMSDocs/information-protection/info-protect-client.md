---
title: Installazione del client di Azure Information Protection | Azure Rights Management
description: Per classificare i documenti e i messaggi di posta elettronica con Azure Information Protection, occorre prima di tutto installare il client di Azure Information Protection. Questa installazione aggiunge una barra Information Protection alle applicazioni di Office (Word, Excel, PowerPoint, Outlook) che mostra le etichette di classificazione per l'organizzazione, oltre a un nuovo gruppo Protezione nella scheda Home di Word, Excel e PowerPoint, che presenta un pulsante denominato Proteggi.
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: ab8388e03803d32a6891785f905a1ddef796bc25


---

# Installazione del client di Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Per classificare i documenti e i messaggi di posta elettronica con Azure Information Protection, occorre prima di tutto installare il client di Azure Information Protection. Questa installazione aggiunge una barra Information Protection alle applicazioni di Office (Word, Excel, PowerPoint, Outlook) che mostra le etichette di classificazione per l'organizzazione, oltre a un nuovo gruppo **Protection** (Protezione) nella scheda **Home** di Word, Excel e PowerPoint, che presenta un pulsante denominato **Protect** (Proteggi):

L'immagine seguente mostra la barra Information Protection e le etichette del [criterio predefinito](configure-policy-default.md):

![Barra Azure Information Protection con criterio predefinito](../media/info-protect-bar-default.png)

Scaricare il client di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Prima di installare il client, verificare di avere le versioni del sistema operativo e le applicazioni richieste: [Requisiti per Azure Information Protection](requirements-azure-infoprotect.md).


## Per installare manualmente il client di Azure Information Protection

1. Dopo avere eseguito il [download del client](https://www.microsoft.com/en-us/download/details.aspx?id=53018), eseguire **AZInfoProtection.exe** e seguire le istruzioni per l'installazione del client. Questa installazione richiede autorizzazioni amministrative locali.

    Selezionare l'opzione per l'installazione di un criterio demo se non si riesce a connettersi a Office 365 o Azure Active Directory, ma si vuole vedere e provare Azure Information Protection sul lato client usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione. 

2. Per iniziare a usare il client di Azure Information Protection: se il computer esegue Office 2010, riavviare il computer. Per altre versioni di Office, riavviare le applicazioni di Office.

## Per installare il client di Azure Information Protection per gli utenti

- È possibile creare script e automatizzare l'installazione del client di Azure Information Protection creando un pacchetto AZInfoProtection.exe e usando le [pzioni della riga di comando di Windows Installer (msiexec)](https://technet.microsoft.com/library/cc759262(v=ws.10).aspx) standard.

    Ad esempio, se la versione nel pacchetto creato è denominata InfoProtect.msi e si vuole installare automaticamente il client: `msiexec /qn InfoProtection.msi`


## Per disinstallare il client di Azure Information Protection

- Per disinstallare un programma, usare il Pannello di controllo: fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

## Per verificare l'installazione, lo stato della connessione o segnalare un problema

1. Aprire un'applicazione di Office, quindi nel gruppo **Protection** (Protezione) della scheda **Home** fare clic su **Protect** (Proteggi) e quindi fare clic su **Help and feedback** (Guida e commenti e suggerimenti).

2. Nella finestra di dialogo **Microsoft Azure Information Protection** notare quanto segue:

    - Il valore **Last connection** (Ultima connessione) che indica quando il client si è connesso per l'ultima volta al servizio Azure Information Protection dell'organizzazione. Quando il client si connette al servizio, scarica automaticamente il criterio più recente se rileva variazioni rispetto al criterio corrente. Se si sono apportate modifiche ai criteri dopo l'ora visualizzata, chiudere e riaprire l'applicazione di Office.

    - Il nome utente visualizzato che identifica l'account usato per autenticare l'utente in Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory.

    - La versione del client di Azure Information Protection.

    - Il collegamento **Invia commenti e suggerimenti** che consente di allegare automaticamente i log del client a un messaggio di posta elettronica da inviare al team di Information Protection per l'analisi.

    - Il collegamento **Esegui diagnostica**: questa funzionalità non è attualmente implementata.

## Percorsi di file

File del client:   

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client e file di criteri attualmente installati:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**


## Passaggi successivi

Per modificare le etichette sulla barra Information Protection, è necessario configurare i criteri di Azure Information Protection. Per altre informazioni, veder e[Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md). 



<!--HONumber=Aug16_HO4-->


