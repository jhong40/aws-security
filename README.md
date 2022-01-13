# aws-security

```
####### Encrypt / Decrypt
cat plain-text.txt
Hello World
aws kms encrypt --key-id 1234abcd-12ab-34cd-56ef-1234567890ab --plaintext fileb://plain-text.txt
aws kms decrypt --ciphertext-blob <value>

####### Sign / Verify
aws kms sign --key-id "64bcd1b9-0b2f-4924-89f1-91dfb000c6c6" --message fileb://demo.txt --signing-algorithm RSASSA_PKCS1_V1_5_SHA_256 --query Signature --output text | base64 -d > sign.txt
 
aws kms verify --key-id "64bcd1b9-0b2f-4924-89f1-91dfb000c6c6" --message fileb://demo.txt --signature fileb://sign.txt --signing-algorithm RSASSA_PKCS1_V1_5_SHA_256

```
