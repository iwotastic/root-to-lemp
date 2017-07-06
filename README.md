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

## Step 3 - Switch to Sudo
Let's leave the land of root by typing the following command.
```
exit
```

