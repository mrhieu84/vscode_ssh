link https://tech.nhdesign.app/article/detail/2510600042205185

## Check if SSH is Installed on Ubuntu

To check if SSH is already installed, run:

```bash
sudo systemctl status ssh
```

If it's not installed, run the following commands:

```bash
sudo apt update
sudo apt install openssh-server -y
```

By default, the `.ssh` directory is located in the home folder of user:

```bash
/home/ubuntu/.ssh/
```

## Create a Private and Public Key Pair on the Ubuntu Server

Run the following command to generate a private and public key pair:

```bash
ubuntu@127.0.0.1:~$ ssh-keygen -t rsa -b 4096 -C "myname"
```

You will be prompted to enter the location where the key pair should be saved:

```bash
Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa): /home/ubuntu/sshkey
```

You can also set a passphrase for the key. If you prefer not to use a passphrase, leave it empty and press Enter.

Once the key pair is generated, you'll see output similar to the following:

```
Your identification has been saved in /home/ubuntu/sshkey
Your public key has been saved in /home/ubuntu/sshkey.pub
```

## Append Public Key to `authorized_keys`

Now append the public key to the `authorized_keys` file:

```bash
ubuntu@127.0.0.1:~$ cat sshkey.pub >> ~/.ssh/authorized_keys
```

## Download the Private Key and Use it to Connect from Clients

Download the private key (`sshkey`) to your local machine and use it to connect to the Ubuntu server from any client.

### On Windows CMD

To connect from a Windows CMD, use the following command:

```bash
ssh -i sshkey user@server_ip
```

### In VSCode

1. Install the **SFTP** extension in VSCode.
   
   ![SFTP Extension](/forum/image/20250416091333048_53.png)

2. Create a `.vscode` folder in your project directory.

3. Inside `.vscode`, create an `sftp.json` configuration file with the following content:

```json
{
  "name": "Ubuntu Server",
  "host": "Server IP",
  "protocol": "sftp",
  "port": 22,
  "username": "ubuntu",
  "remotePath": "/odoo",
  "uploadOnSave": false,
  "useTempFile": false,
  "openSsh": true,
  "privateKeyPath": ".vscode/sshkey",
  "passphrase": "password of privateKey"
}
```

4. Adjust the `remotePath` to match your server's directory.

5. Now, go to the **SFTP** tab and click **Open SSH**.

   ![Open SSH](/forum/image/20250416092606669_43.png)

6. After entering the password for the private key, you will be connected to the server.

   ![Connected to Server](/forum/image/20250416092923555_44.png)

## Synchronize Files Between Server and Client

You can now synchronize files between the server and the client using the **Download/Upload** functionality:

### Download a File

Click the **Download** button to download the file from the server. You will see the file downloaded to your local client.


![image.png](/forum/image/20250416094706874_33.png)

 

### Upload a File

  ![Download File](/forum/image/20250416093201940_25.png)
  
Click the **Upload** button to upload a file from your client to the server.

   ![Upload File](/forum/image/20250416093239971_52.png)
