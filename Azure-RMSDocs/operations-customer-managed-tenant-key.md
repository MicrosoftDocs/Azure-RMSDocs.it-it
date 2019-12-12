---
title: Operazioni del ciclo di vita della chiave del tenant AIP gestite dal cliente
description: Informazioni sulle operazioni del ciclo di vita necessarie per la gestione da parte dell'utente della chiave del tenant per Azure Information Protection (scenario "bring your own key" o BYOK).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/06/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0381e5d6368587a6e743caefd519fc4669c6183b
ms.sourcegitcommit: 07b518c780f5e63eb5a72d7499ec7cfa40a95628
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2019
ms.locfileid: "74898899"
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>Operazioni del ciclo di vita della chiave del tenant gestite dal cliente

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Se la chiave del tenant per Azure Information Protection viene gestita dall'utente (scenario "bring your own key" o BYOK), usare le sezioni seguenti per ottenere altre informazioni sulle operazioni del ciclo di vita rilevanti per questa topologia.

## <a name="revoke-your-tenant-key"></a>Revocare la chiave del tenant

Esistono pochissimi scenari in cui potrebbe essere necessario revocare la chiave invece di eseguire la reimpostazione. Quando si revoca la chiave, tutto il contenuto protetto dal tenant con tale chiave diventerà inaccessibile a tutti gli utenti (inclusi Microsoft, amministratori globali e utenti con privilegi avanzati), a meno che non si disponga di un backup della chiave che è possibile ripristinare. Dopo aver revocato la chiave, non sarà possibile proteggere il nuovo contenuto finché non verrà creata e configurata una nuova chiave del tenant per Azure Information Protection. 

Per revocare la chiave del tenant gestita dal cliente, in Azure Key Vault modificare le autorizzazioni per l'insieme di credenziali delle chiavi che contiene la chiave del tenant di Azure Information Protection in modo che il servizio Azure Rights Management non possa più accedere alla chiave. Questa azione revoca efficacemente la chiave del tenant per Azure Information Protection.

Quando si annulla la sottoscrizione di Azure Information Protection, l'uso della chiave del tenant in Azure Information Protection viene interrotto e non è necessaria alcuna azione da parte dell'utente.

## <a name="rekey-your-tenant-key"></a>Reimpostare la chiave del tenant
Il processo di reimpostazione della chiave è noto anche come rollover della chiave. Quando si esegue questa operazione, Azure Information Protection interrompe l'uso della chiave del tenant esistente per proteggere documenti e messaggi di posta elettronica e inizia a usare una chiave diversa. I criteri e i modelli vengono subito abbandonati, ma questo passaggio è comunque graduale per i client e i servizi esistenti che usano Azure Information Protection. Ciò significa che, per un certo periodo di tempo, parte del nuovo contenuto continua a essere protetta tramite la chiave del tenant precedente.

Per reimpostare la chiave, è necessario configurare l'oggetto della chiave del tenant e specificare la chiave alternativa da usare. La chiave usata in precedenza viene quindi contrassegnata automaticamente come archiviata per Azure Information Protection. Questa configurazione assicura che il contenuto protetto tramite questa chiave rimanga accessibile.

Ecco alcuni casi in cui potrebbe essere necessario reimpostare una chiave per Azure Information Protection:

- La società è stata divisa in due o più società. Quando si reimposta la chiave del tenant, la nuova società non potrà accedere al nuovo contenuto pubblicato dai dipendenti e sarà in grado di accedere al vecchio contenuto se dispone di una copia della chiave del tenant precedente.

- Si vuole passare da una topologia di gestione delle chiavi a un'altra. 

- Si sospetta una violazione della copia master della chiave del tenant in possesso dell'utente.

Per reimpostare la chiave su un'altra chiave gestita, è possibile creare una nuova chiave in Azure Key Vault o usarne una già presente in Azure Key Vault. Seguire quindi le stesse procedure usate per implementare lo scenario BYOK per Azure Information Protection. 

1. Solo se la nuova chiave si trova in un insieme di credenziali delle chiavi diverso da quello già usato per Azure Information Protection: autorizzare Azure Information Protection a usare l'insieme di credenziali delle chiavi usando il cmdlet [set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) .

2. Se Azure Information Protection non è ancora noto alla chiave che si vuole usare, eseguire il cmdlet [use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) .

3. Configurare l'oggetto chiave del tenant usando il cmdlet Run [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) .

Per altre informazioni su ognuna di queste fasi:

- Per reimpostare la chiave su un'altra chiave gestita, vedere [Implementazione dello scenario BYOK per la chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).
    
    Se si esegue la reimpostazione di una chiave protetta tramite HSM creata in locale e trasferita in Key Vault, è possibile usare lo stesso ambiente di sicurezza e accedere alle schede nello stesso modo usato per la chiave corrente.

- Per reimpostare la chiave, passando a una chiave gestita da Microsoft, vedere la sezione [Reimpostare la chiave del tenant](operations-microsoft-managed-tenant-key.md#rekey-your-tenant-key) per le operazioni gestite da Microsoft.

## <a name="backup-and-recover-your-tenant-key"></a>Eseguire il backup e il ripristino della chiave del tenant
L'utente che gestisce la chiave del tenant è anche responsabile del backup della chiave usata da Azure Information Protection. 

Se la chiave del tenant è stata generata in locale, in un modulo di protezione hardware nCipher: per eseguire il backup della chiave, eseguire il backup del file di chiave in formato token, del file globale e delle schede amministratore. Quando la chiave viene trasferita in Azure Key Vault, il servizio salva il file della chiave in formato token come protezione da eventuali errori dei nodi del servizio. Questo file è associato all'ambiente di sicurezza relativo all'area o all'istanza specifica di Azure. È tuttavia opportuno tenere presente che questo file di chiave in formato token non rappresenta un backup completo. Se ad esempio è necessaria una copia in testo normale della chiave da usare all'esterno di un modulo di protezione hardware nCipher, Azure Key Vault non è in grado di recuperarla perché dispone solo di una copia non recuperabile.

Azure Key Vault contiene un [cmdlet di backup](/powershell/module/az.keyvault/backup-azkeyvaultkey). Scaricarlo e archiviarlo in un file per eseguire il backup di una chiave. Il contenuto scaricato è crittografato e può quindi essere usato solo in Azure Key Vault. 

## <a name="export-your-tenant-key"></a>Esportare la chiave del tenant
In uno scenario BYOK non è possibile esportare la chiave del tenant da Azure Key Vault o da Azure Information Protection. La copia presente in Azure Key Vault non è recuperabile. 

## <a name="respond-to-a-breach"></a>Rispondere a una violazione di sicurezza
Indipendentemente dall'affidabilità, nessun sistema di sicurezza può considerarsi completo se non prevede un processo di risposta alle violazioni di sicurezza. La chiave del tenant può essere violata o rubata e anche se è protetta in modo efficiente, potrebbero essere presenti vulnerabilità nella tecnologia attuale della chiave o nella lunghezza e negli algoritmi correlati alle chiavi attuali.

Microsoft ha predisposto un team apposito per rispondere agli eventi imprevisti correlati alla sicurezza che possono verificarsi nei suoi prodotti e servizi. Non appena riceve un report plausibile su un evento imprevisto, il team si attiva per esaminarne l'ambito, la causa radice e le soluzioni. Se l'evento imprevisto influiscono sulle risorse, Microsoft invia una notifica tramite posta elettronica agli amministratori globali del tenant.

In caso di violazione di sicurezza, l'azione più efficace che l'utente o Microsoft possa intraprendere dipende dall'ambito della violazione stessa. Microsoft collaborerà con l'utente durante l'intero processo. Nella tabella seguente vengono descritte alcune situazioni tipiche e la risposta più probabile, sebbene la risposta esatta dipenda da tutte le informazioni raccolte durante l'analisi.

|Descrizione evento imprevisto|Risposta probabile|
|------------------------|-------------------|
|Perdita della chiave del tenant.|Reimpostare la chiave del tenant. Vedere [Reimpostare la chiave del tenant](#rekey-your-tenant-key).|
|Diritti di accesso alla chiave del tenant ottenuti da un utente non autorizzato o da malware, ma nessuna perdita della chiave.|La reimpostazione della chiave del tenant non è sufficiente ed è necessaria un'analisi della causa radice. Se l'utente non autorizzato ha ottenuto l'accesso a causa di un bug del processo o del software, questo problema deve essere risolto.|
|Vulnerabilità scoperta nella tecnologia del moduli di protezione hardware di generazione corrente.|Microsoft deve aggiornare i moduli di protezione hardware. Se si ritiene che la vulnerabilità abbia provocato l'esposizione di chiavi, Microsoft inviterà tutti i clienti a reimpostare le proprie chiavi del tenant.|
|Vulnerabilità scoperta nell'algoritmo RSA o nella lunghezza della chiave oppure attacchi di forza bruta diventati realizzabili a livello di calcolo.|Microsoft deve aggiornare Azure Key Vault o Azure Information Protection per supportare nuovi algoritmi e lunghezze maggiori della chiave che siano resilienti e invitare tutti i clienti a reimpostare la propria chiave del tenant.|
