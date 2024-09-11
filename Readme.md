**Description**
--


This project is used to provision three ece instances with help of ansible and to ssh into them automatically. Once the above steps are successfull we have to shutdown all the instances.

**Step1**
Do ssh-keygen to generate the the public key from root folder. This should generate .ssh/id_rsa.pub file
```ssh-keygen```

**Step2**
Create a IAM role in AWS and attach AmazonEc2_fullAccess policy.After that download the key pair in root folder.Here i have named it as bhargav-dummy-aws-key-pair.pem

**Step3**
Create a [filename].enc file to put your aws_access_key and aws_secret_key. Once yo add your access and secrets key,run the below command.
```ansible-vault encrypt [filename].enc```
Type the password you want to encrypt

**Step5**
Once all the steps are done run the below command from root folder
``` ansible-playbook -i inventory.ini -e @[filename].enc --ask-vault-pass ~/ansible-project/main.yml --private-key bhargav-dummy-aws-key-pair.pem```

Here inventory.ini is a list of hosts.Although we dont have any hosts.Its a good practice to mention them.You will get a 
propmt for the password because of --ask-vault-pass.Please enter the same password while you did for encryption. The
--private-key option is needed for mention your aws-key-pair which is required for authorized key tasks.





