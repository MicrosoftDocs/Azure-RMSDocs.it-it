---
title: "File dell’ambiente di sviluppo | Azure RMS"
description: Questo argomento illustra i file dell'ambiente di sviluppo e i relativi percorsi di installazione nel computer in uso.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: fa85dde3f578f51efa57af78e211d3e712378b61


---

# File dell'ambiente di sviluppo

Questo argomento illustra i file dell'ambiente di sviluppo e i relativi percorsi di installazione nel computer in uso.

Rights Management Services SDK 2.1 include i file seguenti, installati nel computer nel percorso predefinito o in quello specificato, % MsipcSDKDir %.

|File|Percorso|Descrizione|
|----|----|-----------|
|Readme.htm| \ | Contiene i collegamenti alla Guida di RMS e alle [Note sulla versione](release-notes-rtm.md).|
|Isvtier5appsigningprivkey.dat|\bin|Contiene la chiave privata usata per generare un manifesto da utilizzare durante lo sviluppo di un'applicazione abilitata per RMS.|
|Isvtier5appsigningpubkey.dat|\bin|Contiene la chiave pubblicata usata per generare un manifesto da utilizzare durante lo sviluppo di un'applicazione abilitata per RMS.|
|Isvtier5appsignsdk_client.Xml|\bin|Usato per generare un manifesto da utilizzare durante lo sviluppo di un'applicazione abilitata per RMS.|
|YourAppName.isv.mcf|\bin|File di configurazione di un manifesto boilerplate utilizzabile per generare un manifesto durante lo sviluppo di un'applicazione abilitata per RMS.|
|Ipcsecproc_isv.dll|\bin\x86|DLL usata internamente per le applicazioni x86 da Active Directory Rights Management Services Client 2.1 quando si lavora nella gerarchia ISV.|
|Ipcsecproc_ssp_isv.dll|\bin\x86|DLL usata internamente per le applicazioni x86 da AD RMS 2.1 quando si lavora nella gerarchia ISV.|
|Ipcsecproc_isv.dll|\bin\x64.|DLL usata internamente per le applicazioni x64 da AD RMS Client 2.1 quando si lavora nella gerarchia ISV.|
|Ipcsecproc_ssp_isv.dll|\bin\x64.|DLL usata internamente per le applicazioni x64 da AD RMS Client 2.1 quando si lavora nella gerarchia ISV.|
|Msipc.h|\inc|File di inclusione principale per RMS SDK 2.1.|
|Ipcprot.h|\inc|Contiene l'interfaccia pubblica esportata da RMS SDK 2.1.|
|Ipcbase.h|\inc|Contiene i tipi di base e le funzioni di supporto esportate da RMS SDK 2.1.|
|Ipcerror.h|\inc|Contiene i codici di errore pubblici esportati da RMS SDK 2.1.|
|Ipcfile.h|\inc|Contiene le interfacce File API esportate da RMS SDK 2.1.|
|Msipc.lib|\lib|Libreria a cui eseguire il collegamento quando si usa RMS SDK 2.1 per creare applicazioni x86.|
|Msipc_s.lib|\lib|Fornisce il punto di ingresso per [<strong>IpcInitialize</strong>](/information-protection/sdk/2.1/api/win/functions#msipc_ipcinitialize) per le applicazioni x86.|
|Msipc.lib|\lib\x64|Libreria a cui eseguire il collegamento quando si usa RMS SDK 2.1 per creare applicazioni x64.|
|Msipc_s.lib|\lib\x64|Fornisce il punto di ingresso per [<strong>IpcInitialize</strong>](/information-protection/sdk/2.1/api/win/functions#msipc_ipcinitialize) per le applicazioni x64.|
|Genmanifest.exe|\tools|Genera un manifesto da utilizzare durante lo sviluppo di un'applicazione abilitata per RMS.|
 

 

 



<!--HONumber=Sep16_HO5-->


