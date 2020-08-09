## SSH Keys

Follow these instructions to create or add SSH keys on Linux, MacOS & Windows. Windows users without OpenSSH [can install and use PuTTY](https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys/create-with-putty/) instead.

### Create a new key pair, if needed

Open a terminal and run the following command:

```
ssh-keygen
```

​         Copy    

You will be prompted to save and name the key.

​      Generating public/private rsa key pair. Enter file in which to save the key (/Users/USER/.ssh/id_rsa):    

Next you will be asked to create and confirm a passphrase for the key (highly recommended):

​      Enter passphrase (empty for no passphrase): 
Enter same passphrase again:     

This will generate two files, by default called `id_rsa` and `id_rsa.pub`. Next, add this public key.

### Add the public key

Copy and paste the contents of the **.pub**.pub file, typically id_rsa.pub, into the **SSH key content** field on the left.

```
cat ~/.ssh/id_rsa.pub
```

​         Copy    

For more detailed guidance, see [How to Add SSH Keys to Droplets](https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys/)