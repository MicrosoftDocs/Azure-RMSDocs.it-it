---
title: Configurazione dell&quot;API file | Azure RMS
description: "Il comportamento dell&quot;API file può essere configurato tramite le impostazioni del Registro di sistema."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 890319e80941232af636fce6913f362ad48632f6
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="file-api-configuration"></a>Configurazione dell'API file


Il comportamento dell'API file può essere configurato tramite le impostazioni del Registro di sistema.

L'API file offre due tipi di protezione: la protezione nativa e la protezione PFile.

-   **Protezione nativa**: il file è protetto in un formato di AD RMS su cui si basa il tipo MIME (estensione del file).
-   **Protezione PFile**: il file è protetto in base al formato di File di protetto AD RMS (PFile).

Per ulteriori informazioni sui formati di file supportati, vedere **Dettagli sul supporto per il file delle API file** in questo argomento.

## <a name="keykey-value-types-and-descriptions"></a>Descrizioni e tipi di valore chiave/chiave

Le sezioni seguenti descrivono le chiavi e valori chiave che controllano la crittografia.

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection`

**Tipo**: chiave

**Descrizione**: contiene la configurazione generale dell'API file.

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>`

**Tipo**: chiave

**Descrizione**: specifica le informazioni di configurazione di un'estensione file specifica, ad esempio, TXT, JPG e così via.

- Il carattere jolly '*', è consentito, tuttavia, un'impostazione per un'estensione specifica ha la precedenza sull'impostazione con caratteri jolly. Il carattere jolly non influisce sulle impostazioni dei file di Microsoft Office; questi devono essere disabilitati in modo esplicito per tipo di file.
- Per specificare i file che non hanno un'estensione, usare “.”
- Non specificare il carattere “.” carattere quando si specifica la chiave per un'estensione di file specifica, ad esempio usare `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` per specificare le impostazioni per i file con estensione .txt. (non usare `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`).

Impostare il valore della **crittografia** della chiave per specificare il comportamento di protezione. Se il valore della **crittografia** non è impostato, si osserva il comportamento predefinito per il tipo di file.


### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>\Encryption*`

**Tipo**: REG_SZ

**Descrizione**: contiene uno dei tre valori:

- **Off**: la crittografia è disabilitata.

> [!Note]
> Questa impostazione non è rilevante per la decrittografia. È possibile decrittografare qualsiasi file crittografato, se crittografato tramite la protezione nativa o Pfile, purché l'utente disponga del diritto di **ESTRAZIONE**.

- **Nativa**: si usa la crittografia nativa. Per i file di Office, il file crittografato avrà la stessa estensione del file originale. Ad esempio, un file con estensione .docx sarà crittografato in un file con estensione .docx. Per altri file a cui può essere applicata la protezione nativa, il file sarà crittografato in un file con un'estensione del formato p*zzz*, dove *zzz* è l'estensione del file originale. Ad esempio, i file con estensione txt sono crittografati in un file con estensione ptxt. Un elenco di estensioni di file a cui può essere applicata la protezione nativa è indicato di seguito.

- **Pfile**: si usa la crittografia PFile. All'estensione originale del file crittografato sarà aggiunto pfile. Dopo la crittografia, ad esempio, l'estensione di un file sarà .txt.pfile.


> [!Note]
> Questa impostazione non incide sui formati di file Office. Ad esempio, se il valore `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` è impostato su &quot;Pfile", i file con estensione docx verranno comunque crittografati con la protezione nativa e l'estensione del file crittografato sarà ancora docx.

L'impostazione di un valore diverso o la mancata impostazione produce il comportamento predefinito.

## <a name="default-behavior-for-different-file-formats"></a>Comportamento predefinito dei diversi formati dei file

-   **File di Office** è abilitata la crittografia nativa.
-   **File txt, xml, jpg, jpeg, pdf, png, tiff, bmp, gif, giff, jpe, jfif, jif** è abilitata la crittografia nativa (xxx diventa pxxx)
-   **Tutti gli altri file** è abilitata la crittografia del file protetto (pfile) (xxx diventa xxx.pfile)

Se si tenta di crittografare un tipo di file bloccato, si verifica un errore [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx).

### <a name="file-api---file-support-details"></a>API file: dettagli sul supporto dei file

È possibile aggiungere il supporto nativo per qualsiasi tipo di file (estensione). Ad esempio, per tutte le estensioni &lt;ext&gt; (non Office), verrà usata l'estensione \*p&lt;ext&gt; se la configurazione dell'amministratore per l'estensione è "NATIVA".

**File di Office**

-   Estensioni di file: doc, dot, xla, xls, xlt, pps, ppt, docm, docx, dotm, dotx, xlam, xlsb, xlsm, xlsx, ppam, xltx, xps, potm, potx, ppsx, ppsm, pptm, pptx, thmx.
-   Tipo di protezione = Nativa (impostazione predefinita): sample.docx viene crittografato in sample.docx
-   Tipo di protezione = Pfile: per i file Office ha lo stesso effetto della crittografia Nativa.
-   Off: Disabilita la crittografia.

**File PDF**

-   Tipo di protezione = Nativa: sample.pdf è crittografato e denominato sample.ppdf
-   Tipo di protezione = Pfile: sample.pdf è crittografato e denominato sample.pdf.pfile.
-   Off: Disabilita la crittografia.

**Tutti gli altri formati di file**

-   Tipo di protezione = Pfile: sample.*zzz* è crittografato e denominato sample.*zzz*.pfile, dove *zzz* è l'estensione del file originale.
-   Off: Disabilita la crittografia.

### <a name="examples"></a>Esempi

Le seguenti impostazioni abilitano la crittografia PFile per file con estensione txt. Ai file di Office sarà applicata la protezione nativa (per impostazione predefinita), ai file con estensione .txt sarà applicata la protezione PFile e a tutti gli altri file la protezione sarà bloccata (per impostazione predefinita).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

Le seguenti impostazioni abilitano la crittografia PFile per tutti i file non di Office, ad eccezione di file con estensione txt. Ai file di Office sarà applicata la protezione nativa (per impostazione predefinita), ai file con estensione .txt la protezione sarà bloccata e a tutti gli altri file sarà applicata la protezione PFile.

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

Le seguenti impostazioni disabilitano la crittografia nativa per i file docx. Ai file di Office sarà applicata la protezione nativa (per impostazione predefinita) e a tutti gli altri file la protezione sarà bloccata (per impostazione predefinita).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## <a name="related-topics"></a>Argomenti correlati

- [Note per gli sviluppatori](developer-notes.md)
- [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]