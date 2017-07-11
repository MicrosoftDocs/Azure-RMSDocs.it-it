---
title: Configurazioni personalizzate per il client Azure Information Protection
description: Informazioni sulla personalizzazione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ab5465db1527e6236d2dca466936c36b260f03d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
<a id="custom-configurations-for-the-azure-information-protection-client" class="xliff"></a>

# Configurazioni personalizzate per il client Azure Information Protection

>*Si applica a: AD RMS, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti quando si gestisce il client Azure Information Protection. 

<a id="prevent-sign-in-prompts-for-ad-rms-only-computers" class="xliff"></a>

## Evitare le richieste di accesso per i computer solo AD RMS

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection. Per i computer che comunicano solo con AD RMS questo può comportare una richiesta di accesso non necessaria per gli utenti. È possibile evitare questa richiesta di accesso modificando il Registro di sistema:

Individuare il nome di valore seguente e quindi impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indipendentemente da questa impostazione, il client Azure Information Protection segue il normale [processo di individuazione del servizio RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) per trovare il proprio cluster AD RMS.

<a id="sign-in-as-a-different-user" class="xliff"></a>

## Accedere come utente diverso

In un ambiente di produzione, in genere gli utenti non hanno bisogno di accedere con un nome utente diverso quando usano il client Azure Information Protection. Può tuttavia essere necessario eseguire questa operazione come amministratore se sono presenti più tenant, ad esempio se si ha un tenant di prova oltre a Office 365 o un tenant di Azure usato dall'organizzazione.

È possibile verificare con quale account è stato eseguito l'accesso usando la finestra di dialogo di **Microsoft Azure Information Protection**: nell'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

In particolare quando si usa un account amministratore, assicurarsi di controllare il nome di dominio dell'account di accesso che viene visualizzato. Ad esempio, se si ha un account "amministratore" in due diversi tenant, può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo di questo errore può essere l'impossibilità di scaricare i criteri di Azure Information Protection o di visualizzare le etichette o un comportamento previsto.

Per accedere come utente diverso:

1. Usando un editor del Registro di sistema, passare a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** ed eliminare il valore **TokenCache** (con i dati associati).

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzato un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e fare clic su **Accedi** dalla sezione **Stato del client** aggiornata.

Inoltre:

- Se si usa Single Sign-On, è necessario disconnettersi da Windows e accedere con un account utente diverso dopo aver modificato il Registro di sistema. Il client Azure Information Protection eseguirà automaticamente l'autenticazione tramite l'account utente usato per l'accesso.

- Se si vuole reinizializzare l'ambiente per il servizio Azure Rights Management (noto anche come bootstrap), è possibile farlo usando l'opzione **Reimposta** dello [strumento RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Per eliminare i criteri di Azure Information Protection attualmente scaricati, rimuovere il file **Policy.msip** dalla cartella **%localappdata%\Microsoft\MSIP**.

<a id="hide-the-classify-and-protect-menu-option-in-windows-file-explorer" class="xliff"></a>

## Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

È possibile definire questa configurazione avanzata modificando il Registro di sistema quando si usa il client Azure Information Protection versione 1.3.0.0 o successiva. 

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

<a id="support-for-disconnected-computers" class="xliff"></a>

## Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. Se si è conoscenza che il computer in uso non sarà in grado di connettersi a Internet per un determinato periodo di tempo, è possibile impedire al client di provare a connettersi al servizio modificando il Registro di sistema. Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Verificare che nel client sia presente un file di criteri validi denominato **Policy.msip**, nella cartella **%localappdata%\Microsoft\MSIP**. Se necessario, è possibile esportare i criteri dal portale di Azure e copiare il file esportato nel computer client. È inoltre possibile usare questo metodo per sostituire un file di criteri non aggiornato con i criteri pubblicati più recenti.

<a id="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution" class="xliff"></a>

## Integrazione con la classificazione dei messaggi di Exchange per una soluzione di etichettatura dei dispositivi mobili

Benché Outlook sul Web non supporti ancora in modo nativo la protezione e la classificazione di Azure Information Protection, è possibile usare la classificazione dei messaggi di Exchange per estendere le etichette di Azure Information Protection agli utenti dei dispositivi mobili.

Per ottenere questa soluzione: 

1. Usare il cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) di Exchange PowerShell per creare le classificazioni dei messaggi con la proprietà Name che esegue il mapping ai nomi di etichetta nei criteri di Azure Information Protection. 

2. Creare una regola di trasporto di Exchange per ogni etichetta: applicare la regola quando le proprietà del messaggio includono la classificazione configurata e modificare le proprietà del messaggio per impostare un'intestazione del messaggio. 

    Per l'intestazione del messaggio, è possibile trovare le informazioni da specificare nelle intestazioni Internet di un messaggio di posta elettronica inviato e classificato tramite l'etichetta di Azure Information Protection. Cercare l'intestazione **msip_labels** e la stringa immediatamente successiva fino al punto e virgola incluso. Usando l'esempio precedente:
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Quindi, per l'intestazione del messaggio nella regola, specificare **msip_labels** per l'intestazione e la parte rimanente della stringa per il valore dell'intestazione. Ad esempio:
    
    ![Regola di trasporto di Exchange Online di esempio che imposta l'intestazione del messaggio per un'etichetta di Azure Information Protection specifica](../media/exchange-rule-for-message-header.png)

Prima di eseguire il test, tenere presente che spesso si verifica un ritardo quando vengono create o modificate le regole di trasporto, ad esempio un'attesa di un'ora. Se la regola è attiva, quando gli utenti usano Outlook sul Web o un client del dispositivo mobile che supporta la protezione con Rights Management si verifica quanto segue: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Quando i destinatari che eseguono il client Azure Information Protection visualizzano il messaggio di posta elettronica in Outlook, vedranno l'etichetta di Azure Information Protection assegnata e l'eventuale intestazione, piè di pagina o filigrana corrispondente del messaggio di posta elettronica. 

Se le etichette di Azure Information Protection applicano la protezione di Rights Management, aggiungerla alla configurazione della regola selezionando l'opzione per modificare la sicurezza del messaggio, applicare la protezione dei diritti, quindi selezionare il modello RMS o l'opzione Non inoltrare.

È anche possibile configurare le regole di trasporto per eseguire il mapping inverso: quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente. A tale scopo, eseguire questa procedura:

- Per ogni etichetta di Azure Information Protection, creare una regola di trasporto da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **General**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.


<a id="next-steps" class="xliff"></a>

## Passaggi successivi
Dopo aver personalizzato il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
