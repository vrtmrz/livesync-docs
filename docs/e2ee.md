# End-to-end encryption

If we want to use the server, that served as SaaS or as a tenant, we think we would love to keep the document secure more than in the case of using a dedicated server. 
Therefore, we can use end-to-end-encryption, to mitigate this risk of the accidents when somebody can see the disk or network intercommunication.

You can enable `End to End Encryption` after you set `Passphrase`. Then, all content of the remote database will be encrypted automatically while in replication.
**Be careful, filenames and metadata will not be encrypted**.

The encryption algorithm is AES-GCM.

**If you noticed the failure of the algorithm, please inform me!**

## How to change the passphrase?

We must rebuild the remote database.

![[Pasted image 20220727153441.png]]