---
title: Scenario AIP - Controllo dei documenti archiviati in SharePoint
description: Questo scenario e la documentazione di supporto per l'utente usano la tecnologia di protezione Azure Rights Management per verificare che i documenti di Office archiviati in SharePoint rimangano sotto controllo tramite librerie protette.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/11/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3815ed1fdfd7b5201dfec258e6c20364c0397a8b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
<a id="scenario---retain-control-of-documents-stored-in-sharepoint" class="xliff"></a>

# Scenario - Mantenere il controllo dei documenti archiviati in SharePoint

>*Si applica a: Azure Information Protection, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano la tecnologia Azure Rights Management di Azure Information Protection per verificare che i documenti di Office archiviati in SharePoint rimangano sotto controllo tramite librerie protette. Ad esempio, i documenti vengono protetti automaticamente dalle perdite di dati accidentali o previste dagli utenti e l'amministratore può bloccare l'accesso al contenuto anche dopo che questo è stato scaricato o sincronizzato. I file da proteggere dovrebbero essere quelli destinati alla collaborazione interna su documenti o piani di progettazione oppure ad altre consegne. Quando si configurano le raccolte protette per SharePoint, i file di Office archiviati in tali raccolte saranno protetti da Azure Rights Management.

Le istruzioni sono adatte ai casi seguenti:

-   Dipendenti che condividono dati e collaborano usando documenti di Office presenti nella raccolta di SharePoint.

-   Dipendenti che non devono impostare o modificare le autorizzazioni definite da un amministratore a livello di raccolta.

-   Dipendenti che non devono condividere i documenti con utenti esterni all'organizzazione.

<a id="deployment-instructions" class="xliff"></a>

## Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Prima di passare alla documentazione utente, verificare che i requisiti e le procedure di supporto seguenti siano soddisfatti.

<a id="requirements-for-this-scenario" class="xliff"></a>

## Requisiti per questo scenario
Per questo scenario, sono necessari i requisiti seguenti:

|Requisito|Se sono necessarie ulteriori informazioni|
|---------------|--------------------------------|
|Sono stati preparati account e gruppi per Office 365 o Azure Active Directory|[Preparazione per Azure Information Protection](../plan-design/prepare.md)|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|
|Se si usa SharePoint Server: Distribuzione del connettore RMS e configurarlo per SharePoint|[Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md)|
|Configurare le autorizzazioni per il sito SharePoint da protezione|[Gestire le autorizzazioni per un elenco, una raccolta, una cartella, un documento o una voce di elenco](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[Applicare Information Rights Management a un elenco o a una raccolta](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|Configurazione di SharePoint per IRM e le raccolte protette|[Configurare Information Rights Management (IRM) nell'interfaccia di amministrazione di SharePoint](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Applicare Information Rights Management a un elenco o a una raccolta](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

<a id="to-configure-the-sharepoint-library-for-irm-settings" class="xliff"></a>

### Per configurare la raccolta di SharePoint per le impostazioni IRM

1.  Dopo aver configurato SharePoint per usare il servizio IRM, passare alla raccolta di SharePoint da proteggere con Azure RMS. Nella pagina **Impostazioni** &gt; **Information Rights Management (IRM)** per il sito, selezionare **Limita autorizzazioni per la libreria durante il download**, specificare un titolo per i criteri per gli amministratori e una descrizione dei criteri per gli utenti e fare clic su **Mostra opzioni**.

2.  Selezionare gli elementi seguenti:

    -   **Non consentire il caricamento di documenti che non supportano IRM**

    -   Facoltativo: **consentire la protezione del gruppo. Gruppo predefinito** e quindi specificare il nome di un gruppo aggiuntivo che potrebbe collaborare sui documenti archiviati in questa libreria, ma all'esterno di SharePoint. Ad esempio, il gruppo vendite dispone di autorizzazioni di modifica per il sito, un membor di questo gruppo scarica un documento, lo salva sul disco e lo invia tramite posta elettronica a un collega. Il collega avrà accesso al documento (con diritti di modifica) se è membro del gruppo designato.

        Senza questa opzione, solo gli utenti che dispongono dell'accesso alla raccolta di SharePoint saranno in grado di collaborare su tali documenti, solo scaricando i documenti direttamente da SharePoint. In molti casi, questa restrizione risulta appropriata.

<a id="user-documentation-instructions" class="xliff"></a>

## Istruzioni sulla documentazione per l'utente
Non sono disponibili istruzioni procedurali per gli utenti relative a questo scenario, in quanto le raccolte protette non richiedono alcuna azione particolare da parte degli utenti. I documenti sono protetti automaticamente al download, in base alle autorizzazioni definite da un amministratore di SharePoint per il sito. Tuttavia, informare gli utenti su questa modifica in modo che sappiano cosa aspettarsi e informare il supporto tecnico sulle librerie protette e su come è possibile limitare l'uso dei documenti. Ad esempio, a causa delle limitazioni correnti, questi documenti possono essere visualizzati,ma non modificati con i dispositivi mobili. Se è configurata la protezione di gruppo, informare gli utenti su quali gruppi possono accedere e modificare i documenti all'esterno di SharePoint.

Usando il modello seguente, copiare e incollare l'annuncio in una comunicazione per gli utenti finali e apportare tali modifiche in base all'ambiente:

1.  Sostituire ogni istanza di *&lt;nome della raccolta di SharePoint&gt;* con il nome e il collegamento alla raccolta di SharePoint configurata per Azure Rights Management. Se questa comunicazione vale per più di una libreria protetta, modificare le istruzioni.

2.  Se è stato configurato **, consentire la protezione di gruppo. l'opzione Gruppo predefinito**, sostituire *&lt;nome gruppo&gt;* con il nome del gruppo configurato e specificare &lt;motivo per il quale il gruppo dispone delle autorizzazioni di accesso per collaborare nei file ma non usando la raccolta di SharePoint&gt;. Se non si configura questa opzione, eliminare questa frase.

3.  Sostituire *&lt;dettagli contatto&gt;* con istruzioni su come gli utenti possono contattare il supporto tecnico, ad esempio il collegamento a un sito Web, un indirizzo di posta elettronica o un numero di telefono.

4.  Apportare altre eventuali modifiche a questo annuncio e quindi inviarlo agli utenti.

La documentazione dell'esempio mostra come questo annuncio viene visualizzato dagli utenti, dopo le personalizzazioni.

![Documentazione dell'utente del modello per la distribuzione rapida di Azure RMS](../media/AzRMS_UsersBanner.png)

<a id="it-announcement-changes-to-the-ltname-of-sharepoint-librarygt-site" class="xliff"></a>

### Annuncio IT: modifiche al sito &lt;nome della raccolta di SharePoint&gt;
Il sito di SharePoint, **&lt;nome della raccolta di SharePoint&gt;**, è ora configurato per la collaborazione protetta. Attualmente, solo i membri di &lt;nome gruppo&gt; possono aprire questi documenti dal sito, anche se sono stati salvati in locale o inviati tramite posta elettronica ad altri utenti. È possibile tuttavia condividerli con i membri di &lt;nome gruppo&gt; dopo aver scaricato i documenti, affinché &lt;motivo per il quale il gruppo dispone delle autorizzazioni di accesso per collaborare nei file ma non usando la raccolta di SharePoint&gt;. Quando si modifica uno di questi file, nella parte superiore del documento viene visualizzato un banner informativo giallo in cui si indica che è un documento protetto e si specificano gli utenti che possono accedervi.

Questa modifica consente di impedire agli utenti non autorizzati di accedere ai dati confidenziali della società. I documenti protetti possono essere visualizzati anche da dispositivi mobili ma, per modificarli, è necessario un sistema desktop.

Non sarà possibile caricare i documenti nel sito &lt;nome del sito di SharePoint&gt; se la collaborazione protetta non è supportata.

**Serve assistenza?**

-   Contattare il supporto tecnico: &lt;dettagli contatto&gt;

<a id="example-user-documentation" class="xliff"></a>

### Esempio di documentazione per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

<a id="it-announcement-changes-to-the-sales-forecasts-and-reports-site" class="xliff"></a>

#### Annuncio IT: Modifiche apportate al sito relativo a report e previsioni di vendita
Il sito di SharePoint relativo a **report e previsioni di vendita**è ora configurato per la collaborazione protetta. Attualmente, solo i membri del team Vendite e marketing possono aprire questi documenti dal sito, anche se altri utenti li hanno salvati in locale o li hanno inviati tramite posta elettronica. L'unica eccezione è rappresentata dalla possibilità di condividerli con i membri del team Contabilità dopo averli scaricati, in modo da offrire loro la possibilità di estrarre i dati sulle previsioni mensili. Quando si modifica uno di questi file, nella parte superiore del documento viene visualizzato un banner informativo giallo in cui si indica che è un documento protetto e si specificano gli utenti che possono accedervi.

Questa modifica consente di impedire agli utenti non autorizzati di accedere ai dati confidenziali della società. I documenti protetti possono essere visualizzati anche da dispositivi mobili ma, per modificarli, è necessario un sistema desktop.

È possibile caricare sul sito relativo a report e previsioni di vendita solo i documenti che supportano la collaborazione sicura.

**Serve assistenza?**

-   Contattare il supporto tecnico: helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]