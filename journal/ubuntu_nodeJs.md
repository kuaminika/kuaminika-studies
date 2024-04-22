# How I had to resinstall NodeJS

So basically I decided to re-install node, because I tried updating its version with nvm. I made sure that nvm set the latest version of node, and when I did a _node -v_ the version would not match.

## Uninstall node

to uninstall node , it can be done with the following :

```bash
sudo apt-get remove nodejs
```

then you'd have to remove the configurations.

```bash
sudo apt-get purge nodejs
```

then the following will remove some remaining files

```bash
sudo apt-get autoremove
```

## To Install node

### Installing the primer

So apparently, we need to install the primer.. its called the PPA.Its installed in 2 commands.

The first command:

```bash
    sudo apt-get install software-properties-common
```

 The second command:  

```bash
    curl -sL https://deb.nodesource.com/setup_20.x | sudo -E bash -
```

### The installation

the following command

```bash
sudo apt-get install nodejs
```

## Still having issues

I noticed that node was still inatalled despite doing all of these commands.
I ran the following command to see why node still exists:

```bash
 find / -name "node*"
```

I saw that I got the following as a result:

```cmd
/home/linuxbrew/.linuxbrew/opt/node@16
/home/linuxbrew/.linuxbrew/opt/node.js
/home/linuxbrew/.linuxbrew/opt/nodejs
```

## Homebrew installed

So, it turns out I had homebrew installed. I will proceed  to uninstalling it. I used the following command :

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
```

I also noticed that homebrew had overwritten my commands

example:

doing a node -v yielded the following:

```shell
-bash: /home/linuxbrew/.linuxbrew/bin/node: No such file or directory
```

I did the following command to resolve things

```shell
PATH=$(getconf PATH)
```

## Sources

[To deal with homebrew command overwrites](https://askubuntu.com/questions/113419/how-can-i-reset-path-to-its-default-value-in-ubuntu)

[Digital-ocean article about node install](https://www.digitalocean.com/community/tutorials/install-uninstall-nodejs-ubuntu)

[To uninstall homebrew](https://github.com/homebrew/install#uninstall-homebrew)
