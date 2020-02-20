---
title: Classe MIP::P ublishingLicenseInfo
description: Documenta la classe MIP::p ublishinglicenseinfo dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f9283a9cc52ef803e35a6d714e43bfce9b137771
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489640"
---
# <a name="class-mippublishinglicenseinfo"></a>Classe MIP::P ublishingLicenseInfo 
Contiene i dettagli di una licenza di pubblicazione usata per creare un gestore di protezione.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public PublishingLicenseInfo (const std:: Vector\<uint8_t\>& serializedPublishingLicense)  | _Non ancora documentato._
public PublishingLicenseInfo (const std:: Vector\<uint8_t\>& serializedPreLicense, const std:: Vector\<uint8_t\>& serializedPublishingLicense)  | _Non ancora documentato._
public void SetParsedData (const std:: Vector\<std:: String\>& Domains, const std:: String & serverPublicCert, const std:: String & contentId, const std:: String & issuerId)  | _Non ancora documentato._
public void SetDoubleKeyData (const std:: String & Algorithm, const std:: Map\<std:: String, std:: String\>& doubleKeyApplicationData)  | _Non ancora documentato._
public const std:: Vector\<uint8_t\>& GetSerializedPublishingLicense () const  | _Non ancora documentato._
public const std:: Vector\<uint8_t\>& GetPreLicense () const  | _Non ancora documentato._
public const std:: Vector\<std:: String\>& getdomains () const  | _Non ancora documentato._
public const std:: String & GetServerPublicCertificate () const  | _Non ancora documentato._
public const std:: String & GetIssuerId () const  | _Non ancora documentato._
public const std:: String & GetContentId () const  | _Non ancora documentato._
public bool IsLicenseParsed () const  | _Non ancora documentato._
public bool HasPreLicense () const  | _Non ancora documentato._
public bool GetIsDoubleKeyLicense () const  | _Non ancora documentato._
public const std:: String & GetDoubleKeyAlgorithm () const  | _Non ancora documentato._
public const std:: Map\<std:: String, std:: String\>& GetDoubleKeyApplicationData () const  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo (funzione)
_Non ancora documentato._

  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo (funzione)
_Non ancora documentato._

  
### <a name="setparseddata-function"></a>SetParsedData (funzione)
_Non ancora documentato._

  
### <a name="setdoublekeydata-function"></a>SetDoubleKeyData (funzione)
_Non ancora documentato._

  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense (funzione)
_Non ancora documentato._

  
### <a name="getprelicense-function"></a>GetPreLicense (funzione)
_Non ancora documentato._

  
### <a name="getdomains-function"></a>Funzione getdomains
_Non ancora documentato._

  
### <a name="getserverpubliccertificate-function"></a>GetServerPublicCertificate (funzione)
_Non ancora documentato._

  
### <a name="getissuerid-function"></a>GetIssuerId (funzione)
_Non ancora documentato._

  
### <a name="getcontentid-function"></a>GetContentId (funzione)
_Non ancora documentato._

  
### <a name="islicenseparsed-function"></a>IsLicenseParsed (funzione)
_Non ancora documentato._

  
### <a name="hasprelicense-function"></a>HasPreLicense (funzione)
_Non ancora documentato._

  
### <a name="getisdoublekeylicense-function"></a>GetIsDoubleKeyLicense (funzione)
_Non ancora documentato._

  
### <a name="getdoublekeyalgorithm-function"></a>GetDoubleKeyAlgorithm (funzione)
_Non ancora documentato._

  
### <a name="getdoublekeyapplicationdata-function"></a>GetDoubleKeyApplicationData (funzione)
_Non ancora documentato._
