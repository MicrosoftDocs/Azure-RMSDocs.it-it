---
# required metadata

title: Informazioni su come distribuire una soluzione per la protezione di documenti e messaggi di posta elettronica aziendali
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 2e10af43-3138-45c0-b2f7-14a1d2bfb237

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Informazioni su come distribuire una soluzione per la protezione di documenti e messaggi di posta elettronica aziendali
Sono sempre di più le aziende che permettono ai propri dipendenti di aumentare la produttività accedendo a posta elettronica, documenti e risorse aziendali tramite i dispositivi mobili personali. Tuttavia, la quantità di dati riservati che sono archiviati nei documenti e messaggi di posta elettronica aziendali comporta un rischio significativo per le aziende.

Questa guida è rivolta ai professionisti IT e si propone di agevolare la definizione e quindi la distribuzione della soluzione ottimale per consentire all'azienda di applicare l'accesso condizionale in una delle configurazioni descritte di seguito. In questo modo, i dipendenti potranno usare i propri dispositivi mobili per accedere alla posta elettronica aziendale, proteggendo al contempo i dati dell'azienda.

Questa sezione illustra come distribuire una soluzione per la protezione di documenti e messaggi di posta elettronica aziendali. Per informazioni dettagliate sull'architettura di queste soluzioni, vedere [Indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali](architecture-guidance-for-protecting-company-email-and-documents).

> [!TIP]
> È possibile scaricare una copia di questo argomento nella [Raccolta TechNet](https://gallery.technet.microsoft.com/Deploying-Enterprise-16499404).

## Introduzione
La protezione dei dati aziendali è di vitale importanza e rappresenta un compito sempre più complesso man mano che aumenta il numero di dipendenti che usano i dispositivi mobili personali per accedere alle risorse aziendali, inclusi i messaggi e gli allegati di posta elettronica. Per gli amministratori IT è importante assicurarsi che i dati aziendali siano protetti anche quando quei dispositivi mobili non si trovano all'interno della sede fisica dell'azienda.

Microsoft Enterprise Mobility Suite (EMS) risolve questo problema offrendo una protezione completa dei documenti e dei messaggi di posta elettronica aziendali su quattro livelli: identità, dispositivo, applicazione e dati. Tra le altre funzionalità, EMS garantisce che i dipendenti possano accedere alla posta elettronica aziendale solo da dispositivi gestiti da Microsoft Intune e conformi ai criteri IT.

La protezione dei messaggi di posta elettronica aziendali prevede due obiettivi principali:

-   **Consentire solo a dispositivi conformi di accedere alla posta elettronica dell'azienda:** un passaggio importante per la protezione dei dati aziendali consiste nel limitare l'accesso ai dispositivi che non usano una password complessa, non sono jailbroken né crittografati.  Microsoft Intune offre la possibilità di impostare le condizioni che gli utenti devono soddisfare per accedere alle risorse aziendali. Questa caratteristica è nota come accesso condizionale.

-   **Proteggere il contenuto nei messaggi di posta elettronica e negli allegati:** mentre l'accesso condizionale assicura che solo i dispositivi conformi possano accedere alla posta elettronica, resta il problema di proteggere il contenuto dei messaggi e degli allegati di posta elettronica.  Il contenuto può essere copiato, spostato e salvato in un percorso diverso o condiviso con un altro utente.  EMS risolve questo problema usando i criteri di gestione delle applicazioni mobili.

    Le app gestite sono app a cui sono applicati criteri di gestione delle applicazioni mobili per renderle conformi ai requisiti di sicurezza aziendali. Queste app offrono il controllo diretto sulla distribuzione, sulla gestione continuativa, ad esempio di inventari o aggiornamenti, e sulla cancellazione selettiva delle app e dei relativi dati associati. Inoltre, con un set di criteri di gestione delle applicazioni mobili (MAM), Intune permette di modificare la funzionalità delle app e di limitare la condivisione dei dati. Per altri dettagli sul funzionamento di questa soluzione, compresi i dettagli sull'architettura, vedere [Indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali](architecture-guidance-for-protecting-company-email-and-documents).

    > [!NOTE]
    > È possibile creare e distribuire un profilo di posta elettronica, quindi impostare un criterio di conformità che specifica che i profili di posta elettronica devono essere gestiti da Intune (scelta consigliata). Questo permette di cancellare i messaggi di posta elettronica dai dispositivi dismessi e, per iOS, assicura che gli allegati possano essere aperti solo in applicazioni gestite da Intune. Vedere il [Passaggio 5: Creare criteri di conformità e distribuirli agli utenti.](conditional-access-intune-configmgr-exchange.md) per ulteriori informazioni.

### Soluzioni illustrate in questo articolo
Questa sezione presenta una panoramica generale delle singole soluzioni: Configuration Manager con implementazione di Intune, Intune da solo, gestione di applicazioni mobili e servizio Azure Rights Management.

-   **Gestione dell'accesso alla posta elettronica tramite accesso condizionale:** È possibile usare una configurazione ibrida di Configuration Manager con Intune, oppure usare solo Intune, insieme con Exchange Online o Exchange Server locale, per gestire e applicare l'accesso condizionale in tutti i tipi di PC e dispositivi mobili, indipendentemente dalla loro posizione. Applicando l'accesso condizionale in questo tipo di ambiente è possibile consentire all'utente di essere più produttivo, senza compromettere la sicurezza dei dati aziendali.

-   **Protezione degli allegati e dei dati di posta elettronica tramite la soluzione MAM:** In Intune è possibile applicare criteri MAM (Mobile Application Management, gestione di applicazioni mobili) per modificare la funzionalità delle app che vengono distribuite nella società. Ad esempio, è possibile limitare le operazioni Taglia, Copia e Incolla in un'app gestita oppure configurare un'app per aprire tutti i collegamenti Web in Managed Browser. Ciò garantisce che queste applicazioni siano in linea con i criteri di conformità e sicurezza della società.

-   **Servizio di gestione dei diritti di Azure per i criteri di prevenzione della perdita dei dati:** Azure Rights Management (Azure RMS) usa criteri di crittografia, identità e autorizzazione per proteggere file e messaggi di posta elettronica su più dispositivi, ad esempio telefoni, tablet e PC. È possibile proteggere le informazioni sia all'interno che all'esterno dell'organizzazione perché la protezione rimane associata ai dati, anche quando fuoriescono dai confini fisici dell'azienda.

### Valutazione dell'implementazione appropriata
Tra tutte le opzioni di progettazione e configurazione per la gestione dei dispositivi mobili, è difficile determinare quale combinazione soddisfi meglio le esigenze dell'azienda. L'articolo [Mobile Device Management Design Considerations Guide](mdm-design-considerations-guide.md) (Guida alle considerazioni di progettazione per la gestione dei dispositivi mobili) illustra i requisiti di progettazione della gestione dei dispositivi mobili e indica in dettaglio i passaggi e le attività che è possibile eseguire per progettare una soluzione adatta alle esigenze di business e tecnologiche dell'azienda.

### Esperienza generale dell'utente finale:
Dopo aver implementato la soluzione, gli utenti finali potranno accedere alla posta elettronica aziendale solo su dispositivi gestiti **e** conformi. Quando accedono alla posta elettronica sui dispositivi, i dati dell'azienda sono protetti e contenuti all'interno dell'ecosistema di app e sono disponibili unicamente agli utenti previsti. L'accesso potrà essere revocato in qualsiasi momento se il dispositivo risulta non conforme.

In particolare, i criteri di accesso condizionale configurati in Intune fanno sì che i dispositivi possano accedere alla posta elettronica solo se sono conformi ai criteri di conformità impostati. Alcune azioni, ad esempio le operazioni Copia e Incolla oppure il salvataggio nei servizi di archiviazione cloud personale, possono essere limitate usando i criteri di gestione delle applicazioni mobili. Il servizio di Azure Rights Management può essere usato per fare in modo che i dati sensibili di posta elettronica e gli allegati inoltrati possano essere letti solo dai destinatari. L'esperienza dell'utente finale è descritta in dettaglio in [Esperienza utente finale di accesso condizionale](end-user-experience-conditional-access.md).

### Come proseguire
Una volta letto questo argomento, è possibile acquisire altre informazioni sulla distribuzione di una soluzione specifica per la protezione dei messaggi di posta elettronica e dei documenti aziendali, a seconda dell'ambiente:

- [Usare l'accesso condizionale con Microsoft Intune](conditional-access-intune.md)
- [Usare l'accesso condizionale con Microsoft Intune e Configuration Manager](conditional-access-intune-configmgr.md)


<!--HONumber=Apr16_HO4-->


