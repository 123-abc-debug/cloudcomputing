1.Get the following files from your lecturer: 

![8598aca93299843b6b91f38ab586f1a1](C:\Users\21534\Desktop\Lab02.assets\8598aca93299843b6b91f38ab586f1a1.png)

(1) This is the personal digital certificate (also known as client certificate or user certificate) issued to you

It is a digital certificate of the public key issued to you, used to prove your identity.

Contains information such as your name, certificate authority (CA), expiration date, public key, etc.

In HTTPS or encrypted communication, servers or clients use it for authentication.

(2) yinyuang.key 

The private key is absolutely confidential and cannot be disclosed.

-Collaborate with '. ctrt' for encrypted communication (such as decrypting messages sent by clients)
-Digital signature (proving that the message is from you personally)

(3)ca.crt  

This is the root certificate of * * Certificate Authority (CA) * *. CA is a globally recognized authority (such as Let's Encrypt, DigiCert) or a self built authority within your organization.

This is a certificate issued by a Certificate Authority (CA).

Used to verify the trustworthiness of your certificate, that is, to confirm whether 'your name. ctrt' is issued by a trusted CA.

It can also be used to establish a trust chain to ensure the reliability of the identities of both parties in communication.

2.Make your own configuration file and change it to fit myself

![45c2876d4882d5c8429658eee90cc3be](D:\xwechat_files\wxid_me1xs1y80ngw12_ddf8\temp\RWTemp\2025-09\9e20f478899dc29eb19741386f9343c8\45c2876d4882d5c8429658eee90cc3be.png)

3.Run nebula and check the connectivity between your computer and the light house.

![image-20250916164325154](C:\Users\21534\Desktop\Lab02.assets\image-20250916164325154.png)

4.Ping 192.168.100.1 from another terminal

![image-20250916164418266](C:\Users\21534\Desktop\Lab02.assets\image-20250916164418266.png)

5.Use ssh to log in

![image-20250916165008190](C:\Users\21534\Desktop\Lab02.assets\image-20250916165008190.png)



