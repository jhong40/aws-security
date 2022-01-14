# aws-security
## KMS
```
####### Encrypt / Decrypt
cat plain-text.txt
Hello World
aws kms encrypt --key-id 1234abcd-12ab-34cd-56ef-1234567890ab --plaintext fileb://plain-text.txt
aws kms decrypt --ciphertext-blob <value>

aws kms encrypt --key-id 68e86af6-0db6-4fd1-8c17-fb8a20c766cd --plaintext "Hey" --output text --query CiphertextBlob | base64 --decode > ExampleEncryptedFile
aws kms decrypt --ciphertext-blob fileb://ExampleEncryptedFile --output text --query Plaintext > DecryptedPlainText

####### Sign / Verify
aws kms sign --key-id "64bcd1b9-0b2f-4924-89f1-91dfb000c6c6" --message fileb://demo.txt --signing-algorithm RSASSA_PKCS1_V1_5_SHA_256 --query Signature --output text | base64 -d > sign.txt
aws kms verify --key-id "64bcd1b9-0b2f-4924-89f1-91dfb000c6c6" --message fileb://demo.txt --signature fileb://sign.txt --signing-algorithm RSASSA_PKCS1_V1_5_SHA_256


###### Grant
1. Generating the Grant
aws kms create-grant /
--key-id [KEY-ID] /
--grantee-principal [GRANTE-PRINCIPLE-ARN] /
--operations "Encrypt"
2. Using Grant to Perform Operation
aws kms encrypt --plaintext "hello world" 
--key-id [KEY-ID] /
--grant-tokens [GRANT TOKEN RECEIVED] 
3. Revoking the Grant
aws kms revoke-grant --key-id [KEY-ID] --grant-id [GRANT-ID-HERE]


##### ViaService
{
	"Id": "key-consolepolicy-3",
	"Version": "2012-10-17",
	"Statement": [{
			"Sid": "Enable IAM User Permissions",
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::888913816489:root"
			},
			"Action": "kms:*",
			"Resource": "*"
		},
		{
			"Sid": "Allow use of the key",
			"Effect": "Deny",
			"Principal": {
				"AWS": "arn:aws:iam::888913816489:user/Alice"
			},
			"Action": [
				"kms:Encrypt"
			],
			"Resource": "*",
      "Condition": {
        "ForAnyValue:StringEquals": {
          "kms:ViaService": [
            "ec2.us-east-1.amazonaws.com"
         ]
      }
       }
		}
	]
}


#### Encryption Context
aws kms encrypt --key-id 13301e8a-7f95-4c00-bd73-6d0a20b03918 --plaintext fileb://file.txt --output text --query CiphertextBlob --encryption-context mykey=myvalue | base64 --decode > ExampleEncryptedFile
aws kms decrypt --ciphertext-blob fileb://ExampleEncryptedFile --output text --query Plaintext --encryption-context mykey=myvalue | base64 -d


```
