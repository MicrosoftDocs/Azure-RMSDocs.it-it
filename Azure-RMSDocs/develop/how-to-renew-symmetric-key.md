---
title: Come rinnovare la chiave simmetrica in Azure Information Protection
description: Questo articolo illustra il processo di rinnovo di una chiave simmetrica in Azure Information Protection.
keywords: 
author: lleonard-msft
manager: mbaldwin
ms.author: alleonar
ms.date: 03/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0b8c8f0-6ed5-48bb-8155-ac4f319ec178
ms.openlocfilehash: 159e5b58883490e4417ecbdb9815340c9ccaa66d
ms.sourcegitcommit: dca4534a0aa7f63c0c525c9a3ce445088d1362bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-renew-the-symmetric-key-in-azure-information-protection"></a>Procedura: Rinnovare la chiave simmetrica in Azure Information Protection

Una **chiave simmetrica** è un'informazione segreta che consente di crittografare e decrittografare un messaggio in crittografia con chiave simmetrica.  

In Azure Active Directory (Azure AD), quando si crea un oggetto entità servizio per rappresentare un'applicazione, il processo genera anche una chiave simmetrica a 256 bit per verificare l'applicazione. Per impostazione predefinita, la chiave simmetrica è valida un anno. 

La procedura seguente illustra come rinnovare la chiave simmetrica. 

## <a name="prerequisites"></a>Prerequisiti

* Il modulo di Azure Active Directory (Azure AD) PowerShell deve essere installato come descritto in [Riferimenti per Azure AD Powershell](https://docs.microsoft.com/powershell/msonline/).


## <a name="renewing-the-symmetric-key-after-expiry"></a>Rinnovo della chiave simmetrica dopo la scadenza

Non è necessario creare una nuova entità servizio quando scade la chiave simmetrica associata all'applicazione. Al contrario, è possibile usare i [cmdlet di PowerShell](https://docs.microsoft.com/powershell/module/msonline) offerti da Microsoft Online Services (MSol) per creare una nuova chiave simmetrica per un'entità servizio esistente.

Per illustrare questo processo, si supponga che è stata già creata una nuova entità servizio tramite il comando [`New-MsolServicePrincipal`](https://docs.microsoft.com/powershell/msonline/v1/new-msolserviceprincipalcredential).

```
New-MsolServicePrincipalCredential -ServicePrincipalName "SupportExampleApp"
```

Il processo crea una chiave simmetrica e un **AppPrincipalId** come illustrato.

```
The following symmetric key was created as one was not supplied
ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

DisplayName : SupportExampleApp
ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
TrustedForDelegation : False
AccountEnabled : True
Addresses : []
KeyType : Symmetric
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

La chiave simmetrica scade il 22/3/2018 alle ore 15.27.53. Per usare l'entità servizio oltre la data di scadenza, è necessario rinnovare la chiave simmetrica. A tale scopo, usare il comando [`New-MsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/new-msolserviceprincipalcredential). 

```
New-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963
```

Questo comando crea una nuova chiave simmetrica per **AppPrincipalId** specificato.

```
The following symmetric key was created as one was not supplied ON8YYaMYNmwSfMX625Ei4eC6N1zaeCxbc219W090v28-
```
È possibile usare il comando [`GetMsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/get-msolserviceprincipalcredential) per verificare che la nuova chiave simmetrica è associata all'entità servizio corretta come illustrato. Si noti che il comando elenca tutte le chiavi attualmente associate all'entità servizio.

```
Get-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963 -ReturnKeyValues $true

Type : Symmetric
Value :
KeyId : c1ac145f-e899-4c90-8a02-2cef40054fc5
StartDate : 3/24/2017 10:11:07 PM
EndDate : 3/24/2018 10:11:07 PM
Usage : Verify

Type : Symmetric
Value :
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

Dopo avere verificato che la chiave simmetrica è effettivamente associata all'entità servizio appropriata, è possibile aggiornare i parametri di autenticazione dell'entità servizio con la nuova chiave. 

È quindi possibile rimuovere la vecchia chiave simmetrica usando il comando [`Remove-MsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/remove-msolserviceprincipalcredential) e verificare che la chiave è stata rimossa tramite il comando `Get-MsolServicePrincipalCredential`.

```
Remove-MsolServicePrincipalCredential -KeyId acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe -ObjectId 0ee53770-ec86-409e-8939-6d8239880518
```

## <a name="related-topics"></a>Argomenti correlati

* [Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md)
* [Riferimenti per Azure Active Directory MSOnline Powershell](https://docs.microsoft.com/powershell/msonline/)
