# Root to LEMP
*A command-by-command guide to go from a new Ubuntu 16.04 server to a full LEMP stack*

## Step 1 - Connect
First, connect to your new server over SSH.
```
ssh root@[YOUR SERVER IP HERE]
```

## Step 2 - We Don't Need no Stinkin' Root
First, create a new user by running...
```
adduser [YOUR USERNAME]
```
...and answering all the prompts. Now, give yourself superuser privlages with the following command.
```
usermod -aG sudo [YOUR USERNAME]
```

## Step 3 - Passwords!? Where We're Going We Don't Need Passwords.
Let's leave the server by typing the following command.
```
exit
```
Now run the following command to generate a SSH key pair.
```
ssh-keygen
```
The output should be the following.
```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/you/.ssh/id_rsa):
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
```
Now, copy it to your server with...
```
ssh-copy-id [YOUR USERNAME]@[YOUR SERVER IP HERE]
```

## Step 4 - Make it Secure
Now, let's force users to use the SSH keys by disabling password based authentication.

# License
[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)
The entirety of this README file is licensed under
