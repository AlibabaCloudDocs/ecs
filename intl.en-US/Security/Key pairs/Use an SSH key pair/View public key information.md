# View public key information

This topic describes three ways to view public key information. If you want to configure the same public key file for a group of ECS instances but the public key file has no backups in your PC, you can view public key information by using the following methods.

## Windows

To view public key information, perform the following operations:

1.  Start PuTTYgen.

2.  Click **Load**.

3.  Select the .ppk or .pem file.

    PuTTYgen then displays the public key information.


## Linux or macOS

Run the ssh-keygen command with the path of the .pem file specified.

```
ssh-keygen -y -f /path_to_key_pair/my-key-pair.pem
```

The following example shows the returned public key information:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABA****+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIPxxxxxxxxxx/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcxxxxxxxxxxx/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjxxxxxxxxxx+lHtTGiAIRG1riyNRVC47ZEVCxxxxxx
```

**Note:** If the command fails, run the `chmod 400 my-key-pair.pem` command to modify the permissions to ensure that only you can view the file.

## View the public key information in the instance

The public key information is in the ~/.ssh/authorized\_keys file. Open the file in the instance to view the public key information.

