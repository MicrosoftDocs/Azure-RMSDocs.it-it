---
title: Impostazioni del Registro di sistema per il connettore di Rights Management - AIP
description: Informazioni sulle impostazioni del Registro di sistema sui server tramite il connettore RMS. Il metodo consigliato per configurare tali impostazioni è usare lo strumento di configurazione server per il connettore Microsoft RMS.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e9bef060e2147fe42505174493bad44af06ff28a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384860"
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Impostazioni del Registro di sistema per il connettore Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le tabelle riportate nelle sezioni seguenti solo se si desidera controllare o aggiungere manualmente impostazioni del Registro di sistema sui server che eseguono Exchange, SharePoint o Windows Server. Queste impostazioni del Registro di sistema configurano i server per usare il [connettore RMS](deploy-rms-connector.md). Il metodo consigliato per configurare i server è usare lo strumento di configurazione server per il connettore Microsoft RMS.

Istruzioni per l'uso delle impostazioni:

-   *\<YourTenantURL>* è l'URL del servizio Rights Management di Azure per il tenant di Azure Information Protection. Per individuare questo valore:

    1.  Eseguire il cmdlet [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) per il servizio Rights Management di Azure. Se il modulo AIPService non è ancora stato installato, vedere [installazione del modulo PowerShell di AIPService](install-powershell.md).

    2.  Nell'output identificare il valore **LicensingIntranetDistributionPointUrl**.

        Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  In questo valore rimuovere **/_wmcs/licensing** dalla stringa. La stringa rimanente corrisponde all'URL del servizio Azure Rights Management. Nell'esempio, l'URL del servizio Azure Rights Management è il valore seguente:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**
        
        È possibile verificare di avere il valore corretto eseguendo il comando PowerShell seguente:

        ```ps
        (Get-AipServiceConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]
        ```

-   *\<ConnectorFQDN>* è il nome di bilanciamento del carico definito in DNS per il connettore. ad esempio **rmsconnector.contoso.com**.

-   Usare il prefisso HTTPS per l'URL del connettore se quest'ultimo è stato configurato per comunicare con i server locali mediante tale protocollo. Per altre informazioni, vedere la sezione [Configurazione del connettore RMS per l'uso di HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) nelle istruzioni principali. L'URL del servizio Azure Rights Management usa sempre il protocollo HTTPS.


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Impostazioni del Registro di sistema per Exchange 2016 o Exchange 2013

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo**: REG_SZ

**Valore**: predefinito

**Dati**: https:// *\<YourTenantURL>* /_wmcs/Certification

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo**: REG_SZ

**Valore**: predefinito

**Dati**: https:// *\<YourTenantURL>* /_wmcs/licensing

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo**: REG_SZ

**Valore**: https://*\<YourTenantURL>*


**Data**: uno dei seguenti, a seconda che si usi http o HTTPS da Exchange Server al connettore RMS:

- http://*< \connectorfqdn>*

- https://*< \connectorfqdn>*

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo**: REG_SZ

**Valore**: https://*< \yourtenanturl>*


**Data**: uno dei seguenti, a seconda che si usi http o HTTPS da Exchange Server al connettore RMS:

- http://*< \connectorfqdn>*

- https://*< \connectorfqdn>*


## <a name="exchange-2010-registry-settings"></a>Impostazioni del Registro di sistema per Exchange 2010

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo**: REG_SZ

**Valore**: predefinito

**Data**: https://*< \yourtenanturl>*/_wmcs/Certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo**: REG_SZ

**Valore**: predefinito

**Data**: https://*< \yourtenanturl>*/_wmcs/licensing

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo**: REG_SZ

**Valore**: https://*< \yourtenanturl>*

**Data**: uno dei seguenti, a seconda che si usi http o HTTPS da Exchange Server al connettore RMS:

- http://*< \connectorfqdn>*

- https://*< \connectorfqdn>*

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo**: REG_SZ

**Valore**: https://*< \yourtenanturl>*

**Data**: uno dei seguenti, a seconda che si usi http o HTTPS da Exchange Server al connettore RMS:

- http://*< \connectorfqdn>*

- https://*< \connectorfqdn>*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>Impostazioni del Registro di sistema di SharePoint 2016 o SharePoint 2013

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo**: REG_SZ

**Valore**: https://*< \yourtenanturl>*/_wmcs/licensing


**Data**: uno dei seguenti, a seconda che si usi http o HTTPS dal server SharePoint al connettore RMS:

- http://*< \connectorfqdn>*/_wmcs/licensing

- https://*< \connectorfqdn>*/_wmcs/licensing

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo**: REG_SZ

**Valore**: predefinito

**Data**: uno dei seguenti, a seconda che si usi http o HTTPS dal server SharePoint al connettore RMS:

- http://*< \connectorfqdn>*/_wmcs/Certification

- https://*< \connectorfqdn>*/_wmcs/Certification

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo**: REG_SZ

**Valore**: predefinito


**Data**: uno dei seguenti, a seconda che si usi http o HTTPS dal server SharePoint al connettore RMS:

- http://*< \connectorfqdn>*/_wmcs/licensing

- https://*< \connectorfqdn>*/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>Impostazioni del Registro di sistema per i file server e la funzionalità Infrastruttura di classificazione file

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo**: REG_SZ

**Valore**: predefinito

**Data**: http://*< \connectorfqdn>*/_wmcs/licensing

---

**Percorso del registro di sistema**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo**: REG_SZ

**Valore**: predefinito

**Data**: http://*< \connectorfqdn>*/_wmcs/Certification


Tornare a [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md)
