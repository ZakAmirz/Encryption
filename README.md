Encryption
==========

For the latest Habbo version use the HabboEncryptionHandlerV2 class.
To initialize the Encryption handler V2. Put this in your main class somewhere

```
  RsaKeyHolder keys = new RsaKeyHolder();
  HabboEncryptionHandlerV2.Initialize(keys);
```

For the initialization for the crypto event is the packet: string, string

```
  response.WriteString(HabboEncryptionHandlerV2.GetRsaDiffieHellmanPrimeKey());
  response.WriteString(HabboEncryptionHandlerV2.GetRsaDiffieHellmanGeneratorKey());
```

And for the last message event which you get after sending the initialization packet is

```
  string cipherPublicKey = request.ReadString();
  BigInteger sharedKey = HabboEncryptionHandlerV2.CalculateDiffieHellmanSharedKey(cipherPublicKey);
  if (sharedKey != 0)
  {
    // do your stuff with the shared key
  }
  else
  {
    // throw a error
  }
  
  // Initialize a new response
  response.WriteString(HabboEncryptionHandlerV2.GetRsaDiffieHellmanPublicKey());
```
