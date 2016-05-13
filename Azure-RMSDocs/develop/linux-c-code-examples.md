---
# required metadata

title: Esempi di codice Linux | Azure RMS
description: In questo argomento sono presentati scenari elementi di codice importanti per la versione Linux di RMS SDK.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 11acef4b-67f8-4e45-a0e7-d9310213b5f9

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Esempi di codice Linux

In questo argomento sono presentati scenari elementi di codice importanti per la versione Linux di RMS SDK.

I frammenti di codice riportati di seguito provengono da applicazioni di esempio, *rms\_sample* e *rmsauth\_sample*. Per ulteriori informazioni, vedere gli [esempi](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples) sul repository GitHub.

-   [**Scenario**: accesso alle informazioni sui criteri di protezione da un file protetto](#scenario__access_protection_policy_information_from_a___protected_file)
-   [**Scenario**: creazione di un nuovo file protetto tramite un modello](#scenario__create_a_new_protected_file_using_a_template)
-   [**Scenario**: protezione personalizzata di un file](#scenario__protect_a_file_using_custom_protection)
-   [WorkerThread - un metodo di supporto](#workerthread_-_a_supporting_method)
-   [**Scenario**: autenticazione di RMS](#scenario__rms_authentication)

## Scenario: accesso alle informazioni sui criteri di protezione da un file protetto

**Apre e legge un file protetto RMS**
**Origine**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: dopo aver ottenuto un nome file dall'utente, leggere i certificati (vedere *MainWindow::addCertificates*), impostare il callback di autorizzazione con l'ID Client e l'URL di reindirizzamento, chiamare *ConvertFromPFile* (vedere l'esempio di codice seguente), quindi leggere il nome del criterio di protezione, la relativa descrizione e il periodo di validità del contenuto.

**C++**:

    void MainWindow::ConvertFromPFILE(const string&amp; fileIn,
        const string&amp; clientId,
        const string&amp; redirectUrl,
        const string&amp; clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this-&gt;consent);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e)
    {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }

**creazione di un flusso di file protetto**
**Origine**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: questo metodo crea un flusso di file protetto dal flusso di supporto passato tramite il metodo SDK, *ProtectedFileStream::Aquire*, che viene quindi restituito al chiamante.

**C++**:

    shared_ptr&lt;GetProtectedFileStreamResult&gt;PFileConverter::ConvertFromPFile(
    const string           &amp; userId,
    shared_ptr&lt;istream&gt;      inStream,
    shared_ptr&lt;iostream&gt;     outStream,
    IAuthenticationCallback&amp; auth,
    IConsentCallback       &amp; consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast&lt;ResponseCacheFlags&gt;(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) &amp;&amp; (fsResult-&gt;m_status == Success) &amp;&amp;
      (fsResult-&gt;m_stream != nullptr)) {
    auto pfs = fsResult-&gt;m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs-&gt;Size();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }

## Scenario: creazione di un nuovo file protetto tramite un modello

**Consente di proteggere un file con un modello di utente selezionato**
**Origine**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: dopo aver ottenuto un nome file dall'utente, aver letto i certificati (vedere *MainWindow::addCertificates*) e aver impostare il callback di autorizzazione con l'ID Client e l'URL di reindirizzamento, il file selezionato è protetto tramite chiamata a *ConvertToPFileTemplates* (vedere l'esempio di codice seguente).

**C++**:

    void MainWindow::ConvertToPFILEUsingTemplates(const string&amp; fileIn,
                                              const string&amp; clientId,
                                              const string&amp; redirectUrl,
                                              const string&amp; clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this-&gt;consent, this-&gt;templates);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
   catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**Consente di proteggere un file utilizzando un criterio creato da un modello**
**Origine**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: viene recuperato un elenco dei modelli associati all'utente, quindi il modello selezionato viene usato per creare un criterio che a sua volta verrà usato per proteggere il file.

**C++**:

    void PFileConverter::ConvertToPFileTemplates(const string           &amp; userId,
                                             shared_ptr&lt;istream&gt;      inStream,
                                             const string           &amp; fileExt,
                                             std::shared_ptr&lt;iostream&gt;outStream,
                                             IAuthenticationCallback&amp; auth,
                                             IConsentCallback&amp; /*consent*/,
                                             ITemplatesCallback     &amp; templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos &lt; templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }

**consente di proteggere un file con un criterio specifico**
**Origine**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: creare un flusso di file protetto tramite il criterio specificato, quindi proteggere tale file.

**C++**:

    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr&lt;UserPolicy&gt;   policy,
                                               shared_ptr&lt;istream&gt;      inStream,
                                               const string           &amp; fileExt,
                                               std::shared_ptr&lt;iostream&gt;outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream-&gt;Size();
    
    inStream-&gt;seekg(0, ios::end);
    totalSize = inStream-&gt;tellg();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream-&gt;Flush();
    }
    


## Scenario: protezione personalizzata di un file

**Consente di proteggere un file usando una protezione personalizzata**
**Origine**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: dopo aver ottenuto un nome file dall'utente, aver letto i certificati (vedere *MainWindow::addCertificates*), aver raccolto le informazioni sui diritti dall'utente e aver impostare il callback di autorizzazione con l'ID Client e l'URL di reindirizzamento, il file selezionato è protetto tramite chiamata a *ConvertToPFilePredefinedRights* (vedere l'esempio di codice seguente).

**C++**:

    void MainWindow::ConvertToPFILEUsingRights(const string            &amp; fileIn,
                                           const vector&lt;UserRights&gt;&amp; userRights,
                                           const string            &amp; clientId,
                                           const string            &amp; redirectUrl,
                                           const string            &amp; clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog(&quot;ERROR: &quot;, &quot;Please fill email and check rights&quot;);
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this-&gt;consent,
      userRights);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**consente di creare un criterio di protezione con diritti specifici selezionati dall'utente**
**Origine**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descrizione**: creare un descrittore di criteri e inserirvi le informazioni sui diritti dell'utente, quindi utilizzarlo per creare un criterio utente. Questo criterio viene utilizzato per proteggere il file selezionato tramite una chiamata a *ConvertToPFileUsingPolicy* (vedere questo procedimento nella sezione precedente di questo argomento).

**C++**:

    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            &amp; userId,
    shared_ptr&lt;istream&gt;       inStream,
    const string            &amp; fileExt,
    shared_ptr&lt;iostream&gt;      outStream,
    IAuthenticationCallback &amp; auth,
    IConsentCallback&amp; /*consent*/,
    const vector&lt;UserRights&gt;&amp; userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared&lt;string&gt;(&quot;https://client.test.app&quot;));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name(&quot;Test Name&quot;);
    desc.Description(&quot;Test Description&quot;);
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    

## WorkerThread - un metodo di supporto


Il *WorkerThread()* viene chiamato da due degli scenari di esempio precedenti, **Creazione di un flusso di file protetto** e **Protezione di un file con un criterio specifico**, nel modo seguente:

**C++**:

    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));


**metodo di supporto, WorkerThread()**

**C++**:

    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector&lt;thread&gt; threadPool;
    
    static void WorkerThread(shared_ptr&lt;iostream&gt;           stdStream,
                         shared_ptr&lt;ProtectedFileStream&gt;pStream,
                         bool                           modeWrite) {
    vector&lt;uint8_t&gt; buffer(4096);
    int64_t bufferSize = static_cast&lt;int64_t&gt;(buffer.size());
    
    while (totalSize - readPosition &gt; 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition &lt;= 0) {
      threadLocker.unlock();
      return;
    }
    
    // get read/write offset
    int64_t offsetRead  = readPosition;
    int64_t offsetWrite = writePosition;
    int64_t toProcess   = min(bufferSize, totalSize - readPosition);
    readPosition  += toProcess;
    writePosition += toProcess;
    
    // no need to lock more
    threadLocker.unlock();
    
    if (modeWrite) {
      // stdStream is not thread safe!!!
      try {
        threadLocker.lock();
    
        stdStream-&gt;seekg(offsetRead);
        stdStream-&gt;read(reinterpret_cast&lt;char *&gt;(&amp;buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream-&gt;WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException(&quot;Error while writing data&quot;);
        }
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    } else {
      auto read =
        pStream-&gt;ReadAsync(&amp;buffer[0],
                           toProcess,
                           offsetRead,
                           std::launch::deferred).get();
    
      if (read == 0) {
        break;
      }
    
      try {
        // stdStream is not thread safe!!!
        threadLocker.lock();
    
        // seek to write
        stdStream-&gt;seekp(offsetWrite);
        stdStream-&gt;write(reinterpret_cast&lt;const char *&gt;(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    }
    }
    }


## scenario: autenticazione di RMS

Gli esempi seguenti illustrano due diversi approcci di autenticazione, relativi a come ottenere i token oAuth2 per l'autenticazione di Azure con l'interfaccia utente e senza l'interfaccia utente.
**Acquisizione del token di autenticazione oAuth2 con l'interfaccia utente**
**Origine**: [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Passaggio 1**: creare un punto condiviso dell'oggetto **rmsauth::FileCache**.
Descrizione: è possibile impostare il percorso della cache o usare l'impostazione predefinita.

**C++**:

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**Passaggio 2**: creare l'oggetto **rmsauth::AuthenticationContext**
Descrizione: specificare l'*URI dell'autorità* di Azure e l'oggetto *FileCache*.

**C++**:

    AuthenticationContext authContext(
                              std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                              AuthorityValidationType::False,
                              FileCachePtr);


**Passaggio 3**: chiamare il metodo **aquireToken** dell'oggetto **authContext** e specificare i parametri successivi:
Descrizione:

-   *Risorsa richiesta*: risorsa protetta a cui si vuole accedere
-   *ID univoco del client*: in genere un GUID
-   *URI di reindirizzamento*: l'URI a cui verrà reindirizzato dopo il recupero dei token di autenticazione
-   *Comportamento della richiesta di autenticazione*: se si imposta **PromptBehavior::Auto**, la libreria tenta di usare cache e token di aggiornamento, se necessario
-   *ID utente* -nome utente visualizzato nella finestra del prompt

**C++**:

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                std::string(“https://client.test.app”),
                PromptBehavior::Auto,
                std::string(“john.smith@msopentechtest01.onmicrosoft.com”));


**Passaggio 4**: ottenere il token di accesso dal risultato
Descrizione: chiamare il metodo **result-&gt; accessToken()**

**Nota**  Uno qualsiasi dei metodi della libreria di autenticazione può generare **rmsauth::Exception**

 
**Acquisizione del token di autenticazione oAuth2 senza l'interfaccia utente**
**Origine**: [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Passaggio 1**: creare un punto condiviso dell'oggetto **rmsauth::FileCache**
Descrizione: è possibile impostare il percorso della cache o usare l'impostazione predefinita

**C++**:

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**Passaggio 2**: creare l'oggetto **UserCredential**
Descrizione: specificare l'*accesso utente* e la *password*

**C++**:

    auto userCred = std::make_shared&lt;UserCredential&gt;(&quot;john.smith@msopentechtest01.onmicrosoft.com&quot;,
                                                 &quot;SomePass&quot;);


**Passaggio 3**: creare l'oggetto **rmsauth::AuthenticationContext**
Descrizione: specificare l'*URI* dell'autorità di Azure e l'oggetto *FileCache*.

**C++**:

    AuthenticationContext authContext(
                        std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                        AuthorityValidationType::False,
                        FileCachePtr);


**Passaggio 4**: chiamare il metodo **aquireToken** di **authContext** e specificare i parametri:
-   *Risorsa richiesta*: risorsa protetta a cui si vuole accedere
-   *ID univoco del client*: in genere un GUID
-   *Credenziali utente*: passare l'oggetto creato

**C++**:

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                userCred);


**Passaggio 5**: ottenere il token di accesso dal risultato
Descrizione: chiamare il metodo **result-&gt; accessToken()**

**Nota**  Uno qualsiasi dei metodi della libreria di autenticazione può generare **rmsauth::Exception**



<!--HONumber=Apr16_HO3-->


