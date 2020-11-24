---
title: Esempi di codice Android | Azure RMS
description: In questo argomento sono presentati importanti elementi di codice per la versione Android di RMS SDK.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 075eae9729ac9175e570a8f0386dadcbfc22bb05
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568334"
---
# <a name="android-code-examples"></a>Esempi di codice Android

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Questo articolo mostra come scrivere il codice degli elementi per la versione Android di RMS SDK.

**Nota** In questo articolo il termine _MSIPC_ (Microsoft Information Protection and Control) si riferisce al processo client.


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Uso di Microsoft Rights Management SDK 4.2: scenari principali

Questi esempi di codice sono tratti da un'applicazione di esempio di dimensioni maggiori che rappresenta scenari di sviluppo importanti per orientarsi in questo SDK. Questi esempi illustrano come usare:

- Il formato di file protetto da Microsoft, denominato anche _file protetto_.
- Formati di file protetti personalizzati
- Controlli dell'interfaccia utente personalizzati

È disponibile l’applicazione di esempio *MSIPCSampleApp* da usare con questo SDK per il sistema operativo Android. Per altre informazioni, vedere [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android).

### <a name="scenario-consume-an-rms-protected-file"></a>Scenario: utilizzo di un file protetto RMS

- **Passaggio 1**: Creare un oggetto [ProtectedFileInputStream](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-class-java).

    **Origine**: *MsipcAuthenticationCallback.java*

    **Descrizione**: creare un'istanza di un oggetto [ProtectedFileInputStream](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-class-java) e implementare l'autenticazione del servizio.  Usare [AuthenticationRequestCallback](/previous-versions/windows/desktop/msipcthin2/authenticationcompletioncallback-interface-java) per ottenere un token passando un'istanza di **AuthenticationRequestCallback**, come parametro *mRmsAuthCallback*, all'API MSIPC. Vedere la chiamata a [ProtectedFileInputStream.create](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-class-java) verso la fine della sezione del codice di esempio seguente.

    ``` java
        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }
    ```

- **Passaggio 2**: Configurare l'autenticazione usando Active Directory Authentication Library (ADAL).

    **Origine**: *MsipcAuthenticationCallback. Java*.

    **Descrizione**: questo passaggio usa ADAL per implementare [AuthenticationRequestCallback](/previous-versions/windows/desktop/msipcthin2/authenticationrequestcallback-interface-java) con parametri di autenticazione di esempio. Per altre informazioni, vedere [Azure AD Authentication Library (ADAL)](/previous-versions/azure/jj573266(v=azure.100)).


   ``` java
       class MsipcAuthenticationCallback implements AuthenticationRequestCallback
       {

       …

       @Override
       public void getToken(Map<String, String> authenticationParametersMap,
                            final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
       {
           String authority = authenticationParametersMap.get("oauth2.authority");
           String resource = authenticationParametersMap.get("oauth2.resource");
           String userId = authenticationParametersMap.get("userId");
           final String userHint = (userId == null)? "" : userId;
           AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
           if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
           {
               try
               {
                   authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                   App.getInstance().setAuthenticationContext(authenticationContext);
               }
               catch (NoSuchAlgorithmException e)
               {
                   …
                   authenticationCompletionCallbackToMsipc.onFailure();
               }
               catch (NoSuchPaddingException e)
               {
                   …
                   authenticationCompletionCallbackToMsipc.onFailure();
               }
          }
           App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                          "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                           {
                               @Override
                               public void onError(Exception exc)
                               {
                                   …
                                   if (exc instanceof AuthenticationCancelError)
                                   {
                                        …
                                       authenticationCompletionCallbackToMsipc.onCancel();
                                   }
                                   else
                                   {
                                        …
                                       authenticationCompletionCallbackToMsipc.onFailure();
                                   }
                               }

                               @Override
                               public void onSuccess(AuthenticationResult result)
                               {
                                   …
                                   if (result == null || result.getAccessToken() == null
                                           || result.getAccessToken().isEmpty())
                                   {
                                        …
                                   }
                                   else
                                   {
                                       // request is successful
                                       …
                                       authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                   }
                               }
                           }

                           );
                     }
   ```

- **Passaggio 3**: Verificare se esiste il diritto di **modifica** per questo utente su questo contenuto tramite il metodo [UserPolicy.accessCheck](/previous-versions/windows/desktop/msipcthin2/userpolicy-accesscheck-method-java).

    **Origine**: *TextEditorFragment.java*

    ``` java
         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }
    ```


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scenario: creazione di un nuovo file protetto tramite un modello

Questo scenario inizia con il recupero di un elenco di modelli e la selezione del primo di essi per creare un criterio e procede quindi con la creazione e la scrittura di contenuto nel nuovo file protetto.

- **Passaggio 1**: Ottenere un elenco di modelli tramite un oggetto [TemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/templatedescriptor-class-java).

    **Origine**: *MsipcTaskFragment.java*

    ``` java
    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>()
      {
          @Override
          public Context getContext()
          {
              …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      };
      try
      {
              …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback);
      }
      catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
      {
              …
      }
    ```


- **Passaggio 2**: Creare una classe [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) usando il primo modello dell'elenco.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>()
      {
          @Override
          public Context getContext()
          {
              …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      };
      try
      {
           …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback,
                            UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
           …
      }
      catch (InvalidParameterException e)
      {
              …
      }
    ```


-  **Passaggio 3**: Creare una classe [ProtectedFileOutputStream](/previous-versions/windows/desktop/msipcthin2/protectedfileoutputstream-class-java) e scriverci il contenuto.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
    private void createPTxt(final byte[] contentToProtect)
        {
             …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>()
            {
                @Override
                public Context getContext()
                {
                 …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }
    ```


### <a name="scenario-open-a-custom-protected-file"></a>Scenario: aprire di un file protetto personalizzato

- **Passaggio 1**: Creare un oggetto [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) da *serializedContentPolicy*.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>()
            {
                @Override
                public void onSuccess(UserPolicy userPolicy)
                {
                  …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };
            try
            {
                ...

                // Read the serializedContentPolicyLength from the inputStream.
                long serializedContentPolicyLength = readUnsignedInt(inputStream);

                // Read the PL bytes from the input stream using the PL size.
                byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength];
                inputStream.read(serializedContentPolicy);

                ...

                UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,
                userPolicyCreationCallbackFromSerializedContentPolicy);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
            ...
            }
            catch (IOException e)
            {
            ...
            }
   ```


- **Passaggio 2**: Creare una classe [CustomProtectedInputStream](/previous-versions/windows/desktop/msipcthin2/customprotectedinputstream-class-java) usando la classe [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) del **Passaggio 1**.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>()
      {
         @Override
         public Context getContext()
         {
             …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try
    {
      ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,
                                     encryptedContentLength,
                                     customProtectedInputStreamCreationCallback);
    }
    catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
    {
      ...
    }
    catch (IOException e)
    {
      ...
    }
    ```


- **Passaggio 3**: Leggere il contenuto da [CustomProtectedInputStream](/previous-versions/windows/desktop/msipcthin2/customprotectedinputstream-class-java) in *mDecryptedContent* e chiudere.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
    @Override
    public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
    {
      mUserPolicy = customProtectedInputStream.getUserPolicy();
      ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;
      byte[] dataChunk = new byte[16384];

      try
      {
        while ((nRead = customProtectedInputStream.read(dataChunk, 0,
                                                            dataChunk.length)) != -1)
        {
           buffer.write(dataChunk, 0, nRead);
        }

        buffer.flush();
        mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();
        customProtectedInputStream.close();
      }
      catch (IOException e)
      {
        ...
      }
    }
    ```


### <a name="scenario-create-a-custom-protected-file-using-a-custom-policy"></a>Scenario: creare un file protetto personalizzato usando un criterio personalizzato

- **Passaggio 1**: Creare un descrittore di criteri con un indirizzo di posta elettronica fornito dall'utente.

    **Origine**: *MsipcTaskFragment.java*

    **Descrizione**: in pratica vengono creati gli oggetti [UserRights](/previous-versions/windows/desktop/msipcthin2/userrights-class-java) e [PolicyDescriptor](/previous-versions/windows/desktop/msipcthin2/policydescriptor-interface-java) usando gli input dell'utente dall'interfaccia del dispositivo.

    ``` java
      // create userRights list
      UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),
        Arrays.asList( CommonRights.View, EditableDocumentRights.Print));
      ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();
      usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list
      PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(
                                                             usersRigthsList);
      policyDescriptor.setOfflineCacheLifetimeInDays(10);
      policyDescriptor.setContentValidUntil(new Date());
    ```


- **Passaggio 2**: Creare una classe personalizzata [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) dal descrittore del criterio, ovvero *selectedDescriptor*.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,
         mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
    ```


- **Passaggio 3**: Creare e scrivere il contenuto per la classe [CustomProtectedOutputStream](/previous-versions/windows/desktop/msipcthin2/customprotectedoutputstream-class-java) e chiudere.

    **Origine**: *MsipcTaskFragment.java*

    ``` java
    File file = new File(filePath);
        final OutputStream outputStream = new FileOutputStream(file);
        CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>()
        {
            @Override
            public Context getContext()
            {
              …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }
    ```