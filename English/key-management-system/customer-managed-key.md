# Customer Managed Key

### Create a new customer-managed key.

* In the KMS portal, select the "Customer keys" menu to access the list of customer-managed keys.
* Choose "Create Key" and follow the on-screen instructions to create the key:
* Enter key information including: Key Name, Description, Tags.
* Enter key configuration details including: Key Type, Key Usage, and Key Spec.
* Key Material Origin: Users select the Origin = VNGCLOUD.

&#x20;   \-        VNGCLOUD: Key material created on VNG Cloud KMS.

&#x20;   \-        External: Users manage the Key Material yourselves and import it into VNG Cloud KMS for use in VNG Cloud services.

* Click "Create Key" to create the key.

&#x20;   \-   For keys with key material source = VNGCLOUD, upon successful creation, the key status will be "Active"

&#x20;   \-   For keys with key material source = External, upon successful creation, the key status will be "Pending Import" The next step is to follow the instructions in the section "Wait for Key Material Import."

### View the list of keys and key details

* Go to the "Customer keys" menu to see the list of keys created by the user.
* Go to the "VNG Cloud Keys" menu to view the list of keys created by VNG Cloud at the user's request.
* To view detailed information about a key, users should find and navigate to the row containing the key information they want to view, and then click on the hyperlink at the key name.

### Delete Key

Users can only delete keys of the type "Customer Managed Key."

* Go to the "Customer keys" menu, find and select the key you want to delete. Click "Delete key"
* KMS will notify you of the implications of deleting the key. Users need to enter a waiting period to delete the key, which can range from 7 to 30 days.
* Click "Delete"
* The key will change to the status "Pending Deletion" The key will be removed from the system after the waiting period expires. If changing your mind, you can use the "Cancel Deletion" function.

Cancel deletion

### For keys that are in the pending deletion stage, you can change your decision by using the "Cancel Key Deletion" function.

* Go to the "Customer keys" menu, find and select the key with the status "Pending Deletion"
* Click "Cancel Deletion"
* The key will then change to the status "Disable" Users can revert it to "Active" to use the key again by using the "Enable" key function.

### Enable Key

Applicable to cases where Disable keys need to be used.

* Go to the "Customer keys" menu, find and select the key with the status "Disable"
* Click on the hyperlink at the key name.
* Click the "Enable" button to change the key status to "Active"

If there are no active key packages, users cannot enable a key that is in the "Disable" status.

### Import Key Material

VNG Cloud KMS supports importing key material for two types of keys:

* Symmetric Key
* Asymmetric Key

To import a key, users should follow these steps:

1. Log in to the VNG Cloud console at the provided link.
2. Select the “Customer Keys” menu.
3. Choose the Key ID from which you want to download the Public Key and Import Token. If the Master Key has not been created yet, users can refer to the guide on creating a master key.
4. Select the “Encryption Configuration” tab to view detailed information about the key and ensure that the key's origin (Origin) is set to External, which indicates the keys that can have Key Material imported.
5. Select the “Key Material” tab to view detailed information about the Key Material. Click on “Import Key Materials.”
6. If users want to download the Wrapping Public Key and Import Token (Step 1 of the key import process), follow these steps:

* Choose the wrapping key specification (Wrapping Key Spec).
* Choose the wrapping algorithm (Wrapping Algorithm).
* Click on “Download Wrapping Public Key and Import Token.”

7. Upload the key content to KMS (Step 2 of the key import process):

* In the “Wrapped Key Material” section, select the file containing the encrypted key material to upload. To create and wrap Key Material, follow the instructions in the “Create and Wrap Key Content” section.
* In the “Import Token” section, select the import token file to upload.
* If you want to set an expiration date for the Key Material, check “Expiration” and fill in the expiration date information. Skip this step if you do not want to set an expiration date for the imported key content.

8. Click “Submit” to complete the import process.

### Instructions for Creating and Wrapping Key Content:

#### Symmetric Key

Step 1: Generate a 32-byte AES symmetric encryption key.

```
openssl rand -out PlaintextKeyMaterial.bin
```

 Step 2: Use the wrapping public key to encrypt the key content (Key Material).

2.1 RSAES-OAEP-SHA-256&#x20;

```
openssl pkeyutl -encrypt -inkey WrappingPublicKey.pem -pubin -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha256 -in PlaintextKeyMaterial.bin -out EncryptedKeyMaterial.bin 
```

 2.2 RSA\_AES\_KEY\_WRAP\_SHA\_1:&#x20;

```
openssl pkeyutl -encrypt -inkey WrappingPublicKey.pem -pubin -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha1 -in PlaintextKeyMaterial.bin -out EncryptedKeyMaterial.bin
```

#### &#x20;Asymmetric Key

Step 1: Generate a random 32 bytes AES key

```
openssl rand -out aes_key.bin 32
```

&#x20;Step 2: Create your own private key.

```
openssl genpkey -algorithm RSA -out my_private_key.pem -pkeyopt rsa_keygen_bits:4096
```

&#x20;Step 3: Encrypt the AES key with the RSA public key.

3.1 Wrapping algorithm: RSA-AES-KEY-WRAP-SHA-256&#x20;

&#x20;// Some code

```
openssl pkeyutl -encrypt -inkey WrappingPublicKey.pem -pubin -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha256 -in aes_key.bin -out aes_key_wrapped.bin
```

&#x20;3.2 Wrapping algorithm: RSA-AES-KEY-WRAP-SHA-1&#x20;

```
openssl pkeyutl -encrypt -inkey WrappingPublicKey.pem -pubin -pkeyopt rsa_padding_mode:oaep -pkeyopt rsa_oaep_md:sha1 -in aes_key.bin -out aes_key_wrapped.bin
```

&#x20;Step 4: Encrypt the private key with the AES key.

```
openssl enc -aes-256-cbc -salt -in my_private_key.pem -out my_private_key_wrapped.bin -pass file:aes_key.bin -pbkdf2 -iter 10
```

&#x20;Step 5: Combine the encrypted files together

```
cat aes_key_wrapped.bin my_private_key_wrapped.bin > EncryptedKeyMaterial.bin
```

&#x20;
