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
First let's log back on the server, with...
```
ssh [YOUR USERNAME]@[YOUR SERVER IP HERE]
```
Now, let's force users to use the SSH keys by disabling password based authentication, by running...
```
sudo nano /etc/ssh/sshd_config
```
...and edit the line that says `PasswordAuthentication yes` to `PasswordAuthentication no`. Now let's restart SSH with...
```
sudo systemctl reload sshd
```

## Step 5 - Firewall time!
To set up a firewall, run the following commands.
```
sudo ufw allow OpenSSH
sudo ufw enable
```

## Step 6 - NGINX.
To install NGINX run these commands:
```
sudo apt-get update
sudo apt-get install nginx
```
Now let's add NGINX to the firewall whitelist by running...
```
sudo ufw allow 'Nginx HTTP'
```
You should see a welcome page if you go to `http://[YOUR SERVER IP]`.

## Step 7 - It's *MY* SQL
First, install MySQL with...
```
sudo apt-get install mysql-server
```
...and secure your installation with...
```
sudo mysql_secure_installation
```

## Step 8 - Get PHP
It's easy to get with:
```
sudo apt-get install php-fpm php-mysql
```
Let's make it more secure with running...
```
sudo nano /etc/php/7.0/fpm/php.ini
```
...and finding the line with `;cgi.fix_pathinfo=1` and change it to `cgi.fix_pathinfo=0`. Finally, we restart PHP with
```
sudo systemctl restart php7.0-fpm
```

## Step 9 - You're done!
For every NGINX server block you want to use PHP on you have to add the following code.
```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php7.0-fpm.sock;
}
```

# License
[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)
The entirety of this README file is licensed under the Creative Commons Attribution-ShareAlike 4.0 International.
