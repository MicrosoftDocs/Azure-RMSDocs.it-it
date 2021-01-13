---
title: Revocare l'accesso ai documenti-Azure Information Protection
description: Descrive in che modo gli utenti finali possono usare il client AIP per revocare l'accesso ai documenti protetti.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/07/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 294d93666eed55616bbe033215abef0e9dcf62b7
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98163774"
---
# <a name="user-guide-revoke-document-access-with-azure-information-protection-public-preview"></a>Guida dell'utente: revocare l'accesso ai documenti con Azure Information Protection (anteprima pubblica)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Pertinente per**: [AIP Unified Labeling client only](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'utente: tenere traccia dei documenti e revocarli quando si usa il client AIP classico](client-track-revoke.md). *

Questo articolo descrive come revocare l'accesso per i documenti protetti da Microsoft Office. I documenti protetti sono supportati per Track and Revoke, anche se non sono etichettati.

La revoca dell'accesso per un documento protetto impedisce ad altri utenti di accedere al documento, anche se è già stato concesso loro l'accesso. Per altre informazioni, vedere [Guida dell'utente: classificare e proteggere con la Azure Information Protection Unified Labeling client](clientv2-classify-protect.md).

Le funzionalità rileva e revoca per il client Unified Labeling sono attualmente in anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 

## <a name="revoke-access-from-microsoft-office-apps"></a>Revocare l'accesso da app Microsoft Office

Per revocare l'accesso da Word, Excel o PowerPoint:

1. Aprire il file protetto di cui si desidera revocare l'accesso. Deve trattarsi di un file in cui *è* stata applicata la protezione tramite l'account utente *corrente* .

    > [!TIP]
    > Se è stata applicata solo un'etichetta e una protezione, non è possibile revocare l'accesso nella stessa sessione. Riaprire il documento se è necessario revocare l'accesso.

1. Nella scheda **Home** fare clic sul pulsante **Sensitivity** e selezionare **REVOKE Access**:

    :::image type="content" source="../media/track-revoke-word.png" alt-text="Selezionare revoca l'accesso da Microsoft Word":::

    > [!NOTE]
    > Questa opzione non è visibile? Per ulteriori informazioni, vedere i possibili scenari [seguenti](#dont-see-the-revoke-access-option).
    >
 
1. Nel messaggio di conferma visualizzato, fare clic su **Sì** per continuare.

L'accesso viene revocato e gli altri utenti non potranno più accedere al documento. Se è consentito l' [accesso offline](/microsoft-365/compliance/encryption-sensitivity-labels#assign-permissions-now) , gli utenti continueranno a essere in grado di accedere ai documenti revocati fino alla scadenza del periodo di criteri offline. 

### <a name="dont-see-the-revoke-access-option"></a>Non viene visualizzata l'opzione REVOKE Access?

Se non viene visualizzata l'opzione per **revocare l'accesso** nel menu **Sensitivity** , è possibile che si disponga di uno degli scenari seguenti:

- È possibile che sia stata appena applicata la protezione in questa sessione. In tal caso, chiudere e riaprire il documento per riprovare.

- È possibile che venga visualizzato un documento non protetto. La revoca dell'accesso è pertinente solo per i documenti protetti.

- Potrebbe non essere installata la versione più recente di AIP Unified Labeling client o potrebbe essere necessario riavviare le app di Office o il computer dopo l'installazione. 

    Per ulteriori informazioni, vedere [Guida dell'utente: scaricare e installare il client di Azure Information Protection](install-client-app.md).

- È possibile che l'amministratore abbia [disattivato le funzionalità di rilevamento](track-and-revoke-admin.md#turn-off-track-and-revoke-features-for-your-tenant) nell'organizzazione.

## <a name="revoking-access-where-the-document-protection-has-been-changed-on-a-copy"></a>Revoca dell'accesso in cui la protezione dei documenti è stata modificata in una copia

Se un altro utente ha modificato l'etichetta o la protezione su una copia del documento, l'accesso *non viene revocato* per la copia del documento. 

Questo perché il rilevamento e la revoca dell'accesso vengono eseguiti usando un valore ContentID univoco, che cambia ogni volta che viene modificata la protezione.

> [!IMPORTANT]
> Se si ritiene che un utente abbia modificato l'etichetta o il livello di protezione in un documento ed è necessario revocare l'accesso, contattare un amministratore di sistema per consentire di revocare l'accesso a tale copia del documento.
> 
## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere:

- [Guida dell'utente del client per l'assegnazione unificata di AIP](clientv2-user-guide.md)
- [Guida dell'amministratore client per l'assegnazione unificata di AIP](clientv2-admin-guide.md)
- [Problemi noti per le funzionalità di rilevamento e revoca](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)
