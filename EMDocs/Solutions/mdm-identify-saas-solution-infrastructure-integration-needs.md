---
# required metadata

title: Identificare i requisiti di integrazione dell'infrastruttura della soluzione SaaS
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 26b15471-b496-4404-934d-67e621655bca

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Identificare i requisiti di integrazione dell'infrastruttura della soluzione SaaS

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Le decisioni principali da prendere quando si considera la gestione dei dispositivi mobili con una soluzione SaaS sono:

- Come avverrà l'integrazione tra gli account di utenti e dispositivi della directory locale esistente e la soluzione SaaS?
- È necessario integrare la soluzione SaaS con le piattaforme locali esistenti di gestione dei client?

Le decisioni prese in queste due aree avranno un impatto notevole sulla distribuzione, l'amministrazione e l'esperienza degli utenti finali per la soluzione di gestione dei dispositivi mobili.

## Identità e connettività alla directory

La connessione e la sincronizzazione della directory locale degli account di utenti e dispositivi con la soluzione SaaS sono passaggi fondamentali che consentono realmente di connettere gli utenti, i dispositivi mobili, le applicazioni mobili e la gestione dei dispositivi mobili. Conoscere l'identità di un utente e poterla associare a specifici dispositivi mobili è essenziale per gestire l'accesso alle risorse e ai dati aziendali dal dispositivo mobile. Per molti versi, l'ottimizzazione della modalità di connessione di queste aree con la soluzione SaaS determina il vantaggio complessivo per l'organizzazione e per gli utenti di dispositivi mobili.  La connettività universale consente a utenti e dispositivi di usare dispositivi e applicazioni da postazioni remote ed è essenziale che la gestione delle identità utente soddisfi le esigenze di questo tipo di connettività. È importante sottolineare che la modalità di gestione delle identità e dell'autenticazione utente è fondamentale per il successo della soluzione di gestione dei dispositivi mobili.

La sincronizzazione dei servizi della directory locale alla soluzione SaaS è un'altra area chiave da considerare quando si definisce la strategia di gestione dei dispositivi mobili. Molte organizzazioni preferiscono mantenere un'infrastruttura di directory locale di utenti e dispositivi, ma devono estendere gli account a vari servizi basati su cloud. Tali servizi possono includere solo una soluzione di gestione dei dispositivi mobili basata su SaaS, ma nella maggior parte dei casi le organizzazioni devono integrare gli account di utenti e dispositivi in diversi tipi di servizi basati su cloud. Può trattarsi di applicazioni, dati o servizi Web di terze parti basati su cloud. Mantenere sincronizzati gli account di utenti e dispositivi della directory è la base di una soluzione di gestione delle identità ben progettata. Dopo aver integrato la directory locale con la directory cloud, è inoltre possibile abilitare Single Sign-On (SSO) per consentire agli utenti di accedere a tutti i servizi tramite le credenziali locali. <token>Intune</token> e Office 365 possono usare l'integrazione per abilitare Single Sign-On (SSO) con le app SaaS che l'organizzazione potrebbe usare.

### Domande su identità e connettività alla directory

Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione di gestione delle identità e connettività alla directory:

- La soluzione SaaS supporta servizi di autenticazione utente integrati? In caso affermativo, supporta il tipo di servizi di directory in uso nell'infrastruttura locale?
- È necessario supportare l'autenticazione di utenti e dispositivi mobili per applicazioni o servizi interni e/o locali?
- La soluzione SaaS supporta l'autenticazione di utenti e dispositivi mobili per applicazioni o servizi basati su SaaS esterni o di terze parti?
- In che modo la soluzione SaaS gestisce le anomalie e le minacce relative alle identità?
- La soluzione SaaS supporta l'implementazione e la gestione dell'autenticazione a più fattori (MFA, Multi-Factor Authentication)?
- Quali tipi di oggetti dei servizi di directory è necessario estendere alla soluzione SaaS? La soluzione SaaS presenta restrizioni per determinati tipi di oggetti?
- Quali sono i requisiti locali necessari per estendere i servizi di directory alla soluzione SaaS?
- Dopo la connessione con la soluzione SaaS, come avviene la replica o la sincronizzazione con il servizio cloud degli oggetti della directory di utenti e dispositivi mobili? Le impostazioni di sincronizzazione sono personalizzabili o fisse?
- Tutti gli attributi degli oggetti della directory vengono sincronizzati con la soluzione SaaS? È necessario sincronizzare gli attributi degli oggetti della directory personalizzati?
- I servizi della directory locale sono ospitati in una singola posizione o in un raggruppamento logico? In caso contrario, la soluzione SaaS supporta la sincronizzazione dei servizi di più directory da più posizioni e più raggruppamenti logici?

## Connessione con piattaforme esistenti di gestione dei client

Molte organizzazioni dispongono di una piattaforma locale esistente di gestione dei client per gestire server e computer desktop. La modalità di integrazione della gestione dei dispositivi mobili in questo sistema probabilmente avrà un impatto significativo sui costi dell'infrastruttura IT, sui processi di amministrazione della gestione dei dispositivi, sul supporto per il reporting e l'inventario dei dispositivi e sull'integrazione complessiva con altre applicazioni e servizi aziendali critici. Connettendo queste due piattaforme, le organizzazioni sono in grado di utilizzare le economie di scala di una singola piattaforma di gestione unificata.

### Domande sulla connessione a piattaforme di gestione client esistenti

Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione della connessione della soluzione SaaS a piattaforme di gestione client esistenti:

- La piattaforma locale di gestione dei client supporta l'integrazione con la soluzione SaaS? In caso affermativo, sono presenti:
 - Limitazioni sul tipo di soluzione SaaS?
 - Limitazioni sui tipi di dispositivi supportati?
- Quali sono i requisiti per la connessione della piattaforma locale di gestione dei client con la soluzione SaaS? In particolare, esistono:
 - Requisiti relativi ai dispositivi o ai server fisici?
 - Requisiti relativi ai servizi di directory o allo schema di directory?
 - Requisiti relativi ai DNS (Domain Name Services)?
 - Requisiti di identità?
 - Requisiti relativi alla configurazione o agli aggiornamenti della piattaforma di gestione dei client?
 - Requisiti relativi alla configurazione della connettività di rete e/o della sicurezza di rete?
- È possibile condividere o utilizzare le informazioni di configurazione dei client o dei dispositivi esistenti (criteri, profili e impostazioni) nella soluzione SaaS? Queste informazioni dovranno essere ricreate?
- Dopo la connessione delle due piattaforme, come vengono gestiti i client? Diversi tipi di client vengono gestiti in un sistema di amministrazione unificato o separatamente?
- In che modo le modifiche e gli aggiornamenti della soluzione SaaS vengono integrati con la piattaforma locale di gestione dei client? Si tratta di un processo di configurazione automatico o manuale?

>[!TIP]
>Assicurarsi di prendere appunti per ogni risposta e di comprendere la logica alla base della risposta. Le attività successive esamineranno le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Rispondere a queste domande consentirà di selezionare l'opzione più adatta alle esigenze aziendali.

<!--HONumber=Jun16_HO1-->


