---
title: Come aggiungere diritti proprietario espliciti | Azure RMS
description: L'applicazione deve aggiungere in modo esplicito i diritti "proprietario" durante la creazione di una licenza da zero.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: cfdee38bc12393f130abcbfc5d69b1fbd65f5ecd
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95567963"
---
# <a name="how-to-add-explicit-owner-rights"></a>Procedura: Aggiungere diritti espliciti di proprietario

L'applicazione deve aggiungere in modo esplicito i diritti "proprietario" durante la creazione di una licenza da zero tramite [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch).

## <a name="prerequisites"></a>Prerequisiti

Quando l'applicazione crea un handle di licenza tramite [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch), deve anche concedere diritti completi (autorizzazioni) al proprietario in modo esplicito.

> [!NOTE]
> L'impostazione di un utente come "proprietario" tramite [IpcSetLicenseProperty](/previous-versions/windows/desktop/msipc/ipcsetlicenseproperty) con la proprietà **IPC\_LI\_OWNER** non concede al proprietario autorizzazioni complete.

L'esempio di codice seguente illustra solo i passaggi da eseguire per la creazione e l'aggiunta di diritti specifici a una determinata licenza.

## <a name="instructions"></a>Istruzioni
 
## <a name="step-1-example-scenario"></a>Passaggio 1: scenario di esempio

In questo esempio i diritti necessari vengono aggiunti a una licenza creata con [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch). L'esempio illustra la creazione e l'assegnazione dei diritti alla licenza tramite un elenco di diritti.

A questi utenti vengono aggiunti i due diritti seguenti:

- Autorizzazioni di *lettura* assegnate a joe@contoso.com
- Autorizzazioni *complete* assegnate a Mary\_kay@contoso.com

```cpp
// Create User Rights structure
IPC_USER_RIGHTS ownerRightForOwner = {0};

// Create rights
LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

// Assign values to members of Rights structure
ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
ownerRightForOwner.rgwszRights = rgwszOwnerRights;
ownerRightForOwner.cRights = 1;

// Create User Rights structure for Joe with Read permissions
IPC_USER_RIGHTS joeReadRight = {0};
LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

// Assign values to members of Rights structure for Joe
joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
joeReadRight.User.wszID = "joe@contoso.com";
joeReadRight.rgwszRights = rgwszReadRights;
joeReadRight.cRights = 1;

// Create User Rights structure for Mary Kay with Full permissions
IPC_USER_RIGHTS mary_kayFullRight = {0};
LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

// Assign values to members of Rights structure for Mary Kay
mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
mary_kayFullRight.rgwszRights = rgwszFullRights;
mary_kayFullRight.cRights = 1;

// Create User Rights List and assign the above rights
size_t uNoOfUserRights = 3;
PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
(new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

if(pUserRightsList == NULL)
{
  // Handle error
}

// Assign values to members of Rights List structure for Joe and Mary Kay
(*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
(*pUserRightsList).cUserRights = uNoOfUserRights;
(*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
(*pUserRightsList).rgUserRights[1] = joeReadRight;
(*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

// Set the Rights List property on the license via its handle
// hLicense is a license handle created with IpcCreateLicenseFromScratch
hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

if(FAILED(hr))
{
  // Handle the error
}
```


## <a name="related-topics"></a>Argomenti correlati

- [Note per gli sviluppatori](developer-notes.md)
- [IpcSetLicenseProperty](/previous-versions/windows/desktop/msipc/ipcsetlicenseproperty)
- [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch)