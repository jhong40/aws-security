# aws-security

```
cat plain-text.txt
Hello World

aws kms encrypt --key-id 1234abcd-12ab-34cd-56ef-1234567890ab --plaintext fileb://plain-text.txt
aws kms decrypt --ciphertext-blob <value>
```
